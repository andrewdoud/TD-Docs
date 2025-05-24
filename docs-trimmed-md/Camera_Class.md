

# Camera_Class

Camera Class - Derivative




# Camera Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
Helper class that maintains a 3D position and orientation for a camera and provides multiple methods for manipulating the camera's position and direction. This class is used for the [viewportCamera](Palette_camera.html "Palette:camera") palette component.
  

## Members
`dir` → `tdu.Position` :
> Get or set the direction of the camera as a vector that points towards the target. Up is considered to be (0,1,0).
`pivot` → `tdu.Position` :
> Get or set the 3D point in space where the camera will pivot around or towards.
`position` → `tdu.Position` :
> Get or set the 3D point in space where the camera is located.
## Methods
`blendCamera(targetCamera, blendFactor)`→ `tdu.Camera`:
> Returns a camera that is blended with the given camera using the blendFactor. The camera position is blended using linear interpolation, while the rotation is blended using spherical linear interpolation.
> 
> * targetCamera - A second camera that is the blend target.
> * blendfactor - A blend value between 0 and 1."
`dolly()`→ `None`:
> Move the camera away or towards the pivot point.
`frameBounds()`→ `OrthoWidth`:
> Set the camera to frame the given bounding box. Returns the width of the framed scene that can be used when setting up orthographic projections.
`look()`→ `None`:
> Pivot the camera around its position.
`move3D()`→ `None`:
> Move the camera using data from a 3D mouse.
`pan()`→ `None`:
> Pan the camera in a 2D plane facing the pivot point.
`setTransform()`→ `None`:
> Set the camera view matrix.
`track()`→ `None`:
> Move the camera up/down in the Y-Axis or left/right.
`transform()`→ `None`:
> Get the camera view matrix.
`tumble()`→ `None`:
> Rotate the camera around the pivot point.
`walk()`→ `None`:
> Move the camera forward/back along in the ZX plane and rotate around its position.
TouchDesigner Build: 
Latest\nwikieditor
2022.24140
2021.10000
before 2021.10000

Retrieved from "<https://docs.derivative.ca/index.php?title=Camera_Class&oldid=31210>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")