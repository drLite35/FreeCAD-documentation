---
 GuiCommand:
   Name: Part JoinEmbed
   MenuLocation: Part , Join , Embed Object
   Workbenches: Part_Workbench
   Version: 0.16
   SeeAlso: Part_JoinConnect, Part_JoinCutout, Part_Boolean, Part_Thickness
---

# Part JoinEmbed/ro


</div>



## Descriere


<div class="mw-translate-fuzzy">

Instrumentul de încorporare încorporează un obiect cu pereți (de exemplu, o țeavă) într-un alt obiect cu pereți.


</div>

![600px](images/JoinFeatures_Embed.png)




<div class="mw-translate-fuzzy">

## Cum se folosește 


</div>


<div class="mw-translate-fuzzy">

1.  Select the base object first, then the object to be embedded. The order of selection is important. It is enough to select one sub-shape of each object (e.g., faces).
2.  Invoke the Part JoinEmbed command.


</div>

## Properties


{{TitleProperty|Base}}


<div class="mw-translate-fuzzy">

## Properties 


{{TitleProperty|Base}}

-    **Base**: Reference to base object (the one the other object is to be embedded into). The object should be a single solid.

-    **Tool**: Reference to tool object (the object to be embedded). The object can be a single solid, or a [valid compound](Part_MakeCompound.md) of solids.

-    **Mode**: The mode of operation, equals \'Embed\' (Changing that will transform the tool into another Part_JoinXXX). The value of \'bypass\' can be used to temporarily disable the long computations (a compound of Base and Tool will be created, which is a fast operation).

-    **Refine**: Sets whether to apply [Refine](Part_RefineShape.md) operation or not, to the final shape. The default value is determined by a \'Automatically refine shape after boolean operation\' checkbox in PartDesign preferences. When Mode property is \'bypass\', Refine is ignored (never applied).


</div>

## Example


<div class="mw-translate-fuzzy">

## Example 

1.  Create a pipe by applying [thickness](Part_Thickness.md) to a [cylinder](Part_Cylinder.md):
    <img alt="" src=images/JoinFeatures_Example_step1.png  style="width:320px;">
2.  Create another, smaller diameter pipe, and [place](Placement.md) it so that it pierces the wall of the first pipe:
    ![320px](images/JoinFeatures_Example_step2.png)
3.  Select the first pipe, then the second pipe (order of selection is important), and click the \'Embed object\' option from the Join tools dropdown toolbar button.
    ![320px](images/JoinFeatures_Example_step3_Embed.png)
4.  Use some cross-section tool ([Clipping plane](Std_ToggleClipPlane.md), [Arch Section Plane](Arch_SectionPlane.md), [Arch Cut Plane](Arch_CutPlane.md)) to reveal internals. On the picture below, Arch Section Plane is used.
    ![320px](images/JoinFeatures_Example_step4_Embed.png)


</div>

## Algorithm


<div class="mw-translate-fuzzy">

## Algorithm 

The algorithms behind Join tools are quite simple, and understanding them is important to use the tools correctly.


</div>


<div class="mw-translate-fuzzy">

1\. Base object is [boolean-cut](Part_Cut.md) with Tool object. The resulting shape is a set ([compound](Part_MakeCompound.md)) of non-intersecting solids (typically, two).


</div>

2\. The resulting compound is filtered: only the largest solid is kept.


<div class="mw-translate-fuzzy">

3\. That largest solid is [boolean-fused](Part_Union.md) with Tool object.


</div>

4\. If Refine property is true, the resulting shape is [refined](Part_RefineShape.md).
![800px](images/JoinFeatures-Algo-Embed.png)

### Notes


<div class="mw-translate-fuzzy">

### Notes 

-   If after step 1, the object remains in one piece, the result of Embed will be equivalent to [union](Part_Union.md) of Base and Tool, but taking longer to compute.
-   Now, the tool will produce unexpected result, if a compound is supplied as Base. This may be changed in the future.
-   Because the largest piece is determined by comparing volumes of pieces, the tool can only work with solids. This may be changed in the future.


</div>



## Script

The Join tools can by used in [macros](macros.md) and from the python console by using the following function:


```pythonJoinFeatures.makePartJoinFeature(name = 'Embed', mode = 'Embed')```

-   Creates an empty Embed feature (or other Join feature, depending on mode passed). The properties Base and Tool must be assigned explicitly, afterwards.
-   Returns the newly created object.

Exempluː


{{code|code=
import JoinFeatures
j = JoinFeatures.makePartJoinFeature(name = 'Embed', mode = 'Embed' )
j.Base = FreeCADGui.Selection.getSelection()[0]
j.Tool = FreeCADGui.Selection.getSelection()[1]
}}


<div class="mw-translate-fuzzy">

The tool itself is implemented in Python, see /Mod/Part/JoinFeatures.py under where FreeCAD is installed.


</div>



---
⏵ [documentation index](../README.md) > [Part](Part_Workbench.md) > Part JoinEmbed/ro
