---
 GuiCommand:
   Name:  Sketcher ConstrainHorVer
   MenuLocation: Sketch , Sketcher constraints , Constrain horizontal/vertical
   Workbenches: Sketcher_Workbench
   Shortcut: **A**
   Version: 1.0
   SeeAlso: Sketcher_ConstrainHorizontal, Sketcher_ConstrainVertical
---

# Sketcher ConstrainHorVer/en

## Description

The <img alt="" src=images/Sketcher_ConstrainHorVer.svg  style="width:24px;"> [Sketcher ConstrainHorVer](Sketcher_ConstrainHorVer.md) tool constrains lines or pairs of points to be horizontal (parallel to the horizontal axis of the sketch) or vertical, whichever is closest to the current alignment.

This tool combines the [Sketcher ConstrainHorizontal](Sketcher_ConstrainHorizontal.md) and [Sketcher ConstrainVertical](Sketcher_ConstrainVertical.md) tools.

## Usage

See also: [Drawing aids](Sketcher_Workbench#Drawing_aids.md).

### [Continue mode](Sketcher_Workbench#Continue_modes.md) 

1.  Make sure there is no selection.
2.  There are several ways to invoke the tool:
    -   If the **Auto tool for Horizontal/Vertical** [preference](Sketcher_Preferences#General.md) is selected (default): press the **<img src="images/Sketcher_ConstrainHorVer.svg" width=16px> [Constrain horizontal/vertical](Sketcher_ConstrainHorVer.md)** button.
    -   Select the **Sketch → Sketcher constraints → <img src="images/Sketcher_ConstrainHorVer.svg" width=16px> Constrain horizontal/vertical** option from the menu.
    -   Right-click in the [3D view](3D_view.md) and select the **Constrain → <img src="images/Sketcher_ConstrainHorVer.svg" width=16px> Constrain horizontal/vertical** option from the context menu.
    -   Use the keyboard shortcut: **A**.
3.  The cursor changes to a cross with the tool icon.
4.  Do one of the following:
    -   Select two points.
    -   Select a single line.
5.  A constraint is added.
6.  Optionally keep creating constraints.
7.  To finish, right-click or press **Esc**, or start another geometry or constraint creation tool.

### Run-once mode 

1.  Do one of the following:
    -   Select two or more points (the selection order can be relevant see [Notes](#Notes.md)).
    -   Select one or more lines. Points can be included in the selection, but will be ignored.
2.  Invoke the tool as explained above, or with the following additional option:
    -   Right-click in the [3D view](3D_view.md) and select the **<img src="images/Sketcher_ConstrainHorVer.svg" width=16px> Constrain horizontal/vertical** option from the context menu.
3.  Depending on the selection one or more constraints are added.

## Notes

-   More than 2 points are processed in the selection order, one pair at a time. The 1st point is paired with the 2nd. When they are constrained the 2nd point may move. The new location of the 2nd point determines which constraint is applied when the 2nd and 3rd point are constrained, etc.



---
⏵ [documentation index](../README.md) > [Sketcher](Sketcher_Workbench.md) > Sketcher ConstrainHorVer/en
