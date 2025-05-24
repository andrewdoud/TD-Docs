

CUDAMemory Class - Derivative




# CUDAMemory Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
Holds a reference to CUDA memory. The CUDA memory will be deallocated when this class is destructed.
  

## Members
`ptr` → `int` **(Read Only)**:
> Returns the raw memory pointer address for the CUDA memory.
`size` → `int` **(Read Only)**:
> Returns the size of the CUDA Memory, in bytes.
`shape` → `CUDAMemoryShape` **(Read Only)**:
> Returns the [CUDAMemoryShape Class](CUDAMemoryShape_Class.html "CUDAMemoryShape Class") describing this CUDA memory. See the help for that class for notes about channel order for different data types.
## Methods
No operator specific methods.
  
TouchDesigner Build: 
Latest\nwikieditor
2022.24140
2021.10000
before 2021.10000

Retrieved from "<https://docs.derivative.ca/index.php?title=CUDAMemory_Class&oldid=31420>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")