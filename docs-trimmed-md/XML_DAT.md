

XML DAT - TouchDesigner Documentation





























# XML DAT

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The XML DAT can be used to parse arbitrary XML and SGML/HTML formatted data. Once formatted, selected sections of the text can be output for further processing.

One approach to parsing with the XML DAT is to read the XML with a Text DAT or a Web DAT, and pass that to a default XML DAT. Then you start to refine your selection by changing the match-all pattern (the "\*"), to strings that reduce the elements that are in the output.

### XML and HTML Background

XML and HTML data consists of a tree like structure consisting of elements. Each element can be either tagged or contain arbitrary text. Elements may be nested. Tagged elements begin with an opening section and usually are terminated with a closing section.

Example:

```
 <greeting a="1" b="2" c="3"> Hello there. </greeting>			

```

In the example above are two elements. The first is a **tag** element named *greeting* with attributes *a, b* and *c*. The second element is a **text** element consisting of "*Hello there.*"

### XML DAT Operation

The XML DAT begins by parsing its input, creating an internal tree of elements.

The **Element Scope** parameters are then used to filter out unwanted elements. The remaining elements are then used to create the output. The format of the output is determined by the **Format** parameters. The **Output** parameters can then be used to futher limit the information displayed for each scoped element.

Each parsed element contains a number of details:

**Label** - Each element is given an arbitrary label named n0, n1, n2 etc. All elements are children of the reserved element labelled 'root'.

**Type** - Elements are mainly of type 'tag' or 'text', though tag types can be further classified into 'doctype', 'declaration', 'comment' or 'entity'.

**Text** - The text of an element refers to the tag attribute of an element, or the arbitrary text contents. In the above example, the first element would be of type 'tag' and contain text of 'greeting'. The second element would be of type 'text' and contain text of 'Hello there.'

**Level** - This describes how deeply nested an element is. For example the single root element always has a level of 0.

**Parent** - Each element contains one parent. The root element does not have a parent.

**Children** - Each element can have an arbitrary number of children elements.

**Attributes** - Each tagged element can have an arbitrary number of attributes. Each attribute consists of a name and a value. In the above example, the greeting tag would contain 3 attributes (with names a, b and c and values 1, 2, and 3 respectively).

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[xmlDAT\_Class](https://docs.derivative.ca/XmlDAT_Class "XmlDAT Class")

## Contents

* [1 Summary](#Summary)
  + [1.1 XML and HTML Background](#XML_and_HTML_Background)
  + [1.2 XML DAT Operation](#XML_DAT_Operation)
* [2 Parameters - Format Page](#Parameters_-_Format_Page)
* [3 Parameters - Element Scope Page](#Parameters_-_Element_Scope_Page)
* [4 Parameters - Output Page](#Parameters_-_Output_Page)
* [5 Parameters - Common Page](#Parameters_-_Common_Page)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Format Page

Parse SGML/HTML `sgml` - If enabled, the input should be in SGML/HTML format. This includes form data. If disabled, XML format is assumed.
Merge `merge` - ⊞ - Merge and label can be used to combine two inputs of data. The second input must be XML formatted, and not SGML/HTML. These two parameters control where and how the second input is merged.

* Before Element `before` - The second input is merged before the specified element label.

* After Element `after` - The second input is merged after the specified element label.

* Inside Element `inside` - The second input is merged as a child of the specified element label.

* Replace Element `replace` - The second input replaces the specified element label.

Label `mlabel` - Specify the element at which the merge occurs.

  


## Parameters - Element Scope Page

This section of parameters controls which elements are selected for output. By default all elements are selected.

Label `label` - Element labels must match this parameter.
Type `type` - Element types must match this parameter.
Text `text` - Element text must match this parameter.
Name `name` - If an element contains attributes, at least one must have a name matching this parameter.
Value `value` - If an element contains attributes, at least one must have a value matching this parameter.
Parent Label `plabel` - Elements must have a parent whose label matches this parameter.
Parent Type `ptype` - Elements must have a parent whose type matches this parameter.
Parent Text `ptext` - Elements must have a parent whose text matches this parameter.
Parent Name `pname` - Elements must have a parent with an attribute whose name matches this parameter.
Parent Value `pvalue` - Elements must have a parent with an attribute whose value matches this parameter.

  


## Parameters - Output Page

Once a selection of elements have been selected for output, its output can be further refined.

Name Attributes `oaname` - Only output attributes whos name match this parameter.
Value Attributes `oavalue` - Only output attributes whose value match this parameter.
Children Labels `oclabel` - Only output children whose label match this parameter.
Show `show` - ⊞ - This controls how the selected elements are presented.

* Summary Table `sumtable` -

* Summary Tree `sumtree` - This output selection is similar to the summary table, except it outputs an indented ascii representation of the tree. It can be used to quickly identify areas of interest while picking appropriate parameters.

* XML `xml` - This outputs an XML compliant tree of the selected elements. It can then be fed into another XML DAT for further processing.

* Attributes per Row `attribs` - This outputs a table of all attributes for the selected elements. Each element attribute is output on a separate row.

* Attributes per Column `attribscol` - This outputs a table of all attributes for the selected elements. Each element is output in output on a single row, where each column represents one attribute.

* Children `children` - This outputs a table of all children for the selected elements.

* Text `text` - This outputs all text contents from all elements of type 'text'.

Label Prefix `lprefix` - This determines whether or not the element label is prefixed when outputting tables or attributes or children.

  


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
* Input 1:  -

  


## Info CHOP Channels

Extra Information for the XML DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • XML |

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.


There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").


Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.


The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=XML_DAT&oldid=27185>"
[Category](Special_Categories.html "Special:Categories"):

* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")