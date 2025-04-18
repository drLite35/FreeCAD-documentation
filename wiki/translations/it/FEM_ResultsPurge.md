---
 GuiCommand:
   Name: FEM ResultsPurge
   Name/it: Azzera risultati
   MenuLocation: Risultati , Azzera risultati
   Workbenches: FEM_Workbench/it
   Shortcut: **R** **P**
   SeeAlso: FEM_tutorial/it
---

# FEM ResultsPurge/it


</div>



## Descrizione

**FEM ResultsPurge** deletes all [result objects](FEM_ResultShow.md) and all result meshes from the active analysis container in the [Tree view](Tree_view.md).


<small>(v1.1)</small> 

: Deletes all output objects from all solvers (CalculiX results objects, pipelines, filters and text reports).

If you only want to delete a result object and keep the result mesh, create a copy of the result mesh, then select the Result object in the tree view and delete it by pressing **Del**. This way the created copy of the mesh will remain. (Using FEM ResultsPurge would also delete the copy.)



## Utilizzo


<div class="mw-translate-fuzzy">

1.  I diversi modi per richiamare il comando Azzera risultati:
    -   Premere il pulsante <img alt="" src=images/FEM_PurgeResults.png  style="width:24px;">
    -   Usare la scorciatoia da tastiera **S** **S**
    -   Usare **Risultati → Azzera risultati**


</div>


<div class="mw-translate-fuzzy">





</div>


{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM ResultsPurge/it
