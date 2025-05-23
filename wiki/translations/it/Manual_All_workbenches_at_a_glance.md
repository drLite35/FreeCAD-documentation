# Manual:All workbenches at a glance/it
{{Manual:TOC}}

Come accennato in precedenza, FreeCAD offre vari ambienti di lavoro, ciascuno dedicato a diverse applicazioni. Sebbene la moltitudine di opzioni possa sembrare inizialmente travolgente, ogni banco di lavoro è progettato per soddisfare attività specifiche, rendendo il flusso di lavoro complessivo più efficiente e adattato ai vari requisiti del progetto. Ad esempio, l\'ambiente Part Design è ideale per creare e modificare modelli 3D solidi, mentre l\'ambiente Draft è perfetto per il disegno e il disegno 2D. Questo approccio modulare consente agli utenti di personalizzare la propria interfaccia e il proprio set di strumenti in base alle proprie esigenze e preferenze specifiche.

In questa pagina si troveranno informazioni sul set base degli ambienti di lavoro e sulle loro funzionalità. Per ulteriori informazioni, fare riferimento a ciascuna pagina [ambienti di lavoro](Workbenches/it.md) nella documentazione di FreeCAD per un elenco più completo.

Una caratteristica interessante di FreeCAD è la possibilità di ottenere informazioni aggiuntive posizionando il mouse su un comando. Questa funzionalità di descrizione aiuta gli utenti a comprendere la sua funzione, fornendo indicazioni e semplificando l\'apprendimento e la navigazione nel software.

![](images/FreeCAD_022_ObjectDesc.png )

Quattro ambienti di lavoro sono progettati per funzionare in coppia, completamente incorporati l\'uno nell\'altro: BIM contiene tutti gli strumenti Draft e Part Design include tutti gli strumenti Sketcher. Tuttavia, per chiarezza, vengono descritti separatamente nel seguito.

### Part

L\'[Ambiente Part](Part_Workbench/it.md) <img alt="" src=images/Workbench_Part.svg  style="width:24px;"> offre strumenti fondamentali per lavorare con parti solide, comprese primitive come cubi e sfere, nonché operazioni geometriche e booleane di base. Fungendo da collegamento principale con [OpenCasCade](https://en.wikipedia.org/wiki/Open_Cascade_Technology), l\'ambiente Part costituisce la pietra angolare del sistema geometrico di FreeCAD, con quasi tutti gli altri ambienti che generano geometria basata su Parti. Questo sistema di modellazione parametrica consente il controllo e la modifica precisi dei modelli 3D attraverso un flusso di lavoro basato sulla cronologia. Gli utenti possono creare e perfezionare progetti complessi impilando e adattando forme e operazioni più semplici, garantendo un processo di progettazione robusto e flessibile.


