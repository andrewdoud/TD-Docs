

# ParGroup_Class

ParGroup Class - Derivative




# ParGroup Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The ParGroup class describes an instance of a single ParGroup.
See also [Custom Parameters](Custom_Parameters.html "Custom Parameters").
  

## Members
`bindExpr` → `tuple[str, ...]` :
> Get or set expressions that return a Parameter object. This can be used to bind this parameter's constant values to the referenced parameters.
> 
> Example:
> 
> ```
> p.bindExpr = ("op('geo1').par.tx", "op('geo1').par.ty", "op('geo1').par.tz")
> 
> ```
> 
> Note the outside quotes, as bindExpr is an expression, not an object.
`bindMaster` → `tuple` **(Read Only)**:
> The objects to which this parameter is bound to, possibly None.
`bindRange` → `bool` :
> Get or set parameter's range binding state. If True, min, max, clampMin, clampMax, normMin, normMax, normVal values will be based on master bind parameter. Can only be set on Custom Parameters.
`bindReferences` → `tuple` **(Read Only)**:
> The (possibly empty) lists of objects which bind to this parameter.
`clampMax` → `tuple[float, ...]` :
> Get or set the parameter's numerical clamping behaviors. If set to `clampMax = True`, the parameter will clamp on the upper end at the value specified in max Can only be set on Custom Parameters.
`clampMin` → `tuple[bool, ...]` :
> Get or set the parameter's numerical clamping behaviors. If set to `clampMin = True`, the parameter will clamp on the lower end at the value specified in min Can only be set on Custom Parameters.
`collapsable` → `bool` **(Read Only)**:
> Returns True if the parameter is collapsable.
`collapser` → `bool` **(Read Only)**:
> Returns True if the parameter is a parent of collapsable parameters (ie. a collapser).
`default` → `tuple` :
> Get or set the parameter's default values. Can only be set on Custom Parameters.
`defaultExpr` → `tuple[str, ...]` :
> Get or set the parameter's default expressions. Can only be set on Custom Parameters.
> 
> ```
> # value defaults to this expression.
> op('base1').parGroup.Size.defaultExpr = ('me.time.frame', 'me.time.frame', 'me.time.frame')
> 
> ```
`defaultBindExpr` → `tuple[str, ...]` :
> Get or set the parameter's default bind expressions. Can only be set on Custom Parameters.
> 
> ```
> # value defaults to this expression.
> op('base1').parGroup.Size.defaultBindExpr = ('me.par.tx', 'me.par.ty', 'me.par.tz')
> 
> ```
`defaultMode` → `tuple[ParMode, ...]` :
> Get or set the parameter's evaluation modes.
> 
> ```
> op('geo1').parGroup.t.defaultMode = (ParMode.EXPRESSION, ParMode.EXPRESSION, ParMode.EXPRESSION)
> 
> ```
> 
> The modes are one of: ParMode.CONSTANT, ParMode.EXPRESSION, or ParMode.EXPORT, or ParMode.BIND.
> 
> See [Parameter\_Dialog#Working\_with\_Parameter\_Modes](Parameter_Dialog.html#Working_with_Parameter_Modes "Parameter Dialog") for more information.
`enable` → `bool` :
> Get or set the parameter's enable state. Can only be set on Custom Parameters.
`enableExpr` → `str` :
> Get or set an expression that controls the enable state for this parameter group.
> 
> ```
> p.enableExpr = "me.par.X.menuIndex == 5"
> 
> ```
> 
> Note the outside quotes, as this is an expression, not an object.
`exportOP` → `tuple[OP | None, ...]` **(Read Only)**:
> The operators exporting to this parameter.
`exportSource` → `tuple[Cell | Channel | None, ...]` **(Read Only)**:
> tuple of objects exporting to this parameter. Examples: Cell, Channel or None.
`expr` → `tuple[str, ...]` :
> Get or set the non-evaluated expressions only. To get the parameter's current values, regardless of the Parameter Mode (constant, expression, export or bound), use the eval() method described below.
> 
> ```
> op('geo1').parGroup.t.expr = ('absTime.frame', 'absTime.frame', 'absTime.frame')  
> # set to match current frame
> 
> ```
> 
> When setting this member, the parameter will also be placed in expression mode. See mode member below.
> 
> **NOTE:** For convenience, the expression is placed in double-quotes so you can safely put in expressions containing single quotes. 'a' and "a" have the same effect of enclosing strings in python.
`help` → `str` :
> Get or set a custom parameter's help text. To see any parameter's help, rollover the parameter while holding the Alt key.
`isDefault` → `bool` **(Read Only)**:
> True when the parameter value, expression and mode are in their default settings.
`isCustom` → `bool` **(Read Only)**:
> True for Custom Parameters.
`isFloat` → `bool` **(Read Only)**:
> True for floating point numeric parameters.
`isInt` → `bool` **(Read Only)**:
> True for integer numeric parameters.
`isMenu` → `bool` **(Read Only)**:
> True for menu parameters.
`isMomentary` → `bool` **(Read Only)**:
> True for momentary parameters.
`isNumber` → `bool` **(Read Only)**:
> True for numeric parameters.
`isOP` → `bool` **(Read Only)**:
> True for OP parameters.
`isPulse` → `bool` **(Read Only)**:
> True for pulse parameters.
`isPython` → `bool` **(Read Only)**:
> True for python parameters.
`isSequence` → `bool` **(Read Only)**:
> True for sequence header parameters.
`isString` → `bool` **(Read Only)**:
> True for string parameters.
`isToggle` → `bool` **(Read Only)**:
> True for toggle parameters.
`label` → `str` :
> Get or set the parameter's label.
> 
> ```
> op('myOperator').parGroup.Custompar.label = 'Translate'
> 
> ```
> 
> Can only be set on Custom Parameters.
`max` → `tuple[float, ...]` :
> Get or set the parameter's numerical maximum values. The parameter's values will be clamped at that maximum if `clampMax = True`. Can only be set on Custom Parameters.
`menuIndex` → `tuple[int, ...]` :
> Get or set a tuple of menu constant values by their indices.
`menuLabels` → `tuple[list[str], ...]` :
> Get or set a tuple of lists of all possible menu choice labels. In the case of non menu parameters, None(s) are returned. Can only be set on Custom Parameters.
`menuNames` → `tuple[list[str], ...]` :
> Get or set a tuple of lists of all possible menu choice names. In the case of non menu parameters, None(s) are returned. Can only be set on Custom Parameters.
`menuSource` → `tuple[str, ...]` :
> Get or set a tuple of expressions that returns objects with `.menuItems` `.menuNames` members. This can be used to create a custom menu whose entries dynamically follow that of another menu for example.
`min` → `tuple[float, ...]` :
> Get or set the parameter's numerical minimum values. The parameter's values will be clamped at that minimum if `clampMin = True` for the particular Par. Can only be set on Custom Parameters.
`mode` → `tuple[ParMode, ...]` :
> Get or set the parameter's evaluation modes.
> 
> ```
> op('geo1').parGroup.t.mode = (ParMode.EXPRESSION, ParMode.EXPRESSION, ParMode.EXPRESSION)
> 
> ```
> 
> The modes are one of: `ParMode.CONSTANT`, `ParMode.EXPRESSION`, or `ParMode.EXPORT`, or `ParMode.BIND`.
> 
> See [Parameter\_Dialog#Working\_with\_Parameter\_Modes](Parameter_Dialog.html#Working_with_Parameter_Modes "Parameter Dialog") for more information.
`name` → `str` :
> Get or set the parameter's unique name.
> 
> ```
> op('myOperator').parGroup.Custompar.name = 'Translate'
> 
> ```
> 
> Can only be set on Custom Parameters.
`baseName` → `str` :
> Get or set the parameter's base name. This excludes any sequence prefixes, sequence indices or name suffixes. Can only be set on Custom Parameters.
`normMax` → `tuple[float, ...]` :
> Get or set the parameter's maximum slider values if the parameter is a numerical slider. Can only be set on Custom Parameters.
`normMin` → `tuple[float, ...]` :
> Get or set the parameter's minimum slider values if the parameter is a numerical slider. Can only be set on Custom Parameters.
`normVal` → `tuple[float, ...]` :
> Get or set the parameter's values as a normalized slider position. Can only be set on Custom Parameters.
`order` → `int` :
> Get or set the parameter's position on the parameter page. Can only be set on Custom Parameters.
`owner` → `OP` **(Read Only)**:
> The OP to which this object belongs.
`page` → `Page` :
> Get or set the parameter page the custom parameter is part of. Can only be set on Custom Parameters.
`password` → `bool` :
> Get or set the parameter's password mode. When True all text is rendered as asterisks. Can only be set on Custom string, int or float parameters. Custom Parameters.
`prevMode` → `tuple` **(Read Only)**:
> The parameter's previous evaluation modes.
`readOnly` → `bool` :
> Get or set the parameter's read only status. When True the parameter cannot be modified through the UI, only scripting.
`startSection` → `bool` :
> Get or set the parameter's separator status. When True a visible separator is drawn between this parameter and the ones preceding it. Can only be set on Custom Parameters.
`style` → `str` **(Read Only)**:
> Describes the behavior and contents of the custom parameter. Example 'Float', 'Int', 'Pulse', 'XYZ', etc.
`subLabel` → `tuple` **(Read Only)**:
> Returns the names of the sub-label.
`val` → `tuple` :
> Get or set the constant values of the parameter only. To get the parameter's current values, regardless of the Parameter Modes (`constant`, `expression`, `export` or `bound`), use the eval() method described below.
> 
> ```
> op('geo1').parGroup.t.val   # the constant values 
> op('geo1').parGroup.t.eval()   # the evaluated parameter
> op('geo1').parGroup.t.val = (1,2,3)
> op('geo1').parGroup.t = (1,2,3)  #equivalent to above, more concise form
> 
> ```
> 
> When setting this member, the parameter will also be placed in constant mode. See mode member below.
> 
> To set a menu value by its index, use the menuIndex member as described below.
`valid` → `bool` **(Read Only)**:
> True if the referenced parameter currently exists, False if it has been deleted.
`index` → `int` **(Read Only)**:
> The parameter's order in the list.
`sequence` → `Sequence | None` **(Read Only)**:
> The [Sequence](Sequence_Class.html "Sequence Class") this parGroup is a part of. None if not in a sequence.
`sequenceBlock` → `SequenceBlock | None` **(Read Only)**:
> The [SequenceBlock](SequenceBlock_Class.html "SequenceBlock Class") this parGroup belongs to. None if not in a sequence.
`blockIndex` → `int` **(Read Only)**:
> The index of the parGroup within its [SequenceBlock](SequenceBlock_Class.html "SequenceBlock Class"). None if not in a sequence.
`sequenceIndex` → `int` **(Read Only)**:
> The index of the parGroup's [SequenceBlock](SequenceBlock_Class.html "SequenceBlock Class") in its [Sequence](Sequence_Class.html "Sequence Class"). None if not in a sequence.
`size` → `int` :
> Get or set the parameter's vector size.
## Methods
`copy(ParGroup)`→ `None`:
> Copy the specified parameter.
> 
> * ParGroup - The parameter to copy.
> 
> ```
> op('geo1').parGroup.t.copy( op('geo2').parGroup.t )
> 
> ```
`destroy()`→ `None`:
> Destroy the parameter referenced by this ParGroup. An exception will be raised if the parameter has already been destroyed. Only custom and sequential parameters can be destroyed. Destroying a sequential parameter will destroy its entire block. Note: When any parameter is destroyed, any existing parameter objects will be invalid and should be re-fetched.
`eval()`→ `tuple`:
> Evaluate a parameter group. This value may be derived by the parameter group's constant value, expression, or export, dependent on its mode.
> 
> ```
> a = op('geo1').parGroup.t.eval()
> 
> ```
`evalExport()`→ `tuple`:
> Evaluate the export portions of a parameter, if it contains any. This will ignore any expressions, etc.
> 
> ```
> a = op('geo1').parGroup.t.evalExport()
> 
> ```
`evalExpression()`→ `tuple`:
> Evaluate the expression portions of a parameter, if it contains any. This will ignore any exports, etc.
> 
> ```
> a = op('geo1').parGroup.t.evalExpression()
> 
> ```
> 
> To evaluate an arbitrary expression string, that is not inside a parameter, see [OP.evalExpression](OP_Class.html#evalExpression "OP Class").
`evalNorm()`→ `tuple[float, ...[`:
> Similar to eval() but the returns the normalized slider values.
`evalOPs()`→ `tuple[list[op], ...]`:
> Evaluate each parameter as a series of operators. This is useful for a custom parameter that specifies a list of operator paths for example.
> 
> ```
> a = op('base1').parGroup.Paths.evalOPs()
> 
> ```
`pars(pattern)`→ `list`:
> Returns a (possibly empty) list of parameter objects that match the pattern.
> 
> * pattern - Is a string following the Pattern Matching rules, specifying which parameters to return.
> 
> ```
> # translate parameters
> newlist = op('geo1').parGroup.t.pars('t?')
> 
> ```
`reset()`→ `bool`:
> Resets the parameter group to its default state.
> 
> Returns true if anything was changed.
> 
> ```
> op('geo1').parGroup.t.reset()
> 
> ```
`isSameParGroup(parGroup : ParGroup)`→ `bool`:
> True if the provided parGroup is the same ParGroup on the same operator. Because `op('container1').parGroup.x == op('container2').parGroup.x` compares values and `op('container1').parGroup.x is op('container1').parGroup.x` is always False (because of TouchDesigner internals), you must use `isSameParGroup` to compare ParGroup objects.
> 
> * parGroup - The ParGroup to compare identity with.
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditormw-rollbackmw-revertedmw-revertedmw-revertedmw-reverted2023.112802022.24140before 2022.24140
A ParGroup is a group of related parameters that you can set and get as a whole instead of its individual parameters.

Every Parameter can be in one of four modes: Constant Mode, [Expression](Expression.html "Expression") Mode, [Export](Export.html "Export") Mode or Bind ([Binding](Binding.html "Binding")) Mode.

Absolute Time starts counting from 0 when the TouchDesigner process starts, and is always increasing. It will pause if the Power 0/1 button at the top of the UI is Off.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

Matching names using wildcard characters and bracketing. Useful in "[Select](Select_CHOP.html "Select CHOP")" type parameters to select multiple operators, paths, channels, etc.

Retrieved from "<https://docs.derivative.ca/index.php?title=ParGroup_Class&oldid=32164>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")