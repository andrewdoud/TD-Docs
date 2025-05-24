

Engine COMP - TouchDesigner Documentation




# Engine COMP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Engine COMP will run a `.tox file` (component) in a separate process. It uses [TouchEngine](TouchEngine.html "TouchEngine") to manage these processes and pass data between the loaded component and the main project.
**Inputs and Outputs**
The chosen component's top-level Inputs and Outputs are exposed as inputs and outputs on the Engine COMP. Only [TOP](TOP.html "TOP"), [CHOP](CHOP.html "CHOP") and [DAT](DAT.html "DAT") inputs and outputs are supported.
**Custom Parameters**
Any [custom parameters](Custom_Parameters.html "Custom Parameters") on the top-level component are added to the Engine COMP's parameters. Custom parameters which refer to other nodes in the network, such as [TOP](TOP.html "TOP"), [CHOP](CHOP.html "CHOP") and [DAT](DAT.html "DAT") parameters, are not supported - you should use inputs to connect those nodes instead.
Note that parameters work in one direction only - you cannot set a parameter from within the loaded `.tox`.
**External File Paths**
By default, relative paths on OPs or in scripts **inside** the loaded component are relative to the `.tox` file's location. This can be changed with the 'Asset Paths' parameter. Relative paths as file or folder custom parameters **of** the component - those that show up on the Engine COMP - are always relative to the main project.
**Monitoring Engine Status**
It is useful to monitor the state and performance of the Engine COMP. By default, an [Info DAT](Info_DAT.html "Info DAT") is docked to the Engine COMP and contains file path and process ID. A docked [Info CHOP](Info_CHOP.html "Info CHOP") contains three sets of monitoring channels: The Info Type menu is by default set to TouchEngine Status which gives loading / running / error status of the Engine process. Changing the menu to TouchEngine Perform gives the engine's performance statistics, and changing the menu to Initialize/Start give ready / running state information specifically about your loaded component since it can be paused, timed and re-initialized.
**Controlling Engine State**
The Engine process will be started by the TouchDesigner process and it will run your `.tox` component automatically. But you can have more control over the time/memory management of multiple components using the Unload, Reload pulse parameters for the currently-loaded `.tox` file. On the Advanced page, the Launch and Quit Engine Process parameters give you terminate/restart control of the entire Engine process.
**Component Lifetime**
Under TouchEngine, components are loaded into an already-running instance. For this reason, an [Execute DAT](Execute_DAT.html "Execute DAT")'s `onStart()` and `onExit()` method will never be executed under TouchEngine. The `onCreate()` method will be executed when the component is loaded, and is a good place to do any setup you would normally do in `onStart()`.
**Time in TouchEngine**
When the Engine COMP starts the component (after it has loaded, if 'Start when Initialized' is On), the component time in TouchEngine is `0`. It will then increase either in sync with the Engine COMP or according to TouchEngine's internal clock, depending on the setting of the 'Clock' parameter on the Tune parameter page.
An input buffer and output buffer are used to allow for differences in cook rate between the Engine COMP and TouchEngine. Often you may want to adjust the parameters on the Tune page to suit your particular setup. The Engine COMP will cook frames to fill its input buffer, if required, prior to starting to cook the component in TouchEngine - then will cook frames in TouchEngine to fill its output buffer prior to emitting output from the Engine COMP. The Auto setting will attempt to keep small buffers sufficient to avoid dropped frames, but you may wish to set a fixed buffer size to suit your setup, particularly if working with audio.
**TouchEngine Versions**
TouchEngine is installed as part of TouchDesigner, and the currently running version will be used to load the given `.tox`. If you wish to use a different version of TouchEngine you can either set the [environment variable](Variables.html#System_Environment_Variables "Variables") `TOUCHENGINE_APP_PATH` to the path to a TouchDesigner installation (an installation directory on Windows, or a TouchDesigner app on macOS) *or* install TouchDesigner into a folder named `TouchEngine` alongside the `.tox` (on macOS rename an application from TouchDesigner to TouchEngine) *or* create a link named `TouchEngine` alongside the `.tox` which points to an installation directory or TouchDesigner app.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[engineCOMP\_Class](https://docs.derivative.ca/EngineCOMP_Class "EngineCOMP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Engine Page](#Parameters_-_Engine_Page)
* [3 Parameters - Tune Page](#Parameters_-_Tune_Page)
* [4 Parameters - InitStart Page](#Parameters_-_InitStart_Page)
* [5 Parameters - Advanced Page](#Parameters_-_Advanced_Page)
* [6 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [7 Parameters - Common Page](#Parameters_-_Common_Page)
* [8 Info CHOP Channels](#Info_CHOP_Channels)
  + [8.1 Specific Engine COMP Info Channels](#Specific_Engine_COMP_Info_Channels)
  + [8.2 Common COMP Info Channels](#Common_COMP_Info_Channels)
  + [8.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Engine Page
Tox File `file` - Specify the `.tox` file to load with TouchEngine.
Unload `unload` - Unload the currently loaded component.
Reload `reload` - Reload the currently loaded component.
Reload on Crash `reloadoncrash` - If the TouchEngine instance quits for any reason, restart it.
Asset Paths `assetpaths` - ⊞ - Specify how relative paths inside the component are resolved.
* Relative to Project File (`.toe`) `project` - Relative paths inside the component are relative to the project file running TouchEngine.
* Relative to COMP File (`.tox`) `comp` - Relative paths inside the component are relative to the component (`.tox` file).
Callbacks DAT `callbacks` - The Callbacks DAT will execute for events related to the TouchEngine instance.
  

## Parameters - Tune Page
Clock `clock` - ⊞ - Specify the temporal connection to the TouchEngine instance.
* Synchronized `synced` - Time is strictly synchronized between the Engine COMP and the TouchEngine instance.
* Independent `independent` - The TouchEngine instance runs according to its own internal clock.
Match Local Component Rate `matchrate` - When on, the component will be cooked in TouchEngine at the same rate as the Engine COMP.
Frames per Second `fps` - The framerate for cooking the component in TouchEngine.
Wait for Render `wait` - When enabled, if a frame takes a long time to cook in TouchEngine the Engine COMP will wait during cooking rather than dropping the late frame.
This behaviour is affected by the size of the output buffer: eg if Out Buffer Frames is 4, the Engine COMP will wait for the 4th most recent frame to complete.

Render Timeout `timeout` - When waiting for a frame, TouchEngine will give up waiting after this many milliseconds.
In Buffer Auto `inauto` - Automatically manage the number of input frames queued.
In Buffer Frames `inframes` - The number of input frames to queue before passing them to the TouchEngine instance.
To accommodate potential fluctuations in time-slice in the TouchEngine instance, CHOP inputs must send a number of frames ahead of time.

Out Buffer Auto `outauto` - Automatically manage the number of output frames queued.
Out Buffer Frames `outframes` - The number of output frames to queue after receiving them from the TouchEngine instance.
To accommodate potential fluctuations in time-slice in the Engine COMP, CHOP outputs must send a number of frames ahead of time.

  

## Parameters - InitStart Page
Pre-Roll `preroll` - At initialization, run for this long before entering the ready state.
Pre-Roll Units `prerollunits` - ⊞ - The units in which the Pre-Roll is measured.
* F `frames` - The Pre-Roll is measured in frames.
* S `seconds` - The Pre-Roll is measured in seconds.
Ready when `readywhen` - ⊞ - Specify when the Engine COMP will go into the ready state.
* Component Loaded `loaded` - The Engine COMP will go into the ready state when TouchEngine has loaded the component.
* Output Buffered `buffered` - The Engine COMP will go into the ready state when TouchEngine has loaded the component and sufficient frames have been cooked to fill the input and output buffers.
* Component Running `running` - The Engine COMP will go into the ready state when TouchEngine has loaded the component, sufficient frames have been cooked to fill the input and output buffers and the component is running.
Start when Initialized `startoninit` - When enabled, playback will start as soon as the component has initialized and is in the ready state.
Initialize `initialize` - Reload the .tox file, restarting the TouchEngine instance.
Start `start` - Starts playback of the component in the TouchEngine instance.
Play `play` - Turn cooking in the TouchEngine instance on or off.
Go to Done `gotodone` - Puts the Engine COMP in the done state.
On Done `ondone` - ⊞ - Determines the actions taken, if any, when the Engine COMP enters the done state.
* Do Nothing `donothing` - Apart from the state change, nothing happens and TouchEngine continues to run the component.
* Pause `pause` - Playback of the loaded component is paused.
* Unload `unload` - The loaded component is unloaded.
* Re-Initialize `reinit` - The loaded component is unloaded and then initialization takes place.
* Re-Start `restart` - The component remains loaded and playback begins again.
* Quit Engine Process `quit` - TouchEngine is completely shut down.
  

## Parameters - Advanced Page
On Engine COMP Create `oncompcreate` - ⊞ - Specify what happens when the Engine COMP is created, for example when the project is loaded.
* Do Nothing `nothing` - Nothing happens when the Engine COMP is created.
* Launch Engine `launch` - TouchEngine is started when the Engine COMP is created. Any specified component is not loaded.
* Load and Initialize `initialize` - TouchEngine is started and any specified component is loaded and the Engine COMP is initialized and put into the ready state.
Launch Engine Process `launch` - Starts the TouchEngine process if it is not running.
Quit Engine Process `quit` - Stops the TouchEngine process if it is running.
  

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
Extra Information for the Engine COMP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific Engine COMP Info Channels
* input\_buffer\_frames - The number of frames in the input buffer. This is affected by parameters on the Tune parameter page.
  

* output\_buffer\_frames - The number of frames in the output buffer. This is affected by parameters on the Tune parameter page.
  

* output\_cook\_abs\_frame - The value of cook\_abs\_frame when the current output was cooked. This is affected by the number of frames in the output buffer.
  

* output\_did\_wait - 1 when the Engine COMP waited for output to cook. This will only be 1 when Wait for Render is On and is affected by the time taken to complete a frame in TouchEngine and the number of input and output buffers. See the Tune parameter page for more details.
  

* initializing - 1 while the Engine COMP is in the initializing state.
  

* initialize\_fail - 1 if an error occurred during initialization. This would normally indicate an error loading the component in TouchEngine.
  

* ready - 1 after initialization completes and before starting.
  

* running - 1 after starting and until the Engine COMP enters the done state or is re-initialized.
  

* done - 1 when the Engine COMP is in the done state.
  

* timer\_seconds - In the Engine COMP, this matches playing\_seconds.
  

* playing\_seconds - Seconds elapsed since starting, accounting for play state.
  

* running\_seconds - Seconds elapsed since starting.
  

* engine\_launching - 1 when TouchEngine is starting, prior to loading any component.
  

* engine\_running - 1 when TouchEngine has started and is running.
  

* engine\_none - 1 when TouchEngine is not running.
  

* engine\_error - 1 when TouchEngine has encountered an error unrelated to the component.
  

* component\_loading - 1 when TouchEngine is loading a component.
  

* component\_loaded - 1 when TouchEngine has successfully loaded a component.
  

* component\_unloading - 1 when TouchEngine is unloading a component.
  

* component\_none - 1 when TouchEngine has no loaded component.
  

* component\_error - 1 when TouchEngine encountered an error loading or running a component.
  

* crash\_reload\_count - The number of times the component has been reloaded due to an error when Reload on Crash is On.
  

* engine\_absolute\_frame - The value for absolute time in frames in TouchEngine.
  

* engine\_absolute\_seconds - The value for absolute time in seconds in TouchEngine.
  

* engine\_fps - The number of frames rendered in the last second in TouchEngine.
  

* engine\_frame\_msec - Amount of time each frame takes to cook in msec in TouchEngine.
  

* engine\_cook - Is equal to 1 when a frame is cooked and equal to 0 when a frame is skipped in TouchEngine.
  

* engine\_dropped\_frames - The number of frames dropped between the last frame and the current frame in TouchEngine.
  

* engine\_read\_ahead\_misses - How many times the movie read ahead failed to maintain the number of specified Read Ahead frames in TouchEngine.
  

* engine\_gpu\_mem\_used - Amount of GPU memory used in TouchEngine (in megabytes).
  

* engine\_total\_gpu\_mem - Total amount of GPU memory available on the system (in megabytes).
  

* engine\_active\_ops - How many OPs are actively cooking in TouchEngine.
  

* engine\_deactivated\_ops - Number of calls to cook a component that has its Cooking Flag turned off in TouchEngine.
  

* engine\_total\_ops - Total number of OPs in TouchEngine.
  

* engine\_cpu\_mem\_used - Amount of CPU memory used in TouchEngine (in megabytes).
  

* engine\_cookstate - Monitors which frames actually cooked in TouchEngine.
  

* engine\_cookrealtime - Monitors the state of the realtime flag, determining if TouchEngine is running in realtime mode or not.
  

* engine\_cookrate - The global target cook rate (frames per second) of TouchEngine. This is the frames per second of the root component, root.time.rate, typically 60, though due to frames taking too long to cook, the actual frames per second may be lower.
  

* engine\_timeslice\_step - The number of frames that TouchEngine stepped forward for the current cook. It's the length of the Time Slice in frames. It will be equal to 1 when the system is taking 1000/root.time.rate msec or less to complete one frame (16.666 msec for a rate of 60).
  

* engine\_timeslice\_msec - The length of the current Time Slice in milliseconds.
  

* engine\_active\_expressions - The number of active python expressions found in TouchEngine.
  

* engine\_active\_expressions - The number of python expressions that have been optimized in TouchEngine.
  

* engine\_cached\_expressions - The number of python expressions that have been cached in TouchEngine.
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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditormw-replace2023.112802022.241402021.100002020.200002019.146502018.28070before 2018.28070
| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • [Animation](Animation_COMP.html "Animation COMP") • [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • [Constraint](Constraint_COMP.html "Constraint COMP") • [Container](Container_COMP.html "Container COMP") • Engine• [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • [FBX](FBX_COMP.html "FBX COMP") • [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • [Geo Text](Geo_Text_COMP.html "Geo Text COMP") • [Geometry](Geometry_COMP.html "Geometry COMP") • [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • [Impulse Force](Impulse_Force_COMP.html "Impulse Force COMP") • [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Palette:depthProjection](Palette_depthProjection.html "Palette:depthProjection") • [Parameter](Parameter_COMP.html "Parameter COMP") • [Replicator](Replicator_COMP.html "Replicator COMP") • [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • [Text](Text_COMP.html "Text COMP") • [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • [Window](Window_COMP.html "Window COMP") |
An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

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

There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Indicator of certain states of an operator (bypass, display, lock, viewer active).

A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.

Retrieved from "<https://docs.derivative.ca/index.php?title=Engine_COMP&oldid=33646>"
[Category](Special_Categories.html "Special:Categories"):
* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")