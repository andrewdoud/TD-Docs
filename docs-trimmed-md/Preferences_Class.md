

Preferences Class - Derivative




# Preferences Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Preferences class describes the set of configurable preferences that are retained between sessions. It can be accessed with the ui.preferences object or through the [Preferences Dialog](Dialogs_Preferences_Dialog.html "Dialogs:Preferences Dialog").
  

## Members
`defaults` → `dict` **(Read Only)**:
> A dictionary of preferences with their default values.
## Methods
`save()`→ `None`:
> Save preference values to disk. Unless saved, changes to preferences will be lost, next time application is started.
`resetToDefaults()`→ `None`:
> Reset all preferences to their default values.
`load()`→ `None`:
> Restore preference values from disk.
### Special Functions
`len(Preferences)`→ `int`:
> Returns the total number of preferences.
> 
> ```
> a = len(ui.preferences)
> 
> ```
`[<preference name>]`→ `value`:
> Get or set specific preference given a preference name key.
> 
> ```
> v = ui.preferences['dats.autoindent']
> ui.preferences['dats.autoindent'] = 0
> 
> ```
`Iterator`→ `str`:
> Iterate over each preference name.
> 
> ```
> for p in ui.preferences:
> 	print(p) # print the name of all preferences
> 
> ```
  
TouchDesigner Build: 
Latest\n2021.10000
2018.28070
before 2018.28070

Retrieved from "<https://docs.derivative.ca/index.php?title=Preferences_Class&oldid=26986>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")