---
 GuiCommand:
   Name: Part Torus
   Name/ru: Тор
   MenuLocation: Деталь , Примитивы , Тор
   Workbenches: Part_Workbench/ru
   SeeAlso: Part_Primitives/ru
---

# Part Torus/ru



## Описание


<div class="mw-translate-fuzzy">

Создаёт простой параметрический тор с следующими параметрами: положение (position), угол1 (angle1), угол2 (angle2), угол3 (angle3), радиус1 (radius1) и радиус2 (radius2).


</div>

A Part Torus can be turned into a segment of a torus by changing its **Angle3** property. By changing its **Angle1** and/or **Angle2** properties the swept profile can become a segment of a circle.

<img alt="" src=images/Part_Torus_Example.png  style="width:400px;">




<div class="mw-translate-fuzzy">

## Применение


</div>


<div class="mw-translate-fuzzy">

1.  Переключитесь на <img alt="" src=images/Workbench_Part.svg  style="width:16px;"> [верстак Part](Part_Workbench/ru.md)
2.  Существует несколько способов вызова команды:
    -   Нажмите на иконку **<img src="images/Part_Torus.svg" width=16px> тора** на панели инструментов.
    -   Выберите из меню **Деталь → Примитивы → <img src="images/Part_Torus.svg" width=16px> Тор**.


</div>

## Example

![Part Torus from the scripting example](images/Part_Torus_Scripting_Example.png )

A Part Torus object created with the [scripting example](#Scripting.md) below is shown here.

## Notes

-   A Part Torus can also be created with the <img alt="" src=images/Part_Primitives.svg  style="width:16px;"> [Part Primitives](Part_Primitives.md) command. With that command you can specify the dimensions and placement at creation time.




<div class="mw-translate-fuzzy">

![](images/TorusExampleRadius1.jpg ) Параметр Радиус1 (Radius1) со значением 20мм.


</div>

See also: [Property editor](Property_editor.md).

A Part Torus object is derived from a [Part Feature](Part_Feature.md) object and inherits all its properties. It also has the following additional properties:

### Data


{{TitleProperty|Attachment}}

The object has the same attachment properties as a [Part Part2DObject](Part_Part2DObject#Data.md).


{{TitleProperty|Torus}}


<div class="mw-translate-fuzzy">

-    {{Parameter|Радиус1(Radius1):}}Радиус окружности, вокруг которой вращается наш диск

-    {{Parameter|Радиус2 (Radius2):}}Радиус диска, определяющий форму тора

-    {{Parameter|Угол1 (Angle1):}}1-й угол для обрезки / построения диска тора

-    {{Parameter|Угол2 (Angle2):}}2-й угол для обрезки / построения диска тора

-    {{Parameter|Угол3 (Angle3):}}3-й угол для определения длины окружности тора.


</div>

## Scripting

See also: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/), [Part scripting](Part_scripting.md) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

A Part Torus can be created with the {{Incode|addObject()}} method of the document:


```python
torus = FreeCAD.ActiveDocument.addObject("Part::Torus", "myTorus")
```

-   Where {{Incode|"myTorus"}} is the name for the object.
-   The function returns the newly created object.

Example:


```python
import FreeCAD as App

doc = App.activeDocument()

torus = doc.addObject("Part::Torus", "myTorus")
torus.Radius1 = 20
torus.Radius2 = 10
torus.Angle1 = -90
torus.Angle2 = 45
torus.Angle3 = 270
torus.Placement = App.Placement(App.Vector(1, 2, 3), App.Rotation(30, 45, 10))

doc.recompute()
```





{{Part_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [Part](Part_Workbench.md) > Part Torus/ru
