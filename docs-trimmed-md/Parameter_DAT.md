

TouchDesigner Documentation




# Parameter DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Parameter DAT outputs a table of parameter names and values of an operator, including custom parameters, from any OP type.
It can output pre-evaluated expressions, the [Parameter Mode](Parameter_Mode.html "Parameter Mode") plus all attributes that define parameters - their type, label, ranges, menu items, limits, etc. in up to 24 columns of information.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[parameterDAT\_Class](https://docs.derivative.ca/ParameterDAT_Class "ParameterDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Parameter Page](#Parameters_-_Parameter_Page)
* [3 Parameters - Output Page](#Parameters_-_Output_Page)
* [4 Parameters - Define Page](#Parameters_-_Define_Page)
* [5 Parameters - Common Page](#Parameters_-_Common_Page)
  

## Parameters - Parameter Page
Operators `ops` - The operators determine where to obtain the channels. Specify or more operator names or paths. Examples: `wave1`, `slider*`, `constant[1-9] constant[10-19:2]`, `../base1`. Or select the operators using the menu.
Parameters `parameters` - The list of parameters names (which can include wildcards) you want to get from the OP(s). One or more parameter, or \* for all parameters. You can also specify a "NOT" selection with an `^`. Or select the parameter using the menu. See [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Include Op Name `includeopname` - Adds the OP name to the beginning of each parameter name in the table
Rename from `renamefrom` - See [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Rename to `renameto` - See [Pattern Expansion](Pattern_Expansion.html "Pattern Expansion").
Custom `custom` - Output the operators' custom parameters.
Built-In `builtin` - Output the operators' built-in parameters.
  

## Parameters - Output Page
Toggles for information about the parameter and its value
Header `header` - Outputs the column headers.
Name `name` - Outputs the parameter name.
Value `value` - Outputs the evaluated parameter value.
Eval `eval` - Outputs the evaluated parameter value as a python object.
Constant `constant` - Outputs the current constant value of the parameter.
Expression `expression` - Outputs the current python expression of the parameter.
Export `export` - Outputs the export path of the parameter.
Mode `mode` - Outputs the current mode of the parameter (constant, expression, or export).
Style `style` - Outputs what format the parameter is (eg. Float for float parameters, Menu for menu parameters etc.).
Tuplet Name `tupletname` - Outputs the name of the tuplet the parameter is in. For example, tx on the Geometry COMP is a part of the 't' tuplet.
Size `size` - Outputs the size of the tuplet. For example, tx on the Geometry COMP would have a tuplet size of 3 since it's a part of the 't' tuplet with 3 parameters.
Path `path` - Outputs the path to the node.
Menu Index `menuindex` - If the parameter is a menu, then output the selected index of the menu.
  

## Parameters - Define Page
Toggles for information that define the parameter.
Min/Max `minmax` - Outputs the minimum and maximum values of the parameter. These values will clamp the value parameter to be within the range. If clampmin is 0 then the minimum will not clamp and the row/column entry will be 0. If clampmax is 0 then the maximum will not clamp and the row/column entry will be 1.
Clamp Min/Max `clampminmax` - Outputs whether or not the parameter has a clamped min or clamped max. If true, then the values are defined by min/max columns.
Norm Min/Max `normminmax` - Outputs the minimum and maximum values of the parameter in the interface (ie. the minimum and maximum values of a slider).
Default `default` - Outputs the default value of the parameter
Enabled `enabled` - Outputs whether the parameter is currently enabled
Read Only `readonly` - Outputs whether the parameter is currently read-only
Section `section` - Outputs whether the parameter has a section divider/separator (ie. line) above it.
Menu Names `menunames` - Outputs a list of the menu names for any menu parameters.
Menu Labels `menulabels` - Outputs a list of the menu labels for any menu parameters.
  

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
TouchDesigner Build: Latest\n2021.100002019.146502018.28070
| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • Parameter• [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

A text string that contains data (string, float, list, boolean, etc.) and operators (+ \* < etc) that are evaluated by the node's language (python or Tscript) and returns a string, float list or boolean, etc. Expressions are used in parameters, [DATs](DAT.html "DAT") and in scripts.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

A tuplet is the set of parameters that appear on one line of the parameter dialog. Tuplets occupy a [page](Page_Class.html "Page Class") of parameters.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

Retrieved from "<https://docs.derivative.ca/index.php?title=Parameter_DAT&oldid=16166>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")