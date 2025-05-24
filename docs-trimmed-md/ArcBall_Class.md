

ArcBall Class - Derivative




# ArcBall Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
Encapsulates many aspects of 3D viewer interaction. Rotation via arcball, translation and scale.
```
a = tdu.ArcBall(forCamera=False)
```
The 'forCamera' argument controls whether matrices used by the tranform and setTransform methods are from the world or camera perspective. When forCamera is true, the world matrices are inverted before being returned or used.
  

## Members
No operator specific members.
  

## Methods
`beginPan(u, v)`→ `None`:
> Begin a pan at at the given u and v.
> 
> ```
> m.beginPan(.1, .2)
> 
> ```
`beginRotate(u, v)`→ `None`:
> Begin an arcball rotation at the given u and v.
> 
> ```
> m.beginRotate(.1, .2)
> 
> ```
`beginDolly(u, v)`→ `None`:
> Begin a dolly at at the given u and v.
> 
> ```
> m.beginDolly(.1, .2)
> 
> ```
`pan(u, v)`→ `None`:
> Pan the view by the given x and y.
> 
> ```
> m.pan(.1, .2)
> 
> ```
`panTo(u, v, scale=1.0)`→ `None`:
> Pan from the u,v given in the last call to beginPan() to the given u and v, applying a scale as well to the pan amount.
> 
> * scale - (Keyword, Optional) Scale the operation by this amount.
> 
> ```
> m.panTo(.1, .2)
> 
> ```
`rotateTo(u, v, scale=1.0)`→ `None`:
> Rotates the arcball to the given u and v position.
> 
> * scale - (Keyword, Optional) Scale the operation by this amount.
> 
> ```
> m.rotateTo(.1, .2)
> 
> ```
`dolly(z)`→ `None`:
> Dolly the view by the given z value.
> 
> ```
> m.dolly(.3)
> 
> ```
`dollyTo(u, v, scale=1.0)`→ `None`:
> Dolly from the u,v given in the last call to beginDolly() to the given u and v, applying a scale as well to the dolly amount.(Keyword, Optional)
> 
> * scale - Scale the operation by this amount.
> 
> ```
> m.dollyTo(.1, .2)
> 
> ```
`transform()`→ `tdu.Matrix`:
> Gets the current transform [matrix](Matrix_Class.html "Matrix Class") for the arcball.
> 
> ```
> m.transform()
> 
> ```
`setTransform(matrix)`→ `None`:
> Sets the current transform matrix for the arcball. Scales in the given matrix will be ignored.
> 
> ```
> m.setTransform(m)
> 
> ```
`identity()`→ `None`:
> Resets all values of the ArcBall to the default state.
> 
> ```
> m.identity()
> 
> ```
TouchDesigner Build: 
Latest\nwikieditor
wikieditor
wikieditor
mw-rollback
mw-reverted
2022.24140
2021.10000
2018.28070
before 2018.28070

Retrieved from "<https://docs.derivative.ca/index.php?title=ArcBall_Class&oldid=31357>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")