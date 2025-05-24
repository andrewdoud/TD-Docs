

SysInfo Class - Derivative




# SysInfo Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The SysInfo class describes current system information. **Note:** It can be accessed with the `sysinfo` object, found in the automatically imported [td module](Td_Module.html "Td Module").
```
# return the amount of available ram
sysinfo.ram
```
  

## Members
`numCPUs` → `int` **(Read Only)**:
> The number of CPUs/cores on the system.
`ram` → `float` **(Read Only)**:
> Amount of available RAM memory.
`numMonitors` → `int` **(Read Only)**:
> The number of monitors.
`xres` → `int` **(Read Only)**:
> The system's current monitor resolution width.
`yres` → `int` **(Read Only)**:
> The system's current monitor resolution height.
`tfs` → `str` **(Read Only)**:
> The path to the TFS directory.
`MIDIInputs` → `list[str]` **(Read Only)**:
> A list of all MIDI Input device names.
`MIDIOutputs` → `list[str]` **(Read Only)**:
> A list of all MIDI Output device names.
## Methods
No operator specific methods.
  
TouchDesigner Build: 
Latest\nwikieditor
2021.10000
2018.28070
before 2018.28070

Retrieved from "<https://docs.derivative.ca/index.php?title=SysInfo_Class&oldid=31458>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")