

# Impulse_Force_COMP

Impulse Force COMP - TouchDesigner Documentation




# Impulse Force COMP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
An Impulse Force COMP will create a force in the simulation that can be applied for 1 frame using the Pulse Force parameter. In the real world, impulse forces are forces applied over a very short duration, however in [Bullet](Bullet_Dynamics.html "Bullet Dynamics") this is somewhat simplified, and they are instead applied instantly (for a single frame). Examples of impulse forces are kicking a ball or shooting a cannon. The velocities of the affected bodies are changed in an instant by the impulse force, and after that instant the force no longer has an effect unless applied again.
The resulting velocity of the bodies after the impulse force is applied is the same as the [Force COMP](Force_COMP.html "Force COMP") with the same values if the Force COMP is applied for exactly 1 second. For example, if 10N of Impulse Force is applied to a body with mass 5kg then the resulting velocity will be 10N / 5kg \* 1sec = 2m/s.
See also: [Bullet Dynamics](Bullet_Dynamics.html "Bullet Dynamics"), [Bullet Solver COMP](Bullet_Solver_COMP.html "Bullet Solver COMP"), [Actor COMP](Actor_COMP.html "Actor COMP"), [Force COMP](Force_COMP.html "Force COMP"), [Constraint COMP](Constraint_COMP.html "Constraint COMP"), [Bullet Solver CHOP](Bullet_Solver_CHOP.html "Bullet Solver CHOP").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[impulseforceCOMP\_Class](https://docs.derivative.ca/ImpulseforceCOMP_Class "ImpulseforceCOMP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Force Page](#Parameters_-_Force_Page)
* [3 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
  

## Parameters - Force Page
Pulse Force `pulse` - Pulse for the impulse force. When pulsed, on the next frame it will apply the impulse force.
Force `force` - ⊞ - The linear force in Newtons to be applied when the node is pulsed.
* X `forcex` -
* Y `forcey` -
* Z `forcez` -
Relative Position `relpos` - ⊞ - The position at which to apply the linear force, relative to the center of the body (Note: the physical center of the object, not the center of mass). Having a nonzero relative position will also cause the body to rotate due to added torque.
* X `relposx` -
* Y `relposy` -
* Z `relposz` -
Torque `torque` - ⊞ - The rotational force in Newtons that will be applied.
* X `torquex` -
* Y `torquey` -
* Z `torquez` -
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
Global Shortcut `opshortcut` - Specifies a name you can use anywhere at all as the path to that component. See [Global OP Shortcut](Global_OP_Shortcut.html "Global OP Shortcut").
Shortcut `iop0shortcut` - Specifies a name you can use anywhere inside the component as a path to "Internal OP" below. See [Internal Operators](Internal_Operators.html "Internal Operators").
OP `iop0op` - The path to the Internal OP inside this component. See [Internal Operators](Internal_Operators.html "Internal Operators").
Node View `nodeview` - ⊞ - Determines what is displayed in the node viewer, also known as the [Node Viewer](Node_Viewer.html "Node Viewer"). Some options will not be available depending on the Component type ([Object Component](Object_Component.html "Object Component"), [Panel Component](Panel_Component.html "Panel Component"), Misc.)
* Default Viewer `default` - Displays the default viewer for the component type, a 3D Viewer for Object COMPS and a Control Panel Viewer for Panel COMPs.
* Operator Viewer `opviewer` - Displays the node viewer from any operator specified in the Operator Viewer parameter below.
Operator Viewer `opviewer` - Select which operator's node viewer to use when the Node View parameter above is set to Operator Viewer.
Keep in Memory `keepmemory` - Used only for [Panel Components](Panel_Component.html "Panel Component") this keeps the panel in memory to it doesn't reload every time it is displayed.
Enable Cloning `enablecloning` - Control if the OP should be actively cloneing. Turning this off causes this node to stop cloning it's 'Clone Master'.
Enable Cloning Pulse `enablecloningpulse` - Instantaneously clone the contents.
Clone Master `clone` - Path to a component used as the Master [Clone](Clone.html "Clone").
Load on Demand `loadondemand` - Loads the component into memory only when required. Good to use for components that are not always used in the project.
External .tox `externaltox` - Path to a `.tox` file on disk which will source the component's contents upon start of a `.toe`. This allows for components to contain networks that can be updated independently. If the `.tox` file can not be found, whatever the `.toe` file was saved with will be loaded.
Reload .tox on Start `reloadtoxonstart` - When on (default), the external .tox file will be loaded when the .toe starts and the contents of the COMP will match that of the external .tox. This can be turned off to avoid loading from the referenced external .tox on startup if desired (the contents of the COMP are instead loaded from the .toe file). Useful if you wish to have a COMP reference an external .tox but not always load from it unless you specifically push the Re-Init Network parameter button.
Reload Custom Parameters `reloadcustom` - When this checkbox is enabled, the values of the component's [Custom Parameters](Custom_Parameters.html "Custom Parameters") are reloaded when the [.tox](-2.html ".tox") is reloaded. This only affects top-level parameters on the component, all parameters on nodes inside the component are always reloaded with the [.tox](-2.html ".tox").
Reload Built-In Parameters `reloadbuiltin` - When this checkbox is enabled, the values of the component's built-in parameters are reloaded when the [.tox](-2.html ".tox") is reloaded. This only affects top-level parameters on the component, all parameters on nodes inside the component are always reloaded with the [.tox](-2.html ".tox").
Save Backup of External `savebackup` - When this checkbox is enabled, a backup copy of the component specified by the External `.tox` parameter is saved in the `.toe` file. This backup copy will be used if the External `.tox` can not be found. This may happen if the `.tox` was renamed, deleted, or the `.toe` file is running on another computer that is missing component media.
Sub-Component to Load `subcompname` - When loading from an External `.tox` file, this option allows you to reach into the `.tox` and pull out a COMP and make that the top-level COMP, ignoring everything else in the file (except for the contents of that COMP). For example if a `.tox` file named `project1.tox` contains `project1/geo1`, putting `geo1` as the Sub-Component to Load, will result in `geo1` being loaded in place of the current COMP. If this parameter is blank, it just loads the `.tox` file normally using the top level COMP in the file.
Re-Init Network `reinitnet` - This button will re-load from the external `.tox` file (if present), followed by re-initializing itself from its master, if it's a clone.
TouchDesigner Build: Latest\n2021.100002019.146502018.28070
| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • [Animation](Animation_COMP.html "Animation COMP") • [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • [Constraint](Constraint_COMP.html "Constraint COMP") • [Container](Container_COMP.html "Container COMP") • [Engine](Engine_COMP.html "Engine COMP") • [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • [FBX](FBX_COMP.html "FBX COMP") • [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • [Geo Text](Geo_Text_COMP.html "Geo Text COMP") • [Geometry](Geometry_COMP.html "Geometry COMP") • [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • Impulse Force• [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Palette:depthProjection](Palette_depthProjection.html "Palette:depthProjection") • [Parameter](Parameter_COMP.html "Parameter COMP") • [Replicator](Replicator_COMP.html "Replicator COMP") • [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • [Text](Text_COMP.html "Text COMP") • [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • [Window](Window_COMP.html "Window COMP") |
An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

Any component can be extended with its own Python classes which contain python functions and data.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.

Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").

Cloning makes multiple components match the contents of a master component. A [Component](Component.html "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the [Replicator COMP](Replicator_COMP.html "Replicator COMP").

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

Every component contains a network of operators that create and modify data. The operators are connected by wires that define where data is routed after the operator cooks its inputs and generates an output.

Retrieved from "<https://docs.derivative.ca/index.php?title=Impulse_Force_COMP&oldid=23584>"
[Category](Special_Categories.html "Special:Categories"):
* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")