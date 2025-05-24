

Options Class - Derivative




# Options Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Options class describes the set of configurable UI options. It can be accessed with the ui.options object.
  

## Members
No operator specific members.
  

## Methods
`resetToDefaults()`→ `None`:
> Reset all options to their default values.
### Special Functions[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Special Functions")]
`len(Options)`→ `int`:
> Returns the total number of options.
> 
> ```
> a = len(ui.options)
> 
> ```
`[<option name>]`→ `value`:
> Get or set specific option given an option name key.
> 
> ```
> v = ui.options['DAT.width']
> ui.options['DAT.width'] = 50
> 
> ```
`Iterator`→ `str`:
> Iterate over each option name.
> 
> ```
> for n in ui.options:
> 	print(n) # print the name of all options
> 
> ```
  
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

Retrieved from "<https://docs.derivative.ca/index.php?title=Options_Class&oldid=26983>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")