

# Basis_SOP

Basis SOP - TouchDesigner Documentation




# Basis SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Basis SOP provides a set of operations applicable to the parametric space of spline curves and surfaces. The parametric space, also known as the "domain" of a NURBS or Bzier primitive, is defined by one basis in the U direction and, if the primitive is a surface, another basis in the V direction. The size of the domain is given by the values of the knots that make up the basis.
[![BasisSOP.gif](https://docs.derivative.ca/images/b/b8/BasisSOP.gif)](https://docs.derivative.ca/File:BasisSOP.gif)
The Basis SOP contains both ratio-preserving and non ratio-preserving operations.
If the basis reparameterization does not change the distance ratios between knots, the shape of a NURBS primitive is not affected. If the ratios are not preserved, however, a NURBS primitive will change shape in the area influenced by the modified knots; furthermore, if the primitive is a NURBS or Bzier surface, any profiles it may contain will be affected as well.
For more information about bases and knots see Breakpoints, Knots, and Spline Basis in the [Primitive](Primitive.html "Primitive") and [Spline](Spline.html "Spline") articles.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[basisSOP\_Class](https://docs.derivative.ca/BasisSOP_Class "BasisSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Basis Page](#Parameters_-_Basis_Page)
* [3 Parameters - U Page](#Parameters_-_U_Page)
* [4 Parameters - V Page](#Parameters_-_V_Page)
* [5 Operator Inputs](#Operator_Inputs)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Basis Page
Group `group` - Group of spline primitives (accepts patterns, as described in: Scripting Guide). Non-spline types are ignored.
Two sets of pages follow, one for each parametric direction (U and V). In each set the operations are applied in tab order, starting from the left: Parameterization, Mapping, and then raising the spline Order. To disable all the operations of a set, toggle off the U or V check mark above it. The V set is meaningful only for spline surfaces, and is ignored otherwise. Channel names are given for both the U and V pages.

  

  

## Parameters - U Page
Edit the U Basis `ubasis` - Enable editing of the U Basis.
Parameterization `uparmtype` - ⊞ - Select the method of parameterization in u from the options below.
* Unchanged `nochange` - Does not change the basis.
* Uniform `uniform` - Distributes all the knots evenly, maintaining the basis origin and length. Recommended only for regular shapes.
* Chord Length `chord` - Computes the knot ratios based on the distances between successive CVs. This is the most common and most effective parameterization method.
* Centripetal `centripetal` - Similar to the chord length method. Recommended for shapes containing sharp turns.
* Manual: Single `manualone` - Loads the basis with the knots listed in the "Knot Sequence" below. If the SOP input contains several primitives, only the basis of the first spline primitive will be affected.
* Manual: Propagated `manualall` - Same as above + it copies the basis to the basis of all the other spline primitives in the model or in the group. Using this feature on curves that have the point count and degree will generate cleaner surfaces, i.e. surfaces with fewer isoparms.
* Knotslide `slide` - Shift clusters of knots within the basis. See Knotslide (From Paramaterization Menu) for discussion.
Knot Sequence `uknots` - The basis of the first spline primitive in the input loads its knot sequence with the data specified in this field when the Parameterization is set to Manual. The values must be in ascending order, and their total count must match the number of knots in the basis. To ensure an exact count, click on the Read Basis button to read the original knot sequence into this field.
**Note:** Bezier bases cannot have repeated knots. NURBS bases accept repeated knots as long as the knot multiplicity does not exceed the degree of the basis. The first two and last two knots of a NURBS basis must be identical.

Read Basis `uread` - Loads the original knots of the basis into the Knot Sequence field when the Parameterization type is Manual.
Range `urange` - ⊞ - Range specifies the domain interval to be shifted. All the knots captured in this range are shifted by the same amount as far as the closest neighbouring knot on either side.
* `urange1` -
* `urange2` -
Bias `ubias` - Bias indicates the direction and the amount of translation. A Bias of 0.5 does not displace the knots at all. As the Bias decreases, the knot cluster migrates closer to its left-neighbouring knot. A Bias greater than 0.5 forces a migration to the right.
Sometimes a Bias of 0 or 1 does not clamp the knot cluster to the closest neighbouring knot. The reason for this behaviour is that the knot multiplicity cannot be allowed to exceed the degree of the basis. For example, an order 4 (degree 3, or "cubic") spline can have at most 3 identical knots in sequence.
When sliding the knot of a NURBS basis, a larger area of that spline is affected. This may create the impression than more knots than those in the cluster are being displaced.

Concatenate `uconcat` - Indicates whether the bases of the input spline primitives should be concatenated such that the last knot of the first primitive coincides with the first knot of the second primitive, and so on. This operation is performed before the ones below it, thus allowing a whole set of bases to be mapped onto a given interval (usually [0,1]) while enforcing basis continuity.
Origin `udoorigin` - Enables the Origin parameter.
Origin `uorigin` - The new origin of the basis, or the origin of the cummulated bases if Concatenation is On.
Length `udolength` - Enables the Length parameter.
Length `ulength` - The new length of the basis, or the total length of the cummulated bases if Concatenation is On. The Length, which represents the distance between the first and last knot, must be greater than zero.
Scale `udoscale` - Enables the Scale parameter.
Scale `uscale` - The multiplier applied to the basis starting at the basis origin. The Scale must be greater than zero.
Raise to `uraise` - Enables the Raise to parameter.
Raise U to `orderu` - The only operation here is raising the order (or degree) of the spline basis. Valid orders range from 2 to 11. Orders lower than the current spline order are ignored. The operation preserves the shape of the primitive.
**Production Tip:** Before applying a spline-based texture projection with the Texture SOP, remap the U and/or V bases of the spline surface between 0 and 1 to ensure a complete mapping of the texture. If a single texture map must be shared by several surfaces, the surface bases should be concatenated prior to being remapped.

  

## Parameters - V Page
Edit the V Basis `vbasis` - Enable editing of the V Basis.
Parameterization `vparmtype` - ⊞ - Select the method of parameterization in v from the options below.
* Unchanged `nochange` -
* Uniform `uniform` -
* Chord Length `chord` -
* Centripetal `centripetal` -
* Manual: Single `manualone` -
* Manual: Propagated `manualall` -
* Knotslide `slide` -
Knot Sequence `vknots` - The basis of the first spline primitive in the input loads its knot sequence with the data specified in this field when the Parameterization is set to Manual. The values must be in ascending order, and their total count must match the number of knots in the basis. To ensure an exact count, click on the Read Basis button to read the original knot sequence into this field.
**Note:** Bezier bases cannot have repeated knots. NURBS bases accept repeated knots as long as the knot multiplicity does not exceed the degree of the basis. The first two and last two knots of a NURBS basis must be identical.

Read Basis `vread` - Loads the original knots of the basis into the Knot Sequence field when the Parameterization type is Manual
Range `vrange` - ⊞ - Range specifies the domain interval to be shifted. All the knots captured in this range are shifted by the same amount as far as the closest neighbouring knot on either side.
* `vrange1` -
* `vrange2` -
Bias `vbias` - Bias indicates the direction and the amount of translation. A Bias of 0.5 does not displace the knots at all. As the Bias decreases, the knot cluster migrates closer to its left-neighbouring knot. A Bias greater than 0.5 forces a migration to the right.
Sometimes a Bias of 0 or 1 does not clamp the knot cluster to the closest neighbouring knot. The reason for this behaviour is that the knot multiplicity cannot be allowed to exceed the degree of the basis. For example, an order 4 (degree 3, or "cubic") spline can have at most 3 identical knots in sequence.
When sliding the knot of a NURBS basis, a larger area of that spline is affected. This may create the impression than more knots than those in the cluster are being displaced.

Concatenate `vconcat` - Indicates whether the bases of the input spline primitives should be concatenated such that the last knot of the first primitive coincides with the first knot of the second primitive, and so on. This operation is performed before the ones below it, thus allowing a whole set of bases to be mapped onto a given interval (usually [0,1]) while enforcing basis continuity.
Origin `vdoorigin` - Enables the Origin parameter.
Origin `vorigin` - The new origin of the basis, or the origin of the cummulated bases if Concatenation is On.
Length `vdolength` - Enables the Length parameter.
Length `vlength` - The new length of the basis, or the total length of the cummulated bases if Concatenation is On. The Length, which represents the distance between the first and last knot, must be greater than zero.
Scale `vdoscale` - Enables the Scale parameter.
Scale `vscale` - The multiplier applied to the basis starting at the basis origin. The Scale must be greater than zero.
Raise to `vraise` - Enables the Raise to parameter.
Raise V to `orderv` - The only operation here is raising the order (or degree) of the spline basis. Valid orders range from 2 to 11. Orders lower than the current spline order are ignored. The operation preserves the shape of the primitive.
**Production Tip:** Before applying a spline-based texture projection with the Texture SOP, remap the U and/or V bases of the spline surface between 0 and 1 to ensure a complete mapping of the texture. If a single texture map must be shared by several surfaces, the surface bases should be concatenated prior to being remapped.

  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Basis SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\n2022.241402021.100002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • Basis• [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Basis_SOP&oldid=29698>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")