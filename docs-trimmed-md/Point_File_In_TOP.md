

# Point_File_In_TOP

TouchDesigner Documentation




# Point File In TOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Point File In TOP loads 3D point data into TOPs from either a single file or a sequence of files. Points are composed of one or more floating point values such as XYZ positions, RGB color values, 3D normals, scanner intensity, etc. The Point File in TOP will load all available point data, but only four channels can be placed into the output image. By default, the first four point data channels are placed into the red, green, blue and alpha channels respectively; however, you can assign any point channel to a colour channel using the parameters on the Point Data page. Attach a [Point File Select TOP](Point_File_Select_TOP.html "Point File Select TOP") to create additional output images from the same source file.
The Point File In TOP will read point data from various mesh and floating point data files including: `.obj`, `.ply`, `.fits` (astronomy format), and `.exr`. It can also load ASCII point files (`.xyz`, `.pts`, `.csv`, `.txt`, etc) with one point per line and comma or space separated fields. The first line in ASCII point files can either be the number of points, the names of the point fields or the first point in the file.
For a complete list, see [File Types](File_Types.html "File Types"). The [OpenEXR](https://docs.derivative.ca/OpenEXR "OpenEXR") file format is generally best to use as it is binary, can be read in multi-frame file sequences that uses TouchDesigner's movie file pre-reading and buffering, and can be written from TouchDesigner's [Movie File Out TOP](Movie_File_Out_TOP.html "Movie File Out TOP") with unlimited numbers of channels.
Examine the state of a Point File In TOP by attaching an [Info CHOP](Info_CHOP.html "Info CHOP"). This will show information like the number of points, fields per point and the number of frames. It also shows dynamic information like the file open status, current frame, readahead frames and queue size, dropped frame count, CPU decode time and GPU upload time.
**Headers**: If the file contains any additional header data, this can be viewed by attaching an [Info DAT](Info_DAT.html "Info DAT"). Header data is stored as key-value pairs with the keys in the first column and the corresponding data in the second column, which can easily be interpreted with python.
All of the ASCII point list formats are loaded the same way whether their extention is `txt`, `csv`, `xyz`, etc. The parser looks for the first separating character (comma, space or tab) and then uses that to delimit the rest of the file. It will ignore delimiters that are inside single or double quotes. There are a few special rules depending on the delimiter style e.g. multiple spaces are merged together, but a comma at the end of a line indicates a blank field afterwards. Once a delimiter is established, The first line can be the number of points, but it is ignored. If the next line are strings then it is treated as a row of headers (channel names). Each row after that is considered a point.
See also [OpenEXR](https://docs.derivative.ca/OpenEXR "OpenEXR").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[pointfileinTOP\_Class](https://docs.derivative.ca/PointfileinTOP_Class "PointfileinTOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Point Data Page](#Parameters_-_Point_Data_Page)
* [3 Parameters - Play Page](#Parameters_-_Play_Page)
* [4 Parameters - Trim Page](#Parameters_-_Trim_Page)
* [5 Parameters - Tune Page](#Parameters_-_Tune_Page)
* [6 Parameters - Common Page](#Parameters_-_Common_Page)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Specific Point File In TOP Info Channels](#Specific_Point_File_In_TOP_Info_Channels)
  + [7.2 Common TOP Info Channels](#Common_TOP_Info_Channels)
  + [7.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Point Data Page
Control how the point's field data is placed into the output image.
The custom toggles control whether to use a custom field name to select which field is placed in the corresponding color channel. If false, the fields are selected in order e.g. the first field goes in red, the second in green, etc.
When set to custom, you can select the field from the dropdown menu or enter it directly. This parameter will be disabled if the color channel is not available in the output image format (see Pixel Format parameter).
File `file` - The path and name of the point file to load. Point file formats are those found in [File Types](File_Types.html "File Types"). You can specify files on the internet using `http://` ...
To treat a folder of files as an animation, specify the folder containing the files instead of a filename. All of the files must be the same resolution. It will treat each file in that folder as one frame in the animation. The order of the files is alphanumeric. By default the first file has an index of 0, second is 1, etc, regardless of their file names. Overriding the sample rate on the Trim parameter page will let you playback the animation at any frame rate.
Using an `info.xml` file in the directory containing a sequence of files allows you to specify the frames per second. Example xml file:
```
<?xml version="1.0" encoding="ISO-8859-1" standalone="yes" ?>
  <Settings>
      <attributes fps="30.0" />
  </Settings>
```
URLs can be used to fetch files. The file is downloaded to the user's Derivative temp directory and is read into the Point File In TOP.

Reload `reload` - Change from 0 to 1 to force the file to reload. Useful when the file changes or did not exist at first.
Reload Pulse `reloadpulse` - Immediately reload the point data file.
Red `red` - ⊞ - Select one of the available point data channels to place it into the red channel of the output image. Selecting One or Zero will place the constance value into the output channel.
* Zero `Zero` -
* One `One` -
Green `green` - ⊞ - Select one of the available point data channels to place it into the green channel of the output image. Selecting One or Zero will place the constance value into the output channel.
* Zero `Zero` -
* One `One` -
Blue `blue` - ⊞ - Select one of the available point data channels to place it into the blue channel of the output image. Selecting One or Zero will place the constance value into the output channel.
* Zero `Zero` -
* One `One` -
Alpha `alpha` - ⊞ - Select one of the available point data channels to place it into the alpha channel of the output image. Selecting One or Zero will place the constance value into the output channel.
* Zero `Zero` -
* One `One` -
  

## Parameters - Play Page
Play Mode `playmode` - ⊞ - Specifies the method used to play the animation, there are 3 options.
* Locked to Timeline `locked` - This mode locks the animation to the timeline. Scrubbing or jumping in the timeline will change the animation position accordingly. The parameters Play, Reset, Speed, and Index are disabled in this mode since the timeline is directly tied to position.
* Specify Index `specify` - This mode allows the user to specify a particular position in the animation using the Index parameter below. Use this mode for random access to any location in the movie.
* Sequential `sequential` - This mode continually plays regardless of the timeline position (the Index parameter is disabled). Reset and Speed parameters below are enabled to allow some control.
Play `play` - Animation plays when 1, stops when 0.
Speed `speed` - This is a speed multiplier which only works when Play Mode is *Sequential*. A value of 1 is the default playback speed. A value of 2 is double speed, 0.5 is half speed and so on. Negative values will play the animation backwards.
Cue `cue` - Jumps to Cue Point when set to 1. Only available when Play Mode is Sequential.
Cue Pulse `cuepulse` - Instantly jumps to the Cue Point position in the movie.
Cue Point `cuepoint` - Set any index in the animation as a point to jump to.
Cue Point Unit `cuepointunit` - ⊞ - Select the units for this parameter from Index, Frames, Seconds, and Fraction (percentage).
* I `indices` -
* F `frames` -
* S `seconds` -
* % `fraction` -
Cue Behavior `cuebehavior` - ⊞ - Customize the Cue parameter's behavior.
* On Release, Repeat Cued Frame `repeat` - When releasing the Cue parameter, immediately play the next frame.
* On Release, Play Next Frame `play` - When releasing the Cue parameter, first play the cued frame before continuing to play the next frame.
Index `index` - This parameter explicitly sets the file sequence position when Play Mode is set to Specify Index. The units menu on the right lets you specify the index in the following units: Index, Frames, Seconds, and Fraction (percentage). For example, assume you have a sequence that internally is 25 fps, and the timeline that is 60 fps. If you set Units to Index and the parameter value to 25, you get the image that is 1 second into the sequence. If you set the Units to Frames and set the value to 60 you get the same image at 1 second into the movie.
Index Unit `indexunit` - ⊞ - Select the units for this parameter from Index, Frames, Seconds, and Fraction (percentage).
* I `indices` -
* F `frames` -
* S `seconds` -
* % `fraction` -
Loop Crossfade `loopcrossfade` - Crossfades the beginning and end of the animation together to create a smooth transition when looping. If the movie uses Trim options, it will crossfade Trim Start with Trim End positions.
Loop Crossfade Unit `loopcrossfadeunit` - ⊞ - Select the units for this parameter from Index, Frames, Seconds, and Fraction (percentage).
* I `indices` -
* F `frames` -
* S `seconds` -
* % `fraction` -
Step Size `stepsize` - Sets how many frames to skip before displaying next frame. For example, a StepSize of 30 will display every 30th frame. The timing of the animation playback does not change, so with a Step Size of 30 and a sample rate of 30, a new frame will be displayed every second.
Audio Loop `audioloop` - ⊞ - This menu helps you determine how to treat the audio as the end of an animation approaches. This is needed because in some cases of playing an animation, like when driving with an index, the TOP will not know if you intend to loop it or not.
* Silence `silence` - Audio will go silent when the animation ends.
* Fade `fade` - Audio will fade out when the animation ends.
* Match Start to End `match` -
Image Sequence Indexing `imageindexing` - ⊞ - Determines how a file sequence is ordered.
* Zero Based `zero` - Index the sequence of files starting at 0, after sorting them alphanumerically.
* Filename Based `filename` - Index the sequence of files using the numbers on the end of the filenames. I.e a file named flower400.obj will be frame index 400, regardless of if there are other files in the directory before it.
Interpolate Frames `interp` - Interpolates between frames based based on exact time. For example, if the index (in frames) is 1.5, then frames 1 and 2 will be blended 50-50. If the index is 1.7 then 30% of frame 1 is blended with 70% of frame 2 and so on.
Loading/Error Image `loadingerrorimage` - ⊞ - When the file can not be loaded for some reason, select what to display instead.
* Colored Bottom Right Square `coloredbottomright` -
* Zero `zero` -
  

## Parameters - Trim Page
Trim `trim` - Enables the parameters below to set trim in and out points.
Trim Start `tstart` - Trim the starting point of the movie.
Trim Start Unit `tstartunit` - ⊞ - Select the units for this parameter from Index, Frames, Seconds, and Fraction (percentage).
* I `indices` -
* F `frames` -
* S `seconds` -
* % `fraction` -
Trim End `tend` - Trim the ending point of the movie.
Trim End Unit `tendunit` - ⊞ - Select the units for this parameter from Index, Frames, Seconds, and Fraction (percentage).
* I `indices` -
* F `frames` -
* S `seconds` -
* % `fraction` -
Extend Left `textendleft` - ⊞ - Determines how the Point File In TOP handles animation positions that lie before the Trim Start position. For example, if Trim Start is set to 1, and the animation's current index is -10, the Extend Left menu determines how the animation position is calculated.
* Hold `hold` - Displays the first frame in the animation range (the frame specified by Trim Start) for any position before Trim Start.
* Cycle `cycle` - Loops the movie range continuously.
* Mirror `mirror` - Loops the animation range in a zig-zag pattern. For example, playing backwards from Trim Start the animation will index will climb towards Trim End, at which point is will decend down towards Trim Start again and continue to zig-zag (or mirror) the further the animation plays backwards.
* Black `black` - Displays black frame for any animation position before Trim Start.
* Zero `zero` -
Extend Right `textendright` - ⊞ - Determines how the Point File In TOP handles animation positions that lie after the Trim End position. For example, if Trim End is set to 20, and the animation's current index is 25, the Extend Right menu determines how the movie position is calculated.
* Hold `hold` - Displays the last frame in the animation range (the frame specified by Trim End) for any position after Trim End.
* Cycle `cycle` - Loops the animation range continuously.
* Mirror `mirror` - Loops the animation range in a zig-zag pattern. For example, playing forwards from Trim End the movie will index will start decending towards Trim Start, at which point is will start climbing towards Trim End and continue to zig-zag (or mirror) the further the animation plays.
* Black `black` - Displays black frame for any animation position after Trim End.
* Zero `zero` -
Override Sample Rate `overridesample` - Turn On to change the sample rate of the movie. When loading an image sequence, use these parameters to set the playback speed for the sequence.
Sample Rate `samplerate` - Set the sample rate for playback when 'Override Sample Rate' above is On.
  

## Parameters - Tune Page
Pre-Read Frames `prereadframes` - Sets how many animation frames TouchDesigner reads ahead and stores in memory. The Point File In TOP will read and decode frames of the animation into CPU memory before they are used, this can eliminate pops or stutters in playback that occur from some frames taking too long to decode, other resources accessing the hard drive, or looping. When reading a sequence of files, having more Pre-Read Frames will allow multiple files to be decode at the same time. This allows playback of heavy file formats such as .exr in real-time, assuming the machine has enough CPU cores.
Frame Read Timeout `frametimeout` - The time (in milliseconds) TouchDesigner will wait for a frame from the hard drive before giving up. If the Disk Read Timeout time is reached, that frame is simply skipped. This also works for network files that are downloaded via http://.
Frame Timeout Strategy `frametimeoutstrat` - ⊞ - When on, if the Disk Read Timeout is reached TouchDesigner will use the latest available frame in place of the skipped frame.
* Keep Frame `keep` - Keep showing the same frame that is currently being output.
* Best for Playback `playback` - Try to pick the best frame for playback. This may be a newer frame that what is shown, but not quite the frame that is requested.
* Best for Seeking `seeking` - Try to show any frame, either before or after the target frame. Good for when seeking the movie via a shuttle widget in a UI.
Always Load Initial Frame `alwaysloadinitial` - If this parameter is turned on, then for the first loaded frame the Frame Read Timeout will be ignored, and it will always wait for the first frame to ensure the node always starts up with a valid image.
File Open Timeout `opentimeout` - The time (in milliseconds) TouchDesigner will wait for a file to open. If the Disk Open Timout is reached, the Point File In TOP will stop waiting and make its image all black, with a grey square in the bottom right corner. If the file still isn't opened the next time the TOP cooks, it'll wait again, and do the same. It'll keep doing this until the file is opened, or the open fails.
Async Upload to GPU `asyncupload` - When enabled, this will use OpenGL features to upload movie images to the GPU asynchronously. This will reduce the cook time of the Movie File In TOP considerably (in the performance monitor the lines that say "Uploading Image to GPU" will go down to almost nothing). There is a GPU memory cost to using this feature however. It uses up another (Width \* Height \* 4 \* Read Ahead Size) bytes of GPU memory. If you are having poor results with this feature, make sure your graphics drivers are up to date.
Update Image `updateimage` - Image will not update when set to 0. Animation index will continue to move forward but the output image will not update.
Max Decode CPUs `maxdecodecpus` - Limit the maximum number of CPUs that will be used to decode certain file codecs that are capable of multi-CPU decoding.
High Performance Read `highperfread` - This option should be used when playing back files that require very high SSD read speeds. It greatly improves read performance in those cases. It should not be used for low resolution or low data rate files.
High Performance Read Factor `highperfreadfactor` - When doing high performance reads, this parameter controls the size of the read operations that are done on disk. Whatever the largest operation the codec asks to be done, this is multiplied by the read factor and all subsequent reads will read that much data instead. This can result in higher throughput depending on the drives. For example if a request is made to read 1MB and the factor is set to 3, then instead the operations will read 3MB from the disk and the extra 2MB read will be ready for the next frame and will likely already have the next 2 frames available in CPU RAM.
Hardware Decode `hwdecode` - Controls if this node should use hardware decoding via the Nvidia hardware decoder chip. You can check if hardware decoding is being used using the Info CHOP, 'hardware\_decode' channel. This parameter does nothing for Hap and NotchLC codecs, which are always hardware decoded.
  

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
Extra Information for the Point File In TOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific Point File In TOP Info Channels
* num\_points -
* num\_loaded\_points -
* num\_src\_points -
* num\_channels -
* index -
* true\_index -
* index\_fraction -
* file\_resx -
* file\_resy -
* start -
* length -
* sample\_rate -
* last\_index\_uploaded -
* mv\_has\_audio -
* preloading -
* odd\_field -
* last\_frame -
* loop\_frame -
* pre\_read\_misses -
* last\_pre\_read\_miss\_wait -
* hard\_drive\_timeouts -
* num\_pre\_read\_frames -
* first\_index\_to\_read -
* last\_frame\_hd\_read\_time -
* last\_frame\_decode\_time -
* last\_gpu\_upload\_time -
* open -
* opening -
* open\_failed -
* fully\_pre\_read -
* true\_length -
* hardware\_yuv\_to\_rgb -
* has\_non\_av\_track -
* pre\_read\_fails -
* disk\_read\_mbit\_rate -
* has\_decode\_errors -
* num\_decode\_chunks -
* hardware\_decode -
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
  
TouchDesigner Build: Latest\nwikieditorwikieditor2021.100002020.20000before 2020.20000
| TOPs |
| --- |
| [Add](Add_TOP.html "Add TOP") • [Analyze](Analyze_TOP.html "Analyze TOP") • [Anti Alias](Anti_Alias_TOP.html "Anti Alias TOP") • [Blob Track](Blob_Track_TOP.html "Blob Track TOP") • [Bloom](Bloom_TOP.html "Bloom TOP") • [Blur](Blur_TOP.html "Blur TOP") • [Cache Select](Cache_Select_TOP.html "Cache Select TOP") • [Cache](Cache_TOP.html "Cache TOP") • [Channel Mix](Channel_Mix_TOP.html "Channel Mix TOP") • [CHOP to](CHOP_to_TOP.html "CHOP to TOP") • [Chroma Key](Chroma_Key_TOP.html "Chroma Key TOP") • [Circle](Circle_TOP.html "Circle TOP") • [Composite](Composite_TOP.html "Composite TOP") • [Constant](Constant_TOP.html "Constant TOP") • [Convolve](Convolve_TOP.html "Convolve TOP") • [Corner Pin](Corner_Pin_TOP.html "Corner Pin TOP") • [CPlusPlus](CPlusPlus_TOP.html "CPlusPlus TOP") • [Crop](Crop_TOP.html "Crop TOP") • [Cross](Cross_TOP.html "Cross TOP") • [Cube Map](Cube_Map_TOP.html "Cube Map TOP") • [Depth](Depth_TOP.html "Depth TOP") • [Difference](Difference_TOP.html "Difference TOP") • [Direct Display Out](Direct_Display_Out_TOP.html "Direct Display Out TOP") • [DirectX In](DirectX_In_TOP.html "DirectX In TOP") • [DirectX Out](DirectX_Out_TOP.html "DirectX Out TOP") • [Displace](Displace_TOP.html "Displace TOP") • [Edge](Edge_TOP.html "Edge TOP") • [Emboss](Emboss_TOP.html "Emboss TOP") • [Feedback](Feedback_TOP.html "Feedback TOP") • [Fit](Fit_TOP.html "Fit TOP") • [Flip](Flip_TOP.html "Flip TOP") • [Function](Function_TOP.html "Function TOP") • [GLSL Multi](GLSL_Multi_TOP.html "GLSL Multi TOP") • [GLSL](GLSL_TOP.html "GLSL TOP") • [HSV Adjust](HSV_Adjust_TOP.html "HSV Adjust TOP") • [HSV to RGB](HSV_to_RGB_TOP.html "HSV to RGB TOP") • [Import Select](Import_Select_TOP.html "Import Select TOP") • [In](In_TOP.html "In TOP") • [Inside](Inside_TOP.html "Inside TOP") • [Introduction To s Vid](Introduction_To_TOPs_Vid.html "Introduction To TOPs Vid") • [Kinect Azure Select](Kinect_Azure_Select_TOP.html "Kinect Azure Select TOP") • [Kinect Azure](Kinect_Azure_TOP.html "Kinect Azure TOP") • [Kinect](Kinect_TOP.html "Kinect TOP") • [Layout](Layout_TOP.html "Layout TOP") • [Leap Motion](Leap_Motion_TOP.html "Leap Motion TOP") • [Lens Distort](Lens_Distort_TOP.html "Lens Distort TOP") • [Level](Level_TOP.html "Level TOP") • [Limit](Limit_TOP.html "Limit TOP") • [Lookup](Lookup_TOP.html "Lookup TOP") • [Luma Blur](Luma_Blur_TOP.html "Luma Blur TOP") • [Luma Level](Luma_Level_TOP.html "Luma Level TOP") • [Math](Math_TOP.html "Math TOP") • [Matte](Matte_TOP.html "Matte TOP") • [Mirror](Mirror_TOP.html "Mirror TOP") • [Monochrome](Monochrome_TOP.html "Monochrome TOP") • [MoSys](MoSys_TOP.html "MoSys TOP") • [Movie File In](Movie_File_In_TOP.html "Movie File In TOP") • [Movie File Out](Movie_File_Out_TOP.html "Movie File Out TOP") • [MPCDI](MPCDI_TOP.html "MPCDI TOP") • [Multiply](Multiply_TOP.html "Multiply TOP") • [Ncam](Ncam_TOP.html "Ncam TOP") • [NDI In](NDI_In_TOP.html "NDI In TOP") • [NDI Out](NDI_Out_TOP.html "NDI Out TOP") • [Noise](Noise_TOP.html "Noise TOP") • [Normal Map](Normal_Map_TOP.html "Normal Map TOP") • [Notch](Notch_TOP.html "Notch TOP") • [Null](Null_TOP.html "Null TOP") • [Nvidia Background](Nvidia_Background_TOP.html "Nvidia Background TOP") • [Nvidia Denoise](Nvidia_Denoise_TOP.html "Nvidia Denoise TOP") • [Nvidia Flex](Nvidia_Flex_TOP.html "Nvidia Flex TOP") • [Nvidia Flow](Nvidia_Flow_TOP.html "Nvidia Flow TOP") • [Nvidia Upscaler](Nvidia_Upscaler_TOP.html "Nvidia Upscaler TOP") • [OAK Select](OAK_Select_TOP.html "OAK Select TOP") • [Oculus Rift](Oculus_Rift_TOP.html "Oculus Rift TOP") • [OP Viewer](OP_Viewer_TOP.html "OP Viewer TOP") • [OpenColorIO](OpenColorIO_TOP.html "OpenColorIO TOP") • [OpenVR](OpenVR_TOP.html "OpenVR TOP") • [Optical Flow](Optical_Flow_TOP.html "Optical Flow TOP") • [Orbbec Select](Orbbec_Select_TOP.html "Orbbec Select TOP") • [Orbbec](Orbbec_TOP.html "Orbbec TOP") • [Ouster Select](Ouster_Select_TOP.html "Ouster Select TOP") • [Ouster](Ouster_TOP.html "Ouster TOP") • [Out](Out_TOP.html "Out TOP") • [Outside](Outside_TOP.html "Outside TOP") • [Over](Over_TOP.html "Over TOP") • [Pack](Pack_TOP.html "Pack TOP") • [Photoshop In](Photoshop_In_TOP.html "Photoshop In TOP") • Point File In• [Point File Select](Point_File_Select_TOP.html "Point File Select TOP") • [Point Transform](Point_Transform_TOP.html "Point Transform TOP") • [PreFilter Map](PreFilter_Map_TOP.html "PreFilter Map TOP") • [Projection](Projection_TOP.html "Projection TOP") • [Ramp](Ramp_TOP.html "Ramp TOP") • [RealSense](RealSense_TOP.html "RealSense TOP") • [Rectangle](Rectangle_TOP.html "Rectangle TOP") • [Remap](Remap_TOP.html "Remap TOP") • [Render Pass](Render_Pass_TOP.html "Render Pass TOP") • [Render Select](Render_Select_TOP.html "Render Select TOP") • [Render](Render_TOP.html "Render TOP") • [RenderStream In](RenderStream_In_TOP.html "RenderStream In TOP") • [RenderStream Out](RenderStream_Out_TOP.html "RenderStream Out TOP") • [Reorder](Reorder_TOP.html "Reorder TOP") • [Resolution](Resolution_TOP.html "Resolution TOP") • [RGB Key](RGB_Key_TOP.html "RGB Key TOP") • [RGB to HSV](RGB_to_HSV_TOP.html "RGB to HSV TOP") • [Scalable Display](Scalable_Display_TOP.html "Scalable Display TOP") • [Screen Grab](Screen_Grab_TOP.html "Screen Grab TOP") • [Screen](Screen_TOP.html "Screen TOP") • [Script](Script_TOP.html "Script TOP") • [Select](Select_TOP.html "Select TOP") • [Shared Mem In](Shared_Mem_In_TOP.html "Shared Mem In TOP") • [Shared Mem Out](Shared_Mem_Out_TOP.html "Shared Mem Out TOP") • [SICK](SICK_TOP.html "SICK TOP") • [Slope](Slope_TOP.html "Slope TOP") • [Spectrum](Spectrum_TOP.html "Spectrum TOP") • [SSAO](SSAO_TOP.html "SSAO TOP") • [Stype](Stype_TOP.html "Stype TOP") • [Substance Select](Substance_Select_TOP.html "Substance Select TOP") • [Substance](Substance_TOP.html "Substance TOP") • [Subtract](Subtract_TOP.html "Subtract TOP") • [SVG](SVG_TOP.html "SVG TOP") • [Switch](Switch_TOP.html "Switch TOP") • [Syphon Spout In](Syphon_Spout_In_TOP.html "Syphon Spout In TOP") • [Syphon Spout Out](Syphon_Spout_Out_TOP.html "Syphon Spout Out TOP") • [Text](Text_TOP.html "Text TOP") • [Texture 3D](Texture_3D_TOP.html "Texture 3D TOP") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Threshold](Threshold_TOP.html "Threshold TOP") • [Tile](Tile_TOP.html "Tile TOP") • [Time Machine](Time_Machine_TOP.html "Time Machine TOP") • [TOP](TOP.html "TOP") • [Experimental:TOP](Experimental_TOP.html "Experimental:TOP") • [TOP Viewer](TOP_Viewer.html "TOP Viewer") • [Touch In](Touch_In_TOP.html "Touch In TOP") • [Touch Out](Touch_Out_TOP.html "Touch Out TOP") • [Transform](Transform_TOP.html "Transform TOP") • [Under](Under_TOP.html "Under TOP") • [Video Device In](Video_Device_In_TOP.html "Video Device In TOP") • [Video Device Out](Video_Device_Out_TOP.html "Video Device Out TOP") • [Video Stream In](Video_Stream_In_TOP.html "Video Stream In TOP") • [Video Stream Out](Video_Stream_Out_TOP.html "Video Stream Out TOP") • [Vioso](Vioso_TOP.html "Vioso TOP") • [Web Render](Web_Render_TOP.html "Web Render TOP") • [Experimental:ZED Select](Experimental_ZED_Select_TOP.html "Experimental:ZED Select TOP") • [ZED](ZED_TOP.html "ZED TOP") • [Experimental:ZED](Experimental_ZED_TOP.html "Experimental:ZED TOP") |
Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

The panel at the bottom of TouchDesigner, it controls the current global looping [Time](Time_COMP.html "Time COMP") your TouchDesigner project, or of just one component.

The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).

samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP") can set the image resolution. See [Aspect Ratio](TOP_Generator_Common_Page.html "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").

Retrieved from "<https://docs.derivative.ca/index.php?title=Point_File_In_TOP&oldid=29950>"
[Category](Special_Categories.html "Special:Categories"):
* [TOPs](Category_TOPs.html "Category:TOPs")