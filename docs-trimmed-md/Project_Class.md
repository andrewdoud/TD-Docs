

Project Class - Derivative

























# Project Class

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

The Project class describes the current session. It can be accessed with the project object, found in the automatically imported [td module](Td_Module.html "Td Module"). Members changed in this such as the 'paths' member will be written to disk when the project is saved.

  


## Members

`folder` → `str` **(Read Only)**:

> The folder at which the project resides.

`name` → `str` **(Read Only)**:

> The filename under which the project is saved.

`saveVersion` → `str` **(Read Only)**:

> The [App](App_Class.html "App Class") version number when the project was last saved.

`saveBuild` → `str` **(Read Only)**:

> The [App](App_Class.html "App Class") build number when the project was last saved.

`saveTime` → `str` **(Read Only)**:

> The time and date the project was last saved.

`saveOSName` → `str` **(Read Only)**:

> The [App](App_Class.html "App Class") operating system name when the project was last saved.

`saveOSVersion` → `str` **(Read Only)**:

> The [App](App_Class.html "App Class") operating system version when the project was last saved.

`paths` → `dict` **(Read Only)**:

> A dictionary which can be used to define URL-syntax path prefixes, enabling you to move your media to different locations easily. This dictionary is saved and loaded in the `.toe` file. Example: Run `project.paths['movies'] = 'C:/MyMovies'`, and reference it with a parameter expression: `movies://butterfly.jpg`. To manually convert between expanded and collapsed paths, use `tdu.collapsePath()` and `[tdu.expandPath](TDU_Class.html "TDU Class")`, for example `tdu.expandPath('movies://butterfly.jpg')` expands to `C:/MyMovies/butterfly.jpg`. If you already have your paths setup, choosing files from file browsers in OPs will create paths using these shortcuts rather than full paths. Additionally, to enable you to have different media locations on different machines, you can put a JSON file in the same folder as your `.toe` that gets read on startup. This will override any existing locations saved in projects.paths to the new machine specific file paths specified in the .json. Only existing entries in `project.paths` will be used. If the .json contains path names not specified in `project.paths`, those will be ignored. It would contain something like `{ "project.paths": { "movies": "M:/MyMovies" } }`. If your `.toe` file is called `MyProject.10.toe`, the JSON file must be called `MyProject.Settings.json`. The idea is that this .json would be unique to machines, and not commited to version control or shared between machines.

`cookRate` → `float` :

> Get or set the maximum number of frames processed each second. In general you should not need to use this. It is preferred to look at the FPS of the root component to know the cooking rate. Individual [components](COMP_Class.html "COMP Class") may have their own rates, specified by rate.
> 
> ```
> a = project.cookRate # get the current cook rate 
> project.cookRate = 30 # set the cook rate to 30 FPS
> 
> ```
> 
> Note: This is displayed and set in the user interface at the bottom-left: the "FPS" field.

`realTime` → `bool` :

> Get or set the real time cooking state. When True, frames may be skipped in order to maintain the cookRate. When False, all frames are processed sequentially regardless of duration. This is useful to render movies out using the Movie File Out TOP without dropping any frames for example.
> 
> ```
> a = project.realTime
> project.realTime = False # turn off real time playback.
> 
> ```

`isPrivate` → `bool` **(Read Only)**:

> True when the project networks cannot be directly viewed.

`isPrivateKey` → `bool` **(Read Only)**:

> True when the private networks are accessible by a pass phrase.

`cacheParameters` → `bool` :

> Cache parameter values instead of always evaluating.

`externalToxModifiedInProject` → `bool` **(Read Only)**:

> Callback for when an external tox has been modified in the current project and there are other instances of the same tox loaded elsewhere in the project.

`externalToxModifiedOnDisk` → `bool` **(Read Only)**:

> Callback for when an external tox file has been modified on disk.

`windowOnTop` → `bool` :

> Get or set the window on top state.

`windowStartMode` → `WindowStartMode` :

> Get or set the window start mode.
> The mode is one of: `WindowStartMode.AUTO`, `WindowStartMode.FULL`, `WindowStartMode.LEFT`, `WindowStartMode.RIGHT` or `WindowStartMode.CUSTOM`.

`windowDraw` → `bool` :

> Get or set the window drawing state.

`windowStartCustomWidth` → `int` :

