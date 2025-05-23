---
 GuiCommand:
   Name: Draft WireToBSpline
   Name/ro: Draft WireToBSpline
   MenuLocation: Drafting ,  Wire to BSpline
   Workbenches: Draft_Workbench/ro, Arch_Workbench/ro
---

# Draft WireToBSpline/ro


</div>



## Descriere


<div class="mw-translate-fuzzy">

Acest instrument convertește un filament [Wires](Draft_Wire.md) într-o funcție [BSplines](Draft_BSpline.md), și vice-versa.


</div>

<img alt="" src=images/Draft_Wire2BSpline_example.jpg  style="width:400px;"> 
*Converting a wire to a B-spline, and a closed B-spline to a closed wire*




<div class="mw-translate-fuzzy">

## Cum se folosește 


</div>


<div class="mw-translate-fuzzy">

1.  Selectați un [wire](Draft_Wire.md) sau o [BSpline](Draft_BSpline.md)
2.  Apăsați butonul **<img src="images/Draft_WireToBSpline.png" width=16px> [[Draft WireToBSpline]]
**


</div>

## Notes

-   The command may result in a closed, self-intersecting [Draft Wire](Draft_Wire.md) or [Draft BSpline](Draft_BSpline.md) with a face. Such an object will not display properly in the [3D view](3D_view.md). Its **Make Face** property, or its **Closed** property, must be set to `False`.

## Scripting


<div class="mw-translate-fuzzy">

## Scrip-Programare 


</div>


<div class="mw-translate-fuzzy">

Nu este disponibil, dar crearea unui obiect nou cu punctele dintr-un altul este ușor, de exemplu:


</div>


<div class="mw-translate-fuzzy">

-   Dacă obiectul activ este un filament:


</div>


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

p1 = App.Vector(1000, 1000, 0)
p2 = App.Vector(2000, 1000, 0)
p3 = App.Vector(2500, -1000, 0)
p4 = App.Vector(3500, -500, 0)

base_wire = Draft.make_wire([p1, p2, p3, p4])
base_spline = Draft.make_bspline([-p1, -1.3*p2, -1.2*p3, -2.1*p4])

points1 = base_wire.Points
spline_from_wire = Draft.make_bspline(points1)

points2 = base_spline.Points
wire_from_spline = Draft.make_wire(points2)

doc.recompute()
```



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft WireToBSpline/ro
