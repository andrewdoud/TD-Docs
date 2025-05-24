

Window COMP - TouchDesigner Documentation





























# Window COMP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Window Component allows you to create and maintain a separate floating or fixed window displaying the contents of any [Panel](Panel.html "Panel") or any [Node Viewer](Node_Viewer.html "Node Viewer").

Most frequently you are setting up the Window COMP `/perform` in the default TouchDesigner project. `/perform` is the default window for [Perform Mode](Perform_Mode.html "Perform Mode"). In the Parameter dialog of the Window component you adjust its settings such as resolution, centering, and which monitor(s) the window will get displayed on.

You then press F1 to go into [Perform Mode](Perform_Mode.html "Perform Mode") and operate/display the panel standalone.

Press Esc over a window to close it and go back to [Designer Mode](Designer_Mode.html "Designer Mode").

You can create more Window Components, point them to panels or other Operators like TOPs, adjust their parameters and then pulse the parameter Open as Separate Window to see its effect.

Use the Dialog-> [Window Placement Dialog](Window_Placement_Dialog.html "Window Placement Dialog") which controls which window COMPs get displayed on startup. All Window COMPS in your project are listed there and you can test them individually.

A window can be fit to a single monitor, or span several monitors.

Attach an [Info CHOP](Info_CHOP.html "Info CHOP") to the Window component - it will show you the window's current location and size, and whether the window is actually open.

