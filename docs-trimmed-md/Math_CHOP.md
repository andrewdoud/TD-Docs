

Math CHOP - TouchDesigner Documentation





























# Math CHOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Math CHOP performs arithmetic operations on channels. The channels of a CHOP can be combined into one channel, and several CHOPs can be combined into one CHOP.

The OP page lets you pre-operate on each sample, like making all samples positive or taking the square of each sample.

Using **Combine Channels**, for an input CHOP with multi-channels, you can multiply the samples of one channel by the samples in the other channels, reducing N channels down to one. You can combine them by multiplying, adding, finding the maximum, etc..

Using **Combine CHOPs**, where there are two or more CHOP inputs, you can multiply (or add, etc.) the channels in one CHOP with the channels in all the other CHOPs, reducing N CHOPs to 1. (otherwise channels of multi-inputs are just merged)

You can then post-operate on the resulting samples - negate, square root, etc.

Then using the Mult-Add page it can offset and scale the values of each sample.

More conveniently you can use the Range page to do linear scaling as well by setting an output low-high range for a certain input low-high range.

Finally, you can round the resulting values off to an integer.

**Tip**: You can affect only certain channels of your input by using the Scope parameter on the Common page.

**Note**: To do logic operations (and, or, ...) between channels or CHOPs, use the [Logic CHOP](Logic_CHOP.html "Logic CHOP").

