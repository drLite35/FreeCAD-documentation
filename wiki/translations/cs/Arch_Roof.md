# Arch Roof/cs
---
 GuiCommand:   Name: Arch Roof   Name/cs: Arch Střecha   Workbenches: Arch_Workbench/cs   Arch|MenuLocation: Arch , Střecha   Shortcut: R F---


</div>



## Popis


<div class="mw-translate-fuzzy">

Nástroj Střecha umožňuje vytvořit šikmou střechu z vybraných drátů. Vytvořená střecha je parametrická a udržuje vztahy se základním objektem. Mějte na paměti, prosím, že tento nástroj je stále ještě ve vývoji a může zhavarovat u velmi komplexních tvarů. Vše je založeno na principu, že každá viditelná hrana je přidělena profilu střechy (sklon, šířka, přesah, tloušťka, atd)


</div>

**Note:** This tool is still in development, and might fail with very complex shapes.

<img alt="" src=images/RoofExample.png  style="width:600px;">


<div class="mw-translate-fuzzy">

<img alt="" src=images/RoofExample.png  style="width:600px;">


</div>




<div class="mw-translate-fuzzy">

## Použití


</div>


<div class="mw-translate-fuzzy">

1.  Vytvořte drát proti směru hodinových ručiček a vyberte jej.
    -   <img alt="" src=images/CounterclockwiseWire.png  style="width:600px;">
2.  Klikněte na **<img src="images/Arch_Roof.png" width=16px> [Arch Střecha](Arch_Roof.md)
** nebo stiskněte klávesy **R** a potom **F**
3.  Standardní objekt střechy může mít podivný tvar. Je to proto, že nástoj nemá všechny potřebné informace.
4.  Po vytvoření standardní střechy, dvojkliknete na tento objekt ve stromu pohledu, abyste získali editovací přístup k vlastnostem. Úhel musí být mezi 0 a 90 stupňů.
    -   ![](images/RoofTable.png )
5.  Každá čára koresponduje se střešním panelem. Takže můžete nastavit požadované vlastnosti pro každý panel střechy.
6.  Může Vám pomoci to, že můžete nastavit Úhel nebo Vnitřní šířku na 0 a definovat Relativní Id, což zajistí automatický výpočet pro vyhledání relativních dat k relativnímu Id.
7.  Funguje to následovně:
    1.  Je-li Úhel = 0 a Vnitřní šířka = 0 pak profil je identický k relativnímu profilu.
    2.  Je-li Úhel = 0 pak úhel je vypočten tak, že výška je stejná jako u relativních profilu.
    3.  Je-li Sklon = 0 pak Vnitřní šířka je vypočtena tak, že výška je stejná jako u relativních profilu.
8.  A nakonec, nastavení úhlu na 90 stupňů vytvoří štít.
    -   <img alt="" src=images/RoofProfil.png  style="width:600px;">


</div>

## Usage (solid base) 

If your roof has a complex shape (e.g. contains pitched windows or other non-standard features) you can create a custom solid object using various other FreeCAD workbenches ([Part](Part_Workbench.md), [Sketcher](Sketcher_Workbench.md) etc.). And then use this solid as the **Base** object of your roof:

1.  Select the solid base object.
2.  Press the **<img src="images/Arch_Roof.svg" width=16px> [Arch Roof](Arch_Roof.md)** button, or press **R** then **F** keys.

## Subtracting a roof 

Roofs have an automatically generated subtraction volume (<small>(v1.0)</small>  for roofs with a solid base). When a roof is [removed](Arch_Remove.md) from the walls of a building, both the roof itself as well as everything above it is subtracted from the walls.


<small>(v1.0)</small> 

: It is possible to override the automatic subtraction volume by setting the **Subvolume** property of the roof to a custom solid object.

<img alt="" src=images/Arch_Roof_Subtract_Default.png  style="width:" height="150px;"> <img alt="" src=images/Arch_Roof_Subtract_Subvolume.png  style="width:" height="150px;"> <img alt="" src=images/Arch_Roof_Subvolume_Example.png  style="width:" height="150px;"> 
*Solid-based roof before (1st image) and after (2nd image) [removing](Arch_Remove.md) it from walls.<br>
The 3rd image shows the generated subtraction volume.*

## Options

-   Roofs share the common properties and behaviors of all [Arch Components](Arch_Component.md).



## Vlastnosti

### Data


{{TitleProperty|Roof}}


<div class="mw-translate-fuzzy">

-    **Úhly**: Seznam šikmých úhlů střešních panelů (úhel pro každou hranu v drátu).

-    **Vnitřní šířky**: Seznam šířek střešních panelů (sklon pro každou hranu drátu).

-    **IdRel**: Seznam relací Id úhlů sklonů střechy

-    **Tloušťka**: Seznam tlouštěk střešních panelů (tloušťka pro každou hranu v drátu).

-    **Přesah**: Seznam přesahů střešních panelů (přesah pro každou hranu v drátu).

-    **Povrch**: Index povrchu, který má být použit u základního objektu #Ve skutečnosti není použit


</div>

## Scripting


<div class="mw-translate-fuzzy">

## Skriptování


</div>


<div class="mw-translate-fuzzy">

Nástroj Střecha může být využit v [makrech](macros.md) a z konzoly Pythonu použitím následující funkce:


</div>


```python
Roof = makeRoof(baseobj=None, facenr=0, angles=[45.,], run=[], idrel=[0,], thickness=[50.,], overhang=[100.,], name="Roof")
```


<div class="mw-translate-fuzzy">


:   Vytvoří střechu založenou na uzavřeném drátu. Můžete dodat seznam úhlů, vnitřních šířek, idrel (relativních Id), tlouštěk, přesahů pro každou hranu v drátu, který definuje tvar střechy. Standard pro úhel je 45 stupňů a seznam je automaticky zkompletován tak aby odpovídal počtu hran v drátu.


</div>

Příklad:


```python
import FreeCAD as App
import Arch, Draft

doc = App.newDocument()

rect = Draft.makeRectangle(3000, 4000)
doc.recompute()

roof = Arch.makeRoof(rect, angles=[30.,])

p1 = App.Vector(0, 0, 0)
p2 = App.Vector(1000, 1000, 0)
p3 = App.Vector(0, 2000, 0)

wire = Draft.make_wire([p1, p2, p3], closed=True)
doc.recompute()

roof1 = Arch.makeRoof(wire)

doc.recompute()
```


<div class="mw-translate-fuzzy">


</div>



---
⏵ [documentation index](../README.md) > [BIM](Category_BIM.md) > Arch Roof/cs
