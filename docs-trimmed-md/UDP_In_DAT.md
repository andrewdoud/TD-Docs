

UDP In DAT - TouchDesigner Documentation





























# UDP In DAT

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The UDP In DAT is used for receiving information over a UDP connection between two remotely located computers. It captures all the messages without any queuing or buffering, and allows you to send it any messages you want. Once this DAT has received a message it can reply to the sender using the 'send' command. Using the send command before it has received a message will not work because it doesn't know where to send data yet. When in multicast mode it doesn't send out a multicast message, it sends a reply directly to the originator for the last multicast message it got.

See also [Peer Class](Peer_Class.html "Peer Class"), [UDP Out DAT](UDP_Out_DAT.html "UDP Out DAT"), [Touch In DAT](Touch_In_DAT.html "Touch In DAT") and [TCP/IP DAT](TCP/IP_DAT.html "TCP/IP DAT").

**NOTE for Windows OS - If experiencing connection issues make sure Windows Firewall is disabled.**

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[udpinDAT\_Class](https://docs.derivative.ca/UdpinDAT_Class "UdpinDAT Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Connect Page](#Parameters_-_Connect_Page)
* [3 Parameters - Received Data Page](#Parameters_-_Received_Data_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Specific UDP In DAT Info Channels](#Specific_UDP_In_DAT_Info_Channels)
  + [5.2 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [5.3 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Connect Page

Protocol `protocol` - ⊞ - Select which protocol to use, refer to the [Network Protocols](Network_Protocols.html "Network Protocols") article for more information.

* Messaging (UDP) `msging` -

* Multi-Cast Messaging (UDP) `multicastmsging` -

Network Address `address` - The multi-cast IP address to listen for.
Port `port` - The network port to listen on.
Shared Connection `shared` - Use the same connection as other networking DATs using the same network protocol.
Row/Callback Format `format` - ⊞ - Determines how the incoming data is parsed.

* One Per Byte `perbyte` - One row is added to the table per byte received.

* One Per Line `perline` - One row is added to the table per line received. The end of a line is delimited by \n, \r or a null character (\0).

* One Per Message `permessage` - One row is added to the table per message received.

Active `active` - This check box enables the connection.

  


## Parameters - Received Data Page

Callbacks DAT `callbacks` - The Callbacks DAT will execute once for each message coming in. See [udpinDAT\_Class](https://docs.derivative.ca/UdpinDAT_Class "UdpinDAT Class") for usage.
Execute from `executeloc` - ⊞ - Determines the location the script is run from.

* Current Node `current` - The script is executed from the current node location.

* Callbacks DAT `callbacks` - The script is executed from the location of the DAT specified in the Callbacks DAT parameter.

* Specified Operator `op` - The script is executed from the operator specified in the From Operator parameter below.

From Operator `fromop` - The operator whose state change will trigger the DAT to execute its script when Execute from is set to Specified Operator. This operator is also the path that the script will be executed from if the Execute from parameter is set to Specified Operator.
Clamp Output `clamp` - The DAT is limited to 100 messages by default but with Clamp Output, this can be set to anything including unlimited.
Maximum Lines `maxlines` - Limits the number of messages, older messages are removed from the list first.
Clear Output `clear` - Deletes all lines except the heading. To clear with a python script `op("opname").par.clear.pulse()`
Bytes Column `bytes` - Outputs the raw bytes of the message in a separate column.

  


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

Extra Information for the UDP In DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Specific UDP In DAT Info Channels

* messages\_pending -

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
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • UDP In• [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


Some operators have a DAT [docked](Docking.html "Docking") to them that contains some python functions. These functions, called "callbacks", get called when something in the operator changes.


The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=UDP_In_DAT&oldid=24481>"
[Category](Special_Categories.html "Special:Categories"):

* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")