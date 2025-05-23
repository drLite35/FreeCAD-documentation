# Draft OCA/sv
## Description

Draft OCA is a software module used by the <img alt="" src=images/Std_Open.svg  style="width:24px;"> [Std Open](Std_Open.md), <img alt="" src=images/Std_Import.svg  style="width:24px;"> [Std Import](Std_Import.md) and <img alt="" src=images/Std_Export.svg  style="width:24px;"> [Std Export](Std_Export.md) commands to handle the [OCA file format](http://groups.google.com/group/open_cad_format).

The OCA file format is a community effort to create a free, simple and open CAD file format. OCA is largely based on the GCAD file format generated from [gCAD3D](http://www.gcad3d.org/). Both formats can be imported in FreeCAD, and the OCA files exported by FreeCAD can be opened in gCAD3D.


<div class="mw-translate-fuzzy">

### Öppna

Denna funktion importerar OCA/GCAD filer. [OCA filformat](http://groups.google.com/group/open_cad_format) är ett gruppförsök att skapa ett fritt, enkelt och öppet CAD filformat. OCA är i stort sett baserat på GCAD fileformatet från [gCAD3D](http://www.gcad3d.org/). Båda formaten kan importeras i FreeCAD, och de OCA filer som exporteras av FreeCAD kan öppnas i gCAD3D.


</div>


<div class="mw-translate-fuzzy">

Följande OCA objekt kan för tillfället importeras:

-   Linjer
-   Cirkelbågar och Cirklar
-   Slutna ormåden


</div>


<div class="mw-translate-fuzzy">

### Exporting

Objekt som för tillfället kan exporteras :

-   Linjer och trådar (polylines)
-   Cirkelbågar och Cirklar
-   Ytor


</div>

The following FreeCAD objects can be exported:

-   Lines and wires (polylines)
-   Arcs and circles
-   Faces


<div class="mw-translate-fuzzy">

### Alternativ

Följande parametrar kan specificeras i [Draft alternativ](Draft_Preferences/sv.md) tabben (menyn Redigera -\> Alternativ -\> Draft):

-   Importera stängda områden eller inte


</div>

See [Import Export Preferences](Import_Export_Preferences.md).

## Scripting

See also: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

To export objects to OCA use the `export` method of the importOCA module.


```python
importOCA.export(exportList, filename)
```

-   For the Windows OS: use a **/** (forward slash) as the path separator in {{Incode|filename}}.

Example:


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


<div class="mw-translate-fuzzy">


</div>



---
⏵ [documentation index](../README.md) > [File Formats](Category_File%20Formats.md) > [Draft](Draft_Workbench.md) > Draft OCA/sv
