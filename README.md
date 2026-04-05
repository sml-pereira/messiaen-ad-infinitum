# Messiaen ad Infinitum

[![Demo video](https://vumbnail.com/1180267097.jpg)](https://vimeo.com/1180267097)

A generative music system built in [Pure Data](https://puredata.info/) that produces endless, evolving compositions inspired by Olivier Messiaen's aesthetic principles. The patch combines Markov-chain harmonic progressions, non-retrogradable rhythms, and modes of limited transposition into a three-voice generative texture — melody, chords, and bass — output as real-time MIDI.

## Compositional Techniques

The patch implements three core elements of Messiaen's compositional language:

**Non-retrogradable rhythms** — Rhythmic sequences that read identically forwards and backwards (palindromic durations). The bass voice, for instance, uses the prime-number sequence `7 11 13 17 13 11 7`, while the melody draws from `2 3 5 3 2 7 2 5 3 2 2 3`. These are shuffled and reversed at runtime to preserve their symmetric property while introducing variation.

**Modes of limited transposition** — The melodic material is drawn from Messiaen's 2nd Mode (the octatonic scale), segmented as `0 1 3 6 7 9`. This scale admits only a limited number of transpositions before repeating, creating the characteristic harmonic colour Messiaen favoured.

**Probabilistic harmonic progression** — A six-state Markov chain governs chord transitions. Each state (I–VI) has weighted probabilities for moving to the next harmony. State VI features a ten-tier probability distribution that introduces rare chromatic shifts, while the other states favour intervals of 2nds and 3rds at varying likelihoods.

## Architecture

```
messiaen_ad_infinitum.pd          Main patch (control + output)
├── Markov_Chords                 6-state harmonic Markov chain
│   └── States I–VI              Weighted transition probabilities
├── NRrhythm_Melody               Palindromic rhythm generator (melody)
├── NRrhythm_Chords               Palindromic rhythm generator (chords)
├── NRrhythm_Bass                 Palindromic rhythm generator (bass)
├── melody_notes                  Pitch selection from Mode 2
├── chords_notes                  5-voicing chord selector with modulation
└── bass_notes                    Binary bass-voice generator

octaver.pd                        Abstraction for octave transposition
```

The three voices share a modulation bus (`s modulation` / `r modulation`) that gradually shifts all pitch material, simulating Messiaen's approach to tonal drift across large formal spans.

## Requirements

- [Pure Data](https://puredata.info/downloads/pure-data) (Pd Vanilla ≥ 0.51 or Pd-l2ork / Purr Data)
- **cyclone** library (provides `counter`, `zl` objects, and extended `moses`)
- A MIDI output device (hardware synthesiser, virtual instrument, or software)

### Installing the cyclone library

In Pure Data, go to **Help → Find externals**, search for `cyclone`, and click **Install**.

## Getting Started

1. **Clone this repository**
   ```bash
   git clone https://github.com/<your-username>/messiaen-ad-infinitum.git
   cd messiaen-ad-infinitum
   ```

2. **Open the main patch**
   Launch Pure Data and open `patches/messiaen_ad_infinitum.pd`. Ensure `octaver.pd` is in the same directory (it is by default).

3. **Configure MIDI output**
   In Pure Data, go to **Media → MIDI Settings** and select your preferred MIDI output device.

4. **Play**
   Click the **Start** bang in the patch. The system will begin generating music immediately. Use the **Stop** bang to halt playback, and **Reset Modulation** to return the harmonic centre to its starting position.

## Musical Output

The patch produces a continuous three-voice texture:

- **Melody** — Upper voice drawn from Messiaen's 2nd Mode, centred around C5 (MIDI 72), with octave displacement via the `octaver` abstraction.
- **Chords** — Middle voice cycling through five pre-composed voicings (four notes each), selected by the Markov chain and subject to global modulation.
- **Bass** — Lower voice alternating between two two-note patterns, providing a sparse harmonic foundation.

All voices output standard MIDI note-on/note-off messages via `noteout`.

## Repository Structure

```
messiaen-ad-infinitum/
├── patches/
│   ├── messiaen_ad_infinitum.pd    Main generative patch
│   └── octaver.pd                  Octave transposition abstraction
├── README.md                       This file
├── LICENSE                         MIT licence
├── CHANGELOG.md                    Version history
└── .gitignore                      Git ignore rules
```

## Contributing

Contributions are welcome. If you extend the Markov chain, add new modes, or integrate additional Messiaen techniques (e.g., birdsong transcription, colour-sound associations), please open a pull request with a clear description of the changes.

## Licence

This project is licensed under the [MIT Licence](LICENSE).

## Acknowledgements

This project was developed as part of an Interactive Music course assignment at the University of Porto (FEUP). It draws directly on the compositional theory outlined in Olivier Messiaen's *Technique de mon langage musical* (1944).

## Author

**Samuel Pereira** — [sml.p@outlook.pt](mailto:sml.p@outlook.pt)
