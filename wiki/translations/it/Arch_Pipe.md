---
 GuiCommand:
   Name: Arch Pipe
   Name/it: Tubo
   MenuLocation: Arch , Tubazioni , Tubo
   Workbenches: Arch_Workbench/it
   Shortcut: **P** **I**
   Version/it: 0.17
   SeeAlso: Arch_PipeConnector/it, Arch_Equipment/it
---

# Arch Pipe/it


</div>



## Descrizione


<div class="mw-translate-fuzzy">

Questo strumento permette di creare delle tubazioni partendo da zero, o dagli oggetti selezionati. Gli oggetti selezionati devono essere Part-based (Draft, Schizzo, ecc ..) e contenere una e una sola polilinea (wire) aperta,


</div>



## Utilizzo


<div class="mw-translate-fuzzy">

1.  Facoltativamente, selezionare una forma [Part](Part_Workbench/it.md) lineare come una [Linea](Draft_Line/it.md), una [Wire](Draft_Wire/it.md) o uno [Schizzo](Sketcher_NewSketch/it.md) aperto.
2.  Richiamare questo comando utilizzando uno di questi metodi:
    -   Premere il pulsante **<img src="images/Arch_Pipe.svg" width=16px> [Tubo](Arch_Pipe/it.md)** nella barra degli strumenti.
    -   Premere i tasti **P** e poi **I** da tastiera.
    -   Usare la voce **Arch → Strumenti tubazioni → Tubo** del menu principale.


</div>



## Opzioni


<div class="mw-translate-fuzzy">

-   Gli elementi Tubo condividono le proprietà e i comportamenti comuni di tutti i [Componenti Arch](Arch_Component/it.md)


</div>



## Proprietà

### Data


{{TitleProperty|Component}}

-    **Base|Link**: The base wire of this pipe, if any.

For the other properties in the group see [Arch Component](Arch_Component#Properties.md).


{{TitleProperty|Pipe}}


<div class="mw-translate-fuzzy">

-    {{PropertyData/it|Length}}: Imposta la lunghezza del tubo, quando non si basa su una polilinea

-    {{PropertyData/it|Diameter}}: Il diametro del tubo, quando non si basa su un profilo

-    {{PropertyData/it|Base}}: L\'eventuale polilinea su cui si basa il tubo

-    {{PropertyData/it|Profile}}: Il profilo di base del tubo. Se non è dato, il tubo è di forma cilindrica.


</div>



## Flusso di lavoro tipico 


<div class="mw-translate-fuzzy">

-   Iniziare collocando degli apparecchi sanitari o idraulici (il wc della figura sottostante è un file step importato). Commutare questi oggetti in Arch Equipment selezionandoli e premendo il tasto [Arredo](Arch_Equipment/it.md).


</div>

![](images/Arch_pipe_example_01.jpg )

-   Gli oggetti Arch Equipment ora hanno una nuova proprietà **SnapPoints**, che è una lista di vettori 3D. Questo consente di aggiungere dei punti di aggancio personalizzati, a cui è possibile ancorarsi quando il nuovo tasto snap [Speciale](Draft_Snap_Special/it.md) è attivo. Attualmente però la proprietà è disponibile solo per Python. Nel caso sopra è stato aggiunto un nuovo punto di snap all\'uscita dell\'apparecchio WC. I vettori all\'interno di SnapPoints appaiono sul modello come puntini bianchi:

FreeCAD.ActiveDocument.Equipment.SnapPoints=[FreeCAD.Vector(0,0,100)]

![](images/Arch_pipe_example_02.jpg )

-   Con il nuovo snap [\"Speciale\"](Draft_Snap_Special/it.md) di Draft è possibile agganciarsi a questi punti personalizzati:

![](images/Arch_pipe_example_03.jpg )

-   Ora è possibile disegnare le tubazioni con Linee e Polilineee di Draft, o con Schizzi. Comunque, il modo migliore è quello di usare solo Linee di Draft:

![](images/Arch_pipe_example_04.jpg )

-   Vi è ora un nuovo strumento [Pendenza](Draft_Slope/it.md) che permette di modificare la pendenza delle linee Draft, per esempio del 5% (0.05). Così si può rapidamente dare alle linee delle tubazioni di scarico una pendenza corretta. Questo strumento modifica solo le coordinate z, quindi basta agganciarle l\'un l\'altra, la proiezione dall\'alto resta invariata.

![](images/Arch_pipe_example_05.jpg )


<div class="mw-translate-fuzzy">

-   Ora basta selezionare tutte le linee, e premere il pulsante [Tubo](Arch_Pipe/it.md). Arch Tubo funziona con qualsiasi oggetto Part-based che contenga una e una sola polilinea aperta.


</div>

![](images/Arch_pipe_example_06.jpg )


<div class="mw-translate-fuzzy">

-   Ora si possono creare le connessioni selezionando 2 o 3 tubi coincidenti, e premendo il tasto [Raccordo](Arch_PipeConnector/it.md). Se sono selezionati 3 tubi, due di essi devono essere allineati per creare un elemento tee o braga:


</div>

![](images/Arch_pipe_example_07.jpg )

-   Cambiando il raggio dei raccordi non si non cambia la lunghezza della linea di base sottostante, ma solo la lunghezza del tubo risultante (dato che cambia la sua proprietà OffsetStart o OffsetEnd). Così si può disegnare il percorso solo con linee rette, senza doversi preoccupare delle curve e dei raggi.

È anche possibile creare Tubi Arch senza una linea di base, in questo caso utilizzare la proprietà \"Length\" per definire la lunghezza.



## Script


**Vedere anche:**

[API di Arch](Arch_API/it.md) e [Nozioni di base sugli script di FreeCAD](FreeCAD_Scripting_Basics/it.md).

Lo strumento Tubo può essere utilizzato nelle [macro](Macros/it.md) e dalla console [Python](Python/it.md) utilizzando la seguente funzione:


```python
pipe = makePipe(baseobj=None, diameter=0, length=0, placement=None, name="Pipe")
```

-   Creates a `pipe` object from the given `baseobj` and `diameter`.
    -   
        `baseobj`
        
        is a [Draft Line](Draft_Line.md) or [Draft Wire](Draft_Wire.md).

    -   If `baseobj` is omitted, a straight pipe can be created with just the `diameter` and the `length` in the Z direction.
-   If a `placement` is given, it is used.


```python
import Draft, Arch

p1 = FreeCAD.Vector(1000, 0, 0)
p2 = FreeCAD.Vector(2500, 200, 0)
p3 = FreeCAD.Vector(3100, 1000, 0)
p4 = FreeCAD.Vector(3500, 500, 0)
line = Draft.make_wire([p1, p2, p3, p4])

pipe = Arch.makePipe(line, 200)
FreeCAD.ActiveDocument.recompute()

pipe2 = Arch.makePipe(diameter=120, length=3000)
FreeCAD.ActiveDocument.recompute()
```


<div class="mw-translate-fuzzy">





</div>



---
⏵ [documentation index](../README.md) > [BIM](Category_BIM.md) > Arch Pipe/it
