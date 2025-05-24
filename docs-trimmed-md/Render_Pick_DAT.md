

Render Pick DAT - TouchDesigner Documentation




# Render Pick DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Render Pick DAT lets you get information about the 3D surface at any pixel of any 3D render, allowing you to implement multi-touch on a 3D rendered scene. It samples a rendering (from a [Render TOP](Render_TOP.html "Render TOP") or a [Render Pass TOP](Render_Pass_TOP.html "Render Pass TOP")) and returns 3D information from the geometry at the specified pick locations.
You feed it a DAT with minimum three columns: `select`, `u` and `v`. A [Multi Touch In DAT](Multi_Touch_In_DAT.html "Multi Touch In DAT") is usually connected to the Render Pick DAT, where the Multi Touch In DAT points to a container that is displaying the output of the Render TOP.
  
You can pick from multiple cameras simultaneously. You can specify a `camera` which allows the pick to occur from the point of a view other than the first camera listed in the [Render TOP](Render_TOP.html "Render TOP"). The value in the column can either be a path (relative to the Render Pick DAT, or absolute) to a Camera COMP, or it can be an integer index, started at 0. If it's an index it will select the camera to use if there are multiple cameras listed in the [Render TOP](Render_TOP.html "Render TOP"), or if there are cameras listed in the 'Custom Pick Camera(s)' parameter. This is useful for various [Multi-Camera Rendering](Multi-Camera_Rendering.html "Multi-Camera Rendering") setups, and cases such as VR where your picking isn't coming from the point of view of your eye cameras, but instead hand controllers.
The pick location is a u,v (horizontal, vertical) coordinate placed in the table that you connect to the Render Pick DAT input. Each row of the input table represents one pick point to be sampled, except for the first row which contains column headings `select`, `u` and `v` (plus any other unused columns you want). The `select`, `u` and `v` columns are what you would get from a [Panel CHOP](Panel_CHOP.html "Panel CHOP"). The u and v values goes 0 to 1 left to right and bottom to top, no matter what the aspect ratio of the render is.
When Strategy is Always, that u,v location is always sampled and the results are displayed in the corresponding row in the Render Pick DAT output.
The output table will show the path of the geometry that was picked, its position (in a choice of reference frames), surface normal (excluding bump mapping), distance from camera, texture UV coordinate, color, alpha and instance id. It properly picks surfaces with deforming vertices.
There are some examples here:
* [geoPanel](Palette_geoPanel.html "Palette:geoPanel") in the palette.
* [multiTouch](Palette_multiTouch.html "Palette:multiTouch") in the palette under Techniques.
* [Render Pick DAT Example](http://www.derivative.ca/Forum/viewtopic.php?f=22&t=166&p=13447).
See also the single-sample [Render Pick CHOP](Render_Pick_CHOP.html "Render Pick CHOP").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[renderpickDAT\_Class](https://docs.derivative.ca/RenderpickDAT_Class "RenderpickDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Render Pick Page](#Parameters_-_Render_Pick_Page)
* [3 Parameters - Options Page](#Parameters_-_Options_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Render Pick Page
Strategy `strategy` - ⊞ - Decides when to update values based on pick interactions.
* While Select `select` - Continuously updates values when being selected/picked.
* Hold First Picked `holdfirst` - Holds the values first returned when geometry picked.
* Hold Last Picked `holdlast` - Holds the values last returned when geometry picked. This differs from the Continuous strategy in that it will hold the last values picked on geometry if the pick starts sampling empty space (no geometry in that part of the scene). Alternatively, using the Continuous strategy the values will be cleared to zero if the pick starts sampling empty space.
* Always `always` - Continuously updates values at the location picked.
Clear Previous Pick on New Pick `clearprev` - This parameter is only enabled when the Strategy is set to Hold Last Picked. When this is on, starting a new pick on empty space will clear the values. When off, the last values will be held if the pick starts on empty space.
Response Time `responsetime` - ⊞ - Determines when the values are updated.
* Next Cook (Faster) `nextcook` - The values are captured on the current frame and updated next frame. Results are from the previous frame, but much faster cook times.
* This Cook (Slower) `thiscook` - The values are captured and updated in the current frame.
Pick Radius `pickradius` - Controls the radius of the search area for the pick. If nothing is found at the pick's center it will keep searching for geometry in the search area defined by the Pick Radius.
Pick Radial Step `pickradstep` - Used to reduce the searching within the search area. The search area is sampled at locations that correspond to 'spokes' outwards from the center pick point.
Pick Circular Step `pickcirstep` - Used to reduce the searching within the search area. The search area is sampled at locations that correspond to 'rings' outwards from the center pick point.
Render/RenderPass TOP `rendertop` - Specifies which scene to pick on, and which camera to pick from. By default the first camera listed in the [Render TOP](Render_TOP.html "Render TOP") will be used for picking. Another camera can be specified with the 'Custom Pick Camera(s)' parameter, and multiple different cameras can be selected using the `camera` input column.
Custom Pick Camera(s) `custompickcameras` - Picking can be done from the viewport of custom camera(s) by specifying one or more [Camera COMP](Camera_COMP.html "Camera COMP") here. If this parameter is blank the cameras from the Render TOP are used. To pick from the viewpoint of multiple different cameras, a `camera` column must be specified in the input DAT.
Allow Multi-Camera Rendering `allowmulticamera` - [Multi-Camera Rendering](Multi-Camera_Rendering.html "Multi-Camera Rendering") is a faster way to render multiple passes at the same time, and is thus a speed improvement for doing many picks at the same time. This feature may not work correctly for some older [GLSL MATs](GLSL_MAT.html "GLSL MAT") made in 088 though, so this parameter allows forcing off this speed improvement if necessary. Generally it should be left on though.
Use Pickable Flags `usepickableflags` - When turned on only geometry whose [Pickable Flag](Flag.html "Flag") is on can be selected by the Render Pick DAT. The Pickable Flag is found on all [Object](Object.html "Object") components.
Include Non-Pickable Objects `includenonpickable` - Includes the non-pickable objects in the picking algorithm such that non-pickable objects may occlude pickable objects. For example, if there is only one pickable object in the scene with lots of additional non-pickable geometry is present, turning this parameter on will prevent the pickable object from being selected if it is behind a non-pickage object (occluded by the non-pickage object).
Merge Input DAT `mergeinputdat` - Appends input table to the Render Pick DATs columns.
Activate Callbacks `activatecallbacks` - Enables Callback DAT for each pick event.
Callbacks DAT `callbacks` - Path to a DAT containing callbacks for pick event received.
  

## Parameters - Options Page
Fetch Position `position` - ⊞ - Returns the position of the point picked on the geometry. Columns *tx, ty, tz*.
* No `no` - Do not return position values.
* In SOP Space `sopspace` - Return position of point picked in SOP transform space.
* In World Space `worldspace` - Return position of point picked in world transform space.
* In Camera Space `cameraspace` - Return position of point picked in camera transform space.
* Relative to Object `relativetoobj` - Return position of point picked relative to object specified in **Reference Object** parameter.
Fetch Normal `normal` - ⊞ - Returns the normals of the point picked on the geometry. Columns *nx, ny, nz*.
* No `no` - Do not return normal values.
* In SOP Space `sopspace` - Return normals of point picked in SOP transform space.
* In World Space `worldspace` - Return normals of point picked in world transform space.
* In Camera Space `cameraspace` - Return normals of point picked in camera transform space.
* Relative to Object `relativetoobj` - Return normals of point picked relative to object specified in **Reference Object** parameter.
Reference Object `referenceobj` - Object used when fetching position or normals **Relative to Object**.
Fetch Point Color `color` - Returns the point color of the point picked on the geometry. Columns *cr, cg, cb, ca*.
Fetch Texture UV `uv` - Returns the texture coordinates of the point picked on the geometry. Columns *mapu, mapv, mapw*.
Fetch Depth `depth` - Returns the depth of the point picked on the geometry. This value a non-linear ratio of the point's position between the near and far planes of the [Depth Buffer](https://docs.derivative.ca/index.php?title=Depth_Buffer&action=edit&redlink=1 "Depth Buffer (page does not exist)"). Column is *depth*.
Fetch Instance ID `instanceid` - Returns the Instance ID of the object. This will always be 0 if instancing is off. Column is *instance*.
Custom Attrib 1 `customattrib1` - Specify which custom attributes to return from the object.
Custom Attrib 1 Type `customattrib1type` - The type of attribute is selected from this menu.
Custom Attrib 2 `customattrib2` - Specify which custom attributes to return from the object.
Custom Attrib 2 Type `customattrib2type` - The type of attribute is selected from this menu.
Custom Attrib 3 `customattrib3` - Specify which custom attributes to return from the object.
Custom Attrib 3 Type `customattrib3type` - The type of attribute is selected from this menu.
Custom Attrib 4 `customattrib4` - Specify which custom attributes to return from the object.
Custom Attrib 4 Type `customattrib4type` - The type of attribute is selected from this menu.
  

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
Extra Information for the Render Pick DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • Render Pick• [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • [Serial](Serial_DAT.html "Serial DAT") • [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

To re-compute the output data of the [Operators](Operator.html "Operator"). An operator cooks when (1) its inputs change, (2) its [Parameters](Parameter.html "Parameter") change, (3) when the timeline moves forward in some cases, or (4) [Scripting](Script.html "Script") commands are run on the node. When the operator is a [Panel Component](Panel_Component.html "Panel Component"), it also cooks when a user interacts with it. When an operator cooks, it usually causes operators connected to its output to re-cook. When TouchDesigner draws the screen, it re-cooks all the [Dependencies](Dependency.html "Dependency") - the necessary operators in all [Networks](Network.html "Network"), contributing to a frame's total "cook time".

Rendering is the creation of a 3D image with the Render TOP. Rendering is also used more generally to include the compositing (with TOPs) to generate an output image.

Indicator of certain states of an operator (bypass, display, lock, viewer active).

Some operators have a DAT [docked](Docking.html "Docking") to them that contains some python functions. These functions, called "callbacks", get called when something in the operator changes.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").
The grey dashed lines between nodes is a Reference (or [Link](Link.html "Link")). A Reference is (1) a [Parameter Reference](Parameter_Reference.html "Parameter Reference"), a parameter in an OP that is a name or path to another operator, (2) a [Node Reference](https://docs.derivative.ca/index.php?title=Node_Reference&action=edit&redlink=1 "Node Reference (page does not exist)"), an expression in a parameter or DAT script that contains the name or path of another operator, (3) a DAT Cell Reference or (4) a CHOP Channel Reference.
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

(1) A [Geometry Component](Geometry_COMP.html "Geometry COMP") can instance and render its SOP geometry many times: once for each sample in a CHOP, row of a DAT table, pixel in a TOP, or point of a SOP, (2) An instance is an OP that doesn't actually have its own data, but rather just refers to an OP (or has an input) whose data it uses. This includes Null OPs, Switch OPs and in some cases Select OPs.

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=Render_Pick_DAT&oldid=24335>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")