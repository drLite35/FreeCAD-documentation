---
 GuiCommand:
   Name: TechDraw Dimension Angle
   Name/es: TechDraw Dimensión Ángulo
   MenuLocation: TechDraw , Dimensión Ángulo
   Workbenches: TechDraw_Workbench/es
   SeeAlso: TechDraw_3PtAngleDimension/es
---

# TechDraw AngleDimension/es


</div>



## Descripción

The **TechDraw AngleDimension** tool adds an angular dimension to a View. The dimension shows the interior angle between two straight edges.

<img alt="" src=images/TechDraw_Dimension_Angle_example.png  style="width:200px;"> 
*Measuring the angle between two straight edges*



## Utilización

1.  Select two straight edges. The geometry may be selected in the [3D view](3D_view.md) or in the drawing.
2.  If you have selected geometry in the 3D view: add the correct TechDraw View to the selection by selecting it in the [Tree view](Tree_view.md).
3.  There are several ways to invoke the tool:
    -   
        <small>(v1.0)</small> 
        
        : If the **Dimensioning tools** [preference](TechDraw_Preferences#Dimensions.md) is set to {{Value|Single tool}} (default): press the down arrow to the right of the **<img src="images/TechDraw_Dimension.svg" width=|x16px><img src="images/Toolbar_flyout_arrow.svg" width=x16px>** button and select the **<img src="images/TechDraw_AngleDimension.svg" width=16px> Insert Angle Dimension** option from the dropdown.

    -   If this preference has a different value (and in {{VersionMinus|0.21}}): press the **<img src="images/TechDraw_AngleDimension.svg" width=16px> [Insert Angle Dimension](TechDraw_AngleDimension.md)** button.

    -   Select the **TechDraw → Dimensions → <img src="images/TechDraw_AngleDimension.svg" width=16px> Insert Angle Dimension** option from the menu.
4.  A dimension is added to the View.
5.  The dimension may be dragged to the desired position.
6.  If needed, add tolerances as described on [this page](TechDraw_Geometric_dimensioning_and_tolerancing#Tolerances.md).

### Display 3D measurement 

See [TechDraw LengthDimension](TechDraw_LengthDimension#Display_3D_measurement.md).

### Change properties 

To change the properties of a dimension object either double-click it in the drawing or in the [Tree view](Tree_view.md). This will open the [Dimension dialog](TechDraw_LengthDimension#Dimension_dialog.md).



## Limitaciones

Dimension objects are vulnerable to the \"[topological naming problem](Topological_naming_problem.md)\". See [TechDraw LengthDimension](TechDraw_LengthDimension.md).

## Notes

See [TechDraw LengthDimension](TechDraw_LengthDimension#Notes.md).



## Propiedades

See [TechDraw LengthDimension](TechDraw_LengthDimension#Properties.md).


<div class="mw-translate-fuzzy">





</div>


{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw AngleDimension/es
