# Std New/it
---
 GuiCommand:   Name: Std_New   Name/it: Nuovo   MenuLocation: File , Nuovo   Workbenches: Tutti   Shortcut: **Ctrl**+**N**   SeeAlso: Std_Open/it, Std_Import/it---



## Descrizione

Il comando **Nuovo** crea un nuovo documento vuoto e lo rende il documento attivo.



## Utilizzo

1.  Esistono diversi modi per invocare il comando:
    -   Premere il pulsante **<img src="images/Std_New.svg" width=16px> [Nuovo](Std_New/it.md)**.
    -   Selezionare l\'opzione **File → <img src="images/Std_New.svg" width=16px> Nuovo** dal menu.
    -   Usare la scorciatoia da tastiera: **Ctrl**+**N**.



## Preferenze

Vedere anche: [Editor delle Preferenze](Preferences_Editor/it.md).

-   Per impostazione predefinita, FreeCAD si avvia senza un nuovo documento. Selezionare l\'opzione **Modifica → Preferenze... → Generale → Documento → Crea un nuovo documento all'avvio** per modificare questo comportamento.
-   Alcune proprietà del documento: nome dell\'autore, nome dell\'azienda e informazioni sulla licenza, possono essere preimpostate: **Modifica → Preferenze... → Generale → Documento → Diritti d'autore e Licenza**.



## Proprietà

Vedere anche: [Editor delle proprietà](Property_editor/it.md).

Molte proprietà possono anche essere modificate nella finestra di dialogo del comando [Informazioni sul progetto](Std_ProjectInfo/it.md).



### Dati


{{TitleProperty|Base}}

-    **Comment|String**: qualsiasi commento applicabile.

-    **Company|String**: nome dell\'azienda.

-    **Created By|String**: nome dell\'autore.

-    **Creation Date|String**: timbro data automatico (sola lettura).

-    **File Name|String**: il percorso completo del file. Vuoto se il documento non è stato salvato (sola lettura).

-    **Id|String**: non ancora implementato.

-    **Label|String**: il nome che apparirà nella [Vista ad albero](Tree_view/it.md). Sostituito dal nome del documento dopo la riapertura.

-    **Last Modified By|String**: nome dell\'autore.

-    **Last Modified Date|String**: timbro data automatico (sola lettura).

-    **License|String**: tipo di licenza.

-    **License URL|String**: URL della licenza.

-    **Material|Map|Hidden**: mappa con le proprietà del materiale.

-    **Meta|Map|Hidden**: mappa con metainformazioni aggiuntive.

-    **Show Hidden|Bool**: Se vero, gli elementi che sono stati nascosti nella [Vista ad albero](Tree_view/it.md) verranno comunque visualizzati. Nascondere gli elementi nell\'albero può essere utile quando si lavora su modelli più grandi.

-    **Tip|Link**: non ancora implementato.

-    **Tip Name|String**: non ancora implementato.

-    **Transient Dir|String**: la directory temporanea utilizzata per i dati di ripristino (sola lettura).

-    **Uid|UUID|Hidden**: UUID del documento (sola lettura).

-    **Unit System|Enumeration**: il sistema di unità del documento. Il valore iniziale dipende dal [Sistema di unità predefinito](Preferences_Editor/it#Generale_2.md). {{Version/it|1.0}}



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) e [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).

Per creare un nuovo documento usa il metodo `newDocument([name], [hidden<nowiki>=</nowiki>False])` dell\'applicazione FreeCAD. Il nome del documento deve essere univoco, che viene verificato automaticamente. Se non viene fornito alcun nome, il documento sarà denominato \"Senza titolo\". Se viene utilizzato `hidden<nowiki>=</nowiki>True`, il nuovo documento non verrà visualizzato nella GUI e non verrà visualizzata alcuna scheda.


```python
import FreeCAD
from pathlib import Path

# The folder and filename we will use:
fld = 'D:/testfiles/'
fnm = fld + 'test.FCStd'

# Make sure fld exists:
Path(fld).mkdir(parents=True, exist_ok=True)

doc = FreeCAD.newDocument()
doc.saveAs(fnm)

FreeCAD.closeDocument(doc.Name)

doc = FreeCAD.open(fnm)
doc.save()

FreeCAD.closeDocument(doc.Name)
```



---
⏵ [documentation index](../README.md) > Std New/it
