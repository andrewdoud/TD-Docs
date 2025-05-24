

Bridge SOP - TouchDesigner Documentation




# Bridge SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Bridge SOP is useful for skinning trimmed surfaces, holes, creating highly controllable joins between arms and body, branches or tube intersections.
The Bridge SOP is similar to the Skin SOP but with much greater control over the resulting surface. Given a set of profiles (i.e. curves on surface) and/or spatial faces, the Bridge SOP builds a NURBS skin with specified tangent and curvature characteristics. The precision of the resulting surface is highly dependent on the number of required cross-sections and on the quality of the profile extraction. High precisions will generate a very dense surface with, potentially, many multiple knots.
In general, the higher the order of the curve, the better the fit the Bridge SOP will be able to provide. However, it is generally better to stick to cubics (order 4) curves, as the software is optimized for cubics.
Because the Bridge SOP can join both a set of spatial curves and trim curves, it can be used much like the Skin SOP and/or the Fillet SOP. However, bridging trimmed surfaces is more expensive than bridging carved surfaces.
You will usually need a Trim, Bridge, or Profile SOP after a Project SOP.
* Use a Trim SOP to cut a hole in the projected surface
* Use a Bridge SOPto skin the profile curve to another profile curve.
* Use a Profile SOP to extract the curve on surface or remap it's position.
**Note:** To texture-map the resulting skin, use an Orthographic projection rather than a Spline-based projection. This results in better continuity across the surfaces.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[bridgeSOP\_Class](https://docs.derivative.ca/BridgeSOP_Class "BridgeSOP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)
* [3 Parameters - Surface Properties Page](#Parameters_-_Surface_Properties_Page)
* [4 Parameters - Profile Extraction Page](#Parameters_-_Profile_Extraction_Page)
* [5 Example](#Example)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Page
Group `group` - The Group edit field allows you to enter profile groups for profiles and/or faces to bridge. This is optional if you have regular geometric curves or surfaces, however, you must enter something here in order for Bridge to work with profile curves. For example `*.0` will Bridge the 0th (first) profiles of all incoming primitives.
**Note:** Always specify the curves on surface if you want the Bridge SOP bridge curves on surfaces; otherwise it will attempt to bridge free-floating curves.

Bridge `bridge` - ⊞ - Allows bridging of subgroups of N primitives or patterns of primitives.
* All Primitives `all` -
* Groups of N Primitives `group` -
* Skip Every Nth Primitive `skip` -
N `inc` - Determines the pattern of primitives to bridge using this SOP.
Order `order` - Sets the spline order for both profile extraction and skinning operations.
  

## Parameters - Surface Properties Page
Min X-Sections `isodivs` - The minimum number of cross-sections in the resulting skin. If you create a high-density surface, TouchDesigner's level of detail may display the surface less smoothly than it actually is. You can increase the level of detail by adjusting the viewdisplay options (e.g. `viewdisplay -l 1.5 SOPmain.persp1` ) for the Viewport.
**Production Tip:** If, in generating a smooth surface, you create an extremely complex surface, some of the complexity can be removed without damaging the appearance of the surface by appending a Refine SOP, and using its **Unrefine** option. In the Refine SOP, set the **First U** parameter to zero and, in the **Unrefine** option's parameters, set the **U** value close to the order of the surface created in the Bridge SOP.

Use `frenet` - ⊞ - Specifies the type of normal to use for computing direction:
* The Frenet Frame of the Face `frenet` - The Frenet Frame of the face. This option uses a local coordinate system on the curve to compute the direction.
* The Normal of the Face `normal` - The Normal of the face.
Circular Arc Fillet `circular` - Tells TouchDesigner to try to generate a round fillet rather than a free-form fillet. Only the sign (positive or negative) of the tangent scales is used; the scale magnitude is ignored when building a circular fillet.
The radius of the fillet is computed automatically and adjusted according to the distance between the rails (curves and/or profiles) and their tangents.

Rotate Tangents `rotatet` - ⊞ - The scaling and rotation parameters contain three fields. The rotation fields (degrees) apply further rotation to the tangents, while the scale parameter further scales the tangents.
* `rotatet1` - Applies to the first face in the input.
* `rotatet2` - Applies to all intermediate faces.
* `rotatet3` - Applies to the last face in the input.
Scale Tangents `scalet` - ⊞ - The scaling and rotation parameters contain three fields. The rotation fields (degrees) apply further rotation to the tangents, while the scale parameter further scales the tangents.
* `scalet1` - Applies to the first face in the input.
* `scalet2` - Applies to all intermediate faces.
* `scalet3` - Applies to the last face in the input.
Use Curvature `curvature` - Takes curvature into consideration as well.
Scale Curvatures `scalec` - ⊞ - Further scaling of the curvature.
**Note:** If the resulting skin bulges too greatly, you can achieve a smooth resulting transition between surfaces by disabling the Preserve Tangent & Preserve Curvature Magnitude parameters, and manually tweaking the Tangent Scales and the Curvature Scales. In general, avoid tweaking the Rotations of the Tangents unless you wish to deform the resulting surface.
If the bridge bulges on one side but not the other, try increasing the Min. Number of Cross sections in the bridge.
* `scalec1` -
* `scalec2` -
* `scalec3` -
  

## Parameters - Profile Extraction Page
This page's parameters are similar to those found in the Fit and Project SOPs.
Divisions per Span `sdivs` - Number of 2-D points evaluated in each span.
Tolerance `tolerance` - Precision of 2-D fitting algorithm.
Preserve Sharp Corners `csharp` - Enables or disables fitting of sharp turns. If cracks appear in the resulting skin, Preserve Sharp Corners is usually a good solution; however, it may add additional knots which can create undesirable "ripples" in some cases.
If this option is disabled, fewer isoparms are generated and the surface may not follow the contours of the profile curves perfectly unless the profile curves were built using the `Preserve Sharp Corners` option.

  

## Example
1. Place a Circle SOP. Primitive Type: NURBS; Radius = 0.2, 0.2
2. Place a Grid SOP. Primitive Type: NURBS.
3. Feed both the Circle and Grid SOPs into a Project SOP. Make it the display SOP. You notice the projected circle on the grid - our trim curve.
4. Append a Trim SOP and make it the display SOP. Turn on Gouraud shading for the Viewport - you now see the trimmed holes in the surface of the grid.
5. Append a Copy SOP. Number of Copies: 2; Translation Z: 1.0; Rotation X: 30. Make it the display SOP. Now we have two grids with trimmed holes in them.
6. Append a Bridge SOP, and make it the display SOP. Scale Tangents: `0, 0, 0`; Use Curvature: On; Preserve Curvature Magnitudes: Off; Scale Curvatures: `3, 3, 3` . Nothing happens. Why?
7. We need to specify which profile curves to skin. Turn on Profile Numbers in the Viewport options (click M at the bottom-right of Viewport, and enable the icon). We can see the profile numbers of the two trim curves are 0.0 and 1.0 - meaning the 0th profile of the 0th primitive and the 0th profile of the 1st primitive). The strange numbering is because primitive numbers start at 0 instead of 1.
8. In the Bridge SOP's Group field enter: `.0` - this means to include the 0th (first) curve from all (the *\** wildcard character) primitives in the skin. You now see the resulting bridge between the two trim curves. The skin bulges outwards.
9. We can control the bulge by playing with the Scale Curvatures and the Tangent Magnitudes. Set the Scale Curvatures to: `-3, -3, -3` . Now we have an inward-bulging tube connecting the two holes.  
   [![BridgeSOPExample.gif](https://docs.derivative.ca/images/a/a3/BridgeSOPExample.gif)](https://docs.derivative.ca/File:BridgeSOPExample.gif)
10. Experiment with moving the location and size of the holes (change the Translation and Radius in the Circle SOP). The Bridge SOP dynamically updates the geometry connecting the two surfaces. Setting the Scale Curvature to: `0, 0, 0` produces a straight-through connection between the two holes.
  

## Operator Inputs
* Input 0:  -
  

## Info CHOP Channels
Extra Information for the Bridge SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • Bridge• [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=Bridge_SOP&oldid=24173>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")