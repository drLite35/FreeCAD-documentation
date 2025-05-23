---
 GuiCommand:
   Name: Draft AnnotationStyleEditor
   Name/it: Draft Stile delle annotazioni
   MenuLocation: Annotazioni , Stile delle annotazioni...<br>Gestisci , Stile delle annotazioni...
   Workbenches: Draft_Workbench/it, BIM_Workbench/it
   SeeAlso: Draft_Text/it, Draft_Label/it, Draft_Dimension/it
   Version: 0.19
---

# Draft AnnotationStyleEditor/it



## Descrizione

Il comando <img alt="" src=images/Draft_AnnotationStyleEditor.svg  style="width:24px;"> **Stile delle annotazioni** consente di definire gli stili che influenzano le proprietà visive di oggetti simili ad annotazioni, come quelli creati con i comandi [Testo](Draft_Text/it.md), [Quotatura](Draft_Dimension/it.md) ed [Etichetta](Draft_Label/it.md).

![](images/Draft_AnnotationStyleEditor_Dialog.png ) 
*La finestra di dialogo Editor Stile delle Annotazioni*



## Utilizzo

1.  Esistono diversi modi per invocare il comando:
    -   [Draft](Draft_Workbench/it.md): Premere il pulsante **<img src="images/Draft_AnnotationStyleEditor.svg" width=16px> [Stili di annotazione...](Draft_AnnotationStyleEditor/it.md)**.
    -   Draft: Selezionare l\'opzione **Annotazione → <img src="images/Draft_AnnotationStyleEditor.svg" width=16px> Stili di annotazione...** dal menu.
    -   [BIM](BIM_Workbench/it.md): Selezionare l\'opzione **Gestisci → <img src="images/Draft_AnnotationStyleEditor.svg" width=16px> Stili di annotazione...** dal menu.
2.  Si apre la finestra di dialogo **Editor degli stili di annotazione**.
3.  Selezionare uno stile dall\'elenco a discesa **Nome stile** o scegliere {{Value|Aggiungi nuovo...}} per definire un nuovo stile.
4.  Regolare facoltativamente le proprietà dello stile.
5.  Facoltativamente, premere il pulsante **[<img src=images/Accessories-text-editor.svg style="width:16px"> Rinomina** per rinominare lo stile.
6.  Facoltativamente, premere il pulsante **[<img src=images/Edit_Cancel.svg style="width:16px"> Elimina** per eliminare lo stile.
7.  Facoltativamente, premere il pulsante **[<img src=images/Std_Import.svg style="width:16px">** per importare tutti gli stili da un file **.json**. Questo sovrascriverà gli stili esistenti con lo stesso nome.
8.  Facoltativamente, premere il pulsante **[<img src=images/Std_Export.svg style="width:16px">** per esportare tutti gli stili in un file **.json**.
9.  Premere il pulsante **OK** per chiudere la finestra di dialogo e terminare il comando.



## Applicazione

Per applicare uno stile di annotazione, modificare la proprietà **Annotation Style** degli oggetti di annotazione. Questa proprietà può essere trovata nella scheda **Vista** dell\'[Editor delle proprietà](Property_editor.md).

![](images/Draft_AnnotationStyleEditor_Apply.png ) 
*Selezione di uno stile di annotazione*



## Script

Vedere anche: [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) e [Script di base per FreeCAD](FreeCAD_Scripting_Basics/it.md).

Gli stili di annotazione vengono salvati come dizionari serializzati nell\'attributo `Meta` del documento. Questo attributo viene ispezionato dall\'editor dello stile di annotazione quando viene aperto.


```python
>>> print(App.ActiveDocument.Meta["Draft_Style_Text red"])
{"ArrowSize": 2.0, "ArrowType": 0, "Decimals": 2, "DimOvershoot": 4.0, "ExtLines": 0.0, "ExtOvershoot": 4.0, "FontName": "DejaVu Sans", "FontSize": 10.0, "LineColor": 255, "LineSpacing": 1.0, "LineWidth": 2, "ScaleMultiplier": 1.0, "ShowLine": true, "ShowUnit": false, "TextColor": 4278190335, "TextSpacing": 3.0, "UnitOverride": ""}
```

Ogni stile che appare nell\'editor viene salvato internamente con il nome dello stile preceduto da `Draft_Style_`; questo evita i conflitti di nomi con altre chiavi che possono essere salvate in `Meta`, che può contenere informazioni arbitrarie.

Si può definire qualsiasi nuovo stile aggiungendo le informazioni necessarie a una chiave che inizia con `Draft_Style_`. Il valore corrispondente di questa chiave deve essere un dizionario serializzato usando `json`.


```python
import json

meta = App.ActiveDocument.Meta
props = {"ArrowSize": 7.0, "LineWidth": 6}
meta["Draft_Style_Thick_lines"] = json.dumps(props)
App.ActiveDocument.Meta = meta
```

Le proprietà non inserite verranno compilate automaticamente quando questo stile viene selezionato nell\'editor di stile e viene premuto il pulsante **OK**.

Allo stesso modo, qualsiasi dizionario serializzato può essere decompresso per essere editato.


```python
import json

meta = App.ActiveDocument.Meta
new_dict = json.loads(meta["Draft_Style_Thick_lines"])
```

Le proprietà devono avere i seguenti tipi:

Stringhe:


```python
props = {
    "FontName": "DejaVu Sans",
    "UnitOverride": ""
}
```

Numeri decimali (devono essere forniti con un punto decimale):


```python
props = {
    "ArrowSize": 2.0,
    "DimOvershoot": 4.0,
    "ExtLines": 0.0,
    "ExtOvershoot": 4.0
    "FontSize": 10.0,
    "LineSpacing": 1.0,
    "ScaleMultiplier": 1.0,
    "TextSpacing": 3.0
}
```

Numeri interi:


```python
props = {
    "ArrowType": 0,
    "Decimals": 2,
    "LineColor": 255,
    "LineWidth": 2,
    "TextColor": 4278190335
}
```


{{Incode|TextColor}}

e {{Incode|LineColor}} corrispondono a un numero intero a 32 bit, da cui è possibile estrarre i singoli valori RGBA. {{Incode|ArrowType}} è un enumeratore.

Booleane:


```python
props = {
    "ShowLine": true
    "ShowUnit": false,
}
```



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft AnnotationStyleEditor/it
