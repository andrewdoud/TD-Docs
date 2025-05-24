

Delete SOP - TouchDesigner Documentation




# Delete SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Delete SOP deletes input geometry as selected by a group specification or a geometry selection by using either of the three selection options: by entity number, by a bounding volume, and by entity (primitive/point) normals. You can choose to delete the selected or the non-selected geometry.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[deleteSOP\_Class](https://docs.derivative.ca/DeleteSOP_Class "DeleteSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Parameters - Number Page](#Parameters_-_Number_Page)
* [4 Parameters - Bounding Volume Page](#Parameters_-_Bounding_Volume_Page)
* [5 Parameters - Normal Page](#Parameters_-_Normal_Page)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Page
Group `group` - The name of the group to be created. The default name is set to match the name of the SOP.
Operation `negate` - ⊞ - Choose to Delete the Selected Geometry or Delete the Non-Selected Geometry.
* Delete Selected `dele` -
* Delete Non-Selected `keep` -
Entity `entity` - ⊞ - Choose to delete primitives or points.
* Primitives `primitive` -
* Points `point` -
Geometry Type `geotype` - ⊞ - Select the geometry type group. The selection will only pertain to the geometry type specified. e.g. If you only wanted to group polygons.
* All Types `all` - All geometry will be selected.
* Bezier Curve `bezierc` -
* Bezier Surface `bezier` -
* Circle `circle` -
* Mesh `mesh` -
* Metaball `meta` -
* NURBS Curve `nurbc` -
* NURBS Surface `nurb` -
* Particles `part` -
* Polygon `poly` -
* Sphere `sphere` -
* Tube `tube` -
* Triangle Strip `tristrip` -
* Triangle Fan `trifan` -
  

## Parameters - Number Page
Allows selection of grouping of entities by number. When checked, the options relative to this selection option are displayed.
Use Number `usenumber` - When the Enable button is checked under the Number button, the selection options become active and can be used to select entities. The fields available are listed below.
Operation `groupop` - ⊞ - When the Number Enable button is checked, this option groups entities based on a defined Pattern or by a Range.
* Delete by Pattern `pattern` - Select a pattern in the Pattern field below.
* Delete by Range `range` - Select a Range using the Start/End and Select\_of\_ fields below.
* Delete by Expression `filter` - Select a range using the Filter Expression field below.
Pattern `pattern` - Activated when Operation is set to Group by Pattern. In this field, enter the range of primitives to select. The required syntax is "**S.P**", where **S** is the index of the parent surface, and **P** the profile index on that surface. You can mix primitives with profiles in the list. A mixed group is automatically ordered.
**For example**;  
`0.4 2 4 2.5 3.7` selects three profiles and two primitives  
`0-100:2` selects every other number from 0 to 100  
`0-10:2,3` selects every two of three  
`0.0-6` selects six profiles on primitive 0  
`0.*` selects all profiles on primitive 0  
`!4` selects every primitive or point except the fourth  
`9-0` selects first ten (in reverse if ordered flag is on)  
`!0.*` selects all profiles except those on primitive 0  
`*` selects all primitives or points, and no profiles
See Pattern Matching in the [Scripting Guide]

Start / End `range` - ⊞ - Activated when Operation is set to Group by Range. Select the start and end of the primitive/point number selection.
* `rangestart` -
* `rangeend` -
Select \_ of \_ `select` - ⊞ - Activated when Operation is set to Group by Range. Select every nth occurrence of every mth entity in the above Start/End range.
**For example**; entering 1 and 2 selects 1 out of every 2 entities
* `select1` -
* `select2` -
Filter Expression `filter` - The Filter Expression provided is evaluated for every point/primitive. Wherever it is true, the entity is added to the selection.
  

## Parameters - Bounding Volume Page
This option is used for selecting entities based on bounding volumes: **Bounding Box**, or **Bounding Sphere**. When checked, the options relative to this selection option are displayed.
Use Bounds `usebounds` - When the Enable button is checked under the Bounding button, the selection options become active and can be used to select entities. The fields available are listed below. The bounding volume can be seen in the viewport as guide geometry.
Bounding Type `boundtype` - ⊞ - Selects the type of bounding volume to use:
* Bounding Box `usebbox` - Bounding Box entities contained within the box are selected.
* Bounding Sphere `usebsphere` - Bounding Sphere entities contained within the sphere are selected.
Size `size` - ⊞ - Dimensions of either the Bounding Box or Bounding Sphere in X, Y and Z.
* X `sizex` -
* Y `sizey` -
* Z `sizez` -
Center `t` - ⊞ - The X, Y, and Z coordinates of the center of the bounding volume.
* X `tx` -
* Y `ty` -
* Z `tz` -
  

## Parameters - Normal Page
This option is used for selecting entities based on the angle of the entity normals. When checked, the options relative to this selection option are displayed.
Use Normal `usenormal` - When the Enable button is checked under the Normal button, the selection options become active and can be used to select entities. The fields available are listed below.
The primary axis and the spread angle from the defined axis define a range of angles. If any entity normals lie within this range, then the associated entity is selected.
**For example**; if you want to select the polygons that are very steep in a polygon mountain terrain on the XZ axis. You would set the Direction to be `0, 1, 0` and the spread angle to around 75. This selects all the polygons with normals that lie flat to fairly sloped. You will have grouped all of the polygons that lie flat up to polys that are at a 75 angle from the axis. You are left with all of the polygons that are 76 or greater.

Direction `dir` - ⊞ - The default values of `0, 1, 0` create a normal vector straight up in Y, which is perpendicular to the XZ plane, which becomes the primary axis. The `1, 0, 0` points the normal in positive X, giving a normal axis perpendicular to the YZ. The plane may be positioned at an angle by using values typed in (`1, 1, 0` gives a 45 angle plane) or interactively by using the direction vector jack. Values between 0 and 1 should be used.
* X `dirx` -
* Y `diry` -
* Z `dirz` -
Spread Angle `angle` - The value entered in this field generates an angle of deviation from the primary axis. This can be visualized as a cone where the radius of the base of the cone is defined by the Spread Angle and the axis of the cone is determined by the Direction axis. Viewing the primitive normals in the viewport, you can see that any primitives with normals that have an angle that lies in the range of angles defined by the cone will be selected and grouped.
Backface from `camera` - This menu allows you to select an object. Typically, a camera object would be chosen. The primitives which are backface when viewed from the object specified will be grouped or selected.
  

Delete Unused Groups `removegrp` - If any group has 0 entries and if this parameter is enabled, then those groups are removed. If you want to keep empty groups, disable this parameter.
Delete Geometry, Keep Points `keeppoints` - Deletes the geometry but keeps the points.
## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Delete SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • Delete• [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

The 3D data held in SOPs and passed for rendering by the [Geometry COMP](Geometry_COMP.html "Geometry COMP").

A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.

A text string that contains data (string, float, list, boolean, etc.) and operators (+ \* < etc) that are evaluated by the node's language (python or Tscript) and returns a string, float list or boolean, etc. Expressions are used in parameters, [DATs](DAT.html "DAT") and in scripts.

Matching names using wildcard characters and bracketing. Useful in "[Select](Select_CHOP.html "Select CHOP")" type parameters to select multiple operators, paths, channels, etc.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Delete_SOP&oldid=24259>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")