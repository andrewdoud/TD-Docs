

Laser CHOP - TouchDesigner Documentation





























# Laser CHOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Laser CHOP produces channels that can drive a laser projector. It uses the points and lines of a SOP or CHOP and outputs the channels at a specified sample rate, typically 10,000 to 96,000 samples per second. The Laser CHOP gives optimal control over the movement of the reflectors of the laser projector as well as enhanced color control. In particular, it gives better control of lines being straight, end-points being not cut off or over-drawn, and eliminating tails, all adjustable using a set of parameters.

When sending CHOP channels to the Laser CHOP, the CHOP expects `x` and `y` channels and every sample will be interpreted as a point to be drawn. To draw multiple shapes, also specify a channel named `id` to identify each shape. Points with `id = 0` are part of the first shape, points with `id = 1` form the second shape. All other channels will be interpreted as color channels and blanking will be applied to those. This makes it possible to drive lasers that have more than just RGB diodes active.

The channels output from the Laser CHOP can be sent to the [Laser Device CHOP](Laser_Device_CHOP.html "Laser Device CHOP") in case of controlling a Laser via the [ILDA Protocol](https://en.wikipedia.org/wiki/International_Laser_Display_Association), or the [Audio Device Out CHOP](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") in case of using one of LaserAnimation Sollinger's [AVB](https://en.wikipedia.org/wiki/Audio_Video_Bridging) capable devices, where the audio is output via the [Audio Device Out CHOP](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") to a low-latency AVB-ready audio device like those from MOTU, RME, LaserAnimation Sollinger or Apple macOS.

[LaserAnimation Sollinger's AVB2ILDA devices](https://laseranimation.com/en/products/avb-devices) give you access to features for the professional sector including 24-bit resolution on the X/Y signal and all color channels. Additionally the AVB2ILDA device includes software for electronic masking, making it possible to limit the laser output for certain areas (for example to protect scanning areas such as auditoriums or sectors with optical equipment). Also packaged is a color correction tool that includes individual control of the color delay for 3 colors as well as a Digital Geometric Correction to allow for projection on for example uneven surfaces.

The CHOP was developed with the help of [LaserAnimation Sollinger](https://laseranimation.com/en/) who guided us in speccing and implementing the necessary parameters, especially in regards of the blanking timing settings.

**Tip**: See the [OP Snippets](OP_Snippets.html "OP Snippets") for setup and usage examples.

**LASERS ARE DANGEROUS - DAMAGE TO YOUR OR THE AUDIENCE'S EYE SIGHT IS A VERY REAL RISK**

* If you plan to use lasers

1. Understand all the laws and regulations for laser operation in your area.
2. Become a certified Laser Safety Officer (this is required by law in some areas). Courses are available from ILDA directly: [ILDA Laser Safety Courses](https://www.ilda.com/LSOcourse.htm)

* Make sure an emergency stop button is close to you at all times.
* Do not let anyone enter the laser projection area unless all precautions have been taken to limit the output.
* Make sure there are no reflective surfaces in the projection area that might cause the beam to reflect unintendedly.

(The Laser CHOP replaces the legacy Scan CHOP.)

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[laserCHOP\_Class](https://docs.derivative.ca/LaserCHOP_Class "LaserCHOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Laser Page](#Parameters_-_Laser_Page)
* [3 Parameters - Color Page](#Parameters_-_Color_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common CHOP Info Channels](#Common_CHOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Laser Page

Active `active` - When disabled, the CHOP will zero out all channels.
Source OP `source` - ⊞ - Select the source operator type for the laser image.

* SOP `sop` - Use a SOP as the source for the Laser image. Appart from position attributes, the SOP's point color attributes are used to determine the color output.

* CHOP `chop` - Use a CHOP as the source for the laser image. The CHOP expects `x` and `y` channels and every sample will be interpreted as a point to be drawn. To draw multiple shapes, also specify a channel named `id` to identify each shape. Points with `id = 0` are part of the first shape, points with `id = 1` form the second shape. All other channels will be interpreted as color channels and blanking will be applied to those. This makes it possible to drive lasers that have more than just RGB diodes active.

SOP `sop` - Path to the SOP.
CHOP `chop` - Path to the CHOP. The input CHOP must have **x**, **y** channels for the point positions. In addition, it also supports **z**, **r**, **g**, **b**, and **id** channels. The **id** channel is used for grouping points together as a single shape. By default when no **id** channel is present, each point is separate and unconnected. Additional and arbitrarily named colour channels may be added for laser projectors that accept more than just r, g, b.
Input Sample Rate `inputrate` - Specify the Sample Rate the input source will be sampled at. This can be lower than the output sample rate. If lower than the output sample rate then the output will be resampled (same as if put through a Resample CHOP).
Output Sample Rate `outputrate` - The sample rate of the CHOP, and the sample rate at which it will output to the laser. With the default 48000 samples per second and a 60fps frame rate, the Laser CHOP can output 800 position and color values per frame.
Swap Output `swap` - Lets you swap the x and y axis of the output.
X Scale `xscale` - Control the horizontal scale of the output.
Y Scale `yscale` - Control the vertical scale of the output.
Rotate `rotate` - Control the rotation of the output.
Update Method `updatemethod` - ⊞ - Control how the Laser CHOP pulls data from its source.

In most cases you will want to keep this at the default setting "When All Points Drawn".

There is a specific usage case that requires the "Every Frame" update method. Background is that the Laser CHOP might have to draw the input values over multiple frames. For example given a source with 200 sampling values. After applying all blanking and step sizes at a certain sample rate, the Laser might need more than one frame to draw the full image. The effect will be visible by the Laser image flickering. With the default setting, the Laser will grab a new set of samples from its input once it has completed drawing all previous values. With the "Every Frame" update method, the Laser will grab the updated values for the remaining samples after each frame.

* When All Points Drawn `alldrawn` - The Laser CHOP will read the source data once all points of the previous frame have been drawn.

* Every Frame `everyframe` - The Laser CHOP will update the input every frame, no matter if it finished drawing the previous frame or not.

Frame Start Pulse `startpulse` - When enabled, will insert a sample with all colors set to -1 at the beginning of the laser frame.
Vertex Order `vertexorder` - Output the points in the same order as the vertices of each polygon, instead of the order in which the points are defined in the geometry.
Step Size `stepsize` - The distance each x,y can change while outputing color.
Blanking Step Size `bstepsize` - The distance each x,y can change while not outputing color (blanking).
Minimum Vertex Hold `minverthold` - The minimum value of the vertex hold of a point. The value of the vertex hold of a point is calculated linearly in the range from the minimum to maximum vertex hold, based on the steepness of the angle at the point. This angle is calculated with the following three points: the previous point, the point itself, and the next point. Example: when the angle at the point is 180 degrees then the vertex hold of the point will be the minimum value.
Maximum Vertex Hold `maxverthold` - The maximum value of the vertex hold of a point. See Minimum Vertex Hold for more details. When the angle at the point is 0 degrees, then the vertex hold will be the maximum value. If the maximum value is lower than the minimum then the maximum will be clamped upward.
Camera `camera` - Specify the path to a Camera COMP used to draw a SOP from the cameras view.

  


## Parameters - Color Page

These parameters let you control how the color channels for the Laser are created. Especially paying attention to the blanking settings which will have to be adjusted matching the capabilities of your laser projector.

Blanking is the capability of a laser projector to rapidly turn on / off the laser when displaying animations. For example when displaying multiple shapes, the laser needs the ability of blanking to omit the empty spots between the shapes.
As the laser's mirrors are driven by motors, the positional data that is send to the laser is likely to be ahead of the actual mirror position - the mirror must catch up to the data. The Color data though is in time and as a result the effect can be visible tails at points where the laser switches off its color. Adjusting the blanking parameters can help prevent this.

Red Scale `redscale` - Set the intensity of the Red Channel.
Green Scale `greenscale` - Set the intensity of the Green Channel.
Blue Scale `bluescale` - Set the intensity of the Blue Channel.
Pre Blanking On Delay `preblankon` - Set the time in ms the Laser should wait at a position before turning the color output off.
Post Blanking On Delay `postblankon` - Set the time in ms the Laser should wait at a position after turning the color output off.
Pre Blanking Off Delay `preblankoff` - Set the time in ms the Laser should wait at a position before turning the color output on.
Post Blanking Off Delay `postblankoff` - Set the time in ms the Laser should wait at a position after turning the color output on.
Start-Point Hold Time `starthold` - Set the time in ms the Laser should wait at the first point of a new data frame before continuing on.
Color Delay `colordelay` - Set the delay in ms of the color channels in the output.

  


## Parameters - Common Page

Time Slice `timeslice` - Turning this on forces the channels to be "[Time Sliced](Time_Slicing.html "Time Slicing")". A Time Slice is the time between the last cook frame and the current cook frame.
Scope `scope` - To determine which channels get affected, some CHOPs use a Scope string on the Common page.
Sample Rate Match `srselect` - ⊞ - Handle cases where multiple input CHOPs' sample rates are different. When Resampling occurs, the curves are interpolated according to the Interpolation Method Option, or "Linear" if the Interpolate Options are not available.

* Resample At First Input's Rate `first` - Use rate of first input to resample others.

* Resample At Maximum Rate `max` - Resample to the highest sample rate.

* Resample At Minimum Rate `min` - Resample to the lowest sample rate.

* Error If Rates Differ `err` - Doesn't accept conflicting sample rates.

Export Method `exportmethod` - ⊞ - This will determine how to connect the CHOP channel to the parameter. Refer to the [Export](Export.html "Export") article for more information.

* DAT Table by Index `datindex` - Uses the docked DAT table and references the channel via the index of the channel in the CHOP.

* DAT Table by Name `datname` - Uses the docked DAT table and references the channel via the name of the channel in the CHOP.

* Channel Name is Path:Parameter `autoname` - The channel is the full destination of where to export to, such has `geo1/transform1:tx`.

Export Root `autoexportroot` - This path points to the root node where all of the paths that exporting by **Channel Name is Path:Parameter** are relative to.
Export Table `exporttable` - The DAT used to hold the export information when using the DAT Table Export Methods (See above).

  


## Info CHOP Channels

Extra Information for the Laser CHOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


### Common CHOP Info Channels

* start - Start of the CHOP interval in samples.

* length - Number of samples in the CHOP.

* sample\_rate - The samplerate of the channels in frames per second.

* num\_channels - Number of channels in the CHOP.

* time\_slice - 1 if CHOP is Time Slice enabled, 0 otherwise.

* export\_sernum - A count of how often the export connections have been updated.

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

  

TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2021.100002020.20000before 2020.20000

| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • Laser• [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Experimental:Parameter](Experimental_Parameter_CHOP.html "Experimental:Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [Experimental:POP to](Experimental_POP_to_CHOP.html "Experimental:POP to CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [Experimental:Resample](Experimental_Resample_CHOP.html "Experimental:Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Experimental:Script](Experimental_Script_CHOP.html "Experimental:Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Experimental:Touch In](Experimental_Touch_In_CHOP.html "Experimental:Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.


The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).


To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.


A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.


A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.


Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.


TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.







Retrieved from "<https://docs.derivative.ca/index.php?title=Laser_CHOP&oldid=33578>"
[Category](Special_Categories.html "Special:Categories"):

* [CHOPs](Category_CHOPs.html "Category:CHOPs")