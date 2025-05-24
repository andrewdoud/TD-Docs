

Monitor Class - Derivative

























# Monitor Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

The Monitor class describes a single instance of a monitor display. They can be accessed from the [monitors](Monitors_Class.html "Monitors Class") object.

  


## Members

`index` → `int` **(Read Only)**:

> The monitor position in the list.

`isPrimary` → `bool` **(Read Only)**:

> Returns true, if this monitor is the primary display.

`isAffinity` → `bool` **(Read Only)**:

> Returns true, if this monitor is connected to the GPU that has been selected for GPU Affinity. Always True if GPU Affinity is not used.

`width` → `int` **(Read Only)**:

> The width of the monitor area, measured in pixels.

`height` → `int` **(Read Only)**:

> The height of the monitor area, measured in pixels.

`left` → `int` **(Read Only)**:

> The position of left edge of the monitor area, measured in pixels.

`right` → `int` **(Read Only)**:

> The position of right edge of the monitor area, measured in pixels.

`top` → `int` **(Read Only)**:

> The position of top edge of the monitor area, measured in pixels.

`bottom` → `int` **(Read Only)**:

> The position of bottom edge of the monitor area, measured in pixels.

`displayName` → `str` **(Read Only)**:

> The unique display name associated with this monitor.

`description` → `str` **(Read Only)**:

> A description of the monitor or its display adapter.

`dpiScale` → `float` **(Read Only)**:

> The DPI Scaling factor the monitor is current set to.

`scaledWidth` → `int` **(Read Only)**:

> The width of the monitor area, measured in points.

`scaledHeight` → `int` **(Read Only)**:

> The height of the monitor area, measured in points.

`scaledLeft` → `int` **(Read Only)**:

> The position of left edge of the monitor area, measured in points.

`scaledRight` → `int` **(Read Only)**:

> The position of right edge of the monitor area, measured in points.

`scaledTop` → `int` **(Read Only)**:

> The position of top edge of the monitor area, measured in points.

`scaledBottom` → `int` **(Read Only)**:

> The position of bottom edge of the monitor area, measured in points.

`serialNumber` → `str` **(Read Only)**:

> The serial number name associated with this monitor. May be blank.

`refreshRate` → `float` **(Read Only)**:

> The refresh rate the monitor is currently running at.

## Methods

No operator specific methods.

## Accessing Monitors[[edit](https://docs.derivative.ca/index.php?title=Template:Section&action=edit&section=T-1 "Edit section: Accessing Monitors")]

See [Monitors Class](Monitors_Class.html "Monitors Class") for examples on how to access individual monitors.

  

TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.







Retrieved from "<https://docs.derivative.ca/index.php?title=Monitor_Class&oldid=28324>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")