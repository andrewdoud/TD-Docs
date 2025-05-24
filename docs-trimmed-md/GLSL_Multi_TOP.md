

# GLSL_Multi_TOP

GLSL Multi TOP - TouchDesigner Documentation




# GLSL Multi TOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The GLSL Multi TOP renders a GLSL shader into a TOP image. Its parameters and functionality are identical to the [GLSL TOP](GLSL_TOP.html "GLSL TOP"), except it allows for more than 3 inputs.  
Refer to the [GLSL TOP](GLSL_TOP.html "GLSL TOP") help page for more information.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[glslmultiTOP\_Class](https://docs.derivative.ca/GlslmultiTOP_Class "GlslmultiTOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - GLSL Page](#Parameters_-_GLSL_Page)
* [3 Parameters - Vectors Page](#Parameters_-_Vectors_Page)
* [4 Parameters - Arrays Page](#Parameters_-_Arrays_Page)
* [5 Parameters - Matrices Page](#Parameters_-_Matrices_Page)
* [6 Parameters - Atomic Counters Page](#Parameters_-_Atomic_Counters_Page)
* [7 Parameters - Constants Page](#Parameters_-_Constants_Page)
* [8 Parameters - Common Page](#Parameters_-_Common_Page)
* [9 Operator Inputs](#Operator_Inputs)
* [10 Info CHOP Channels](#Info_CHOP_Channels)
  + [10.1 Common TOP Info Channels](#Common_TOP_Info_Channels)
  + [10.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - GLSL Page
GLSL Version `glslversion` - ⊞ - Pick what version of GLSL to compile the shader with.
* 1.20 `glsl120` -
* 3.30 `glsl330` -
* 4.00 `glsl400` -
* 4.10 `glsl410` -
* 4.20 `glsl420` -
* 4.30 `glsl430` -
* 4.40 `glsl440` -
* 4.50 `glsl450` -
* 4.60 `glsl460` -
Mode `mode` - ⊞ - Choose what type of shader you are writing, vertex/pixel shader, or a compute shader.
* Vertex/Pixel Shader `vertexpixel` -
* Compute Shader `compute` -
Preprocess Directives `predat` -
Vertex Shader `vertexdat` - Points to the [DAT](DAT.html "DAT") holding the Vertex Shader. Drag & Drop a DAT here, or manually enter the path to the DAT.
Pixel Shader `pixeldat` - Points to the [DAT](DAT.html "DAT") holding the Pixel Shader. Drag & Drop a DAT here, or manually enter the path to the DAT.
Compute Shader `computedat` - Points to the [DAT](DAT.html "DAT") holding the [Compute Shader](Compute_Shader.html "Compute Shader"). Drag & Drop a DAT here, or manually enter the path to the DAT.
Load Uniform Names `loaduniformnames` - When this button is pressed the node will try to pre-fill all it's uniform parameter with uniforms that are declare in the shader. Note that the shader compiler will likely not expose uniforms that are unused.
Auto Dispatch Size `autodispatchsize` - Automatically set the dispatch size based on the compute shader's local size and the output texture resolution. Ensures at least one thread per pixel will execute.
Dispatch Size `dispatchsize` - ⊞ - The dispatch size to use when executing a compute shader.
* X `dispatchsizex` -
* Y `dispatchsizey` -
* Z `dispatchsizez` -
Output Access `outputaccess` - ⊞ - Controls how the output textures will be accessed. If the textures will be read from (such as using previous frame's values), then the access should be changed to Read-Write instead of Write Only.
* Write Only `writeonly` -
* Read Only `readonly` -
* Read-Write `readwrite` -
Output Type `type` - ⊞ - Specify what type of texture to create. When creating a 3D texture the TOP will render once for every slice of the output. Refer to  [3D Textures and 2D Texture Arrays](https://docs.derivative.ca/Write_a_GLSL_TOP#3D_Textures_and_2D_Texture_Arrays "Write a GLSL TOP") for more info.
* 2D Texture `texture2d` - Creates a 2D texture.
* 2D Texture Array `texture2darray` - Creates a [2D Texture Array](https://docs.derivative.ca/2D_Texture_Array "2D Texture Array"). Slices of the array can be access using a non-normalized integer index for the w coordinate.
* 3D Texture `texture3d` - Creates a [3D Texture](https://docs.derivative.ca/3D_Texture "3D Texture"). Slices of the array can be accessed using the w coordinate in the range 0-1. Value of the texture in between slices are interpolated.
Depth `depth` - ⊞ - Set the depth of the 3D texture from the **Input** or the **Custom Depth** parameter.
* Input `input` -
* Custom `custom` -
Custom Depth `customdepth` - Manually set the depth of the 3D texture, otherwise it will use the depth of the input.
Clear Outputs `clearoutputs` -
Clear Value `clearvalue` - ⊞ -
* Clear Value `clearvaluer` -
* Clear Value `clearvalueg` -
* Clear Value `clearvalueb` -
* Clear Value `clearvaluea` -
Input Mapping `inputmapping` - ⊞ - Determines how the node's input(s) are passed into the shader for use when creating a 3D Texture. By default all of the inputs are passed to each slice. When using the **N inputs per Slice** mode, the first N inputs are passed to the first slice, the next N inputs are passed the second slice, and so on. When it runs out of inputs it loops back to the first input. N is selected by the parameter **N Value**.
* All Inputs to Every Slice `all` -
* N Input(s) per Slice `ninputs` -
N Value `nval` - Determines how many inputs are passed to the shader per slice when using the **N inputs per Slice** mode for **Input Mapping**. If for example this is set to 2, then the first 2 inputs will be passed to the first slice, the next 2 inputs will be passed the second slice, and so on. It will loop back to the start of the inputs if it runs out before it reaches the last slice.
Input Extend Mode UV `inputextenduv` - ⊞ - Controls what is returned from your texture sampling functions when the U and V texture coordinates (called S and T in the shader) are outside [0-1] range.
* Hold `hold` -
* Zero `zero` -
* Repeat `repeat` -
* Mirror `mirror` -
Input Extend Mode W `inputextendw` - ⊞ - Controls what is returned from your texture sampling functions when the W texture coordinate (called W in the shader) are outside [0-1] range. Only useful for [3D Texture](https://docs.derivative.ca/3D_Texture "3D Texture").
* Hold `hold` -
* Zero `zero` -
* Repeat `repeat` -
* Mirror `mirror` -
# of Color Buffers `numcolorbufs` - Any shader you write can output to more than one RGBA buffer at a time. Turn up this value to have more color buffers allocated for you, and refer to [Write\_a\_GLSL\_TOP#Outputting\_to\_Multiple\_Color\_Buffers Write a GLSL TOP] for more information on using this feature.
  

## Parameters - Vectors Page
These are passed as uniforms into your shader. Depending on how the uniform is declared only some of the values of the 4 available per parameter as passes to the shader. For example, if the uniform is declared as a vec2, then only the first 2 values are passed to the shader, the other 2 are ignored.
Vector `vec` - Sequence of vector uniforms
Name `vec0name` - The uniform name, as declared in the shader
Value `vec0value` - ⊞ - The value(s) to give the uniform.
* Value `vec0valuex` -
* Value `vec0valuey` -
* Value `vec0valuez` -
* Value `vec0valuew` -

  

## Parameters - Arrays Page
CHOP Uniforms allow you to send CHOP channel data into a GLSL shader as an array. Depending on the array type used, the number of values you can send into the shader may be limited. If you are using Uniform Arrays, you can use the Built-In variable `int(var('SYS_GFX_GLSL_MAX_UNIFORMS'))` to get an idea of how many values you can pass to the shader. Current GPUs are vec4 based for uniform arrays, so the maximum array size is `int(var('SYS_GFX_GLSL_MAX_UNIFORMS')) / 4`. Other uniforms will take away from this maximum. If you are using Texture Buffers the maximum array size is far bigger, `int(var('SYS_GFX_MAX_TEXTURE_BUFFER_SIZE'))` will tell you the max for this. The max for texture buffer is per texture buffer, and having multiple texture buffers does not take away from the max for each array.
Array `array` - Sequence of array uniforms
Name `array0name` - The name of the uniform. You can send up to 4 channels into the GLSL shader in a single uniform. The number of channels is determined by the float/vec2/vec3/vec4 menu to the right of the name. For a CHOP with a single channel declare your uniform as a float, for one with two channels declare your uniform as a vec2, etc. The data is interleaved in the uniform. I.e the .x component is the 1st channel, .y is the 2nd channel, etc.
Type `array0type` - ⊞ - The data type of the uniform in the shader.
* float `float` -
* vec2 `vec2` -
* vec3 `vec3` -
* vec4 `vec4` -
CHOP `array0chop` - The channels from this CHOP will be sent to the GLSL shader.
Array Type `array0arraytype` - ⊞ - The type of the uniform.
* Uniform Array `uniformarray` - All GPUs can send array data into a GLSL shader using Uniform Arrays.
* Texture Buffer `texturebuffer` - Newer GPUs can send array data into a GLSL shader using Texture Buffers. Texture Buffers use texture memory and texture fetches to access the data, which allows them to store many more values.
Declare them:
```
uniform samplerBuffer <uniformname>;
```
And sample them like this
```
vec4 val = texelFetch(<uniformname>, i);
```
Where i is the 0-based index (an integer) into the buffer that you want to get a value for.

  

## Parameters - Matrices Page
Matrix `matrix` - Sequence of matrix uniforms
Name `matrix0name` - The name of the matrix uniform.
Matrix `matrix0value` - The value to assign the matrix. For valid ways to specify this, see the [Matrix Parameters](Matrix_Parameters.html "Matrix Parameters") article.
  

## Parameters - Atomic Counters Page
Atomic Counter `ac` - Sequence of atomic counter uniforms
Name `ac0name` - The name of the uniform.
Initial Value Type `ac0initvalue` - ⊞ - Specifies how the atomic counters receive their initial value, either through a single default value or a CHOP.
* Single Value `val` -
* CHOP Values `chop` -
Initial Value `ac0singlevalue` - Specifies a single value that all atomic counters in this binding will be initialized to.
Initial Values CHOP `ac0chopvalue` - A reference to the CHOP that will determine the initial values of the atomic counters in this binding. The CHOP will be spanned in track order, so the values from the first track will be read in order first, then the next track (if there is one) and so on. If there are more initial values to fill than there are values in the CHOP then they will all be set to 0. Atomic counters will be initialized from low to high offsets.
  

## Parameters - Constants Page
[Specialization Constants](https://docs.derivative.ca/Write_a_GLSL_TOP#Specialization_Constants "Write a GLSL TOP") can optionally have their values assigned here.
Constant `const` - Sequence of constant uniforms
Name `const0name` - The constant name, as declared in the shader.
Value `const0value` - The value to give the constant.
  

## Parameters - Common Page
Output Resolution `outputresolution` - ⊞ - quickly change the resolution of the TOP's data.
* Use Input `useinput` - Uses the input's resolution.
* Eighth `eighth` - Multiply the input's resolution by that amount.
* Quarter `quarter` - Multiply the input's resolution by that amount.
* Half `half` - Multiply the input's resolution by that amount.
* 2X `2x` - Multiply the input's resolution by that amount.
* 4X `4x` - Multiply the input's resolution by that amount.
* 8X `8x` - Multiply the input's resolution by that amount.
* Fit Resolution `fit` - Fits the width and height to the resolution given below, while maintaining the aspect ratio.
* Limit Resolution `limit` - The width and height are limited to the resolution given below. If one of the dimensions exceeds the given resolution, the width and height will be reduced to fit inside the given limits while maintaining the aspect ratio.
* Custom Resolution `custom` - Enables the Resolution parameter below, giving direct control over width and height.
Resolution `resolution` - ⊞ - Enabled only when the Resolution parameter is set to Custom Resolution. Some Generators like Constant and Ramp do not use inputs and only use this field to determine their size. The drop down menu on the right provides some commonly used resolutions.
* W `resolutionw` -
* H `resolutionh` -
Resolution Menu `resmenu` - A drop-down menu with some commonly used resolutions.
Use Global Res Multiplier `resmult` - Uses the Global Resolution Multiplier found in **Edit>Preferences>TOPs**. This multiplies all the TOPs resolutions by the set amount. This is handy when working on computers with different hardware specifications. If a project is designed on a desktop workstation with lots of graphics memory, a user on a laptop with only 64MB VRAM can set the Global Resolution Multiplier to a value of half or quarter so it runs at an acceptable speed. By checking this checkbox on, this TOP is affected by the global multiplier.
Output Aspect `outputaspect` - ⊞ - Sets the image aspect ratio allowing any textures to be viewed in any size. Watch for unexpected results when compositing TOPs with different aspect ratios. (You can define images with non-square pixels using xres, yres, aspectx, aspecty where xres/yres != aspectx/aspecty.)
* Use Input `useinput` - Uses the input's aspect ratio.
* Resolution `resolution` - Uses the aspect of the image's defined resolution (ie 512x256 would be 2:1), whereby each pixel is square.
* Custom Aspect `custom` - Lets you explicitly define a custom aspect ratio in the Aspect parameter below.
Aspect `aspect` - ⊞ - Use when Output Aspect parameter is set to Custom Aspect.
* Aspect1 `aspect1` -
* Aspect2 `aspect2` -
Aspect Menu `armenu` - A drop-down menu with some commonly used aspect ratios.
Input Smoothness `inputfiltertype` - ⊞ - This controls pixel filtering on the input image of the TOP.
* Nearest Pixel `nearest` - Uses nearest pixel or accurate image representation. Images will look jaggy when viewing at any zoom level other than Native Resolution.
* Interpolate Pixels `linear` - Uses linear filtering between pixels. This is how you get TOP images in viewers to look good at various zoom levels, especially useful when using any Fill Viewer setting other than Native Resolution.
* Mipmap Pixels `mipmap` - Uses  [mipmap](Mipmapping.html "Mipmapping") filtering when scaling images. This can be used to reduce artifacts and sparkling in moving/scaling images that have lots of detail.
Fill Viewer `fillmode` - ⊞ - Determine how the TOP image is displayed in the viewer.
**NOTE:**To get an understanding of how TOPs work with images, you will want to set this to **Native Resolution** as you lay down TOPs when starting out. This will let you see what is actually happening without any automatic viewer resizing.
* Use Input `useinput` - Uses the same Fill Viewer settings as it's input.
* Fill `fill` - Stretches the image to fit the edges of the viewer.
* Fit Horizontal `width` - Stretches image to fit viewer horizontally.
* Fit Vertical `height` - Stretches image to fit viewer vertically.
* Fit Best `best` - Stretches or squashes image so no part of image is cropped.
* Fit Outside `outside` - Stretches or squashes image so image fills viewer while constraining it's proportions. This often leads to part of image getting cropped by viewer.
* Native Resolution `nativeres` - Displays the native resolution of the image in the viewer.
Viewer Smoothness `filtertype` - ⊞ - This controls pixel filtering in the viewers.
* Nearest Pixel `nearest` - Uses nearest pixel or accurate image representation. Images will look jaggy when viewing at any zoom level other than Native Resolution.
* Interpolate Pixels `linear` - Uses linear filtering between pixels. Use this to get TOP images in viewers to look good at various zoom levels, especially useful when using any Fill Viewer setting other than Native Resolution.
* Mipmap Pixels `mipmap` - Uses  [mipmap](Mipmapping.html "Mipmapping") filtering when scaling images. This can be used to reduce artifacts and sparkling in moving/scaling images that have lots of detail.
Passes `npasses` - Duplicates the operation of the TOP the specified number of times. Making this larger than 1 is essentially the same as taking the output from each pass, and passing it into the first input of the node and repeating the process. Other inputs and parameters remain the same for each pass.
Channel Mask `chanmask` - Allows you to choose which channels (R, G, B, or A) the TOP will operate on. All channels are selected by default.
Pixel Format `format` - ⊞ - Format used to store data for each channel in the image (ie. R, G, B, and A). Refer to [Pixel Formats](Pixel_Formats.html "Pixel Formats") for more information.
* Use Input `useinput` - Uses the input's pixel format.
* 8-bit fixed (RGBA) `rgba8fixed` - Uses 8-bit integer values for each channel.
* sRGB 8-bit fixed (RGBA) `srgba8fixed` - Uses 8-bit integer values for each channel and stores color in sRGB colorspace.
* 16-bit float (RGBA) `rgba16float` - Uses 16-bits per color channel, 64-bits per pixel.
* 32-bit float (RGBA) `rgba32float` - Uses 32-bits per color channel, 128-bits per pixels.
* 10-bit RGB, 2-bit Alpha, fixed (RGBA) `rgb10a2fixed` - Uses 10-bits per color channel and 2-bits for alpha, 32-bits total per pixel.
* 16-bit fixed (RGBA) `rgba16fixed` - Uses 16-bits per color channel, 64-bits total per pixel.
* 11-bit float (RGB), Positive Values Only `rgba11float` - A RGB floating point format that has 11 bits for the Red and Green channels, and 10-bits for the Blue Channel, 32-bits total per pixel (therefore the same memory usage as 8-bit RGBA). The Alpha channel in this format will always be 1. Values can go above one, but can't be negative. ie. the range is [0, infinite).
* 16-bit float (RGB) `rgb16float` -
* 32-bit float (RGB) `rgb32float` -
* 8-bit fixed (Mono) `mono8fixed` - Single channel, where RGB will all have the same value, and Alpha will be 1.0. 8-bits per pixel.
* 16-bit fixed (Mono) `mono16fixed` - Single channel, where RGB will all have the same value, and Alpha will be 1.0. 16-bits per pixel.
* 16-bit float (Mono) `mono16float` - Single channel, where RGB will all have the same value, and Alpha will be 1.0. 16-bits per pixel.
* 32-bit float (Mono) `mono32float` - Single channel, where RGB will all have the same value, and Alpha will be 1.0. 32-bits per pixel.
* 8-bit fixed (RG) `rg8fixed` - A 2 channel format, R and G have values, while B is 0 always and Alpha is 1.0. 8-bits per channel, 16-bits total per pixel.
* 16-bit fixed (RG) `rg16fixed` - A 2 channel format, R and G have values, while B is 0 always and Alpha is 1.0. 16-bits per channel, 32-bits total per pixel.
* 16-bit float (RG) `rg16float` - A 2 channel format, R and G have values, while B is 0 always and Alpha is 1.0. 16-bits per channel, 32-bits total per pixel.
* 32-bit float (RG) `rg32float` - A 2 channel format, R and G have values, while B is 0 always and Alpha is 1.0. 32-bits per channel, 64-bits total per pixel.
* 8-bit fixed (A) `a8fixed` - An Alpha only format that has 8-bits per channel, 8-bits per pixel.
* 16-bit fixed (A) `a16fixed` - An Alpha only format that has 16-bits per channel, 16-bits per pixel.
* 16-bit float (A) `a16float` - An Alpha only format that has 16-bits per channel, 16-bits per pixel.
* 32-bit float (A) `a32float` - An Alpha only format that has 32-bits per channel, 32-bits per pixel.
* 8-bit fixed (Mono+Alpha) `monoalpha8fixed` - A 2 channel format, one value for RGB and one value for Alpha. 8-bits per channel, 16-bits per pixel.
* 16-bit fixed (Mono+Alpha) `monoalpha16fixed` - A 2 channel format, one value for RGB and one value for Alpha. 16-bits per channel, 32-bits per pixel.
* 16-bit float (Mono+Alpha) `monoalpha16float` - A 2 channel format, one value for RGB and one value for Alpha. 16-bits per channel, 32-bits per pixel.
* 32-bit float (Mono+Alpha) `monoalpha32float` - A 2 channel format, one value for RGB and one value for Alpha. 32-bits per channel, 64-bits per pixel.
  

## Operator Inputs
* Input 0:  - Multi input
  

## Info CHOP Channels
Extra Information for the GLSL Multi TOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Common TOP Info Channels
* resx - Horizontal resolution of the TOP in pixels.
* resy - Vertical resolution of the TOP in pixels.
* aspectx - Horizontal aspect of the TOP.
* aspecty - Vertical aspect of the TOP.
* depth - Depth of 2D or 3D array if this TOP contains a 2D or 3D texture array.
* gpu\_memory\_used - Total amount of texture memory used by this TOP.
### Common Operator Info Channels
* total\_cooks - Number of times the operator has cooked since the process started.
* cook\_time - Duration of the last cook in milliseconds.
* cook\_frame - Frame number when this operator was last cooked relative to the component timeline.
* cook\_abs\_frame - Frame number when this operator was last cooked relative to the absolute time.
* cook\_start\_time - Time in milliseconds at which the operator started cooking in the frame it was cooked.
* cook\_end\_time - Time in milliseconds at which the operator finished cooking in the frame it was cooked.
* cooked\_this\_frame - 1 if operator was cooked this frame.
* warnings - Number of warnings in this operator if any.
* errors - Number of errors in this operator if any.
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2022.241402021.100002020.200002018.28070before 2018.28070
| TOPs |
| --- |
| [Add](Add_TOP.html "Add TOP") • [Analyze](Analyze_TOP.html "Analyze TOP") • [Anti Alias](Anti_Alias_TOP.html "Anti Alias TOP") • [Blob Track](Blob_Track_TOP.html "Blob Track TOP") • [Bloom](Bloom_TOP.html "Bloom TOP") • [Blur](Blur_TOP.html "Blur TOP") • [Cache Select](Cache_Select_TOP.html "Cache Select TOP") • [Cache](Cache_TOP.html "Cache TOP") • [Channel Mix](Channel_Mix_TOP.html "Channel Mix TOP") • [CHOP to](CHOP_to_TOP.html "CHOP to TOP") • [Chroma Key](Chroma_Key_TOP.html "Chroma Key TOP") • [Circle](Circle_TOP.html "Circle TOP") • [Composite](Composite_TOP.html "Composite TOP") • [Constant](Constant_TOP.html "Constant TOP") • [Convolve](Convolve_TOP.html "Convolve TOP") • [Corner Pin](Corner_Pin_TOP.html "Corner Pin TOP") • [CPlusPlus](CPlusPlus_TOP.html "CPlusPlus TOP") • [Crop](Crop_TOP.html "Crop TOP") • [Cross](Cross_TOP.html "Cross TOP") • [Cube Map](Cube_Map_TOP.html "Cube Map TOP") • [Depth](Depth_TOP.html "Depth TOP") • [Difference](Difference_TOP.html "Difference TOP") • [Direct Display Out](Direct_Display_Out_TOP.html "Direct Display Out TOP") • [DirectX In](DirectX_In_TOP.html "DirectX In TOP") • [DirectX Out](DirectX_Out_TOP.html "DirectX Out TOP") • [Displace](Displace_TOP.html "Displace TOP") • [Edge](Edge_TOP.html "Edge TOP") • [Emboss](Emboss_TOP.html "Emboss TOP") • [Feedback](Feedback_TOP.html "Feedback TOP") • [Fit](Fit_TOP.html "Fit TOP") • [Flip](Flip_TOP.html "Flip TOP") • [Function](Function_TOP.html "Function TOP") • GLSL Multi• [GLSL](GLSL_TOP.html "GLSL TOP") • [HSV Adjust](HSV_Adjust_TOP.html "HSV Adjust TOP") • [HSV to RGB](HSV_to_RGB_TOP.html "HSV to RGB TOP") • [Import Select](Import_Select_TOP.html "Import Select TOP") • [In](In_TOP.html "In TOP") • [Inside](Inside_TOP.html "Inside TOP") • [Introduction To s Vid](Introduction_To_TOPs_Vid.html "Introduction To TOPs Vid") • [Kinect Azure Select](Kinect_Azure_Select_TOP.html "Kinect Azure Select TOP") • [Kinect Azure](Kinect_Azure_TOP.html "Kinect Azure TOP") • [Kinect](Kinect_TOP.html "Kinect TOP") • [Layout](Layout_TOP.html "Layout TOP") • [Leap Motion](Leap_Motion_TOP.html "Leap Motion TOP") • [Lens Distort](Lens_Distort_TOP.html "Lens Distort TOP") • [Level](Level_TOP.html "Level TOP") • [Limit](Limit_TOP.html "Limit TOP") • [Lookup](Lookup_TOP.html "Lookup TOP") • [Luma Blur](Luma_Blur_TOP.html "Luma Blur TOP") • [Luma Level](Luma_Level_TOP.html "Luma Level TOP") • [Math](Math_TOP.html "Math TOP") • [Matte](Matte_TOP.html "Matte TOP") • [Mirror](Mirror_TOP.html "Mirror TOP") • [Monochrome](Monochrome_TOP.html "Monochrome TOP") • [MoSys](MoSys_TOP.html "MoSys TOP") • [Movie File In](Movie_File_In_TOP.html "Movie File In TOP") • [Movie File Out](Movie_File_Out_TOP.html "Movie File Out TOP") • [MPCDI](MPCDI_TOP.html "MPCDI TOP") • [Multiply](Multiply_TOP.html "Multiply TOP") • [Ncam](Ncam_TOP.html "Ncam TOP") • [NDI In](NDI_In_TOP.html "NDI In TOP") • [NDI Out](NDI_Out_TOP.html "NDI Out TOP") • [Noise](Noise_TOP.html "Noise TOP") • [Normal Map](Normal_Map_TOP.html "Normal Map TOP") • [Notch](Notch_TOP.html "Notch TOP") • [Null](Null_TOP.html "Null TOP") • [Nvidia Background](Nvidia_Background_TOP.html "Nvidia Background TOP") • [Nvidia Denoise](Nvidia_Denoise_TOP.html "Nvidia Denoise TOP") • [Nvidia Flex](Nvidia_Flex_TOP.html "Nvidia Flex TOP") • [Nvidia Flow](Nvidia_Flow_TOP.html "Nvidia Flow TOP") • [Nvidia Upscaler](Nvidia_Upscaler_TOP.html "Nvidia Upscaler TOP") • [OAK Select](OAK_Select_TOP.html "OAK Select TOP") • [Oculus Rift](Oculus_Rift_TOP.html "Oculus Rift TOP") • [OP Viewer](OP_Viewer_TOP.html "OP Viewer TOP") • [OpenColorIO](OpenColorIO_TOP.html "OpenColorIO TOP") • [OpenVR](OpenVR_TOP.html "OpenVR TOP") • [Optical Flow](Optical_Flow_TOP.html "Optical Flow TOP") • [Orbbec Select](Orbbec_Select_TOP.html "Orbbec Select TOP") • [Orbbec](Orbbec_TOP.html "Orbbec TOP") • [Ouster Select](Ouster_Select_TOP.html "Ouster Select TOP") • [Ouster](Ouster_TOP.html "Ouster TOP") • [Out](Out_TOP.html "Out TOP") • [Outside](Outside_TOP.html "Outside TOP") • [Over](Over_TOP.html "Over TOP") • [Pack](Pack_TOP.html "Pack TOP") • [Photoshop In](Photoshop_In_TOP.html "Photoshop In TOP") • [Point File In](Point_File_In_TOP.html "Point File In TOP") • [Point File Select](Point_File_Select_TOP.html "Point File Select TOP") • [Point Transform](Point_Transform_TOP.html "Point Transform TOP") • [PreFilter Map](PreFilter_Map_TOP.html "PreFilter Map TOP") • [Projection](Projection_TOP.html "Projection TOP") • [Ramp](Ramp_TOP.html "Ramp TOP") • [RealSense](RealSense_TOP.html "RealSense TOP") • [Rectangle](Rectangle_TOP.html "Rectangle TOP") • [Remap](Remap_TOP.html "Remap TOP") • [Render Pass](Render_Pass_TOP.html "Render Pass TOP") • [Render Select](Render_Select_TOP.html "Render Select TOP") • [Render](Render_TOP.html "Render TOP") • [RenderStream In](RenderStream_In_TOP.html "RenderStream In TOP") • [RenderStream Out](RenderStream_Out_TOP.html "RenderStream Out TOP") • [Reorder](Reorder_TOP.html "Reorder TOP") • [Resolution](Resolution_TOP.html "Resolution TOP") • [RGB Key](RGB_Key_TOP.html "RGB Key TOP") • [RGB to HSV](RGB_to_HSV_TOP.html "RGB to HSV TOP") • [Scalable Display](Scalable_Display_TOP.html "Scalable Display TOP") • [Screen Grab](Screen_Grab_TOP.html "Screen Grab TOP") • [Screen](Screen_TOP.html "Screen TOP") • [Script](Script_TOP.html "Script TOP") • [Select](Select_TOP.html "Select TOP") • [Shared Mem In](Shared_Mem_In_TOP.html "Shared Mem In TOP") • [Shared Mem Out](Shared_Mem_Out_TOP.html "Shared Mem Out TOP") • [SICK](SICK_TOP.html "SICK TOP") • [Slope](Slope_TOP.html "Slope TOP") • [Spectrum](Spectrum_TOP.html "Spectrum TOP") • [SSAO](SSAO_TOP.html "SSAO TOP") • [Stype](Stype_TOP.html "Stype TOP") • [Substance Select](Substance_Select_TOP.html "Substance Select TOP") • [Substance](Substance_TOP.html "Substance TOP") • [Subtract](Subtract_TOP.html "Subtract TOP") • [SVG](SVG_TOP.html "SVG TOP") • [Switch](Switch_TOP.html "Switch TOP") • [Syphon Spout In](Syphon_Spout_In_TOP.html "Syphon Spout In TOP") • [Syphon Spout Out](Syphon_Spout_Out_TOP.html "Syphon Spout Out TOP") • [Text](Text_TOP.html "Text TOP") • [Texture 3D](Texture_3D_TOP.html "Texture 3D TOP") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Threshold](Threshold_TOP.html "Threshold TOP") • [Tile](Tile_TOP.html "Tile TOP") • [Time Machine](Time_Machine_TOP.html "Time Machine TOP") • [TOP](TOP.html "TOP") • [Experimental:TOP](Experimental_TOP.html "Experimental:TOP") • [TOP Viewer](TOP_Viewer.html "TOP Viewer") • [Touch In](Touch_In_TOP.html "Touch In TOP") • [Touch Out](Touch_Out_TOP.html "Touch Out TOP") • [Transform](Transform_TOP.html "Transform TOP") • [Under](Under_TOP.html "Under TOP") • [Video Device In](Video_Device_In_TOP.html "Video Device In TOP") • [Video Device Out](Video_Device_Out_TOP.html "Video Device Out TOP") • [Video Stream In](Video_Stream_In_TOP.html "Video Stream In TOP") • [Video Stream Out](Video_Stream_Out_TOP.html "Video Stream Out TOP") • [Vioso](Vioso_TOP.html "Vioso TOP") • [Web Render](Web_Render_TOP.html "Web Render TOP") • [Experimental:ZED Select](Experimental_ZED_Select_TOP.html "Experimental:ZED Select TOP") • [ZED](ZED_TOP.html "ZED TOP") • [Experimental:ZED](Experimental_ZED_TOP.html "Experimental:ZED TOP") |
An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

The OpenGL (pre-2022) or Vulkan (2022-) code that runs on the GPU and creates rendered images from polygons and textures. A shader is programmed in [Text DATs](Text_DAT.html "Text DAT") and referenced by a [GLSL Material](GLSL_MAT.html "GLSL MAT") or a [GLSL TOP](GLSL_TOP.html "GLSL TOP"). Shaders are composed of up to three parts: Vertex Shader, Pixel Shader and Compute Shader.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP") can set the image resolution. See [Aspect Ratio](TOP_Generator_Common_Page.html "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").

Retrieved from "<https://docs.derivative.ca/index.php?title=GLSL_Multi_TOP&oldid=32276>"
[Category](Special_Categories.html "Special:Categories"):
* [TOPs](Category_TOPs.html "Category:TOPs")