<div class="mw-translate-fuzzy">

  Tool                                                                                                                       Descrizione                                                                Tool                                                                                                           Descrizione
     
  <img alt="" src=images/Part_Box.svg  style="width:32px;"> [Box](Part_Box/it.md)                                                 Disegna un cubo                                                            <img alt="" src=images/Part_Cone.svg  style="width:32px;"> [Cono](Part_Cone/it.md)                                 Disegna un cono
  <img alt="" src=images/Part_Cylinder.svg  style="width:32px;"> [Cilindro](Part_Cylinder/it.md)                             Disegna un cilindro                                                        <img alt="" src=images/Part_Sphere.svg  style="width:32px;"> [Sfera](Part_Sphere/it.md)                          Disegna una sfera
  <img alt="" src=images/Part_Torus.svg  style="width:32px;"> [Toro](Part_Torus/it.md)                                          Disegna un toro (anello)                                                   <img alt="" src=images/Part_Primitives.svg  style="width:32px;"> [Crea primitive](Part_Primitives/it.md)     Crea varie altre primitive geometriche parametriche
  <img alt="" src=images/Part_Builder.svg  style="width:32px;"> [Genera una forma](Part_Builder/it.md)                        Crea forme più complesse da primitive                                      <img alt="" src=images/Part_Fuse.svg  style="width:32px;"> [Unione](Part_Fuse/it.md)                               Unisce (fonde) due oggetti
  <img alt="" src=images/Part_Common.svg  style="width:32px;"> [Intersezione](Part_Common/it.md)                               Estrae la parte comune (intersezione) di due oggetti                       <img alt="" src=images/Part_Cut.svg  style="width:32px;"> [Taglio](Part_Cut/it.md)                                  Taglia (sottrae) un oggetto da un altro
  <img alt="" src=images/Part_JoinConnect.svg  style="width:32px;"> [JoinConnect](Part_JoinConnect/it.md)                 Collega gli interni di oggetti con pareti (es. tubazioni)                  <img alt="" src=images/Part_JoinEmbed.svg  style="width:32px;"> [JoinEmbed](Part_JoinEmbed/it.md)             Incorpora un oggetto con pareti in un altro oggetto analogo
  <img alt="" src=images/Part_JoinCutout.svg  style="width:32px;"> [Join Cutout](Part_JoinCutout/it.md)                    Crea un ritaglio nella parete di un oggetto per un altro oggetto analogo   <img alt="" src=images/Part_Extrude.svg  style="width:32px;"> [Estrudi](Part_Extrude/it.md)                     Estrude le facce piane di un oggetto
  <img alt="" src=images/Part_Fillet.svg  style="width:32px;"> [Raccorda](Part_Fillet/it.md)                                   Raccordo (arrotonda) i bordi di un oggetto                                 <img alt="" src=images/Part_Revolve.svg  style="width:32px;"> [Rivoluziona](Part_Revolve/it.md)                 Crea un solido ruotando un altro oggetto (non solido) attorno ad un asse
  <img alt="" src=images/Part_Section.svg  style="width:32px;"> [Sezione](Part_Section/it.md)                                 Crea una sezione intersecando un oggetto con un altro                      <img alt="" src=images/Part_CrossSections.svg  style="width:32px;"> [Sezioni](Part_CrossSections/it.md)   Crea più sezioni trasversali lungo un oggetto
  <img alt="" src=images/Part_Chamfer.svg  style="width:32px;"> [Smussa](Part_Chamfer/it.md)                                  Smussa i bordi di un oggetto                                               <img alt="" src=images/Part_Mirror.svg  style="width:32px;"> [Specchia](Part_Mirror/it.md)                       Specchia l\'oggetto selezionato in un determinato piano di specchio
  <img alt="" src=images/Part_RuledSurface.svg  style="width:32px;"> [Crea superficie rigata](Part_RuledSurface/it.md)   Crea una superficie rigata tra le curve selezionate                        <img alt="" src=images/Part_Sweep.svg  style="width:32px;"> [Sweep](Part_Sweep/it.md)                             Spazza uno o più profili lungo un percorso
  <img alt="" src=images/Part_Loft.svg  style="width:32px;"> [Loft](Part_Loft/it.md)                                             Congiunge due profili                                                      <img alt="" src=images/Part_Offset.png  style="width:32px;"> [Offset](Part_Offset/it.md)                         Crea una copia in scala dell\'oggetto originale
  <img alt="" src=images/Part_Thickness.svg  style="width:32px;"> [Spessore](Part_Thickness/it.md)                          Assegna uno spessore alle facce di una forma                                                                                                                                              


</div>

### Part Design 


<div class="mw-translate-fuzzy">

L\'ambiente Part Design contiene strumenti avanzati per costruire parti solide. Esso contiene inoltre tutti gli strumenti di Sketcher. Dato che può produrre solo forme solide (la regola numero uno di Parte Design), è il principale ambiente da utilizzare nella progettazione di pezzi (parti) da produrre come manufatti o stampare in 3D, poiché si ottengono sempre oggetti stampabili.


</div>


<div class="mw-translate-fuzzy">

  Tool                                                                                                                                   Descrizione                                                                               Tool                                                                                                                                                Descrizione
     
  <img alt="" src=images/PartDesign_Pad.svg  style="width:32px;"> [Prisma](PartDesign_Pad/it.md)                                        Estrudere un oggetto solido da uno schizzo selezionato                                    <img alt="" src=images/PartDesign_Pocket.svg  style="width:32px;"> [Cavità](PartDesign_Pocket/it.md)                                            Crea una tasca da uno schizzo selezionato. Il disegno deve essere mappato sulla faccia di un oggetto solido esistente
  <img alt="" src=images/PartDesign_Revolution.svg  style="width:32px;"> [Rivoluzione](PartDesign_Revolution/it.md)              Crea un solido rivoluzionando uno schizzo attorno ad un asse                              <img alt="" src=images/PartDesign_Groove.svg  style="width:32px;"> [Gola](PartDesign_Groove/it.md)                                              Crea una gola rivoluzionando uno schizzo attorno ad un asse
  <img alt="" src=images/PartDesign_Fillet.svg  style="width:32px;"> [Raccordo](PartDesign_Fillet/it.md)                             Arrotonda i bordi di un oggetto                                                           <img alt="" src=images/PartDesign_Chamfer.svg  style="width:32px;"> [Smusso](PartDesign_Chamfer/it.md)                                         Smussa i bordi di un oggetto
  <img alt="" src=images/PartDesign_Draft.svg  style="width:32px;"> [Sformo](PartDesign_Draft/it.md)                                  Applica uno sformo angolare alle facce di un oggetto                                      <img alt="" src=images/PartDesign_Mirrored.svg  style="width:32px;"> [Specchiato](PartDesign_Mirrored/it.md)                                  Specchia le funzioni su un piano o una faccia
  <img alt="" src=images/PartDesign_LinearPattern.svg  style="width:32px;"> [Serie lineare](PartDesign_LinearPattern/it.md)   Crea una schiera lineare di funzioni                                                      <img alt="" src=images/PartDesign_PolarPattern.svg  style="width:32px;"> [Serie polare](PartDesign_PolarPattern/it.md)                    Crea una schiera polare di funzioni
  <img alt="" src=images/PartDesign_Scaled.svg  style="width:32px;"> [Scalatura](PartDesign_Scaled/it.md)                            Scala le funzioni a una dimensione diversa                                                <img alt="" src=images/PartDesign_MultiTransform.svg  style="width:32px;"> [Trasformazione multipla](PartDesign_MultiTransform/it.md)   Permette di creare una schiera con una qualsiasi combinazione delle altre trasformazioni
  <img alt="" src=images/PartDesign_WizardShaft.svg  style="width:32px;"> [Shaft wizard](PartDesign_WizardShaft/it.md)          Genera un albero da una tabella di valori e permette di analizzare le forze e i momenti   <img alt="" src=images/PartDesign_InvoluteGear.svg  style="width:32px;"> [Involute gear wizard](PartDesign_InvoluteGear/it.md)            Consente di creare diversi tipi di ingranaggi


