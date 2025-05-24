

Constraint COMP - TouchDesigner Documentation





























# Constraint COMP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

A Constraint COMP is used to restrict the movement of the bodies in a set of [Actor COMPs](Actor_COMP.html "Actor COMP"). Currently this can be done in a few ways: point to point, hinge or slider. Constraints can either be applied on a single body or between two bodies. Constraints can be used to create connectivity between bodies, or to create bodies that can move but need to have that movement restricted in some way. Some examples of constraints in the real world: a train, a door, an arm.

If a point to point constraint is applied to a single body, then that body will be restricted to 3 degrees of freedom (DOF). It will still have all 3 degrees of freedom for rotation (ie. All 3 axes), but the 3 degrees of freedom for translation will all be constrained. If a point to point constraint is applied between two bodies, then they will both be similarly constrained to 3 DOF. However, they will be able to move (translate) along all 3 axes but they will do it connected to each other at their pivot points. By using this constraint method, a chain of bodies can be created. For instance, point to point constraints can be used to simulate train cars connected to each other.

If a hinge constraint is applied to a single body, then that body will be restricted to 1 DOF relative to the other body. It will only be able to rotate around 1 axis, and that axis is defined using the Axis parameter on the Constraint COMP. Much like the point to point constraint, the hinge also as a pivot point around which it will rotate. If a hinge constraint is applied between two bodies, then they will both be able to move with 3 DOF but they will do it connected to each other at their pivot points. However, they will still only be able to rotate around their respective axis. The simplest example of a hinge constraint is a door.

If a slider constraint is applied to a single body, then that body's translation/rotation will be constrained to just that axis. In other words, the body can only move along that axis (either direction) and can only rotate along that axis (either direction).

