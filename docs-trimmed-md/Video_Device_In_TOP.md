

Video Device In TOP - TouchDesigner Documentation




# Video Device In TOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Video Device In TOP can be used to capture video from an external camera, capture card, capture dongle, IP camera, or video decoder connected to the system. Multiple devices can simultaneously stream video into TouchDesigner by using multiple Device In TOPs. HD-SDI video can be streamed into TouchDesigner through capture cards such and those from [Blackmagic Design](Blackmagic_Design.html "Blackmagic Design"), [AJA](AJA.html "AJA") and [Deltacast](Deltacast.html "Deltacast").
[![Magewell.2.jpg](https://docs.derivative.ca/images/8/84/Magewell.2.jpg)](https://docs.derivative.ca/File:Magewell.2.jpg)
[![Webcam2.png](https://docs.derivative.ca/images/1/1c/Webcam2.png)](https://docs.derivative.ca/File:Webcam2.png)
[![CaptureCard.jpg](https://docs.derivative.ca/images/b/bd/CaptureCard.jpg)](https://docs.derivative.ca/File:CaptureCard.jpg)
[![DVcam.jpg](https://docs.derivative.ca/images/1/17/DVcam.jpg)](https://docs.derivative.ca/File:DVcam.jpg)
[![WebcamMan.jpg](https://docs.derivative.ca/images/4/4f/WebcamMan.jpg)](https://docs.derivative.ca/File:WebcamMan.jpg)
If the device does not seem to provide a video stream but it is visible in the Cameras parameter menu, make sure no other applications are currently using the device.
**TIP**: Create an [Info DAT](Info_DAT.html "Info DAT") and point it to the Video Device In TOP to see what devices are currently attached. The [Info CHOP](Info_CHOP.html "Info CHOP") gives data for analyzing the performance of Video Device In and Out TOPs. Additionally, the [Info CHOP](Info_CHOP.html "Info CHOP") can be used to obtain timecode embeded into the source signal on some device, as indicated in the below list.
Major capture devices vendors currently supported:
* [Blackmagic Design](Blackmagic_Design.html "Blackmagic Design") - Supports Timecode.
* [AJA](AJA.html "AJA") - Supports Timecode.
* [Deltacast](Deltacast.html "Deltacast") - Supports Timecode.
* [Bluefish444](Bluefish444.html "Bluefish444")
AJA and Blackmagic Design devices now support 12-bit input and output formats, including AJA’s ability to capture at a full 12-bit RGB 4:4:4. Furthermore, 10-bit input and output have received performance improvements and better support for a wider selection of firmware.
Also supported with native drivers are some models from Datapath SDI, Allied Vision, Imaging Development Systems (IDS), FLIR/Point Grey, and Ximea.
For Magewell HDMI-to-USB3 capture (highly recommended, no drivers, plug-and-play), see [Magewell](http://www.magewell.com/usb-capture-hdmi).
**IP Cameras** include models from [Allied Vision](https://www.alliedvision.com/en/products/cameras.html) (PvAPI SDK models only, not Vimba SDK), [Point Grey FLIR Flycapture2 and Spinnaker](https://www.ptgrey.com/) and [Imaging Development Systems (IDS)](https://en.ids-imaging.com/). In case of IDS's Cameras, TouchDesigner implements the *uEye IDS Software Suite*. *GigE Vision* cameras are currently not supported.
**USB3 Cameras** include models from [Allied Vision](https://www.alliedvision.com/en/products/cameras.html) (PvAPI SDK models only, not Vimba SDK), [Point Grey FLIR Flycapture2 and Spinnaker](https://www.ptgrey.com/) and [Imaging Development Systems (IDS)](https://en.ids-imaging.com/)
Only a small subset of cameras from each manufacturer has been tested in-house, however it's expected that any modern camera from the supported manufacturer should work. If any issues are encountered please contact `support@derivative.ca`.
See also [Video Device Out TOP](Video_Device_Out_TOP.html "Video Device Out TOP").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[videodeviceinTOP\_Class](VideodeviceinTOP_Class.html "VideodeviceinTOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Video In Page](#Parameters_-_Video_In_Page)
* [3 Parameters - Options Page](#Parameters_-_Options_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Specific Video Device In TOP Info Channels](#Specific_Video_Device_In_TOP_Info_Channels)
  + [5.2 Common TOP Info Channels](#Common_TOP_Info_Channels)
  + [5.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Video In Page
Active `active` - When set to one the TOP captures the image stream from the camera or decoder.
Driver `driver` - ⊞ - Selects the library to use to interface with the cameras.
* DirectShow (WDM) `directshow` -
* Media Foundation `mediafoundation` -
* Imaging Source - Not Supported `imagingsource` -
* DataPath (RGBEASY) `datapath` -
* Blackmagic `blackmagic` -
* Allied Vision (GigE) `alliedvisiongige` -
* Imaging Development Systems (IDS) `ids` -
* FLIR / Point Grey (FlyCapture2) `pointgreyflycapture` -
* FLIR / Point Grey (Spinnaker) `flirspinnaker` -
* AVFoundation (macOS) `avfoundation` -
* BlueFish444 `bluefish444` -
* AJA `aja` -
* Ximea `ximea` -
* Deltacast `deltacast` -
Device `device` - ⊞ - Select which camera or decoder you want from this menu.
* NDI Webcam Video 1 `V1` -
Specify IP `specifyip` - When using Allied Vision library allows you to specify the camera address by IP.
IP `ip` - The IP address used when Specify IP above is turned on.
Options `options` - Opens the options or control panel for the camera. NOTE: Only works when using DirectShow (WDM) cameras.
Deinterlace `deinterlace` - ⊞ - Sets which fields to capture.
* Off `off` - Captures all fields.
* Even `even` - Capture Even fields only.
* Odd `odd` - Captures Odd fields only.
* Bob (Split) `bob` - Alternatively shows the even then odd fields, resulting in twice the framerate being shown, and removing the interlacing artifacts.
Field Precedence `precedence` - ⊞ - When using Bob (Split) deinterlacing, this selects which field is shown first for each frame.
* Even `even` -
* Odd `odd` -
TV Channel `channel` - Selects the TV channel if a TV tuner is used as the video input.
Signal Format `signalformat` - The signal format to capture input at. This is the resolution and the frame rate, as well as if the frames are progressive or interlaced. Note that when using an interlaced format, the rate refers to fields per second.
Quad Link `quadlink` - Used for cards that support quad-link formats. Quad-link esstenially takes 4 inputs and creates one single larger input out of them, for example 4 1080p inputs become a single 4K input.
Input Pixel Format `inputpixelformat` - ⊞ - Some capture devices support pixel formats other than 8-bit. For supported devices (Blackmagic Design) this will make the node attempt to use that capability.
* 8-bit `fixed8` - 8-bit per channel precision.
* 10-bit `fixed10` - 10-bit per channel precision. The texture pixel format will be set to RGB10A2.
* 16-bit `fixed16` - 16-bit per channel precision. The texture pixel format will be set to RGBA16-Fixed.
* 12-bit `fixed12` -
Transfer Mode `transfermode` - ⊞ - Controls how the frames are transferred from the input device to CPU memory, and how they are transferred from CPU memory to the GPU.
* Automatic `automatic` - Will choose the best transfer mode for the components installed on the computer. In general this will be 'Pre-Upload'.
* Pre-Upload `preupload` - Upload the frames to the GPU as they arrived. This ensures the data is already in GPU memory when the GPU wants to process it.
* On-Demand `ondemand` - Only upload frames to the GPU if the TOP is going to display them for that cook. This reduces PCIe bandwidth between the GPU and CPU memory in cases where the TOP is showing less frames than what the input device is capturing. However this means the GPU may stall waiting for that frame to be uploaded.
* On-Demand, Sync to Frame Input `ondemandsync` - This mode is currently only available for [AJA](AJA.html "AJA") devices. This causes the whole TouchDesigner process to stall until right after a frame arrives on this input. Then the process will start executing and use that input frame for this nodes cook. This removes any latency from the capture input, but can result in worse performance. Real-time should turned off for the TouchDesigner process at the top of the UI, and only one node should be set to this mode in a single process.
Memory Mode `memorymode` - ⊞ - Controls the memory type used to transfer data between the capture card and the GPU.
* Automatic `automatic` - Will choose the best memory mode for the transfer. This will be 'Pinned' for capture cards that support it, and 'Regular' if not.
* Pinned `pinned` - Pinned memory allows data to be transferred in 2 copies instead of three. Capture->Pinned CPU Memory, Pinned CPU Memory->GPU Memory.
* Regular `regular` - The regular memory mode means 3 copies are required. Capture->Capture Writable Memory, Capture Writable Memory->GPU Readable Memory, GPU Readable Memory->GPU Memory.
Sync Inputs `syncinputs` - Enabling syncing of multiple Video Device In TOPs. Syncing allows multiple nodes using multiple inputs and capture cards on a single system to ensure they are outputting frames in sync. Without this each node will be free running and will possible be outputting frames that came it at different times due to internal queuing. It's important the input sources are GenLocked to ensure all of their data arrives to all of the inputs at the same time, otherwise syncing will not work. This feature is currently supported for Blackmagic, DataPath, Deltacast and BlueFish devices.
Sync Group Index `syncgroupindex` - There can be multiple sync groups active in a .toe file. Nodes will only sync to other nodes that are part of the same sync group.
Max Sync Offset (ms) `maxsyncoffset` - Specified in milliseconds. The maximum difference in time two image could have arrived at be considered in-sync. Images that arrive at times more different than this offset will be considered to be part of different 'frame'.
Sync Timeout (ms) `synctimeout` - How much time to wait for all frames in a sync group to become available before giving up trying to sync. Expressed in milliseconds. If this timeout elapses when waiting for a frame from one or more sources in the sync group, all of the nodes in the sync group will keep their current image and not output a new image, even if some new images arrived on some of the inputs.
Reset Stats `resetstats` - A pulse to reset the statistics in an attached [Info CHOP](Info_CHOP.html "Info CHOP").
  

## Parameters - Options Page
Currently all of these options are only available for [Ximea](https://docs.derivative.ca/index.php?title=Ximea&action=edit&redlink=1 "Ximea (page does not exist)") cameras.
Preset `preset` - ⊞ -
* Externally Configured `externallyconfigured` -
* Custom `custom` -
Auto Gain/Exposure `autoge` -
Auto Gain/Exposure Bias `autogebias` -
Auto Gain/Exposure Level `autogelevel` -
Max Gain `maxgain` -
Max Exposure (ms) `maxexposure` -
Gain `gain` -
Exposure (ms) `exposure` -
Chromaticity Gamma `cgamma` -
Luminosity Gamma `lgamma` -
Limit FPS `limitfps` -
FPS `limitedfps` -
Capture `capture` -
Capture Pulse `capturepulse` -
Auto White-Balance `autowb` -
White-Balance Coeffs `wbcoeffs` - ⊞ -
* White-Balance Coeffs `wbcoeffsr` -
* White-Balance Coeffs `wbcoeffsg` -
* White-Balance Coeffs `wbcoeffsb` -
Custom Bandwidth `custombandwidth` - ⊞ -
* Default `default` -
* On `on` -
* Off `off` -
Bandwidth Limit (Mb/s) `bandwidthlimit` -
Camera Bit Depth `camerabitdepth` - ⊞ -
* Automatic `automatic` -
* 8-Bit `8bit` -
* 10-Bit `10bit` -
* 12-Bit `12bit` -
GPU Demosaic `gpudemosaic` -
  

## Parameters - Common Page
Output Resolution `outputresolution` - ⊞ - quickly change the resolution of the TOP's data.
* Use Input `useinput` - Uses the input's resolution.
* Eighth `eighth` - Multiply the input's resolution by that amount.
* Quarter `quarter` - Multiply the input's resolution by that amount.
* Half `half` - Multiply the input's resolution by that amount.
* 2X `2x` - Multiply the input's resolution by that amount.
* 4X `4x` - Multiply the input's resolution by that amount.
* 8X `8x` - Multiply the input's resolution by that amount.
* Fit Resolution `fit` - Grow or shrink the input resolution to fit this resolution, while keeping the aspect ratio the same.
* Limit Resolution `limit` - Limit the input resolution to be not larger than this resolution, while keeping the aspect ratio the same.
* Custom Resolution `custom` - Directly control the width and height.
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
* Mipmap Pixels `mipmap` - Uses  [mipmap](Mipmapping.html "Mipmapping") filtering when scaling images. This can be used to reduce artifacts and sparkling in moving/scaling images that have lots of detail. When the input is 32-bit float format, only nearest filtering will be used (regardless of what is selected).
Passes `npasses` - Duplicates the operation of the TOP the specified number of times. For every pass after the first it takes the result of the previous pass and replaces the node's first input with the result of the previous pass. One exception to this is the [GLSL TOP](GLSL_TOP.html "GLSL TOP") when using compute shaders, where the input will continue to be the connected TOP's image.
Channel Mask `chanmask` - Allows you to choose which channels (R, G, B, or A) the TOP will operate on. All channels are selected by default.
Pixel Format `format` - ⊞ - Format used to store data for each channel in the image (ie. R, G, B, and A). Refer to [Pixel Formats](Pixel_Formats.html "Pixel Formats") for more information.
* Use Input `useinput` - Uses the input's pixel format.
* 8-bit fixed (RGBA) `rgba8fixed` - Uses 8-bit integer values for each channel.
* sRGB 8-bit fixed (RGBA) `srgba8fixed` - Uses 8-bit integer values for each channel and stores color in sRGB colorspace. Note that this does **not** apply an sRGB curve to the pixel values, it only stores them using an sRGB curve. This means more data is used for the darker values and less for the brighter values. When the values are read downstream they will be converted back to linear. For more information refer to [sRGB](https://docs.derivative.ca/SRGB "SRGB").
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
  

## Info CHOP Channels
Extra Information for the Video Device In TOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific Video Device In TOP Info Channels
* connected - 1 if the node is successfully connected to the device, 0 if not. This does not necessarily mean there is valid input coming to the device.
  

* sync\_timeouts - When using the 'Sync Group' feature, this counts how many times the group failed to all provide a frame with similar enough timestamps within the timeout period.
  

* last\_sync\_wait - How long the node had to wait from the time it was ready for a new frame until all the inputs provided valid frames for a synced output.
  

* odd\_field - When de-interlacing an interlaced input, this will be 1 when the odd field is being shown and 0 when the even field is being shown.
  

* capture\_fps - The calculated number of frames per second that are being captured by the device. This does **not** map directly to the signal format rate. It won't show 59.97 for example. This is simply a count of how many frames were captured in the last 1000ms.
  

* capture\_total - The total number of frames that have been captured this capture began.
  

* frames\_repeated - How many times the node has shown the same frame more than once. It does not currently correct for if the repeats are expected, such as when capturing a 30hz signal but TouchDesigner is running at 60fps. In that case the channel will keep increasing since each captured frame will be shown twice.
  

* frames\_dropped - This counts how many frames were captured by the card, but never consumed by TouchDesigner's reading thrad. This occurs if the capture is running faster than TouchDesigner is able to consume frames.
  

* frames\_skipped - This counts how many frames were consumed by TouchDesigner's reading thread, but never consumed by the node itself. This can occur if TouchDesigner isn't running at full frame rate.
  

* connection\_changes - Counts connection changes, not supported by all devices.
  

* temperature - On supported devices, outputs the temperature of the device in celsius. Will be a very negative number for devices that don't support it.
  

* signal\_fps - The actual signal format FPS of the input signal. 0 if unknown.
  

* rgb\_input - Will be 1 if the input is detected as an RGB (such as RGB 4:4:4 colorspace) format. 0 if it is a YUV based colorspace. -1 if it is unknown or not supported by the the library.
  

* frame\_queue\_length - The number of receieved frames queued inside TouchDesigner.
  

* frame\_hw\_queue\_length - The number of frames still queued on the device that TouchDesigner has not yet read.
  

* last\_dma\_copy\_time - The number of milliseconds it took to copy the last frame from the device to the CPU. -1 if this is not measured.
  

* frame\_timestamp - Time in seconds of the last frame displayed. -1 if this is not provided by the device.
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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditormw-rollback2022.241402021.100002020.200002018.28070before 2018.28070
| TOPs |
| --- |
| [Add](Add_TOP.html "Add TOP") • [Analyze](Analyze_TOP.html "Analyze TOP") • [Anti Alias](Anti_Alias_TOP.html "Anti Alias TOP") • [Blob Track](Blob_Track_TOP.html "Blob Track TOP") • [Bloom](Bloom_TOP.html "Bloom TOP") • [Blur](Blur_TOP.html "Blur TOP") • [Cache Select](Cache_Select_TOP.html "Cache Select TOP") • [Cache](Cache_TOP.html "Cache TOP") • [Channel Mix](Channel_Mix_TOP.html "Channel Mix TOP") • [CHOP to](CHOP_to_TOP.html "CHOP to TOP") • [Chroma Key](Chroma_Key_TOP.html "Chroma Key TOP") • [Circle](Circle_TOP.html "Circle TOP") • [Composite](Composite_TOP.html "Composite TOP") • [Constant](Constant_TOP.html "Constant TOP") • [Convolve](Convolve_TOP.html "Convolve TOP") • [Corner Pin](Corner_Pin_TOP.html "Corner Pin TOP") • [CPlusPlus](CPlusPlus_TOP.html "CPlusPlus TOP") • [Crop](Crop_TOP.html "Crop TOP") • [Cross](Cross_TOP.html "Cross TOP") • [Cube Map](Cube_Map_TOP.html "Cube Map TOP") • [Depth](Depth_TOP.html "Depth TOP") • [Difference](Difference_TOP.html "Difference TOP") • [Direct Display Out](Direct_Display_Out_TOP.html "Direct Display Out TOP") • [DirectX In](DirectX_In_TOP.html "DirectX In TOP") • [DirectX Out](DirectX_Out_TOP.html "DirectX Out TOP") • [Displace](Displace_TOP.html "Displace TOP") • [Edge](Edge_TOP.html "Edge TOP") • [Emboss](Emboss_TOP.html "Emboss TOP") • [Feedback](Feedback_TOP.html "Feedback TOP") • [Fit](Fit_TOP.html "Fit TOP") • [Flip](Flip_TOP.html "Flip TOP") • [Function](Function_TOP.html "Function TOP") • [GLSL Multi](GLSL_Multi_TOP.html "GLSL Multi TOP") • [GLSL](GLSL_TOP.html "GLSL TOP") • [HSV Adjust](HSV_Adjust_TOP.html "HSV Adjust TOP") • [HSV to RGB](HSV_to_RGB_TOP.html "HSV to RGB TOP") • [Import Select](Import_Select_TOP.html "Import Select TOP") • [In](In_TOP.html "In TOP") • [Inside](Inside_TOP.html "Inside TOP") • [Introduction To s Vid](Introduction_To_TOPs_Vid.html "Introduction To TOPs Vid") • [Kinect Azure Select](Kinect_Azure_Select_TOP.html "Kinect Azure Select TOP") • [Kinect Azure](Kinect_Azure_TOP.html "Kinect Azure TOP") • [Kinect](Kinect_TOP.html "Kinect TOP") • [Layout](Layout_TOP.html "Layout TOP") • [Leap Motion](Leap_Motion_TOP.html "Leap Motion TOP") • [Lens Distort](Lens_Distort_TOP.html "Lens Distort TOP") • [Level](Level_TOP.html "Level TOP") • [Limit](Limit_TOP.html "Limit TOP") • [Lookup](Lookup_TOP.html "Lookup TOP") • [Luma Blur](Luma_Blur_TOP.html "Luma Blur TOP") • [Luma Level](Luma_Level_TOP.html "Luma Level TOP") • [Math](Math_TOP.html "Math TOP") • [Matte](Matte_TOP.html "Matte TOP") • [Mirror](Mirror_TOP.html "Mirror TOP") • [Monochrome](Monochrome_TOP.html "Monochrome TOP") • [MoSys](MoSys_TOP.html "MoSys TOP") • [Movie File In](Movie_File_In_TOP.html "Movie File In TOP") • [Movie File Out](Movie_File_Out_TOP.html "Movie File Out TOP") • [MPCDI](MPCDI_TOP.html "MPCDI TOP") • [Multiply](Multiply_TOP.html "Multiply TOP") • [Ncam](Ncam_TOP.html "Ncam TOP") • [NDI In](NDI_In_TOP.html "NDI In TOP") • [NDI Out](NDI_Out_TOP.html "NDI Out TOP") • [Noise](Noise_TOP.html "Noise TOP") • [Normal Map](Normal_Map_TOP.html "Normal Map TOP") • [Notch](Notch_TOP.html "Notch TOP") • [Null](Null_TOP.html "Null TOP") • [Nvidia Background](Nvidia_Background_TOP.html "Nvidia Background TOP") • [Nvidia Denoise](Nvidia_Denoise_TOP.html "Nvidia Denoise TOP") • [Nvidia Flex](Nvidia_Flex_TOP.html "Nvidia Flex TOP") • [Nvidia Flow](Nvidia_Flow_TOP.html "Nvidia Flow TOP") • [Nvidia Upscaler](Nvidia_Upscaler_TOP.html "Nvidia Upscaler TOP") • [OAK Select](OAK_Select_TOP.html "OAK Select TOP") • [Oculus Rift](Oculus_Rift_TOP.html "Oculus Rift TOP") • [OP Viewer](OP_Viewer_TOP.html "OP Viewer TOP") • [OpenColorIO](OpenColorIO_TOP.html "OpenColorIO TOP") • [OpenVR](OpenVR_TOP.html "OpenVR TOP") • [Optical Flow](Optical_Flow_TOP.html "Optical Flow TOP") • [Orbbec Select](Orbbec_Select_TOP.html "Orbbec Select TOP") • [Orbbec](Orbbec_TOP.html "Orbbec TOP") • [Ouster Select](Ouster_Select_TOP.html "Ouster Select TOP") • [Ouster](Ouster_TOP.html "Ouster TOP") • [Out](Out_TOP.html "Out TOP") • [Outside](Outside_TOP.html "Outside TOP") • [Over](Over_TOP.html "Over TOP") • [Pack](Pack_TOP.html "Pack TOP") • [Photoshop In](Photoshop_In_TOP.html "Photoshop In TOP") • [Point File In](Point_File_In_TOP.html "Point File In TOP") • [Point File Select](Point_File_Select_TOP.html "Point File Select TOP") • [Point Transform](Point_Transform_TOP.html "Point Transform TOP") • [PreFilter Map](PreFilter_Map_TOP.html "PreFilter Map TOP") • [Projection](Projection_TOP.html "Projection TOP") • [Ramp](Ramp_TOP.html "Ramp TOP") • [RealSense](RealSense_TOP.html "RealSense TOP") • [Rectangle](Rectangle_TOP.html "Rectangle TOP") • [Remap](Remap_TOP.html "Remap TOP") • [Render Pass](Render_Pass_TOP.html "Render Pass TOP") • [Render Select](Render_Select_TOP.html "Render Select TOP") • [Render](Render_TOP.html "Render TOP") • [RenderStream In](RenderStream_In_TOP.html "RenderStream In TOP") • [RenderStream Out](RenderStream_Out_TOP.html "RenderStream Out TOP") • [Reorder](Reorder_TOP.html "Reorder TOP") • [Resolution](Resolution_TOP.html "Resolution TOP") • [RGB Key](RGB_Key_TOP.html "RGB Key TOP") • [RGB to HSV](RGB_to_HSV_TOP.html "RGB to HSV TOP") • [Scalable Display](Scalable_Display_TOP.html "Scalable Display TOP") • [Screen Grab](Screen_Grab_TOP.html "Screen Grab TOP") • [Screen](Screen_TOP.html "Screen TOP") • [Script](Script_TOP.html "Script TOP") • [Select](Select_TOP.html "Select TOP") • [Shared Mem In](Shared_Mem_In_TOP.html "Shared Mem In TOP") • [Shared Mem Out](Shared_Mem_Out_TOP.html "Shared Mem Out TOP") • [SICK](SICK_TOP.html "SICK TOP") • [Slope](Slope_TOP.html "Slope TOP") • [Spectrum](Spectrum_TOP.html "Spectrum TOP") • [SSAO](SSAO_TOP.html "SSAO TOP") • [Stype](Stype_TOP.html "Stype TOP") • [Substance Select](Substance_Select_TOP.html "Substance Select TOP") • [Substance](Substance_TOP.html "Substance TOP") • [Subtract](Subtract_TOP.html "Subtract TOP") • [SVG](SVG_TOP.html "SVG TOP") • [Switch](Switch_TOP.html "Switch TOP") • [Syphon Spout In](Syphon_Spout_In_TOP.html "Syphon Spout In TOP") • [Syphon Spout Out](Syphon_Spout_Out_TOP.html "Syphon Spout Out TOP") • [Text](Text_TOP.html "Text TOP") • [Texture 3D](Texture_3D_TOP.html "Texture 3D TOP") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Threshold](Threshold_TOP.html "Threshold TOP") • [Tile](Tile_TOP.html "Tile TOP") • [Time Machine](Time_Machine_TOP.html "Time Machine TOP") • [TOP](TOP.html "TOP") • [Experimental:TOP](Experimental_TOP.html "Experimental:TOP") • [TOP Viewer](TOP_Viewer.html "TOP Viewer") • [Touch In](Touch_In_TOP.html "Touch In TOP") • [Touch Out](Touch_Out_TOP.html "Touch Out TOP") • [Transform](Transform_TOP.html "Transform TOP") • [Under](Under_TOP.html "Under TOP") • Video Device In• [Video Device Out](Video_Device_Out_TOP.html "Video Device Out TOP") • [Video Stream In](Video_Stream_In_TOP.html "Video Stream In TOP") • [Video Stream Out](Video_Stream_Out_TOP.html "Video Stream Out TOP") • [Vioso](Vioso_TOP.html "Vioso TOP") • [Web Render](Web_Render_TOP.html "Web Render TOP") • [Experimental:ZED Select](Experimental_ZED_Select_TOP.html "Experimental:ZED Select TOP") • [ZED](ZED_TOP.html "ZED TOP") • [Experimental:ZED](Experimental_ZED_TOP.html "Experimental:ZED TOP") |
An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").

A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP") can set the image resolution. See [Aspect Ratio](TOP_Generator_Common_Page.html "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=Video_Device_In_TOP&oldid=31087>"
[Category](Special_Categories.html "Special:Categories"):
* [TOPs](Category_TOPs.html "Category:TOPs")