</div>

### Draft


<div class="mw-translate-fuzzy">

L\'ambiente Draft fornisce gli strumenti per fare disegni di base CAD 2D: linee, cerchi, ecc \... e una serie di utili strumenti generici come spostare, ruotare o scalare. Esso fornisce inoltre diversi aiuti di disegno, come la griglia e l\'aggancio. Esso è pensato principalmente per disegnare le linee guida per gli oggetti di Arch, ma serve anche come \"coltellino svizzero\" di FreeCAD.


</div>


<div class="mw-translate-fuzzy">

  Tool                                                                                                                     Descrizione                                                        Tool                                                                                                                 Descrizione
     
  <img alt="" src=images/Draft_Line.svg  style="width:32px;"> [Linea](Draft_Line/it.md)                                       Disegna un segmento tra 2 punti                                    <img alt="" src=images/Draft_Wire.svg  style="width:32px;"> [Wire](Draft_Wire/it.md)                                    Disegna una linea composta da più segmenti (polilinea)
  <img alt="" src=images/Draft_Circle.svg  style="width:32px;"> [Cerchio](Draft_Circle/it.md)                               Disegna un cerchio da centro e raggio                              <img alt="" src=images/Draft_Arc.svg  style="width:32px;"> [Arco](Draft_Arc/it.md)                                       Disegna un arco da centro, raggio, angolo iniziale e angolo finale
  <img alt="" src=images/Draft_Ellipse.svg  style="width:32px;">[Ellisse](Draft_Ellipse/it.md)                             Disegna un\'ellisse da due punti d\'angolo                         <img alt="" src=images/Draft_Polygon.svg  style="width:32px;"> [Poligono](Draft_Polygon/it.md)                       Disegna un poligono regolare da un centro e un raggio
  <img alt="" src=images/Draft_Rectangle.svg  style="width:32px;"> [Rettangolo](Draft_Rectangle/it.md)                   Disegna un rettangolo da 2 vertici opposti                         <img alt="" src=images/Draft_Text.svg  style="width:32px;"> [Testo](Draft_Text/it.md)                                   Disegna un testo di annotazione multi-linea
  <img alt="" src=images/Draft_Dimension.svg  style="width:32px;"> [Dimensione](Draft_Dimension/it.md)                   Disegna un\'annotazione dimensione                                 <img alt="" src=images/Draft_BSpline.svg  style="width:32px;"> [BSpline](Draft_BSpline/it.md)                        Disegna una B-Spline da una serie di punti
  <img alt="" src=images/Draft_Point.svg  style="width:32px;"> [Punto](Draft_Point/it.md)                                    Inserisce un singolo punto                                         <img alt="" src=images/Draft_ShapeString.svg  style="width:32px;"> [Forma da testo](Draft_ShapeString/it.md)     Inserisce in un dato punto nel documento corrente una forma composta che riproduce una stringa di testo
  <img alt="" src=images/Draft_Facebinder.svg  style="width:32px;"> [Lega facce](Draft_Facebinder/it.md)                Crea un nuovo oggetto da facce selezionate su oggetti esistenti    <img alt="" src=images/Draft_BezCurve.svg  style="width:32px;"> [Curva di Bezier](Draft_BezCurve/it.md)             Disegna una curva di Bezier da una serie di punti
  <img alt="" src=images/Draft_Move.svg  style="width:32px;"> [Sposta](Draft_Move/it.md)                                      Sposta o copia gli oggetti da un posto ad un altro                 <img alt="" src=images/Draft_Rotate.svg  style="width:32px;"> [Ruota](Draft_Rotate/it.md)                             Ruota gli oggetti di un certo angolo attorno ad un punto
  <img alt="" src=images/Draft_Offset.svg  style="width:32px;"> [Offset](Draft_Offset/it.md)                                Crea un offset di un oggetto ad una certa distanza                 <img alt="" src=images/Draft_Trimex.svg  style="width:32px;"> [Tronca o estendi](Draft_Trimex/it.md)                  Tronca, estende o estrude un oggetto
  <img alt="" src=images/Draft_Upgrade.svg  style="width:32px;"> [Promuovi](Draft_Upgrade/it.md)                           Converte o unisce gli oggetti in un oggetto di livello superiore   <img alt="" src=images/Draft_Downgrade.svg  style="width:32px;"> [Retrocedi](Draft_Downgrade/it.md)                Converte o separa gli oggetti in un oggetto di livello inferiore
  <img alt="" src=images/Draft_Scale.svg  style="width:32px;"> [Scala](Draft_Scale/it.md)                                    Scala gli oggetti in relazione a un punto                          <img alt="" src=images/Draft_Shape2DView.svg  style="width:32px;"> [Vista Profilo 2D](Draft_Shape2DView/it.md)   Crea un oggetto 2D ottenuto dalla proiezione di un altro oggetto
  <img alt="" src=images/Draft_Draft2Sketch.svg  style="width:32px;"> [Da Draft a Sketch](Draft_Draft2Sketch/it.md)   Converte un oggetto Draft in uno schizzo e viceversa               <img alt="" src=images/Draft_OrthoArray.svg  style="width:32px;"> [Matrice](Draft_OrthoArray/it.md)               Crea una serie polare o rettangolare da un oggetto
  <img alt="" src=images/Draft_Clone.svg  style="width:32px;"> [Clona](Draft_Clone/it.md)                                    Crea copie collegate di oggetti                                                                                                                                                         
  <img alt="" src=images/Draft_Mirror.svg  style="width:32px;"> [Specchia](Draft_Mirror/it.md)                              Specchia oggetti rispetto a una linea                                                                                                                                                   


