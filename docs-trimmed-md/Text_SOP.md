

TouchDesigner Documentation





























# Text SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Text SOP creates text geometry from any [TrueType](http://en.wikipedia.org/wiki/TrueType) or [OpenType](http://en.wikipedia.org/wiki/OpenType) font that is installed on the system, or any TrueType/OpenType font file on disk. [Unicode](Unicode.html "Unicode") is supported.

See also: [Text TOP](Text_TOP.html "Text TOP"), [Unicode](Unicode.html "Unicode").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[textSOP\_Class](https://docs.derivative.ca/TextSOP_Class "TextSOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Text Page](#Parameters_-_Text_Page)
* [3 Parameters - Transform Page](#Parameters_-_Transform_Page)
* [4 Info CHOP Channels](#Info_CHOP_Channels)
  + [4.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [4.2 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Text Page

Font `font` - Select the font for the text from this drop down menu. All fonts are provided by the OS, any [TrueType](http://en.wikipedia.org/wiki/TrueType) font that is loaded into the OS can be used.
Font File `fontfile` - Specify any TrueType or OpenType font file (`.ttf, .otf file`) to use for the text. When using a font file, the Font menu above is disabled.
Bold `bold` - Displays the text in **bold**.
Italic `italic` - Displays the text in *Italic*.
Font Size X `fontsizex` - Sets the font size in X (horizontal). The font size defines the distance from the baseline to the top of the layout box for the given font. The default size of 1 of the default font is close to the vertical size of capital letters with no descenders.
Font Size Y `fontsizey` - Sets the font size in Y (vertical).
Keep Font Ratio `keepfontratio` - Ignores Y value in Font Size. Sets both X and Y size to Font Size X.
Scale Font to BBox Height `scalefontobboxheight` - Scale the font’s vertical size so it’s based on the vertical bounding box of the font.
Output `output` - ⊞ - Specify geometry output of Triangles, Closed Polygons or Open Polygons.

* Triangles `triangles` - The output is a triangulated mesh suitable for shaded renders.

* Closed Polygons (Filled Holes) `closedpolys` - The output is a set of separated closed outlines, suitable for [Laser CHOP](Laser_CHOP.html "Laser CHOP"), [Extrude SOP](Extrude_SOP.html "Extrude SOP"), etc. Append a [Hole SOP](Hole_SOP.html "Hole SOP") to preserve holes properly.

* Open Polygons `openpolys` - The output is a set of separated open outlines, suitable for the [Laser CHOP](Laser_CHOP.html "Laser CHOP"), etc. Renders as a wireframe always.

Level of Detail `levelofdetail` - Controls the quality of the text's shape by adding/removing subdivisions to the geometry.
Language `language` - Language type hint to help format the glyphs correctly. This should be a abbreviation from the [Text TOP/SOP Unicode Language Abbreviations](https://docs.derivative.ca/Text_TOP/SOP_Unicode_Language_Abbreviations "Text TOP/SOP Unicode Language Abbreviations") table.
Reading Direction `readingdirection` - ⊞ - Use to set whether the language reads Left to Right or Right to Left.

* Left To Right `lefttoright` -

* Right To Left `righttoleft` -

Kerning `kerning` - ⊞ - The amount of space to add between letters in X and Y. Kerning is way of adding an arbitrary offset between letters. There already is a default offset associated with each font so the letters are flush against each other. The Kerning parameter this adds to that and allows for a Y offset.

* `kerning1` -

* `kerning2` -

Line Spacing `linespacing` - Determines the amount of space between lines of text.
Horizontal Align `alignx` - ⊞ - Sets the horizontal alignment.

* In Reading Direction `reading` -

* Left `left` - Left justifies the text.

* Center `center` - Centers the text.

* Right `right` - Right justifies the text.

Word Wrap `wordwrap` - When checked text is automatically line wrapped once it takes up the space set in Word Wrap Size parameter below.
Word Wrap Size `wordwrapsize` - Determines the amount of 3D space used before the line wraps.
Text `text` - The string of text to create as geometry. If newlines or tabs are desired, the recommended way is to change this parameter to expression mode, and specify a Python string that includes \n or \t to signify newlines and tabs. E.g `'First Line\nSecond Line'`.
Legacy Parsing `legacyparsing` - **Note, it's recommended to use a Python expression in the Text parameter instead of enabling legacy parsing, as this parsing can easily run into issues with more complex strings.** When enabled and if the Text parameter is in Constant Mode, \t and \n character sequences will be turned into tab and newline characters respectively. Otherwise the \t and \n sequences will be left as literal \ and t and \ and n.

  


## Parameters - Transform Page

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

Translate `t` - ⊞ - These three fields move the geometry in the three axes.

* X `tx` -

* Y `ty` -

* Z `tz` -

Rotate `r` - ⊞ - These three fields rotate the geometry in the three axes.

* X `rx` -

* Y `ry` -

* Z `rz` -

Scale `s` - ⊞ - These three fields scale the geometry in the three axes.

* X `sx` -

* Y `sy` -

* Z `sz` -

Pivot `p` - ⊞ - The pivot point for the transformations (not the same as the pivot point in the pivot channels). The pivot point parameters allow you to define the point about which geometry scales and rotates. Altering the pivot point produces different results depending on the transformation performed on the object.

For example, during a scaling operation, if the pivot point of an object is located at: `-1, -1, 0` and you wanted to scale the object by `0.5` (reduce its size by 50%) the object would scale toward the pivot point and appear to slide down and to the left.

* X `px` -

* Y `py` -

* Z `pz` -

  


## Info CHOP Channels

Extra Information for the Text SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").


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

  

TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2021.100002018.28070before 2018.28070

| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • Text• [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Text_SOP&oldid=30477>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")