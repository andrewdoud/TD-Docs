

Anatomy of a CHOP - Derivative




# Anatomy of a CHOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Contents
* [1 Inside a CHOP](#Inside_a_CHOP)
* [2 CHOP Inputs, Parameters and Outputs](#CHOP_Inputs,_Parameters_and_Outputs)
* [3 Parts of a CHOP](#Parts_of_a_CHOP)
* [4 CHOP Networks](#CHOP_Networks)
* [5 Importing / Exporting CHOP Channels](#Importing_/_Exporting_CHOP_Channels)
  + [5.1 Object, SOP and COP Channels Imported from CHOPs](#Object,_SOP_and_COP_Channels_Imported_from_CHOPs)
  + [5.2 CHOPs Exported to Component, SOP and TOP Channels](#CHOPs_Exported_to_Component,_SOP_and_TOP_Channels)
* [6 Channel Index and Value](#Channel_Index_and_Value)
* [7 CHOPs for Audio](#CHOPs_for_Audio)
## Inside a CHOP[[edit](https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&action=edit&section=1 "Edit section: Inside a CHOP")]
* A CHOP contains a set of **channels** defined over a **start-end interval**.
* The channels of a CHOP can represent **motion, MIDI, audio, color maps, rolloff curves** or **lookup tables**.
* Each channel is one **array of raw samples**, which is simply a list of numbers.
* Each channel of a CHOP has a **channel name** that can be set by the user.
* The group of CHOP channels is known as a **clip**.
* A **CHOP contains a clip plus control parameters, a sample rate, some on/off flags, and a start/end interval**.
* The CHOP can have any start/end indexes. All channels in a CHOP share the same start-end interval.
* The interval goes from the start position to the end position.
* The interval of a CHOP is not restricted to be the length of the animation.
* Each CHOP has a **sample rate**, used if the CHOP contains time-dependent motion or audio data.
* Audio has a high sample rates when compared to animated motion.
## CHOP Inputs, Parameters and Outputs[[edit](https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&action=edit&section=2 "Edit section: CHOP Inputs, Parameters and Outputs")]
* CHOPs have "parameters" used to define the data, plus the data channels, which are input/output from the CHOP as its data stream.
* The CHOP parameters are usually constant-valued, but can be time-dependent expressions.
* Each CHOP receives channels at its inputs. When the CHOP cooks, the channels of the inputs are combined. The CHOP outputs the resulting channels to other CHOPs.
* CHOPs output their data channels as arrays of numbers, not interpolated segments. Some CHOPs retain interpolated segments internally, but all CHOPs always output their data as raw samples.
* If the CHOP's inputs are not changing and the control parameters are not time-dependent, the CHOP will be non-time-dependent and it will not cook every time the animation frame advances.
* Some CHOPs have Local Variables:  
   $I (the array index within the CHOP), $C (the channel number within the CHOP)
* Some CHOPs output or use CHOP attributes, such as channels grouped as quaternion rotation channels.
## Parts of a CHOP[[edit](https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&action=edit&section=3 "Edit section: Parts of a CHOP")]
* Each CHOP has a set of parameters.
* CHOPs' parameters can be expressed in different units: samples (indexes), frames or seconds. These units are selected by the user in a menu to the right of such parameters.
* Each CHOP has flags: 
  + **The Graph** flag marks the CHOP to be displayed in the Graph of the CHOP Editor.
  + **The Export** flag causes the CHOP channels to override channels of objects, SOps.
  + **The Lock** flag causes the CHOP can be locked and hand-edited. The Channel Editor is the interactive editor of parameter channels in CHOPs.
  + **The Bypass** flag is a convenient way for a CHOP's effect to be disabled.
* Each CHOP has an info pop-up menu accessible by middle-mouse clicking on the CHOP. This lists channel names and values, sample rate and interval.
* Each CHOP has a comment field.
## CHOP Networks[[edit](https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&action=edit&section=4 "Edit section: CHOP Networks")]
* CHOPs are arranged in OP networks in components, where CHOP outputs are connected to the inputs of other CHOPs.
## Importing / Exporting CHOP Channels[[edit](https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&action=edit&section=5 "Edit section: Importing / Exporting CHOP Channels")]
### Object, SOP and COP Channels Imported from CHOPs [[edit](https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&action=edit&section=6 "Edit section: Object, SOP and COP Channels Imported from CHOPs")]
Parameters of SOPs, TOPs and objects (components) are able to get values from CHOP channels with expressions like the following:
```
 chop(CHOPchannelpath)
 chopi(CHOPchannelpath, index
```
However, exporting is preferred where possible. It is faster and involves less typing.
### CHOPs Exported to Component, SOP and TOP Channels[[edit](https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&action=edit&section=7 "Edit section: CHOPs Exported to Component, SOP and TOP Channels")]
* CHOP data channels are exported to Components, SOPs, etc. to drive their parameters. CHOPs can be exported to any TouchDesigner parameter.
* Each CHOP has an Export flag (and an Export Prefix, infrequently used), causing the CHOP to attach its channels to Components, SOPs, TOPs and so on.
* The Export flag and Export Prefix are used to connect channels of an object or SOP directly to a CHOP. It uses automatic matching of channels names. For example, a CHOP "tx" channel could map to an Geometry Component's tx parameter.
* When a CHOP exports to an object, SOP or TOP, the latters' channels are said to be overridden. An OP's Override menu lists what is overridden.
## Channel Index and Value[[edit](https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&action=edit&section=8 "Edit section: Channel Index and Value")]
[![ChannelsInfo2.gif](images/2/2b/ChannelsInfo2.gif)](File_ChannelsInfo2.html)
* The horizontal axis is called the i-axis or the index-axis.
* The vertical axis is called the v-axis or the value-axis.
* An index is a point along the i-axis,denoted by i.
* A value is a point along the v-axis, denoted by v.
* A sample is an index-value pair (i,v). i.e. the value of a channel at a certain index.
* A sample is made of a sample index and a sample value.
* An interval is an index range, which goes from a start index to an end index.
* A value range goes from a start value to an end value.
* The index duration is the end index minus the start index + 1.
* CHOP data channels are arrays of raw samples, in 32-bit floating point format.
* Channels in a CHOP may be control (parameter) channels or data channels. CHOPs manupulate the data channels.
* CHOPs can be evaluated at integer and non-integer indexes.
* Frame is used when the index corresponds to time.
* When speaking of animation frames, you can refer to start frame, end frame and frame range.
  

## CHOPs for Audio[[edit](https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&action=edit&section=9 "Edit section: CHOPs for Audio")]
* [Audio File In CHOP](Audio_File_In_CHOP.html "Audio File In CHOP")
* [Audio Movie CHOP](Audio_Movie_CHOP.html "Audio Movie CHOP")
* [Audio Play CHOP](Audio_Play_CHOP.html "Audio Play CHOP")
* [Audio Device In CHOP](Audio_Device_In_CHOP.html "Audio Device In CHOP")
* [Audio Device Out CHOP](Audio_Device_Out_CHOP.html "Audio Device Out CHOP")
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

An [Operator Family](Operator_Family.html "Operator Family") that contains its own [Network](Network.html "Network"). There are sixteen 3D [Object Component](Object_Component.html "Object Component") and ten 2D [Panel Component](Panel_Component.html "Panel Component") types. See also [Network Path](Network_Path.html "Network Path").

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

Any of the procedural data operators. OPs do all the work in TouchDesigner. They "cook" and output data to other OPs, which ultimately result in new images, data and audio being generated. See [Node](Node.html "Node").

Retrieved from "<https://docs.derivative.ca/index.php?title=Anatomy_of_a_CHOP&oldid=7891>"
[Categories](Special_Categories.html "Special:Categories"):
* [CHOP Topics](Category_CHOP_Topics.html "Category:CHOP Topics")
* [TDPages](Category_TDPages.html "Category:TDPages")