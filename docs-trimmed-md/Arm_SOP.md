

# Arm_SOP

Arm SOP - TouchDesigner Documentation




# Arm SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Arm SOP creates all the necessary geometry for an arm, and provides a smooth, untwisted skin that connects the arm to the body. It is controlled through inverse kinematics linked to a handprint.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[armSOP\_Class](https://docs.derivative.ca/ArmSOP_Class "ArmSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Arm Page](#Parameters_-_Arm_Page)
* [3 Parameters - Lengths Page](#Parameters_-_Lengths_Page)
* [4 Parameters - Transforms Page](#Parameters_-_Transforms_Page)
* [5 Parameters - End Affector Page](#Parameters_-_End_Affector_Page)
* [6 Info CHOP Channels](#Info_CHOP_Channels)
  + [6.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [6.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Arm Page
Capture Type `capttype` - ⊞ - You can use either **Ellipses** or **Capture Regions** as deformation geometry. Ellipses are for use with the Skeleton SOP. Capture Regions are for use with the Capture SOP.
* Ellipses `ellipses` -
* Capture Regions `cregions` -
Arm Axis `axis` - ⊞ - Position the model along the +X or -X axis.
* + X `posx` -
* - X `negx` -
Radius `bonerad` - Controls the scale of the circle radii.
Rotate Hand `rotatehand` - This parameter rotates the hand and the wrist joint to match the orientation of the hand-print object. In order to operate correctly, the end-affector (hand print) scale transformations must remain at 1.
**Note:** If the channel is set to 0, then the hand rotations are relative to the forearm. If the channel is set to 1, the hand rotations are the same orientation as the end affector.

Auto Elbow Twist `autoelbow` - This parameter affects the default twist of the elbow joint to a more natural position.
Elbow Twist `elbowtwist` - Specifies the rotation angle of the elbow joint.
Flip Elbow `flipelbow` - This toggle positions the arm using an alternative elbow position solution.
  

## Parameters - Lengths Page
[![TouchGeometry216.gif](https://docs.derivative.ca/images/9/9e/TouchGeometry216.gif)](https://docs.derivative.ca/File:TouchGeometry216.gif)
Clavicle `clavlength` - Control bone lengths, as illustrated above.
Humerous `humlength` - Control bone lengths, as illustrated above.
Ulna `ulnalength` - Control bone lengths, as illustrated above.
Hand `handlength` - Control bone lengths, as illustrated above.
Shoulder Joint `shoulder` - Control the joint lengths, as illustrated above.
Elbow Joint `elbow` - Control the joint lengths, as illustrated above.
Wrist Joint `wrist` - Control the joint lengths, as illustrated above.
  

## Parameters - Transforms Page
When the arm is positioned to reach the end affector (hand print), the shoulder, elbow and wrist joints may produce unnatural looking bends. The transform fields allow manual adjustment of each controlling circle of each joint to fix this.
Each joint circle (e.g. Shoulder 1) is given three transform fields (two translates and one scale). These values are scaled by the amount of bend applied to the particular joint. In other words, when the arm is fully extended, the transforms have no effect. When the arm joint angles are at 90, they have maximum effect. Thus, set the joints to 90 before adjusting these values.
Shoulder 1 `shoulder1t` - ⊞ - The X, Z position of the first shoulder circle, as well as its overall scale.
* X `shoulder1tx` - The X position of the first shoulder circle.
* Y `shoulder1ty` - The Z position of the first shoulder circle. (**Note:** the parameter is labelled Y).
* Z `shoulder1tz` - The overall scale of the first shoulder circle. (**Note:** the parameter is labelled Z).
Shoulder 2 `shoulder2t` - ⊞ - The X, Z position of the second shoulder circle, as well as its overall scale.
* X `shoulder2tx` - The X position of the second shoulder circle.
* Y `shoulder2ty` - The Z position of the second shoulder circle. (**Note:** the parameter is labelled Y).
* Z `shoulder2tz` - The overall scale of the second shoulder circle. (**Note:** the parameter is labelled Z).
Shoulder 3 `shoulder3t` - ⊞ - The X, Z position of the third shoulder circle, as well as its overall scale.
* X `shoulder3tx` - The X position of the third shoulder circle.
* Y `shoulder3ty` - The Z position of the third shoulder circle. (**Note:** the parameter is labelled Y).
* Z `shoulder3tz` - The overall scale of the third shoulder circle. (**Note:** the parameter is labelled Z).
Shoulder 4 `shoulder4t` - ⊞ - The X, Z position of the fourth shoulder circle, as well as its overall scale.
* X `shoulder4tx` - The X position of the fourth shoulder circle.
* Y `shoulder4ty` - The Z position of the fourth shoulder circle. (**Note:** the parameter is labelled Y).
* Z `shoulder4tz` - The overall scale of the fourth shoulder circle. (**Note:** the parameter is labelled Z).
Shoulder 5 `shoulder5t` - ⊞ - The X, Z position of the fifth shoulder circle, as well as its overall scale.
* X `shoulder5tx` - The X position of the fifth shoulder circle.
* Y `shoulder5ty` - The Z position of the fifth shoulder circle. (**Note:** the parameter is labelled Y).
* Z `shoulder5tz` - The overall scale of the fifth shoulder circle. (**Note:** the parameter is labelled Z).
Elbow 1 `elbow1t` - ⊞ - The X, Z position of the first elbow circle, as well as its overall scale.
* X `elbow1tx` - The X position of the first elbow circle.
* Y `elbow1ty` - The Z position of the first elbow circle. (**Note:** the parameter is labelled Y).
* Z `elbow1tz` - The overall scale of the first elbow circle. (**Note:** the parameter is labelled Z).
Elbow 2 `elbow2t` - ⊞ - The X, Z position of the second elbow circle, as well as its overall scale.
* X `elbow2tx` - The X position of the second elbow circle.
* Y `elbow2ty` - The Z position of the second elbow circle. (**Note:** the parameter is labelled Y).
* Z `elbow2tz` - The overall scale of the second elbow circle. (**Note:** the parameter is labelled Z).
Elbow 3 `elbow3t` - ⊞ - The X, Z position of the third elbow circle, as well as its overall scale.
* X `elbow3tx` - The X position of the third elbow circle.
* Y `elbow3ty` - The Z position of the third elbow circle. (**Note:** the parameter is labelled Y).
* Z `elbow3tz` - The overall scale of the third elbow circle. (**Note:** the parameter is labelled Z).
Elbow 4 `elbow4t` - ⊞ - The X, Z position of the fourth elbow circle, as well as its overall scale.
* X `elbow4tx` - The X position of the fourth elbow circle.
* Y `elbow4ty` - The overall scale of the fourth elbow circle. (**Note:** the parameter is labelled Z).
* Z `elbow4tz` - The overall scale of the fourth elbow circle. (**Note:** the parameter is labelled Z).
Elbow 5 `elbow5t` - ⊞ - The X, Z position of the fifth elbow circle, as well as its overall scale.
* X `elbow5tx` - The X position of the fifth elbow circle.
* Y `elbow5ty` - The overall scale of the fifth elbow circle. (**Note:** the parameter is labelled Z).
* Z `elbow5tz` - The overall scale of the fifth elbow circle. (**Note:** the parameter is labelled Z).
Wrist 1 `wrist1t` - ⊞ - The X, Z position of the first wrist circle, as well as its overall scale.
* X `wrist1tx` - The X position of the first wrist circle.
* Y `wrist1ty` - The overall scale of the first wrist circle. (**Note:** the parameter is labelled Z).
* Z `wrist1tz` - The overall scale of the first wrist circle. (**Note:** the parameter is labelled Z).
Wrist 2 `wrist2t` - ⊞ - The X, Z position of the second wrist circle, as well as its overall scale.
* X `wrist2tx` - The X position of the second wrist circle.
* Y `wrist2ty` - The overall scale of the second wrist circle. (**Note:** the parameter is labelled Z).
* Z `wrist2tz` - The overall scale of the second wrist circle. (**Note:** the parameter is labelled Z).
Wrist 3 `wrist3t` - ⊞ - The X, Z position of the third wrist circle, as well as its overall scale.
* X `wrist3tx` - The X position of the third wrist circle.
* Y `wrist3ty` - The overall scale of the third wrist circle. (**Note:** the parameter is labelled Z).
* Z `wrist3tz` - The overall scale of the third wrist circle. (**Note:** the parameter is labelled Z).
Wrist 4 `wrist4t` - ⊞ - The X, Z position of the fourth wrist circle, as well as its overall scale.
* X `wrist4tx` - The X position of the fourth wrist circle.
* Y `wrist4ty` - The overall scale of the fourth wrist circle. (**Note:** the parameter is labelled Z).
* Z `wrist4tz` - The overall scale of the fourth wrist circle. (**Note:** the parameter is labelled Z).
Wrist 5 `wrist5t` - ⊞ - The X, Z position of the fifth wrist circle, as well as its overall scale.
* X `wrist5tx` - The X position of the fifth wrist circle.
* Y `wrist5ty` - The overall scale of the fifth wrist circle. (**Note:** the parameter is labelled Z).
* Z `wrist5tz` - The overall scale of the fifth wrist circle. (**Note:** the parameter is labelled Z).
  

## Parameters - End Affector Page
Affector Object `affector` - Allows the end affector to be another object, or simply defined by a default box, which is controlled by the transformations below.
Translate `t` - ⊞ - End Affector Translation. For a full explanation of transforms, see the [Transform SOP](Transform_SOP.html "Transform SOP").
* X `tx` - End Affector X Translate.
* Y `ty` - End Affector Y Translate.
* Z `tz` - End Affector Z Translate.
Rotate `r` - ⊞ - End Affector Rotation. For a full explanation of transforms, see the [Transform SOP](Transform_SOP.html "Transform SOP").
* X `rx` - End Affector X Rotate.
* Y `ry` - End Affector Y Rotate.
* Z `rz` - End Affector Z Rotate.
Scale `s` - ⊞ - End Affector Scale. For a full explanation of transforms, see the [Transform SOP](Transform_SOP.html "Transform SOP").
* X `sx` - End Affector X Scale.
* Y `sy` - End Affector Y Scale.
* Z `sz` - End Affector Z Scale.
  

## Info CHOP Channels
Extra Information for the Arm SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • Arm• [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Arm_SOP&oldid=24254>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")