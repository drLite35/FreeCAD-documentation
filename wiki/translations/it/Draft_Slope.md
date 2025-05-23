---
 GuiCommand:
   Name: Draft Slope
   Name/it: Draft Pendenza
   MenuLocation: Modifiche , Imposta la pendenza<br>Utilità , Imposta la pendenza
   Workbenches: Draft_Workbench/it, BIM_Workbench/it
   Version: 0.17
   SeeAlso: Draft Line/it, Draft Wire/it
---

# Draft Slope/it



## Descrizione

Il comando <img alt="" src=images/Draft_Slope.svg  style="width:24px;"> **Draft Pendenza** rende pendenti [Draft Linee](Draft_Line/it.md) o [Draft Polilinee](Draft_Wire/it.md) aumentando o diminuendo la coordinata Z di tutti i punti successivi al primo. Può essere utilizzato anche per appiattire [Polilinee](Draft_Wire/it.md). Si noti che la pendenza è relativa al piano XY definito dal **Placement** degli oggetti.

<img alt="" src=images/Draft_Slope_example.png  style="width:400px;"> 
*A sinistra una linea orizzontale. Sulla destra la stessa linea con un valore di pendenza di 1 (l'angolo è di 45°)*



## Utilizzo

1.  Selezionare una o più [Draft Linee](Draft_Line/it.md) e/o [Draft Polilinee](Draft_Wire/it.md).
2.  Esistono diversi modi per invocare il comando:
    -   [Draft](Draft_Workbench/it.md): Premere il pulsante **<img src="images/Draft_Slope.svg" width=16px> [Imposta la pendenza](Draft_Slope/it.md)**.
    -   Draft: Selezionare l\'opzione **Modifiche → <img src="images/Draft_Slope.svg" width=16px> Imposta la pendenza** dal menu.
    -   [BIM](BIM_Workbench/it.md): Selezionare l\'opzione **Utilità → <img src="images/Draft_Slope.svg" width=16px> Imposta la pendenza** dal menu.
3.  Inserire un valore **Pendenza**. {{Value|0}} significa che ogni segmento è orizzontale, {{Value|0.5}} significa che l\'altezza delta per ogni segmento è {{Value|0.5}} volte la sua lunghezza, ecc. Il valore può anche essere negativo.
4.  Premere **Enter** o il pulsante **OK** per terminare il comando.



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) e [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).

Non esiste un metodo Python per impostare la pendenza agli oggetti. Per emulare i risultati del comando Draft Pendenza è necessario modificare la proprietà `Punti` degli oggetti polilinea.



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft Slope/it
