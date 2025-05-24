

TouchDesigner Documentation





























# Polyspline SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Polyspline SOP fits a spline curve to a polygon or hull and outputs a polygonal approximation of that spline. You can choose either to create divisions between the original points, or to ignore the position of the original points and divide the shape into segments of equal lengths.

Polyspline can optionally resample the output curve, providing control over the length and number of its segments.

**Tip:** When using this SOP, it is useful to enable Points display in the Viewport options dialog. This way you can see exactly what effect the SOP is having.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[polysplineSOP\_Class](https://docs.derivative.ca/PolysplineSOP_Class "PolysplineSOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Operator Inputs](#Operator_Inputs)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [4.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Page

Group `group` - Subset of faces to use. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Spline Type `basis` - ⊞ - Spline type to use. There are seven choices:

* Bezier `bezier` - Typical Bezier spline.

* Special Bezier `sbezier` - Variation on Bezier.

* Special Smooth Bezier `c1bezier` - Variation on Bezier.

* Degree 2 Bezier `degree2` - Variation on Bezier.

* BSpline `bspline` - Softer curve does not pass through the original points of the Source.

* Cardinal `cardinal` - The curve passes through the original points of the Source.

* Linear `linear` - Straight line segments.

Close `closure` - ⊞ - Determines if the output spline is open or closed.

* Off `cnone` - Output spline open.

* On `calways` - Output spline closed.

* If polygon does `cifpoly` - Use the closure of the input face. In other words, Closed splines are created if the Source polygons are closed, open splines are created if the Source polygons are open.

Division Method `divide` - ⊞ - Settings for refining the spline by adding extra divisions.

* Standard `standard` - Do not resample curve.

* Even Length Segments `evenlen` - Ensure equal segment lengths.

* Even X Segments `evenx` - Ensure segments have equal length in X.

* Even Y Segments `eveny` - Ensure segments have equal length in Y.

* Even Z Segments `evenz` - Ensure segments have equal length in Z.

Segment Length `segsize` - The length of the segments in the resampled curve.

Division Method Standard
If Even Length Segments are selected, Segment Length sets the length of output segments. The number of output segments is determined by Output Divisions.
If Output Divisions is zero, the number of output segments is calculated using the Segment Length parameter, and is determined by how many segments of this size will fit into the overall shape.
If Even Length Segments is selected, along with zero Output Divisions and Segment Length of zero, an error message is generated, saying "Invalid number of divisions or segment size".



Output Divisions `polydivs` - Number of segments in the resampled curve.

If Division Method = Standard is selected, this has no effect. If Even Length Segments is selected, this parameter sets the number of edges that is created. The length of the segments is determined by Segment Length. If Segment Length is 0, the length of the output segments is determined by dividing the over all shape into this number of segments.

If the Output Divisions parameter is set to zero, the value of the Segment Length parameter is used to calculate the number of Output Divisions.



Sample Divisions `edgedivs` - Number of spline divisions before resampling.

If Division Method = Standard is selected, this is the number of subdivisions for every edge. If Even Length Segments is chosen, it has the subtle effect of determining the accuracy with which the segment lengths can be calculated.



First CV Count `first` - Number of times to repeat the first control vertex, determining its multiplicity. This determines the number of times to replicate the first vertex of the Source polygon(s). This is most useful when the Source consists of open polygons; extra vertices at the beginning of the line will force the curve to extend to the beginning of the line. For example a value of two will force a Cardinal curve to extend to its first vertex and a value of three will force a Bspline to start at is first vertex.
Last CV Count `last` - This determines the number of times to repeat the last control vertex, determining its multiplicity. This determines the number of times to replicate the last vertex of the Source polygon(s). This is most useful when the Source consists of open polygons; extra vertices at the end of the line will force the curve to extend to the end of the line.
CV Tension `tension` - The tension exerted by the points from the Source polygons. The greater the tension, the closer the resulting shape will be to the original shape.

  


## Operator Inputs

* Input 0:  -

  


## Info CHOP Channels

Extra Information for the Polyspline SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • Polyspline• [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Polyspline_SOP&oldid=24219>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")