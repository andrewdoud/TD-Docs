

TouchDesigner Documentation




# MQTT Client DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The MQTT Client DAT receives and sends data from/to [MQTT](MQTT.html "MQTT") devices via MQTT servers (broker). TouchDesigner can act as a client and another computer needs to act as a MQTT Server. Once a client establishes a connection with a server, it can do two things:
1. Send a message to the server to express interest in any data that has a specific "topic" string. This is called "subscribing". Then the MQTT Client DAT will receive all messages that the server gets with that topic.
2. Inform the server that it will send messages to the server with a certain topic string, and then send messages with that topic. The messages then get forward to any client that has expressed interest in that topic.
See also [MQTT](MQTT.html "MQTT"), [TCP/IP DAT](TCP/IP_DAT.html "TCP/IP DAT").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[mqttclientDAT\_Class](https://docs.derivative.ca/MqttclientDAT_Class "MqttclientDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Connect Page](#Parameters_-_Connect_Page)
* [3 Parameters - Received Data Page](#Parameters_-_Received_Data_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Specific MQTT Client DAT Info Channels](#Specific_MQTT_Client_DAT_Info_Channels)
  + [5.2 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [5.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Connect Page
Active `active` - Enable the connection.
Network Address `netaddress` - The address of the broker to connect to. The address should take the form `<protocol>://<host>:<port>`. Accepted protocol URIs can include `tcp`, `ssl`, `ws`, and `wss`.
Specify ID `specifyid` - Allows naming the client with parameter `User Client ID`, otherwise automatically and uniquely generated for each connection.
User Client ID `usercid` - Client name when `Specify ID` enabled.
Keep Alive Interval `keepalive` - Specifies in seconds, the maximum time to expect without communication. If no data is sent during this time, a lightweight ping message is sent to the server instead. Can be set to 0 to avoid pings.
Max in Flight `maxinflight` - Controls how many messages can be in-flight simultaneously.
Clean Session `cleansession` - If `Specify ID` is selected, the server will preserve any state information associated with the connection of that ID, such as subscriptions, delivery attempts, etc.
Verify Certificate `verifycert` - Enables TLS (transport layer security) certificate verification against the server (ie. broker).
Username `username` - Specify the username for authentication if the server requires it. MQTT servers that support the MQTT v3.1 protocol provide authentication and authorization via username and password.
Password `password` - Specify the password for authentication if the server requires it. MQTT servers that support the MQTT v3.1 protocol provide authentication and authorization via username and password.
Reconnect `reconnect` - Will attempt to reconnect to the MQTT broker.
  

## Parameters - Received Data Page
Callbacks DAT `callbacks` - The Callbacks DAT contains functions that are called when connections are made, lost or published data arrives. See [mqttclientDAT\_Class](https://docs.derivative.ca/MqttclientDAT_Class "MqttclientDAT Class") for usage.
Execute from `executeloc` - ⊞ - Determines the location the script is run from.
* Current Node `current` - The script is executed from the current node location (for example, where 'cc' points to).
* Callbacks DAT `callbacks` - The script is executed from the location of the DAT specified in the Callbacks DAT parameter.
* Specified Operator `op` - The script is executed from the operator specified in the From Operator parameter below.
From Operator `fromop` - The operator whose state change will trigger the DAT to execute its script when Execute From is set to Specified Operator. This operator is also the path that the script will be executed from if the Execute From parameter is set to Specified Operator.
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
Extra Information for the MQTT Client DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific MQTT Client DAT Info Channels
* connected -
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
  
TouchDesigner Build: Latest\nwikieditor2021.100002018.28070before 2018.28070
| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • MQTT Client• [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=MQTT_Client_DAT&oldid=29769>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")