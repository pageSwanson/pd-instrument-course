## Sampling
- [sampling](https://en.wikipedia.org/wiki/Sampling_%28signal_processing%29) is the practice of extracting portions of an audio signal for re-use
- typically today we do this in real-time and immediately recall the portion of audio for playback
- the portions of audio are made up of 'samples' which represent instantaneous points in the audio signal
- a sample is just a value for the amplitude of the audio signal at some point in time (sample rate)
- we can be capture samples very frequently for a better picture of the frequency content of the audio we're working with
- we can adjust the resolution of the sample by representing the samples with a large range of values (bit resolution)

### audio sampling in pure data

#### recording audio
- the `adc~` object in pure data records audio using the microphone device on your computer
    - make sure this is configured - check 'Media > Audio Settings...' in the top ribbon

#### creating a table
- using a `tabwrite~ <table-name>` object (introduced in past sessions for previewing signals)
- you'll need an Array with a name matching what you used for tabwrite
    - in the properties window, remember the size of the array you specify
    - this demonstration uses a size of 44,100 values
        - chosen based on your 'Media > Audio Settings... > '
    - this corresponds to 1 second of a signal recorded at a sample rate of 44,100 Hz (really, samples per second) (we'll get to that)
- capture audio over a limited period of time and store it
- trigger the table write with a 'start' and 'stop' message
    - 'start' and 'stop' are special signals for the `tabwrite~` object
    - send a bang to the start message so that writing begins
    - send a delayed bang so that we stop sampling after a certain period (the table stops updating)
- connect the 'adc' to the inlet on the 'tabwrite' object

#### reading from the table
- using `tabread~ <table-name>` for recalling stored audio signal
- for controlling the read operation, use a `vline` function
    - the idea here is to create a continuous, linear function, like a ramp
    - starting at the first sample in the table, concluding at the last
    - reading each value sequentially over the course of 1 second
    - `vline~` with a message box input '0, 44100 1000'
        - starting position, ending position duration
- we'll play all 44,100 samples over the course of 1 second this way
- you can now click to recall the sample