> Get or set the window start width. Only used when windowStartMode is `WindowStartMode.CUSTOM`.

`windowStartCustomHeight` → `int` :

> Get or set the window start height. Only used when windowStartMode is `WindowStartMode.CUSTOM`.

`windowStartCustomX` → `int` :

> Get or set the window start X position. Only used when windowStartMode is `WindowStartMode.CUSTOM`.

`windowStartCustomY` → `int` :

> Get or set the window start Y position. Only used when windowStartMode is `WindowStartMode.CUSTOM`.

`performOnStart` → `bool` :

> Get or set the perform on start state.

`performWindowPath` → `OP` :

> Get or set the perform window path.

`resetAudioOnDeviceChange` → `bool` :

> Get or set whether audio devices momentarily reset when devices are added or removed to the system.

## Methods

`load(path)`→ `None`:

> Load a specific .toe file from disk.
> 
> * path - (Optional) The path of the file to load. If not specified, loads the default[.toe file](https://docs.derivative.ca/index.php?title=.toe_file&action=edit&redlink=1 ".toe file (page does not exist)"), as specified in preferences.
> 
> ```
> project.load('test_demo.toe')
> 
> ```

`save(path, saveExternalToxs=False)`→ `bool`:

> Save the current session to disk. Returns True if a file was saved, False otherwise (eg, if the file exists, and when prompted, the user selects to not overwrite).
> 
> * path - (Optional) If not provided the default/current filename is incremented and used. The current file is project.name under folder project.folder.
> * saveExternalToxs - (Keyword, Optional) If set to True, will save out the contents of any COMP that references an external .tox into the referenced .tox file.
> 
> ```
> project.save('test_demo.toe')
> project.save()
> 
> ```

`quit(force=False, crash=False)`→ `None`:

> Quit the project.
> 
> * force - (Keyword, Optional) If set to True, unsaved changes will be discarded without prompting.
> * crash - (Keyword, Optional) If set to True, the application will terminate unexpectedly. This is used for system testing.
> 
> ```
> project.quit()  #quit project, possibly prompting for unsaved changes if 'Prompt to Save on Exit' in Preferences dialog is enabled.
> project.quit(force=True)  #quit project immediately.
> 
> ```

`addPrivacy(key)`→ `bool`:

> Add privacy to a toe file with the given key.
> 
> Privacy can only be added to toes that currently have no privacy, and are using a Pro license.
> 
> * key - The key phrase. This should resolve to a non-blank string.
> 
> ```
> project.addPrivacy('secret')
> 
> ```

`removePrivacy(key)`→ `bool`:

> Completely remove privacy from a toe file.
> 
> * key - The current privacy key phrase.
> 
> ```
> project.removePrivacy('secret')
> 
> ```

`accessPrivateContents(key)`→ `bool`:

> Gain access to a private file. The file will still be private the next time it is saved or re-opened.
> 
> * key - The current privacy key phrase.
> 
> ```
> project.accessPrivateContents('secret')
> 
> ```

`applyWindowSettings()`→ `None`:

> Applies the project's window start settings to the current TouchDesigner window.

`stack()`→ `str`:

> Formatted contents of current cook and parameter evaluation stack.
> 
> ```
> print(project.stack())
> 
> ```

`pythonStack()`→ `str`:

> Formatted contents of current python stack.
> 
> ```
> print(project.pythonStack())
> 
> ```

TouchDesigner Build: Latest\nwikieditor2022.241402021.100002018.28070before 2018.28070

TOuch Environment file, the file type used by TouchDesigner to save your entire project.


The [Frames](Frame.html "Frame")-per-Second that TouchDesigner's [Timeline](Timeline.html "Timeline") runs at. Set with `project.cookRate`.


An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


Some operators have a DAT [docked](Docking.html "Docking") to them that contains some python functions. These functions, called "callbacks", get called when something in the operator changes.


Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").


An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").


TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.


Privacy of TouchDesigner Components (`.tox` files) or Projects (`.toe` files) is the protection of networks that enables them to be used but not be visible or editable.







Retrieved from "<https://docs.derivative.ca/index.php?title=Project_Class&oldid=31145>"
[Category](Special_Categories.html "Special:Categories"):

* [Python Reference](Category_Python_Reference.html "Category:Python Reference")