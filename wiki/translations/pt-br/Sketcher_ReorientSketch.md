---
 GuiCommand:-br
   Name: Sketcher Reorient
   Name/pt-br: Sketcher Reorient
   Empty: 1
   Workbenches: Sketcher Workbench/pt-br, PartDesign Workbench/pt-br
   MenuLocation: Part design , Reorient sketch
   SeeAlso: Sketcher_MapSketch/pt-br, Sketcher_NewSketch/pt-br
---

# Sketcher ReorientSketch/pt-br


</div>

## Description

The <img alt="" src=images/Sketcher_ReorientSketch.svg  style="width:24px;"> [Sketcher ReorientSketch](Sketcher_ReorientSketch.md) tool places a sketch on one of the main planes with an optional offset. It can also be used to detach a sketch.

## Usage

1.  Select a sketch.
2.  There are several ways to invoke the tool:
    -   Press the **<img src="images/Sketcher_ReorientSketch.svg" width=16px> [Reorient sketch](Sketcher_ReorientSketch.md)** button (not available in the [PartDesign Workbench](PartDesign_Workbench.md)).
    -   Select the **Sketch → <img src="images/Sketcher_ReorientSketch.svg" width=16px> Reorient sketch** option from the menu.
3.  If the sketch is attached:
    1.  The **Sketch has support** dialog opens.
    2.  Press the **Yes** button to detach the sketch.
4.  The **Choose orientation** dialog opens.
5.  Optionally press the **Cancel** button to only detach the sketch and finish the tool.
6.  Specify the plane for the orientation. The plane is relative to the local coordinate system the sketch is in:
    -   If the **Reverse direction** checkbox is not checked:
        -   Top: **XY-Plane**
        -   Front: **XZ-Plane**
        -   Right: **YZ-Plane**
    -   If the **Reverse direction** checkbox is checked:
        -   Bottom: **XY-Plane**
        -   Rear: **XZ-Plane**
        -   Left: **YZ-Plane**
7.  Optionally change the **Offset**. The offset is measured along the Z, Y or X axis of the local coordinate system.
8.  Press the **OK** button.





{{Sketcher Tools navi

}}



---
⏵ [documentation index](../README.md) > [Sketcher](Sketcher_Workbench.md) > Sketcher ReorientSketch/pt-br
