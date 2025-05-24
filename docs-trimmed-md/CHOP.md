

CHOP - Derivative

























# CHOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

[![OP CHOP.png](images/e/e9/OP_CHOP.png)](File_OP_CHOP.html)

**CHOPs**, or **CHannel OPerators**, are a powerful technology which enables the processing of motion, audio, math, logic, MIDI data, numeric info and data streamed from/to devices and protocols.

CHOPs are an [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))).

CHOPs provide a unique way of creating and editing motion and audio. The combination of procedural editing of motion, keyframe animation, motion capture and live controls provides you with a wide range of animation techniques. In keeping with the TouchDesigner procedural paradigm, channel operators combine and refine the data without destroying the original data. CHOPs were designed to reduce the tedium of motion editing and to help build and manage more complex motion. CHOPs enable creators to think about motion at a more creative level and to experiment with motion more than any other animation technology.

A CHOP contains one or more named **channels**. The channels of a CHOP is made of a sequence of one or more "**samples**". A sample is one floating point number per channel.

A CHOP has a **sample rate**, which is the number samples-per-second, which matters only when a CHOP represents animation or audio over time.

The length of a CHOP is expressed in samples, and when the CHOP represents animation or audio, the length can also be expressed in seconds or frames. A frame is a unit of time of the timeline, typically 1/60 of a second.

A CHOP creates or modifies the [Channel](Channel.html "Channel"), and then passes the channels on to the next CHOP in a network. CHOPs are then connected to object motion or any other animated part of TouchDesigner via "[exporting](Export.html "Export")" and "channel references".

See also [Category:CHOPs](Category_CHOPs.html "Category:CHOPs") for a full list of articles related to CHOPs, especially [Anatomy of a CHOP](Anatomy_of_a_CHOP.html "Anatomy of a CHOP") and [Time Slicing](Time_Slicing.html "Time Slicing").

## Contents

