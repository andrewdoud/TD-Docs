

# AttributeData_Class

AttributeData Class - Derivative




# AttributeData Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
An AttributeData contains specific geometric [Attribute](Attribute.html "Attribute") values, associated with a [Prim Class](Prim_Class.html "Prim Class"), [Point Class](Point_Class.html "Point Class"), or [Vertex Class](Vertex_Class.html "Vertex Class"). Each value of the attribute must be of the same type, and can be one of float, string or integer. For example, a point or vertex normal attribute data, consists of 3 float values.
  

## Members
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
`val` → `float | int | str | tuple | [TDU.Position](Position_Class.html "Position Class") | [TDU.Vector](Vector_Class.html "Vector Class")` **(Read Only)**:
> The set of values contained within this object. Dependent on the type of attribute, it may return a float, integer, string, tuple, [Position](Position_Class.html "Position Class"), or [Vector](Vector_Class.html "Vector Class"). For example Normal attribute data is expressed as a [Vector](Vector_Class.html "Vector Class"), while [Position](Position_Class.html "Position Class") attribute data is expressed as a Position.
## Methods
No operator specific methods.
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2022.241402021.100002018.28070before 2018.28070
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=AttributeData_Class&oldid=31418>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")