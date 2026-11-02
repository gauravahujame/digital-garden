---
title: Live coding music
tags:
  - seedling
  - music
  - programming
---

Live coding is performing music by writing and editing code in real time, usually with the code projected so the audience can watch it change. Instead of hiding the instrument, the code *is* the instrument.

## The tools

- **TidalCycles**: a Haskell-based pattern language. It popularized the compact "mini-notation" for rhythms.
- **Strudel**: a JavaScript port of Tidal's ideas that runs entirely in the browser at strudel.cc. No install needed.
- **Sonic Pi**: Ruby-flavoured and designed for teaching, though people perform with it too.
- **SuperCollider**: the audio engine behind Tidal and a full language in its own right.

## Mini-notation in five lines

Patterns describe one *cycle* (roughly one bar). Everything inside the quotes gets squeezed into that cycle:

```javascript
// four evenly spaced sounds per cycle
s("bd sd bd sd")

// [ ] subdivides a step; ~ is a rest
s("bd [~ bd] sd [bd bd]")

// a melody, using a sawtooth synth and a low-pass filter
note("c3 e3 g3 b3").s("sawtooth").lpf(800)

// stack layers on top of each other
stack(
  s("bd*4"),
  s("~ hh ~ hh"),
  note("<c2 a1 f1 g1>").s("square")
)
```

`<a b c>` picks one item per cycle, so the bassline above changes every bar. A few symbols give you a lot of rhythmic control, which makes the mini-notation a nice example of a [[tech/Deep modules|deep module]].

## Why it's interesting

- **Mistakes are part of the show.** Errors happen in public, and performers recover from them live.
- **Algorithmic thinking for music.** Functions like `.every(4, fast(2))` (double the speed every fourth cycle) express ideas that are tedious to program in a traditional sequencer.
- **Algorave culture.** People dancing to music made from code, with the code projected on the wall.

> [!todo] Seedling
> Next: try a pattern built on just-intonation ratios instead of equal temperament. See [[music/Why twelve notes]] for why they sound different.
