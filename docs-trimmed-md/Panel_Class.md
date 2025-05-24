

Panel Class - Derivative

























# Panel Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

The Panel class manages Panel Components, and is used to access the state of a panel via its [Panel Value Class](PanelValue_Class.html "PanelValue Class").

For a list of available panel values, see: [Panel Value](Panel_Value.html "Panel Value").

  


## Members

`owner` → `OP` **(Read Only)**:

> The [OP](OP_Class.html "OP Class") to which this object belongs.
> 
> In addition to the above, this object contains a member for each panel value in the component.
> 
> ```
> a = op('button1').panel.u
> 
> ```

## Methods

No operator specific methods.

  

TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").







Retrieved from "<https://docs.derivative.ca/index.php?title=Panel_Class&oldid=21904>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")