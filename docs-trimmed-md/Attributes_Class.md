

# Attributes_Class

Attributes Class - Derivative




# Attributes Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
An Attributes object describes a set of [Prim](Prim_Class.html "Prim Class") Class, [Point](Point_Class.html "Point Class") Class, or [Vertex Class](Vertex_Class.html "Vertex Class") [attributes](Attribute.html "Attribute"), contained within a [SOP](SOP_Class.html "SOP Class").
  

## Members
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
## Methods
`[name]`→ `Attribute`:
> [Attributes](Attribute_Class.html "Attribute Class") can be accessed using the [] subscript operator.
> 
> * name - The name of the attribute.
> 
> ```
> attribs = scriptOP.pointAttribs # get the Attributes object
> normals = attribs['N']
> 
> ```
`create(name, default)`→ `Attribute`:
> Create a new [Attribute](Attribute_Class.html "Attribute Class").
> 
> * name - The name of the attribute.
> * default - (Optional) Specify default values for custom attributes. For standard attributes, default values are implied.
> 
> Standard attributes are: N (normal), uv (texture), T (tangent), v (velocity), Cd (diffuse color).
> 
> ```
> # create a Normal attribute with implied defaults.
> n = scriptOP.pointAttribs.create('N')
> 
> # set the X component of the first point's Normal attribute.
> scriptOp.points[0].N[0] = 0.3 
> 
> # Create a Vertex Attribute called custom1 with defaults set to (0.0, 0.0)
> n = scriptOP.vertexAttribs.create('custom1', (0.0, 0.0) )
> 
> # Create a Primitive Attribute called custom2 defaulting to 1
> n = scriptOP.primAttribs.create('custom2', 1 )
> 
> ```
TouchDesigner Build: Latest\nwikieditor2022.241402021.100002018.28070before 2018.28070
Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

A surface type in [SOPs](SOP.html "SOP") that includes polygon, curve (NURBS and Bezier), patch (NURBS and Bezier) and other basic shapes like sphere, tube and metaball. [Points](Point.html "Point") and Primitives are part of the [Geometry Detail](Geometry_Detail.html "Geometry Detail"), which is a part of a [SOP](SOP.html "SOP").

Retrieved from "<https://docs.derivative.ca/index.php?title=Attributes_Class&oldid=31419>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")