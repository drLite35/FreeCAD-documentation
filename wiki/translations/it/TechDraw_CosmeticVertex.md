---
 GuiCommand:
   Name: TechDraw CosmeticVertex
   Name/it: TechDraw Vertice cosmetico
   MenuLocation: TechDraw , Aggiugi Vertici , Vertice cosmetico
   Workbenches: TechDraw_Workbench/it
   Version: 0.19
   SeeAlso: TechDraw_Midpoints/it, TechDraw_Quadrants/it

---

# TechDraw CosmeticVertex/it



## Descrizione

Lo strumento **TechDraw Vertice cosmetico** aggiunge ad una Vista un [vertice](Glossary#V.md) che non fa parte della geometria di origine. Questo vertice si comporta come qualsiasi altro vertice e può essere utilizzato per la quotatura.

<img alt="" src=images/TechDraw_CosmeticVertex_Sample.png  style="width:300px;"> 
*Vertice cosmetico utilizzato per creare una quotatura altrimenti impossibile*



## Utilizzo

1.  Seleziona una Vista.
2.  Esistono diversi modi per richiamare lo strumento:
    -   Premere il pulsante **<img src="images/TechDraw_CosmeticVertex.svg" width=16px> [Aggiungi Vertice cosmetico](TechDraw_CosmeticVertex/it.md)**.
    -   Seleziona l\'opzione **TechDraw → Aggiungi vertici → <img src="images/TechDraw_CosmeticVertex.svg" width=16px> Aggiungi Vertice cosmetico** dal menu.
3.  Si apre un pannello delle azioni.
4.  Facoltativamente premere il pulsante **Selettore punti** e selezionare un punto sulla pagina. Premere il pulsante **Uscita selettore** per annullare questa operazione.
5.  Facoltativamente, modificare o specificare le coordinate X e Y del punto. Le coordinate sono relative al centro della vista.
6.  Premere il pulsante **OK**.



## Note

-   Non è possibile modificare la posizione di un vertice cosmetico esistente. Al momento non c\'è altro modo che cancellarlo e crearne uno nuovo.



## Proprietà

I vertici cosmetici non hanno proprietà proprie, in quanto non sono dei Document Objects. Condividono le impostazioni di colore e dimensione con i normali vertici della geometria.



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) e [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).

I vertici cosmetici sono accessibili dalle [macro](Macros/it.md) o dalla console [Python](Python/it.md).


```python
dvp = App.ActiveDocument.View
org = App.Vector(0.0, 0.0, 0.0)
dvp.makeCosmeticVertex(org);

#lines too!
start = FreeCAD.Vector (1.0, 5.0, 0.0)
end = FreeCAD.Vector(1.0, -5.0, 0.0)
style = 2
weight = 0.75
pyGreen = (0.0, 0.0, 1.0, 0.0)
dvp.makeCosmeticLine(start,end,style, weight, pyGreen)
```





{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw CosmeticVertex/it
