

Sync Out CHOP - TouchDesigner Documentation





# Sync Out CHOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
**NOTE**
**License:** Only available in [TouchDesigner Pro](TouchDesigner_Pro.html "TouchDesigner Pro").

The [Sync In CHOP](Sync_In_CHOP.html "Sync In CHOP") and Sync Out CHOP are used to keep timelines in two or more TouchDesigner processes within a single frame of each other. One process will contain a Sync Out CHOP while one or more other processes contain [Sync In CHOPs](Sync_In_CHOP.html "Sync In CHOP"). The processes with [Sync In CHOPs](Sync_In_CHOP.html "Sync In CHOP") should have their **Realtime flag checked off**, as their frame rates will be determined by the Sync Out CHOP. Also note, all monitors (including all clients and server) should be set to the **same rate**. Note that unplugging or re-adding monitors may sometime change previously configured settings.
The CHOPs synchronize by pausing their own timeline until all Sync In/Out CHOPs have cooked. The Sync Out CHOP will be ahead of the [Sync In CHOPs](Sync_In_CHOP.html "Sync In CHOP"). If any CHOPs fail to communicate, the others will timeout, causing all processes to run slowly.
Client machines may come online at any point, or be switched off as desired, as the Sync Out CHOP will adjust accordingly, either timing out, temporarily or permanently banning individual clients as specified.
In addition any extra CHOP channels sent through the Sync Out CHOP is received by the [Sync In CHOPs](Sync_In_CHOP.html "Sync In CHOP").
**NOTE for Windows OS - If experiencing connection issues make sure Windows Firewall is disabled.**
An [Info DAT](Info_DAT.html "Info DAT"), pointing to the Sync Out CHOP, provides a detailed list of all clients:
The columns are:
* `pid`: process id of the client
* `address`: ip and port number
* `machine_name`: client machine name
* `filename`: name of the `.toe` file the client resides in
* `op_path`: full operator path to the client
* `include`: when 1, the Sync Out CHOPs waits for a reply, when 0, it is ignored.
* `timeout_total`: The total number of times the Sync Out CHOP stalled waiting for this client
* `timeout_consecutive`: The running number of times the Sync Out CHOP stalled waiting for this client.
* `steady_total`: The total number of times the Sync Out CHOP received a reply in time.
* `steady_consecutive`: The running number of times the Sync Out CHOP received a reply in time:
* `reply`: The last reply from the client, all clients should have the same increasing value.
  
