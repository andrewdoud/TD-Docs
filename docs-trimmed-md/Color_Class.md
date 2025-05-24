

Color Class - Derivative

























# Color Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

The color class holds a single 4 component color (R, G, B, A).

```
v = tdu.Color() # starts as (0, 0, 0, 1)
v2 = tdu.Color(0, 0, 1, 1)
values = [0, 1, 0, 1]
v3 = tdu.Color(values)
green = v3[1] # access individual elements by index. Same as v3.g

```

  


## Members

`r` → `float` :

> Gets or sets the red component of the color.

`g` → `float` :

> Gets or sets the green component of the color.

`b` → `float` :

> Gets or sets the blue component of the color.

`a` → `float` :

> Gets or sets the alpha component of the color.

## Methods

`[index]`→ `float`:

> Sample values may be accessed from a Color using the [] subscript operator.

`copy()`→ `Color`:

> Returns a new color that is a copy of the color.

TouchDesigner Build: 
Latest\n2022.24140
2021.10000
2018.28070
before 2018.28070






Retrieved from "<https://docs.derivative.ca/index.php?title=Color_Class&oldid=26974>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")