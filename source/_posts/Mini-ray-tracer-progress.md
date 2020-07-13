---
title: Mini ray tracer progress
date: 2020-07-13 14:23:30
tags: cg
---

Even though I thought I was not going to modify my ray tracer in WebGL any more, but with passion out of no where, I added camera rotation and tried to clean up a bit. There now is a working version which I was pretty happy with. Also added triangles, cubes and planes.
![wip1](/images/toycer/21.gif)

Then I started working on refraction, some buggies showed up again. After trying two nights, I started wondering if those issues are from my code (of course). But I decided to keep up with my ShaderToy tracer to switch my mood. 
First step I added some lights and created two spheres.
![wip2](/images/toycer/2.png)

Then I started kinda 'copying' my code from WebGL tracer. After adding diffuse material by using reflected rays, the shading looks correct but the sampling looks weird. Then I read the book, just to find the shading can be simply combined with Amibient + Diffuse + Specular. I'm not sure about the relationship between the Lambertian modal and the way where we actually shoot rays bounced by the sphere. That is my confusion now.
![wip3](/images/toycer/3.png)

