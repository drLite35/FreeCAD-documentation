# Draft SVG/it
## Descrizione

Draft SVG è un modulo software utilizzato dai comandi <img alt="" src=images/Std_Open.svg  style="width:24px;"> [Apri](Std_Open/it.md), <img alt="" src=images/Std_Import.svg  style="width:24px;"> [Importa](Std_Import/it.md) e <img alt="" src=images/Std_Export.svg  style="width:24px;"> [Esporta](Std_Export/it.md) per gestire il formato [SVG](SVG/it.md).

![](images/Screenshot_inkscape.jpg ) 
*Disegno di Inkscape esportato in SVG, e successivamente aperto in FreeCAD*



## Importazione

Si possono importare i seguenti oggetti SVG:

-   Oggetti PATH
-   Oggetti LINE
-   Oggetti RECT
-   Oggetti CIRCLE
-   Oggetti ELLIPSE
-   Oggetti POLYGON
-   Oggetti POLYLINE



## Limitazioni

FreeCAD non importerà oggetti tracciato che hanno un solo punto ([forum discussion](https://forum.freecadweb.org/viewtopic.php?f=3&t=43856)).



## Esportazione

È possibile esportare i seguenti oggetti FreeCAD:

-   Linee e spezzate (polilinee)
-   Archi e circonferenze
-   Facce
-   Testi
-   Dimensioni



### Limitazione

Ricordare che il formato SVG è un formato 2D, quindi si perdono tutte le informazioni sull\'asse Z (tutti gli oggetti risultano appiattiti).



## Gestione delle Unità 

Quando si esporta, una Unità utente (px) equivale a un millimetro.

Durante l\'importazione sono rispettati la larghezza, l\'altezza e gli attributi Viewbox. Tutti gli elementi vengono scalati alle loro dimensioni in millimetri, che è l\'unità interna di FreeCAD. Se il file SVG non contiene informazioni sulla dimensione fisica, si presuppone di avere una risoluzione di 90 DPI. L\'utilizzo di unità assolute negli attributi all\'interno del SVG è da evitare. Unità relative come em, ex e % non sono attualmente supportate.

L\'editor di SVG [Inkscape](https://inkscape.org/) attualmente funziona solo con documenti con 90 DPI. Non importa quale unità è stata selezionata in Inkscape. In uscita, tutto deve essere considerato convertito in 90 DPI e arrotondato a 6 decimali.

Dato che FreeCAD (e lo standard SVG) è agnostico alla precisione di arrotondamento fatta in Inkscape questi valori non sono arrotondati in ingresso. E rimarranno i valori strani in millimetri.

Se è necessario importare l\'SVG senza arrotondamenti, lavorare in Unità utente (px) in Inkscape. La scalatura può essere eseguita dopo l\'importazione in FreeCAD o modificando la larghezza, l\'altezza e gli attributi Viewbox.



## Preferenze

Vedere [Preferenze di Importa/Esporta](Import_Export_Preferences/it.md).



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) e [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).

Per esportare oggetti in SVG utilizzare il metodo `export` del modulo importSVG.


```python
importSVG.export(exportList, filename)
```

-   Per il sistema operativo Windows: utilizzare un **/** (barra) come separatore del percorso in {{Incode|filename}}.

Esempio:


```python
import FreeCAD as App
import Draft
import importSVG

doc = App.newDocument()

polygon1 = Draft.make_polygon(3, radius=500)
polygon2 = Draft.make_polygon(5, radius=1500)

doc.recompute()

objects = [polygon1, polygon2]
importSVG.export(objects, "/home/user/Pictures/myfile.svg")
```



---
⏵ [documentation index](../README.md) > [File Formats](Category_File%20Formats.md) > [Draft](Draft_Workbench.md) > Draft SVG/it
