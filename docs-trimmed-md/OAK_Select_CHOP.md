

OAK Select CHOP - TouchDesigner Documentation





























# OAK Select CHOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The OAK Select CHOP is like a [Script CHOP](Script_CHOP.html "Script CHOP") combined with a [Select CHOP](Select_CHOP.html "Select CHOP"), and any of the other hardware-specific CHOPs. The basic operation involves providing an [OAK Device CHOP](OAK_Device_CHOP.html "OAK Device CHOP") and a stream name. In the simplest case, the stream's data will show up as well-named channels. For example, [ImgDetections](https://docs.luxonis.com/projects/api/en/latest/components/messages/img_detections/) messages indicating the 2D coordinates and labels of detected objects will show up as CHOP channels without any manual coding. In more complex cases such as hand landmark tracking, the stream may be of [NNData](https://docs.luxonis.com/projects/api/en/latest/components/messages/nn_data/) or [Buffer](https://docs.luxonis.com/projects/api/en/latest/components/messages/buffer/) type, requiring the user to implement a callback and parse the data.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[oakselectCHOP\_Class](OakselectCHOP_Class.html "OakselectCHOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - OAK Page](#Parameters_-_OAK_Page)
* [3 Parameters - Common Page](#Parameters_-_Common_Page)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common CHOP Info Channels](#Common_CHOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  + [5.3 Script CHOP Functionality](#Script_CHOP_Functionality)
  + [5.4 Queue Size](#Queue_Size)
  + [5.5 Max Items](#Max_Items)
  + [5.6 Output Format](#Output_Format)
  + [5.7 Use First Sample Only](#Use_First_Sample_Only)
  + [5.8 Info CHOP](#Info_CHOP)
  + [5.9 See Also](#See_Also)

  


## Parameters - OAK Page

Active `active` - Toggle whether the OAK Select CHOP cooks.
OAK Device CHOP `chop` - An OAK Device CHOP running a depthai pipeline.
Stream `stream` - The name of the stream to be received.
Queue Size `queuesize` - For memory efficiency, this parameter controls the number of messages TouchDesigner reuses when receiving messages from OAK. See "Queue Size" below.
Max Items `maxitems` - This parameter helps the OAK Select CHOP output a consistent number of channels. When running an image detection pipeline, the number of detected items will vary from frame to frame, but we want TouchDesigner to output a consistent number of channels.
Output Format `outputformat` - ⊞ - The default option "Items As Separate Channels" enables time-slicing while "Items as Separate Samples" does not. If the stream is one which automatically fills in the CHOP, then "Items as Separate Samples" is a useful way to make the CHOP output **Max Items** samples consistently.

* Items As Separate Channels `itemsaschannels` -

* Items As Separate Samples `itemsassamples` -

Use First Sample Only `firstsample` - Only use the most recently received message with the OAK Select CHOP. For example, for an IMU stream which is sending very high-frame rate data, toggling this parameter will only show the latest sample.
Sample Rate `rate` - The sample rate of the CHOP. The default sample rate is `me.time.rate`.
Callbacks DAT `callbacks` - Specifies the DAT which holds the callbacks.
Setup Parameters `setuppars` - Clicking the button runs the setupParameters() callback function.

  


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

  


## Operator Inputs

## Info CHOP Channels

Extra Information for the oakselect CHOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\n2023.11280before 2023.11280

| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • OAK Select• [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |

  


### Script CHOP Functionality[[edit](https://docs.derivative.ca/index.php?title=OAK_Select_CHOP&action=edit&section=1 "Edit section: Script CHOP Functionality")]

The OAK Select CHOP mimics the [Script CHOP](Script_CHOP.html "Script CHOP") in several ways. There's a callback for `onSetupParameters`, where custom parameters can be added. Also, in the other callbacks such as `onReceiveNNData`, `onReceiveBuffer`, and `onReceiveSystemInformation` it's possible to append channels and write data. When implementing a custom callback like below, if you want to disable time-slicing or set the number of output samples, the **Output Format** parameter should be "Items as Separate Samples".

```
import depthai as dai
def onReceiveNNData(oakSelectOp, oakNnData: dai.NNData):
    oakSelectOp.clear()
    oakSelectOp.appendChan('foo')
    oakSelectOp.numSamples = 1  # Output Format must be "Items as Separate Samples"
    oakSelectOp['foo'][0] = 42    
    return

```
### Queue Size[[edit](https://docs.derivative.ca/index.php?title=OAK_Select_CHOP&action=edit&section=2 "Edit section: Queue Size")]

The Queue Size parameter helps TouchDesigner avoid holding onto too many messages while also re-using memory for a minimum number of messages. For example, picking 2 is a good choice because TouchDesigner can show 1 message to the user while 1 remaining message can asynchronously be written to with new data. However, if the stream is meant to be high frame-rate, such as [IMU](https://docs.luxonis.com/projects/api/en/latest/components/messages/imu_data/) data, then the queue size should be at least double the number of messages you expect to receive in a single TouchDesigner frame. If TouchDesigner were to drop a video frame, then the next cook would want to use two times the number of messages that would have normally be shown, requiring the queue size to be at least twice as large.

### Max Items[[edit](https://docs.derivative.ca/index.php?title=OAK_Select_CHOP&action=edit&section=3 "Edit section: Max Items")]

Some messages can be described as items. For example, [ImgDetections](https://docs.luxonis.com/projects/api/en/latest/components/messages/img_detections/) can be grouped into item0's channels, item1's channels, item2's channels and so on. For these kinds of streams, it can be helpful to have a constant number of channels in the OAK Select CHOP, regardless of whether an item exists in the most recent message.

### Output Format[[edit](https://docs.derivative.ca/index.php?title=OAK_Select_CHOP&action=edit&section=4 "Edit section: Output Format")]

The default Output Format is "Items as Separate Channels". For example, when receiving [ImgDetections](https://docs.luxonis.com/projects/api/en/latest/components/messages/img_detections/) from MobileNet, each detection would require 6 channels ("confidence", "label", "xmin", "xmax", "ymin", "ymax"). The total number of channels would be 6 times the **Max Items** built-in parameter. In this situation, time-slicing is enabled, so the number of samples will vary according to time-slicing.

If you're willing to sacrifice time-slicing, you can set the output format to "Items as Separate Samples". This will shuffle the latest messages into 6 channels by **Max Items** samples. In other words, each ImgDetection item will correspond to a CHOP sample. Another reason to use "Items as Separate Samples" is if you're implementing a callback such as `onReceiveNNData` and need to set the number of samples (`oakSelectOp.numSamples = 1`).

### Use First Sample Only[[edit](https://docs.derivative.ca/index.php?title=OAK_Select_CHOP&action=edit&section=5 "Edit section: Use First Sample Only")]

Like the [Shuffle CHOP](Shuffle_CHOP.html "Shuffle CHOP"), the **Use First Sample Only** parameter makes it easy to only use the most recently received message with the OAK Select CHOP. For example, an IMU stream might be sending very high-frame rate data, and toggling this parameter on would be like using a [Trim CHOP](Trim_CHOP.html "Trim CHOP") in "Absolute" value mode to only show the latest sample.

### Info CHOP[[edit](https://docs.derivative.ca/index.php?title=OAK_Select_CHOP&action=edit&section=6 "Edit section: Info CHOP")]

When an OAK Select CHOP is connected to an [Info CHOP](Info_CHOP.html "Info CHOP"), in addition to the regular cook-related channels, there will be a few OAK-specific ones:

* sequence\_num: (see "sequenceNum" in the depthai [documentation](https://docs.luxonis.com/projects/api/en/latest/components/messages/img_detections/))
* messages\_received: the total number of messages received with stream name set on the OAK Select CHOP
* fps: The effective frames-per-second of this stream, i.e., how quickly TouchDesigner is receiving messages. This is not the target FPS of the stream.

### See Also[[edit](https://docs.derivative.ca/index.php?title=OAK_Select_CHOP&action=edit&section=7 "Edit section: See Also")]

* [OAK-D](OAK-D.html "OAK-D")
* [OAK Device CHOP](OAK_Device_CHOP.html "OAK Device CHOP")
* [OAK Select TOP](OAK_Select_TOP.html "OAK Select TOP")

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.


A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.


Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.


TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.


A set of commands located in a Text DAT that are triggered to run under certain conditions. There are two scripting languages in TouchDesigner: [Python](Python.html "Python") and the original [Tscript](Tscript.html "Tscript"). Scripts and single-line commands can also be run in the [Textport](Textport.html "Textport").


The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.







Retrieved from "<https://docs.derivative.ca/index.php?title=OAK_Select_CHOP&oldid=30325>"
[Category](Special_Categories.html "Special:Categories"):

* [CHOPs](Category_CHOPs.html "Category:CHOPs")