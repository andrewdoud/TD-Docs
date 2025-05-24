

VFS Class - Derivative




# VFS Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The VFS Class describes a COMP's [Virtual File System](Virtual_File_System.html "Virtual File System").   
To access a virtual file in any operator's file parameter, use the virtual path format: `vfs:<path to comp>:<filename>`.   
[VFSFile\_Class](VFSFile_Class.html "VFSFile Class") does the file operators.
  

## Members
`owner` → `OP` **(Read Only)**:
> Get the OP owner.
## Methods
`[name]`→ `VFSFile`:
> [VFS Files](VFSFile_Class.html "VFSFile Class") may be easily accessed using the [] syntax.
> 
> * name - Must be an exact VFS file name. Wildcards are not supported. If not found, an error will be raised.
> 
> ```
> p = op('base1').vfs['Banana.tif']
> 
> ```
`addByteArray(byteArray, name)`→ `VFSFile`:
> Add an embedded file from a bytearray to the component. Returns a VFSFile instance of the added file. To delete the file, see `destroy()` on [VFSFile Class](VFSFile_Class.html "VFSFile Class").
> 
> * byteArray - A bytearray or bytes object representing the contents of the file.
> * name - The name of the file on VFS.
`addFile(filePath, overrideName=None)`→ `VFSFile`:
> Add an embedded file from disk to the component with an option to override the name. Returns a VFSFile instance of the added file. To delete the file, see `destroy()` on [VFSFile Class](VFSFile_Class.html "VFSFile Class").
> 
> * filePath - The path of the file on disk to add.
> * overrideName (Keyword, Optional) - When specified, will override the name of the file in VFS.
`export(folder, pattern='*', overwrite=False)`→ `list`:
> Exports any matching files to the folder on disk. If overwrite is True then any existing files on disks with the same name will be overwritten. Returns a list of paths on disk to the exported files.
> 
> * folder - The folder on disk to export the files to.
> * pattern (Keyword, Optional) - The pattern to match names by.
> * overwrite (Keyword, Optional) - When True, will overwrite any files that share the same name.
> 
> ```
> # VFS contains one file with name 'A/B.tif'
> COMP.vfs.export('C:/tmp') # returns ['C:/tmp/A/B.tif']
> 
> ```
`find(pattern='*')`→ `list`:
> Finds all files in VFS with names matching the pattern. Returns a list of VFSFile objects.
> 
> * pattern (Keyword, Optional) - The pattern to match names by.
### Special Functions[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Special Functions")]
`len(VFS)`→ `int`:
> Returns the total number of virtual files.
> 
> ```
> a = len(op('base1').vfs)
> 
> ```
`Iterator`→ `str`:
> Iterate over each virtual file name.
> 
> ```
> for f in op('base1').vfs:
> 	debug(f) # print info of all virtual files on base1
> 
> ```
  
TouchDesigner Build: Latest\n2021.10000before 2021.10000
Lets you embed files inside a `[.tox](-2.html ".tox")` or `[.toe](.html ".toe")` file. Operators like the Movie File In TOP that read regular files can also read the embedded VFS files using a `vfs:` syntax.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=VFS_Class&oldid=26991>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")