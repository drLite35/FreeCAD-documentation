---
 GuiCommand:
   Name: Sketcher ConstrainRadius
   Workbenches: Sketcher Workbench
   MenuLocation: Sketch , Sketcher constraints , Constrain radius
   SeeAlso: Sketcher ConstrainDistance, Sketcher ConstrainDistanceX, Sketcher ConstrainDistanceY
---

# Sketcher ConstrainRadius/ro


</div>




<div class="mw-translate-fuzzy">

## Descriere

Această constrângere obligă valoarea razei unui cerc sau a unui arc de cerc să aibă o valoare specifică. Dacă este selectat mai mult de un cerc sau un arc de cerc înainte de lansarea comenzii, un dialog contextual vă va întreba dacă toate elementele selectate ar trebui să partajeze aceeași rază. În cazul unui răspuns afirmativ, se va adăuga o constrângere de rază și o [equal length](Sketcher_ConstrainEqual.md) va fi adăugată la toate elementele. În negativ, vor fi create constrângeri separate de rază pentru fiecare cerc / arc, dar cu valori egale care vor fi editate separat după crearea.


</div>

The <img alt="" src=images/Sketcher_ConstrainRadius.svg  style="width:24px;"> [Sketcher ConstrainRadius](Sketcher_ConstrainRadius.md) tool fixes the radius of circles, arcs and [B-spline weight circles](Sketcher_CreateBSpline#Notes.md).

![](images/Sketcher_ConstrainRadius_example.png )




<div class="mw-translate-fuzzy">

## Cum se folosește 


</div>

See also: [Drawing aids](Sketcher_Workbench#Drawing_aids.md).

### [Continue mode](Sketcher_Workbench#Continue_modes.md) 


<div class="mw-translate-fuzzy">

1.  Selectați una sau mai multe cercuri sau arce e cerc.
2.  Apăsați butonul **[<img src=images/Sketcher_ConstrainRadius.png style="width:24px"> '''Constrain radius'''** .
3.  Un dialog contextual se deschide pentru a edita sau a confirma vloarea. Apăsați **OK** pentru a valida.În cazul în care au fost selectate mai multe cercuri/arce, toate constrângerile vor adopta această valoare. Editați valorile lor separat făcând dublu clic pe cota/eticheta de dimensiuni din vizualizarea 3D; sau în lista Constrângeri, faceți dublu clic pe constrângere sau faceți clic dreapta și selectați**Change value**.
4.  Opțional, eticheta/cota și linia de cotă pot fi mutate și rotite în vizualizarea 3D făcând clic pe valoare și tragând în timp ce mențineți apăsat butonul stânga al mouse-ului.


</div>

### Run-once mode 

See [Sketcher ConstrainRadiam](Sketcher_ConstrainRadiam#Run-once_mode.md).

## Scripting


```pythonSketch.addConstraint(Sketcher.Constraint('Radius', ArcOrCircle, App.Units.Quantity('123.0 mm')))```

The [Sketcher scripting](Sketcher_scripting.md) page explains the values which can be used for `ArcOrCircle`, and contains further examples on how to create constraints from Python scripts.



---
⏵ [documentation index](../README.md) > [Sketcher](Sketcher_Workbench.md) > Sketcher ConstrainRadius/ro
