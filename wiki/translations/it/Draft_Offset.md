---
 GuiCommand:
   Name: Draft Offset
   Name/it: Draft Offset
   MenuLocation: Modifiche , Offset<br>Modifica , Offset
   Workbenches: Draft_Workbench/it, BIM_Workbench/it
   Shortcut: **O** **S**
   SeeAlso: Part_Offset2D/it
---

# Draft Offset/it



## Descrizione

Il comando <img alt="" src=images/Draft_Offset.svg  style="width:24px;"> **Offset** sposta ogni segmento di un oggetto selezionato ad una determinata distanza, o crea una copia traslata dell\'oggetto selezionato.

<img alt="" src=images/Draft_Offset_example.jpg  style="width:400px;"> 
*Offset di una Polilinea*



## Utilizzo

Vedere anche: [Aggancio](Draft_Snap/it.md) e [Vincolare](Draft_Constrain/it.md).

1.  Facoltativamente selezionare un oggetto. L\'oggetto deve trovarsi sul [piano di lavoro](Draft_SelectPlane/it.md).
2.  Esistono diversi modi per invocare il comando:
    -   Premere il pulsante **<img src="images/Draft_Offset.svg" width=16px> [Offset](Draft_Offset/it.md)**.
    -   [Draft](Draft_Workbench/it.md): Selezionare l\'opzione **Modifiche → <img src="images/Draft_Offset.svg" width=16px> Offset** dal menu.
    -   [BIM](BIM_Workbench/it.md): Selezionare l\'opzione **Modifica → <img src="images/Draft_Offset.svg" width=16px> Offset** dal menu.
    -   Usare la scorciatoia da tastiera: **O** poi **S**.
3.  Se non si ha ancora selezionato un oggetto: selezionare un oggetto nella [Vista 3D](3D_view/it.md).
4.  Si apre il pannello attività **Offset**. Vedere [Opzioni](#Opzioni.md) per maggiori informazioni.
5.  Per definire la distanza di offset, eseguire una delle seguenti operazioni:
    -   Scegliere un punto nella [Vista 3D](3D_view/it.md).
    -   Inserire un valore numerico:
        1.  Assicurarsi che il puntatore si trovi sul lato corretto dell\'oggetto nella [Vista 3D](3D_view/it.md).
        2.  Non spostare il puntatore fuori dalla [Vista 3D](3D_view/it.md).
        3.  Inserire una **Distanza**.
        4.  Premere **Enter** per terminare il comando.



## Opzioni

È possibile modificare le scorciatoie da tastiera a carattere singolo disponibili nel pannello delle attività. Vedere [Preferenze di Draft](Draft_Preferences/it.md). Le scorciatoie qui menzionate sono le scorciatoie predefinite (per la versione 1.0).

-   Se la casella di controllo **Offset in OCC** è selezionata, viene utilizzato uno stile di offset speciale: le [Polilinee](Draft_Wire/it.md) aperte sono sfalsate su entrambi i lati e i nuovi bordi sono collegati con angoli arrotondati. Questo funziona solo per oggetti planari con almeno due spigoli. Si noti che con questo stile viene creato un nuovo oggetto non parametrico e, se la modalità di copia è disattivata, l\'oggetto originale viene eliminato.
-   Premere **C** o fare clic sulla casella di controllo **Copia** per attivare o disattivare la modalità di copia. Se la modalità copia è attiva, il comando creerà una copia sfalsata invece di sfalsare l\'oggetto originale.
-   Tenendo premuto **Alt** prima di selezionare i punti nella [Vista 3D](3D_view/it.md) si attiverà anche la modalità di copia. Mentre si tiene premuto **Alt** è possibile selezionare più punti di offset. Rilasciare **Alt** per terminare il comando e vedere le copie create.
-   Tenere premuto **Maiusc** per mantenere la distanza di offset collegata al segmento corrente.
-   Premere **S** per attivare o disattivare [Aggancia](Draft_Snap/it.md).
-   Premere **Esc** o il pulsante **Chiudi** per interrompere il comando.



## Note

-   Per creare una versione offset di una [BSpline](Draft_BSpline/it.md) i suoi punti vengono sfalsati singolarmente e dai nuovi punti viene calcolata una nuova spline. Questa nuova spline non è parallela alla spline originale. Per un esatto offset parallelo di una [BSpline](Draft_BSpline/it.md) si dovrebbe utilizzare il comando [Part Offset2D](Part_Offset2D/it.md).
-   Il comando Draft Offset non può gestire [BezCurves](Draft_BezCurve/it.md). Utilizzare invece il comando [Part Offset2D](Part_Offset2D/it.md).



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) e [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).

Per sfalsare gli oggetti usare il metodo `offset` del modulo Draft. Il metodo può gestire solo [Polilinee](Draft_Wire/it.md), [Cerchi](Draft_Circle/it.md), [Rettangoli](Draft_Rectangle/it.md), [ Poligoni](Draft_Polygon/it.md) e [BSplines](Draft_BSpline/it.md).


```python
offset_obj = offset(obj, delta, copy=False, bind=False, sym=False, occ=False)
```

-    `obj`è l\'oggetto da sfalsare.

-    `delta`contiene le informazioni sull\'offset:

    -   Per [Polilinee](Draft_Wire/it.md), [Rettangoli](Draft_Rectangle/it.md) e [Poligoni](Draft_Polygon/it.md) è un vettore di offset che deve essere perpendicolare al primo segmento dell\'oggetto.
    -   Per [Cerchi](Draft_Circle/it.md) è il nuovo raggio.
    -   Per [BSplines](Draft_BSpline/it.md) è un elenco di nuovi punti.

-   Se `copy` è `True` l\'oggetto originale viene mantenuto e viene creato un nuovo oggetto.

-   Se `bind` è `True` viene creata una faccia collegando la forma dell\'oggetto originale e la forma del suo offset. Funziona solo per [Polilinee](Draft_Wire/it.md).

-   Se `sym` è `True`, e anche `bind` è `True`, l\'offset viene eseguito su entrambi i lati dell\'oggetto originale, la larghezza totale è la lunghezza del vettore dato. Funziona solo per [Polilinee](Draft_Wire/it.md).

-   Se `occ` è `True` viene utilizzato l\'offset in stile OCC. Vedere [Opzioni](#Opzioni.md). Se `occ` è `True` gli argomenti `bind` e `sym` vengono ignorati.

Esempio:


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

p1 = App.Vector(0, 0, 0)
p2 = App.Vector(1500, 2000, 0)
p3 = App.Vector(4000, 0, 0)

wire = Draft.make_wire([p1, p2, p3])
doc.recompute()

vector = App.Vector(-200, 150, 0)
offset1 = Draft.offset(wire, vector, copy=True, bind=True, sym=True)
offset2 = Draft.offset(wire, 3*vector, copy=True)
offset3 = Draft.offset(wire, 6*vector, copy=True)
offset4 = Draft.offset(wire, 9*vector, copy=True)
offset5 = Draft.offset(wire, 1.5*vector, copy=True, occ=True)

doc.recompute()
```



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft Offset/it
