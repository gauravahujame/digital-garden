---
title: Why twelve notes?
tags:
  - evergreen
  - music
  - math
---

Western music divides the octave into 12 notes. That number isn't arbitrary. It's the best small compromise between two ratios that don't fit together.

## Consonance is about simple ratios

Two notes sound consonant when their frequencies form a simple ratio:

| Interval | Ratio |
|---|---|
| Octave | $2:1$ |
| Perfect fifth | $3:2$ |
| Perfect fourth | $4:3$ |
| Major third | $5:4$ |

The octave and the fifth are the two strongest consonances, so a tuning system should include both.

## Stacking fifths

Start on C and keep going up by perfect fifths: C → G → D → A → E → B → F♯ → … After 12 fifths you're back at a C, about 7 octaves higher. Or almost:

$$
\frac{(3/2)^{12}}{2^{7}} = \frac{531441}{524288} \approx 1.01364
$$

The gap is called the **Pythagorean comma**, about 23.46 cents (a cent is $1/100$ of a semitone). Twelve pure fifths overshoot seven octaves by roughly a quarter of a semitone. The circle of fifths doesn't quite close.

## Why 12 is the sweet spot

We want a number of equal steps $n$ where some whole number of steps $k$ comes close to a fifth:

$$
2^{k/n} \approx \frac{3}{2} \quad\Longleftrightarrow\quad \frac{k}{n} \approx \log_2 1.5 \approx 0.58496
$$

$7/12 = 0.58333$ is a very good approximation for such a small denominator. The next clearly better options, like 41 or 53 notes per octave, are far too many for instruments and human hands.

## Equal temperament: spreading the error

Modern tuning (12-tone equal temperament) makes every semitone exactly $2^{1/12}$. The fifth becomes:

$$
2^{7/12} \approx 1.49831
$$

That's about 1.96 cents flat of a pure $3:2$, small enough that most listeners don't notice. In exchange, every key sounds the same, so you can modulate anywhere. Major thirds pay more: they're about 13.7 cents sharp of a pure $5:4$, which is why a barbershop chord sung in just intonation can sound brighter than a piano.

> [!info] Takeaway
> 12 notes is what you get when you want pure octaves, nearly pure fifths, and a keyboard a human can play.

Related: [[music/Live coding music|Live coding music]], where these note numbers become code.
