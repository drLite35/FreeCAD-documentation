# Draft DXF/cs
## Description

Draft DXF is a software module used by the <img alt="" src=images/Std_Open.svg  style="width:24px;"> [Std Open](Std_Open.md), <img alt="" src=images/Std_Import.svg  style="width:24px;"> [Std Import](Std_Import.md) and <img alt="" src=images/Std_Export.svg  style="width:24px;"> [Std Export](Std_Export.md) commands to handle the DXF file format.

![](images/Screenshot_qcad.jpg ) 
*Qcad drawing exported to DXF, which is subsequently opened in FreeCAD*




<div class="mw-translate-fuzzy">

### Otevírání

Tato funkce otevírá soubory DXF (jakoukoliv verzi od 12 do 2007) v novém výkresu. V současné době jsou podporovány následující objekty DXF:

-   přímky
-   lomené čáry a lwpolylines
-   kružnice
-   oblouky
-   vrstvy (vrstvy obsahující objekty jsou konvertovány do skupin FreeCADu)
-   texty a mtexty
-   kótování
-   bloky (pouze konstrukce; texty, kóty a atributy uvnitř bloků jsou přeskočeny)
-   body <small>(v0.13)</small> 
-   vynášecí čáry <small>(v0.13)</small> 

Ostatní DXF entity nejsou v současné době importovány, protože zatím nejsou ve FreeCADU implementovány korespondující objekty. Jakmile budou implementovány nové funkcionality, bude pravděpodobně možné importovat více typů entit.


</div>

Two importers are available, which one is used can be specified under **Edit → Preferences... → Import-Export → DXF**. One is built-in, C++-based and fast, the other is legacy, coded in Python, slower, and requires the installation of an add-on, but can handle some entities better and can create more refined FreeCAD objects. Both support all DXF versions starting from R12.

3D solids inside a DXF file are stored under a binary ACIS/SAT blob, which at the moment cannot be read by FreeCAD.

### C++ importer 

This importer can import the following DXF objects:

-   lines
-   polylines (and lwpolylines)
-   arcs
-   circles
-   ellipses
-   splines
-   points
-   texts and mtexts
-   dimensions
-   leaders
-   blocks (only geometry, texts, dimensions and attributes inside blocks are skipped)
-   layers
-   paper space objects

### Legacy importer 

This importer can import the following DXF objects:

-   lines
-   polylines (and lwpolylines)
-   arcs
-   circles
-   ellipses
-   splines
-   3D faces
-   texts and mtexts
-   leaders
-   layers




<div class="mw-translate-fuzzy">

### Exportování

Exportovaný DXF je kompatibilní s Autocadem verze 12 a vyšší, takže by mělo být možné jej otevřít v jakékoliv aplikaci, která podporuje DXF formát. V současnosti jsou exportovány následující objekty FreeCADu:

-   přímky a dráty (lomené čáry)
-   oblouky a kružnice
-   texty
-   barvy jsou mapovány z RGB barev objektů na indexy barev Autocadu (ACI). Černá bude vždy \"podle vrstvy\"
-   vrstvy jsou mapovány z názvů skupin. Jsou-li skupiny \"zahnízděny\" (skupina ve skupině), pak je jméno vrstvy podle nejhlubší skupiny.
-   kóty, které jsou exportovány ve \"Standardním\" stylu kót


</div>

There are also two exporters. The legacy exporter exports to the R12 DXF format, the C++ exporter to the R14 DXF format. Both formats can be handled by many applications.

### C++ exporter 

Some of the features and limitations of this exporter are:

-   All FreeCAD 2D geometry is exported, except [Draft CubicBezCurves](Draft_CubicBezCurve.md), [Draft BezCurves](Draft_BezCurve.md) and [Draft Points](Draft_Point.md).
-   Straight edges from faces of 3D objects are exported, but curved edges only if they are on a plane parallel to the XY plane of the global coordinate system. Note that a DXF created from 3D objects will contain duplicate lines.
-   Texts and dimensions are not exported.
-   Colors are ignored.
-   Layers are mapped from object names.

### Legacy exporter 

Some of the features and limitations of this exporter are:

-   All FreeCAD 2D geometry is exported, except [Draft Points](Draft_Point.md). But ellipses, B-splines and Bézier curves are not exported properly.
-   3D objects are exported as flattened 2D views.
-   Compound objects are exported as blocks.
-   Texts and dimensions are exported.
-   The colors in the DXF are based on the line color of objects. Black is mapped to \"ByBlock\", other colors are mapped using AutoCAD Color Index (ACI) colors.
-   Layers are mapped from layer and group names. When groups are nested, the deepest group gives the layer name.

## Installing

For licensing reasons, the required [DXF](DXF.md) import/export libraries needed by the legacy version of the importer are not part of the FreeCAD source code. For more information see: [FreeCAD and DXF Import](FreeCAD_and_DXF_Import.md).

## Preferences

See [Import Export Preferences](Import_Export_Preferences.md).

## DWG

Because the DWG format is a proprietary, closed and undocumented format it is hard for open-source projects like FreeCAD to support it. That is why FreeCAD relies on external converters to read and write DWG files. To import a DWG file a converter is used to create a DXF first, which can then be processed by the FreeCAD DXF importer. When exporting to DWG the opposite conversion happens: the DXF created by the FreeCAD DXF exporter is turned into a DWG.

Note that the DXF format allows a 1:1 conversion of the DWG format. All applications that can read and write DWG files can do the same with DXF files, with no data loss. So asking for DXF files instead of DWG files, and supplying DXF files in turn, should not cause any problems.

There is built-in support for the following DWG converters:

-   [LibreDWG](https://www.gnu.org/software/libredwg) (open-source, lacks support for some DWG entities).
-   [ODA File Converter](https://www.opendesign.com/guestfiles/oda_file_converter) (free).
-   [QCAD pro](https://qcad.org/en/qcad-command-line-tools#dwg2dwg) (commercial).

See [Import Export Preferences](Import_Export_Preferences#DWG.md) and [FreeCAD and DWG Import](FreeCAD_and_DWG_Import.md) for more information.

## Scripting

See also: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

To export objects to DXF use the `export` method of the importDXF module.


```python
importDXF.export(objectslist, filename, nospline=False, lwPoly=False)
```

-   For the Windows OS: use a **/** (forward slash) as the path separator in {{Incode|filename}}.

Example:


```python
import FreeCAD as App
import Draft
import importDXF

doc = App.newDocument()

polygon1 = Draft.make_polygon(3, radius=500)
polygon2 = Draft.make_polygon(5, radius=1500)

doc.recompute()

objects = [polygon1, polygon2]
importDXF.export(objects, "/home/user/Pictures/myfile.dxf")
```


<div class="mw-translate-fuzzy">


</div>



---
⏵ [documentation index](../README.md) > [File Formats](Category_File%20Formats.md) > [Draft](Draft_Workbench.md) > Draft DXF/cs
