

# Text_COMP

Text COMP - TouchDesigner Documentation




# Text COMP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Text COMP is a [panel](Panel.html "Panel") used to display text for building user interfaces. The text can be view-only, view-only but copy/pasteable, or be fully editable directly in the panel.
There are **formatting** modes for displaying single-line strings and multi-line text, floating point and integer numbers, password fields and more. The source of the text comes from the Text parameter and it is then formatted for display in the panel. Formatting examples include displaying a number as a currency, percent or scientific notation, or converting an integer timecode value to hours/minutes/seconds/frames. Other formatting options include support for Python syntax, Custom C++ Fmt and Custom Python F-String syntax.
When a user clicks in the panel to edit the text, the contents are displayed in a raw format and then formatted again once the editing is completed.
The Text COMP supports **[inline formatting directives](https://docs.derivative.ca/Text_Formatting_Codes "Text Formatting Codes")** in the text for things like color, strikeouts, underlines, small caps, subscripts, gradients, etc. For example, the code `{#color(255, 0, 0);}` will turn all text that follows on that line red.
It has **text-fitting** options for wraparound, shrinking text if it doesn't fit, left-center-right alignment and language reading direction. View-only text can be selectable or not selectable.
You can draw **multiple transformed/formatted strings using a "Specification DAT" table**: It draws one string per row of the table, each with its own position and formatting in your panel. Columns can be `x`, `y`, `text`, `fontsize`, `fontcolorr`, `fontcolorg`, `fontcolorb`, `fontalpha`, `skew`, `tracking` and `horzstretch`. You can also use a Specification CHOP for the numeric values of the text attributes.
Every row of the Spec DAT represents a "block" or "text block". Every Spec DAT contains a column named `text` which is the string that overrides the Text parameter.
It has **python callbacks** that can be executed for every character or string that has changed, and a callback for change of focus.
**Resolution-independent text** is drawn directly to the screen at the resolution required for the panel size, resulting in perfectly crisp text at all zoom levels. It is GPU-based using the [Slug Library](Slug_Library.html "Slug Library").
Units for X, Y, Width and Height are in "**panel units**" whereas they were actual pixel units before. Default Font Size, Text Offsets and Padding are in panel units.
See [Operator Snippets](OP_Snippets.html "OP Snippets") for examples of the Text COMP.
See [Text Formatting Codes](https://docs.derivative.ca/Text_Formatting_Codes "Text Formatting Codes")
See also [Geo Text COMP](Geo_Text_COMP.html "Geo Text COMP") for the 3D rendered equivalent of the Text COMP.
Note: The Text COMP is a replacement for the [Field COMP](Field_COMP.html "Field COMP"), completely replacing it and adding many new features not previously available.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[textCOMP\_Class](TextCOMP_Class.html "TextCOMP Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Text Page](#Parameters_-_Text_Page)
* [3 Parameters - Font Page](#Parameters_-_Font_Page)
* [4 Parameters - Layout Page](#Parameters_-_Layout_Page)
* [5 Parameters - Panel Page](#Parameters_-_Panel_Page)
* [6 Parameters - Look Page](#Parameters_-_Look_Page)
* [7 Parameters - Children Page](#Parameters_-_Children_Page)
* [8 Parameters - Drag/Drop Page](#Parameters_-_Drag/Drop_Page)
* [9 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [10 Parameters - Common Page](#Parameters_-_Common_Page)
  

## Parameters - Text Page
Mode `mode` - ⊞ - Controls whether the contents are taken from the Text parameter or from a Specification DAT/CHOP.
* Text `text` -
* Specification DAT/CHOP `specdat` -
Text `text` - This parameter is the data source for the text that is displayed in the panel. The value may be a number, string, or a reference to an external data source using a python or bind expression. When the text is edited by the user in the panel, those changes will be saved back to this value or to the original data source it is bound to. For example, you can bind the text in the panel to the contents of a DAT cell using a bind expression like 'op('table1')[0,0]'
Specification DAT `specdat` - A path to a Table DAT that is the source of the text data when in Specification mode. The table should have 3 columns labeled x, y and text in their first rows. Each row after that will display one line of text at the given x, y coordinates as measured from the bottom-left corner. x and y are measured in panel units.
Specification CHOP `specchop` - A path to a CHOP that can provide numerical data when in Specification mode. Channels named x and y can be used to position the text data specified in the Specificaction DAT. Each data row in the DAT should have a corresponding sample in the CHOP.
Type `type` - ⊞ - The Type parameter controls how the value is interpreted and as well as what formatting and editing options are available.
* String `string` - The value is interpreted as a single line of text. If the source text contains multiple lines, they will be appended into one line. This mode is useful for simply labels or as an input field for data.
* Float `float` - The value is treated as a floating point number before it is formatted for display in the panel. When editing, only numeric digits are accepted.
* Integer `integer` - The value is treated as a whole integer number before it is formatted for display in the panel. When editing, only numeric digits are accepted. Integer mode can be used for formatting time codes and other whole numbers.
* Multi Line `multiline` - Use this mode when displaying longer text that spans multiple lines. Lines are broken by a new line character (\n), or they can be set to wrap at the bounds of the panel. Note: Use expression mode for the Text parameter when entering new line characters using the '\n' escape sequence. Escape sequences are ignored and treated as literals when the parameter is in constance mode.
* Password `password` - Use this mode to simulate a password box where the formatted text is replaced with dots. Note: While the password is not visible in the panel, it is not secure and is still displayed in the value parameter and is accessible with python.
* Specification DAT `specdat` - In this mode, the Text parameter is ignored and data is taken from a DAT table given in the Specification DAT parameter. This mode can be used for displaying multiple single line strings at arbitrary locations inside the panel. This mode does not support editing the text directly in the panel. The table must contain at least 3 columns labeled x, y and text in their first rows. Each subsequent row will display one line of text at the given x, y coordinates. x and y are given in panel units measured from the bottom-left. The alignment parameters can be used to position the text relative to each x, y point.
Formatting `formatting` - ⊞ - This parameter controls how the source text is is formatted and displayed inside the panel. The options available will change depending on the selected mode. For example, in Float mode there are options for scientific notation or percentage, while in Integer mode there are options to treat the source value as a time code.
* Default `default` - This option is available in all modes and applies minimal formatting to the source value.
* Custom (Fmt Syntax) `customfmt` - The text value is formatted using the c++ Fmt syntax where the source text is value 0. In Float mode, the width is also available as value 1 and the precision is value 2. See the [Fmt documentation](https://fmt.dev/latest/syntax.html) for more details.
* Custom (Python F-String Syntax e.g. {val} ) `customfstring` - The text value is formatted using the Python F-String syntax where the source text is available in the variable 'val'. In this format, anything between the curly braces is treated as a python expression, which allows easy mixing of literal text and dynamic expressions.
Custom Formatting `customformatting` - This parameter provides the formatting string for custom modes like Python F-String and C++ Fmt. In both cases, the source text is defined inside curly braces ( {} ) while text outside the braces is treated as constants.
Precision `precision` - Used in Float mode to set the number of decimal places.
Thousands Separator `thousandsseparator` - ⊞ - Used in Float and Integer mode to add a separator between thousands to make it easier to read large numbers. For example 1,000,000
* None `none` - Do not add a separator.
* Space `space` - Use a half space character to separate thousands i.e. 1 000 000
* Comma `comma` - Use a comma to separate thousands 1,000,000
Framerate `framerate` - Sets the number of frames per second when formatting integers into time codes.
Use Smart Punctuation `smartquote` - Enables the use of smart punctuation. For example, pairs of quotes will be replaced with appropriate angled quotes, 3 periods will be replaced with an ellipses character and two hypens will become an em-dash.
Formatting Codes `formatcodes` - Enables the use of formatting directives in the text. For example, the code {#color(255, 0, 0);} will turn all text afterwards on that line red. See [Text Formatting Codes](https://docs.derivative.ca/Text_Formatting_Codes "Text Formatting Codes") for all available codes.
Smart Punctuation `smartpunct` - Enables the use of smart punctuation. For example, pairs of quotes will be replaced with appropriate angled quotes, 3 periods will be replaced with an ellipses character and two hypens will become an em-dash.
Word Wrap `wordwrap` - Enables word wrap and can only be used when the 'Type' parameter above is set to 'Multi Line'. Word wrap will split single lines of text onto multiple lines when they extend past the edge of the panel. The panel width is based on the Width parameter minus the left and right padding. Lines are generally broken at spaces, tabs or hypens, but can be broken mid word if a single word is longer than the page.
Edit Mode `editmode` - ⊞ - Controls whether the text can be editing directly in the viewer.
* Locked `locked` - The text is read only and cannot be edited in the viewer.
* Editable `editable` - Clicking in an active viewer will begin edit mode, allowing the text to be edited directly in the viewer. When the viewer loses focus, by clicking outside or hitting enter or escape, the contents of the viewer will be saved back to Text parameter. If the Text parameter contains a bind expression, the text will be saved back to the member on the other side of the bind i.e. another parameter, DAT cell or python attribute.
* Select Only `selectonly` - The text in the viewer can be selected and copied, but cannot be changed.
* Editable (Continuous Update) `editablecontinuous` - Similar to the 'Editable' option, but the value is saved back to the source after every key stroke rather than just after the viewer loses focus.
Shift-Enter for New Line `shiftenter` - In multiline mode, when this option is enabled, pressing Enter will complete editing and save the value and users must hold Shift and Enter if they wish to create a new line.
Reading Direction `readingdirection` - ⊞ - Use this parameter to control whether the text is displayed from left-to-right (LTR) or from right-to-left (RTL). Bidirectional layout is also supported when LTR characters are detected when using RTL mode.
* Left To Right `lefttoright` -
* Right To Left `righttoleft` -
Drag Drop Behaviour `dragdropmode` - ⊞ - This parameter controls what happens when a user drags something onto an active panel.
* Use Panel System `panel` - Use the standard drag/drop controls.
* Replace Text `textreplace` - Automatically replace the text with text contents of the object being dragged. For example, if a node is dragged onto the viewer, the text will be replaced with the path for that node.
* Append Text `textappend` - Automatically append the text contents of the object being dragged onto the current contents of the view. For example, if a node is dragged onto the viewer, the path of that node will be added to the end of the current text.
Focus Order `fieldfocus` - A path to a Table DAT containing a list of component paths that is used to control which panel receives the focus when a user hits TAB or Shift+Tab during editing.
Drag Drop Behavior `dragdropmode` - ⊞ - This parameter controls what happens when a user drags something onto an active panel.
* Use Panel System `panel` -
* Insert Text `textinsert` -
* Replace Text `textreplace` -
* Append Text `textappend` -
Callbacks DAT `callbacks` - The path of a Text DAT containing python callback functions that can be used to react to different events in the viewer.
  

## Parameters - Font Page
Legacy Font Selection `legacyfontselection` - Enable to select the font using the legacy system of bold and italic toggles. In the new system, bold and italic options can be chosen using the typeface parameter when available.
Font `font` - Select the font to be used from the dropdown menu. Available fonts are those that have been registered with the operating system. There may be a delay when selecting fonts that have not been used before as the system creates the necessary intermediate files required for rendering.
Font File `fontfile` - Specify a font file to be used for rendering the text. This option can be used for fonts that are not registered with the operating system and do not appear in the drop down menu.
Typeface `typeface` - ⊞ - Select a specific typeface for the current font e.g. Bold, Regular, Italic, etc. Not applicable in legacy font mode.
* Regular `Regular` -
* Italic `Italic` -
* Bold `Bold` -
* Bold Italic `Bold Italic` -
Bold `bold` - Display the text in **bold**.
Italic `italic` - Display the text in *italics*.
Drop Shadow `dropshadow` - Draw a drop shadow under the text.
Scale Text to Fit `scaletofit` - ⊞ - Automatically adjust the font size to fit inside the panel.
* Never `never` - Use the given font size and do not scale the text.
* Always `always` - Scale the text so that it fills the vertical and horizontal dimensions of the panel while still maintaining its original proportions.
* Only when Too Large `onlyshrink` - In this mode, the text is only scaled if it is too large to fit inside the panel. Text that is smaller than the panel, will remain at its original font size.
Font Size `fontsize` - Set the size of the font. By default the font is defined in resolution-independent panel units that will be rendered to a variable number of pixels depending on DPI settings of the output window (e.g. monitor scaling).
Font Size Units `fontsizeunits` - ⊞ - Determines how the font size is interpretted. The default is resolution-independent panel units.
* P `panelunits` - A resolution-independent unit that is rendered to a variable number of pixels depending on the current DPI settings of the display device.
* F `fract` - A percentage of the panel height i.e. 0.5 is 50% or half of the panel height. 1.0 would be the full height of the panel.
* A `relfract` -
* Pt `points` - Set the font size using points which are defined using the Windows convention that at 100% display scaling (1 panel unit = 1 pixel), 96 pixels is 72 points or the equavalent of 1.333 panel units.
Tracking `tracking` - Sets the horizontal spacing between characters, where 0 is default spacing, > 0 is increased spacing and < 0 is decreased spacing.
Skew `skew` - Tilts the top of the characters forwards or backwards relative to the baseline.
Horz Stretch `horzstretch` - Horizontally stretch the characters relative to their current alignment.
Line Spacing `linespacing` - The spacing between lines when using multiline mode. The value is a multiplier of the default spacing which is defined as 1.2 \* font size.
Font Color `fontcolor` - ⊞ - The default color of the text. Additional colors can be applied to separate parts of the text using formatting codes.
* Font Color `fontcolorr` -
* Font Color `fontcolorg` -
* Font Color `fontcolorb` -
Font Alpha `fontalpha` - The blending value used to display the text over the background. 1 is opaque while 0 is transparent.
Custom Select Color `customselectcolor` - Enable this parameter to define a custom color used for the selection bar when editing the text. When disabled, the selection color will be automatically chosen to maximize contrast between the background and text colors.
Select Color `selectcolor` - ⊞ - The color of the selection bar when Custom Select Color is enabled.
* Select Color `selectcolorr` -
* Select Color `selectcolorg` -
* Select Color `selectcolorb` -
Text Offset `textoffset` - ⊞ - An offset applied to the text position after any other alignment operations. Positive values move the text up and to the right.
* Text Offset `textoffsetx` -
* Text Offset `textoffsety` -
Text Offset Units `textoffsetunits` - ⊞ - Determine the units used by the Text Offset parameter.
* P `panelunits` -
* F `fract` -
* A `relfract` -
* Pt `points` -
Text Padding `textpadding` - ⊞ - Set the amount of space between the edges of the panel and the text. Whether the padding has an effect on the position of the text depends on the current alignment mode and whether word wrapping is used. For example, if the text is left aligned, the text will be positioned away from the left edge based on the left padding. But the text may extend any distance from the right edge depending on the length of the text. However, if word wrap is enabled in multiline mode, then the text will be wrapped at a distance from the right edge based on the padding.
* Text Padding `textpaddingl` -
* Text Padding `textpaddingr` -
* Text Padding `textpaddingb` -
* Text Padding `textpaddingt` -
Text Padding Units `textpaddingunits` - ⊞ - The units used by the text padding.
* P `panelunits` -
* F `fract` -
* A `relfract` -
* Pt `points` -
Horizontal Align `alignx` - ⊞ - Determines how the text is positioned horizontally in the panel. For example, with left alignment, the text will be positioned against the left side of the panel plus any defined padding.
* Left `left` -
* Center `center` -
* Right `right` -
Horizontal Align Mode `alignxmode` - ⊞ - Determines how the text is measured for calculating the alignment. Only font metrics are available when using Multiline or Specification DAT mode.
* Use Font Metrics `metrics` - Uses the general dimensions of the font rather than the specific characters of the text. Use this setting to maintain a constant alignment when the text may be changing.
* Use Text Bounding Box `bbox` - Uses the exact dimensions of the current string to do the alignment. This is useful when trying to align special characters like forward slashes that may not align with the standard character box.
Vertical Align `aligny` - ⊞ - Determines how the text is positioned vertically inside the panel.
* Bottom `bottom` -
* Center `center` - When using Font Metrics alignment, centering is based on the distance from the baseline to the defined ascent (usually the height of the capital Latin characters) for the font. Descending characters like 'g' or 'j' are not accounted for.
* Top `top` -
* Baseline `baseline` -
Vertical Align Mode `alignymode` - ⊞ - Determines how the text is measured when doing the vertical alignment.
* Use Font Metrics `metrics` - The vertical alignment is based on the general size of the font i.e. the font may be positioned a small distance from the bottom of the panel to account for any descending characters like 'g' or 'j' even if those characters are not present in the text. Use this setting to maintain a constant alignment when the text may be changing or is unknown.
* Use Text Bounding Box `bbox` - The vertical alignment is based on the specific characters of the text e.g. text with no descending characters may be positioned directly against the bottom edge when using bottom alignment.
  

## Parameters - Layout Page
The Layout parameter page controls the size and position of the panel.
X `x` - Specify the horizontal position in pixels relative to its parent.
Y `y` - Specify the vertical position in pixels relative to its parent.
Width `w` - Specify the panel's width in pixels.
Height `h` - Specify the Panel's height in pixels.
Fixed Aspect `fixedaspect` - ⊞ - Allows easy creation of panels with a specific aspect set in the Aspect Ratio parameter below. Only requires setting the width or height of the panel and the other dimension is calculated based on the Aspect Ratio parameter.
* Off `off` -
* Use Horizontal `horizontal` -
* Use Vertical `vertical` -
Aspect Ratio `aspect` - Specify the ratio when using Fixed Aspect parameter above, the ratio is width/height.
Depth Layer `layer` - Specifies the order the panel components are drawn in, similar to layers in Photoshop. Higher values will be drawn over any other panel with a lower value (that is at the same level of hierarchy). If two panel components have the same Depth Layer value then they are ordered based on the operator's name.
Horizontal Mode `hmode` - ⊞ - Select one of 3 modes to determine the horizontal width of the panel.
* Fixed Width `fixed` - Uses the Width parameter above to set this panel's width in pixels.
* Fill `fill` - The width of this panel will match (fill) the width of the parent panel.
* Anchors `anchors` - The width of this panel is set by the Left Anchor and Right Anchor parameters below which will maintain a relative width to the parent panel as the parent panel changes size. This allows for stretchy panels. These anchor parameters are normalized 0-1 like uv coordinates where 0 is the left edge and 1 is the right edge of the parent panel. For example, Left Anchor = 0.2 and Right Anchor = 0.8 will maintain the width proportionally to the parent panel such that the left edge is 20% (0.2) in from the left and the right edge is 20% (0.8) in from the right.
Left Anchor `leftanchor` - Position of the left anchor of the panel with respect to the parent. This value is normalized 0-1, 0 is the left edge of the parent and 1 is the right edge of the parent.
Left Offset `leftoffset` - An offset for the left anchor in pixels.
Right Anchor `rightanchor` - Position of the right anchor of the panel with respect to the parent. This value is normalized 0-1, 0 is the left edge of the parent and 1 is the right edge of the parent.
Right Offset `rightoffset` - An offset for the right anchor in pixels.
Horizontal Origin `horigin` - Sets the position of the panel's origin horizontally. The default origin (0,0) is the bottom-left corner of the panel.
Horizontal Fill Weight `hfillweight` - When multiple panels are using Horizontal Mode = Fill and being aligned by the parent either Left to Right or Right to Left, this fill weight parameter can be used to bias the fill width of the panels.
Vertical Mode `vmode` - ⊞ - Select one of 3 modes to determine the vertical height of the panel.
* Fixed Height `fixed` - Uses the Height parameter above to set this panel's height in pixels.
* Fill `fill` - The height of this panel will match (fill) the height of the parent panel.
* Anchors `anchors` - The height of this panel is set by the Bottom Anchor and Top Anchor parameters below which will maintain a relative and proportionally height to the parent panel as the parent panel changes size. This allows for stretchy panels. These anchor parameters are normalized 0-1 like uv coordinates where 0 is the bottom edge and 1 is the top edge of the parent panel. For example, Bottom Anchor = 0.3 and Right Anchor = 0.5 will maintain the height proportionally to the parent panel such that the bottom edge is 30% (0.3) up from the bottom and the top edge is 50% (0.5) down from the top.
Bottom Anchor `bottomanchor` - Position of the bottom anchor of the panel with respect to the parent. This value is normalized 0-1, 0 is the bottom edge of the parent and 1 is the top edge of the parent.
Bottom Offset `bottomoffset` - An offset for the bottom anchor in pixels.
Top Anchor `topanchor` - Position of the top anchor of the panel with respect to the parent. This value is normalized 0-1, 0 is the bottom edge of the parent and 1 is the top edge of the parent.
Top Offset `topoffset` - An offset for the top anchor in pixels.
Vertical Origin `vorigin` - Sets the position of the panel's origin vertically. The default origin (0,0) is the bottom-left corner of the panel.
Vertical Fill Weight `vfillweight` - When multiple panels are using Vertical Mode = Fill and being aligned by the parent either Top to Bottom or Bottom to Top, this fill weight parameter can be used to bias the fill height of the panels.
Parent Alignment `alignallow` - ⊞ - When set to Ignore, the Panel will ignore any Align parameter settings from its parent.
* Allow `allow` - Aligns the panel based on settings in parent.
* Ignore `ignore` - Does not align the panel but respects margins.
* Ignore and Ignore Margins `ignoremargin` - Does not align the panel and disregards margins.
Align Order `alignorder` - This parameter allows you to specify the align position when its parent's Align parameter is set to something other then **None** or **Match Network Nodes**. Lower numbers are first.
Post Offset `postoffset` - ⊞ - Adds an offset after all other postions and alignment options have been applied to the panel.
* X `postoffsetx` -
* Y `postoffsety` -
Size from Window `sizefromwindow` - When enabled the panel component's width and height are set by resizing its floating viewer window.
  

## Parameters - Panel Page
The Panel parameter page controls panel attributes such as display on/off, enable on/off, panel help, and interactions with the cursor.
Display `display` - Specifies if the panel is displayed or hidden. Changing this parameter may incur some layout processing costs. For simple cases, such as overlays it is more performant to adjust the opacity parameter instead.
Enable `enable` - Allows you to prevent all interaction with this panel.
Help DAT `helpdat` - Lets you specify the path to a [Text DAT](Text_DAT.html "Text DAT") whose content will be displayed as a rollover pop-up help for the control panel.
Cursor `cursor` - ⊞ - Changes the cursor displayed when cursor is over the panel.
* Normal Select `pointer` -
* Link Select `linkselect` -
* Text Select `ibeam` -
* Precision Select `cross` -
* Busy `busy` -
* Activate `activate` -
* Invisible `invisible` -
Multi-Touch `multitouch` - ⊞ - When enabled, this panel will process the first touch it gets in a similar manner to how it processes a mouse click, with updates to u, v, state etc. The touch event must be initiated from the panel. Subsequent touches are ignored. If this panel handles multi-touch events via the [Multi Touch In DAT](Multi_Touch_In_DAT.html "Multi Touch In DAT"), you may want to disable Built-in Multi-Touch so it won't interfere with script processing.
* Use Parent's Multi-Touch Settings `mtouchparent` - Use the parent's Multi-Touch setting. This defaults to enabled in the root component.
* Use Built-in Multi-Touch `mtouchyes` - Enable use of first touch as mouse.
* Do Not Use Built-in Multi-Touch `mtouchno` - Disable use of first touch as mouse.
Constrain Cursor `constraincursor` - Constrains the cursor to this panel, keeping it inside once it enters.
Click Through `clickthrough` - When enabled all mouse clicks are ignored by this [Panel Component](Panel_Component.html "Panel Component").
Use Mouse Wheel `mousewheel` - Turn on to capture events when the mouse wheel is used over the panel.
Mouse UV Buttons `uvbuttons` - ⊞ - Allows you to specify which mouse buttons update the uv [Panel Values](Panel_Value.html "Panel Value").
* Left `uvbuttonsleft` -
* Middle `uvbuttonsmiddle` -
* Right `uvbuttonsright` -
Relative UV `mouserel` - When enabled the uv [Panel Values](Panel_Value.html "Panel Value") will reflect relative mouse movement.
Drag Edges to Resize `resize` - ⊞ - Four checkboxes allow you to enable resizing a panel by grabbing the corresponding edge or corner: Resize Left, Right, Bottom, Top.
* L `resizel` -
* R `resizer` -
* B `resizeb` -
* T `resizet` -
W Range `resizew` - ⊞ - Limits the left-right (width) resizing range.
* `resizewmin` -
* `resizewmax` -
H Range `resizeh` - ⊞ - Limits the bottom-top (height) resizing range.
* `resizehmin` -
* `resizehmax` -
Drag to Reposition `reposition` - ⊞ - Enables repositioning of the panel or window by dragging with the mouse.
* Off `off` -
* Window `window` -
* Component `component` -
Component `repocomp` - Enabled by choosing the **Component** option from the Reposition parameter. Specify the path to the panel component you would like to reposition by mouse.
X Range `repositionx` - ⊞ - Enabled by choosing the **Component** option from the Reposition parameter. Sets the maximum range for repositioning the panel component horizontally.
* `repositionxmin` -
* `repositionxmax` -
Y Range `repositiony` - ⊞ - Enabled by choosing the **Component** option from the Reposition parameter. Sets the maximum range for repositioning the panel component vertically.
* `repositionymin` -
* `repositionymax` -
Anchor Drag `anchordrag` - ⊞ - When Drag To Reposition parameter is set to Component, and the panel's Horizontal Mode and/or Vertical Mode is set to Anchors, this menu determines whether drag-to-reposition actions change Anchor values or Offset values.
* Anchors `anchors` - Drag-to-reposition actions change Anchor parameter values
* Offsets `offsets` - Drag-to-reposition actions change Offset parameter values
Scroll Overlay `scrolloverlay` - ⊞ - Controls whether the panel is affected by scrollbar position. This allows the creation of panel overlays that aren't affected by the panel's scrollbars.
* Off `off` - Scrollbar affects panel normally.
* Ignore `ignore` - Panel will not move when scrollbar is moved. Panel depth is determined by Depth Layer parameter normally.
* Ignore and Draw Over `ignoreover` - Panel will not move when scrollbar is moved. Panel is drawn over scrollbars and sibling panels.
  

## Parameters - Look Page
The Color parameter page sets the panel's background, border, and disabled colors.
Background Color `bgcolor` - ⊞ - RGB values for the background. (default: black (0,0,0))
* Red `bgcolorr` -
* Green `bgcolorg` -
* Blue `bgcolorb` -
Background Alpha `bgalpha` - Set the alpha value for the background.
Background TOP `top` - Allows you to specify a [TOP](TOP.html "TOP") as the background for the panel.
TOP Fill `topfill` - ⊞ - This menu specifies the way the Background TOP will fill the panel's background.
* Stretch `off` -
* Fill Width `horizontal` -
* Fill Height `vertical` -
* Fill Best `best` -
* Native Resolution `native` -
TOP Smoothness `topsmoothness` - ⊞ - This menu controls background TOP's viewer smoothness settings. In previous builds of TouchDesigner, this was always 'Mipmap Pixels', so old files will load with this setting whereas the default for new Panel COMP's is 'Interpolate Pixels'.
* Nearest Pixel `nearest` - Uses nearest pixel or accurate image representation. Images will look jaggy when viewing at any zoom level other than Native Resolution.
* Interpolate Pixels `linear` - Uses linear filtering between pixels. Use this to get TOP images in viewers to look good at various zoom levels, especially useful when using any Fill Viewer setting other than Native Resolution.
* Mipmap Pixels `mipmap` - Uses mipmap filtering when scaling images. This can be used to reduce artifacts and sparkling in moving/scaling images that have lots of detail. When the input is 32-bit float format, only nearest filtering will be used (regardless of what is selected).
Border A `bordera` - ⊞ - RGB values for border A color.
* Red `borderar` -
* Green `borderag` -
* Blue `borderab` -
Border A Alpha `borderaalpha` - Alpha value for border A color.
Border B `borderb` - ⊞ - RGBA values for border B color.
* Red `borderbr` -
* Green `borderbg` -
* Blue `borderbb` -
Border B Alpha `borderbalpha` - Alpha value for border B color.
Left Border `leftborder` - What color the 2 left-most pixels are. Options are 0 (no change), Border A (uses color defined in Border A), or Border B (uses color defined in Border B).
Left Border Inside `leftborderi` - Same as above parameter but used for an inside border.
Right Border `rightborder` - What color the 2 right-most pixels are. Options are 0 (no change), Border A (uses color defined in Border A), or Border B (uses color defined in Border B).
Right Border Inside `rightborderi` - Same as above parameter but used for an inside border.
Bottom Border `bottomborder` - What color the 2 bottom-most pixels are. Options are 0 (no change), Border A (uses color defined in Border A), or Border B (uses color defined in Border B).
Bottom Border Inside `bottomborderi` - Same as above parameter but used for an inside border.
Top Border `topborder` - What color the 2 top-most pixels are. Options are 0 (no change), Border A (uses color defined in Border A), or Border B (uses color defined in Border B).
Top Border Inside `topborderi` - Same as above parameter but used for an inside border.
Border Over Children `borderover` - Draws the panel's borders on top of all children panels.
Disable Color `dodisablecolor` - Enable the use of a unique disable color below when the panel's Enable = Off.
Disable Color `disablecolor` - ⊞ - RGB values for the disable color. (default: black (0,0,0))
* Red `disablecolorr` -
* Green `disablecolorg` -
* Blue `disablecolorb` -
Disable Alpha `disablealpha` - Set the alpha value for the disable color.
Multiply RGB by Alpha `multrgb` - Multiplies the RGB channels by the alpha channel.
Composite `composite` - ⊞ - Selects how the panel is composited with its siblings panels. See the [Composite TOP](Composite_TOP.html "Composite TOP") for a description of the various composite methods.
* Over `over` -
* Under `under` -
* Inside `inside` -
* Outside `outside` -
* Add `add` -
* Subtract `subtract` -
* Multiply `multiply` -
Opacity `opacity` - Allows you to control the transparency of the panel.
  

## Parameters - Children Page
The Children parameter page controls aspects of the Panel's children alignment, size, and position.
Align `align` - ⊞ - This menu allows you to specify how the children inside the Panel Component will be laid out. The options **Layout Grid Rows**, **Layout Grid Columns** and **Match Network Nodes** will scale the Panel Component's children to fit the Component. They use the Align Order of each of the children to determine the ordering of the children.
* None `none` -
* Left to Right `horizlr` -
* Right to Left `horizrl` -
* Top to Bottom `verttb` -
* Bottom to Top `vertbt` -
* Grid Rows `gridrows` -
* Grid Columns `gridcols` -
* Match Network Nodes `nodes` -
Spacing `spacing` - This is enabled by choosing any Align option other than **None** or **Match Network Nodes**. It defines the space between the children when they are being aligned.
Max per Line `alignmax` - This is enabled by choosing any Align option other than **None**, **Layout Grid Horizontal**, **Layout Grid Vertical**, or **Match Network Nodes**, and defines the maximum number of children placed in one row or column.
Margin `margin` - ⊞ - The four fields allow you to specify the space that surrounds the Panel Component. The margin is the space between the Panel Component's border and the outer edge.
The Margin is defined in absolute pixels and does not stretch with the window, as a result margin is not reflected in the node's panel viewer but only when the parent is drawn in a floating window.
* L `marginl` -
* R `marginr` -
* B `marginb` -
* T `margint` -
Justify Mathod `justifymethod` - ⊞ - This menu specifies if the panel's children are being justified as a group or individually using the Jusitfy Horizontal / Vertical parameters below.
* individual `individual` - Align all children individually, separately from each other.
* Group `group` - Align all children as a group. First group all children into a bounding box, then align that box.
Justify Horizontal `justifyh` - ⊞ - This menu specifies if the panel's children are being justified horizontally.
* Off `off` -
* Left `left` -
* Center `center` -
* Right `right` -
Justify Vertical `justifyv` - ⊞ - This menu specifies if the panel's children are being justified vertically.
* Off `off` -
* Top `top` -
* Center `center` -
* Bottom `bottom` -
Fit `fit` - ⊞ - This menu allows you to scale the panel's children. It overrides the Justify Horizontal and Justify Vertical parameters.
* Off `off` -
* Fit Width `horizontal` -
* Fit Height `vertical` -
* Fit Best `best` -
Scale `scale` - ⊞ - Allows you to uniformly scale the Panel's children.
* X `scalex` -
* Y `scaley` -
Offset `offset` - ⊞ - Allows you to offset the Panel's children. This parameter is overwritten by the Align, Justify Horizontal, and Justify Vertical parameters above.
* X `offsetx` -
* Y `offsety` -
Crop `crop` - ⊞ - This menu determines if any children panels which are positioned partially or completely outside the panel component's dimensions get cropped.
* Off (Use Parent) `off` -
* On `on` -
* Never `never` -
Horizontal Scrollbar `phscrollbar` - ⊞ - Setting for horizontal scrollbar on this panel.
* Off `off` - No scrollbar.
* On `on` - Always include scrollbar.
* Automatic `auto` - Include scrollbar only when child width is greater than this panel's width.
Vertical Scrollbar `pvscrollbar` - ⊞ - Setting for vertical scrollbar on this panel.
* Off `off` - No scrollbar.
* On `on` - Always include scrollbar.
* Automatic `auto` - Include scrollbar only when child height is greater than this panel's height.
Thickness `scrollbarthickness` - Set the thickness of the scrollbars in pixels.
  

## Parameters - Drag/Drop Page
Please refer to [Drag-and-Drop](Drag-and-Drop.html "Drag-and-Drop") for a full explanation on how Drag and Drop between Panel Components functions.
When Dragging This `drag` - ⊞ - Specify if this Panel Component can be dragged.
* Use Parent's Drag Settings `dragparent` - Follow the parent Panel Components Drag setting.
* Legacy Drag System `legacy` - Allow Dragging for this Panel Component. Use the Paramters `Drag Script`, `Drop Destination Script` and `Dropped Operator` to control the behaviour.
* Do Not Allow Drag `dragno` - Disallows Dragging for this Panel Component.
Drag Script `dragscript` - Specify a script that will be executed when starting to drag a Panel Component. Please refer to the Drag Script section of the [Drag and Drop](Drag-and-Drop.html#Drag_Scripts "Drag-and-Drop") page.
Drop Destination Script `dropdestscript` - Specify a script that will be executed when the dragged Panel Component is dropped. A temporary network is created and the component (or the alternative operator specified in Dropped Component) is copied to this network. You can add or modify operators in this network. Please refer to the Drop Destination Script section of the [Drag and Drop](Drag-and-Drop.html#Drop_Destination_Scripts "Drag-and-Drop") page.
Drop Types `droptypescript` - If a drop destination script is specified, you can also add a DAT table with a list of return types that the drop destination script will provide. Return types can be one of the op types (COMP,TOP,CHOP,SOP,MAT,DAT), channel, or supported filetypes. Please refer to the Drop Types section of the [Drag and Drop](Drag-and-Drop.html#Drop_Types "Drag-and-Drop") page.
Dropped Operator `paneldragop` - The Dropped Component parameter is the easiest way to specify an alternative operator to drop. Note that this alternative operator must exist, otherwise the component itself will be dropped. The alternative is only used when dropping onto a network or control panel. Text pasted via dragging and dropping, or files saved via dropping onto the desktop, will still use the original.
On Dropping Into `drop` - ⊞ - Specify if this Panel Component accepts items that are dropped onto it.
* Use Parent's Drop Settings `dropparent` - Follow the parent Panel Components Drop setting.
* Legacy Drop System `legacy` - Allow Dropping onto this Panel Component. Use the Paramter `Drop Script` to control the behaviour.
* Do Not Allow Drop `dropno` - Disallows Dropping onto this Panel Component.
Drop Script `dropscript` - A component's Drop Script is run when you drop another component or an external file into that component. Please refer to the Drop Scripts - Text section of the [Drag and Drop](Drag-and-Drop.html#Drop_Scripts_-_Text "Drag-and-Drop") page.
Alternatively specify a Table DAT in the drop script field. TouchDesigner will automatically look for 2 columns in the table. The first column should indicate the data type and the second should indicate the Text DAT that holds the script to process that data type. Please refer to the Drop Script - Tables section of the [Drag and Drop](Drag-and-Drop.html#Drop_Script_-_Tables "Drag-and-Drop") page.

  

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
Keep in Memory `keepmemory` -
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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2023.112802022.24140before 2022.24140
| COMPs |
| --- |
| [Actor](Actor_COMP.html "Actor COMP") • [Ambient Light](Ambient_Light_COMP.html "Ambient Light COMP") • [Animation](Animation_COMP.html "Animation COMP") • [Annotate](Annotate_COMP.html "Annotate COMP") • [Base](Base_COMP.html "Base COMP") • [Blend](Blend_COMP.html "Blend COMP") • [Bone](Bone_COMP.html "Bone COMP") • [Bullet Solver](Bullet_Solver_COMP.html "Bullet Solver COMP") • [Button](Button_COMP.html "Button COMP") • [Camera Blend](Camera_Blend_COMP.html "Camera Blend COMP") • [Camera](Camera_COMP.html "Camera COMP") • [MediaWiki:Common.js](MediaWiki_Common.html "MediaWiki:Common.js") • [Component](Component.html "Component") • [Experimental:Component](Experimental_Component.html "Experimental:Component") • [Constraint](Constraint_COMP.html "Constraint COMP") • [Container](Container_COMP.html "Container COMP") • [Engine](Engine_COMP.html "Engine COMP") • [Environment Light](Environment_Light_COMP.html "Environment Light COMP") • [FBX](FBX_COMP.html "FBX COMP") • [Field](Field_COMP.html "Field COMP") • [Force](Force_COMP.html "Force COMP") • [Geo Text](Geo_Text_COMP.html "Geo Text COMP") • [Geometry](Geometry_COMP.html "Geometry COMP") • [GLSL](GLSL_COMP.html "GLSL COMP") • [Handle](Handle_COMP.html "Handle COMP") • [Impulse Force](Impulse_Force_COMP.html "Impulse Force COMP") • [Light](Light_COMP.html "Light COMP") • [List](List_COMP.html "List COMP") • [Null](Null_COMP.html "Null COMP") • [Nvidia Flex Solver](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](Nvidia_Flow_Emitter_COMP.html "Nvidia Flow Emitter COMP") • [OP Viewer](OP_Viewer_COMP.html "OP Viewer COMP") • [Palette:depthProjection](Palette_depthProjection.html "Palette:depthProjection") • [Parameter](Parameter_COMP.html "Parameter COMP") • [Replicator](Replicator_COMP.html "Replicator COMP") • [Select](Select_COMP.html "Select COMP") • [Shared Mem In](Shared_Mem_In_COMP.html "Shared Mem In COMP") • [Shared Mem Out](Shared_Mem_Out_COMP.html "Shared Mem Out COMP") • [Slider](Slider_COMP.html "Slider COMP") • [Table](Table_COMP.html "Table COMP") • Text• [Time](Time_COMP.html "Time COMP") • [USD](USD_COMP.html "USD COMP") • [Widget](Widget_COMP.html "Widget COMP") • [Window](Window_COMP.html "Window COMP") |
An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP") can set the image resolution. See [Aspect Ratio](TOP_Generator_Common_Page.html "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

A form of [DATs](DAT.html "DAT") (Data Operators) that is structured as rows and columns of text strings.

(1) The TouchDesigner window is made of a menu bar at the top, a [Timeline](Timeline.html "Timeline") at the bottom, plus one of a choice of Layouts in the middle. A Layout is made on one or more Panes, each Pane can contain a Network Editor, Viewer, Panel, etc. See [Pane](Pane.html "Pane") and [Bookmark](Bookmark.html "Bookmark"). (2) Nodes in a network are arranged using Layout commands in the RMB menu.

A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").

A Window in TouchDesigner is a window in Microsoft Windows or macOS that contains either (1) the TouchDesigner editing interface that exists in [Designer Mode](Designer_Mode.html "Designer Mode"), or (2) a user-created [Panel](Panel.html "Panel") inside a [Window Component](Window_COMP.html "Window COMP"). The user-created windows can span [Multiple Monitors](Multiple_Monitors.html "Multiple Monitors") borderless, or be floating windows with borders, or popups.

A [Link](Link.html "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](Operator_Family.html "Operator Family").
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](Export.html "Export"), node [Paths](Network_Path.html "Network Path") in parameters, and [expressions](Expression.html "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](Wire.html "Wire") that connects nodes in the same [Operator Family](Operator_Family.html "Operator Family").

Display devices in TouchDesigner that support multiple-finger or control-point input.

There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

The sub-[Family](Operator_Family.html "Operator Family") of [Components](Component.html "Component") that are used to create custom interactive 2D control [panels](Panel.html "Panel") (Container, Widget, Text COMP Slider, Button, etc.).

A set of commands located in a Text DAT that are triggered to run under certain conditions. There are two scripting languages in TouchDesigner: [Python](Python.html "Python") and the original [Tscript](Tscript.html "Tscript"). Scripts and single-line commands can also be run in the [Textport](Textport.html "Textport").

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

MATs or Materials are an [Operator Family](Operator_Family.html "Operator Family") that applies a [Shader](Shader.html "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.

Any component can be extended with its own Python classes which contain python functions and data.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.

A name for a component that is accessible from any node in a project, which can be declared in a component's Global Operator Shortcut parameter.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.

The viewer of a node can be (1) the interior of a node (the [Node Viewer](Node_Viewer.html "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](Pane.html "Pane") that graphically shows the results of an operator.

A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").

Cloning makes multiple components match the contents of a master component. A [Component](Component.html "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the [Replicator COMP](Replicator_COMP.html "Replicator COMP").

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

Retrieved from "<https://docs.derivative.ca/index.php?title=Text_COMP&oldid=32546>"
[Category](Special_Categories.html "Special:Categories"):
* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")