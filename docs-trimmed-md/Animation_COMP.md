

Animation COMP - TouchDesigner Documentation




# Animation COMP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Animation Component is a special component used for creating keyframe animation channels. The component contains a pre-defined network utilizing a [Keyframe CHOP](Keyframe_CHOP.html "Keyframe CHOP") and a number of [Table DATs](Table_DAT.html "Table DAT") to define the animated [CHOP](CHOP.html "CHOP") channels.
The [Animation Editor](Animation_Editor.html "Animation Editor") is the user interface for creating and editing the animation of the Animation Component.
The Animation Component has both in and out CHOP connectors.
**Animation Component Inputs**
With no input connected, the Animation Component's index loops over the time range of the channels.
The CHOP input can be used to manually control the index of the animated channels. For example, if the channels are keyed from frame 1 to 600, you can connect an input to the component and manually drive the animation output by feeding it a number between 1 and 600 (indexes outside the range will use the channel extend conditions).
Using the Keyframe CHOP's Index Units menu, you can drive the animation with numbers expressed in seconds, samples, or a fraction where 0 is the start and 1 is the end.
**Animation Component Outputs**
The CHOP output gives access to the animation channel's current value. CHOPs can be directly connected or a [Null CHOP](Null_CHOP.html "Null CHOP") may be appended for [exporting](CHOP_Export.html "CHOP Export") the channels to parameters. The current channel values can also be viewed by turning on the Animation Component's [node viewer](Node_Viewer.html "Node Viewer").
[![AnimationCOMPTimesliced.png](https://docs.derivative.ca/images/f/fe/AnimationCOMPTimesliced.png)](https://docs.derivative.ca/File:AnimationCOMPTimesliced.png)
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[animationCOMP\_Class](https://docs.derivative.ca/AnimationCOMP_Class "AnimationCOMP Class")
## Contents
* [1 Summary](#Summary)
  + [1.1 Using the Animation Component](#Using_the_Animation_Component)
* [2 Parameters - Animation Page](#Parameters_-_Animation_Page)
* [3 Parameters - Range Page](#Parameters_-_Range_Page)
* [4 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [5 Parameters - Common Page](#Parameters_-_Common_Page)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common COMP Info Channels](#Common_COMP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

### Using the Animation Component
Keyframing any parameter, attribute, or data in TouchDesigner begins with an Animation Component. You can create an Animation COMP from;
* The [OP Create Dialog](OP_Create_Dialog.html "OP Create Dialog")
* Right-click on any parameter of an OP. **RMB -> Keyframe Parameter in... -> New Animation** to create a new Animation COMP
To open the Animation Editor, right-click on an Animation COMP and select **Edit Animation...** to open that animation in the editor. You can also change any pane to **Animation Editor** type and the Editor will open whilst pointing to the last Animation COMP that was scoped.
Then you can create and keyframe animation channels. Refer to the [Animation Editor](Animation_Editor.html "Animation Editor") for instructions on keyframing.
[![AnimationCOMPEdit.png](images/a/af/AnimationCOMPEdit.png)](File_AnimationCOMPEdit.html)
  

## Parameters - Animation Page
Time Reference `timeref` - The location the Animation COMP looks to for its time information. This is used for default channel range and rate when the Type parameter on the Range page is set to **Timeline**.
Play Mode `playmode` - ⊞ - Specifies the method used to playback the animation or allows the output the entire animation curve.
* Locked to Timeline `locked` - This mode locks the animation position to the timeline. Scrubbing or jumping in the timeline will change the animation position accordingly. The parameters Play, Speed, Cue, and Cue Point are disabled in this mode since the timeline is directly controlling the animation's position.
* Use Input Index `input` - This mode allows the user to specify a particular position in the animation using the index input on the Animation COMP (the CHOP input to the Animation COMP). The Input Index Unit parameter can be used to change the units of the input channel. Use this mode for random access to any location in the animation for maximum flexibility.
* Sequential `sequential` - This mode continually plays regardless of the timeline position (the Index parameter is disabled). Reset and Speed parameters below are enabled to allow some control.
* Output Full Range `outputrange` - This option outputs the entire animation channel range. This is useful for using the Animation COMP to create custom lookup curves/channels.
Play `play` - Animation plays when On and stops when Off. This animation playback control is only available when Play Mode is *Sequential*.
Speed `speed` - This is a speed multiplier which only works when Play Mode is *Sequential*. A value of 1 is the default playback speed. A value of 2 is double speed, 0.5 is half speed and so on. Negative values will play the animation backwards.
Cue `cue` - Jumps to Cue Point when set to 1. Only available when Play Mode is Sequential.
Cue Pulse `cuepulse` - Instantly jumps to the Cue Point.
Cue Point `cuepoint` - Set any index in the animation as a point to jump to. Only available when Play Mode is Sequential.
Cue Point Unit `cuepointunit` - Units used when setting the Cue Point parameter.
Input Index Unit `inputindexunit` - ⊞ - When Play Mode is set to **Use Input Index** use this menu to choose the units for the index input channel. For example, choose between setting the index with frames or seconds. The Units X option sets the index to use the key information directly from the key DAT table inside the Animation COMP, disregarding any custom settings found in the attributes DAT table.
* Samples `samples` -
* Frames `frames` -
* Seconds `seconds` -
* Fraction `fraction` -
* X Units `xunits` -
Cyclic Range `cyclic` - ⊞ - Adapts the range of the animation for cyclic or non-cyclic input indices. When using a cyclic input index the lookup value for index 0.0 and 1.0 result in the same value. To avoid this, set Cyclic Range to Yes and the lookup will cycle smoothly.
* Automatic `auto` - Checks the right extend condition of each channel (Assumes type cycle and mirror are cyclic lookups).
* Yes `yes` - Cycles the output when index is outside the animation range.
* No `no` - Does not cycle the output when index is outside the animation range.
Specify Edit Attributes `specifyedit` - Turn this on to enable the edit attributes parameter below.
Edit Origin `editorigin` - Changes the origin of the animation channel edits. This does not change the data stored in the key DAT table, but it does effect the channels display in the graph and playback of the animation.
Edit Rate `editrate` - Changes the rate of the animation channel edits. This does not change the data stored in the key DAT table, but it does effect the channels display in the graph and playback of the animation.
Edit Animation... `editanimation` - Clicking this button will open this Animation COMP in the Animation Editor.
  

## Parameters - Range Page
Type `rangetype` - ⊞ - Set the working range for the Animation COMP.
* Timeline `timeline` - Uses the range set in the timeline specified by the Time Reference parameter on the previous Animation parameter page.
* Custom `custom` - Set a custom range using the Start and End parameters below.
Start `start` - Start of the Custom range, expressed in units seconds, frames or samples.
Start Unit `startunit` - Select the units to use for this parameter, Samples, Frames, or Seconds.
End `end` - End of the Custom range, expressed in units seconds, frames or samples.
End Unit `endunit` - Select the units to use for this parameter, Samples, Frames, or Seconds.
Trim Left `tleft` - ⊞ - Determines the output of the channels when past the 'End' position. Does not affect Play Mode = Output Full Range, to manipulate the [Extend Conditions](Extend_Conditions.html "Extend Conditions") of that mode adjust the Extend parameters of the [Keyframe CHOP](Keyframe_CHOP.html "Keyframe CHOP") inside the Animation COMP.
* Hold `hold` - Hold the current value of the channel.
* Slope `slope` - Continue the slope before the start of the channel.
* Cycle `cycle` - Cycle the channel repeatedly.
* Mirror `mirror` - Cycle the channel repeatedly, mirroring every other cycle.
* Default Value `default` - Use the constant value specified in the Default Value parameter.
Trim Right `tright` - ⊞ - Determines the output of the channels when before the 'Start' position. Does not affect Play Mode = Output Full Range, to manipulate the [Extend Conditions](Extend_Conditions.html "Extend Conditions") of that mode adjust the Extend parameters of the [Keyframe CHOP](Keyframe_CHOP.html "Keyframe CHOP") inside the Animation COMP.
* Hold `hold` - Hold the current value of the channel.
* Slope `slope` - Continue the slope after the end of the channel.
* Cycle `cycle` - Cycle the channel repeatedly.
* Mirror `mirror` - Cycle the channel repeatedly, mirroring every other cycle.
* Default Value `default` - Use the constant value specified in the Default Value parameter.
Trim Default `tdefault` - The value used for the Default Value trim conditio above.
  

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
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Animation COMP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2022.241402021.100002018.28070before 2018.28070
| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • Animation• [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • [Constraint](Constraint_COMP.html "Constraint COMP") • [Container](Container_COMP.html "Container COMP") • [Engine](Engine_COMP.html "Engine COMP") • [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • [FBX](FBX_COMP.html "FBX COMP") • [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • [Geo Text](Geo_Text_COMP.html "Geo Text COMP") • [Geometry](Geometry_COMP.html "Geometry COMP") • [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • [Impulse Force](Impulse_Force_COMP.html "Impulse Force COMP") • [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Palette:depthProjection](Palette_depthProjection.html "Palette:depthProjection") • [Parameter](Parameter_COMP.html "Parameter COMP") • [Replicator](Replicator_COMP.html "Replicator COMP") • [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • [Text](Text_COMP.html "Text COMP") • [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • [Window](Window_COMP.html "Window COMP") |
An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

In the Animation component each keyframe specifies a channel's value at a specific time (or frame). A keyframe holds a value, slopes and accelerations, and an interpolation type. A channel's keyframes are used to interpolate and determine the values of all the samples of the channel.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").
The grey dashed lines between nodes is a Reference (or [Link](Link.html "Link")). A Reference is (1) a [Parameter Reference](Parameter_Reference.html "Parameter Reference"), a parameter in an OP that is a name or path to another operator, (2) a [Node Reference](https://docs.derivative.ca/index.php?title=Node_Reference&action=edit&redlink=1 "Node Reference (page does not exist)"), an expression in a parameter or DAT script that contains the name or path of another operator, (3) a DAT Cell Reference or (4) a CHOP Channel Reference.
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").

The panel at the bottom of TouchDesigner, it controls the current global looping [Time](Time_COMP.html "Time COMP") your TouchDesigner project, or of just one component.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

Any component can be extended with its own Python classes which contain python functions and data.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.

A name for a component that is accessible from any node in a project, which can be declared in a component's Global Operator Shortcut parameter.

Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

Cloning makes multiple components match the contents of a master component. A [Component](Component.html "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the [Replicator COMP](Replicator_COMP.html "Replicator COMP").

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").

Retrieved from "<https://docs.derivative.ca/index.php?title=Animation_COMP&oldid=30721>"
[Category](Special_Categories.html "Special:Categories"):
* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")