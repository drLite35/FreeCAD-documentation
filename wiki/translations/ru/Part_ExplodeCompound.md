---
 GuiCommand:
   Name: Part ExplodeCompound
   Name/ru: Part ExplodeCompound
   MenuLocation: Деталь , Соединить , Разъединить соединение
   Workbenches: Part_Workbench/ru
   Version: 0.18
   SeeAlso: Part_Compound/ru, Draft_Downgrade/ru
---

# Part ExplodeCompound/ru


</div>



## Описание

The <img alt="" src=images/Part_ExplodeCompound.svg  style="width:24px;"> **Part ExplodeCompound** tool splits a compound of shapes, to make each contained shape (child) available as a separate object. The children are automatically put into a [Group](Std_Group.md) if there is more than one child.

It is semi-parametric: the shapes of the children will update as the source compound changes, but if the number of children in the compound is changed, the explosion will be either missing some shapes, or have redundant objects in an error state.

Placements of extracted shapes follow the placements of the originals, plus the Placement property of each child.

The tool will also explode non-compound shapes into their lower-level constituents: compsolids into solids, solids into shells, shells into faces, faces into wires, wires into edges, edges into vertices.



## Применение

1.  Select a single compound.
2.  There are several ways to invoke the tool:
    -   Press the **<img src="images/Part_ExplodeCompound.svg" width=16px> [Explode compound](Part_ExplodeCompound.md)** button.
    -   Select the **Part → Compound → <img src="images/Part_ExplodeCompound.svg" width=16px> Explode compound** option from the menu.

## Use cases 

-   Tweaking positions of shapes made by <img alt="" src=images/Draft_OrthoArray.svg  style="width:16px;"> [Draft OrthoArray](Draft_OrthoArray.md)
-   Obtaining split pieces from result of <img alt="" src=images/Part_Slice.svg  style="width:16px;"> [Part Slice](Part_Slice.md) and <img alt="" src=images/Part_Cut.svg  style="width:16px;"> [Part Cut](Part_Cut.md)
-   Obtaining individual contours from multi-contour sketches and faces
-   Obtaining a pure solid from a solid-in-compound, for use in <img alt="" src=images/Workbench_FEM.svg  style="width:16px;"> [FEM Workbench](FEM_Workbench.md).



---
⏵ [documentation index](../README.md) > [Part](Part_Workbench.md) > Part ExplodeCompound/ru
