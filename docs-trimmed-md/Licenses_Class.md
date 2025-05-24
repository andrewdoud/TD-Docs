

# Licenses_Class

Licenses Class - Derivative




# Licenses Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The Licenses class describes the set of all installed [license objects](License_Class.html "License Class"). It can be accessed with the licenses object, , found in the automatically imported [td module](Td_Module.html "Td Module").
```
print(len(licenses))	# number of licenses 
print(licenses[0])		# first license in the list
for l in licenses:
	print(l.type)		# print all installed licenses' types
```
  

## Members
`disablePro` → `bool` :
> When True, the application will run as though no Pro licenses are available. This can be used to test compatibility with lesser licenses. (See also: [app.addNonCommercialLimit](App_Class.html#Methods "App Class"))
`dongles` → `list` **(Read Only)**:
> Get the list of dongles connected to the system.
`machine` → `str` **(Read Only)**:
> The computer machine name.
`systemCode` → `str` **(Read Only)**:
> The unique computer system code.
`isPro` → `bool` **(Read Only)**:
> When True, the application is running with a Pro license. It is recommended to use this and isNonCommerical over the type method.
`isNonCommercial` → `bool` **(Read Only)**:
> When True, the application is running with a Non-Commercial license. It is recommended to use this and isPro over the type method.
`type` → `str` **(Read Only)**:
> The highest ranking license type of all installed licenses, some products being 'Pro', 'Non-Commercial', 'Commercial'. See also app.product in [App Class](App_Class.html "App Class").
## Methods
`install(key)`→ `bool`:
> Install a [license](License_Class.html "License Class") with the specified key. Returns True if successful.
TouchDesigner Build: 
Latest\nwikieditor
2021.10000
2018.28070
before 2018.28070

Retrieved from "<https://docs.derivative.ca/index.php?title=Licenses_Class&oldid=28353>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")