---
layout: post
title: "Back to fundamentals"
kicker: "Devlog #0"
description: "Why I'm rebuilding my graphics work from the ground up, and what's coming next."
---

I've always been amazed by how renderers can create such believable visuals. Walking around a virtual place as if it were real made me want to understand how silicon and copper, ones and zeros, can produce images that rich. The more effort I put into learning it, the more it pulled me in.

I've been writing graphics code for a while: an OpenGL renderer built through LearnOpenGL's "Advanced OpenGL" chapters, a DDA raycasting game on an Arduino, a few Shadertoy shaders and some engine experiments.

But those projects were built before I had a plan, and they don't show how I work today. So I'm starting over in one cohesive repo, **gfx-lab**: one structure, one build, tests, clean commits, and a visible progression from the first triangle to a modern-API renderer. The goal is to become a professional graphics programmer.

## What's coming

- LearnOpenGL from scratch, alongside *Computer Graphics: Principles and Practice*
- A CPU software rasterizer and ray caster, with my own math library
- A scene renderer of my own design: deferred shading, shadows, PBR, HDR
- A CPU path tracer
- A Vulkan or DX12 renderer

## So far

The build is in place: one CMake setup, shared by every project in the repo. Next up: the classic "Hello Triangle".

## Follow along

The code lives in [gfx-lab](https://github.com/OSANNnn/gfx-lab), and there'll be a new post here at every milestone.
