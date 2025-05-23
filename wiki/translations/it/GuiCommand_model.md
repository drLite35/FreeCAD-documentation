---
 GuiCommand:
   Name: Base ExampleCommandModel
   Name/it: Esempio di comando
   Icon: 
   MenuLocation: Menu , Sottomenu , Comando
   Workbenches: Workbench Name/it
   Shortcut: 
   SeeAlso: 
   Version: 0.17
---

# GuiCommand model/it


</div>



## Descrizione

Mentre la pagina è in costruzione, aggiungere il template [Template:UnfinishedDocu](Template_UnfinishedDocu.md) nella parte superiore della pagina semplicemente digitando: ****

In questo primo paragrafo fornire una breve descrizione di ciò che fa il comando. La descrizione può fare riferimento ad altri ambienti di lavoro come <img alt="" src=images/Workbench_Sketcher.svg  style="width:24px;"> [Sketcher](Sketcher_Workbench/it.md). (*Nota dell\'editore:* l\'immagine è 24px, non 16px)

Remember to use [Template:Version](Template_Version.md), [Template:VersionMinus](Template_VersionMinus.md), [Template:VersionPlus](Template_VersionPlus.md) and [Template:Obsolete](Template_Obsolete.md) when applicable.

For example: The `App::Link` feature (<small>(v0.19)</small> ) allows linking between sub-assemblies etc\...


<div class="mw-translate-fuzzy">

Aggiungere un\'immagine se possibile, e per favore seguire le linee guida di [WikiPages#Graphics](WikiPages#Graphics.md). Esempio tratto da Draft Linea:


</div>

![](images/Part_Sweep_simple.png )


<div class="mw-translate-fuzzy">



*Facoltativo: aggiungere una didascalia sotto l'immagine per spiegare cosa sta facendo lo strumento.*


</div>

Chiudere e riaprire i tag di traduzione prima e dopo le immagini e gli altri elementi fissi, se non c\'è bisogno di tradurli. La didascalia dovrebbe sempre essere tradotta.




<div class="mw-translate-fuzzy">

## Utilizzo


</div>

1.  There are several ways to invoke the command:
    -   Press the **<img src="images/Std_Open.svg" width=16px> [Base ExampleCommandModel](GuiCommand_model.md)** button. (*Editor note:* This uses the [Template:Button](Template_Button.md) template, it is necessary to link to the command as shown in this example)
    -   Select the **Menu → Submenu → <img src="images/Std_Open.svg" width=16px> Menu text for the command** option from the menu. (*Editor note:* This uses the [Template:MenuCommand](Template_MenuCommand.md) template)
    -   Select the **Submenu → <img src="images/Std_Open.svg" width=16px> Menu text for the command** option from the [Tree view](Tree_view.md) context menu or [3D view](3D_view.md) context menu. (*Editor note:* This also uses the [Template:MenuCommand](Template_MenuCommand.md) template, not all commands can be accessed from a context menu)
    -   Use the keyboard shortcut **F** then **C** or **Ctrl**+**Z**. (*Editor note:* This uses the [Template:KEY](Template_KEY.md) template, not all commands have a keyboard shortcut)
2.  Detailed steps as needed. Some steps may need **Keyboard** presses while others may require using the mouse to click on a **Button**.
3.  Set options and press **OK**.




<div class="mw-translate-fuzzy">

## Opzioni


</div>


<div class="mw-translate-fuzzy">

-   Qui elencare le opzioni del comando. Dare un\'occhiata a due esempi, [Linea di Draft](Draft_Line/it.md) e [Pad di PartDesign ](PartDesign_Pad/it.md).


</div>




<div class="mw-translate-fuzzy">

## Esempio

Optionale


</div>

Optional.




<div class="mw-translate-fuzzy">

## Limitazioni

-   Facoltativo, utilizzare l\'elenco puntato se ci sono più elementi


</div>

-   Optional. Use a bullet list if there are multiple items. You can also mention limitations here.




<div class="mw-translate-fuzzy">

## Proprietà


</div>

See also: [Property editor](Property_editor.md).

An object is usually derived from a base object. You should not list the properties that are inherited from that base object. See for example [Draft Wire](Draft_Wire#Properties.md).




<div class="mw-translate-fuzzy">

### Dati


</div>


{{TitleProperty|Property Group}}


<div class="mw-translate-fuzzy">

-    {{PropertyData/it|Nome della proprietà 1}}: descrizione della proprietà


</div>




<div class="mw-translate-fuzzy">

### Vista


</div>


{{TitleProperty|Property Group}}


<div class="mw-translate-fuzzy">

-    {{PropertyView/it|Nome della proprietà 2}}: descrizione della proprietà


</div>




<div class="mw-translate-fuzzy">

## Script


</div>


<div class="mw-translate-fuzzy">


**Vedere anche:**

[TechDraw API](TechDraw_API/it.md) e [Nozioni di base sugli script di FreeCAD](FreeCAD_Scripting_Basics/it.md).


</div>


<div class="mw-translate-fuzzy">

Lo strumento ExampleCommandModel può essere utilizzato nelle [macro](macros/it.md) e dalla [console Python](Python/it.md) tramite la seguente funzione:


</div>


```python
Object = makeExampleCommandModel(Data1, Data2)
```

-   Crea un `Object` usando `Data1` e `Data2`.

Esempio:


```python
import FreeCAD, Base

Model = Base.makeExampleCommandModel(FreeCAD.Data1, FreeCAD.Data2)
```




<div class="mw-translate-fuzzy">

## Ulteriori informazioni 

Optionale


</div>

Optional.

## Selectable block 


<languages/>

<translate>



{{GuiCommand
|Name=Base ExampleCommandModel
|Icon= 
|MenuLocation=Menu → Submenu → Menu text for the command
|Workbenches=[Workbench](Workbench_Name.md)
|Shortcut=**F** **C**
|Version=0.19
|SeeAlso= 
}}

== Description ==

While the page is under construction, add the [[Template:UnfinishedDocu]] template at the top of the page by simply typing: ''''''

In this first paragraph give a short description of what the command does. The description can refer to other workbenches such as the <img src="images/Workbench_Sketcher.svg" width=24px> [Sketcher Workbench](Sketcher_Workbench.md). (''Editor note:'' The image is 24px, not 16px)

Remember to use [[Template:Version]], [[Template:VersionMinus]], [[Template:VersionPlus]] and [[Template:Obsolete]] when applicable.

For example: The `App::Link` feature (<small>(v0.19)</small> ) allows linking between sub-assemblies etc...

Add an image if possible, and please follow the guidelines in [WikiPages](WikiPages#Graphics.md). Example taken from [Part Sweep](Part_Sweep.md):
</translate>
![](images/)
<translate>

*Optional: add a caption below the image to explain what the tool does*

Closing and opening translate tags should surround images, and other fixed elements, if they don't need to be translated. The caption should always be translated.

== Usage ==

# There are several ways to invoke the command:
#* Press the **<img src="images/Std_Open.svg" width=16px> [Base ExampleCommandModel](GuiCommand_model.md)** button. (''Editor note:'' This uses the [[Template:Button]] template, it is necessary to link to the command as shown in this example)
#* Select the **Menu → Submenu → <img src="images/Std_Open.svg" width=16px> Menu text for the command** option from the menu. (''Editor note:'' This uses the [[Template:MenuCommand]] template)
#* Select the **Submenu → <img src="images/Std_Open.svg" width=16px> Menu text for the command** option from the [Tree view](Tree_view.md) context menu or [3D view](3D_view.md) context menu. (''Editor note:'' This also uses the [[Template:MenuCommand]] template, not all commands can be accessed from a context menu)
#* Use the keyboard shortcut **F** then **C** or **Ctrl**+**Z**. (''Editor note:'' This uses the [[Template:KEY]] template, not all commands have a keyboard shortcut)
# Detailed steps as needed. Some steps may need **Keyboard** presses while others may require using the mouse to click on a **Button**.
# Set options and press **OK**.

== Options ==

* Optional. List the command options here. See for example [Draft Wire](Draft_Wire.md).

== Example ==

Optional.

== Notes ==

* Optional. Use a bullet list if there are multiple items. You can also mention limitations here.

== Properties ==

See also: [Property editor](Property_editor.md).

An object is usually derived from a base object. You should not list the properties that are inherited from that base object. See for example [Draft Wire](Draft_Wire#Properties.md).

=== Data ===

{{TitleProperty|Property Group}}

* **Property Name 1|PropertyType**: Description of the property. (''Editor note:'' to find the {{Value|PropertyType}} select **Show all** in the context menu of the [Property editor](Property_editor.md). The tooltip of each property will then include this information. But the {{Value|PropertyType}} can also be found in the source code.)

=== View ===

{{TitleProperty|Property Group}}

* **Property Name 2|PropertyType**: Description of the property.

== Scripting ==

See also: [https://freecad.github.io/SourceDoc/ Autogenerated API documentation] and [FreeCAD Scripting Basics](FreeCAD_Scripting_Basics.md).

The ExampleCommandModel tool can be used in [macros](Macros.md) and from the [Python](Python.md) console by using the following function:

</translate>
```python
Object = makeExampleCommandModel(Data1, Data2)
```
<translate>

* Creates an `Object` using `Data1` and `Data2`.

Example:

</translate>
```python
import FreeCAD, Base

Model = Base.makeExampleCommandModel(FreeCAD.Data1, FreeCAD.Data2)
```
<translate>

== Other ==

Optional.




</translate>
{{Workbench_Tools_navi}} 






{{Workbench_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [Workbench_Tools_navi{{#translation:}}}} <!--use the](Category_Workbench_Tools_navi{{#translation:}}}}%20<!--use%20the.md) > [Workbench](Category_Workbench.md) > GuiCommand model/it
