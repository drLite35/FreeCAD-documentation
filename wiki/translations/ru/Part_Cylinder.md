---
 GuiCommand:
   Name/ru: Цилиндр
   MenuLocation: Деталь , Примитивы , Цилиндр
   Workbenches: Part_Workbench/ru
   SeeAlso: Part_Primitives/ru
---

# Part Cylinder/ru



## Описание


<div class="mw-translate-fuzzy">

Создаёт простой цилиндр с параметрами расположение, угол, радиус и длина.


</div>

A Part Cylinder can be turned into a segment of a cylinder by changing its **Angle** property.

<img alt="" src=images/Part_Cylinder_Example.png  style="width:400px;">



## Применение


<div class="mw-translate-fuzzy">

1.  Нажмите на <img alt="" src=images/Workbench_Part.svg  style="width:16px;"> [Верстак Part](Part_Workbench/ru.md)
2.  Существует несколько способов вызова команды:
    -   Нажмите на иконку **<img src="images/Part_Cylinder.svg" width=16px> Цилиндр** на панели инструментов.
    -   Выберите из меню **Деталь → Примитивы → <img src="images/Part_Cylinder.svg" width=16px> Цилиндр**.


</div>

## Example

![Part Cylinder from the scripting example](images/Part_Cylinder_Scripting_Example.png )

A Part Cylinder object created with the [scripting example](#Scripting.md) below is shown here.

## Notes

-   A Part Cylinder can also be created with the <img alt="" src=images/Part_Primitives.svg  style="width:16px;"> [Part Primitives](Part_Primitives.md) command. With that command you can specify the dimensions and placement at creation time.



## Свойства

See also: [Property editor](Property_editor.md).

A Part Cylinder object is derived from a [Part Feature](Part_Feature.md) object and inherits all its properties. It also has the following additional properties:

### Data


{{TitleProperty|Attachment}}

The object has the same attachment properties as a [Part Part2DObject](Part_Part2DObject#Data.md).


{{TitleProperty|Cylinder}}

-    **Radius|Length**: The radius of the circular arc that defines the cylinder. The default is {{Value|2mm}}.

-    **Height|Length**: The height of the cylinder. The default is {{Value|10mm}}.

-    **Angle|Angle**: The angle of the circular arc that defines the cylinder. Valid range: {{Value|0° &lt; value &lt;&#61; 360°}}. The default is {{Value|360°}}. If it is smaller than {{Value|360°}} the resulting solid will be a segment of a cylinder.


{{TitleProperty|Prism}}

-    **First Angle|Angle**: The angle between the extrusion direction of the cylinder and its positive Z axis, measured around its Y axis. The angle is positive towards its positive X axis. Valid range: {{Value|0° &lt;&#61; value &lt; 90°}}. The default is {{Value|0°}}. <small>(v0.20)</small> 

-    **Second Angle|Angle**: The angle between the extrusion direction of the cylinder and its positive Z axis, measured around its X axis. The angle is positive towards its positive Y axis. Valid range: {{Value|0° &lt;&#61; value &lt; 90°}}. The default is {{Value|0°}}. <small>(v0.20)</small> 

## Scripting

See also: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/), [Part scripting](Part_scripting.md) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

A Part Cylinder can be created with the {{Incode|addObject()}} method of the document:


```python
cylinder = FreeCAD.ActiveDocument.addObject("Part::Cylinder", "myCylinder")
```

-   Where {{Incode|"myCylinder"}} is the name for the object.
-   The function returns the newly created object.

Example:


```python
import FreeCAD as App

doc = App.activeDocument()

cylinder = doc.addObject("Part::Cylinder", "myCylinder")
cylinder.Radius = 10
cylinder.Height = 50
cylinder.Placement = App.Placement(App.Vector(5, 10, 15), App.Rotation(75, 60, 30))

doc.recompute()
```





{{Part_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [Part](Part_Workbench.md) > Part Cylinder/ru
