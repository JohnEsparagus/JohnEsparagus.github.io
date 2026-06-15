---
title: "Voxel Ray Marcher"
description: "A real-time voxel renderer using ray marching in a fragment shader. Supports ambient occlusion, soft shadows, and procedural generation."
tags: [GLSL, WebGL, C++]
github: "https://github.com/your-username/your-repo/tree/main/projects/voxel-marcher"
order: 2
---

## Overview

A fragment-shader ray marcher for sparse voxel octrees. The scene is encoded as an SVO and uploaded as a buffer texture; the shader traverses it per-pixel.

## Lighting

Soft shadows are computed by cone-marching toward the light source. Ambient occlusion samples the SVO at 5 offsets per pixel with a cheap heuristic that holds up surprisingly well at distance.
