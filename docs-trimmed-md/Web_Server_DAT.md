

TouchDesigner Documentation




# Web Server DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Web Server DAT allows you to connect to TouchDesigner as a web client, through a web browser for example. The Web Server DAT supports HTTP, WebSockets, as well as the sending/receiving of binary data, such as images (uploading/downloading). How client requests are handled is left up to the user via callbacks.
The Web Server DAT can be secure, and also supports basic authentication via the authenticateBasic in the [webserverDAT\_Class](https://docs.derivative.ca/WebserverDAT_Class "WebserverDAT Class"). Currently only Basic authentication (ie. encoded username and password) is supported via a python method. Authentication will be in the HTTP request dictionary under the key 'Authorization'.
Ultimately, security is the complete responsibility of the user. It is up to the user to ensure that HTTP requests are properly authenticated, and any data storing usernames/passwords are encrypted or saved privately.
HTTPS is supported via the Secure (TLS) parameter.
The Web Server DAT is built with [POCO](https://github.com/pocoproject/poco) v1.9.1.
See also: [Web Client DAT](Web_Client_DAT.html "Web Client DAT")
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[webserverDAT\_Class](https://docs.derivative.ca/WebserverDAT_Class "WebserverDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Web Server Page](#Parameters_-_Web_Server_Page)
* [3 Parameters - Common Page](#Parameters_-_Common_Page)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Specific Web Server DAT Info Channels](#Specific_Web_Server_DAT_Info_Channels)
  + [4.2 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [4.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Web Server Page
Active `active` - Starts and Stops the webserver.
Restart `restart` - When the server is active, pulsing will restart it.
Port `port` - The web server's connection port. Eg. If the port number is 9980, the web server can be connected to locally (via a web browser) at the address "localhost:9980".
Secure (TLS) `secure` - When enabled, the web server will use transport layer security (TLS) to create secure connections with clients. As a result, the web server will run through HTTPS instead of HTTP.
Private Key File Path `privatekey` - The path to the private key file of the server's TLS certificate.
Certificate File Path `certificate` - The path to the certificate file of the server's TLS certificate.
Certificate Password `password` - The password for the certificate specified above. The password is only visually hidden and can still be accessed via python. In order to protect it and encrypt it when the project is saved, the Web Server DAT should be put in a private component.
Callbacks DAT `callbacks` - A reference to a DAT with python callbacks. The Web Server DAT relies heavily on the Callbacks DAT, and in fact most functionality passes through the callbacks.
`onHTTPRequest` - Triggered when the web server receives an HTTP request. The request is a dictionary of HTTP headers. Similarly, response is a dictionary of response data such as status and reason. Additional key/value pairs can be added to the response dictionary that will be added as headers in the HTTP response. The response server must be returned from the callback. This response will be sent back to the client.
`onWebSocketOpen` - Triggered when a WebSocket connection is opened with a client. The client address is passed to the callback.
`onWebSocketClose` - Triggered when a WebSocket connection is closed. The client address is passed to the callback.
`onWebSocketReceiveText` - Triggered when the server's WebSocket connection receives text data from a client. The client that sent the text data is passed through to the callback.
`onWebSocketReceiveBinary` - Triggered when the server's WebSocket connection receives binary data from a client. The client that sent the binary data is passed through to the callback.
`onServerStart` - Triggered when the server starts.
`onServerStop` - Triggered when the server stops.

  

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
Extra Information for the Web Server DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific Web Server DAT Info Channels
* server\_running -
* websocket\_connections -
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
  
TouchDesigner Build: Latest\n2021.100002020.20000before 2020.20000
| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • Web Server• [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=Web_Server_DAT&oldid=24484>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")