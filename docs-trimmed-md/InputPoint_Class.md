

# InputPoint_Class

InputPoint Class - Derivative




# InputPoint Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
A Input Point is a special case of a [Point](Point_Class.html "Point Class") object, only available in the [Point SOP's](Point_SOP.html "Point SOP") parameters.
The members below are unique to Input Point. See [Point Class](Point_Class.html "Point Class") for other members and more information.
  

## Members
`color` → `[TDU.Color](Color_Class.html "Color Class")` **(Read Only)**:
> The color for this point. This is different from the Cd attribute, since it can come from a Vertex if there is no color on the inputPoint itself.
`normal` → `[TDU.Vector](Vector_Class.html "Vector Class")` **(Read Only)**:
> The normal for this point. This is different from the N attribute, since it can come from a Vertex or from the destination point, if there is no normal on the inputPoint itself.
`sopCenter` → `[TDU.Position](Position_Class.html "Position Class")` **(Read Only)**:
> Get the barycentric coordinate of the geometry the inputPoint is a part of. This is faster than other methods to get the center of a SOP's geometry due to internal optimizations. It is expressed as a tdu.Position.
## Methods
No operator specific methods.
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditor2021.100002018.28070before 2018.28070
Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Retrieved from "<https://docs.derivative.ca/index.php?title=InputPoint_Class&oldid=31599>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")