* [1 Sweet 16 CHOPs](#Sweet_16_CHOPs)
* [2 CHOPs Create and Process Channels](#CHOPs_Create_and_Process_Channels)
* [3 Parts of a CHOP](#Parts_of_a_CHOP)
* [4 Inputs and Outputs](#Inputs_and_Outputs)
* [5 Referencing and Exporting CHOP Channels](#Referencing_and_Exporting_CHOP_Channels)
* [6 Difference Between a Sample and a Frame](#Difference_Between_a_Sample_and_a_Frame)
* [7 Sample Index and Value](#Sample_Index_and_Value)
* [8 Using .chanIndex in CHOP Parameters](#Using_.chanIndex_in_CHOP_Parameters)
* [9 Common CHOP Members](#Common_CHOP_Members)
* [10 See Also](#See_Also)
## Sweet 16 CHOPs[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=1 "Edit section: Sweet 16 CHOPs")]

[![Sweet 16 CHOPs.jpg](images/thumb/4/4f/Sweet_16_CHOPs.jpg/200px-Sweet_16_CHOPs.jpg)](Sweet_16_CHOPs_Vid.html "Sweet 16 CHOPs Vid")

Click the [video](Sweet_16_CHOPs_Vid.html "Sweet 16 CHOPs Vid") above to watch an overview of all Sweet 16 CHOPs. Watch individual CHOP videos by clicking on the appropriate CHOP's video icon below. The following 16 CHOPs are commonly used, we recommend familiarizing yourself with them.

| CHOP | Purpose | Related CHOP |
| --- | --- | --- |
| [Constant](Constant_CHOP.html "Constant CHOP") | Create new channels. | [Pattern](Pattern_CHOP.html "Pattern CHOP") |
| [LFO](LFO_CHOP.html "LFO CHOP") | Low Frequency Oscillator. | [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") |
| [Noise](Noise_CHOP.html "Noise CHOP") | Create semi-random patterns. |  |
| [Select](Select_CHOP.html "Select CHOP") | Grab a channel from any other CHOP. | [Switch](Switch_CHOP.html "Switch CHOP"), [Cross](Cross_CHOP.html "Cross CHOP") |
| [Merge](Merge_CHOP.html "Merge CHOP") | Merge channels from two or more CHOPs. | [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") |
| [Math](Math_CHOP.html "Math CHOP") | Add, multiply or scale channels. | [Logic](Logic_CHOP.html "Logic CHOP"), [Script](Script_CHOP.html "Script CHOP") |
| [Lag](Lag_CHOP.html "Lag CHOP") | Smooth and delay a channel. | [Filter](Filter_CHOP.html "Filter CHOP") |
| [Speed](Speed_CHOP.html "Speed CHOP") | Use speed to calculate distance. | [Count](Count_CHOP.html "Count CHOP"), [Slope](Slope_CHOP.html "Slope CHOP") |
| [Lookup](Lookup_CHOP.html "Lookup CHOP") | Use one channel to get values from another CHOP. | [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") |
| [Trail](Trail_CHOP.html "Trail CHOP") | Watch a time-history of CHOP channels. | [Perform](Perform_CHOP.html "Perform CHOP") |
| [SOP to](SOP_to_CHOP.html "SOP to CHOP") | Record a time-history of channels. | [DAT to](DAT_to_CHOP.html "DAT to CHOP"), [TOP to](TOP_to_CHOP.html "TOP to CHOP") |
| [Limit](Limit_CHOP.html "Limit CHOP") | Restrict channels to a range or certain step values. | [Analyze](Analyze_CHOP.html "Analyze CHOP") |
| [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") | Get audio from input device. | [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") |
| [OSC In](OSC_In_CHOP.html "OSC In CHOP") | Open Sound Control, MIDI. | [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") |
| [Panel](Panel_CHOP.html "Panel CHOP") | Get state, u, v etc values from any panel gadget. | [Info](Info_CHOP.html "Info CHOP") |
| [Timer](Timer_CHOP.html "Timer CHOP") | Run timers, loops, delays and trigger events. | [Beat](Beat_CHOP.html "Beat CHOP") |

All CHOPs are documented in the [Category:CHOPs](Category_CHOPs.html "Category:CHOPs").

## CHOPs Create and Process Channels[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=2 "Edit section: CHOPs Create and Process Channels")]

CHOPs are procedural networks, where "procedural" means the operators are wired together so the output of one CHOP flows into the input of one or more other CHOPs, and the data flows automatically every time the display is updated (by default, 60 times per second).

Some CHOPs, generator CHOPs, create CHOP channels from scratch. Some examples are the Constant CHOP, the Wave CHOP, and the Timing CHOP. CHOPs can also take data from

* on-screen sliders, buttons, menus, XY-controllers, XYZ values from clicking in 3D viewers.
* hardware devices including data via MIDI and OSC protocols.
* other processes/applications feeding TouchDesigner through pipes.

CHOPs process channel data and connect the results to any other part of TouchDesigner.

  


## Parts of a CHOP[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=3 "Edit section: Parts of a CHOP")]

[![CHOP.1.png](images/thumb/e/e5/CHOP.1.png/800px-CHOP.1.png)](File_CHOP.1.html)

A CHOP contains a set of **Channels**, plus control **[Parameters](https://docs.derivative.ca/index.php?title=Parameters&action=edit&redlink=1 "Parameters (page does not exist)")**, a **sample rate**, some on/off **[Flags](https://docs.derivative.ca/index.php?title=Flags&action=edit&redlink=1 "Flags (page does not exist)")**, and a **start/end interval**.

The channels of a CHOP can represent motion, MIDI, audio, color maps, rolloff curves or lookup tables. Any data that can be represented as a sequence of numbers can be represent in CHOP channels. The sequence of numbers are called **samples**.

Like all [Operators](Operator.html "Operator"), CHOPs have **[Parameters](https://docs.derivative.ca/index.php?title=Parameters&action=edit&redlink=1 "Parameters (page does not exist)")** used to define the data, plus the data channels, which are input/output from the CHOP as its data stream. The parameters are usually constant-valued, but can be time-dependent expressions.

CHOPs' parameters can be expressed in different CHOP **units**: samples (indexes), frames or seconds. These units are selected by the user in a menu to the right of such parameters. Each sample index, starting from 0, corresponds to some frame number (based on frames per second), and a moment in time (seconds).

[![CHOP Units menu](images/3/3d/CHOPUnits.jpg)](File_CHOPUnits.html "CHOP Units menu")

The **sample rate** (samples per second) is used if the CHOP contains time-dependent motion or audio data. Audio has a high sample rate when compared to animated motion.

Each CHOP has **flags**:

* The Display flag marks the CHOP to be displayed in a [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer").
* The Export flag causes the CHOP channel [exports](Export.html "Export") to toggle on and off.
* The Lock flag causes the CHOP to be locked and then can be hand-edited.
* The [Bypass Flag](Bypass_Flag.html "Bypass Flag") is a convenient way for a CHOP's effect to be disabled.

CHOPs can have any start/end indexes but all channels in a single CHOP share the same **start-end interval**. The interval goes from a start index to an end index and is not restricted to the length of any animation or timeline.

Each CHOP also has a **comment field** to add a note to a CHOP to explain what it is doing in the network. An **info pop-up** can be opened by middle-clicking on the CHOP, this lists channel names and values, sample rate and intervals.

In CHOPs, **Extend Conditions** determine what numbers you get when you try to get a channel value that is outside its start-end range - in its **Extend Regions**, before the CHOP's start time or after its end time. The CHOP may hold its last value, it may cycle, repeat, or be held at a default value. You can see a CHOP's extend conditions in the info pop-up (middle-mouse click on the CHOP), or by looking at a CHOP in the channel viewer outside its start-end range. You will see that a [Pattern CHOP](Pattern_CHOP.html "Pattern CHOP") cycles and a [Keyframe CHOP](Keyframe_CHOP.html "Keyframe CHOP") holds in the Extend Regions.

You can change the Extend Conditions with an [Extend CHOP](Extend_CHOP.html "Extend CHOP") or via menus on the Channel page in many CHOPs.

See also [Anatomy of a CHOP](Anatomy_of_a_CHOP.html "Anatomy of a CHOP").

## Inputs and Outputs[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=4 "Edit section: Inputs and Outputs")]

Each CHOP receives channels at its inputs. When the CHOP [cooks](Cook.html "Cook"), the channels of the inputs are combined. The CHOP outputs the resulting channels to other CHOPs.

CHOPs output their data channels as arrays of numbers, not keyframed, interpolated segments. Some CHOPs ([Keyframe CHOP](Keyframe_CHOP.html "Keyframe CHOP")) retain interpolated segments internally, but all CHOPs always output their data as raw samples. If the CHOP's inputs are not changing and the control parameters are not time-dependent, the CHOP will be non-time-dependent and it will not cook every time the animation frame on the timeline advances.

Some CHOPs output or use CHOP **attributes**, such as channels grouped as quaternion rotation channels.

  


## Referencing and Exporting CHOP Channels[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=5 "Edit section: Referencing and Exporting CHOP Channels")]

*Main article: [Export](Export.html "Export")*

Parameters of any node are able to get values from CHOP channels with expressions like the following:

```
op('filter1')[0]
op('filter1')['chan2']
op('pattern1')['chan1'][99]    # gets the 100th sample of chan1

```

However, exporting is preferred where possible. It is faster and involves less typing.

CHOP data channels are exported to Components, SOPs, etc. to drive their parameters. CHOPs can be exported to any TouchDesigner operator's parameter. Each CHOP has an Export flag (and an Export Prefix, infrequently used), causing the CHOP to connect its channels to Components, SOPs, TOPs and so on. The Export flag and Export Prefix can also use automatic matching of channels names to find export destinations. For example, a CHOP "tx" channel could map to an Geometry Component's tx parameter. When a CHOP exports to an object, SOP or TOP, the parameters exported to are said to be overridden.

  


## Difference Between a Sample and a Frame[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=6 "Edit section: Difference Between a Sample and a Frame")]

A frame always refers to the timeline, which is expressed in frames or seconds, and frames & seconds are tied via a certain number of "frames per second" or FPS. The default FPS for TouchDesigner is 60, and with FPS of 60, there will always be 60 frames per second. A CHOP range can start at any frame number (or second), and end at any later frame number. A frame will always correspond to a certain time expressed in seconds. Precisely, seconds is `(frame-1)/FPS`.

The sample index may have no relation to time or frame, as when a CHOP is used as lookup table. But when "index" is tied to time, the CHOP's samples per second (sample rate), determines how many samples per second there are, and even how many samples per frame. Some CHOPs default to 60 samples per second, which is 1 sample per frame. But CHOPs can be created or resampled to any sample rate, so a CHOP's sample rate of 240 samples per second gives 4 samples per frame, and audio at 24,000 samples per second is 400 samples per frame.

Even if a CHOP is shifted in time to start at a frame number like 301 (10 seconds), its sample index always starts at 0. Its `op('wave1').sampleIndex` is 0 at its first sample.

**NOTE**: Set the "frames per second" of the timeline for the project via the bottom of the timeline, or in Python `project.cookRate = 120`, for example. It is better to DO IT AT THE START OF A PROJECT, lest you get tripped up. Note each component can have its own timeline and its own sample rate. See [Timeline](Timeline.html "Timeline").

## Sample Index and Value[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=7 "Edit section: Sample Index and Value")]

[![ChannelsInfo2.gif](images/2/2b/ChannelsInfo2.gif)](File_ChannelsInfo2.html)

* The horizontal axis is called the i-axis or the sample index-axis.
* The vertical axis is called the v-axis or the value-axis.
* A sample index is a point along the i-axis, denoted by i.
* A value is a point along the v-axis, denoted by v.
* A sample is an index-value pair (i,v). i.e. the value of a channel at a certain sample index.
* A sample is made of a sample index and a sample value.
* An interval is an index range, which goes from a start index to an end index.
* A value range goes from a start value to an end value.
* The index duration is the end index minus the start index + 1.
* CHOP data channels are arrays of raw samples, in 32-bit floating point format, all computations are done at 64 bits, and parameters are stored as 64 bits.
* Channels in a CHOP may be control (parameter) channels or data channels. CHOPs manipulate the data channels.
* CHOPs can be evaluated at integer and non-integer indexes.
* Frame is used when the index corresponds to time.
* When speaking of animation frames, you can refer to start frame, end frame and frame range.

## Using `.chanIndex` in CHOP Parameters[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=8 "Edit section: Using .chanIndex in CHOP Parameters")]

A "Channel Index" is the channel number of a CHOP, 0 being the first channel, and is available for use in parameters in some CHOPs as `me.chanIndex`. Numerous CHOPs like the [Pattern CHOP](Pattern_CHOP.html "Pattern CHOP"), [Math CHOP](Math_CHOP.html "Math CHOP") and [Delay CHOP](Delay_CHOP.html "Delay CHOP") have extra local members that allow the customization of each channel: The Python object for the operator has a `.chanIndex` member. For example, if the Pattern CHOP generates three channels you can put something like `[3, 4, 5][me.chanIndex]` in the Amplitude parameter to customize its value for each channel. The first channel will be evaluated with an Amplitude value 3, the second channel with a value of 5, etc. Search `me.chanIndex` in the wiki. See also the Scope parameter on most CHOPs to affect selective channels.

## Common CHOP Members[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=9 "Edit section: Common CHOP Members")]

There are Python members of a CHOP that are common to many or all CHOPs. See [CHOP Class](CHOP_Class.html "CHOP Class") and [Channel Class](Channel_Class.html "Channel Class").

  


## See Also[[edit](https://docs.derivative.ca/index.php?title=CHOP&action=edit&section=10 "Edit section: See Also")]

| Introduction to CHOPs | [Uses of CHOPs](Uses_of_CHOPs.html "Uses of CHOPs") | [Exporting from CHOPs to Parameters](Export.html "Export") |
| --- | --- | --- |
| [Common page of all CHOPs](CHOP_Common_Page.html "CHOP Common Page") | [Channel page of CHOPs](CHOP_Channel_Page.html "CHOP Channel Page") | [Other Frequent Parameters](Edit_Keyframes.html "Edit Keyframes") |
| [The Idea of Time Slicing](Time_Slicing.html "Time Slicing") | [Exporting Channels](Export.html "Export") | [CHOP Operator Variables](Variables.html "Variables") |
| [CHOP File Formats](File_Types.html "File Types") | [Tscript Expressions](Expression.html "Expression") | [Category:MIDI](https://docs.derivative.ca/index.php?title=Category:MIDI&action=edit&redlink=1 "Category:MIDI (page does not exist)") and [OSC](OSC.html "OSC") |
| [Manually Editing Key Frames](Edit_Keyframes.html "Edit Keyframes") | [CHOP Techniques](CHOP_Techniques.html "CHOP Techniques") | [Working with Audio](https://docs.derivative.ca/index.php?title=Category:Audio&action=edit&redlink=1 "Category:Audio (page does not exist)") |

  


| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [Experimental:POP to](Experimental_POP_to_CHOP.html "Experimental:POP to CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [Experimental:Resample](Experimental_Resample_CHOP.html "Experimental:Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Experimental:Script](Experimental_Script_CHOP.html "Experimental:Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Experimental:Touch In](Experimental_Touch_In_CHOP.html "Experimental:Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").


In CHOPs, Extend Conditions determine what numbers you get when you try to get a channel value that is outside its start-end range - in its Extend Regions.


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).


The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.


A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.







Retrieved from "<https://docs.derivative.ca/index.php?title=CHOP&oldid=26376>"
[Categories](Special_Categories.html "Special:Categories"):

* [Touch Glossary](Category_Touch_Glossary.html "Category:Touch Glossary")
* [CHOP Topics](Category_CHOP_Topics.html "Category:CHOP Topics")
* [TDPages](Category_TDPages.html "Category:TDPages")