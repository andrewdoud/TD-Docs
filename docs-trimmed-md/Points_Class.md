

# Points_Class

Points Class - Derivative




# Points Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Points class describes the set of [point objects](Point_Class.html "Point Class") owned by one [SOP](SOP_Class.html "SOP Class").
  

## Members
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
## Methods
No operator specific methods.
### Special Functions[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Special Functions")]
`len(Points)`→ `int`:
> Returns the total number of points.
> 
> ```
> a = len(op('box1').points)
> 
> ```
`[index]`→ `td.Point`:
> Get a specific point given an integer index.
> 
> ```
> n = op('box1').points[0]
> 
> ```
`Iterator`→ `td.Point`:
> Iterate over each point.
> 
> ```
> for m in op('box1').points:
> 	# do something with m, which is a Point
> 
> ```
  
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

Retrieved from "<https://docs.derivative.ca/index.php?title=Points_Class&oldid=12133>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")