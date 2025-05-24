

Render Pick CHOP - TouchDesigner Documentation




# Render Pick CHOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Render Pick CHOP samples a rendering (from a [Render TOP](Render_TOP.html "Render TOP") or a [Render Pass TOP](Render_Pass_TOP.html "Render Pass TOP")) and returns 3D information from the geometry at that particular pick location. Values sampled can include position, normals, point color, texture coordinates, depth and the object's path. An [Info DAT](Info_DAT.html "Info DAT") should be used to retrieve the object's path.
The pick location is specified through uv coordinates of the rendering. These uv coordinates can be selected by clicking on a [Panel Component](Panel_Component.html "Panel Component") or explicitly setting them in the U and V parameters in the Render Pick CHOP.
Along with the geometric data returned, this node has two channels 'picked' and 'trigger' that inform the picked status. 'picked' will be 1 when an object has been found at the search location. 'trigger' will be 1 when both an object has been found, and the 'Picking By' condition has been met. That is, either the 'Panel Value' is 1, or the 'Select' parmeter is 'On.
See also the multi-sample [Render Pick DAT](Render_Pick_DAT.html "Render Pick DAT").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[renderpickCHOP\_Class](https://docs.derivative.ca/RenderpickCHOP_Class "RenderpickCHOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Render Pick Page](#Parameters_-_Render_Pick_Page)
* [3 Parameters - Options Page](#Parameters_-_Options_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common CHOP Info Channels](#Common_CHOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Render Pick Page
Strategy `strategy` - ⊞ - Decides when to update values based on pick interactions.
* While Select `select` -
* Hold First Picked `holdfirst` - Holds the values first returned when geometry picked.
* Hold Last Picked `holdlast` - Holds the values last returned when geometry picked. This differs from the Continuous strategy in that it will hold the last values picked on geometry if the pick starts sampling empty space (no geometry in that part of the scene). Alternatively, using the Continuous strategy the values will be cleared to zero if the pick starts sampling empty space.
* Always `always` -
Clear Previous Pick on New Pick `clearprev` - This parameter is only enabled when the Strategy is set to Hold Last Picked. When this is on, starting a new pick on empty space will clear the values. When off, the last values will be held if the pick starts on empty space.
Response Time `responsetime` - ⊞ - Determines when the values are updated.
* Next Cook (Faster) `nextcook` - The values are captured on the current frame and updated next frame. Results are from the previous frame, but much faster cook times.
* This Cook (Slower) `thiscook` - The values are captured and updated in the current frame.
Pick Radius `pickradius` - Controls the radius of the search area for the pick. If nothing is found at the pick's center it will keep searching for geometry in the search area defined by the Pick Radius.
Pick Radial Step `pickradstep` - Used to reduce the searching within the search area. The search area is sampled at locations that correspond to 'spokes' outwards from the center pick point.
Pick Circular Step `pickcirstep` - Used to reduce the searching within the search area. The search area is sampled at locations that correspond to 'rings' outwards from the center pick point.
Render/RenderPass TOP `rendertop` - Specifies which render to sample.
Use Pickable Flags `usepickableflags` - When turned on only geometry whose [Pickable Flag](Flag.html "Flag") is on can be selected by the Render Pick CHOP. The [Pickable Flag](Pickable_Flag.html "Pickable Flag") is found on all [Object](Object.html "Object") components.
Include Non-Pickable Objects `includenonpickable` - Includes the non-pickable objects in the picking algorithm such that non-pickable objects may occlude pickable objects. For example, if there is only one pickable object in the scene with lots of additional non-pickable geometry is present, turning this parameter on will prevent the pickable object from being selected if it is behind a non-pickage object (occluded by the non-pickage object).
Picking by `pickingby` - ⊞ - Determines how the pick location is set.
* Panel `panel` - Uses the Panel Component scoped in the **Panel** parameter. The uv position of the mouse on this component's control panel will be the uv position in the render that is sampled. The pick is active when the panel value specified by the **Panel Value** parameter is 1.
* Parameters `parameters` - Uses the **U**, **V**, and **Pick** parameters below for picking.
Panel `panel` - Specifies which panel component to use when picking by panel.
Panel Value `panelvalue` - Specifies with panel value to use to trigger the pick when picking by panel.
U `picku` - Sets the u coordinate when picking by parameters.
V `pickv` - Sets the v coordinate when picking by parameters.
Select `select` - When picking by parameters, picking is active when this parameter = 1.
Activate Callbacks `activatecallbacks` - Enables Callback DAT for each pick event.
Callbacks DAT `callbacks` - Path to a DAT containing callbacks for pick event received.
  

## Parameters - Options Page
Fetch Position `position` - ⊞ - Returns the position of the point picked on the geometry. Channels *tx, ty, tz*.
* No `no` - Do not return position values.
* In SOP Space `sopspace` - Return position of point picked in SOP transform space.
* In World Space `worldspace` - Return position of point picked in world transform space.
* In Camera Space `cameraspace` - Return position of point picked in camera transform space.
* Relative to Object `relativetoobj` - Return position of point picked relative to object specified in **Reference Object** parameter.
Fetch Normal `normal` - ⊞ - Returns the normals of the point picked on the geometry. Channels *nx, ny, nz*.
* No `no` - Do not return normal values.
* In SOP Space `sopspace` - Return normals of point picked in SOP transform space.
* In World Space `worldspace` - Return normals of point picked in world transform space.
* In Camera Space `cameraspace` - Return normals of point picked in camera transform space.
* Relative to Object `relativetoobj` - Return normals of point picked relative to object specified in **Reference Object** parameter.
Reference Object `referenceobj` - Object used when fetching position or normals **Relative to Object**.
Fetch Point Color `color` - Returns the point color of the point picked on the geometry. Channels *cr, cg, cb, ca*.
Fetch Texture UV `uv` - Returns the texture coordinates of the point picked on the geometry. Channels *mapu, mapv, mapw*.
Fetch Object Path `path` - Return the path to the object that is picked. This result requires and [Info DAT](Info_DAT.html "Info DAT") with its **Node Path** parameter referecning the Render Pick CHOP.
Fetch Depth `depth` - Returns the depth of the point picked on the geometry. This value a non-linear ratio of the point's position between the near and far planes of the [Depth Buffer](https://docs.derivative.ca/index.php?title=Depth_Buffer&action=edit&redlink=1 "Depth Buffer (page does not exist)"). Channel is *depth*.
Fetch Instance ID `instanceid` - Returns the Instance ID of the object. This will always be 0 if instancing is off. Channel is *instance*.
Custom Attrib 1 `customattrib1` - Specify which custom attributes to return from the object.
Custom Attrib 1 Type `customattrib1type` - The type of attribute is selected from this menu.
Custom Attrib 2 `customattrib2` - Specify which custom attributes to return from the object.
Custom Attrib 2 Type `customattrib2type` - The type of attribute is selected from this menu.
Custom Attrib 3 `customattrib3` - Specify which custom attributes to return from the object.
Custom Attrib 3 Type `customattrib3type` - The type of attribute is selected from this menu.
Custom Attrib 4 `customattrib4` - Specify which custom attributes to return from the object.
Custom Attrib 4 Type `customattrib4type` - The type of attribute is selected from this menu.
  

## Parameters - Common Page
Time Slice `timeslice` - Turning this on forces the channels to be "[Time Sliced](Time_Slicing.html "Time Slicing")". A Time Slice is the time between the last cook frame and the current cook frame.
Scope `scope` - To determine which channels get affected, some CHOPs use a Scope string on the Common page.
Sample Rate Match `srselect` - ⊞ - Handle cases where multiple input CHOPs' sample rates are different. When Resampling occurs, the curves are interpolated according to the Interpolation Method Option, or "Linear" if the Interpolate Options are not available.
* Resample At First Input's Rate `first` - Use rate of first input to resample others.
* Resample At Maximum Rate `max` - Resample to the highest sample rate.
* Resample At Minimum Rate `min` - Resample to the lowest sample rate.
* Error If Rates Differ `err` - Doesn't accept conflicting sample rates.
Export Method `exportmethod` - ⊞ - This will determine how to connect the CHOP channel to the parameter. Refer to the [Export](Export.html "Export") article for more information.
* DAT Table by Index `datindex` - Uses the docked DAT table and references the channel via the index of the channel in the CHOP.
* DAT Table by Name `datname` - Uses the docked DAT table and references the channel via the name of the channel in the CHOP.
* Channel Name is Path:Parameter `autoname` - The channel is the full destination of where to export to, such has `geo1/transform1:tx`.
Export Root `autoexportroot` - This path points to the root node where all of the paths that exporting by **Channel Name is Path:Parameter** are relative to.
Export Table `exporttable` - The DAT used to hold the export information when using the DAT Table Export Methods (See above).
  

## Info CHOP Channels
Extra Information for the Render Pick CHOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Common CHOP Info Channels
* start - Start of the CHOP interval in samples.
* length - Number of samples in the CHOP.
* sample\_rate - The samplerate of the channels in frames per second.
* num\_channels - Number of channels in the CHOP.
* time\_slice - 1 if CHOP is Time Slice enabled, 0 otherwise.
* export\_sernum - A count of how often the export connections have been updated.
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
| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • Render Pick• [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • [Transform](Transform_CHOP.html "Transform CHOP") • [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The internal states of a panel component are Panel Values, and are accessed with a Panel CHOP, a `OP.panel` Python expression, or a [Panel Execute DAT](Panel_Execute_DAT.html "Panel Execute DAT").

To re-compute the output data of the [Operators](Operator.html "Operator"). An operator cooks when (1) its inputs change, (2) its [Parameters](Parameter.html "Parameter") change, (3) when the timeline moves forward in some cases, or (4) [Scripting](Script.html "Script") commands are run on the node. When the operator is a [Panel Component](Panel_Component.html "Panel Component"), it also cooks when a user interacts with it. When an operator cooks, it usually causes operators connected to its output to re-cook. When TouchDesigner draws the screen, it re-cooks all the [Dependencies](Dependency.html "Dependency") - the necessary operators in all [Networks](Network.html "Network"), contributing to a frame's total "cook time".

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").

The sub-[Family](Operator_Family.html "Operator Family") of [Components](Component.html "Component") that are used to create custom interactive 2D control [panels](Panel.html "Panel") (Container, Widget, Text COMP Slider, Button, etc.).

Some operators have a DAT [docked](Docking.html "Docking") to them that contains some python functions. These functions, called "callbacks", get called when something in the operator changes.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").
The grey dashed lines between nodes is a Reference (or [Link](Link.html "Link")). A Reference is (1) a [Parameter Reference](Parameter_Reference.html "Parameter Reference"), a parameter in an OP that is a name or path to another operator, (2) a [Node Reference](https://docs.derivative.ca/index.php?title=Node_Reference&action=edit&redlink=1 "Node Reference (page does not exist)"), an expression in a parameter or DAT script that contains the name or path of another operator, (3) a DAT Cell Reference or (4) a CHOP Channel Reference.
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

(1) A [Geometry Component](Geometry_COMP.html "Geometry COMP") can instance and render its SOP geometry many times: once for each sample in a CHOP, row of a DAT table, pixel in a TOP, or point of a SOP, (2) An instance is an OP that doesn't actually have its own data, but rather just refers to an OP (or has an input) whose data it uses. This includes Null OPs, Switch OPs and in some cases Select OPs.

A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.

A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.

samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.

TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.

Retrieved from "<https://docs.derivative.ca/index.php?title=Render_Pick_CHOP&oldid=24154>"
[Category](Special_Categories.html "Special:Categories"):
* [CHOPs](Category_CHOPs.html "Category:CHOPs")