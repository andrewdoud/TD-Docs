

Colors Class - Derivative




# Colors Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Colors Class describes the application colors. It can be accessed from the global [ui](UI_Class.html "UI Class") object.
  

## Members
No operator specific members.
  

## Methods
`resetToDefaults()`→ `None`:
> Set the colors to their default values.
### Special Functions
The Colors class is an iterable object that contains a set of named color attributes. The len, subscript and assignment operators are defined.
Each name can be used to get or set a triplet of values corresponding to that color.
`len(Colors)`→ `int`:
> Returns the total color options.
> 
> ```
> a = len(ui.colors)
> 
> ```
`[<color option name>]`→ `triplet(r,g,b)`:
> Get or set specific color option, given a string key.
> 
> ```
> n = ui.colors['default.bg']
> ui.colors['default.bg'] = (1,0,0)
> 
> ```
`Iterator`→ `str`:
> Iterate over each color option name.
> 
> ```
> for n in ui.colors:
> 	print(n)
> 	ui.colors[n] = myColorsList[n]
> 
> ```
  
TouchDesigner Build: 
Latest\n2022.24140
2021.10000
2018.28070
before 2018.28070

Retrieved from "<https://docs.derivative.ca/index.php?title=Colors_Class&oldid=26975>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")