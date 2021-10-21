## configuring pure data for desktop
- go to [puredata.info](puredata.info)
    - click 'Pure Data' under featured downloads at the right
- run the downloaded installer
    - the default options should be appropriate
- when finished, it will prompt you to run
- Pd will ask if you want to make a patch folder - you can accept or decline
- note: on Windows, you may have to adjust the font size if it appears small
    - select the 'Edit' dropdown from the top ribbon, choose 'Font' and modify
- at the top, select 'File' and then 'New'
    - this will open a patch window
- select 'Media' from the top
    - select 'DSP on'
    - Go to 'Test Audio and MIDI'
        - turn down your volume!
        - select the test tones on the left
        - if this doesn't give you sound, go back and select 'Audio Settings'
        - change your output options and repeat until you can hear sound

## visualization
- tabwrite and arrays
    - allows us to visualize signals (waveforms) in a simple manner
    - plotting the periodic value over time
    - two 'dimensions' - time and amplitude

### creating the visualizer
- create an array using the 'Put' option from the top ribbon
    -  you'll be prompted to provide properties
        - we'll want a larger number than the default 100 to represent the signal value over a sufficient amount of time
        - this will allow us to continually update the values of the array with the output of our audio source
- create a 'tabwrite' object
    - this will allow us to update the contents of the array provided the content of our signal
    - create a bang to engage it
- create a 'metro' object
    - the 'tabwrite' refreshes the array when it sees a bang
    - but unless we consistently click the object, we won't get continuous updates
    - a 'metro' object (read : metronome) produces bangs at regular intervals
        - provide the interval in milliseconds as an argument i.e. 100
    - send the metro outlet to the tabwrite inlet (shared with the audio signal)
- use the bang to start the metro


## sound in puredata

### oscillating wave
- moving periodic value
    - periodic meaning that the same value recurs at some _frequency_
- draw your finger along a shape, when you are about to go backwards, instead go forwards but continue the curve of the shape...
- you are tracing the curve of a wave
    - doing so for a circle produces a [sine](https://en.wikipedia.org/wiki/Sine_wave) (or cosine, depnding where on the circle you start (phase))
- pd provides objects that produce convenient periodic functions (like a cosine)
    - add a tilde '~'
    - this means we'll produce a 'signal' or wave suitable for audio

### noise
- in pure data, this object provides evenly distributed random values
- values move regularly, and the frequencies present are audible
    - the values change quickly enough for us to hear
- the pd object `noise~` produces random frequencies present across a [normal distribution](https://en.wikipedia.org/wiki/Normal_distribution)

### envelopes
- using the line function, we can create a ramping value
    - we can use functions like this to control the amplitude of a signal
    - especially for percussive sounds, we can simulate strikes
- the 'line' function takes multiple arguments, but the timing is key
    - the first argument is the destination value (to what point is the ramp headed)
    - the second is the time taken for the value to move to that point
    - the third is the 'grain' - indicating how frequently the value will be updated until it reaches the point
- the line function arguments are tricky though - it will forget the second argument once you've triggered it a single time
    - solution? Provide a 'list' of arguments, which are sent every time
    - add a message box with two spaced arguments - the destination value and the ramp time
- finally - this is only helpful if we are satisfied with the new destination
    - if we want to restore the value, we have to send messages to the ramp in succession
    - first, sending where we want to start from
    - finally, the arguments for the ramp

### filtering
- a [filter](https://en.wikipedia.org/wiki/Filter_(signal_processing)) limits the frequencies present in a signal
    - this is realized by attenuating (reducing the gain) of recurring periodic values (frequencies) present in the signal
- in pd, a low pass filter object `lop~` is used to gain limit frequencies beyond the 'pass band'
    - the pass band represents the range of frequencies that will 'pass' through the filter with minimal attenuation
    - the limit of the band range is the 'cuttoff frequency', beyond which frequencies are attenuated
- in pd, the cutoff frequency is provided at the right-hand inlet
    - just like the `osc~` object, this is a float value with the 'Hz' unit

### message delays (bang ... bang!)
- the delay object receives a bang and transmits another following a delay
    - specify the delay at the second inlet, the first inlet with the bang, or as an argument
    - time in milliseconds
- in combination with the line function, can generate successive ramps
    - create complex variations with different ramp times

## simulating a drum
- we'll create a sound like a drum, and a way to trigger a [flam](https://en.wikipedia.org/wiki/Drum_rudiment#Flam)
- noise will be used as the source of the sound
- envelopes will allow us to articulate the volume over time
    - this way, the patch remains 'silent' until triggered
    - we can also use the envelope to change the character of the sound
- filters will let us modify the content of the noise
    - the sound will differ for the second strike
- finally, a delay will be used to produce strikes in succession
