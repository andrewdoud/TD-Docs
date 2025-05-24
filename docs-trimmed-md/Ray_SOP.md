

TouchDesigner Documentation





























# Ray SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Ray SOP is used to project one surface onto another. Rays are projected from each point of the input geometry in the direction of its normal. This can be used to drape clothes over surfaces, shrink-wrap one object with another, and other similar effects.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[raySOP\_Class](https://docs.derivative.ca/RaySOP_Class "RaySOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Example](#Example)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Page

Group `group` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the group specified. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Method `method` - ⊞ - Select the method of projection for the Ray SOP.

* Minimum Distance `minimum` - Points are placed on the closest point on the collision geometry. This method does not use point normals. Use it to shrinkwrap or project one primitve onto another.

* Project Rays `project` - Points are projected along their normals until intersecting with collision geometry.

Transform Points `dotrans` - If selected, it will transform the input points as defined below. Leave this off when only interested in updating the source point attributes.
Intersect Farthest Surface `lookfar` - If selected, this option allows the user to choose between intersecting with the closest intersecting object or the furthest. See example, below.
Point Intersection Normal `normal` - ⊞ - If selected, updates each point in the source geometry with the normal at the collision surface it intersects with. If the point doesn't intersect at the collision surface, a normal of (0,0,0) is used.

* Source Normal `source` -

* Collision Normal `collision` -

* Reflected Ray `reflect` -

Bounces `bounces` - The number of times to bounce the ray off of the collision surface before creating the output position. For example, if bounces is set to 1, then the point will be projected onto surface at the first point it hits. If set to 2, the ray will be re-projected off of that first surface as if it was reflected, or bounced and will then be projected onto the next surface the ray hits. See the second Ray snippet for an example.
Save Bounce Geometry `bouncegeo` - When enabled, the projected geometry will be saved each time the projected ray bounces off a surface resulting in multiple copies of the input geometry. See the second Ray snippet for an example.
Point Intersection Distance `putdist` - If selected, updates each point intersected with the distance to the collision surface. If the point doesn't intersect at the collision surface a distance of 0 is used. This value is placed in the `$DIST` point attribute, accessible from the [Point SOP](Point_SOP.html "Point SOP").
Scale `scale` - A value of zero will leave the input point unaffected. A value of one will land the point on the intersection surface. Negative values and values > 1 are also valid.
Lift `lift` - This value further offsets the surface input by offsetting it in the direction of its normal.
Sample `sample` - This value determines the number of rays sent per point. If greater than one, the remaining rays are perturbed randomly, and averaged.
Jitter Scale `jitter` - Controls the perturbation of the extra sample rays.
Seed `seed` - Allows a different random sequence at higher sampling rates.
Create Point Group `newgrp` - If selected, it will create a point group containing all the points which were intersected successfully.
Ray Hit Group `hitgrp` - Specifies the name of the above point group.

  


## Example

1. Place a [Grid SOP](Grid_SOP.html "Grid SOP") and translate it in TZ by 2.5. Turn it's template flag on.
2. Append a Point SOP to the Grid and enable the Create Point Normals option.
3. Place a NURBS Sphere with a Radius of 2,2,2 and translate it in Z by -2.5 .
4. Display point normals by enabling the option in the Viewport > Display Options.
5. Append a Ray SOP to the Point SOP and connect the Sphere to the right input. Make it the display SOP.
6. Toggle the Intersect Farthest Surface button on and off.

The Ray SOP will move the points of the Grid in the direction of the point normals. The first surface of the Collision Source (right input) will be where those points of the grid will rest. You can make those points rest on the other side of the sphere by enabling the Intersect Farthest Surface option. This means that the points should continue to project to the farthest surface of the collision source.

  


## Operator Inputs

* Input 0:  -
* Input 1:  -

  


## Info CHOP Channels

Extra Information for the Ray SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • Ray• [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


The 3D data held in SOPs and passed for rendering by the [Geometry COMP](Geometry_COMP.html "Geometry COMP").


samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Ray_SOP&oldid=24225>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")