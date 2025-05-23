---
 GuiCommand:
   Name: Draft Snap Special
   Workbenches: Draft Workbench, Arch Workbench
   MenuLocation: Draft , Draft Snap , Special
   Shortcut: 
   SeeAlso: 
---

# Draft Snap Special/ro


</div>

## Description


<div class="mw-translate-fuzzy">

### Descriere

Când această locație de ancorare este activată, sunt disponibile locații speciale de ancorare definite de obiect. Acestea includ:


</div>

![](images/Draft_Snap_Special_example.png ) 
*Snapping the second point of a line to a special point of an  Arch Wall, which is a vertex of its Base object*

## Usage

For general information about snapping see [Draft Snap](Draft_Snap.md).

1.  Make sure snapping is enabled. See <img alt="" src=images/Draft_Snap_Lock.svg  style="width:16px;"> [Draft Snap Lock](Draft_Snap_Lock.md).
2.  If **Draft Snap Special** is not active do one of the following:
    -   Press the **<img src="images/Draft_Snap_Special.svg" width=16px> [Snap special](Draft_Snap_Special.md)** button in the Draft snap toolbar.
    -   [Draft](Draft_Workbench.md): Hold down the **<img src="images/Draft_Snap_Lock.svg" width=x16px><img src="images/Toolbar_flyout_arrow.svg" width=x16px>** button in the [Draft snap widget](Draft_snap_widget.md) and in the menu that opens select the **<img src="images/Draft_Snap_Special.svg" width=16px> Snap special** option.
    -   [BIM](BIM_Workbench.md): Select the **Snapping → <img src="images/Draft_Snap_Special.svg" width=16px> Snap special** option from the menu, or from the [3D view](3D_view.md) context menu.
3.  Choose a Draft or BIM command to create your geometry.
4.  Note that you can also change snap options while a command is active.
5.  Move the cursor over a supported object.
6.  The object is highlighted.
7.  If a special point is found the point is marked and the <img alt="" src=images/Draft_Snap_Special.svg  style="width:16px;"> icon is displayed near the cursor.
8.  If the object has multiple special points: optionally move the cursor closer to another special point.
9.  Click to confirm the point.

## Supported special points 

-   The vertices of the **Base** object of <img alt="" src=images/Arch_Wall.svg  style="width:16px;"> [Arch Walls](Arch_Wall.md).
-   The **Placement** point of <img alt="" src=images/Arch_Structure.svg  style="width:16px;"> [Arch Structures](Arch_Structure.md).
-   The **Snap Points** of <img alt="" src=images/Arch_Equipment.svg  style="width:16px;"> [Arch Equipment](Arch_Equipment.md).

## Preferences

See [Draft Snap](Draft_Snap#Preferences.md).



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft Snap Special/ro