</div>

\|- \| <img alt="" src=images/Draft_Snap_Extension.svg  style="width:32px;"> [Snap extension](Draft_Snap_Extension.md) \| Snaps to an imaginary line that extends beyond the endpoints of straight edges \| <img alt="" src=images/Draft_Snap_Parallel.svg  style="width:32px;"> [Snap parallel](Draft_Snap_Parallel.md) \| Snaps to an imaginary line parallel to straight edges \|- \| <img alt="" src=images/Draft_Snap_Special.svg  style="width:32px;"> [Snap special](Draft_Snap_Special.md) \| Snaps to special points defined by the object. \| <img alt="" src=images/Draft_Snap_Near.svg  style="width:32px;"> [Snap near](Draft_Snap_Near.md) \| Snaps to the nearest point on faces and edges \|- \| <img alt="" src=images/Draft_Snap_Ortho.svg  style="width:32px;"> [Snap ortho](Draft_Snap_Ortho.md) \| Snaps to imaginary lines that cross the previous point at multiples of 45°. \| <img alt="" src=images/Draft_Snap_Grid.svg  style="width:32px;"> [Snap grid](Draft_Snap_Grid.md) \| Snaps to the intersections of grid lines. \|- \| <img alt="" src=images/Draft_Snap_WorkingPlane.svg  style="width:32px;"> [Snap working plane](Draft_Snap_WorkingPlane.md) \| Projects snap points onto the current [working plane](Draft_SelectPlane.md) \| <img alt="" src=images/Draft_Snap_Dimensions.svg  style="width:32px;"> [Snap dimensions](Draft_Snap_Dimensions.md) \| Shows temporary X and Y dimensions \|}

### Sketcher


<div class="mw-translate-fuzzy">

L\'ambiente Sketcher contiene gli strumenti per costruire e modificare gli oggetti 2D complessi, chiamati schizzi. La geometria all\'interno di questi disegni può essere posizionata con precisione e relazionata usando i vincoli. Gli schizzi sono destinati principalmente ad essere i mattoni della geometria di PartDesign, ma in FreeCAD sono utili ovunque.


</div>


