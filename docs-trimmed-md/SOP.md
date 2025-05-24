

SOP - Derivative




# SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
[![OP SOP.png](images/e/e6/OP_SOP.png)](File_OP_SOP.html)
See [Category:SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)") for a full list of articles related to SOPs.
**Surface Operators**, also known as **SOPs**, are operators that can generate, import, modify and combine 3D surfaces (also called geometry). The surface types include 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs - see `particlesGpu` in the palette and components in the `PointClouds` folder of the palette.
See also: [Geometry Detail](Geometry_Detail.html "Geometry Detail"), [Point](Point.html "Point"), [Point List](Point_List.html "Point List"), [Point Class](Point_Class.html "Point Class"), [Primitive](Primitive.html "Primitive"), [Prims Class](Prims_Class.html "Prims Class"), [Polygon](Polygon.html "Polygon"), [Vertex](Vertex.html "Vertex"), [SOP Class](SOP_Class.html "SOP Class"), [SOP to DAT](SOP_to_DAT.html "SOP to DAT"), [Script SOP](Script_SOP.html "Script SOP"), [Point Groups](Point_Group.html "Point Group"), [Primitive Groups](Primitive_Group.html "Primitive Group"), [Attributes](https://docs.derivative.ca/index.php?title=Attributes&action=edit&redlink=1 "Attributes (page does not exist)").
  

## Sweet 16 SOPs[[edit](https://docs.derivative.ca/index.php?title=SOP&action=edit&section=1 "Edit section: Sweet 16 SOPs")]
The following 16 SOPs are commonly used, we recommend familiarizing yourself with them.
| SOP | Purpose | Related SOP |
| --- | --- | --- |
| [Circle](Circle_SOP.html "Circle SOP") | Circle, sphere, torus primitives. | [Sphere](Sphere_SOP.html "Sphere SOP"), [Torus](Torus_SOP.html "Torus SOP") |
| [Grid](Grid_SOP.html "Grid SOP") | Grid, box, rectangle. | [Box](Box_SOP.html "Box SOP"), [Rectangle](Rectangle_SOP.html "Rectangle SOP") |
| [Merge](Merge_SOP.html "Merge SOP") | Merge and delete. | [Object Merge](Object_Merge_SOP.html "Object Merge SOP"), [Delete](Delete_SOP.html "Delete SOP") |
| [Copy](Copy_SOP.html "Copy SOP") | Copy or replicate. | [Limit](Limit_SOP.html "Limit SOP") |
| [Switch](Switch_SOP.html "Switch SOP") | Switch or blend multi-inputs. | [Blend](Blend_SOP.html "Blend SOP"), [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") |
| [Texture](Texture_SOP.html "Texture SOP") | Apply texture coordinated to points or vertices. | [Material](Material_SOP.html "Material SOP") |
| [Noise](Noise_SOP.html "Noise SOP") | Apply noise, twist and deform. | [Twist](Twist_SOP.html "Twist SOP"), [Deform](Deform_SOP.html "Deform SOP") |
| [Transform](Transform_SOP.html "Transform SOP") | Transform point positions. | [Script](Script_SOP.html "Script SOP") |
| [DAT to](DAT_to_SOP.html "DAT to SOP") | DAT table to SOP points. | [Add](Add_SOP.html "Add SOP") |
| [CHOP to](CHOP_to_SOP.html "CHOP to SOP") | CHOP channel samples to SOP points. | [Line](Line_SOP.html "Line SOP") |
| [Trace](Trace_SOP.html "Trace SOP") | Trace a TOP image to polygons. | [File In](File_In_SOP.html "File In SOP") |
| [Clip](Clip_SOP.html "Clip SOP") | Clip and carve. | [Carve](Carve_SOP.html "Carve SOP") |
| [Facet](Facet_SOP.html "Facet SOP") | Facet, subdivide, convert. | [Subdivide](Subdivide_SOP.html "Subdivide SOP"), [Convert](Convert_SOP.html "Convert SOP") |
| [Particle](Particle_SOP.html "Particle SOP") | Particles. |  |
| [Sweep](Sweep_SOP.html "Sweep SOP") | Sweep, skin, rails. | [Skin](Skin_SOP.html "Skin SOP"), [Rails](Rails_SOP.html "Rails SOP") |
| [Sort](Sort_SOP.html "Sort SOP") | Sort and reorder. |  |
## Using SOPs[[edit](https://docs.derivative.ca/index.php?title=SOP&action=edit&section=2 "Edit section: Using SOPs")]
* 3D geometry data, processed on CPU
* FBX Import: .fbx importer, File In SOP - recommend importing geometry from more mature modelers
* FBX Export: Right-click and select **Save Geometry...** In the File Browser that opens, change the file type to .fbx to create a FBX file of that geometry.
## See Also[[edit](https://docs.derivative.ca/index.php?title=SOP&action=edit&section=3 "Edit section: See Also")]
[Category:SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")  
[Geometry Detail](Geometry_Detail.html "Geometry Detail")  
[Primitive](Primitive.html "Primitive")  
[Point](Point.html "Point")
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

The 3D data held in SOPs and passed for rendering by the [Geometry COMP](Geometry_COMP.html "Geometry COMP").

Retrieved from "<https://docs.derivative.ca/index.php?title=SOP&oldid=26932>"
[Categories](Special_Categories.html "Special:Categories"):
* [Touch Glossary](Category_Touch_Glossary.html "Category:Touch Glossary")
* [Geometry](Category_Geometry.html "Category:Geometry")