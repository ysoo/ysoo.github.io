---
layout: post
title: "Ray Tracer - Part 1"
date: 2023-11-20 19:41:00 -0800
permalink: /blog/:title
---

Hi, it's been a while since I written here.

I have wanted to create my own physics engine for a while and I have finally carved out time on procrastinating on other stuff to work on this.

But it turns out that there is no instant gratification in building out a physics engine since we would also require a graphics engine to showcase the physics that come out from a physics engine.

So here, I think I'm going to start by building a ray tracer.

I am referring mainly to the Ray Tracing in One Weekend book by Peter Shirley, Trevor David Black and Steve Hollasch to learn how to build it https://raytracing.github.io/books/RayTracingInOneWeekend.html

This site, scratchapixel, also has a lot of information https://www.scratchapixel.com/index.html

And I'm pushing into this repository https://github.com/ysoo/tinyraytracer

We start off by just rendering an image:

#### What I've learnt

1. Rendering an image is literally just specifying what each pixel would be in red/green/blue, with a header with some metadata, in PPM it's just the width and height of the image.
2. Rays can be imagined as a function P(t) = A + tb
   - A is the ray origin
   - b is the ray direction

Ray tracers at it's core

1. Calculate the ray from the camera through the pixel
2. Determine the objects where the ray intersects
3. Compute a color for the closest intersection point

Here's the fun part, we are adding a sphere. To do that, we need to find how a ray and a sphere would intersect. 

So, spheres are made out of the equation
{% highlight ruby %}
(x - C_x) ^2 + (y - C_y) ^2 + (z - C_z) ^2 = r^2
{% endhighlight %}

Where C is the sphere center

So, let's take a point P and we try to find the vector from P to the center would be (P - C)

{% highlight ruby %}
(P - C) dot (P - C) = (x - C_x) ^2 + (y - C_y) ^2 + (z - C_z) ^2 = r^2
{% endhighlight %}

{% highlight ruby %}
(P(t) - C) dot (P(t) - C) = ((A + tb) - C) dot ((A + tb) - C) = r^2
{% endhighlight %}

And then we can expand it to become a quadratic equation and then we can determine if we are hitting the sphere by checking if we are > 0 (outside the sphere) or <= 0 (inside the sphere)

{% highlight ruby %}
t^2 b dot b + 2 t b dot(A - C) + (A  - C) dot (A - C) - r^2 = 0
{% endhighlight %}