<div class="mw-translate-fuzzy">

  Tool                                                                                                                                                       Descrizione                                                                                                                                                                Tool                                                                                                                                                             Descrizione
     
  <img alt="" src=images/Sketcher_CreatePoint.svg  style="width:32px;"> [Punto](Sketcher_CreatePoint/it.md)                                           Disegna un punto                                                                                                                                                           <img alt="" src=images/Sketcher_Line.svg  style="width:32px;"> [Linea](Sketcher_CreateLine/it.md)                                                                Disegna un segmento da 2 punti
  <img alt="" src=images/Sketcher_Arc.svg  style="width:32px;"> [Arco](Sketcher_CreateArc/it.md)                                                              Disegna un arco dal centro, raggio, angolo iniziale e angolo finale                                                                                                        <img alt="" src=images/Sketcher_Create3PointArc.svg  style="width:32px;"> [Arco da 3 punti](Sketcher_Create3PointArc/it.md)                           Disegna un arco da due punti finali e un altro punto sulla circonferenza
  <img alt="" src=images/Sketcher_Circle.svg  style="width:32px;"> [Cerchio](Sketcher_CreateCircle/it.md)                                                  Disegna un cerchio da centro e raggio                                                                                                                                      <img alt="" src=images/Sketcher_Create3PointCircle.svg  style="width:32px;"> [Cerchio da 3 punti](Sketcher_Create3PointCircle/it.md)               Disegna un cerchio da tre punti sulla circonferenza
  <img alt="" src=images/Sketcher_CreateEllipseByCenter.svg  style="width:32px;"> [Ellisse](Sketcher_CreateEllipseByCenter/it.md)           Disegna un\'ellisse da centro, punto su raggio maggiore e punto su raggio minore                                                                                           <img alt="" src=images/Sketcher_CreateEllipseBy3Points.svg  style="width:32px;"> [Ellisse da 3 punti](Sketcher_CreateEllipseBy3Points/it.md)   Disegna un\'ellisse da diametro maggiore (2 punti) e punto su raggio minore
  <img alt="" src=images/Sketcher_CreateArcOfEllipse.svg  style="width:32px;"> [Arco di ellisse](Sketcher_CreateArcOfEllipse/it.md)            Disegna un arco di ellisse da centro,punto su raggio maggiore, punto iniziale e punto finale                                                                               <img alt="" src=images/Sketcher_CreatePolyline.svg  style="width:32px;"> [Polilinea](Sketcher_CreatePolyline/it.md)                                    Disegna una linea fatta di molteplici segmenti di linea. Sono disponibili diverse modalità di disegno
  <img alt="" src=images/Sketcher_CreateRectangle.svg  style="width:32px;"> [Rettangolo](Sketcher_CreateRectangle/it.md)                          Disegna un rettangolo da 2 vertici opposti                                                                                                                                 <img alt="" src=images/Sketcher_CreateTriangle.svg  style="width:32px;"> [Triangolo](Sketcher_CreateTriangle/it.md)                                    Disegna un triangolo regolare inscritto in un cerchio di geometria di costruzione
  <img alt="" src=images/Sketcher_CreateSquare.svg  style="width:32px;"> [Quadrato](Sketcher_CreateSquare/it.md)                                     Disegna un quadrato regolare inscritto in un cerchio di geometria di costruzione                                                                                           <img alt="" src=images/Sketcher_CreatePentagon.svg  style="width:32px;"> [Pentagono](Sketcher_CreatePentagon/it.md)                                    Disegna un pentagono regolare inscritto in un cerchio di geometria di costruzione
  <img alt="" src=images/Sketcher_CreateHexagon.svg  style="width:32px;"> [Esagono](Sketcher_CreateHexagon/it.md)                                   Disegna un esagono regolare inscritto in un cerchio di geometria di costruzione                                                                                            <img alt="" src=images/Sketcher_CreateHeptagon.svg  style="width:32px;"> [Ettagono](Sketcher_CreateHeptagon/it.md)                                     Disegna un ettagono regolare inscritto in un cerchio di geometria di costruzione
  <img alt="" src=images/Sketcher_CreateOctagon.svg  style="width:32px;"> [Ottagono](Sketcher_CreateOctagon/it.md)                                  Disegna un ottagono regolare inscritto in un cerchio di geometria di costruzione                                                                                           <img alt="" src=images/Sketcher_CreateSlot.svg  style="width:32px;"> [Asola](Sketcher_CreateSlot/it.md)                                                    Disegna un\'asola selezionando il centro di un semicerchio e un punto finale dell\'altro semicerchio
  <img alt="" src=images/Sketcher_CreateFillet.svg  style="width:32px;"> [Raccordo](Sketcher_CreateFillet/it.md)                                     Crea un raccordo tra le due linee                                                                                                                                          <img alt="" src=images/Sketcher_Trimming.svg  style="width:32px;"> [Smusso](Sketcher_Trimming/it.md)                                                         Tronca una linea, un cerchio o un arco in un dato punto cliccato
  <img alt="" src=images/Sketcher_External.svg  style="width:32px;"> [Geometria esterna](Sketcher_External/it.md)                                        Crea un bordo collegato alla geometria esterna                                                                                                                             <img alt="" src=images/Sketcher_ToggleConstruction.svg  style="width:32px;"> [Costruzione](Sketcher_ToggleConstruction/it.md)                      Commuta un elemento da/in modalità di costruzione. Un oggetto costruzione non è utilizzato in un\'operazione di geometria 3D ed è visibile solo durante la modifica dello schizzo che lo contiene
  <img alt="" src=images/Constraint_PointOnPoint.svg  style="width:32px;"> [Coincidente](Sketcher_ConstrainCoincident/it.md)                       Sovrappone un punto su (coincidente con) uno o più altri punti.                                                                                                            <img alt="" src=images/Constraint_PointOnObject.svg  style="width:32px;"> [Punto su oggetto](Sketcher_ConstrainPointOnObject/it.md)                   Sovrappone un punto su un altro oggetto come una linea, un arco o un asse.
  <img alt="" src=images/Constraint_Vertical.svg  style="width:32px;"> [Verticale](Sketcher_ConstrainVertical/it.md)                                   Vincola le linee selezionate o gli elementi di una polilinea ad avere un orientamento verticale. Prima di applicare questo vincolo si può selezionare più di un oggetto.   <img alt="" src=images/Constraint_Horizontal.svg  style="width:32px;"> [Orizzontale](Sketcher_ConstrainHorizontal/it.md)                                 Vincola le linee selezionate o gli elementi di una polilinea ad avere un orientamento orizzontale. Prima di applicare questo vincolo si può selezionare più di un oggetto.
  <img alt="" src=images/Sketcher_ConstrainParallel.svg  style="width:32px;"> [Parallelo](Sketcher_ConstrainParallel/it.md)                     Vincola due o più linee parallele tra loro.                                                                                                                                <img alt="" src=images/Sketcher_ConstrainPerpendicular.svg  style="width:32px;"> [Perpendicolare](Sketcher_ConstrainPerpendicular/it.md)       Vincola due linee perpendicolari tra loro, o vincola una linea perpendicolare ad un punto finale di un arco.
  <img alt="" src=images/Sketcher_ConstrainTangent.svg  style="width:32px;"> [Tangente](Sketcher_ConstrainTangent/it.md)                         Crea un vincolo di tangenza tra due entità selezionate, o un vincolo collineare tra due segmenti di linea.                                                                 <img alt="" src=images/Sketcher_ConstrainEqual.svg  style="width:32px;"> [Uguale lunghezza](Sketcher_ConstrainEqual/it.md)                             Vincoli due entità selezionate uguali fra loro. Se usato su cerchi o archi vengono posti uguali i loro raggi.
  <img alt="" src=images/Sketcher_ConstrainSymmetric.svg  style="width:32px;"> [Simmetrico](Sketcher_ConstrainSymmetric/it.md)                 Vincola due punti simmetricamente rispetto a una linea, o vincola i primi due punti selezionati simmetricamente rispetto ad un terzo punto selezionato.                    <img alt="" src=images/Sketcher_ConstrainLock.svg  style="width:32px;"> [Blocca](Sketcher_ConstrainLock/it.md)                                          Vincola l\'elemento selezionato impostando le distanze verticale e orizzontale rispetto all\'origine, bloccando in tal modo la posizione di tale elemento
  <img alt="" src=images/Constraint_HorizontalDistance.svg  style="width:32px;"> [Distanza orizzontale](Sketcher_ConstrainDistanceX/it.md)   Fissa la distanza orizzontale tra due punti o tra i punti finali della linea. Se viene selezionato un solo elemento, la distanza è impostata dall\'origine.                <img alt="" src=images/Constraint_VerticalDistance.svg  style="width:32px;"> [Distanza verticale](Sketcher_ConstrainDistanceY/it.md)               Fissa la distanza verticale tra due punti o tra i punti finali della linea. Se viene selezionato un solo elemento, la distanza è impostata dall\'origine.
  <img alt="" src=images/Sketcher_ConstrainDistance.svg  style="width:32px;"> [Lunghezza](Sketcher_ConstrainDistance/it.md)                     Fissa la lunghezza di una linea selezionata, e definisce la distanza tra due punti vincolando la distanza fra loro.                                                        <img alt="" src=images/Sketcher_ConstrainRadius.svg  style="width:32px;"> [Raggio](Sketcher_ConstrainRadius/it.md)                                    Definisce il raggio di un arco o cerchio selezionato vincolando il raggio.
  <img alt="" src=images/Sketcher_ConstrainAngle.svg  style="width:32px;"> [Angolo interno](Sketcher_ConstrainAngle/it.md)                         Definisce l\'angolo interno tra due linee selezionate.                                                                                                                     <img alt="" src=images/Sketcher_MapSketch.svg  style="width:32px;"> [Mappa sketch](Sketcher_MapSketch/it.md)                                                Mappa uno schizzo sulla faccia di un solido selezionata in precedenza
  <img alt="" src=images/Sketcher_MergeSketch.svg  style="width:32px;"> [Unisci](Sketcher_MergeSketches/it.md)                                        Unisce due o più schizzi                                                                                                                                                   <img alt="" src=images/Sketcher_MirrorSketch.svg  style="width:32px;"> [Rifletti](Sketcher_MirrorSketch/it.md)                                           Riflette gli elementi selezionati in uno schizzo


