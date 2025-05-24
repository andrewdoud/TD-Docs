

Par Class - Derivative




# Par Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Par class describes an instance of a single [Parameter](Parameter.html "Parameter"). See also [Custom Parameters](Custom_Parameters.html "Custom Parameters").
  

## Contents
* [1 Members](#Members)
  + [1.1 Type Members](#Type_Members)
  + [1.2 Menu Parameters](#Menu_Parameters)
* [2 Methods](#Methods)
  + [2.1 Casting to a Value](#Casting_to_a_Value)
## Members
`val` → `Any` :
> Get or set the **constant mode value** of the parameter only. **Important:** To get the parameter's current working value, regardless of the [Parameter Mode](Parameter_Mode.html "Parameter Mode") (constant, expression, export or bound), always use the `eval()` method described [below](Par_Class.html#Methods "Par Class").
> 
> ```
> op('geo1').par.tx.val   # the constant value 
> op('geo1').par.tx.eval()   # the evaluated parameter
> op('geo1').par.tx.val = 5
> op('geo1').par.tx = 5  # equivalent to above, more concise form
> op('parexec1').par.op = [parent(), parent(2)] # you can assign a list of ops to a parameter that allows multiple operators
> 
> ```
> 
> When setting this member, the parameter will also be placed in constant mode. See mode member below.
> 
> To set a menu value by its index, use the `menuIndex` member as described below.
`expr` → `str` :
> Get or set the non-evaluated expression only. To get the parameter's current value, regardless of the [Parameter Mode](Parameter_Mode.html "Parameter Mode") (constant, expression, export or bound), use the `eval()` method described below.
> 
> ```
> op('geo1').par.tx.expr = 'absTime.frame'  #set to match current frame
> 
> ```
> 
> When setting this member, the parameter will also be placed in expression mode. See mode member below.
> 
> **NOTE:** For convenience, the expression is placed in double-quotes so you can safely put in expressions containing single quotes. 'a' and "a" have the same effect of enclosing strings in python.
`enableExpr` → `str` :
> Get or set an expression that controls the enable state for this parameter.
> 
> ```
> p.enableExpr = "me.par.X.menuIndex == 5"
> # Note the outside quotes, as this is an expression, not an object.
> 
> ```
`exportOP` → `OP` **(Read Only)**:
> The [operator](OP_Class.html "OP Class") exporting to this parameter.
`exportSource` → `Channel` **(Read Only)**:
> The object exporting to this parameter. Examples: [Cell](Cell_Class.html "Cell Class"), [Channel](Channel_Class.html "Channel Class") or None.
`bindExpr` → `str` :
> Get or set an expression that returns a bindable object. This can be used to bind this parameter's constant value to the referenced object's value.
> 
> ```
> p.bindExpr = "op('geo1').par.tx"
> 
> ```
> 
> Note the outside quotes, as bindExpr is an expression, not an object.
`bindMaster` → `OP` **(Read Only)**:
> The object to which this parameter is bound to, possibly None.
`bindReferences` → `list` **(Read Only)**:
> The (possibly empty) list of objects which bind to this parameter.
`bindRange` → `bool` :
> Get or set parameter's range binding state. If True, min, max, clampMin, clampMax, normMin, normMax, normVal values will be based on master bind parameter. Can only be set on Custom Parameters.
`hidden` → `bool` **(Read Only)**:
> Get the parameter's hidden status. When True the parameter is considered obsolete or irrelevant and should not be modified. They are not shown in the dialog but only maintained for backward compatibility.
`index` → `int` **(Read Only)**:
> A unique identifier for the parameter. May change in the case of custom parameters.
`vecIndex` → `int` **(Read Only)**:
> The parameter's vector index. For example, `op('geo1').par.tz` would have a value of 2.
`name` → `str` :
> Get or set the parameter's unique name.
> 
> ```
> op('myOperator').par.Custompar.name = 'Translate'
> 
> ```
> 
> Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`label` → `str` :
> Get or set the parameter's label.
> 
> ```
> op('myOperator').par.Custompar.label = 'Translate'
> 
> ```
> 
> Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`subLabel` → `str` **(Read Only)**:
> Returns the name of the sub-label.
`startSection` → `bool` :
> Get or set the parameter's separator status. When `True` a visible separator is drawn between this parameter and the ones preceding it. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`readOnly` → `bool` :
> Get or set the parameter's read only status. When `True` the parameter cannot be modified through the UI, only scripting.
`help` → `str` **(Read Only)**:
> Get or set a custom parameter's help text. To see any parameter's help, rollover the parameter while holding the Alt key. For built-in parameters this can be used to get the parameter's help text.
`parGroup` → `ParGroup` **(Read Only)**:
> The [ParGroup](ParGroup.html "ParGroup") of parameters this parameter belongs to. A ParGroup is a set of parameters sharing one line on a parameter dialog with a common label, example: Translate (x, y, z)..
`min` → `int` :
> Get or set the parameter's numerical minimum value. The parameter's value will be clamped at that minimum if clampMin = True. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`max` → `int` :
> Get or set the parameter's numerical maximum value. The parameter's value will be clamped at that maximum if clampMax = True. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`clampMin` → `bool` :
> Get or set the parameter's numerical clamping behavior. If set to clampMin = True, the parameter will clamp on the lower end at the value specified in min Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`clampMax` → `bool` :
> Get or set the parameter's numerical clamping behavior. If set to clampMax = True, the parameter will clamp on the upper end at the value specified in max Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`default` → `Any` :
> Get or set the parameter's default value. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`defaultBindExpr` → `str` :
> Get or set the parameter's default bind expression. Can only be set on Custom Parameters.
> 
> ```
> op('base1').par.Size.defaultBindExpr = 'me.par.tx'
> 
> ```
`defaultExpr` → `str` :
> Get or set the parameter's default expression. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
> 
> ```
> # value defaults to this expression.
> op('base1').par.Size.defaultExpr = 'me.time.frame'
> 
> ```
`defaultMode` → `ParMode` :
> Get or set the parameter's default evaluation mode.
> 
> ```
> op('geo1').par.tx.defaultMode = ParMode.EXPRESSION
> 
> ```
> 
> The mode is one of: ParMode.CONSTANT, ParMode.EXPRESSION, or ParMode.EXPORT, or ParMode.BIND.
> 
> See [Parameter\_Dialog#Working\_with\_Parameter\_Modes](Parameter_Dialog.html#Working_with_Parameter_Modes "Parameter Dialog") for more information.
`normMin` → `int` :
> Get or set the parameter's minimum slider value if the parameter is a numerical slider. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`normMax` → `int` :
> Get or set the parameter's maximum slider value if the parameter is a numerical slider. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`normVal` → `float` :
> Get or set the parameter's value as a normalized slider position. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`enable` → `bool` :
> Get or set the parameter's enable state. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`order` → `float` :
> Get or set the parameter's position on the parameter page. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`page` → `td.Page` :
> Get or set the parameter page the custom parameter is part of. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`password` → `bool` :
> Get or set the parameter's password mode. When True all text is rendered as asterisks. Can only be set on Custom string, int or float parameters. [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`mode` → `ParMode` :
> Get or set the parameter's evaluation mode.
> 
> ```
> op('geo1').par.tx.mode = ParMode.EXPRESSION
> 
> ```
> 
> The mode is one of: `ParMode.CONSTANT`, `ParMode.EXPRESSION`, or `ParMode.EXPORT`, or `ParMode.BIND`.
> 
> See [Parameter\_Dialog#Working\_with\_Parameter\_Modes](Parameter_Dialog.html#Working_with_Parameter_Modes "Parameter Dialog") for more information.
`prevMode` → `ParMode` **(Read Only)**:
> The parameter's previous evaluation mode.
`menuNames` → `list` :
> Get or set a list of all possible menu choice names. In the case of non menu parameters, None is returned. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`menuLabels` → `list` :
> Get or set a list of all possible menu choice labels. In the case of non menu parameters, None is returned. Can only be set on [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`menuIndex` → `int` :
> Get or set a menu constant value by its index.
`menuSource` → `str` :
> Get or set an expression that returns an object with .menuItems .menuNames members. This can be used to create a custom menu whose entries dynamically follow that of another menu for example. Simple menu sources include another parameter with a menu c, an object created by [tdu.TableMenu](Tdu_Module.html "Tdu Module"), or an object created by [TDFunctions.parMenu](TDFunctions.html "TDFunctions").
> 
> ```
> p.menuSource = "op('audiodevin1').par.device"
> 
> ```
> 
> Note the outside quotes, as menuSource is an expression, not an object.
`valid` → `bool` **(Read Only)**:
> True if the referenced parameter currently exists, False if it has been deleted.
`sequence` → `Sequence | None` **(Read Only)**:
> The [Sequence](Sequence_Class.html "Sequence Class") this parameter belongs to. None if not in a sequence.
`sequenceBlock` → `SequenceBlock | None` **(Read Only)**:
> The [SequenceBlock](SequenceBlock_Class.html "SequenceBlock Class") this parameter belongs to. None if not in a sequence.
`owner` → `OP` **(Read Only)**:
> The [OP](OP_Class.html "OP Class") to which this object belongs.
`styleCloneImmune` → `bool` :
> Get or set the parameter's style clone immunity. When `False`, the parameter definition is matched to any matching master parameter its operator is cloned to. When `True`, it is left unchanged.
`lastScriptChange` → `tuple` **(Read Only)**:
> Return information about when this parameter was last modified by a script. Cleared when the parameter is updated via the UI.
> 
> ```
> python >>> op('/level1').par.invert.lastScriptChange
> SetInfo(dat=type:textDAT path:/text1, function='<module>', line=1, frame=300061, timeStamp=1613150878)
> 
> ```
### Type Members[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Type Members")]
`isDefault` → `bool` **(Read Only)**:
> True when the parameter value, expression and mode are in their default settings.
`isCustom` → `bool` **(Read Only)**:
> True for [Custom Parameters](Custom_Parameters.html "Custom Parameters").
`isPulse` → `bool` **(Read Only)**:
> True for pulse parameters.
`isMomentary` → `bool` **(Read Only)**:
> True for momentary parameters.
`isMenu` → `bool` **(Read Only)**:
> True for menu parameters.
`isNumber` → `bool` **(Read Only)**:
> True for numeric parameters.
`isFloat` → `bool` **(Read Only)**:
> True for floating point numeric parameters.
`isInt` → `bool` **(Read Only)**:
> True for integer numeric parameters.
`isOP` → `bool` **(Read Only)**:
> True for OP parameters.
`isPython` → `bool` **(Read Only)**:
> True for python parameters.
`isSequence` → `bool` **(Read Only)**:
> True for sequence header parameters.
`isString` → `bool` **(Read Only)**:
> True for string parameters.
`isToggle` → `bool` **(Read Only)**:
> True for toggle parameters.
`style` → `str` **(Read Only)**:
> Describes the behavior and contents of the custom parameter. Example `'Float'`, `'Int'`, `'Pulse'`, `'XYZ'`, etc.
`collapser` → `bool` **(Read Only)**:
> Returns True if the parameter is a parent of collapsable parameters (ie. a collapser).
`collapsable` → `bool` **(Read Only)**:
> Returns True if the parameter is collapsable.
### Menu Parameters[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Menu Parameters")]
Menu parameters can be get or set by specifying either the string value of the menu, or its numeric index. For example, the following are equivalent:
```
op('geo1').par.xord = 'trs'
op('geo1').par.xord = 5
```
Alternatively, the menu can be accessed more directly:
```
n = op('geo1')
n.par.xord.menuIndex = 5  #trs
a = n.menuNames[0]  #returns 'srt'
b = n.menuLabels[0] #returns 'Scale Rotate Translate'
```
## Methods
`copy(Par)`→ `None`:
> Copy the specified parameter.
> 
> * Par - The parameter to copy.
> 
> ```
> op('geo1').par.tx.copy( op('geo2').par.tx )
> 
> ```
`eval()`→ `Any`:
> Evaluate a parameter. This value may be derived by the parameter's constant value, expression, export, or bind, dependent on its mode.
> 
> ```
> a = op('geo1').par.tx.eval()
> 
> ```
> 
> Calling `eval` on an OP parameter that can hold multiple OPs will return a single OP if there is only 1 result, a list of OPs if there are more than 1, and None if there are no results.
`evalNorm()`→ `float`:
> Similar to eval() but the returns the normalized slider value.
`evalExpression()`→ `Any`:
> Evaluate the expression portion of a parameter, if it contains one. This will ignore any exports, etc.
> 
> ```
> a = op('geo1').par.tx.evalExpression()
> 
> ```
> 
> **Note**: the results of evalExpression is always the expression's Python return value, which can be slightly different than `Par.eval()`. For example, in parameters that hold an operator, `.eval()` will always return an operator if it exists, even if the expression actually returns a string path. The evalExpression function would return the string path.
> 
> To evaluate an arbitrary expression string, that is not inside a parameter, see [OP](OP_Class.html "OP Class").evalExpression.
`evalExport()`→ `Any`:
> Evaluate the export portion of a parameter, if it contains one. This will ignore any expressions, etc.
> 
> ```
> a = op('geo1').par.tx.evalExport()
> 
> ```
`evalOPs()`→ `List[OP]`:
> Evaluate the parameter as series of operators. This is useful for a custom parameter that specifies a list of operator paths for example.
> 
> ```
> a = op('base1').par.Paths.evalOPs()
> 
> ```
`evalFile()`→ `tdu.FileInfo`:
> Evaluate the parameter as a file path. This returns a [FileInfo](Tdu_Module.html "Tdu Module") object with the full path.
> 
> ```
> a = op('moviefilein1').par.file.evalFile()
> print(a.ext)
> print(a.baseName)
> print(a.exists)
> 
> ```
`pulse(value=1, frames=0, seconds=0)`→ `None`:
> Pulsing sets a parameter to the specific value, cooks the operator, then restores the parameter to its previous value.
> 
> For pulse type parameters no value or time is specified or used.
> 
> * value - (Optional) The value to pulse this parameter with, default is 1.
> * frames - (Optional) Number of frames before restoring the parameter to its original value.
> * seconds - (Optional) Number of seconds before restoring the parameter to its original value.
> 
> ```
> op('moviein1').par.reload.pulse(1) #set the reload toggle, then cook
> op('glsl1').par.loadvariablenames.pulse() #activate the pulse parameter
> op('geo1').par.ty.pulse(2, frames=120) #pulse geometry ty for 120 frames
> op('text1').par.text.pulse('GO!', seconds=3) #pulse text TOP string field, for 3 seconds
> op('noise').par.type.pulse('random', seconds=0.5) #pulse noise meny type for half a second
> 
> ```
`destroy()`→ `None`:
> Destroy the parameter referenced by this Par. An exception will be raised if the parameter has already been destroyed. Only custom and sequential parameters can be destroyed. Destroying a sequential parameter will destroy its entire block. Note: When any parameter is destroyed, any existing parameter objects will be invalid and should be re-fetched.
`reset()`→ `bool`:
> Resets the parameter to its default state.
> 
> Returns true if anything was changed.
> 
> ```
> op('geo1').par.tx.reset()
> 
> ```
`isPar(par : Par)`→ `bool`:
> True if the provided Par is the same parameter on the same operator. Because `op('container1').par.x == op('container2').par.x` compares values and `op('container1').par.x is op('container1').par.x` is always False (because of TouchDesigner internals), you must use `isPar` to compare parameter objects.
> 
> * par - The parameter to compare identity with.
### Casting to a Value[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Casting to a Value")]
The Par Class implements all necessary methods to be treated as a number or string, which in this case gets or sets its value. Therefore, an explicit call to `eval()` or `set()` is unnecessary when used in a parameter, or in a numeric expression.
For example, the following are equivalent in a parameter:
* `(float)me.par.tx`
* `me.par.tx.eval()`
* `me.par.tx`
The following are also equivalent:
* `me.par.tx.eval() + 1`
* `me.par.tx + 1`
As are the following:
* `me.par.tx.val = 3`
* `me.par.tx = 3`
**Note:** However, you can't use functions belonging to the cast object type without evaluating the parameter:
* `me.par.tx.hex() # doesn't work`
* `me.par.tx.eval().hex() # works!`
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditormw-rollback2023.112802022.241402021.100002020.200002018.28070before 2018.28070
Absolute Time starts counting from 0 when the TouchDesigner process starts, and is always increasing. It will pause if the Power 0/1 button at the top of the UI is Off.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").

A ParGroup is a group of related parameters that you can set and get as a whole instead of its individual parameters.

To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

Retrieved from "<https://docs.derivative.ca/index.php?title=Par_Class&oldid=32015>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")