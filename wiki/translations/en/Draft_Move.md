---
 GuiCommand:
   Name: Draft Move
   MenuLocation: Modification , Move<br>Modify , Move
   Workbenches: Draft_Workbench, BIM_Workbench
   Shortcut: **M** **V**
   Version: 0.7
   SeeAlso: Draft_SubelementHighlight
---

# Draft Move/en

## Description

The <img alt="" src=images/Draft_Move.svg  style="width:24px;"> **Draft Move** command moves or copies selected objects from one point to another. In subelement mode the command moves selected points and edges, or copies selected edges, of [Draft Lines](Draft_Line.md) and [Draft Wires](Draft_Wire.md).

The command can be used on 2D objects created with the [Draft Workbench](Draft_Workbench.md) or [Sketcher Workbench](Sketcher_Workbench.md), but also on many 3D objects such as those created with the [Part Workbench](Part_Workbench.md), [PartDesign Workbench](PartDesign_Workbench.md) or [BIM Workbench](BIM_Workbench.md).

<img alt="" src=images/Draft_Move_example.jpg  style="width:400px;"> 
*Moving an object from one point to another*

## Usage

See also: [Draft Snap](Draft_Snap.md) and [Draft Constrain](Draft_Constrain.md).

1.  Optionally select one or more objects, or one or more subelements of [Draft Lines](Draft_Line.md) or [Draft Wires](Draft_Wire.md).
2.  There are several ways to invoke the command:
    -   Press the **<img src="images/Draft_Move.svg" width=16px> [Move](Draft_Move.md)** button.
    -   [Draft](Draft_Workbench.md): Select the **Modification → <img src="images/Draft_Move.svg" width=16px> Move** option from the menu.
    -   [BIM](BIM_Workbench.md): Select the **Modify → <img src="images/Draft_Move.svg" width=16px> Move** option from the menu.
    -   Use the keyboard shortcut: **M** then **V**.
3.  If you have not yet selected an object: select an object in the [3D view](3D_view.md).
4.  The **Move** task panel opens. See [Options](#Options.md) for more information.
5.  If subelements have been selected: check the **Modify subelements** checkbox to switch on subelement mode.
6.  Pick the first point, the base point, in the [3D view](3D_view.md), or type coordinates and press the **<img src="images/Draft_AddPoint.svg" width=16px> Enter point** button.
7.  Pick the second point, the target point, in the [3D view](3D_view.md), or type coordinates and press the **<img src="images/Draft_AddPoint.svg" width=16px> Enter point** button.

## Options

The single character keyboard shortcuts available in the task panel can be changed. See [Draft Preferences](Draft_Preferences.md). The shortcuts mentioned here are the default shortcuts (for version 1.0).

-   To manually enter coordinates enter the X, Y and Z component, and press **Enter** after each. Or you can press the **<img src="images/Draft_AddPoint.svg" width=16px> Enter point** button when you have the desired values. It is advisable to move the pointer out of the [3D view](3D_view.md) before entering coordinates.
-   To use polar coordinates enter a value for the **Length** and a value for the **Angle**, and press **Enter** after each.
-   Check the **Angle** checkbox to constrain the pointer to the specified angle.
-   Press **L** to change the focus from the **X** input box to the **Length** input box and back. Depending on the input box that receives the focus the **Angle** checkbox is checked or unchecked.
-   Press **R** or click the **Relative** checkbox to toggle relative mode. If relative mode is on, the coordinates of the second point are relative to the first point, else they are relative to the coordinate system origin.
-   Press **G** or click the **Global** checkbox to toggle global mode. If global mode is on, coordinates are relative to the global coordinate system, else they are relative to the [working plane](Draft_SelectPlane.md) coordinate system.
-   Press **N** or click the **Continue** checkbox to toggle continue mode. If continue mode is on, the command will restart after finishing. This mode really only makes sense if copy mode is switched on. Depending on the **Select base objects after copying** preference, either the original objects are selected for the next command call or the copies that were created last. See [Preferences](#Preferences.md).
-   Press **C** or click the **Copy** checkbox to toggle copy mode. If copy mode is on, the command will create moved copies instead of moving the original objects.
-   Press **B** or click the **Modify subelements** checkbox to toggle subelement mode. If subelement mode is on, the command will use the selected subelements instead of the whole objects. The subelements must belong to [Draft Lines](Draft_Line.md) or [Draft Wires](Draft_Wire.md).
-   If copy mode and subelement mode are both on, and edges of [Draft Wires](Draft_Wire.md) are selected, new wires will be created from those edges.
-   Holding down **Alt** after picking the base point will also toggle copy mode. While **Alt** is held down multiple target points can be picked. Release **Alt** to finish the command and see the created copies.
-   Press **S** to switch [Draft snapping](Draft_Snap.md) on or off.
-   Press **Esc** or the **Close** button to abort the command.

## Notes

-   An Object that is [attached](Part_EditAttachment.md) cannot be moved with the Draft Move command. To move it either its **Support** object has to be moved, or its **Attachment Offset** has to be changed.

## Preferences

See also: [Preferences Editor](Preferences_Editor.md) and [Draft Preferences](Draft_Preferences.md).

-   To change the initial focus of the task panel to the **Length** input box: **Edit → Preferences... → Draft → General → Set focus on Length instead of X coordinate**. Note that you must move the pointer in the [3D view](3D_view.md) for the change to take effect.
-   To reselect the base objects after copying objects: **Edit → Preferences... → Draft → General → Select base objects after copying**.

## Scripting

See also: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

To move objects use the `move` method of the Draft module.


```python
moved_list = move(objectslist, vector, copy=False)
```

-    `objectslist`contains the objects to be moved. It is either a single object or a list of objects.

-    `vector`is the displacement.

-   If `copy` is `True` copies are created instead of moving the original objects.

-    `moved_list`is returned with the original moved objects, or with the new copies. It is either a single object or a list of objects, depending on `objectslist`.

Example:


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

polygon1 = Draft.make_polygon(5, radius=1000)
polygon2 = Draft.make_polygon(3, radius=500)
polygon3 = Draft.make_polygon(6, radius=220)

Draft.move(polygon1, App.Vector(500, 500, 0))
Draft.move(polygon1, App.Vector(500, 500, 0))
Draft.move(polygon2, App.Vector(1000, -1000, 0))
Draft.move(polygon3, App.Vector(-500, -500, 0))

list1 = [polygon1, polygon2, polygon3]

vector = App.Vector(-2000, -2000, 0)
list2 = Draft.move(list1, vector, copy=True)
list3 = Draft.move(list1, -2*vector, copy=True)

doc.recompute()
```



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft Move/en
