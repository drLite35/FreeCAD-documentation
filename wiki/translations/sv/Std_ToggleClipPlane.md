---
 GuiCommand:
   Name: Std ToggleClipPlane
   Name/sv: Std ToggleClipPlane
   MenuLocation: View , Clipping plane‏‎
   Workbenches: All
   Shortcut: 
   SeeAlso: 
---

# Std ToggleClipPlane/sv


</div>

## Description

The **Std ToggleClipPlane** command temporarily hides objects and parts of objects on one side of up to three virtual planes in the active [3D view](3D_view.md).

![](images/Std_ToggleClipPlane_example.png ) 
*A clipped hollow object*

![](images/Std_ToggleClipPlane_Dialog.png ) 
*The Clipping dialog box*

## Usage

1.  Select the **View → <img src="images/Std_ToggleClipPlane.svg" width=16px> Clipping plane** option from the menu.
2.  The **Clipping** dialog box opens.
3.  Do one of the following:
    -   Check one or more of the **Clipping X** to **Clipping Z** checkboxes.
        -   Optionally change the offset distance(s).
        -   Optionally press the **Flip** button(s) to change the side of the clipping plane objects are hidden on.
    -   Check the **Clipping custom direction** checkbox.
        -   Optionally change the offset distance.
        -   Do one of the following:
            -   Press the **View** button to use the direction of the current view.
            -   Check the **Adjust to view direction** checkbox for a direction that dynamically adepts to view changes.
            -   Specify the direction by entering the X, Y and Z coordinates of a normal vector.
4.  Optionally change the view to inspect the model.
5.  Press the **Close** button to close the task panel and finish the command.

## Notes

-   To clearly distinguish the interior of partially clipped objects change their **Lighting** property to {{Value|One side}}. The color of the interior side of their faces will then depend on the backlight settings: **Edit → Preferences... → Display → 3D View → Backlight color - Intensity**. See [Preferences Editor](Preferences_Editor#3D_View.md).



---
⏵ [documentation index](../README.md) > Std ToggleClipPlane/sv
