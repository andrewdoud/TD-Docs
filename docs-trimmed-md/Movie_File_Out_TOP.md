

# Movie_File_Out_TOP

Movie File Out TOP - TouchDesigner Documentation




# Movie File Out TOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Movie File Out TOP saves a TOP stream out to a movie file (`.mov`/`.mp4`) using a variety of codecs, including the H.264/H.265, [Hap Q](Hap.html "Hap"), [NotchLC](NotchLC.html "NotchLC"), [Apple ProRes](Apple_ProRes.html "Apple ProRes") and Animation video codecs. It can also save single frame images, image sequences, or stop-frame movies.
For codecs that support Alpha, use the 'Movie Pixel Format' parameter to select a format that includes alpha.
The [Export Movie Dialog](Export_Movie_Dialog.html "Export Movie Dialog") is a user interface built around the Movie File Out TOP.
To record movies with audio using the Movie File Out TOP, a [Time Sliced](Time_Slicing.html "Time Slicing") CHOP with mono or stereo channels of audio is required. If TouchDesigner is running at a lower frame rate than the target video frame rate and a CHOP is specified for audio, the Movie File Out TOP will automatically repeat video frames to ensure the video and audio stay in sync.
Recording a movie without frame drops can be done in non-realtime by turning off the Realtime flag at the top of the user interface.
The length of the video is not predetermined and depends on the amount of time the Record parameter is on.
You can record a sequence of `.tif` or `.exr` files by setting the Type parameter to Image Sequence. When Image File Type is set to OpenEXR, the EXR page has options to record any number of color channels from multiple TOPs into an EXR image file, and can create it with metadata that would get read by a [Point File In TOP](Point_File_In_TOP.html "Point File In TOP").
**H264/H265 NOTE:** Encoding movies in H.264/H.265 codec is only available with a [Commercial](TouchDesigner_Commercial.html "TouchDesigner Commercial") or [Pro](TouchDesigner_Pro.html "TouchDesigner Pro") license. Nvidia graphic hardware is also required.
**\*\*\* WARNING - GPU Driver Timeout on long GPU activities \*\*\*** Encoding some formats at high-resolution may be a slow, GPU-intensive operation. Generally only the RGBA BC7 mode for HapQ can suffer from this though. Consequently it will usually take longer than the default 2 seconds per frame that Windows gives the GPU driver to complete an operation. If you see a message saying that Windows has reset the GPU driver, this is the issue you are running into. To fix the issue, create this registry value:
`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\GraphicsDrivers\TdrDelay`  
The value should be of type `REG_DWORD`. The value is the number of seconds an operation can take before the OS resets the GPU driver. Set it to something larger, like 20-40 (seconds), depending on the resolution you intend to encode. You must reboot your machine for this setting to take effect. If you still get driver resets, make it even larger.
Recording still images and stop-frame animation can be done by changing the 'Type' parameter. Then the 'Add Frame' pulse button can be pulsed manually or via a script to cause the frames to be written.
See also [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP"), [Recording Movies with Audio](https://docs.derivative.ca/Recording_Movies_with_Audio "Recording Movies with Audio").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[moviefileoutTOP\_Class](https://docs.derivative.ca/MoviefileoutTOP_Class "MoviefileoutTOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Movie Out Page](#Parameters_-_Movie_Out_Page)
* [3 Parameters - EXR Page](#Parameters_-_EXR_Page)
* [4 Parameters - Settings Page](#Parameters_-_Settings_Page)
* [5 Parameters - Common Page](#Parameters_-_Common_Page)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Specific Movie File Out TOP Info Channels](#Specific_Movie_File_Out_TOP_Info_Channels)
  + [7.2 Common TOP Info Channels](#Common_TOP_Info_Channels)
  + [7.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Movie Out Page
Type `type` - ⊞ - Output either a movie, image, image sequence, or stop-frame movie.
* Movie `movie` - Records a movie file.
* Image `image` - Records a single image.
* Image Sequence `imagesequence` - Records a sequence of images.
* Stop-Frame Movie `stopframemovie` -
Video Codec `videocodec` - ⊞ - Select the video compression codec used to encode the movie.
* Animation `rle` - Run-length encoded video, lossless codec and low decode times, but very large file size. Alpha channel can be included when Pixel Format is RGBA.
* Photo/Motion JPEG `mjpa` - JPEG encoded video, lossy codec and low decode times with medium file sizes. Good for playback both forwards and backwards or for random access.
* MPEG 4 (Part 2) `mpeg4` - High quality but can produce large files size and/or have high decode times.
* H.264 (NVIDIA GPU) `h264nvgpu` - H.264 GPU encoding, only available when using Nvidia graphics cards. Great compression and quality and small file sizes. However can suffer from high decode times and not the best for random access, scrubbing, or reverse playback. See the H264 parameter page for additional H264 encoding options.
* GoPro-Cineform `cineform` - A lossy compression similar to Apple ProRes. Alpha channel can be included.
* Hap `hap` - See [Hap](Hap.html "Hap"), a fast codec that uses the GPU. Lower quality than Hap Q.
* Hap Q `hapq` - See [Hap](Hap.html "Hap"), a fast codec that uses the GPU. Higher quality than regular Hap.
* H.265/HEVC (NVIDIA GPU) `h265nvgpu` - H.265 GPU encoding, only available when using Nvidia graphics cards. Better compression (and sometimes quality) than H.264 but more resource intensive to encode/decode.
* GIF `gif` - An animated [.gif](https://en.wikipedia.org/wiki/GIF) file. Because there is no way to specific the color palette currently, a default palette will be used.
* NotchLC `notchlc` - [NotchLC](NotchLC.html "NotchLC") is a high quality, GPU accelerated video format. It offers higher quality results than HapQ, at the cost of higher GPU usage as well as larger file sizes.
* VP8 `vp8` - The open standard [VP8](https://en.wikipedia.org/wiki/VP8) format. Somewhat comparable to H264.
* VP9 `vp9` - The open standard [VP9](https://docs.derivative.ca/index.php?title=VP9https://en.wikipedia.org/wiki/VP9&action=edit&redlink=1 "VP9https://en.wikipedia.org/wiki/VP9 (page does not exist)") format. Somehwat comaparable to HEVC/H265.
* Apple ProRes `prores` - [Apple ProRes](Apple_ProRes.html "Apple ProRes") video format.
Video Codec Type `videocodectype` - Some video codecs such as [Apple ProRes](Apple_ProRes.html "Apple ProRes"), [Hap](Hap.html "Hap") and [Hap Q](Hap.html "Hap") have a various different types such as ProRes 442 HQ, ProRe 4444 HQ etc.
Image File Type `imagefiletype` - ⊞ - Choose what file type to use when Type is set to Image.
* TIFF `tiff` - A lossless, compressed, image format that includes alpha.
* JPEG `jpeg` - A lossy image format, very well compressed. No support for alpha.
* BMP `bmp` - A lossless, uncompressed, image format that includes alpha.
* OpenEXR `exr` - A lossless, compressed, image format that can save files in 16-bit float and 32-bit float formats. Can also include alpha. More information [here](https://en.wikipedia.org/wiki/OpenEXR).
* PNG `png` - A lossless, compressed, image format that can include alpha. Supports bit 8-bit and 16-bit fixed data.
* DDS `dds` - A lossless, uncompressed, image format that can include alpha. Can include mipmap information. Natively support most pixel formats supported by TOPs.
Unique Suffix `uniquesuff` - When enabled, me.fileSuffix will be a unique suffix when used in the file parameter.
N `n` - N is the index used in me.fileSuffix. When unique suffix is enabled, N specifies the starting index to increment from when calculating a unique suffix/name.
File `file` - Sets the path and filename of the movie file that is saved out. The filename must include the file extension such as .mov/.mp4 etc. For movies, generally the .mov file extension will work with the most codecs.
Movie Pixel Format `moviepixelformat` - ⊞ - Options for the pixel format based on the Video Codec selected. Use this parameter to change the color quality of the output (how many bits are used, YUV sampling etc.), as well as selecting formats that include alpha for codecs that support alpha.
* YUV 4:2:0 `yuv420` - (Photo/Motion JPEG, MPEG 4 (Part 2), )
* YUV 4:2:0 (8-Bit) `yuv420` - (H.264 (NVIDIA GPU), H.265/HEVC (NVIDIA GPU))
* YUV 4:2:0 (10-Bit) `yuv420p10bit` - (H.265/HEVC (NVIDIA GPU))
* YUV 4:2:2 `yuv422` - (Photo/Motion JPEG, )
* YUV 4:4:4 (8-Bit) `yuv444` - (H.264 (NVIDIA GPU), H.265/HEVC (NVIDIA GPU))
* YUV 4:4:4 (10-Bit) `yuv444p10bit` - (H.265/HEVC (NVIDIA GPU))
* RGB `rgb` - (Animation, Hap, Hap Q)
* RGBA `rgba` - (Animation, GoPro-Cineform, Hap, Hap Q)
* RGBA BC7 `rgba` - (Hap Q) - Slow, Read Help Before Using!
* RGB Palette `3` - (GIF)
Audio CHOP `audiochop` - Specify a CHOP to use as the audio track for the movie. Drag & Drop a CHOP here or manually enter the CHOP's path. **The CHOP needs to be [time-sliced](Time_Slicing.html "Time Slicing")**.
Audio Codec `audiocodec` - ⊞ - Select the audio compression codec used to encode the audio.
* ALAC (Apple Lossless) `alac` - A lossless audio codec that still offers some compression for the data.
* MP3 `mp3` - Highly compressed lossy codec. Can only do 2 channels of audio. MP3 compression will not have gapless playback.
* Uncompressed 16-bit (PCM) `pcm16` - Uncompressed audio (Pulse Code Modulation)
* Uncompressed 24-bit (PCM) `pcm24` - Uncompressed audio (Pulse Code Modulation)
* Uncompressed 32-bit (PCM) `pcm32` - Uncompressed audio (Pulse Code Modulation)
* Vorbis `vorbis` - Vorbis is a lossy audio compression codec. Vorbis compression will have gapless playback.
Audio Bit Rate `audiobitrate` - ⊞ - The bitrate to write the audio out at.
Note: A particlular behavior on Windows OS AAC encoder; for 1 and 2 channelsthe selction of bit rate is for both channels ie. it’s 192kb/s for either of them, so either 1x192kb/s or 2x96kb/s. However, when using more than 2 channels the bitrate is per channel ie. for 6 channel then it’s 6x192kb/s.
* 96 kb/s `b96` -
* 128 kb/s `b128` -
* 192 kb/s `b192` -
* 256 kb/s `b256` -
* 320 kb/s `b320` -
Quality `quality` - Select the quality of the movie compression. NOTE: Some codecs can not output lossless compression.
Movie FPS `fps` - The frame rate of the movie file created.
Limit Length `limitlength` - This can be used to automatically stop recording the file once it reaches a specified length.
Length `length` - The length to stop recording the file at.
Length Unit `lengthunit` - ⊞ - The unit the length is specified in.
* I `indices` -
* F `frames` -
* S `seconds` -
Record `record` - When this parameter is set to 1, the movie will be recording.
Pause `pause` - Pauses the recording.
Add Frame `addframe` - Adds a single frame to the output for each click of the button. Pause must be **On** to enable the Add Frame parameter.
Max Threads `maxthread` - When outputting sequences of images, this controls the maximum number of threads can be used to output images (one thread per image). If this is set to 1 then the main thread will be used to write the image.
Header Source DAT `headerdat` - The path to a Table DAT that stores header metadata that should be written to the output image or movie file. Header data is written as key-value pairs with the first column storing the keys and the second column storing the associated values. **Note:** Currently only supported for EXR files. **Warning:** Files may fail to save if the header data conflicts with system headers.
  

## Parameters - EXR Page
The Inputs page can be used to add extra channels of image data to the output file and to change the names of the base 4 channels.
Each 'Additional Input TOP' is a path to a TOP containing the image data to add to the file. The associated Red, Green, Blue and Alpha parameters are the names assigned to that input's channels in the new file. If the channel parameter is left blank, that channel will not be added to the output file. Channels with duplicate names will be overwritten.
**Note:** Additional inputs are currently only supported in EXR images and sequences. In EXR files, channels are stored in alphabetical order.
Save as Point Cloud `pointcloud` - When enabled, an additional header will be added to the file that indicates the contents are point data rather than images. This header is used to automatically load the file into a [Point File In TOP](Point_File_In_TOP.html "Point File In TOP") rather than a [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP") when dragging and dropping.
Additional Input TOP `input` - Sequence of TOPs containing image data to add to the file
Red `input0r` - Name assigned to the specified TOP's Red channel.
Green `input0g` - Name assigned to the specified TOP's Green channel.
Blue `input0b` - Name assigned to the specified TOP's Blue channel.
Alpha `input0a` - Name assigned to the specified TOP's Alpha channel.
TOP `input1top` - The path to the TOP used to specify addition channels to the EXR file. The first 4 channels specified above come from the input connected to the Movie File Out TOP, this TOPs RGBA data can be assigned unique names in the EXR file using the Red, Green, Blue, Alpha parameters below.
  

## Parameters - Settings Page
Stall for File Open `stallforopen` - When this is on playback will stall until the file is opened and ready to receive frames, to make sure the frame that was inputted when Record was turned on gets recorded. When this is off recording may start on a later frame, after the file has been opened. Turning this off can avoid a stall in playback, if missing recording some frames at the start is acceptable.
Profile `profile` - ⊞ - Select the H.264 profile to use.
* Auto-Select `autoselect` -
* Baseline `baseline` -
* Main `main` -
* High `high` -
Preset `preset` - ⊞ - The H264 preset to use.
* None `none` - Select from the available presets.
* Lossless `lossless` -
Bit Rate Mode `bitratemode` - ⊞ - Select between Constant or Variable bit rate, and regular or high quality bit rate modes.
* Constant (CBR) `constant` -
* Variable (VBR) `variable` -
* Constant HQ (CBR) `constanthq` -
* Variable HQ (VBR) `variablehq` -
Average Bitrate (Kb/s) `avgbitrate` - Set the average bitrate target for the encoding.
Peak Bitrate (Kb/s) `peakbitrate` - Set the peak bitrate allowed for the encoding.
Keyframe Interval `keyframeinterval` - Set the number of frames between key-frames (I-frames) while encoding.
Max B-Frames `maxbframes` - Controls the maximum number of B-frames (bi-directional frames) that will be created between pairs of key-frames.
Motion Prediction `motionpredict` - ⊞ - Controls the quality of the Motion Prediction used when encoding H264/H265.
* Default `default` -
* Quarter `quarter` -
* Half `half` -
* Full `full` -
Frame Slicing `frameslicing` - Controls if H264/H265 frames are sliced into multiple pieces, allowing them to be decoded using multiple CPUs more easily.
Num Slices `numslices` - The number of slices each frame is split into.
Entropy Mode `entropymode` - ⊞ - Controls which entropy mode is used for H265 encoding.
* Auto-Select `autoselect` -
* CABAC `cabac` -
* CAVLC `cavlc` -
Secondary Compression `secondarycompression` - [Hap](Hap.html "Hap") uses a secondary CPU compression stage usually. Encoding video without this compression will result in faster playback, but potentially larger file sizes (which would require faster drives to play back).
Encode Test Mode `encodetestmode` - This mode disables file writting, and only does the encoding. This is useful to test the GPU/CPU performance of encoding while taking the SSD speed out of the equation.
Include Mip Maps `mipmaps` - When saving out .dds file, mipmaps can be included if this is enabled. This is primarily used for the [PreFilter Map TOP](PreFilter_Map_TOP.html "PreFilter Map TOP"), which will encode special information into the mipmap levels of the texture which needs to be maintained.
  

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
Extra Information for the Movie File Out TOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific Movie File Out TOP Info Channels
* last\_frames\_written - The number of frames written to the file on the last cook. This many be multiple repeats of the same image if TouchDesigner dropped frames, to ensure time stays in sync.
* total\_frames\_written - The total number of frames written to the file so far.
* last\_audio\_samples\_written - The number of audio samples written to the file on the last cook.
* total\_audio\_samples\_written - The total number of audio samplers written to the file.
* last\_audio\_frames\_written - The number of audio frames written to the file on the last cook. This is the samples value, converted to frame units.
* total\_audio\_frames\_written - The total number of audio frames written to the file. This is the samples value, converted to frame units.
* total\_frames\_dropped - The number frames that TouchDesigner failed to provide unique images for in the output file. This occurs when TouchDesigner drops frames when the file needed new images.
* active\_records - When recording sequences of images, they may be written using multiple CPUs at the same time. This tells how many images are currently being recorded.
* cur\_seq\_index - When recording sequences of images, this is the current sequence image index.
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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2023.112802021.100002020.200002019.146502018.28070before 2018.28070
| TOPs |
| --- |
| [Add](Add_TOP.html "Add TOP") • [Analyze](Analyze_TOP.html "Analyze TOP") • [Anti Alias](Anti_Alias_TOP.html "Anti Alias TOP") • [Blob Track](Blob_Track_TOP.html "Blob Track TOP") • [Bloom](Bloom_TOP.html "Bloom TOP") • [Blur](Blur_TOP.html "Blur TOP") • [Cache Select](Cache_Select_TOP.html "Cache Select TOP") • [Cache](Cache_TOP.html "Cache TOP") • [Channel Mix](Channel_Mix_TOP.html "Channel Mix TOP") • [CHOP to](CHOP_to_TOP.html "CHOP to TOP") • [Chroma Key](Chroma_Key_TOP.html "Chroma Key TOP") • [Circle](Circle_TOP.html "Circle TOP") • [Composite](Composite_TOP.html "Composite TOP") • [Constant](Constant_TOP.html "Constant TOP") • [Convolve](Convolve_TOP.html "Convolve TOP") • [Corner Pin](Corner_Pin_TOP.html "Corner Pin TOP") • [CPlusPlus](CPlusPlus_TOP.html "CPlusPlus TOP") • [Crop](Crop_TOP.html "Crop TOP") • [Cross](Cross_TOP.html "Cross TOP") • [Cube Map](Cube_Map_TOP.html "Cube Map TOP") • [Depth](Depth_TOP.html "Depth TOP") • [Difference](Difference_TOP.html "Difference TOP") • [Direct Display Out](Direct_Display_Out_TOP.html "Direct Display Out TOP") • [DirectX In](DirectX_In_TOP.html "DirectX In TOP") • [DirectX Out](DirectX_Out_TOP.html "DirectX Out TOP") • [Displace](Displace_TOP.html "Displace TOP") • [Edge](Edge_TOP.html "Edge TOP") • [Emboss](Emboss_TOP.html "Emboss TOP") • [Feedback](Feedback_TOP.html "Feedback TOP") • [Fit](Fit_TOP.html "Fit TOP") • [Flip](Flip_TOP.html "Flip TOP") • [Function](Function_TOP.html "Function TOP") • [GLSL Multi](GLSL_Multi_TOP.html "GLSL Multi TOP") • [GLSL](GLSL_TOP.html "GLSL TOP") • [HSV Adjust](HSV_Adjust_TOP.html "HSV Adjust TOP") • [HSV to RGB](HSV_to_RGB_TOP.html "HSV to RGB TOP") • [Import Select](Import_Select_TOP.html "Import Select TOP") • [In](In_TOP.html "In TOP") • [Inside](Inside_TOP.html "Inside TOP") • [Introduction To s Vid](Introduction_To_TOPs_Vid.html "Introduction To TOPs Vid") • [Kinect Azure Select](Kinect_Azure_Select_TOP.html "Kinect Azure Select TOP") • [Kinect Azure](Kinect_Azure_TOP.html "Kinect Azure TOP") • [Kinect](Kinect_TOP.html "Kinect TOP") • [Layout](Layout_TOP.html "Layout TOP") • [Leap Motion](Leap_Motion_TOP.html "Leap Motion TOP") • [Lens Distort](Lens_Distort_TOP.html "Lens Distort TOP") • [Level](Level_TOP.html "Level TOP") • [Limit](Limit_TOP.html "Limit TOP") • [Lookup](Lookup_TOP.html "Lookup TOP") • [Luma Blur](Luma_Blur_TOP.html "Luma Blur TOP") • [Luma Level](Luma_Level_TOP.html "Luma Level TOP") • [Math](Math_TOP.html "Math TOP") • [Matte](Matte_TOP.html "Matte TOP") • [Mirror](Mirror_TOP.html "Mirror TOP") • [Monochrome](Monochrome_TOP.html "Monochrome TOP") • [MoSys](MoSys_TOP.html "MoSys TOP") • [Movie File In](Movie_File_In_TOP.html "Movie File In TOP") • Movie File Out• [MPCDI](MPCDI_TOP.html "MPCDI TOP") • [Multiply](Multiply_TOP.html "Multiply TOP") • [Ncam](Ncam_TOP.html "Ncam TOP") • [NDI In](NDI_In_TOP.html "NDI In TOP") • [NDI Out](NDI_Out_TOP.html "NDI Out TOP") • [Noise](Noise_TOP.html "Noise TOP") • [Normal Map](Normal_Map_TOP.html "Normal Map TOP") • [Notch](Notch_TOP.html "Notch TOP") • [Null](Null_TOP.html "Null TOP") • [Nvidia Background](Nvidia_Background_TOP.html "Nvidia Background TOP") • [Nvidia Denoise](Nvidia_Denoise_TOP.html "Nvidia Denoise TOP") • [Nvidia Flex](Nvidia_Flex_TOP.html "Nvidia Flex TOP") • [Nvidia Flow](Nvidia_Flow_TOP.html "Nvidia Flow TOP") • [Nvidia Upscaler](Nvidia_Upscaler_TOP.html "Nvidia Upscaler TOP") • [OAK Select](OAK_Select_TOP.html "OAK Select TOP") • [Oculus Rift](Oculus_Rift_TOP.html "Oculus Rift TOP") • [OP Viewer](OP_Viewer_TOP.html "OP Viewer TOP") • [OpenColorIO](OpenColorIO_TOP.html "OpenColorIO TOP") • [OpenVR](OpenVR_TOP.html "OpenVR TOP") • [Optical Flow](Optical_Flow_TOP.html "Optical Flow TOP") • [Orbbec Select](Orbbec_Select_TOP.html "Orbbec Select TOP") • [Orbbec](Orbbec_TOP.html "Orbbec TOP") • [Ouster Select](Ouster_Select_TOP.html "Ouster Select TOP") • [Ouster](Ouster_TOP.html "Ouster TOP") • [Out](Out_TOP.html "Out TOP") • [Outside](Outside_TOP.html "Outside TOP") • [Over](Over_TOP.html "Over TOP") • [Pack](Pack_TOP.html "Pack TOP") • [Photoshop In](Photoshop_In_TOP.html "Photoshop In TOP") • [Point File In](Point_File_In_TOP.html "Point File In TOP") • [Point File Select](Point_File_Select_TOP.html "Point File Select TOP") • [Point Transform](Point_Transform_TOP.html "Point Transform TOP") • [PreFilter Map](PreFilter_Map_TOP.html "PreFilter Map TOP") • [Projection](Projection_TOP.html "Projection TOP") • [Ramp](Ramp_TOP.html "Ramp TOP") • [RealSense](RealSense_TOP.html "RealSense TOP") • [Rectangle](Rectangle_TOP.html "Rectangle TOP") • [Remap](Remap_TOP.html "Remap TOP") • [Render Pass](Render_Pass_TOP.html "Render Pass TOP") • [Render Select](Render_Select_TOP.html "Render Select TOP") • [Render](Render_TOP.html "Render TOP") • [RenderStream In](RenderStream_In_TOP.html "RenderStream In TOP") • [RenderStream Out](RenderStream_Out_TOP.html "RenderStream Out TOP") • [Reorder](Reorder_TOP.html "Reorder TOP") • [Resolution](Resolution_TOP.html "Resolution TOP") • [RGB Key](RGB_Key_TOP.html "RGB Key TOP") • [RGB to HSV](RGB_to_HSV_TOP.html "RGB to HSV TOP") • [Scalable Display](Scalable_Display_TOP.html "Scalable Display TOP") • [Screen Grab](Screen_Grab_TOP.html "Screen Grab TOP") • [Screen](Screen_TOP.html "Screen TOP") • [Script](Script_TOP.html "Script TOP") • [Select](Select_TOP.html "Select TOP") • [Shared Mem In](Shared_Mem_In_TOP.html "Shared Mem In TOP") • [Shared Mem Out](Shared_Mem_Out_TOP.html "Shared Mem Out TOP") • [SICK](SICK_TOP.html "SICK TOP") • [Slope](Slope_TOP.html "Slope TOP") • [Spectrum](Spectrum_TOP.html "Spectrum TOP") • [SSAO](SSAO_TOP.html "SSAO TOP") • [Stype](Stype_TOP.html "Stype TOP") • [Substance Select](Substance_Select_TOP.html "Substance Select TOP") • [Substance](Substance_TOP.html "Substance TOP") • [Subtract](Subtract_TOP.html "Subtract TOP") • [SVG](SVG_TOP.html "SVG TOP") • [Switch](Switch_TOP.html "Switch TOP") • [Syphon Spout In](Syphon_Spout_In_TOP.html "Syphon Spout In TOP") • [Syphon Spout Out](Syphon_Spout_Out_TOP.html "Syphon Spout Out TOP") • [Text](Text_TOP.html "Text TOP") • [Texture 3D](Texture_3D_TOP.html "Texture 3D TOP") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Threshold](Threshold_TOP.html "Threshold TOP") • [Tile](Tile_TOP.html "Tile TOP") • [Time Machine](Time_Machine_TOP.html "Time Machine TOP") • [TOP](TOP.html "TOP") • [Experimental:TOP](Experimental_TOP.html "Experimental:TOP") • [TOP Viewer](TOP_Viewer.html "TOP Viewer") • [Touch In](Touch_In_TOP.html "Touch In TOP") • [Touch Out](Touch_Out_TOP.html "Touch Out TOP") • [Transform](Transform_TOP.html "Transform TOP") • [Under](Under_TOP.html "Under TOP") • [Video Device In](Video_Device_In_TOP.html "Video Device In TOP") • [Video Device Out](Video_Device_Out_TOP.html "Video Device Out TOP") • [Video Stream In](Video_Stream_In_TOP.html "Video Stream In TOP") • [Video Stream Out](Video_Stream_Out_TOP.html "Video Stream Out TOP") • [Vioso](Vioso_TOP.html "Vioso TOP") • [Web Render](Web_Render_TOP.html "Web Render TOP") • [Experimental:ZED Select](Experimental_ZED_Select_TOP.html "Experimental:ZED Select TOP") • [ZED](ZED_TOP.html "ZED TOP") • [Experimental:ZED](Experimental_ZED_TOP.html "Experimental:ZED TOP") |
An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).

A built-in panel in TouchDesigner that contains a library of components and media that can be dragged-dropped into a TouchDesigner network.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

A form of [DATs](DAT.html "DAT") (Data Operators) that is structured as rows and columns of text strings.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

In the [Animation component](Animation_COMP.html "Animation COMP") each keyframe specifies a channel's value at a specific time (or frame). A keyframe holds a value, slopes and accelerations, and an interpolation type. A channel's keyframes are used to interpolate and determine the values of all the samples of the channel.

The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP") can set the image resolution. See [Aspect Ratio](TOP_Generator_Common_Page.html "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").

Retrieved from "<https://docs.derivative.ca/index.php?title=Movie_File_Out_TOP&oldid=32418>"
[Category](Special_Categories.html "Special:Categories"):
* [TOPs](Category_TOPs.html "Category:TOPs")