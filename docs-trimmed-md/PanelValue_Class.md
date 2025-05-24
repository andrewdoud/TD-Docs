

PanelValue Class - Derivative




# PanelValue Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
A PanelValue describes an instance to a [Panel Value](Panel_Value.html "Panel Value"). They can be accessed through a component's [panel](Panel.html "Panel") member, and are used in the [Panel Execute DAT](Panel_Execute_DAT.html "Panel Execute DAT").
For a list of available panel values, see: [Panel Value](Panel_Value.html "Panel Value").
  

## Members
`name` → `str` **(Read Only)**:
> The name of the panel value. See [Panel Value](Panel_Value.html "Panel Value") for the list of possible names. name is a string.
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
`val` → `Any` :
> Get or set the panel value.
`valid` → `bool` **(Read Only)**:
> True if the referenced panel value currently exists, False if it has been deleted.
## Methods
No operator specific methods.
### Casting to a Value[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Casting to a Value")]
The PanelValue Class implements all necessary methods to be treated as a number or string, which in this case gets or sets its value. Therefore, an explicit call to eval() or set() is unnecessary when used in a parameter, or in a numeric expression.
For example, the following are equivalent in a parameter:
```
(float)parent().panel.u
parent().panel.u.val
parent().panel.u
# the following are also equivalent
parent().panel.u.val + 1
parent().panel.u + 1
# as are the following
parent().panel.u.val = 0.5
parent().panel.u = 0.5
```
TouchDesigner Build: Latest\nwikieditor2021.100002018.28070before 2018.28070
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=PanelValue_Class&oldid=31437>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")