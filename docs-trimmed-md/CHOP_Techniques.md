

# CHOP_Techniques

CHOP Techniques - Derivative




# CHOP Techniques
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
These are a few basic CHOP techniques. This is Tscript-focused and requires a python makeover.
## Contents
* [1 Getting RGBA values between TOPs and CHOPs](#Getting_RGBA_values_between_TOPs_and_CHOPs)
* [2 Getting XYZ values between SOPs and CHOPs](#Getting_XYZ_values_between_SOPs_and_CHOPs)
* [3 Speeding Up CHOPs using the Performance Monitor](#Speeding_Up_CHOPs_using_the_Performance_Monitor)
* [4 Diagnosing CHOPs with the print() Function](#Diagnosing_CHOPs_with_the_print()_Function)
* [5 Multiple Objects and CHOP Networks](#Multiple_Objects_and_CHOP_Networks)
* [6 The Use of CHOPs in Managing Large Projects](#The_Use_of_CHOPs_in_Managing_Large_Projects)
* [7 Bypassing CHOP networks](#Bypassing_CHOP_networks)
## Getting RGBA values between TOPs and CHOPs[[edit](https://docs.derivative.ca/index.php?title=CHOP_Techniques&action=edit&section=1 "Edit section: Getting RGBA values between TOPs and CHOPs")]
The [TOP to CHOP](TOP_to_CHOP.html "TOP to CHOP") is used to get the RGBA values in a [TOP](TOP.html "TOP")'s pixels into the channels of a [CHOP](CHOP.html "CHOP"), where they can be edited with CHOPs.
The [CHOP to TOP](CHOP_to_TOP.html "CHOP to TOP") gets pixel values quickly back into TOPs.
## Getting XYZ values between SOPs and CHOPs[[edit](https://docs.derivative.ca/index.php?title=CHOP_Techniques&action=edit&section=2 "Edit section: Getting XYZ values between SOPs and CHOPs")]
The [SOP to CHOP](SOP_to_CHOP.html "SOP to CHOP") is used to get the XYZ values in a [SOP](SOP.html "SOP")'s points into the channels of a CHOP, where they can be edited with CHOPs. All point attributes in a SOP can be obtained, including user-defined point attributes.
The [CHOP to SOP](CHOP_to_SOP.html "CHOP to SOP") is used to get values in CHOP channels into the points of a SOP. The CHOP to SOP takes a geometry at its input, and without changing the surface type or connections between vertices of polygons or meshes, it modifies point values only. It operates much more quickly than the Point SOP.
Any point attribute can be replaced by values in CHOP channels.
In both cases, point groups in SOPs can be used to restrict the data being transferred between SOPs and CHOPs.
## Speeding Up CHOPs using the Performance Monitor[[edit](https://docs.derivative.ca/index.php?title=CHOP_Techniques&action=edit&section=3 "Edit section: Speeding Up CHOPs using the Performance Monitor")]
See [Optimize](Optimize.html "Optimize").
## Diagnosing CHOPs with the print() Function[[edit](https://docs.derivative.ca/index.php?title=CHOP_Techniques&action=edit&section=4 "Edit section: Diagnosing CHOPs with the print() Function")]
Sometimes it unclear what value a CHOP parameter may have when it is cooked, if it is an expression. You can put the expression in a print() function, and it will display its value when it evaluates. The syntax is `print(string, expression)` where string is printed in front of the value on the standard output.
## Multiple Objects and CHOP Networks[[edit](https://docs.derivative.ca/index.php?title=CHOP_Techniques&action=edit&section=5 "Edit section: Multiple Objects and CHOP Networks")]
Sometimes you want one CHOP network to drive one object. You may want to clone the pair dozens of times, but you may want each to behave a bit differently. So you want to get a number in each of the objects and CHOP networks that identifies it.
If you could get the digits in the object name and the CHOP network name, you could use this number to identify the unit. But there is no obvious way of getting that number into CHOP or object parameters. Here is a way:
The expression function, `opdigits()` gets the numbers that are in an OP name. For example, it extracts the 23 from an OP named leg23left .
This allows you to make one CHOP network for each of 100 similar characters. For example, in a CHOP, you can get the number of the CHOP network by using these functions:
```
   opname("..") = "ch1" (a string)
```
```
   opdigits("..") = 1 (a set of digits)
```
```
   opdigits("opname") returns the numeric value of the concatenation of all the digits in a node's name. It is used when building several similar networks. For example:
   opdigits("/obj/geo7") = 7
```
```
   opdigits("..") = 7 (at the SOP level of geo1)
```
In the 100 objects geo1 to geo100, you can use the expression:
```
   opdigits(".")
```
You can use this function in the Random Seed parameter in the [Noise CHOP](Noise_CHOP.html "Noise CHOP"), which will generate a different noise curve for each CHOP network.
## The Use of CHOPs in Managing Large Projects[[edit](https://docs.derivative.ca/index.php?title=CHOP_Techniques&action=edit&section=6 "Edit section: The Use of CHOPs in Managing Large Projects")]
You can hold many moves for many characters in one CHOP network and examine any CHOP by connecting it to a character immediately. So it acts as a library and viewer of moves. Also, when several animators work on one project and the goal is to make the character have similar behavior from scene to scene, animators can pick moves from the library to start with. This is like a library of materials that keep the rendered look the same from scene to scene.
## Bypassing CHOP networks[[edit](https://docs.derivative.ca/index.php?title=CHOP_Techniques&action=edit&section=7 "Edit section: Bypassing CHOP networks")]
Avoids cooking of CHOP networks when you want to make sure CHOPs are not cooking. Click the [Bypass Flag](Bypass_Flag.html "Bypass Flag"), or [Lock Flag](Lock_Flag.html "Lock Flag").
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

TouchDesigner's original built-in Command scripting language prior to [Python](Python.html "Python").

A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

The tool built-in to TouchDesigner that analyzes and displays what TouchDesigner is doing as it generates the output images, audio and data.

Retrieved from "<https://docs.derivative.ca/index.php?title=CHOP_Techniques&oldid=10124>"