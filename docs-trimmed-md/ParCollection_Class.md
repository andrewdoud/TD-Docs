

ParCollection Class - Derivative

























# ParCollection Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

The ParCollection class can be used to access [Parameters](Par_Class.html "Par Class"). To access a parameter you need to use its internal name, which you can obtain by hovering your mouse over the parameter name, and looking at the popup that will come up. See also [Par Class](Par_Class.html "Par Class"). An operator's instance of this can be found in `OP.par`.

  


## Members

This object contains a member for each parameter in the component. You can both read the value using:

```
a = op('geo1').par.tx

```

You can also change the value using

```
a = op('geo1').par.tx = 4
a = op('geo1').par.lookat = 'null1'

```

`owner` → `OP` **(Read Only)**:

> The [OP](OP_Class.html "OP Class") to which this object belongs.

## Methods

`[name]`→ `Par`:

> [Parameters](Par_Class.html "Par Class") may be easily accessed using the [] subscript and assignment operators.
> 
> * name - Must be an exact string name. Wildcards are not supported. If not found None is returned.
> 
> ```
> p = op('base1').par['Myfloat5']
> 
> ```

TouchDesigner Build: Latest\n2021.100002020.230602018.28070before 2018.28070

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").







Retrieved from "<https://docs.derivative.ca/index.php?title=ParCollection_Class&oldid=26058>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")