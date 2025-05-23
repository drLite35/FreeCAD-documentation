---
 GuiCommand:
   Name/ru: Указать радиус
   Name: TechDraw_RadiusDimension
   MenuLocation: TechDraw , Размеры , Указать радиус
   Workbenches: TechDraw_Workbench/ru
   SeeAlso: TechDraw_DiameterDimension/ru
---

# TechDraw RadiusDimension/ru



## Описание

The **TechDraw RadiusDimension** tool adds a radius dimension to a View. The dimension may be applied to any edge which is a circle or circular arc.

<img alt="" src=images/TechDraw_Dimension_Radius_example.png  style="width:130px;"> 
*Measuring a circle, indicating the radius*



## Применение

1.  Select a circle or circular arc. The geometry may be selected in the [3D view](3D_view.md) or in the drawing. Note some arcs which appear to be circular are actually ellipses or B-splines. You cannot make a radius dimension in these cases.
2.  If you have selected geometry in the 3D view: add the correct TechDraw View to the selection by selecting it in the [Tree view](Tree_view.md).
3.  There are several ways to invoke the tool:
    -   
        <small>(v1.0)</small> 
        
        : If the **Dimensioning tools** [preference](TechDraw_Preferences#Dimensions.md) is set to {{Value|Single tool}} (default): press the down arrow to the right of the **<img src="images/TechDraw_Dimension.svg" width=|x16px><img src="images/Toolbar_flyout_arrow.svg" width=x16px>** button and select the **<img src="images/TechDraw_RadiusDimension.svg" width=16px> Insert Radius Dimension** option from the dropdown.

    -   If this preference has a different value (and in {{VersionMinus|0.21}}): press the **<img src="images/TechDraw_RadiusDimension.svg" width=16px> [Insert Radius Dimension](TechDraw_RadiusDimension.md)** button.

    -   Select the **TechDraw → Dimensions → <img src="images/TechDraw_RadiusDimension.svg" width=16px> Insert Radius Dimension** option from the menu.
4.  A dimension is added to the View.
5.  The dimension may be dragged to the desired position.
6.  If needed, add tolerances as described on [this page](TechDraw_Geometric_dimensioning_and_tolerancing#Tolerances.md).

### Display 3D measurement 

See [TechDraw LengthDimension](TechDraw_LengthDimension#Display_3D_measurement.md).

### Change properties 

To change the properties of a dimension object either double-click it in the drawing or in the [Tree view](Tree_view.md). This will open the [Dimension dialog](TechDraw_LengthDimension#Dimension_dialog.md).



## Ограничения

Dimension objects are vulnerable to the \"[topological naming problem](Topological_naming_problem.md)\". See [TechDraw LengthDimension](TechDraw_LengthDimension.md).

## Notes

See [TechDraw LengthDimension](TechDraw_LengthDimension#Notes.md).



## Свойства

See [TechDraw LengthDimension](TechDraw_LengthDimension#Properties.md).



## Программирование


**См. так же:**

[TechDraw API](TechDraw_API/ru.md) и [Основы составления скриптов FreeCAD](FreeCAD_Scripting_Basics/ru.md).

The Radius Dimension tool can be used in [macros](Macros.md) and from the [Python](Python.md) console by using the following functions:


```python
dim1 = FreeCAD.ActiveDocument.addObject("TechDraw::DrawViewDimension", "Dimension")
dim1.Type = "Radius"
dim1.References2D=[(view1, "Edge1")]
page.addView(dim1)
```





{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw RadiusDimension/ru
