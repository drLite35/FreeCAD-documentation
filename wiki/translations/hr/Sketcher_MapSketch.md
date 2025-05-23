---
 GuiCommand:
   Name: Sketcher MapSketch
   MenuLocation: Sketch , Attach sketch...
   Workbenches: Sketcher_Workbench, PartDesign_Workbench
   SeeAlso: Sketcher_ReorientSketch, Sketcher_NewSketch
---

# Sketcher MapSketch/hr

## Description

The <img alt="" src=images/Sketcher_MapSketch.svg  style="width:24px;"> [Sketcher MapSketch](Sketcher_MapSketch.md) tool attaches a sketch to selected geometry.

Typical use cases are:

-   The sketch was created on a standard plane (XY, XZ or YZ) and you want to attach it to the face of a solid in order to build a new feature upon it.
-   The sketch was attached to a specific face of a solid but you need to attached it to a different face.
-   A broken model needs to be repaired.

<img alt="" src=images/Sketcher_MapSketch_00.png  style="width:480px;">

## Usage

1.  Select an object with a shape, or one or more vertices, edges, and/or faces, and/or a plane.
2.  There are several ways to invoke the tool:
    -   Press the **<img src="images/Sketcher_MapSketch.svg" width=16px> [Attach sketch...](Sketcher_MapSketch.md)** button.
    -   Select the **Sketch → <img src="images/Sketcher_MapSketch.svg" width=16px> Attach sketch...** option from the menu.
3.  The **Select sketch** dialog opens.
4.  Select a sketch from the dropdown list.
5.  Press the **OK** button.
6.  The **Sketch attachment** dialog opens.
7.  Select an [attachment method](Part_EditAttachment#Attachment_modes.md) from the dropdown list. Or select **Don\'t attach** to detach the sketch.
8.  Press the **OK** button.





{{Sketcher Tools navi

}}



---
⏵ [documentation index](../README.md) > [Sketcher](Sketcher_Workbench.md) > Sketcher MapSketch/hr