Similarly, an [Info CHOP](Info_CHOP.html "Info CHOP") will reveal further information: [Info CHOP Channels](#Info_CHOP_Channels)
## Example Files[[edit](https://docs.derivative.ca/index.php?title=Sync_CHOPs_Common&action=edit&section=T-1 "Edit section: Example Files")]
Here are two simple example files that use Sync In and Out CHOPs. You would run the SyncServer.toe only once, and run the SyncClient.toe for every machine you want to display on. Note that you may need to adjust the [Window COMP](Window_COMP.html "Window COMP") located at /perform to output to your desired monitor. Also note that [Hardware Frame Lock](Hardware_Frame_Lock.html "Hardware Frame Lock") is not enabled in these examples, so if you want to use that feature you'll need to turn that parameter on in the [Window COMP](Window_COMP.html "Window COMP") for SyncClient.toe as well.
[File:SyncServer.toe](https://docs.derivative.ca/File:SyncServer.toe "File:SyncServer.toe")  
[File:SyncClient.toe](https://docs.derivative.ca/File:SyncClient.toe "File:SyncClient.toe")
## Intermittent Connections[[edit](https://docs.derivative.ca/index.php?title=Sync_CHOPs_Common&action=edit&section=T-2 "Edit section: Intermittent Connections")]
Whenever a client replies, it is immediately assumed reliable, and waited upon, by the Sync Out CHOP each frame thereafter.
When a client times-out a number of times in a row, however, it is continuously ignored by the Sync Out CHOP, until it replies on time again.
This also applies to clients that have stopped communicating altogether.
The number of consecutive timeouts is controlled by the `Client Timeouts (consecutive)` parameter and is reflected by the `timeout_consecutive` [Info DAT](Info_DAT.html "Info DAT") column.
## Fixing Dropped frames on Client[[edit](https://docs.derivative.ca/index.php?title=Sync_CHOPs_Common&action=edit&section=T-3 "Edit section: Fixing Dropped frames on Client")]
If a particular client is dropping frames, inspect the Sync Out CHOP on the server side with an info DAT. Look at the column for timeout\_consecutive. As well take note of the info chop channel for the sync in CHOP called sync\_incompletes. If one or both of these attributes are increasing, try adjusting the TimeOut parameter on the sync CHOP. Increasing this value has been known to remedy this issue.
## Banning[[edit](https://docs.derivative.ca/index.php?title=Sync_CHOPs_Common&action=edit&section=T-4 "Edit section: Banning")]
If a client produces unreliable communication, sometimes steady, sometimes timing out, then it can be permanently ignored by enabling `Ban Clients` and setting the `Total Timeouts` accordingly. Once a client timeouts a certain number of times, its Info DAT `include` column reports `banned` and it will always be ignored, even if it starts responding in time again.
## Resetting[[edit](https://docs.derivative.ca/index.php?title=Sync_CHOPs_Common&action=edit&section=T-5 "Edit section: Resetting")]
Whenever the Sync Out CHOP first starts any and all clients are accepted, and nothing is banned. Pressing `Clear Stats` in the Sync Out CHOP also returns to this state, clearing all banned lists, and totals, even in the remote client [Info CHOPs](Info_CHOP.html "Info CHOP").
  
  
See also [Syncing Multiple Computers](Syncing_Multiple_Computers.html "Syncing Multiple Computers") and [Hardware Frame Lock](Hardware_Frame_Lock.html "Hardware Frame Lock").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[syncoutCHOP\_Class](SyncoutCHOP_Class.html "SyncoutCHOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Example Files](#Example_Files)
* [3 Intermittent Connections](#Intermittent_Connections)
* [4 Fixing Dropped frames on Client](#Fixing_Dropped_frames_on_Client)
* [5 Banning](#Banning)
* [6 Resetting](#Resetting)
* [7 Parameters - Sync Out Page](#Parameters_-_Sync_Out_Page)
* [8 Parameters - Common Page](#Parameters_-_Common_Page)
* [9 Operator Inputs](#Operator_Inputs)
* [10 Info CHOP Channels](#Info_CHOP_Channels)
  + [10.1 Specific Sync Out CHOP Info Channels](#Specific_Sync_Out_CHOP_Info_Channels)
  + [10.2 Common CHOP Info Channels](#Common_CHOP_Info_Channels)
  + [10.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Sync Out Page
Active `active` - Whether or not the CHOP is currently attempting to synchronize itself.
Multicast Address `multicastaddress` - An IP address to communicate on (224.0.0.1).
Network Port `port` - The network port associated with the address.
Local Address `localaddress` - Specify an IP address to send from, useful when the system has mulitple NICs (Network Interface Card) and you want to select which one to use.
Local Port Mode `localportmode` - ⊞ - Choose between automatically or manually selecting local port to use.
* Automatic `automatic` -
* Manual `manual` -
Local Port `localport` - When the above parameter is set to 'Manual', enter the port number to use here.
Timeout (msec) `timeout` - The maximum amount of time the CHOP will wait for synchronization signals from the other Sync CHOPs. This value is expressed in milliseconds.
Client Timeouts (Consecutive) `clienttimeouts` - The maximum number of consecutive timeouts a client must generate until it is ignored, causing no further timeouts. It will remain ignored until it replies on time again or this CHOP is reset.
Ban Clients `banclients` - Enables permanent banning of clients.
Total Timeouts `banclienttimeouts` - The maximum number of timeouts a client must generate until it is permanently ignored. Only a reset will allow it to be included again.
Clear Stats `clearstats` - Pressing this button will clear all banned lists, as well as totals reported in an [Info CHOP](Info_CHOP.html "Info CHOP").
  

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
Extra Information for the Sync Out CHOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific Sync Out CHOP Info Channels
* sync\_incompletes - This number is constant when the system is in sync, and will climb up each time the number of clients responding does not match the expected number. **When all is steady, the number does not change**.
* sync\_totaldelay - The total amount of time spent waiting for acknowledgement replies from the clients (milliseconds).
* sync\_lastdelay - The amount of time waiting for acknowledgement replies from the clients for the last message (milliseconds).
* sync\_internal - The number of clients within the same .toe file (process) that it is waiting on.
* sync\_external - The number of clients from different .toe files (other processes) that it is waiting on.
* sync\_serial - The last serial index sent to the clients. Increases each message sent.
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
  
TouchDesigner Build: Latest\nwikieditor2021.100002018.28070before 2018.28070
| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • Sync Out• [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.

A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.

samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.

TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.

Retrieved from "<https://docs.derivative.ca/index.php?title=Sync_Out_CHOP&oldid=32977>"
[Category](Special_Categories.html "Special:Categories"):
* [CHOPs](Category_CHOPs.html "Category:CHOPs")