</div>




<div class="mw-translate-fuzzy">

### Arch


</div>


<div class="mw-translate-fuzzy">

L\'ambiente Arch contiene gli strumenti per lavorare con i progetti [BIM](https://en.wikipedia.org/wiki/Building_information_modeling) (ingegneria civile e architettura). Esso contiene inoltre tutti gli strumenti dell\'ambiente Draft. Arch è usato principalmente per creare oggetti BIM o dare gli attributi BIM agli oggetti costruiti con altri ambienti, al fine di esportarli in [IFC](https://en.wikipedia.org/wiki/Industry_Foundation_Classes).


</div>


<div class="mw-translate-fuzzy">

  Tool                                                                                              Descrizione                                                           Tool                                                                                                                 Descrizione
     
  <img alt="" src=images/Arch_Wall.svg  style="width:32px;"> [Muro](Arch_Wall/it.md)                    Crea un muro da zero o utilizzando un oggetto selezionato come base   <img alt="" src=images/Arch_Structure.svg  style="width:32px;"> [Struttura](Arch_Structure/it.md)                   Crea un elemento strutturale da zero o utilizzando un oggetto selezionato come base
  <img alt="" src=images/Arch_Rebar.svg  style="width:32px;"> [Armatura](Arch_Rebar/it.md)             Crea una barra di rinforzo in un elemento strutturale selezionata     <img alt="" src=images/Arch_Floor.svg  style="width:32px;"> [Piano](Arch_Floor/it.md)                                   Crea un piano includendo gli oggetti selezionati
  <img alt="" src=images/Arch_Building.svg  style="width:32px;"> [Edificio](Arch_Building/it.md)    Crea un edificio includendo gli oggetti selezionati                   <img alt="" src=images/Arch_Site.svg  style="width:32px;"> [Sito](Arch_Site/it.md)                                       Crea un sito includendo gli oggetti selezionati
  <img alt="" src=images/Arch_Window.svg  style="width:32px;"> [Finestra](Arch_Window/it.md)          Crea una finestra utilizzando un oggetto selezionato come base        <img alt="" src=images/Arch_SectionPlane.svg  style="width:32px;"> [Piano di sezione](Arch_SectionPlane/it.md)   Aggiunge un oggetto piano di sezione al documento
  <img alt="" src=images/Arch_Axis.svg  style="width:32px;"> [Asse](Arch_Axis/it.md)                    Aggiunge un sistema di assi al documento                              <img alt="" src=images/Arch_Roof.svg  style="width:32px;"> [Tetto](Arch_Roof/it.md)                                      Crea una falda del tetto da una faccia selezionata
  <img alt="" src=images/Arch_Space.svg  style="width:32px;"> [Spazio](Arch_Space/it.md)               Crea un oggetto spazio nel documento                                  <img alt="" src=images/Arch_Stairs.svg  style="width:32px;"> [Scale](Arch_Stairs/it.md)                                Crea un oggetto scala nel documento
  <img alt="" src=images/Arch_Panel.svg  style="width:32px;"> [Pannello](Arch_Panel/it.md)             Crea un oggetto pannello da un oggetto 2D selezionato                 <img alt="" src=images/Arch_Frame.svg  style="width:32px;"> [Telaio](Arch_Frame/it.md)                                  Crea un oggetto telaio da uno schema selezionato
  <img alt="" src=images/Arch_Equipment.svg  style="width:32px;"> [Arredo](Arch_Equipment/it.md)   Crea un oggetto attrezzature o arredo                                 <img alt="" src=images/Arch_SetMaterial.svg  style="width:32px;"> [Materiale](Arch_SetMaterial/it.md)             Attribuisce un materiale agli oggetti selezionati
  <img alt="" src=images/Arch_Schedule.svg  style="width:32px;"> [Scheda](Arch_Schedule/it.md)      Crea diversi tipi di schede                                           <img alt="" src=images/Arch_CutPlane.svg  style="width:32px;"> [Taglia con piano](Arch_CutPlane/it.md)               Taglia un oggetto con un piano
  <img alt="" src=images/Arch_Add.svg  style="width:32px;"> [Aggiungi](Arch_Add/it.md)                   Aggiunge oggetti a un componente                                      <img alt="" src=images/Arch_Remove.svg  style="width:32px;"> [Rimuovi](Arch_Remove/it.md)                              Sottrae o rimuove oggetti da un componente
  <img alt="" src=images/Arch_Survey.svg  style="width:32px;"> [Ispeziona](Arch_Survey/it.md)         Entra o esce dalla modalità di ispezione                                                                                                                                                   


