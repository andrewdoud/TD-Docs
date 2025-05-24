

# Replicator_COMP

Replicator COMP - TouchDesigner Documentation




# Replicator COMP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
  

## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Replicator COMP creates copies of a component, one for every row in a table or using a Number of Replicants parameter - it is the "for-loop" of operators. Unlike [Clone](Clone.html "Clone"), it automatically creates copies of a master component.
It creates replicant nodes ("[replicants](http://en.wikipedia.org/wiki/Replicant)") and deletes them as the table changes or the replicant count changes. The replicant master can be a full component and its contents or a single node.
It takes the node specified in the Master Node parameter, and makes a copy of the master for every row in the Template Table (or specified by the Number of Replicant parameter).
The nodes that are created can be named in two ways. Copies can be named/numbered sequentially using
the prefix specified by the Node Prefix parameter: `item1`, `item2`, ... Alternately, copies can be named based on the string in a column of the table, specified with the Name from Table parameter.
[![Replicator.1.png](images/thumb/d/d4/Replicator.1.png/700px-Replicator.1.png)](File_Replicator.1.html)
If you want to create a node for the first row of the table, un-set the Ignore First Row parameter.
The replicants get laid out in a grid in the network, determined by the Layout and Layout Origin parameters.
The Replicator does not assume or require that the master and replicants are components – they can all be Movie File In TOPs if you want. It also does not assume or require that the replicants are [Clones](Clone.html "Clone"). However the Master Node can be a component whose [Clone](Clone.html "Clone") parameter is set to itself, so that all nodes created are clones of the master.
For every replicant, you can run a script in the callback DAT where you can see some examples of typical cases that you can adapt. Here are some others:
* change the expression of a [parameter](Par_Class.html "Par Class"): `c.par.display.expr = "op('thing')[op.digits, 'display']"`
* Change the parameter expression mode: `c.par.display.mode = ParMode.EXPRESSION` The mode is one of: `ParMode.CONSTANT`, `ParMode.EXPRESSION`, or `ParMode.EXPORT`.
If only one line of a table changes, the other existing replicants are not changed or re-created. In the callback DAT, removing `onRemoveReplicant()` will keep the replicants around to be re-used when the table grows again.
This is an extremely powerful node type. Examples: (1) A button gadget for each row of the table. a geometry component, which is replicated at every point of a 3D particle system, each behaving separately. (2) You can feed the table of a [Multi Touch In DAT](Multi_Touch_In_DAT.html "Multi Touch In DAT") directly to the Replicator to create something at each fingertip.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[replicatorCOMP\_Class](ReplicatorCOMP_Class.html "ReplicatorCOMP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Replicator Page](#Parameters_-_Replicator_Page)
* [3 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common COMP Info Channels](#Common_COMP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Replicator Page
Replication Method `method` - ⊞ - Choose between using a Template DAT Table where each row will create a replicant or using the Number of Replicants parameter below to set how many replications to make.
* By Number `bynum` -
* By Table `bytable` -
Number of Replicants `numreplicants` - Set number of replicants when using Replication Method = By Number above.
Template DAT Table `template` - Path to the table DAT that will drive the replicating.
Name from Table `namefromtable` - ⊞ - How the node names will be generated.
* Row Index `rowindex` - Uses the Node Prefix parameter followed by the row number. The default creates nodes named `item1`, `item2`, `item3` .... (The top row is 0).
* Column by Index `colbyindex` - The node name is in the column specified by a column number.
* Column by Name `colbyname` - The node name is in a column specified by a column name in the first row.
Ignore First Row `ignorefirstrow` - Do not create a node for the first row.
Column Name `colname` - Name at the top of the column.
Column Index `colindex` - Column number, starting from 0.
Operator Prefix `opprefix` - Add this prefix to all nodes.
Master Operator `master` - Which node or component to replicate.
Destination `destination` - Where to put the replicant nodes. If the location is `..`, it puts the nodes inside the parent, which is actually alongside the Replicator component. If you put `.`, it will put it inside itself, that is, inside the Replicator component. If left blank, it will error.
Maximum Operators `domaxops` - Enable the parameter below to set a maximum number of allowed replicants.
Maximum Operators `maxops` - Max number of nodes replicated.
Script `tscript` - Tscript only (use callback DAT in python): For every replicant, you can run a script to customize it relative to the master, such as setting the Display or Clone parameters, or a Render flag. Replicator runs the script command to customize each replicant versus the master. `me.curItem` can be used here to access the current item and make changes to it. Select one of the 3 entries in the drop menu to the right for some examples.
If you are using [Tscript](Tscript.html "Tscript"), some local variables are defined:
* $ITEM Name of current node being replicated.
* $MASTER Name of master node.
* $LOCATION Name of the location component.
The most common need is for the master to not display, and the replicants to display. For Panel components it is most commonly "`opparm $ITEM paneldisplay ( 1 )`", and for Geometry components it is most commonly "`opset -d on $ITEM`". Use the popup menu for some common scripts.

Script Names `scriptmenu` - Select from some commonly used scripts (Tscript) in this menu.
Callbacks DAT `callbacks` - Path to a DAT containing callbacks for each event received. See [replicatorCOMP\_Class](ReplicatorCOMP_Class.html "ReplicatorCOMP Class") for usage.
Layout `layout` - ⊞ - How to lay out the new nodes - all in one place (Off), horizontally, vertically, or in a grid.
* Off `off` -
* Horizontal `horizontal` -
* Vertical `vertical` -
* Grid `grid` -
Layout Origin `layoutorigin` - ⊞ - Where to lay out the new nodes, giving the XY location of the top-left node's bottom-left corner.
* `layoutorigin1` -
* `layoutorigin2` -
Incremental Update `doincremental` - Enables the parameter below for incremental creation of replicants.
Incremental Update `increment` - Staggers the replication of operators to avoid large frame drops when creating replicants. It will create the specified number of replicants per frame at most, by default 1 per frame, if Incremental Update is on.
Recreate All Operators `recreateall` - Deletes all nodes it has created, then re-creates them using the template and its current parameters.
Recreate Missing Operators `recreatemissing` - Re-creates missing operators from the template table but does not delete and re-create already existing replicants.
  

## Parameters - Extensions Page
The Extensions parameter page sets the component's python extensions. Please see [extensions](Extensions.html "Extensions") for more information.
Extension `ext` - Sequence of info for creating extensions on this component
Object `ext0object` - A number of class instances that can be attached to the component.
Name `ext0name` - Optional name to search by, instead of the instance class name.
Promote `ext0promote` - Controls whether or not the extensions are visible directly at the component level, or must be accessed through the `.ext` member. Example: `n.Somefunction` vs `n.ext.Somefunction`

Re-Init Extensions `reinitextensions` - Recompile all extension objects. Normally extension objects are compiled only when they are referenced and their definitions have changed.
  

## Parameters - Common Page
The Common parameter page sets the component's [node viewer](Node_Viewer.html "Node Viewer") and [clone](Clone.html "Clone") relationships.
Parent Shortcut `parentshortcut` - Specifies a name you can use anywhere inside the component as the path to that component. See [Parent Shortcut](Parent_Shortcut.html "Parent Shortcut").
Global OP Shortcut `opshortcut` - Specifies a name you can use anywhere at all as the path to that component. See [Global OP Shortcut](Global_OP_Shortcut.html "Global OP Shortcut").
Internal OP `iop` - Sequence header for internal operators.
Shortcut `iop0shortcut` - Specifies a name you can use anywhere inside the component as a path to "Internal OP" below. See [Internal Operators](Internal_Operators.html "Internal Operators").
OP `iop0op` - The path to the Internal OP inside this component. See [Internal Operators](Internal_Operators.html "Internal Operators").

Operator Viewer `opviewer` - Select which operator's node viewer to use when the Node View parameter above is set to Operator Viewer.
Enable Cloning `enablecloning` - Control if the OP should be actively cloneing. Turning this off causes this node to stop cloning it's 'Clone Master'.
Enable Cloning Pulse `enablecloningpulse` - Instantaneously clone the contents.
Clone Master `clone` - Path to a component used as the Master [Clone](Clone.html "Clone").
Load on Demand `loadondemand` - Loads the component into memory only when required. Good to use for components that are not always used in the project.
Enable External .tox `enableexternaltox` - When on (default), the external .tox file will be loaded when the .toe starts and the contents of the COMP will match that of the external .tox. This can be turned off to avoid loading from the referenced external .tox on startup if desired (the contents of the COMP are instead loaded from the .toe file). Useful if you wish to have a COMP reference an external .tox but not always load from it unless you specifically push the Re-Init Network parameter button.
Enable External .tox Pulse `enableexternaltoxpulse` - This button will re-load from the external `.tox` file (if present).
External .tox Path `externaltox` - Path to a `.tox` file on disk which will source the component's contents upon start of a `.toe`. This allows for components to contain networks that can be updated independently. If the `.tox` file can not be found, whatever the `.toe` file was saved with will be loaded.
Reload Custom Parameters `reloadcustom` - When this checkbox is enabled, the values of the component's [Custom Parameters](Custom_Parameters.html "Custom Parameters") are reloaded when the [.tox](-2.html ".tox") is reloaded. This only affects top-level parameters on the component, all parameters on nodes inside the component are always reloaded with the [.tox](-2.html ".tox").
Reload Built-In Parameters `reloadbuiltin` - When this checkbox is enabled, the values of the component's built-in parameters are reloaded when the [.tox](-2.html ".tox") is reloaded. This only affects top-level parameters on the component, all parameters on nodes inside the component are always reloaded with the [.tox](-2.html ".tox").
Save Backup of External `savebackup` - When this checkbox is enabled, a backup copy of the component specified by the External `.tox` parameter is saved in the `.toe` file. This backup copy will be used if the External `.tox` can not be found. This may happen if the `.tox` was renamed, deleted, or the `.toe` file is running on another computer that is missing component media.
Sub-Component to Load `subcompname` - When loading from an External `.tox` file, this option allows you to reach into the `.tox` and pull out a COMP and make that the top-level COMP, ignoring everything else in the file (except for the contents of that COMP). For example if a `.tox` file named `project1.tox` contains `project1/geo1`, putting `geo1` as the Sub-Component to Load, will result in `geo1` being loaded in place of the current COMP. If this parameter is blank, it just loads the `.tox` file normally using the top level COMP in the file.
Relative File Path Behavior `relpath` - ⊞ - Set whether the child file paths within this COMP are relative to the .toe itself or the .tox, or inherit from parent.
* Use Parent's Behavior `inherit` - Inherit setting from parent.
* Relative to Project File (.toe) `project` - The path, when specified as a relative path, will be relative to the .toe file.
* Relative to External COMP File (.tox) `externaltox` - The path, when specified as a relative path, will be relative to the .tox file. When no external COMP file is specified, or when Enable External .tox is not toggled on, this doesn't have any impact.
  

## Info CHOP Channels
Extra Information for the Replicator COMP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Common COMP Info Channels
* num\_children - Number of children in this component.
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
  
TouchDesigner Build: Latest\nwikieditor2021.100002018.28070before 2018.28070
| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • [Animation](Animation_COMP.html "Animation COMP") • [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • [Constraint](Constraint_COMP.html "Constraint COMP") • [Container](Container_COMP.html "Container COMP") • [Engine](Engine_COMP.html "Engine COMP") • [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • [FBX](FBX_COMP.html "FBX COMP") • [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • [Geo Text](Geo_Text_COMP.html "Geo Text COMP") • [Geometry](Geometry_COMP.html "Geometry COMP") • [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • [Impulse Force](Impulse_Force_COMP.html "Impulse Force COMP") • [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Palette:depthProjection](Palette_depthProjection.html "Palette:depthProjection") • [Parameter](Parameter_COMP.html "Parameter COMP") • Replicator• [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • [Text](Text_COMP.html "Text COMP") • [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • [Window](Window_COMP.html "Window COMP") |
Creates copies of a component, one for every row in a table or using a Number of Replicants parameter - it is the "for-loop" of operators. Unlike [Clone](Clone.html "Clone"), it automatically creates copies of a master component.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

(1) The TouchDesigner window is made of a menu bar at the top, a [Timeline](Timeline.html "Timeline") at the bottom, plus one of a choice of Layouts in the middle. A Layout is made on one or more Panes, each Pane can contain a Network Editor, Viewer, Panel, etc. See [Pane](Pane.html "Pane") and [Bookmark](Bookmark.html "Bookmark"). (2) Nodes in a network are arranged using Layout commands in the RMB menu.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

A set of commands located in a Text DAT that are triggered to run under certain conditions. There are two scripting languages in TouchDesigner: [Python](Python.html "Python") and the original [Tscript](Tscript.html "Tscript"). Scripts and single-line commands can also be run in the [Textport](Textport.html "Textport").

TouchDesigner's original built-in Command scripting language prior to [Python](Python.html "Python").

Cloning makes multiple components match the contents of a master component. A [Component](Component.html "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the Replicator COMP.

Any component can be extended with its own Python classes which contain python functions and data.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.

A name for a component that is accessible from any node in a project, which can be declared in a component's Global Operator Shortcut parameter.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=Replicator_COMP&oldid=30723>"
[Categories](Special_Categories.html "Special:Categories"):
* [Touch Glossary](Category_Touch_Glossary.html "Category:Touch Glossary")
* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")