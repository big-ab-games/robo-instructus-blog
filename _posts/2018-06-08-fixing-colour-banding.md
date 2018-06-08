---
preface: robo-2
title: A Random Solution To Colour Banding
---

You may have noticed something about Robo Instructus' puzzle backgrounds when looking at screenshots in previous posts, there is a stepped gradient affect happening. While the gradient is intentional the stepping isn't! Let's take a look at colour banding, why does it occur and what can be done?

![](/assets/2018-06-08/banding.png "Can you see the colour banding in the background?")

Looking at the background you should be able to make out lines; unintended steps of colour instead of a smooth gradient.

First, it's worth mentioning that in itself it's not a big deal. The game backgrounds will eventually be replaced with textures anyway. Even so I believe it's always worth trying to understand the cause of an issue, so we can better address it when it does become important. Often such things aren't too hard to address straight away.

Let's zoom in a little and highlight some of the bands.

![](/assets/2018-06-08/labelled-bands.png "5 visible bands where all should be smooth")

Hopefully this closeup will help you see the banding if you couldn't before. So why is it happening? The gradient is defined in a simple fragment shader, a small program that runs on the GPU for each pixel on the screen.

```glsl
// background fragment shader
#version 330 core

in vec2 f_position;

out vec4 out_color;

const float DARKER = 0.01;
const float LIGHTER = 0.025;

void main() {
    float y_factor = (-f_position.y + 1.0) * 0.5;
    float x_factor = (-f_position.x + 1.0) * 0.5;
    float shade = mix(DARKER, LIGHTER, mix(y_factor, x_factor * x_factor, -0.8));
    out_color = vec4(vec3(shade), 1.0);
}
```

The shader is picking a colour for one pixel. You can see it's picking a grey colour value mixed between **0.01** _(quite dark)_ & **0.025** _(a bit lighter)_ depending where on the screen the pixel is. The resultant ***shade*** is a 32-bit floating point variable which is definitely accurate enough to appear smooth. The strange thing is no stepped-rounding is occurring in this shader to produce the bands we see. Indeed the gradient defined here looks like it should be totally smooth.

Actually the cause is the **colour format**. This format describes how the colour is actually stored in the render buffer. For Robo Instructus the format is just 8-bits each for _red, green, blue & alpha_. This means the colour output of the fragment shaders will be converted to this lower precision representation. 8-bit means only 256 greys are available, and since our background isn't going from white to black actually even fewer greys are available for the gradient.

Now we know why the banding occurs we can consider how to fix it. The most direct solution would be simply increasing the size of the colour format, if we used 32-bit, or even 16-bit, for each colour we'd have plenty of greys. However, for various compatibility reasons we're going to be stuck on our 8-bit grey format. A sneakier workaround is required.

## Dithering
Dithering is described as _" intentionally applied form of noise used to randomize quantization error, preventing large-scale patterns such as color banding in images"_. So it sounds promising!

The idea is I get a pseudo-random number that I use to nudge each pixel colour just a little lighter or darker. If the nudge is too small the noise will be totally lost after conversion to 8-bit grey, but if it's big enough it will nudge _some_ pixels up, or down, to another grey. So previously where greys halfway between two bands would be rendered as either one-band or the other uniformly, the noise will nudge half these pixels one-way and the other half the other-way randomly.

But how do we get pseudo-random numbers into our fragment shader? There isn't a built in ***rand()*** function for us. One way is to generate a noise texture and sample that to get per-pixel random value, and this is a very flexible general solution. But more fun is to use some clever pseudo-random maths logic found on stackoverflow or shadertoy, so let's add one I found & adapted to my fragment shader.

```glsl
// background fragment shader
#version 330 core

in vec2 f_position;

out vec4 out_color;

const float DARKER = 0.01;
const float LIGHTER = 0.025;
const float NOISE_FACTOR = 0.25 / 255.0;

// "gold noise" returns psuedo-random in range: (0, 1)
float rand(vec2 coord) {
    const float GR = 1.61803398874989484820459 * 0.1; // golden ratio
    const float PI  = 3.14159265358979323846264 * 0.1;
    const float SQ2 = 1.41421356237309504880169 * 10000.0; // root 2
    return fract(sin(dot(coord * GR, vec2(GR, PI))) * SQ2);
}

void main() {
    float y_factor = (-f_position.y + 1.0) * 0.5;
    float x_factor = (-f_position.x + 1.0) * 0.5;
    float shade = mix(DARKER, LIGHTER, mix(y_factor, x_factor * x_factor, -0.8));
    float noise = mix(NOISE_FACTOR, -NOISE_FACTOR, rand(gl_FragCoord.xy));
    out_color = vec4(vec3(shade) + noise, 1.0);
}
```

The ***rand*** function is not random at all, but produces noise from window coordinates that _appears_ random. In fragment shaders appearance is all the matters, and not having to use a texture makes this a nice drop in fix to the shader. The effect is subtle visible noise, but without any colour banding.

![](/assets/2018-06-08/band-dithered.png "Fragment shader old vs new")

The effect is subtle visible noise, but without any colour banding!

![](/assets/2018-06-08/dithered.png "No more bands!")

The noise here is set pretty low, but can actually provide a nice grainy texture to a colour. So as a bonus the ***rand*** function gives me a texture-less way to provide this grain to other bits of Robo Instructus if desired.
