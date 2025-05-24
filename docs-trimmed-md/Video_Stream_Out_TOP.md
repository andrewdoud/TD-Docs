

# Video_Stream_Out_TOP

Video Stream Out TOP - TouchDesigner Documentation




# Video Stream Out TOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
**Note:** This TOP uses the Nvidia Hardware Encoder to create the stream and therefore requires an Nvidia GPU and Windows to operate.
The Video Stream Out TOP creates either an [RTSP](RTSP.html "RTSP") server, or can act as an [RTMP](RTMP.html "RTMP") or [SRT](SRT.html "SRT") sender, to send H.264 video and MP3 audio across the network. It uses Nvidia's hardware H264 encoder. For RTSP, it can handle multiple clients connecting to it at the same time. Multiple Video Stream Out TOPs using the same port will be handled using the same underlying RTSP server. The Video Stream Out TOP can also be used to send a video stream through [WebRTC](WebRTC.html "WebRTC") video/audio tracks.
##### RTSP
Obtain the URL to connect to the Video Steam Out TOP's RTSP server by using an Info DAT or by middle clicking on the node. It will be in the form:
`rtsp://<ipaddress>:<port>/<streamName>`
e.g.
`rtsp://192.168.0.1:554/tdvidstream`
##### RTMP
To obtain the RTMP URL stream to, you may need to search to find the correct URL depending on your location and the service you are using. This should be in the format:
`{service url}/{stream key}`.
For example for Twitch the URL would be something like
`rtmp://live-yto.twitch.tv/app/live_1234567_sduhy3xJ1KJ34Eg6CjksdJLubFS7gtUY`
For more information on different services see [RTMP](RTMP.html "RTMP").
##### SRT
[SRT](https://en.wikipedia.org/wiki/Secure_Reliable_Transport) can use either H.264 or H.265 video codec. It can also send per-frame metadata when a CHOP or DAT is specified in the Per-Frame Metadata parameter. The SRT server is settings are controlled by URL options. E.g to create a listener you'd specify the URL:
`srt://0.0.0.0:9494?mode=listener`
To connect to listener, you'd do:
`srt://127.0.0.1:9494?mode=caller`
Either side of the connection can be the listener or the caller, it doesn't matter which is sending the video and which is receiving the video. The receiver would set their mode to be the opposite of whatever the sender is setting their mode to be.
All the options that are available are listed [here](https://ffmpeg.org/ffmpeg-protocols.html#srt). Multiple options can be set using a & as separator. E.g
`srt://127.0.0.1:9494?mode=caller&send_buffer_size=100000`
SRT sent from the Video Stream Out TOP can include per-frame metadata making it easy to send and receive CHOP/DAT data in sync with video. It can be read with the [Video Stream In TOP](Video_Stream_In_TOP.html "Video Stream In TOP").
  

##### Limitations
RTSP streaming does not support sending directly to another RTSP server via RTP.
The maximum stream outs on a NVIDIA Geforce card is 2: The number of streams the GPU can handle is different depending on driver versions and hardware, however in general it is 2 streams max on Geforce level cards. Using a lower resolution does not avoid the 2 stream limit. Quadros can do more streams. Refer to [Nvidia Video GPU Support Matrix](https://developer.nvidia.com/video-encode-and-decode-gpu-support-matrix-new) for more information.
One test using the default TouchDesigner startup file on a M6000 was able to do 13 1080p@30hz Video Stream Out TOPs.
See also the [Video Stream In TOP](Video_Stream_In_TOP.html "Video Stream In TOP"), [RTMP](RTMP.html "RTMP"), [RTSP](RTSP.html "RTSP") and [Video Streaming User Guide](Video_Streaming_User_Guide.html "Video Streaming User Guide").
For other protocols over IP see [NDI (Network Data Interface)](NDI.html "NDI"), and [Touch Out TOP](Touch_Out_TOP.html "Touch Out TOP") / [Touch In TOP](Touch_In_TOP.html "Touch In TOP").
**NOTE for Windows OS - If experiencing connection issues make sure Windows Firewall is disabled.**
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[videostreamoutTOP\_Class](https://docs.derivative.ca/VideostreamoutTOP_Class "VideostreamoutTOP Class")
## Contents
* [1 Summary](#Summary)
  + [1.1 RTSP](#RTSP)
  + [1.2 RTMP](#RTMP)
  + [1.3 SRT](#SRT)
  + [1.4 Limitations](#Limitations)
* [2 Parameters - Video Stream Out Page](#Parameters_-_Video_Stream_Out_Page)
* [3 Parameters - WebRTC Page](#Parameters_-_WebRTC_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Specific Video Stream Out TOP Info Channels](#Specific_Video_Stream_Out_TOP_Info_Channels)
  + [6.2 Common TOP Info Channels](#Common_TOP_Info_Channels)
  + [6.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Video Stream Out Page
Active `active` - Controls if the server is active or not. If this is Off then the port this server uses will not be tied up.
Mode `mode` - ⊞ - Selects if the mode works as an RTSP server, sends RTMP to a receiever such as a distribution service like YouTube or Twitch, or sends to an SRT destination.
* RTSP Server `rtspserver` - Use the RTSP and RTP protocol. More information [here](https://docs.derivative.ca/index.php?title=Experimental:Video_Stream_Out_TOP&action=edit&redlink=1 "Experimental:Video Stream Out TOP (page does not exist)").
* RTMP Sender `rtmpsender` - Use the RTMP protocol. More information [here](https://docs.derivative.ca/index.php?title=Experimental:Video_Stream_Out_TOP&action=edit&redlink=1 "Experimental:Video Stream Out TOP (page does not exist)").
* SRT `srt` - Use the SRT protocol. More information [here](https://docs.derivative.ca/index.php?title=Experimental:Video_Stream_Out_TOP&action=edit&redlink=1 "Experimental:Video Stream Out TOP (page does not exist)").
* WebRTC `webrtc` - Use a WebRTC peer. More info: [WebRTC](WebRTC.html "WebRTC"), [WebRTC DAT](WebRTC_DAT.html "WebRTC DAT").
Network Port `port` - The port the server should listen on. Multiple Video Stream Out TOPs can use the same port as long as each has a unique Stream Name.
Stream Name `streamname` - The name of the stream for this node. This name is what comes after the / in the URL after the ipaddress:port combination.
Multi-Cast `multicast` - Controls if RTSP server sends its video out using unicast or multicast UDP packets.
RTMP Destination URL `url` - The URL to sent the RTMP stream to. This should be in the format of {service url}/{stream key}. For example for twitch the URL would be something like `rtmp://live-yto.twitch.tv/app/live_1234567_sduhy3xJ1KJ34Eg6CjksdJLubFS7gtUY`. You may need to search to find the correct URL depending on your location and the service you are using.
Destination URL `url` - The URL to sent the RTMP stream to. This should be in the format of {service url}/{stream key}. For example for twitch the URL would be something like `rtmp://live-yto.twitch.tv/app/live_1234567_sduhy3xJ1KJ34Eg6CjksdJLubFS7gtUY`. You may need to search to find the correct URL depending on your location and the service you are using.
Force IDR `forceidr` - For debugging, this will force the server to create a new video keyframe to send to all the clients. If clients aren't getting proper image this can be used to attempt to fix it. If you need to use this parameter please report the case to support@derivative.ca.
FPS `fps` - The FPS to send video at.
Video Codec `videocodec` - ⊞ - Select which codec to use for encoding the stream.
* H.264 (NVIDIA GPU) `h264nvgpu` -
* H.265/HEVC (NVIDIA GPU) `h265nvgpu` -
Profile `profile` - ⊞ - The H.264 profile to use to encode the frames. Some decoders can only support H.264 encoder at certain profiles.
* Baseline `baseline` -
* Main `main` -
* High `high` -
Quality `quality` - ⊞ - The quality level of the encoding.
* Low-Latency Low `lowlatencylow` -
* Low-Latency Medium `lowlatencymedium` -
* Low-Latency High `lowlatencyhigh` -
* High-Latency Low `highlatencylow` -
* High-Latency High `highlatencyhigh` -
Keyframe Interval `keyframeinterval` - Set the keyframe interval for the H.264 encoder.
Max B-Frames `maxbframes` - The maximum number of bi-directional frames that can occur between keyframes. More will increase latency but reduce bandwidth.
Intra-Refresh Period `intrarefreshperiod` - Intra-refresh is a gradual keyframe that is applied across the image to clean up streaming artifacts over multiple frames, instead of one large keyframe. This controls the number of frames that elapse between each intra-refresh occuring.
Intra-Refresh Length `intrarefreshlength` - The number of frames the intra-refresh will be spread out across.
Bitrate Mode `bitratemode` - ⊞ - Chooses between constant (CBR) and variable (VBR) bit rate modes. Mode streaming services prefer a constant bit rate mode.
* Constant (CBR) `constant` -
* Variable (VBR) `variable` -
* Constant HQ (CBR) `constanthq` -
* Variable HQ (VBR) `variablehq` -
Average Bitrate (Mb/s) `avgbitrate` - The target bitrate for the encoding. This is specified in Mb/s (megabits/second).
Per-Frame Metadata `perframemetadata` - Send metadata from this OP with each frame of the video stream. This data can be received from the [Video Stream In TOP](Video_Stream_In_TOP.html "Video Stream In TOP") using an [Info CHOP](Info_CHOP.html "Info CHOP") and [Info DAT](Info_DAT.html "Info DAT").
Max Bitrate (Mb/s) `maxbitrate` - The maximum bitrate for the encoding. This is specified in Mb/s (megabits/second).
Num H264 Slices per Frame `numslices` - This controls how many pieces (slices) each H.264 frame is separated into. Some decoders are able to decode multiple slices simultaneously so setting this to a value above 1 allows those decoders to run more efficiently.
Audio CHOP `audiochop` - A timesliced audio source to send along with the video. For RTSP, Audio will be resampled to 44100Hz before being encoded into MP3. For RTMP the sample rate must already be 44100. For WebRTC the sample rate must be 48000.
Audio Bit Rate `audiobitrate` - ⊞ - Set the bit rate used for encoding audio.
* 96 kb/s `b96` -
* 128 kb/s `b128` -
* 192 kb/s `b192` -
* 256 kb/s `b256` -
* 320 kb/s `b320` -
Include Silent Audio Stream `includesilentaudio` - ⊞ - Some broadcasting services require an audio stream to be included. This will include a silent audio stream along with the video in the event there isn't actual audio being streamed video the CHOP parameter.
* Automatic `automatic` -
* On `on` -
* Off `off` -
Per-Frame Metadata CHOP/DAT `perframemetadata` - Send metadata from this OP with each frame of the video stream. This data can be recevied from the [Video Stream In TOP](Video_Stream_In_TOP.html "Video Stream In TOP") using an [Info CHOP](Info_CHOP.html "Info CHOP") and [Info DAT](Info_DAT.html "Info DAT").
  

## Parameters - WebRTC Page
WebRTC `webrtc` - Set the [WebRTC DAT](WebRTC_DAT.html "WebRTC DAT") (ie. peer) to send the video stream over. Setting this will automatically populate the WebRTC Connection parameter menu with available connections.
WebRTC Connection `webrtcconnection` - Select the [WebRTC](WebRTC.html "WebRTC") peer-to-peer connection. Selecting this will automatically population the WebRTC Track parameter menu with available video output tracks.
WebRTC Video Track `webrtcvideotrack` - Select the video output track that's a part of the WebRTC peer-to-peer connection.
WebRTC Audio Track `webrtcaudiotrack` - Optionally select the audio output track that's a part of the WebRTC peer-to-peer connection, to be sent along with the video.
  

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
Extra Information for the Video Stream Out TOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific Video Stream Out TOP Info Channels
* last\_encode\_time -
* last\_send\_delay -
* packet\_loss\_ratio -
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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditor2022.241402021.100002020.236802018.28070before 2018.28070
| TOPs |
| --- |
| [Add](Add_TOP.html "Add TOP") • [Analyze](Analyze_TOP.html "Analyze TOP") • [Anti Alias](Anti_Alias_TOP.html "Anti Alias TOP") • [Blob Track](Blob_Track_TOP.html "Blob Track TOP") • [Bloom](Bloom_TOP.html "Bloom TOP") • [Blur](Blur_TOP.html "Blur TOP") • [Cache Select](Cache_Select_TOP.html "Cache Select TOP") • [Cache](Cache_TOP.html "Cache TOP") • [Channel Mix](Channel_Mix_TOP.html "Channel Mix TOP") • [CHOP to](CHOP_to_TOP.html "CHOP to TOP") • [Chroma Key](Chroma_Key_TOP.html "Chroma Key TOP") • [Circle](Circle_TOP.html "Circle TOP") • [Composite](Composite_TOP.html "Composite TOP") • [Constant](Constant_TOP.html "Constant TOP") • [Convolve](Convolve_TOP.html "Convolve TOP") • [Corner Pin](Corner_Pin_TOP.html "Corner Pin TOP") • [CPlusPlus](CPlusPlus_TOP.html "CPlusPlus TOP") • [Crop](Crop_TOP.html "Crop TOP") • [Cross](Cross_TOP.html "Cross TOP") • [Cube Map](Cube_Map_TOP.html "Cube Map TOP") • [Depth](Depth_TOP.html "Depth TOP") • [Difference](Difference_TOP.html "Difference TOP") • [Direct Display Out](Direct_Display_Out_TOP.html "Direct Display Out TOP") • [DirectX In](DirectX_In_TOP.html "DirectX In TOP") • [DirectX Out](DirectX_Out_TOP.html "DirectX Out TOP") • [Displace](Displace_TOP.html "Displace TOP") • [Edge](Edge_TOP.html "Edge TOP") • [Emboss](Emboss_TOP.html "Emboss TOP") • [Feedback](Feedback_TOP.html "Feedback TOP") • [Fit](Fit_TOP.html "Fit TOP") • [Flip](Flip_TOP.html "Flip TOP") • [Function](Function_TOP.html "Function TOP") • [GLSL Multi](GLSL_Multi_TOP.html "GLSL Multi TOP") • [GLSL](GLSL_TOP.html "GLSL TOP") • [HSV Adjust](HSV_Adjust_TOP.html "HSV Adjust TOP") • [HSV to RGB](HSV_to_RGB_TOP.html "HSV to RGB TOP") • [Import Select](Import_Select_TOP.html "Import Select TOP") • [In](In_TOP.html "In TOP") • [Inside](Inside_TOP.html "Inside TOP") • [Introduction To s Vid](Introduction_To_TOPs_Vid.html "Introduction To TOPs Vid") • [Kinect Azure Select](Kinect_Azure_Select_TOP.html "Kinect Azure Select TOP") • [Kinect Azure](Kinect_Azure_TOP.html "Kinect Azure TOP") • [Kinect](Kinect_TOP.html "Kinect TOP") • [Layout](Layout_TOP.html "Layout TOP") • [Leap Motion](Leap_Motion_TOP.html "Leap Motion TOP") • [Lens Distort](Lens_Distort_TOP.html "Lens Distort TOP") • [Level](Level_TOP.html "Level TOP") • [Limit](Limit_TOP.html "Limit TOP") • [Lookup](Lookup_TOP.html "Lookup TOP") • [Luma Blur](Luma_Blur_TOP.html "Luma Blur TOP") • [Luma Level](Luma_Level_TOP.html "Luma Level TOP") • [Math](Math_TOP.html "Math TOP") • [Matte](Matte_TOP.html "Matte TOP") • [Mirror](Mirror_TOP.html "Mirror TOP") • [Monochrome](Monochrome_TOP.html "Monochrome TOP") • [MoSys](MoSys_TOP.html "MoSys TOP") • [Movie File In](Movie_File_In_TOP.html "Movie File In TOP") • [Movie File Out](Movie_File_Out_TOP.html "Movie File Out TOP") • [MPCDI](MPCDI_TOP.html "MPCDI TOP") • [Multiply](Multiply_TOP.html "Multiply TOP") • [Ncam](Ncam_TOP.html "Ncam TOP") • [NDI In](NDI_In_TOP.html "NDI In TOP") • [NDI Out](NDI_Out_TOP.html "NDI Out TOP") • [Noise](Noise_TOP.html "Noise TOP") • [Normal Map](Normal_Map_TOP.html "Normal Map TOP") • [Notch](Notch_TOP.html "Notch TOP") • [Null](Null_TOP.html "Null TOP") • [Nvidia Background](Nvidia_Background_TOP.html "Nvidia Background TOP") • [Nvidia Denoise](Nvidia_Denoise_TOP.html "Nvidia Denoise TOP") • [Nvidia Flex](Nvidia_Flex_TOP.html "Nvidia Flex TOP") • [Nvidia Flow](Nvidia_Flow_TOP.html "Nvidia Flow TOP") • [Nvidia Upscaler](Nvidia_Upscaler_TOP.html "Nvidia Upscaler TOP") • [OAK Select](OAK_Select_TOP.html "OAK Select TOP") • [Oculus Rift](Oculus_Rift_TOP.html "Oculus Rift TOP") • [OP Viewer](OP_Viewer_TOP.html "OP Viewer TOP") • [OpenColorIO](OpenColorIO_TOP.html "OpenColorIO TOP") • [OpenVR](OpenVR_TOP.html "OpenVR TOP") • [Optical Flow](Optical_Flow_TOP.html "Optical Flow TOP") • [Orbbec Select](Orbbec_Select_TOP.html "Orbbec Select TOP") • [Orbbec](Orbbec_TOP.html "Orbbec TOP") • [Ouster Select](Ouster_Select_TOP.html "Ouster Select TOP") • [Ouster](Ouster_TOP.html "Ouster TOP") • [Out](Out_TOP.html "Out TOP") • [Outside](Outside_TOP.html "Outside TOP") • [Over](Over_TOP.html "Over TOP") • [Pack](Pack_TOP.html "Pack TOP") • [Photoshop In](Photoshop_In_TOP.html "Photoshop In TOP") • [Point File In](Point_File_In_TOP.html "Point File In TOP") • [Point File Select](Point_File_Select_TOP.html "Point File Select TOP") • [Point Transform](Point_Transform_TOP.html "Point Transform TOP") • [PreFilter Map](PreFilter_Map_TOP.html "PreFilter Map TOP") • [Projection](Projection_TOP.html "Projection TOP") • [Ramp](Ramp_TOP.html "Ramp TOP") • [RealSense](RealSense_TOP.html "RealSense TOP") • [Rectangle](Rectangle_TOP.html "Rectangle TOP") • [Remap](Remap_TOP.html "Remap TOP") • [Render Pass](Render_Pass_TOP.html "Render Pass TOP") • [Render Select](Render_Select_TOP.html "Render Select TOP") • [Render](Render_TOP.html "Render TOP") • [RenderStream In](RenderStream_In_TOP.html "RenderStream In TOP") • [RenderStream Out](RenderStream_Out_TOP.html "RenderStream Out TOP") • [Reorder](Reorder_TOP.html "Reorder TOP") • [Resolution](Resolution_TOP.html "Resolution TOP") • [RGB Key](RGB_Key_TOP.html "RGB Key TOP") • [RGB to HSV](RGB_to_HSV_TOP.html "RGB to HSV TOP") • [Scalable Display](Scalable_Display_TOP.html "Scalable Display TOP") • [Screen Grab](Screen_Grab_TOP.html "Screen Grab TOP") • [Screen](Screen_TOP.html "Screen TOP") • [Script](Script_TOP.html "Script TOP") • [Select](Select_TOP.html "Select TOP") • [Shared Mem In](Shared_Mem_In_TOP.html "Shared Mem In TOP") • [Shared Mem Out](Shared_Mem_Out_TOP.html "Shared Mem Out TOP") • [SICK](SICK_TOP.html "SICK TOP") • [Slope](Slope_TOP.html "Slope TOP") • [Spectrum](Spectrum_TOP.html "Spectrum TOP") • [SSAO](SSAO_TOP.html "SSAO TOP") • [Stype](Stype_TOP.html "Stype TOP") • [Substance Select](Substance_Select_TOP.html "Substance Select TOP") • [Substance](Substance_TOP.html "Substance TOP") • [Subtract](Subtract_TOP.html "Subtract TOP") • [SVG](SVG_TOP.html "SVG TOP") • [Switch](Switch_TOP.html "Switch TOP") • [Syphon Spout In](Syphon_Spout_In_TOP.html "Syphon Spout In TOP") • [Syphon Spout Out](Syphon_Spout_Out_TOP.html "Syphon Spout Out TOP") • [Text](Text_TOP.html "Text TOP") • [Texture 3D](Texture_3D_TOP.html "Texture 3D TOP") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Threshold](Threshold_TOP.html "Threshold TOP") • [Tile](Tile_TOP.html "Tile TOP") • [Time Machine](Time_Machine_TOP.html "Time Machine TOP") • [TOP](TOP.html "TOP") • [Experimental:TOP](Experimental_TOP.html "Experimental:TOP") • [TOP Viewer](TOP_Viewer.html "TOP Viewer") • [Touch In](Touch_In_TOP.html "Touch In TOP") • [Touch Out](Touch_Out_TOP.html "Touch Out TOP") • [Transform](Transform_TOP.html "Transform TOP") • [Under](Under_TOP.html "Under TOP") • [Video Device In](Video_Device_In_TOP.html "Video Device In TOP") • [Video Device Out](Video_Device_Out_TOP.html "Video Device Out TOP") • [Video Stream In](Video_Stream_In_TOP.html "Video Stream In TOP") • Video Stream Out• [Vioso](Vioso_TOP.html "Vioso TOP") • [Web Render](Web_Render_TOP.html "Web Render TOP") • [Experimental:ZED Select](Experimental_ZED_Select_TOP.html "Experimental:ZED Select TOP") • [ZED](ZED_TOP.html "ZED TOP") • [Experimental:ZED](Experimental_ZED_TOP.html "Experimental:ZED TOP") |
An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.

In the [Animation component](Animation_COMP.html "Animation COMP") each keyframe specifies a channel's value at a specific time (or frame). A keyframe holds a value, slopes and accelerations, and an interpolation type. A channel's keyframes are used to interpolate and determine the values of all the samples of the channel.

The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).

The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP") can set the image resolution. See [Aspect Ratio](TOP_Generator_Common_Page.html "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").

Retrieved from "<https://docs.derivative.ca/index.php?title=Video_Stream_Out_TOP&oldid=32429>"
[Category](Special_Categories.html "Special:Categories"):
* [TOPs](Category_TOPs.html "Category:TOPs")