# Phasor Components
[emdata][1] makes use of two phasor component representations, as used by [Harrington][2], [Hayt and Buck][3], and others.

All time-harmonic signals are phasors. All phasor components used by emdata must be unambiguous. These are specified in the `phasorComponent` key of a [column object][6].

## Amplitude and Phase
A phasor quantity, *Z*, may be represented by its amplitude (or magnitude), *A*, and phase, *φ*, as follows:

*Z* = *Ae<sup>jφ</sup>* or *Z* = *A*&ang;*φ*

Where *e* is [Euler's number][4] and *j* is the [imaginary unit][5].

These are referenced in the emdata file as:
* `"phasorComponent": "amplitude"` (or `"magnitude"`)
* `"phasorComponent": "phase"`

## Real and Imaginary
A phasor quantity, *Z*, may be represented by its real, *R*, and imaginary, *X*, parts as follows:

*Z* = *R* + *jX*

Where *j* is the [imaginary unit][5].

These are referenced in the emdata file as:
* `"phasorComponent": "real"`
* `"phasorComponent": "imaginary"`

Both of these components *should* have the same units. It is not strictly necessary, but it precludes confusion and headaches.

## Other Considerations
### RMS Amplitude
Do not use RMS amplitude for data interchange. The RMS amplitude is not a first-class property of the signal, and using it results in a high probability of confusion and misunderstanding.


[1]:https://github.com/finitemobius/emdata
[2]:https://www.amazon.com/Time-Harmonic-Electromagnetic-Fields-Roger-Harrington/dp/047120806X
[3]:https://www.amazon.com/Engineering-Electromagnetics-William-Hayt/dp/0073380660
[4]:https://en.wikipedia.org/wiki/E_(mathematical_constant)
[5]:https://en.wikipedia.org/wiki/Imaginary_unit
[6]:object_schema.md#column-object