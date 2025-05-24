

Keyboard In DAT - TouchDesigner Documentation





























# Keyboard In DAT

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Keyboard In DAT lists the most recent key events in its FIFO (first in/first out) table. There is one row for every key press down and every key-up, including Shift, Ctrl and Alt, with distinction between left and right side. For convenience, with each key press, a column indicates if the Shift, Ctrl and Alt were being held down at the time.

You get key presses even of the cursor is outside the TouchDesigner windows, whether they are control panels, Perform Mode or the network editor window. Exceptions: while entering text in the editor window.

You can set a filter to watch only certain keys. Custom shortcuts can be defined and handled by a [python callback in the attached script](https://docs.derivative.ca/KeyboardinDAT_Class "KeyboardinDAT Class").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[keyboardinDAT\_Class](https://docs.derivative.ca/KeyboardinDAT_Class "KeyboardinDAT Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Keyboard In Page](#Parameters_-_Keyboard_In_Page)
* [3 Parameters - Log Page](#Parameters_-_Log_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Notes](#Notes)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Keyboard In Page

Active `active` - Inhibits and allows message to be added to log.
Perform Window Only `perform` - When on, key events are only detected while in perform mode.
Keys `keys` - List of keys to allow through the filter. Just put the characters in the list, space-separated. Eg. '1 2 g h' for the 1, 2, g and h keys. Only these keys will be added to the log and generate an event. If blank, no filtering will be done. List of accepted keys: [Keyboard UI](https://docs.derivative.ca/Keyboard_UI "Keyboard UI")
Shortcuts `shortcuts` - List of shortcuts to watch for. See "Shortcuts" in the notes for defining shortcuts.
Panels `panels` - Optional list of references to panels to detect events from. Events will only be fired when any of the listed panels has focus.
Left/Right Modifiers `lrmodifiers` - When on, the states of the left and right modifier keys (see Notes) will be added to the table. Switching the state of this parameter will reset the table's contents.

  


## Parameters - Log Page

Callbacks DAT `callbacks` - Path to a DAT containing callbacks for each keyboard event received. See keyboardinDAT\_Class for usage.
Execute from `executeloc` - ⊞ - Determines the location the script is run from.

* Current Node `current` - The script is executed from the current node location (for example, where 'cc' points to).

* Callbacks DAT `callbacks` -

* Specified Operator `op` - The script is executed from the operator specified in the From Operator parameter below.

From Operator `fromop` - The operator whose state change will trigger the DAT to execute its script when Execute is set to Specified Operator. This operator is also the path that the script will be executed from if the Execute From parameter is set to Specified Operator.
Clamp Output `clamp` - The DAT is limited to 100 messages by default but with Clamp Output, this can be set to anything including unlimited.
Maximum Lines `maxlines` - Limits the number of messages, older messages are removed from the list first.
Clear Output `clear` - Deletes all lines except the heading. To clear with a python script `op("opname").par.clear.pulse()`

  


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

  


## Notes

**Shortcuts** are defined by a list of modifier keys (see below) and a "trigger" key separated by .'s.

For example, `ctrl.shift.a` the modifier keys are ctrl and shift, and the trigger key is a. This shortcut will be activated when one of the ctrl and shift keys are pressed and the trigger key, a is pressed down. If any other modifier keys are pressed, the shortcut will not be detected.

Modifier Keys - The following are all the valid modifier keys:

* `lalt` - Left alt key.
* `ralt` - Right alt key.
* `alt` - Either left or right alt key.
* `lctrl` - Left ctrl key.
* `rctrl` - Right ctrl key.
* `ctrl` - Either left or right ctrl key.
* `lshift` - Left shift key.
* `rshift` - Right shift key.
* `shift` - Either left or right shift key.

  


## Operator Inputs

* Input 0:  -

  


## Info CHOP Channels

Extra Information for the Keyboard In DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • Keyboard In• [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


Perform Mode is an optimized mode for live performance that only renders one specified [Window COMP](Window_COMP.html "Window COMP") which is one window that contains your video outputs and your (optional) control interface. In Perform Mode the network editing window is not open - you edit your networks in [Designer Mode](Designer_Mode.html "Designer Mode"). Alternate with F1 and Esc.


A Window in TouchDesigner is a window in Microsoft Windows or macOS that contains either (1) the TouchDesigner editing interface that exists in [Designer Mode](Designer_Mode.html "Designer Mode"), or (2) a user-created [Panel](Panel.html "Panel") inside a [Window Component](Window_COMP.html "Window COMP"). The user-created windows can span [Multiple Monitors](Multiple_Monitors.html "Multiple Monitors") borderless, or be floating windows with borders, or popups.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Keyboard_In_DAT&oldid=24323>"
[Category](Special_Categories.html "Special:Categories"):

* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")