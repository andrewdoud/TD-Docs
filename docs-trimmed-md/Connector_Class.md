

# Connector_Class

Connector Class - Derivative




# Connector Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Connector class describes the input or output connection point of an [operator](OP_Class.html#Connection "OP Class"). There are two types of connections: those between Components, and those between regular operators.
Connections between regular operators can be accessed through the [OP.inputConnectors](OP_Class.html#Connection "OP Class") and [OP.outputConnectors](OP_Class.html#Connection "OP Class") members. These are the connectors on the left and right sides of [Operators](Operator.html "Operator").
Connections between components can be accessed through the [COMP.inputCOMPConnectors](COMP_Class.html#Connection "COMP Class") and [COMP.outputCOMPConnectors](COMP_Class.html "COMP Class") members. These are the connectors on the top and bottom of [Component](Component.html "Component") operators
  

## Members
`index` → `int` **(Read Only)**:
> The numeric index of this connector.
`isInput` → `bool` **(Read Only)**:
> True when the connector is an input.
`isOutput` → `bool` **(Read Only)**:
> True when the connector is an output.
`inOP` → `OP` **(Read Only)**:
> Will return any input operators (e.g. [inSOP](https://docs.derivative.ca/InSOP_Class "InSOP Class"), [inCHOP](https://docs.derivative.ca/InCHOP_Class "InCHOP Class")) associated with this connector. This only applies to regular operator connections attached to components.
`outOP` → `OP` **(Read Only)**:
> Will return any output operators (e.g. [outSOP](https://docs.derivative.ca/OutSOP_Class "OutSOP Class"), [outCHOP](https://docs.derivative.ca/OutCHOP_Class "OutCHOP Class")) associated with this connector. This only applies to regular operator connections attached to components.
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
`connections` → `list` **(Read Only)**:
> The list of connector objects connected to this object.
`description` → `str` **(Read Only)**:
> A description for this connection. Example: 'Color Image'.
## Methods
`connect(target)`→ `None`:
> Wire this connector to a target location. The target may be an [operator](OP_Class.html "OP Class") or another connector.
> 
> When the connector is an input, its connection is replaced with the target.
> When the connector is an output, a new connection is appended to the target.
> 
> * target - The OP or connector you want to connect to.
> 
> ```
> # connect noise1 to lag1
> op('noise1').outputConnectors[0].connect(op('lag1'))
> 
> # connect choptotop1 to 2nd input of displace1
> op('choptotop1').outputConnectors[0].connect(op('displace1').inputConnectors[1])
> 
> # connect geo1 to geo2, two equivalent methods:
> op('geo1').outputCOMPConnectors[0].connect(op('geo2'))
> op('geo2').inputCOMPConnectors[0].connect(op('geo1'))
> 
> ```
`disconnect()`→ `None`:
> Disconnect this connector.
> 
> ```
> op('lag1').inputConnectors[0].disconnect()
> op('lag1').outputConnectors[0].disconnect()
> 
> # disconnect geo2 from geo1, two equivalent methods
> op('geo1').outputCOMPConnectors[0].disconnect()
> op('geo2').inputCOMPConnectors[0].disconnect()
> 
> ```
TouchDesigner Build: Latest\n2022.241402021.100002018.28070before 2018.28070
The notches on the left and right of each [Node](Node.html "Node") that let you [Wire](Wire.html "Wire") the output of one [Operator](Operator.html "Operator") to the input of another of the same [Operator Family](Operator.html "Operator"). The notches on the top and bottom of [3D Object Components](Object.html "Object") and [Panel Components](Panel_Component.html "Panel Component") that tie the components of each sub-[Family](Operator_Family.html "Operator Family") in a [Hierarchy](Hierarchy.html "Hierarchy").

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

The connection of an output of one node to the input of another node in a network. In contrast, see [Link](Link.html "Link").

Retrieved from "<https://docs.derivative.ca/index.php?title=Connector_Class&oldid=26687>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")