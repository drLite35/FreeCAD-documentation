---
 GuiCommand:
   Name: Arch Nest
   MenuLocation: Utils , Panel tools , Nest
   Workbenches: BIM_Workbench
   Version: 0.17
   SeeAlso: Arch_Panel, Arch_Panel_Sheet
---

# Arch Nest/en

## Description

The **Arch Nest** tool allows to select a flat shape to be a container, and a series of other flat shapes to be organized inside the space defined by the container shape. This is typically needed for CNC operations, where you want to cut a series of pieces out of a base panel, and need to organize those pieces in the best possible compact way so they occupy less space on the panel.

The algorithm behind the Nest tool is in constant evolution, and is currently not fully optimized. In the future the performance of this tool should become much better.

<img alt="" src=images/Arch_Nest_example.jpg  style="width:600px;">

*The image above shows a series of shapes before and after the nesting operation.*

## Usage

1.  Select the **Utils → Panel tools → <img src="images/Arch_Nest.svg" width=16px> Nest** option from the menu.
2.  Select an object to be the container. This object must be flat, and, at the moment, rectangular.
3.  Click the **Pick selected** button to use that object as the container.
4.  Select a series of other flat objects that you wish to place inside the container. These objects must all be flat and in the same plane as the container.
5.  Adjust desired options below.
6.  Start the calculation process.
7.  At the end of the calculation, click the **Preview** button to create a temporary preview of the result.
8.  If you wish to apply the result (move and rotate the actual shapes into place), click **OK**.

<img alt="" src=images/Arch_Nest_panel.jpg  style="width:800px;"> 
*Taskview panel for the [Arch Nest](Arch_Nest.md) tool*

## Notes

-   All objects must have a face
-   At the moment the tool will only work with flat objects that all have the same orientation.
-   At the moment, the container must be rectangular.
-   At the moment, margin / spacing between the pieces is not implemented yet
-   The calculation can take a lot of time with many objects. That will be optimized in the future



---
⏵ [documentation index](../README.md) > [BIM](Category_BIM.md) > Arch Nest/en
