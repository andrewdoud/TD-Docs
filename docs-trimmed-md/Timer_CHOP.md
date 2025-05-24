

Timer CHOP - TouchDesigner Documentation





























# Timer CHOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Timer CHOP is an engine for running timed processes. It outputs channels such as timing fractions, counters, pulses and timer states, and it calls python functions (callbacks) when various timing events occur.

Examples using the Timer CHOP include triggering multiple timed cues, running playlists, timelines, state machines, and driving pre-animated animation components in 3D scenes. See Help -> Operator Snippets for numerous examples.

You set a timer to a number of seconds (or unlimited), frames or samples, and trigger it to start via the Start parameter or the second input CHOP. The Timer CHOP outputs in seconds, frames, samples, fraction and on-off states as it’s counting, including a `done` channel that goes on when it is complete. When it reaches certain states like end-of-cycles or when it’s done, various python callbacks are called allowing you to customize its behavior.

The Timer CHOP gets triggered by events (via pulsing its parameters or driving its two inputs). It takes events in, counts time, changes state. Via its python callback functions, you can send events out to other nodes, set parameters, get/set values in DATs, CHOPs and storage, restart itself, or trigger other nodes. As such, it can operate as a state machine.

It has play/pause, plus a speed control to slow down or speed up the timer.

It can also cycle indefinitely and then can be signaled to end immediately or at the end of the current cycle.

**Recommended**: the **OP Snippets for Timer CHOP**. See the channel descriptions in [Initialize Start](Initialize_Start.html "Initialize Start").

**Multiple Timer segments** - One Timer CHOP can also have multiple timers within it. By attaching a Table DAT you can define one timer (segment) per row. In Serial Timers mode it allows for one time segment followed by another. In Parallel Timers mode, the timers all run in parallel, each with its own begin time and length, and its own set of output channels.

