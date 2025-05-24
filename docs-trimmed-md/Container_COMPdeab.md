

TouchDesigner Documentation





# Container COMP
From Derivative
Revision as of 17:54, 8 March 2018 by [Markus Heckmann](https://docs.derivative.ca/User:Markus_Heckmann "User:Markus Heckmann") ([talk](https://docs.derivative.ca/index.php?title=User_talk:Markus_Heckmann&action=edit&redlink=1 "User talk:Markus Heckmann (page does not exist)") | [contribs](https://docs.derivative.ca/Special:Contributions/Markus_Heckmann "Special:Contributions/Markus Heckmann"))([diff](https://docs.derivative.ca/index.php?title=Container_COMP&diff=prev&oldid=10206 "Container COMP")) [← Older revision](https://docs.derivative.ca/index.php?title=Container_COMP&direction=prev&oldid=10206 "Container COMP") | [Latest revision](https://docs.derivative.ca/Container_COMP "Container COMP") ([diff](https://docs.derivative.ca/index.php?title=Container_COMP&diff=cur&oldid=10206 "Container COMP")) | [Newer revision →](https://docs.derivative.ca/index.php?title=Container_COMP&direction=next&oldid=10206 "Container COMP") ([diff](https://docs.derivative.ca/index.php?title=Container_COMP&diff=next&oldid=10206 "Container COMP"))

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
  

* Invalid title: ""
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Container Component groups together any number of button, slider, field, container and other [Panel Components](https://docs.derivative.ca/Panel_Component "Panel Component") to build an interface. For example, the Container Component would be used to start creating your control panel, inside it you would place all the sliders, buttons, and viewer panels. It could also be used to group multiple sliders and buttons together into one panel that can be moved and scaled together, such as 3 RGB sliders for a color picker in your control panel.
[![PythonIcon.png](https://docs.derivative.ca/images/c/c2/PythonIcon.png)](https://docs.derivative.ca/File:PythonIcon.png)[[{{{opClass}}}]]
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Layout Page](#Parameters_-_Layout_Page)
* [3 Parameters - Panel Page](#Parameters_-_Panel_Page)
* [4 Parameters - Look Page](#Parameters_-_Look_Page)
* [5 Parameters - Children Page](#Parameters_-_Children_Page)
* [6 Parameters - Drag/Drop Page](#Parameters_-_Drag/Drop_Page)
* [7 Parameters - Extensions Page](#Parameters_-_Extensions_Page)
* [8 Parameters - Common Page](#Parameters_-_Common_Page)
  

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
Help DAT `helpdat` - Lets you specify the path to a [Text DAT](https://docs.derivative.ca/Text_DAT "Text DAT") whose content will be displayed as a rollover pop-up help for the control panel.
Cursor `cursor` - ⊞ - Changes the cursor displayed when cursor is over the panel.
* Normal Select `pointer` -
* Link Select `linkselect` -
* Text Select `ibeam` -
* Precision Select `cross` -
* Busy `busy` -
* Activate `activate` -
* Invisible `invisible` -
Multi-Touch `multitouch` - ⊞ - When enabled, this panel will process the first touch it gets in a similar manner to how it processes a mouse click, with updates to u, v, state etc. The touch event must be initiated from the panel. Subsequent touches are ignored. If this panel handles multi-touch events via the [Multi Touch In DAT](https://docs.derivative.ca/Multi_Touch_In_DAT "Multi Touch In DAT"), you may want to disable Built-in Multi-Touch so it won't interfere with script processing.
* Use Parent's Multi-Touch Settings `mtouchparent` - Use the parent's Multi-Touch setting. This defaults to enabled in the root component.
* Use Built-in Multi-Touch `mtouchyes` - Enable use of first touch as mouse.
* Do Not Use Built-in Multi-Touch `mtouchno` - Disable use of first touch as mouse.
Constrain Cursor `constraincursor` - Constrains the cursor to this panel, keeping it inside once it enters.
Click Through `clickthrough` - When enabled all mouse clicks are ignored by this [Panel Component](https://docs.derivative.ca/Panel_Component "Panel Component").
Use Mouse Wheel `mousewheel` - Turn on to capture events when the mouse wheel is used over the panel.
Mouse UV Buttons `uvbuttons` - ⊞ - Allows you to specify which mouse buttons update the uv [Panel Values](https://docs.derivative.ca/Panel_Value "Panel Value").
* Left `uvbuttonsleft` -
* Middle `uvbuttonsmiddle` -
* Right `uvbuttonsright` -
Relative UV `mouserel` - When enabled the uv [Panel Values](https://docs.derivative.ca/Panel_Value "Panel Value") will reflect relative mouse movement.
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
Background TOP `top` - Allows you to specify a [TOP](https://docs.derivative.ca/TOP "TOP") as the background for the panel.
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
Composite `composite` - ⊞ - Selects how the panel is composited with its siblings panels. See the [Composite TOP](https://docs.derivative.ca/Composite_TOP "Composite TOP") for a description of the various composite methods.
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
Please refer to [Drag-and-Drop](https://docs.derivative.ca/Drag-and-Drop "Drag-and-Drop") for a full explanation on how Drag and Drop between Panel Components functions.
When Dragging This `drag` - ⊞ - Specify if this Panel Component can be dragged.
* Use Parent's Drag Settings `dragparent` - Follow the parent Panel Components Drag setting.
* Legacy Drag System `legacy` - Allow Dragging for this Panel Component. Use the Paramters `Drag Script`, `Drop Destination Script` and `Dropped Operator` to control the behaviour.
* Do Not Allow Drag `dragno` - Disallows Dragging for this Panel Component.
Drag Script `dragscript` - Specify a script that will be executed when starting to drag a Panel Component. Please refer to the Drag Script section of the [Drag and Drop](https://docs.derivative.ca/Drag-and-Drop#Drag_Scripts "Drag-and-Drop") page.
Drop Destination Script `dropdestscript` - Specify a script that will be executed when the dragged Panel Component is dropped. A temporary network is created and the component (or the alternative operator specified in Dropped Component) is copied to this network. You can add or modify operators in this network. Please refer to the Drop Destination Script section of the [Drag and Drop](https://docs.derivative.ca/Drag-and-Drop#Drop_Destination_Scripts "Drag-and-Drop") page.
Drop Types `droptypescript` - If a drop destination script is specified, you can also add a DAT table with a list of return types that the drop destination script will provide. Return types can be one of the op types (COMP,TOP,CHOP,SOP,MAT,DAT), channel, or supported filetypes. Please refer to the Drop Types section of the [Drag and Drop](https://docs.derivative.ca/Drag-and-Drop#Drop_Types "Drag-and-Drop") page.
Dropped Operator `paneldragop` - The Dropped Component parameter is the easiest way to specify an alternative operator to drop. Note that this alternative operator must exist, otherwise the component itself will be dropped. The alternative is only used when dropping onto a network or control panel. Text pasted via dragging and dropping, or files saved via dropping onto the desktop, will still use the original.
On Dropping Into `drop` - ⊞ - Specify if this Panel Component accepts items that are dropped onto it.
* Use Parent's Drop Settings `dropparent` - Follow the parent Panel Components Drop setting.
* Legacy Drop System `legacy` - Allow Dropping onto this Panel Component. Use the Paramter `Drop Script` to control the behaviour.
* Do Not Allow Drop `dropno` - Disallows Dropping onto this Panel Component.
Drop Script `dropscript` - A component's Drop Script is run when you drop another component or an external file into that component. Please refer to the Drop Scripts - Text section of the [Drag and Drop](https://docs.derivative.ca/Drag-and-Drop#Drop_Scripts_-_Text "Drag-and-Drop") page.
Alternatively specify a Table DAT in the drop script field. TouchDesigner will automatically look for 2 columns in the table. The first column should indicate the data type and the second should indicate the Text DAT that holds the script to process that data type. Please refer to the Drop Script - Tables section of the [Drag and Drop](https://docs.derivative.ca/Drag-and-Drop#Drop_Script_-_Tables "Drag-and-Drop") page.

  

## Parameters - Extensions Page
The Extensions parameter page sets the component's python extensions. Please see [extensions](https://docs.derivative.ca/Extensions "Extensions") for more information.
Extension `ext` - Sequence of info for creating extensions on this component
Object `ext0object` - A number of class instances that can be attached to the component.
Name `ext0name` - Optional name to search by, instead of the instance class name.
Promote `ext0promote` - Controls whether or not the extensions are visible directly at the component level, or must be accessed through the `.ext` member. Example: `n.Somefunction` vs `n.ext.Somefunction`

Re-Init Extensions `reinitextensions` - Recompile all extension objects. Normally extension objects are compiled only when they are referenced and their definitions have changed.
  

## Parameters - Common Page
The Common parameter page sets the component's [node viewer](https://docs.derivative.ca/Node_Viewer "Node Viewer") and [clone](https://docs.derivative.ca/Clone "Clone") relationships.
Parent Shortcut `parentshortcut` - Specifies a name you can use anywhere inside the component as the path to that component. See [Parent Shortcut](https://docs.derivative.ca/Parent_Shortcut "Parent Shortcut").
Global Shortcut `opshortcut` - Specifies a name you can use anywhere at all as the path to that component. See [Global OP Shortcut](https://docs.derivative.ca/Global_OP_Shortcut "Global OP Shortcut").
Shortcut `iop0shortcut` - Specifies a name you can use anywhere inside the component as a path to "Internal OP" below. See [Internal Operators](https://docs.derivative.ca/Internal_Operators "Internal Operators").
OP `iop0op` - The path to the Internal OP inside this component. See [Internal Operators](https://docs.derivative.ca/Internal_Operators "Internal Operators").
Node View `nodeview` - ⊞ - Determines what is displayed in the node viewer, also known as the [Node Viewer](https://docs.derivative.ca/Node_Viewer "Node Viewer"). Some options will not be available depending on the Component type ([Object Component](https://docs.derivative.ca/Object_Component "Object Component"), [Panel Component](https://docs.derivative.ca/Panel_Component "Panel Component"), Misc.)
* Default Viewer `default` - Displays the default viewer for the component type, a 3D Viewer for Object COMPS and a Control Panel Viewer for Panel COMPs.
* Operator Viewer `opviewer` - Displays the node viewer from any operator specified in the Operator Viewer parameter below.
Operator Viewer `opviewer` - Select which operator's node viewer to use when the Node View parameter above is set to Operator Viewer.
Keep in Memory `keepmemory` - Used only for [Panel Components](https://docs.derivative.ca/Panel_Component "Panel Component") this keeps the panel in memory to it doesn't reload every time it is displayed.
Enable Cloning `enablecloning` - Control if the OP should be actively cloneing. Turning this off causes this node to stop cloning it's 'Clone Master'.
Enable Cloning Pulse `enablecloningpulse` - Instantaneously clone the contents.
Clone Master `clone` - Path to a component used as the Master [Clone](https://docs.derivative.ca/Clone "Clone").
Load on Demand `loadondemand` - Loads the component into memory only when required. Good to use for components that are not always used in the project.
External .tox `externaltox` - Path to a `.tox` file on disk which will source the component's contents upon start of a `.toe`. This allows for components to contain networks that can be updated independently. If the `.tox` file can not be found, whatever the `.toe` file was saved with will be loaded.
Reload .tox on Start `reloadtoxonstart` - When on (default), the external .tox file will be loaded when the .toe starts and the contents of the COMP will match that of the external .tox. This can be turned off to avoid loading from the referenced external .tox on startup if desired (the contents of the COMP are instead loaded from the .toe file). Useful if you wish to have a COMP reference an external .tox but not always load from it unless you specifically push the Re-Init Network parameter button.
Reload Custom Parameters `reloadcustom` - When this checkbox is enabled, the values of the component's [Custom Parameters](https://docs.derivative.ca/Custom_Parameters "Custom Parameters") are reloaded when the [.tox](https://docs.derivative.ca/.tox ".tox") is reloaded. This only affects top-level parameters on the component, all parameters on nodes inside the component are always reloaded with the [.tox](https://docs.derivative.ca/.tox ".tox").
Reload Built-In Parameters `reloadbuiltin` - When this checkbox is enabled, the values of the component's built-in parameters are reloaded when the [.tox](https://docs.derivative.ca/.tox ".tox") is reloaded. This only affects top-level parameters on the component, all parameters on nodes inside the component are always reloaded with the [.tox](https://docs.derivative.ca/.tox ".tox").
Save Backup of External `savebackup` - When this checkbox is enabled, a backup copy of the component specified by the External `.tox` parameter is saved in the `.toe` file. This backup copy will be used if the External `.tox` can not be found. This may happen if the `.tox` was renamed, deleted, or the `.toe` file is running on another computer that is missing component media.
Sub-Component to Load `subcompname` - When loading from an External `.tox` file, this option allows you to reach into the `.tox` and pull out a COMP and make that the top-level COMP, ignoring everything else in the file (except for the contents of that COMP). For example if a `.tox` file named `project1.tox` contains `project1/geo1`, putting `geo1` as the Sub-Component to Load, will result in `geo1` being loaded in place of the current COMP. If this parameter is blank, it just loads the `.tox` file normally using the top level COMP in the file.
Re-Init Network `reinitnet` - This button will re-load from the external `.tox` file (if present), followed by re-initializing itself from its master, if it's a clone.
  
TouchDesigner Build: Latest\nwikieditor2022.241402021.100002020.200002018.28070before 2018.28070
| COMPs |
| --- |
| [Actor](https://docs.derivative.ca/Actor_COMP "Actor COMP") • [Ambient Light](https://docs.derivative.ca/Ambient_Light_COMP "Ambient Light COMP") • [Animation](https://docs.derivative.ca/Animation_COMP "Animation COMP") • [Annotate](https://docs.derivative.ca/Annotate_COMP "Annotate COMP") • [Base](https://docs.derivative.ca/Base_COMP "Base COMP") • [Blend](https://docs.derivative.ca/Blend_COMP "Blend COMP") • [Bone](https://docs.derivative.ca/Bone_COMP "Bone COMP") • [Bullet Solver](https://docs.derivative.ca/Bullet_Solver_COMP "Bullet Solver COMP") • [Button](https://docs.derivative.ca/Button_COMP "Button COMP") • [Camera Blend](https://docs.derivative.ca/Camera_Blend_COMP "Camera Blend COMP") • [Camera](https://docs.derivative.ca/Camera_COMP "Camera COMP") • [MediaWiki:Common.js](https://docs.derivative.ca/MediaWiki:Common.js "MediaWiki:Common.js") • [Component](https://docs.derivative.ca/Component "Component") • [Experimental:Component](https://docs.derivative.ca/Experimental:Component "Experimental:Component") • [Constraint](https://docs.derivative.ca/Constraint_COMP "Constraint COMP") • Container• [Engine](https://docs.derivative.ca/Engine_COMP "Engine COMP") • [Environment Light](https://docs.derivative.ca/Environment_Light_COMP "Environment Light COMP") • [FBX](https://docs.derivative.ca/FBX_COMP "FBX COMP") • [Field](https://docs.derivative.ca/Field_COMP "Field COMP") • [Force](https://docs.derivative.ca/Force_COMP "Force COMP") • [Geo Text](https://docs.derivative.ca/Geo_Text_COMP "Geo Text COMP") • [Geometry](https://docs.derivative.ca/Geometry_COMP "Geometry COMP") • [GLSL](https://docs.derivative.ca/GLSL_COMP "GLSL COMP") • [Handle](https://docs.derivative.ca/Handle_COMP "Handle COMP") • [Impulse Force](https://docs.derivative.ca/Impulse_Force_COMP "Impulse Force COMP") • [Light](https://docs.derivative.ca/Light_COMP "Light COMP") • [List](https://docs.derivative.ca/List_COMP "List COMP") • [Null](https://docs.derivative.ca/Null_COMP "Null COMP") • [Nvidia Flex Solver](https://docs.derivative.ca/Nvidia_Flex_Solver_COMP "Nvidia Flex Solver COMP") • [Nvidia Flow Emitter](https://docs.derivative.ca/Nvidia_Flow_Emitter_COMP "Nvidia Flow Emitter COMP") • [OP Viewer](https://docs.derivative.ca/OP_Viewer_COMP "OP Viewer COMP") • [Parameter](https://docs.derivative.ca/Parameter_COMP "Parameter COMP") • [Replicator](https://docs.derivative.ca/Replicator_COMP "Replicator COMP") • [Select](https://docs.derivative.ca/Select_COMP "Select COMP") • [Shared Mem In](https://docs.derivative.ca/Shared_Mem_In_COMP "Shared Mem In COMP") • [Shared Mem Out](https://docs.derivative.ca/Shared_Mem_Out_COMP "Shared Mem Out COMP") • [Slider](https://docs.derivative.ca/Slider_COMP "Slider COMP") • [Table](https://docs.derivative.ca/Table_COMP "Table COMP") • [Text](https://docs.derivative.ca/Text_COMP "Text COMP") • [Experimental:Text](https://docs.derivative.ca/Experimental:Text_COMP "Experimental:Text COMP") • [Time](https://docs.derivative.ca/Time_COMP "Time COMP") • [USD](https://docs.derivative.ca/USD_COMP "USD COMP") • [Widget](https://docs.derivative.ca/Widget_COMP "Widget COMP") • [Window](https://docs.derivative.ca/Window_COMP "Window COMP") |
The Container component type is a [Panel Component](https://docs.derivative.ca/Panel_Component "Panel Component") that holds, lays out and displays any number of other Panel Components.

An [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") that contains its own [Network](https://docs.derivative.ca/Network "Network"). There are sixteen 3D [Object Component](https://docs.derivative.ca/Object_Component "Object Component") and ten 2D [Panel Component](https://docs.derivative.ca/Panel_Component "Panel Component") types. See also [Network Path](https://docs.derivative.ca/Network_Path "Network Path").

(1) The TouchDesigner window is made of a menu bar at the top, a [Timeline](https://docs.derivative.ca/Timeline "Timeline") at the bottom, plus one of a choice of Layouts in the middle. A Layout is made on one or more Panes, each Pane can contain a Network Editor, Viewer, Panel, etc. See [Pane](https://docs.derivative.ca/Pane "Pane") and [Bookmark](https://docs.derivative.ca/Bookmark "Bookmark"). (2) Nodes in a network are arranged using Layout commands in the RMB menu.

A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](https://docs.derivative.ca/Panel_Component "Panel Component").

A Window in TouchDesigner is a window in Microsoft Windows or macOS that contains either (1) the TouchDesigner editing interface that exists in [Designer Mode](https://docs.derivative.ca/Designer_Mode "Designer Mode"), or (2) a user-created [Panel](https://docs.derivative.ca/Panel "Panel") inside a [Window Component](https://docs.derivative.ca/Window_COMP "Window COMP"). The user-created windows can span [Multiple Monitors](https://docs.derivative.ca/Multiple_Monitors "Multiple Monitors") borderless, or be floating windows with borders, or popups.

An [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](https://docs.derivative.ca/Script "Script") or [GLSL](https://docs.derivative.ca/GLSL "GLSL") Shader, but can be any multi-line text. [Tables](https://docs.derivative.ca/Table_DAT "Table DAT") are rows and columns of cells, each containing a text string.

A [Link](https://docs.derivative.ca/Link "Link"). The grey dashed lines between nodes is a Reference or Link that indicates one operator is getting data from another operator from any [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family").
A Link or Reference is a dashed line between nodes that represent other data flowing between nodes. Examples are CHOP [Exports](https://docs.derivative.ca/Export "Export"), node [Paths](https://docs.derivative.ca/Network_Path "Network Path") in parameters, and [expressions](https://docs.derivative.ca/Expression "Expression") in parameters referencing CHOP channels, DAT tables and other nodes. In contrast is a [Wire](https://docs.derivative.ca/Wire "Wire") that connects nodes in the same [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family").

Display devices in TouchDesigner that support multiple-finger or control-point input.

There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](https://docs.derivative.ca/3D_Parenting "3D Parenting") and panel [Parenting](https://docs.derivative.ca/Parent "Parent").

An [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

The width and height of an image in pixels. Most TOPs, like the [Movie File In TOP](https://docs.derivative.ca/Movie_File_In_TOP "Movie File In TOP") can set the image resolution. See [Aspect Ratio](https://docs.derivative.ca/TOP_Generator_Common_Page "TOP Generator Common Page") for the width/height ratio of an image, taking into account non-square pixels.

An [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") that contains its own [Network](https://docs.derivative.ca/Network "Network"). There are sixteen 3D [Object Component](https://docs.derivative.ca/Object_Component "Object Component") and ten 2D [Panel Component](https://docs.derivative.ca/Panel_Component "Panel Component") types. See also [Network Path](https://docs.derivative.ca/Network_Path "Network Path").

The sub-[Family](https://docs.derivative.ca/Operator_Family "Operator Family") of [Components](https://docs.derivative.ca/Component "Component") that are used to create custom interactive 2D control [panels](https://docs.derivative.ca/Panel "Panel") (Container, Widget, Text COMP Slider, Button, etc.).

A set of commands located in a Text DAT that are triggered to run under certain conditions. There are two scripting languages in TouchDesigner: [Python](https://docs.derivative.ca/Python "Python") and the original [Tscript](https://docs.derivative.ca/Tscript "Tscript"). Scripts and single-line commands can also be run in the [Textport](https://docs.derivative.ca/Textport "Textport").

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](https://docs.derivative.ca/Node "Node").

An [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") which operate on [Channels](https://docs.derivative.ca/Channel "Channel") (a sequence of numbers ([Samples](https://docs.derivative.ca/Sample "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

A [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

MATs or Materials are an [Operator Family](https://docs.derivative.ca/Operator_Family "Operator Family") that applies a [Shader](https://docs.derivative.ca/Shader "Shader") to a SOP or 3D Geometry Object for rendering textured surfaces with lighting.

A form of [DATs](https://docs.derivative.ca/DAT "DAT") (Data Operators) that is structured as rows and columns of text strings.

Any component can be extended with its own Python classes which contain python functions and data.

The sub-[Family](https://docs.derivative.ca/Operator_Family "Operator Family") of [Component](https://docs.derivative.ca/Component "Component") types that are used to define and render 3D scenes. A [Geometry Component](https://docs.derivative.ca/Geometry_COMP "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](https://docs.derivative.ca/Camera_COMP "Camera COMP") and [Light COMP](https://docs.derivative.ca/Light_COMP "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.

Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](https://docs.derivative.ca/Parent_Shortcut "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](https://docs.derivative.ca/Global_OP_Shortcut "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](https://docs.derivative.ca/Node "Node").

The viewer of a node can be (1) the interior of a node (the [Node Viewer](https://docs.derivative.ca/Node_Viewer "Node Viewer")), (2) a floating window (RMB->View... on node), or (3) a [Pane](https://docs.derivative.ca/Pane "Pane") that graphically shows the results of an operator.

A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](https://docs.derivative.ca/Panel_Component "Panel Component").

Cloning makes multiple components match the contents of a master component. A [Component](https://docs.derivative.ca/Component "Component") whose Clone parameter is set will be forced to contain the same nodes, wiring and parameters as its master component. Cloning does not create new components as does the [Replicator COMP](https://docs.derivative.ca/Replicator_COMP "Replicator COMP").

To "pulse" a parameter is to send it a signal from (1) an [exported](https://docs.derivative.ca/Export "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](https://docs.derivative.ca/Speed_CHOP "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](https://docs.derivative.ca/Root "Root"). This path is displayed at the top of every [Pane](https://docs.derivative.ca/Pane "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](https://docs.derivative.ca/Folder "Folder").

TouchDesigner Component file, the file type used to save a [Component](https://docs.derivative.ca/Component "Component") of your TouchDesigner project.

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

Every component contains a network of operators that create and modify data. The operators are connected by wires that define where data is routed after the operator cooks its inputs and generates an output.

Retrieved from "<https://docs.derivative.ca/index.php?title=Container_COMP&oldid=10206>"
[Categories](https://docs.derivative.ca/Special:Categories "Special:Categories"):
* [Touch Glossary](https://docs.derivative.ca/Category:Touch_Glossary "Category:Touch Glossary")
* [COMPs](https://docs.derivative.ca/index.php?title=Category:COMPs&action=edit&redlink=1 "Category:COMPs (page does not exist)")