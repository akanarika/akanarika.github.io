---
title: SDF basics 1
date: 2020-07-24 22:07:00
tags: cg
---

### Concept

SDF refers to "Signed Distance Function".
The surface of a geometry `f(p) = 0`, an implicit function, where `p` is a point in the space. Usually ray marching approach can be used to draw such geometry objects.

### Ray marching
We start from the camera, trying to find the closest distance. Then from the distance on the ray, march again, and again, until the distance is too long, or it can't reach much further.

```
float rayMarch(in vec3 ro, in vec3 rd) {
	float t = 0.;
    for (int i = 0; i < 100; i++) {
    	vec3 p = ro + t * rd;
        float h = getDist(p); // SDF function
        t += h;
        if (t > 200. || h < 0.001) break; 
    }
    if (t > 200.) t = -1.;
    return t;
}
```

### Normals
[Ref from Inigo Quilez](https://iquilezles.org/www/articles/normalsSDF/normalsSDF.htm)
The normal of the surface can be down through the gradient of the SDF at points located on the surface.
![](/images/shaderstudy/2.png)
![](/images/shaderstudy/3.png)

