

Runs Class - Derivative

























# Runs Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

The Runs class describes the set of all delayed [run objects](Run_Class.html "Run Class"). It can be accessed with the runs object, found in the automatically imported [td module](Td_Module.html "Td Module"). See [Run Command Examples](Run_Command_Examples.html "Run Command Examples") for more info.

```
print(len(runs))	# number of active run objects 
print(runs[0])		# first run object
for r in runs:
	r.kill()		# kill all run objects

```

  


## Members

No operator specific members.

  


## Methods

No operator specific methods.

  

TouchDesigner Build: 
Latest\n2021.10000
2018.28070
before 2018.28070






Retrieved from "<https://docs.derivative.ca/index.php?title=Runs_Class&oldid=28007>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")