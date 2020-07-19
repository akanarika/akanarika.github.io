---
title: Mini ray tracer more and some thoughts
date: 2020-07-18 20:58:39
tags: cg
---

Our mini ray tracer now has a ground and the material with refraction. I used the same refraction calculation approach as I tried in the Web tracer and it works here. Whereas, there appears to be some other small issue here, what are those black noises here?
![current stage](/images/toycer/4.png)

Some cartoon-like 'bug':
![some cute 'bug'](/images/toycer/5.png)

As I think of the reason why the diffuse reflection didn't work here. I started to get the concept fo **Global Illumination** we used to learn in the graphics class. As illustrated in the Wikipedia:
> Global illumination[1] (shortened as GI), or indirect illumination, is a group of algorithms used in 3D computer graphics that are meant to add more realistic lighting to 3D scenes. Such algorithms take into account not only the light that comes directly from a light source (direct illumination), but also subsequent cases in which light rays from the same source are reflected by other surfaces in the scene, whether reflective or not (indirect illumination).

and
> Images rendered using global illumination algorithms often appear more photorealistic than those using only direct illumination algorithms. However, such images are computationally more expensive and consequently much slower to generate.


