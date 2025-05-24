

Spring SOP - TouchDesigner Documentation




# Spring SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Spring SOP deforms and moves the input geometry using spring "forces" on the edges of polygons and on masses attached to each point.
Geometry is deformed using forces that simulate simple physics on the points and edges. A simulated "mass" is assigned to each point. Its primitive edges act as "springs" which oppose the forces, and pull the points back toward their original positions. When the springs are stretched by the forces, they try to pull the points back. The points do not stop moving when they return to their original positions, however, but continue to oscillate because of their mass, until the oscillation dies out.
Forces which act upon the points are as follows:
external force (gravity)
wind (similar to external force)
turbulence (chaotic forces)
The greater the drag value, or smaller the mass, the faster the oscillation dies out.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[springSOP\_Class](https://docs.derivative.ca/SpringSOP_Class "SpringSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - State Page](#Parameters_-_State_Page)
* [3 Parameters - Forces Page](#Parameters_-_Forces_Page)
* [4 Parameters - Nodes Page](#Parameters_-_Nodes_Page)
* [5 Parameters - Limits Page](#Parameters_-_Limits_Page)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - State Page
Preroll Time `timepreroll` - How many seconds of the simulation to bypass, after the reset time is reached. For example, if you put the number 33 into this field (and reset is at `$TSTART`), frame one will show the simulation that was at a time of 33 seconds. In other words, the first thirty-two seconds have been bypassed, and the time at thirty-three seconds is shifted to frame one. The first thirty-two seconds must still be calculated in order to compute the status of the points, so you will notice some delay upon reset.
Time Inc `timeinc` - The Time Inc parameter determines how often to cook the SOP. By default, this parameter is set to `1/$FPS`. This means that the SOP will cook once for every frame. When complex dynamics are involved, the SOP may require more frequent cooking for increased mathematical accuracy. To get sub-frame accuracy in the cooking, set the Time Inc to something smaller than `1/$FPS` . For example, setting the Time Inc to `0.5/$FPS` will mean that the SOP gets cooked twice for every frame.
**Note:** Never set this parameter greater than `1/$FPS`.

Accurate Moves `accurate` - This option makes the nodes move more accurately between frames by calculating their trajectories for fractional frame values.
Attractor Use `attractmode` - ⊞ - Describes how attractor points are assigned to each particle.
* All Points `all` - All point attractors affect all particles (or points).
* Single Point per Particle `single` - When enabled, each particle is assigned a single attractor point, and is affected by only that point. Assignment is done by point number modulo the total number of attractor points.
Reset `reset` - While On resets the spring effect of the SOP.
Reset Pulse `resetpulse` - Instantly reset the spring effect.
  

## Parameters - Forces Page
External Force `external` - ⊞ - Forces of gravity acting on the points. When drag is zero, the points can accelerate with no limit on their speed.
* X `externalx` -
* Y `externaly` -
* Z `externalz` -
Wind `wind` - ⊞ - Wind forces acting on the points. Similar to external force. Using wind (and no other forces, such as turbulence), the points will not exceed the wind velocity.
* X `windx` -
* Y `windy` -
* Z `windz` -
Turbulence `turb` - ⊞ - The amplitude of turbulent (chaotic) forces along each axis. Use positive values, if any.
* X `turbx` -
* Y `turby` -
* Z `turbz` -
Turb Period `period` - A small period means that the turbulence varies quickly over a small area, while a larger value will cause points close to each other to be affected similarly.
Seed `seed` - Random number seed for the simulation.
  

## Parameters - Nodes Page
Fixed Points `fixed` - This is a point group. All points in the point group will remain unaffected by the forces. Also see the [Group SOP](Group_SOP.html "Group SOP") for notes on how to specify point ranges.
Fixed Points go to Source Positions `revertfixed` - Determines whether or not points in the Fixed Points group should be moved to the positions of the corresponding points in the Source geometry.
Copy Groups from Source `copygroups` - Determines if the Spring SOP should copy groups from the Source geometry at each frame. This lets you specify the name of an animating group in the Fixed Points field, and the contents of this group will be kept up to date.
Add Mass Attribute `domass` - When selected, the Mass is computed for the deforming geometry.
Mass `mass` - Mass of each point. Heavier points take longer to get into motion, and longer to stop.
Add Drag Attribute `dodrag` - When selected, the geometry is deformed by the Drag attribute.
Drag `drag` - Drag of each point.
Spring Behavior `springbehavior` - ⊞ - How the springs will behave:
* Hooke's Law `hooke` - Springs will work according to Hooke's Law. This is generally more stable than Normalized Displacement.
**Hooke's Law**: Force = Displacement Spring constant
* Normalize Displacement `normalize` - Similar to Hooke's Law except that the displacement is normalized to the original length of the Spring.
Spring Constant `springk` - The spring constant. How tight the springs are. Increase this value to make the springs tighter and thus make the object more rigid. As this number becomes higher, the springs can oscillate out of control. Decrease the Time Inc if this happens.
Initial Tension `tension` - The Initial k constant of the geometry before being deformed by the spring operation.
  

## Parameters - Limits Page
+ Limit Plane `limitpos` - ⊞ - The points will bounce off the limit planes when it reaches them. The six limit plane fields define a bounding cube. The default settings are one thousand units away, which is very large. Reduce the values to about one to see the effect.
* X `limitposx` -
* Y `limitposy` -
* Z `limitposz` -
- Limit Plane `limitneg` - ⊞ - The points will bounce off the limit planes when it reaches them. The six limit plane fields define a bounding cube. The default settings are one thousand units away, which is very large. Reduce the values to about one to see the effect.
* X `limitnegx` -
* Y `limitnegy` -
* Z `limitnegz` -
Hit Behavior `hit` - ⊞ - Control over what happens when the geometry hits either the six collision planes or the collision object. The options are:
* Bounce on Contact `bounce` - Geometry will bounce upon contact with the Collision input.
* Stick on Contact `stick` - Geometry will stick to the Collision input upon contact.
Gain Tangent `gaintan` - Friction parameters which can be regarded as energy-loss upon collision. The first parameter affects the energy loss (gain) perpendicular to the surface. 0 means all energy (velocity) is lost, 1 means no energy is lost perpendicular to surface. The second parameter is the energy gain tangent to the surface.
Gain Normal `gainnorm` - Friction parameters which can be regarded as energy-loss upon collision. The first parameter affects the energy loss (gain) perpendicular to the surface. 0 means all energy (velocity) is lost, 1 means no energy is lost perpendicular to surface. The second parameter is the energy gain tangent to the surface.
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
* Input 2:  -
  

## Info CHOP Channels
Extra Information for the Spring SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Common SOP Info Channels
* num\_points - Number of points in this SOP.
* num\_prims - Number of primitives in this SOP.
* num\_particles - Number of particles in this SOP.
* last\_vbo\_update\_time - Time spent in another thread updating geometry data on the GPU from the SOP's CPU data. As it is part of another thread, this time is not part of the usual frame time.
* last\_meta\_vbo\_update\_time - Time spent in another thread updating meta surface geometry data (such as metaballs or nurbs) on the GPU from the SOP's CPU data. As it is part of another thread, this time is not part of the usual frame time.
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
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • Spring• [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Spring_SOP&oldid=27192>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")