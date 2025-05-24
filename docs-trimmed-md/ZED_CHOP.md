

ZED CHOP - TouchDesigner Documentation





# ZED CHOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
**NOTE**
**OS:** This operator is only supported under the **Microsoft Windows** operating system.  

The ZED CHOP reads positional and plane tracking from the ZED camera. It can additionally use a UV to find plane in the room, and return information about that plane such as it's size/orientation either relative to the camera, or the room itself.
Additionally, the ZED CHOP can do skeleton tracking by enabling the 'Body Tracking' menu.
**NOTE:** This CHOP works with the [Stereolabs ZED](https://www.stereolabs.com/zed/) hardware.
For more information and to know what ZED SDK to install refer to the [ZED](ZED.html "ZED") article.
See also [ZED TOP](ZED_TOP.html "ZED TOP") and [ZED SOP](ZED_SOP.html "ZED SOP").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[zedCHOP\_Class](https://docs.derivative.ca/ZedCHOP_Class "ZedCHOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - ZED Page](#Parameters_-_ZED_Page)
* [3 Parameters - Common Page](#Parameters_-_Common_Page)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Common CHOP Info Channels](#Common_CHOP_Info_Channels)
  + [4.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - ZED Page
Active `active` - When 'On' data is captured from the ZED camera.
Camera `camera` - Selects which ZED camera to use.
Camera Transform `cameratransform` -
Camera Transform `resetcameratransform` - Zeros out the current camera position, effectively makes the current position the new origin.
Plane Orientation `planeorientation` - Enables plane at point, which returns the position of the plane corresponding the UV coordinate.
Get Plane `getplane` - Returns the camera position relative to the initial position of the camera. A `tx`, `ty`, `tz` triplet of channels will be output for the position of the camera in meters. An `rx`, `ry`, `rz` triplet will be output for the orientation.
Pulse `getplanepulse` -
Plane Reference Frame `planereferenceframe` - ⊞ - Controls if the panel coordinates will be given relative to the camera or the world.
* World `world` -
* Camera `camera` -
Plane Point U `planepointu` - Sets the U coordinate of the point in the image to extract plane position.
Plane Point V `planepointv` - Sets the V coordinate of the point in the image to extract plane position.
Plane Position `planeposition` - Returns `tx`, `ty`, and `tz` position channels of the center of the plane.
Plane Rotation `planerotation` - Returns `rx`, `ry`, and `rz` rotation channels for the plane.
Plane Normal `planenormal` - Returns `nx`, `ny`, and `nz` normal channels of the plane.
Plane Size `planesize` - Returns size of the bounding rectangle of the plane.
Body Tracking `bodytracking` - ⊞ - Body tracking allows for tracking human skeletons that are found in the video frame. Each mode uses an AI model that will need to be trained one for your GPU. This will take several minutes, but only needs to be done once per model per machine, as long as the GPU isn't changed. For models where the 'Joint Mode' parameter is disabled, the outputs will be 'Absolute'.
* Off `off` - Body Tracking is disabled.
* Skeleton - 18 Joints `skeleton18` - Tracks an 18 joint skeleton as described in [this article](https://www.stereolabs.com/docs/body-tracking/).
* Skeleton - 34 Joints `skeleton34` - Tracks an 34 joint skeleton as described in [this article](https://www.stereolabs.com/docs/body-tracking/). The positions and rotations are relative to the parent joints, as described in that article, where the 0 joint is the 'root' joint.
Max Bodies `maxbodies` - The maximum number of bodies that will be tracked.
Body 3D `body3d` - Enable to output 3D positions. Rotations will be included if the Joint Mode is set to 'Relative'.
Joint Mode `jointmode` - ⊞ - Controls if the joint values are given in absolute in scene or relative to each other.
* Absolute Position `absolute` - Absolute XYZ positions of each in space, given in meters.
* Relative, with Orientation `relative` - 3D skeleton positions and rotations in heriachical terms, each relative to a parent joint.
Body 2D `body2d` - 2D normalized UV coordinates for each joint, giving their position within the image.
Aspect Correct UVs `aspectcorrectuv` - Apply a correct to the UVs so they as aspect correct.
  

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
Extra Information for the ZED CHOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2021.100002018.28070before 2018.28070
| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • ZED• [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").
The grey dashed lines between nodes is a Reference (or [Link](Link.html "Link")). A Reference is (1) a [Parameter Reference](Parameter_Reference.html "Parameter Reference"), a parameter in an OP that is a name or path to another operator, (2) a [Node Reference](https://docs.derivative.ca/index.php?title=Node_Reference&action=edit&redlink=1 "Node Reference (page does not exist)"), an expression in a parameter or DAT script that contains the name or path of another operator, (3) a DAT Cell Reference or (4) a CHOP Channel Reference.
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").

The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.

A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.

samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.

TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.

Retrieved from "<https://docs.derivative.ca/index.php?title=ZED_CHOP&oldid=32535>"
[Category](Special_Categories.html "Special:Categories"):
* [CHOPs](Category_CHOPs.html "Category:CHOPs")