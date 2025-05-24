

# UI_Class

UI Class - Derivative




# UI Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The UI class describes access to the UI elements of the application, found in the automatically imported [td module](Td_Module.html "Td Module").
To access members and methods of this class use the default instance `ui`.
For Example:
```
# open the Midi Device Mapper Dialog
ui.openMIDIDeviceMapper()
```
  

## Members
`clipboard` → `str` :
> Get or set the operating system clipboard text contents.
`colors` → `Colors` **(Read Only)**:
> Access to the application [colors](Colors_Class.html "Colors Class").
`dpiBiCubicFilter` → `bool` :
> Get or set the global DPI scale filtering mode of TouchDesigner windows. True means bi-cubic, False means linear.
`masterVolume` → `float` :
> Get or set the master audio output volume. A value of 0 is no output, while a value of 1 is full output.
`options` → `Options` **(Read Only)**:
> Access to the application [options](Options_Class.html "Options Class").
`panes` → `Panes` **(Read Only)**:
> Access to the set of all [panes](Panes_Class.html "Panes Class").
`performMode` → `bool` :
> Get or set [Perform Mode](Perform_Mode.html "Perform Mode"). Set to True to go into Perform Mode, False to go into [Designer Mode](Designer_Mode.html "Designer Mode").
`preferences` → `Preferences` **(Read Only)**:
> Access to the application [preferences](Preferences_Class.html "Preferences Class"), which can also be access through the [Preferences Dialog](Dialogs_Preferences_Dialog.html "Dialogs:Preferences Dialog").
`redrawMainWindow` → `bool` :
> Get or set whether the main window should redraw. The main window is either the main network editor, or the perform window.
`rolloverOp` → `OP` **(Read Only)**:
> Operator currently under the mouse in a network editor.
`rolloverPar` → `Par` **(Read Only)**:
> Parameter currently under the mouse in a parameter dialog.
`rolloverPanel` → `PanelCOMP` **(Read Only)**:
> returns the latest panel to get a rollover event. Takes into account click through, depth order, and other panel settings.
`lastChopChannelSelected` → `Channel` **(Read Only)**:
> Last [CHOP channel](Channel.html "Channel") selected via mouse.
`showPaletteBrowser` → `bool` :
> Get or set display of the palette browser.
`status` → `str` :
> Get or set the status message.
> 
> ```
> ui.status = 'Operation Complete'
> 
> ```
`undo` → `Undo` **(Read Only)**:
> The [Undo](Undo_Class.html "Undo Class") object, which provides access to application undo functions.
`windowWidth` → `int` **(Read Only)**:
> Get the app window width.
`windowHeight` → `int` **(Read Only)**:
> Get the app window height.
`windowX` → `int` **(Read Only)**:
> Get the app window X position.
`windowY` → `int` **(Read Only)**:
> Get the app window Y position.
## Methods
`copyOPs(listOfOPs)`→ `None`:
> Copy a list of operators to the operator clipboard. All operators must be children of the same component.
> 
> * listOfOPs - A list containing one or more OPs to be copied.
> 
> ```
> ui.copyOPs( op('geo1').selected )
> 
> ```
`pasteOPs(COMP, x=None, y=None)`→ `None`:
> Copy the contents of the operator clipboard into the specified component.
> 
> * COMP - The destination to receive the operators.
> * x - Optional network coordinates at which to paste the operators.
> * y - see x
> 
> ```
> l = ui.pasteOPs( op('geo2') )
> 
> ```
`messageBox(title, message, buttons=['Ok'])`→ `int`:
> This method will open a message dialog box with the specified message. Returns the index of the button clicked.
> 
> * title - Specifies the window title.
> * message - Specifies the content of the dialog.
> * buttons - (Keyword, Optional) Specifies a list button labels to show in the dialog.
> 
> ```
> # basic usage
> ui.messageBox('Warning', 'Have a nice day.')
> # specify options and report result
> a = ui.messageBox('Please select:', 'Buttons:', buttons=['a', 'b', 'c'])
> ui.messageBox('Results', 'You selected item: ' + str(a))
> # pick a node from their paths
> ui.messageBox('Please select:', 'Nodes:', buttons=parent().children)
> # pick a node from their first names (list comprehension)
> ui.messageBox('Please select:', 'Nodes:', buttons=[x.name for x in parent().children])
> # pick a cell
> ui.messageBox('Please select:', 'Cells:', buttons=op('table1').cells('*','*'))
> 
> ```
`refresh()`→ `None`:
> Update and redraw all viewports, nodes, UI elements etc immediately. This update is otherwise done once per frame at the end of all script executions. For example, if the current frame is manually changed during a script, a call to refresh will cause all dependent data to update immediately.
> 
> ```
> for i in range(100):
> 	ui.status = str(i)
> 	ui.refresh()
> 
> ```
`chooseFile(load=True, start=None, fileTypes=None, title=None, asExpression=False)`→ `str | None`:
> Open a dialog box for loading or saving a file. Returns the filename selected or None if the dialog is cancelled.
> 
> * load - (Keyword, Optional) If set to True, the dialog will be a Load dialog, otherwise it's a Save dialog.
> * start - (Keyword, Optional) If provided, specifies an initial folder location and/or filename selection.
> * fileTypes - (Keyword, Optional) If provided, specifies a list of file extensions that can be used as filters. Otherwise '\*.\*' is the only filter.
> * asExpression - (Keyword, Optional) If set to true, the results are provided as an expression, suitable for a [Parameter](Par_Class.html "Par Class") expression or as input to an eval() call. [App Class](App_Class.html "App Class") member constants such as samplesFolder may be included in the result.
> * title (Keyword, Optional) If provided, will override the default window title.
> 
> ```
> a = ui.chooseFile(start='python_examples.toe', fileTypes=['toe'], title='Select a toe') # specify extension
> a = ui.chooseFile(fileTypes=tdu.fileTypes['image'], title='Select an image') # any support image extension
> path = ui.chooseFile(load=False,fileTypes=['txt'],title='Save table as:')
> if (path):
> 	op('table1').save(path)
> 
> ```
`chooseFolder(title='Select Folder', start=None, asExpression=False)`→ `str | None`:
> Open a dialog box for selecting a folder. Returns the folder selected or None if the dialog is cancelled.
> 
> * title - (Keyword, Optional) If provided, specifies the window title.
> * start - (Keyword, Optional) If provided, specifies an initial folder location and/or filename selection.
> * asExpression - (Keyword, Optional) If set to true, the results are provided as an expression, suitable for a [Parameter](Par_Class.html "Par Class") expression or as input to an eval() call. [App Class](App_Class.html "App Class") member constants such as samplesFolder may be included in the result.
> 
> ```
> a = ui.chooseFolder()
> a = ui.chooseFolder(title='Select a folder location.')
> 
> ```
`viewFile(URL_or_path, showInFolder=False)`→ `None`:
> View a URL or file in the default external application. You can use `ui.viewFile()` to open a folder/directory in Windows Explorer or macOS Finder.
> 
> * URL\_or\_path - URL or path to launch.
> 
> ```
> a = ui.viewFile('output.txt')
> 
> ```
> 
> * showInFolder - Show file as selected in Explorer or macOS Finder instead of launching an external application.
> 
> ```
> a = ui.viewFile('output.txt', showInFolder=True)
> 
> ```
`openBeat()`→ `None`:
> Open the [Beat Dialog](Beat_Dialog.html "Beat Dialog").
`openBookmarks()`→ `None`:
> Open the [Bookmarks Dialog](Bookmarks_Dialog.html "Bookmarks Dialog").
`openCOMPEditor(path)`→ `None`:
> Open component editor for the specific operator.
> 
> * path - Specifies the path to the operator. An OP can be passed in as well.
`openConsole()`→ `None`:
> Open the [Console Window](https://docs.derivative.ca/index.php?title=Console_Window&action=edit&redlink=1 "Console Window (page does not exist)").
`openDialogHelp(title)`→ `None`:
> Open help page for the specific dialog.
> 
> * title - Specifies the help page to open.
> 
> ```
> ui.openDialogHelp('Window Placement Dialog')
> 
> ```
`openErrors()`→ `None`:
> Open the [Errors Dialog](https://docs.derivative.ca/Errors_Dialog "Errors Dialog").
`openExplorer()`→ `None`:
> Open an Explorer window.
`openExportMovie(path)`→ `None`:
> Open the [Export Movie Dialog](Export_Movie_Dialog.html "Export Movie Dialog").
> 
> * path - Specifies the operator content to export, optional.
> 
> ```
> ui.openExportMovie('/project1/out1')
> 
> ```
`openImportFile()`→ `None`:
> Open the [Import File Dialog](https://docs.derivative.ca/Import_File_Dialog "Import File Dialog").
`openKeyManager()`→ `None`:
> Open the [Key Manager Dialog](Key_Manager_Dialog.html "Key Manager Dialog").
`openMIDIDeviceMapper()`→ `None`:
> Open the [MIDI Device Mapper Dialog](MIDI_Device_Mapper_Dialog.html "MIDI Device Mapper Dialog").
`openNewProject()`→ `None`:
> Open the [New Project Dialog](https://docs.derivative.ca/New_Project_Dialog "New Project Dialog").
`openOperatorSnippets(family=None, type=None, example=None)`→ `None`:
> Open the Operator Snippets window.
`openPaletteBrowser()`→ `None`:
> Open the [Palette](Palette.html "Palette").
`openPerformanceMonitor()`→ `None`:
> Open the [Performance Monitor Dialog](https://docs.derivative.ca/Performance_Monitor_Dialog "Performance Monitor Dialog").
`openPreferences()`→ `None`:
> Open the [Preferences Dialog](Dialogs_Preferences_Dialog.html "Dialogs:Preferences Dialog").
`openSearch()`→ `None`:
> Open the [Search Replace Dialog](https://docs.derivative.ca/Search_Replace_Dialog "Search Replace Dialog").
`openTextport()`→ `None`:
> Open the [Textport](Textport.html "Textport").
`openVersion()`→ `None`:
> Open a dialog displaying current version information.
> See also: [App.version](App_Class.html "App Class")
`openWindowPlacement()`→ `None`:
> Open the [Window Placement Dialog](Window_Placement_Dialog.html "Window Placement Dialog").
`findEditDAT(filename)`→ `DAT | None`:
> Given an external filename, finds the corresponding DAT thats update from this filename if any..
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditorwikieditorwikieditorwikieditorwikieditor2022.241402021.100002018.28070before 2018.28070
Any floating window that is not a [Pane](Pane.html "Pane") or [Viewer](Viewer.html "Viewer").

Perform Mode is an optimized mode for live performance that only renders one specified [Window COMP](Window_COMP.html "Window COMP") which is one window that contains your video outputs and your (optional) control interface. In Perform Mode the network editing window is not open - you edit your networks in [Designer Mode](Designer_Mode.html "Designer Mode"). Alternate with F1 and Esc.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

A [CHOP](CHOP.html "CHOP") outputs one or more channels, where a channel is simply a sequence of numbers ([Samples](Sample.html "Sample")), representing motion, audio, etc. Channels are passed between CHOPs in TouchDesigner networks. Channels can be [Exported](Export.html "Export") to [Parameters](Parameter.html "Parameter").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

A Folder in TouchDesigner always refers to a Windows or macOS operating system directory/folder system that contain files and other folders. It does not refer to operators within TouchDesigner. See [Network Path](Network_Path.html "Network Path").

A Window in TouchDesigner is a window in Microsoft Windows or macOS that contains either (1) the TouchDesigner editing interface that exists in [Designer Mode](Designer_Mode.html "Designer Mode"), or (2) a user-created [Panel](Panel.html "Panel") inside a [Window Component](Window_COMP.html "Window COMP"). The user-created windows can span [Multiple Monitors](Multiple_Monitors.html "Multiple Monitors") borderless, or be floating windows with borders, or popups.

[OP Snippets](OP_Snippets.html "OP Snippets") is a set of 700+ live examples of TouchDesigner operators. You can access snippets via the Help menu, or by right-clicking on network operators, or r-clicking on OP Create dialog items.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

Retrieved from "<https://docs.derivative.ca/index.php?title=UI_Class&oldid=32014>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")