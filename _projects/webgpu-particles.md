---
title: "WebGPU Particle System"
description: "Real-time particle simulation using compute shaders. 100k+ particles with gravity, orbital forces, and dynamic coloring — runs entirely in the browser."
tags: [WebGPU, WGSL, TypeScript]
demo: "projects/webgpu-particles/"
github: "https://github.com/your-username/your-repo/tree/main/projects/webgpu-particles"
order: 1
---

## Overview

This project explores compute-based particle simulation on the GPU using the WebGPU API. All physics runs in a WGSL compute shader — the CPU only submits a single dispatch per frame.

## Technical details

The system uses a ping-pong buffer pattern: two storage buffers alternate between read and write each frame, avoiding any CPU readback. The render pass then draws instanced quads using the final particle positions.

### Compute shader design

Each workgroup of 64 invocations processes one particle. Forces applied per frame:

- **Gravity**: constant downward acceleration
- **Orbital**: attraction toward configurable attractor points
- **Drag**: velocity damping to prevent runaway energy

### Performance

On an M2 MacBook Pro, 100k particles run at a stable 60fps with ~0.3ms GPU time per frame. The bottleneck at higher counts shifts to the vertex stage, not compute.

## What I learned

WebGPU's explicit resource binding model makes it easier to reason about GPU memory layout than WebGL. The lack of implicit state also makes debugging more predictable with RenderDoc.
