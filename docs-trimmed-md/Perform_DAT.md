

Perform DAT - TouchDesigner Documentation




# Perform DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Perform DAT logs various performance times in a [Table DAT](Table_DAT.html "Table DAT") format. These benchmarks are similar to those reported by the [Performance Monitor](https://docs.derivative.ca/Performance_Monitor_Dialog "Performance Monitor Dialog").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[performDAT\_Class](https://docs.derivative.ca/PerformDAT_Class "PerformDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Perform Page](#Parameters_-_Perform_Page)
* [3 Parameters - Common Page](#Parameters_-_Common_Page)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [4.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Perform Page
Active `active` - Turns logging on/off. The DAT will continuously log while Active is On.
Active Pulse `activepulse` - Use resetpulse button to grab a single frame snapshot.
Trigger Mode `triggermode` - ⊞ - Offers two options for when to trigger a refresh of the logs.
* When Frame Length Exceeds Threshold `threshold` - Use the Trigger Threshold parameter below to set a maximum frame time to wait before refreshing the log.
* When a Frame is Dropped `droppedframe` - Refresh the log as soon as a frame is dropped.
Trigger Threshold `triggerthreshold` - This is the amount of time, in milliseconds, that a frame must exceed to cause the DAT to log and output the frame's timing. For example to see what happens when a frame takes more that 33 ms to cook, put this parameter to 33.
Cook Time `logcook` - Logs the cook time of operators.
Export Time `logexport` - Logs time spent exporting CHOP channels.
Viewport Draw Time `logviewport` - Logs time to draw 3D geometry and SOP viewers.
Movie Time `logmovie` - Logs time taken to read video and audio from movie files.
Draw Channels Time `logdrawchannels` - Logs time to draw channels in CHOP viewers.
Object View Time `logobjectview` - Logs time to draw objects in 3D viewers.
Custom Panel Time `logcustompanel` - Logs time taken by custom panels build with [Panel Components](Panel_Component.html "Panel Component").
MIDI Time `logmidi` - Logs time spent on MIDI.
Graphics Time `loggraphics` - Logs various graphics system calls, such as time spent waiting for the graphics card, calls to the graphic driver, converting TOP data to CHOPs, etc.
Frame Length `logframelength` - Logs total frame time in milliseconds (ms).
Misc `logmisc` - Logs miscellaneous times that do not fit into other categories.
Script `logscript` - Logs time spent running scripts.
Render `logrender` - Logs time spend by Render or Renderpass TOPs.
  

## Parameters - Common Page
Language `language` - ⊞ - Select how the DAT decides which script language to operate on.
* Input `input` - The DAT uses the inputs script language.
* Node `node` - The DAT uses it's own script language.
Edit/View Extension `extension` - ⊞ - Select the file extension this DAT should expose to external editors.
* dat `dat` - various common file extensions.
* From Language `language` - pick extension from DATs script language.
* Custom Extension `custom` - Specify a custom extension.
Custom Extension `customext` - Specifiy the custom extension.
Word Wrap `wordwrap` - ⊞ - Enable Word Wrap for Node Display.
* Input `input` - The DAT uses the inputs setting.
* On `on` - Turn on Word Wrap.
* Off `off` - Turn off Word Wrap.
  

## Info CHOP Channels
Extra Information for the Perform DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Common DAT Info Channels
* num\_rows - Number of rows in this DAT.
* num\_cols - Number of columns in this DAT.
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
| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • Perform• [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

To re-compute the output data of the [Operators](Operator.html "Operator"). An operator cooks when (1) its inputs change, (2) its [Parameters](Parameter.html "Parameter") change, (3) when the timeline moves forward in some cases, or (4) [Scripting](Script.html "Script") commands are run on the node. When the operator is a [Panel Component](Panel_Component.html "Panel Component"), it also cooks when a user interacts with it. When an operator cooks, it usually causes operators connected to its output to re-cook. When TouchDesigner draws the screen, it re-cooks all the [Dependencies](Dependency.html "Dependency") - the necessary operators in all [Networks](Network.html "Network"), contributing to a frame's total "cook time".

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

A set of commands located in a Text DAT that are triggered to run under certain conditions. There are two scripting languages in TouchDesigner: [Python](Python.html "Python") and the original [Tscript](Tscript.html "Tscript"). Scripts and single-line commands can also be run in the [Textport](Textport.html "Textport").

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

Retrieved from "<https://docs.derivative.ca/index.php?title=Perform_DAT&oldid=24305>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")