

MOD Class - Derivative

























# MOD Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

The MOD class provides access to Module On Demand object, which allows [DATs](DAT.html "DAT") to be dynamically imported as modules. It can be accessed with the mod object, found in the automatically imported [td module](Td_Module.html "Td Module"). Alternatively, one can use the regular python statement: import.
Use of the import statement is limited to modules in the search path, where as the mod format allows complete statements in one line, which is more useful for entering expressions. Also note that DAT modules cannot be organized into packages as regular file system based python modules can be.

  


## Contents

* [1 Members](#Members)
* [2 Methods](#Methods)
* [3 Usage](#Usage)
* [4 Comparing Usage](#Comparing_Usage)
* [5 Search Path](#Search_Path)
## Members

No operator specific members.

  


## Methods

No operator specific methods.

## Usage[[edit](https://docs.derivative.ca/index.php?title=Template:Section&action=edit&section=T-1 "Edit section: Usage")]

There are three methods to import DATs as modules in a script.

* `import datName`  
  Import the module defined by the DAT named datName. All regular import options are supported (from, as, etc). If a DAT is not found, the regular file system search path is then used.
  ```
  # import a DAT named addMonth
  import addMonths
  
  ```
* `m = mod.datName`  
  Import the module defined by the DAT named datName.
  ```
  m = mod.addMonths(1,2,3)
  
  ```
* `m = mod(pathToDat)`  
  Similar to above, except a path to the DAT can be used.
  ```
  m = mod('myMods/adders').addMonths(1,2,3)
  
  ```

## Comparing Usage[[edit](https://docs.derivative.ca/index.php?title=Template:Section&action=edit&section=T-1 "Edit section: Comparing Usage")]

Example using import:

```
import myUtils
a = myUtils.add(5,6)

```

Same example using mod:

```
a = mod.myUtils.add(5,6)

```

Example using mod outside the search path:

```
a = mod('/projects/utils/utilsA').add(5,6)

```

Notice however, that a single import statement will be faster than the case of multiple identical mod statements:

```
import myUtils
a = myUtils.add(5,6)
b = myUtils.add(5,6)
c = myUtils.add(5,6)

```

will execute faster than:

```
a = mod.myUtils.add(5,6)
b = mod.myUtils.add(5,6)
c = mod.myUtils.add(5,6)

```

However the above could be rewritten more efficiently like this, which would then execute at the same speed as the import statement:

```
m = mod.myUtils
a = m.add(5,6)
b = m.add(5,6)
c = m.add(5,6)

```
## Search Path[[edit](https://docs.derivative.ca/index.php?title=Template:Section&action=edit&section=T-1 "Edit section: Search Path")]

The current component is searched first.

If the [DAT](DAT.html "DAT") is not found, the local/modules [component](Component.html "Component") of the current [component](Component.html "Component") is then searched.

Next the local/modules [component](Component.html "Component") of each parent is successively searched.

If the [DAT](DAT.html "DAT") is still not found, None is returned.

  

TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").







Retrieved from "<https://docs.derivative.ca/index.php?title=MOD_Class&oldid=13529>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")