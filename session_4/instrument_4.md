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
