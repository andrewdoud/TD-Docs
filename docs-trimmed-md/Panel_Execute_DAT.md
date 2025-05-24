

TouchDesigner Documentation





























# Panel Execute DAT

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Panel Execute DAT will run its script when the [Panel Values](Panel_Value.html "Panel Value") of a specified panel component changes. You can specify which panel values to monitor, and trigger scripts based on their values changing in various ways.

Panel Execute DATs are created with [default python method](https://docs.derivative.ca/PanelexecuteDAT_Class "PanelexecuteDAT Class") placeholders. For each monitored condition in the parameters, there is a matching python method in the DAT. When a condition is turned on in the parameters, each time that condition is satisfied the corresponding python method will be executed.

In the template Python script, `panelValue` is passed to each method, and you can query each call by printing `panelValue.name` and `panelValue.val`. See [PanelValue Class](PanelValue_Class.html "PanelValue Class").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[panelexecuteDAT\_Class](https://docs.derivative.ca/PanelexecuteDAT_Class "PanelexecuteDAT Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Panel Execute Page](#Parameters_-_Panel_Execute_Page)
* [3 Parameters - File Page](#Parameters_-_File_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Panel Execute Page

Active `active` - While on, the DAT will respond to the Panel that is referenced.
Execute from `executeloc` - ⊞ - ([Tscript](Operator_Language.html "Operator Language") only) Determines the location the script is run from.

* Current Node `current` - ([Tscript](Operator_Language.html "Operator Language") only) The script is executed from the current node location.

* This Node `here` - The script is executed from the parent of the DAT. The DAT executes from the parent to make siblings of the DAT easy to access: DAT scripts used to execute from inside the DAT.

* Specified Operator `op` - The script is executed from the operator specified in the From Operator parameter below.

From Operator `fromop` - The path that the script will be executed from if the Execute From parameter is set to *Specified Operator*.
Panels `panels` - Select which [Panel COMPs](Panel_Component.html "Panel Component") to monitor for changes.
Panel Value `panelvalue` - The [Panel Value](Panel_Value.html "Panel Value")(s) that is monitored to trigger the execution of the script.

Scripts will execute based on a combination of the five trigger events listed below. The script is executed once per trigger (except for While On/While Off cases). Each event will only cause one trigger to go off (i.e. if both Off to On and On Value Change are checked, one event will be fired with Off to On as the trigger). Logic for the 'on' state is *greater than zero*.



Off to On `offtoon` - The onOffToOn() method executes when the panel value specified switches from off to on, called at the first "on" frame.
While On `whileon` - The whileOn() method executes when the panel value specified is on. It is called once each frame.
On to Off `ontooff` - The onOnToOff() method executes when the panel value specified switches from on to off, called at the first "off" frame.
While Off `whileoff` - The whileOff() method executes when the panel value specified is off. It is called once each frame.
Value Change `valuechange` - The onValueChange() method executes when the panel value specified changes value in any way. It is called once each frame.
Edit.. `edit` - Clicking this opens a text editor to edit text in the DAT.

  


## Parameters - File Page

File `file` - The filesystem path and name of the file to load. Accepts `.txt` and `.dat` files.
Sync to File `syncfile` - When On, loads the file from disk into the DAT when the projects starts. A filename must be specified. Turning on the option will load the file from disk immediately. If the file does not exist, it will be created the first time the DAT is updated. The file is monitored so that any changes made to the file will update the DAT, and any changes made to the DAT will be written to the file right away. If the file is removed, the DAT will retain its current contents.
Load on Start `loadonstart` - When On, reloads the file from disk into the DAT when the projects starts.
Load File `loadonstartpulse` - Instantly reloads the file.
Write on Toe Save `write` - When On, writes the contents of the DAT out to the file on disk when the project is saved.
Write File `writepulse` - Instantly write the file to disk.

  


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

  


## Info CHOP Channels

Extra Information for the Panel Execute DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\n2022.241402021.100002018.28070before 2018.28070

| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • Panel Execute• [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


The internal states of a panel component are Panel Values, and are accessed with a Panel CHOP, a `OP.panel` Python expression, or a Panel Execute DAT.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Panel_Execute_DAT&oldid=27278>"
[Category](Special_Categories.html "Special:Categories"):

* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")