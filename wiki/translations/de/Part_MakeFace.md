---
 GuiCommand:
   Name: Part MakeFace‏‎
   Name/de: Part FlächeAusLinienzügen‏‎
   MenuLocation: Formteil , Erstelle Fläche anhand von Kantenzügen
   Workbenches: Part_Workbench/de
   Version: 0.19
   SeeAlso: Part_RuledSurface/de
---

# Part MakeFace/de



## Beschreibung

The <img alt="" src=images/Part_MakeFace.svg  style="width:24px;"> **Part MakeFace** command creates a planar face from one or more coplanar closed wires (contours). They can be any valid wire, i.e. created with the [Part Workbench](Part_Workbench.md), the [Draft Workbench](Draft_Workbench.md) or the [Sketcher Workbench](Sketcher_Workbench.md). The contours should not self-intersect, or intersect each other. They can be nested to create voids.

<img alt="" src=images/Part_MakeFace-example.png  style="width:500px;">



*Faces created from different sets of wires*



## Anwendung

1.  Select one or more objects containing one or more closed wires.
2.  There are several ways to invoke the command:
    -   Press the **<img src="images/Part_MakeFace.svg" width=16px> [Make face from wires](Part_MakeFace.md)** button.
    -   Select the **Part → <img src="images/Part_MakeFace.svg" width=16px> Make face from wires** option from the menu.



---
⏵ [documentation index](../README.md) > [Part](Part_Workbench.md) > Part MakeFace/de
