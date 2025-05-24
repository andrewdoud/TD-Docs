

# Position_Class

Position Class - Derivative




# Position Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The position class holds a single 3 component position. A position is a single point in space, and it's important to use a position or [vector](Vector_Class.html "Vector Class") as appropriate for the data that is being calculated, since matrix operations on them will end in different results. When being multiplied by a [Matrix](Matrix_Class.html "Matrix Class"), this class will implicitly have a 4th component (W component) of 1. If the Matrix is a projection matrix that will cause the W component to become something other than 1, all 4 components will be divided by W to make the position homogeneous again. A new position can be created without any arguments, with 3 arguments for the x,y,z values, or with a single argument which is a variable that has 3 entries such as a list of length 3, or another position or vector.
  
Examples of creating a position:
```
p = tdu.Position() # starts as (0, 0, 0)
p2 = tdu.Position(1, 5, 0)
values = [0, 1, 0]
p3 = tdu.Position(values)
```
  

## Members
`x` → `float` :
> Gets or sets the X component of the position.
`y` → `float` :
> Gets or sets the Y component of the position.
`z` → `float` :
> Gets or sets the Z component of the position.
## Methods
`translate(x, y, z)`→ `None`:
> Translates the position by the specified values.
> 
> * x, y, z - The values to translate by.
> 
> ```
> p.translate(5, 2, 0)
> 
> ```
`scale(x, y, z)`→ `None`:
> Scales each component of the position by the specified values.
> 
> * x, y, z - The values to scale each component of the position by.
> 
> ```
> p.scale(1, 2, 1)
> 
> ```
`copy()`→ `tdu.Position`:
> Returns a new position that is a copy of the position.
> 
> ```
> newV = v.copy()
> 
> ```
### Special Functions[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Special Functions")]
`tdu.Position[i]`→ `float`:
> Gets or sets the component of the position specified by i, where i can be 0, 1, or 2.
> 
> ```
> y = p[1]
> p[1] = y + 2.0
> 
> ```
`tdu.Position * float`→ `tdu.Position`:
> Scales the position by the give float scalar and returns a new Position as the result.
> 
> ```
> p = p * 0.1
> p = 0.1 * p
> 
> ```
`tdu.Position + float`→ `tdu.Position`:
> Adds the given scalar to all 3 components of the position and returns a new position as the result.
> 
> ```
> p = p + 1.2
> p = 1.2 + p
> 
> ```
`tdu.Position - float`→ `tdu.Position`:
> Subtracts the given scalar from all 3 components of the position and returns a new position as the result.
> 
> ```
> p = p - 1.2
> p = 1.2 - p
> 
> ```
`tdu.Vector + tdu.Position`→ `tdu.Position`:
> Adds the vector to the position. ie. it displaces the given position by the vector. Returns a new position as the result.
> 
> ```
> p2 = v + p1
> p2 = p1 + v
> 
> ```
`tdu.Position - tdu.Vector`→ `tdu.Position`:
> Subtracts the vector from the position. Notice that the reverse is not a legal operation: subtracting a position from a vector does not have any meaning. Returns a new position with the results.
> 
> ```
> p2 = p1 - v
> 
> ```
`tdu.Position - tdu.Position`→ `tdu.Vector`:
> Subtracts the two positions to create a vector that is pointing from the 2nd one to the 1st one, with length equal to the distance between the positions.
> 
> ```
> v = p1 - p2
> 
> ```
`tdu.Position += float`→ `None`:
> Adds the given scalar to all 3 components of the position, the position will contain the result of the operation.
> 
> ```
> p += 0.1
> 
> ```
`tdu.Position += tdu.Vector`→ `None`:
> Displaces the position by the given vector, the position will contain the result of the operation.
> 
> ```
> p += v
> 
> ```
`tdu.Position -= float`→ `None`:
> Subtracts the given scalar from all 3 components of the position, the position will contain the result of the operation.
> 
> ```
> p -= 0.4
> 
> ```
`tdu.Position -= tdu.Vector`→ `None`:
> Displaces the position by the given vector, the position will contain the result of the operation.
> 
> ```
> p -= v
> 
> ```
`tdu.Matrix * tdu.Position`→ `tdu.Position`:
> Multiplies the Position by the matrix and returns the a new position as the result.
> 
> ```
> p2 = m * p1
> 
> ```
`tdu.Position / float`→ `tdu.Position`:
> Divides each component of the position by the scalar and returns the a new position as the result.
> 
> ```
> p2 = p1 / 2.0
> 
> ```
`tdu.Position *= tdu.Matrix`→ `None`:
> Multiplies the position by the matrix, the position will contain the result. The is position multiplied on the right of the matrix. It is the equivalent of doing Position = Matrix \* Position.
> 
> ```
> p *= m
> 
> ```
`tdu.Position *= float`→ `None`:
> Scales all 3 components of the position by the given scalar. The position will contain the result.
> 
> ```
> p *= 1.3
> 
> ```
`tdu.Position *= tdu.Position`→ `None`:
> Component-wise multiplies the 3 components of the first position by the 3 components of the 2nd position.
> 
> ```
> p1 *= p2
> 
> ```
`abs(tdu.Position)`→ `tdu.Position`:
> Returns a new position with all 3 components being the absolute value of the given position's components.
> 
> ```
> p2 = abs(p1)
> 
> ```
`-tdu.Position`→ `tdu.Position`:
> Returns a new position with all 3 component's being negated.
> 
> ```
> p2 = -p1
> 
> ```
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

Retrieved from "<https://docs.derivative.ca/index.php?title=Position_Class&oldid=12160>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")