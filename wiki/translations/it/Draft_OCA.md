# Draft OCA/it
{{docnav/it
|[SVG](Draft_SVG/it.md)
|[DAT](Draft_DAT/it.md)
|[Draft](Draft_Workbench/it.md)
|IconL=
|IconR=
|IconC=Workbench_Draft.svg
}}






## Descrizione

Draft OCA è un modulo software utilizzato dai comandi <img alt="" src=images/Std_Open.svg  style="width:24px;"> [Std Open](Std_Open/it.md), <img alt="" src=images/Std_Import.svg  style="width:24px;"> [Std Import](Std_Import/it.md) and <img alt="" src=images/Std_Export.svg  style="width:24px;"> [Std Export](Std_Export/it.md) per gestire il [formato OCA](http://groups.google.com/group/open_cad_format).

Il formato di file OCA è uno sforzo della comunità per creare un formato di file CAD gratuito, semplice e aperto. OCA è in gran parte basato sul formato di file GCAD generato da [gCAD3D](http://www.gcad3d.org/). Entrambi i formati possono essere importati in FreeCAD e i file OCA esportati da FreeCAD possono essere aperti in gCAD3D.



## Importazione

Si posssono importare i seguenti oggetti OCA:

-   Linee
-   Archi e circonferenze
-   Aree chiuse



## Esportazione

È possibile esportare i seguenti oggetti FreeCAD:

-   Linee e spezzate (polilinee)
-   Archi e circonferenze
-   Facce



## Preferenze

Vedere [Preferenze di Importa/Esporta](Import_Export_Preferences/it.md).



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) e [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).

Per esportare oggetti in OCA utilizzare il metodo `export` del modulo importOCA.


```python
importOCA.export(exportList, filename)
```

-   Per il sistema operativo Windows: utilizzare un **/** (barra) come separatore del percorso in {{Incode|filename}}.

Esempio:


```python
import FreeCAD as App
import Draft
import importOCA

doc = App.newDocument()

polygon1 = Draft.make_polygon(3, radius=500)
polygon2 = Draft.make_polygon(5, radius=1500)

doc.recompute()

objects = [polygon1, polygon2]
importOCA.export(objects, "/home/user/Pictures/myfile.oca")
```


{{docnav/it
|[SVG](Draft_SVG/it.md)
|[DAT](Draft_DAT/it.md)
|[Draft](Draft_Workbench/it.md)
|IconL=
|IconR=
|IconC=Workbench_Draft.svg
}}



---
⏵ [documentation index](../README.md) > [File Formats](Category_File%20Formats.md) > [Draft](Draft_Workbench.md) > Draft OCA/it