**Tip: Customizing each channel:**: You can use the local member `chanIndex` in a parameter like Post-Add, for example, `me.chanIndex*2` to give a different post-add value for each channel. `chanIndex` is available in numerous CHOPs like the [Pattern CHOP](Pattern_CHOP.html "Pattern CHOP"). (expressions are non-optimized)

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[mathCHOP\_Class](https://docs.derivative.ca/MathCHOP_Class "MathCHOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - OP Page](#Parameters_-_OP_Page)
* [3 Parameters - Mult-Add Page](#Parameters_-_Mult-Add_Page)
* [4 Parameters - Range Page](#Parameters_-_Range_Page)
* [5 Parameters - Common Page](#Parameters_-_Common_Page)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common CHOP Info Channels](#Common_CHOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - OP Page

The four steps are performed in the following order:

Channel Pre OP `preop` - ⊞ - Unary operations can be performed on individual channels. A menu of unary operations (as described above) that are performed on each channel as it comes in to the Math CHOP include:

* Off `off` - Don't do anything to the channel.

* Negate `negate` - Take the negative value of each sample of the channel.

* Positive `pos` - Make negative values of the channel positive (absolute).

* Root `root` - Take the square root of all values in the channel.

* Square `square` - Square all the values in the channel.

* Inverse `inverse` - Take the inverse (1/x) of all values in the channel.

Combine Channels `chanop` - ⊞ - A choice of operations is performed between the channels of an input CHOP, for each input. The Nth sample of one channel is combined with the Nth sample of other channels:

* Off `off` - Don't combine the channels.

* Add `add` - Sum all the channels.

* Subtract `sub` - Subtract all the channels from the first.

* Multiply `mul` - Multiply all the channels.

* Divide `div` - Divide the first channel by all the rest.

* Average `avg` - Take the average of all the channels.

* Minimum `min` - Take the minimum value of all the channels.

* Maximum `max` - Take the maximum value of all the channels.

* Length `len` - Assume the channels are a vector and compute its length.

Combine CHOPs `chopop` - ⊞ - A menu of operations that is performed between the input CHOPs, combining several CHOPs into one.

* Off `off` - Don't combine the channels.

* Add `add` - Sum all the channels.

* Subtract `sub` - Subtract all the channels from the first.

* Multiply `mul` - Multiply of all the channels.

* Divide `div` - Divide the first channel by all the rest.

* Average `avg` - Take the average of all the channels.

* Minimum `min` - Take the minimum value of all the channels.

* Maximum `max` - Take the maximum value of all the channels.

* Length `len` - Assume the channels are a vector and compute its length.

Channel Post OP `postop` - ⊞ - A menu (same as Channel Pre OP) is performed as the finale stage upon the channels resulting from the above operations.

* Off `off` -

* Negate `negate` -

* Positive `pos` -

* Root `root` -

* Square `square` -

* Inverse `inverse` -

Match by `match` - ⊞ - Match channels between inputs by name or index.

* Channel Number `index` -

* Channel Name `name` -

Align `align` - ⊞ - This menu handles cases where multiple input CHOPs have different start or end times. All channels output from a CHOP share the same start/end interval, so the inputs must be treated with the Align Options:

* Automatic `auto` - It will trim to the current [Time Slice](https://docs.derivative.ca/index.php?title=Time_Slice&action=edit&redlink=1 "Time Slice (page does not exist)") if there are any Time Slices, else it will do an Extend Min/Max.

* Extend to Min/Max `none` - Find the earliest start and latest end, and extend all inputs to that range using the extend conditions. (see [Extend Conditions](Extend_Conditions.html "Extend Conditions")).

* Stretch to Min/Max `stretch` - Find the earliest start and latest end, and stretch every channel's start and end to that range.

* Shift to Minimum `start` - Find the earliest start and shift all channels so they all start at that index. All channels are extended to the length of the longest one.

* Shift to Maximum `end` - Find the latest end and shift all channels so they all end at that index. Extend all channels to the length of the longest one.

* Shift to First Interval `shift1` - Shift all channels to the start of the first CHOP and sample all inputs using the first input's range.

* Trim to First Interval `trim1` - Trim all channels to first CHOP's range.

* Stretch to First Interval `stretch1` - Stretch all channels to the first CHOP's range.

* Trim to Smallest Interval `trim` - Trim all channels to the smallest start/end interval. The start and end values may not come from the same channel.

* Stretch to Smallest Interval `squash` - Stretch all channels to the smallest start/end interval. The start and end values may not come from the same channel.

Interp Pars per Sample `interppars` - Use this option when the input is a higher frequency than the timeline (example: audio). It will avoid any pops or crackles in the output when adjusting the multiply, add or range parameters.
Integer `integer` - ⊞ - The resulting values can be converted to integer.

* Off `off` - Don't affect the value.

* Ceiling `ceiling` - Round a value up to the next integer.

* Floor `floor` - Round a value down to the next integer.

* Round `round` - Round a value to the nearest integer.

  


## Parameters - Mult-Add Page

The three steps are next performed in the following order:

Pre-Add `preoff` - First, add the value to each sample of each channel.
Multiply `gain` - Then multiply by this value.
Post-Add `postoff` - Then add this value.

  


## Parameters - Range Page

This is the final step prior to output.

From Range `fromrange` - ⊞ - Another way to multiply/add. Converts from one low-high range to another range.

* `fromrange1` -

* `fromrange2` -

To Range `torange` - ⊞ - Another way to multiply/add. Converts from one low-high range to another range.

* `torange1` -

* `torange2` -

  


## Parameters - Common Page

Time Slice `timeslice` - Turning this on forces the channels to be "[Time Sliced](Time_Slicing.html "Time Slicing")". A Time Slice is the time between the last cook frame and the current cook frame.
Scope `scope` - To determine which channels get affected, some CHOPs use a Scope string on the Common page. See [Pattern Matching](Pattern_Matching.html "Pattern Matching").
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

  


## Operator Inputs

* Input 0:  -

  


## Info CHOP Channels

Extra Information for the Math CHOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070

| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • Math• [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.


samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.


A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.


samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.


Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.







Retrieved from "<https://docs.derivative.ca/index.php?title=Math_CHOP&oldid=27464>"
[Category](Special_Categories.html "Special:Categories"):

* [CHOPs](Category_CHOPs.html "Category:CHOPs")