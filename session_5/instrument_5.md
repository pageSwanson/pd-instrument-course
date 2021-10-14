## More instrument effects
- manipulating a signal over time to create changes in sound

### time-based effects
#### [delays](https://en.wikipedia.org/wiki/Delay_(audio_effect))
- anywhere from short time to long time, typically longer time frame (order of milliseconds)
- the 'copy' of the signal starting at some time (buffer) is continuously behind by some other time (the delay)
- we use a [delay line](https://en.wikipedia.org/wiki/Digital_delay_line) to achieve this
- we can get the signal to delay multiple times over by re-introducing the delayed copy into the input of the delay ... again
    - feedback
- in pd
    - `delwrite~`, `delread~`

#### [filters](https://en.wikipedia.org/wiki/Digital_filter)
- can be implemented as a 'short-time' effect
- effect limits the presence of specific frequencies by mixing many recent copies of the signal into itself
- a feedback loop which cancels out certain frequency portions that we want to 'cutoff' at the output
- same idea as the feedback path for delay, but the purpose is to 'cancel' specific frequencies - not to reproduce the signal exactly as it came in
- in pd
    - `lop\~`, `hip\~`, `vcf\~`
