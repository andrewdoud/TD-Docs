

Creating Audio with CHOPs - Derivative
























# Creating Audio with CHOPs

From Derivative



[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Contents

* [1 Introduction](#Introduction)
* [2 Quick Audio Startup](#Quick_Audio_Startup)
* [3 Loading Audio](#Loading_Audio)
  + [3.1 Scrub Controls](#Scrub_Controls)
  + [3.2 Repeating Audio](#Repeating_Audio)
  + [3.3 TouchDesigner Audio Output Volume](#TouchDesigner_Audio_Output_Volume)
* [4 Outputting Audio to a File](#Outputting_Audio_to_a_File)
* [5 Modifying Audio](#Modifying_Audio)
* [6 3D Audio](#3D_Audio)
## Introduction[[edit](https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&action=edit&section=1 "Edit section: Introduction")]

Audio is managed with CHOPs in TouchDesigner. CHOPs can generate sounds and can read sounds into TouchDesigner from external sources. Audio can be generated, played from audio files, filtered, mixed and recorded.

The ways to obtain audio in CHOPs include: from files, movies, microphones or line in. These are described in detail in the section below. To hear audio output from CHOPs, send the audio to an [Audio Device Out CHOP](Audio_Device_Out_CHOP.html "Audio Device Out CHOP").

For example, the [Audio Oscillator CHOP](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") can generate a constant-frequency audio signal. The [Trigger CHOP](Trigger_CHOP.html "Trigger CHOP") takes an on-off control from TouchDesigner, and generates a volume envelope with a delay, attack, decay, sustain and release transition that can multiplied with an audio CHOP with a [Math CHOP](Math_CHOP.html "Math CHOP") controlling its loudness. The [Math CHOP](Math_CHOP.html "Math CHOP") and [Audio Dynamics CHOP](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") act as a mixer and the [Audio Para EQ CHOP](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") filters the spectrum of audio.

## Quick Audio Startup[[edit](https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&action=edit&section=2 "Edit section: Quick Audio Startup")]

To quickly get audio going, try the following: [File:Audio with CHOPS ex.tox](https://docs.derivative.ca/File:Audio_with_CHOPS_ex.tox "File:Audio with CHOPS ex.tox")

* Connect a default LFO CHOP to a default Audio Oscillator CHOP.
* Connect the Audio Oscillator CHOP to an Audio Device Out CHOP.
* You should hear a rising and falling tone.
* Connect the LFO CHOP to a new Audio Oscillator CHOP and set the oscillator's Base Frequency to 330.
* Connect the two Oscillators to a Merge CHOP. Connect the Merge CHOP to the Audio Device Out CHOP. You should hear one oscillator in each left and right channels.

Next use an Audio File In CHOP as a sound source, connecting it to the Audio Device Out CHOP.

## Loading Audio[[edit](https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&action=edit&section=3 "Edit section: Loading Audio")]

[Audio File In CHOP](Audio_File_In_CHOP.html "Audio File In CHOP") - loads audio from a file as it plays. This method of streaming uses very little memory as it only loads the samples of audio it needs at the time, ideal for large audio files. The CHOP channels created are [time-sliced](Time_Slicing.html "Time Slicing").

[Audio Movie CHOP](Audio_Movie_CHOP.html "Audio Movie CHOP") - loads the audio track from a movie that has been loaded into a [Movie File In TOP](Movie_File_In_TOP.html "Movie File In TOP"). Playback is controlled from Movie File In TOP. The CHOP channels created are [time-sliced](Time_Slicing.html "Time Slicing").

[File In CHOP](File_In_CHOP.html "File In CHOP") - loads the entire audio file into CHOPs. The audio is loaded into CHOPs at the sample rate of the audio file. The higher the sample rate, the more memory CHOPs will use to load the audio. The channels created are not [time-sliced](Time_Slicing.html "Time Slicing"). When completely loaded into CHOPs, it is easy to manipulate the audio downstream with additional Filter CHOPs; stretch, splice, pitch, volume, etc. Care must be taken running real-time systems with large audio files and high sample rates, as CPU usage for these operations is very high.

[Audio Device In CHOP](Audio_Device_In_CHOP.html "Audio Device In CHOP") - streams audio into TouchDesigner from any audio input device attached to the computer. The CHOP channels created are [time-sliced](Time_Slicing.html "Time Slicing").

[Audio Play CHOP](Audio_Play_CHOP.html "Audio Play CHOP") - plays back a sound file directly to the audio output device. Great for simple triggering of sounds. Plays back just a single file or selects from a list of files stored in a [DAT](DAT.html "DAT") list. Can also be triggered using the Tscript `audioplay` Command. Audio is not passed further down the CHOP network.

  


### Scrub Controls [[edit](https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&action=edit&section=4 "Edit section: Scrub Controls")]

When using a Audio File In CHOP, audio can be cued or scrubbed at least 3 ways:

* Audio File In's parameter Play Mode must first be set to Sequential. Select a Cue Point and press Cue Pulse.
* Audio File In's parameter Play Mode must first be set to Specify Index. using the Index parameter. Turn off the Repeat parameter to stop audio buzzing when not scrubbing.
* When using the Audio Movie CHOP, scrubbing the audio can be done through the Movie File In TOP which is referenced. As the movie playback is scrubbed, the audio will follow.

Using a File In CHOP, audio can be scrubbed by scrubbing TouchDesigner's main [Timeline](Timeline.html "Timeline") throughout the frame range of the File In CHOP.

### Repeating Audio[[edit](https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&action=edit&section=5 "Edit section: Repeating Audio")]

When using an [Audio File In CHOP](Audio_File_In_CHOP.html "Audio File In CHOP"), set the Repeat parameter to On.

Using a [File In CHOP](File_In_CHOP.html "File In CHOP"), which statically loads the entire audio file, you can set the Extend Left and Extend Right parameters to Cycle.

[Audio Play CHOPs](Audio_Play_CHOP.html "Audio Play CHOP") need to be repeatedly triggered to repeat the audio.

### TouchDesigner Audio Output Volume[[edit](https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&action=edit&section=6 "Edit section: TouchDesigner Audio Output Volume")]

The Audio Device Out CHOP sets the overall output level to the speakers. This is sent to the volume controls in Windows.

## Outputting Audio to a File[[edit](https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&action=edit&section=7 "Edit section: Outputting Audio to a File")]

You can output the audio in any CHOP using the [RMB](Mouse_Click.html "Mouse Click") menu on the CHOP. Select Save Data Channels in the menu and hit the arrow button to see the file format suffixes that can be used on your output files, such as `.aif`. You can check the file by playing it with [VLC](http://www.videolan.org/vlc/index.html) or [QuickTime](http://support.apple.com/kb/DL837) or another audio player.

Note, the CHOP may be [time-sliced](Time_Slicing.html "Time Slicing"), in which case you will need to first record it into a [Record CHOP](Record_CHOP.html "Record CHOP") or [Trail CHOP](Trail_CHOP.html "Trail CHOP").

## Modifying Audio[[edit](https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&action=edit&section=8 "Edit section: Modifying Audio")]

* [Math CHOP](Math_CHOP.html "Math CHOP") - Increase/decrease volume, mix sounds, stereo to mono, perform functions of a level mixer.
* [Audio Oscillator CHOP](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") - Make audible tones & LFO (low frequency oscillator).
* [Constant CHOP](Constant_CHOP.html "Constant CHOP") - Provide constant-pitch control for oscillator.
* [LFO CHOP](LFO_CHOP.html "LFO CHOP") - Add vibrato or LFO.
* [Noise CHOP](Noise_CHOP.html "Noise CHOP") - Generate white noise.
* [Audio Band EQ CHOP](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") - Graphic equalizer.
* [Audio Para EQ CHOP](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") - Filter, echo, pitch shift.
* [Audio Filter CHOP](Audio_Filter_CHOP.html "Audio Filter CHOP") - Low pass, high pass, band pass filter.
* [Resample CHOP](Resample_CHOP.html "Resample CHOP") - Change the sample rate of a sound.
* [Trigger CHOP](Trigger_CHOP.html "Trigger CHOP") - Make volume envelope with delay, attack, decay, sustain, release.
* [Timer CHOP](Timer_CHOP.html "Timer CHOP") - Cross-dissolve one sound to another.
* [Lag CHOP](Lag_CHOP.html "Lag CHOP") - Make glissando pitch sweeps.
* [Envelope CHOP](Envelope_CHOP.html "Envelope CHOP") - Follow the loudness of a sound.

When you are processing an audio clip by reading the whole file into an [File In CHOP](File_In_CHOP.html "File In CHOP"):

* [Trim CHOP](Trim_CHOP.html "Trim CHOP") - Shorten the audio.
* [Cycle CHOP](Cycle_CHOP.html "Cycle CHOP") - Make it repeat.
* [Wave CHOP](Wave_CHOP.html "Wave CHOP") - Add vibrato or LFO.
* [Shift CHOP](Shift_CHOP.html "Shift CHOP") - Re-time the sounds, simple echo, delay.
* [Stretch CHOP](Stretch_CHOP.html "Stretch CHOP") - Make a sound slower or faster, but shifting pitch too.
* [Copy CHOP](Copy_CHOP.html "Copy CHOP") - Use triggers to copy sounds along a timeline.
* [Pulse CHOP](Pulse_CHOP.html "Pulse CHOP") - Time pulses to produce rhythms as a sequencer.
* [Composite CHOP](Composite_CHOP.html "Composite CHOP") - Layer one sound over a longer sound.
* [Lookup CHOP](Lookup_CHOP.html "Lookup CHOP") - Soft limit amplitudes etc.

## 3D Audio[[edit](https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&action=edit&section=9 "Edit section: 3D Audio")]

CHOPs can take events from a 3D scene, imported through the [SOP to CHOP](SOP_to_CHOP.html "SOP to CHOP") or [Object CHOP](Object_CHOP.html "Object CHOP"), and be used to trigger sounds and control the placement of sounds in 3D space.

An object, particle, or point position in 3D space can be used to set the left-right ear separation, or used as reverb controls which add a cue that simulates proximity of the sound.

Audio can be generated for offscreen objects, adding more 3D cues and realism.

[Filter Animation Channels](https://docs.derivative.ca/index.php?title=Filter_Animation_Channels&action=edit&redlink=1 "Filter Animation Channels (page does not exist)")

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.


An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.


TouchDesigner's original built-in Command scripting language prior to [Python](Python.html "Python").


Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.


To "pulse" a parameter is to send it a signal from (1) an [exported](Export.html "Export") CHOP channel or (2) a python command or (3) a mouse click that causes a new action to occur immediately. A pulse via python is via the `.pulse()` function on a pulse-type parameter, such as Reset parameter in a [Speed CHOP](Speed_CHOP.html "Speed CHOP"). A pulse from a CHOP is typically a 0 to 1 to 0 signal in an exported channel.


Operators that need 1 or more inputs are called Filters in TouchDesigner, like a Math CHOP. See [Generator](Generator.html "Generator").







Retrieved from "<https://docs.derivative.ca/index.php?title=Creating_Audio_with_CHOPs&oldid=10344>"
[Categories](Special_Categories.html "Special:Categories"):

* [TouchDesigner Tips](Category_TouchDesigner_Tips.html "Category:TouchDesigner Tips")
* [Audio](https://docs.derivative.ca/index.php?title=Category:Audio&action=edit&redlink=1 "Category:Audio (page does not exist)")
* [CHOP Topics](Category_CHOP_Topics.html "Category:CHOP Topics")
* [TDPages](Category_TDPages.html "Category:TDPages")