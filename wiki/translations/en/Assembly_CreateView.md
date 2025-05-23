---
 GuiCommand:
   Name: Assembly CreateView
   MenuLocation: Assembly , Create Exploded View
   Workbenches: Assembly_Workbench
   Shortcut: **V**
   Version: 1.0
   SeeAlso: 
---

# Assembly CreateView/en

## Description

The <img alt="" src=images/Assembly_CreateView.svg  style="width:24px;"> [Assembly CreateView](Assembly_CreateView.md) tool creates an exploded views container (Exploded_Views object) in the active Assembly that contains one (default) or more exploded views (Exploded_View objects). An assembly can only hold one exploded views container.

An exploded view collects the moves (Move objects) used to relocate parts from assembled position to exploded position. The altered positions of assembled parts and the representations of the moves are only visible when an exploded view is being edited and in TechDraw views derived from an exploded view.

## Usage

1.  Make sure an assembly is active.
2.  There are several ways to invoke the tool:
    -   Press the **<img src="images/Assembly_CreateView.svg" width=16px> [Create Exploded View](Assembly_CreateView.md)** button.
    -   Select the **Assembly → <img src="images/Assembly_CreateView.svg" width=16px> Create Exploded View** option from the menu.
    -   Use the keyboard shortcut: **E**.
3.  If no Exploded_Views object pre-exists: An Exploded_Views container is added to the active assembly.
4.  An Exploded_View object is added to the Exploded_Views container.
5.  The **Create Exploded View** dialog opens in the [task panel](Task_panel.md).
6.  Optionally check **Parts as single solid** checkbox to\...
7.  Optionally choose one way to add a Move:
    -   Explode radially:
        1.  Press **Explode radially**
        2.  All parts are selected and a dragger (see [Notes](#Notes.md)) appears.
        3.  Optionally realign the dragger by selecting one option from the **Align dragger to\...** drop-down list.
            -   Align to\...
                1.  Select an edge or a face of any part to align the dragger.
            -   Align to part center.
                1.  The dragger is aligned according to the grounded part\'s center.
            -   Align to part origin.
                1.  The dragger is aligned according to the grounded part\'s origin.
        4.  Move the dragger by one or more of the following options (only the offset from the start point counts, each part\'s direction is calculated separately):
            -   Press and hold the left mouse button on an axis arrow and drag to translate the object along that axis.
            -   Press and hold the left mouse button on a plane and drag to translate the object along that plane.
            -   Press and hold the left mouse button on a sphere and drag to rotate the object around that axis.
        5.  A Move (see [Notes](#Notes.md)) is added once the left mouse button is released.
    -   Explode along separate movements:
        1.  Select one or more parts.
        2.  A dragger appears.
        3.  Optionally realign the dragger (see above).
        4.  Move the dragger as described above (the directions according to the dragger handles are taken into account).
        5.  A Move is added once the left mouse button is released.
        6.  Optionally select/deselect parts and/or repeat dragging to add more Moves.
8.  Do one of the following:
    -   Press the **OK** button to confirm and finish the tool.
    -   Press the **Cancel** button to revert all changes and finish the tool.
9.  All parts are moved back into their assembly position and the connecting lines are hidden.

## Notes

-   The dragger is a tool similar to the transformation manipulator (<img alt="" src=images/Std_TransformManip.svg  style="width:16px;"> [Std TransformManip](Std_TransformManip.md)), but without an **Increments** task panel.
-   A Move object in the [tree view](Tree_view.md) is represented in the [3D view](3D_view.md) by a dashed red line for each part involved in this move. These connecting lines are only visible when this tool is running, or in a TechDraw view that is derived from an Exploded_View object.
-   To add an exploded view to a TechDraw page: switch to the [TechDraw Workbench](TechDraw_Workbench.md), add a page, select the exploded view object in the tree, and click [Insert View](TechDraw_View.md).

## Properties

See also: [Property editor](Property_editor.md).

Exploded_Views containers are {{Incode|Assembly::ViewGroup}} objects. Exploded_View objects are derived from the {{Incode|ExplodedView}} class, and Move objects from the {{Incode|ExplodedViewStep}} class.

### Assembly::ViewGroup

#### Data


{{TitleProperty|Base}}

-    **Label|String**:

-    **Label2|String|Hidden**:

-    **Expression Engine|ExpressionEngine|Hidden**:

-    **Visibility|Bool|Hidden**:

-    **Group|LinkList**:

-    **_ Group Touched|Bool|Hidden**:

#### View


{{TitleProperty|Display Options}}

-    **Display Mode|Enumeration**:

-    **Show In Tree|Bool**:

-    **Visibility|Bool**:


{{TitleProperty|Selection}}

-    **On Top When Selected|Enumeration**:

-    **Selection Style|Enumeration**:

### ExplodedView

An **ExplodedView** object is derived from an [App FeaturePython](App_FeaturePython.md) object and inherits all its properties. It also has the following additional properties:

#### Data 


{{TitleProperty|Exploded View}}

-    **Moves|LinkList**: List of the Move objects of the exploded view.

### ExplodedViewStep

An **ExplodedViewStep** object is derived from an [App FeaturePython](App_FeaturePython.md) object and inherits all its properties. It also has the following additional properties:

#### Data 


{{TitleProperty|Exploded Move}}

-    **Move Type|Enumeration**: The Type of the move. ({{Value|Normal}}, {{Value|Radial}}).

-    **Movement Transform|Placement**: This is the movement of the move.

    :   The end placement is the result of the start placement \* this placement.

-    **Obj Names|StringList**: The objects moved by the move.

-    **Parts|LinkList**: The containing parts of objects moved by the move.





{{Assembly_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [Assembly](Assembly_Workbench.md) > Assembly CreateView/en
