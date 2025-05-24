

FBX COMP - TouchDesigner Documentation





























# FBX COMP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The FBX COMP imports geometry, animations and scenes using the FBX file format from Maya, 3DS Max, Cinema4D, Houdini and others.
The FBX COMP currently uses the 2020.3.7 (VS2022) version of the FBX SDK.

[FBX](https://www.autodesk.com/products/fbx/overview) is a file format and set of libraries from Autodesk that is used to exchange models, animations and image/texture data between applications. The FBX COMP reads FBX files and supports most of its features. You can drag-drop a `.fbx` into a TouchDesigner network or import it via the File > Import File... menu. The FBX COMP can also import meshes from .obj and .4ds files, see also [File Types](File_Types.html "File Types").

The assets from the FBX file are saved into a "`.tdc`" file with the same name as the FBX file inside the `TDImportCache` folder, which is created next to your `.toe` file. Assets are read from the "`.tdc`" file using Import Select OPs ([Import Select TOP](Import_Select_TOP.html "Import Select TOP") / [Import Select SOP](Import_Select_SOP.html "Import Select SOP") / [Import Select CHOP](Import_Select_CHOP.html "Import Select CHOP")). Upon reloading a `.toe` file, the assets can be imported directly from the "`.tdc`" cache, and the FBX file will not need to be re-imported. However, if there is no existing "`.tdc`" (for instance, if the toe file changed computers) then the FBX file will be reopened to grab the assets and a new "`.tdc`" will be saved out.

To open an FBX file in an FBX COMP:

1) Specify a valid file path in the "FBX File" parameter, including the name of the file with correct `.fbx` extension.

2) This step is varied depending on whether the FBX COMP is just created and if any changes in the default values of parameters are required or not. If the file is being loaded for the first time in the network and the default parameter values are accepted then simply press the "Import" button to generate the FBX network and import the assets. Note that we recommend changing the "Import Method" to to other modes (less work) can significantly improve performance. Generally, any changes in the parameters above the "Import" button requires the network to be built again.

3) With the "Import Method" menu set to "Merge with Existing", the "Import" pulse will reload the internal assets (e.g. meshes, etc.) and this is specifically useful if the file has moved to another location and when the `.toe` file is opened the assets were not found and reloaded properly.

4) With the "Import Method" menu set to "Import Assets (Import Selects)", the "Import" button is used when some changes on FBX file are made and we want to merge those changes into the current network without fully rebuilding it.

**Animation channels**: When there is animation in the FBX file, use the controls on the Play page to initialize, start and guide the animation. Also create an [Info CHOP](Info_CHOP.html "Info CHOP") and attach it to the FBX COMP to watch its animation timing. The Info CHOP channels are similar to those of the [Timer CHOP](Timer_CHOP.html "Timer CHOP").

**Textures**: Textures can either be embedded within the FBX file or external and referenced by a path to a texture file. For example, Blender has an option during FBX export to embed, otherwise they'll be external. If they're external then they may be exported with an absolute path to the texture file, which means if you move the FBX file to a different machine or relocate the file, then the textures will fail to load. In this case, if you are unable to re-export to embed the textures, then you can instead specify a search directory using the Texture Directory parameter so that the FBX COMP knows where to locate the texture files at import.

