

Table DAT - TouchDesigner Documentation





























# Table DAT

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

  


## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Table DAT lets you hand-edit or create a table of rows and columns of cells, each cell containing a text string. A "table" is one of the two forms of DATs (the other being simply lines of "free-form" text via the [Text DAT](Text_DAT.html "Text DAT")).

**Manually editing cells** - When a Table DAT has its [Viewer Active](Viewer_Active.html "Viewer Active") on, you can add rows and columns by right-clicking on row 0 or column 0 to add rows/columns, and typing text into any cell of its [node viewer](Node_Viewer.html "Node Viewer"). Use the Tab key to jump to the next cell, and the up/down arrow keys to navigate to adjacent cells.

**Procedurally filling cells** - You can conveniently create and fill rows and columns of a table. On the Fill page, the Fill Type menu gives 5 options: Manual, Set Size, Set Size and Contents, Fill by Column, and Fill by Row. When a Fill option is chosen, you can generate multiple rows/columns with specific headings using space-separated names or an expression, plus expressions to fill the cells.

You can use `me.subRow` and `me.subCol` (for sub-section being filled) in your expressions. See the popup menu on the Cell Expression parameter for suggestions.

Click the + below the parameters to you generate multiple sets of new cols or rows.

**Filling cells externally with python**  - If you are not auto-filling, you can put strings into table cells using something like `op('table1')[2,'select'] = 'yes'` in a python script elsewhere, or append rows using `.appendRow()` in python. See also the [Script DAT](Script_DAT.html "Script DAT") and its Snippets.

**Loading from external files** - The Table DAT can also can load a table from a `.csv`, `.txt` or `.dat` file on disk or on the web. Either drag-drop the file into a network, or use the File parameter.

Use `http://` when specifying a table on the internet.

If you drag the Table DAT to a desktop or folder, The DAT text will be converted into tab-delimited tables in a `.txt` file.

See also [Script DAT](Script_DAT.html "Script DAT"), [Text DAT](Text_DAT.html "Text DAT").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[tableDAT\_Class](TableDAT_Class.html "TableDAT Class")

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
Default Read Encoding `defaultreadencoding` - ⊞ - Sets the expected file encoding format, or auto-detects the format. UTF8, UTF16-LE, UTF16-BE, CP1252

* Auto Detect `manual` -

* UTF8 `utf8` -

* UTF16-LE `utf16le` -

* UTF16-BE `utf16be` -

* CP1252 `cp1252` -

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
Fills `fills` - Sequence of fill information for *Fill by Column* and *Fill by Row* Fill Types
Names `fills0names` - Space-separated names of one or more columns or rows. If it is an expression, each name can be the member of a python list, like `['heading1', 'heading2']`. This parameter is the start of a sequential block.
Cell Expression `fills0expr` - Expression used to fill each cell if the Fill Type is Fill by Row or Fill by Column. Can include expressions `me.subRow` and `me.subCol`.

  


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

Extra Information for the Table DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • Table• [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |

A form of [DATs](DAT.html "DAT") (Data Operators) that is structured as rows and columns of text strings.


A text string that contains data (string, float, list, boolean, etc.) and operators (+ \* < etc) that are evaluated by the node's language (python or Tscript) and returns a string, float list or boolean, etc. Expressions are used in parameters, [DATs](DAT.html "DAT") and in scripts.


[OP Snippets](OP_Snippets.html "OP Snippets") is a set of 700+ live examples of TouchDesigner operators. You can access snippets via the Help menu, or by right-clicking on network operators, or r-clicking on OP Create dialog items.


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. Tables are rows and columns of cells, each containing a text string.


The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Table_DAT&oldid=32309>"
[Categories](Special_Categories.html "Special:Categories"):

* [Touch Glossary](Category_Touch_Glossary.html "Category:Touch Glossary")
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")