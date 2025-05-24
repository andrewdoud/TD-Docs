

Prim Class - Derivative




# Prim Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
A Prim describes an instance to a single [geometry primitive](Primitive.html "Primitive"). They are accessible through the [SOP.prims](SOP_Class.html "SOP Class") member.
  

## Members
`center` → `TDU.Position` :
> Get or set the barycentric coordinate of this primitive. It is expressed as a TDU.Position object.
`index` → `int` **(Read Only)**:
> The primitive index in the list.
`normal` → `TDU.Vector` **(Read Only)**:
> The calculated normal vector of this primitive, expressed as a TDU.Vector object.
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
`weight` → `float` **(Read Only)**:
> The associated weight of the primitive. Only certain primitives, such as those created by the [Metaball SOP](Metaball_SOP.html "Metaball SOP") can modify this value from its default of 2.0.
`direction` → `TDU.Vector` **(Read Only)**:
> A normalized vector pointing from the centroid of the SOP to the centroid of this primitive.
`min` → `TDU.Position` **(Read Only)**:
> The minimum coordinates of this primitive along each dimension, expressed as a TDU.Position object.
`max` → `TDU.Position` **(Read Only)**:
> The maximum coordinates of this primitive along each dimension, expressed as a TDU.Position object.
`size` → `TDU.Position` **(Read Only)**:
> The size of this primitive along each dimension, expressed as a TDU.Position object.
## Methods
`destroy(destroyPoints=True)`→ `None`:
> Destroy and remove the actual primitive this object refers to. This operation is only valid when the primitive belongs to a [scriptSOP](https://docs.derivative.ca/ScriptSOP_Class "ScriptSOP Class"). Note: after this call, other existing Prim objects in this SOP may no longer be valid.
> 
> * destroyPoints - (Keyword, Optional) If True, its [points](Point_Class.html "Point Class") are destroyed as well, if false, they are simply detached. The argument is True by default.
`eval(u, v)`→ `TDU.Position`:
> Evaluate the [position](Position_Class.html "Position Class") on the primitive given the u,v coordinates. u,v should be in the range [0,1]. **Note:** Polygons and curves ignore the v parameter.
> 
> ```
> center = op('box1').prim[0].eval(0.5, 0.5)
> 
> ```
### Special Functions[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Special Functions")]
`len(Prim)`→ `int`:
> Returns the total number of vertices.
> 
> ```
> a = len(op('box1').prim[0])
> 
> ```
`[index]`→ `td.Vertex`:
> Get specific vertex given an integer index
> 
> ```
> n = op('box1').prims[5][0]
> 
> ```
`[row, col]`→ `td.Vertex`:
> Get specific vertex from a Mesh given integer row and column values.
> 
> ```
> v = op('grid1').prims[2,3]
> 
> ```
`Iterator`→ `td.Vertex`:
> Iterate over each vertex.
> 
> ```
> for m in op('box1').prims[5]:
> 	# do something with m, which is a Vertex
> 
> ```
  
TouchDesigner Build: Latest\nwikieditor2021.100002018.28070before 2018.28070
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

Retrieved from "<https://docs.derivative.ca/index.php?title=Prim_Class&oldid=31452>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")