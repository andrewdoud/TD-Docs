

TOP Viewer - Derivative
























# TOP Viewer

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

All [TOP](TOP.html "TOP") operators have interactive [Node Viewers](Node_Viewer.html "Node Viewer"). To interact with it, turn on the TOP's [Viewer Active Flag](Viewer_Active_Flag.html "Viewer Active Flag") to make the viewer active.

[![TOPviewer.jpg](images/b/bb/TOPviewer.jpg)](File_TOPviewer.html)

A gray checkerboard background will be displayed in images where an alpha channel is present. This can be turned off by opening [Preferences](Dialogs_Preferences_Dialog.html "Dialogs:Preferences Dialog") in the **Edit** menu. In preferences you can choose to use checkerboard or black as you alpha background.

Use [LMB](Mouse_Click.html "Mouse Click") to move the image around. Use [MMB](Mouse_Click.html "Mouse Click") to zoom in and out of the image. Re-center the image by using the home shortcut "**h**".

Clicking the [RMB](Mouse_Click.html "Mouse Click") will open the viewer options menu. Keyboard shortcuts are listed beside each entry in the menu.

[![TOPviewermenu.png](images/c/c1/TOPviewermenu.png)](File_TOPviewermenu.html)

**Home** - Re-centers and scales the image to fit in the viewer.

**Display Pixel Values** - Displays pixel information over the image. The [Timeline](Timeline.html "Timeline") should be playing forward for the values to properly update.

The following is displayed:

* cursor uv coordinates
* cursor xy pixel coordinates
* RGB values 0-255
* RGB values 0-1

**Display Field Guide** - Displays a 24x24 field guide over the image. The guide also displays the action safe zone and title safe zone for the image.

**Display Mode** - The display mode options give the option of viewing certain channels of the image.

The following display modes are available:

* Color - Display all RGB channles.
* Red/Green/Blue/Alpha - Display the Red/Green/Blue/Alpha channel respectively.
* Mono - Display the image in monochrome.
* Normalize Split - Displays each channel in the image at the same time normalized from 0-1. Excellent for viewing floating point and point cloud data.

**View as Points** - Displays the data in the TOP as 3D points for each pixel assuming red = x, green = y, and blue = z. Useful for viewing point cloud data.

[![PointCloudViews.png](images/thumb/c/cc/PointCloudViews.png/800px-PointCloudViews.png)](File_PointCloudViews.html)

Point cloud data displayed 3 modes: 1) Color 2) Normalized Split 3) View as Points

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.







Retrieved from "<https://docs.derivative.ca/index.php?title=TOP_Viewer&oldid=20207>"
[Category](Special_Categories.html "Special:Categories"):

* [TOPs](Category_TOPs.html "Category:TOPs")