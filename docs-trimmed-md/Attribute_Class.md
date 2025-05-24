

Attribute Class - Derivative




# Attribute Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
An [Attribute](Attribute.html "Attribute") describes a general geometric Attribute, associated with a [Prim Class](Prim_Class.html "Prim Class"), [Point Class](Point_Class.html "Point Class"), or [Vertex Class](Vertex_Class.html "Vertex Class").
Specific values for each Prim, Point or Vertex are described with the [AttributeData Class](AttributeData_Class.html "AttributeData Class").
Lists of attributes for the [SOP](SOP_Class.html "SOP Class") are described with the [Attributes Class](Attributes_Class.html "Attributes Class").
  

## Members
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
`name` → `str` **(Read Only)**:
> The name of this attribute.
`size` → `int` **(Read Only)**:
> The number of values associated with this attribute. For example, a normal attribute has a size of 3.
`type` → `float | int | str | tuple | [TDU.Position](Position_Class.html "Position Class") | [TDU.Vector](Vector_Class.html "Vector Class")` **(Read Only)**:
> The type associated with this attribute: float, integer, string, tuple, [Position](Position_Class.html "Position Class"), or [Vector](Vector_Class.html "Vector Class").
`default` → `float | int | str | tuple | [TDU.Position](Position_Class.html "Position Class") | [TDU.Vector](Vector_Class.html "Vector Class")` **(Read Only)**:
> The default values associated with this attribute. Dependent on the type of attribute, it may return a float, integer, string, tuple, [Position](Position_Class.html "Position Class"), or [Vector](Vector_Class.html "Vector Class").
## Methods
`destroy()`→ `None`:
> Destroy the attribute referenced by this object.
> 
> ```
> n = scriptOP.pointAttribs['N'].destroy()
> 
> ```
`vals(delayed=False)`→ `list`:
> Returns the attribute values as a list.
> 
> * delayed - (Keyword, Optional) If set to True, the download results will be delayed until the next call to vals(), avoiding stalling the GPU waiting for the result immediately.
### Accessing Attributes[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Accessing Attributes")]
See [Attributes](Attributes_Class.html "Attributes Class") for examples on how to access individual attributes.
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditor2022.241402021.100002018.28070before 2018.28070
Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

Retrieved from "<https://docs.derivative.ca/index.php?title=Attribute_Class&oldid=31417>"
[Categories](Special_Categories.html "Special:Categories"):
* [Pages using duplicate arguments in template calls](https://docs.derivative.ca/index.php?title=Category:Pages_using_duplicate_arguments_in_template_calls&action=edit&redlink=1 "Category:Pages using duplicate arguments in template calls (page does not exist)")
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")