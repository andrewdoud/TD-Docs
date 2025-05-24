

Geo Text COMP - TouchDesigner Documentation





























# Geo Text COMP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Geo Text COMP renders text in 3D. It does not read or generate a SOP as it does direct rendering using the [Slug Library](Slug_Library.html "Slug Library") and can be lit and textured with any [MAT](MAT.html "MAT") material.

You can set fonts, colors, sizes, bold, italic, tracking, multi-lines like you can with the [Text COMP](Text_COMP.html "Text COMP"). But because the Geo Text COMP doesn't have a boundary, width or height like the Text COMP, we substitute it with a layout box and the Layout Box parameters. The layout box has a width and height, and by default the bottom left of the layout box is placed at 0,0,0 in 3D space of the Geo Text COMP ("object space"). The Layout Box Anchor U and V let you put the center of the layout box at 0,0,0 by setting the anchors to .5, 5.

The layout box's size although you can't see it by default, is the Layout Box Size parameter. With that you can right-justify or top-justify text in the layout box, and clip to the layout box. You can also pad space aroud each side of the layout box.

See also the 2D equivalent [Text COMP](Text_COMP.html "Text COMP"). See [Text Formatting Codes](https://docs.derivative.ca/Text_Formatting_Codes "Text Formatting Codes") for ways to override settings per-character.

**Render multiple strings transformed separately**: The Specification DAT and Specification CHOP allow for individual strings to be each positioned and styled independently in 3D.

Every row of the Spec DAT represents a "block" or "text block". Every Spec DAT contains a column named `text` which is the string that overrides the Text parameter.

Most columns override a Geo Text COMP parameter, such as `text`, `tx` and `fontsize`. Some column names noted below have no corresponding parameter.

The Spec CHOP can also specify values per block. When including a Spec CHOP the number of Spec CHOP samples needs to be the same number of rows as the Spec DAT following the first column header.

Parameters that can be overrided include `fontsize`, `fontcolor`, tracking etc., plus all the layout box and alignment parameters. Font/bold/italic are supported as columns as they are separate fonts.

**Transforming text blocks**: The column or channel names can include `tx`, `ty`, `tz` and all the rotate and scale channels (which use the Transform Order parameter).

A special column/channel called `append` can be used, when `append` is `1`, to position one block of text relative to the end of the previous block. Regular transforms are inherited by each appended text block.

Local transforms (`ltx`, `lrz`, etc), can be used to apply additional transforms to a block that are not inherited by appended blocks. If the special column/channel `localxform` is set to '`pre`', then the local transform is applied in world space before the inherited transforms are applied.

**Note** - The Geo Text COMP uses **blending/transparency** to create the glyphs floating in space (Each glyph is a partially transparent rectangle), so to view properly without the enclosing polygons that surround them, you need to ensure they are drawn after other geometry that they are sitting in-front of. This is usually due using the [Draw Priority](#Parameters_-_Render_Page) parameter on the 'Render' parameter page and making the value more negative than the Draw Priority of other objects. All things with the highest draw priority are drawn first, then all things with the same second higher draw priority are drawn second. If the priority is the same between two objects, then the order they are drawn is arbitrary and will possibly change. **Note**: Text within a Spec DAT should be setup so things in the back are earlier in the table than things in the front. It will draw row-by-row from the Spec DAT.

See OP Snippets for further transform options - `relative` and `append`.

The Geo Text COMP is similar to the [Text COMP](Text_COMP.html "Text COMP") which is a 2D [Panel](Panel.html "Panel").

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[geotextCOMP\_Class](https://docs.derivative.ca/GeotextCOMP_Class "GeotextCOMP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Text Page](#Parameters_-_Text_Page)
* [3 Parameters - Font Page](#Parameters_-_Font_Page)
* [4 Parameters - Xform Page](#Parameters_-_Xform_Page)
* [5 Parameters - Pre-Xform Page](#Parameters_-_Pre-Xform_Page)
* [6 Parameters - Instance Page](#Parameters_-_Instance_Page)
* [7 Parameters - Instance 2 Page](#Parameters_-_Instance_2_Page)
  + [7.1 Instance Texturing](#Instance_Texturing)
* [8 Parameters - Instance 3 Page](#Parameters_-_Instance_3_Page)
* [9 Parameters - Render Page](#Parameters_-_Render_Page)
* [10 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [11 Parameters - Common Page](#Parameters_-_Common_Page)

  


## Parameters - Text Page

Mode `mode` - ⊞ - Controls where text is generated from. Either from the 'Text' parameter, or a table DAT provided via the 'Specification DAT' parameter.

* Text `text` - The text will be generated using the contents of the 'Text' parameter.

* Specification DAT `specdat` - The text will be generated using rows and channels from the 'Specification DAT' or 'Specification CHOP' parameters.

Text `text` - When in 'Text' mode, this specifies the text that will be rendered.
Specification DAT `specdat` - In this mode, the Text parameter is ignored and data is taken from a DAT table given in the Specification DAT parameter. Each row of the DAT is a separate line of text, which can have different transforms, alignment, color, word wrap settings applied to them. The column headers should match the parameter name which the column is overriding. If a column entry for a particular row is left empty, then the value of the parameter is used instead. This allows a default value to be used for all rows, but allowing select rows to have different settings as needed. Transforms are not overridden, any transform that is given is applied as a pre-transform before the other transforms given by the parameters. Valid columns are currently: `text, tx, ty, tz, rx, ry, rz, sx, sy, sz, px, py, pz, ltx, lty, ltz, lrx, lry, lrz, lsx, lsy, lsz, lpx, lpy, lpz, fontcolorr, fontcolorg, fontcolorb, fontalpha, alignx, aligny, alignymode, fontsize, tracking, skew, horzstretch, linespacing, wordwrap, layoutsizew, layoutsizeh, layoutanchoru, layoutanchorv, textpaddingl, textpaddingr, textpaddingb, textpaddingt, render, append, localxform`.
Specification CHOP `specchop` - Allows use of CHOP data to set parameters of text blocks defined in the Specification DAT. Each sample of the CHOP corresponds to the data rows in the Specification DAT. Only numerical data such as `tx, ty, rz, fontcolorr`, etc can be provided by the CHOP.
Sort by Depth `sorted` - Only available when using a Specification DAT. When enabled, lines in the specification DAT are rendered from back to front relative to the current camera to allow for proper alpha blending. Note: sorting a large number of text blocks can cause performance issues, so this should only be enabled if regular alpha blending is not sufficient.
Formatting Codes `formatcodes` - Enables the use of formatting codes in the text. For example, the code {#color(255, 0, 0);} will turn all text afterwards on that line red. See [Text Formatting Codes](https://docs.derivative.ca/Text_Formatting_Codes "Text Formatting Codes") for all available codes.
Parse Escape Sequences `escapeseq` - When enabled, '\t' sequences will be converted to tabs and '\r' or '\n' to line breaks. This feature is only enabled when using the Specification DAT. For Text mode, python expressions should be used when escape sequences are needed.
Smart Punctuation `smartpunct` - Enables the use of smart punctuation. For example, pairs of quotes will be replaced with appropriate angled quotes, 3 periods will be replaced with an ellipses character and two hypens will become an em-dash.
Word Wrap `wordwrap` - Wrap lines of text if they go beyond the width of the layout box.

  


## Parameters - Font Page

Font `font` - ⊞ - Select the font to be used from the dropdown menu. Available fonts are those that have been registered with the operating system. There may be a delay when selecting fonts that have not been used before as the system creates the necessary intermediate files required for rendering.

* Arial `Arial` -

* Adobe Devanagari `Adobe Devanagari` -

* Arial Black `Arial Black` -

* BIZ UDGothic `BIZ UDGothic` -

* BIZ UDMincho Medium `BIZ UDMincho Medium` -

* BIZ UDPGothic `BIZ UDPGothic` -

* BIZ UDPMincho Medium `BIZ UDPMincho Medium` -

* Bahnschrift `Bahnschrift` -

* Bahnschrift Condensed `Bahnschrift Condensed` -

* Bahnschrift Light `Bahnschrift Light` -

* Bahnschrift Light Condensed `Bahnschrift Light Condensed` -

* Bahnschrift Light SemiCondensed `Bahnschrift Light SemiCondensed` -

* Bahnschrift SemiBold `Bahnschrift SemiBold` -

* Bahnschrift SemiBold Condensed `Bahnschrift SemiBold Condensed` -

* Bahnschrift SemiBold SemiCondensed `Bahnschrift SemiBold SemiCondensed` -

* Bahnschrift SemiCondensed `Bahnschrift SemiCondensed` -

* Bahnschrift SemiLight `Bahnschrift SemiLight` -

* Bahnschrift SemiLight Condensed `Bahnschrift SemiLight Condensed` -

* Bahnschrift SemiLight SemiCondensed `Bahnschrift SemiLight SemiCondensed` -

* Book Antiqua `Book Antiqua` -

* Bookshelf Symbol 7 `Bookshelf Symbol 7` -

* Calibri `Calibri` -

* Calibri Light `Calibri Light` -

* Cambria `Cambria` -

* Cambria Math `Cambria Math` -

* Candara `Candara` -

* Candara Light `Candara Light` -

* Century `Century` -

* Century Gothic `Century Gothic` -

* Comic Sans MS `Comic Sans MS` -

* Consolas `Consolas` -

* Constantia `Constantia` -

* Corbel `Corbel` -

* Corbel Light `Corbel Light` -

* Courier New `Courier New` -

* Ebrima `Ebrima` -

* Franklin Gothic Medium `Franklin Gothic Medium` -

* Gabriola `Gabriola` -

* Gadugi `Gadugi` -

* Georgia `Georgia` -

* Graphium `Graphium` -

* HoloLens MDL2 Assets `HoloLens MDL2 Assets` -

* Impact `Impact` -

* Ink Free `Ink Free` -

* Javanese Text `Javanese Text` -

* Leelawadee UI `Leelawadee UI` -

* Leelawadee UI Semilight `Leelawadee UI Semilight` -

* Lucida Console `Lucida Console` -

* Lucida Sans Unicode `Lucida Sans Unicode` -

* MS Gothic `MS Gothic` -

* MS Mincho `MS Mincho` -

* MS Outlook `MS Outlook` -

* MS PGothic `MS PGothic` -

* MS PMincho `MS PMincho` -

* MS Reference Sans Serif `MS Reference Sans Serif` -

* MS Reference Specialty `MS Reference Specialty` -

* MS UI Gothic `MS UI Gothic` -

* MT Extra `MT Extra` -

* MV Boli `MV Boli` -

* Malgun Gothic `Malgun Gothic` -

* Malgun Gothic Semilight `Malgun Gothic Semilight` -

* Marlett `Marlett` -

* Material Design Icons `Material Design Icons` -

* Material Design Icons Desktop `Material Design Icons Desktop` -

* Meiryo `Meiryo` -

* Meiryo UI `Meiryo UI` -

* Microsoft Himalaya `Microsoft Himalaya` -

* Microsoft JhengHei `Microsoft JhengHei` -

* Microsoft JhengHei Light `Microsoft JhengHei Light` -

* Microsoft JhengHei UI `Microsoft JhengHei UI` -

* Microsoft JhengHei UI Light `Microsoft JhengHei UI Light` -

* Microsoft New Tai Lue `Microsoft New Tai Lue` -

* Microsoft PhagsPa `Microsoft PhagsPa` -

* Microsoft Sans Serif `Microsoft Sans Serif` -

* Microsoft Tai Le `Microsoft Tai Le` -

* Microsoft YaHei `Microsoft YaHei` -

* Microsoft YaHei Light `Microsoft YaHei Light` -

* Microsoft YaHei UI `Microsoft YaHei UI` -

* Microsoft YaHei UI Light `Microsoft YaHei UI Light` -

* Microsoft Yi Baiti `Microsoft Yi Baiti` -

* MingLiU-ExtB `MingLiU-ExtB` -

* MingLiU\_HKSCS-ExtB `MingLiU_HKSCS-ExtB` -

* Mongolian Baiti `Mongolian Baiti` -

* Myanmar Text `Myanmar Text` -

* NSimSun `NSimSun` -

* Nirmala UI `Nirmala UI` -

* Nirmala UI Semilight `Nirmala UI Semilight` -

* Noto Sans CJK JP `Noto Sans CJK JP` -

* Open Sans `Open Sans` -

* Open Sans Light `Open Sans Light` -

* Open Sans SemiBold `Open Sans SemiBold` -

* PMingLiU-ExtB `PMingLiU-ExtB` -

* PT Mono `PT Mono` -

* Palatino Linotype `Palatino Linotype` -

* Roboto `Roboto` -

* Roboto Black `Roboto Black` -

* Roboto Condensed `Roboto Condensed` -

* Roboto Medium `Roboto Medium` -

* Segoe MDL2 Assets `Segoe MDL2 Assets` -

* Segoe Print `Segoe Print` -

* Segoe Script `Segoe Script` -

* Segoe UI `Segoe UI` -

* Segoe UI Black `Segoe UI Black` -

* Segoe UI Emoji `Segoe UI Emoji` -

* Segoe UI Historic `Segoe UI Historic` -

* Segoe UI Light `Segoe UI Light` -

* Segoe UI Semibold `Segoe UI Semibold` -

* Segoe UI Semilight `Segoe UI Semilight` -

* Segoe UI Symbol `Segoe UI Symbol` -

* SimSun `SimSun` -

* SimSun-ExtB `SimSun-ExtB` -

* Sitka Banner `Sitka Banner` -

* Sitka Display `Sitka Display` -

* Sitka Heading `Sitka Heading` -

* Sitka Small `Sitka Small` -

* Sitka Subheading `Sitka Subheading` -

* Sitka Text `Sitka Text` -

* Sylfaen `Sylfaen` -

* Symbol `Symbol` -

* TSTAR TW PRO `TSTAR TW PRO` -

* Tahoma `Tahoma` -

* Times New Roman `Times New Roman` -

* Trebuchet MS `Trebuchet MS` -

* UD Digi Kyokasho N-B `UD Digi Kyokasho N-B` -

* UD Digi Kyokasho N-R `UD Digi Kyokasho N-R` -

* UD Digi Kyokasho NK-B `UD Digi Kyokasho NK-B` -

* UD Digi Kyokasho NK-R `UD Digi Kyokasho NK-R` -

* UD Digi Kyokasho NP-B `UD Digi Kyokasho NP-B` -

* UD Digi Kyokasho NP-R `UD Digi Kyokasho NP-R` -

* Verdana `Verdana` -

* Webdings `Webdings` -

* Wingdings `Wingdings` -

* Wingdings 2 `Wingdings 2` -

* Wingdings 3 `Wingdings 3` -

* Yu Gothic `Yu Gothic` -

* Yu Gothic Light `Yu Gothic Light` -

* Yu Gothic Medium `Yu Gothic Medium` -

* Yu Gothic UI `Yu Gothic UI` -

* Yu Gothic UI Light `Yu Gothic UI Light` -

* Yu Gothic UI Semibold `Yu Gothic UI Semibold` -

* Yu Gothic UI Semilight `Yu Gothic UI Semilight` -

* Yu Mincho `Yu Mincho` -

* Yu Mincho Demibold `Yu Mincho Demibold` -

* Yu Mincho Light `Yu Mincho Light` -

Font File `fontfile` - Specify a font file to be used for rendering the text. This option can be used for fonts that are not registered with the operating system and do not appear in the drop down menu.
Bold `bold` - Display the text in **bold**.
Italic `italic` - Display the text in *italics*.
Font Size `fontsize` - The font size. This is in the same units as the geometry space. So it's arbitrary based on the size of your scene.
Tracking `tracking` - Sets the horizontal spacing between characters, where 0 is default spacing, > 0 is increased spacing and < 0 is decreased spacing.
Skew `skew` - Tilts the top of the characters forwards or backwards relative to the baseline.
Horz Stretch `horzstretch` - Horizontally stretch the characters relative to their current alignment.
Line Spacing `linespacing` - Adjust spacing between lines. The value is a multiplier of the default spacing defined by the font.
Font Color `fontcolor` - ⊞ - The color for the font.

* Font Color `fontcolorr` -

* Text Color `fontcolorg` -

* Text Color `fontcolorb` -

* Font Color `fontcolorg` -

* Font Color `fontcolorb` -

Font Alpha `fontalpha` - The alpha value for the font.
Layout Box Anchor U `layoutanchoru` - Along with the Layout Box Anchor V, this allows shifting the layout box from it's current position left/down. It also controls how rotations will pivot around the layout box, so a 0.5, 0.5 anchor will cause rotations to move about the center of the layout box.
Layout Box Anchor V `layoutanchorv` - The V component of the Layout Box Anchor pair.
Layout Box Size `layoutsize` - ⊞ - Text is aligned and word-wrapped within a virtual layout box. This box is what is transformed by the various transform parameters, and then the text is aligned and laid out within that. The width and height units are the same units as the font size.

* Layout Box Size `layoutsizew` -

* Layout Box Size `layoutsizeh` -

Clip to Layout Box `cliptolayoutbox` - When enabled, text that falls outside of the layout box will not be drawn.
Text Padding `textpadding` - ⊞ - Move the text a minimum distance from the edge of the layout box.

* Text Padding `textpaddingl` -

* Text Padding `textpaddingr` -

* Text Padding `textpaddingb` -

* Text Padding `textpaddingt` -

Horizontal Align `alignx` - ⊞ - Controls the horizontal alignment of the text.

* Left `left` -

* Center `center` -

* Right `right` -

Vertical Align `aligny` - ⊞ - Controls the vertical alignment of the text.

* Top `top` -

* Center `center` -

* Bottom `bottom` -

Vertical Align Mode `alignymode` - ⊞ - Controls how the alignment is calculated for vertical alignment.

* Use Font Metrics `metrics` - Uses the font defined layout information, ascender size, descender size etc. to layout the box. This provides consistent alignment regardless of the text contents.

* Use Text Bounding Box `bbox` - The alignment will be based on the bounding box of the current text string. This can cause the string to move up/down as the text changes. Useful to perfectly align static text that would otherwise be offset due to the character size and standard layout not resulting in the text being perfectly centered.

Padding `textpadding` - ⊞ - Extra padding to add to the sides of the layout box, pushing the text inwards for alignment.

* Padding `textpaddingl` - Padding on the left.

* Padding `textpaddingr` - Padding on the right.

* Padding `textpaddingb` - Padding on the bottom.

* Padding `textpaddingt` - Padding on the top.

  


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

  

TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2023.112802022.24140before 2022.24140

| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • [Animation](Animation_COMP.html "Animation COMP") • [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • [Constraint](Constraint_COMP.html "Constraint COMP") • [Container](Container_COMP.html "Container COMP") • [Engine](Engine_COMP.html "Engine COMP") • [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • [FBX](FBX_COMP.html "FBX COMP") • [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • Geo Text• [Geometry](Geometry_COMP.html "Geometry COMP") • [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • [Impulse Force](Impulse_Force_COMP.html "Impulse Force COMP") • [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Parameter](Parameter_COMP.html "Parameter COMP") • [Replicator](Replicator_COMP.html "Replicator COMP") • [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • [Text](Text_COMP.html "Text COMP") • [Experimental:Text](https://docs.derivative.ca/Experimental:Text_COMP "Experimental:Text COMP") • [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • [Window](Window_COMP.html "Window COMP") |

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.


(1) The TouchDesigner window is made of a menu bar at the top, a [Timeline](Timeline.html "Timeline") at the bottom, plus one of a choice of Layouts in the middle. A Layout is made on one or more Panes, each Pane can contain a Network Editor, Viewer, Panel, etc. See [Pane](Pane.html "Pane") and [Bookmark](Bookmark.html "Bookmark"). (2) Nodes in a network are arranged using Layout commands in the RMB menu.


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


[OP Snippets](OP_Snippets.html "OP Snippets") is a set of 700+ live examples of TouchDesigner operators. You can access snippets via the Help menu, or by right-clicking on network operators, or r-clicking on OP Create dialog items.


Unicode text is fully supported in TouchDesigner. Unicode can be typed into parameters, DATs, Python scripts etc. Unicode encoded text files can be loaded into DATs. File paths can include any unicode character that is legal for a file path.


A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").

The grey dashed lines between nodes is a Reference (or [Link](Link.html "Link")). A Reference is (1) a [Parameter Reference](Parameter_Reference.html "Parameter Reference"), a parameter in an OP that is a name or path to another operator, (2) a [Node Reference](https://docs.derivative.ca/index.php?title=Node_Reference&action=edit&redlink=1 "Node Reference (page does not exist)"), an expression in a parameter or DAT script that contains the name or path of another operator, (3) a DAT Cell Reference or (4) a CHOP Channel Reference.

A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").


MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.


A set of commands located in a Text DAT that are triggered to run under certain conditions. There are two scripting languages in TouchDesigner: [Python](Python.html "Python") and the original [Tscript](Tscript.html "Tscript"). Scripts and single-line commands can also be run in the [Textport](Textport.html "Textport").


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


Hierarchy relates components with other components. There are two groups of Hierarchy in TouchDesigner. 3D Object Components, and 2D Panel Components. Hierarchies let one component to be positioned relative to another. Each group can be connected via lines between the bottoms/tops of nodes in a network, or by placing one component inside the other.


The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").


(1) A [Geometry Component](Geometry_COMP.html "Geometry COMP") can instance and render its SOP geometry many times: once for each sample in a CHOP, row of a DAT table, pixel in a TOP, or point of a SOP, (2) An instance is an OP that doesn't actually have its own data, but rather just refers to an OP (or has an input) whose data it uses. This includes Null OPs, Switch OPs and in some cases Select OPs.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


Operators that need 1 or more inputs are called Filters in TouchDesigner, like a Math CHOP. See [Generator](Generator.html "Generator").


The 3D data held in SOPs and passed for rendering by the [Geometry COMP](Geometry_COMP.html "Geometry COMP").


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







Retrieved from "<https://docs.derivative.ca/index.php?title=Geo_Text_COMP&oldid=33770>"
[Category](Special_Categories.html "Special:Categories"):

* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")