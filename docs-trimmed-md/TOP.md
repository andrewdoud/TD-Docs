

TOP - Derivative




# TOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
[![OP TOP.png](images/a/a9/OP_TOP.png)](File_OP_TOP.html)
See also [Category:TOPs](Category_TOPs.html "Category:TOPs") for a full list of articles related to TOPs.
**Texture Operators**, also known as **TOPs**, are image operators that provide real-time, GPU-based compositing and image manipulation. All calculations for TOPs are performed on the system's GPU. TOPs can be used for preparing textures, compositing streams images and movies, building control panel elements, manipulation of 32-bit floating point data, and almost any other image task you might have. TOPs support many formats, including floating-point image formats for working with high-dynamic range (HDR) images.
All renders and composites occur offscreen with TOPs. Data can be scaled to any resolution, limited only by the amount of graphics RAM and the maximum resolution of the graphics card.
TOPs that are being used to hold point cloud data, where R G B holds 32-bit X Y Z data can be viewed as a 3D set of points by right-clicking on the viewer and selecting View as Points.
**NOTE:** TouchDesigner Non-Commercial is limited to 1280x1280 resolution.
  

## Contents
* [1 Sweet 16 TOPs](#Sweet_16_TOPs)
* [2 TOP Flags](#TOP_Flags)
* [3 TOP Viewers](#TOP_Viewers)
* [4 Using TOPs](#Using_TOPs)
* [5 See also](#See_also)
## Sweet 16 TOPs[[edit](https://docs.derivative.ca/index.php?title=TOP&action=edit&section=1 "Edit section: Sweet 16 TOPs")]
The following 16 TOPs are commonly used, we recommend familiarizing yourself with them.
| TOP | Purpose | Related TOP |
| --- | --- | --- |
| [Movie File In](Movie_File_In_TOP.html "Movie File In TOP") | Read movies, still images, or a sequence of still images. | [Video Device In](Video_Device_In_TOP.html "Video Device In TOP"), [Movie File Out](Movie_File_Out_TOP.html "Movie File Out TOP") |
| [Ramp](Ramp_TOP.html "Ramp TOP") | Create vertical, horizontal, radial, and circular ramps. | [Constant](Constant_TOP.html "Constant TOP"), [Noise](Noise_TOP.html "Noise TOP") |
| [Level](Level_TOP.html "Level TOP") | Adjust contrast, brightness, gamma, black level, color range, opacity. | [Luma Level](Luma_Level_TOP.html "Luma Level TOP") |
| [Transform](Transform_TOP.html "Transform TOP") | Translate, scale, rotate, multi-repeat tile, background fill. | [Flip](Flip_TOP.html "Flip TOP") |
| [Over](Over_TOP.html "Over TOP") | Place and shift one image over another based on the alpha of one image. | [Cross](Cross_TOP.html "Cross TOP"), [Multiply](Multiply_TOP.html "Multiply TOP") |
| [Text](Text_TOP.html "Text TOP") | Text generation with variety of fonts. |  |
| [Blur](Blur_TOP.html "Blur TOP") | Blur. | [Luma Blur](Luma_Blur_TOP.html "Luma Blur TOP") |
| [Composite](Composite_TOP.html "Composite TOP") | Combine multiple images with variety of operations like under, difference. |  |
| [Render](Render_TOP.html "Render TOP") | Render 3D objects, lights and camera into an image. |  |
| [CHOP to](CHOP_to_TOP.html "CHOP to TOP") | Convert CHOP channels into scanlines of an image. |  |
| [Resolution](Resolution_TOP.html "Resolution TOP") | Change the resolution of an image and smooth-filter down. | all TOPs alter resolution |
| [Crop](Crop_TOP.html "Crop TOP") | Crop image to smaller resolution. | [Corner Pin](Corner_Pin_TOP.html "Corner Pin TOP"), [Fit](Fit_TOP.html "Fit TOP") |
| [Select](Select_TOP.html "Select TOP") | Selects an image from the same network or a different network. | [Switch](Switch_TOP.html "Switch TOP") |
| [Reorder](Reorder_TOP.html "Reorder TOP") | Re-order the channels of an image. | [Channel Mix](Channel_Mix_TOP.html "Channel Mix TOP") |
| [Cache](Cache_TOP.html "Cache TOP") | Hold a static or dynamic sequence of images and output one of them. | [Feedback](Feedback_TOP.html "Feedback TOP") |
| [Displace](Displace_TOP.html "Displace TOP") | Use red-blue of one image to warp another image. | [Time Machine](Time_Machine_TOP.html "Time Machine TOP") |
All TOPs are documented in the [Category:TOPs](Category_TOPs.html "Category:TOPs").
## TOP Flags[[edit](https://docs.derivative.ca/index.php?title=TOP&action=edit&section=2 "Edit section: TOP Flags")]
The lower right corner contains only 2 flags, the TOP’s [Display Flag](Display_Flag.html "Display Flag") and [Viewer Active Flag](Viewer_Active_Flag.html "Viewer Active Flag"). Turning on the display flag displays the TOP as a background in the current [Network Pane](Network_Editor.html "Network Editor"). Turning on multiple TOP Display Flags will display a tiled sequence of multiple TOP outputs as the background of the network pane.
  
[![TOPDisplaySingle.jpg](images/d/da/TOPDisplaySingle.jpg)](File_TOPDisplaySingle.html) [![TOPDisplayMulti.jpg](images/6/69/TOPDisplayMulti.jpg)](File_TOPDisplayMulti.html)
  

## TOP Viewers[[edit](https://docs.derivative.ca/index.php?title=TOP&action=edit&section=3 "Edit section: TOP Viewers")]
All TOP operators have interactive [Node Viewers](Node_Viewer.html "Node Viewer"). To interact with it, turn on the TOP's [Viewer Active Flag](Viewer_Active_Flag.html "Viewer Active Flag") to make the viewer active.
[![TOPviewer.jpg](images/b/bb/TOPviewer.jpg)](File_TOPviewer.html)
A gray checkerboard background will be displayed in images where an alpha channel is present. This can be turned off by opening [Preferences](Dialogs_Preferences_Dialog.html "Dialogs:Preferences Dialog") in the **Edit** menu. In preferences you can choose to use checkerboard or black as you alpha background.
Use [LMB](Mouse_Click.html "Mouse Click") to move the image around. Use [MMB](Mouse_Click.html "Mouse Click") to zoom in and out of the image. Re-center the image by using the home shortcut "**h**".
Clicking the [RMB](Mouse_Click.html "Mouse Click") will open the viewer options menu. Keyboard shortcuts are listed beside each entry in the menu.
[![TOPviewermenu.png](images/c/c1/TOPviewermenu.png)](File_TOPviewermenu.html)
**Home** - Re-centers and scales the image to fit in the viewer.
**Display Pixel Values** - Displays pixel information over the image. The [Timeline](Timeline.html "Timeline") should be playing forward for the values to properly update.
The following is displayed:
* cursor uv coordinates
* cursor xy pixel coordinates
* RGB values 0-255
* RGB values 0-1
**Display Field Guide** - Displays a 24x24 field guide over the image. The guide also displays the action safe zone and title safe zone for the image.
**Display Mode** - The display mode options give the option of viewing certain channels of the image.
The following display modes are available:
* Color - Display all RGB channles.
* Red/Green/Blue/Alpha - Display the Red/Green/Blue/Alpha channel respectively.
* Mono - Display the image in monochrome.
* Normalize Split - Displays each channel in the image at the same time normalized from 0-1. Excellent for viewing floating point and point cloud data.
**View as Points** - Displays the data in the TOP as 3D points for each pixel assuming red = x, green = y, and blue = z. Useful for viewing point cloud data.
[![PointCloudViews.png](images/thumb/c/cc/PointCloudViews.png/800px-PointCloudViews.png)](File_PointCloudViews.html)
Point cloud data displayed 3 modes: 1) Color 2) Normalized Split 3) View as Points
  

## Using TOPs[[edit](https://docs.derivative.ca/index.php?title=TOP&action=edit&section=4 "Edit section: Using TOPs")]
* 2D image data, everything processed on GPU, generators and filters, real-time compositing
* Import: Movie File In TOP, Video Device In TOP
* Export: right-click menu, Movie File Out TOP, Export Movie Dialog
## See also[[edit](https://docs.derivative.ca/index.php?title=TOP&action=edit&section=5 "Edit section: See also")]
[Category:TOPs](Category_TOPs.html "Category:TOPs")  
[Mipmapping](Mipmapping.html "Mipmapping") and [Texture Filtering](Texture_Filtering.html "Texture Filtering")  
[TOP Generator Common Page](TOP_Generator_Common_Page.html "TOP Generator Common Page") and [TOP Filter Common Page](TOP_Filter_Common_Page.html "TOP Filter Common Page")  
[Pixel Formats](Pixel_Formats.html "Pixel Formats")
  

| TOPs |
| --- |
| [Add](Add_TOP.html "Add TOP") • [Analyze](Analyze_TOP.html "Analyze TOP") • [Anti Alias](Anti_Alias_TOP.html "Anti Alias TOP") • [Blob Track](Blob_Track_TOP.html "Blob Track TOP") • [Bloom](Bloom_TOP.html "Bloom TOP") • [Blur](Blur_TOP.html "Blur TOP") • [Cache Select](Cache_Select_TOP.html "Cache Select TOP") • [Cache](Cache_TOP.html "Cache TOP") • [Channel Mix](Channel_Mix_TOP.html "Channel Mix TOP") • [CHOP to](CHOP_to_TOP.html "CHOP to TOP") • [Chroma Key](Chroma_Key_TOP.html "Chroma Key TOP") • [Circle](Circle_TOP.html "Circle TOP") • [Composite](Composite_TOP.html "Composite TOP") • [Constant](Constant_TOP.html "Constant TOP") • [Convolve](Convolve_TOP.html "Convolve TOP") • [Corner Pin](Corner_Pin_TOP.html "Corner Pin TOP") • [CPlusPlus](CPlusPlus_TOP.html "CPlusPlus TOP") • [Crop](Crop_TOP.html "Crop TOP") • [Cross](Cross_TOP.html "Cross TOP") • [Cube Map](Cube_Map_TOP.html "Cube Map TOP") • [Depth](Depth_TOP.html "Depth TOP") • [Difference](Difference_TOP.html "Difference TOP") • [Direct Display Out](Direct_Display_Out_TOP.html "Direct Display Out TOP") • [DirectX In](DirectX_In_TOP.html "DirectX In TOP") • [DirectX Out](DirectX_Out_TOP.html "DirectX Out TOP") • [Displace](Displace_TOP.html "Displace TOP") • [Edge](Edge_TOP.html "Edge TOP") • [Emboss](Emboss_TOP.html "Emboss TOP") • [Feedback](Feedback_TOP.html "Feedback TOP") • [Fit](Fit_TOP.html "Fit TOP") • [Flip](Flip_TOP.html "Flip TOP") • [Function](Function_TOP.html "Function TOP") • [GLSL Multi](GLSL_Multi_TOP.html "GLSL Multi TOP") • [GLSL](GLSL_TOP.html "GLSL TOP") • [HSV Adjust](HSV_Adjust_TOP.html "HSV Adjust TOP") • [HSV to RGB](HSV_to_RGB_TOP.html "HSV to RGB TOP") • [Import Select](Import_Select_TOP.html "Import Select TOP") • [In](In_TOP.html "In TOP") • [Inside](Inside_TOP.html "Inside TOP") • [Introduction To s Vid](Introduction_To_TOPs_Vid.html "Introduction To TOPs Vid") • [Kinect Azure Select](Kinect_Azure_Select_TOP.html "Kinect Azure Select TOP") • [Kinect Azure](Kinect_Azure_TOP.html "Kinect Azure TOP") • [Kinect](Kinect_TOP.html "Kinect TOP") • [Layout](Layout_TOP.html "Layout TOP") • [Leap Motion](Leap_Motion_TOP.html "Leap Motion TOP") • [Lens Distort](Lens_Distort_TOP.html "Lens Distort TOP") • [Level](Level_TOP.html "Level TOP") • [Limit](Limit_TOP.html "Limit TOP") • [Lookup](Lookup_TOP.html "Lookup TOP") • [Luma Blur](Luma_Blur_TOP.html "Luma Blur TOP") • [Luma Level](Luma_Level_TOP.html "Luma Level TOP") • [Math](Math_TOP.html "Math TOP") • [Matte](Matte_TOP.html "Matte TOP") • [Mirror](Mirror_TOP.html "Mirror TOP") • [Monochrome](Monochrome_TOP.html "Monochrome TOP") • [MoSys](MoSys_TOP.html "MoSys TOP") • [Movie File In](Movie_File_In_TOP.html "Movie File In TOP") • [Movie File Out](Movie_File_Out_TOP.html "Movie File Out TOP") • [MPCDI](MPCDI_TOP.html "MPCDI TOP") • [Multiply](Multiply_TOP.html "Multiply TOP") • [Ncam](Ncam_TOP.html "Ncam TOP") • [NDI In](NDI_In_TOP.html "NDI In TOP") • [NDI Out](NDI_Out_TOP.html "NDI Out TOP") • [Noise](Noise_TOP.html "Noise TOP") • [Normal Map](Normal_Map_TOP.html "Normal Map TOP") • [Notch](Notch_TOP.html "Notch TOP") • [Null](Null_TOP.html "Null TOP") • [Nvidia Background](Nvidia_Background_TOP.html "Nvidia Background TOP") • [Nvidia Denoise](Nvidia_Denoise_TOP.html "Nvidia Denoise TOP") • [Nvidia Flex](Nvidia_Flex_TOP.html "Nvidia Flex TOP") • [Nvidia Flow](Nvidia_Flow_TOP.html "Nvidia Flow TOP") • [Nvidia Upscaler](Nvidia_Upscaler_TOP.html "Nvidia Upscaler TOP") • [OAK Select](OAK_Select_TOP.html "OAK Select TOP") • [Oculus Rift](Oculus_Rift_TOP.html "Oculus Rift TOP") • [OP Viewer](OP_Viewer_TOP.html "OP Viewer TOP") • [OpenColorIO](OpenColorIO_TOP.html "OpenColorIO TOP") • [OpenVR](OpenVR_TOP.html "OpenVR TOP") • [Optical Flow](Optical_Flow_TOP.html "Optical Flow TOP") • [Orbbec Select](Orbbec_Select_TOP.html "Orbbec Select TOP") • [Orbbec](Orbbec_TOP.html "Orbbec TOP") • [Ouster Select](Ouster_Select_TOP.html "Ouster Select TOP") • [Ouster](Ouster_TOP.html "Ouster TOP") • [Out](Out_TOP.html "Out TOP") • [Outside](Outside_TOP.html "Outside TOP") • [Over](Over_TOP.html "Over TOP") • [Pack](Pack_TOP.html "Pack TOP") • [Photoshop In](Photoshop_In_TOP.html "Photoshop In TOP") • [Point File In](Point_File_In_TOP.html "Point File In TOP") • [Point File Select](Point_File_Select_TOP.html "Point File Select TOP") • [Point Transform](Point_Transform_TOP.html "Point Transform TOP") • [PreFilter Map](PreFilter_Map_TOP.html "PreFilter Map TOP") • [Projection](Projection_TOP.html "Projection TOP") • [Ramp](Ramp_TOP.html "Ramp TOP") • [RealSense](RealSense_TOP.html "RealSense TOP") • [Rectangle](Rectangle_TOP.html "Rectangle TOP") • [Remap](Remap_TOP.html "Remap TOP") • [Render Pass](Render_Pass_TOP.html "Render Pass TOP") • [Render Select](Render_Select_TOP.html "Render Select TOP") • [Render](Render_TOP.html "Render TOP") • [RenderStream In](RenderStream_In_TOP.html "RenderStream In TOP") • [RenderStream Out](RenderStream_Out_TOP.html "RenderStream Out TOP") • [Reorder](Reorder_TOP.html "Reorder TOP") • [Resolution](Resolution_TOP.html "Resolution TOP") • [RGB Key](RGB_Key_TOP.html "RGB Key TOP") • [RGB to HSV](RGB_to_HSV_TOP.html "RGB to HSV TOP") • [Scalable Display](Scalable_Display_TOP.html "Scalable Display TOP") • [Screen Grab](Screen_Grab_TOP.html "Screen Grab TOP") • [Screen](Screen_TOP.html "Screen TOP") • [Script](Script_TOP.html "Script TOP") • [Select](Select_TOP.html "Select TOP") • [Shared Mem In](Shared_Mem_In_TOP.html "Shared Mem In TOP") • [Shared Mem Out](Shared_Mem_Out_TOP.html "Shared Mem Out TOP") • [SICK](SICK_TOP.html "SICK TOP") • [Slope](Slope_TOP.html "Slope TOP") • [Spectrum](Spectrum_TOP.html "Spectrum TOP") • [SSAO](SSAO_TOP.html "SSAO TOP") • [Stype](Stype_TOP.html "Stype TOP") • [Substance Select](Substance_Select_TOP.html "Substance Select TOP") • [Substance](Substance_TOP.html "Substance TOP") • [Subtract](Subtract_TOP.html "Subtract TOP") • [SVG](SVG_TOP.html "SVG TOP") • [Switch](Switch_TOP.html "Switch TOP") • [Syphon Spout In](Syphon_Spout_In_TOP.html "Syphon Spout In TOP") • [Syphon Spout Out](Syphon_Spout_Out_TOP.html "Syphon Spout Out TOP") • [Text](Text_TOP.html "Text TOP") • [Texture 3D](Texture_3D_TOP.html "Texture 3D TOP") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Threshold](Threshold_TOP.html "Threshold TOP") • [Tile](Tile_TOP.html "Tile TOP") • [Time Machine](Time_Machine_TOP.html "Time Machine TOP") • TOP• [Experimental:TOP](Experimental_TOP.html "Experimental:TOP") • [TOP Viewer](TOP_Viewer.html "TOP Viewer") • [Touch In](Touch_In_TOP.html "Touch In TOP") • [Touch Out](Touch_Out_TOP.html "Touch Out TOP") • [Transform](Transform_TOP.html "Transform TOP") • [Under](Under_TOP.html "Under TOP") • [Video Device In](Video_Device_In_TOP.html "Video Device In TOP") • [Video Device Out](Video_Device_Out_TOP.html "Video Device Out TOP") • [Video Stream In](Video_Stream_In_TOP.html "Video Stream In TOP") • [Video Stream Out](Video_Stream_Out_TOP.html "Video Stream Out TOP") • [Vioso](Vioso_TOP.html "Vioso TOP") • [Web Render](Web_Render_TOP.html "Web Render TOP") • [Experimental:ZED Select](Experimental_ZED_Select_TOP.html "Experimental:ZED Select TOP") • [ZED](ZED_TOP.html "ZED TOP") • [Experimental:ZED](Experimental_ZED_TOP.html "Experimental:ZED TOP") |
The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

Any floating window that is not a [Pane](Pane.html "Pane") or [Viewer](Viewer.html "Viewer").

Retrieved from "<https://docs.derivative.ca/index.php?title=TOP&oldid=32538>"
[Categories](Special_Categories.html "Special:Categories"):
* [Touch Glossary](Category_Touch_Glossary.html "Category:Touch Glossary")
* [TOPs](Category_TOPs.html "Category:TOPs")