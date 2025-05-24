

JSON DAT - TouchDesigner Documentation





























# JSON DAT

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The JSON DAT converts and filters JSON text using [JSONPath](https://docs.derivative.ca/JSONPath "JSONPath") syntax and outputs the filtered results. It eliminates having to code scripts to parse and manipulate JSON, and keeps the data flow procedural.

It expects JSON text as input and converts the input to a Python object in the `DAT.source` member.

It then filters the JSON down using the [JSONPath Filter parameter](https://docs.derivative.ca/JSONPath "JSONPath"), and it outputs the resulting data from the DAT as JSON text.

It also puts the filtered results as `DAT.results` (a Python list of results) and `DAT.result` (the first result).

You can test expressions on `DAT.source`, `DAT.result` and `DAT.results` by setting the Output menu to Expression and using expressions like `me.result['city']`, which outputs the evaluated expression from the DAT. You can then use that expression as `op('json1').result['city']` in an expression elsewhere. `DAT.expr` is also a member of the JSON DAT, for example, `op('json1').expr` returns the evaluated expression parameter.

**Output tables**: The JSON DAT can output a table by setting the Output Format menu to Table. It will do its best to take the result of the JSON Filter and form rows and columns of values and headings in a DAT table. Any cell that can't be expressed as a simple string, integer, float or boolean will be left as the JSON string of the remainder. A cell or range of cells can be further reduced with a [Select DAT](Select_DAT.html "Select DAT") and then passed to another JSON DAT which can convert the JSON strings to a table.

**See also:** [JSONPath](https://docs.derivative.ca/JSONPath "JSONPath"), [OP Snippets](OP_Snippets.html "OP Snippets"), and the [TDJSON](TDJSON.html "TDJSON") functions for converting and manipulating JSON data.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[jsonDAT\_Class](https://docs.derivative.ca/JsonDAT_Class "JsonDAT Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - JSON Page](#Parameters_-_JSON_Page)
* [3 Parameters - Common Page](#Parameters_-_Common_Page)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - JSON Page

Filter `filter` - A filter string following JSONPath syntax that will be used to filter the input JSON.
Output `output` - ⊞ - Select the output of the JSON DAT.

* Filter Result `filterresult` - Outputs list returned from applying the filter to the JSON text input.

* Expression `expression` - Output a custom expression.

Expression `expression` - The custom expression to output
Format Output `formatoutput` - When enabled, the output of the DAT will formatted with indents and newlines.
Hold Last Non-Empty Results `holdlast` - When enabled, the most recent result will be held if the results become empty, in effect only new non-empty results will update the output.

  


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

  


## Operator Inputs

* Input 0:  - A JSON text input.

  


## Info CHOP Channels

Extra Information for the JSON DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\nwikieditor2021.10000before 2021.10000

| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • JSON• [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Experimental:POP to](https://docs.derivative.ca/Experimental:POP_to_DAT "Experimental:POP to DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


A text string that contains data (string, float, list, boolean, etc.) and operators (+ \* < etc) that are evaluated by the node's language (python or Tscript) and returns a string, float list or boolean, etc. Expressions are used in parameters, [DATs](DAT.html "DAT") and in scripts.


Operators that need 1 or more inputs are called Filters in TouchDesigner, like a Math CHOP. See [Generator](Generator.html "Generator").


The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=JSON_DAT&oldid=33190>"
[Category](Special_Categories.html "Special:Categories"):

* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")