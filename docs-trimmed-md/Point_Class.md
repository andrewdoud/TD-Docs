

# Point_Class

Point Class - Derivative




# Point Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
A Point describes an instance to a single [geometry point](Point.html "Point"). They are accessible through the [SOP.points](SOP_Class.html "SOP Class") member.
  

## Members
`index` → `int` **(Read Only)**:
> The point index in the list.
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
`P` → `td.AttributeData` :
> The coordinates as [AttributeData](AttributeData_Class.html "AttributeData Class"). Individual components can be read or written with the [] operator.
> 
> ```
> point.P[0] = 5
> point.P = (1,0,1)
> 
> ```
`x` → `float` :
> Get or set x coordinate value. This is the same as P[0].
`y` → `float` :
> Get or set y coordinate value. This is the same as P[1].
`z` → `float` :
> Get or set z coordinate value. This is the same as P[2].
`normP` → `tdu.Position` **(Read Only)**:
> The normalized position of this point within the bounding box of the SOP. Will always be in the range [0,1]. Expressed as tdu.Position object.
### Attributes[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Attributes")]
In addition to the above members, all [attributes](Attribute_Class.html "Attribute Class") are members as well.
For example, if the Point contains texture coordinates, they may be accessed with:`Point.uv`
```
box = op('box1')
print(box.N[0], box.N[1], box.N[2])
print(box.uv[0], box.uv[1], box.uv[2])
```
See: [Attribute Class](Attribute_Class.html "Attribute Class") for more information.
## Methods
`destroy()`→ `None`:
> Destroy and remove the actual point this object refers to. This operation is only valid when the primitive belongs to a [scriptSOP](https://docs.derivative.ca/ScriptSOP_Class "ScriptSOP Class"). Note: after this call, other existing Point objects in this SOP may no longer be valid.
TouchDesigner Build: Latest\n2021.100002020.200002018.28070before 2018.28070
Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

Retrieved from "<https://docs.derivative.ca/index.php?title=Point_Class&oldid=19012>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")