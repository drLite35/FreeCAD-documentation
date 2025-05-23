---
 GuiCommand:
   Name: Draft BSpline
   Name/ru: Draft BSpline
   MenuLocation: Черчение , B-сплайн
   Workbenches: Draft_Workbench/ru, Arch_Workbench/ru
   Shortcut: **B** **S**
   SeeAlso: Draft Wire
---

# Draft BSpline/ru


</div>



## Описание


<div class="mw-translate-fuzzy">

Инструмент BSpline создает кривую [B-Spline](http://en.wikipedia.org/wiki/B-spline) из нескольких точек текущей [work plane](Draft_SelectPlane.md). Он берет [linewidth and color](Draft_Linestyle.md) , предварительно установленный на вкладке «Задачи». Инструмент BSpline ведет себя точно так же, как инструмент [Draft Wire](Draft_Wire.md).


</div>

The Draft BSpline command specifies the **exact points** through which the curve will pass. The [Draft BezCurve](Draft_BezCurve.md) and the [Draft CubicBezCurve](Draft_CubicBezCurve.md) commands, on the other hand, use **control points** to define the position and curvature of the spline.

<img alt="" src=images/Draft_bspline_example.jpg  style="width:400px;"> 
*Сплайн сформированный несколькими точками*



## Применение

See also: [Draft Tray](Draft_Tray.md), [Draft Snap](Draft_Snap.md) and [Draft Constrain](Draft_Constrain.md).

1.  There are several ways to invoke the command:
    -   Press the **<img src="images/Draft_BSpline.svg" width=16px> [B-spline](Draft_BSpline.md)** button.
    -   [Draft](Draft_Workbench.md): Select the **Drafting → <img src="images/Draft_BSpline.svg" width=16px> B-spline** option from the menu.
    -   [BIM](BIM_Workbench.md): Select the **2D Drafting → <img src="images/Draft_BSpline.svg" width=16px> B-spline** option from the menu.
    -   Use the keyboard shortcut: **B** then **S**.
2.  The **B-spline** task panel opens. See [Options](#Options.md) for more information.
3.  Pick the first point in the [3D view](3D_view.md), or type coordinates and press the **<img src="images/Draft_AddPoint.svg" width=16px> Enter point** button.
4.  Pick additional points in the [3D view](3D_view.md), or type coordinates and press the **<img src="images/Draft_AddPoint.svg" width=16px> Enter point** button.
5.  Press **Esc** or the **Close** button to finish the command.



## Опции

The single character keyboard shortcuts available in the task panel can be changed. See [Draft Preferences](Draft_Preferences.md). The shortcuts mentioned here are the default shortcuts (for version 1.0).

-   To manually enter coordinates enter the X, Y and Z component, and press **Enter** after each. Or you can press the **<img src="images/Draft_AddPoint.svg" width=16px> Enter point** button when you have the desired values. It is advisable to move the pointer out of the [3D view](3D_view.md) before entering coordinates.
-   Press **R** or click the **Relative** checkbox to toggle relative mode. If relative mode is on, coordinates are relative to the last point, if available, else they are relative to the coordinate system origin.
-   Press **G** or click the **Global** checkbox to toggle global mode. If global mode is on, coordinates are relative to the global coordinate system, else they are relative to the [working plane](Draft_SelectPlane.md) coordinate system.
-   Press **F** or click the **Filled** checkbox to toggle filled mode. If filled mode is on, the created spline will have **Make Face** set to `True` and will have a filled face, provided it is closed and does not self-intersect. Note that a self-intersecting spline with a face will not display properly, for such a spline **Make Face** must be set to `False`.
-   Press **N** or click the **Continue** checkbox to toggle continue mode. If continue mode is on, the command will restart after using **<img src="images/Draft_FinishLine.svg" width=16px> Finish** or **<img src="images/Draft_CloseLine.svg" width=16px> Close**, or after creating a closed spline by snapping to the first point of the spline, allowing you to continue creating splines.
-   Press **/** or the **<img src="images/Draft_UndoLine.svg" width=16px> Undo** button to undo the last point.
-   Press **A** or the **<img src="images/Draft_FinishLine.svg" width=16px> Finish** button to finish the command and leave the spline open.
-   Press **O** or the **<img src="images/Draft_CloseLine.svg" width=16px> Close** button to finish the command and close the spline. A closed spline can also be created by snapping to the first point of the spline.
-   Press **W** or the **<img src="images/Draft_Wipe.svg" width=16px> Wipe** button to delete the curve segments already placed, but keep working from the last point.
-   Press **U** or the **<img src="images/Draft_SelectPlane.svg" width=16px> [Set WP](Draft_SelectPlane.md)** button to adjust the current working plane in the orientation defined by the last and the previous point.
-   Press **S** to switch [Draft snapping](Draft_Snap.md) on or off.
-   Press **Esc** or the **Close** button to finish the command.



## Примечания

-   A Draft BSpline can be edited with the [Draft Edit](Draft_Edit.md) command.
-   A Draft BSpline can be converted to a [Draft Wire](Draft_Wire.md) with the [Draft WireToBSpline](Draft_WireToBSpline.md) command.



## Свойства

See also: [Property editor](Property_editor.md).

A Draft BSpline object is derived from a [Part Part2DObject](Part_Part2DObject.md) and inherits all its properties. It also has the following additional properties:



### Данные


{{TitleProperty|Draft}}

-    **Area|Area**: (read-only) specifies the area of the face of the spline. The value will be {{value|0.0}} if **Make Face** if `False` or the face cannot be created.

-    **Closed|Bool**: specifies if the spline is closed or not. If the spline is initially open this value is `False`, setting it to `True` will draw a curve segment to close the spline. If the spline is initially closed this value is `True`, setting it to `False` will remove the last curve segment and make the spline open.

-    **Make Face|Bool**: specifies if the spline makes a face or not. If it is `True` a face is created, otherwise only the perimeter is considered part of the object. This property only works if **Closed** is `True` and if the spline does not self-intersect.

-    **Parameterization|Float**: affects the shape of the spline.

-    **Points|VectorList**: specifies the points of the spline in its local coordinate system.



### Вид


{{TitleProperty|Draft}}

-    **Arrow Size|Length**: specifies the size of the symbol displayed at the end of the spline.

-    **Arrow Type|Enumeration**: specifies the type of symbol displayed at the end of the spline, which can be {{value|Dot}}, {{value|Circle}}, {{value|Arrow}}, {{value|Tick}} or {{value|Tick-2}}.

-    **End Arrow|Bool**: specifies whether to show a symbol at the end of the spline, so it can be used as an annotation line.

-    **Pattern|Enumeration**: specifies the [Draft Pattern](Draft_Pattern.md) with which to fill the face of the closed spline. This property only works if **Make Face** is `True` and if **Display Mode** is {{value|Flat Lines}}.

-    **Pattern Size|Float**: specifies the size of the [Draft Pattern](Draft_Pattern.md).



## Программирование

See also: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

To create a Draft BSpline use the `make_bspline` method (<small>(v0.19)</small> ) of the Draft module. This method replaces the deprecated `makeBSpline` method.


```python
bspline = make_bspline(pointslist, closed=False, placement=None, face=None, support=None)
bspline = make_bspline(Part.Wire, closed=False, placement=None, face=None, support=None)
```

-   Creates a `bspline` object from the given list of points, `pointslist`.
    -   Each point in the list is defined by its `FreeCAD.Vector`, with units in millimeters.
    -   Alternatively, the input can be a `Part.Wire`, from which points are extracted.
-   If `closed` is `True`, or if the first and last points are identical, the spline is closed.
-   If `placement` is `None` the spline is created at the origin.
-   If `face` is `True`, and the spline is closed, the spline will make a face, that is, it will appear filled.

Пример:


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

p1 = App.Vector(0, 0, 0)
p2 = App.Vector(1000, 1000, 0)
p3 = App.Vector(2000, 0, 0)

spline1 = Draft.make_bspline([p1, p2, p3], closed=False)
spline2 = Draft.make_bspline([p1, 2*p3, 1.3*p2], closed=False)
spline3 = Draft.make_bspline([1.3*p3, p1, -1.7*p2], closed=False)

doc.recompute()
```


<div class="mw-translate-fuzzy">





</div>



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft BSpline/ru
