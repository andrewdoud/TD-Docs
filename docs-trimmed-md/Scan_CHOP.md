

Scan CHOP - TouchDesigner Documentation




# Scan CHOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Scan CHOP converts a [SOP](SOP.html "SOP") or [TOP](TOP.html "TOP") to oscilloscope or laser friendly control waves. The output is usually in the audible range and can be heard directly via an [Audio Device Out CHOP](Audio_Device_Out_CHOP.html "Audio Device Out CHOP"), or used to drive the X and Y deflector inputs of an oscilloscope, or a laser projector recreating the imagery.
The output can also be visualized through use of a [Limit SOP](Limit_SOP.html "Limit SOP").
A sample component found at: [Op to Audio CHOP example](http://www.derivative.ca/Forum/viewtopic.php?f=22&t=1201)
A sample video can be found at: [Total Internal Reflection](http://vimeo.com/channels/touchdesigner#3750626)
See also: [EtherDream CHOP](EtherDream_CHOP.html "EtherDream CHOP"), [EtherDream DAT](EtherDream_DAT.html "EtherDream DAT")
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[scanCHOP\_Class](https://docs.derivative.ca/ScanCHOP_Class "ScanCHOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Scan Page](#Parameters_-_Scan_Page)
* [3 Parameters - TOP Page](#Parameters_-_TOP_Page)
* [4 Parameters - SOP Page](#Parameters_-_SOP_Page)
* [5 Parameters - CHOP Page](#Parameters_-_CHOP_Page)
* [6 Parameters - Common Page](#Parameters_-_Common_Page)
  

## Parameters - Scan Page
Source OP `source` - ⊞ - Choose the source node family.
* TOP `top` - A raster image is converted to control signals by converting each pixel's location to X and Y amplitude values.
* SOP `sop` - A geometry is converted to control signals by converting each point's position to X and Y amplitude values.
* CHOP `chop` - A waveform is converted to control signals by converting each graph into corresponding horizontal and vertical offsets.
Sample Rate `rate` - Samples per second, the output sample rate.
Swap Output `swap` - Reverse the X and Y channel outputs.
X Scale `xscale` - Scale the x amplitude.
Y Scale `yscale` - Scale the y amplitude.
Rotate `rotate` - Specified in degrees, rotates the output x,y values.
Randomize Samples `randomize` - Output all samples in a random order. Creates a fuzzy chaotic image on an oscilloscope.
Output Color `color` - If on, r,g,b channels are created.If on, r,g,b channels are created.
Red Scale `redscale` - Scale the output r channel.
Green Scale `greenscale` - Scale the output g channel.
Blue Scale `bluescale` - Scale the output b channel.
Blanking Count `blankingcount` - In the case of SOP input, the number of black/off positions to insert between geometry primitives. In the case of TOP input, the number of black/off positions to insert between full raster scans. Color output must be enabled.In the case of SOP input, the number of black/off positions to insert between geometry primitives. In the case of TOP input, the number of black/off positions to insert between full raster scans. Color output must be enabled.
  

## Parameters - TOP Page
A raster image is converted to control signals by converting each pixel's location to X and Y amplitude values. The luminance is controlled by how long each sample is "drawn" on the scope. Since the output is low bandwidth, different resampling and ordering options are available for minimizing (or enhancing) flicker.
TOP `top` - Path to the TOP node.
Width `width` - The number of columns to resample the image at.
Height `height` - The number of rows to resample the image at.
Level `level` - The number of brightness levels each pixel can have.
Auto Reduce `limit` - Automatically reduce the number of rows and columns dynamically to keep the output frame rate
at a constant level.

Layered `layered` - Output the pixels in order of brightness, else they are output left to right for each row.
Interleave `interleave` - ⊞ - Controls the order in which rows are output to minimize flicker.
* Sweep `sweep` - The rows are output in order, from top to bottom.
* Even Odd `evenodd` - The rows are output in two passes, first even, then odd.
* Max `max` - The rows are output in fully interleaved fashion.
  

## Parameters - SOP Page
Every point in a SOP creates a frame-buffered, stereo audio sample, where the SOP vertex X is placed on the X channel and Y is placed on the Y channel. The oscilloscope output thus contains no aliased lines, just razor-sharp vectors.
SOP `sop` - Path to the SOP node.
Vertex Order `vertexorder` - Output the points in the same order as the vertices of each polygon, instead of the order in which the points are defined in the geometry.
Limit Step Size `limitstep` - Breakup long x,y jumps into several smaller incremental jumps.
Step Size `stepsize` - The distance each x,y can change when above option enabled.
Vertex Repeat `vertexrepeat` - Repeat each vertex of the each primitive multiple times.
Camera `camera` - Project the geometry onto a 2D plane from this camera, otherwise, only the original x,y components of the geometry are used.
  

## Parameters - CHOP Page
A waveform is converted to control signals by converting each graph into corresponding horizontal and vertical offsets, reproducing the original CHOP waveform. The CHOP should not be [Time Sliced](https://docs.derivative.ca/index.php?title=Time_Slice&action=edit&redlink=1 "Time Slice (page does not exist)"), but instead have some length (example a [Trail CHOP](Trail_CHOP.html "Trail CHOP") or animated [Wave CHOP](Wave_CHOP.html "Wave CHOP")).
CHOP `chop` - Path to the CHOP node.
Trigger `trigger` - The output graph will begin where its value exceeds this value. This allows for steady 'frozen' waveforms, analagous to an oscilloscope triggered sweep.
Trigger Value `triggerval` - The value to begin the trigger.
Trim `trim` - Limit the length of the CHOP to be scanned.
Trim Value `trimval` - The length of the CHOP to be scanned.
Trim Units `trimunits` - Select the units to use for this parameter, Samples, Frames, or Seconds.
  

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
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • Scan• [Script](Script_CHOP.html "Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.

A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.

TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.

Retrieved from "<https://docs.derivative.ca/index.php?title=Scan_CHOP&oldid=27197>"
[Category](Special_Categories.html "Special:Categories"):
* [CHOPs](Category_CHOPs.html "Category:CHOPs")