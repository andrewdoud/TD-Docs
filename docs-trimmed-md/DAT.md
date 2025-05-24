

DAT - Derivative




# DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
  
[![OP DAT.png](images/thumb/c/c5/OP_DAT.png/1000px-OP_DAT.png)](File_OP_DAT.html)
See also [Category:DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)") for a full list of articles related to DATs.
**DATa Operators** (or **DATs**) are used to hold text data like strings, scripts, and XML. DATs either contain multiple lines of text as in a script, or a table of rows and columns of cells, each containing one string. You can edit the contents of the DAT directly in the [DAT Viewer](DAT_Viewer.html "DAT Viewer").
Access a DAT containing normal text using `op('text1').text`. Access a cell in a DAT containing a table using `op('table1')[1,2]` or by row/col names `op('table1')['rowname', 'colname']`.
**IMPORTANT**: `op('table1')[1,2]` is a python [cell object](Cell_Class.html "Cell Class") which usually gets converted for you to the string in the cell. More safely use `op('table1')[1,2].val` which always gives you the string.
## Sweet Sixteen DATs[[edit](https://docs.derivative.ca/index.php?title=DAT&action=edit&section=1 "Edit section: Sweet Sixteen DATs")]
The following 16 DATs are commonly used, we recommend familiarizing yourself with them.
| DAT | Purpose | Related DAT |
| --- | --- | --- |
| [Text](Text_DAT.html "Text DAT") | A place to edit and hold any text data. |  |
| [Table](Table_DAT.html "Table DAT") | Edit tables of text in rows and columns of "cells". | [Convert](Convert_DAT.html "Convert DAT") |
| [Merge](Merge_DAT.html "Merge DAT") | Merges tables or text DATs into one. | [Switch](Switch_DAT.html "Switch DAT") |
| [Select](Select_DAT.html "Select DAT") | Select specific columns or rows from a DAT. | [Substitute](Substitute_DAT.html "Substitute DAT") |
| [Reorder](Reorder_DAT.html "Reorder DAT") | Re-orders and repeats rows or columns in a DAT. | [Transpose](Transpose_DAT.html "Transpose DAT") |
| [Insert](Insert_DAT.html "Insert DAT") | Adds one row or column to a table filling with text in the new cells. |  |
| [Evaluate](Evaluate_DAT.html "Evaluate DAT") | Evaluates expressions in DATs. | [Script](Script_DAT.html "Script DAT") |
| [CHOP to](CHOP_to_DAT.html "CHOP to DAT") | Converts CHOP channels to DATs. | [SOP to](SOP_to_DAT.html "SOP to DAT") |
| [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") | Runs the DAT as a script when a CHOP changes. |  |
| [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") | Runs the DAT as a script when a [Panel](Panel.html "Panel") changes. |  |
| [DAT Execute](DAT_Execute_DAT.html "DAT Execute DAT") | Runs the DAT as a script when another DAT changes. | [Execute](Execute_DAT.html "Execute DAT") |
| [OSC In](OSC_In_DAT.html "OSC In DAT")/[UDP In](UDP_In_DAT.html "UDP In DAT") | Receive data from other applications via Open Sound Control. | [OSC Out](OSC_Out_DAT.html "OSC Out DAT")/[UDP Out](UDP_Out_DAT.html "UDP Out DAT") |
| [Web](Web_DAT.html "Web DAT") | Fetch a page on the internet based on a URL. | [XML](XML_DAT.html "XML DAT") |
| [Render Pick](Render_Pick_DAT.html "Render Pick DAT") | Use mouse to pick 3D objects and surfaces. | [Info](Info_DAT.html "Info DAT") |
| [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") | Receive input from Windows 7+ multi-touch devices. |  |
| [MIDI In](MIDI_In_DAT.html "MIDI In DAT") | Get MIDI controller and button data. | [Serial](Serial_DAT.html "Serial DAT") |
All DATs are documented in the [Category:DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)").
## DATs for Scripting[[edit](https://docs.derivative.ca/index.php?title=DAT&action=edit&section=2 "Edit section: DATs for Scripting")]
DATs can be linked together to select, re-arrange and evaluate data and expressions, making DATs a powerful **procedural scripting tool**.
DATs that contain scripts can be triggered by events like mouse clicks and any operation of gadgets in TouchDesigner control panels. DAT scripts can also be triggered by channel changes in CHOPs.
**Script Example**: This will create a button that plays a sound when you click it: Create a Button component (Tab -> COMP -> Button). Go inside it (Enter) and create an Audio Play CHOP (Tab -> CHOP -> Audio Play).Then create a Panel Execute DAT (Tab -> DAT -> Panel Execute) and make its [Viewer Active](Viewer_Active.html "Viewer Active"). Then click in its viewer and and change the `offToOn()` function to be:
```
def offToOn(panelValue):
     op('audioplay1').par.trigger.pulse()
     return
```
Click outside the node to end text entry. Go back up (u), make the button a Momentary button via its Button page and Button Type parameter. Then make the button [Viewer Active](Viewer_Active.html "Viewer Active"). Click on the viewer of the button. It should make a Notify sound.
You can also run a script in a Text DAT by using the "`run`" command from the textport or another DAT.
## DATs for Tables[[edit](https://docs.derivative.ca/index.php?title=DAT&action=edit&section=3 "Edit section: DATs for Tables")]
DAT tables are rows and columns of cells containing text strings.
The DAT whose name is [Table DAT](Table_DAT.html "Table DAT") is used to define new tables. To manually add, delete rows and columns of tables, press RMB over the table when [Viewer Active](Viewer_Active.html "Viewer Active") is on and select from the menu.
The tables are then manipulated by the [Select DAT](Select_DAT.html "Select DAT"), [Evaluate DAT](Evaluate_DAT.html "Evaluate DAT"), [Merge DAT](Merge_DAT.html "Merge DAT"), [Switch DAT](Switch_DAT.html "Switch DAT"), [Sort DAT](Sort_DAT.html "Sort DAT") and others.
You can use table DATs to export to parameters. See [DAT Export](DAT_Export.html "DAT Export").
DAT tables can be modified with the `tabcell` command.
Table cells are read with a `tab()`, `tabr()`, `tabc()` or `tabrc()` expression. See Help -> Commands and Expressions.
**Table Example**: This will create two TOP images with names in it: Create a Table DAT (Tab -> DAT -> Table). Make its [Viewer Active](Viewer_Active.html "Viewer Active"). Right-click on the viewer and select Add Column, and then Add Row, and again Add Row, which should give you 3 rows and 2 columns of empty cells (or put 2 and 3 in the parameters.)Click in the top left cell and type `name`, top right type `age`, and fill in the remaining cells with `joe`, `9`, `jane`, `21`.Now create a Text TOP (Tab -> TOP -> Text) and in its parameter called Text, type this expression to retrieve a cell from the table: ``tabc("table1", $OD, "name")``. You should see "joe" in the Text TOP viewer. Copy/paste the Text TOP (Ctrl-C, Ctrl-V). The new TOP should be called `text2` and its viewer should say "jane".That `tabc()` expression gets from the table, `table1`, the node you edited. It gets from the column called `name`. And the row is `$OD`, which is a variable you can use in any node that means "operator digits", the digits at the end of the operator name, which in this case is `1` and `2` for `text1` and `text2`.In the TOPs' expressions, you can replace `"name"` with `"age"`.
## DATs for manipulating Web and XML Data[[edit](https://docs.derivative.ca/index.php?title=DAT&action=edit&section=4 "Edit section: DATs for manipulating Web and XML Data")]
The [Web Client DAT](Web_Client_DAT.html "Web Client DAT") gets HTML or other data by passing a URL to the internet and receiving a response. The result and any XML data can be filtered with an [XML DAT](XML_DAT.html "XML DAT"), then further processed with the other DATs.
## DATs for Raw Text[[edit](https://docs.derivative.ca/index.php?title=DAT&action=edit&section=5 "Edit section: DATs for Raw Text")]
DATs can also be use to hold raw text which can then used by the [Text TOP](Text_TOP.html "Text TOP") and [Text SOP](Text_SOP.html "Text SOP") for use in compositing and 3D. They can also be used to leave comments your networks or for pop-up help messages for panel gadgets.
## Editing DATs[[edit](https://docs.derivative.ca/index.php?title=DAT&action=edit&section=6 "Edit section: Editing DATs")]
DATs can be edited directly in their viewers by turning on the [Viewer Active Flag](Viewer_Active_Flag.html "Viewer Active Flag").
You can also edit DATs in the [Textport](Textport.html "Textport") by right-clicking on a DAT and selecting **Edit Contents in Textport**.
Some DAT generators and most DAT filters can not be edited because their data is fed to them from their input. This is indicated in the viewer by a more muted text color compared to those DATs which can be edited. If you need to temporarily edit the contents of one of these DATs you can lock the DAT using the [Lock Flag](Lock_Flag.html "Lock Flag") and then edit it. However, these changes will be lost when the DAT is unlocked and locking it keeps it from [cooking](Cook.html "Cook"), so this is generally only useful for troubleshooting and debugging.
By default, text-type DATs display line numbers in the left margin area and table-type DATs display row and column numbers. The display of these numbers can be controlled in [Preferences](https://docs.derivative.ca/index.php?title=Preferences_Dialog&action=edit&redlink=1 "Preferences Dialog (page does not exist)").
## Editing DAT Text in an External Editor[[edit](https://docs.derivative.ca/index.php?title=DAT&action=edit&section=7 "Edit section: Editing DAT Text in an External Editor")]
In any DAT (or any parameter), if you right-click the DAT node and select **Edit Contents...** you will be editing the text in an external editor. Notepad is Windows default text editor.
To change the text editor to something else, like Notepad++, Vim, Sublime, etc. you need to change the Text Editor and Table Editor preference values. These preferences can be found in the Preferences dialog under the DATs page. Set their values to the path of the installed application executable (.exe) of the editor you want to use. For example, `C:/Program Files ..`.
Everyone has a favorite, have a look at Sublime Text 2.
To see how you set an environment variable, see [Variables](Variables.html "Variables").
## Using DATs[[edit](https://docs.derivative.ca/index.php?title=DAT&action=edit&section=8 "Edit section: Using DATs")]
* text data, text and table formats (tab delimited)
* use for scripts, commands, storage of values and arrays
* can be edited in the viewer, textport, or any external text editor
* Import: Text DAT, Table DAT, Web DAT
* Export: (right-click to save)
  

| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • DAT• [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

A set of commands located in a Text DAT that are triggered to run under certain conditions. There are two scripting languages in TouchDesigner: [Python](Python.html "Python") and the original [Tscript](Tscript.html "Tscript"). Scripts and single-line commands can also be run in the [Textport](Textport.html "Textport").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

A form of DATs (Data Operators) that is structured as rows and columns of text strings.

The dialog box in which commands and scripts can typed in manually. Output to the textport includes script errors and messages from `print()` and `debug()` calls in python code. You can also edit DATs in the textport.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

Retrieved from "<https://docs.derivative.ca/index.php?title=DAT&oldid=31530>"
[Categories](Special_Categories.html "Special:Categories"):
* [Touch Glossary](Category_Touch_Glossary.html "Category:Touch Glossary")
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")
* [Tscript](https://docs.derivative.ca/index.php?title=Category:Tscript&action=edit&redlink=1 "Category:Tscript (page does not exist)")