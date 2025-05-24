

TouchDesigner Documentation




# Primitive SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Primitive SOP is like the [Point SOP](Point_SOP.html "Point SOP") but manipulates a [primitive](Primitive.html "Primitive")'s position, size, orientation, color, alpha, in addition to primitive-specific attributes, such as reversing primitive normals. The Primitive SOP also lets you create custom primitive attributes.
You can also apply parametric affine transformations to a profile by using this SOP. You can also use it to open, close, reverse, and cycle the profile curves.
**Note:** When applying transformations to a profile, you can only rotate about the Z axis because the projected curve is a planar curve that lives in the domain of the surface. Therefore it wouldn't make any sense to allow rotations in X or Y for profiles.
### Transformation of Primitives vs Profiles
A Bezier surface is a single primitive, as is a NURBS surface, while a polygon mesh can consist of hundreds of individual primitives. Care must be taken to ensure the desired result. Profiles can be translated, rotated, and scaled along with 3D primitives. The Z component of translation and scaling is ignored. The X and Y components would be interpreted as U and V values because they apply to the space in which profiles are defined.
  

### Example - Mapping a Texture Inside a Sphere
There are many uses for the Primitive SOP. Normally, if you apply a texture onto a sphere, it is mapped onto the outside surface because the U surface normals point outwards by default. If you wanted to map the texture onto the inside of the sphere instead, you could simply run the sphere geometry through a Primitive SOP, and select Reverse U (i.e. the surface normals) in the Face/Hull page > Vertex menu.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[primitiveSOP\_Class](https://docs.derivative.ca/PrimitiveSOP_Class "PrimitiveSOP Class")
## Contents
* [1 Summary](#Summary)
  + [1.1 Transformation of Primitives vs Profiles](#Transformation_of_Primitives_vs_Profiles)
  + [1.2 Example - Mapping a Texture Inside a Sphere](#Example_-_Mapping_a_Texture_Inside_a_Sphere)
* [2 Parameters - Primitive Page](#Parameters_-_Primitive_Page)
* [3 Parameters - Transform Page](#Parameters_-_Transform_Page)
* [4 Parameters - Attributes Page](#Parameters_-_Attributes_Page)
* [5 Parameters - Face/Hull Page](#Parameters_-_Face/Hull_Page)
* [6 Parameters - Meta Page](#Parameters_-_Meta_Page)
* [7 Parameters - Particles Page](#Parameters_-_Particles_Page)
* [8 Operator Inputs](#Operator_Inputs)
* [9 Info CHOP Channels](#Info_CHOP_Channels)
  + [9.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [9.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Primitive Page
Source Group `group` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the group specified. You can specify profile curves within the group by providing a profile pattern (e.g. \*.3 specifies the fourth profile in all spline surfaces).
**Tip:** By specifying both a primitive and a profile here (example: 0 0.\* ), you can affect a transformation of both the parent surface and a profile curve.

Template Group `templategrp` - A subset of template points to transform to.
  

## Parameters - Transform Page
Do Transformation `doxform` - When checked, allows transformations to occur.
Rotate to Template `dorot` - ⊞ - A template can be specified using the second input of the Primitive SOP. When set to On, this template can be used to transform each primitive to the location and orientation of the template point. This is similar to what the [Copy SOP](Copy_SOP.html "Copy SOP") does except that the actual primitives are transformed, not copies made.
* Off `off` - Don't rotate.
* On `on` - The primitive gets rotated as if its normal was (0,0,1), and is meant to point the same direction as the template normal.
* Match Normals `match` - Rotates the primitive so that its real normal lines up with the normal of the template point.
Transform Order `xord` - ⊞ - Sets the overall transform order for the transformations. The transform order determines the order in which transformations take place. Depending on the order, you can achieve different results using the exact same values. Choose the appropriate order from the menu.
* Scale Rotate Translate `srt` -
* Scale Translate Rotate `str` -
* Rotate Scale Translate `rst` -
* Rotate Translate Scale `rts` -
* Translate Scale Rotate `tsr` -
* Translate Rotate Scale `trs` -
Rotate Order `rord` - ⊞ - Sets the order of the rotations within the overall transform order.
* Rx Ry Rz `xyz` -
* Rx Rz Ry `xzy` -
* Ry Rx Rz `yxz` -
* Ry Rz Rx `yzx` -
* Rz Rx Ry `zxy` -
* Rz Ry Rx `zyx` -
Translate `t` - ⊞ - These three fields move the input geometry in the three axes. Profiles use tx and ty only.
* X `tx` -
* Y `ty` -
* Z `tz` -
Rotate `r` - ⊞ - These three fields rotate the Source geometry in the three axes. Profiles use rz only.
* X `rx` -
* Y `ry` -
* Z `rz` -
Scale `s` - ⊞ - These three fields scale the Source geometry in the three axes. Profiles use sx and sy only.
* X `sx` -
* Y `sy` -
* Z `sz` -
Pivot `p` - ⊞ - The pivot point for the transformations. Profiles use px and py only.
* X `px` -
* Y `py` -
* Z `pz` -
Lookat Object `lookat` - Selects the object the primitive should point towards. This performs the lookat in object space; if you need to a lookat in world space, use the lookat in the object's Transform page instead.
**Tip:** In order to get multiple sprites to always be perpendicular to the camera, feed them into a Primitive SOP and specify the camera as your **Lookat Object**. Then the sprites should always be perpendicular to the camera.

Up-Vector `upvector` - ⊞ - Defines the orientation of the primitive along the X, Y, or Z axes.
The Up Vector determines how a primitive orients itself with respect to the target object (specified in Lookat Object). The default value is of 1 in the Y direction. This will produce nice behaviour if you want the object to rotate somewhat in the Z axis as the Lookat Object gets very close and/or passes the target. Scaling the Up Vector will cause the Lookat primitives to remain more upright as they get very close and/or pass the target. The stronger the Up Vector, the more the primitives will want to stay vertical and resist the rotation.
* X `upvectorx` -
* Y `upvectory` -
* Z `upvectorz` -
  

## Parameters - Attributes Page
Color `doclr` - ⊞ - If Keep is selected, the color attribute is left unchanged. If Add is selected, this parameter changes the color of input primitives according to diffuse color field. If No is selected, the color attribute is removed.
* Keep Color `off` -
* Add Color `on` -
* No Color `remove` -
Color `diff` - ⊞ - The color to add.
* Red `diffr` -
* Green `diffg` -
* Blue `diffb` -
Alpha `alpha` - The alpha value to add.
Crease `docrease` - ⊞ - If Keep is selected, the crease attribute is left unchanged. If Add is selected, this parameter generates a crease attribute for the primitive. If No is selected, the crease attribute is removed.
* Keep Crease `off` -
* Add Crease `on` -
* No Crease `remove` -
Crease `crease` - Attribute is used to set edge crease weights for subdivision surfaces (see [Subdivide SOP](Subdivide_SOP.html "Subdivide SOP")). The Crease Weight attribute for a primitive sets all edges of the polygon to the value specified. On shared edges, the maximum of the two crease weights is used to define the sharpness of the subdivided surface. Crease weights should be larger than 0, with larger values defining sharper edges.
Custom Attrib `attr` - Sequence of custom attributes to be added to the geometry created.
Name `attr0name` - Creates a custom attribute with this name.
Size `attr0size` - ⊞ - The size of the attribute to create. It'll use however many values from the Value parameter as the size is.
* float `float` -
* vec2 `vec2` -
* vec3 `vec3` -
* vec4 `vec4` -
Value `attr0value` - ⊞ - The value(s) to assign to the attribute.
* Value 1 `attr0value1` -
* Value 1 `attr0value2` -
* Value 1 `attr0value3` -
* Value 1 `attr0value4` -

  

## Parameters - Face/Hull Page
Preserve Shape U `pshapeu` - These options only become available once a type of clamping or closure has been selected.
**Closure** - Change the closure and clamping of a face or hull.

Preserve Shape V `pshapev` - These options only become available once a type of clamping or closure has been selected.
**Closure** - Change the closure and clamping of a face or hull. The options are:

Close U `closeu` - ⊞ - Close the primitive in U / V. Select from: Open, Closed Straight, Close Rounded, and Unroll. When you unroll a closed curve you duplicate the wrapped points (you make them unique) and turn the curve into an open curve. The shape of the curve does not change. Same goes for hulls, only there we unique entire rows and cols. This addresses a problem with texturing wrapped surfaces whereby the texture repeats itself in the wrapped portion of the surface.
* No change `sameclosure` -
* Open `open` -
* Close Straight `closesharp` -
* Close Rounded `closeround` -
* Unroll `unroll` -
Close V `closev` - ⊞ - Close the primitive in U / V. Select from: Open, Closed Straight, Close Rounded, and Unroll. When you unroll a closed curve you duplicate the wrapped points (you make them unique) and turn the curve into an open curve. The shape of the curve does not change. Same goes for hulls, only there we unique entire rows and cols. This addresses a problem with texturing wrapped surfaces whereby the texture repeats itself in the wrapped portion of the surface.
* No change `sameclosure` -
* Open `open` -
* Close Straight `closesharp` -
* Close Rounded `closeround` -
* Unroll `unroll` -
Clamp U `clampu` - ⊞ - Clamp the primitive in U / V. Select from: Clamp, Unclamp.
* No change `sameclamp` -
* Clamp `clamp` -
* Unclamp `unclamp` -
Clamp V `clampv` - ⊞ - Clamp the primitive in U / V. Select from: Clamp, Unclamp.
* No change `sameclamp` -
* Clamp `clamp` -
* Unclamp `unclamp` -
Vertex `vtxsort` - ⊞ - Reorder the vertices in a number of ways.
* No change `samevertex` - Does not affect the ordering of the vertices.
* Reverse `reverse` - Reverses both U and V for hulls, and just U for faces.  
  **For example:**
* Reverse U `reverseu` - Reverses column order of hulls.
* Reverse V `reversev` - Reverses row order of hulls.
* Swap U and V `swapuv` - Interchanges rows/columns while preserving topology.
* Shift `shift` - Cycles the vertices by "U Offset" and "V Offset".
* Flip Face `flipfacing` -
U Offset `vtxuoff` - Cycles face or hull columns / rows when the Shift operation is selected.
V Offset `vtxvoff` - Cycles face or hull columns / rows when the Shift operation is selected.
  

## Parameters - Meta Page
Meta-Surface Weight `metaweight` - When selected, allows meta-surface weighting.
Weight `doweight` - Enter weight of meta-surface here when Meta-surface Weight is selected.
  

## Parameters - Particles Page
Particle Render Type `doprender` - When On the Particle Type menu below allows section of particle render type.
Particle Type `prtype` - ⊞ - Selects how the particles are rendered.
* Render as Lines `lines` - Each particle will be rendered as a 2-point line, with the length determined based on the particles velocity. If the particle has no velocity it will just be a single pixel in size.
* Render as Point Sprites `pointprites` - For use with the [Point Sprite MAT](Point_Sprite_MAT.html "Point Sprite MAT"). Each particle is a square of pixels that always face the camera. The size of the square is determined by parameters in the Point Sprite and the `pscale` vertex/point attribute. The point sprites will have texture coordinates generated for them automatically also ((0,0) in the bottom left and (1,1) in the top right).
* Render as Point Sprites `pointsprites` -
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
  

## Info CHOP Channels
Extra Information for the Primitive SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditor2021.100002020.200002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • Primitive• [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Primitive_SOP&oldid=32301>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")