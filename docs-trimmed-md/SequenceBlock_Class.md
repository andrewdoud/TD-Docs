

SequenceBlock Class - Derivative




# SequenceBlock Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The SequenceBlock class can be used to access the parGroups of a specific block (set of parGroups) in a sequence.
```
block = op('/add1').seq.point[3] # get the fourth block from the sequence named "iop"
print([parGroup for parGroup in block]) # print all the parGroups in the block
```
**Note:** use the parameter name *without* the sequence prefix.
  

## Members
`index` → `int` **(Read Only)**:
> The numeric index of the block.
`owner` → `OP` **(Read Only)**:
> The OP to which this object belongs.
`par` → `ParCollection` **(Read Only)**:
> An intermediate parameter collection object, from which a specific sequence parameter can be found.
> 
> Names do not include sequence info prefix.
> 
> ```
> n.seq.Info.blocks[2].par.Tx # raises exception if not found
> 
> ```
> 
> ```
> n.seq.Info.blocks[2].parGroup['Tx'] #returns None if not found
> 
> ```
`parGroup` → `ParGroupCollection` **(Read Only)**:
> An intermediate parameter collection object, from which a specific sequence parameter group can be found.
> 
> Names do not include sequence info prefix.
> 
> ```
> n.seq.Info.blocks[2].par.T # raises exception if not found
> 
> ```
> 
> ```
> n.seq.Info.blocks[2].parGroup['T'] #returns None if not found
> 
> ```
`sequence` → `Sequence` **(Read Only)**:
> The sequence object this block belongs to.
## Methods
No operator specific methods.
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditor2023.11280
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=SequenceBlock_Class&oldid=31440>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")