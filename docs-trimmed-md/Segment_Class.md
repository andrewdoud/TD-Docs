

Segment Class - Derivative




# Segment Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
A Segment object describes a single segment from a Timer CHOP.
  

## Members
`beginFrames` → `int` **(Read Only)**:
> The beginning point of the segment expressed in frames.
`beginSamples` → `int` **(Read Only)**:
> The beginning point of the segment expressed in samples.
`beginSeconds` → `float` **(Read Only)**:
> The beginning point of the segment expressed in seconds.
`custom` → `dict` **(Read Only)**:
> dictionary of all the extra column values associated with the segment.
`cycle` → `bool` **(Read Only)**:
> Whether or not the segment will repeat itself.
`cycleEndAlertFrames` → `int` **(Read Only)**:
> The amount of time before cycling the callback will be executed, expressed in frames.
`cycleEndAlertSamples` → `int` **(Read Only)**:
> The amount of time before cycling the callback will be executed, expressed in samples.
`cycleEndAlertSeconds` → `float` **(Read Only)**:
> The amount of time before cycling the callback will be executed, expressed in seconds.
`cycleLimit` → `bool` **(Read Only)**:
> Whether or not the segment will repeat itself indefinitely.
`delayFrames` → `int` **(Read Only)**:
> The delay portion of the segment expressed in frames.
`delaySamples` → `int` **(Read Only)**:
> The delay portion of the segment expressed in samples.
`delaySeconds` → `float` **(Read Only)**:
> The delay portion of the segment expressed in seconds.
`lengthFrames` → `int` **(Read Only)**:
> The length portion of the segment expressed in frames.
`lengthSamples` → `int` **(Read Only)**:
> The length portion of the segment expressed in samples.
`lengthSeconds` → `float` **(Read Only)**:
> The length portion of the segment expressed in seconds.
`maxCycles` → `int` **(Read Only)**:
> The maximum number of repetitions.
`owner` → `OP` **(Read Only)**:
> The OP to which this object belongs.
`row` → `int` **(Read Only)**:
> Named tuple of all the parameter or column values describing the segment.
`speed` → `float` **(Read Only)**:
> The speed multiplier of the segment.
`index` → `int` **(Read Only)**:
> The numeric index of this segment.
## Methods
No operator specific methods.
TouchDesigner Build: Latest\nwikieditor2022.24140
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=Segment_Class&oldid=31455>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")