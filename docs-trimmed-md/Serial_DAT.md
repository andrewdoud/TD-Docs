

TouchDesigner Documentation




# Serial DAT
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Serial DAT is used for serial communication through an external port, using the RS-232 protocol. These ports are usually a 9 pin connector, or a USB port on new machines. (Using a USB port requires a USB-to-serial adapter and driver.)
All of a computer's available serial ports can be found in the Device Manager in the Windows operating system under Computer –> Manage -> Devices -> Serial… -> COM ports. Their names begin with 'COM'. Example: COM1, COM2, COM3.
To send bytes out this connection, see the send methods in the [serialDAT\_Class](https://docs.derivative.ca/SerialDAT_Class "SerialDAT Class"), or in Tscript the `send` Command.
See also [Arduino](Arduino.html "Arduino") and [Serial CHOP](Serial_CHOP.html "Serial CHOP").
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[serialDAT\_Class](https://docs.derivative.ca/SerialDAT_Class "SerialDAT Class")
## Contents
* [1 Summary](#Summary)
* [2 Parameters - Connect Page](#Parameters_-_Connect_Page)
* [3 Parameters - Received Data Page](#Parameters_-_Received_Data_Page)
* [4 Parameters - Common Page](#Parameters_-_Common_Page)
* [5 Info CHOP Channels](#Info_CHOP_Channels)
  + [5.1 Specific Serial DAT Info Channels](#Specific_Serial_DAT_Info_Channels)
  + [5.2 Common DAT Info Channels](#Common_DAT_Info_Channels)
  + [5.3 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Connect Page
Active `active` - This check box enables the serial connection.
Row/Callback Format `format` - ⊞ - Interpret the incoming data as binary or ASCII data. If the format is Per Byte, one row is appended for each binary byte received. If the format is Per Line, one row is appended for each null or newline delimited message received.
* One Per Byte `perbyte` - (formerly called 'binary').
* One Per Line `perline` - (formerly called 'Ascii') null/newln delimited.
* One Per Message `permessage` - Full incoming msg.
Port `port` - Selects the COM port that the serial connection will use. Default port names 1 through 8 are available in the popup menu, though any name can be manually entered in this field.
Baud Rate `baudrate` - ⊞ - The maximum number of bits of information, including "control" bits, that are transmitted per second. Check your input device's default baud rate and set accordingly.
* 1200 `1200` -
* 2400 `2400` -
* 9600 `9600` -
* 19200 `19200` -
* 38400 `38400` -
* 57600 `57600` -
* 115200 `115200` -
* 230400 `230400` -
* 460800 `460800` -
* 921600 `921600` -
* 1382400 `1382400` -
Data Bits `databits` - ⊞ - This parameter sets the number of data bits sent in each. Data bits are transmitted "backwards". Backwards refers to the order of transmission, which is from least significant bit (LSB) to most significant bit (MSB). To interpret the data bits, you must read from right to left.
* 6 `6` -
* 7 `7` -
* 8 `8` -
* 9 `9` -
Parity `parity` - ⊞ - This parameter can be set to none, even, or odd. The optional parity bit follows the data bits and is included as a simple means of error checking. Parity bits work by specifying ahead of time whether the parity of the transmission is to be even or odd. If the parity is set to be odd, the transmitter will then set the parity bit in such a way as to make an odd number of 1's among the data bits and the parity bit.
* Even `even` -
* Odd `odd` -
* None `none` -
Stop Bits `stopbits` - ⊞ - The last part of transmission packet consists of 1 or 2 Stop bits. The connection will now wait for the next Start bit.
* 1 `1` -
* 2 `2` -
DTR `dtr` - ⊞ - The DTR (data-terminal-ready) flow control. (Windows Only).
* Disable `disable` - Disables the line when device is opened.
* Enable `enable` - Enables the line when device is opened.
* Handshake `handshake` - Enables handshaking with the device.
RTS `rts` - ⊞ - The RTS (request-to-send) flow control. (Windows Only).
* Disable `disable` - Disables the line when device is opened.
* Enable `enable` - Enables the line when device is opened.
* Handshake `handshake` - Enables RTS handshaking.
* Toggle `toggle` - Line high only when bytes available.
  

## Parameters - Received Data Page
Callbacks DAT `callbacks` - The Callbacks DAT will execute once for each message received.
Execute from `executeloc` - ⊞ - Determines the location the script is run from.
* Current Node `current` - The script is executed from the current node location.
* Callbacks DAT `callbacks` - The script is executed from the location of the DAT specified in the Callbacks DAT parameter.
* Specified Operator `op` - The script is executed from the component specified in the Component parameter below.
From Operator `fromop` - The path that the script will be executed from if the Execute From parameter is set to Specified Operator.
Clamp Output `clamp` - The DAT is limited to 100 messages by default but with Clamp Output, this can be set to anything including unlimited.
Maximum Lines `maxlines` - Limits the number of messages, older messages are removed from the list first.
Clear Output `clear` - Deletes all lines except the heading. To clear with a script command, here is an example: `opparm -c /serial1 clear`
Bytes Column `bytes` - Outputs the raw bytes of the message in a separate column.
  

## Parameters - Common Page
Language `language` - ⊞ - Select how the DAT decides which script language to operate on.
* Input `input` - The DAT uses the inputs script language.
* Node `node` - The DAT uses it's own script language.
Edit/View Extension `extension` - ⊞ - Select the file extension this DAT should expose to external editors.
* dat `dat` - various common file extensions.
* From Language `language` - pick extension from DATs script language.
* Custom Extension `custom` - Specify a custom extension.
Custom Extension `customext` - Specifiy the custom extension.
Word Wrap `wordwrap` - ⊞ - Enable Word Wrap for Node Display.
* Input `input` - The DAT uses the inputs setting.
* On `on` - Turn on Word Wrap.
* Off `off` - Turn off Word Wrap.
  

## Info CHOP Channels
Extra Information for the Serial DAT can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").
### Specific Serial DAT Info Channels
* bytes\_read -
* bytes\_written -
* bytes\_write\_queued -
* bytes\_write\_rate -
* messages\_pending -
### Common DAT Info Channels
* num\_rows - Number of rows in this DAT.
* num\_cols - Number of columns in this DAT.
### Common Operator Info Channels
* total\_cooks - Number of times the operator has cooked since the process started.
* cook\_time - Duration of the last cook in milliseconds.
* cook\_frame - Frame number when this operator was last cooked relative to the component timeline.
* cook\_abs\_frame - Frame number when this operator was last cooked relative to the absolute time.
* cook\_start\_time - Time in milliseconds at which the operator started cooking in the frame it was cooked.
* cook\_end\_time - Time in milliseconds at which the operator finished cooking in the frame it was cooked.
* cooked\_this\_frame - 1 if operator was cooked this frame.
* warnings - Number of warnings in this operator if any.
* errors - Number of errors in this operator if any.
  
TouchDesigner Build: Latest\n2021.100002018.28070before 2018.28070
| DATs |
| --- |
| [Art-Net](Art-Net_DAT.html "Art-Net DAT") • [Audio Devices](Audio_Devices_DAT.html "Audio Devices DAT") • [CHOP Execute](CHOP_Execute_DAT.html "CHOP Execute DAT") • [CHOP to](CHOP_to_DAT.html "CHOP to DAT") • [Clip](Clip_DAT.html "Clip DAT") • [Convert](Convert_DAT.html "Convert DAT") • [CPlusPlus](CPlusPlus_DAT.html "CPlusPlus DAT") • [DAT](DAT.html "DAT") • [Experimental:DAT](Experimental_DAT.html "Experimental:DAT") •  [Execute](DAT_Execute_DAT.html "DAT Execute DAT") • [DAT Export](DAT_Export.html "DAT Export") • [Error](Error_DAT.html "Error DAT") • [EtherDream](EtherDream_DAT.html "EtherDream DAT") • [Evaluate](Evaluate_DAT.html "Evaluate DAT") • [Examine](Examine_DAT.html "Examine DAT") • [Execute](Execute_DAT.html "Execute DAT") • [FIFO](FIFO_DAT.html "FIFO DAT") • [File In](File_In_DAT.html "File In DAT") • [File Out](File_Out_DAT.html "File Out DAT") • [Folder](Folder_DAT.html "Folder DAT") • [In](In_DAT.html "In DAT") • [Indices](Indices_DAT.html "Indices DAT") • [Info](Info_DAT.html "Info DAT") • [Insert](Insert_DAT.html "Insert DAT") • [JSON](JSON_DAT.html "JSON DAT") • [Keyboard In](Keyboard_In_DAT.html "Keyboard In DAT") • [Lookup](Lookup_DAT.html "Lookup DAT") • [Media File Info](Media_File_Info_DAT.html "Media File Info DAT") • [Merge](Merge_DAT.html "Merge DAT") • [MIDI Event](MIDI_Event_DAT.html "MIDI Event DAT") • [MIDI In](MIDI_In_DAT.html "MIDI In DAT") • [Monitors](Monitors_DAT.html "Monitors DAT") • [MPCDI](MPCDI_DAT.html "MPCDI DAT") • [MQTT Client](MQTT_Client_DAT.html "MQTT Client DAT") • [Multi Touch In](Multi_Touch_In_DAT.html "Multi Touch In DAT") • [NDI](NDI_DAT.html "NDI DAT") • [Null](Null_DAT.html "Null DAT") • [OP Execute](OP_Execute_DAT.html "OP Execute DAT") • [OP Find](OP_Find_DAT.html "OP Find DAT") • [OSC In](OSC_In_DAT.html "OSC In DAT") • [OSC Out](OSC_Out_DAT.html "OSC Out DAT") • [Out](Out_DAT.html "Out DAT") • [Panel Execute](Panel_Execute_DAT.html "Panel Execute DAT") • [Parameter](Parameter_DAT.html "Parameter DAT") • [Parameter Execute](Parameter_Execute_DAT.html "Parameter Execute DAT") • [ParGroup Execute](ParGroup_Execute_DAT.html "ParGroup Execute DAT") • [Perform](Perform_DAT.html "Perform DAT") • [Render Pick](Render_Pick_DAT.html "Render Pick DAT") • [Reorder](Reorder_DAT.html "Reorder DAT") • [Script](Script_DAT.html "Script DAT") • [Select](Select_DAT.html "Select DAT") • Serial• [Experimental:Serial Devices](Experimental_Serial_Devices_DAT.html "Experimental:Serial Devices DAT") • [SocketIO](SocketIO_DAT.html "SocketIO DAT") • [SOP to](SOP_to_DAT.html "SOP to DAT") • [Sort](Sort_DAT.html "Sort DAT") • [Substitute](Substitute_DAT.html "Substitute DAT") • [Switch](Switch_DAT.html "Switch DAT") • [Table](Table_DAT.html "Table DAT") • [TCP/IP](TCP/IP_DAT.html "TCP/IP DAT") • [Text](Text_DAT.html "Text DAT") • [Touch In](Touch_In_DAT.html "Touch In DAT") • [Touch Out](Touch_Out_DAT.html "Touch Out DAT") • [Transpose](Transpose_DAT.html "Transpose DAT") • [TUIO In](TUIO_In_DAT.html "TUIO In DAT") • [UDP In](UDP_In_DAT.html "UDP In DAT") • [UDP Out](UDP_Out_DAT.html "UDP Out DAT") • [UDT In](UDT_In_DAT.html "UDT In DAT") • [UDT Out](UDT_Out_DAT.html "UDT Out DAT") • [Video Devices](Video_Devices_DAT.html "Video Devices DAT") • [Web Client](Web_Client_DAT.html "Web Client DAT") • [Web](Web_DAT.html "Web DAT") • [Web Server](Web_Server_DAT.html "Web Server DAT") • [WebRTC](WebRTC_DAT.html "WebRTC DAT") • [WebSocket](WebSocket_DAT.html "WebSocket DAT") • [XML](XML_DAT.html "XML DAT") |
An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

TouchDesigner's original built-in Command scripting language prior to [Python](Python.html "Python").

Some operators have a DAT [docked](Docking.html "Docking") to them that contains some python functions. These functions, called "callbacks", get called when something in the operator changes.

The generic thing that holds an [Operator](Operator.html "Operator"), and includes [Flags](Flag.html "Flag") (display, bypass, lock, render, immune) and its position/size in the network. Whether you "lay down an Operator" or "lay down an Node", you're doing the same thing.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Retrieved from "<https://docs.derivative.ca/index.php?title=Serial_DAT&oldid=27194>"
[Category](Special_Categories.html "Special:Categories"):
* [DATs](https://docs.derivative.ca/index.php?title=Category:DATs&action=edit&redlink=1 "Category:DATs (page does not exist)")