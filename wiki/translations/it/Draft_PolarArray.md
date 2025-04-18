---
 GuiCommand:
   Name: Draft PolarArray
   Name/it: Draft Serie polare
   MenuLocation: Modifiche , Strumenti serie , Serie polare<br>Modifiche , Serie polare
   Workbenches: Draft_Workbench/it, BIM_Workbench/it
   Version: 0.19
   SeeAlso: Draft_OrthoArray/it, Draft_CircularArray/it, Draft_PathArray/it, Draft_PathLinkArray/it, Draft_PointArray/it, Draft_PointLinkArray/it
---

# Draft PolarArray/it



## Descrizione

Il comando <img alt="" src=images/Draft_PolarArray.svg  style="width:24px;"> **Serie polare** crea una serie (array) da un oggetto selezionato posizionando copie lungo una circonferenza. Il comando può facoltativamente creare una Serie di [Link](App_Link.md), che è più efficiente di una normale Serie.

Il comando può essere utilizzato su oggetti 2D creati con [Draft](Draft_Workbench/it.md) o [Sketcher](Sketcher_Workbench/it.md), ma anche su molti oggetti 3D come quelli creati con gli ambienti [Part](Part_Workbench/it.md), [PartDesign](PartDesign_Workbench/it.md) o [BIM](BIM_Workbench/it.md).

<img alt="" src=images/Draft_PolarArray_example.png  style="width:400px;"> 
*Serie polare*



## Utilizzo

Vedere anche: [Aggancio](Draft_Snap/it.md).

1.  Facoltativamente selezionare un oggetto.
2.  Esistono diversi modi per invocare il comando:
    -   Premere il pulsante **<img src="images/Draft_PolarArray.svg" width=16px> [Serie polare](Draft_PolarArray/it.md)**.
    -   [Draft](Draft_Workbench/it.md): Selezionare l\'opzione **Modifiche → Strumenti serie → <img src="images/Draft_PolarArray.svg" width=16px> Serie polare** dal menu.
    -   [BIM](BIM_Workbench/it.md): Selezionare l\'opzione **Modifica → <img src="images/Draft_PolarArray.svg" width=16px> Serie polare** dal menu.
3.  Si apre il pannello attività **Serie polare**. Vedere [Opzioni](#Opzioni.md) per maggiori informazioni.
4.  Se non si ha ancora selezionato un oggetto: selezionare un oggetto.
5.  Immettere i parametri richiesti nel pannello delle attività.
6.  Per completare il comando, eseguire una delle seguenti operazioni:
    -   Scegliere un punto nella [Vista 3D](3D_view/it.md) per il **Centro di rotazione**.
    -   Premere **Enter**.
    -   Premere il pulsante **OK**.



## Opzioni

-   Immettere **Angolo polare** per specificare l\'angolo totale della serie. L\'angolo è positivo in senso antiorario.
-   Inserire il **Numero di elementi**. Deve essere almeno {{Value|2}}. Il massimo che può essere inserito nel pannello delle attività è {{Value|99}}, ma sono possibili valori più alti modificando la proprietà **Number Polar** della serie.
-   Scegliere un punto nella [Vista 3D](3D_view/it.md), notare che anche questo terminerà il comando, oppure digitare le coordinate per **Centro di rotazione**. L\'asse di rotazione della serie passerà per questo punto. Si consiglia di spostare il puntatore fuori dalla [Vista 3D](3D_view/it.md) prima di inserire le coordinate.
-   Premere il pulsante **Resetta il punto** per reimpostare il **Centro di rotazione** all\'origine.
-   Se la casella di controllo **Fuse** è selezionata, gli elementi sovrapposti nella serie vengono fusi. Questo non funziona per le serie di link.
-   Se la casella **Serie di link** è spuntata, viene creato una Serie di link invece di una normale serie. Una Serie di Link è più efficiente perché i suoi elementi sono oggetti [App Link](App_Link/it.md).
-   Premiere **Esc** o il pulsante **Annulla** per interrompere il comando.



## Note

-   L\'asse di rotazione predefinito per la serie è l\'asse Z positivo. Questo può essere cambiato modificando la sua proprietà **Axis**.
-   Una Serie polare può essere trasformata in una [Serie ortogonale](Draft_OrthoArray/it.md) o in una [Serie circolare](Draft_CircularArray/it.md) modificandone la proprietà **Array Type**.
-   Una Serie di link non può essere trasformata in una serie normale o viceversa. Il tipo di serie deve essere deciso al momento della creazione.



## Proprietà

Vedere [Serie ortogonale](Draft_OrthoArray/it#Propertà.md).



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) and [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).



### Serie parametrica 

Per creare una serie polare parametrica usare il metodo `make_array` ({{Version/it|0.19}}) del modulo Draft. Questo metodo sostituisce il metodo deprecato `makeArray`. Il metodo `make_array` può creare [Serie ortogonali](Draft_OrthoArray/it.md), Serie polari e [Serie circolari](Draft_CircularArray/it.md). Per ogni tipo di serie sono disponibili uno o più wrapper.

Il metodo principale:


```python
array = make_array(base_object, arg1, arg2, arg3, arg4=None, arg5=None, arg6=None, use_link=True)
```

Il wrapper per le Serie polari è:


```python
array = make_polar_array(base_object,
                         number=5, angle=360, center=App.Vector(0, 0, 0),
                         use_link=True)
```

-    `base_object`è l\'oggetto da disporre in serie. Può anche essere la `Label` (string) di un oggetto nel documento corrente.

-    `number`è il numero di elementi nel modello, incluso l\'oggetto originale.

-    `angle`è l\'angolo dell\'arco polare in gradi.

-    `center`è il vettore che definisce il centro del motivo.

-   Se `use_link` è `True` gli elementi creati sono [App Links](App_Link/it.md) invece di normali copie.

-    `array`viene restituito con l\'oggetto serie creato.

Esempio:


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

tri = Draft.make_polygon(3, 600)
center = App.Vector(-1600, 0, 0)

array = Draft.make_polar_array(tri, 8, 270, center)
doc.recompute()
```



### Serie non parametrica 

Per creare una serie polare non parametrica usare il metodo `array` del modulo Draft. Questo metodo restituisce `None`.


```python
array(objectslist, center, angle, number)
```

Esempio:


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

tri = Draft.make_polygon(3, 600)
center = App.Vector(-1600, 0, 0)

Draft.array(tri, center, 270, 8)
doc.recompute()
```



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft PolarArray/it
