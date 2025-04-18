---
 GuiCommand:
   Name: TechDraw ExportPageDXF
   Name/it: TechDraw Esporta Pagina in DXF
   MenuLocation: TechDraw , Pagina , Esporta Pagina in DXF
   Workbenches: TechDraw_Workbench/it
   Version: 0.18
   SeeAlso: TechDraw_ExportPageSVG/it, Draft_DXF/it
---

# TechDraw ExportPageDXF/it



## Descrizione

Lo **strumento TechDraw Esporta Pagina in DXF** salva una pagina di disegno come file [DXF](DXF/it.md).



## Utilizzo

1.  Se nel documento sono presenti più pagine di disegno: facoltativamente attivare la pagina desiderata selezionandola nella [Vista ad albero](Tree_view/it.md).
2.  Esistono diversi modi per richiamare lo strumento:
    -   Premere il pulsante **<img src="images/TechDraw_ExportPageDXF.svg" width=16px> [Esporta Pagina in DXF](TechDraw_ExportPageDXF/it.md)**.
    -   Selezionare l\'opzione **TechDraw → Pagina → <img src="images/TechDraw_ExportPageDXF.svg" width=16px> Esporta Pagina in DXF** dal menu.
    -   Se una pagina viene visualizzata nell\'[Area della vista principale](Main_view_area/it.md): fare clic con il pulsante destro del mouse sulla finestra della pagina e selezionare l\'opzione **Esporta DXF** dal menu contestuale.
3.  Se nel documento sono presenti più pagine di disegno e non si ha ancora attivato una pagina, si apre la finestra di dialogo **Scelta Pagina**:
    1.  Selezionare la pagina desiderata.
    2.  Premere il pulsante **OK**.
4.  Si apre la finestra di dialogo **Salva file DXF**.
5.  Selezionare una posizione e un nome file.



## Limitazioni

-   Le quote radiali e di diametro verranno esportate correttamente solo se sono \"all\'interno\" dell\'arco.
-   Il ridimensionamento non è supportato. Il DXF verrà disegnato nelle dimensioni effettive della pagina TechDraw.
-   Le unità non sono supportate. Il DXF verrà disegnato in millimetri (mm). Il testo della quota verrà mostrato esattamente come visualizzato in TechDraw.
-   TechDraw non può esportare un [oggetto Draft](TechDraw_DraftView/it.md) o un [oggetto Arch](TechDraw_ArchView/it.md) in DXF. Queste viste sono elementi [SVG](SVG/it.md) generati internamente da [Draft](Draft_Workbench/it.md), quindi non è presente alcuna forma geometrica da esportare. Per esportare una vista come DXF, deve essere stata creata con [Inserisci vista](TechDraw_View/it.md) o [Inserisci gruppo di proiezione](TechDraw_ProjectionGroup/it.md). Ad esempio, selezionare un [Arch Piano di Sezione](Arch_SectionPlane/it.md), quindi utilizzare [Draft Vista forma 2D](Draft_Shape2DView/it.md) per creare una forma di proiezione piatta, quindi utilizzare [Inserisci Vista](TechDraw_View/it.md) su questo oggetto. In alternativa, selezionare gli oggetti dalla vista ad albero o dalla vista 3D ed esportali in DXF utilizzando **File → [Exporta](Std_Export.md)**.
-   Anche il cartiglio di una pagina è un modello [SVG](SVG/it.md), quindi neppure questo verrà esportato in DXF.
-   In generale, TechDraw può esportare in DXF solo gli elementi supportati dalla classe `Import::ImpExpDxfWrite` del [Import Module](Draft_DXF/it.md).



## Note

-   Questa funzione esporta le versioni R12 (AC1009) e R14 (AC1014) di [DXF](DXF/it.md).
    -   R12 è una versione precedente e più semplice dello standard, ma dovrebbe essere leggibile dalla maggior parte degli altri software.
    -   R14 è la versione predefinita. Include, tra le altre cose, il supporto per spline ed ellissi.
-   Questi parametri influiscono sull\'output:
    -   
        **Strumenti → Modifica parametri → BaseApp/Preferences/Mod/Import → DxfVersionOut**
        
        . Questo è un valore intero. Le voci valide sono 12 o 14. Il valore predefinito è 14.

    -   
        **Strumenti → Modifica parametri → BaseApp/Preferences/Mod/Import → DiscretizeEllipses**
        
        . Questo è un valore booleano. Se `True`, spline ed ellissi vengono convertite in polilinee; se `False`, spline ed ellissi vengono scritte come oggetti spline ed ellissi. Il valore predefinito è `False`. Se il parametro DxfVersionOut è 12, le spline e le ellissi vengono sempre convertite in polilinee.

    -   
        **Strumenti → Modifica parametri → BaseApp/Preferences/Mod/Import → maxsegmentlength**
        
        . Questo è un valore float. Se le spline e le ellissi vengono convertite in polilinee, questo parametro determina la lunghezza del segmento.



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) e [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).

Lo strumento SaveDXF può essere utilizzato nelle [macro](macros/it.md) e dalla console [Python](Python/it.md) tramite la seguente funzione:


```python
TechDraw.writeDXFPage(page,filename)
```





{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw ExportPageDXF/it
