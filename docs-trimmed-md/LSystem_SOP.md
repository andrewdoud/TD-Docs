

# LSystem_SOP

TouchDesigner Documentation




# LSystem SOP
From Derivative

[Jump to navigation](#mw-head)
[Jump to search](#searchInput)
## Summary[[edit](https://docs.derivative.ca/index.php?title=Template:Summary&action=edit&section=T-1 "Edit section: Summary")]
The Lsystem SOP implements L-systems (Lindenmayer-systems, named after Aristid Lindenmayer (1925-1989)), allow definition of complex shapes through the use of iteration. They use a mathematical language in which an initial string of characters is evaluated repeatedly, and the results are used to generate geometry. The result of each evaluation becomes the basis for the next iteration of geometry, giving the illusion of growth.
You begin building an L-system by defining a sequence of rules which are evaluated to produce a new string of characters. Each character of the new string represents one command which affects an imaginary stylus, or "turtle". Repeating this process will grow your geometry.
You can use L-systems to create things such as:
* Create organic objects such as trees, plants, flowers over time.
* Create animated branching objects such as lightning and snowflakes.
The file can be read in from disk or from the web. Use http:// when specifying a URL.
### The Algorithmic Beauty of Plants
The descriptions located here should be enough to get you started in writing your own L-system rules, however, if you have any serious interests in creating L-systems, you should obtain the book:
```
The Algorithmic Beauty of Plants			
Przemyslaw Prusinkiewicz & Aristid Lindenmayer			
Springer-Verlag, New York, Phone: 212.460.1500			
ISBN: 0-387-94676-4, 1996.			
```
which is the definitive reference on the subject. It contains a multitude of L-systems examples complete with descriptions of the ideas and theories behind modelling realistic plant growth.
[![PythonIcon.png](images/c/c2/PythonIcon.png)](File_PythonIcon.html)[lsystemSOP\_Class](https://docs.derivative.ca/LsystemSOP_Class "LsystemSOP Class")
## Contents
* [1 Summary](#Summary)
  + [1.1 The Algorithmic Beauty of Plants](#The_Algorithmic_Beauty_of_Plants)
* [2 Parameters - Geometry Page](#Parameters_-_Geometry_Page)
* [3 Parameters - Tube Page](#Parameters_-_Tube_Page)
* [4 Parameters - Values Page](#Parameters_-_Values_Page)
* [5 Parameters - Funcs Page](#Parameters_-_Funcs_Page)
* [6 Rule Substitution](#Rule_Substitution)
  + [6.1 Limitations to Rules](#Limitations_to_Rules)
  + [6.2 Turtle Operators](#Turtle_Operators)
* [7 Production Rule Syntax](#Production_Rule_Syntax)
  + [7.1 Context Sensitivity](#Context_Sensitivity)
* [8 Parameter Symbols](#Parameter_Symbols)
* [9 Operator Override](#Operator_Override)
  + [9.1 Examples](#Examples)
  + [9.2 List of Operator Overrides](#List_of_Operator_Overrides)
* [10 Edge Rewriting](#Edge_Rewriting)
* [11 Expressions](#Expressions)
  + [11.1 L-System Specific Expression Functions](#L-System_Specific_Expression_Functions)
  + [11.2 Conditions](#Conditions)
  + [11.3 Probability](#Probability)
* [12 Creating Groups with L-Systems](#Creating_Groups_with_L-Systems)
  + [12.1 Optional Group Parameters](#Optional_Group_Parameters)
* [13 Controlling the Length over Time](#Controlling_the_Length_over_Time)
* [14 Example](#Example)
* [15 Operator Inputs](#Operator_Inputs)
* [16 Info CHOP Channels](#Info_CHOP_Channels)
  + [16.1 Common SOP Info Channels](#Common_SOP_Info_Channels)
  + [16.2 Common Operator Info Channels](#Common_Operator_Info_Channels)
  

## Parameters - Geometry Page
Type `type` - ⊞ - Provides two options for output geometry:
* Skeleton `skel` - Creates wire frame geometry. This option is ideal for geometry that is stiff and jagged like lightning or snowflakes. It is also useful to reduce SOP cooking time.
* Tube `tube` - Creates tube geometry. This option can be used with solid geometry that would need smooth curves, like trees or shrubs. Parameters on the [Tube Page](#Parameters_-_Tube_Page) are only enabled when this Type is selected.
Generations `generations` - Determines the number of times to apply the rules to the initial string. This value controls the growth of the L-system. Place a time-based function here to animate the L-system growth.
Random Scale `randscale` - Random Scale as a percentage. This will apply a random scale to the changing geometry's lengths, angles and thickness.
Random Seed `randseed` - Random Seed for the SOP. This value can be used to select different sequences of random values.
Continuous Angles `contangl` - Calculates the incremental angles of branches, if a non-integer generational value is used. If the Generations field is animating, this should be set to ensure smooth growth.
Continuous Length `contlength` - Calculates the incremental lengths of the geometry points if a non-integer generational value is used. As with Continuous Angles, if the Generations field is animating, this should be set to ensure smooth, continuous growth. The Continuous Width field applies to tube thickness.
Continuous Width `contwidth` - Calculates the incremental lengths of the geometry points if a non-integer generational value is used. As with Continuous Angles, if the Generations field is animating, this should be set to ensure smooth, continuous growth. The Continuous Width field applies to tube thickness.
Apply Color `docolor` - Use a TOP to apply color to the L-system as it grows.
Image File `colormap` - Defines a TOP to use when the Apply Color button is selected. Also see the ` and # turtle operators.
UV Increment `inc` - ⊞ - Defines the default color U, V index increments when the turtle symbols ` or # are used.
* `incu` -
* `incv` -
Point Width Attribute `pointwidth` - Adds a point `width` attribute to each point in the geometry. This width is effected by the Thickness and Thickness Scale parameters on the Tube Page.
  

## Parameters - Tube Page
The parameters on this page are active only if [Geometry Page](#Parameters_-_Geometry_Page) > Type has been set to the Tube type.
Rows `rows` - The first option sets the number of tube sides and the second sets the number of divisions per step length if tube geometry is selected.
Columns `cols` - The first option sets the number of tube sides and the second sets the number of divisions per step length if tube geometry is selected.
Tension `tension` - Tension defines the smoothness of branching corners.
Branch Blend `smooth` - Enabling this option allows a child branch to be continuously joined to its parent branch.
Thickness `thickinit` - This number defines the default tube thickness.
Thickness Scale `thickscale` - This number is the scale factor used with the ! or ? operator.
Apply Tube Texture Coordinates `dotexture` - When enabled, UV texture coordinates are applied to the tube segments, such that the texture wraps smoothly and continuously over branches.
Vertical Increment `vertinc` - Defines the vertical spacing of texture coordinates over tube geometry when tube texture is applied.
  

## Parameters - Values Page
Step Size `stepinit` - Step Size allows you to define the default length of the edges when new geometry is generated.
Step Size Scale `stepscale` - Step Size Scale defines the scale by which the geometry will be modified by the " or \_ (double quote, or underscore) turtle operators.
Angle `angleinit` - Angle defines the default turning angle for turns, rolls and pitches.
Angle Scale `anglescale` - Angle Scale allows you to enter the scaling factor to be employed when the ; or @ operators are used.
Variable b `varb` - Substitutes user-defined b, c and d variables in rules or premise. These variables are expanded and so may include system variables such as `$F` and `$T`.
Variable c `varc` - Substitutes user-defined b, c and d variables in rules or premise. These variables are expanded and so may include system variables such as `$F` and `$T`.
Variable d `vard` - Substitutes user-defined b, c and d variables in rules or premise. These variables are expanded and so may include system variables such as `$F` and `$T`.
Gravity `gravity` - This parameter determines the amount of gravity applied to the geometry via the T (tropism vector) turtle operator. **Tropism** is when a plant bends or curves in response to an external stimulus. L-systems employ a tropism vector to simulate this behaviour. The bending is characterised by the fact that the thicker or shorter parts bend less than the longer or thinner parts.
  

## Parameters - Funcs Page
The parameters on this page allow you to stamp your leaf geometry (each copy can be different) as opposed to simply copying them. See the example in [Example - Stamping L-system Leaves](#Example_-_Stamping_L-system_Leaves).
Pic Image TOP `pictop` - This is the TOP which the pic() function uses. See [#Expressions L-system Specific Expression Functions](#Expressions_L-system_Specific_Expression_Functions) below.
Group Prefix `grpprefix` - If the production g(n) is encountered, all subsequent geometry is included in a primitive group prefixed with this label and ending with the ascii value of n. See [#CreateGroup Creating Groups within L-systems](#CreateGroup_Creating_Groups_within_L-systems) below for an example.
Channel Prefix `chanprefix` - If the expression chan(n) is encountered, it is replaced with the local channel prefixed with this label and ending with the ascii value of n.
Leaf Param A `stampa` - You can determine which parameters are used by leaves.  
 See [#CreateGroup Creating Groups within L-systems](#CreateGroup_Creating_Groups_within_L-systems) below for an example.
Leaf Param B `stampb` - You can determine which parameters are used by leaves.  
 See [#CreateGroup Creating Groups within L-systems](#CreateGroup_Creating_Groups_within_L-systems) below for an example.
Leaf Param C `stampc` - You can determine which parameters are used by leaves.  
 See [#CreateGroup Creating Groups within L-systems](#CreateGroup_Creating_Groups_within_L-systems) below for an example.
Rules DAT `rules` - Path to the DAT defining the rules for the LSystem.
* Context Ignore `context_ignore:` - Defining this in the Rules DAT specifies all characters which are to be skipped when testing context sensitivity in the rules below.
* Premise `premise:` - Define an initial string of characters to which the substitution rules are applied.
* Rules - This is where the turtle substitution rules are defined.
  

## Rule Substitution
You create the highly structured organic and branching objects using L-systems grammar. An L-system is a process in which a sequence of rules are applied to an initial string of characters to create a new string. To build the geometry, each character of the final string represents one command which affects an imaginary stylus, or "turtle".
The process begins by examining the first character of the premise string. All sixteen rules are searched sequentially until an applicable rule is found. The current character is then replaced with one or more characters as defined by the rule. The remaining characters in the premise string are replaced in a similar fashion. The entire process is repeated once for each generation.
### Limitations to Rules
* Polygon {} and branch [] operators can be nested 30 levels deep
* Rules can be 256 characters in length
* Variables can have up to 5 parameters
* Up to 25 rules can be defined
  

### Turtle Operators
`F` Move forward (creating geometry)
`H` Move forward half the length (creating geometry)
`G` Move forward but don't record a vertex
`f` Move forward (no geometry created)
`h` Move forward a half length (no geometry created)
`J K M` Copy geometry source J, K or M at the turtle's position   
 after rescaling and reorienting the geometry.
`T` Apply tropism vector
`+` Turn right
`-` Turn left (minus sign)
`&` Pitch up
`^` Pitch down
`\` Roll clockwise
`/` Roll counter-clockwise
`|` Turn 180 degrees
`*` Roll 180 degrees
`~` Pitch / Roll / Turn random amount
`"` Multiply current length
`!` Multiply current thickness
`;` Multiply current angle
`_` Divide current length (underscore)
`?` Divides current width
`@` Divide current angle
`'` Increment color index U (single quote)
`#` Increment color index V
`%` Cut off remainder of branch
`$` Rotate `up' towards the sun about heading
`[` Push turtle state (start a branch)
`]` Pop turtle state (end a branch)
`{` Start a polygon
`.` Make a polygon vertex
`}` End a polygon
`g` Create a new primitive group to which subsequent geometry is added
  

## Production Rule Syntax
A Touch L-system rule is specified as:
[**lc**<] **pred** [>**rc**] [:**cond**]=**succ** [:**prob**]
where:
* **lc** - Optional left context
* **pred** - predecessor symbol to be replaced
* **rc** - Optional right context
* **cond** - Condition expression (optional)
* **succ** - Replacement string
* **prob** - Probability of rule execution (optional)
### Context Sensitivity
The most basic type of rule is:
**pred** = **succ**
In this case, a character is replaced with the characters of **succ** if, and only if, it matches **pred**.
For example:
Premise: `ABC`  
Rule 1: `B=DOG`
will result in `ADOGC`
**pred** can only specify one letter, but left and right context symbols can be specified. The general syntax is [**lc**<] **pred** [>**rc**] = **succ**.
**For example:**
Premise: `ABC`  
 Rule 1: `A<B=DOG`
again results in `ADOGC` because `B` is preceded by `A`. If the rule were: `Z<B=DOG` or `B>A=DOG` the rule would not be applied.
  

## Parameter Symbols
Each symbol can have up to five user-defined variables associated with it which can be referenced or assigned in expressions. Variables in the predecessor are instanced while variables in the successor are assigned.
For example:
The rule `A(i, j) = A(i+1, j-1)`, will replace each `A` with a new `A` in which the first parameter has been incremented and the second parameter decremented.
Note that the variables in the predecessor can also be referenced by the condition or probability portions of the rule.
For example:
The rule `A(i):i<5 = A(i+1) A(i+1)`, will double each `A` a maximum of five times (assuming a Premise of `A(0)`).  

Parameters assigned to geometric symbols (e.g. `F`, `+`, or `!`) are interpreted geometrically.
For example:
The rule `F(i, j) = F(0.5*i, 2*j)`, will again replace each `F` with a new `F` containing modified parameters. In addition to this, the new `F` will now be drawn at half the length and twice the width.
  

## Operator Override
Normally turtle symbols use the current length/angle/thickness etc. to determine their effect. By providing a turtle operator with an explicit parameter, it will override the value normally used by the turtle operator.
Override parameters for `F`, `f`, `G`, `h`, `H` take the form of:
> `F(i,j,k,l,m)`
* **`i`** - Override Length.
* **`j`** - Override Thickness.
* `k` - Override # Tube Segments.
* `l` - Override # Tube Rows.
* `m` - User parameter.
The **k** and **l** override parameters allow dynamic resolution of tube segments.
### Examples
**`F`** - Moves forward current length creating geometry.
 **`H`** - Moves forward half current length creating geometry.
`F(i, j)` - Moves forward a distance of `i,` creating geometry of thickness `j`.
 **`H(i, j)`** - Move forward half the distance of `i`, creating geometry of thickness half of `j`.
**`+`** - Turn by current angle amount.   
 **`~`** - Rotate by random angle.
**`+(i)`** - Turn by i degrees.  
 **`~(i)`** - Override random angle with value of `i`.
`$(x0,y0,z0)` - Points the turtle to location `(x0,y0,z0)`.
Given the above, the Premise:
`F(1) +(90) F(1) +(90) F(1) +(90) F(1)`
generates a unit box regardless of the default Step Size or Angle settings.
  

### List of Operator Overrides
The following list describes the geometric interpretation of parameters assigned to certain turtle symbols:
[![TouchGeometry84.gif](https://docs.derivative.ca/images/3/3a/TouchGeometry84.gif)](https://docs.derivative.ca/File:TouchGeometry84.gif)
  
[![TouchGeometry93.gif](https://docs.derivative.ca/images/0/0f/TouchGeometry93.gif)](https://docs.derivative.ca/File:TouchGeometry93.gif)
  
[![TouchGeometry98.gif](https://docs.derivative.ca/images/9/91/TouchGeometry98.gif)](https://docs.derivative.ca/File:TouchGeometry98.gif)
  

## Edge Rewriting
In The Algorithmic Beauty of Plants, many examples use a technique called Edge Rewriting which involve left and right subscripts. A typical example might look like:
Generations `10`  
Angle `90`  
Premise `F(l)`  
Rules  
`F(l) = F(l)+F(r)+  
 F(r) = -F(l)-F(r)`
However, Touch doesn't know what `F(l)` and `F(r)` are. In this case, we can modify the rules to use parameter passing. For the `F` turtle symbol, the first four parameters are length, width, tubesides, and tubesegs, leaving the last parameter user-definable. We can define this last parameter such that `0` is left, and `1` is right:
Generations `10`  
Angle `90`  
Premise `F(1,1,3,3,0)`  
Rules
After two generations this produces: `Fl+Fr+-Fl-Fr`. There should not be any difference between this final string and `F+F+-F-F.`
Another approach is to use two new variables, and use a conditional statement on the final step to convert them to `F`:
Variable b `ch("generations")`  
Premise `l`  
Rules   
`l:t<b=l+r+  
 r:t<b=-l-r  
 l=F  
 r=F`  
**Output** `l`  
`F`  
`F+F+`  
`F+F++-F-F+`
  

## Expressions
In the earlier example, the expressions `0.5*i` and `2*j` are used. In fact, expressions can be used anywhere a numeric field is expected. Currently the following symbols can be used in expressions:
`( )` - brackets for nesting priority
`^ + - * / %` - arithmetic operators
`min() max() sin() cos() asin() acos() pic() in()` - supported functions
`== != = < <= > >=` - logical operators
`& | !` - logical operators: and, or, not
`b c d` - SOP b, c, d parameters after expansion
`x y z` - current turtle position
`g` - age of symbol
`t` - time (generations) of L-system
`a` - SOP angle parameter
`T` - SOP tropism (gravity) parameter
The pre-defined variables above should not be used in the arguments of the predecessor.
**For example:** `A(a,b) = B(a*2,b*2)` is wrong (a is the SOP Angle parameter). `a<b (A,B) = b(A+1,B)` is right.
The last statement is correct because `a` and `b` are used as symbols and not variable names. `A` and `B` are correct because variable names are case sensitive.
### L-System Specific Expression Functions
* **`pic(u, v, c)`** - Using the image specified with Pic Image File, this function returns a normalized value (between `0` and `1`) of the pixel at the normalized coordinates `(u,v)`; `c` selects one of four channels to examine:  
  `0`  
  `1`  
  `2`  
  `3`
* **`in(q, r, s)`** - Given a MetaTest input source containing a metaball geometry, this function returns a `1` if the point `(q, r, s)` is contained within the metaball, and `0` if not. Use `in(x, y, z)` (the letters `x`, `y`, and `z` are special and contain the X, Y, and Z location of the turtle) to test whether or not the turtle is currently inside the metaball to create pruned outputs.
  

### Conditions
Each rule may have an optional condition specified. The syntax is:
[lc<] pred [>rc]:cond = succ
**For example:**
The Rule1 `A:y>2=J` includes source `J` at all `A`'s above the height of `2`.
  

### Probability
Each rule can specify the probability that it is used (provided it is otherwise applicable). The syntax is:
[lc<] pred [>rc]:cond=succ=prob
**For example:**
Rule1 `A=B:0.5`  
Rule2 `A=C:0.5` 
will replace `A` with either `B` or  `C` with equal probability.
  

## Creating Groups with L-Systems
There is a group operator '**`g`'** which lumps all geometry currently being built into group g.
**For example:** `g[F]` lumps geometry from F into a group called `lsys0`. You can set the lsys prefix from the [Funcs page](#Parameters_-_Funcs_Page).
### Optional Group Parameters
`g` takes an optional parameter as well.
**For example:** `g(1)[F]` lumps geometry from `f` into a group called `lsys1`. If no parameter is given, the default index is bumped up appropriately.
The current group container is pushed/popped with the turtle state so you can do things like:
`gF [ gFF] F` - The first and last `F`'s are put into group `0`, and the middle `FF`'s are put into group `1`. 
`gF [ FF] F` - The geometry from all four `F`'s are put into group `0`, (pushing the turtle adopts the parent's group).
To exclude the middle `FF` from the parent's group type: `gF [ g(-1)FF ] F`
  

## Controlling the Length over Time
To create an L-system which goes forward X percent less for each iteration, you need to start your Premise with a value, and then within a rule, multiply that value by the percentage you want to remain:
Premise `A(1)`  
Rule `A(i) = F(i)A(i*0.5)`
This way "`i`" is scaled before `A` is again evaluated. The important part is the Premise. You need to start with a value to be able to scale that value.
  

## Example
**Step 1)** Place a [Circle SOP](Circle_SOP.html "Circle SOP"), and set the Number of Divisions to`: param("lsys", 3`)
It then displays a triangle (3 is default value).
**Step 2)** Pipe this into the J input of a L-System SOP. If the L-system Premise is:
`J A`  
`J(,,4) A`  
`J(,,5) A`
This way, you can customize each leaf before it gets copied.
**Step 3)** Change the Premise and Rule to:
Premise`A(0)`  
Rule1`A(i)=FJ(,,i+3)A(i+1)`
This creates a line of increasing-order polygons.
**Step 4)** Finally, we will want to create 20 leaves, and put them all into a [Switch SOP](Switch_SOP.html "Switch SOP"). Do this by entering the following expression into the Switch SOP's Select Input: `param("lsys",0)`  
**Step 5)** Then in your L-system, J(,,0) gives you the first SOP, J(,,1) gives you the second, and so on. This solves the problem of a limited number of leaves using only JKM.
Also note that these examples use only the first stamp parameter, you can use up to three parameters: e.g. J(,,1,2,3)
The first two parameters of J, K, M are used to override length and width, like symbol F.
  

## Operator Inputs
* Input 0:  -
* Input 1:  -
* Input 2:  -
* Input 3:  -
  

## Info CHOP Channels
Extra Information for the LSystem SOP can be accessed via an [Info CHOP](Info_CHOP.html "Info CHOP").

### Common SOP Info Channels
* num\_points - Number of points in this SOP.
* num\_prims - Number of primitives in this SOP.
* num\_particles - Number of particles in this SOP.
* last\_vbo\_update\_time - Time spent in another thread updating geometry data on the GPU from the SOP's CPU data. As it is part of another thread, this time is not part of the usual frame time.
* last\_meta\_vbo\_update\_time - Time spent in another thread updating meta surface geometry data (such as metaballs or nurbs) on the GPU from the SOP's CPU data. As it is part of another thread, this time is not part of the usual frame time.
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
| SOPs |
| --- |
| [Add](Add_SOP.html "Add SOP") • [Alembic](Alembic_SOP.html "Alembic SOP") • [Align](Align_SOP.html "Align SOP") • [Arm](Arm_SOP.html "Arm SOP") • [Attribute Create](Attribute_Create_SOP.html "Attribute Create SOP") • [Attribute](Attribute_SOP.html "Attribute SOP") • [Basis](Basis_SOP.html "Basis SOP") • [Blend](Blend_SOP.html "Blend SOP") • [Bone Group](Bone_Group_SOP.html "Bone Group SOP") • [Boolean](Boolean_SOP.html "Boolean SOP") • [Box](Box_SOP.html "Box SOP") • [Bridge](Bridge_SOP.html "Bridge SOP") • [Cache](Cache_SOP.html "Cache SOP") • [Cap](Cap_SOP.html "Cap SOP") • [Capture Region](Capture_Region_SOP.html "Capture Region SOP") • [Capture](Capture_SOP.html "Capture SOP") • [Carve](Carve_SOP.html "Carve SOP") • [CHOP to](CHOP_to_SOP.html "CHOP to SOP") • [Circle](Circle_SOP.html "Circle SOP") • [Clay](Clay_SOP.html "Clay SOP") • [Clip](Clip_SOP.html "Clip SOP") • [Convert](Convert_SOP.html "Convert SOP") • [Copy](Copy_SOP.html "Copy SOP") • [CPlusPlus](CPlusPlus_SOP.html "CPlusPlus SOP") • [Creep](Creep_SOP.html "Creep SOP") • [Curveclay](Curveclay_SOP.html "Curveclay SOP") • [Curvesect](Curvesect_SOP.html "Curvesect SOP") • [DAT to](DAT_to_SOP.html "DAT to SOP") • [Deform](Deform_SOP.html "Deform SOP") • [Delete](Delete_SOP.html "Delete SOP") • [Divide](Divide_SOP.html "Divide SOP") • [Extrude](Extrude_SOP.html "Extrude SOP") • [Face Track](Face_Track_SOP.html "Face Track SOP") • [Facet](Facet_SOP.html "Facet SOP") • [File In](File_In_SOP.html "File In SOP") • [Fillet](Fillet_SOP.html "Fillet SOP") • [Fit](Fit_SOP.html "Fit SOP") • [Font](Font_SOP.html "Font SOP") • [Force](Force_SOP.html "Force SOP") • [Fractal](Fractal_SOP.html "Fractal SOP") • [Grid](Grid_SOP.html "Grid SOP") • [Group](Group_SOP.html "Group SOP") • [Hole](Hole_SOP.html "Hole SOP") • [Import Select](Import_Select_SOP.html "Import Select SOP") • [In](In_SOP.html "In SOP") • [Introduction To s Vid](Introduction_To_SOPs_Vid.html "Introduction To SOPs Vid") • [Inverse Curve](Inverse_Curve_SOP.html "Inverse Curve SOP") • [Iso Surface](Iso_Surface_SOP.html "Iso Surface SOP") • [Join](Join_SOP.html "Join SOP") • [Joint](Joint_SOP.html "Joint SOP") • [Kinect](Kinect_SOP.html "Kinect SOP") • [Lattice](Lattice_SOP.html "Lattice SOP") • [Limit](Limit_SOP.html "Limit SOP") • [Line](Line_SOP.html "Line SOP") • [Line Thick](Line_Thick_SOP.html "Line Thick SOP") • [LOD](LOD_SOP.html "LOD SOP") • LSystem• [Magnet](Magnet_SOP.html "Magnet SOP") • [Material](Material_SOP.html "Material SOP") • [Merge](Merge_SOP.html "Merge SOP") • [Metaball](Metaball_SOP.html "Metaball SOP") • [Model](Model_SOP.html "Model SOP") • [Noise](Noise_SOP.html "Noise SOP") • [Null](Null_SOP.html "Null SOP") • [Object Merge](Object_Merge_SOP.html "Object Merge SOP") • [Oculus Rift](Oculus_Rift_SOP.html "Oculus Rift SOP") • [OpenVR](OpenVR_SOP.html "OpenVR SOP") • [Out](Out_SOP.html "Out SOP") • [Particle](Particle_SOP.html "Particle SOP") • [Point](Point_SOP.html "Point SOP") • [Polyloft](Polyloft_SOP.html "Polyloft SOP") • [Polypatch](Polypatch_SOP.html "Polypatch SOP") • [Polyreduce](Polyreduce_SOP.html "Polyreduce SOP") • [Polyspline](Polyspline_SOP.html "Polyspline SOP") • [Polystitch](Polystitch_SOP.html "Polystitch SOP") • [Primitive](Primitive_SOP.html "Primitive SOP") • [Profile](Profile_SOP.html "Profile SOP") • [Project](Project_SOP.html "Project SOP") • [Rails](Rails_SOP.html "Rails SOP") • [Raster](Raster_SOP.html "Raster SOP") • [Ray](Ray_SOP.html "Ray SOP") • [Rectangle](Rectangle_SOP.html "Rectangle SOP") • [Refine](Refine_SOP.html "Refine SOP") • [Resample](Resample_SOP.html "Resample SOP") • [Revolve](Revolve_SOP.html "Revolve SOP") • [Script](Script_SOP.html "Script SOP") • [Select](Select_SOP.html "Select SOP") • [Sequence Blend](Sequence_Blend_SOP.html "Sequence Blend SOP") • [Skin](Skin_SOP.html "Skin SOP") • [Sort](Sort_SOP.html "Sort SOP") • [Sphere](Sphere_SOP.html "Sphere SOP") • [Spring](Spring_SOP.html "Spring SOP") • [Sprinkle](Sprinkle_SOP.html "Sprinkle SOP") • [Sprite](Sprite_SOP.html "Sprite SOP") • [Stitch](Stitch_SOP.html "Stitch SOP") • [Subdivide](Subdivide_SOP.html "Subdivide SOP") • [Superquad](Superquad_SOP.html "Superquad SOP") • [Surfsect](Surfsect_SOP.html "Surfsect SOP") • [Sweep](Sweep_SOP.html "Sweep SOP") • [Switch](Switch_SOP.html "Switch SOP") • [Text](Text_SOP.html "Text SOP") • [Texture](Texture_SOP.html "Texture SOP") • [Torus](Torus_SOP.html "Torus SOP") • [Trace](Trace_SOP.html "Trace SOP") • [Trail](Trail_SOP.html "Trail SOP") • [Transform](Transform_SOP.html "Transform SOP") • [Trim](Trim_SOP.html "Trim SOP") • [Tristrip](Tristrip_SOP.html "Tristrip SOP") • [Tube](Tube_SOP.html "Tube SOP") • [Twist](Twist_SOP.html "Twist SOP") • [Vertex](Vertex_SOP.html "Vertex SOP") • [Wireframe](Wireframe_SOP.html "Wireframe SOP") • [ZED](ZED_SOP.html "ZED SOP") • [Experimental:ZED](Experimental_ZED_SOP.html "Experimental:ZED SOP") |
A [Operator Family](Operator_Family.html "Operator Family") that reads, creates and modifies 3D points, polygons, lines, particles, surfaces, spheres and meatballs. Particles and point clouds are now done primarily on the GPU using TOPs.

An [Operator Family](Operator_Family.html "Operator Family") that creates, composites and modifies images, and reads/writes images and movies to/from files and the network. TOPs run on the graphics card's GPU.

Each SOP has a list of Points. Each point has an XYZ 3D position value plus other optional attributes. Each polygon [Primitive](Primitive.html "Primitive") is defined by a vertex list, which is list of point numbers.

An [Operator Family](Operator_Family.html "Operator Family") that manipulates text strings: multi-line text or tables. Multi-line text is often a python [Script](Script.html "Script") or [GLSL](GLSL.html "GLSL") Shader, but can be any multi-line text. [Tables](Table_DAT.html "Table DAT") are rows and columns of cells, each containing a text string.

The location of an operator within the TouchDesigner environment, for example, `/geo1/circle1`, a node called `circle1` in a component called `geo1`. The path `/` is called [Root](Root.html "Root"). This path is displayed at the top of every [Pane](Pane.html "Pane"), showing which Component's network you are currently in. To refer instead to a filesystem folder, directory, disk file or `http:` address, see [Folder](Folder.html "Folder").

A polygon is a type of [Primitive](Primitive.html "Primitive") that is formed from a set of [Vertices](Vertex.html "Vertex") in 3D that are implicitly connected together to form a multi-edge shape.

A text string that contains data (string, float, list, boolean, etc.) and operators (+ \* < etc) that are evaluated by the node's language (python or Tscript) and returns a string, float list or boolean, etc. Expressions are used in parameters, [DATs](DAT.html "DAT") and in scripts.

A way of moving data from one TouchDesigner process to another. Images are moved via Touch Out / In TOPs, channels are moved via Touch Out / In CHOPs and Pipe Out / In CHOPs. Data moves via TCP/IP or UDP.

An [Operator Family](Operator_Family.html "Operator Family") which operate on [Channels](Channel.html "Channel") (a sequence of numbers ([Samples](Sample.html "Sample"))) which are used for animation, audio, mathematics, simulation, logic, UI construction, and data streamed from/to devices and protocols.

The Graphics Processing Unit. This is the high-speed, many-core processor of the graphics card/chip that takes geometry, images and data from the CPU and creates images and processed data.

Retrieved from "<https://docs.derivative.ca/index.php?title=LSystem_SOP&oldid=24204>"
[Category](Special_Categories.html "Special:Categories"):
* [SOPs](https://docs.derivative.ca/index.php?title=Category:SOPs&action=edit&redlink=1 "Category:SOPs (page does not exist)")