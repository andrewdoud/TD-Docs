

Resolution TOP - TouchDesigner Documentation






























# Resolution TOP

From Derivative
Revision as of 18:11, 29 May 2018 by [Greg](https://docs.derivative.ca/User:Greg "User:Greg") ([talk](https://docs.derivative.ca/index.php?title=User_talk:Greg&action=edit&redlink=1 "User talk:Greg (page does not exist)") | [contribs](https://docs.derivative.ca/Special:Contributions/Greg "Special:Contributions/Greg"))([diff](https://docs.derivative.ca/index.php?title=Resolution_TOP&diff=prev&oldid=11772 "Resolution TOP")) [← Older revision](https://docs.derivative.ca/index.php?title=Resolution_TOP&direction=prev&oldid=11772 "Resolution TOP") | [Latest revision](https://docs.derivative.ca/Resolution_TOP "Resolution TOP") ([diff](https://docs.derivative.ca/index.php?title=Resolution_TOP&diff=cur&oldid=11772 "Resolution TOP")) | [Newer revision →](https://docs.derivative.ca/index.php?title=Resolution_TOP&direction=next&oldid=11772 "Resolution TOP") ([diff](https://docs.derivative.ca/index.php?title=Resolution_TOP&diff=next&oldid=11772 "Resolution TOP"))


[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

  


* Invalid title: ""

## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Resolution TOP changes the resolution of the TOP image. This can also be done on the Common page of most other TOPs.

[![PythonIcon.png](https://docs.derivative.ca/images/c/c2/PythonIcon.png)](https://docs.derivative.ca/File:PythonIcon.png)[[{{{opClass}}}]]

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Parameters - Common Page](#Parameters_-_Common_Page)

  


## Parameters - Page

[Template:ParToggle](https://docs.derivative.ca/index.php?title=Template:ParToggle&action=edit&redlink=1 "Template:ParToggle (page does not exist)")

  


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

* Mipmap Pixels `mipmap` - Uses  [mipmap](https://docs.derivative.ca/Mipmapping "Mipmapping") filtering when scaling images. This can be used to reduce artifacts and sparkling in moving/scaling images that have lots of detail.

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

* Mipmap Pixels `mipmap` - Uses  [mipmap](https://docs.derivative.ca/Mipmapping "Mipmapping") filtering when scaling images. This can be used to reduce artifacts and sparkling in moving/scaling images that have lots of detail.

Passes `npasses` - Duplicates the operation of the TOP the specified number of times. Making this larger than 1 is essentially the same as taking the output from each pass, and passing it into the first input of the node and repeating the process. Other inputs and parameters remain the same for each pass.
Channel Mask `chanmask` - Allows you to choose which channels (R, G, B, or A) the TOP will operate on. All channels are selected by default.
Pixel Format `format` - ⊞ - Format used to store data for each channel in the image (ie. R, G, B, and A). Refer to [Pixel Formats](https://docs.derivative.ca/Pixel_Formats "Pixel Formats") for more information.

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

TouchDesigner Build: Latest\n2021.10000before 2021.10000

| TOPs |
| --- |
| [Add](https://docs.derivative.ca/Add_TOP "Add TOP") • [Analyze](https://docs.derivative.ca/Analyze_TOP "Analyze TOP") • [Anti Alias](https://docs.derivative.ca/Anti_Alias_TOP "Anti Alias TOP") • [Blob Track](https://docs.derivative.ca/Blob_Track_TOP "Blob Track TOP") • [Bloom](https://docs.derivative.ca/Bloom_TOP "Bloom TOP") • [Blur](https://docs.derivative.ca/Blur_TOP "Blur TOP") • [Cache Select](https://docs.derivative.ca/Cache_Select_TOP "Cache Select TOP") • [Cache](https://docs.derivative.ca/Cache_TOP "Cache TOP") • [Channel Mix](https://docs.derivative.ca/Channel_Mix_TOP "Channel Mix TOP") • [CHOP to](https://docs.derivative.ca/CHOP_to_TOP "CHOP to TOP") • [Chroma Key](https://docs.derivative.ca/Chroma_Key_TOP "Chroma Key TOP") • [Circle](https://docs.derivative.ca/Circle_TOP "Circle TOP") • [Composite](https://docs.derivative.ca/Composite_TOP "Composite TOP") • [Constant](https://docs.derivative.ca/Constant_TOP "Constant TOP") • [Convolve](https://docs.derivative.ca/Convolve_TOP "Convolve TOP") • [Corner Pin](https://docs.derivative.ca/Corner_Pin_TOP "Corner Pin TOP") • [Experimental:Corner Pin](https://docs.derivative.ca/Experimental:Corner_Pin_TOP "Experimental:Corner Pin TOP") • [CPlusPlus](https://docs.derivative.ca/CPlusPlus_TOP "CPlusPlus TOP") • [Crop](https://docs.derivative.ca/Crop_TOP "Crop TOP") • [Cross](https://docs.derivative.ca/Cross_TOP "Cross TOP") • [Cube Map](https://docs.derivative.ca/Cube_Map_TOP "Cube Map TOP") • [Depth](https://docs.derivative.ca/Depth_TOP "Depth TOP") • [Difference](https://docs.derivative.ca/Difference_TOP "Difference TOP") • [Direct Display Out](https://docs.derivative.ca/Direct_Display_Out_TOP "Direct Display Out TOP") • [DirectX In](https://docs.derivative.ca/DirectX_In_TOP "DirectX In TOP") • [DirectX Out](https://docs.derivative.ca/DirectX_Out_TOP "DirectX Out TOP") • [Displace](https://docs.derivative.ca/Displace_TOP "Displace TOP") • [Edge](https://docs.derivative.ca/Edge_TOP "Edge TOP") • [Emboss](https://docs.derivative.ca/Emboss_TOP "Emboss TOP") • [Feedback](https://docs.derivative.ca/Feedback_TOP "Feedback TOP") • [Fit](https://docs.derivative.ca/Fit_TOP "Fit TOP") • [Flip](https://docs.derivative.ca/Flip_TOP "Flip TOP") • [Function](https://docs.derivative.ca/Function_TOP "Function TOP") • [GLSL Multi](https://docs.derivative.ca/GLSL_Multi_TOP "GLSL Multi TOP") • [GLSL](https://docs.derivative.ca/GLSL_TOP "GLSL TOP") • [Experimental:GLSL](https://docs.derivative.ca/Experimental:GLSL_TOP "Experimental:GLSL TOP") • [HSV Adjust](https://docs.derivative.ca/HSV_Adjust_TOP "HSV Adjust TOP") • [HSV to RGB](https://docs.derivative.ca/HSV_to_RGB_TOP "HSV to RGB TOP") • [Import Select](https://docs.derivative.ca/Import_Select_TOP "Import Select TOP") • [In](https://docs.derivative.ca/In_TOP "In TOP") • [Inside](https://docs.derivative.ca/Inside_TOP "Inside TOP") • [Introduction To s Vid](https://docs.derivative.ca/Introduction_To_TOPs_Vid "Introduction To TOPs Vid") • [Kinect Azure Select](https://docs.derivative.ca/Kinect_Azure_Select_TOP "Kinect Azure Select TOP") • [Kinect Azure](https://docs.derivative.ca/Kinect_Azure_TOP "Kinect Azure TOP") • [Kinect](https://docs.derivative.ca/Kinect_TOP "Kinect TOP") • [Layout](https://docs.derivative.ca/Layout_TOP "Layout TOP") • [Leap Motion](https://docs.derivative.ca/Leap_Motion_TOP "Leap Motion TOP") • [Lens Distort](https://docs.derivative.ca/Lens_Distort_TOP "Lens Distort TOP") • [Level](https://docs.derivative.ca/Level_TOP "Level TOP") • [Limit](https://docs.derivative.ca/Limit_TOP "Limit TOP") • [Lookup](https://docs.derivative.ca/Lookup_TOP "Lookup TOP") • [Luma Blur](https://docs.derivative.ca/Luma_Blur_TOP "Luma Blur TOP") • [Luma Level](https://docs.derivative.ca/Luma_Level_TOP "Luma Level TOP") • [Math](https://docs.derivative.ca/Math_TOP "Math TOP") • [Matte](https://docs.derivative.ca/Matte_TOP "Matte TOP") • [Mirror](https://docs.derivative.ca/Mirror_TOP "Mirror TOP") • [Monochrome](https://docs.derivative.ca/Monochrome_TOP "Monochrome TOP") • [MoSys](https://docs.derivative.ca/MoSys_TOP "MoSys TOP") • [Movie File In](https://docs.derivative.ca/Movie_File_In_TOP "Movie File In TOP") • [Movie File Out](https://docs.derivative.ca/Movie_File_Out_TOP "Movie File Out TOP") • [Experimental:Movie File Out](https://docs.derivative.ca/Experimental:Movie_File_Out_TOP "Experimental:Movie File Out TOP") • [MPCDI](https://docs.derivative.ca/MPCDI_TOP "MPCDI TOP") • [Multiply](https://docs.derivative.ca/Multiply_TOP "Multiply TOP") • [Ncam](https://docs.derivative.ca/Ncam_TOP "Ncam TOP") • [NDI In](https://docs.derivative.ca/NDI_In_TOP "NDI In TOP") • [NDI Out](https://docs.derivative.ca/NDI_Out_TOP "NDI Out TOP") • [Noise](https://docs.derivative.ca/Noise_TOP "Noise TOP") • [Experimental:Noise](https://docs.derivative.ca/Experimental:Noise_TOP "Experimental:Noise TOP") • [Normal Map](https://docs.derivative.ca/Normal_Map_TOP "Normal Map TOP") • [Notch](https://docs.derivative.ca/Notch_TOP "Notch TOP") • [Null](https://docs.derivative.ca/Null_TOP "Null TOP") • [Nvidia Background](https://docs.derivative.ca/Nvidia_Background_TOP "Nvidia Background TOP") • [Nvidia Denoise](https://docs.derivative.ca/Nvidia_Denoise_TOP "Nvidia Denoise TOP") • [Nvidia Flex](https://docs.derivative.ca/Nvidia_Flex_TOP "Nvidia Flex TOP") • [Nvidia Flow](https://docs.derivative.ca/Nvidia_Flow_TOP "Nvidia Flow TOP") • [Nvidia Upscaler](https://docs.derivative.ca/Nvidia_Upscaler_TOP "Nvidia Upscaler TOP") • [OAK Select](https://docs.derivative.ca/OAK_Select_TOP "OAK Select TOP") • [Oculus Rift](https://docs.derivative.ca/Oculus_Rift_TOP "Oculus Rift TOP") • [OP Viewer](https://docs.derivative.ca/OP_Viewer_TOP "OP Viewer TOP") • [OpenColorIO](https://docs.derivative.ca/OpenColorIO_TOP "OpenColorIO TOP") • [OpenVR](https://docs.derivative.ca/OpenVR_TOP "OpenVR TOP") • [Optical Flow](https://docs.derivative.ca/Optical_Flow_TOP "Optical Flow TOP") • [Orbbec Select](https://docs.derivative.ca/Orbbec_Select_TOP "Orbbec Select TOP") • [Orbbec](https://docs.derivative.ca/Orbbec_TOP "Orbbec TOP") • [Ouster Select](https://docs.derivative.ca/Ouster_Select_TOP "Ouster Select TOP") • [Ouster](https://docs.derivative.ca/Ouster_TOP "Ouster TOP") • [Out](https://docs.derivative.ca/Out_TOP "Out TOP") • [Outside](https://docs.derivative.ca/Outside_TOP "Outside TOP") • [Over](https://docs.derivative.ca/Over_TOP "Over TOP") • [Pack](https://docs.derivative.ca/Pack_TOP "Pack TOP") • [Photoshop In](https://docs.derivative.ca/Photoshop_In_TOP "Photoshop In TOP") • [Point File In](https://docs.derivative.ca/Point_File_In_TOP "Point File In TOP") • [Point File Select](https://docs.derivative.ca/Point_File_Select_TOP "Point File Select TOP") • [Point Transform](https://docs.derivative.ca/Point_Transform_TOP "Point Transform TOP") • [Experimental:POP to](https://docs.derivative.ca/Experimental:POP_to_TOP "Experimental:POP to TOP") • [PreFilter Map](https://docs.derivative.ca/PreFilter_Map_TOP "PreFilter Map TOP") • [Projection](https://docs.derivative.ca/Projection_TOP "Projection TOP") • [Ramp](https://docs.derivative.ca/Ramp_TOP "Ramp TOP") • [RealSense](https://docs.derivative.ca/RealSense_TOP "RealSense TOP") • [Rectangle](https://docs.derivative.ca/Rectangle_TOP "Rectangle TOP") • [Remap](https://docs.derivative.ca/Remap_TOP "Remap TOP") • [Render Pass](https://docs.derivative.ca/Render_Pass_TOP "Render Pass TOP") • [Render Select](https://docs.derivative.ca/Render_Select_TOP "Render Select TOP") • [Render](https://docs.derivative.ca/Render_TOP "Render TOP") • [RenderStream In](https://docs.derivative.ca/RenderStream_In_TOP "RenderStream In TOP") • [RenderStream Out](https://docs.derivative.ca/RenderStream_Out_TOP "RenderStream Out TOP") • [Reorder](https://docs.derivative.ca/Reorder_TOP "Reorder TOP") • Resolution• [RGB Key](https://docs.derivative.ca/RGB_Key_TOP "RGB Key TOP") • [RGB to HSV](https://docs.derivative.ca/RGB_to_HSV_TOP "RGB to HSV TOP") • [Scalable Display](https://docs.derivative.ca/Scalable_Display_TOP "Scalable Display TOP") • [Screen Grab](https://docs.derivative.ca/Screen_Grab_TOP "Screen Grab TOP") • [Screen](https://docs.derivative.ca/Screen_TOP "Screen TOP") • [Script](https://docs.derivative.ca/Script_TOP "Script TOP") • [Experimental:Script](https://docs.derivative.ca/Experimental:Script_TOP "Experimental:Script TOP") • [Select](https://docs.derivative.ca/Select_TOP "Select TOP") • [Shared Mem In](https://docs.derivative.ca/Shared_Mem_In_TOP "Shared Mem In TOP") • [Shared Mem Out](https://docs.derivative.ca/Shared_Mem_Out_TOP "Shared Mem Out TOP") • [SICK](https://docs.derivative.ca/SICK_TOP "SICK TOP") • [Slope](https://docs.derivative.ca/Slope_TOP "Slope TOP") • [Spectrum](https://docs.derivative.ca/Spectrum_TOP "Spectrum TOP") • [SSAO](https://docs.derivative.ca/SSAO_TOP "SSAO TOP") • [Experimental:ST2110 In](https://docs.derivative.ca/Experimental:ST2110_In_TOP "Experimental:ST2110 In TOP") • [Experimental:ST2110 Out](https://docs.derivative.ca/Experimental:ST2110_Out_TOP "Experimental:ST2110 Out TOP") • [Stype](https://docs.derivative.ca/Stype_TOP "Stype TOP") • [Substance Select](https://docs.derivative.ca/Substance_Select_TOP "Substance Select TOP") • [Substance](https://docs.derivative.ca/Substance_TOP "Substance TOP") • [Subtract](https://docs.derivative.ca/Subtract_TOP "Subtract TOP") • [SVG](https://docs.derivative.ca/SVG_TOP "SVG TOP") • [Switch](https://docs.derivative.ca/Switch_TOP "Switch TOP") • [Syphon Spout In](https://docs.derivative.ca/Syphon_Spout_In_TOP "Syphon Spout In TOP") • [Syphon Spout Out](https://docs.derivative.ca/Syphon_Spout_Out_TOP "Syphon Spout Out TOP") • [Text](https://docs.derivative.ca/Text_TOP "Text TOP") • [Texture 3D](https://docs.derivative.ca/Texture_3D_TOP "Texture 3D TOP") • [Texture Sampling Parameters](https://docs.derivative.ca/Texture_Sampling_Parameters "Texture Sampling Parameters") • [Threshold](https://docs.derivative.ca/Threshold_TOP "Threshold TOP") • [Tile](https://docs.derivative.ca/Tile_TOP "Tile TOP") • [Time Machine](https://docs.derivative.ca/Time_Machine_TOP "Time Machine TOP") • [TOP](https://docs.derivative.ca/TOP "TOP") • [Experimental:TOP](https://docs.derivative.ca/Experimental:TOP "Experimental:TOP") • [TOP Viewer](https://docs.derivative.ca/TOP_Viewer "TOP Viewer") • [Touch In](https://docs.derivative.ca/Touch_In_TOP "Touch In TOP") • [Touch Out](https://docs.derivative.ca/Touch_Out_TOP "Touch Out TOP") • [Transform](https://docs.derivative.ca/Transform_TOP "Transform TOP") • [Under](https://docs.derivative.ca/Under_TOP "Under TOP") • [Video Device In](https://docs.derivative.ca/Video_Device_In_TOP "Video Device In TOP") • [Video Device Out](https://docs.derivative.ca/Video_Device_Out_TOP "Video Device Out TOP") • [Video Stream In](https://docs.derivative.ca/Video_Stream_In_TOP "Video Stream In TOP") • [Video Stream Out](https://docs.derivative.ca/Video_Stream_Out_TOP "Video Stream Out TOP") • [Vioso](https://docs.derivative.ca/Vioso_TOP "Vioso TOP") • [Web Render](https://docs.derivative.ca/Web_Render_TOP "Web Render TOP") • [Experimental:ZED Select](https://docs.derivative.ca/Experimental:ZED_Select_TOP "Experimental:ZED Select TOP") • [ZED](https://docs.derivative.ca/ZED_TOP "ZED TOP") • [Experimental:ZED](https://docs.derivative.ca/Experimental:ZED_TOP "Experimental:ZED TOP") |

The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](https://docs.derivative.ca/Movie_File_In_TOP "Movie File In TOP") can set the image resolution. See [Aspect Ratio](https://docs.derivative.ca/TOP_Generator_Common_Page "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.


An [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


The viewer of a node can be (1) the interior of a node (the [Node Viewer](https://docs.derivative.ca/Node_Viewer "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](https://docs.derivative.ca/Pane "Pane") that graphically shows the results of an operator.


A [CHOP](https://docs.derivative.ca/CHOP "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](https://docs.derivative.ca/Sample "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](https://docs.derivative.ca/Export "Export") to [Parameters](https://docs.derivative.ca/Parameter "Parameter").







Retrieved from "<https://docs.derivative.ca/index.php?title=Resolution_TOP&oldid=11772>"
[Categories](https://docs.derivative.ca/Special:Categories "Special:Categories"):

* [Touch Glossary](https://docs.derivative.ca/Category:Touch_Glossary "Category:Touch Glossary")
* [TOPs](https://docs.derivative.ca/Category:TOPs "Category:TOPs")