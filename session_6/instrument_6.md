## continued time + frequency effects
- observe characteristics of filters using different sound sources

#### [filters](https://en.wikipedia.org/wiki/Digital_filter)
- can be implemented as a 'short-time' effect
- effect limits the presence of specific frequencies by mixing many recent copies of the signal into itself
- a feedback loop which cancels out certain frequency portions that we want to 'cutoff' at the output
- same idea as the feedback path for delay, but the purpose is to 'cancel' specific frequencies - not to reproduce the signal exactly as it came in
- in pd
    - `lop\~`, `hip\~`, `vcf\~`
