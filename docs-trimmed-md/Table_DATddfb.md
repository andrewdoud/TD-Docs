

# Table_DATddfb

Table DAT - TouchDesigner Documentation





# Table DAT
From Derivative
Revision as of 02:21, 7 June 2023 by [Greg](https://docs.derivative.ca/User:Greg "User:Greg") ([talk](https://docs.derivative.ca/index.php?title=User_talk:Greg&action=edit&redlink=1 "User talk:Greg (page does not exist)") | [contribs](https://docs.derivative.ca/Special:Contributions/Greg "Special:Contributions/Greg"))([diff](https://docs.derivative.ca/index.php?title=Table_DAT&diff=prev&oldid=28902 "Table DAT")) [← Older revision](https://docs.derivative.ca/index.php?title=Table_DAT&direction=prev&oldid=28902 "Table DAT") | [Latest revision](https://docs.derivative.ca/Table_DAT "Table DAT") ([diff](https://docs.derivative.ca/index.php?title=Table_DAT&diff=cur&oldid=28902 "Table DAT")) | [Newer revision →](https://docs.derivative.ca/index.php?title=Table_DAT&direction=next&oldid=28902 "Table DAT") ([diff](https://docs.derivative.ca/index.php?title=Table_DAT&diff=next&oldid=28902 "Table DAT"))

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
  

## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Table DAT lets you hand-edit or create a table of rows and columns of cells, each cell containing a text string. A "table" is one of the two forms of DATs (the other being simply lines of "free-form" text via the [Text DAT](https://docs.derivative.ca/Text_DAT "Text DAT")).
**Manually editing cells** - When a Table DAT has its [Viewer Active](https://docs.derivative.ca/Viewer_Active "Viewer Active") on, you can add rows and columns by right-clicking on row 0 or column 0 to add rows/columns, and typing text into any cell of its [node viewer](https://docs.derivative.ca/Node_Viewer "Node Viewer"). Use the Tab key to jump to the next cell, and the up/down arrow keys to navigate to adjacent cells.
**Procedurally filling cells** - You can conveniently create and fill rows and columns of a table. On the Fill page, the Fill Type menu gives 5 options: Manual, Set Size, Set Size and Contents, Fill by Column, and Fill by Row. When a Fill option is chosen, you can generate multiple rows/columns with specific headings using space-separated names or an expression, plus expressions to fill the cells.
You can use `me.subRow` and `me.subCol` (for sub-section being filled) in your expressions. See the popup menu on the Cell Expression parameter for suggestions.
Click the + below the parameters to you generate multiple sets of new cols or rows.
**Filling cells externally with python**  - If you are not auto-filling, you can put strings into table cells using something like `op('table1')[2,'select'] = 'yes'` in a python script elsewhere, or append rows using `.appendRow()` in python. See also the [Script DAT](https://docs.derivative.ca/Script_DAT "Script DAT") and its Snippets.
**Loading from external files** - The Table DAT can also can load a table from a `.csv`, `.txt` or `.dat` file on disk or on the web. Either drag-drop the file into a network, or use the File parameter.
Use `http://` when specifying a table on the internet.
If you drag the Table DAT to a desktop or folder, The DAT text will be converted into tab-delimited tables in a `.txt` file.
See also [Script DAT](https://docs.derivative.ca/Script_DAT "Script DAT"), [Text DAT](https://docs.derivative.ca/Text_DAT "Text DAT").
[![PythonIcon.png](https://docs.derivative.ca/images/c/c2/PythonIcon.png)](https://docs.derivative.ca/File:PythonIcon.png)[tableDAT\_Class](https://docs.derivative.ca/TableDAT_Class "TableDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Table Page](#Parameters_-_Table_Page)
* [3 Parameters - Fill Page](#Parameters_-_Fill_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Table Page
Edit.. `edit` - Clicking this opens a text editor to add/edit/delete text from the DAT.
File `file` - The filesystem path and name of the file to load. Accepts `.txt` and `.dat` files.
Sync to File `syncfile` - When On, loads the file from disk into the DAT when the projects starts. A filename must be specified. Turning on the option will load the file from disk immediately. If the file does not exist, it will be created the first time the DAT is updated. The file is monitored so that any changes made to the file will update the DAT, and any changes made to the DAT will be written to the file right away. If the file is removed, the DAT will retain its current contents.
Default Read Encoding `defaultreadencoding` - Sets the expected file encoding format, or auto-detects the format. UTF-8, UTF16-LE, UTF16-BE, CP1252
Load on Start `loadonstart` - When On, reloads the file from disk into the DAT when the projects starts.
Write on Toe Save `write` - When On, writes the contents of the DAT out to the file on disk when the project is saved.
Remove Blank Lines `removeblank` - When enabled, do not convert blank lines into empty rows when loading files.
  

## Parameters - Fill Page
Fill Type `fill` - ⊞ - You can create and fill rows and columns of a table. Fill Type menu gives 5 options: Manual, Set Size, Set Size and Contents, Fill by Column, and Fill by Row. When a Fill option is chosen, you can generate multiple rows/columns with specific headings using space-separated names or an expression, plus expressions to fill the cells.
* Manual `manual` - Rows and Columns will be added manually by user.
  

* Set Size `setsize` - The size will be set by the Rows and Columns parameters, but the cells will not be filled in.
* Set Size and Contents `setsizeandcontents` - The size will be set by the Rows and Columns parameters, and the cells will be filled based on the Cell Expression.
* Fill by Column `fillbycol` - The number of rows will be set by the Rows parameter, and the content of the columns will be defined by the Names 0 and Cell Expression 0 parameters.
* Fill by Row `fillbyrow` - The number of columns will be set by the Columns parameter, and the content of the rows will be defined by the Names 0 and Cell Expression 0 parameters.
Rows `rows` - Defines the number of rows in the table, where applicable.
Columns `cols` - Defines the number of columns in the table, where applicable.
Cell Expression `cellexpr` - Expression used to fill each cell if the Fill Type is Set Size and Contents. Can include expressions `me.subRow` and `me.subCol`
Include Names `includenames` - Creates an extra row at the top, or a column at the left for the names of the columns or rows, filled with the Include Names parameter.
Names 0 `cellexpr` - Space-separated names of one or more columns or rows. If it is an expression, each name can be the member of a python list, like `['heading1', 'heading2']`. This parameter is the start of a sequential block.
Cell Expression 0 `cellexpr` - Expression used to fill each cell if the Fill Type is Fill by Row or Fill by Column. Can include expressions `me.subRow` and `me.subCol`.
  

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
Extra Information for the Table DAT can be accessed via an [Info CHOP](https://docs.derivative.ca/Info_CHOP "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2021.100002018.28070before 2018.28070
| DATs |
| --- |
| [Art-Net](https://docs.derivative.ca/Art-Net_DAT "Art-Net DAT") • [Audio Devices](https://docs.derivative.ca/Audio_Devices_DAT "Audio Devices DAT") • [CHOP Execute](https://docs.derivative.ca/CHOP_Execute_DAT "CHOP Execute DAT") • [CHOP to](https://docs.derivative.ca/CHOP_to_DAT "CHOP to DAT") • [Clip](https://docs.derivative.ca/Clip_DAT "Clip DAT") • [Convert](https://docs.derivative.ca/Convert_DAT "Convert DAT") • [CPlusPlus](https://docs.derivative.ca/CPlusPlus_DAT "CPlusPlus DAT") • [DAT](https://docs.derivative.ca/DAT "DAT") • [Experimental:DAT](https://docs.derivative.ca/Experimental:DAT "Experimental:DAT") •  [Execute](https://docs.derivative.ca/DAT_Execute_DAT "DAT Execute DAT") • [DAT Export](https://docs.derivative.ca/DAT_Export "DAT Export") • [Error](https://docs.derivative.ca/Error_DAT "Error DAT") • [EtherDream](https://docs.derivative.ca/EtherDream_DAT "EtherDream DAT") • [Evaluate](https://docs.derivative.ca/Evaluate_DAT "Evaluate DAT") • [Examine](https://docs.derivative.ca/Examine_DAT "Examine DAT") • [Execute](https://docs.derivative.ca/Execute_DAT "Execute DAT") • [FIFO](https://docs.derivative.ca/FIFO_DAT "FIFO DAT") • [File In](https://docs.derivative.ca/File_In_DAT "File In DAT") • [File Out](https://docs.derivative.ca/File_Out_DAT "File Out DAT") • [Folder](https://docs.derivative.ca/Folder_DAT "Folder DAT") • [In](https://docs.derivative.ca/In_DAT "In DAT") • [Indices](https://docs.derivative.ca/Indices_DAT "Indices DAT") • [Info](https://docs.derivative.ca/Info_DAT "Info DAT") • [Insert](https://docs.derivative.ca/Insert_DAT "Insert DAT") • [JSON](https://docs.derivative.ca/JSON_DAT "JSON DAT") • [Keyboard In](https://docs.derivative.ca/Keyboard_In_DAT "Keyboard In DAT") • [Lookup](https://docs.derivative.ca/Lookup_DAT "Lookup DAT") • [Media File Info](https://docs.derivative.ca/Media_File_Info_DAT "Media File Info DAT") • [Merge](https://docs.derivative.ca/Merge_DAT "Merge DAT") • [MIDI Event](https://docs.derivative.ca/MIDI_Event_DAT "MIDI Event DAT") • [MIDI In](https://docs.derivative.ca/MIDI_In_DAT "MIDI In DAT") • [Monitors](https://docs.derivative.ca/Monitors_DAT "Monitors DAT") • [MPCDI](https://docs.derivative.ca/MPCDI_DAT "MPCDI DAT") • [MQTT Client](https://docs.derivative.ca/MQTT_Client_DAT "MQTT Client DAT") • [Multi Touch In](https://docs.derivative.ca/Multi_Touch_In_DAT "Multi Touch In DAT") • [NDI](https://docs.derivative.ca/NDI_DAT "NDI DAT") • [Null](https://docs.derivative.ca/Null_DAT "Null DAT") • [OP Execute](https://docs.derivative.ca/OP_Execute_DAT "OP Execute DAT") • [OP Find](https://docs.derivative.ca/OP_Find_DAT "OP Find DAT") • [OSC In](https://docs.derivative.ca/OSC_In_DAT "OSC In DAT") • [OSC Out](https://docs.derivative.ca/OSC_Out_DAT "OSC Out DAT") • [Out](https://docs.derivative.ca/Out_DAT "Out DAT") • [Panel Execute](https://docs.derivative.ca/Panel_Execute_DAT "Panel Execute DAT") • [Parameter](https://docs.derivative.ca/Parameter_DAT "Parameter DAT") • [Parameter Execute](https://docs.derivative.ca/Parameter_Execute_DAT "Parameter Execute DAT") • [ParGroup Execute](https://docs.derivative.ca/ParGroup_Execute_DAT "ParGroup Execute DAT") • [Perform](https://docs.derivative.ca/Perform_DAT "Perform DAT") • [Experimental:POP to](https://docs.derivative.ca/Experimental:POP_to_DAT "Experimental:POP to DAT") • [Render Pick](https://docs.derivative.ca/Render_Pick_DAT "Render Pick DAT") • [Reorder](https://docs.derivative.ca/Reorder_DAT "Reorder DAT") • [Script](https://docs.derivative.ca/Script_DAT "Script DAT") • [Select](https://docs.derivative.ca/Select_DAT "Select DAT") • [Serial](https://docs.derivative.ca/Serial_DAT "Serial DAT") • [Experimental:Serial Devices](https://docs.derivative.ca/Experimental:Serial_Devices_DAT "Experimental:Serial Devices DAT") • [SocketIO](https://docs.derivative.ca/SocketIO_DAT "SocketIO DAT") • [SOP to](https://docs.derivative.ca/SOP_to_DAT "SOP to DAT") • [Sort](https://docs.derivative.ca/Sort_DAT "Sort DAT") • [Substitute](https://docs.derivative.ca/Substitute_DAT "Substitute DAT") • [Switch](https://docs.derivative.ca/Switch_DAT "Switch DAT") • Table• [TCP/IP](https://docs.derivative.ca/TCP/IP_DAT "TCP/IP DAT") • [Text](https://docs.derivative.ca/Text_DAT "Text DAT") • [Touch In](https://docs.derivative.ca/Touch_In_DAT "Touch In DAT") • [Touch Out](https://docs.derivative.ca/Touch_Out_DAT "Touch Out DAT") • [Transpose](https://docs.derivative.ca/Transpose_DAT "Transpose DAT") • [TUIO In](https://docs.derivative.ca/TUIO_In_DAT "TUIO In DAT") • [UDP In](https://docs.derivative.ca/UDP_In_DAT "UDP In DAT") • [UDP Out](https://docs.derivative.ca/UDP_Out_DAT "UDP Out DAT") • [UDT In](https://docs.derivative.ca/UDT_In_DAT "UDT In DAT") • [UDT Out](https://docs.derivative.ca/UDT_Out_DAT "UDT Out DAT") • [Video Devices](https://docs.derivative.ca/Video_Devices_DAT "Video Devices DAT") • [Web Client](https://docs.derivative.ca/Web_Client_DAT "Web Client DAT") • [Web](https://docs.derivative.ca/Web_DAT "Web DAT") • [Web Server](https://docs.derivative.ca/Web_Server_DAT "Web Server DAT") • [WebRTC](https://docs.derivative.ca/WebRTC_DAT "WebRTC DAT") • [WebSocket](https://docs.derivative.ca/WebSocket_DAT "WebSocket DAT") • [XML](https://docs.derivative.ca/XML_DAT "XML DAT") |
A form of [DATs](https://docs.derivative.ca/DAT "DAT") (Data Operators) that is structured as rows and columns of text strings.

A text string that contains data (string, float, list, boolean, etc.) and operators (+ \* < etc) that are evaluated by the node's language (python or Tscript) and returns a string, float list or boolean, etc. Expressions are used in parameters, [DATs](https://docs.derivative.ca/DAT "DAT") and in scripts.

[OP Snippets](https://docs.derivative.ca/OP_Snippets "OP Snippets") is a set of 700+ live examples of TouchDesigner operators. You can access snippets via the Help menu, or by right-clicking on network operators, or r-clicking on OP Create dialog items.

An [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](https://docs.derivative.ca/Script "Script") or [GLSL](https://docs.derivative.ca/GLSL "GLSL") Shader, but can be any multi-line text. Tables are rows and columns of cells, each containing a text string.

The generic thing that holds an [Operator](https://docs.derivative.ca/Operator "Operator"), and includes [Flags](https://docs.derivative.ca/Flag "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

An [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") which operate on [Channels](https://docs.derivative.ca/Channel "Channel") (a sequence of numbers ([Samples](https://docs.derivative.ca/Sample "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=Table_DAT&oldid=28902>"
[Categories](https://docs.derivative.ca/Special:Categories "Special:Categories"):
* [Touch Glossary](https://docs.derivative.ca/Category:Touch_Glossary "Category:Touch Glossary")
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")