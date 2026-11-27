---
layout: post
title: "Space Dust Shader"
kicker: "Shadertoy"
date: 2026-11-27 15:00:00 +0100
description: "Dust particles drifting toward the camera in a single fragment shader, plus a sun and a star field I never planned to make."
---

<div class="embed">
  <iframe src="https://www.shadertoy.com/embed/fcscDs?gui=true&t=10&paused=true&muted=false" title="Space Dust on Shadertoy" allowfullscreen loading="lazy"></iframe>
</div>

<p class="embed-link"><a href="https://www.shadertoy.com/view/fcscDs">View the full shader and code on Shadertoy ↗</a></p>

While working on The ISAAC Protocol, I kept thinking about a shader for the space dust drifting past the cockpit window. I finally sat down and made it. It's my first particle shader, and it took a couple of sessions, about four hours.

## A sun by accident

I built it step by step, starting with a single particle. It had a glow, and on its own it looked exactly like a sun. So I moved it to a corner and added a flicker.

Next I needed more than one dot. I repeated the circle across the screen with `fract`, which splits the screen into a grid of cells, and used a hash function to give each dot a random offset inside its cell so they don't line up:

```glsl
float hash21(vec2 p) {
    p = fract(p * vec2(123.34, 456.21));
    p += dot(p, p + 45.32);
    return fract(p.x * p.y);
}
```

They still had the glow, so they looked like stars. I kept them as the background and gave them a flicker too, with different frequencies so they don't all twinkle in sync.

## The actual dust

Then I redid the circle without the glow, the dust I was after from the start, and scattered it with the same offset logic. A particle in every cell looked far too dense, so I looked up how to thin them out: a second hash per cell decides whether that cell gets a particle at all, and only about one cell in five does.

To make it move, I looked into how to fake depth. Each layer zooms toward the camera and loops, and three layers offset in time keep the dust coming:

```glsl
float z1 = 1.0 - fract(iTime * 0.2);
float z2 = 1.0 - fract(iTime * 0.2 + 0.33);
float z3 = 1.0 - fract(iTime * 0.2 + 0.66);
```

The first version popped: particles appeared and vanished abruptly every time a layer looped. Fading them in and out fixed it. Getting the fades and the perspective right was the hardest part.

## What I learned

How to fake depth in 2D, and how to add movement that actually makes sense.

## What I'd change

I'd give the particles some color and different shapes. There's also a small bug in the star glow: each star only exists in its own cell's local coordinates, so its glow gets cut off at the cell border.
