---
 GuiCommand:
   Name/ru: Показать/скрыть внутреннюю геометрию
   Name: Sketcher_RestoreInternalAlignmentGeometry
   MenuLocation: Sketch , Инструменты для эскиза , Показать/скрыть внутреннюю геометрию
   Workbenches: Sketcher_Workbench/ru
   Shortcut: Ctrl+Shift+E
   SeeAlso: 
---

# Sketcher RestoreInternalAlignmentGeometry/ru


</div>



## Описание

The <img alt="" src=images/Sketcher_RestoreInternalAlignmentGeometry.svg  style="width:24px;"> [Sketcher RestoreInternalAlignmentGeometry](Sketcher_RestoreInternalAlignmentGeometry.md) tool deletes the internal geometry of elements, or recreates missing internal geometry. The tool does not delete internal geometry that has associated constraints.



## Применение

1.  Select one or more sketch elements that support internal geometry ([ellipse](Sketcher_CreateEllipseByCenter.md), [arc of ellipse](Sketcher_CreateArcOfEllipse.md), [arc of hyperbola](Sketcher_CreateArcOfHyperbola.md), [arc of parabola](Sketcher_CreateArcOfParabola.md) or [B-spline](Sketcher_CreateBSpline.md)).
2.  There are several ways to invoke the tool:
    -   Press the **<img src="images/Sketcher_RestoreInternalAlignmentGeometry.svg" width=16px> [Show/hide internal geometry](Sketcher_RestoreInternalAlignmentGeometry.md)** button.
    -   Select the **Sketch → Sketcher visual → <img src="images/Sketcher_RestoreInternalAlignmentGeometry.svg" width=16px> Show/hide internal geometry** option from the menu.
    -   Use the keyboard shortcut: **Z** then **I**.
3.  Internal geometry is deleted for selected elements with a complete set of internal geometry, else missing internal geometry is recreated.


<div class="mw-translate-fuzzy">





</div>



---
⏵ [documentation index](../README.md) > [Sketcher](Sketcher_Workbench.md) > Sketcher RestoreInternalAlignmentGeometry/ru
