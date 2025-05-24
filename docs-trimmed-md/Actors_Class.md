

Actors Class - Derivative

























# Actors Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

The Actors Class describes the set of all [Actor COMPs](Actor_COMP.html "Actor COMP") used by the [Bullet Solver COMP](Bullet_Solver_COMP.html "Bullet Solver COMP") and [Nvidia Flex Solver COMP](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP"). It can be accessed with a Bullet Solver COMP. It can be accessed much like a Python list.

```
actors = op('bsolver1').actors	# get the Actors object
print(len(actors))				# number of Actors 
print(actors[0])				# first Actor component in the list
for a in actors:
	print(a)					# print all Actors

```

  


## Members

No operator specific members.

  


## Methods

No operator specific methods.

  

TouchDesigner Build: Latest\n2022.241402021.100002019.146502018.28070

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").







Retrieved from "<https://docs.derivative.ca/index.php?title=Actors_Class&oldid=26964>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")