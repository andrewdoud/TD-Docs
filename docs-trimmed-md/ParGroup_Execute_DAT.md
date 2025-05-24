

ParGroup Execute DAT - TouchDesigner Documentation





# ParGroup Execute DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[pargroupexecuteDAT\_Class](https://docs.derivative.ca/PargroupexecuteDAT_Class "PargroupexecuteDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - ParGroup Execute Page](#Parameters_-_ParGroup_Execute_Page)
* [3 Parameters - File Page](#Parameters_-_File_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Operator Inputs](#Operator_Inputs)
  

## Parameters - ParGroup Execute Page
Active `active` - While on, the DAT will respond to the Parameter that is referenced.
OPs `op` - Specify which operator(s) the triggering parameter belongs to.
Parameters `pars` - Specify which parameter(s) to monitor for triggering the script.
Callback Mode `callbackmode` - ⊞ - This controls the format of the 'curr' and 'prev' arguments to the callbacks.
* Per ParGroup Change `pargroup` - 'curr' and 'prev' are individual ParGroup objects.
* Combine ParGroup Changes as List `pargrouplist` - 'curr' and 'prev' are lists of all changed parameters.
Value Change `valuechange` - The onValueChange() method executes when the parameter value specified changes value in any way. It is called once each frame.
On Pulse `onpulse` - The onPulse() method executes when a 'pulse' type parameter is pulsed by clicking on it or via the [Par](Par_Class.html "Par Class").pulse() method.
Expression Change `expressionchange` - The onExpressionChange() method executes whenever the specified parameter's expression changes. For example, changing the expression from `me.time.frame` to `me.time.seconds` will trigger the script.
Export Change `exportchange` - The onExportChange() method executes if the export path to the specified parameter changes. For example, if the parameter is being exported to from /chopname/chan1 and that is changed so /chopname2/chan2 is now exporting to it, then the script will be triggered.
Enable Change `enablechange` - The onEnableChange() method executes if the specified parameter goes from being disabled to enabled.
Mode Change `modechange` - The onModeChange() method executes if the specified [parameter's mode](Parameter_Mode.html "Parameter Mode") changes between the available constant, expression, export or bind mode.
Custom `custom` - Monitor [Custom Parameters](Custom_Parameters.html "Custom Parameters").
Built-In `builtin` - Monitor Built-In parameters.
Edit.. `edit` - Clicking this opens a text editor to edit text in the DAT.
  

## Parameters - File Page
File `file` - The filesystem path and name of the file to load. Accepts `.txt` and `.dat` files.
Sync to File `syncfile` - When On, loads the file from disk into the DAT when the projects starts. A filename must be specified. Turning on the option will load the file from disk immediately. If the file does not exist, it will be created the first time the DAT is updated. The file is monitored so that any changes made to the file will update the DAT, and any changes made to the DAT will be written to the file right away. If the file is removed, the DAT will retain its current contents.
Load on Start `loadonstart` - When On, reloads the file from disk into the DAT when the projects starts.
Load File `loadonstartpulse` - Instantly reloads the file.
Write on Toe Save `write` - When On, writes the contents of the DAT out to the file on disk when the project is saved.
Write File `writepulse` - Instantly write the file to disk.
  

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
  

## Operator Inputs
* Input 0:  -
TouchDesigner Build: Latest\n2022.24140before 2022.24140
| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • ParGroup Execute• [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
A ParGroup is a group of related parameters that you can set and get as a whole instead of its individual parameters.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

Some operators have a DAT [docked](Docking.html "Docking") to them that contains some python functions. These functions, called "callbacks", get called when something in the operator changes.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

A text string that contains data (string, float, list, boolean, etc.) and operators (+ \* < etc) that are evaluated by the node's language (python or Tscript) and returns a string, float list or boolean, etc. Expressions are used in parameters, [DATs](DAT.html "DAT") and in scripts.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

Retrieved from "<https://docs.derivative.ca/index.php?title=ParGroup_Execute_DAT&oldid=26771>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")