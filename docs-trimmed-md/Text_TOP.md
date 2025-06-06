

TouchDesigner Documentation





























# Text TOP

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]

The Text TOP displays text strings in an image. It allows for multiple fonts, sizes, colors, borders, character separation and line separation. The text can be displayed as bit maps, anti-aliased lines, or filled polygon characters. Any TrueType font can be rendered by the Text TOP. [Unicode](Unicode.html "Unicode") is supported. The new Scalable Display Method uses [Slug Library](Slug_Library.html "Slug Library") to render scalable, resolution independent text at the highest qulaity available in the Text TOP.

It can display simple text strings with embedded numeric values. It can also format lines of text and numbers in decimal or floating point format, reading the numbers from a CHOP, using special formatting characters.

It can also render text strings from a [Table DAT](Table_DAT.html "Table DAT") via the Specification DAT parameter, where column headings are the parameter names that are to ve overidden when rendering a line of text for reach row of the table.

Any [TrueType](http://en.wikipedia.org/wiki/TrueType) or [OpenType](http://en.wikipedia.org/wiki/OpenType) font that has been loaded into Windows can be rendered by the Text TOP. To import a new font into your Windows system, open the **Fonts** folder in the **Control Panel**, then drag and drop your  [font files](File_Types.html "File Types") in (`.ttf/.otf` file format). Fonts can also be specified as `.ttf/.otf` file paths in the Font File parameter.

You can render **Unicode** text by reading the text as a python string. See [Unicode](Unicode.html "Unicode").

**Tip:** You can use the [textTOP\_Class](TextTOP_Class.html "TextTOP Class").textWidth member to calculate the width of the text in the Text TOP.

See also: [Field COMP](Field_COMP.html "Field COMP"), [Text SOP](Text_SOP.html "Text SOP"), [Unicode](Unicode.html "Unicode").

[![TextTOP.jpg](https://docs.derivative.ca/images/3/36/TextTOP.jpg)](https://docs.derivative.ca/File:TextTOP.jpg)

[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[textTOP\_Class](TextTOP_Class.html "TextTOP Class")

## Contents

* [1 Summary](#Summary)
* [2 Parameters - Text Page](#Parameters_-_Text_Page)
* [3 Parameters - Font Page](#Parameters_-_Font_Page)
* [4 Parameters - Color Page](#Parameters_-_Color_Page)
* [5 Parameters - Output Page](#Parameters_-_Output_Page)
* [6 Parameters - Common Page](#Parameters_-_Common_Page)
* [7 Operator Inputs](#Operator_Inputs)
* [8 Info CHOP Channels](#Info_CHOP_Channels)
  + [8.1 Specific Text TOP Info Channels](#Specific_Text_TOP_Info_Channels)
  + [8.2 Common TOP Info Channels](#Common_TOP_Info_Channels)
  + [8.3 Common Operator Info Channels](#Common_Operator_Info_Channels)

  


## Parameters - Text Page

Field Component `field` - Specifies a [Field Component](Field_COMP.html "Field COMP") to use as the source of the text. The font and style of the text displayed in the Field Component are set using the parameters in the Text TOP.
DAT `dat` - Specifies a DAT to use for the source of the text. Drag and Drop a DAT onto this field, or manually enter the DAT's path.
DAT Row `rowindex` - The row number (starting from 0) of the cell, if the DAT is a table.
DAT Col `colindex` - The column number of the cell, if the DAT is a table.
Specification DAT `specdat` - A Table DAT that allows you to specify and position text by pixel, with the lower left corner being at 0, 0. Column headers must include `position1` or `x`, `position2` or `y`, and `text`. A sample table can be:
```
x	y	text		
0	0	lower left text		
100	100	somewhere in the middle

```

Text `text` - A string of text. It optionally can be followed by a numeric value and another post-string, as set with Value and Post Text below. If newlines or tabs are desired, the recommended way is to change this parameter to expression mode, and specify a Python string that includes \n or \t to signify newlines and tabs. E.g 'First Line\nSecond Line'.
Legacy Parsing `legacyparsing` - In older builds the syntax \XXX (E.g \200 would be character 200), \t, \n as well as [] and {} (to position strings) was parsed in the string. This is now deprecated. For specifying characters codes, \t and \n [Python syntax should be used instead.](https://docs.python.org/3.3/howto/unicode.html). The 'Specification DAT' should be used to position strings instead of [], {}. This parameter can be enabled to turn back on this legacy parsing though. If this is enabled and you want to display the characters `\ [ ] { }`, you must precede them with a `\`.
Append Value `appendvalue` - Enables the Value field defined below. This value is inserted between the Text string and the Post Text string.
Value `valuetouse` - The numeric value to display.
Total Digits `totaldigits` - The total number of digits in the value displayed.
Decimal Digits `decimaldigits` - The number of digits displayed after the decimal place.
Post Text `posttext` - The text string appended after Text and Value (if present).
CHOP Value %-Replace `chopvaluereplace` - Allows portions of the strings to be replaced by CHOP values via a syntax similar to C-style printf()/sprintf(). More details of the syntax are provided in the next parameter, 'CHOP' .
CHOP `chop` - The CHOP containing all the values to insert in the Text strings. The Text TOP will repeat the Text string until all CHOP channels are displayed. They are displayed by using a special syntax in your Text string, defined as string starting with `%`, for example `%4d`:
> `%[flags][width][.precision][type]`

* `flags` (optional) - Alignment options.
  + - : left align (text is right aligned by default)
  + 0 : pad the left side with zeros
* `width` (optional) - Total number of digits in the number displayed.
* `precision` (optional) - Number of digits after the decimal place.
* `type` - Number format.
  + d : integer
  + f : float
  + g : double, exponential format is used only when the exponent of the value is less than ?4.

Drag and Drop a CHOP onto this field, or manually enter the CHOP's path.

[![TextTOPCHOPValue.jpg](https://docs.derivative.ca/images/a/ad/TextTOPCHOPValue.jpg)](https://docs.derivative.ca/File:TextTOPCHOPValue.jpg)



Word Wrap `wordwrap` - When checked text is automatically line wrapped so it doesn't extend outside the TOP's borders. When using Word Wrap and Auto-Size together, the text will first word-wrap based on the specified font size, then auto size the resulting block of text.
Smart Quote `smartquote` - Enables smart quotes which use a left (opening) quotation mark and a right (closing) quotation mark instead of straight quotes.

  


## Parameters - Font Page

Font `font` - Select the font for the text from this drop down menu. All fonts are provided by Windows, any [TrueType](http://en.wikipedia.org/wiki/TrueType) font that is loaded into Windows can be used.
Font File `fontfile` - Specify any TrueType font file (`.ttf file`) to use for the text. When using a font file, the Font menu above is disabled.
Character Set `charset` - ⊞ - Select which character set to use.

* Unicode `unicode` -

* Symbol `symbol` -

Display Method `dispmethod` - ⊞ - The display method used.

* Automatic `automatic` - Automatically chooses which display mode to use based on font size and settings.

* Polygon `polygon` - Uses polygons to display the text. Polygons look better using large font sizes. They also support anti-aliasing (see Anti-Aliased below).

* Stroke `stroke` - Same as polygons but only an outline of the text is displayed.

* Bitmap `bitmap` - Uses bitmap images for the text. Bitmap fonts are better for very small font sizes where high precision is required.

* Scalable `scalable` - Uses [Slug Library](Slug_Library.html "Slug Library") to render high-quality, scalable, resolution independent text.

Anti-Alias `antialias` - ⊞ - Smoothes out the edges of the text. Not available for Texture Display Mode.

* 1x (Off) `aa1` -

* 2x `aa2` -

* 4x `aa4` -

* 8x (Medium) `aa8mid` -

* 8x (High) `aa8high` -

* 16x (Low) `aa16low` -

* 16x (Medium) `aa16mid` -

* 16x (High) `aa16high` -

* 32x `aa32` -

Stroke Width `strokewidth` - Controls the width of the outline when using Stroke Display Method.
Bold `bold` - Displays the text in **bold**.
Italic `italic` - Displays the text in *Italic*.
Auto-Size Font `fontautosize` - ⊞ - Automatically controls font size using one of the following 3 options. When using this feature along with Word Wrap turned on, it will first word-wrap the text based on the specified font size, then auto size the resulting block of text.

* No Auto-Fit `nofit` - Does not use any auto-fitting. Font Size specified in Font Size X and Font Size Y parameters.

* Auto-Fit Always `alwaysfit` - The font size will be increased or decreased so the text fits across the Text TOP from edge to edge.

* Auto-Fit if Too Large `fitiffat` - Only auto sizes the text if the text is too large and spills past the edges of the Text TOP. In this case the font size will be decreased to fit it within the borders of the TOP.

Font Size X `fontsizex` - Sets the font size in X (horizontal). **Note:** Floating point font sizes are permissable when using *Polygon* and *Outline* Display Methods.
Font Size X Unit `fontsizexunit` - Select the units for this parameter from Pixels, Fraction, Fraction Aspect or Points (font point size). A Point is defined using the Windows conventions for 100% scaling, which is 96 pixels to 72 points. That is, a point size of 10 is the same as a pixel size of 10\*(96/72) = 13.333.
Font Size Y `fontsizey` - Sets the font size in Y (vertical). **Note:** Floating point font sizes are permissable when using *Polygon* and *Outline* Display Methods.
Font Size Y Unit `fontsizeyunit` - Select the units for this parameter from Pixels, Fraction, Fraction Aspect or Points (font point size).
Keep Font Ratio `keepfontratio` - Ignores Y value in Font Size. Sets both X and Y size to Font Size X.
Break Language `breaklang` - Language type hint to help format the glyphs correctly.
Reading Direction `readingdirection` - ⊞ - Use to set whether the language reads Left to Right or Right to Left.

* Left To Right `lefttoright` -

* Right To Left `righttoleft` -

Tracking `tracking` - ⊞ - The amount of space to add between letters in X and Y. Tracking is way of adding an arbitrary offset between letters. There already is a default offset associated with each font so the letters are flush against each other. The Tracking parameter this adds to that and allows for a Y offset.

* `tracking1` -

* `tracking2` -

Position `position` - ⊞ - The starting position of the text in X and Y.

TIP: Inside the Text and Post Text fields the position can be overridden by using brackets.

* **[x,y]** - `"bleh[x,y]newtext"` will place *newtext* at position (x,y) on the screen.
* **{X,Y}** - `"bleh{(+/-)x,(+/-)y}newtext"` will offset *newtext* x,y from current position.
* **\n** - using `"\n"` causes the text to move down to the next line and reset its position. (i.e. New Line and Carriage Return)

* `position1` -

* `position2` -

Position Unit `positionunit` - Select the units for this parameter from Pixels, Fraction (0-1), Fraction Aspect (0-1 considering aspect ratio).
Line Spacing `linespacing` - Determines the amount of space between lines of text.
Line Spacing Unit `linespacingunit` - Select the units for this parameter from Pixels, Fraction (0-1), Fraction Aspect (0-1 considering aspect ratio).
Horizontal Align `alignx` - ⊞ - Sets the horizontal alignment.

* Left `left` - Left justifies the text.

* Center `center` - Centers the text.

* Right `right` - Right justifies the text.

Horizontal Align Mode `alignxmode` - ⊞ - Determines how horizontal alignment is calculated.

* Use Font Metrics `metrics` - Uses the font's built-in information to position the text.

* Use Text Bounding Box `bbox` - Uses a bounding box around the text to position the text.

Vertical Align `aligny` - ⊞ - Sets the vertical alignment.

* Bottom `bottom` - Bottom justifies the text.

* Center `center` - Centers the text.

* Top `top` - Top justifies the text.

Vertical Align Mode `alignymode` - ⊞ - Determines how vertical alignment is calculated.

* Use Font Metrics `metrics` - Uses the font's built-in information to position the text.

* Use Text Bounding Box `bbox` - Uses a bounding box around the text to position the text.

Border Space `borderspace` - ⊞ - When using Auto-Size Font, it will further shrink the text to give it a border.

* `borderspace1` -

* `borderspace2` -

  


## Parameters - Color Page

Multiply RGB by Alpha `multrgbbyalpha` - Multiplies the RGB channels by the alpha channel.
Font Color `fontcolor` - ⊞ - RGBA values for the text displayed. (default: white (1,1,1,1))

* Red `fontcolorr` -

* Green `fontcolorg` -

* Blue `fontcolorb` -

Font Alpha `fontalpha` - Set the alpha value for the font.
Background Color `bgcolor` - ⊞ - RGBA values for the background. (default: black (0,0,0,0))

* Red `bgcolorr` -

* Green `bgcolorg` -

* Blue `bgcolorb` -

Background Alpha `bgalpha` - Set the alpha value for the background.
Border A `bordera` - ⊞ - RGBA values for border A color.

* Red `borderar` -

* Green `borderag` -

* Blue `borderab` -

Border A Alpha `borderaalpha` - Set the alpha value for border A.
Border B `borderb` - ⊞ - RGBA values for border B color.

* Red `borderbr` -

* Green `borderbg` -

* Blue `borderbb` -

Border B Alpha `borderbalpha` - Set the alpha value for border B.
Left Border `leftborder` - What color the 2 left-most pixels are. Options are 0 (no change), Border A (uses color defined in Border A), or Border B (uses color defined in Border B).
Left Border Inside `leftborderi` - Same as above parameter but used for an inside border.
Right Border `rightborder` - What color the 2 right-most pixels are. Options are 0 (no change), Border A (uses color defined in Border A), or Border B (uses color defined in Border B).
Right Border Inside `rightborderi` - Same as above parameter but used for an inside border.
Bottom Border `bottomborder` - What color the 2 bottom-most pixels are. Options are 0 (no change), Border A (uses color defined in Border A), or Border B (uses color defined in Border B).
Bottom Border Inside `bottomborderi` - Same as above parameter but used for an inside border.
Top Border `topborder` - What color the 2 top-most pixels are. Options are 0 (no change), Border A (uses color defined in Border A), or Border B (uses color defined in Border B).
Top Border Inside `topborderi` - Same as above parameter but used for an inside border.

  


## Parameters - Output Page

Comp Over Input `compoverinput` - Turning this On will composite the input with the image.
Operation `operand` - ⊞ - Choose which composite operation is performed from this menu. Search the web for 'blend modes' for more detailed information on the effects of each type.

* Add `add` - input1.rgba + input2.rgba

* Atop `atop` - (input1.rgba \* input2.a) + (input2.rgba \* (1.0 - input1.a))

* Average `average` - (input1.rgba + input2.rgba)/2

* Brightest `brightest` -

* Burn Color `burncolor` -

* Burn Linear `burnlinear` -

* Chroma Difference `chromadifference` -

* Color `color` -

* Darker Color `darkercolor` -

* Difference `difference` - absoluteValue(input1.rgb - input2.rgb). Alpha always equals 1.0

* Dimmest `dimmest` -

* Divide `divide` - input1.rgba / input2.rgba

* Dodge `dodge` -

* Exclude `exclude` -

* Freeze `freeze` -

* Glow `glow` -

* Hard Light `hardlight` -

* Hard Mix `hardmix` -

* Heat `heat` -

* Hue `hue` -

* Inside `inside` - input1.rgba \* clamp(input2.a, 0.0, 1.0)

* Inside Luminance `insideluminance` -

* Inverse `inverse` -

* Lighter Color `lightercolor` -

* Luminance Difference `luminancedifference` -

* Maximum `maximum` - max(input1.r, input2.r), max(input1.g, input2.g), max(input1.b, input2.b), max(input1.a, input2.a)

* Minimum `minimum` - min(input1.r, input2.r), min(input1.g, input2.g), min(input1.b, input2.b), min(input1.a, input2.a)

* Multiply `multiply` -

* Negate `negate` -

* Outside `outside` - input1.rgba \* (1.0 - input2.a)

* Outside Luminance `outsideluminance` -

* Over `over` - (input2.rgba \* (1.0 - input1.a)) + input1.rgba

* Overlay `overlay` -

* Pinlight `pinlight` -

* Reflect `reflect` -

* Screen `screen` - 1.0 - ((1.0 - input1.rgba) \* (1.0 - input2.rgba))

* Soft Light `softlight` -

* Linear Light `linearlight` -

* Stencil Luminance `stencilluminance` -

* Subtract `subtract` - input1.rgba - input2.rgba

* Subtractive `subtractive` -

* Under `under` - (input1.rgba \* (1.0 - input2.a)) + input2.rgba

* Vivid Light `vividlight` -

* Xor `xor` - (input1.rgba \* (1.0 - input2.a)) + (input2.rgba \* (1.0 - input1.a))

* Y Film `yfilm` -

* Z Film `zfilm` -

Swap Order `swaporder` - Swaps the order of the composite with the input.

  


## Parameters - Common Page

Output Resolution `outputresolution` - ⊞ - quickly change the resolution of the TOP's data.

* Use Input `useinput` - Uses the input's resolution.

* Eighth `eighth` - Multiply the input's resolution by that amount.

* Quarter `quarter` - Multiply the input's resolution by that amount.

* Half `half` - Multiply the input's resolution by that amount.

* 2X `2x` - Multiply the input's resolution by that amount.

* 4X `4x` - Multiply the input's resolution by that amount.

* 8X `8x` - Multiply the input's resolution by that amount.

* Fit Resolution `fit` - Grow or shrink the input resolution to fit this resolution, while keeping the aspect ratio the same.

* Limit Resolution `limit` - Limit the input resolution to be not larger than this resolution, while keeping the aspect ratio the same.

* Custom Resolution `custom` - Directly control the width and height.

Resolution `resolution` - ⊞ - Enabled only when the Resolution parameter is set to Custom Resolution. Some Generators like Constant and Ramp do not use inputs and only use this field to determine their size. The drop down menu on the right provides some commonly used resolutions.

* W `resolutionw` -

* H `resolutionh` -

Resolution Menu `resmenu` - A drop-down menu with some commonly used resolutions.
Use Global Res Multiplier `resmult` - Uses the Global Resolution Multiplier found in **Edit>Preferences>TOPs**. This multiplies all the TOPs resolutions by the set amount. This is handy when working on computers with different hardware specifications. If a project is designed on a desktop workstation with lots of graphics memory, a user on a laptop with only 64MB VRAM can set the Global Resolution Multiplier to a value of half or quarter so it runs at an acceptable speed. By checking this checkbox on, this TOP is affected by the global multiplier.
Output Aspect `outputaspect` - ⊞ - Sets the image aspect ratio allowing any textures to be viewed in any size. Watch for unexpected results when compositing TOPs with different aspect ratios. (You can define images with non-square pixels using xres, yres, aspectx, aspecty where xres/yres != aspectx/aspecty.)

* Use Input `useinput` - Uses the input's aspect ratio.

* Resolution `resolution` - Uses the aspect of the image's defined resolution (ie 512x256 would be 2:1), whereby each pixel is square.

* Custom Aspect `custom` - Lets you explicitly define a custom aspect ratio in the Aspect parameter below.

Aspect `aspect` - ⊞ - Use when Output Aspect parameter is set to Custom Aspect.

* Aspect1 `aspect1` -

* Aspect2 `aspect2` -

Aspect Menu `armenu` - A drop-down menu with some commonly used aspect ratios.
Input Smoothness `inputfiltertype` - ⊞ - This controls pixel filtering on the input image of the TOP.

* Nearest Pixel `nearest` - Uses nearest pixel or accurate image representation. Images will look jaggy when viewing at any zoom level other than Native Resolution.

* Interpolate Pixels `linear` - Uses linear filtering between pixels. This is how you get TOP images in viewers to look good at various zoom levels, especially useful when using any Fill Viewer setting other than Native Resolution.

* Mipmap Pixels `mipmap` - Uses  [mipmap](Mipmapping.html "Mipmapping") filtering when scaling images. This can be used to reduce artifacts and sparkling in moving/scaling images that have lots of detail.

Fill Viewer `fillmode` - ⊞ - Determine how the TOP image is displayed in the viewer.

**NOTE:**To get an understanding of how TOPs work with images, you will want to set this to **Native Resolution** as you lay down TOPs when starting out. This will let you see what is actually happening without any automatic viewer resizing.

* Use Input `useinput` - Uses the same Fill Viewer settings as it's input.

* Fill `fill` - Stretches the image to fit the edges of the viewer.

* Fit Horizontal `width` - Stretches image to fit viewer horizontally.

* Fit Vertical `height` - Stretches image to fit viewer vertically.

* Fit Best `best` - Stretches or squashes image so no part of image is cropped.

* Fit Outside `outside` - Stretches or squashes image so image fills viewer while constraining it's proportions. This often leads to part of image getting cropped by viewer.

* Native Resolution `nativeres` - Displays the native resolution of the image in the viewer.

Viewer Smoothness `filtertype` - ⊞ - This controls pixel filtering in the viewers.

* Nearest Pixel `nearest` - Uses nearest pixel or accurate image representation. Images will look jaggy when viewing at any zoom level other than Native Resolution.

* Interpolate Pixels `linear` - Uses linear filtering between pixels. Use this to get TOP images in viewers to look good at various zoom levels, especially useful when using any Fill Viewer setting other than Native Resolution.

* Mipmap Pixels `mipmap` - Uses  [mipmap](Mipmapping.html "Mipmapping") filtering when scaling images. This can be used to reduce artifacts and sparkling in moving/scaling images that have lots of detail. When the input is 32-bit float format, only nearest filtering will be used (regardless of what is selected).

Passes `npasses` - Duplicates the operation of the TOP the specified number of times. For every pass after the first it takes the result of the previous pass and replaces the node's first input with the result of the previous pass. One exception to this is the [GLSL TOP](GLSL_TOP.html "GLSL TOP") when using compute shaders, where the input will continue to be the connected TOP's image.
Channel Mask `chanmask` - Allows you to choose which channels (R, G, B, or A) the TOP will operate on. All channels are selected by default.
Pixel Format `format` - ⊞ - Format used to store data for each channel in the image (ie. R, G, B, and A). Refer to [Pixel Formats](Pixel_Formats.html "Pixel Formats") for more information.

* Use Input `useinput` - Uses the input's pixel format.

* 8-bit fixed (RGBA) `rgba8fixed` - Uses 8-bit integer values for each channel.

* sRGB 8-bit fixed (RGBA) `srgba8fixed` - Uses 8-bit integer values for each channel and stores color in sRGB colorspace. Note that this does **not** apply an sRGB curve to the pixel values, it only stores them using an sRGB curve. This means more data is used for the darker values and less for the brighter values. When the values are read downstream they will be converted back to linear. For more information refer to [sRGB](https://docs.derivative.ca/SRGB "SRGB").

* 16-bit float (RGBA) `rgba16float` - Uses 16-bits per color channel, 64-bits per pixel.

* 32-bit float (RGBA) `rgba32float` - Uses 32-bits per color channel, 128-bits per pixels.

* 10-bit RGB, 2-bit Alpha, fixed (RGBA) `rgb10a2fixed` - Uses 10-bits per color channel and 2-bits for alpha, 32-bits total per pixel.

* 16-bit fixed (RGBA) `rgba16fixed` - Uses 16-bits per color channel, 64-bits total per pixel.

* 11-bit float (RGB), Positive Values Only `rgba11float` - A RGB floating point format that has 11 bits for the Red and Green channels, and 10-bits for the Blue Channel, 32-bits total per pixel (therefore the same memory usage as 8-bit RGBA). The Alpha channel in this format will always be 1. Values can go above one, but can't be negative. ie. the range is [0, infinite).

* 16-bit float (RGB) `rgb16float` -

* 32-bit float (RGB) `rgb32float` -

* 8-bit fixed (Mono) `mono8fixed` - Single channel, where RGB will all have the same value, and Alpha will be 1.0. 8-bits per pixel.

* 16-bit fixed (Mono) `mono16fixed` - Single channel, where RGB will all have the same value, and Alpha will be 1.0. 16-bits per pixel.

* 16-bit float (Mono) `mono16float` - Single channel, where RGB will all have the same value, and Alpha will be 1.0. 16-bits per pixel.

* 32-bit float (Mono) `mono32float` - Single channel, where RGB will all have the same value, and Alpha will be 1.0. 32-bits per pixel.

* 8-bit fixed (RG) `rg8fixed` - A 2 channel format, R and G have values, while B is 0 always and Alpha is 1.0. 8-bits per channel, 16-bits total per pixel.

* 16-bit fixed (RG) `rg16fixed` - A 2 channel format, R and G have values, while B is 0 always and Alpha is 1.0. 16-bits per channel, 32-bits total per pixel.

* 16-bit float (RG) `rg16float` - A 2 channel format, R and G have values, while B is 0 always and Alpha is 1.0. 16-bits per channel, 32-bits total per pixel.

* 32-bit float (RG) `rg32float` - A 2 channel format, R and G have values, while B is 0 always and Alpha is 1.0. 32-bits per channel, 64-bits total per pixel.

* 8-bit fixed (A) `a8fixed` - An Alpha only format that has 8-bits per channel, 8-bits per pixel.

* 16-bit fixed (A) `a16fixed` - An Alpha only format that has 16-bits per channel, 16-bits per pixel.

* 16-bit float (A) `a16float` - An Alpha only format that has 16-bits per channel, 16-bits per pixel.

* 32-bit float (A) `a32float` - An Alpha only format that has 32-bits per channel, 32-bits per pixel.

* 8-bit fixed (Mono+Alpha) `monoalpha8fixed` - A 2 channel format, one value for RGB and one value for Alpha. 8-bits per channel, 16-bits per pixel.

* 16-bit fixed (Mono+Alpha) `monoalpha16fixed` - A 2 channel format, one value for RGB and one value for Alpha. 16-bits per channel, 32-bits per pixel.

* 16-bit float (Mono+Alpha) `monoalpha16float` - A 2 channel format, one value for RGB and one value for Alpha. 16-bits per channel, 32-bits per pixel.

* 32-bit float (Mono+Alpha) `monoalpha32float` - A 2 channel format, one value for RGB and one value for Alpha. 32-bits per channel, 64-bits per pixel.

  


## Operator Inputs

* Input 0: Composite Input - Control the Composite operation via the parameters on the Output Page of this operator.

  


## Info CHOP Channels

Extra Information for the Text TOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Specific Text TOP Info Channels

* text\_width -

* text\_height -

* cursor\_start -

* cursor\_end -

* cursor\_x -

* cursor\_y -

* cursor\_width -

* cursor\_height -

### Common TOP Info Channels

* resx - Horizontal resolution of the TOP in pixels.

* resy - Vertical resolution of the TOP in pixels.

* aspectx - Horizontal aspect of the TOP.

* aspecty - Vertical aspect of the TOP.

* depth - Depth of 2D or 3D array if this TOP contains a 2D or 3D texture array.

* gpu\_memory\_used - Total amount of texture memory used by this TOP.

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

| TOPs |
| --- |
| [Add](Add_TOP.html "Add TOP") • [Analyze](Analyze_TOP.html "Analyze TOP") • [Anti Alias](Anti_Alias_TOP.html "Anti Alias TOP") • [Blob Track](Blob_Track_TOP.html "Blob Track TOP") • [Bloom](Bloom_TOP.html "Bloom TOP") • [Blur](Blur_TOP.html "Blur TOP") • [Cache Select](Cache_Select_TOP.html "Cache Select TOP") • [Cache](Cache_TOP.html "Cache TOP") • [Channel Mix](Channel_Mix_TOP.html "Channel Mix TOP") • [CHOP to](CHOP_to_TOP.html "CHOP to TOP") • [Chroma Key](Chroma_Key_TOP.html "Chroma Key TOP") • [Circle](Circle_TOP.html "Circle TOP") • [Composite](Composite_TOP.html "Composite TOP") • [Constant](Constant_TOP.html "Constant TOP") • [Convolve](Convolve_TOP.html "Convolve TOP") • [Corner Pin](Corner_Pin_TOP.html "Corner Pin TOP") • [CPlusPlus](CPlusPlus_TOP.html "CPlusPlus TOP") • [Crop](Crop_TOP.html "Crop TOP") • [Cross](Cross_TOP.html "Cross TOP") • [Cube Map](Cube_Map_TOP.html "Cube Map TOP") • [Depth](Depth_TOP.html "Depth TOP") • [Difference](Difference_TOP.html "Difference TOP") • [Direct Display Out](Direct_Display_Out_TOP.html "Direct Display Out TOP") • [DirectX In](DirectX_In_TOP.html "DirectX In TOP") • [DirectX Out](DirectX_Out_TOP.html "DirectX Out TOP") • [Displace](Displace_TOP.html "Displace TOP") • [Edge](Edge_TOP.html "Edge TOP") • [Emboss](Emboss_TOP.html "Emboss TOP") • [Feedback](Feedback_TOP.html "Feedback TOP") • [Fit](Fit_TOP.html "Fit TOP") • [Flip](Flip_TOP.html "Flip TOP") • [Function](Function_TOP.html "Function TOP") • [GLSL Multi](GLSL_Multi_TOP.html "GLSL Multi TOP") • [GLSL](GLSL_TOP.html "GLSL TOP") • [HSV Adjust](HSV_Adjust_TOP.html "HSV Adjust TOP") • [HSV to RGB](HSV_to_RGB_TOP.html "HSV to RGB TOP") • [Import Select](Import_Select_TOP.html "Import Select TOP") • [In](In_TOP.html "In TOP") • [Inside](Inside_TOP.html "Inside TOP") • [Introduction To s Vid](Introduction_To_TOPs_Vid.html "Introduction To TOPs Vid") • [Kinect Azure Select](Kinect_Azure_Select_TOP.html "Kinect Azure Select TOP") • [Kinect Azure](Kinect_Azure_TOP.html "Kinect Azure TOP") • [Kinect](Kinect_TOP.html "Kinect TOP") • [Layout](Layout_TOP.html "Layout TOP") • [Leap Motion](Leap_Motion_TOP.html "Leap Motion TOP") • [Lens Distort](Lens_Distort_TOP.html "Lens Distort TOP") • [Level](Level_TOP.html "Level TOP") • [Limit](Limit_TOP.html "Limit TOP") • [Lookup](Lookup_TOP.html "Lookup TOP") • [Luma Blur](Luma_Blur_TOP.html "Luma Blur TOP") • [Luma Level](Luma_Level_TOP.html "Luma Level TOP") • [Math](Math_TOP.html "Math TOP") • [Matte](Matte_TOP.html "Matte TOP") • [Mirror](Mirror_TOP.html "Mirror TOP") • [Monochrome](Monochrome_TOP.html "Monochrome TOP") • [MoSys](MoSys_TOP.html "MoSys TOP") • [Movie File In](Movie_File_In_TOP.html "Movie File In TOP") • [Movie File Out](Movie_File_Out_TOP.html "Movie File Out TOP") • [MPCDI](MPCDI_TOP.html "MPCDI TOP") • [Multiply](Multiply_TOP.html "Multiply TOP") • [Ncam](Ncam_TOP.html "Ncam TOP") • [NDI In](NDI_In_TOP.html "NDI In TOP") • [NDI Out](NDI_Out_TOP.html "NDI Out TOP") • [Noise](Noise_TOP.html "Noise TOP") • [Normal Map](Normal_Map_TOP.html "Normal Map TOP") • [Notch](Notch_TOP.html "Notch TOP") • [Null](Null_TOP.html "Null TOP") • [Nvidia Background](Nvidia_Background_TOP.html "Nvidia Background TOP") • [Nvidia Denoise](Nvidia_Denoise_TOP.html "Nvidia Denoise TOP") • [Nvidia Flex](Nvidia_Flex_TOP.html "Nvidia Flex TOP") • [Nvidia Flow](Nvidia_Flow_TOP.html "Nvidia Flow TOP") • [Nvidia Upscaler](Nvidia_Upscaler_TOP.html "Nvidia Upscaler TOP") • [OAK Select](OAK_Select_TOP.html "OAK Select TOP") • [Oculus Rift](Oculus_Rift_TOP.html "Oculus Rift TOP") • [OP Viewer](OP_Viewer_TOP.html "OP Viewer TOP") • [OpenColorIO](OpenColorIO_TOP.html "OpenColorIO TOP") • [OpenVR](OpenVR_TOP.html "OpenVR TOP") • [Optical Flow](Optical_Flow_TOP.html "Optical Flow TOP") • [Orbbec Select](Orbbec_Select_TOP.html "Orbbec Select TOP") • [Orbbec](Orbbec_TOP.html "Orbbec TOP") • [Ouster Select](Ouster_Select_TOP.html "Ouster Select TOP") • [Ouster](Ouster_TOP.html "Ouster TOP") • [Out](Out_TOP.html "Out TOP") • [Outside](Outside_TOP.html "Outside TOP") • [Over](Over_TOP.html "Over TOP") • [Pack](Pack_TOP.html "Pack TOP") • [Photoshop In](Photoshop_In_TOP.html "Photoshop In TOP") • [Point File In](Point_File_In_TOP.html "Point File In TOP") • [Point File Select](Point_File_Select_TOP.html "Point File Select TOP") • [Point Transform](Point_Transform_TOP.html "Point Transform TOP") • [PreFilter Map](PreFilter_Map_TOP.html "PreFilter Map TOP") • [Projection](Projection_TOP.html "Projection TOP") • [Ramp](Ramp_TOP.html "Ramp TOP") • [RealSense](RealSense_TOP.html "RealSense TOP") • [Rectangle](Rectangle_TOP.html "Rectangle TOP") • [Remap](Remap_TOP.html "Remap TOP") • [Render Pass](Render_Pass_TOP.html "Render Pass TOP") • [Render Select](Render_Select_TOP.html "Render Select TOP") • [Render](Render_TOP.html "Render TOP") • [RenderStream In](RenderStream_In_TOP.html "RenderStream In TOP") • [RenderStream Out](RenderStream_Out_TOP.html "RenderStream Out TOP") • [Reorder](Reorder_TOP.html "Reorder TOP") • [Resolution](Resolution_TOP.html "Resolution TOP") • [RGB Key](RGB_Key_TOP.html "RGB Key TOP") • [RGB to HSV](RGB_to_HSV_TOP.html "RGB to HSV TOP") • [Scalable Display](Scalable_Display_TOP.html "Scalable Display TOP") • [Screen Grab](Screen_Grab_TOP.html "Screen Grab TOP") • [Screen](Screen_TOP.html "Screen TOP") • [Script](Script_TOP.html "Script TOP") • [Select](Select_TOP.html "Select TOP") • [Shared Mem In](Shared_Mem_In_TOP.html "Shared Mem In TOP") • [Shared Mem Out](Shared_Mem_Out_TOP.html "Shared Mem Out TOP") • [SICK](SICK_TOP.html "SICK TOP") • [Slope](Slope_TOP.html "Slope TOP") • [Spectrum](Spectrum_TOP.html "Spectrum TOP") • [SSAO](SSAO_TOP.html "SSAO TOP") • [Stype](Stype_TOP.html "Stype TOP") • [Substance Select](Substance_Select_TOP.html "Substance Select TOP") • [Substance](Substance_TOP.html "Substance TOP") • [Subtract](Subtract_TOP.html "Subtract TOP") • [SVG](SVG_TOP.html "SVG TOP") • [Switch](Switch_TOP.html "Switch TOP") • [Syphon Spout In](Syphon_Spout_In_TOP.html "Syphon Spout In TOP") • [Syphon Spout Out](Syphon_Spout_Out_TOP.html "Syphon Spout Out TOP") • Text• [Texture 3D](Texture_3D_TOP.html "Texture 3D TOP") • [Texture Sampling Parameters](Texture_Sampling_Parameters.html "Texture Sampling Parameters") • [Threshold](Threshold_TOP.html "Threshold TOP") • [Tile](Tile_TOP.html "Tile TOP") • [Time Machine](Time_Machine_TOP.html "Time Machine TOP") • [TOP](TOP.html "TOP") • [Experimental:TOP](Experimental_TOP.html "Experimental:TOP") • [TOP Viewer](TOP_Viewer.html "TOP Viewer") • [Touch In](Touch_In_TOP.html "Touch In TOP") • [Touch Out](Touch_Out_TOP.html "Touch Out TOP") • [Transform](Transform_TOP.html "Transform TOP") • [Under](Under_TOP.html "Under TOP") • [Video Device In](Video_Device_In_TOP.html "Video Device In TOP") • [Video Device Out](Video_Device_Out_TOP.html "Video Device Out TOP") • [Video Stream In](Video_Stream_In_TOP.html "Video Stream In TOP") • [Video Stream Out](Video_Stream_Out_TOP.html "Video Stream Out TOP") • [Vioso](Vioso_TOP.html "Vioso TOP") • [Web Render](Web_Render_TOP.html "Web Render TOP") • [Experimental:ZED Select](Experimental_ZED_Select_TOP.html "Experimental:ZED Select TOP") • [ZED](ZED_TOP.html "ZED TOP") • [Experimental:ZED](Experimental_ZED_TOP.html "Experimental:ZED TOP") |

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").


Unicode text is fully supported in TouchDesigner. Unicode can be typed into parameters, DATs, Python scripts etc. Unicode encoded text files can be loaded into DATs. File paths can include any unicode character that is legal for a file path.


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


A form of [DATs](DAT.html "DAT") (Data Operators) that is structured as rows and columns of text strings.


A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP") can set the image resolution. See [Aspect Ratio](TOP_Generator_Common_Page.html "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.


The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.


A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").







Retrieved from "<https://docs.derivative.ca/index.php?title=Text_TOP&oldid=27220>"
[Category](Special_Categories.html "Special:Categories"):

* [TOPs](Category_TOPs.html "Category:TOPs")