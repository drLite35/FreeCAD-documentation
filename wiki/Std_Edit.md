---
 GuiCommand:
   Name: Std Edit
   MenuLocation: Edit , Toggle Edit mode
   Workbenches: All
   SeeAlso: Std_UserEditMode
---

# Std Edit

## Description

The **Std Edit** command activates or deactivates an object\'s edit mode.

## Usage

1.  If no object is in edit mode: select a single object.
2.  Select the **Edit → <img src="images/Std_Edit.svg" width=16px> Toggle Edit mode** option from the menu.
3.  Either the default edit mode of the selected object is activated or the existing edit mode deactivated.

## Notes

-   Some tools will be disabled (greyed-out) in the user interface while an object\'s edit mode is active.
-   Not all object types have an edit mode.
-   The functionality available in edit mode depends on the object type.
-   An object\'s edit mode can also be activated by double-clicking it in the [Tree view](Tree_view.md). In that case the edit mode that is used can be defined with the [Std UserEditMode](Std_UserEditMode.md) command.

## Scripting

See also: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

To activate an object\'s edit mode use the `setEdit` method of the document object. This method is not available if FreeCAD is in console mode.

 
```python
import FreeCADGui

FreeCADGui.ActiveDocument.setEdit("myObjectName",0)
```

The second argument is the EditMode. The following options are available:

0 = Default
1 = Transform
2 = Cutting
3 = Color

To deactivate an object\'s edit mode use the `resetEdit` method of the document object.

 
```python
import FreeCADGui

FreeCADGui.ActiveDocument.resetEdit()
```



---
⏵ [documentation index](../README.md) > Std Edit
