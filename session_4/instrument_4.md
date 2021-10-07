## Instrument audio effects

### waveform effects
#### [clipping](https://en.wikipedia.org/wiki/Clipping_(audio))
- waveform is amplified
- but it's also forced to a threshold beyond which the signal is 'maxed-out'
- a signal moving from 0 and back to 0 again over the following course...
    - 0 -> .4 -> .7 -> 1.5 -> 3 -> 1.5 -> etc
- becomes the following when clipped at a threshold of 1
    - 0 -> .4 -> .7 -> 1 -> 1 -> 1 -> .7 -> etc
- in pd
    - `clip~`

#### [wavefolding or rectifiers](https://en.wikipedia.org/wiki/Rectifier)
- waveform is amplified
- like clipping, but when the threshold is reached, the wave form peak overlaps with itself
- the wave will no longer dip below zero, but instead will peak back up
- in pd
    - `abs~`

### time-based effects
#### [delays](https://en.wikipedia.org/wiki/Delay_(audio_effect))
- anywhere from short time to long time, typically longer time frame
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
- same idea as the feedback path for delay, but the purpose is to 'cancel' specific frequencies - not to reproduce the signal 'verbatim'
- in pd
    - `lop\~`, `hip\~`, `vcf\~`
