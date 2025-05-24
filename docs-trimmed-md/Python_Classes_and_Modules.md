

# Python_Classes_and_Modules

Python Classes and Modules - Derivative




# Python Classes and Modules
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Contents
* [1 Operator Related Classes](#Operator_Related_Classes)
* [2 Helper Classes](#Helper_Classes)
* [3 Standard Python Modules](#Standard_Python_Modules)
* [4 TouchDesigner Utility Modules and Python Utilities](#TouchDesigner_Utility_Modules_and_Python_Utilities)
* [5 3rd Party Packages](#3rd_Party_Packages)
* [6 Installing Custom Packages and Modules](#Installing_Custom_Packages_and_Modules)
The following list of important Python classes and modules is roughly grouped together by subject.
[Python Reference](Category_Python_Reference.html "Category:Python Reference") has an alphabetical list of all TouchDesigner Python pages on this wiki.
### Operator Related Classes[[edit](https://docs.derivative.ca/index.php?title=Python_Classes_and_Modules&action=edit&section=1 "Edit section: Operator Related Classes")]
The following classes are Python interfaces for operators and objects that operators use. Individual operator classes (e.g. [TextTOP Class](TextTOP_Class.html "TextTOP Class") and [RampTOP Class](RampTOP_Class.html "RampTOP Class")) are not listed but do exist in the [`td` module](Td_Module.html "Td Module"), and links to each can be found [here](Category_Python_Reference.html "Category:Python Reference") or by clicking on the Python Help button in their [parameter dialog](Parameter_Dialog.html "Parameter Dialog"). These classes are found in the [td module](Td_Module.html "Td Module") so do not need to be imported.
* **[OP Class](OP_Class.html "OP Class")** - a TouchDesigner [operator](Operator.html "Operator").
  + **[Connector Class](Connector_Class.html "Connector Class")** - a wire connector for an OP. Lists of these can be found in `OP.inputConnectors` and `OP.outputConnectors`. Components also have `COMP.inputCOMPConnectors` and `COMP.outputCOMPConnectors`.
  + **[Page Class](Page_Class.html "Page Class")** - a parameter page. Lists of these can be found in `OP.pages` and, on components and script operators, `OP.customPages`.
  + **[ParCollection Class](ParCollection_Class.html "ParCollection Class")** (`OP.par`) - holds all the parameters for an OP.
    - **[Par Class](Par_Class.html "Par Class")** - an individual [parameter](Parameter.html "Parameter").
  + **[ParGroupCollection Class](ParGroupCollection_Class.html "ParGroupCollection Class")** (`OP.par`) - holds all the parameter groups for an OP.
    - **[ParGroup Class](ParGroup_Class.html "ParGroup Class")** - an individual [parameter group](ParGroup_Class.html "ParGroup Class").
  + **[SequenceCollection Class](SequenceCollection_Class.html "SequenceCollection Class")** (`OP.seq`) - holds all the sequences for an OP.
    - **[Sequence Class](Sequence_Class.html "Sequence Class")** - describes and controls a set of sequential parameters. Sequential parameters will have a reference to one of these objects in their `sequence` member.
      * **[SequenceBlock Class](SequenceBlock_Class.html "SequenceBlock Class")** - used to access the parGroups of a specific block (set of parGroups) in a sequence.
  + **[CHOP Class](CHOP_Class.html "CHOP Class")** - subclass of OPs defining [CHOP](CHOP.html "CHOP") operators.
    - **[Channel Class](Channel_Class.html "Channel Class")** - a [channel](Channel.html "Channel") object. Accessed through a CHOP index or other CHOP members such as `chan`, `chans` etc.
    - **[Segment Class](Segment_Class.html "Segment Class")** - describes a single segment from a [Timer CHOP](Timer_CHOP.html "Timer CHOP").
  + **[COMP Class](COMP_Class.html "COMP Class")** - a subclass of OPs defining [component](Component.html "Component") operators.
    - **[ObjectCOMP Class](ObjectCOMP_Class.html "ObjectCOMP Class")** - a subclass of COMPs defining [Objects](Object.html "Object"), used to create and render 3D scenes.
    - **[PanelCOMP Class](PanelCOMP_Class.html "PanelCOMP Class")** - a subclass of COMPS defining [Panel Components](Panel_Component.html "Panel Component"), used to create 2D UI elements.
      * **[Panel Class](Panel_Class.html "Panel Class")** - a member of panelCOMPs containing all associated [panel values](Panel_Value.html "Panel Value"). Accessed through `panelCOMP.panel`.
        + **[PanelValue Class](PanelValue_Class.html "PanelValue Class")** - individual [panel values](Panel_Value.html "Panel Value"). Accessed through the `panel` member of panelCOMPS and also in callbacks in the [Panel Execute DAT](Panel_Execute_DAT.html "Panel Execute DAT").
      * **[ListAttributes Class](ListAttributes_Class.html "ListAttributes Class")** - a collection of [list attributes](ListAttribute_Class.html "ListAttribute Class") used in a [ListCOMP](ListCOMP_Class.html "ListCOMP Class").
        + **[ListAttribute Class](ListAttribute_Class.html "ListAttribute Class")** - contains attributes defining a cell in a [ListCOMP](ListCOMP_Class.html "ListCOMP Class").
      * **[Actors Class](Actors_Class.html "Actors Class")** - describes the set of all Actor COMPs used by the Bullet Solver COMP and Nvidia Flex Solver COMP. used in a [BulletsolverCOMP](BulletsolverCOMP_Class.html "BulletsolverCOMP Class") or [flexsolverCOMP](FlexsolverCOMP_Class.html "FlexsolverCOMP Class").
      * **[Bodies Class](Bodies_Class.html "Bodies Class")** - a collection of [bodies](Body_Class.html "Body Class") used in an [ActorCOMP](ActorCOMP_Class.html "ActorCOMP Class").
        + **[Body Class](Body_Class.html "Body Class")** - a single body (physics object) used in an [ActorCOMP](ActorCOMP_Class.html "ActorCOMP Class").
    - **[VFS Class](VFS_Class.html "VFS Class")** - a COMP's Virtual File System
      * **[VFSFile Class](VFSFile_Class.html "VFSFile Class")** - a virtual file contained within a Virtual File System.
  + **[DAT Class](DAT_Class.html "DAT Class")** - a subclass of OPs defining [DAT](DAT.html "DAT") operators.
    - **[Cell Class](Cell_Class.html "Cell Class")** - defines an individual cell of a [DAT](DAT.html "DAT") table.
    - **[Peer Class](Peer_Class.html "Peer Class")** - describes the network connection originating a message in the callback functions found in [oscinDAT](OSC_In_DAT.html "OSC In DAT"), [tcpipDAT](TCP/IP_DAT.html "TCP/IP DAT"), [udpinDAT](UDP_In_DAT.html "UDP In DAT"), [udtinDAT](UDT_In_DAT.html "UDT In DAT").
  + **[MAT Class](MAT_Class.html "MAT Class")** - a subclass of OPs defining [MAT](MAT.html "MAT") operators.
  + **[SOP Class](SOP_Class.html "SOP Class")** - a subclass of OPs defining [SOP](SOP.html "SOP") operators.
    - **[Attributes Class](Attributes_Class.html "Attributes Class")** - a collection of SOP [attributes](Attribute.html "Attribute")
      * **[Attribute Class](Attribute_Class.html "Attribute Class")** - information about an entity such as its color, velocity, normal, and so on.
        + **[AttributeData Class](AttributeData_Class.html "AttributeData Class")** - contains specific geometric Attribute values, associated with a Prim Class, Point Class, or Vertex Class.
    - **[Group Class](Group_Class.html "Group Class")** - describes groups lists of Prim Class or Point Class.
    - **[Points Class](Points_Class.html "Points Class")** - a collection of [points](Point_Class.html "Point Class").
      * **[Point Class](Point_Class.html "Point Class")** - a single geometry [point](Point.html "Point").
        + **[InputPoint Class](InputPoint_Class.html "InputPoint Class")** - a special point object used in [Point SOP](Point_SOP.html "Point SOP") parameters.
    - **[Prims Class](Prims_Class.html "Prims Class")** - a collection of [primitives](Prim_Class.html "Prim Class").
      * **[Prim Class](Prim_Class.html "Prim Class")** - a single geometry [primitive](Primitive.html "Primitive").
        + **[Poly Class](Poly_Class.html "Poly Class")** - a subclass of Prim defining a geometry [polygon](Polygon.html "Polygon").
        + **[Mesh Class](Mesh_Class.html "Mesh Class")** - a subclass of Prim defining a geometry [mesh](Mesh.html "Mesh").
        + **[Bezier Class](Bezier_Class.html "Bezier Class")** - a subclass of Prim defining a set of Bezier curves.
        + **[Vertex Class](Vertex_Class.html "Vertex Class")** - a member of Prim defining a single geometry [vertex](Vertex.html "Vertex").
  + **[TOP Class](TOP_Class.html "TOP Class")** - a subclass of OPs defining [TOP](TOP.html "TOP") operators.
    - **[CUDAMemory Class](CUDAMemory_Class.html "CUDAMemory Class")** - holds a reference to CUDA memory.
      * **[CUDAMemoryShape Class](CUDAMemoryShape_Class.html "CUDAMemoryShape Class")** - describes the shape of a CUDA memory segment.
    - **[TextLine Class](TextLine_Class.html "TextLine Class")** - a line of text in the [Text TOP](Text_TOP.html "Text TOP") or [Text SOP](Text_SOP.html "Text SOP"), after it has been formatted. Contains various members about the line such as it's text, position etc.
### Helper Classes[[edit](https://docs.derivative.ca/index.php?title=Python_Classes_and_Modules&action=edit&section=2 "Edit section: Helper Classes")]
The following helper objects are part of the [td module](Td_Module.html "Td Module") and can thus be accessed anywhere, including expressions, without imports (e.g. `absTime.frame`).
* **[AbsTime Class](AbsTime_Class.html "AbsTime Class")** (`absTime`) - information about [absolute time](Absolute_Time.html "Absolute Time")
* **[App Class](App_Class.html "App Class")** (`app`) - information about the TouchDesigner app, including version, installation folders, etc.
* **[Project Class](Project_Class.html "Project Class")** (`project`) - information about the current TouchDesigner session
* **[Tdu Module](Tdu_Module.html "Tdu Module")** (`tdu`) - generic utilities for TouchDesigner not relating directly to TD objects.
  + **[ArcBall Class](ArcBall_Class.html "ArcBall Class")** (`tdu.ArcBall`) - encapsulates many aspects of 3D viewer interaction.
  + **[Camera Class](Camera_Class.html "Camera Class")** (`tdu.Camera`) - maintains a 3D position and orientation for a camera and provides multiple methods for manipulating the camera's position and direction.
  + **[Color Class](Color_Class.html "Color Class")** (`tdu.Color`) - holds a 4 component color
  + **[Dependency Class](Dependency_Class.html "Dependency Class")** (`tdu.Dependency`) - used to create [Dependable](Dependency.html "Dependency") Python data.
  + **[Matrix Class](Matrix_Class.html "Matrix Class")** (`tdu.Matrix`) - holds a single 4x4 matrix for use in transformations. See [ObjectCOMP Class](ObjectCOMP_Class.html "ObjectCOMP Class") for transforms of 3D objects.
  + **[Position Class](Position_Class.html "Position Class")** (`tdu.Position`) - holds a 3 component position
  + **[Quaternion Class](Quaternion_Class.html "Quaternion Class")** (`tdu.Quaternion`) - holds a quaternion object for 3D rotations
  + **[Timecode Class](Timecode_Class.html "Timecode Class")** (`tdu.Timecode`) - holds a timecode value
  + **[Vector Class](Vector_Class.html "Vector Class")** (`tdu.Vector`) - holds a 3 component vector
* **[Licenses Class](Licenses_Class.html "Licenses Class")** (`licenses`) - information about installed [license](License_Class.html "License Class") objects
  + **[DongleList Class](DongleList_Class.html "DongleList Class")** (`licenses.dongles`) - list of attached dongles
    - **[Dongle Class](Dongle_Class.html "Dongle Class")** - an individual dongle connected to the system
  + **[License Class](License_Class.html "License Class")** - a single instance of an installed license
    - * **[ProductEntry Class](ProductEntry_Class.html "ProductEntry Class")** - a dongle entry for a single dongle connected to the system
* **[MOD Class](MOD_Class.html "MOD Class")** (`mod`) - access to modules located in TouchDesigner DATs
* **[Monitors Class](Monitors_Class.html "Monitors Class")** (`monitors`) - access to information about all connected display devices
  + **[Monitor Class](Monitor_Class.html "Monitor Class")** - an individual display device
* **[Runs Class](Runs_Class.html "Runs Class")** (`runs`) - information about all delayed [run objects](Run_Class.html "Run Class")
  + **[Run Class](Run_Class.html "Run Class")** - an individual delayed run object
* **[SysInfo Class](SysInfo_Class.html "SysInfo Class")** (`sysInfo`) - current system/hardware information
* **[UI Class](UI_Class.html "UI Class")** (`ui`) - information about application ui elements
  + **[Colors Class](Colors_Class.html "Colors Class")** (`ui.colors`) - application colors
  + **[Options Class](Options_Class.html "Options Class")** (`ui.options`) - configurable ui options
  + **[Panes Class](Panes_Class.html "Panes Class")** (`ui.panes`) - collection of all panes open in the editor
    - **[Pane Class](Pane_Class.html "Pane Class")** - an individual pane object
      * **[NetworkEditor Class](NetworkEditor_Class.html "NetworkEditor Class")** - subclass of Pane that displays a network editor
  + **[Preferences Class](Preferences_Class.html "Preferences Class")** (`ui.preferences`) - collection of TouchDesigner preferences
  + **[Undo Class](Undo_Class.html "Undo Class")** (`ui.undo`) - tools for interacting with the undo system, including creating script-based undo steps
### Standard Python Modules[[edit](https://docs.derivative.ca/index.php?title=Python_Classes_and_Modules&action=edit&section=3 "Edit section: Standard Python Modules")]
The [`td` module](Td_Module.html "Td Module") also automatically imports a number of helpful standard modules, allowing them to be accessed in expressions through their namespace (e.g. `math.cos(math.pi)`):
* [`collections`](https://docs.python.org/3.7/library/collections.html) - container datatypes
* [`enum`](https://docs.python.org/3.7/library/enum.html) - support for enumerations
* [`inspect`](https://docs.python.org/3.7/library/inspect.html) - inspect live objects
* [`math`](https://docs.python.org/3.7/library/math.html) - mathematical functions
* [`re`](https://docs.python.org/3.7/library/re.html) - regular expression operations
* [`sys`](https://docs.python.org/3.7/library/sys.html) - OS specific data and functions
* [`traceback`](https://docs.python.org/3.7/library/traceback.html) - stack utilities
* [`warnings`](https://docs.python.org/3.7/library/warnings.html) - warning control
### TouchDesigner Utility Modules and Python Utilities[[edit](https://docs.derivative.ca/index.php?title=Python_Classes_and_Modules&action=edit&section=4 "Edit section: TouchDesigner Utility Modules and Python Utilities")]
The following contain extended Python utilities for use with TouchDesigner.
* **[TDFunctions](TDFunctions.html "TDFunctions")** - A variety of utilities for advanced Python coding in TouchDesigner.
* **[TDJSON](TDJSON.html "TDJSON")** - JSON utilities specific to TouchDesigner.
* **[TDStoreTools](TDStoreTools.html "TDStoreTools")** - utilities for use with TouchDesigner's [Storage](Storage.html "Storage") and [Dependency](Dependency.html "Dependency") system.
* **[TDResources](TDResources.html "TDResources")** (`op.TDResources...`) - not a module, but does contain system resources that can be accessed via Python. It includes system [pop-up menu](TDResources.html#Pop-Up_Menu "TDResources"), [button pop-up menu](TDResources.html#Button_Pop-Up_Menu "TDResources"), [pop-up dialog](TDResources.html#Pop-Up_Dialog "TDResources"), and [mouse](TDResources.html#Mouse "TDResources") resources.
  

### 3rd Party Packages[[edit](https://docs.derivative.ca/index.php?title=Python_Classes_and_Modules&action=edit&section=5 "Edit section: 3rd Party Packages")]
**The following 3rd party packages are automatically installed with TouchDesigner.** They are not in the [td module](Td_Module.html "Td Module"), so must be imported explicitly to be used in scripts. The name in parentheses is the actual package name used (e.g. to use OpenCV, write this at top of script: `import cv2`). For information on adding or installing other Python modules, see [Importing Modules](Introduction_to_Python_Tutorial.html#Importing_Modules).
* **[attr](https://www.attrs.orgs/)** 22.2.0 (`attr`) - Classes without boilerplate (legacy).
* **[attrs](https://www.attrs.orgs/)** 22.2.0 (`attrs`) - Classes without boilerplate.
* **[Certifi](https://pypi.org/project/certifi/)** 2022.12.07 (`certifi`) - Root Certificates for validating the trustworthiness of SSL certificates while verifying the identity of TLS hosts.
* **[Chardet](https://pypi.org/project/chardet/)** 5.1.0 (`chardet`) - The Universal Character Encoding Detector.
* **[charset-normalizer](https://pypi.org/project/charset-normalizer/)** 3.0.1 (`charset_normalizer`) - A library that helps you read text from an unknown charset encoding.
* **[decorator](https://https://github.com/micheles/decorator)** 5.1.1 (`decorator`) - Define signature-preserving function decorators and decorator factories.
* **[opencv-python](https://pypi.org/project/opencv-python/)** (`cv2`) 4.8.0 - Pre-built CPU-only OpenCV packages for Python.
* **[depthai](https://pypi.org/project/depthai/)** (`depthai`) 2.24.0.0.dev0+7b57b28305368582d004d5c6ec2cffb66562f2e0 - Python bindings for C++ [depthai-core library](https://docs.luxonis.com/projects/api/en/latest/).
* **[idna](https://pypi.org/project/idna/)** (`idna`) 3.4 - Support for the Internationalised Domain Names in Applications (IDNA) protocol.
* **[jsonpath](https://pypi.org/project/jsonpath-ng/)** (`jsonpath_ng`) 1.5.3 - JSONPath tools for accessing and altering JSON structures.
* **[jsonschema](https://pypi.org/project/jsonschema/)** (`jsonschema`) 4.23.0 - jsonschema is an implementation of the [JSON Schema](https://json-schema.org/) specification for Python.
* **[MWParserFromHell](https://mwparserfromhell.readthedocs.io/en/latest/)** (`mwparserfromhell`) 0.6.4 - An easy-to-use and outrageously powerful parser for MediaWiki wikicode.
* **[NumPy](http://www.numpy.org/)** (`numpy`) 1.24.1 - Fundamental package for scientific computing with Python.
* **[OAuthlib](https://pypi.org/project/oauthlib/)** (`oauthlib`) 3.2.2 - Library to build OAuth and OpenID Connect servers.
* **[packaging](https://pypi.org/project/packaging/)** (`packaging`) 23.0 - Package tools including version handling, specifiers, markers, requirements, tags, utilities. Used for version string comparison.
* **[pip](https://pypi.org/project/pip/)** (`pip`) 22.3.1 - pip is the package installer for Python. You can use pip to install packages from the Python Package Index and other indexes.
* **[ply](https://www.dabeaz.com/ply/)** (`ply`) 3.11 - Parsing tools for lex and yacc.
* **[Pygments](https://pypi.org/project/Pygments/)** (`pygments`) 2.14.0 - A syntax highlighting package written in Python.
* **[pyparsing](https://pypi.org/project/pyparsing/)** (`pyparsing`) 3.0.9 - A library of classes that client code uses to construct parsing grammar directly in Python code.
* **[pyrankvote](https://pypi.org/project/pyrankvote/)** (`pyrankvote`) 2.0.5 - PyRankVote is a python library for different ranked-choice voting systems (sometimes called preferential voting systems) created by Jon Tingvold in June 2019.
* **[pyrfc6266](https://pypi.org/project/pyrfc6266/)** (`pyrfc6266`) 1.0.2 - A python implementation of RFC 6266.
* **[pyrsistent](https://pypi.org/project/pyrsistent/)** (`pyrsistent`) 0.19.3 - Pyrsistent is a number of persistent collections (by some referred to as functional data structures). Persistent in the sense that they are immutable.
* **[Requests](http://docs.python-requests.org/en/master/)** (`requests`) 2.28.2 - The only Non-GMO HTTP library for Python, safe for human consumption
* **[Requests OAuthlib](https://requests-oauthlib.readthedocs.io/en/latest/index.html)** (`requests_oauthlib`) 1.3.1 - Easy-to-use Python interface for building OAuth1 and OAuth2 clients
* **[six](https://pypi.org/project/six/)** (`six`) 1.16.0 - Python 2 and 3 compatibility utilities.
* **[smartypants](https://pypi.org/project/smartypants/)** (`smartypants`) 2.0.1 - a Python fork of [SmartyPants](http://daringfireball.net/projects/smartypants/).
* **[tabulate](https://pypi.org/project/tabulate/)** (`tabulate`) 0.9.0 - Pretty-print tabular data in Python.
* **[urllib3](https://urllib3.readthedocs.io/en/latest/)** (`urllib3`) 1.26.14 - HTTP client.
* **[whats-that-code](https://pypi.org/project/whats-that-code/)** (`whats_that_code`) 0.1.4 - programming language detection library.
* **[PyYAML](https://pyyaml.org/wiki/PyYAMLDocumentation)** (`yaml`) 6.0 - YAML parser and emitter.
### Installing Custom Packages and Modules[[edit](https://docs.derivative.ca/index.php?title=Python_Classes_and_Modules&action=edit&section=6 "Edit section: Installing Custom Packages and Modules")]
You can also install your own Python packages that are not included with TouchDesigner. For instructions, go [here](Category_Python.html#Installing_Custom_Python_Packages "Category:Python").
Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Lets you embed files inside a `[.tox](-2.html ".tox")` or `[.toe](.html ".toe")` file. Operators like the Movie File In TOP that read regular files can also read the embedded VFS files using a `vfs:` syntax.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

A sequence of vertices form a [Polygon](Polygon.html "Polygon") in a [SOP](SOP.html "SOP"). Each vertex is an integer index into the [Point List](Point_List.html "Point List"), and each [Point](Point.html "Point") holds an XYZ position and attributes like Normals and Texture Coordinates.

Absolute Time starts counting from 0 when the TouchDesigner process starts, and is always increasing. It will pause if the Power 0/1 button at the top of the UI is Off.

is the [Procedural](Procedural.html "Procedural") mechanism in TouchDesigner, where if one piece of data changes, it automatically causes other operators and expressions to re-[Cook](Cook.html "Cook").

TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.

Retrieved from "<https://docs.derivative.ca/index.php?title=Python_Classes_and_Modules&oldid=32534>"
[Categories](Special_Categories.html "Special:Categories"):
* [Python](Category_Python.html "Category:Python")
* [TDPages](Category_TDPages.html "Category:TDPages")