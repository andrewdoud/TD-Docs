

Texture SOP - TouchDesigner Documentation




# Texture SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Texture SOP assigns texture UV and W coordinates to the Source geometry for use in texture and bump mapping. It generates multi-layers of texture coordinates.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[textureSOP\_Class](https://docs.derivative.ca/TextureSOP_Class "TextureSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Fixing Seams & Unrolling Geometry](#Fixing_Seams_&_Unrolling_Geometry)
* [3 Parameters - Page](#Parameters_-_Page)
* [4 Parameters - Texture Page](#Parameters_-_Texture_Page)
* [5 Parameters - Transform Page](#Parameters_-_Transform_Page)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Fixing Seams & Unrolling Geometry
**NOTE:** the following discussing pertains only to face and hull primitives.
If a texture type requires fixing of seams and the texture is applied to vertices, the wrapped primitives are unrolled before computing the texture coordinates. Unrolling a wrapped primitive turns it into an open primitive whose new vertices use the same points as the vertices they have been uniqued from. Thus, unrolling does not change the point count, nor does it allow cracks to appear further down the road. Explicit unrolling, using the [Primitive SOP](Primitive_SOP.html "Primitive SOP"), is not required.
The seam fixing is done after computing the texture coordinates. It is required whether textures are applied to vertices or points, and it's done in u, v, or both.
The following texture types require fixing of seams:
* Cylindrical - seams fixed in u.
* Polar - seams fixed in u and v.
* Row/col - seams fixed in u and v.
* Spline types: Uniform, Chord Length, and Average - seams fixed in u and v.
**Note:** When the projection type is **Cylindrical** or **Polar**, closed meshes, Bzier & NURBS surfaces will be opened. At least one row/column of vertices will be added (possibly more for NURBS<). This is to prevent poor interpolation of texture coordinates at the seam of the join.
  

## Parameters - Page
Primitive Group `group` - If there are input primitive groups, specifying a group name in this field will cause this SOP to act only upon the group specified. Does not work with point or vertex groups. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
  

## Parameters - Texture Page
Texture Layer `texlayer` - If the geometry has multiple textures layers applied to it, this parameter determines which layer of UV coordinates this Texture SOP will effect.
Texture Type `type` - ⊞ - The Face, Uniform Spline, and Arc-Length Spline texturing methods accept spline curves as well as polygons.
When using one of the spline-based methods, specifying a paste hierarchy in the Group field will propagate the computation of texture coordinates to all of its nodes. Projection methods will typically yield smoother texture continuity between pasted surfaces than any of the spline methods. Sometimes it helps ensuring that pasted features are Chord-length parameterized with the [Basis SOP](Basis_SOP.html "Basis SOP").
* Orthographic `texture` - Direct projection from Projection Axis.
* XYZ Position `xyzposition` - The XYZ position of the vertices will be copied into the UVW values.
* Equirectangular Inside (Spherical Polar) `equirectangularin` - Applies corrdinates to properly apply an equirectangular texture map to the inside of an object. Useful for skyboxes for example.
* Equirectangular Outside (Spherical Polar) `equirectangularout` - Applies corrdinates to properly apply an equirectangular texture map to the outside of an object.
* Cylindrical `cylin` - Wrap cylindrically in Projection Axis direction.
* Row & Columns `rowcol` - For geometry constructed as a mesh (Grid, Sphere, Tube, Skin, and Sweep). The U coordinates are placed along rows, and the V coordinates along columns. This is good for texturing curved meshes such as car fenders where you cannot project from any one axis.
* Face `face` - Maps a copy of the texture onto every face. You should make points unique using a [Facet SOP](Facet_SOP.html "Facet SOP"), before using this function in the Texture SOP. The map is graphically projected to each face along its normal, so the texture is oriented properly for each face. However, the map is not scaled to fit each polygon, nor is it distorted by the shape of each polygon. If the geometry changes in size in object space, the texture does not "stick" to the geometry. It is best suited to texturing objects that represent chunks of rock and brick, as the textures will likely not match at the edges between polygons.
* Modify Source `modify` - If the Source already has texture UV coordinates, they are maintained. You can offset and scale them, however, using Scale and Offset.
* Uniform Spline `suniform` - This projection type operates only on NURBS and Bzier surfaces. It samples the domain space (i.e. the basis) of each surface uniformly in U and V and assigns those (u,v) values as texture coordinates to the surface points or vertices. To ensure continuity between the texture space of adjacent surfaces insert a [Basis SOP](Basis_SOP.html "Basis SOP") before the Texture SOP and toggle Concatenate on to merge the spline bases in U and/or V.
* Average Spline `saverage` - Stores the average of degree successive knots into the texture attribute. These averages are known as **Greville points**. This method and Uniform Spline are recommended for pasted surfaces.
* Arc Length Spline `sarclen` - This method is similar to the Uniform Spline method since it relies on the underlying spline basis when computing the texture coordinates. Both methods generate texture coordinates in the same range, bounded by the minimum and maximum knot values. The difference between the two spline methods lies in the spacing between successive texture coordinates. The uniform method samples the parameter space uniformly. The Arc-Length Spline method chooses the texture coordinates based on surface arc-lengths.
Since the Uniform Spline method relies heavily on the parametric fabric of the surface, the resulting texture will tend to squash and stretch given uneven surface parameterizations. The Arc-Length Spline method reduces this effect by relating the texture space directly to the world space of the surface, while ensuring that the size and origin of the generated texture space coincide with those of the underlying domain.
* Edge Length `edgelength` - Applies to hulls + faces (NURBs/Bezier/Polygon).
* Perspective From Camera `persp` - The texture coordinates are assigned so that the world space of the object can be textured to fit the projection of the camera exactly. If any points are behind the near clipping plane or beyond the far clipping plane, the texture coordinates (`0, 0, 0`) are assigned. Note: Unless a Custom Projection matrix is used in the [Camera COMP](Camera_COMP.html "Camera COMP"), the aspect ratio of the projection is assumed to be 1:1. You may need to scale the UVs to match the aspect ratio of your render.
* Equidistant Azimuth (Fish Eye 180) `equiazimuth` - Applies coordinates for using 180 degree Fish Eye maps.
* Equidistant Azimuth (Fish Eye 360) `equiazimuth360` - Applies coordinates for using 360 degree Fish Eye maps.
Projection Axis `axis` - ⊞ - Axis to project along, or projection method from splines. X, Y, or Z axes.
* X Axis `x` -
* Y Axis `y` -
* Z Axis `z` -
Camera Name `camera` - This is used when the Perspective From Camera Texture Type is selected. The menu is used to select which light or camera to project the perspective coordinates from.
Apply to `coord` - ⊞ - Select to apply texture coordinates to their Natural Location, Point textures, or Vertex textures.
When Natural location is selected, the UV's will be applied to the verticies when using Polar, Cylindrical, Rows and Columns, and Face texture types. Orthographic, Uniform Spline, Average Spline and Arc Length Spline will always generate point UV's when you choose Natural.
Natural Location will also create vertex uvs when creating new texture layers, if a vertex uv already exists for layer 0.
IIf the primitive is open in both directions like a grid or a surface (so that the ends do not touch), then the advantage of vertex UV's does not apply since there are no matched seams on the single surface to worry about.
Using vertex UVs gives you unique points at the closed seam whereas point UVs are shared at seams and are, by default given a value of 0 for either U or V depending on the closed direction of the surface. If you want to make a closed surface open, simply insert a [Carve SOP](Carve_SOP.html "Carve SOP") in the chain and place a single carve in the surface of the direction that the surface is closed.
* Natural location `natural` -
* Point texture `point` -
* Vertex texture (fix seams) `vertex` -
Scale `s` - ⊞ - Scales the texture coordinates a specific amount.
* `su` -
* `sv` -
* `sw` -
Offset `offset` - ⊞ - Offsets the texture coordinates a specific amount.
* `offsetu` -
* `offsetv` -
* `offsetw` -
Rotate `angle` - Rotates the texture coordinates the specified value.
**Tip:** Before applying a spline-based texture projection with the Texture SOP, remap the U and/or V bases of the spline surface (using a [Basis SOP](Basis_SOP.html "Basis SOP")) between 0 and 1 to ensure a complete mapping of the texture. If a single texture map must be shared by several surfaces, the surface bases should be concatenated prior to being remapped.

Fix Face Seams `fixseams` - Attempts to correct texture continuity at face seams.
  

## Parameters - Transform Page
Add further transformations to the texture coordinate space.
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
Translate `t` - ⊞ - These three fields move the texture coordinates in the three axes.
* X `tx` -
* Y `ty` -
* Z `tz` -
Rotate `r` - ⊞ - These three fields rotate the texture coordinates in the three axes.
* X `rx` -
* Y `ry` -
* Z `rz` -
Scale `scaletwo` - ⊞ - These three fields scale the texture coordinates in the three axes.
* X `scaletwox` -
* Y `scaletwoy` -
* Z `scaletwoz` -
Pivot `p` - ⊞ - The pivot point for the transformations (not the same as the pivot point in the pivot channels). The pivot point parameters allow you to define the point about which the texture coordinates scale and rotate. Altering the pivot point produces different results depending on the transformation performed.
For example, during a scaling operation, if the pivot point of the texture coordinates is located at: `-1, -1, 0` and you wanted to scale by `0.5` (reduce its size by 50%) the texture would scale toward the pivot point and appear to slide down and to the left.
[![TouchGeometry91.gif](https://docs.derivative.ca/images/b/bf/TouchGeometry91.gif)](https://docs.derivative.ca/File:TouchGeometry91.gif)
In the example above, rotations performed on a texture coordinates with different pivot points produce very different results.
* X `px` -
* Y `py` -
* Z `pz` -
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Texture SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • Texture• [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

The 3D data held in SOPs and passed for rendering by the [Geometry COMP](Geometry_COMP.html "Geometry COMP").

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Texture_SOP&oldid=24272>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")