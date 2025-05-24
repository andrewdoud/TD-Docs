

# Panes_Class

Panes Class - Derivative




# Panes Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Panes class describes the list of all [pane objects](Pane_Class.html "Pane Class"). It can be accessed from [ui.panes](UI_Class.html "UI Class").
  

## Members
`current` → `td.Pane` **(Read Only)**:
> The currently selected [pane](Pane_Class.html "Pane Class").
## Methods
`createFloating(type=None, name=None, maxWidth=1920, maxHeight=1080, monitorSpanWidth=0.9, monitorSpanHeight=0.9)`→ `Pane`:
> Return a floating pane.
> 
> * type - (Keyword, Optional) Type of pane created. See [Pane](Pane_Class.html "Pane Class") for examples. Defaults to Network Editor.
> * name - (Keyword, Optional) Name of the pane. This value can be used to find the pane in ui.panes.
> * maxWidth - (Keyword, Optional) Upper limit on the width of the created window. Specified in pixels.
> * maxHeight - (Keyword, Optional) Upper limit on the height of the created window. Specified in pixels.
> * monitorSpanWidth - (Keyword, Optional) Specifies window width as a portion of the monitor width.
> * monitorSpanHeight - (Keyword, Optional) Specifies window height as a portion of the monitor height.
> 
> Example
> 
> ```
>     p = ui.panes.createFloating(type=PaneType.NETWORKEDITOR, name="Output")
>     p.owner = op('/project1/base1')
> 
> ```
### Special Functions[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Special Functions")]
`len(Panes)`→ `int`:
> Returns the total number of panes.
> 
> ```
> a = len(ui.panes)
> 
> ```
`[index]`→ `td.Pane`:
> Get specific pane, referenced by string or index.
> 
> ```
> p = ui.panes[0]
> p = ui.panes['pane1']
> 
> ```
`Iterator`→ `td.Pane`:
> Iterate over each pane.
> 
> ```
> for n in ui.panes:
> 	# do something with n
> 
> ```
  
TouchDesigner Build: Latest\nwikieditorwikieditor2021.100002018.28070before 2018.28070
A work area in TouchDesigner's layout that includes the [Network Editor](Network_Editor.html "Network Editor") and 7 other pane types used for different tasks. The TouchDesigner interface can consist of a single pane, or be split into multiple panes.

A pane type where networks of operators can be created and edited.

Retrieved from "<https://docs.derivative.ca/index.php?title=Panes_Class&oldid=31568>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")