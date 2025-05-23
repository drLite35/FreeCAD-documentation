---
 GuiCommand:
   Name: Spreadsheet SetAlias
   MenuLocation: -
   Workbenches: Spreadsheet_Workbench
   Shortcut: **Ctrl**+**Shift**+**A**
   Version: 0.17
---

# Spreadsheet SetAlias/pt-br



## Descrição

The <img alt="" src=images/Spreadsheet_SetAlias.svg  style="width:24px;"> **Spreadsheet SetAlias** tool opens a dialog to set up an alias for a cell. Instead of using the exact cell name like A2, B3, or C4, a custom name can be used.



## Uso

1.  Make sure there is an active [spreadsheet](Spreadsheet_CreateSheet.md).
2.  Select a cell.
3.  There are several ways to invoke the tool:
    -   Press the **[<img src=images/Spreadsheet_SetAlias.svg style="width:16px"> [Set alias](Spreadsheet_SetAlias.md)** button.
    -   Use the keyboard shortcut: **Ctrl**+**Shift**+**A**.
4.  Enter an alias:
    -   Only alphanumeric characters and underscores (`A` to `Z`, `a` to `z`, `0` to `9` and `_`) are allowed.
    -   The first character must be a letter.
    -   Using 1 or 2 capital letters followed by 1 to 5 numbers, for example `AB123`, is not allowed as this is considered a cell address.
    -   Character sequences that are units are not allowed. For example `W` is an invalid alias as it is the unit for [Watt](https://en.wikipedia.org/wiki/Watt). Since FreeCAD supports many units it is best to avoid short aliases. See [Expressions](Expressions#Units.md).
    -   Using the mathematical constants `pi` and `e` as aliases will lead to errors and should be avoided.
    -   Do not use spaces in aliases as they will also lead to errors.





{{Spreadsheet_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [Spreadsheet](Spreadsheet_Workbench.md) > Spreadsheet SetAlias/pt-br
