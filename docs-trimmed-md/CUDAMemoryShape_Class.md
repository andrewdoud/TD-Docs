

# CUDAMemoryShape_Class

CUDAMemoryShape Class - Derivative




# CUDAMemoryShape Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
Describes the shape of a CUDA memory segment.
  

## Members
`width` → `int` :
> Get/Set the width in pixels of the memory.
`height` → `int` :
> Get/Set the height in pixels of the memory.
`numComps` → `int` :
> Get/Set the number of color components per pixel of the memory.
`dataType` → `numpy.dtype` :
> Get/Set the data type of each color component, as a numpy data type. E.g numpy.uint8, numpy.float32. Note that for uint8 data types, the channel ordering will be BGRA for 4 component textures. It will be RGBA however for other data types.
## Methods
No operator specific methods.
  
TouchDesigner Build: 
Latest\nwikieditor
2022.24140
2021.10000

Retrieved from "<https://docs.derivative.ca/index.php?title=CUDAMemoryShape_Class&oldid=31421>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")