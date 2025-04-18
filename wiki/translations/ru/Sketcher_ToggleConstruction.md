---
 GuiCommand:
   Name/ru: Переключить построительную геометрию
   Name: Sketcher_ToggleConstruction
   MenuLocation: Sketch , Геометрия эскиза , Переключить построительную геометрию
   Workbenches: Sketcher_Workbench/ru
---

# Sketcher ToggleConstruction/ru


</div>



## Описание


<div class="mw-translate-fuzzy">

Этот инструмент переключает геометрию эскиза из/в вспомогательный режим. Может использоваться для любого типа геометрии: линии, дуги или круга.


</div>


<div class="mw-translate-fuzzy">

Вспомогательная геометрия является важным инструментом в создании эскизов. При использовании эскиза для 3D-операций вспомогательная геометрия игнорируется.


</div>

<img alt="" src=images/Sketcher_ConstructionMode_fr_01.png  style="width:480px;">



## Применение

### Toggle tools 

1.  Make sure there is no selection.
2.  There are several ways to invoke the tool:
    -   Press the **<img src="images/Sketcher_ToggleConstruction.svg" width=16px> [Toggle construction geometry](Sketcher_ToggleConstruction.md)** button.
    -   Select the **Sketcher → Sketcher geometries → <img src="images/Sketcher_ToggleConstruction.svg" width=16px> Toggle construction geometry** option from the menu.
    -   Right-click in the [3D view](3D_view.md) and select the **<img src="images/Sketcher_ToggleConstruction.svg" width=16px> Toggle construction geometry** option from the context menu.
    -   Use the keyboard shortcut: **G** then **N**.
3.  The mode of the geometry creation tools is toggled:
    -   In normal mode their menu and toolbar icons are white, and they create regular geometry (default color white). The icon of this tool is then: <img alt="" src=images/Sketcher_ToggleConstruction.svg  style="width:16px;">.
    -   In construction mode their menu and toolbar icons are blue, and they create construction geometry (default color blue). The icon of this tool is then: <img alt="" src=images/Sketcher_ToggleConstruction_Constr.svg  style="width:16px;">.

### Toggle geometry 

1.  Select one or more elements in the sketch.
2.  Invoke the tool as described above, or with the following additional option:
    -   Right-click in the **Elements** section of the [Sketcher Dialog](Sketcher_Dialog.md) and select the **<img src="images/Sketcher_ToggleConstruction.svg" width=16px> Toggle construction geometry** option from the context menu.
3.  The selected elements are changed from normal geometry to construction geometry or vice versa. Their appearance changes accordingly.
4.  The mode of the geometry creation tools is not changed.


<div class="mw-translate-fuzzy">





</div>



---
⏵ [documentation index](../README.md) > [Sketcher](Sketcher_Workbench.md) > Sketcher ToggleConstruction/ru