</div>



### Altri ambienti incorporati 

Quanto sopra riassume i più importanti strumenti di FreeCAD, ma sono disponibili molti altri ambienti di lavoro, tra i quali:


<div class="mw-translate-fuzzy">

-   L\'ambiente [TechDraw](TechDraw_Workbench/it.md) per produrre disegni tecnici da modelli 3D.
-   L\'ambiente [Mesh](Mesh_Workbench/it.md) permette di lavorare con le [mesh poligonali](https://en.wikipedia.org/wiki/Polygon_mesh). Anche se le mesh (maglie) non sono il tipo di geometria preferito con cui lavorare in FreeCAD, a causa della loro mancanza di precisione e di supporto per le curve, le mesh sono ancora molto usate, e sono pienamente supportate in FreeCAD. L\'ambiente Mesh offre anche una serie di strumenti \"da Part a Mesh\" e \"da Mesh a Part\".
-   L\'ambiente [Raytracing](Raytracing_Workbench/it.md) offre strumenti per interfacciarsi con i renderer esterni come POV-Ray o LuxRender. Proprio da dentro FreeCAD, questo ambiente permette di produrre rendering di alta qualità dai modelli.
-   L\'ambiente [Spreadsheet](Spreadsheet_Workbench/it.md) permette di creare e manipolare i dati dei fogli di calcolo, che possono essere estratti dai modelli FreeCAD. Le celle del foglio possono anche essere usate da riferimento per molti settori (campi di inserimento dati) di FreeCAD, e questo permette di usarle come base di dati.
-   L\'ambiente [FEM](FEM_Workbench/it.md) si occupa di [Finite Elements Analysis](https://en.wikipedia.org/wiki/Finite_element_method), e consente di effettuare i calcoli pre e post-elaborazione FEA e di visualizzare i risultati graficamente.


