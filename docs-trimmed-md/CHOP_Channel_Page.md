

CHOP Channel Page - Derivative
























# CHOP Channel Page

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Contents

* [1 Channel Name Creation](#Channel_Name_Creation)
* [2 Start-End](#Start-End)
* [3 Sample Rate](#Sample_Rate)
* [4 Extend Conditions](#Extend_Conditions)
* [5 Legal Channel Names](#Legal_Channel_Names)
## Channel Name Creation[[edit](https://docs.derivative.ca/index.php?title=CHOP_Channel_Page&action=edit&section=1 "Edit section: Channel Name Creation")]

Channel Name - The following kinds of text patterns generate multiple channel names:

| Channel Pattern | Channels Created |
| --- | --- |
| `chan1 chan2 chan3` | `chan1 chan2 chan3` |
| `chan[1-3]` | `chan1 chan2 chan3` |
| `ch[1-2]n[2-6:2]` | `ch1n2 ch1n4 ch1n6 ch2n2 ch2n4 ch2n6` |
| `r[xyz]` | `rx, ry rz` |
| `geo[1-2]:t[xy]` | `geo1:tx geo1:ty geo2:tx geo2:ty` |
| `gain band[4-6] off[lr]` | `gain band4 band5 band6 offl offr` |

## Start-End[[edit](https://docs.derivative.ca/index.php?title=CHOP_Channel_Page&action=edit&section=2 "Edit section: Start-End")]

Start/End - Specifies a start-end interval. The default is start-end of 0. The values in these options can be expressed in any [Units](CHOP_Common_Page.html#Units "CHOP Common Page").

## Sample Rate[[edit](https://docs.derivative.ca/index.php?title=CHOP_Channel_Page&action=edit&section=3 "Edit section: Sample Rate")]

Sample Rate - Usually the CHOP sample rate is set to 60 "samples per second". This means TouchDesigner will attempt to cook the operation 60 times per second. Using a lower sample rate than the global sample sample rate can cause aliasing (errors) in the channel data.

## Extend Conditions[[edit](https://docs.derivative.ca/index.php?title=CHOP_Channel_Page&action=edit&section=4 "Edit section: Extend Conditions")]

Extend Conditions - Found in the Extend CHOP and also in several generator CHOPs, this determines what values you get when you try to sample a CHOP outside its start-end range. It can hold values, repeat the channel and more.

When using the `chop()` function to sample a channel, the index-value may be outside the interval of the CHOP. But a reasonable value is returned. The user is able to control the value of the channel outside the CHOP's interval.

You can see the state of the Extend Conditions in the pop-up info of any CHOP.

Extend Left - The extend condition before the CHOP interval. They are:

* Hold - Hold the first or last value.
* Slope - Continue the slope before the start, or after the end of the channel.
* Cycle - Cycle the channel repeatedly.
* Mirror - Cycle the channel repeatedly, mirroring every other cycle.
* Default Value - Use the constant value specified in the Default Value parameter.

Extend Right - Extend condition after the interval. Same options as Extend Left.

Default Value - The value used for the Default Value extend condition.

## Legal Channel Names[[edit](https://docs.derivative.ca/index.php?title=CHOP_Channel_Page&action=edit&section=5 "Edit section: Legal Channel Names")]

CHOP channel names can have the following characters:

* Upper and lower-case letters
* Numbers
* The following characters: `-` `_` `:` `/`

In general, CHOPs will replace invalid characters with underscores.

samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.


An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


In CHOPs, Extend Conditions determine what numbers you get when you try to get a channel value that is outside its start-end range - in its Extend Regions.







Retrieved from "<https://docs.derivative.ca/index.php?title=CHOP_Channel_Page&oldid=33652>"
[Category](Special_Categories.html "Special:Categories"):

* [OP Help Common Pages](https://docs.derivative.ca/index.php?title=Category:OP_Help_Common_Pages&action=edit&redlink=1 "Category:OP Help Common Pages (page does not exist)")