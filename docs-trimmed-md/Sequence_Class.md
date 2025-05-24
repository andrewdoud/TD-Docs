

Sequence Class - Derivative




# Sequence Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
An object describing and controlling a set of [sequential parameters](Sequential_Parameters.html "Sequential Parameters"). Accessed via
* the `sequence` member of [parameters](Par_Class.html "Par Class")
* `OP.seq` [Sequence Collection](SequenceCollection_Class.html "SequenceCollection Class") - the set of sequences of an object.
* `me.curSeq` in a parameter expression
```
mySequence = op('/add1').par.point0weight.sequence	# get the sequence object
alsoMySequence = op('/add1').seq.point				# another way to get the sequence object
# A sequence block is a SequenceBlock object, which gives access to one set of parameters in the sequence.
print(len(seq))									# number of sequence blocks in the sequence
print(seq[0])									# first sequence block in the sequence
for parBlock in seq:
	print([par for par in parBlock])			# print all sequence blocks
seq.numBlocks += 1							    # add a new sequence block (same as pressing + in the UI)
# Example 2
# Examine siblings of a constant CHOP sequence
n = op('/project1/constant1')
p = n.par.const2name
p.sequenceBlock.par.name  # const2name
p.sequenceBlock.par.value  # const2value
```
See also: [Sequential Parameters](Sequential_Parameters.html "Sequential Parameters"), [SequenceBlock Class](SequenceBlock_Class.html "SequenceBlock Class"), [SequenceCollection Class](SequenceCollection_Class.html "SequenceCollection Class")
  

  

## Members
`blockSize` → `int` :
> Get or set the sequence blocksize, which is the number of [ParGroups](ParGroup.html "ParGroup") in the block.
`blocks` → `list[SequenceBlock]` **(Read Only)**:
> The set of all blocks in this sequence. A block is a set of parameters which can be repeated in an operator. See [SequenceBlock](SequenceBlock_Class.html "SequenceBlock Class") class.
`maxBlocks` → `int | None` **(Read Only)**:
> The maximum number of blocks allowed in the sequence, or None if limitless.
`name` → `str` :
> Get or set the sequence name, which affects all its parameter names.
`numBlocks` → `int` :
> Get or set the total number of parameter blocks in this sequence.
`owner` → `OP` **(Read Only)**:
> The OP to which this object belongs.
`blockPars` → `list` **(Read Only)**:
> An intermediate parameter collection object, from which specific sequence parameters can be found.
> 
> Returns a list of one parameter from each block.
> 
> ```
> n.seq.Info.blockPars.Tx
> n.seq.Info.blockPars.Tx[3] #Par from 4th block.
> 
> ```
> 
> ```
> n.seq.Info.blockPars['Tx'] #returns None if not found.
> 
> ```
`blockParGroups` → `list` **(Read Only)**:
> An intermediate parGroup collection object, from which specific sequence parameter groups can be found.
> 
> Returns a list of one parGroup from each block.
> 
> ```
> n.seq.Info.blockParGroups.T
> n.seq.Info.blockParGroups.T[3] #ParGroup from 4th block.
> 
> ```
> 
> ```
> n.seq.Info.blockParGroups['T'] #returns None if not found.
> 
> ```
`sequencePar` → `Par` **(Read Only)**:
> The main sequence parameter defining this sequence.
## Methods
`[block index]`→ `SequenceBlock`:
> [Sequence blocks](SequenceBlock_Class.html "SequenceBlock Class") may be easily accessed using the `[]` subscript and assignment operators.
> 
> * block index - The index of the desired block.
`destroyBlock(block)`→ `None`:
> Destroy the block of parameters at the given location.
> 
> * block - The index of the existing block to destroy.
`insertBlock(block)`→ `SequenceBlock`:
> Insert a block of parameters at the given location.
> 
> * block - The index of the new block to insert.
> 
> Returns the newly created block.
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditormw-replace2023.112802021.100002020.20000before 2020.20000
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

A ParGroup is a group of related parameters that you can set and get as a whole instead of its individual parameters.

Retrieved from "<https://docs.derivative.ca/index.php?title=Sequence_Class&oldid=32907>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")