

Folder DAT - TouchDesigner Documentation





























# Folder DAT

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Folder DAT lists the files and subfolders found in a file system folder and monitors any changes.

For each item found, a row is created in the table with optional columns for the following information:

* Name
* Base Name
* Extension
* Type
* Size
* Depth
* Folder
* Path
* Relative Path
* Date Created
* Date Modified
* Date Accessed

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[folderDAT\_Class](https://docs.derivative.ca/FolderDAT_Class "FolderDAT Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Folder Page](#Parameters_-_Folder_Page)
* [3 Parameters - Columns Page](#Parameters_-_Columns_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Folder Page

Active `active` - When off, the DAT outputs a single-row table with only the headings, useful when dormant or when sending the DAT to a [Replicator COMP](Replicator_COMP.html "Replicator COMP").
Root Folder `rootfolder` - The folder in the filesystem whose contents will be displayed in the DAT list.
Refresh `refresh` - When on, it monitors the specified folder(s) of the filesystem.
Refresh Pulse `refreshpulse` - The pulse button reads the folder contents once.
Asynchronous Update `async` - When on, the update happens asynchronously from the main thread so it doesn't make TouchDesigner drop frames or pause. As a result, the Folder DAT way not update its data within the next frame after the change on disk.
Name Format `nameformat` - ⊞ - Select whether to include the filename extension or not.

* Include Extension `extension` -

* No Extension `noextension` -

Date Format `dateformat` - ⊞ - The format used to display the item's dates in the table.

* Standard `std` - A standard date format.

* Epoch `epoch` - A reference date format.

Type `type` - ⊞ - The types of contents to display.

* Files `files` - Include files.

* Folders `folders` - Include folders.

* Files and Folders `filesandfolders` - Include both files and folders.

Folders `folders` - Use [Pattern Matching](Pattern_Matching.html "Pattern Matching") to specify which folders are included. Matches the folder path. Delimiters used are spaces and commas. To match spaces, enclose the entire search term in double quotes.
Names `names` - Use [Pattern Matching](Pattern_Matching.html "Pattern Matching") to specify which names are included. Delimiters used are spaces and commas. To match spaces, enclose the entire search term in double quotes.
All Extensions `allextensions` - Includes all file extensions.
Image Extensions `imageextensions` - Includes image contents that are supported by TouchDesigner. See supported [File Types](File_Types.html "File Types").
Movie Extensions `movieextensions` - Includes movie contents that are supported by TouchDesigner. See supported [File Types](File_Types.html "File Types").
Audio Extensions `audioextensions` - Includes audio contents that are supported by TouchDesigner. See supported [File Types](File_Types.html "File Types").
Extensions `extensions` - Use [Pattern Matching](Pattern_Matching.html "Pattern Matching") to specify which extensions are included. Extensions listed here should not include the period. E.g \*txt, not \*.txt.
Include Subfolders `subfolders` - Includes the subfolders from the root folder specified.
Minumum Depth `mindepth` - Set a minmum depth for the subfolders the Folder DAT should recursively search through.
Limit Depth `limitdepth` - Turns on the Maximum Depth parameter to limit searching through subfolders. Turning this toggle off will search through all subtrees.
Maximum Depth `maxdepth` - Set the maximum depth for the subfolders the Folder DAT should recursively search through.

  


## Parameters - Columns Page

Name `namecol` - The name of the folder or file. In the case of a file this includes the extension. ie. `myfile.txt`
Base Name `basenamecol` - The name of the folder or file. In the case of a file this form does not includes the extension. ie. `myfile`
Extension `extensioncol` - The file extension of the file, blank for folders. ie. `txt`
Type `typecol` - The type of file as reported by the operating system.
Size `sizecol` - The size of the file in Bytes. Folders do not report any size.
Depth `depthcol` - How many folders deep the item is found from the Root Folder. Items on the Root Folder level have a depth of 0.
Folder `foldercol` - The path of the folder, or in the case of a file, the path of the folder the file is found in.
Path `pathcol` - The full path to the folder or file.
Relative Path `relpathcol` - The relative path to the folder or file from the Root Folder.
Date Created `datecreatedcol` - The date of creation.
Date Modified `datemodifiedcol` - The date of most recent modification.
Date Accessed `dateaccessedcol` - The date of most recent access or opening.

  


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

Extra Information for the Folder DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • Folder• [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |

A Folder in TouchDesigner always refers to a Windows or macOS operating system directory/folder system that contain files and other folders. It does not refer to operators within TouchDesigner. See [Network Path](Network_Path.html "Network Path").


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.


To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.


Any component can be extended with its own Python classes which contain python functions and data.


The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Folder_DAT&oldid=24296>"
[Category](Special_Categories.html "Special:Categories"):

* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")