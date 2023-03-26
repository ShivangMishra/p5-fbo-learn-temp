Learn page for p5.Framebuffer

Introduction
For quite some time, createGraphics() has been the recommended way to create a texture and use it elsewhere in a sketch. While it is very flexible and approachable, it unfortunately comes with inherent performance implication. Every time you call createGraphics, p5 creates an entirely new canvas object, containing a new webGL context. Browsers limit the number of webGL contexts that you can have on a single page. If you try and create too many, the browser will remove the oldest ones!
Now, p5 provides p5.Framebuffer as a solution to these limitations.

What is a framebuffer ?
A framebuffer is a low-level graphics buffer that provides a way to render graphics off-screen and then use the resulting image as a texture in a subsequent rendering pass. It consists of several components, including color attachments, depth attachments, and stencil attachments. The color attachments are used to store the color values of rendered objects, while the depth and stencil attachments are used to store depth and stencil information, respectively. These attachments can be combined in different ways to create various rendering effects.

How does p5.Framebuffer relate to p5.Graphics ?
A Framebuffer is similar to p5.Graphics as it lets you draw to a canvas, and then treat that canvas like an image, but they are different as framebuffer: 

- is faster: it shares the same WebGL context as the rest of the sketch, so it doesn't need to copy extra data to the GPU each frame
- has more information: you can access the WebGL depth buffer as a texture, letting you do things like write focal blur shaders.
- is WebGL only: this will not work in 2D mode! p5.Graphics should be fine for that.

To summarize, p5.Graphics is a higher-level graphics buffer that is simpler to use and more versatile, while framebuffer is a low-level graphics buffer that allows for more advanced image manipulation using the WebGL API.

Floating point textures
Sometimes, you want to write code that adds on to or modifies the previous frame. You may notice weird artifacts that show up due to the fact that colors are internally stored as integers: sometimes if you overlay a color with a very small alpha, the change in color is too small to round the resulting color up to the next integer value, so it doesn't change at all.
This can be fixed if you store colors as floating point values! You can specify this in an optional options object when creating a Framebuffer object.

Depth Information
By using the depth information of a scene, it is possible to simulate the way that a camera focuses on objects at different depths. This can be used to create a variety of depth of field effects such as the following -
https://openprocessing.org/sketch/1738229
https://openprocessing.org/sketch/1721124
https://openprocessing.org/sketch/1787913