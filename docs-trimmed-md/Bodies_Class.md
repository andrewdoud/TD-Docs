

Bodies Class - Derivative




# Bodies Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Bodies Class describes the set of all [Bodies](Body_Class.html "Body Class") in an [Actor COMP](Actor_COMP.html "Actor COMP") (Actor COMPs are used by the [Bullet Solver COMP](Bullet_Solver_COMP.html "Bullet Solver COMP") and [Nvidia Flex Solver COMP](Nvidia_Flex_Solver_COMP.html "Nvidia Flex Solver COMP")). The Bodies object is accessed via its Actor COMP and is used much like a Python list.
```
bodies = op('bsolver1/actor1').bodies	# get the Bodies object
print(len(bodies))						# number of Bodies 
print(bodies[0])						# first Body in the list
for b in bodies:
	print(b)							# print all Bodies
```
  

## Members
No operator specific members.
  

## Methods
No operator specific methods.
  
TouchDesigner Build: Latest\n2022.241402021.100002019.146502018.28070
An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

Retrieved from "<https://docs.derivative.ca/index.php?title=Bodies_Class&oldid=26970>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")