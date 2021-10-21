## automating changes in our instruments
- this session will introduce programmatic techniques for automating a patch
- we'll also use abstractions to incorporate previous instruments we've made to create new systems

## User (Player) Interaction
- instruments often have meaningful methods of interaction
- allows users can suggest changes to sound in a learned manner
- actions can be repeated and behaviors can be reproduced
    - means for sharing and playing songs

### controls
- Pure data has some built-in controller objects
- these can be used to update parameters with gestures
- all are accessible from the 'Put' dropdown at the top ribbon

#### the bang
- very familiar with this one - sends a bang when clicked, behaves like a button - sends once per click

#### the toggle
- we've seen the toggle previously - this continuously sends a 'bang' when enabled, and stops when disabled

#### the radio
- a radio control lets us select an output based on a graphical interface with boxes

#### the slider
- this control lets us smoothly select from a range of values with the mouse or another user gesture

### control properties
- connect a number box or a bang to the outlet of these controls to observe their behavior
- these can provide more intuitive control for instruments you create
- all of the above controls have a properties option when right-clicking - choose this to label your control, change the color, or adjust the limits available on the control

## Sequencing
- a [sequencer](https://en.wikipedia.org/wiki/Music_sequencer) is a tool that allows users to store and recall repeating patterns and information about events like notes or rhythms
- typically, sequencers keep information in the form of 'steps', where each step maintains properties that are recalled as that step is reached
- the sequence proceeds with the use of a time-keeping system like a clock at some rate (usually given as bpm)

### creating a sequencer
- we can create a sequencer algorithmically, rather than storing discrete information
    - the patterns will be stored as a procedure, which can be evaluated to produce each step
- the sequence can proceed with the use of the 'metro' object
    - the metro repeatedly sends bangs after every n milliseconds
    - adding an accumulator means we can track how many ticks have passed so far
- pitch data (oscillator frequency) will be determined using the value of the accumulator at different times
- using the [modulo operator](https://en.wikipedia.org/wiki/Modulo_operation) ('mod' in pure data) we can select on specific updates rather than responding to every tick
    - we can determine which beat we want to trigger a sound
    - we can select which beat we want to change the pitch
    - a combination gives us rhythms

#### the clock
- we previously used metro to update a visualization
    - provided a 'bang' at regular intervals to update the display of a waveform
    - now - we'll use it to advance our sequence of events - triggering frequency changes and other sounds
- passing an integer argument for the metro like 'metro 1000' sets the metronome to update every 1000 ms (1 second)
- adding an accumulator keeps track of how many times it's updated
    - send the output of the metro to the left inlet of a '+ 1' object
    - send the output of that addition to a number box
    - send the output of the number box _back_ to the addition at the right inlet (cold inlet)
    - initialize the system by sending a message box '1' to the addition at the left-inlet - this starts the accumulator at '1'

#### step events (beats)
- the 'mod' object
    - takes an integer at the left inlet, and another at the right inlet
    - performs integer division and outputs the remainder
    - 6 mod 2 gives 0, 7 mod 2 gives 1
- the '==' object
    - takes an integer at the left inlet, and another at the right inlet
    - if the left is equal to the right (or is equal to a set argument) then the output is 1; otherwise, 0
- the 'spigot' object
    - takes a bang at the left inlet and a message at the right inlet
    - it passes the message to the output when it sees a bang at the left inlet
- a network of the above objects will allow us to trigger steps conditionally
    - accumulator -> mod -> == -> spigot
    - this network produces a bang and a number for every time the remainder of the 'mod' operation equals a value we specify

#### pitch control
- we want to change pitches on a beat
- in this session, the accumulator and the 'mod' object are used to generate a number that moves from 0 to 1 and back again at varying rates, synchronized with the clock
- the result is used to make a midi note number (there are 127 possible [midi notes](https://www.inspiredacoustics.com/en/MIDI_note_numbers_and_center_frequencies)) with the 'mtof' object
    - (from 0 to 1) \* 127 -> (0 - 127) -> mtof -> a frequency
- once we have a frequency, we can send that information to control an oscillator
- in order to control how frequently the pitch value changes, we can use a 'spigot' again
    - passing the frequency value to the right inlet
    - pass the output from a step event controller to the left inlet
    - the output is a frequency value that only updates on the beat
