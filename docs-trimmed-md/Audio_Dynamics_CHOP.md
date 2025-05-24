

TouchDesigner Documentation




# Audio Dynamics CHOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Audio Dynamics CHOP is designed to control the dynamic range of an audio signal. Dynamic range refers to how loud and quiet the audio is over some period of time. The Operator contains two types of dynamic control: compression and limiting.
It is recommended that you [link](Link.html "Link") this CHOP to an [Info CHOP](Info_CHOP.html "Info CHOP"), so that you can have some visual feedback: The amount of compression or limiting which is being applied will be displayed in the Info CHOP.
**Compressor**
The goal of a compressor is to reduce the amplitude of a signal when it crosses a certain threshold, while introducing little to no harmonic distortion. The desired threshold is set by the user, and the amount of compression to be applied is determined by the compression ratio. The attack and release parameters determine how quickly the compression will be applied and released, as incoming signal goes above and below the threshold.
**Limiter**
The purpose of a limiter is to ensure a signal is within a certain dynamic range, while introducing as little harmonic distortion as possible. Unlike the compressor, the goal is not to apply a smooth or musical form of dynamic control, but instead to keep the signal within a 'safe' range that is compatible with any CHOPS that are downstream (for example, an Audio Device Out). This means that the Limiter has a much more abrupt (instant) attack value, which cannot be adjusted by the user.
Input 2: **Side Chain Channels** - Other audio channels coming in can be used to determine the gains that are applied to the audio channels of the first input.
**NOTE**: This is a useful article for procedurally [mixing audio for games](http://gameaudionoise.blogspot.co.uk/p/all-in-mix-importance-of-real-time.html).
See [Audio Filter CHOP](Audio_Filter_CHOP.html "Audio Filter CHOP"), [Audio Para EQ CHOP](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP"), [Audio Band EQ CHOP](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP"), [Audio Spectrum CHOP](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP")
See also: [Envelope CHOP](Envelope_CHOP.html "Envelope CHOP").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[audiodynamicsCHOP\_Class](https://docs.derivative.ca/AudiodynamicsCHOP_Class "AudiodynamicsCHOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Pre Page](#Parameters_-_Pre_Page)
* [3 Parameters - Compressor Page](#Parameters_-_Compressor_Page)
* [4 Parameters - Limiter Page](#Parameters_-_Limiter_Page)
* [5 Parameters - Post Page](#Parameters_-_Post_Page)
* [6 Parameters - Common Page](#Parameters_-_Common_Page)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
* [8 Operator Inputs](#Operator_Inputs)
* [9 Info CHOP Channels](#Info_CHOP_Channels_2)
  + [9.1 Specific Audio Dynamics CHOP Info Channels](#Specific_Audio_Dynamics_CHOP_Info_Channels)
  + [9.2 Common CHOP Info Channels](#Common_CHOP_Info_Channels)
  + [9.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Pre Page
Input Gain (dB) `inputgain` - This parameter controls the volume of the channel before it reaches the compressor. If the signal to be compressed is not in a useful dynamic range, this parameter can be used to repair it.
  

## Parameters - Compressor Page
Enable Compressor `enablecompressor` - Turns the compressor on or off.
Compression Type `compressiontype` - ⊞ - Determines which compression method to use.
* Automatic Gain Control `compagc` - This type of compression is suitable for passages of audio which are varying in amplitude over an extended period of time. To apply this type of compression, set the threshold to a value which is near the maximum volume that you want to hear. Apply a large compression ratio (around 1.0), and set the attack and release to high values. As the passage of audio crosses the threshold value, compression will slowly be applied, and if set properly, the signal will be compressed to a constant range. Setting the attack and release too low will cause the output volume to waver too quickly, while high values may cause the compression to be applied too slowly.
* Musical Dynamics `compmus` - If a passage of vocals or a musical instrument is varying in amplitude and needs to be brought into a uniform dynamic range, try applying this type of compression. Unless a heavy compression sound is desired, it is best to use this effect lightly. Set the threshold into the volume range that you want to compress and apply a low compression ratio. Try different values of attack and release until you achieve a good dynamic balance.
Channel Linking `chanlinkingcomp` - ⊞ - As various channels come into the CHOP, they can either be compressed by an equal amount, or individually. If they are compressed equally, all of the channels will be evaluated for the highest peak value, and this value will be used to determine the compression amount.
If they are compressed separately, each channel will be evaluated and compressed by different amounts.
* Compress Equally `compequally` -
* Compress Individually `compindividually` -
Threshold (dB) `thresholdcompressor` - This parameter sets the threshold value which a signal must cross before compression is applied. It uses a decibel scale, where '0 decibels' would be considered the loudest possible signal\*, and '-60 decibels' would be nearly inaudible. This is assuming that input signals are normalized to a "-1 to +1" range.
Ratio `ratiocompressor` - The ratio is the amount of compression that will be applied to the signal, with respect to how far the signal has gone past the threshold value. A ratio of '0' will apply no compression. A value of '1' will cause a signals amplitude to be held down to the threshold value. With values over '1', the signal will become quieter as it passes the threshold.
Knee `kneecompressor` - The knee defines how the CHOP will transition into compression as signals approach or cross the threshold. With a knee of '0' (a hard knee), think of the compressor as applying a flat compression response, where:
compression\_gain(db) = amount\_that\_signal\_has\_crossed\_threshold(dB) \* compression\_ratio
This type of compression is not always desirable, as it can have a strong effect upon the dynamics of a sound. Increasing the knee parameter will cause there to be a smoothed transition into the compression.
See the Knee diagram below.
[![AudioKnee.png](https://docs.derivative.ca/images/thumb/4/43/AudioKnee.png/300px-AudioKnee.png)](https://docs.derivative.ca/File:AudioKnee.png)

Attack (msec=10\*\*val) `attackcompressor` - The attack will control how quickly the compressor responds when a signal crosses the threshold. Increasing the attack parameter will cause the compressor to apply compression at a slower and smoother rate. Increasing the parameter too much, will cause compression to be applied too slowly.
Release (msec=10\*\*val) `releasecompressor` - The release will control how quickly the compressor responds when a signal drops to a lower level, or goes below the threshold altogether. Just like the attack, higher value will slow down the response, but too high of a value will be too slow.
Output Gain (dB) `gaincompressor` - After applying compression, the signal can be reduced with Gain to a lower volume level. To make up the lost volume, this parameter can be increased.
  

## Parameters - Limiter Page
Enable Limiter `enablelimiter` - Turns the limiter on or off.
Channel Linking `chanlinkinglim` - ⊞ - Same as compressor.
* Limit Equally `compequally` -
* Limit Individually `compindividually` -
Threshold (dB) `thresholdlimiter` - This is the threshold value which a signal must cross before limiting is applied. Usually, this value should be left at '0' decibels. Just like the compressor, a value of '0' decibels is considered to be the loudest possible signal.
From the perspective of digital audio, a signal level which varies between "+1 <-> -1" is at a volume level of "0" decibels, because it is not possible for a digital system to respresent any values larger than "+1 <-> -1". Instead, they will simply be clipped as they proceed to the output device. The limiter allows you to stop your audio from being clipped if you exceed this range, and applies a much smoother form of fast compression, which is barely audible.
Lowering the threshold value will cause the output to be clamped to a lower level.

Release (msec=10\*\*val) `releaselimiter` - Although the attack of a limiter is always quick, the release can still be set by the user. This will determine how long the limiter takes to transition out of a limiting situation. Increasing the release will help smooth out the effect of the limiter. Too high of a value may cause the limiter to release too slowly. For example, after an excessively loud tone burst, the limiter's gain may have been pushed up to an extreme value. This extreme value will take a long time to be fully released.
Each channel can be different by putting expressions with the channel index, `me.channelIndex` in parameters like the frequency channel.

Knee `kneelimiter` - Similar to the compressor, this parameter controls how the CHOP will transition into limiting, when a signal becomes louder. A larger knee will mean a smoother transition. See the Knee diagram above.
If set to '0', no limiting will be applied until a signal goes over the threshold value. When increasing the knee parameter, some limiting will be applied before a signal goes beyond the threshold value, in an attempt to smooth out the effects of limiting overall.

  

## Parameters - Post Page
Dry / Wet Mix `drywet` - As this parameter is reduced from 1 (Wet) toward 0 (Dry), it removes the effect of the filter.
  

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
* `compressor_multiplier` - the amount that the compressor reduced the loudness. 1 means no-change. expressed not in dB – linear
* `limiter_multiplier` - the amount that the limiter reduced the loudness. not db – linear
* `compressor_db` - same as above but expressed in decibels
* `limiter_db`
* `compressor_attack_msec` - this is in milliseconds, computed from the parameter which is 1 msec at value 1 and 100,000 msec at value 5 (10\*\*val)
* `compressor_release_msec`
* `limiter_release_msec`
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
  

## Info CHOP Channels
Extra Information for the Audio Dynamics CHOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific Audio Dynamics CHOP Info Channels
* compressor\_multiplier -
* compressor\_db -
* compressor\_attack\_msec -
* compressor\_release\_msec -
* limiter\_multiplier -
* limiter\_db -
* limiter\_release\_msec -
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
  
TouchDesigner Build: Latest\n2022.241402021.100002018.28070before 2018.28070
| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • Audio Dynamics• [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.

A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.

samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.

TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.

Retrieved from "<https://docs.derivative.ca/index.php?title=Audio_Dynamics_CHOP&oldid=24421>"
[Category](Special_Categories.html "Special:Categories"):
* [CHOPs](Category_CHOPs.html "Category:CHOPs")