

ListAttributes Class - Derivative




# ListAttributes Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The ListAttributes class describes a set of [list attribute objects](ListAttribute_Class.html "ListAttribute Class") for cells, rows, columns or table. It can be accessed from a [List Component](ListCOMP_Class.html "ListCOMP Class").
Access to individual List Attributes depends on what type: row, col, or cell:
```
rowAttribs = op('list1').rowAttribs		# get the ListAttributes object for rows
print(len(rowAttribs))					# number of rows 
print(rowAttribs[0].bgColor)			# rows are accessed by row #. 
										# This prints the background color settings for the first row
colAttribs = op('list1').colAttribs		# get the ListAttributes object for columns
print(len(colAttribs))					# number of columns 
print(colAttribs[0].bgColor)			# cols are accessed by column #. 
										# This prints the background color settings for the first column
cellAttribs = op('list1').cellAttribs	# get the ListAttributes object for columns
print(len(cellAttribs))					# total number of cells 
print(colAttribs[0,2].bgColor)			# cells are accessed by [row, col]. 
										# This prints the background color settings for the cell in the first row, third column
```
**Note:** The attributes above are the settings for List Component's hierarchical layout technique. This means that cell settings
override row settings, which override column settings, which override table settings. If you want to know the final value in a
given cell, use `listCOMP.displayAttribs[row, col]`.
  

## Members
No operator specific members.
  

## Methods
No operator specific methods.
  
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
Information associated with [SOP](SOP.html "SOP") geometry. [Points](Point.html "Point") and [primitives](Primitive.html "Primitive") (polygons, NURBS, etc.) can have any number of attributes - position (P) is standard, and built-in optional attributes are [normals](Normals.html "Normals") (N), texture coordinates (uv), color (Cd), etc.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

Retrieved from "<https://docs.derivative.ca/index.php?title=ListAttributes_Class&oldid=26981>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")