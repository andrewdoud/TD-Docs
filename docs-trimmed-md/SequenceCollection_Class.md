

# SequenceCollection_Class

SequenceCollection Class - Derivative




# SequenceCollection Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The SequenceCollection class can be used to access sequences by name.
```
	myOperator.seq.Color #raises Exception if not found.
	# or
	myOperator.seq['Color'] #returns None if not found.
```
  

## Members
`owner` → `OP` **(Read Only)**:
> The OP to which this object belongs.
## Methods
No operator specific methods.
  
TouchDesigner Build: Latest\nwikieditorwikieditor2023.11280
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=SequenceCollection_Class&oldid=30808>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")