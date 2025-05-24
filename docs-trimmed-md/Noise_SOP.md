

Noise SOP - TouchDesigner Documentation





























# Noise SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Noise SOP displaces geometry points using noise patterns. It uses the same math as the [Noise CHOP](Noise_CHOP.html "Noise CHOP").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[noiseSOP\_Class](https://docs.derivative.ca/NoiseSOP_Class "NoiseSOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Noise Page](#Parameters_-_Noise_Page)
* [3 Parameters - Transform Page](#Parameters_-_Transform_Page)
* [4 Operator Inputs](#Operator_Inputs)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [5.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Noise Page

Group `group` - If there are input groups, specifying a group name in this field will cause this SOP to act only upon the group specified. Accepts patterns, as described in [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Attribute `attribute` - ⊞ - This menu sets which attribute of the geometry the Noise SOP acts on.

* Point Position `pos` - Noise is applied in the direction of the point normal. If no normal is specified, a normal is computed.

* Point Normals `n` - Noise is applied to each component of the normal independently and then the vector is renormalized.

* Point Diffuse Color `cd` - Noise is applied to each component of the color independently.

* Point Alpha `alpha` - Noise is applied to alpha.

* Point Texture UV `uv` - Noise is applied to each component uv independently.

* Point Texture W `w` - Noise is applied to texture w.

Type `type` - ⊞ - The noise function used to generate noise. The functions available are:

* Sparse `sparse` - Produces high quality, continuous noise based on Sparse Convolution.

* Hermite `hermite` - Quicker than Sparse, but produces lower quality noise.

* Harmomic Summation `harmonic` - Sparse noise with the ability to control the frequency step of the harmonics. Takes the longest to compute.

* Brownian `brownian` - Works like a bug in random flight. With Num of Integrals at 2, its acceleration is changed randomly every frame.

* Random `random` - (White Noise) Every sample is random and unrelated to any other sample. It is the same as "white noise" in audio.

* Alligator `alligator` - Cell Noise.

Seed `seed` - Any number, integer or non-integer, which starts the random number generator. Each number gives completely different noise patterns, but with similar characteristics.
Period `period` - The approximate separation between peaks of a noise cycle. It is expressed in Units. Increasing the period stretches the noise pattern out.

Period is the opposite of frequency. If the period is 2 seconds, the base frequency is 0.5 cycles per second, or 0.5Hz for short. Hz refers to Hertz, the electrical and audio engineer of the 19th century, not the car guy.

If the Type is set to Random, setting this to zero will produce completely random noise. Otherwise, the period should be greater than zero.



Harmonics `harmon` - The number of higher frequency components to layer on top of the base frequency. The higher this number, the bumpier the noise will be (as long as roughness is not set to zero). 0 Harmonics give the base shape.

Harmonics with a base frequency of 0.1Hz will by default produce harmonics at 0.2Hz, 0.4Hz, 0.8Hz, etc. (up to the number of harmonics specified by the Harmonics parameter).



Harmonic Spread `spread` - The factor by which the frequency of the harmonics are increased. It is normally 2. A spread of 3 and a base frequency of 0.1Hz will produce harmonics at 0.3Hz, 0.9Hz, 2.7Hz, etc.. This parameter is only valid for the Harmonic Summation type.
Roughness `rough` - Controls the effect of the higher frequency noise. When Roughness is zero, all harmonics above the base frequency have no effect. At one, all harmonics are equal in amplitude to the base frequency. When Roughness is between one and zero, the amplitude of higher harmonics drops off exponentially from the base frequency.

The default roughness is 0.5. This means the amplitude of the first harmonic is 0.5 of the base frequency, the second is 0.25, the third is 0.125. The harmonics are added to the base to give the final shape. The Harmonics parameter and the Roughness parameter must both be non-zero to see the harmonic effects.



Exponent `exp` - Pushes the noise values toward 0, or +1 and -1. (It raises the value to the power of the exponent.) Exponents greater than one will pull the channel toward zero, and powers less than one will pull peaks towards +1 and -1. It is used to reshape the channels.
Number of Integrals `numint` - Defines the number of times to integrate (see the [Speed CHOP](Speed_CHOP.html "Speed CHOP")) the Brownian noise. Higher values produce smoother curves with fewer features. Values beyond 4 produce somewhat identical curves. This parameter is only valid for the Random noise type.
Amplitude `amp` - Defines the noise value's amplitude (a scale on the values output).
Keep Computed Normals `keepnormals` -

  


## Parameters - Transform Page

The Translate, Rotate, Scale and Pivot parameters let you sample in a different part of the 3D noise space. Imagine a different noise value for every XYZ point in space. Normally, the Noise SOP samples the noise space from (0,0,0) along the X-axis in steps of 2/period.

By changing the transform, you are translating, rotating and scaling the line along which the Noise SOPs samples the noise space. A slight Y-rotation is like walking in a straight path in the mountains, recording your altitude along the way, then re-starting from the same initial location, walking in a slightly different direction. Your altitude starts off being similar but then diverges.

Transform Order `xord` - ⊞ - The menu attached to this parameter allows you to specify the order in which the transforms will take place. Changing the Transform order will change where things go much the same way as going a block and turning east gets you to a different place than turning east and then going a block.

* Scale Rotate Translate `srt` -

* Scale Translate Rotate `str` -

* Rotate Scale Translate `rst` -

* Rotate Translate Scale `rts` -

* Translate Scale Rotate `tsr` -

* Translate Rotate Scale `trs` -

Rotate Order `rord` - ⊞ - The rotational matrix presented when you click on this option allows you to set the transform order for the rotations. As with transform order (above), changing the order in which the rotations take place will alter the final position.

* Rx Ry Rz `xyz` -

* Rx Rz Ry `xzy` -

* Ry Rx Rz `yxz` -

* Ry Rz Rx `yzx` -

* Rz Rx Ry `zxy` -

* Rz Ry Rx `zyx` -

Translate `t` - ⊞ - Translate the sampling plane through the noise space.

* X `tx` -

* Y `ty` -

* Z `tz` -

Rotate `r` - ⊞ - Rotate the sampling plane in the noise space.

* X `rx` -

* Y `ry` -

* Z `rz` -

Scale `s` - ⊞ - Scale the sampling plane.

* X `sx` -

* Y `sy` -

* Z `sz` -

Pivot `p` - ⊞ - Control the pivot for the transform of the sampling plane.

* X `px` -

* Y `py` -

* Z `pz` -

  


## Operator Inputs

* Input 0:  -

  


## Info CHOP Channels

Extra Information for the Noise SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • Noise• [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Noise_SOP&oldid=24210>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")