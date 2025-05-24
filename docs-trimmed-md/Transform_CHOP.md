

# Transform_CHOP

Transform CHOP - TouchDesigner Documentation




# Transform CHOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Transform CHOP takes transformations in various formats, applied operations to them, and outputs them in various formats. It can be used to:
* Change the position and orientation of an object.
* Convertion transforms one format to another format.
* Convert a set of transform channels with a certain transform order into an equivalent set of channels with a different transform order.
* Change the direction, starting point and scale of motion capture data or other data being calibrated to match other reference frames.
( See also the [Transform XYZ CHOP](Transform_XYZ_CHOP.html "Transform XYZ CHOP") for doing transforms on XYZ positions and vectors. )
Three transform formats exists:
* Transform with Euler angles for rotation. These are defined by channels with suffixes: `tx ty tz, rx ry rz, sx sy sz` and an optional transform and rotate order `xord and rord`.
* Transform with Quaternion for rotation. These are defined by channels with suffixes: `tx ty tz, qx qy qx qw, sx sy sz` and an optional transform order `xord`.
* A 4x4 or 3x3 matrix. These are defined by channels with suffixes: `m00, m10, m20, m30, m01, m11... m33`. Where the notation is `m[row][col]`. The matrix should be be in column-major order, that is to say, the translate portion should be in `m03, m13, m23`. The 4th row and column can be omitted to use a 3x3 matrix instead. Unlike the other formats, this format can not have arbitrary missing channels. Either 9 channels for 3x3 or 16 channels for 4x4 matrices must be provided.
The first two transform formats can be specified with missing channels, in which case default values will be used. 0s for translates and rotates, 1s for scale, and (0,0,0,1) for quaternion.
Frequently the input channels come from an [Object CHOP](Object_CHOP.html "Object CHOP") or [Parameter CHOP](Parameter_CHOP.html "Parameter CHOP"). Examples are:
* geo1:tx geo1:ty geo1:tz geo1:rx ...
* headtx headty headtz headrx
* tx ty tz rx ... (what you would get from a Parameter CHOP)
* cam1:m00 cam1:m10 cam1:m20 .... cam1:m33
### Multiple Transform Sets
Any of the above defines a transformation matrix. Multiple transform 'sets' can be specified by channels having different prefixes. Different sets using different formats can be all in the same CHOP. Formats can not be mixed within a set though. Each set will be combined with sets from the other input, and the transform on the 'Transform' page to create final transforms for each set.
If no inputs are connected to the CHOP, it will output the transform generated from the 'Transform' page.
If inputs are connected, the output will contain the same number of samples as the first input. Samples will be combined between the inputs 1:1, that is, the start/end range and the sample rate of the inputs are ignored. If the second input contains less samples than the first one, the extend conditions for that CHOP will be used to determine values for the samples coming from the 2nd CHOP that are out of range.
If multiple sets are provided, they will be matched 1st-to-1st set, 2nd-to-2nd set. If there are less sets in the second input than the first one, then it will loop over the sets. E.g if the first input as 5 sets and the second input as 2 sets, the matching will be 1st-to-1st, 2nd-to-2nd, 3rd-to-1st, 4th-to-2nd and 5th-to-1st.
### Order of Operation
The inputs will be combined together first, then the result from that will be combined with the transform defined on the 'Transform' page.
The channels of a Transform CHOP are frequently exported back to objects.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[transformCHOP\_Class](https://docs.derivative.ca/TransformCHOP_Class "TransformCHOP Class")
## Contents
* [1 Summary](#Summary)
  + [1.1 Multiple Transform Sets](#Multiple_Transform_Sets)
  + [1.2 Order of Operation](#Order_of_Operation)
* [2 Parameters - Input Page](#Parameters_-_Input_Page)
* [3 Parameters - Transform Page](#Parameters_-_Transform_Page)
* [4 Parameters - Output Page](#Parameters_-_Output_Page)
* [5 Parameters - Common Page](#Parameters_-_Common_Page)
* [6 Operator Inputs](#Operator_Inputs)
* [7 Info CHOP Channels](#Info_CHOP_Channels)
  + [7.1 Common CHOP Info Channels](#Common_CHOP_Info_Channels)
  + [7.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Input Page
This page defines what the incoming channels' transform order is assumed to be. Using the incoming channels and the transform order here, a matrix for the incoming channels in built. It is then multiplied by the transformation matrix defined by the Transform page and output.
Any missing translation, rotation or scale channels will default to zero (or one in the case of scale).
Custom Input Orders `custinputorders` - This allows the input order, if provided, to be ignored and overridden by a custom order chosen by the following two parameters.
Transform Order `inxord` - ⊞ - Changing the Transform order will change where things go much the same way as going a block and turning east gets you to a different place than turning east and then going a block. In matrix math terms, if we use the 'multiply vector on the right' (column vector) convention, a transform order of Scale, Rotate, Translate would be written as T \* R \* S \* Position
* Scale Rotate Translate `srt` -
* Scale Translate Rotate `str` -
* Rotate Scale Translate `rst` -
* Rotate Translate Scale `rts` -
* Translate Scale Rotate `tsr` -
* Translate Rotate Scale `trs` -
Rotate Order `inrord` - ⊞ - As with transform order (above), changing the order in which the rotations take place will alter the final position and orientation. A Rotation order of Rx Ry Rz would create the final rotation matrix as follows R = Rz \* Ry \* Rx
* Rx Ry Rz `xyz` -
* Rx Rz Ry `xzy` -
* Ry Rx Rz `yxz` -
* Ry Rz Rx `yzx` -
* Rz Rx Ry `zxy` -
* Rz Ry Rx `zyx` -
Input 0 Pre Operation `input0preop` - ⊞ - Operation(s) to apply on the transforms on Input 0, before they are combined with other transforms.
* None `none` - No operation is applied.
* Invert `invert` - Invert the transform.
* Transpose `transpose` - Transpose the transform. This only has an effect for matrix format transforms.
* Invert Transpose `inverttranspose` - Invert and Transpose the transform. The transpose will only be done if the input is a matrix format transform.
Input 1 Pre Operation `input1preop` - ⊞ - Operation(s) to apply on the transforms on Input 1, before they are combined with other transforms.
* None `none` - No operation is applied.
* Invert `invert` - Invert the transform.
* Transpose `transpose` - Transpose the transform. This only has an effect for matrix format transforms.
* Invert Transpose `inverttranspose` - Invert and Transpose the transform. The transpose will only be done if the input is a matrix format transform.
Input Operation `inputoperation` - ⊞ - The operation that should be applied between transforms coming from Input 0 and Input 1. Refer to the main description of this node for an explanation of how multiple samples and/or transform sets are combined between the two inputs.
* Input 0, then Input 1 `input0input1` - The operation will be `input1 * input0`. It it ordered this way since ultimately the transform is applied to a position/vector in the form input1 \* input0 \* Position, so the input0 operation is done first.
* Input 1, then Input 0 `input1input0` - The operation will be `input1 * input0`.
* Quaternion Lerp `quatlerp` -
* Quaternion Slerp `quatslerp` -
Input Weight `inputweight` - Specify the Blend weight for the above 'Input Operation'
  

## Parameters - Transform Page
This page defines an additional transform that can be combined with the transform created by combining the inputs, if any. If the node has no inputs connected then the transform generated from this page will be what is output from this node.
Transform Order `xord` - ⊞ - See description from earlier Transform Order parameter.
* Scale Rotate Translate `srt` -
* Scale Translate Rotate `str` -
* Rotate Scale Translate `rst` -
* Rotate Translate Scale `rts` -
* Translate Scale Rotate `tsr` -
* Translate Rotate Scale `trs` -
Rotate Order `rord` - ⊞ - See description from earlier Rotate Order parameter.
* Rx Ry Rz `xyz` -
* Rx Rz Ry `xzy` -
* Ry Rx Rz `yxz` -
* Ry Rz Rx `yzx` -
* Rz Rx Ry `zxy` -
* Rz Ry Rx `zyx` -
Translate `t` - ⊞ - XYZ translation values.
* X `tx` -
* Y `ty` -
* Z `tz` -
Rotate `r` - ⊞ - XYZ rotation, in degrees.
* X `rx` -
* Y `ry` -
* Z `rz` -
Scale `s` - ⊞ - XYZ scale to shrink or enlarge the transform.
* X `sx` -
* Y `sy` -
* Z `sz` -
Pivot `p` - ⊞ - XYZ pivot to apply the above operations around.
* X `px` -
* Y `py` -
* Z `pz` -
Xform Matrix/CHOP/DAT `xformmatrixop` -
Multiply Order `multiplyorder` - ⊞ - Controls how the input transform(s) are combined with the transform specified on this page. The below two descriptions use a multiply "vector on the right" convention (column vectors).
* Input, then Transform Page `inputxformpage` - The transforms will be combined as `Transform Page * Input`.
* Transform Page, then Input `xformpageinput` - The transforms will be combined as `Input * Transform Page`.
Look At `lookat` - Allows you to generate your transform channels by specifying an object you would like to Look At, or point to. The generated transform channels will be such that when you transform an object using it, it will make the object face your intended Look At Object. This is useful if, for instance, you want a camera to follow another object's movements. The Look At parameter points the object in question at the other object's origin.
**Tip:** To designate a centre of interest for the camera that doesn't appear in your scene, create a Null object and disable its display flag. Then Parent the Camera to the newly created Null object, and tell the camera to look at this object using the Look At parameter. You can direct the attention of the camera by moving the Null object with the Select state. If you want to see both the camera and the Null object, enable the Null object's display flag, and use the Select state in an additional Viewport by clicking one of the icons in the top-right corner of the TouchDesigner window.

Up Vector `upvector` - ⊞ - When orienting an object, the Up Vector is used to determine where the positive Y axis points.
* Up Vector `upvectorx` -
* Up Vector `upvectory` -
* Up Vector `upvectorz` -
Forward Direction `forwarddir` - ⊞ - Sets which axis and direction is considered the forward direction.
* +X `posx` -
* -X `negx` -
* +Y `posy` -
* -Y `negy` -
* +Z `posz` -
* -Z `negz` -
Pre Operation `preop` - ⊞ - Operation(s) to apply on the transform generated by Transform/Rotate/Scale/Pivot parameters, before it is combined with other transforms. Done before combining with the Xform Matrix and Look At.
* None `none` - No operation.
* Invert `invert` - Invert the transform.
Operation `operation` - ⊞ - Controls how the input transform(s) are combined with the transform specified on this page. The below two descriptions use a multiply "vector on the right" convention (column vectors).
* Input, then Transform Page `inputxformpage` -
* Transform Page, then Input `xformpageinput` -
* Quaternion Lerp `quatlerp` -
* Quaternion Slerp `quatslerp` -
Weight `weight` - Specify the Blend weight for the above 'Operation'
  

## Parameters - Output Page
This page controls what information is output from the node.
Post Operation `postop` - ⊞ - Optionally applied one last operation to the final generated transform before it is output.
* None `none` - No operation.
* Invert `invert` - Invert the transform.
* Transpose `transpose` - Transpose the transform. This only has an effect for matrix format transforms.
* Invert Transpose `inverttranspose` - Invert and Transpose the transform. The transpose will only be done if the input is a matrix format transform.
Output `output` - ⊞ - Specify the format the transform will be output in.
* Transform (Euler) `transform` - The standard Translate, Rotate and Scale channels. t[xyz], r[xyz], s[xyz]. Will also include xord and rord channels for Transform and Rotate Order, unless 'Include Order Channels' is turned off.
* Transform (Quaternion) `transformquat` - Translate, Quaternion (for rotation) and Scale channels. t[xyz], q[xyzw], s[xyz]. Will also include xord channel for Transform Order, unless 'Include Order Channels' is turned off.
* 4x4 Matrix `mat` - 16 channels for a 4x4 matrix. The channels will be output in column-by-column order. That is, with the last 4 channels being the 'translate' portion of the matrix.
* 3x3 Matrix `mat3` - 9 channels for a 3x3 matrix. This includes the rotation and the scale, but not the translation.
* Position `position` - The final position of the transform in space. This doesn't include any orientation information.
Determinant `determ` - When outputting a matrix, it's determinant can also be output by enabling this parameter.
Un-matched Channels `unmatchedchans` - ⊞ - Controls how channels that don't match the naming convention for the various transform format are treated.
* Warn `warn` - Give a warning if transform channels that don't match any of the naming convenstions are found.
* Ignore `ignore` - Ignore (give no warning) if channels that don't match the naming convention are found.
* Delete `delete` - Delete all channels that don't match any of the naming conventions.
Custom Output Orders `custoutputorders` - By default the output transforms will use the orders given on teh Transform page. Enabling this allows for custom orders to be used for the transform that is output. This doesn't change the transform itself, but the values of the channels will likely change since they are combined in a different order to obtain the same overall transform.
Transform Order `outxord` - ⊞ - See description from earlier Transform Order parameter.
* Scale Rotate Translate `srt` -
* Scale Translate Rotate `str` -
* Rotate Scale Translate `rst` -
* Rotate Translate Scale `rts` -
* Translate Scale Rotate `tsr` -
* Translate Rotate Scale `trs` -
Rotate Order `outrord` - ⊞ - See description from earlier Rotate Order parameter.
* Rx Ry Rz `xyz` -
* Rx Rz Ry `xzy` -
* Ry Rx Rz `yxz` -
* Ry Rz Rx `yzx` -
* Rz Rx Ry `zxy` -
* Rz Ry Rx `zyx` -
Include Order Channels `includeorderchans` - Specified if the 'xord' and 'rord' channels should be output from this node. 'xord' will be output for 'Transform (Euler)' and 'Transform (Quaternion)' modes. 'rord' will be output for the 'Transform (Euler)' mode. The matrix and position modes do not include orders.
Continuous Rotations `continuousrotations` - In the case the input has multiple samples, this will attempt to keep rotations of neighbouring samples continuous. Basically, it tries to avoid 360 degree jumps. 360-> 361 instead of 360 -> 1 (which is the same two rotations.
Use Rotation Hint `usehint` - An initial rotation hint given in r[xyz] degrees to try to stay continuous against. Turning this on and using the Hint parameter below allows you to specify approximate starting values for the rotation channels produced. This allows you to change the rotation channel solution to a specific starting point (e.g. for camera output control).
Hint `hint` - ⊞ - Specify approximate starting values for the rotation channels produced.
* Hint `hintx` -
* Hint `hinty` -
* Hint `hintz` -
  

## Parameters - Common Page
Time Slice `timeslice` - Turning this on forces the channels to be "[Time Sliced](Time_Slicing.html "Time Slicing")". A Time Slice is the time between the last cook frame and the current cook frame.
Scope `scope` - To determine which channels get affected, some CHOPs use a Scope string on the Common page. See [Pattern Matching](Pattern_Matching.html "Pattern Matching").
Sample Rate Match `srselect` - ⊞ - Handle cases where multiple input CHOPs' sample rates are different. When Resampling occurs, the curves are interpolated according to the Interpolation Method Option, or "Linear" if the Interpolate Options are not available.
* Resample At First Input's Rate `first` - Use rate of first input to resample others.
* Resample At Maximum Rate `max` - Resample to the highest sample rate.
* Resample At Minimum Rate `min` - Resample to the lowest sample rate.
* Error If Rates Differ `err` - Doesn't accept conflicting sample rates.
Export Method `exportmethod` - ⊞ - This will determine how to connect the CHOP channel to the parameter. Refer to the [Export](Export.html "Export") article for more information.
* DAT Table by Index `datindex` - Uses the docked DAT table and references the channel via the index of the channel in the CHOP.
* DAT Table by Name `datname` - Uses the docked DAT table and references the channel via the name of the channel in the CHOP.
* Channel Name is Path:Parameter `autoname` - The channel is the full destination of where to export to, such has `geo1/transform1:tx`.
Export Root `autoexportroot` - This path points to the root node where all of the paths that exporting by **Channel Name is Path:Parameter** are relative to.
Export Table `exporttable` - The DAT used to hold the export information when using the DAT Table Export Methods (See above).
  

## Operator Inputs
* Input 0:  - One or more transform sets, as defined by the allowable formats described at the start of the article.
* Input 1:  - One or more transform sets, as defined by the allowable formats described at the start of the article.
  

## Info CHOP Channels
Extra Information for the Transform CHOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Common CHOP Info Channels
* start - Start of the CHOP interval in samples.
* length - Number of samples in the CHOP.
* sample\_rate - The samplerate of the channels in frames per second.
* num\_channels - Number of channels in the CHOP.
* time\_slice - 1 if CHOP is Time Slice enabled, 0 otherwise.
* export\_sernum - A count of how often the export connections have been updated.
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
  
TouchDesigner Build: Latest\nwikieditorwikieditorwikieditor2023.112802021.100002019.175002018.28070before 2018.28070
| CHOPs |
| --- |
| [Ableton Link](Ableton_Link_CHOP.html "Ableton Link CHOP") • [Analyze](Analyze_CHOP.html "Analyze CHOP") • [Angle](Angle_CHOP.html "Angle CHOP") • [Attribute](Attribute_CHOP.html "Attribute CHOP") • [Audio Band EQ](Audio_Band_EQ_CHOP.html "Audio Band EQ CHOP") • [Audio Binaural](Audio_Binaural_CHOP.html "Audio Binaural CHOP") • [Audio Device In](Audio_Device_In_CHOP.html "Audio Device In CHOP") • [Audio Device Out](Audio_Device_Out_CHOP.html "Audio Device Out CHOP") • [Audio Dynamics](Audio_Dynamics_CHOP.html "Audio Dynamics CHOP") • [Audio File In](Audio_File_In_CHOP.html "Audio File In CHOP") • [Audio File Out](Audio_File_Out_CHOP.html "Audio File Out CHOP") • [Audio Filter](Audio_Filter_CHOP.html "Audio Filter CHOP") • [Audio Movie](Audio_Movie_CHOP.html "Audio Movie CHOP") • [Audio NDI](Audio_NDI_CHOP.html "Audio NDI CHOP") • [Audio Oscillator](Audio_Oscillator_CHOP.html "Audio Oscillator CHOP") • [Audio Para EQ](Audio_Para_EQ_CHOP.html "Audio Para EQ CHOP") • [Audio Play](Audio_Play_CHOP.html "Audio Play CHOP") • [Audio Render](Audio_Render_CHOP.html "Audio Render CHOP") • [Experimental:Audio Render](Experimental_Audio_Render_CHOP.html "Experimental:Audio Render CHOP") • [Audio Spectrum](Audio_Spectrum_CHOP.html "Audio Spectrum CHOP") • [Audio Stream In](Audio_Stream_In_CHOP.html "Audio Stream In CHOP") • [Audio Stream Out](Audio_Stream_Out_CHOP.html "Audio Stream Out CHOP") • [Audio VST](Audio_VST_CHOP.html "Audio VST CHOP") • [Audio Web Render](Audio_Web_Render_CHOP.html "Audio Web Render CHOP") • [Beat](Beat_CHOP.html "Beat CHOP") • [Bind](Bind_CHOP.html "Bind CHOP") • [BlackTrax](BlackTrax_CHOP.html "BlackTrax CHOP") • [Blend](Blend_CHOP.html "Blend CHOP") • [Blob Track](Blob_Track_CHOP.html "Blob Track CHOP") • [Body Track](Body_Track_CHOP.html "Body Track CHOP") • [Bullet Solver](Bullet_Solver_CHOP.html "Bullet Solver CHOP") • [Clip Blender](Clip_Blender_CHOP.html "Clip Blender CHOP") • [Clip](Clip_CHOP.html "Clip CHOP") • [Clock](Clock_CHOP.html "Clock CHOP") • [Composite](Composite_CHOP.html "Composite CHOP") • [Constant](Constant_CHOP.html "Constant CHOP") • [Copy](Copy_CHOP.html "Copy CHOP") • [Count](Count_CHOP.html "Count CHOP") • [CPlusPlus](CPlusPlus_CHOP.html "CPlusPlus CHOP") • [Cross](Cross_CHOP.html "Cross CHOP") • [Cycle](Cycle_CHOP.html "Cycle CHOP") • [DAT to](DAT_to_CHOP.html "DAT to CHOP") • [Delay](Delay_CHOP.html "Delay CHOP") • [Delete](Delete_CHOP.html "Delete CHOP") • [DMX In](DMX_In_CHOP.html "DMX In CHOP") • [DMX Out](DMX_Out_CHOP.html "DMX Out CHOP") • [Envelope](Envelope_CHOP.html "Envelope CHOP") • [EtherDream](EtherDream_CHOP.html "EtherDream CHOP") • [Event](Event_CHOP.html "Event CHOP") • [Expression](Expression_CHOP.html "Expression CHOP") • [Extend](Extend_CHOP.html "Extend CHOP") • [Face Track](Face_Track_CHOP.html "Face Track CHOP") • [Fan](Fan_CHOP.html "Fan CHOP") • [Feedback](Feedback_CHOP.html "Feedback CHOP") • [File In](File_In_CHOP.html "File In CHOP") • [File Out](File_Out_CHOP.html "File Out CHOP") • [Filter](Filter_CHOP.html "Filter CHOP") • [Experimental:Filter](Experimental_Filter_CHOP.html "Experimental:Filter CHOP") • [FreeD In](FreeD_In_CHOP.html "FreeD In CHOP") • [FreeD Out](FreeD_Out_CHOP.html "FreeD Out CHOP") • [Function](Function_CHOP.html "Function CHOP") • [Gesture](Gesture_CHOP.html "Gesture CHOP") • [Handle](Handle_CHOP.html "Handle CHOP") • [Helios DAC](Helios_DAC_CHOP.html "Helios DAC CHOP") • [Hog](Hog_CHOP.html "Hog CHOP") • [Hokuyo](Hokuyo_CHOP.html "Hokuyo CHOP") • [Hold](Hold_CHOP.html "Hold CHOP") • [Import Select](Import_Select_CHOP.html "Import Select CHOP") • [In](In_CHOP.html "In CHOP") • [Info](Info_CHOP.html "Info CHOP") • [Interpolate](Interpolate_CHOP.html "Interpolate CHOP") • [Introduction To s Vid](Introduction_To_CHOPs_Vid.html "Introduction To CHOPs Vid") • [Inverse Curve](Inverse_Curve_CHOP.html "Inverse Curve CHOP") • [Inverse Kin](Inverse_Kin_CHOP.html "Inverse Kin CHOP") • [Join](Join_CHOP.html "Join CHOP") • [Joystick](Joystick_CHOP.html "Joystick CHOP") • [Keyboard In](Keyboard_In_CHOP.html "Keyboard In CHOP") • [Keyframe](Keyframe_CHOP.html "Keyframe CHOP") • [Kinect Azure](Kinect_Azure_CHOP.html "Kinect Azure CHOP") • [Kinect](Kinect_CHOP.html "Kinect CHOP") • [Lag](Lag_CHOP.html "Lag CHOP") • [Laser](Laser_CHOP.html "Laser CHOP") • [Experimental:Laser](Experimental_Laser_CHOP.html "Experimental:Laser CHOP") • [Laser Device](Laser_Device_CHOP.html "Laser Device CHOP") • [Experimental:Laser Device](Experimental_Laser_Device_CHOP.html "Experimental:Laser Device CHOP") • [Leap Motion](Leap_Motion_CHOP.html "Leap Motion CHOP") • [Leuze ROD4](Leuze_ROD4_CHOP.html "Leuze ROD4 CHOP") • [LFO](LFO_CHOP.html "LFO CHOP") • [Limit](Limit_CHOP.html "Limit CHOP") • [Logic](Logic_CHOP.html "Logic CHOP") • [Lookup](Lookup_CHOP.html "Lookup CHOP") • [LTC In](LTC_In_CHOP.html "LTC In CHOP") • [LTC Out](LTC_Out_CHOP.html "LTC Out CHOP") • [Math](Math_CHOP.html "Math CHOP") • [Merge](Merge_CHOP.html "Merge CHOP") • [MIDI In](MIDI_In_CHOP.html "MIDI In CHOP") • [MIDI In Map](MIDI_In_Map_CHOP.html "MIDI In Map CHOP") • [MIDI Out](MIDI_Out_CHOP.html "MIDI Out CHOP") • [MoSys](MoSys_CHOP.html "MoSys CHOP") • [Mouse In](Mouse_In_CHOP.html "Mouse In CHOP") • [Mouse Out](Mouse_Out_CHOP.html "Mouse Out CHOP") • [Ncam](Ncam_CHOP.html "Ncam CHOP") • [Noise](Noise_CHOP.html "Noise CHOP") • [Null](Null_CHOP.html "Null CHOP") • [OAK Device](OAK_Device_CHOP.html "OAK Device CHOP") • [OAK Select](OAK_Select_CHOP.html "OAK Select CHOP") • [Object](Object_CHOP.html "Object CHOP") • [Oculus Audio](Oculus_Audio_CHOP.html "Oculus Audio CHOP") • [Oculus Rift](Oculus_Rift_CHOP.html "Oculus Rift CHOP") • [OpenVR](OpenVR_CHOP.html "OpenVR CHOP") • [OptiTrack In](OptiTrack_In_CHOP.html "OptiTrack In CHOP") • [OSC In](OSC_In_CHOP.html "OSC In CHOP") • [OSC Out](OSC_Out_CHOP.html "OSC Out CHOP") • [Out](Out_CHOP.html "Out CHOP") • [Override](Override_CHOP.html "Override CHOP") • [Panel](Panel_CHOP.html "Panel CHOP") • [Pangolin](Pangolin_CHOP.html "Pangolin CHOP") • [Parameter](Parameter_CHOP.html "Parameter CHOP") • [Pattern](Pattern_CHOP.html "Pattern CHOP") • [Perform](Perform_CHOP.html "Perform CHOP") • [Phaser](Phaser_CHOP.html "Phaser CHOP") • [Pipe In](Pipe_In_CHOP.html "Pipe In CHOP") • [Pipe Out](Pipe_Out_CHOP.html "Pipe Out CHOP") • [PosiStageNet](PosiStageNet_CHOP.html "PosiStageNet CHOP") • [Pulse](Pulse_CHOP.html "Pulse CHOP") • [RealSense](RealSense_CHOP.html "RealSense CHOP") • [Record](Record_CHOP.html "Record CHOP") • [Rename](Rename_CHOP.html "Rename CHOP") • [Render Pick](Render_Pick_CHOP.html "Render Pick CHOP") • [RenderStream In](RenderStream_In_CHOP.html "RenderStream In CHOP") • [Reorder](Reorder_CHOP.html "Reorder CHOP") • [Replace](Replace_CHOP.html "Replace CHOP") • [Resample](Resample_CHOP.html "Resample CHOP") • [S Curve](S_Curve_CHOP.html "S Curve CHOP") • [Scan](Scan_CHOP.html "Scan CHOP") • [Script](Script_CHOP.html "Script CHOP") • [Select](Select_CHOP.html "Select CHOP") • [Sequencer](Sequencer_CHOP.html "Sequencer CHOP") • [Serial](Serial_CHOP.html "Serial CHOP") • [Shared Mem In](Shared_Mem_In_CHOP.html "Shared Mem In CHOP") • [Shared Mem Out](Shared_Mem_Out_CHOP.html "Shared Mem Out CHOP") • [Shift](Shift_CHOP.html "Shift CHOP") • [Shuffle](Shuffle_CHOP.html "Shuffle CHOP") • [Slope](Slope_CHOP.html "Slope CHOP") • [SOP to](SOP_to_CHOP.html "SOP to CHOP") • [Sort](Sort_CHOP.html "Sort CHOP") • [Speed](Speed_CHOP.html "Speed CHOP") • [Splice](Splice_CHOP.html "Splice CHOP") • [Spring](Spring_CHOP.html "Spring CHOP") • [Stretch](Stretch_CHOP.html "Stretch CHOP") • [Stype In](Stype_In_CHOP.html "Stype In CHOP") • [Stype Out](Stype_Out_CHOP.html "Stype Out CHOP") • [Switch](Switch_CHOP.html "Switch CHOP") • [Sync In](Sync_In_CHOP.html "Sync In CHOP") • [Sync Out](Sync_Out_CHOP.html "Sync Out CHOP") • [Tablet](Tablet_CHOP.html "Tablet CHOP") • [Time Slice](Time_Slice_CHOP.html "Time Slice CHOP") • [Timecode](Timecode_CHOP.html "Timecode CHOP") • [Timeline](Timeline_CHOP.html "Timeline CHOP") • [Timer](Timer_CHOP.html "Timer CHOP") • [TOP to](TOP_to_CHOP.html "TOP to CHOP") • [Touch In](Touch_In_CHOP.html "Touch In CHOP") • [Touch Out](Touch_Out_CHOP.html "Touch Out CHOP") • [Trail](Trail_CHOP.html "Trail CHOP") • Transform• [Transform XYZ](Transform_XYZ_CHOP.html "Transform XYZ CHOP") • [Trigger](Trigger_CHOP.html "Trigger CHOP") • [Experimental:Trigger](Experimental_Trigger_CHOP.html "Experimental:Trigger CHOP") • [Trim](Trim_CHOP.html "Trim CHOP") • [Warp](Warp_CHOP.html "Warp CHOP") • [Wave](Wave_CHOP.html "Wave CHOP") • [WrnchAI](WrnchAI_CHOP.html "WrnchAI CHOP") • [ZED](ZED_CHOP.html "ZED CHOP") • [Experimental:ZED](Experimental_ZED_CHOP.html "Experimental:ZED CHOP") |
An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

The sub-[Family](Operator_Family.html "Operator Family") of [Component](Component.html "Component") types that are used to define and render 3D scenes. A [Geometry Component](Geometry_COMP.html "Geometry COMP") is an Object that contains the 3D shapes to render. A [Camera COMP](Camera_COMP.html "Camera COMP") and [Light COMP](Light_COMP.html "Light COMP") are other Object types. Separately, "Objects" also refers to Python objects.

A Time Slice is the time from the last cook frame to the current cook frame. In CHOPs it is the set of short channels that contain the CHOP channels' samples between the last and the current cook frame.

A parameter in most CHOPs that restricts which channels of that CHOP will be affected. Normally all channels of a CHOP are affected by the operator. TOPs have Channel Mask, a similar feature.

samples-per-second of a [CHOP](CHOP.html "CHOP"). Each CHOP in your network has a sample rate. In contrast, the overall timeline has a [Frame Rate](Frame_Rate.html "Frame Rate"), which is the number of frames to [cook](Cook.html "Cook") and display per second, generally your monitor display frequency, default 60.

Exporting is the connection of CHOP channels to parameters of operators. The output of each exporting CHOP is one or more channels, active only while the [CHOP Viewer](CHOP_Viewer.html "CHOP Viewer") is on. The current value of a channel can be exported to a parameter of any operator, overriding that parameter's value. See [Parameter](Parameter.html "Parameter").

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

Every operator in TouchDesigner has a set of control Parameters that can be integer or floating point numbers, menus, binary toggles, text strings or operator [paths](Network_Path.html "Network Path"), which determine the output of the operator.

TouchDesigner is a hierarchy of components. "root" is the top-most network in the hierarchy. The [Network Path](Network_Path.html "Network Path") or Path for root is simply `/`. A typical path is `/project1/moviein1`.

Retrieved from "<https://docs.derivative.ca/index.php?title=Transform_CHOP&oldid=31276>"
[Category](Special_Categories.html "Special:Categories"):
* [CHOPs](Category_CHOPs.html "Category:CHOPs")