See also: [FBX](FBX.html "FBX"), [Import Select CHOP](Import_Select_CHOP.html "Import Select CHOP"), [Import Select TOP](Import_Select_TOP.html "Import Select TOP"), [Import Select SOP](Import_Select_SOP.html "Import Select SOP"), [USD COMP](USD_COMP.html "USD COMP")

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[fbxCOMP\_Class](https://docs.derivative.ca/FbxCOMP_Class "FbxCOMP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - FBX Page](#Parameters_-_FBX_Page)
* [3 Parameters - Play Page](#Parameters_-_Play_Page)
* [4 Parameters - Xform Page](#Parameters_-_Xform_Page)
* [5 Parameters - Pre-Xform Page](#Parameters_-_Pre-Xform_Page)
* [6 Parameters - Render Page](#Parameters_-_Render_Page)
* [7 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [8 Parameters - Common Page](#Parameters_-_Common_Page)
* [9 Info CHOP Channels](#Info_CHOP_Channels)
  + [9.1 Specific FBX COMP Info Channels](#Specific_FBX_COMP_Info_Channels)
  + [9.2 Common COMP Info Channels](#Common_COMP_Info_Channels)
  + [9.3 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - FBX Page

**NOTE:** changes to any of the below parameters aren’t applied until the FBX File is rebuilt, either through "Build Network" or "Update".

FBX File `file` - The FBX file to import.
Import Method `importmethod` - ⊞ - Determines what to do when clicking the 'Import' button below.

* Full Replacement `full` - Fully rebuilds the network inside the FBX COMP and reloads the assets from the FBX file.

* Merge with Existing `merge` - Merges any changes in the FBX file with the existing contents of the FBX COMP.

* Reload Assets (Import Selects) `reload` - Assets that are loaded into Import Select operators (geos, textures, animations) are reloaded into the existing FBX COMP's network from the FBX file.

Import `imp` - A pulse to import the contents based on the setting in the 'Import Method' parameter above.
Import Scale `importscale` - Scales the imported geometry as a multipier.
Texture Directory `texdir` - Specifies an additional search location for external texture files if they can't be found at the default location specified inside the FBX file.
Lights `lights` - When enabled the FBX COMP will import any lights within the FBX File.
Cameras `cameras` - When enabled the FBX COMP will import any cameras within the FBX File.
Generate Actor COMPs `genactors` - When enabled, will generate Actor COMPs in place of Geometry COMPs as the parents' of Import Select SOPs. This is useful for working with [Bullet Dynamics](Bullet_Dynamics.html "Bullet Dynamics") systems with your imported geometry.
Merge Geometry `mergegeo` - When enabled the FBX COMP will merge Geometry COMPs. Geometry COMPs are merged if they have only default parameters except transform. If they have the same material then their Import Select SOPs will be merged.
Merge Level `mergelevel` - When enabled the FBX COMP will attempt to merge up to the desired “level”. Level is how many steps down a node is from the root (FBX COMP). If its level is higher than the merge level and it is mergeable then it will be merged upward.
Primitive Groups `primgroups` - When enabled the FBX COMP will put each merged SOP into its own primitive group, so that they can be split up later if need be.
Max Wired Children `maxwiredchildren` - Any COMPs that have more wired children than this parameter will have those wired children converted to internal children of the COMP. This maintains parenting but can cleanup networks.
Direct to GPU `gpudirect` - Load the geometry directly to the GPU.
Keep Parameters `keepparams` - When enabled, any parameter conflicts during update will keep the user changes. When disabled, any user changes to parameters may be overwritten.
Keep Connections `keepconnections` - When enabled, any wiring/connection conflicts during update will keep the user changes. When disabled, any user changes to wiring/connections may be overwritten.
Callbacks DAT `callbacks` - The Callbacks DAT will execute during import or update allowing for modification and customization of the imported operators and resulting network.

  


## Parameters - Play Page

This page includes the animation controls parameters of FBX within TouchDesigner.

Animation `animation` - Specifies the animation name (if any is specified) to playback from the imported FBX.
Shift Animation Start `shiftanimationstart` - A toggle to specify whether to shift the animation to the start of animation indicated in the importing file.
Sample Rate Mode `sampleratemode` - ⊞ - Select between using the 'File FPS' embedded in the FBX file or setting a 'Custom' sample rate.

* File FPS `filefps` -

* Custom `custom` -

Sample Rate `samplerate` - Set the sample rate when the "Sample Rate Mode" parameter above is set to 'Custom'.
Play Mode `playmode` - ⊞ - A menu to specify the method used to play the animation.

* Locked to Timeline `lockedtotimeline` - This mode locks the animation position to the timeline. The parameters Play, Speed, Index, Cue and Cue Point, are disabled in this mode since the timeline is directly tied to animation position.

* Specify Index `specifyindex` - This mode allows the user to specify a particular index (position) in the animation using the Index parameter below. Use this mode for random access to any location in the animation.

* Sequential `sequential` - This mode continually plays regardless of the timeline position (the Index parameter is disabled). Play, Speed, Cue, and Cue Point parameters below are enabled to allow some control. The default is set to this value.

Initialize `initialize` - Resets the animation to its initial state.
Start `start` - Resets the animation to its initial state and starts playback.
Cue `cue` - Jumps to and holds at the Cue Point when set to 1. Only available when Play Mode is Sequential.
Cue Pulse `cuepulse` - Jumps to the Cue Point when pulsed. Only available when Play Mode is Sequential.
Cue Point `cuepoint` - Set any index in the animation as a point to jump to. Only available when Play Mode is Sequential.
Cue Point Unit `cuepointunit` - ⊞ - Select what type of unit to specify the Cue Point with.

* Frames `frames` -

* Seconds `seconds` -

* Fraction `fraction` -

* Index `indices` -

Play `play` - Animation plays when On and stops when Off. This animation playback control is only available when Play Mode is Sequential.
Index `index` - This parameter explicitly sets the animation position when Play Mode is set to Specify Index. The units menu on the right lets you specify the index in the following units: Index, Frames, Seconds, and Fraction (percentage)
Index Unit `indexunit` - ⊞ -

* Frames `frames` -

* Seconds `seconds` -

* Fraction `fraction` -

* Index `indices` -

Speed `speed` - This is a speed multiplier which only works when Play Mode is Sequential. A value of 1 is the default playback speed. A value of 2 is double speed, 0.5 is half speed and so on. Negative values will play backwards.
Trim `trim` - A toggle to enable the Trim Start and Trim End parameters.
Trim Start `tstart` - Sets an in point from the beginning of the animation, allowing you to trim the starting index of the animation. The units’ menu on the right let you specify this position by index, frames, seconds, or fraction (percentage).
Trim Start Unit `tstartunit` - ⊞ - Specifies a unit type for Trim Start. Changing this will convert the previous unit to the selected unit.

* Frames `frames` -

* Seconds `seconds` -

* Fraction `fraction` -

* Index `indices` -

Trim End `tend` - Sets an end point from the end of the movie, allowing you to trim the ending index of the animation. The units’ menu on the right let you specify this position by index, frames, seconds, or fraction (percentage).
Trim End Unit `tendunit` - ⊞ - Specifies a unit type for Trim End. Changing this will convert the previous unit to the selected unit.

* Frames `frames` -

* Seconds `seconds` -

* Fraction `fraction` -

* Index `indices` -

Extend Left `textendleft` - ⊞ - Determines how the animation behaves before the start of the animation (or Trim Start position if it is used).

* Hold `hold` -

* Cycle `cycle` -

* Mirror `mirror` -

Extend Right `textendright` - ⊞ - Determines how the animation behaves after the end of the animation (or Trim End position if it is used).

* Hold `hold` -

* Cycle `cycle` -

* Mirror `mirror` -

  


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

Extra Information for the FBX COMP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Specific FBX COMP Info Channels

* fbx\_file\_version -

* initializing -

* ready -

* running -

* done -

* timer\_fraction -

* timer\_seconds -

* timer\_index -

* playing\_seconds -

* running\_seconds -

* length\_seconds -

* cycles -

* file\_start\_index -

* file\_end\_index -

* file\_sample\_rate -

* sample\_rate -

* index -

* start\_index -

* end\_index -

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

  

TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2022.241402021.100002019.146502018.28070

| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • [Animation](Animation_COMP.html "Animation COMP") • [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • [Constraint](Constraint_COMP.html "Constraint COMP") • [Container](Container_COMP.html "Container COMP") • [Engine](Engine_COMP.html "Engine COMP") • [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • FBX• [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • [Geo Text](Geo_Text_COMP.html "Geo Text COMP") • [Geometry](Geometry_COMP.html "Geometry COMP") • [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • [Impulse Force](Impulse_Force_COMP.html "Impulse Force COMP") • [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Palette:depthProjection](Palette_depthProjection.html "Palette:depthProjection") • [Parameter](Parameter_COMP.html "Parameter COMP") • [Replicator](Replicator_COMP.html "Replicator COMP") • [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • [Text](Text_COMP.html "Text COMP") • [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • [Window](Window_COMP.html "Window COMP") |

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


TOuch Environment file, the file type used by TouchDesigner to save your entire project.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


Every component contains a network of operators that create and modify data. The operators are connected by wires that define where data is routed after the operator cooks its inputs and generates an output.


The 3D data held in SOPs and passed for rendering by the [Geometry COMP](Geometry_COMP.html "Geometry COMP").


A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").


A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.


The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.


The panel at the bottom of TouchDesigner, it controls the current global looping [Time](Time_COMP.html "Time COMP") your TouchDesigner project, or of just one component.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


Hierarchy relates components with other components. There are two groups of Hierarchy in TouchDesigner. 3D Object Components, and 2D Panel Components. Hierarchies let one component to be positioned relative to another. Each group can be connected via lines between the bottoms/tops of nodes in a network, or by placing one component inside the other.


The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.


An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


Any component can be extended with its own Python classes which contain python functions and data.


A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.


A name for a component that is accessible from any node in a project, which can be declared in a component's Global Operator Shortcut parameter.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.


The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.


A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").


Cloning makes multiple components match the contents of a master component. A [Component](Component.html "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the [Replicator COMP](Replicator_COMP.html "Replicator COMP").


TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.


There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").







Retrieved from "<https://docs.derivative.ca/index.php?title=FBX_COMP&oldid=33329>"
[Category](Special_Categories.html "Special:Categories"):

* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")