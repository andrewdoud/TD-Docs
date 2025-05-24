

# Web_DAT

Web DAT - TouchDesigner Documentation




# Web DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
**Note**: Web DAT deprecated build 2019.15230, use [Web Client DAT](Web_Client_DAT.html "Web Client DAT").
```
   The Web DAT fetches pages of data from a web connection. The data should be ASCII-readable. The Web DAT will automatically uncompress any gzip compressed page transfers. XML content is formatted into a readable indented structure, versus one long line normally sent by the server. An Info DAT can be used to obtain properties of the last page retrieved.		
```
There are two main methods of retrieving a page from a web site using the Web DAT:
* Fetch
* Submit and Fetch
The Fetch method simply fetches the page from the internet using the simple protocol "GET", while the Submit and Fetch method can be used for submitting form data to a server. By default the latter method uses the "POST" protocol.
  
Both methods allow a DAT table input to specify options while fetching. This table should consist of rows of name/value pairs. The first column consists of the names, while the second column consists of the values. The Fetch method simply concatenates the pairs into the specified URL, while the Update and Fetch method posts the pairs to a webserver, before fetching the resulting page.
For example, assume a table with the following contents is connected to the Web DAT:
| name | joe |
| --- | --- |
| month | May |
If the specified URL is:
*[http://www.example.com](http://www.example.com/)*
Then the Fetch method will actually fetch:
*[http://www.example.com?name=joe&month=May](http://www.example.com/?name=joe&month=May)*
Similarly, the Submit and Fetch method will post the pairs to the specified webserver, before fetching the page.
Note that spaces and other special characters in the table will be properly encoded. For example, each space in a name or value would be encoded as: %20
The first input can also be text data, in which case the data is sent to the webserver during a POST as-is, without any formatting or encoding. If the first input is text it will be ignored during a GET operation.
The 2nd input of the Web DAT can be used for custom HTTP request headers to be specified as part of the request. Like the 1st input this should be a table of name/value pairs for header field name and the value. E.g
| Content-Type | application/json |
| --- | --- |
| Date | Tue, 12 Nov 2013 08:12:31 GMT |
Each row will automatically be merged into a single line of text separated by a colon. If the 2nd column is empty then the entry in the first column will have a semi-color append to it when it's turned into the request header.
See also [XML DAT](XML_DAT.html "XML DAT"), [TCP/IP DAT](TCP/IP_DAT.html "TCP/IP DAT"), [WebSocket DAT](WebSocket_DAT.html "WebSocket DAT").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[webDAT\_Class](https://docs.derivative.ca/WebDAT_Class "WebDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Fetch Page](#Parameters_-_Fetch_Page)
* [3 Parameters - Common Page](#Parameters_-_Common_Page)
* [4 Operator Inputs](#Operator_Inputs)
  

## Parameters - Fetch Page
URL `url` - The url address of the web page to be retrieved.
Fetch `fetch` - The data will be fetched when this button is pressed. Use this method to retrieve simple single pages from the internet. By default the Web DAT will stall the process until the whole page has been transferred, or an error occurs. You can do asynchronous downloads using the Asynchronous Fetch option.
Submit Method `method` - ⊞ - Currently only POST is implemented, though this will be expanded with other techniques such as GET.
* POST `post` -
Submit and Fetch `submitfetch` - Post all the name/value pairs from the input DAT to the server, then fetch the page specified in the URL parameter.
Use this method to post data to a web server before retrieving the page. The data to be sent is in the form of name and value pairs. It can be specified with a table formatted DAT connected to the first input, where the first column represents data names, and the second column represents data values. The Web DAT will pause until the whole page has been transferred, or an error occurs.

Include Header in Output `includeheader` - Includes the HTTP header in the output.
Timeout `timeout` - If this value is 0 the fetch request will never timeout. Any other value is how many milliseconds before the fetch times out.
Disconnect `disconnect` - Closes the session.
Asynchronous Fetch `asyncfetch` - Turn on this option to allow the download to occur in the background. You can use a [DAT Execute DAT](DAT_Execute_DAT.html "DAT Execute DAT") to do something when the data finally arrives.
Verify Peer Certificate `verifypeer` - Enables TLS (transport layer security) certificate verification.
  

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
* Input 1:  -
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • Web• [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

Retrieved from "<https://docs.derivative.ca/index.php?title=Web_DAT&oldid=22474>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")