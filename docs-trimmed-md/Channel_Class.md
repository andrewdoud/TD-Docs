

Channel Class - Derivative

























# Channel Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

A Channel object describes a single [channel](Channel.html "Channel") from a [CHOP](CHOP.html "CHOP"). The [CHOP Class](CHOP_Class.html "CHOP Class") provides many ways of accessing its individual channels.
See [Working with CHOPs in Python](https://docs.derivative.ca/Working_with_CHOPs_in_Python "Working with CHOPs in Python") for more examples of how to use this class.

  


## Members

`valid` → `bool` **(Read Only)**:

> True if the referenced chanel value currently exists, False if it has been deleted.

`index` → `int` **(Read Only)**:

> The numeric index of the channel.

`name` → `str` **(Read Only)**:

> The name of the channel.

`owner` → `OP` **(Read Only)**:

> The [OP](OP_Class.html "OP Class") to which this object belongs.

`exports` → `list` **(Read Only)**:

> The (possibly empty) list of [parameters](Par_Class.html "Par Class") this channel currently exports to.

`vals` → `list` :

> Get or set the full list of Channel values. Modifying Channel values can only be done in Python within a [Script CHOP](https://docs.derivative.ca/ScriptCHOP_Class "ScriptCHOP Class").

## Methods

`[index]`→ `float`:

> Sample values may be easily accessed from a Channel using the [] subscript operator.
> 
> * index - Must be an numeric sample index. Wildcards are not supported.
> 
> To get the third sample from the channel, assuming the channel has 3 or more samples:
> 
> ```
> n = op('pattern1')
> c = n['chan1'][2] # the third sample
> l = len(n['chan2']) # the total number of samples in the channel
> 
> ```

`eval(index)`→ `float`:

> Evaluate the channel at the specified index sample index. If no index is given, the current index based on the current time is used.
> 
> * index - (Optional) The sample index to evaluate at.

`evalFrame(frame)`→ `float`:

> Evaluate the channel at the specified frame. If no frame is given, the current frame is used.
> 
> * frame - (Optional) The frame to evaluate at.

`evalSeconds(secs)`→ `float`:

> Evaluate the channel at the specified seconds. If no time is given, the current time is used.
> 
> * secs - (Optional) The time in seconds to evaluate at.

`numpyArray()`→ `numpy.ndarray`:

> Returns this channels data as a NumPy array with a length equal to the track length.

`destroy()`→ `None`:

> Destroy and remove the actual Channel this object refers to. This operation is only valid when the channel belongs to a  [Script CHOP](https://docs.derivative.ca/ScriptCHOP_Class "ScriptCHOP Class") or [OSC In CHOP](https://docs.derivative.ca/OscinCHOP_Class "OscinCHOP Class") .
> Note: after this call, other existing Channel objects in this CHOP may no longer be valid.

`average()`→ `float`:

> Returns the average value of all the channel samples.

`min()`→ `float`:

> Returns the minimum value of all the channel samples.

`max()`→ `float`:

> Returns the maximum value of all the channel samples.

`copyNumpyArray(numpyArray)`→ `None`:

> Copies the contents of the numpyArray into the Channel sample values.
> 
> * numpyArray - The NumPy Array to copy. Must be shape(n), where n is the sample length of the CHOP. The data type must be float32. Modifying Channel values can only be done in Python within a [Script CHOP](Script_CHOP.html "Script CHOP").

### Casting to a Value[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Casting to a Value")]

The Channel Class implements all necessary methods to be treated as a number, which in this case evaluates its current value. Therefore, an explicit call to eval() is unnecessary when used in a parameter, or in a numeric expression.

For example, the following are equivalent in a channel:

```
(float)n['chan1']
n['chan1'].eval()

```

The following are also equivalent, because the + 1 will implicitly cast the channel to a number:

```
n['chan1'].eval() + 1
n['chan1'] + 1

```

TouchDesigner Build: Latest\nwikieditor2022.241402021.100002018.28070before 2018.28070

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.







Retrieved from "<https://docs.derivative.ca/index.php?title=Channel_Class&oldid=31665>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")