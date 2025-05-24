

# Select_DAT

Select DAT - TouchDesigner Documentation




# Select DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Select DAT allows you to fetch a DAT from any other location in the project, and to select any subset of rows and columns if it is a table.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[selectDAT\_Class](https://docs.derivative.ca/SelectDAT_Class "SelectDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Select Page](#Parameters_-_Select_Page)
* [3 Parameters - Common Page](#Parameters_-_Common_Page)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Select Page
DAT `dat` - The [path](Network_Path.html "Network Path") of the DAT being referenced.
Include First Row `firstrow` - Forces the first row to be selected even if it is not specified by the Select Rows settings.
Include First Col `firstcol` - Forces the first column to be selected even if it is not specified by the Select Cols settings.
Select Rows `extractrows` - ⊞ - This parameter allows you to pick different ways of specifying the rows selected.
* All `all` - All rows selected.
* by Name `byname` - Rows selected using Start Row Name and End Row Name parameters.
* by Index `byindex` - Rows selected using Start Row Index and End Row Index parameters.
* by Start Name, End Index `bynameindex` - Rows selected using Start Row Name and End Row Index parameters.
* by Start Index, End Name `byindexname` - Rows selected using Start Row Index and End Row Name parameters.
* by Values `bynames` - Rows selected by specifying the row values explicitly.
* by Condition `byexpr` - Rows selected by an expression to be evaluated for the from column.
Start Row Name `rownamestart` - Specify the row name to start the selection range from.
Start Row Index `rowindexstart` - Specify the row index to start the selection range from.
End Row Name `rownameend` - Specify the row name to end the selection range.
End Row Index `rowindexend` - Specify the row index to end the selection range.
Row Select Values `rownames` - Specify actual row names that you want to select. You can use TouchDesigner's pattern matching (see wiki page [Pattern Matching](Pattern_Matching.html "Pattern Matching")), for example `row[1-4]` will select all the rows names `row1` thru `row4`. Some characters like `'` need a `\` in front of it.
Row Select Condition `rowexpr` - Specify an expression that will be evaluated. If the expression evaluates to true, the row will be selected.
Expand the parameter and you will see that it is in [expression mode](Parameter_Mode.html "Parameter Mode").
[![SelectDAT rowselectexpr.png](https://docs.derivative.ca/images/f/ff/SelectDAT_rowselectexpr.png)](https://docs.derivative.ca/File:SelectDAT_rowselectexpr.png)
By default, the [Python](Python.html "Python") expression is `re.match('.*',me.inputCell.val) != None`. `'.*'` means match any character multiple times, so this expression matches all values. If you want to match the parent's operator name followed by any numeric number you can use `parent().name+'[0-9]*'`, where `'[0-9]*'` matches any numerical string. `'.*'+parent().name+'.*'` will match any cell that contains the operator's parent name. You can check [Regular Expression Operations](https://docs.python.org/3.3/library/re.html) for additional information on how to use the Python Regular Expression module.

From Column `fromcol` - When selecting rows by values, this parameter selects which column to use when matching cell values to Selected Row Values to determine which rows are selected.
Select Cols `extractcols` - ⊞ - This parameter allows you to pick different ways of specifying the columns selected.
* All `all` - All columns selected.
* by Name `byname` - Columns selected using Start Col Name and End Col Name parameters.
* by Index `byindex` - Columns selected using Start Col Index and End Col Index parameters.
* by Start Name, End Index `bynameindex` - Columns selected using Start Col Name and End Col Index parameters.
* by Start Index, End Name `byindexname` - Columns selected using Start Col Index and End Col Name parameters.
* by Values `bynames` - Columns selected by specifying the column values explicitly.
* by Condition `byexpr` - Rows selected by an expression to be evaluated for the from row.
Start Col Name `colnamestart` - Specify the column name to start the selection range from.
Start Col Index `colindexstart` - Specify the column index to start the selection range from.
End Col Name `colnameend` - Specify the column name to end the selection range.
End Col Index `colindexend` - Specify the column index to end the selection range.
Col Select Values `colnames` - Specify actual column names that you want to select. You can use TouchDesigner's pattern matching (see wiki page [Pattern Matching](Pattern_Matching.html "Pattern Matching")), for example `colvalue[1-4]` will select all the columns named `colvalue1` thru `colvalue4`. Matching some characters like `'` need a `\` in front of it.
Col Select Condition `colexpr` - Specify an expression that will be evaluated. If the expression evaluates to true, the column will be selected. See Row Select Condition for more details.
From Row `fromrow` - When extracting columns by Specified Names, this parameter selects which row to use when matching cell values to Selected Col Values to determine which columns are selected.
Output `output` - ⊞ - Determines what format will be used for output from the DAT.
* Input Data `data` - Passes through data from first input without manipulation.
* Strings `string` - Evaluates input data as strings, including expanding any variable values to full strings.
* Expressions `expr` - Evaluates input data as expressions.
  

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
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Select DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • Select• [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

A text string that contains data (string, float, list, boolean, etc.) and operators (+ \* < etc) that are evaluated by the node's language (python or Tscript) and returns a string, float list or boolean, etc. Expressions are used in parameters, [DATs](DAT.html "DAT") and in scripts.

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=Select_DAT&oldid=27473>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")