</div>



### Ambienti esterni 


<div class="mw-translate-fuzzy">

Esistono anche numerosi altri ambienti molto utili, prodotti dai membri della comunità FreeCAD. Anche se non sono inclusi in una installazione standard di FreeCAD, sono facili da installare come plug-in. Essi sono tutti referenziati nel repositorio [FreeCAD-addons](https://github.com/FreeCAD/FreeCAD-addons). Tra i più sviluppati ci sono:


</div>

-   L\'ambiente [Drawing Dimensioning](https://github.com/hamish2014/FreeCAD_drawing_dimensioning) offre molti nuovi strumenti per lavorare direttamente su fogli di disegno (Drawing) e permette di aggiungere quote, annotazioni e altri simboli tecnici con un grande controllo sul loro aspetto. **L\'ambiente di lavoro Drawing non è più mantenuto.**
-   L\'ambiente [Fasteners](https://github.com/shaise/FreeCAD_FastenersWB) offre una vasta gamma di oggetti dispositivi di fissaggio pronti per l\'uso come viti, bulloni, barre, rondelle e dadi. Sono disponibili molte opzioni e impostazioni.
-   L\'ambiente [A2plus](https://github.com/kbwbe/A2plus) offre una serie di strumenti per assiemare e lavorare con gli [assemblaggi](https://en.wikipedia.org/wiki/Assembly_modelling).

**Approfondimenti**


<div class="mw-translate-fuzzy">

-   [La lista completa degli ambienti](Workbenches/it.md)
-   [Ambiente Part](Part_Workbench/it.md)
-   [Ambiente Draft](Draft_Workbench/it.md)
-   [Ambienti Sketch e Part Design](PartDesign_Workbench/it.md)
-   [Ambiente Arch](Arch_Workbench/it.md)
-   [Ambiente Drawing](Drawing_Workbench/it.md)
-   [Ambiente FEM](FEM_Workbench/it.md)
-   [Il repository FreeCAD-addons](https://github.com/FreeCAD/FreeCAD-addons)


</div>



---
⏵ [documentation index](../README.md) > Manual:All workbenches at a glance/it
