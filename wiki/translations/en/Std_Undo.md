---
 GuiCommand:
   Name: Std Undo
   MenuLocation: Edit , Undo
   Workbenches: All
   Shortcut: **Ctrl**+**Z**
   SeeAlso: Std_Redo
---

# Std Undo/en

## Description

The **Std Undo** command undoes the last action.

## Usage

1.  There are several ways to invoke the command:
    -   Press the **<img src="images/Std_Undo.svg" width=16px> [Undo](Std_Undo.md)** button.
    -   Select the **Edit → <img src="images/Std_Undo.svg" width=16px> Undo** option from the menu.
    -   Use the keyboard shortcut: **Ctrl**+**Z**.

## Options

-   To undo multiple actions click on the small black down arrow to the right of the **<img src="images/Std_Undo.svg" width=16px> [Undo](Std_Undo.md)** button and select from the list.

## Preferences

See also: [Preferences Editor](Preferences_Editor.md).

-   The Undo/Redo functionality can be disabled by unchecking the **Edit → Preferences... → General → Document → Using Undo/Redo on documents** option. But this is not recommended.
-   The maximum number of Undo/Redo steps is controlled by **Edit → Preferences... → General → Document → Maximum Undo/Redo steps**.

## Scripting

See also: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

To undo the last action use the `undo` method of the document object. Its counterpart, the `redo` method, is also available.


```python
import FreeCAD

FreeCAD.ActiveDocument.undo()
```

When running FreeCAD in pure console mode (CLI), the undo/redo mechanism isn\'t enabled by default. It must be explicitly activated for each document.


```python
import FreeCAD

FreeCAD.ActiveDocument.UndoMode = 1
```



---
⏵ [documentation index](../README.md) > Std Undo/en
