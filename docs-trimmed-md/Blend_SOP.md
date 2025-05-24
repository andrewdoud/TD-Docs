

# Blend_SOP

TouchDesigner Documentation




# Blend SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Blend SOP provides 3D metamorphosis between shapes with the same topology. It can blend between sixteen input SOPs using the average weight of each input's respective channel. It will also interpolate point colors and/or texture co-ordinates between shapes.
For best results, there should be the same number of points / CVs (and faces) in the geometry of each SOP. The points should have a similar order; if point 17 in one source is on the left side, and point 17 in another Source is on the right side, it will move across the object during the blend, which may create distorted and twisted shapes. To ensure that this doesn't happen, you can make all the pieces to be blended by editing point positions of one common base shape. Each of the pieces to be morphed must be in different SOPs.
For example, when editing the shapes in the Model Editor, each particular geometry can be saved and then read in, or input the Model SOP directly into the Blend SOP. You would then have the base model geometry entering the Blend SOP in the first Blend, then up to 15 Model SOPs feeding from the SOP containing the base model geometry, which in turn would feed into the Blend SOP. Remember that Model SOPs cannot be unlocked and, therefore, are a safe way to store data without using a File In SOP.
The Blend SOP now only cooks non-zero-weighted inputs.
See also [Sequence Blend SOP](Sequence_Blend_SOP.html "Sequence Blend SOP").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[blendSOP\_Class](https://docs.derivative.ca/BlendSOP_Class "BlendSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Blend Page](#Parameters_-_Blend_Page)
* [3 Parameters - Weights Page](#Parameters_-_Weights_Page)
* [4 Uses](#Uses)
* [5 Example](#Example)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Blend Page
Group `group` - Specifies a point or primitive group in the first input. If, for example, a group is specified containing the first and third points, then the first and third point of every input will be blended whereas the second, fourth, fifth, etc. points will be set to match the first input source. Accepts patterns, as described in: [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Differencing `diff` - Generates exaggerated blends between objects where values above 1 or less than 0 will result in over-scaled blends.
When this option is checked, the above channel values are not summed and scaled to 1. The first input is considered a reference; Blend computes the difference between the first input and the others for each point; values greater than 1 and less than 0 produce exaggerations of the shapes for inputs 2 and higher. The first input, however, cannot be exaggerated by its blend channel, /blend1, and it is considered to be the "base". When using Differencing, the /blend1 channel has no effect. If the geometry in the first input must be deformed, feed it into another input, where the blend channels have an effect.

Blend Position `dopos` - When checked, the point positions of the inputs will be blended based on the weights of the blend channels. If not checked, the input geometry will not change, only allowing Blending of Colors, Normals and Textures if selected.
Blend Colors `doclr` - When checked, the point colors of the geometry inputs will be blended based on the weights of the blend channels.
Blend Normals `donml` - When checked, the point normals of the geometry inputs will be blended based on the weights of the blend channels.
Blend Texture `douvw` - When checked, the point texture co-ordinates of the geometry inputs will be blended based on the weights of the blend channels.
Blend Up `doup` - When checked, the Up Vector of the geometry inputs will be blended based on the weights of the blend channels.
  

## Parameters - Weights Page
Channels controlling the contribution of the geometry inputs to the output geometry. Add parameters below as needed for the number of inputs connected.
Input `input` - Sequence of input weights
Weight `input0weight` - The weight or contribution of this input. 0 has no contribution, 1 is full contribution.
  

## Uses
This SOP can be used as a form of geometry deformation. Model your geometry, such as the mouth on the head of a character. This will become your first input.
  

## Example
Set the input to the first SOP to be blended. For example, if there are five shapes to be blended, the simplest set-up is the following:
Use four Model SOPs, and import the geometry from the base geometry to be deformed / morphed. In each of the Model SOPs, edit the geometry to suit.
Append a Blend SOP off of the SOP containing the base geometry and then proceed to connect up the four Model SOPs into the Blend SOP.
The amount that each input contributes to the resulting shape is controlled by each input's blend channel. Editing the values of the blend channels will result in each input to determine the final shape based on ratios.
For example, if the /blend3 channel's value is 1, and the rest of the channels are set to 0, the resulting shape is the geometry in the third input SOP. Now change the value in the /blend5 channel to 1, the resulting shape will be a 50/50 percent blend of the geometry contained in the input SOPs' three and five. You would get the exact same result by setting both channels to 0.3, or to any number if the numbers are the same in both channels, there will be equal contribution to the shape.
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Blend SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2022.241402021.100002020.200002018.28070before 2018.28070
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • Blend• [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Blend_SOP&oldid=32294>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")