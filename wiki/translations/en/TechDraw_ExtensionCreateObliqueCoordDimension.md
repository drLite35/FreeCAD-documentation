---
 GuiCommand:
   Name: TechDraw ExtensionCreateObliqueCoordDimension
   MenuLocation: TechDraw , Extensions: Dimensions , Create Oblique Coordinate Dimensions
   Workbenches: TechDraw_Workbench
   Shortcut: 
   Version: 0.20
   SeeAlso: TechDraw_ExtensionCreateHorizCoordDimension, TechDraw_ExtensionCreateVertCoordDimension
---

# TechDraw ExtensionCreateObliqueCoordDimension/en

## Description

The **TechDraw ExtensionCreateObliqueCoordDimension** tool creates oblique coordinate dimensions: multiple evenly spaced dimensions starting from the same baseline.

<img alt="" src=images/TechDraw_ExtensionCreateObliqueCoordDimensionExample.png  style="width:400px;"> 
*On the right the created dimensions*

## Usage

1.  Optionally specify the cascade spacing with the <img alt="" src=images/TechDraw_ExtensionSelectLineAttributes.svg  style="width:16px;"> [TechDraw ExtensionSelectLineAttributes](TechDraw_ExtensionSelectLineAttributes.md) tool.
2.  Select three or more vertexes.
3.  The selection order of the first two vertexes determines the position of the baseline. If the vertex that is selected first is to the left of the second, the baseline is created at the leftmost vertex, else it is created at the rightmost vertex.
4.  The first two vertexes also define the direction.
5.  There are several ways to invoke the tool:
    -   
        <small>(v1.0)</small> 
        
        : If the **Dimensioning tools** [preference](TechDraw_Preferences#Dimensions.md) is set to {{Value|Single tool}} (default): press the down arrow to the right of the **<img src="images/TechDraw_Dimension.svg" width=|x16px><img src="images/Toolbar_flyout_arrow.svg" width=x16px>** button and select the **<img src="images/TechDraw_ExtensionCreateObliqueCoordDimension.svg" width=16px> Create Oblique Coordinate Dimensions** option from the dropdown.

    -   If this preference has a different value (and in {{VersionMinus|0.21}}): press the **<img src="images/TechDraw_ExtensionCreateObliqueCoordDimension.svg" width=16px> [Create Oblique Coordinate Dimensions](TechDraw_ExtensionCreateObliqueCoordDimension.md)** button.

    -   Select the **TechDraw → Extensions: Dimensions → <img src="images/TechDraw_ExtensionCreateObliqueCoordDimension.svg" width=16px> Create Oblique Coordinate Dimensions** option from the menu.
6.  Coordinate dimensions with centered dimension texts are created.





{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw ExtensionCreateObliqueCoordDimension/en
