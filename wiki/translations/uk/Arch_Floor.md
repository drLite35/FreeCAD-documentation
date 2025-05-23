# Arch Floor/uk
---
 GuiCommand:   Name: Arch Floor   Name/uk: Arch Floor   Workbenches: Arch_Workbench/uk   Arch, Arch Site/uk---


</div>

## Description

The **Arch Floor** tool is a special type of FreeCAD group object that has a couple of additional properties particularly suited for building floors. Particularly, they have a height property, that its children objects ([walls](Arch_Wall.md) and [structures](Arch_Structure.md)) can use to set their own height automatically. They are mostly used to organize your model.

As of <small>(v0.18)</small>  the Arch Floor is derived entirely from the [Arch BuildingPart](Arch_BuildingPart.md) object, which is a general container to organize a building model not limited to floors or storeys. Older Floor objects can be converted to the new type by right clicking on them and choosing `Convert to BuildingPart`.

## Usage

1.  Optionally, select one or more objects to be included in your new floor.
2.  Invoke the Arch Floor command several ways:
    -   Pressing the **<img src="images/Arch_Floor.svg" width=16px> [Floor](Arch_Floor.md)** button on the toolbar.
    -   Using the **L** then **V** keyboard keys.
    -   Using the **3D/BIM → Floor** entry from the top menu.

## Options

-   After creating a floor, you can add more objects to it by drag and dropping them in the Tree View or by using the **<img src="images/Arch_Add.svg" width=16px> [Arch Add](Arch_Add.md)** tool.
-   You can remove objects from a floor by drag and dropping them out of it the Tree View or by using the **<img src="images/Arch_Remove.svg" width=16px> [Arch Remove](Arch_Remove.md)** tool.

## Properties

An Arch Floor object shares all properties from an [Arch BuildingPart](Arch_BuildingPart.md), with the **Ifc Type** set to `"Building Storey"`.

## Scripting


**See also:**

[Arch API](Arch_API.md) and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

The Floor tool can be used in [macros](Macros.md) and from the [Python](Python.md) console by using the following function:


```python
Floor = makeFloor(objectslist=None, baseobj=None, name="Floor")
```

-   Creates a `Floor` object from `objectslist`, which is a list of objects.

Example:


```python
import FreeCAD, Draft, Arch

p1 = FreeCAD.Vector(0, 0, 0)
p2 = FreeCAD.Vector(2000, 0, 0)
baseline = Draft.makeLine(p1, p2)
baseline2 = Draft.makeLine(p1, -1*p2)

Wall1 = Arch.makeWall(baseline, length=None, width=150, height=2000)
Wall2 = Arch.makeWall(baseline2, length=None, width=150, height=1800)
FreeCAD.ActiveDocument.recompute()

Floor = Arch.makeFloor([Wall1, Wall2])

Building = Arch.makeBuilding([Floor])
Site = Arch.makeSite(Building)
FreeCAD.ActiveDocument.recompute() 
```


<div class="mw-translate-fuzzy">


{{docnav/uk|[Rebar](Arch_Rebar.md)|[Building Part](Arch_BuildingPart.md)|[Arch](Arch_Workbench/uk.md)|IconL=Arch_Rebar.svg |IconC=Workbench_Arch.svg |IconR=Arch_BuildingPart.svg}}


</div>



---
⏵ [documentation index](../README.md) > [BIM](Category_BIM.md) > Arch Floor/uk
