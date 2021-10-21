## Sub-patches, more instrument effects
- adding complexity to a patch can be done in segments
- manipulating a signal over time to create changes in sound
    - help to declutter the environment and focus on different parts at a time

### sub-patches
- sub-patches are created with the 'pd' object
    - provide an argument to the object to title the patch
    - i.e. 'pd sound-maker-5000'
- when creating the object, a new window is made, showing the contents of the sub-patch
- to interact with the sub-patch from your primary patch, add inlets and outlets to the sub-patch window
    - 'inlet' objects are used to receive parameters from the main patch
    - 'outlet' objects are used to send data from the sub-patch
    - adding a '~' after the name of either of these will allow you to pass audio
        - for audio, it's typical to avoid creating a 'dac~' inside of your sub-patch
        - this way, all of your audio control is done in the primary patch
    - as you add these items to your sub-patch, you'll see the 'pd ...' object aquire inlets that can be used in the main patch
        - these are added in order from left to right
    - connect these to begin interactions with your sub-patch

## incorporating previous instruments as sub-patches
- from previous sessions, we created a noise patch [here](../session_2/)
- download this patch and open it using Pure Data
- open a new patch window, and add an object
    - `pd noise-drum`
    - once you've added, it will open a sub-patch window
    - this window is where you'll define how this new object behaves
- open the noise patch and click, drag, copy, and paste all of its contents to the new subpatch window
    - add 'inlets' for the parameters you want to manipulate
    - remove the `dac~` objects and add a single `outlet~` for the audio signals in the patch
    - you should now see that your sub-patch object in the blank patch window should have markers indicating inputs/outputs
    - save the changes to the file
- for the noise patch, I added 3 'inlet' objects and connected them to the bang, the multiplier number for the filter, and the right inlet for the delay object, respectively. I added one `outlet~` for the audio output to replace the `dac~`
- when you save the blank patch window (the primary window), your sub-patch will save along with it

### time-based effects
#### [delays](https://en.wikipedia.org/wiki/Delay_(audio_effect))
- anywhere from short time to long time, typically longer time frame (order of milliseconds)
- the 'copy' of the signal starting at some time (buffer) is continuously behind by some other time (the delay)
- we use a [delay line](https://en.wikipedia.org/wiki/Digital_delay_line) to achieve this
- we can get the signal to delay multiple times over by re-introducing the delayed copy into the input of the delay ... again
    - feedback
- in pd
    - `delwrite~`, `delread~`
