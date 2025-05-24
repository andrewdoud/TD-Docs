

# Panel_COMP_Panel_Page

Panel COMP Panel Page - Derivative




# Panel COMP Panel Page
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Parameters - Panel Page[[edit](https://docs.derivative.ca/index.php?title=Panel_COMP_Panel_Page&action=edit&section=1 "Edit section: Parameters - Panel Page")]
The Panel parameter page controls panel attributes such as display on/off, enable on/off, panel help, and interactions with the cursor.
Display `display` - Specifies if the panel is displayed or hidden.
Enable `enable` - Allows you to prevent all interaction with this panel.
Help DAT `helpdat` - Lets you specify the path to a [Text DAT](Text_DAT.html "Text DAT") whose content will be displayed as a rollover pop-up help for the control panel.
Floating Viewer Aspect `vieweraspect` - Controls whether the aspect ratio is proportional or unconstrained when resizing a floating viewer ie. dragging the edges of the viewer to resize it.
  
Cursor `cursor` - Changes the cursor displayed when cursor is over the panel.
Multi-Touch `multitouch` - When enabled, this panel will process the first touch it gets in a similar manner to how it processes a mouse click, with updates to u, v, state etc. The touch event must be initiated from the panel. Subsequent touches are ignored. If this panel handles multi-touch events via the [Multi Touch In DAT](Multi_Touch_In_DAT.html "Multi Touch In DAT"), you may want to disable Built-in Multi-Touch so it won't interfere with script processing.
* Use Parent's Multi-Touch Settings - Use the parent's Multi-Touch setting. This defaults to enabled in the root component.
* Use Built-in Multi-Touch - Enable use of first touch as mouse.
* Do Not Use Built-in Multi-Touch - Disable use of first touch as mouse.
Click Through `clickthrough` - When enabled all mouse clicks are ignored by this [Panel Component](Panel_Component.html "Panel Component").
Use Mouse Wheel `mousewheel` - Turn on to capture events when the mouse wheel is used over the panel.
Mouse UV Buttons `uvbuttons[left,middle,right]` - Allows you to specify which mouse buttons update the uv [Panel Values](Panel_Value.html "Panel Value").
Relative UV `mouserel` - When enabled the uv [Panel Values](Panel_Value.html "Panel Value") will reflect relative mouse movement.
  
Drag Edges to Resize `resize[lrbt]` - Four checkboxes allow you to enable resizing a panel by grabbing the corresponding edge or corner: Resize Left, Right, Bottom, Top.
W Range `resizewmin resizewmax` - Limits the left-right (width) resizing range.
H Range `resizehmin resizehmax` - Limits the bottom-top (height) resizing range.
Drag to Reposition `reposition` - Enables repositioning of the panel or window by dragging with the mouse.
Component `repocomp` - Enabled by choosing the **Component** option from the Reposition parameter. Specify the path to the panel component you would like to reposition by mouse.
X Range `repositionx[min,max]` - Enabled by choosing the **Component** option from the Reposition parameter. Sets the maximum range for repositioning the panel component horizontally.
Y Range `repositiony[min,max]` - Enabled by choosing the **Component** option from the Reposition parameter. Sets the maximum range for repositioning the panel component vertically.
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

Display devices in TouchDesigner that support multiple-finger or control-point input.

There are 2 kinds of parenting. The "parent component" is the component in which a node resides. The metaphor is extended to include grand parents, grand-grand parents, etc. The root `/` is the ultimate parent to all nodes. See also [3D Parenting](3D_Parenting.html "3D Parenting") and panel [Parenting](Parent.html "Parent").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

Retrieved from "<https://docs.derivative.ca/index.php?title=Panel_COMP_Panel_Page&oldid=33662>"
[Category](Special_Categories.html "Special:Categories"):
* [OP Help Common Pages](https://docs.derivative.ca/index.php?title=Category:OP_Help_Common_Pages&action=edit&redlink=1 "Category:OP Help Common Pages (page does not exist)")