See also [Window](Window.html "Window"), [Multiple Monitors](Multiple_Monitors.html "Multiple Monitors").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[windowCOMP\_Class](https://docs.derivative.ca/WindowCOMP_Class "WindowCOMP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Window Page](#Parameters_-_Window_Page)
* [3 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Specific Window COMP Info Channels](#Specific_Window_COMP_Info_Channels)
  + [5.2 Common COMP Info Channels](#Common_COMP_Info_Channels)
  + [5.3 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Window Page

Window Operator `winop` - Specifies the operator the window will display.
Title `title` - Specify the window's title.

---

Justisy and Offset to... `justifyoffsetto` - ⊞ - All the positioning parameters below are done relative to the location you specify here. Your window can span more than the specified 'area', it's just used as the reference for positioning. **Note for macOS**: When using 'Bounds of all Monitors' you must turn off the 'Displays have separate Spaces' toggle in System Preferences > Desktop & Dock > Mission Control, see [Multiple\_Monitors#macOS](Multiple_Monitors.html#macOS "Multiple Monitors") for details.

* Primary Monitor `primarymonitor` - The primary monitor which is sometimes referred to as the **main display** in Windows control panel or the **primary display** in the NVIDIA control panel.

* Specify Monitor `specifymonitor` - Defines the location to be the monitor specified in the Monitor parameter below.

* Bounds of All Monitors `allmonitors` - Defines the location to include all monitors. The TaskBar is ignored when using this option.

Ignore Taskbar `ignoretaskbar` - The Windows taskBar is ignored when this option is 'On'. When off the taskbar is accounted for so position and sizing will not cover it up.
Monitor `monitor` - Specify the monitor index when Area is set to **Single Monitor**.
Justify Horizontal `justifyh` - ⊞ - Aligns the window horizontally with the monitor or bounds of all monitors.

* Left `left` - Align window so that left edge coincides with left edge of specified area.

* Center `center` - Align window so that horizontal center coincides with horizontal center of specified area.

* Right `right` - Align window so that right edge coincides with right edge of specified area.

* Mouse `mouse` - Align window so it opens horizontally centered on the mouse cursor.

Justify Vertical `justifyv` - ⊞ - Aligns the window vertically with the monitor or bounds of all monitors.

* Top `top` - Align window so that top edge coincides with top edge of specified area.

* Center `center` - Align window so that vertical center coincides with vertical center of specified area.

* Bottom `bottom` - Align window so that bottom edge coincides with bottom edge of specified area.

* Mouse `mouse` - Align window so it opens vertically centered on the mouse cursor.

Offset `winoffset` - ⊞ - Horizontal offset applied to window after justifying.

* X `winoffsetx` - Horizontal offset applied to window after justifying.

* Y `winoffsety` - Vertical offset applied to window after justifying.

Shift to Single Monitor `single` - This menu has options for shifting the opening window. You can either shift to a single monitor or shift to the monitor the cursor is over when the window opens.

---

DPI Scaling `dpiscaling` - ⊞ - Options for managing DPI scaling on high DPI monitors. To inspect a monitor's DPI scaling setting, you can use the [Monitors DAT](Monitors_DAT.html "Monitors DAT") and refer to the `dpi_scale` column.

* Native `native` - Uses the full resolution of the monitor's native pixels, regardless of the operating system's display scaling setting for that monitor. ie Display Scale = 1.0

* Use DPI Scale `usedpiscale` - Uses the resolution set by the operating system's display scaling setting for that monitor. For example, a 3840x2160 monitor with display scaling set to 2.0 results in an addressable resolution of 1920x1080. On Windows system this would be a Display Scaling setting of 200%.

Opening Size `size` - ⊞ - Determines how the size of the window is determined.

* Automatic from Panel COMP/TOP `automatic` - Determines the size automatically from the size of the COMP/TOP specified.

* Fill Location `fill` - Fills the location specified in the Justify and Offset To... parameter above.

* Custom `custom` - Use the Width and Height parameters below to specify a custom size.

Width `winw` - The width of the window when Opening Size parameter is set to Custom.
Height `winh` - The height of the window when Opening Size parameter is set to Custom.
Update Settings from Window `update` - When the window is open you can reposition and resize it. Clicking this button will then read its current windows settings and apply them to the parameters above.

---

Borders `borders` - Controls whether or not the window contains borders and a title bar.
Include Borders in Size `bordersinsize` - When 'On' the borders are included in the size of the window.
Always on Top `alwaysontop` - Controls whether or not the window always sits atop other floating windows.
Cursor Visible `cursorvisible` - ⊞ - Controls whether or not the cursor remains visible when over this window.

* Never `nocursor` - The cursor is never visible over the window.

* When Moving `cursoronmove` - The cursor will only be visible when moving and for a short period after it stops moving.

* Always `alwaysvisible` - The cursor will always be visble when over the window.

Close on Escape Key `closeescape` - When 'On' pressing the escape key over this window will close it. **TIP**: Shift-Escape will always close it, whether this parameter is on or off.
Allow Viewer Interaction `interact` - Enables interactions with the operator specified in the Window Operator parameter.
Allow Minimize `allowminimize` - Enables the window to be minimized in the taskbar (dock in macOS).

---

V-Sync Mode `vsyncmode` - ⊞ - Controls how the window is updated with regards to V-Sync. Enabled means it will update in sync with the monitors refresh which avoids tearing and lost frames. Disabled means it can update at any point during the refresh which can result in tearing or lost frames. FPS is Half Monitor Rate should be used when doing things such as running a 30fps file on a 60Hz display. This makes each update be shown for exactly 2 refreshes which keeps motion looking smooth.

* Disabled `disabled` - Vertical Sync off.

* Enabled `enabled` - Vertical Sync on.

* FPS is Half Monitor Rate `halfmonitorrate` - This allows you to run your project at 30FPS on a 60Hz monitor, but ensuring every image is shown for exactly 2 refreshes. Without this option an image may be shown for 1 or 3 refreshes, which makes the content look like it is stuttering. Currently this feature is not functional in the 2022.20000+ series of builds, but we hope to bring back this feature when Vulkan adds support for it.

Draw Window `drawwindow` - When disabled the window will not update it's contents at all. Useful for processes that arn't doing rendering such as Audio or networking processes, or for when using VR devices.
Hardware Frame-Lock `hwframelock` - Provides multi-GPU frame-lock sync using [Nvidia Quadro Sync](https://www.nvidia.com/en-us/design-visualization/solutions/quadro-sync/) and [AMD S400](http://www.amd.com/us/products/workstation/graphics/s400/Pages/s400.aspx) sync cards. For more information, see [Syncing Multiple Computers](Syncing_Multiple_Computers.html "Syncing Multiple Computers") and [Hardware Frame Lock](Hardware_Frame_Lock.html "Hardware Frame Lock").
OpenGL Stereo `openglstereo` - **No longer supported.** Turn 'On' when using openGL stereoscopic output.
Right Eye Operator `winrightop` - **No longer supported.** This parameter is enabled when the OpenGL Stereo parameter above is turned on. Specify the [Camera COMP](Camera_COMP.html "Camera COMP") used for the right eye here.

---

Open as Perform Window `performance` - Opens this Window COMP in [Perform Mode](Perform_Mode.html "Perform Mode"). Any Window COMP can be set as default Perform Window (opens using F1 shortcut) using the [Window Placement Dialog](Window_Placement_Dialog.html "Window Placement Dialog"). This button allows you to open this Window COMP in Perform Mode without changing what is currently selected as the 'default' Perform Window.
Open as Separate Window `winopen` - Opens this Window COMP as its own floating window, not as the Perform Window. Useful for things such as dialog boxes, popups, or testing, but should not be used for putting final rendered content to outputs. Use a single large Perform Window for that instead of separate windows.
Close `winclose` - Closes the window, if it's open.
Set as Perform Window `setperform` - Permanently changes the Perform Window setting in the Window Placement dialog to this window.
Window Placement Dialog `opendialog` - A shortcut to open the Window Placement dialog.
Include in Placement Dialog `includedialog` - When 'On' this Window COMP will be displayed in the Window Placement Dialog.

  


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

Extra Information for the Window COMP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Specific Window COMP Info Channels

* winx -

* winy -

* winw -

* winh -

* winopen -

* fill -

* borders -

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

  

TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditor2021.100002018.28070before 2018.28070

| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • [Animation](Animation_COMP.html "Animation COMP") • [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • [Constraint](Constraint_COMP.html "Constraint COMP") • [Container](Container_COMP.html "Container COMP") • [Engine](Engine_COMP.html "Engine COMP") • [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • [FBX](FBX_COMP.html "FBX COMP") • [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • [Geo Text](Geo_Text_COMP.html "Geo Text COMP") • [Geometry](Geometry_COMP.html "Geometry COMP") • [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • [Impulse Force](Impulse_Force_COMP.html "Impulse Force COMP") • [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Palette:depthProjection](Palette_depthProjection.html "Palette:depthProjection") • [Parameter](Parameter_COMP.html "Parameter COMP") • [Replicator](Replicator_COMP.html "Replicator COMP") • [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • [Text](Text_COMP.html "Text COMP") • [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • Window |

A Window in TouchDesigner is a window in Microsoft Windows or macOS that contains either (1) the TouchDesigner editing interface that exists in [Designer Mode](Designer_Mode.html "Designer Mode"), or (2) a user-created [Panel](Panel.html "Panel") inside a Window Component. The user-created windows can span [Multiple Monitors](Multiple_Monitors.html "Multiple Monitors") borderless, or be floating windows with borders, or popups.


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


Any floating window that is not a [Pane](Pane.html "Pane") or [Viewer](Viewer.html "Viewer").


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.


The term "Frame" is a measurement of time used (1) in the [Timeline](Timeline.html "Timeline"), (2) as a time-unit in CHOPs, and (3) as a time unit in movie files that are read into [TOPs](TOP.html "TOP") and written out from TOPs. The frame rate is the frames per second ([FPS](https://docs.derivative.ca/index.php?title=FPS&action=edit&redlink=1 "FPS (page does not exist)")).


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.


Perform Mode is an optimized mode for live performance that only renders one specified Window COMP which is one window that contains your video outputs and your (optional) control interface. In Perform Mode the network editing window is not open - you edit your networks in [Designer Mode](Designer_Mode.html "Designer Mode"). Alternate with F1 and Esc.


Any component can be extended with its own Python classes which contain python functions and data.


The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.


A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.


A name for a component that is accessible from any node in a project, which can be declared in a component's Global Operator Shortcut parameter.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.


The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.


Cloning makes multiple components match the contents of a master component. A [Component](Component.html "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the [Replicator COMP](Replicator_COMP.html "Replicator COMP").


To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.


TOuch Environment file, the file type used by TouchDesigner to save your entire project.


There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Window_COMP&oldid=32450>"
[Category](Special_Categories.html "Special:Categories"):

* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")