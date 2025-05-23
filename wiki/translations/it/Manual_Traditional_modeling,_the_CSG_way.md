# Manual:Traditional modeling, the CSG way/it
{{Manual:TOC}}


<div class="mw-translate-fuzzy">

CSG sta per [Geometria solida costruttiva](https://en.wikipedia.org/wiki/Constructive_solid_geometry) e rappresenta il modo più semplice per lavorare con la geometria solida 3D, con cui si creano oggetti complessi con l\'aggiunta e la rimozione di pezzi a o da solidi usando le operazioni booleane, come unione, sottrazione o intersezione.


</div>


<div class="mw-translate-fuzzy">

Come si è visto in precedenza in questo manuale, FreeCAD è in grado di gestire diversi tipi di geometrie, ma il tipo preferito e più utile per gli oggetti 3D che si vogliono progettare con FreeCAD, cioè gli oggetti del mondo reale, è, senza dubbio , quella solida, la geometria [BREP](https://en.wikipedia.org/wiki/Boundary_representation) che viene gestita principalmente dall\'ambiente [Part](Part_Workbench/it.md). A differenza dei [poligoni mesh](https://en.wikipedia.org/wiki/Polygon_mesh), che sono fatti solo di punti e triangoli, gli oggetti BREP hanno le loro facce definite da curve matematiche che permettono una precisione assoluta, a prescindere dalla scala.


</div>


<div class="mw-translate-fuzzy">

![](images/Mesh_vs_brep.jpg )


</div>


<div class="mw-translate-fuzzy">

La differenza tra i due può essere paragonata alla differenza tra le immagini bitmap e quelle vettoriali. Come nelle immagini bitmap, le mesh poligonali hanno le loro superfici curve frazionate in una serie di punti. Se si guardano da molto vicino, o si stampano molto grandi, non si vede una curva, ma una superficie sfaccettata. Invece nelle immagini vettoriali, come con i dati BREP, la posizione di un punto di una curva non viene memorizzata nella geometria, ma calcolata al volo, con assoluta precisione.


</div>


<div class="mw-translate-fuzzy">

In FreeCAD, tutta la geometria basata su BREP è gestita da [OpenCasCade](https://en.wikipedia.org/wiki/Open_Cascade_Technology), che è un\'altra parte di software open-source. L\'interfaccia principale tra FreeCAD e il kernel OpenCasCade è l\'ambiente Parte. La maggior parte degli altri ambienti costruiscono la loro funzionalità sull\'ambiente Parte.


</div>

While other workbenches in FreeCAD, such as the Part Design and Surface Workbenches, offer more advanced tools for building and manipulating geometry, they rely on the underlying Part Workbench. Understanding how Part objects work internally and being adept with the basic Part tools is beneficial. Often, these simpler tools can resolve issues that more complex tools may not handle effectively.

![](images/Mesh_vs_brep.jpg )

The difference between the two can be compared to the difference between bitmap and vector images. As with bitmap images, polygon meshes have their curved surfaces divided into a series of points. If you look at it closely or print it very large, you will see not a curved but a faceted surface. In both vector images and BREP data, the position of any point on a curve is not stored in the geometry but calculated on the fly, with exact precision.


<div class="mw-translate-fuzzy">

Per illustrare il funzionamento dell\'ambiente Parte, modelliamo questo tavolo, utilizzando solo operazioni CSG (tranne le viti, per cui useremo uno degli addons, e le dimensioni che vedremo nel prossimo capitolo):


</div>

![](images/Exercise_table_complete.jpg )


<div class="mw-translate-fuzzy">

Creare un nuovo documento (**Ctrl + N** o il menu File → Nuovo documento)per cominciare a modellare il tavolo. Inizialmente nella scheda Modello del pannello Vista combinata il documento viene chiamato \"senza nome\", ma se si salva il documento (**Ctrl + Maius + S** o dal menu File → Salva come) come un nuovo documento di FreeCAD chiamato \"table.FCStd\" il documento viene rinominato \"table\", che identifica più chiaramente il progetto.


</div>

Ora si può passare all\'ambiente Part e iniziare a creare la prima gamba del tavolo.


<div class="mw-translate-fuzzy">

-   Premere il pulsante <img alt="" src=images/Part_Box.svg  style="width:16px;"> 
**Cube**
-   Selezionare il Cube, quindi impostare le seguenti proprietà (nella tabella **Dati**):
    -   Lunghezza: 80 mm (o 8 cm, o 0.8 m, FreeCAD opera in qualsiasi unità)
    -   Larghezza: 80 mm
    -   Altezza: 75 cm
-   Duplicare il Cube premendo **Ctrl+C** poi **Ctrl+V** (o menu Modifica → Copia e Incolla) (Non si vede nessun cambiamento, poiché il secondo oggetto è sovrapposto al primo).
-   Selezionare il nuovo oggetto denominato Cube001 che è stato creato (Fare clic su Cube001 nella scheda Modello a sinistra)
-   Cambiare la sua posizione modificando la sua proprietà Placement:
    -   Posizione x: 8 mm
    -   Posizione y: 8 mm


</div>

Si dovrebbe ottenere due parallelepipedi, uno scostato dall\'altro di 8 millimetri:

![](images/Exercise_table_01.jpg )

-   Ora possiamo sottrarre uno dall\'altro: Selezionare il **primo**, vale a dire quello che **rimane**, poi,con il tasto CTRL premuto, selezionare il **secondo**, quello da **sottrarre** (l\'ordine è importante) e premere il pulsante <img alt="" src=images/Part_Cut.svg  style="width:16px;"> **Taglio**:

![](images/Exercise_table_02.jpg )

Osservare che l\'oggetto appena creato, chiamato \"Cut\", contiene ancora i due cubi usati come operandi. In realtà, i due cubi sono ancora lì nel documento, sono semplicemente stati nascosti e raggruppati sotto l\'oggetto Cut nella vista ad albero. È ancora possibile selezionarli espandendo la freccia accanto all\'oggetto Cut, e, se lo si desidera, renderli nuovamente visibili cliccandoli con il tasto destro o modificando le loro proprietà.


<div class="mw-translate-fuzzy">

Puoi usare lo strumento Taglia e altri strumenti booleani anche tramite \"Combo view\" con il comando <img alt="" src=images/Part_Boolean.svg  style="width:16px;"> [Operazioni booleane](Part_Boolean/it.md). Questo fornisce un modo più esplicito ma più laborioso.


</div>


<div class="mw-translate-fuzzy">

-   Ora creare le altre tre gambe duplicando il cubo di base 6 altre volte. Dato che è ancora copiato, si può semplicemente incollarlo (CTRL + V) 6 volte. Cambiare la loro posizione con la seguente:
    -   Cube002: x: 0, y: 80 cm
    -   Cube003: x: 8 mm, y: 79.2 cm
    -   Cube004: x: 120 cm, y: 0
    -   Cube005: x: 119.2 cm, y: 8 mm
    -   Cube006: x: 120 cm, y: 80 cm
    -   Cube007: x: 119.2 cm, y: 79.2 cm


</div>


<div class="mw-translate-fuzzy">

-   Ora fare gli altri tre Tagli, selezionando prima il cubo \"ospite\", quindi il cubo da tagliare. Ora abbiamo quattro oggetti Cut:


</div>

![](images/Exercise_table_03.jpg )


<div class="mw-translate-fuzzy">

Si potrebbe avere pensato che, invece di duplicare il cubo di base sei volte, si poteva duplicare tre volte la gamba completa. Questo è totalmente vero, come sempre in FreeCAD, ci sono molti modi per raggiungere il medesimo risultato. Questa è una cosa preziosa da ricordare, perché, come si vedrà con oggetti più complessi, alcune operazioni potrebbero non dare il risultato atteso e spesso bisogna provare in altri modi.


</div>


<div class="mw-translate-fuzzy">

-   Ora faremo i fori per le viti, utilizzando lo stesso metodo di Taglio. Dato che servono 8 fori, due in ogni gamba, potremmo fare 8 oggetti da sottrarre. Invece, esploriamo altri modi e facciamo 4 tubi, che saranno riutilizzati da due delle gambe. Quindi creare quattro tubi utilizzando lo strumento <img alt="" src=images/Part_Cylinder.svg  style="width:16px;"> **Cilindro**. È nuovamente possibile farne un solo e poi duplicarlo. Dare a tutti i cilindri un raggio di 6 mm. Questa volta, avremo bisogno di ruotarli, che avviene anche attraverso la proprietà **Placement** nella scheda Dati *(**Nota:** cambiare la proprietà dell\'Asse*prima*di impostare l\'angolo, altrimenti la rotazione non viene applicata)*:
    -   Cylinder: height: 130 cm, angle: 90°, axis: x:0,y:1,z:0, position: x:-10 mm, y:40 mm, z:72 cm
    -   Cylinder001: height: 130 cm, angle: 90°, axis: x:0,y:1,z:0, position: x:-10 mm, y:84 cm, z:72 cm
    -   Cylinder002: height: 90 cm, angle: 90°, axis: x:-1,y:0,z:0, position: x:40 mm, y:-10 mm, z:70 cm
    -   Cylinder003: height: 90cm, angle: 90°, axis: x:-1,y:0,z:0, position: x:124 cm, y:-10 mm, z:70 cm


</div>

![](images/Exercise_table_04.jpg )

Notare che i cilindri sono un po\' più lunghi del necessario. Questo perché, come in tutte le applicazioni 3D basate su solidi, le operazioni booleane in FreeCAD sono a volte ipersensibili nelle situazioni faccia-contro-faccia e potrebbero non riuscire. In questo modo, ci mettiamo dalla parte della sicurezza.


<div class="mw-translate-fuzzy">

-   Ora facciamo le sottrazioni. Selezionare la prima gamba, poi, con CTRL premuto, selezionare uno dei tubi che la attraversa, premere il pulsante **Taglio**. Viene fatto il foro e viene nascosto il tubo. Cercarlo nella vista ad albero espandendo la gamba forata.
-   Selezionare un\'altra gamba trapassata da questo tubo nascosto, quindi ripetere l\'operazione, questa volta CTRL + selezionare il tubo nella vista ad albero, dato che nella vista 3D è nascosto (si può anche renderlo di nuovo visibile e selezionarlo nella vista 3D). Ripetere questa operazione per le altre gambe fino a quando ognuna di esse ha i suoi due fori:


</div>

![](images/Exercise_table_05.jpg )

Come si può vedere, ogni gamba è diventata una serie piuttosto lunga di operazioni. Tutto questo rimane parametrico, e in qualsiasi momento si può andare a cambiare qualsiasi parametro di una delle operazioni precedenti. In FreeCAD, spesso ci riferiamo a questa pila come allo \"storico della modellazione\", infatti riporta tutta la storia delle operazioni che sono state eseguite.

Un\'altra particolarità di FreeCAD è che il concetto di oggetto 3D e il concetto di operazione 3D tendono a fondersi in una stessa cosa. Il Taglio è allo stesso tempo una operazione e anche l\'oggetto 3D risultante da questa operazione. In FreeCAD questo si chiama \"caratteristica\" (feature), piuttosto che oggetto o operazione.


<div class="mw-translate-fuzzy">

-   Ora facciamo il piano del tavolo, si tratta di un semplice blocco di legno, facciamolo con un altro **Box** con lunghezza: 126 cm, larghezza: 86 cm, altezza: 8 cm, posizione: x: 10 mm, y: 10 mm, z: 67 cm. Nella scheda **Vista** si può dare un bel marrone, come il colore del legno, modificando la sua proprietà **Shape Color**:


</div>

Ora che i cinque pezzi sono completi, è un buon momento per dare loro dei nomi più appropriati di \"Cut015\". Facendo clic destro sugli oggetti nella vista ad albero (o premendo **F2**), si possono rinominare in qualcosa di più significativo per voi stessi o per un\'altra persona che in seguito apra il file. Si dice spesso che semplicemente dare dei nomi propri agli oggetti è molto più importante del modo in cui sono modellati.

-   Ora posizioniamo alcune viti. Attualmente c\'è un addon estremamente utile sviluppato da un membro della comunità di FreeCAD, che si trova nel repository [FreeCAD addons](https://github.com/FreeCAD/FreeCAD-addons), chiamato [Fasteners](https://github.com/shaise/FreeCAD_FastenersWB), che rende molto facile l\'inserimento di viti. Installazione degli ambienti supplementari è facile ed è descritto nelle [pagine addons](Std_AddonMgr/it.md).
-   Una volta installato l\'ambiente Fasteners e riavviato FreeCAD, esso appare nella lista degli ambienti, ed è possibile passare in esso. Per aggiungere una vite ai fori selezionare prima il bordo circolare del foro:


<div class="mw-translate-fuzzy">

![](images/Exercise_table_07.jpg )


</div>


<div class="mw-translate-fuzzy">

-   Poi possiamo premere uno dei pulsanti vite dell\'ambiente Fasteners, ad esempio, la **EN 1665 Vite a testa esagonale con flangia, serie pesante**. La vite viene posizionata e allineata con il foro, e il diametro viene selezionato automaticamente in base alle dimensioni del foro. A volte la vite viene posta invertita, cosa che possiamo correggere invertendo la sua proprietà **invert**. Possiamo anche impostare il suo offset a 2 mm, per seguire la stessa regola usata tra il tavolo e le gambe:


</div>


<div class="mw-translate-fuzzy">

![](images/Exercise_table_08.jpg )


</div>

-   Ripetere questa operazione per tutti i fori, e il tavolo è completo!


<div class="mw-translate-fuzzy">

**La struttura interna degli oggetti Parte**


</div>


<div class="mw-translate-fuzzy">

Come visto in precedenza, in FreeCAD è possibile selezionare non solo oggetti interi, ma parte di essi, come il bordo circolare del foro della vite. Questo è un buon momento per dare un rapido sguardo a come sono costruiti internamente gli oggetti Parte. Ogni ambiente che produce la geometria Parte si basa su questi:


</div>

![](images/Tabble_alternative_complete.png )

**The internal structure of Part objects**

As we saw above, it is possible in FreeCAD to select not only whole objects but parts of them, such as the circular border of our screw hole. This is a good time to have a quick look at how Part objects are constructed internally. Every workbench that produces Part geometry will be based on these:

-   **Vertices**: These are points (usually endpoints) on which all the rest is built. For example, a line has two vertices.
-   **Edges**: the edges are linear geometry like lines, arcs, ellipses or [NURBS](https://en.wikipedia.org/wiki/Non-uniform_rational_B-spline) curves. They usually have two vertices, but some special cases have only one (a closed circle for example).
-   **Wires**: A wire is a sequence of edges connected by their endpoints. It can contain edges of any type, and it can be closed or not.
-   **Faces**: Faces can be planar or curved, and can be formed by one closed wire, which forms the border of the face, or more than one, in case the face has holes.
-   **Shells**: Shells are simply a group of faces connected by their edges. It can be open or closed.
-   **Solids**: When a shell is tightly closed, that is, it has no \"leak\", it becomes a solid. Solids carry the notion of inside and outside. Many workbenches rely on this to make sure the objects they produce can be built in the real world.
-   **Compounds**: Compounds are simply aggregates of other shapes, no matter their type, into a single shape.

In the 3D view, you can select individual **vertices**, **edges** or **faces**. Selecting one of these also selects the whole object.

**Una nota sulla progettazione condivisa**


<div class="mw-translate-fuzzy">

Si può guardare il tavolo di cui sopra, e pensare il suo design non è buono. Il serraggio delle gambe con il piano del tavolo probabilmente è troppo debole. Si può desiderare di aggiungere dei pezzi di rinforzo, o semplicemente avere altre idee per renderlo migliore. Questo è dove la condivisione diventa interessante. È possibile scaricare il file realizzato nel corso di questo esercizio dal link sottostante, e modificarlo per renderlo migliore. Poi, se si condivide il file migliorato, altri possono essere in grado di renderlo ancora migliore, o possono utilizzare il tavolo ben progettato nei loro progetti. Il vostro disegno potrebbe poi dare altre idee ad altre persone, e forse avrete dato un piccolo contributo per un mondo migliore \...


</div>

**Download**

-   Il file prodotto in questo esercizio: <https://github.com/yorikvanhavre/FreeCAD-manual/blob/master/files/table.FCStd>

**Approfondimenti**

-   [L\'ambiente Part](Part_Workbench/it.md)
-   [The FreeCAD addons repository](https://github.com/FreeCAD/FreeCAD-addons)
-   [The Fasteners Workbench](https://github.com/shaise/FreeCAD_FastenersWB)



---
⏵ [documentation index](../README.md) > [Tutorials](Category_Tutorials.md) > Manual:Traditional modeling, the CSG way/it
