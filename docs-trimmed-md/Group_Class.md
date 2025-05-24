

# Group_Class

Group Class - Derivative




# Group Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
An Group describes groups lists of [Prim Class](Prim_Class.html "Prim Class") or [Point Class](Point_Class.html "Point Class").
A Group can be created with the [Group SOP](Group_SOP.html "Group SOP") or using the `createPointGroup(str)` or `createPrimGroup(str)` methods of the [ScriptSOP Class](https://docs.derivative.ca/ScriptSOP_Class "ScriptSOP Class").
  

## Members
`default` → `tuple` **(Read Only)**:
> The default values associated with this Group. It returns a tuple item of group points.
`name` → `str` :
> Set/gets the group name.
`owner` → `OP` **(Read Only)**:
> Gets the owner of this group.
## Methods
`add(item : [Point](Point_Class.html "Point Class") | [Prim](Prim_Class.html "Prim Class") | int)`→ `None`:
> Adds a point/primitive to this group. The point or primitive to be added can be specified by a point, primitive object or the index of a point or primitive object.
`discard(item : [Point](Point_Class.html "Point Class") | [Prim](Prim_Class.html "Prim Class") | int)`→ `None`:
> Removes a point/primitive from this group. The point or primitive to be removed can be specified by a point, primitive object or the index of a point or primitive object.
`destroy()`→ `None`:
> Destroys the current point/primitive group.
TouchDesigner Build: Latest\nwikieditorwikieditor2021.10000before 2021.10000
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=Group_Class&oldid=31425>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")