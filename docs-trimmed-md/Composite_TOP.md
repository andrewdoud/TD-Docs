

Composite TOP - TouchDesigner Documentation





























# Composite TOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Composite TOP is a multi-input TOP that will perform a composite operation for each input. Select the composite operation using the Operation parameter on the Composite parameter page.

**Note:** See also the [blendModes component](Palette_blendModes.html "Palette:blendModes") in the Palette. Refer also to [OP Snippets](OP_Snippets.html "OP Snippets").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[compositeTOP\_Class](https://docs.derivative.ca/CompositeTOP_Class "CompositeTOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Composite Page](#Parameters_-_Composite_Page)
* [3 Parameters - Transform Page](#Parameters_-_Transform_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common TOP Info Channels](#Common_TOP_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Composite Page

TOP `top` - In addition to all the inputs attached, you can specify more using the TOPs listed in this field. Example: `ramp*` will composite all TOPs whose name starts with `ramp`.
Preview Grid `previewgrid` - This outputs an image showing the effect of all operation types in a grid, with the inputs swapped on the right side of each tile.
Select Input `selectinput` - Instead of doing the composites, this causes only one of the inputs to pass through.
Input Index `inputindex` - When passing through an input with Select Input on, this is the index of the image that is passed through.
Operation `operand` - ⊞ - Choose which composite operation is performed from this menu. Search the web for 'blend modes' for more detailed information on the effects of each type.

* Add `add` - input1.rgba + input2.rgba

* Atop `atop` - (input1.rgba \* input2.a) + (input2.rgba \* (1.0 - input1.a))

* Average `average` - (input1.rgba + input2.rgba)/2

* Brightest `brightest` -

* Burn Color `burncolor` -

* Burn Linear `burnlinear` -

* Chroma Difference `chromadifference` -

* Color `color` -

* Darker Color `darkercolor` -

* Difference `difference` - absoluteValue(input1.rgb - input2.rgb). Alpha always equals 1.0

* Dimmest `dimmest` -

* Divide `divide` - input1.rgba / input2.rgba

* Dodge `dodge` -

* Exclude `exclude` -

* Freeze `freeze` -

* Glow `glow` -

* Hard Light `hardlight` -

* Hard Mix `hardmix` -

* Heat `heat` -

* Hue `hue` -

* Inside `inside` - input1.rgba \* clamp(input2.a, 0.0, 1.0)

* Inside Luminance `insideluminance` -

* Inverse `inverse` -

* Lighter Color `lightercolor` -

* Luminance Difference `luminancedifference` -

* Maximum `maximum` - max(input1.r, input2.r), max(input1.g, input2.g), max(input1.b, input2.b), max(input1.a, input2.a)

* Minimum `minimum` - min(input1.r, input2.r), min(input1.g, input2.g), min(input1.b, input2.b), min(input1.a, input2.a)

* Multiply `multiply` -

* Negate `negate` -

* Outside `outside` - input1.rgba \* (1.0 - input2.a)

* Outside Luminance `outsideluminance` -

* Over `over` - (input2.rgba \* (1.0 - input1.a)) + input1.rgba

* Overlay `overlay` -

* Pinlight `pinlight` -

* Reflect `reflect` -

* Screen `screen` - 1.0 - ((1.0 - input1.rgba) \* (1.0 - input2.rgba))

* Soft Light `softlight` -

* Linear Light `linearlight` -

* Stencil Luminance `stencilluminance` -

* Subtract `subtract` - input1.rgba - input2.rgba

* Subtractive `subtractive` -

* Under `under` - (input1.rgba \* (1.0 - input2.a)) + input2.rgba

* Vivid Light `vividlight` -

* Xor `xor` - (input1.rgba \* (1.0 - input2.a)) + (input2.rgba \* (1.0 - input1.a))

* Y Film `yfilm` -

* Z Film `zfilm` -

Swap Operation Order `swaporder` - Swaps the order of the input pairs. A operation B is changed to B operation A. Operations like Add don't matter, but many do, like Over and Hard Light.

  


## Parameters - Transform Page

Fixed Layer `size` - ⊞ - The selected input will become the fixed layer and the other input will be the overlay. This does not change the order of the composite (Input1 + Input2), only which layer is considered fixed and which layer is adjustable by the parameters on the Transform page. The resolution and aspect ratio of the Fixed Layer is used as the composite's final resolution and aspect ratio unless manually on the [Common Page](#Parameters_-_Common_Page)

* Input 1 `input1` -

* Input 2 `input2` -

Pre-Fit Overlay `prefit` - ⊞ - Determines how the Overlay layer (Overlay layer is the input that is NOT the Fixed Layer) fills the composite.

* Fill `fill` - Overlay layer is stretched/squashed to fill the resolution and aspect ratio of the Fixed Layer.

* Fit Horizontal `fithorz` - Overlay layer is stretched/squashed to fit the Fixed Layer horizontally.

* Fit Vertical `fitvert` - Overlay layer is stretched/squashed to fit the Fixed Layer vertically.

* Fit Best `fitbest` - Overlay layer is stretch/squashed to fit the Fixed Layer using the best possible match that does not crop any of the Overlay layer. The aspect ratio of the Overlay is maintained.

* Fit Outside `fitoutside` - Overlay layer is stretched squashed to fit the Fixed Layer using the worst possible match. This is the opposite of Best Fit. The aspect ratio of the Overlay is maintained.

* Native Resolution `nativeres` - Overlay is not squashed or stretched. The Overlay layer uses its own resolution and aspect ratio during the composite. Pixel accurate composites require Native Resolution, use this setting for to maintain an image's original resolution during the composite.

Justify Horizontal `justifyh` - ⊞ - Specify the horizontal alignment of the Overlay.

* Left `left` - The Overlay is aligned to the left side of the Fixed Layer.

* Center `center` - The Overlay is centered in the Fixed Layer.

* Right `right` - The Overlay is aligned to the right side of the Fixed Layer.

Justify Vertical `justifyv` - ⊞ - Specify the vertical alignment of the Overlay.

* Bottom `bottom` - The Overlay is aligned to the bottom of the Fixed Layer.

* Center `center` - The Overlay is centered in the Fixed Layer.

* Top `top` - The Overlay is aligned to the top of the Fixed Layer.

Extend Overlay `extend` - ⊞ - Sets the extend (or repeat) conditions of the Overlay layer. This parameter determines what happens at the edges of the Overlay layer.

* Hold `hold` - The pixel values at the edges of the Overlay layer continue to extend past that edge.

* Zero `zero` - The image does not extend past the edges of the Overlay.

* Repeat `repeat` - The image is repeated at the edges of the Overlay.

* Mirror `mirror` - The image is mirrored at the edges of the Overlay.
> **NOTE:** All the transform parameters below affect the Overlay layer only.

Rotate `r` - Rotates the Overlay layer. Increasing values rotate clockwise, decreasing values rotate counter-clockwise.
Translate `t` - ⊞ - Translates the Overlay layer in x and y.

* X `tx` -

* Y `ty` -

Translate Units `tunit` - Sets the units used in the Translate parameter.
Scale `s` - ⊞ - Scales the Overlay layer in x and y.

* X `sx` -

* Y `sy` -

Pivot `p` - ⊞ - Allows you to define the point about which the Overlay layer scales and rotates. Altering the pivot point produces different results depending on the Transform Order.

* X `px` -

* Y `py` -

Pivot Units `punit` - Sets the units used in the Pivot parameter.
Translate Step `tstep` - ⊞ - Translates the Overlay layers cumulatively, starting at the 3rd input (index 2). That layer is translated by the amount specified, the next layer is translated by 2 times that amount, the following layer by 3 times that amount and so on.

* X `tstepx` -

* Y `tstepy` -

Translate Step Units `tstepunit` - Sets the units used in the Translate Step parameter
Legacy Transform `legacyxform` - When enabled, will use the legacy method of building the transform matrix, which has inverted rotation and transform order.

  


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

* Input 0:  -

  


## Info CHOP Channels

Extra Information for the Composite TOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\nwikieditorwikieditor2022.241402021.100002018.28070before 2018.28070

| TOPs |
| --- |
| [Add](Add_TOP.html "Add TOP") • [Analyze](Analyze_TOP.html "Analyze TOP") • [Anti Alias](Anti_Alias_TOP.html "Anti Alias TOP") • [Blob Track](Blob_Track_TOP.html "Blob Track TOP") • [Bloom](Bloom_TOP.html "Bloom TOP") • [Blur](Blur_TOP.html "Blur TOP") • [Cache Select](Cache_Select_TOP.html "Cache Select TOP") • [Cache](Cache_TOP.html "Cache TOP") • [Channel Mix](Channel_Mix_TOP.html "Channel Mix TOP") • [CHOP to](CHOP_to_TOP.html "CHOP to TOP") • [Chroma Key](Chroma_Key_TOP.html "Chroma Key TOP") • [Circle](Circle_TOP.html "Circle TOP") • Composite• [Constant](Constant_TOP.html "Constant TOP") • [Convolve](Convolve_TOP.html "Convolve TOP") • [Corner Pin](Corner_Pin_TOP.html "Corner Pin TOP") • [CPlusPlus](CPlusPlus_TOP.html "CPlusPlus TOP") • [Crop](Crop_TOP.html "Crop TOP") • [Cross](Cross_TOP.html "Cross TOP") • [Cube Map](Cube_Map_TOP.html "Cube Map TOP") • [Depth](Depth_TOP.html "Depth TOP") • [Difference](Difference_TOP.html "Difference TOP") • [Direct Display Out](Direct_Display_Out_TOP.html "Direct Display Out TOP") • [DirectX In](DirectX_In_TOP.html "DirectX In TOP") • [DirectX Out](DirectX_Out_TOP.html "DirectX Out TOP") • [Displace](Displace_TOP.html "Displace TOP") • [Edge](Edge_TOP.html "Edge TOP") • [Emboss](Emboss_TOP.html "Emboss TOP") • [Feedback](Feedback_TOP.html "Feedback TOP") • [Fit](Fit_TOP.html "Fit TOP") • [Flip](Flip_TOP.html "Flip TOP") • [Function](Function_TOP.html "Function TOP") • [GLSL Multi](GLSL_Multi_TOP.html "GLSL Multi TOP") • [GLSL](GLSL_TOP.html "GLSL TOP") • [HSV Adjust](HSV_Adjust_TOP.html "HSV Adjust TOP") • [HSV to RGB](HSV_to_RGB_TOP.html "HSV to RGB TOP") • [Import Select](Import_Select_TOP.html "Import Select TOP") • [In](In_TOP.html "In TOP") • [Inside](Inside_TOP.html "Inside TOP") • [Introduction To s Vid](Introduction_To_TOPs_Vid.html "Introduction To TOPs Vid") • [Kinect Azure Select](Kinect_Azure_Select_TOP.html "Kinect Azure Select TOP") • [Kinect Azure](Kinect_Azure_TOP.html "Kinect Azure TOP") • [Kinect](Kinect_TOP.html "Kinect TOP") • [Layout](Layout_TOP.html "Layout TOP") • [Leap Motion](Leap_Motion_TOP.html "Leap Motion TOP") • [Lens Distort](Lens_Distort_TOP.html "Lens Distort TOP") • [Level](Level_TOP.html "Level TOP") • [Limit](Limit_TOP.html "Limit TOP") • [Lookup](Lookup_TOP.html "Lookup TOP") • [Luma Blur](Luma_Blur_TOP.html "Luma Blur TOP") • [Luma Level](Luma_Level_TOP.html "Luma Level TOP") • [Math](Math_TOP.html "Math TOP") • [Matte](Matte_TOP.html "Matte TOP") • [Mirror](Mirror_TOP.html "Mirror TOP") • [Monochrome](Monochrome_TOP.html "Monochrome TOP") • [MoSys](MoSys_TOP.html "MoSys TOP") • [Movie File In](Movie_File_In_TOP.html "Movie File In TOP") • [Movie File Out](Movie_File_Out_TOP.html "Movie File Out TOP") • [MPCDI](MPCDI_TOP.html "MPCDI TOP") • [Multiply](Multiply_TOP.html "Multiply TOP") • [Ncam](Ncam_TOP.html "Ncam TOP") • [NDI In](NDI_In_TOP.html "NDI In TOP") • [NDI Out](NDI_Out_TOP.html "NDI Out TOP") • [Noise](Noise_TOP.html "Noise TOP") • [Normal Map](Normal_Map_TOP.html "Normal Map TOP") • [Notch](Notch_TOP.html "Notch TOP") • [Null](Null_TOP.html "Null TOP") • [Nvidia Background](Nvidia_Background_TOP.html "Nvidia Background TOP") • [Nvidia Denoise](Nvidia_Denoise_TOP.html "Nvidia Denoise TOP") • [Nvidia Flex](Nvidia_Flex_TOP.html "Nvidia Flex TOP") • [Nvidia Flow](Nvidia_Flow_TOP.html "Nvidia Flow TOP") • [Nvidia Upscaler](Nvidia_Upscaler_TOP.html "Nvidia Upscaler TOP") • [OAK Select](OAK_Select_TOP.html "OAK Select TOP") • [Oculus Rift](Oculus_Rift_TOP.html "Oculus Rift TOP") • [OP Viewer](OP_Viewer_TOP.html "OP Viewer TOP") • [OpenColorIO](OpenColorIO_TOP.html "OpenColorIO TOP") • [OpenVR](OpenVR_TOP.html "OpenVR TOP") • [Optical Flow](Optical_Flow_TOP.html "Optical Flow TOP") • [Orbbec Select](Orbbec_Select_TOP.html "Orbbec Select TOP") • [Orbbec](Orbbec_TOP.html "Orbbec TOP") • [Ouster Select](Ouster_Select_TOP.html "Ouster Select TOP") • [Ouster](Ouster_TOP.html "Ouster TOP") • [Out](Out_TOP.html "Out TOP") • [Outside](Outside_TOP.html "Outside TOP") • [Over](Over_TOP.html "Over TOP") • [Pack](Pack_TOP.html "Pack TOP") • [Photoshop In](Photoshop_In_TOP.html "Photoshop In TOP") • [Point File In](Point_File_In_TOP.html "Point File In TOP") • [Point File Select](Point_File_Select_TOP.html "Point File Select TOP") • [Point Transform](Point_Transform_TOP.html "Point Transform TOP") • [PreFilter Map](PreFilter_Map_TOP.html "PreFilter Map TOP") • [Projection](Projection_TOP.html "Projection TOP") • [Ramp](Ramp_TOP.html "Ramp TOP") • [RealSense](RealSense_TOP.html "RealSense TOP") • [Rectangle](Rectangle_TOP.html "Rectangle TOP") • [Remap](Remap_TOP.html "Remap TOP") • [Render Pass](Render_Pass_TOP.html "Render Pass TOP") • [Render Select](Render_Select_TOP.html "Render Select TOP") • [Render](Render_TOP.html "Render TOP") • [RenderStream In](RenderStream_In_TOP.html "RenderStream In TOP") • [RenderStream Out](RenderStream_Out_TOP.html "RenderStream Out TOP") • [Reorder](Reorder_TOP.html "Reorder TOP") • [Resolution](Resolution_TOP.html "Resolution TOP") • [RGB Key](RGB_Key_TOP.html "RGB Key TOP") • [RGB to HSV](RGB_to_HSV_TOP.html "RGB to HSV TOP") • [Scalable Display](Scalable_Display_TOP.html "Scalable Display TOP") • [Screen Grab](Screen_Grab_TOP.html "Screen Grab TOP") • [Screen](Screen_TOP.html "Screen TOP") • [Script](Script_TOP.html "Script TOP") • [Select](Select_TOP.html "Select TOP") • [Shared Mem In](Shared_Mem_In_TOP.html "Shared Mem In TOP") • [Shared Mem Out](Shared_Mem_Out_TOP.html "Shared Mem Out TOP") • [SICK](SICK_TOP.html "SICK TOP") • [Slope](Slope_TOP.html "Slope TOP") • [Spectrum](Spectrum_TOP.html "Spectrum TOP") • [SSAO](SSAO_TOP.html "SSAO TOP") • [Stype](Stype_TOP.html "Stype TOP") • [Substance Select](Substance_Select_TOP.html "Substance Select TOP") • [Substance](Substance_TOP.html "Substance TOP") • [Subtract](Subtract_TOP.html "Subtract TOP") • [SVG](SVG_TOP.html "SVG TOP") • [Switch](Switch_TOP.html "Switch TOP") • [Syphon Spout In](Syphon_Spout_In_TOP.html "Syphon Spout In TOP") • [Syphon Spout Out](Syphon_Spout_Out_TOP.html "Syphon Spout Out TOP") • [Text](Text_TOP.html "Text TOP") • [Texture 3D](Texture_3D_TOP.html "Texture 3D TOP") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Threshold](Threshold_TOP.html "Threshold TOP") • [Tile](Tile_TOP.html "Tile TOP") • [Time Machine](Time_Machine_TOP.html "Time Machine TOP") • [TOP](TOP.html "TOP") • [Experimental:TOP](Experimental_TOP.html "Experimental:TOP") • [TOP Viewer](TOP_Viewer.html "TOP Viewer") • [Touch In](Touch_In_TOP.html "Touch In TOP") • [Touch Out](Touch_Out_TOP.html "Touch Out TOP") • [Transform](Transform_TOP.html "Transform TOP") • [Under](Under_TOP.html "Under TOP") • [Video Device In](Video_Device_In_TOP.html "Video Device In TOP") • [Video Device Out](Video_Device_Out_TOP.html "Video Device Out TOP") • [Video Stream In](Video_Stream_In_TOP.html "Video Stream In TOP") • [Video Stream Out](Video_Stream_Out_TOP.html "Video Stream Out TOP") • [Vioso](Vioso_TOP.html "Vioso TOP") • [Web Render](Web_Render_TOP.html "Web Render TOP") • [Experimental:ZED Select](Experimental_ZED_Select_TOP.html "Experimental:ZED Select TOP") • [ZED](ZED_TOP.html "ZED TOP") • [Experimental:ZED](Experimental_ZED_TOP.html "Experimental:ZED TOP") |

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


A built-in panel in TouchDesigner that contains a library of components and media that can be dragged-dropped into a TouchDesigner network.


The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP") can set the image resolution. See [Aspect Ratio](TOP_Generator_Common_Page.html "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.


The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.


A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Composite_TOP&oldid=29677>"
[Category](Special_Categories.html "Special:Categories"):

* [TOPs](Category_TOPs.html "Category:TOPs")