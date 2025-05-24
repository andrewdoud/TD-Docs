

OSC Out DAT - TouchDesigner Documentation




# OSC Out DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The OSC Out DAT is used for sending information over a OSC connection between remotely located computers. Use the [`.sendOSC()`](https://docs.derivative.ca/OscoutDAT_Class "OscoutDAT Class") python method to output the OSC messages.
OSC bundles allows you to send a group of messages in a single command rather than as separate, individual messages. The OSC Out DAT `sendOSC()` function will accept a list of messages and send as a bundle when you set the kwarg `asBundle=True`.
Bundles were created as a performance optimization for real-time control of synthesizers with a large number of parameters. (thx Jesse Gilbert)
See also [OSC](OSC.html "OSC"), [OSC In DAT](OSC_In_DAT.html "OSC In DAT"), [OSC In CHOP](OSC_In_CHOP.html "OSC In CHOP"), [OSC Out CHOP](OSC_Out_CHOP.html "OSC Out CHOP"), [iOS and OSC](IOS_and_OSC.html "IOS and OSC"), [Network Protocols](Network_Protocols.html "Network Protocols"), [Sync](Sync.html "Sync").
**NOTE for Windows OS - If experiencing connection issues make sure Windows Firewall is disabled.**
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[oscoutDAT\_Class](https://docs.derivative.ca/OscoutDAT_Class "OscoutDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Connect Page](#Parameters_-_Connect_Page)
* [3 Parameters - Received Messages Page](#Parameters_-_Received_Messages_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Specific OSC Out DAT Info Channels](#Specific_OSC_Out_DAT_Info_Channels)
  + [6.2 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [6.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Connect Page
Active `active` - While on, the DAT receives/sends information from/to the network port. While Off, no updating occurs. Data sent to the port is lost.
Protocol `protocol` - ⊞ - Selects the network protocol to use. Refer to the [Network Protocols](Network_Protocols.html "Network Protocols") article for more information.
* Messaging (UDP) `msging` -
* Multi-Cast Messaging (UDP) `multicastmsging` -
* Reliable Messaging (UDT Library) `reliablemsging` -
Network Address `address` - The network address of the target computer when using UDP. For multi-cast this is the multi-cast address to send to. This address is a standard WWW address, such as 'foo' or 'foo.bar.com'. You can put an IP address (e.g. 100.123.45.78). If you put "localhost", it means the other end of the pipe is on the same computer.
Port `port` - The network port to send to.
Local Address `localaddress` - Specify an IP address to send from, useful when the system has mulitple NICs (Network Interface Card) and you want to select which one to use.
Shared Connection `shared` - Use the same connection as other networking DATs using the same network protocol.
OSC Address Scope `addscope` - To reduce which channels are generated, you can use channel name patterns to include or exclude channels. For example, `^*accel*` will exclude accelerometer channels coming in from an iOS or iPhone app like mrmr. See [Pattern Matching](Pattern_Matching.html "Pattern Matching") for the syntax of the possible channel name patterns.
Include Type Tag `typetag` - Includes the argument list type tag in each message. It includes the parameter type keywords (in case the parsing application needs to identify parmameter types).
Split Bundle into Messages `splitbundle` - When On, each message contained within a bundle is given its own row.
Split Message into Columns `splitmessage` - When On, OSC address and arguments are given individual columns, otherwise they are included in the message column.
Bundle Timestamp Column `bundletimestamp` - When On, each bundle timestamp value is included in a column.
  

## Parameters - Received Messages Page
Callbacks DAT `callbacks` - The Callbacks DAT will execute once for each message received.
Execute from `executeloc` - ⊞ - Determines the location the script is run from.
* Current Node `current` - The script is executed from the current node location.
* Callbacks DAT `callbacks` - The script is executed from the location of the DAT specified in the Callbacks DAT parameter.
* Specified Operator `op` - The script is executed from the operator specified in the From Operator parameter below.
From Operator `fromop` - The operator whose state change will trigger the DAT to execute its script when Execute from is set to Specified Operator. This operator is also the path that the script will be executed from if the Execute From parameter is set to Specified Operator.
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
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the OSC Out DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific OSC Out DAT Info Channels
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
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • OSC Out• [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.

Each operator can have a set of text strings that are its "tags". You can set them and search for them within TouchDesigner.

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=OSC_Out_DAT&oldid=26635>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")