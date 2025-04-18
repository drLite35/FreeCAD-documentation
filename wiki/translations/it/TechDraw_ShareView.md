---
 GuiCommand:
   Name: TechDraw ShareView
   Name/it: TechDraw Condividi Vista
   MenuLocation: TechDraw , Viste TechDraw , Condividi Vista
   Workbenches: TechDraw_Workbench/it
   Version: 0.20
   SeeAlso: 
---

# TechDraw ShareView/it



## Descrizione

Lo strumento **TechDraw Condividi Vista** rende visibile una Vista e tutti i suoi elementi dipendenti (pallinature, quote, ecc.) su una seconda Pagina.



## Utilizzo

1.  Facoltativamente selezionare una Vista, una Pagina iniziale ed una Pagina finale. Le Pagine devono essere selezionate in questo ordine.
2.  Esistono diversi modi per richiamare lo strumento:
    -   Premere il pulsante **<img src="images/TechDraw_ShareView.svg" width=16px> [Condividi Vista](TechDraw_ShareView/it.md)**.
    -   Selezionare l\'opzione **TechDraw → Viste TechDraw → <img src="images/TechDraw_ShareView.svg" width=16px> Condividi Vista** dal menu.
3.  Si aprirà una finestra di dialogo che consentirà di selezionare una Vista, da Pagina a Pagina.
4.  Premere il pulsante **OK**.



## Note

Esiste un solo oggetto View dopo l\'operazione di condivisione. Qualsiasi modifica apportata alla vista si rifletterà in entrambe le Pagine. Se la Vista viene eliminata da una pagina, verrà eliminata anche dall\'altra.



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) e [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).

Lo strumento Condividi Vista può essere utilizzato nelle [macro](Macros/it.md) e dalla [console di Python](FreeCAD_Scripting_Basics/it.md) tramite la seguente funzione:


```python
import TechDrawTools
#MoveView with a True parameter in the last position performs a copy
TechDrawTools.MoveView(viewName, fromPageName, toPageName, True)
```





{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw ShareView/it