See also: [Bullet Dynamics](Bullet_Dynamics.html "Bullet Dynamics"), [Bullet Solver COMP](Bullet_Solver_COMP.html "Bullet Solver COMP"), [Actor COMP](Actor_COMP.html "Actor COMP"), [Force COMP](Force_COMP.html "Force COMP"), [Impulse Force COMP](Impulse_Force_COMP.html "Impulse Force COMP"), [Bullet Solver CHOP](Bullet_Solver_CHOP.html "Bullet Solver CHOP").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[constraintCOMP\_Class](https://docs.derivative.ca/ConstraintCOMP_Class "ConstraintCOMP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Constraint Page](#Parameters_-_Constraint_Page)
* [3 Parameters - Limits Page](#Parameters_-_Limits_Page)
* [4 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [5 Parameters - Common Page](#Parameters_-_Common_Page)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common COMP Info Channels](#Common_COMP_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Constraint Page

Active `active` - Toggle the constraint on/off in the simulation.
Type `type` - ⊞ - The type of constraint to create: point to point, hinge, or slider.

* Point To Point `p2p` -

* Hinge `hinge` -

* Slider `slider` -

Body to Body `bodytobody` - Toggle body to body mode on/off. Body to body mode creates a constraint between two bodies (Actor 1 Bodies and Actor 2 Bodies). When toggled off it will create constrain bodies individually. If Actor 1 Bodies and Actor 2 Bodies contain the same number of referenced bodies, then this mode will create a constraint between each respective pair. For instance, if Actor 1 Bodies contains the string "0 1 2", and Actor 2 Bodies contains the string "3 4 5" then this will create 3 constraints: 0->3, 1->4, 2->5. It is a 1 to 1 relationship between these two parameters. However, if Actor 1 Bodies has more bodies than Actor 2 Bodies, then the remaining "unmatched" bodies of Actor 1 Bodies will instead be individually constrained. For instance, if Actor 1 Bodies contains the string "0 1 2" and Actor 2 Bodies contains the string "3 4", then two constraints will be created between bodies: 0->3, 1->4. Body 2 will be constrained individually. If Actor 2 Bodies contains more bodies than Actor 1 Bodies, then any unmatched bodies in Actor 2 Bodies will simply be disregarded (no constraint created for them).
Collisions between Bodies `collisions` - Turns on/off collisions between the body to body constraints.
Display Constraint `dispcom` - Turns on/off the display of the constraint guide in the viewer.
Actor COMP `actor1` - A reference to an Actor COMP. This specifies the Actor COMP of which you want to constrain some bodies.
Actor Bodies `bodies1` - A list (regular expression) of the IDs of the bodies in actor1 to constrain. If an Actor COMP contains N bodies, then body IDs will go from 0 to N-1 for that Actor COMP. The number of bodies can be verified using the [Bullet Solver CHOP](Bullet_Solver_CHOP.html "Bullet Solver CHOP").
Pivot `pivot1` - ⊞ - The pivot point for the constraint.

* X `pivot1x` -

* Y `pivot1y` -

* Z `pivot1z` -

Hinge Axis `axis1` - ⊞ - The axis around which to create the hinge. Each value is typically a number between 0 and 1. For example, to spin around the Z axis set to 0, 0, 1.

* X `axis1x` -

* Y `axis1y` -

* Z `axis1z` -

Slider Rotation `sliderrot1` - ⊞ - The rotation of the slider constraint axis. By default the slider constraint is applied on the X axis.

* X `sliderrot1x` -

* Y `sliderrot1y` -

* Z `sliderrot1z` -

Actor COMP `actor2` - A reference to an Actor COMP. This specifies the Actor COMP of which you want to constrain some bodies. This Actor COMP is only used when body to body mode is toggled on.
Actor Bodies `bodies2` - A list (regular expression) of the IDs of the bodies in actor2 to constrain. If an Actor COMP contains N bodies, then body IDs will go from 0 to N-1 for that Actor COMP. The number of bodies can be verified using the Bullet Solver CHOP.
Pivot `pivot2` - ⊞ - The pivot point for the constraint.

* X `pivot2x` -

* Y `pivot2y` -

* Z `pivot2z` -

Hinge Axis `axis2` - ⊞ - The axis around which to create the hinge. Each value is typically a number between 0 and 1. For example, to spin around the Z axis set to 0, 0, 1.

* X `axis2x` -

* Y `axis2y` -

* Z `axis2z` -

Slider Rotation `sliderrot2` - ⊞ - The rotation of the slider constraint axis. By default the slider constraint is applied on the X axis.

* X `sliderrot2x` -

* Y `sliderrot2y` -

* Z `sliderrot2z` -

  


## Parameters - Limits Page

Enable Limits `enablelimits` - Enables limits on the constraint. Without constraints, the bodies will be able to rotate a full 360 degrees, or translate any distance.
Lower Linear Limit `lowerlinlim` - The lower limit for translation of the body along the constraint. Only used with slider constraints.
Upper Linear Limit `upperlinlim` - The upper limit for translation of the body along the constraint. Only used with slider constraints.
Lower Angular Limit `loweranglim` - The lower limit for rotation of the body around its axis. Used with slider constraints or hinge constraints.
Upper Angular Limit `upperanglim` - The upper limit for rotation of the body around its axis. Used with slider constraints or hinge constraints.

  


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


Node View `nodeview` - ⊞ - Determines what is displayed in the node viewer, also known as the [Node Viewer](Node_Viewer.html "Node Viewer"). Some options will not be available depending on the Component type ([Object Component](Object_Component.html "Object Component"), [Panel Component](Panel_Component.html "Panel Component"), Misc.)

* Default Viewer `default` - Displays the default viewer for the component type, a 3D Viewer for Object COMPS and a Control Panel Viewer for Panel COMPs.

* Operator Viewer `opviewer` - Displays the node viewer from any operator specified in the Operator Viewer parameter below.

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

Extra Information for the Constraint COMP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\nwikieditor2022.241402021.100002019.146502018.28070

| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • [Animation](Animation_COMP.html "Animation COMP") • [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • Constraint• [Container](Container_COMP.html "Container COMP") • [Engine](Engine_COMP.html "Engine COMP") • [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • [FBX](FBX_COMP.html "FBX COMP") • [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • [Geo Text](Geo_Text_COMP.html "Geo Text COMP") • [Geometry](Geometry_COMP.html "Geometry COMP") • [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • [Impulse Force](Impulse_Force_COMP.html "Impulse Force COMP") • [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Palette:depthProjection](Palette_depthProjection.html "Palette:depthProjection") • [Parameter](Parameter_COMP.html "Parameter COMP") • [Replicator](Replicator_COMP.html "Replicator COMP") • [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • [Text](Text_COMP.html "Text COMP") • [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • [Window](Window_COMP.html "Window COMP") |

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


Any component can be extended with its own Python classes which contain python functions and data.


The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.


A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.


A name for a component that is accessible from any node in a project, which can be declared in a component's Global Operator Shortcut parameter.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.


A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").


Cloning makes multiple components match the contents of a master component. A [Component](Component.html "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the [Replicator COMP](Replicator_COMP.html "Replicator COMP").


To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.


TOuch Environment file, the file type used by TouchDesigner to save your entire project.


There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").







Retrieved from "<https://docs.derivative.ca/index.php?title=Constraint_COMP&oldid=30725>"
[Category](Special_Categories.html "Special:Categories"):

* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")