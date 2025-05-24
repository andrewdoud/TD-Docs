

Particle SOP - TouchDesigner Documentation




# Particle SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Particle SOP is used for creating and controlling motion of "particles" for particle systems simulations. Particle systems are often used to create simulations of natural events such as rain and snow, or effects such as fireworks and sparks. In Touch, the points of the input geometry are used as the starting positions of the particles. Each point of the input can be affected by external force (gravity) and wind. Particles can collide and bounce off another object, set by the Collision Source. They can also bounce off, or die at, limit planes set in X, Y and Z.
Particles are created with an initial velocity/direction that comes from the source geometry’s point normals, and that velocity can be controlled by modifying the normals using, for instance, a [Point SOP](Point_SOP.html "Point SOP"), [Facet SOP](Facet_SOP.html "Facet SOP") or [Script SOP](Script_SOP.html "Script SOP"). A point with a Normal of magnitude 1 emit bear particles with a velocity of 1 unit per second in the direction of the normal.
Particles have various [Attributes](Attribute.html "Attribute") that regular geometry do not have, such as velocity, life expectancy and age. These attributes must be carried with each point in order to carry out the simulation.
The fourth input is Surface Attractors that cause the particles to be attached to areas of a surface. Each particle's id is used to determine a random target primitive, and random u,v on that primitive. That target position is used to modify the current velocity.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[particleSOP\_Class](https://docs.derivative.ca/ParticleSOP_Class "ParticleSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Parameters - State Page](#Parameters_-_State_Page)
* [4 Parameters - Forces Page](#Parameters_-_Forces_Page)
  + [4.1 Discussion - Wind vs External Force](#Discussion_-_Wind_vs_External_Force)
* [5 Parameters - Particles Page](#Parameters_-_Particles_Page)
* [6 Parameters - Limits Page](#Parameters_-_Limits_Page)
* [7 Operator Inputs](#Operator_Inputs)
* [8 Info CHOP Channels](#Info_CHOP_Channels)
  + [8.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [8.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Page
Source Group `sourcegrp` - Limit the particle emission to the points found in the specified point groups.
  

## Parameters - State Page
Particle Type `prtype` - ⊞ - Selects how the particles are rendered.
* Render as Lines `lines` - Each particle will be rendered as a 2-point line, with the length determined based on the particles velocity. If the particle has no velocity it will just be a single pixel in size.
* Render as Point Sprites `pointprites` - For use with the [Point Sprite MAT](Point_Sprite_MAT.html "Point Sprite MAT"). Each particle is a square of pixels that always face the camera. The size of the square is determined by parameters in the Point Sprite and the `pscale` vertex/point attribute. The point sprites will have texture coordinates generated for them automatically also ((0,0) in the bottom left and (1,1) in the top right).
Behavior `behave` - ⊞ - Select between emitting particles from the geometry's points or deforming the original geometry using the Particle SOP's behavior.
* Particle System `psystem` - Act like a particle system, where particles are born from the input points.
* Modify Source Geometry `modify` - Deforms the source input geometry.
**Tip:** You can also instance geometry to particles. Use a [SOP to CHOP](SOP_to_CHOP.html "SOP to CHOP") to get the particle positions into CHOPs, and on the Instance page of the [Geometry COMP](Geometry_COMP.html "Geometry COMP") to position any geometry at each particle positions. This is by far the most efficient way of animating many copies of geometry with a particle system.

Compute Normals `normals` - Creates normals on the geometry. Only used when Behaviour is set to Modify Source Geometry.
Point Reuse `ptreuse` - ⊞ - Decide how the internal memory for points is reused when a point needs to be created or when a point dies.
* Reuse Points in Loop `loop` -
* Reuse First Available Point `unused` -
* Don't Reuse Points `none` -
Preroll Time `timepreroll` - How many seconds of the simulation to bypass, after the reset time is reached. For example, if you put the number `33` into this field (and reset is at `Tstart`), frame one will show the simulation that was at a time of 33 seconds. In other words, the first thirty-two seconds have been bypassed, and the time at thirty-three seconds is shifted to frame one. The first thirty-two seconds must still be calculated in order to compute the status of the points, so you will notice some delay upon reset.
Time Inc `timeinc` - The Time Inc parameter determines how often to cook the SOP. By default, this parameter is set to `1/me.time.rate`. This means that the SOP will cook once for every frame. When complex dynamics are involved, the SOP may require more frequent cooking for increased mathematical accuracy. To get sub-frame accuracy in the cooking, set the Time Inc to something smaller than `1/me.time.rate`.
**For example:** Setting the Time Inc to `0.5/me.time.rate` will mean that the SOP gets cooked twice for every frame.
**Note:** Never set this parameter to be greater than `1/me.time.rate`.

Max Steps `maxsteps` - Limits how far back in time TouchDesigner calculates particle positions for proper interactions. If frame rates are slow this computation back in time can become high, this parameter limits that effect.
Jitter Births `jitter` - This allows you to jitter the location pixels of each particle as they are born.
Accurate Moves `accurate` - This option makes the particles move more accurately between frames by calculating their trajectories for fractional frame values.
Remove Unused Points `rmunused` - Removes all unused points from the input geometry. This is provided as an explicit option instead of automatically because it saves the time needed to purge the points from memory during the simulation. This prevents unnecessary slowdowns during the simulation.
Attractor Use `attractmode` - ⊞ - Select which mode of attraction to use for Surface Attractors.
* All Points `all` - All point attractors affect all particles (or points).
* Single Point per Particle `single` - When enabled, each particle is assigned a single attractor point, and is affected by only that point. Assignment is done by point number modulo the total number of attractor points.
Reset `reset` - When On the particle system is held in a reset state and does not emit particles.
Reset Pulse `resetpulse` - Instantly reset the particle system to its starting state.
  

## Parameters - Forces Page
External Force `external` - ⊞ - Forces of gravity acting on the particles. When drag is zero, the particles can accelerate with no limit on their speed.
* X `externalx` -
* Y `externaly` -
* Z `externalz` -
Wind `wind` - ⊞ - Wind forces acting on the particles. Similar to External Force. Using Wind (and no other forces, such as Turbulence), the particles will not exceed the wind velocity.
#### Discussion - Wind vs External Force
The application of External Force directly affects a particles' acceleration, the rate of which is determined by the mass (F = Mass Acceleration). Wind is an additional force, but one that is velocity sensitive. If a particle is already travelling at wind velocity, then it shouldn't receive any extra force from it. This implies a maximum velocity when using Wind on its own.
An increase in mass impedes acceleration for a given constant force. Drag is a force opposing the direction of motion which is velocity sensitive, i.e. the larger the velocity, the greater the effect of drag. Its useful for limiting the velocity of particles.
* X `windx` -
* Y `windy` -
* Z `windz` -
Turbulence `turb` - ⊞ - The amplitude of turbulent (chaotic) forces along each axis. Use positive values, if any.
* X `turbx` -
* Y `turby` -
* Z `turbz` -
Turb Period `period` - A small period means that the turbulence varies quickly over a small area, while a larger value will cause points close to each other to be affected similarly.
Seed `seed` - Random number seed for the particle simulation.
  

## Parameters - Particles Page
Add Particle ID `doid` - Adds an ID number to each particle as it is born. **Note:** New attributes only appear once the particle system is reset via the `reset` parameter or loads for first time.
Add Mass Attribute `domass` - When selected, calculates the mass of the particle, as specified in the Mass field.
Mass `mass` - The relative mass of each particle. Heavier particles take longer to start moving, and longer to slow down.
Add Drag Attribute `dodrag` - When selected, calculates the drag coefficient of the particle, as entered in the Drag field.
Drag `drag` - Drag of each particle.
Birth `birth` - The number of particles born each second. Particles are not released in clusters. They are born at random times during the first frame of their existence. Their birth time is set randomly during the first frame.
Life Expect `life` - How long each particle will exist, in seconds. The default is `3` seconds. You may want to adjust this number based on the length of your animation.
Life Variance `lifevar` - Variance of a particle's life expectancy in seconds. If life expectancy is one second, and the variance is zero seconds, each particle will live exactly one second. If variance is set to 0.5, then some particles will live only a half second, while others will live a second and a half. The rest will live some time in-between. This randomness gives a more natural look to the particle births.
Alpha Speed `alpha` - As a particle goes faster, it should become more transparent. The Alpha Speed parameter defaults to 0, which doesn't change alpha as the speed increases. A typical value of 0.5 causes the particle to be 70% opaque when it's going 1 unit/second. Increasing the Alpha Speed parameter makes it more transparent at a given speed. At zero speed, a particle is always 100% opaque.
Surface Attraction `subattract` - Gives control over how much particles are attracted towards the Particle SOP's 4th input surface attractor.
Birth Count `birthcount` - Specifies the number of particles created when the Birth pulse parameter is hit.
Birth `birthpulse` - Manually create n particles when pulsed. The number of particles created is controlled by the Birth Count parameter.
  

## Parameters - Limits Page
+ Limit Plane `limitpos` - ⊞ - The particles will die or bounce off the limit planes when it reaches them. The six limit plane fields define a bounding cube. The default settings are `1000` units away, which is very large. Reduce the values to about one to see the effect.
* X `limitposx` -
* Y `limitposy` -
* Z `limitposz` -
- Limit Plane `limitneg` - ⊞ - The particles will die or bounce off the limit planes when it reaches them. The six limit plane fields define a bounding cube. The default settings are `1000` units away, which is very large. Reduce the values to about one to see the effect.
* X `limitnegx` -
* Y `limitnegy` -
* Z `limitnegz` -
Hit Behavior `hit` - ⊞ - Control over what happens when a particle hits either the six collision planes or the collide object. The options are:
* Die on Contact `die` - The particles will disappear when they collide with the Collision input.
* Bounce on Contact `bounce` - The particles will bounce upon contact with the Collision input.
* Stick on Contact `stick` - The particles will stick to the Collision input.
Gain Tangent `gaintan` - Friction parameters which can be regarded as energy loss upon collision. The first parameter affects the energy loss (gain) perpendicular to the surface. 0 means all energy (velocity) is lost, 1 means no energy is lost perpendicular to surface. The second parameter is the energy gain tangent to the surface.
Gain Normal `gainnorm` - Friction parameters which can be regarded as energy loss upon collision. The first parameter affects the energy loss (gain) perpendicular to the surface. 0 means all energy (velocity) is lost, 1 means no energy is lost perpendicular to surface. The second parameter is the energy gain tangent to the surface.
* 1 and 1 means nothing is lost or gained.
* 0.1 and 1 cause the particles to strike the surface and dribble along it, like rain atop a roof.
* 1 and 0 makes them bounce perpendicular to the surface, no matter what angle they came in at.
* -1 and 1 makes the particle bounce back from whence it came.
* Gains greater than 1 cause energy gain (like a pinball machine bumper).

Split `splittype` - ⊞ - Select if the particle will split and under what conditions.
* No Splitting `no` - The default setting, this keeps the particles intact.
* Split on Contact `bounce` - The particles will split upon contact with the Collision Source.
* Split on Death `die` - The particles will split when they die.
Min/Max Splits `split` - ⊞ - When a particle splits, it splits into a number of other particles. The number of particles is randomly set between this range.
* `splitmin` -
* `splitmax` -
Split Velocity `splitvel` - ⊞ - Each split particle is given this base velocity.
* X `splitvelx` -
* Y `splitvely` -
* Z `splitvelz` -
Velocity Variance `splitvar` - ⊞ - This is a random amount that is added to the split velocity. When creating fireworks, the variance is large while the velocity is low. When rendering raindrops splashing, the split velocity is large in Y, and the variance in X and Z causes the particles to bounce up - but randomly - in the XZ plane.
* X `splitvarx` -
* Y `splitvary` -
* Z `splitvarz` -
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
* Input 2:  -
* Input 3:  -
  

## Info CHOP Channels
Extra Information for the Particle SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditor2021.100002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • Particle• [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

The 3D data held in SOPs and passed for rendering by the [Geometry COMP](Geometry_COMP.html "Geometry COMP").

(1) A [Geometry Component](Geometry_COMP.html "Geometry COMP") can instance and render its SOP geometry many times: once for each sample in a CHOP, row of a DAT table, pixel in a TOP, or point of a SOP, (2) An instance is an OP that doesn't actually have its own data, but rather just refers to an OP (or has an input) whose data it uses. This includes Null OPs, Switch OPs and in some cases Select OPs.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Particle_SOP&oldid=31305>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")