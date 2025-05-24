

Geometry COMP - TouchDesigner Documentation




# Geometry COMP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
  

## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Geometry Component is a 3D surface or [3D Object](Object.html "Object") that you render in TouchDesigner with a [Render TOP](Render_TOP.html "Render TOP"). [Lights](Light_COMP.html "Light COMP"), [Cameras](Camera_COMP.html "Camera COMP") and other Components affect the scene, but are not visible surfaces.
Each Geometry Component contains a [Network](Network.html "Network") containing [SOPs](SOP.html "SOP") (and any other node types), where SOPs are the operators that define its 3D shape. The 3D surfaces can be [polygons](Polygon.html "Polygon"), [particles](Particle.html "Particle"), sprites, [meshes](Mesh.html "Mesh"), [NURBS](Spline.html "Spline") (with trim curves), [Bezier](Spline.html "Spline") patches or [metaballs](Metaball.html "Metaball"). They can be shaded as solid-shaded surfaces or as wireframes.
In the Geometry COMP's network
* the [SOPs](SOP.html "SOP") (Surface Operators) whose [Render Flag](Render_Flag.html "Render Flag") is On are rendered by a [Render TOP](Render_TOP.html "Render TOP"). More than one SOP can be turned on for rendering in a Geometry component.
* The SOPs whose [Display Flag](Display_Flag.html "Display Flag") is on are seen in the [Geometry Viewer](Geometry_Viewer.html "Geometry Viewer") of the Geometry COMP and Camera COMPs in the same network.
NOTE: Most often users turn on/off the Render and Display flags together so they are always in the same state.
See [Geometry Viewer](Geometry_Viewer.html "Geometry Viewer") to learn about how you can inspect the SOPs that are turned on for display.
Some SOPs, like the [Texture SOP](Texture_SOP.html "Texture SOP") determine how texture images wrap and fit on the surface.
Every Geometry component needs a [Material](MAT.html "MAT") (MAT) operator to apply to the surface. This is assigned in the Material parameter of the Geometry component, or with a [Material SOP](Material_SOP.html "Material SOP").
To get to the Geometry Component's network, use the roller wheel to zoom into it, or hit Enter or 'i' after selecting a Geometry Component.
See [Geometry Viewer](Geometry_Viewer.html "Geometry Viewer"), [Render Flag](Render_Flag.html "Render Flag") and [Display Flag](Display_Flag.html "Display Flag").
[![Geometry Component.jpg](images/0/04/Geometry_Component.jpg)](File_Geometry_Component.html)
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[geometryCOMP\_Class](GeometryCOMP_Class.html "GeometryCOMP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Xform Page](#Parameters_-_Xform_Page)
* [3 Parameters - Pre-Xform Page](#Parameters_-_Pre-Xform_Page)
* [4 Parameters - Instance Page](#Parameters_-_Instance_Page)
* [5 Parameters - Instance 2 Page](#Parameters_-_Instance_2_Page)
  + [5.1 Instance Texturing](#Instance_Texturing)
* [6 Parameters - Instance 3 Page](#Parameters_-_Instance_3_Page)
* [7 Parameters - Render Page](#Parameters_-_Render_Page)
* [8 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [9 Parameters - Common Page](#Parameters_-_Common_Page)
* [10 Info CHOP Channels](#Info_CHOP_Channels)
  + [10.1 Common COMP Info Channels](#Common_COMP_Info_Channels)
  + [10.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Xform Page
The Xform parameter page controls the object component's transform in world space.
Transform Order `xord` - ⊞ - This allows you to specify the order in which the changes to your Component will take place. Changing the Transform Order will change where things go much the same way as going a block and turning east gets you to a different place than turning east and then going a block. In matrix math terms, if we use the 'multiply vector on the right' (column vector) convention, a transform order of Scale, Rotate, Translate would be written as `T * R * S * Position`.
* Scale Rotate Translate `srt` -
* Scale Translate Rotate `str` -
* Rotate Scale Translate `rst` -
* Rotate Translate Scale `rts` -
* Translate Scale Rotate `tsr` -
* Translate Rotate Scale `trs` -
Rotate Order `rord` - ⊞ - This allows you to set the transform order for the Component's rotations. As with transform order (above), changing the order in which the Component's rotations take place will alter the Component's final position. A Rotation order of Rx Ry Rz would create the final rotation matrix as follows `R = Rz * Ry * Rx`
* Rx Ry Rz `xyz` - `R = Rz * Ry * Rx`
* Rx Rz Ry `xzy` - `R = Ry * Rz * Rx`
* Ry Rx Rz `yxz` - `R = Rz * Rx * Ry`
* Ry Rz Rx `yzx` - `R = Rx * Rz * Ry`
* Rz Rx Ry `zxy` - `R = Ry * Rx * Rz`
* Rz Ry Rx `zyx` - `R = Rx * Ry * Rz`
Translate `t` - ⊞ - This allows you to specify the amount of movement along any of the three axes; the amount, in degrees, of rotation around any of the three axes; and a non-uniform scaling along the three axes. As an alternative to entering the values directly into these fields, you can modify the values by manipulating the Component in the Viewport with the Select & Transform state.
* X `tx` -
* Y `ty` -
* Z `tz` -
Rotate `r` - ⊞ - Theis specifies the amount of movement along any of the three axes; the amount, in degrees, of rotation around any of the three axes; and a non-uniform scaling along the three axes. As an alternative to entering the values directly into these fields, you can modify the values by manipulating the Component in the Viewport with the Select & Transform state.
* X `rx` -
* Y `ry` -
* Z `rz` -
Scale `s` - ⊞ - This specifies the amount of movement along any of the three axes; the amount, in degrees, of rotation around any of the three axes; and a non-uniform scaling along the three axes. As an alternative to entering the values directly into these fields, you can modify the values by manipulating the Component in the Viewport with the Select & Transform state.
* X `sx` -
* Y `sy` -
* Z `sz` -
Pivot `p` - ⊞ - The Pivot point edit fields allow you to define the point about which a Component scales and rotates. Altering the pivot point of a Component produces different results depending on the transformation performed on the Component.
For example, during a scaling operation, if the pivot point of an Component is located at `-1, -1, 0` and you wanted to scale the Component by `0.5` (reduce its size by 50%), the Component would scale toward the pivot point and appear to slide down and to the left.
[![Objects17.gif](images/6/60/Objects17.gif)](File_Objects17.html)
In the example above, rotations performed on an Component with different pivot points produce very different results.
* X `px` -
* Y `py` -
* Z `pz` -
Uniform Scale `scale` - This field allows you to change the size of an Component uniformly along the three axes.
> **Note:** Scaling a camera's channels is not generally recommended. However, should you decide to do so, the rendered output will match the Viewport as closely as possible when scales are involved.

Parent Transform Source `parentxformsrc` - ⊞ - ***NOTE:** This parameter replaces the previous '**Constrain To'** parameter.* Use 'Parent Transform Source' and to specify what initial position is used for this object. Can be one of "Parent (Hierarchy)", "Specify Parent Object", or "World Origin".
* From Parent Object (Hierarchy) `hierarchy` -
* Specify Parent Object `specify` -
* World Origin `worldorigin` -
Parent Object `parentobject` - Allows the location of the object to be constrained to any other object whose path is specified in this parameter.
Look At `lookat` - Allows you to orient this Component by naming another 3D Component you would like it to Look At, or point to. Once you have designated this Component to look at, it will continue to face that Component, even if you move it. This is useful if, for instance, you want a camera to follow another Component's movements. The Look At parameter points the Component in question at the other Component's origin.
> **Tip:** To designate a center of interest for the camera that doesn't appear in your scene, create a Null Component and disable its display flag. Then Parent the Camera to the newly created Null Component, and tell the camera to look at this Component using the Look At parameter. You can direct the attention of the camera by moving the Null Component with the Select state. If you want to see both the camera and the Null Component, enable the Null Component's display flag, and use the Select state in an additional Viewport by clicking one of the icons in the top-right corner of the TouchDesigner window.

Forward Direction `forwarddir` - ⊞ - Sets which axis and direction is considered the forward direction.
* +X `posx` -
* -X `negx` -
* +Y `posy` -
* -Y `negy` -
* +Z `posz` -
* -Z `negz` -
Look At Up Vector `lookup` - ⊞ - When specifying a Look At, it is possible to specify an up vector for the lookat. Without using an up vector, it is possible to get poor animation when the lookat Component, for example, passes through the Y axis of the target Component.
* Don't Use Up Vector - Use this option if the look at Component does not pass through the Y axis of the target Component.
* Use Up Vector - This precisely defines the rotates on the Component doing the looking. The Up Vector specified should not be parallel to the look at direction. See Up Vector below.
* Use Quaternions - Quaternions are a mathematical representation of a 3D rotation. This method finds the most efficient means of moving from one point to another on a sphere.
* Don't use up vector `off` -
* Use up vector `on` -
* Use quaternions `quat` -
* Use Roll `roll` -
Path SOP `pathsop` - Names the SOP that functions as the path you want this Component to move along. For instance, you can name a SOP that provides a path for the camera to follow.
Roll `roll` - Using the angle control you can specify a Component's rotation as it animates along the path.
Position `pos` - This parameter lets you specify the Position of the Component along the path. The values you can enter for this parameter range from `0` to `1`, where `0` equals the starting point and `1` equals the end point of the path. The value slider allows for values as high as `10` for multiple "passes" along the path.
Orient along Path `pathorient` - If this option is selected, the Component will be oriented along the path. The positive Z axis of the Component will be pointing down the path.
Orient Up Vector `up` - ⊞ - When orienting a Component, the Up Vector is used to determine where the positive Y axis points.
* X `upx` -
* Y `upy` -
* Z `upz` -
Auto-Bank Factor `bank` - The Auto-Bank Factor rolls the Component based on the curvature of the path at its current position. To turn off auto-banking, set the bank scale to `0`.
  

## Parameters - Pre-Xform Page
The Pre-Xform parameter page applies a transform to the object component the same way connecting another [Object](Object.html "Object") as a parent of this node does. The transform is applied to the left of the [Xform](Object_COMP_Xform_Page.html "Object COMP Xform Page") page's parameters. In terms of matrix math, if we use the 'multiply on the right' (column vector) convention, the equation would be `preXForm * xform * Position`.
Apply Pre-Transform `pxform` - Enables the transformation on this page.
Transform Order `pxord` - ⊞ - Refer to the documentation on Xform page for more information.
* Scale Rotate Translate `srt` -
* Scale Translate Rotate `str` -
* Rotate Scale Translate `rst` -
* Rotate Translate Scale `rts` -
* Translate Scale Rotate `tsr` -
* Translate Rotate Scale `trs` -
Rotate Order `prord` - ⊞ - Refer to the documentation on Xform page for more information.
* Rx Ry Rz `xyz` -
* Rx Rz Ry `xzy` -
* Ry Rx Rz `yxz` -
* Ry Rz Rx `yzx` -
* Rz Rx Ry `zxy` -
* Rz Ry Rx `zyx` -
Translate `pt` - ⊞ - Refer to the documentation on Xform page for more information.
* X `ptx` -
* Y `pty` -
* Z `ptz` -
Rotate `pr` - ⊞ - Refer to the documentation on Xform page for more information.
* X `prx` -
* Y `pry` -
* Z `prz` -
Scale `ps` - ⊞ - Refer to the documentation on Xform page for more information.
* X `psx` -
* Y `psy` -
* Z `psz` -
Pivot `pp` - ⊞ - Refer to the documentation on Xform page for more information.
* X `ppx` -
* Y `ppy` -
* Z `ppz` -
Uniform Scale `pscale` - Refer to the documentation on Xform page for more information.
Reset Transform `preset` - This button will reset this page's transform so it has no translate/rotate/scale.
Commit to Main Transform `pcommit` - This button will copy the transform from this page to the main Xform page, and reset this page's transform.
Xform Matrix/CHOP/DAT `xformmatrixop` - This parameter can be used to transform using a 4x4 matrix directly. For information on ways to specify a matrix directly, refer to the [Matrix Parameters](Matrix_Parameters.html "Matrix Parameters") page. This transform will be applied after the regular Pre-Transform transformation. That is, it'll be applied in the oder XformMatrix \* PreXForm \* Position.
  

## Parameters - Instance Page
The Instance parameter page provides the ability to create hardware instances of geometry. Each instance has an instance ID which can be passed into a [MAT](MAT.html "MAT") shader via a uniform value. The instance ID can be retrieved by the [Render Pick CHOP](Render_Pick_CHOP.html "Render Pick CHOP"). Any code in a vertex shader can customize the instance based on the instance ID.
Instance's attributes can be individually driven by the data from any type of OP. When the instance data is supplied by a TOP, the TOP's RGBA channels are assigned to instance attributes, when data is supplied by a CHOP, the CHOP's channels are assigned to instance attributes, when from a SOP then the SOP's attributes are assigned to instance attributes, and when a DAT is used then a column is assigned to the instances attributes. The mapping of operator data to instance attributes is setup on the parameters below and on the Instance 2 and Instance 3 parameter pages.
Instancing `instancing` - Turns on instancing for the Geometry Component.
Instance Count Mode `instancecountmode` - ⊞ - Two modes to determine how many instances will be created.
* Manual `manual` - Use the Num Instances parameter below to set the number of instances.
* Instance OP(s) Length `oplength` - The number of CHOP samples/DAT rows in the Instance CHOP/DAT determines the number of instances.
Num Instances `numinstances` - When using the Manual mode for Instance Count, this parameter set the number of instances.
Default Instance OP `instanceop` - Specify a path to a CHOP or DAT used to transform the instances. Number of samples/rows in this CHOP or DAT determines the number of instances when using the CHOP Length/DAT Num Rows mode for Instance Count.
First Row is `instancefirstrow` - ⊞ - What to do with the first row of a table DAT when using DAT rows for Instance Count.
* Ignored `ignored` - The first row is ignored and it's values won't be used as part of an instance. Indices must be used to select the columns to use for instance attributes.
* Names `names` - The first row contains column names which can be used to select which columns to use from the table.
* Values `values` - The first row is considered to contain values for the first instance. Indices must be used to select the columns to use for instance attributes.
Transform Order `instxord` - ⊞ - Controls the order the transform operations will be applied to each instance. Refer to the documentation for the Xform page for more details.
* Scale Rotate Translate `srt` -
* Scale Translate Rotate `str` -
* Rotate Scale Translate `rst` -
* Rotate Translate Scale `rts` -
* Translate Scale Rotate `tsr` -
* Translate Rotate Scale `trs` -
Rotate Order `instrord` - ⊞ - The rotational matrix presented when you click on this option allows you to set the transform order for the Component's rotations. As with transform order (above), changing the order in which the Component's rotations take place will alter the Component's final position.
* Rx Ry Rz `xyz` -
* Rx Rz Ry `xzy` -
* Ry Rx Rz `yxz` -
* Ry Rz Rx `yzx` -
* Rz Rx Ry `zxy` -
* Rz Ry Rx `zyx` -
Translate OP `instancetop` - Select a specific operator to get data from for the Translate instance attributes below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
Active `instanceactive` - Select the data channel that will be used to control which instances are rendered. Only instances with a non-zero value in this channel will be rendered; instances with a zero active channel value will be skipped. If no data is assigned to this channel then all instances are rendered. Use the drop-down menu on the right to easily select from the available options.
Translate X `instancetx` - Select what data to use to translate instances, use the drop-down menu on the right to easily select from the available options.
Translate Y `instancety` - Select what data to use to translate instances, use the drop-down menu on the right to easily select from the available options.
Translate Z `instancetz` - Select what data to use to translate instances, use the drop-down menu on the right to easily select from the available options.
Rotate OP `instancerop` - Select a specific operator to get data from for the Rotate instance attributes below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
Rotate X `instancerx` - Select what data to use to rotate instances, use the drop-down menu on the right to easily select from the available options.
Rotate Y `instancery` - Select what data to use to rotate instances, use the drop-down menu on the right to easily select from the available options.
Rotate Z `instancerz` - Select what data to use to rotate instances, use the drop-down menu on the right to easily select from the available options.
Scale OP `instancesop` - Select a specific operator to get data from for the Scale instance attributes below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
Scale X `instancesx` - Select what data to use to scale instances, use the drop-down menu on the right to easily select from the available options.
Scale Y `instancesy` - Select what data to use to scale instances, use the drop-down menu on the right to easily select from the available options.
Scale Z `instancesz` - Select what data to use to scale instances, use the drop-down menu on the right to easily select from the available options.
Pivot OP `instancepop` - Select a specific operator to get data from for the Pivot instance attributes below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
Pivot X `instancepx` - Select what data to use for the pivot of the instances, use the drop-down menu on the right to easily select from the available options.
Pivot Y `instancepy` - Select what data to use for the pivot of the instances, use the drop-down menu on the right to easily select from the available options.
Pivot Z `instancepz` - Select what data to use for the pivot of the instances, use the drop-down menu on the right to easily select from the available options.
  

## Parameters - Instance 2 Page
When the instance data is supplied by a TOP, the TOP's RGBA channels are assigned to instance attributes; when data is supplied by a CHOP, the CHOP's channels are assigned to instance attributes; when from a SOP then the SOP's attributes are assigned to instance attributes; and when a DAT is used then a column is assigned to the instances attributes.
Rotate to Vector: Order `instancerottoorder` - ⊞ - Controls where in the transform equation the Rotate To Vector operation is applied.
* Default `default` - The Rotate to Vector operation will be applied before all other transform operations (except the pivot offset), regardless of their order of operation. E.g  `T * R * S * (RotToVector) * Position` ,  `R * S * T * (RotToVector) * Position` .
* Pre-Rot `prerot` - The Rotate To Vector operation will be applied after the main rotation as part of the TRS order. I.e  `T * (RotToVector * R) * S * Position`,  `(RotToVector * R) * S * T * Position`.
* Post-Rot `postrot` - The Rotate To Vector operation will be applied before the main rotation as part of the TRS order. I.e  `T * (R * RotToVector) * S * Position`,  `(R * RotToVector) * S * T * Position`.
Rotate to Vector: Forward Direction `instancerottoforward` - ⊞ - Determine which axis for the geometry original orientation is considered 'forward'. That is, it'll treat the part of the geometry that is looking down that axis as the front and rotate it so it's aligned with the rotate to vector direction.
* +X `posx` -
* -X `negx` -
* +Y `posy` -
* -Y `negy` -
* +Z `posz` -
* -Z `negz` -
Rotate to OP `instancerottoop` - Select a specific operator to get data from for the Rotate to Vector instance attributes below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
Rotate to Vector X `instancerottox` - Select what data to use to rotate to vector instances, use the drop-down menu on the right to easily select from the available options.
Rotate to Vector Y `instancerottoy` - Select what data to use to rotate to vector instances, use the drop-down menu on the right to easily select from the available options.
Rotate to Vector Z `instancerottoz` - Select what data to use to rotate to vector instances, use the drop-down menu on the right to easily select from the available options.
Rotate Up OP `instancerotupop` - Select a specific operator to get data from for the Rotate Up instance attributes below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
Rotate Up X `instancerotupx` - Select what data to use to rotate up instances, use the drop-down menu on the right to easily select from the available options.
Rotate Up Y `instancerotupy` - Select what data to use to rotate up instances, use the drop-down menu on the right to easily select from the available options
Rotate Up Z `instancerotupz` - Select what data to use to rotate up instances, use the drop-down menu on the right to easily select from the available options
Instance Order `instanceorder` - ⊞ - Sets how transforms are applied to the instances.
* Instance, then World Transform `instanceworld` - Use the individual instance transforms first, then apply the world transform (i.e. Xform and Pre-Xform parameter pages). `worldXform * instanceXForm * Position`
* World Transform, then Instance `worldinstance` - Use the world transform first, then apply the individual instance transforms. `instanceXForm * worldXForm * Position`
Texture Mode `instancetexmode` - ⊞ - Set how the texture coordinates are applied to the instances.
* Replace `replace` - Replaces texture coordinates.
* Transform `transform` - Offsets texture coordinates.
Tex Coord OP `instancetexcoordop` - Select a specific operator to get data from for the Texture Coord instance attributes below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
U `instanceu` - Select what data to apply to texture coordinates of the instances, use the drop-down menu on the right to easily select from the available options. This interacts with the first texture layer [uv[0] attributes](Attribute.html "Attribute") coming from the SOP.
V `instancev` - Select what data to apply to texture coordinates of the instances, use the drop-down menu on the right to easily select from the available options. This interacts with the first texture layer [uv[0] attributes](Attribute.html "Attribute") coming from the SOP.
W `instancew` - Select what data to apply to texture coordinates of the instances, use the drop-down menu on the right to easily select from the available options. This interacts with the first texture layer [uv[0] attributes](Attribute.html "Attribute") coming from the SOP.
Color Mode `instancecolormode` - ⊞ - Controls how the instance color values interact with the SOPs ['Cd' (diffuse color)](Attribute.html "Attribute") attribute. If the SOP doesn't have a 'Cd' attribute, then it will behave as if its 'Cd' is (1, 1, 1, 1).
* Replace `replace` -
* Multiply `multiply` -
* Add `add` -
* Subtract `subtract` -
Color OP `instancecolorop` - Select a specific operator to get data from for the Color instance attributes below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
R `instancer` - Select what data to apply to the diffuse color of the instances, use the drop-down menu on the right to easily select from the available options. These parameters will be combined/replaced with the SOPs 'Cd' attribute, as chosen by the Color Mode parameter.
G `instanceg` - Select what data to apply to the diffuse color of the instances, use the drop-down menu on the right to easily select from the available options. These parameters will be combined/replaced with the SOPs 'Cd' attribute, as chosen by the Color Mode parameter.
B `instanceb` - Select what data to apply to the diffuse color of the instances, use the drop-down menu on the right to easily select from the available options. These parameters will be combined/replaced with the SOPs 'Cd' attribute, as chosen by the Color Mode parameter.
A `instancea` - Select what data to apply to the diffuse color of the instances, use the drop-down menu on the right to easily select from the available options. These parameters will be combined/replaced with the SOPs 'Cd' attribute, as chosen by the Color Mode parameter.
Instance Textures `instancetexs` - ⊞ - Specify the paths one or more TOP containing the textures to use with the instances. Wildcards and pattern matching is supported.
Extend U `instancetexextendu` - ⊞ -
* Hold `hold` -
* Zero `zero` -
* Repeat `repeat` -
* Mirror `mirror` -
Extend V `instancetexextendv` - ⊞ -
* Hold `hold` -
* Zero `zero` -
* Repeat `repeat` -
* Mirror `mirror` -
Extend W `instancetexextendw` - ⊞ -
* Hold `hold` -
* Zero `zero` -
* Repeat `repeat` -
* Mirror `mirror` -
Filter `instancetexfilter` - ⊞ -
* Nearest `nearest` -
* Linear `linear` -
* Mipmap Linear `mipmaplinear` -
Anisotropic Filter `instancetexanisotropy` - ⊞ -
* Off `off` -
* 2x `2x` -
* 4x `4x` -
* 8x `8x` -
* 16x `16x` -
### Instance Texturing
This feature allows for arbitrary textures to be applied to instances. The textures do not need to be the same resolution, and they don't need to be combined into an grouped format such as a 3D Texture or a 2D Texture array. Multiple TOPs can be specified using the "Instance Textures" parameter, and the texture that is applied per-instance is specified using the channel chosen in the "Texture Index" parameter. This is different from a 3D Texture or 2D Texture Array, which would use the W texture coordinate to select a texture from within a single texture. By default this texture will be used as the "Base Color Map" texture for a [PBR MAT](PBR_MAT.html "PBR MAT"), and the Color Map for all other materials such as the [Phong MAT](Phong_MAT.html "Phong MAT"). For materials that support more than one map, the map that this this feature replaces can be chosen in the material's parameters. Currently on Windows at most 16384 textures can be used at once, and on macOS at most 128 textures can be used at once. These numbers are reduced by other textures that are used by the render such as other maps, cone light lookup map etc.
  

Tex Index OP `instancetexindexop` - Select a specific operator to get data from for the Texture Index instance attribute below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
Texture Index `instancetexindex` - Select what data to select which texture to use for the instances, use the drop-down menu on the right to easily select from the available options.
  

## Parameters - Instance 3 Page
Custom attributes allow arbitrary attributes to be assigned to instances, usable in a [GLSL MAT](GLSL_MAT.html "GLSL MAT"). They can be accessed using `TDInstanceCustomAttrib0()`, `TDInstanceCustomAttrib1()` etc. For more information refer to [Write a GLSL Material](Write_a_GLSL_Material.html "Write a GLSL Material"). These attributes will be ignored in other materials such as the [PBR MAT](PBR_MAT.html "PBR MAT").
Below you can add more parameters as you require more custom attributes. Different GPUs will have a different number of maximum custom attributes supported.
Custom Instance `instance` - Sequence of arbitrary attributes to be assigned to instances
OP `instance0customop` - Select a specific operator to get data from for the instance attributes below. If not specified, the the operator specified in the 'Default Instance OP' on the Instance parameter page can be used.
X `instance0customx` - Select what data to use for this instance attribute, use the drop-down menu on the right to easily select from the available options.
Y `instance0customy` - Select what data to use for this instance attribute, use the drop-down menu on the right to easily select from the available options.
Z `instance0customz` - Select what data to use for this instance attribute, use the drop-down menu on the right to easily select from the available options.
W `instance0customw` - Select what data to use for this instance attribute, use the drop-down menu on the right to easily select from the available options.
  

## Parameters - Render Page
The Display parameter page controls the component's [material](https://docs.derivative.ca/index.php?title=Material&action=edit&redlink=1 "Material (page does not exist)") and [rendering](Rendering.html "Rendering") settings.
Material `material` - Selects a [MAT](MAT.html "MAT") to apply to the geometry inside.
Render `render` - Whether the Component's geometry is visible in the [Render TOP](Render_TOP.html "Render TOP"). This parameter works in conjunction (logical AND) with the Component's [Render Flag](Render_Flag.html "Render Flag").
Draw Priority `drawpriority` - Determines the order in which the Components are drawn. Smaller values get drawn after larger values. The value is compared with other Components in the same parent Component, or if the Component is the top level one listed in the Render TOP's 'Geometry' parameter, then against other top-level Components listed there. This value is most often used to help with [Transparency](Transparency.html "Transparency").
Pick Priority `pickpriority` - When using a [Render Pick CHOP](Render_Pick_CHOP.html "Render Pick CHOP") or a [Render Pick DAT](Render_Pick_DAT.html "Render Pick DAT"), there is an option to have a 'Search Area'. If multiple objects are found within the search area, the pick priority can be used to select one object over another. A higher value will get picked over a lower value. This does not affect draw order, or objects that are drawn over each other on the same pixel. Only one will be visible for a pick per pixel.
Wireframe Color `wcolor` - ⊞ - Use the R, G, and B fields to set the Component's color when displayed in wireframe shading mode.
* Red `wcolorr` -
* Green `wcolorg` -
* Blue `wcolorb` -
Light Mask `lightmask` - By default all lights used in the [Render TOP](Render_TOP.html "Render TOP") will affect geometry renderer. This parameter can be used to specify a sub-set of lights to be used for this particular geometry. The lights must be listed in the [Render TOP](Render_TOP.html "Render TOP") as well as this parameter to be used.
  

## Parameters - Extensions Page
The Extensions parameter page sets the component's python extensions. Please see [extensions](Extensions.html "Extensions") for more information.
Extension `ext` - Sequence of info for creating extensions on this component
Object `ext0object` - A number of class instances that can be attached to the component.
Name `ext0name` - Optional name to search by, instead of the instance class name.
Promote `ext0promote` - Controls whether or not the extensions are visible directly at the component level, or must be accessed through the `.ext` member. Example: `n.Somefunction` vs `n.ext.Somefunction`

Re-Init Extensions `reinitextensions` - Recompile all extension objects. Normally extension objects are compiled only when they are referenced and their definitions have changed.
  

## Parameters - Common Page
The Common parameter page sets the component's [node viewer](Node_Viewer.html "Node Viewer") and [clone](Clone.html "Clone") relationships.
Parent Shortcut `parentshortcut` - Specifies a name you can use anywhere inside the component as the path to that component. See [Parent Shortcut](Parent_Shortcut.html "Parent Shortcut").
Global OP Shortcut `opshortcut` - Specifies a name you can use anywhere at all as the path to that component. See [Global OP Shortcut](Global_OP_Shortcut.html "Global OP Shortcut").
Internal OP `iop` - Sequence header for internal operators.
Shortcut `iop0shortcut` - Specifies a name you can use anywhere inside the component as a path to "Internal OP" below. See [Internal Operators](Internal_Operators.html "Internal Operators").
OP `iop0op` - The path to the Internal OP inside this component. See [Internal Operators](Internal_Operators.html "Internal Operators").

Node View `nodeview` - ⊞ - Determines what is displayed in the node viewer, also known as the [Node Viewer](Node_Viewer.html "Node Viewer"). Some options will not be available depending on the Component type ([Object Component](Object_Component.html "Object Component"), [Panel Component](Panel_Component.html "Panel Component"), Misc.)
* Default Viewer `default` - Displays the default viewer for the component type, a 3D Viewer for Object COMPS and a Control Panel Viewer for Panel COMPs.
* Operator Viewer `opviewer` - Displays the node viewer from any operator specified in the Operator Viewer parameter below.
Operator Viewer `opviewer` - Select which operator's node viewer to use when the Node View parameter above is set to Operator Viewer.
Enable Cloning `enablecloning` - Control if the OP should be actively cloneing. Turning this off causes this node to stop cloning it's 'Clone Master'.
Enable Cloning Pulse `enablecloningpulse` - Instantaneously clone the contents.
Clone Master `clone` - Path to a component used as the Master [Clone](Clone.html "Clone").
Load on Demand `loadondemand` - Loads the component into memory only when required. Good to use for components that are not always used in the project.
Enable External .tox `enableexternaltox` - When on (default), the external .tox file will be loaded when the .toe starts and the contents of the COMP will match that of the external .tox. This can be turned off to avoid loading from the referenced external .tox on startup if desired (the contents of the COMP are instead loaded from the .toe file). Useful if you wish to have a COMP reference an external .tox but not always load from it unless you specifically push the Re-Init Network parameter button.
Enable External .tox Pulse `enableexternaltoxpulse` - This button will re-load from the external `.tox` file (if present).
External .tox Path `externaltox` - Path to a `.tox` file on disk which will source the component's contents upon start of a `.toe`. This allows for components to contain networks that can be updated independently. If the `.tox` file can not be found, whatever the `.toe` file was saved with will be loaded.
Reload Custom Parameters `reloadcustom` - When this checkbox is enabled, the values of the component's [Custom Parameters](Custom_Parameters.html "Custom Parameters") are reloaded when the [.tox](-2.html ".tox") is reloaded. This only affects top-level parameters on the component, all parameters on nodes inside the component are always reloaded with the [.tox](-2.html ".tox").
Reload Built-In Parameters `reloadbuiltin` - When this checkbox is enabled, the values of the component's built-in parameters are reloaded when the [.tox](-2.html ".tox") is reloaded. This only affects top-level parameters on the component, all parameters on nodes inside the component are always reloaded with the [.tox](-2.html ".tox").
Save Backup of External `savebackup` - When this checkbox is enabled, a backup copy of the component specified by the External `.tox` parameter is saved in the `.toe` file. This backup copy will be used if the External `.tox` can not be found. This may happen if the `.tox` was renamed, deleted, or the `.toe` file is running on another computer that is missing component media.
Sub-Component to Load `subcompname` - When loading from an External `.tox` file, this option allows you to reach into the `.tox` and pull out a COMP and make that the top-level COMP, ignoring everything else in the file (except for the contents of that COMP). For example if a `.tox` file named `project1.tox` contains `project1/geo1`, putting `geo1` as the Sub-Component to Load, will result in `geo1` being loaded in place of the current COMP. If this parameter is blank, it just loads the `.tox` file normally using the top level COMP in the file.
Relative File Path Behavior `relpath` - ⊞ - Set whether the child file paths within this COMP are relative to the .toe itself or the .tox, or inherit from parent.
* Use Parent's Behavior `inherit` - Inherit setting from parent.
* Relative to Project File (.toe) `project` - The path, when specified as a relative path, will be relative to the .toe file.
* Relative to External COMP File (.tox) `externaltox` - The path, when specified as a relative path, will be relative to the .tox file. When no external COMP file is specified, or when Enable External .tox is not toggled on, this doesn't have any impact.
  

  

## Info CHOP Channels
Extra Information for the Geometry COMP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Common COMP Info Channels
* num\_children - Number of children in this component.
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
  
TouchDesigner Build: Latest\nwikieditorwikieditormw-replace2021.100002020.200002018.28070before 2018.28070
| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • [Animation](Animation_COMP.html "Animation COMP") • [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • [Constraint](Constraint_COMP.html "Constraint COMP") • [Container](Container_COMP.html "Container COMP") • [Engine](Engine_COMP.html "Engine COMP") • [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • [FBX](FBX_COMP.html "FBX COMP") • [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • [Geo Text](Geo_Text_COMP.html "Geo Text COMP") • Geometry• [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • [Impulse Force](Impulse_Force_COMP.html "Impulse Force COMP") • [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Palette:depthProjection](Palette_depthProjection.html "Palette:depthProjection") • [Parameter](Parameter_COMP.html "Parameter COMP") • [Replicator](Replicator_COMP.html "Replicator COMP") • [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • [Text](Text_COMP.html "Text COMP") • [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • [Window](Window_COMP.html "Window COMP") |
An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.

MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.

Hierarchy relates components with other components. There are two groups of Hierarchy in TouchDesigner. 3D Object Components, and 2D Panel Components. Hierarchies let one component to be positioned relative to another. Each group can be connected via lines between the bottoms/tops of nodes in a network, or by placing one component inside the other.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A Geometry Component is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

(1) A Geometry Component can instance and render its SOP geometry many times: once for each sample in a CHOP, row of a DAT table, pixel in a TOP, or point of a SOP, (2) An instance is an OP that doesn't actually have its own data, but rather just refers to an OP (or has an input) whose data it uses. This includes Null OPs, Switch OPs and in some cases Select OPs.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

Operators that need 1 or more inputs are called Filters in TouchDesigner, like a Math CHOP. See [Generator](Generator.html "Generator").

The 3D data held in SOPs and passed for rendering by the Geometry COMP.

Any component can be extended with its own Python classes which contain python functions and data.

A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.

A name for a component that is accessible from any node in a project, which can be declared in a component's Global Operator Shortcut parameter.

Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").

Cloning makes multiple components match the contents of a master component. A [Component](Component.html "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the [Replicator COMP](Replicator_COMP.html "Replicator COMP").

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").

Retrieved from "<https://docs.derivative.ca/index.php?title=Geometry_COMP&oldid=33041>"
[Categories](Special_Categories.html "Special:Categories"):
* [Touch Glossary](Category_Touch_Glossary.html "Category:Touch Glossary")
* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")