[![Timer CHOP.2.png](https://docs.derivative.ca/images/8/82/Timer_CHOP.2.png)](https://docs.derivative.ca/File:Timer_CHOP.2.png)

The Timer CHOP can be Locked to Timeline in a deterministic way, or run more freely in Sequential Mode. When run independently from the timeline, you can jump ahead, break out of cycles, pause, `goTo()` exact position or timecode in the timer, and dynamically adjust the speed.

Attach an Info DAT to the Timer CHOP to see the timecodes, or use the `.timecode` members. Custom text strings can be placed in the Info DAT for each segment, and custom animated channels can be created.

To make an entire Timer CHOP loop after the last segment, set the On Done menu to Re-Start.

**Tip: What happens when you press Start** - The timers are at 0 when you initialize, for example timer\_frames = 0. On the frame when you press Start, by default, the running channel goes from 0 to 1, all the timer counter channels step forward by 1 frame. If you want the timers to hold at 0 until the next frame, set the Delay parameter to 1 frame. This is useful when you are cutting from black to a visible first-frame of a movie. If the length of the timer is 100 frames, it will make the running channel on for 100 frames, otherwise it will be 99 (though subsequent cycles are always 100).

**Chaining Timers** - The Timer CHOPs can be chained together, so that when one ends, the next can begin. They just need to all be Initialized together, where the `ready_pulse` channel of one Timer CHOP is exported to the Initialize parameter of the next Timer CHOP. Then they can be run in sequence, where the output of one Timer CHOP’s `done_pulse` channel is wired to the Start input (or exported to the Start parameter) of the next Timer CHOP. You start the chain of timers by starting the first Timer CHOP. By using some Timer CHOPs to loop awaiting input or response, or by adding logic to decide which CHOP to start next, state machines can be implemented.

### Callbacks

The callbacks are called at different moments during the timer progression.

`onInitialize()` gets called when you pulse the Initialize parameter. Here you can prepare any part of your setup prior to starting. At the end of Initialize the timer goes into a "ready" state.

`onStart()` gets called on the frame that the Start parameter is pulsed. The timer then goes into a "running" state.

`onTimerActive()` gets called every frame that the timer is running and there is no Delay or Play is off.

`onCycleStart()` gets called if the timer is set to cycle via the Cycle parameters.

Before a cycle or segment ends, an `onCycleEndAlert()` callback based on the Cycle End Alert parameter can be called to allow you to prepare for the next cycle, segment or Timer CHOP.

`onSegmentEnter()` and `onSegmentExit()` get called if the timer is being driven by a Segments DAT which acts like several timers in one. The argument `segment` in these callbacks is actually an object with useful members including any custom columns you have in your segment table: In `onSegmentEnter()`, put the code `print(help(segment))`

`onDone()` gets called when the timer reaches its finished state.

You can initialize at a specific time by using `.masterSeconds` in `onInitialize()`.

**See also**: [Trigger CHOP](Trigger_CHOP.html "Trigger CHOP"), [Event CHOP](Event_CHOP.html "Event CHOP"), [Speed CHOP](Speed_CHOP.html "Speed CHOP"), [Count CHOP](Count_CHOP.html "Count CHOP"), [Beat CHOP](Beat_CHOP.html "Beat CHOP"), [Event CHOP](Event_CHOP.html "Event CHOP"), [Clock CHOP](Clock_CHOP.html "Clock CHOP"), [Delay CHOP](Delay_CHOP.html "Delay CHOP"), [CHOP Execute DAT](CHOP_Execute_DAT.html "CHOP Execute DAT"), [LFO CHOP](LFO_CHOP.html "LFO CHOP").
time measurements

Time Measurements and what affects them

| Name | Speed | Play | Cycles | Go To and Cueing | Subrange | Delay Between Segments |
| --- | --- | --- | --- | --- | --- | --- |
| Cumulative Time Count | slows if speed<1 | pauses when off | keeps counting | jumps | jumps | pauses |
| Playing Time Count | unaffected | pauses when off | keeps counting | keeps counting | keeps counting | keeps counting |
| Running Time Count | unaffected | unaffected | keeps counting | keeps counting | keeps counting | keeps counting |
| Master Time Count | slows if speed<1 | pauses when off | see note \* | jumps | jumps | keeps counting |
| Segment + Fraction | 0 to 1 per-segment | pauses when off | see note \* | jumps | jumps | pauses |

**note: jumps back every cycle if Cycle Limit is off. keeps counting up if Cycle Limit is on.**

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[timerCHOP\_Class](TimerCHOP_Class.html "TimerCHOP Class")

## Contents

* [1 Summary](#Summary)
  + [1.1 Callbacks](#Callbacks)
* [2 Parameters - Timer Page](#Parameters_-_Timer_Page)
* [3 Parameters - Segments Page](#Parameters_-_Segments_Page)
* [4 Parameters - Sub Range Page](#Parameters_-_Sub_Range_Page)
* [5 Parameters - Outputs Page](#Parameters_-_Outputs_Page)
* [6 Parameters - External Page](#Parameters_-_External_Page)
* [7 Parameters - Common Page](#Parameters_-_Common_Page)
* [8 Operator Inputs](#Operator_Inputs)
* [9 Info CHOP Channels](#Info_CHOP_Channels)
  + [9.1 Specific Timer CHOP Info Channels](#Specific_Timer_CHOP_Info_Channels)
  + [9.2 Common CHOP Info Channels](#Common_CHOP_Info_Channels)
  + [9.3 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Timer Page

Active `active` - ⊞ - The Timer cooks: Never / Always / While Running (while in "running" state) / While Playing (while in "running" state and Play is on).

* Never `never` -

* Always `always` -

* While Running `running` -

* While Playing `playing` -

Time Control `timecontrol` - ⊞ - **Sequential** (timeline-independent) or **Locked to Timeline**. In Locked to Timeline, non-deterministic features are disabled. **External CHOP Channel** lets you drive the master time (`.masterSeconds` etc) using a CHOP channel defined by the parameters on the External page. **External Timecode** lets you drive the master time using a timecode CHOP/DAT/Object.

* Lock To Timeline `lock` - Output is determined by the current frame position.

* Sequential `sequential` - Output runs continuously, regardless of current frame position.

* External CHOP Channel `chop` - Output is determined by external CHOP channel value.

* External Timecode `timecode` - Output is determined by the value of an external timecode.

Defer Par Changes `deferpars` - When On, parameter changes like Length, Cycles and others are ignored until the next Intitalize. When Off, paraameter changes affect the timer immediately (possibly giving jumps in state).
Initialize `initialize` - (pulse parameter) Initialize is the signal to get the timer ready: sets the counters to zero (delay, timer, cycle, segment), set the output channels in the proper state, `done` to be off, the onInitialize() callback is run, and when initialize is complete, it indicates it’s ready by turning on the `ready` channel, awaiting a Start pulse.
Start `start` - (pulse) Start is the signal to commence the timers counting. It will count through the delay first, then the timer length. It does an Initialize if it is not already initialized, and then starts counting.
Length Type `lengthtype` - ⊞ - Describes how the length is defined.

* Fixed `fixed` - Lengths are finite, that is of a specific duration.

* Infinite `infinite` - The segments run continuously without end.

Length `length` - (float) the time-length of the timer. Set the Units menu to Seconds, Frames or Samples.
Length Units `lengthunits` - ⊞ - Choose between using Samples, Frames, or Seconds as the units for this parameter.

* I `samples` -

* F `frames` -

* S `seconds` -

Delay `delay` - (float) after Start, the delay before the timer begins counting.
Delay Units `delayunits` - ⊞ - Choose between using Samples, Frames, or Seconds as the units for this parameter.

* I `samples` -

* F `frames` -

* S `seconds` -

Play `play` - (onoff) Pauses the timer. It is basically a 0 or 1 multiplier on the Speed.
Speed `speed` - (default 1) Slows down or speeds up the timer.
Cue `cue` - Freezes playing at the Cue Point.
Cue Pulse `cuepulse` - Jump instantly to the Cue Point.
Cue Point `cuepoint` - Time (Seconds, Frames or Fraction) which the cue point is frozen to.
Cue Units `cueunits` - ⊞ - Choose between using Samples, Frames, Seconds, Fraction(0-1) as the units for this parameter.

* I `samples` -

* F `frames` -

* S `seconds` -

* % `fraction` -

Cycle `cycle` - (default Off) causes the timer to loop back to 0 when it reaches the end of the cycle.
Cycle Limit `cyclelimit` - When the Cycle parameter is On, this determines if it will cycle indefinitely or cycle some maximum number of cycles.
Maximum Cycles `maxcycles` - When Cycle is on and Cycle Limit is on, this sets the maximum number of cycles.
Cycle End Alert `cycleendalert` - The number of seconds, frames or samples before a cycle, segment or done state is reached that the `onCycleEndAlert()` callback is called. This allows you to prepare for the next cycle, segment or timer.
Notify Units `notifyunits` - ⊞ - Choose between using Samples, Frames, or Seconds as the units for this parameter.

* I `samples` -

* F `frames` -

* S `seconds` -

Exit Segment at End of Cycle `exitendcycle` - When pulsed, it will exit the cycle (and segment) at the end of the currently-playing cycle.
Go to End of Cycle `gotoendcycle` - When pulsed, it will exit the cycle (and segment) immediately.
Go to Done `gotodone` - Will immediately go to the Done state.
On Done `ondone` - ⊞ - Determines which action to take when the timer gets to the end, ie "is done" or finished. Note there is also a onDone callback that can be used for customizing behavior.

* Do Nothing `donothing` - No action taken.

* Re-Initialize `reinit` - Will re-initialize the timer, this is the same as pulsing the Initialize parameter above.

* Re-Start `restart` - Will re-initialize and re-start the timer, this is the same as pulsing the Start parameter above.

* Re-Start without Initializing `restartnoinit` - Will re-star the timeer without re-initializing.

Callbacks DAT `callbacks` - The path to the DAT containing callbacks for this Timer CHOP.

  


## Parameters - Segments Page

You can specify multiple timers in one Timer CHOP. A "segment" acts as one timer, with its own length, delay time, number of cycles to repeat and other conditions.

Segments DAT `segdat` - A table DAT that contains one row per timer (segment). The column headings can be `delay` or `begin`, `length`, `cycle`, `cyclelimit`, `maxcycles` and `cycleendalert`, which override the equivalent parameters. (These are the internal names for the corresponding parameters.) `begin` is unique as it replaces `delay`, and it represents the time from Start that the timer will begin counting, whether the CHOP is set to Serial Timers or Parallel Timers (see Segment Method).

The Segments DAT also can include any number of custom columns. See Columns to Custom Channels and Columns to Info DAT below.



Segment Method `segmethod` - ⊞ - If the Segment Method is **Serial Timers**, the timers will be played back-to-back. If the Segment Method is **Parallel Timers**, the timers can be played at the same time, and a set of channels will be output for each timer.

* Serial Timers `serial` -

* Parallel Timers `parallel` -

Segment Units `segunits` - ⊞ - For the columns `delay`, `begin`, `length` and `cycleendalert`, you specify whether it’s seconds, frames or samples with this menu.

* Samples `samples` -

* Frames `frames` -

* Seconds `seconds` -

Segments End Time `segsendtime` - ⊞ - Describes how the end time is calculated.

* From Segments DAT `dat` - The end time is based on the Segments DAT values.

* From Length Parameter `par` - The end time is based on the Length parameter value.

* Max of Parameter/Table `max` - The end time is based on the greater of the Length parameter value and the Segments DAT values.

Columns to Custom Channels `channelcolumns` - Optional extra columns (any name) in the segments DAT can be output as extra channels (the columns must contain numbers). Specify their names in the Columns to Channels parameter. The channel name will be the column name. You can also output the `length`, `delay`, etc columns as channels.
Custom Channel Interpolation `interpolation` - ⊞ - By default, custom channels step to their new value at the begin of the segment. This menu lets you interpolate to the new value linearly, or any combination of ease-in and ease-out.

* Step to Value `steptovalue` -

* Linear to Value `lineartovalue` -

* Ease In to Value `easeintovalue` -

* Ease Out to Value `easeouttovalue` -

* Ease In-Out to Value `easeinouttovalue` -

Columns to Info DAT `infocolumns` - Optional extra columns (any name) in the segments DAT can be output to the Info DAT (attach an Info DAT to the Timer CHOP) if you specify their names in this parameter.
Go to Previous Segment `gotoprevseg` - (pulse) Jump to Previous Segment.
Go to Next Segment `gotonextseg` - (pulse) Jump to Next Segment.

*Lingo*

* Segment – each segment acts as one timer, with delay time, length, number of cycles to repeat and other conditions.
* Begin – in Parallel Timers, the number of seconds after a Start (frames or samples) after which each timer starts counting up from zero.
* Done – The state it goes into when all the timers has finished counting, whether they are in Parallel or Serial, Segments or not.
* End – Cycle End is the end of each cycle, Segment End is the end of the segment.
* Cumulative Time – Zero at Start, a count that is affected by speed and rises while timers are active (not during delays).
* Running Time – Zero at Start, the wall-clock time since Start was called no matter what are the delays, speeds, cycles or premature clicking of Go To Segment End. It stops counting when Done has been reached.

  


## Parameters - Sub Range Page

Operate the timer within a sub range of the total length.

Sub Range `subrange` - Turn this parameter on to limit the timer output to a subrange of the full length.
Sub Start `substart` - The beginning point of the sub range.
Sub Start Units `substartunits` - ⊞ - Choose between using Samples, Frames, or Seconds as the units for this parameter.

* I `samples` -

* F `frames` -

* S `seconds` -

Sub End `subend` - The end point of the sub range.
Sub End Units `subendunits` - ⊞ - Choose between using Samples, Frames, or Seconds as the units for this parameter.

* I `samples` -

* F `frames` -

* S `seconds` -

Sub End Action `subendaction` - ⊞ - Controls the behavior once the sub range end point is reached: Loop at End, or Pause at End.

* Pause at End `pause` -

* Loop at End `loop` -

  


## Parameters - Outputs Page

Timer Fraction `outfraction` - Outputs channel `timer_fraction` for each segment.
Timer Count `outtimercount` - ⊞ - Outputs the elapsed Seconds channel as `timer_seconds`, Frames outputs channel as `timer_frames`, or Samples outputs channel as `timer_samples`. Because this is elapsed time, `timer_frames` starts at 0, as do the others.

* Off `off` -

* Samples `samples` -

* Frames `frames` -

* Seconds `seconds` -

* All `all` -

Timer Active `outtimeractive` - Outputs channel `timer_active` which is on only while the timer fraction is counting (is non-zero).
Timer Pulse `outtimerpulse` - Outputs channel `timer_pulse` when the timer reaches its length.
Delay Fraction `outdelayfraction` - Outputs a 0-1 fraction in `delay_fraction` while the delay occurs.
Delay Count `outdelaycount` - ⊞ - Outputs the delay count in seconds, frames or samples.

* Off `off` -

* Samples `samples` -

* Frames `frames` -

* Seconds `seconds` -

* All `all` -

Initializing `outinit` - Outputs channel `initializing` = 1 while the timer is initalizing (i.e. while the callback `onInitialize()` returns non-zero).
Ready `outready` - Outputs channel `ready` which is 1 after an Initialize and before a Start.
Ready Pulse `outreadypulse` - Outputs a pulse when initialization has finished and the timer is ready to start. It pulses even when the timer starts rights away after an initialization.
Running `outrunning` - Outputs channel `running` which is 1 after a Start and before the Done.
Done `outdone` - Outputs channel `done` when done or complete.
Done Pulse `outdonepulse` - Outputs channel `done` when the all timers have reached their completion.
Cycles `outcycle` - Outputs channel `cycles`, which is the number of cycles completed (In a segment), starting with 0 during the entire first cycle. If you jump to Done, cycle is incremented as if it played normally to the done state.
Cycle Pulse `outcyclepulse` - Outputs a pulse at the end of every cycle, even on the first and only cycle.
Cycles + Fraction `outcycleplusfraction` - Outputs channel `cycle_plus_fraction`, starting with 0 for entire first cycle.
Segment `outseg` - Outputs channel `segment`, starting with 0 for first segment.
Segment Pulse `outsegpulse` - Outputs channel `segment_pulse` which is a pulse at the end of each segment.
Segment + Fraction `outsegplusfraction` - Outputs channel `segment_plus_fraction`, starting with 0 for first segment ending at #segments at end.
Length `outlength` - ⊞ - Outputs channel `length`, starting with 0 for first segment ending at #segments at end.

* Off `off` -

* Seconds `seconds` -

* Frames `frames` -

* Samples `samples` -

* All `all` -

Cumulative Timer Count `outcumulativecount` - ⊞ - Outputs `cumulative_seconds`, `cumulative_frames` or `cumulative_samples`. It is a time count that adds up all the Timer Active times for all segments since Start: it is affected by "Speed", and counts up only while `timer_active` (Play) is on. See the python member `.cumulativeSeconds`.

* Off `off` -

* Samples `samples` -

* Frames `frames` -

* Seconds `seconds` -

* All `all` -

Playing Timer Count `outplayingcount` - ⊞ - Outputs `playing_seconds`, `playing_frames` or `playing_samples`. It is a time count that adds up all the Timer Active times for all segments since Start: it is not affected by "Speed", and counts up only while `timer_active` and `play` is on. See the python member `.playingSeconds`.

* Off `off` -

* Seconds `seconds` -

* Frames `frames` -

* Samples `samples` -

* All `all` -

Running Time Count `outrunningcount` - ⊞ - Outputs the "wall-clock" time since Start occurred, no matter what are the delays, speeds, cycles or pre-mature clicking of Go To Segment End, etc. It stops counting when Done has been reached. `running_seconds`, `running_frames`, or `running_samples`. When CHOP is set to Parallel Timers, this will output a channel per segment plus one global running time channel. See the python member `.runningSeconds`.

* Off `off` -

* Samples `samples` -

* Frames `frames` -

* Seconds `seconds` -

* All `all` -

Master Time Count `outmastercount` - ⊞ - Outputs `master_seconds`, `master_frames` or `master_samples`. It is a time count that adds up all the Timer Active times for all segments since Start: it is affected by "Speed", and counts up only while `timer_active` and `play` is on. It also includes any delay times. See the python member `.masterSeconds`.

* Off `off` -

* Seconds `seconds` -

* Frames `frames` -

* Samples `samples` -

* All `all` -

  


## Parameters - External Page

External CHOP `extchop` - The CHOP used to control the current point in the timer.
External Units `extunits` - ⊞ - Choose between using Samples, Frames, or Seconds as the units for this parameter.

* I `samples` -

* F `frames` -

* S `seconds` -

* % `fraction` -

External Channel `extchannel` - The channel that will control the current point of the timer.
External Timecode Object `exttcobj` - Time is specified using a timecode. Should be a reference to either a CHOP with channels 'hour', 'second', 'minute', 'frame', a DAT with a timecode string in its first cell, or a [Timecode Class](Timecode_Class.html "Timecode Class") object.
External Start Offset `extstartoff` - Specifies the external time at which the timer should start.
External Initialize Offset `extinitoff` - Specifies the external time at which the timer should initialize.
Sample Rate `rate` - The sample rate that the CHOP outputs at, which is also used when the units of Length, Delay and Cycle End Alert time are set to Samples. The default sample rate is 60 samples per second.

  


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

* Input 0:  -
* Input 1:  -

  


## Info CHOP Channels

Extra Information for the Timer CHOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Specific Timer CHOP Info Channels

* frames\_timer -

* frames\_segment -

* frames\_cumulative -

* frames\_running -

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

  

TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2023.112802022.241402021.100002018.28070before 2018.28070

| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Experimental:Parameter](Experimental_Parameter_CHOP.html "Experimental:Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [Experimental:POP to](Experimental_POP_to_CHOP.html "Experimental:POP to CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [Experimental:Resample](Experimental_Resample_CHOP.html "Experimental:Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Experimental:Script](Experimental_Script_CHOP.html "Experimental:Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • Timer• [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Experimental:Touch In](Experimental_Touch_In_CHOP.html "Experimental:Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


[OP Snippets](OP_Snippets.html "OP Snippets") is a set of 700+ live examples of TouchDesigner operators. You can access snippets via the Help menu, or by right-clicking on network operators, or r-clicking on OP Create dialog items.


A form of [DATs](DAT.html "DAT") (Data Operators) that is structured as rows and columns of text strings.


The panel at the bottom of TouchDesigner, it controls the current global looping [Time](Time_COMP.html "Time COMP") your TouchDesigner project, or of just one component.


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").


The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.


Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.


samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.


A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.


A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.


Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.







Retrieved from "<https://docs.derivative.ca/index.php?title=Timer_CHOP&oldid=33437>"
[Category](Special_Categories.html "Special:Categories"):

* [CHOPs](Category_CHOPs.html "Category:CHOPs")