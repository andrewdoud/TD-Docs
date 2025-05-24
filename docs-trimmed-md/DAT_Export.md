

DAT Export - Derivative
























# DAT Export

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)

DAT exporting sends numbers, strings or expressions in a table format to a [parameter](Parameter.html "Parameter") of any [operator](Operator.html "Operator").

To export data from a DAT, the green Export flag at the bottom of the DAT must be on, AND the DAT must be in a table format with properly named columns.
The columns are named:

`path parameter value enable` 

Each row represents one value to be exported to a parameter of another node.

The `path` and `parameter` specify the network path to the operator and parameter where the data will be exported to.

The `value` column contains the data to be exported. It can be a numeric value, string value or expression.

The `enable` column is optional. When set to '0' the export in that row is disabled, when set to '1' the export is enabled.

The DAT's green [Export Flag](Export_Flag.html "Export Flag") must be On to enable the export.
Once the export is established, a dotted data [link](Link.html "Link") will connect the DAT and the operator to indicate a connection.

To disable the export, simply toggle the DAT's export flag off.

[![DATexport.png](https://docs.derivative.ca/images/6/60/DATexport.png)](https://docs.derivative.ca/File:DATexport.png)

For exporting from CHOPs, see also: [CHOP Export](CHOP_Export.html "CHOP Export").

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.


Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").







Retrieved from "<https://docs.derivative.ca/index.php?title=DAT_Export&oldid=9885>"
[Category](Special_Categories.html "Special:Categories"):

* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")