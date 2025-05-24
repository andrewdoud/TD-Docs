

Vertex Class - Derivative




# Vertex Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
A Vertex describes an instance to a single geometry vertex, contained within a [Prim](Prim_Class.html "Prim Class") object.
  

## Members
`index` → `int` **(Read Only)**:
> The vertex position in its [primitive](Prim_Class.html "Prim Class").
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
`point` → `td.Point` :
> Get or set the [point](Point_Class.html "Point Class") to which the vertex refers.
`prim` → `td.Prim` **(Read Only)**:
> The [prim](Prim_Class.html "Prim Class") to which the vertex belongs.
### Attributes[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Attributes")]
In addition to the above members, all attributes are members as well.
For example, if the Vertex contains texture coordinates, they may be accessed with: `Vertex.uv`
See: [Attribute Class](Attribute_Class.html "Attribute Class") for more information.
## Methods
No operator specific methods.
  
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

Retrieved from "<https://docs.derivative.ca/index.php?title=Vertex_Class&oldid=13561>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")