

OP Find DAT - TouchDesigner Documentation




# OP Find DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The OP Find DAT traverses the component hierarchy starting at one component and looking at all nodes within that component, and outputs a table with one row per node that matches criteria the user chooses. For example, the criteria could be all Ramp TOPs, or all nodes whose name starts with “`wave`”, or all nodes with the Clone parameter set to “`master1`”, or all Geometry components with a tag called “`emitter`”.
The criteria can limited to include only nodes of certain families, or certain operator types. It can filter on matching its path, certain parameters containing certain values (both constant and expressions), comments, tags, or the content of a DAT containing certain strings.
You can also cause the DAT to only look to some depth of the hierarchy from the specified component, such as 2 levels down, or limitless.
Criteria can be case-sensitive or not, but case-sensitive On or Off applies to all criteria in the OP Find DAT.
Furthermore you can exclude some nodes using more specialized criteria by returning a True of False in a callback contained in the attached callback DAT.
With the Combine Filters Menu (Any or All, Default is All), you can do an "or" or "and" on the pattern matching criterea.
It also takes an optional DAT containing a list of operators (eg, another OP Find DAT) which can be used to chain filters.
### Output Columns
There is a variety of columns that you can select from including `name`, `id`, `paths`, `type` and `tags`. (`id` is a member of the operator, which is an integer unique to the node, and doesn't change during the running of the TouchDesigner process.)
You can also output custom columns by defining the column names in the callback DAT, and filling in the column cells via another function in the callback DAT. For example, you can output a custom column which is the `tx` parameter value of the node.
You can control when the OP Find DAT cooks. Normally it cooks whenever any of the nodes in the specified hierarchy changes. Using the Active Cook menu parameter, you can also force-cook it every frame, or turn off cooking entirely. You can also click the Pulse parameter on Active Cook in order to force-cook it once, or do the equivalent using the node.cookpulse.pulse() python call.
Instead of being give the path to a component to start at, the OP Find DAT can take an input DAT containing a pre-generated list of paths to nodes to start from, and merge the results of each input line together in the output. To use this, the input DAT should contain the node “id” as the first column, which can be generated with another OP Find DAT with the Column called “ID” turned on.
For example, say you first list all components that are panels, then you separate into groups based on type or Clone parameter. The first OP Find DAT pre-filters a huge hierarchy to a small fraction of the nodes, the subsequent OP Find DATs are operating on simpler sets to eliminate a lot of checking and cooking.
Refer to Help -> [Operator Snippets](OP_Snippets.html "OP Snippets").
See also: [Script DAT](Script_DAT.html "Script DAT")
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[opfindDAT\_Class](https://docs.derivative.ca/OpfindDAT_Class "OpfindDAT Class")
## Contents
* [1 Summary](#Summary)
  + [1.1 Output Columns](#Output_Columns)
* [2 Parameters - Component Page](#Parameters_-_Component_Page)
* [3 Parameters - Families Page](#Parameters_-_Families_Page)
* [4 Parameters - Filters Page](#Parameters_-_Filters_Page)
* [5 Parameters - Columns Page](#Parameters_-_Columns_Page)
* [6 Parameters - Callbacks Page](#Parameters_-_Callbacks_Page)
* [7 Parameters - Common Page](#Parameters_-_Common_Page)
* [8 Operator Inputs](#Operator_Inputs)
  

## Parameters - Component Page
Active Cook `activecook` - ⊞ - Determines when to cook the DAT.
* Off `off` - This stops the operator from cooking altogether.
* Automatic `auto` - Only cook / update the contents when the results would change.
* Always `always` - Continually cook this operator repeatedly for update cases that might be missed.
* Incremental `incremental` - This will cook each frame, but only add one result per cook, until all results are added. At that point cooking stops.
Cook Pulse `cookpulse` - Manually force the OP Find DAT to update.
Component `component` - The path to the component where the search starts from.
Include Component `includecomponent` - Include the component the search starts from in the search itself.
Include Wire Hierarchy `includewired` - Any components wired to the starting component are included in the search.
Minimum Depth `mindepth` - Set a minmum depth for the sub-components the OP Find DAT should recursively search through.
Limit Max Depth `limitmaxdepth` - Turns on the Maximum Depth parameter to limit searching through sub-components. Turning this toggle off will search through all sub-networks.
Maximum Depth `maxdepth` - Set the maximum depth for the sub-components the OP Find DAT should recursively search through.
Limit Max Operators `limitmaxops` - Limit the total number of operators iterated in the search.
Maximum Operators `maxops` - Number of operators the search is limited to.
  

## Parameters - Families Page
The page of parameters determines which operator families are included in the search.
Object COMPs `objects` - Include Object COMPs, like Geo COMP, in the search.
Panel COMPs `panels` - Include Panel COMPs, like Container COMP, in the search.
Other COMPs `other` - Include other type COMPs, like Base COMP, in the search.
TOPs `tops` - Include DAT family operators in the search.
CHOPs `chops` - Include CHOP family operators in the search.
SOPs `sops` - Include SOP family operators in the search.
MATs `mats` - Include MAT family operators in the search.
DATs `dats` - Include DAT family operators in the search.
  

## Parameters - Filters Page
Case Sensitive `casesensitive` - Use case sensitivity in all pattern matching below.
Combine Filters `combinefilters` - ⊞ - Combine 'All', 'Any' or 'Custom' of the filters below to get a match. 'Custom' allows for specifying a subselection of filters with 'or' and 'and' keywords.
* All `all` - All filters must match for an operator to be included in the search result. (AND)
* Any `any` - Any of the filter conditions must be met for an operator to be included in the search result. (OR)
* Custom `custom` -
Custom Combine `customcombine` - Specify which filters to combine in the search.
Name `namefilter` - Use the operator's names like 'wave1', 'wave2', etc.
Type `typefilter` - Use names like `waveCHOP` and `panelexecuteDAT`. Look at the column Type to see the syntax.
Parent Shortcut `parentshortcutfilter` - Only match operators that include the here specified Parent Shortcut.
OP Shortcut `opshortcutfilter` - Only match operators that include the here specified OP Shortcut.
Path `pathfilter` - Specify a path that the operator should be located in.
Parent Path (relative) `parentfilter` - Specify a relative parent path that operators should be located in. This is a filter option on the `parentPath` column of this DAT that can be enabled by toggling the `Parent Path` parameter on this DAT's `Columns` page.
Exclude Path (relative) `excludefilter` - Specify a relative path that should be excluded from the search.
Wire Path `wirepathfilter` -
Comment `commentfilter` - Only match operators that include the here specified comment string.
Tags `tagsfilter` - Only match operators that match the here specified tags. Multiple tags can be searched for as a space seperated list.
DAT Text `textfilter` - Only include operators that - in the case of being from the DAT family - match specified string in their content.
Par Name `parnamefilter` - Only match operators with specified parameter name. Parameters must match ALL of name, value and expression to be included.
Par Value `parvaluefilter` - Only include operators that match specified parameter value. Parameters must match ALL of name, value and expression to be included.
Par Expression `parexpressionfilter` - Only include operators that match specified parameter expression string. Parameters must match ALL of name, value and expression to be included.
Par Non-Default Only `parnondefaultonly` - Only match with parameters that are non-default values.
  

## Parameters - Columns Page
Use Legacy Columns `legacycols` - Use only when expecting column headers to be named with legacy titles.
ID `idcol` - An integer that uniquely defines the node in this process. It's the same number for the duration of the process, but may be different when you run the process again.
Name `namecol` - Inlcude the name of the operator in the result table.
Type `typecol` - Include the operator type in the result table. For example `rampTOP`.
Parent Shortcut `parentshortcutcol` - Include the operator's Parent Shortcut in the result table.
OP Shortcut `opshortcutcol` - Include the operator's OP Shortcut in the result table.
Path `pathcol` - Include the operator's path in the result table.
Relative Path `relpathcol` - Include the operator's, relative to the search root, path in the result table.
Parent Path `parentpath` - Include the parent path.
Wire Path `wirepathcol` - Include the operator's wire path in the result table.
Depth `depthcol` - Include a column showing the relative depth to the root path of the found operator.
Cook Times `cooktimescol` - Include cook-time of found operators.
Tags `tagscol` - Include the operator's tags.
General Properties `genprop` - Include the operator's name, id, isCOMP, node position, node size and dock id in the result table.
CPU Time `cputime` - Include the operator's CPU cooktime in the result table.
GPU Time `gputime` - Include the operator's GPU cooktime in the result table.
CPU Memory `cpumem` - Include the operator's CPU memory in the result table.
GPU Memory `gpumem` - Include the operator's GPU memory in the result table.
Children `children` - Include the children of the operator in the result table.
  

## Parameters - Callbacks Page
Callbacks DAT `callbacks` - Path to a DAT containing callbacks for each event received. See [opfindDAT\_Class](https://docs.derivative.ca/OpfindDAT_Class "OpfindDAT Class") for usage.
Convert Bool to Int `convertbool` - For boolean logic values, the value will be '1' or '0'. When this parameter is Off, they will be 'True" or 'False'.
Convert None to Empty `convertnone` - For 'None' values, the value will be converted to Empty.
  

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
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • OP Find• [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

Cloning makes multiple components match the contents of a master component. A [Component](Component.html "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the [Replicator COMP](Replicator_COMP.html "Replicator COMP").

To re-compute the output data of the [Operators](Operator.html "Operator"). An operator cooks when (1) its inputs change, (2) its [Parameters](Parameter.html "Parameter") change, (3) when the timeline moves forward in some cases, or (4) [Scripting](Script.html "Script") commands are run on the node. When the operator is a [Panel Component](Panel_Component.html "Panel Component"), it also cooks when a user interacts with it. When an operator cooks, it usually causes operators connected to its output to re-cook. When TouchDesigner draws the screen, it re-cooks all the [Dependencies](Dependency.html "Dependency") - the necessary operators in all [Networks](Network.html "Network"), contributing to a frame's total "cook time".

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

The connection of an output of one node to the input of another node in a network. In contrast, see [Link](Link.html "Link").

Hierarchy relates components with other components. There are two groups of Hierarchy in TouchDesigner. 3D Object Components, and 2D Panel Components. Hierarchies let one component to be positioned relative to another. Each group can be connected via lines between the bottoms/tops of nodes in a network, or by placing one component inside the other.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

The Container component type is a [Panel Component](Panel_Component.html "Panel Component") that holds, lays out and displays any number of other Panel Components.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.

A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.

Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

A text string that contains data (string, float, list, boolean, etc.) and operators (+ \* < etc) that are evaluated by the node's language (python or Tscript) and returns a string, float list or boolean, etc. Expressions are used in parameters, [DATs](DAT.html "DAT") and in scripts.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

Retrieved from "<https://docs.derivative.ca/index.php?title=OP_Find_DAT&oldid=27897>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")