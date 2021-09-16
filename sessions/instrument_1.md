## to begin
- requirements
    - [desktop download](www.puredata.info)
    - [browser version](https://purrdata.glitch.me)
- what can pd do
    - [example patch](https://www.youtube.com/watch?v=V1E52x15RYU)
- how does it work
    - how do you 'program' with it
    - pd is graphical
    - pd is live

## basic modules / nodes / operators / functions
- numbers
    - respond to changing values, send a value
    - change the value by dragging
- message
    - keep a static value, change by editing
    - send the value you keep
- objects
    - 'blank' boxes, provide the name of a function
- bang
    - unique to pd, allows flow
    - bang is an object, but the behavior is not solely for the 'bang'
    - other objects can behave this way, too i.e. messages

## 'box properties'
- lines represent the flow of value
- boxes interrupt, interpret, receive
- 'hot' inlets are usually left-hand
    - performs the operation when it sees a bang, or change
- 'cold' inlets are usually on the right
    - keeps the value received but doesn't operate
- outlets
    - provide the result of functions or pass-through inputs
    - transmit changes or bangs
- boxes take 'arguments'
    - what sits inside the box before anything happens
    - details how it will behave
- modify behavior with the 'property' selector
    - right-clicking a box lets you adjust various properties

## the pd environment
- the help property
    - you can always right-click to view information about a box
    - you can see further help in the ribbon at the top
- pd will start with edit mode
- edit mode is for adding new things and moving things
- to control and modify items as you would outside of edit mode
    - hold cmd (mac) or ctrl (windows)

## producing sound
- oscillator
    - a moving value, fast enough to produce an audible sound
    - the '~' indicates an audio object
    - lines drawn will be bolder than data connections
- attenuator (multiply)
    - scale the volume and control the maximum value at a given time
- dac object
    - digital to audio converter
    - left and right channels

## combining concepts for an instrument

## at end
- we've synthesized
    - using a very basic 'additive' technique
    - we'll introduce more techniques
    - understand how objects make sound
- we can play this 'instrument'
    - we made a simple interface to do this
    - we'll learn more means of control
- because of the module scheme
    - we can extend and adapt it
    - we'll be able to connect our instruments
