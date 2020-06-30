---
title: Starting a mini ray tracer with ShaderToy
date: 2020-06-29 22:55:42
tags: [cg]
---

Today I started a new project called Toycer. Because it is expected to be a ray tracer built with ShaderToy. After I tried to implement [a ray tracer with WebGL](https://github.com/akanarika/Tracer), I have got some basic ideas about how to start from scratch.

For the first part I set up a scene, where the camera sits at ```(0., 0., 2.)``` and a sphere is at ```(0., 0., -4.)```. So the camera looks into ```-z``` direction. Currently there is no shading for it. The color here depends on the ```t``` value of the hit point. And it looks like this:
![demo](/images/toycer/1.png)

Some helpful videos I referred to on Youtube:
* [Shadertoy for absolute beginners](https://www.youtube.com/watch?v=u5HAYVHsasc)
* [ShaderToy Tutorial Part 2 - Building stuff with circles](https://www.youtube.com/watch?v=GgGBR4z8C9o)
* [ShaderToy Tutorial - The simplest 3D](https://www.youtube.com/watch?v=dKA5ZVALOhs)

