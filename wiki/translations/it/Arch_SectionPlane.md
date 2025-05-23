---
 GuiCommand:
   Name: Arch SectionPlane
   Name/it: Piano di sezione
   MenuLocation: Arch , Piano di sezione
   Workbenches: Arch_Workbench/it
   Shortcut: **S** **P**
   SeeAlso: Draft_Shape2DView/it, TechDraw_ArchView/it
---

# Arch SectionPlane/it


</div>



## Descrizione


<div class="mw-translate-fuzzy">

Questo strumento posiziona nel documento corrente un attrezzo **Piano di sezione**, che definisce una sezione o un piano di vista. Il piano di sezione viene posizionato in funzione del corrente [Piano di lavoro](Draft_SelectPlane/it.md) e può essere spostato e riorientato muovendolo e ruotandolo, fino a quando non riproduce la vista 2D che si vuole ottenere. L\'oggetto Piano di sezione prende in considerazione solo un certo insieme di oggetti. Gli oggetti che sono selezionati quando si crea un piano di sezione sono aggiunti a queesto insieme automaticamente. Altri oggetti possono essere aggiunti o rimossi da un Piano di sezione anche in seguito con gli strumenti [Aggiungi componente](Arch_Add/it.md) o [Rimuovi componente](Arch_Remove/it.md), o facendo doppio clic sul Piano di sezione nella vista ad albero.


</div>

Il piano di sezione da solo non creerà alcuna vista del suo insieme di oggetti. Per questo, è necessario creare una [Vista Arch di TechDraw](TechDraw_ArchView/it.md) per creare una vista in una [Pagina TechDraw](TechDraw_Workbench/it.md).

<img alt="" src=images/Arch_SectionPlane_example.jpg  style="width:600px;">



## Utilizzo


<div class="mw-translate-fuzzy">

1.  Opzionalmente, impostare il [Piano di lavoro](Draft_SelectPlane/it.md) per riflettere il piano in cui si desidera posizionare il piano di sezione.
2.  Selezionare gli oggetti da includere nella sezione.
3.  Premere il pulsante **<img src="images/Arch_SectionPlane.svg" width=16px> [Piano di sezione](Arch_SectionPlane/it.md)**, oppure premere i tasti **S** e **P**.
4.  [Spostare](Draft_Move/it.md) o [ruotare](Draft_Rotate/it.md) il piano di sezione nella posizione corretta, se necessario.
5.  Selezionare il piano di sezione se non è già stato selezionato.
6.  Utilizzare una [Vista 2D di Draft](Draft_Shape2DView/it.md) o una [Vista TechDraw di Arch](TechDraw_ArchView/it.md) per creare una vista.


</div>



## Opzioni

-   L\'oggetto Piano di sezione prende in considerazione solo un certo insieme di oggetti, non tutti gli oggetti del documento. Gli oggetti possono essere aggiunti o rimossi da un oggetto Piano di sezione utilizzando gli strumenti [Aggiungi](Arch_Add/it.md) e [Rimuovi](Arch_Remove/it.md), o facendo doppio clic sul Piano di sezione nella vista ad albero, e poi selezionando gli oggetti sia nella lista che nella scena 3D, e premendo il tasto **aggiungi** o **rimuovi**.

-   Con un oggetto piano di sezione selezionato, utilizzare lo strumento [Vista 2D](Draft_Shape2DView/it.md) per creare nel documento un oggetto che rappresenta la vista di sezione

<img alt="" src=images/Arch_Section_example2.jpg  style="width:600px;">

-   Create delle [Viste Arc di TechDraw](TechDraw_ArchView/it.md).

<img alt="" src=images/Arch_Section_example3.jpg  style="width:600px;">

-   Il Piano di sezione può anche essere usato per mostrare l\'intera vista 3D tagliata da un piano infinito. Questo è solo visivo, e non influenza la geometria degli oggetti da tagliare.

<img alt="" src=images/Arch_SectionPlane_CutView.jpg  style="width:600px;">



## Proprietà

-    {{PropertyData/it|Only Solids}}: se questo è vero, gli oggetti non solidi vengono ignorati

-    {{PropertyView/it|Display Length}}: la lunghezza della sezione piana gizmo nella vista 3D. Non influisce sulla vista risultante

-    {{PropertyView/it|Display Height}}: l\'altezza della sezione piana gizmo nella vista 3D. Non influisce sulla vista risultante

-    {{PropertyView/it|Arrow Size}}: la dimensione delle frecce del piano di sezione gizmo nella vista 3D. Non influisce sulla vista risultante

-    {{PropertyView/it|Cut View}}: se questo è `True`, vero, l\'intera vista 3D viene tagliata in corrispondenza di tale piano di sezione.

-    **Clip view**: se `True`, ritaglia la vista all\'altezza e alla lunghezza della visualizzazione del piano di taglio. Questo trasforma efficacemente il piano di taglio in una fotocamera ortografica, limitando il campo visivo del piano.

<img alt="" src=images/Arch_SectionPlane_ClipView.png  style="width:600px;">



*Il piano di sezione con l'opzione clip view si comporta come una fotocamera, limitando il campo visivo.*



## Aggiustamenti

-   Aggiungere manualmente una proprietà denominata **RotateSolidRender** di tipo **App::PropertyAngle** alle proprietà **View** del piano di sezione (fare clic con il pulsante destro del mouse sulla vista delle proprietà -\> mostra tutto, destra -fare nuovamente clic -\> aggiungi proprietà) consente di ruotare il rendering quando si utilizza la modalità Solido. Ciò è utile quando una vista renderizzata ha, ad esempio, sia elementi Arch che Draft e il rendering degli elementi Arch viene ruotato rispetto agli elementi Draft.



## Script


**Vedere anche:**

[API di Arch ](Arch_API/it.md) e [Nozioni di base sugli script di FreeCAD](FreeCAD_Scripting_Basics/it.md).

Lo strumento Piano di sezione può essere utilizzato nelle [macro](Macros/it.md) e dalla console [Python](Python/it.md) tramite la seguente funzione:


```python
Section = makeSectionPlane(objectslist=None, name="Section")
```

-   Crea un oggetto `Section` da una `objectslist`, che è una lista di oggetti.

Esempio:


```python
import FreeCAD, Draft, Arch

p1 = FreeCAD.Vector(0, 0, 0)
p2 = FreeCAD.Vector(2000, 0, 0)
baseline = Draft.makeLine(p1, p2)
baseline2 = Draft.makeLine(p1, -1*p2)

Wall1 = Arch.makeWall(baseline, length=None, width=150, height=2000)
Wall2 = Arch.makeWall(baseline2, length=None, width=150, height=1800)
Structure = Arch.makeStructure(length=1000, width=1000, height=200)
FreeCAD.ActiveDocument.recompute()

BuildingPart = Arch.makeBuildingPart([Wall1, Wall2])

Floor = Arch.makeFloor([BuildingPart])
Building = Arch.makeBuilding([Floor, Structure])
Site = Arch.makeSite(Building)
FreeCAD.ActiveDocument.recompute()

Section1 = Arch.makeSectionPlane([Wall1, Wall2])
Section2 = Arch.makeSectionPlane([Structure])
Section3 = Arch.makeSectionPlane([Site])
FreeCAD.ActiveDocument.recompute()
```


<div class="mw-translate-fuzzy">





</div>



---
⏵ [documentation index](../README.md) > [BIM](Category_BIM.md) > Arch SectionPlane/it
