---
 GuiCommand:
   Name: Base BeispielBefehlModell
   Icon:  
   MenuLocation: Menü , Untermenü , Menütext des Befehls
   Workbenches: Workbench_Name
   Shortcut: **F** **C**
   Version: 0.19
   SeeAlso:  
---

# GuiCommand model/de



## Beschreibung

So lange die Seite in Bearbeitung ist, fügt man oben auf der Seite die Vorlage [Template:UnfinishedDocu](Template_UnfinishedDocu.md) ein, einfach durch tippen von: ****

In diesem ersten Absatz beschreibt man kurz, was der Befehl macht. Die Beschreibung kann auf andere Arbeitsbereiche verweisen, wie z. B. Arbeitsbereich <img alt="" src=images/Workbench_Sketcher.svg  style="width:24px;"> [Sketcher](Sketcher_Workbench/de.md). (*Editor note:* Das Symbol hat 24px, nicht 16px)

Nicht vergessen [Template:Version](Template_Version.md), [Template:VersionMinus](Template_VersionMinus.md), [Template:VersionPlus](Template_VersionPlus.md) und [Template:Obsolete](Template_Obsolete.md) einzusetzen, wo sie anwendbar sind.

Ein Beispiel: Das `App::Link`-Objekt ({{Version/de|0.19}}) ermöglicht die Verbindung zwischen Unterbaugruppen usw\...

Wenn möglich, eine Abbildung hinzufügen, dabei bitte den Leitfaden unter [WikiSeiten](WikiPages/de#Grafiken.md) befolgen. Das Beispiel stammt von [Part Sweep](Part_Sweep/de.md): ![](images/Part_Sweep_simple.png ) 
*Wahlweise: Eine Bildunterschrift unter der Abbildung hinzufügen, die beschreibt, was das Werkzeug macht*

Schließende und öffnende Übersetzungs-Tags sollten Bilder und andere unveränderliche Elemente einfassen, wenn sie nicht übersetzt werden müssen. Die Bildunterschriften sollten immer übersetzt werden.



## Anwendung

1.  Es gibt mehrere Möglichkeiten den Befehl aufzurufen:
    -   Die Schaltfläche **<img src="images/Std_Open.svg" width=16px> [Base ExampleCommandModel](GuiCommand_model.md)** drücken. (*Editor note:* Hier wird Die Vorlage [Template:Button](Template_Button.md) verwendet; es ist wichtig, auf den Befehl, wie in diesem Beispiel gezeigt, zu verweisen)
    -   Den Menüeintrag **Menü → Untermenü → <img src="images/Std_Open.svg" width=16px> Menütext des Befehls** auswählen. (*Editor note:* Hier wird die Vorlage [Template:MenuCommand](Template_MenuCommand.md) verwendet)
    -   Den Menüeintrag **Untermenü → <img src="images/Std_Open.svg" width=16px> Menütext des Befehls** im Kontextmenü der [Baumansicht](Tree_view/de.md) oder der [3DAnsicht](3D_view/de.md) auswählen. (*Editor note:* Auch hier wird die Vorlage [Template:MenuCommand](Template_MenuCommand.md) verwendet. Es können nicht alle Befehle über ein Kontextmenü erreicht werden.)
    -   Das Tastaturkürzel **F** dann **C** oder **Ctrl**+**Z**. (*Editor note:* Hier wird die Vorlage [Template:KEY](Template_KEY.md) verwendet; nicht alle Befehle haben ein Tastaturkürzel)
2.  Schritte mit der erforderlichen Genauigkeit beschreiben. Einige Schritte brauchen einen Tastendruck auf der **Tastatur**, während andere das Anklicken einer **Schaltfläche** mit der Maus benötigen.
3.  Optionen bearbeiten und **OK** drücken.



## Optionen

-   Wahlweise werden hier die Befehlsoptionen aufgelistet. Siehe z.B. [Draft Wire](Draft_Wire.md).



## Beispiel

Optional.



## Hinweise

-   Wahlweise kann man eine Stichpunktliste verwenden, wenn es mehrere Optionen gibt. Man kann hier auch Einschränkungen erwähnen.



## Eigenschaften

Siehe auch: [Eigenschafteneditor](Property_editor/de.md).

ein Objekt ist normalerweise von einem Basisobjekt abgeleitet. Man sollte nicht die vom Basisobjekt vererbten Eigenschaften auflisten. Siehe z.B [Draft Wire](Draft_Wire#Properties.md).



### Daten


{{TitleProperty|Property Group}}

-    **Property Name 1|PropertyType**: Beschreibung der Eigenschaft. (*Editor note:* Um den {{Value|PropertyType}} zu finden, wählt man **Alle anzeigen** im Kontextmenü des [Eigenschafteneditors](Property_editor/de.md) aus. Die QuickInfo jeder Eigenschaft enthält dann diese Information. Aber der {{Value|PropertyType}} kann auch im Quellcode gefunden werden.)



### Ansicht


{{TitleProperty|Property Group}}

-    **Property Name 2|PropertyType**: Beschreibung der Eigenschaft.



## Skripten

Siehe auch: [Autogenerierte API-Dokumentation](https://freecad.github.io/SourceDoc/) und [Grundlagen der Skripterstellung in FreeCAD](FreeCAD_Scripting_Basics/de.md).

Das Werkzeug BeispielBefehlsModell kann in [Makros](Macros/de.md) und von der [Python](Python/de.md)-Konsole aus mit den folgenden Funktionen verwendet werden:


```python
Object = makeExampleCommandModel(Data1, Data2)
```

-   Erstellt ein `Object` unter Verwndung von `Data1` und `Data2`.

Beispiel:


```python
import FreeCAD, Base

Model = Base.makeExampleCommandModel(FreeCAD.Data1, FreeCAD.Data2)
```



## Andere

Optional.



## Auswählbarer Block 


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
⏵ [documentation index](../README.md) > [Workbench_Tools_navi{{#translation:}}}} <!--use the](Category_Workbench_Tools_navi{{#translation:}}}}%20<!--use%20the.md) > [Workbench](Category_Workbench.md) > GuiCommand model/de
