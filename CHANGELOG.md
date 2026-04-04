# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.0.0] - 2024-08-06

### Added

- Main generative patch (`messiaen_ad_infinitum.pd`) with three-voice MIDI output.
- Six-state Markov chain for probabilistic harmonic progression (states I–VI).
- Non-retrograde rhythm generators for melody, chords, and bass voices.
- Melodic pitch selection based on Messiaen's 2nd Mode of Limited Transposition.
- Five pre-composed four-note chord voicings with stochastic re-selection.
- Global modulation bus for gradual harmonic drift across all voices.
- Octave transposition abstraction (`octaver.pd`).
- Start/stop and reset modulation controls.
