

TouchDesigner Documentation





























# Multi Touch In DAT

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Multi Touch In DAT is used for receiving messages and events from the Windows standard multi-touch API. It captures all the messages, where each new message changes the table it outputs. When a messages is added to the DAT, any script can be called pointing to the new message. The Multi Touch In DAT can be sent to the [Render Pick DAT](Render_Pick_DAT.html "Render Pick DAT"), or used with interactTouch methods in the [Panel Component](Panel_Component.html "Panel Component") and [Web Render TOP](Web_Render_TOP.html "Web Render TOP"). Multi Touch DAT is not supported on macOS.

It can output either of two table formats: (1) Raw Events as a FIFO (first in - first out) list, or (2) ID Table, which is the events processed into a more usable one-row-per-finger table.

The Raw Events format creates a FIFO-type DAT (see also [FIFO DAT](FIFO_DAT.html "FIFO DAT")) which, for each multi-touch event, has a row added to the bottom of the table while at the same time a row at the top is deleted.

Note: To operate panel gadgets with multi-touch screens that send events through the Windows event stream, multi-touch works without requiring DATs. You need to use the DAT when using multiple fingers on one panel, like in a container displaying a 3D render whose objects you want to pick.

The ID table format includes the columns:

* `id` - every finger press increases the id by 1
* `sn` - an ongoing count of each finger press.
* `select` - when 1, this row represents a finger is down.
* `downf` - the absolute frame number when the finger press occurred.
* `upf` - the absolute frame number that the finger press ended
* `x`, `y` - the position, in pixels in the horizontal and vertical directions. `NOTE`: The `x` and `y` values are expressed in screen pixels, not panel width/height pixels. For example, the top-right corner of a panel will be different if the panel is scaled within another panel, window or network viewer. It is better to use `u` and `v`, and scale them by the panel Width and Height.
* `u`, `v` - the position, 0 to 1 in the horizontal and vertical directions
* `downu`, `downv` - the position, 0 to 1 in the horizontal and vertical directions when the touch first occured (ie. initial touch down location).

`contactx`, `contacty` - the width of the contact area.
`contactu`, `contactv` - the height of the contact area.

* + `monitor` - monitor number, starting with 0
* `clicktime` - like `downf`, in seconds
* `elapsedtime` - the number of seconds that finger has been down.
* `changedtime` - the time since the finger press that the most recent u or v value changed.
* `dclick` - double-tap occurred
* `aux` - user supplied data via the [PanelCOMP\_Class](PanelCOMP_Class.html "PanelCOMP Class") method `interactTouch()`. When the event is triggered by the mouse via the Include Mouse option, `aux` will include the mouse buttons used (`1` for left, `2` for middle, `4` for right, can be tested bitwise).

You can use the attached callback DAT (named `mtouchin1_callbacks`) to react to multi-touch events. This is suitable for 2D interfaces that do not require a [Render Pick DAT](Render_Pick_DAT.html "Render Pick DAT").

See the [Palette:multiTouch](Palette_multiTouch.html "Palette:multiTouch") example in the [Palette](Palette.html "Palette") under Tools.

See also the [MultiTouch](MultiTouch.html "MultiTouch") page.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[multitouchinDAT\_Class](https://docs.derivative.ca/MultitouchinDAT_Class "MultitouchinDAT Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Multi Touch In Page](#Parameters_-_Multi_Touch_In_Page)
* [3 Parameters - Received Messages Page](#Parameters_-_Received_Messages_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Multi Touch In Page

Active `active` - Registers event when Active is On.
Output `outputtype` - ⊞ - Sets how the output is displayed in the table.

* Raw Events `log` - Events are added to the table in a first in - first out (FIFO) order.

* ID Table `changes` - Events are processed using one-row-per-finger in the table.

Panel `panel` - The [Panel Component](Panel_Component.html "Panel Component") to capture the touch events from.
Relative IDs `relativeid` - Reorder the touch ids so only the ones within the specified panel are counted.
Relative Position `relativepos` - Output position and normalized coordinates relative to lower left corner of the specified panel.
Include Mouse `mouse` - When on, the mouse add a touch event when clicked. This event always shares ID 1 with the first touch. Using mouse and multitouch at the same time may result in unexpected behaviours.
Position Threshold `posthresh` - A new message will not be added if a finger has moved less than this number of units. The units are determined by the input device, not necessarily the resolution of the screen that it is associated with.
Contact Threshold `contactthresh` - Some touch devices have a width and height of a press, representing pressure of amount of finger contact. This is a minimum threshold below which no events are recognized.
Min Rows Displayed `minrows` - The minimum number of rows always displayed in the table.
Double Click (secs) `doubleclickthresh` - The maximum time allowed between clicks to be registered as a 'double-click'.

  


## Parameters - Received Messages Page

Callbacks DAT `callbacks` - Path to a DAT containing callbacks.
Execute from `executeloc` - ⊞ - Determines the location the script is run from.

* Current Node `current` - The script is executed from the current node location (for example, where 'cc' points to).

* Callbacks DAT `callbacks` - The script is executed from the location of the Callbacks DAT specified above.

* Specified Operator `op` - The script is executed from the component specified in the Component parameter below.

From Operator `fromop` - The path that the script will be executed from if the Execute From parameter is set to *Specified Operator*.
Clamp Output `clamp` - The DAT is limited to 100 messages by default but with Clamp Output, this can be set to anything including unlimited.
Maximum Lines `maxlines` - Limits the number of messages, older messages are removed from the list first.
Clear Output `clear` - Deletes all lines except the heading. To clear with a script command, here is an example: `opparm -c /serial1 clear`

  


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

Extra Information for the Multi Touch In DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\nwikieditor2021.100002018.28070before 2018.28070

| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • Multi Touch In• [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Multi_Touch_In_DAT&oldid=30039>"
[Category](Special_Categories.html "Special:Categories"):

* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")