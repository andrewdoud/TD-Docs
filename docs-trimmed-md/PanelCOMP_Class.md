

# PanelCOMP_Class

PanelCOMP Class - Derivative




# PanelCOMP Class
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
The PanelCOMP describes an instance of a [Panel Component](Panel_Component.html "Panel Component"). The state is represented by [Panel Values](Panel_Value.html "Panel Value").
This class inherits from the COMP Class.
  

## Contents
* [1 Members](#Members)
* [2 Methods](#Methods)
* [3 COMP Class](#COMP_Class)
  + [3.1 Members](#Members_2)
    - [3.1.1 Privacy](#Privacy)
    - [3.1.2 Connection](#Connection)
  + [3.2 Methods](#Methods_2)
    - [3.2.1 Custom Parameters](#Custom_Parameters)
    - [3.2.2 Privacy](#Privacy_2)
    - [3.2.3 Component Variables](#Component_Variables)
* [4 OP Class](#OP_Class)
  + [4.1 Members](#Members_3)
    - [4.1.1 General](#General)
    - [4.1.2 Common Flags](#Common_Flags)
    - [4.1.3 Appearance](#Appearance)
    - [4.1.4 Connection](#Connection_2)
    - [4.1.5 Cook Information](#Cook_Information)
    - [4.1.6 Type](#Type)
  + [4.2 Methods](#Methods_3)
    - [4.2.1 General](#General_2)
    - [4.2.2 Errors](#Errors)
    - [4.2.3 Appearance](#Appearance_2)
    - [4.2.4 Viewers](#Viewers)
    - [4.2.5 Storage](#Storage)
    - [4.2.6 Miscellaneous](#Miscellaneous)
## Members
`panel` → `td.Panel` **(Read Only)**:
> The [Panel](Panel_Class.html "Panel Class") from which [Panel Values](Panel_Value.html "Panel Value") and the [PanelValue Class](PanelValue_Class.html "PanelValue Class") may be accessed. (The second form is usually sufficient.)
> 
> ```
> v = op('button1').panel.u.val
> v = op('button1').panel.u
> 
> ```
`panelRoot` → `OP` **(Read Only)**:
> The panelCOMP at the top of the panel hierarchy.
`panelChildren` → `list` **(Read Only)**:
> The children panelCOMPs of this operator.
`x` → `int` **(Read Only)**:
> The panel's x coordinate, as measured in pixels.
`y` → `int` **(Read Only)**:
> The panel's y coordinate, as measured in pixels.
`width` → `int` **(Read Only)**:
> The panel's width, as measured in pixels.
`height` → `int` **(Read Only)**:
> The panel's height, as measured in pixels.
`marginX` → `int` **(Read Only)**:
> The panel's x coordinate adjusted by margins as measured in pixels.
`marginY` → `int` **(Read Only)**:
> The panel's y coordinate adjusted by margins, as measured in pixels.
`marginWidth` → `int` **(Read Only)**:
> The panel's width adjusted by margins, as measured in pixels.
`marginHeight` → `int` **(Read Only)**:
> The panel's height adjusted by margins, as measured in pixels.
`dropReady` → `bool` **(Read Only)**:
> The current state of the drop operation. True when the drop will be accepted.
## Methods
`panelParent(n)`→ `OP | None`:
> The nth panel parent of this operator. If n not specified, returns the panel parent. If n = 2, returns the parent of the parent, etc. If no panel parent exists at that level, None is returned. A panel parent is the panel wired to the input of this operator, or if that does not exist, the panel containing this operator.
> 
> * n - (Optional) n is the number of levels up to climb. When n = 1 it will return the operator's panel parent.
> 
> ```
> p = me.panelParent(2) #grandfather
> 
> ```
`interactMouse(u, v, leftClick=0, middleClick=0, rightClick=0, left=False, middle=False, right=False, wheel=0, pixels=False, Screen=False, quiet=True)`→ `PanelCOMP`:
> Simulates virtual mouse clicks, rollovers, moves and drags on a panel. It will also update the panel values: inside, insideu, insidev, state, u and v, in panels all the way up to the parent panel. The first (primary) mouse down/touch on a panel takes precedence over subsequent mouse downs and touches, and overrides any hovers. The primary state on a panel is global as each panel can only have one interaction updating its state.
> 
> * u - The first coordinate for the click to occur at.
> * v - The second coordinate for the click to occur at.
> * leftClick, middleClick, rightClick - (Keyword, Optional) Use to specify the number of times a button is clicked on
> * left, middle, right - (Keyword, Optional) Use to specify if the button is being pressed. When set to False it simulates a mouse move with the button up. The first time the button is set to True will initiate a virtual mouse down on the child panel at the coordinates u,v. Subsequent True states will simulate a drag (mouse button down and moving). Simulate a mouse-up by calling the button set to False, e.g. left=False.
> * wheel - (Keyword, Optional) Roll the mouse wheel
> * pixels - (Keyword, Optional) When True, the coordinates are treated as pixel offsets. When False, they are treated as normalized values.
> * screen - (Keyword, Optional) When True, the coordinates are relative to the screen. When False, they are relative to the calling container.
> * quiet - (Keyword, Optional) When False, print warning messages, such as starting a mouse-down-move on a panel that is already being moved (dragged).
> * aux - (Keyword, Optional) Auxiliary data.
> 
> ```
> op('container1').interactMouse(0.5, 0.5) # roll over the middle of container1
> op('container1').interactMouse(0.5, 0.5, leftClick=2) # double click the middle of container1
> op('container1').interactMouse(0.5, 0.5, left=True) # left mouse down on the middle of container1
> op('container1').interactMouse(0.6, 0.6, left=True) # move with left mouse down in container1
> op('container1').interactMouse(0.6, 0.6) # mouse up
> op('container1').interactMouse(0.5, 0.5, wheel=0.3) # roll the mouse wheel in the middle of container1
> op('container1').interactMouse(10, 20, pixels=True) # send a mouse event 10 pixels to the right, and 20 pixels above the lower left corner of container1
> 
> ```
`interactTouch(u, v, hover='id', start='id', move='id', end='id', pixels=False, screen=False, quiet=True, aux='data')`→ `PanelCOMP`:
> Simulates virtual multiple touches and hovers on a panel via user assigned id. It will also update the panel values: inside, insideu, insidev, state, u and v, in panels all the way up to the parent panel. The first (primary) mouse down/touch on a panel takes precedence over subsequent mouse downs and touches, and overrides any hovers. The primary state on a panel is global.
> 
> * u - The first coordinate for the click to occur at.
> * v - The second coordinate for the click to occur at.
> * hover - (Keyword, Optional) Indicates a hover performed by the touch identifiable by 'id'. If 'id' is used by a touch, the touch is ended. If the <u,v> is out of bounds, the hover will end.
> * start - (Keyword, Optional) Start a touch identifiable by 'id'. If 'id' is already touching or hovering, the action is ended and a new touch is started.
> * move - (Keyword, Optional) Move a touch identifiable by 'id'. Nothing happens if 'id' is not found.
> * end - (Keyword, Optional) End a touch identifiable by 'id'. Nothing happens if 'id' is not found.
> * pixels - (Keyword, Optional) When True, the coordinates are treated as pixel offsets. When False, they are treated as normalized values.
> * screen - (Keyword, Optional) When True, the coordinates are relative to the screen. When False, they are relative to the calling container.
> * quiet - (Keyword, Optional) Print warning messages, such as starting a touch down on a panel that already has a touch.
> 
> ```
> op('container1').interactTouch(0.5, 0.5, hover='finger') # roll over the middle of container1
> op('container1').interactTouch(0.5, 0.5, start='finger') # ends the hover and start a touch
> op('container1').interactTouch(0.7, 0.5, move='finger') # move the touch
> op('container1').interactTouch(0.3, 0.4, start='finger') # ends the previous touch and start a new touch
> op('container1').interactTouch(-1, -1, hover='finger') # ends the previous touch, and end any rollover state
> 
> ```
`interactClear()`→ `None`:
> Terminates any existing interactions. Touch or mouse interactions will end. Panels that are hovered over will end their rollover state.
`interactStatus()`→ `list`:
> Returns a list of panel interactions. Each interaction is encapsulated in a list as follows: [id, panel, state, primary].
> 
> * id - The unique string identifying the interaction. '\_\_MOUSE\_\_' is used if the interaction was established via interactMouse.
> * panel - The child panel being interacted with .
> * state - Interaction types 'hover' or 'touch'.
> * primary - True if the interaction is the first to act on the panel.
> 
> ```
> op('container1').interactStatus  # list the current hover over a slider and 2 touches over a button in container1
> [['touch1', type:sliderCOMP path:/project1/container1/slider1, 'hover', False],
> ['__MOUSE__', type:buttonCOMP path:/project1/container1/button1, 'touch', True],
> ['touch2', type:buttonCOMP path:/project1/container1/button1, 'touch', False]]
> 
> ```
`locateMouse()`→ `Tuple[float, float]`:
> Returns a tuple containing the mouse coordinates relative to the [Panel Component](Panel_Component.html "Panel Component"). If the mouse is not over a window containing the panel, None is returned instead.
`locateMouseUV()`→ `Tuple[float, float]`:
> Returns a tuple containing the normalized mouse coordinates relative to the [Panel Component](Panel_Component.html "Panel Component"). If the mouse is not over a window containing the panel, None is returned instead.
`setFocus(moveMouse=False)`→ `None`:
> Set the hierarchical focus to this component, which sets the Panel value focusselect to 1. Focus will only be set successfully if the panel is open.
> 
> * moveMouse - (Keyword, Optional) If set to True, the mouse will be moved to the component as well.
# COMP Class[[edit](https://docs.derivative.ca/index.php?title=Template:ClassInheritance&action=edit&section=T-1 "Edit section: COMP Class")]
## Members
`extensions` → `List` **(Read Only)**:
> A list of [extensions](Extensions.html "Extensions") attached to this component.
`extensionsReady` → `Bool` **(Read Only)**:
> True unless the extensions are currently compiling. Can be used to avoid accessing promoted members prematurely during an extension initialization function.
`internalOPs` → `Dict` **(Read Only)**:
> A dictionary of [internal operator shortcuts](Internal_Operators.html "Internal Operators") found in this component. See also [OP.iop](OP_Class.html#General "OP Class")
`internalPars` → `Dict` **(Read Only)**:
> A dictionary of [internal parameters shortcuts](Internal_Parameters.html "Internal Parameters") found in this component. See also [OP.ipar](OP_Class.html#General "OP Class")
`clones` → `List` **(Read Only)**:
> A list of all [components](COMP_Class.html "COMP Class") cloned to this component.
`componentCloneImmune` → `Bool` :
> Get or set [component clone Immune flag](Immune_Flag.html "Immune Flag"). This works together with the cloneImmune member of the [OP\_Class](OP_Class.html "OP Class"). When componentCloneImmune is True, everything inside the clone is [immune](Immune.html "Immune"). When componentCloneImmune is False, it uses the [OP\_Class](OP_Class.html "OP Class") cloneImmune member to determine if just the component is immune (its parameters etc, but not the component's network inside).
`vfs` → `VFS` **(Read Only)**:
> An intermediate [VFS object](VFS_Class.html "VFS Class") from which embedded [VFSFile objects](VFSFile_Class.html "VFSFile Class") can be accessed. For more information see [Virtual File System](Virtual_File_System.html "Virtual File System").
`dirty` → `Bool` **(Read Only)**:
> True if the contents of the component need to be saved.
`currentChild` → `OP` **(Read Only)**:
> The child [operator](OP_Class.html "OP Class") that is currently selected. To make an operator current, use its own [OP.current](OP_Class.html#Common_Flags "OP Class") method.
`selectedChildren` → `List` **(Read Only)**:
> The list of currently selected [children](OP_Class.html "OP Class"). To change an individual operator's selection state, use its own [OP.selected](OP_Class.html#Common_Flags "OP Class") method.
`cpuCookTime` → `float` **(Read Only)**:
> Duration of the last measured cook in CPU time (in milliseconds).
`childrenCPUCookTime` → `float` **(Read Only)**:
> The total accumulated cook time of all children of this operator during the last frame. Zero if the operator is not a COMP and/or has no children.
`childrenCPUCookAbsFrame` → `int` **(Read Only)**:
> The absolute frame on which childrenCookTime is based.
`gpuMemory` → `int` **(Read Only)**:
> The amount of GPU memory this OP is using, in bytes.
`pickable` → `Bool` :
> Get or set [pickable flag](Pickable_Flag.html "Pickable Flag").
`utility` → `Bool` :
> Get or set utility flag.
`isCOMP` → `Bool` **(Read Only)**:
> True if the operator is a component.
### Privacy[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Privacy")]
`isPrivate` → `Bool` **(Read Only)**:
> True if the the component contents cannot be directly viewed.
`isPrivacyActive` → `Bool` **(Read Only)**:
> True if the component is private, and privacy is active. When inactive the contents can be temporarily viewed.
`isPrivacyLicensed` → `Bool` **(Read Only)**:
> True if the component is private and if the required CodeMeter license is present to run it.
`privacyFirmCode` → `int` **(Read Only)**:
> The CodeMeter firm code needed to use this private component. 0 if this component is not private using a CodeMeter dongle.
`privacyProductCode` → `int` **(Read Only)**:
> The CodeMeter product code needed to use this private component. 0 if this component is not private using a CodeMeter dongle.
`privacyDeveloperName` → `string` **(Read Only)**:
> The name of the developer of this private component.
`privacyDeveloperEmail` → `string` **(Read Only)**:
> The email of the developer of this private component.
### Connection[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Connection")]
`inputCOMPs` → `List` **(Read Only)**:
> List of input [components](COMP_Class.html "COMP Class") to this component through its top connector.
`inputCOMPConnectors` → `List` **(Read Only)**:
> List of input [connectors](Connector_Class.html "Connector Class") (on the top) associated with this component.
`outputCOMPs` → `List` **(Read Only)**:
> List of output [components](COMP_Class.html "COMP Class") from this component through its bottom connector.
`outputCOMPConnectors` → `List` **(Read Only)**:
> List of output [connectors](Connector_Class.html "Connector Class") (on the bottom) associated with this component.
## Methods
`create(opType, name, initialize=True)`→ `OP`:
> Create a new node of the given type, inside this component. If `name` is supplied the new node will use that name, or the next numbered name if its already in use. opType can be a specific type object, example `waveCHOP`, or it can be a string `'waveCHOP'`. If given an actual instance of a node `n`, these can be accessed via `type(n)` and `n.OPType` respectively.
> 
> An initialization script associated with the operator is run, unless initialize=False.
> The new node is returned.
> 
> * opType - The python OP type for the type of operator you want to create.
> * name - (Optional) The name for the new operator. If there already is an operator with that name, the next numbered name will be used.
> * initialize - (Keyword, Optional) If set to false, then the initialization script for that node won't be run. Most nodes don't do anything to initialize, but some do. For example the Light COMP initializes a network inside itself of SOPs.
> 
> ```
> n.create(waveCHOP)
> w = n.create(boxSOP, 'box12')
> 
> ```
`collapseSelected()`→ `None`:
> Move all selected operators into a new [Base COMP](Base_COMP.html "Base COMP"). Equivalent to right-click on the network background and choosing Collapse Selected.
`copy(OP, name=None, includeDocked=True)`→ `OP`:
> Copy the operator into this component. If name is supplied, the new node will use that name. The new node is returned.
> 
> * OP - The operator to copy. This is not a string, it must be an OP.
> * name - (Keyword, Optional) If provided, the new node will have this name. If there already is an operator with that name, the next numbered name will be used.
> * includeDocked - (Keyword, Optional) When true a copy will include any externally docked operators to the source component.
> 
> ```
> w = n.copy( op('wave1') )
> 
> ```
`copyOPs(listOfOPs)`→ `List`:
> Copy a list of operators into this component.
> 
> This is preferred over multiple single copies, as connections between the operators are preserved.
> A new list with the created operators is returned.
> 
> * listOfOPs - A list containing one or more OPs to be copied.
> 
> ```
> alist = [op('wave1'), op('wave2')]
> n.copyOPs(alist)
> 
> ```
`findChildren(type=None, name=None, path=None, depth=None, maxDepth=None, text=None, comment=None, tags=[], allTags=False, parValue=None, parExpr=None, parName=None, onlyNonDefaults=False, includeUtility=False, key=None)`→ `List of OPs`:
> Return a list of [operators](OP_Class.html "OP Class") matching the specified criteria.
> 
> * type - (Keyword, Optional) Specify the type of OP. Example type=boxSOP
> * name - (Keyword, Optional) Specify the name of the OP. [Pattern Matching](Pattern_Matching.html "Pattern Matching") supported. Example: name='project\*'
> * path - (Keyword, Optional) Specify the path of the OP. [Pattern Matching](Pattern_Matching.html "Pattern Matching") supported. Example: path='\*/pics/\*'
> * depth - (Keyword, Optional) Specify the relative depth of the OP to the calling OP. Children have depth 1, their children have depth 2, etc.
> * maxDepth - (Keyword, Optional) Specify the maximum relative depth of the OP from the calling OP.
> * text - (Keyword, Optional) Specify the DAT contents of the OP. [Pattern Matching](Pattern_Matching.html "Pattern Matching") supported. Example: text='\*import\*'
> * comment - (Keyword, Optional) Specify the OP comment. [Pattern Matching](Pattern_Matching.html "Pattern Matching") supported. Example: comment='\*todo\*'
> * tags - (Keyword, Optional) Specify a list of tags to search. [Pattern Matching](Pattern_Matching.html "Pattern Matching") supported. Example: tags=['\*sequencer\*', '\*interface\*']
> * allTags - (Keyword, Optional) When True, only include OPs where all specified tags are matched.
> * parValue - (Keyword, Optional) Specify the value of any parameters in the OP. [Pattern Matching](Pattern_Matching.html "Pattern Matching") supported. Example: parValue='500'
> * parExpr - (Keyword, Optional) Specify the expression of any parameters in the OP. [Pattern Matching](Pattern_Matching.html "Pattern Matching") supported. Example: parExpr='\*sin\*'
> * parName - (Keyword, Optional) Specify the name of any parameters in the OP. [Pattern Matching](Pattern_Matching.html "Pattern Matching") supported. Example: parName='clone'
> * onlyNonDefaults - (Keyword, Optional) When True, only non default parameters are included.
> * includeUtility - (Keyword, Optional) If specified, controls whether or not [Utility nodes](Network_Utilities__Comments%2c_Network_Boxes%2c_Annotates.html "Network Utilities: Comments, Network Boxes, Annotates") (e.g. Comments) are included in the results.
> * key - (Keyword, Optional) Specify a custom search function.
> 
> ```
> #find all OPs whose name begins with circle
> n.findChildren(name='circle*')
> 
> #find all wide CHOPs
> n.findChildren(type=CHOP, key = lambda x: x.nodeWidth > 200)
> 
> #find all COMPs specifying clones
> n.findChildren(type=COMP, parName='clone', onlyNonDefaults=True)
> 
> ```
`initializeExtensions(index=None)`→ `Extension`:
> Initialize the components [extensions](Extensions.html "Extensions"). To initialize an individual extension, specify its index.
> 
> Returns the compiled extension.
> 
> * index - (Optional) Index to initialize. 0 = first extension, etc.
> 
> ```
> n.initializeExtensions(0) # initialize first extension.
> 
> ```
`loadTox(filepath, unwired=False, pattern=None, password=None)`→ `OP`:
> Load the component from the given file path into this component.
> 
> * filepath - The path and filename of the `.tox` to load.
> * unwired - (Keyword, Optional) If True, the component inputs will remain unwired.
> * pattern - (Keyword, Optional) Can be specified to only load operators within the component that match the pattern. Wildcards are not supported.
> * password - (Keyword, Optional) If specified, decrypts the tox with the password.
`loadByteArray(byteArray, unwired=False, pattern=None, password=None)`→ `OP`:
> Load the component from the given bytearray into this COMP. See .saveByteArray() as a way to generate this byteArray.
> 
> * bytearray - A bytearray containing the component, from a call to saveByteArray().
> * unwired - (Keyword, Optional) If True, the component inputs will remain unwired.
> * pattern - (Keyword, Optional) Can be specified to only load operators within the component that match the pattern. Wildcards are not supported.
> * password - (Keyword, Optional) If specified, decrypts the component with the password."
`reload(filepath, password=None)`→ `None`:
> Reloads the component from the given file path. This will replace its children as well as top level parameters and update flags, node width/height, storage, comments and inputs (but keep original node x,y).
> 
> * filepath - The path and filename of the .tox to load.
> * password - (Keyword, Optional) If specified, decrypts the component with the password."
`resetNetworkView(recurse)`→ `None`:
> Reset the network view such that the network editor will be re-homed upon entering this component.
> 
> * recurse - (Optional) When True, resets network view of all children components as well. Default False.
> 
> ```
> n.resetNetworkView(True) # reset network view of n and all its children.
> 
> ```
`save(filepath, createFolders=False, password=None)`→ `Path`:
> Saves the component to disk. If no path is provided, a default filename is used and the `.tox` is saved to `project.folder`.
> 
> Returns the filename used.
> 
> * filepath - (Optional) The path and filename to save the `.tox` to.
> * createFolders - (Keyword, Optional) If True, it creates the not existent directories provided by the filepath.
> * password - (Keyword, Optional) If specified, encrypts the tox with the password.
> 
> ```
> name = n.save() # save in native tox format with default name
> n.save('output.tox')  # supply name
> n.save('C:/Desktop/myFolder/output.tox', createFolders=True)  # supply name and createFolder flag
> 
> ```
`saveByteArray(password=None)`→ `bytearray`:
> Save the component into a bytearray. The bytearray is the same data that is held in a .tox file. `loadByteArray()` can be used to load the component.
> 
> * password - (Keyword, Optional) If specified, encrypts the tox with the password.
`saveExternalTox(recurse=False, password=None)`→ `int`:
> Save out the contents of any COMP referencing an external .tox
> 
> Returns the number of components saved.
> 
> * recurse - (Keyword, Optional) If set to True, child components are included in the operation.
> * password - (Keyword, Optional) If specified, encrypts the tox with the password.
> 
> ```
> root.saveExternalTox(recurse=True)
> op('geo1').saveExternalTox(recurse=False)
> 
> ```
### Custom Parameters[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Custom Parameters")]
`appendCustomPage(name)`→ `Page`:
> Add a new [page](Page_Class.html "Page Class") of custom parameters. See [Page Class](Page_Class.html "Page Class") for more details. See [Custom Parameters](Custom_Parameters.html "Custom Parameters") for the procedure.
> 
> ```
> n = op('base1')
> page = n.appendCustomPage('Custom1')
> page.appendFloat('X1')
> 
> ```
`destroyCustomPars()`→ `Total`:
> Remove all custom parameters from COMP.
`sortCustomPages(page1, page2, page3...)`→ `None`:
> Reorder custom parameter pages by listing their page names.
> 
> ```
> n = op('base1')
> n.sortCustomPages('Definition','Controls')
> 
> ```
### Privacy[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Privacy")]
`accessPrivateContents(key)`→ `Bool`:
> Gain access to a private component. The component will still be private the next time it is saved or re-opened.
> 
> Returns true when the key is correct, and access is granted. If dongle privacy is being used, no arguments are required.
> 
> * key - (Optional) The existing key phrase. This should resolve to a non-blank string. Not required for dongle privacy.
> 
> ```
> n.accessPrivateContents('secret')
> 
> ```
`addPrivacy(key, developerName=None)`→ `None`:
> Add privacy to a component with the given key.
> 
> Privacy can only be added to components that currently have no privacy. Adding Privacy requires a Pro license.
> 
> * key - The new key phrase. This should resolve to a non-blank string.
> 
> ```
> n.addPrivacy('secret')
> 
> ```
`addPrivacy(firmCode, productCode, developerName=None, developerEmail=None)`→ `None`:
> Add privacy to a component with the given CodeMeter firm code and product code.
> 
> Privacy can only be added to components that currently have no privacy. Adding Privacy requires a Pro license.
> 
> The first bit of the CodeMeter Dongle's Feature Map must be set to enable privacy and add prodcut code as well as to access the private component in edit mode later.
> 
> The private component can be used with any Dongle matching the firm code and product code without the first Feature Map bit set. In this case the component will run in private mode keeping the contents of the component hidden.
> 
> * firmCode - The CodeMeter firm code to use.
> * productCode - The CodeMeter product code to use.
> 
> ```
> n.addPrivacy(10, 4)
> 
> ```
`blockPrivateContents(key)`→ `None`:
> Block access to a private component that was temporarily accessible.
> 
> ```
> n.blockPrivateContents()
> 
> ```
`removePrivacy(key)`→ `Bool`:
> Completely remove privacy from a component.
> 
> Returns true when the key is correct.
> 
> * key - The existing key phrase. This should resolve to a non-blank string.
> 
> ```
> n.removePrivacy('secret')
> 
> ```
### Component Variables[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Component Variables")]
`setVar(name, value)`→ `None`:
> Set a component variable to the specified value.
> 
> * name - The variable name to use.
> * value - The value for this variable.
`unsetVar(name)`→ `None`:
> Unset the specified component variable. This removes the entry from the '`local/set_variables`' table, if found.
> 
> * name - The name of the variable to unset.
`vars(pattern1, pattern2...)`→ `List`:
> Return a list of all component variables in this COMP. Optional name patterns may be specified.
> 
> * pattern - (Optional) The name(s) of variables whose values should be returned. [Pattern Matching](Pattern_Matching.html "Pattern Matching") can be used.
> 
> ```
> a = n.vars()
> a = n.vars('A*', 'B*')
> 
> ```
# OP Class[[edit](https://docs.derivative.ca/index.php?title=Template:ClassInheritance&action=edit&section=T-1 "Edit section: OP Class")]
## Members
### General[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: General")]
`valid` → `bool` **(Read Only)**:
> True if the referenced operator currently exists, False if it has been deleted.
`id` → `int` **(Read Only)**:
> Unique id for the operator. This id can also be passed to the op() and ops() methods. Id's are not consistent when a file is re-opened, and will change if the OP is copied/pasted, changes OP types, deleted/undone. The id will not change if the OP is renamed though. Its data type is integer.
`name` → `str` :
> Get or set the operator name.
`path` → `str` **(Read Only)**:
> Full path to the operator.
`digits` → `int` **(Read Only)**:
> Returns the numeric value of the last consecutive group of digits in the name, or None if not found. The digits can be in the middle of the name if there are none at the end of the name.
`base` → `str` **(Read Only)**:
> Returns the beginning portion of the name occurring before any digits.
`passive` → `bool` **(Read Only)**:
> If true, operator will not cook before its access methods are called. To use a passive version of an operator n, use passive(n).
`curPar` → `td.Par` **(Read Only)**:
> The parameter currently being evaluated. Can be used in a parameter expression to reference itself. An easy way to see this is to put the expression `curPar.name` in any string parameter.
`curBlock` → **(Read Only)**:
> The SequenceBlock of the parameter currently being evaluated. Can be used in a parameter expression to reference itself.
`curSeq` → `Sequence` **(Read Only)**:
> The Sequence of the parameter currently being evaluated. Can be used in a parameter expression to reference itself.
`time` → `OP` **(Read Only)**:
> [Time Component](TimeCOMP_Class.html "TimeCOMP Class") that defines the operator's time reference.
`ext` → `class` **(Read Only)**:
> The object to search for parent [extensions](Extensions.html "Extensions").
> 
> ```
> me.ext.MyClass
> 
> ```
`fileFolder` → `str` **(Read Only)**:
> Returns the folder where this node is saved.
`filePath` → `str` **(Read Only)**:
> Returns the file location of this node.
`mod` → `mod` **(Read Only)**:
> Get a [module on demand](MOD_Class.html "MOD Class") object that searches for DAT modules relative to this operator.
`pages` → `list` **(Read Only)**:
> A list of all built-in pages.
`parGroup` → `tuple` **(Read Only)**:
> An intermediate [parameter collection](ParGroupCollection_Class.html "ParGroupCollection Class") object, from which a specific [parameter group](ParGroup_Class.html "ParGroup Class") can be found.
> 
> ```
> n.parGroup.t
> # or
> n.parGroup['t']
> 
> ```
`par` → `td.Par` **(Read Only)**:
> An intermediate [parameter collection](ParCollection_Class.html "ParCollection Class") object, from which a specific [parameter](Par_Class.html "Par Class") can be found.
> 
> ```
> n.par.tx
> # or
> n.par['tx']
> 
> ```
`builtinPars` → `list or par` **(Read Only)**:
> A list of all [built-in parameters](Par_Class.html "Par Class").
`customParGroups` → `list of parGroups` **(Read Only)**:
> A list of all [ParGroups](ParGroup_Class.html "ParGroup Class"), where a ParGroup is a set of parameters all drawn on the same line of a dialog, sharing the same label.
`customPars` → `list of par` **(Read Only)**:
> A list of all [custom parameters](Par_Class.html "Par Class").
`customPages` → `list` **(Read Only)**:
> A list of all [custom pages](Page_Class.html "Page Class").
`replicator` → `OP or None` **(Read Only)**:
> The [replicatorCOMP](ReplicatorCOMP_Class.html "ReplicatorCOMP Class") that created this operator, if any.
`storage` → `dict` **(Read Only)**:
> [Storage](Storage.html "Storage") is dictionary associated with this operator. Values stored in this dictionary are persistent, and saved with the operator. The dictionary attribute is read only, but not its contents. Its contents may be manipulated directly with methods such as OP.fetch() or OP.store() described below, or examined with an [Examine DAT](Examine_DAT.html "Examine DAT").
`tags` → `list` :
> Get or set a set of user defined strings. [Tags](Tag.html "Tag") can be searched using OP.findChildren() and the [OP Find DAT](OP_Find_DAT.html "OP Find DAT").
> 
> The set is a regular python set, and can be accessed accordingly:
> 
> ```
> n.tags = ['effect', 'image filter']
> n.tags.add('darken')
> 
> ```
`children` → `list` **(Read Only)**:
> A list of [operators](OP_Class.html "OP Class") contained within this operator. Only [component](COMP_Class.html "COMP Class") operators have children, otherwise an empty list is returned.
`numChildren` → `int` **(Read Only)**:
> Returns the number of children contained within the operator. Only [component](COMP_Class.html "COMP Class") operators have children.
`numChildrenRecursive` → `int` **(Read Only)**:
> Returns the number of operators contained recursively within this operator. Only [component](COMP_Class.html "COMP Class") operators have children.
`op` → `OP or None` **(Read Only)**:
> The operator finder object, for accessing operators through paths or shortcuts. **Note:** a version of this method that searches relative to '/' is also in the global [td module](Td_Module.html "Td Module").
> 
> `op(pattern1, pattern2..., includeUtility=False)` → `[OP](OP_Class.html "OP Class") or None`
> 
> > Returns the first OP whose path matches the given pattern, relative to the inside of this operator. Will return None if nothing is found. Multiple patterns may be specified which are all added to the search. Numeric OP ids may also be used.
> > 
> > * `pattern` - Can be string following the [Pattern Matching](Pattern_Matching.html "Pattern Matching") rules, specifying which OP to return, or an integer, which must be an OP Id. Multiple patterns can be given, the first matching OP will be returned.
> > * `includeUtility` **(Optional)** - if True, allow [Utility nodes](Network_Utilities__Comments%2c_Network_Boxes%2c_Annotates.html "Network Utilities: Comments, Network Boxes, Annotates") to be returned. If False, Utility nodes will be ignored.
> > 
> > ```
> > b = op('project1')
> > b = op('foot*', 'hand*') #comma separated
> > b = op('foot* hand*')  #space separated
> > b = op(154)
> > 
> > ```
> 
> `op.shortcut` → `OP`
> 
> > An operator specified with by a [Global OP Shortcut](Global_OP_Shortcut.html "Global OP Shortcut"). If no operator exists an exception is raised. These shortcuts are global, and must be unique. That is, cutting and pasting an operator with a Global OP Shortcut specified will lead to a name conflict. One shortcut must be renamed in that case. Furthermore, only components can be given Global OP Shortcuts.
> > 
> > * `shortcut` - Corresponds to the Global OP Shortcut parameter specified in the target operator.
> > ```
> > b = op.Videoplayer
> > 
> > ```
> > 
> > To list all Global OP Shortcuts:
> > 
> > ```
> > for x in op:
> > 	print(x)
> > 
> > ```
`opex` → `OP` **(Read Only)**:
> An operator finder object, for accessing operators through paths or shortcuts. Works like the op() shortcut method, except it will raise an exception if it fails to find the node instead of returning None as op() does. This is now the recommended way to get nodes in parameter expressions, as the error will be more useful than, for example, `NoneType has no attribute "par"`, that is often seen when using op(). **Note:** a version of this method that searches relative to '/' is also in the global [td module](Td_Module.html "Td Module").
> 
> `op(pattern1, pattern2..., includeUtility=False)` → `[OP](OP_Class.html "OP Class")`
> 
> > Returns the first OP whose path matches the given pattern, relative to the inside of this operator. Will return None if nothing is found. Multiple patterns may be specified which are all added to the search. Numeric OP ids may also be used.
> > 
> > * `pattern` - Can be string following the [Pattern Matching](Pattern_Matching.html "Pattern Matching") rules, specifying which OP to return, or an integer, which must be an OP Id. Multiple patterns can be given, the first matching OP will be returned.
> > * `includeUtility` **(Optional)** - if True, allow [Utility nodes](Network_Utilities__Comments%2c_Network_Boxes%2c_Annotates.html "Network Utilities: Comments, Network Boxes, Annotates") to be returned. If False, Utility operators will be ignored.
`parent` → `Shortcut` **(Read Only)**:
> The [Parent Shortcut](Parent_Shortcut.html "Parent Shortcut") object, for accessing parent components through indices or shortcuts.
> 
> **Note:** *a version of this method that searches relative to the current operator is also in the global [td module](Td_Module.html "Td Module").*
> 
> `parent(n)` → `OP or None`
> 
> > The nth parent of this operator. If n not specified, returns the parent. If n = 2, returns the parent of the parent, etc. If no parent exists at that level, None is returned.
> > 
> > * n - (Optional) n is the number of levels up to climb. When n = 1 it will return the operator's parent.
> > 
> > ```
> > p = parent(2) #grandfather
> > 
> > ```
> 
> `parent.shortcut` → `OP`
> 
> > A parent component specified with a shortcut. If no parent exists an exception is raised.
> > 
> > * shortcut - Corresponds to the [Parent Shortcut](Parent_Shortcut.html "Parent Shortcut") parameter specified in the target parent.
> > 
> > ```
> > n = parent.Videoplayer
> > 
> > ```
> > 
> > See also Parent Shortcut for more examples.
`iop` → `OP` **(Read Only)**:
> The Internal Operator Shortcut object, for accessing internal shortcuts. See also [Internal Operators](Internal_Operators.html "Internal Operators").
> **Note:** a version of this method that searches relative to the current operator is also in the global [td Module](Td_Module.html "Td Module").
`ipar` → `ParCollection` **(Read Only)**:
> The Internal Operator Parameter Shortcut object, for accessing internal shortcuts. See also [Internal Parameters](Internal_Parameters.html "Internal Parameters").
> **Note:** a version of this method that searches relative to the current operator is also in the global [td Module](Td_Module.html "Td Module").
`currentPage` → `[Page](Page_Class.html "Page Class")` :
> Get or set the currently displayed parameter page. It can be set by setting it to another page or a string label.
> 
> ```
> n.currentPage = 'Common'
> 
> ```
### Common Flags[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Common Flags")]
The following methods get or set specific operator [Flags](Flag.html "Flag"). Note specific operators may contain other flags not in this section.
  

`activeViewer` → `bool` :
> Get or set [Viewer Active Flag](Viewer_Active_Flag.html "Viewer Active Flag").
`allowCooking` → `bool` :
> Get or set [Cooking Flag](Cooking_Flag.html "Cooking Flag"). Only COMPs can disable this flag.
`bypass` → `bool` :
> Get or set [Bypass Flag](Bypass_Flag.html "Bypass Flag").
`cloneImmune` → `bool` :
> Get or set [Clone Immune Flag](Immune_Flag.html "Immune Flag").
`current` → `bool` :
> Get or set [Current Flag](Current_Flag.html "Current Flag").
`display` → `bool` :
> Get or set [Display Flag](Display_Flag.html "Display Flag").
`expose` → `bool` :
> Get or set the [Expose Flag](Expose_Flag.html "Expose Flag") which hides a node from view in a network.
`lock` → `bool` :
> Get or set [Lock Flag](Lock_Flag.html "Lock Flag").
`selected` → `bool` :
> Get or set [Selected Flag](Selected_Flag.html "Selected Flag"). This controls if the node is part of the network selection. (yellow box around it).
`seq` → **(Read Only)**:
> An intermediate sequence collection object, from which a specific sequence group can be found.
> 
> ```
> n.seq.Color #raises Exception if not found.
> # or
> n.seq['Color'] #returns None if not found.
> 
> ```
`python` → `bool` :
> Get or set parameter expression language as python.
`render` → `bool` :
> Get or set [Render Flag](Render_Flag.html "Render Flag").
`showCustomOnly` → `bool` :
> Get or set the Show Custom Only Flag which controls whether or not non custom parameters are display in [parameter dialogs](Parameter_Dialog.html "Parameter Dialog").
`showDocked` → `bool` :
> Get or set [Show Docked Flag](Docking.html "Docking"). This controls whether this node is visible or hidden when it is docked to another node.
`viewer` → `bool` :
> Get or set [Viewer Flag](Viewer_Flag.html "Viewer Flag").
### Appearance[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Appearance")]
`color` → `tuple(r, g, b)` :
> Get or set color value, expressed as a 3-tuple, representing its red, green, blue values. To convert between color spaces, use the built in colorsys module.
`comment` → `str` :
> Get or set comment string.
`nodeHeight` → `int` :
> Get or set node height, expressed in [network editor](NetworkEditor_Class.html "NetworkEditor Class") units.
`nodeWidth` → `int` :
> Get or set node width, expressed in [network editor](NetworkEditor_Class.html "NetworkEditor Class") units.
`nodeX` → `int` :
> Get or set node X value, expressed in [network editor](NetworkEditor_Class.html "NetworkEditor Class") units, measured from its left edge.
`nodeY` → `int` :
> Get or set node Y value, expressed in [network editor](NetworkEditor_Class.html "NetworkEditor Class") units, measured from its bottom edge.
`nodeCenterX` → `int` :
> Get or set node X value, expressed in [network editor](NetworkEditor_Class.html "NetworkEditor Class") units, measured from its center.
`nodeCenterY` → `int` :
> Get or set node Y value, expressed in [network editor](NetworkEditor_Class.html "NetworkEditor Class") units, measured from its center.
`dock` → `OP` :
> Get or set the [operator](OP_Class.html "OP Class") this operator is docked to. To clear docking, set this member to None.
`docked` → `list` **(Read Only)**:
> The (possibly empty) list of [operators](OP_Class.html "OP Class") docked to this node.
### Connection[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Connection")]
See also the `OP.parent` methods. To connect components together see [COMP\_Class#Connection](COMP_Class.html#Connection "COMP Class") section.
  

`inputs` → `list` **(Read Only)**:
> List of input [operators](OP_Class.html "OP Class") (via left side connectors) to this operator. To get the number of inputs, use len(OP.inputs).
`outputs` → `list` **(Read Only)**:
> List of output [operators](OP_Class.html "OP Class") (via right side connectors) from this operator.
`inputConnectors` → `list` **(Read Only)**:
> List of input [connectors](Connector_Class.html "Connector Class") (on the left side) associated with this operator.
`outputConnectors` → `list` **(Read Only)**:
> List of output [connectors](Connector_Class.html "Connector Class") (on the right side) associated with this operator.
### Cook Information[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Cook Information")]
`cookFrame` → `float` **(Read Only)**:
> Last frame at which this operator cooked.
`cookTime` → `float` **(Read Only)**:
> **Deprecated** Duration of the last measured cook (in milliseconds).
`cpuCookTime` → `float` **(Read Only)**:
> Duration of the last measured cook in CPU time (in milliseconds).
`cookAbsFrame` → `float` **(Read Only)**:
> Last absolute frame at which this operator cooked.
`cookStartTime` → `float` **(Read Only)**:
> Last offset from frame start at which this operator cook began, expressed in milliseconds.
`cookEndTime` → `float` **(Read Only)**:
> Last offset from frame start at which this operator cook ended, expressed in milliseconds. Other operators may have cooked between the start and end time. See the cookTime member for this operator's specific cook duration.
`cookedThisFrame` → `bool` **(Read Only)**:
> True when this operator has cooked this frame.
`cookedPreviousFrame` → `bool` **(Read Only)**:
> True when this operator has cooked the previous frame.
`childrenCookTime` → `float` **(Read Only)**:
> **Deprecated** The total accumulated cook time of all children of this operator during the last frame. Zero if the operator is not a [COMP](COMP_Class.html "COMP Class") and/or has no children.
`childrenCPUCookTime` → `float` **(Read Only)**:
> The total accumulated cook time of all children of this operator during the last frame. Zero if the operator is not a [COMP](COMP_Class.html "COMP Class") and/or has no children.
`childrenCookAbsFrame` → `float` **(Read Only)**:
> **Deprecated** The absolute frame on which childrenCookTime is based.
`childrenCPUCookAbsFrame` → `float` **(Read Only)**:
> The absolute frame on which childrenCPUCookTime is based.
`gpuCookTime` → `float` **(Read Only)**:
> Duration of GPU operations during the last measured cook (in milliseconds).
`childrenGPUCookTime` → `float` **(Read Only)**:
> The total accumulated GPU cook time of all children of this operator during the last frame. Zero if the operator is not a COMP and/or has no children.
`childrenGPUCookAbsFrame` → `float` **(Read Only)**:
> The absolute frame on which childrenGPUCookTime is based.
`totalCooks` → `int` **(Read Only)**:
> Number of times the operator has cooked.
`cpuMemory` → `int` **(Read Only)**:
> The approximate amount of CPU memory this Operator is using, in bytes.
`gpuMemory` → `int` **(Read Only)**:
> The amount of GPU memory this OP is using, in bytes.
### Type[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Type")]
`type` → `str` **(Read Only)**:
> Operator type as a string. Example: 'oscin'.
`subType` → `str` **(Read Only)**:
> Operator subtype. Currently only implemented for [components](Component.html "Component"). May be one of: 'panel', 'object', or empty string in the case of base components.
`OPType` → `str` **(Read Only)**:
> Python operator class type, as a string. Example: 'oscinCHOP'. Can be used with COMP.create() method.
`label` → `str` **(Read Only)**:
> Operator type label. Example: 'OSC In'.
`icon` → `str` **(Read Only)**:
> Get the letters used to create the operator's icon.
`family` → `str` **(Read Only)**:
> Operator family. Example: CHOP. Use the global dictionary families for a list of each operator type.
`isFilter` → `bool` **(Read Only)**:
> True if operator is a filter, false if it is a generator.
`minInputs` → `int` **(Read Only)**:
> Minimum number of inputs to the operator.
`maxInputs` → `int` **(Read Only)**:
> Maximum number of inputs to the operator.
`isMultiInputs` → `bool` **(Read Only)**:
> True if inputs are ordered, false otherwise. Operators with an arbitrary number of inputs have unordered inputs, example [Merge CHOP](Merge_CHOP.html "Merge CHOP").
`visibleLevel` → `int` **(Read Only)**:
> Visibility level of the operator. For example, expert operators have visibility level 1, regular operators have visibility level 0.
`isBase` → `bool` **(Read Only)**:
> True if the operator is a Base (miscellaneous) [component](Component.html "Component").
`isCHOP` → `bool` **(Read Only)**:
> True if the operator is a [CHOP](CHOP.html "CHOP").
`isCOMP` → `bool` **(Read Only)**:
> True if the operator is a [component](Component.html "Component").
`isDAT` → `bool` **(Read Only)**:
> True if the operator is a [DAT](DAT.html "DAT").
`isMAT` → `bool` **(Read Only)**:
> True if the operator is a [Material](MAT.html "MAT").
`isObject` → `bool` **(Read Only)**:
> True if the operator is an [object](Object.html "Object").
`isPanel` → `bool` **(Read Only)**:
> True if the operator is a [Panel](Panel.html "Panel").
`isSOP` → `bool` **(Read Only)**:
> True if the operator is a [SOP](SOP.html "SOP").
`isTOP` → `bool` **(Read Only)**:
> True if the operators is a [TOP](TOP.html "TOP").
`licenseType` → `str` **(Read Only)**:
> Type of [License](License_Class.html "License Class") required for the operator.
## Methods
### General[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: General")]
**NOTE**: `create()`, `copy()` and `copyOPs()` is done by the parent operator (a component). For more information see [COMP.create, COMP.copy and COMP.copyOPs methods](COMP_Class.html#Methods "COMP Class").
  

`pars(pattern)`→ `list`:
> Returns a (possibly empty) list of [parameter objects](Par_Class.html "Par Class") that match the pattern.
> 
> * pattern - Is a string following the [Pattern Matching](Pattern_Matching.html "Pattern Matching") rules, specifying which parameters to return.
> 
> ```
> newlist = op('geo1').pars('t?', 'r?', 's?') #translate/rotate/scale parameters
> 
> ```
> 
> Note: If searching for a single parameter given a name, it's much more efficient to use the subscript operator. For example:
> 
> ```
> name = 'MyName1'
> op('geo1').par[name]
> 
> ```
`cook(force=False, recurse=False, includeUtility=False)`→ `None`:
> Cook the contents of the operator if required.
> 
> * force - (Keyword, Optional) If True, the operator will always cook, even if it wouldn't under normal circumstances.
> * recurse - (Keyword, Optional) If True, all children and sub-children of the operator will be cooked.
> * includeUtility - (Keyword, Optional) If specified, controls whether or not utility components (eg Comments) are included in the results.
`copyParameters(OP, custom=True, builtin=True)`→ `None`:
> Copy all of the parameters from the specified [operator](OP_Class.html "OP Class"). Both operators should be the same type.
> 
> * OP - The operator to copy.
> * custom - (Keyword, Optional) When True, custom parameters will be copied.
> * builtin - (Keyword, Optional) When True, built in parameters will be copied.
> 
> ```
> op('geo1').copyParameters( op('geo2') )
> 
> ```
`changeType(OPtype)`→ `OP`:
> Change referenced operator to a new operator type. After this call, this OP object should no longer be referenced. Instead use the returned OP object.
> 
> * OPtype - The python class name of the operator type you want to change this operator to. This is not a string, but instead is a class defined in the global [td module](Td_Module.html "Td Module").
> 
> ```
> n = op('wave1').changeType(nullCHOP) #changes 'wave1' into a Null CHOP
> n = op('text1').changeType(tcpipDAT) #changes 'text1' operator into a TCPIP DAT
> 
> ```
`dependenciesTo(OP)`→ `list`:
> Returns a (possibly empty) list of operator dependency paths between this operator and the specified operator. Multiple paths may be found.
`evalExpression(str)`→ `value`:
> Evaluate the expression from the context of this OP. Can be used to evaluate arbitrary snippets of code from arbitrary locations.
> 
> * str - The expression to evaluate.
> 
> ```
> op('wave1').evalExpression('me.digits')  #returns 1
> 
> ```
> 
> If the expression already resides in a parameter, use that parameters [evalExpression()](Par_Class.html "Par Class") method instead.
`destroy()`→ `None`:
> Destroy the operator referenced by this OP. An exception will be raised if the OP's operator has already been destroyed.
`var(name, search=True)`→ `str`:
> Evaluate a [variable](Variables.html "Variables"). This will return the empty string, if not found. Most information obtained from variables (except for Root and Component variables) are accessible through other means in Python, usually in the global [td module](Td_Module.html "Td Module").
> 
> * name - The variable name to search for.
> * search - (Keyword, Optional) If set to True (which is default) the operator hierarchy is searched until a variable matching that name is found. If false, the search is constrained to the operator.
`openMenu(x=None, y=None)`→ `None`:
> Open a node menu for the operator at x, y. Opens at mouse if x & y are not specified.
> 
> * x - (Keyword, Optional) The X coordinate of the menu, measured in screen pixels.
> * y - (Keyword, Optional) The Y coordinate of the menu, measured in screen pixels.
`relativePath(OP)`→ `str`:
> Returns the relative path from this operator to the OP that is passed as the argument. See OP.shortcutPath for a version using expressions.
`setInputs(listOfOPs)`→ `None`:
> Set all the operator inputs to the specified list.
> 
> * listOfOPs - A list containing one or more OPs. Entries in the list can be None to disconnect specific inputs. An empty list disconnects all inputs.
`shortcutPath(OP, toParName=None)`→ `str`:
> Returns an expression from this operator to the OP that is passed as the argument. See OP.relativePath for a version using relative path constants.
> 
> * toParName - (Keyword, Optional) Return an expression to this parameter instead of its operator.
`ops(pattern1, pattern2.., includeUtility=False)`→ `list of OPs`:
> Returns a (possibly empty) list of OPs that match the patterns, relative to the inside of this OP.
> 
> Multiple patterns may be provided. Numeric OP ids may also be used.
> 
> * `pattern` - Can be string following the [Pattern Matching](Pattern_Matching.html "Pattern Matching") rules, specifying which OPs to return, or an integer, which must be an OP Id. Multiple patterns can be given and all matched OPs will be returned.
> * `includeUtility` - (Keyword, Optional) If specified, controls whether or not utility components (eg Comments) are included in the results.
> 
> **Note:** a version of this method that searches relative to '/' is also in the global [td module](Td_Module.html "Td Module").
> 
> ```
> newlist = n.ops('arm*', 'leg*', 'leg5/foot*')
> 
> ```
`resetPars(parNames='*', parGroupNames='*', pageNames='*', includeBuiltin=True, includeCustom=True)`→ `bool`:
> Resets the specified parameters in the operator.
> 
> Returns true if anything was changed.
> 
> * parNames (Keyword, Optional) - Specify parameters by Par name.
> * parGroupNames (Keyword, Optional) - Specify parameters by ParGroup name.
> * pageNames (Keyword, Optional) - Specify parameters by page name.
> * includeBuiltin (Keyword, Optional) - Include builtin parameters.
> * includeCustom (Keyword, Optional) - Include custom parameters.
> 
> ```
> op('player').resetPars(includeBuiltin=False) # only reset custom
> 
> ```
### Errors[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Errors")]
`addScriptError(msg)`→ `None`:
> Adds a script error to a node.
> 
> * msg - The error to add.
`addError(msg)`→ `None`:
> Adds an error to an operator. Only valid if added while the operator is cooking. (Example Script SOP, CHOP, DAT).
> 
> * msg - The error to add.
`addWarning(msg)`→ `None`:
> Adds a warning to an operator. Only valid if added while the operator is cooking. (Example Script SOP, CHOP, DAT).
> 
> * msg - The error to add.
`errors(recurse=False)`→ `str`:
> Get error messages associated with this OP.
> 
> * recurse - Get errors in any children or subchildren as well.
`warnings(recurse=False)`→ `str`:
> Get warning messages associated with this OP.
> 
> * recurse - Get warnings in any children or subchildren as well.
`scriptErrors(recurse=False)`→ `str`:
> Get script error messages associated with this OP.
> 
> * recurse - Get errors in any children or subchildren as well.
`clearScriptErrors(recurse=False, error='*')`→ `None`:
> Clear any errors generated during script execution. These may be generated during execution of DATs, Script Nodes, Replicator COMP callbacks, etc.
> 
> * recurse - Clear script errors in any children or subchildren as well.
> * error - Pattern to match when clearing errors
> 
> ```
> op('/project1').clearScriptErrors(recurse=True)
> 
> ```
`childrenCPUMemory()`→ `int`:
> Returns the total CPU memory usage for all the children from this COMP.
`childrenGPUMemory()`→ `int`:
> Returns the total GPU memory usage for all the children from this COMP.
### Appearance[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Appearance")]
`resetNodeSize()`→ `None`:
> Reset the node tile size to its default width and height.
### Viewers[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Viewers")]
`closeViewer(topMost=False)`→ `None`:
> Close the floating content viewers of the OP.
> 
> * topMost - (Keyword, Optional) If True, any viewer window containing any parent of this OP is closed instead.
> 
> ```
> op('wave1').closeViewer()
> op('wave1').closeViewer(topMost=True) # any viewer that contains 'wave1' will be closed.
> 
> ```
`openViewer(unique=False, borders=True)`→ `None`:
> Open a floating content viewer for the OP.
> 
> * unique - (Keyword, Optional) If False, any existing viewer for this OP will be re-used and popped to the foreground. If unique is True, a new window is created each time instead.
> * borders - (Keyword, Optional) If true, the floating window containing the viewer will have borders.
> 
> ```
> op('geo1').openViewer(unique=True, borders=False) # opens a new borderless viewer window for 'geo1'
> 
> ```
`resetViewer(recurse=False)`→ `None`:
> Reset the OP content viewer to default view settings.
> 
> * recurse - (Keyword, Optional) If True, this is done for all children and sub-children as well.
> 
> ```
> op('/').resetViewer(recurse=True) # reset the viewer for all operators in the entire file.
> 
> ```
`openParameters()`→ `None`:
> Open a floating dialog containing the operator parameters.
### Storage[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Storage")]
[Storage](Storage.html "Storage") can be used to keep data within components. Storage is implemented as one python dictionary per node.
When an element of storage is changed by using `n.store()` as explained below, expressions and operators that depend on it will automatically re-cook. It is retrieved with the `n.fetch()` function.
Storage is saved in `.toe` and `.tox` files and restored on startup.
Storage can hold any python object type (not just strings as in Tscript variables). Storage elements can also have optional startup values, specified separately. Use these startup values for example, to avoid saving and loading some session specific object, and instead save or load a well defined object like `None`.
See the [Examine DAT](Examine_DAT.html "Examine DAT") for procedurally viewing the contents of storage.
  

`fetch(key, default, search=True, storeDefault=False)`→ `value`:
> Return an object from the OP storage dictionary. If the item is not found, and a default it supplied, it will be returned instead.
> 
> * key - The name of the entry to retrieve.
> * default - (Optional) If provided and no item is found then the passed value/object is returned instead.
> * storeDefault - (Keyword, Optional) If True, and the key is not found, the default is stored as well.
> * search - (Keyword, Optional) If True, the parent of each OP is searched recursively until a match is found
> 
> ```
> v = n.fetch('sales5', 0.0)
> 
> ```
`fetchOwner(key)`→ `OP`:
> Return the operator which contains the stored key, or None if not found.
> 
> * key - The key to the stored entry you are looking for.
> 
> ```
> who = n.fetchOwner('sales5') #find the OP that has a storage entry called 'sales5'
> 
> ```
`store(key, value)`→ `value`:
> Add the key/value pair to the OP's storage dictionary, or replace it if it already exists. If this value is not intended to be saved and loaded in the toe file, it can be be given an alternate value for saving and loading, by using the method storeStartupValue described below.
> 
> * key - A string name for the storage entry. Use this name to retrieve the value using fetch().
> * value - The value/object to store.
> 
> ```
> n.store('sales5', 34.5) # stores a floating point value 34.5.
> n.store('moviebank', op('/project1/movies')) # stores an OP for easy access later on.
> 
> ```
`unstore(keys1, keys2..)`→ `None`:
> For key, remove it from the OP's storage dictionary. Pattern Matching is supported as well.
> 
> * keys - The name or pattern defining which key/value pairs to remove from the storage dictionary.
> 
> ```
> n.unstore('sales*') # removes all entries from this OPs storage that start with 'sales'
> 
> ```
`storeStartupValue(key, value)`→ `None`:
> Add the key/value pair to the OP's storage startup dictionary. The storage element will take on this value when the file starts up.
> 
> * key - A string name for the storage startup entry.
> * value - The startup value/object to store.
> 
> ```
> n.storeStartupValue('sales5', 1) # 'sales5' will have a value of 1 when the file starts up.
> 
> ```
`unstoreStartupValue(keys1, keys2..)`→ `None`:
> For key, remove it from the OP's storage startup dictionary. Pattern Matching is supported as well. This does not affect the stored value, just its startup value.
> 
> * keys - The name or pattern defining which key/value pairs to remove from the storage startup dictionary.
> 
> ```
> n.unstoreStartupValue('sales*') # removes all entries from this OPs storage startup that start with 'sales'
> 
> ```
### Miscellaneous[[edit](https://docs.derivative.ca/index.php?title=Template:SubSection&action=edit&section=T-1 "Edit section: Miscellaneous")]
`__getstate__()`→ `dict`:
> Returns a dictionary with persistent data about the object suitable for pickling and deep copies.
`__setstate__()`→ `dict`:
> Reads the dictionary to update persistent details about the object, suitable for unpickling and deep copies.
TouchDesigner Build: Latest\nwikieditorwikieditor2021.100002018.28070before 2018.28070
An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

A custom interactive control panel built within TouchDesigner. Panels are created using [Panel Components](Panel_Component.html "Panel Component").

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Lets you embed files inside a `[.tox](-2.html ".tox")` or `[.toe](.html ".toe")` file. Operators like the Movie File In TOP that read regular files can also read the embedded VFS files using a `vfs:` syntax.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Privacy of TouchDesigner Components (`.tox` files) or Projects (`.toe` files) is the protection of networks that enables them to be used but not be visible or editable.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

TouchDesigner Component file, the file type used to save a [Component](Component.html "Component") of your TouchDesigner project.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

A ParGroup is a group of related parameters that you can set and get as a whole instead of its individual parameters.

A name for a component that is accessible from any node in a project, which can be declared in a component's Global Operator Shortcut parameter.

Operator shortcuts are Python objects that return operators (or sometimes parameters). These include [Parent Shortcuts](Parent_Shortcut.html "Parent Shortcut") for accessing a component from within that component, and [Global OP Shortcuts](Global_OP_Shortcut.html "Global OP Shortcut") that access a unique component from anywhere in TouchDesigner.

A Parent Shortcut is a parameter on a component that contains a name that you can use anywhere inside the component to refer to that component using the syntax `parent.Name`, for example `parent.Effect.width` to obtain panel width.

Indicator of certain states of an operator (bypass, display, lock, viewer active).

To re-compute the output data of the [Operators](Operator.html "Operator"). An operator cooks when (1) its inputs change, (2) its [Parameters](Parameter.html "Parameter") change, (3) when the timeline moves forward in some cases, or (4) [Scripting](Script.html "Script") commands are run on the node. When the operator is a [Panel Component](Panel_Component.html "Panel Component"), it also cooks when a user interacts with it. When an operator cooks, it usually causes operators connected to its output to re-cook. When TouchDesigner draws the screen, it re-cooks all the [Dependencies](Dependency.html "Dependency") - the necessary operators in all [Networks](Network.html "Network"), contributing to a frame's total "cook time".

TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.

A set of commands located in a Text DAT that are triggered to run under certain conditions. There are two scripting languages in TouchDesigner: [Python](Python.html "Python") and the original [Tscript](Tscript.html "Tscript"). Scripts and single-line commands can also be run in the [Textport](Textport.html "Textport").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Creates copies of a component, one for every row in a table or using a Number of Replicants parameter - it is the "for-loop" of operators. Unlike [Clone](Clone.html "Clone"), it automatically creates copies of a master component.

Storage is a python dictionary in each operator, where users can store and fetch extra data.

TOuch Environment file, the file type used by TouchDesigner to save your entire project.

TouchDesigner's original built-in Command scripting language prior to [Python](Python.html "Python").

Matching names using wildcard characters and bracketing. Useful in "[Select](Select_CHOP.html "Select CHOP")" type parameters to select multiple operators, paths, channels, etc.

Retrieved from "<https://docs.derivative.ca/index.php?title=PanelCOMP_Class&oldid=31605>"
[Category](Special_Categories.html "Special:Categories"):
* [Python Reference](Category_Python_Reference.html "Category:Python Reference")