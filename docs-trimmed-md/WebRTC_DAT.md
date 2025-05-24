

# WebRTC_DAT

WebRTC DAT - TouchDesigner Documentation





# WebRTC DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
A WebRTC DAT represents a peer on one end of any number of [WebRTC](WebRTC.html "WebRTC") peer-to-peer connections.
Each connection is represented in TouchDesigner by a generated UUID. The UUID must be passed to [WebrtcDAT Class](https://docs.derivative.ca/WebrtcDAT_Class "WebrtcDAT Class") connection-level python methods.
The WebRTC DAT output is a table formatted with a row per connection, with columns: id (ie. UUID), [connection\_state](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/connectionState), [signaling\_state](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/signalingState), [ice\_connection\_state](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/iceConnectionState), and [ice\_gathering\_state](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/iceGatheringState).
The columns altogether describe the state of a connection and can also be useful for debugging. For example, if ice\_connection\_state failed then that means there's an issue pairing local and remote ICE candidates for streaming over the network. It could be that NAT traversal failed, and if using a STUN server that might indicate a need for a TURN server (see <https://en.wikipedia.org/wiki/STUN#Limitations>).
WebRTC video and audio input/output is done via the [Video Stream In TOP](Video_Stream_In_TOP.html "Video Stream In TOP"), [Video Stream Out TOP](Video_Stream_Out_TOP.html "Video Stream Out TOP"), [Audio Stream In CHOP](Audio_Stream_In_CHOP.html "Audio Stream In CHOP"), and [Audio Stream Out CHOP](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP").
See also [WebRTC](WebRTC.html "WebRTC").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[webrtcDAT\_Class](https://docs.derivative.ca/WebrtcDAT_Class "WebrtcDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Connection Page](#Parameters_-_Connection_Page)
* [3 Parameters - ICE Page](#Parameters_-_ICE_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
  

## Parameters - Connection Page
Active `active` - When active, can connect to peers and send media/data. When deactivated, all existing connections will be closed.
Reset `reset` - Resets the peer associated with the DAT. Equivalent to deactivating then reactivating the active parameter.
Custom Bit Rate Limits `bitratelimits` - When enabled, custom min/max bit rates can be specified. These max bit rate limits are expressed in kbps and apply to all tracks associated with the WebRTC DAT.
Minimum Bit Rate (kbps) `minbitrate` - Minimum bit rate for all tracks associated with the WebRTC DAT.
Maximum Bit Rate (kbps) `maxbitrate` - Maximum bit rate for all tracks associated with the WebRTC DAT.
Callbacks DAT `callbacks` - Reference to a DAT containing WebRTC callbacks.
  

## Parameters - ICE Page
STUN Server URL `stun` - URL of the STUN server. See [WebRTC#ICE](WebRTC.html#ICE "WebRTC") for more details regarding STUN.
TURN Username `username` - Username for access to the specified TURN servers.
TURN Password `password` - Password for access to the specified TURN servers.
TURN Server `turn` - Sequence of TURN server urls.
TURN Server URL 0 `turn0server` - URL of the TURN server. See [WebRTC#ICE](WebRTC.html#ICE "WebRTC") for more details regarding TURN.
  

## Parameters - Common Page
Language `language` - ⊞ - Select how the DAT decides which script language to operate on.
* Input `input` - The DAT uses the inputs script language.
* Node `node` - The DAT uses it's own script language.
Edit/View Extension `extension` - ⊞ - Select the file extension this DAT should expose to external editors.
* dat `dat` - various common file extensions.
* frag `frag` -
* glsl `glsl` -
* html `html` -
* md `md` -
* py `py` -
* rtf `rtf` -
* tsv `tsv` -
* txt `txt` -
* vert `vert` -
* xml `xml` -
* From Language `languageext` - pick extension from DATs script language.
* Custom Extension `customext` - Specify a custom extension.
Custom Extension `customext` - Specifiy the custom extension.
Word Wrap `wordwrap` - ⊞ - Enable Word Wrap for Node Display.
* Input `input` - The DAT uses the inputs setting.
* On `on` - Turn on Word Wrap.
* Off `off` - Turn off Word Wrap.
TouchDesigner Build: Latest\nwikieditorwikieditor2022.24140before 2022.24140
| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • WebRTC• [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").
The grey dashed lines between nodes is a Reference (or [Link](Link.html "Link")). A Reference is (1) a [Parameter Reference](Parameter_Reference.html "Parameter Reference"), a parameter in an OP that is a name or path to another operator, (2) a [Node Reference](https://docs.derivative.ca/index.php?title=Node_Reference&action=edit&redlink=1 "Node Reference (page does not exist)"), an expression in a parameter or DAT script that contains the name or path of another operator, (3) a DAT Cell Reference or (4) a CHOP Channel Reference.
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

Retrieved from "<https://docs.derivative.ca/index.php?title=WebRTC_DAT&oldid=32308>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")