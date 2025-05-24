

Font SOP - TouchDesigner Documentation





























# Font SOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

**Note**: Font SOP deprecated build 2019.14650, use [Text SOP](Text_SOP.html "Text SOP").

The Font SOP allows you to create text in your model from Adobe Type 1 Postscript Fonts.

To install fonts, copy the font files to the `$TFS/touch/fonts` directory of your installation path. They will be ready to be used in the Font SOP after restarting TouchDesigner.

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[fontSOP\_Class](https://docs.derivative.ca/FontSOP_Class "FontSOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Page](#Parameters_-_Page)

  


## Parameters - Page

Primitive Type `type` - ⊞ - Select from the following types. For information on the different types, see the Geometry Types section. Bzier Curves and Polygons provide the most efficient use of memory, because they use polygons for letters containing straight segments, and Bzier curves for all others.

**Note:** Due to an Open GL bug, holes in Bzier fonts may shade incorrectly.

* Bezier Curves and Polygons `bezierpoly` -

* Beziers Only `bezier` -

* Polygons Only `poly` -

Font `file` - Choose the font to create the text. By clicking on the + button a File Dialog will appear, and clicking menu drop down brings up a menu of the most used fonts.
Text `text` - Enter the text you want to generate here.

Your text can contain the following special characters:

* `\`  - Take the next character literally (so you can use the / and ` characters in your text);
* ``string``  - Evaluate the string contained by the backquotes (above the T key) as an expression;
* `\n`  - Start a new line;
* `\xxx`  - Specify a character by it's ascii code (e.g. \007).

**For Example:** If you put something like `\\$F3` in the text string, you should see all the possible characters of a font as you play the animation (set the last frame to 256).

**Entering Expressions as Text** - You can also use expressions for the text.

**For Example:** `me.time.frame` - will display the current frame.

`op('null1')['chan1']` - will display the current value of channel chan1 in CHOP `null1`.

`'hello world'[int(me.time.frame)%11]` - causes the eleven letters of the text to appear in succession during the first eleven frames.

**Other Methods of Entering Text -** You can use the `\xxx` decimal notation to specify characters. The available characters will depend on the font type used.

**For Example:** \065 - will display '`a`'.

You can also use the [Par Class](Par_Class.html "Par Class") to set text in the Font SOP. This can be done from the textport, a [Logic CHOP](Logic_CHOP.html "Logic CHOP") or [Expression CHOP](Expression_CHOP.html "Expression CHOP"), or any script. (See [Scripting](Introduction_to_Python_Tutorial.html "Introduction to Python Tutorial") articles)

**For Example:** `op('font1').par.text = 'hello world'` - will display the words: hello world



Center Text Horizontally `hcenter` - This check box allows you to center the text horizontally about X = 0.
Center Text Vertically `vcenter` - This check box allows you to center the text vertically about Y = 0.
Translate `t` - ⊞ - Translates the geometry in x, y and z.

* X `tx` -

* Y `ty` -

* Z `tz` -

Scale `s` - ⊞ - Scales the text in the X and Y axis.

* X `sx` -

* Y `sy` -

Kerning `kern` - ⊞ - Letter spacing in the X direction. Line spacing in the Y direction if there are multiple lines. If you need manual character-by-character, you can do it in Model mode.

* X `kernx` -

* Y `kerny` -

Italic Angle `italic` - Doesn't actually give an italic version of the font, but rather obliques the text by shearing it the specified number of degrees. A negative number makes the text slant to the left.
Level of Detail `lod` - Adobe fonts are defined by Bzier curves. If polygons only is selected, the Font SOP converts these to polygons. This value adjusts the number of points in the polygons that it gets converted to.
Hole Faces `hole` - Generates holes in polygons and Bzier faces.
Texture Coordinates `texture` - ⊞ - This adds uv coordinates to the geometry created by the Font SOP.

* Off `off` - No uv coordinates added.

* Orthographic `ortho` - Orthographic uv coordinates added.

TouchDesigner Build: Latest\nwikieditorwikieditor2021.100002018.28070before 2018.28070

| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • Font• [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • [LSystem](LSystem_SOP.html "LSystem SOP") • [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Experimental:POP to](https://docs.derivative.ca/Experimental:POP_to_SOP "Experimental:POP to SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").


Any floating window that is not a [Pane](Pane.html "Pane") or [Viewer](Viewer.html "Viewer").


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Font_SOP&oldid=33200>"
[Category](Special_Categories.html "Special:Categories"):

* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")