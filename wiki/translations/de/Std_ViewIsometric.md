---
 GuiCommand:
   Name: Std ViewIsometric
   Name/de: Std ViewIsometric
   MenuLocation: Ansicht , Standardansichten , Axonometrisch , Isometrisch
   Workbenches: Alle
   Shortcut: **0**
   SeeAlso: Std_ViewDimetric/de, Std_ViewTrimetric/de
---

# Std ViewIsometric/de



## Beschreibung

Der **Std AnsichtIsometrisch**-Befehl richtet die Kamera in der aktiven [3D-Ansicht](3D_view/de.md) neu aus, um eine [isometrisch](https://de.wikipedia.org/wiki/Axonometrie#Isometrische_Axonometrie)e Ansicht zu erreichen. Für eine wahrlich (truly) trimetrische Ansicht muss die 3D-Ansicht im [orthographischen Modus](Std_OrthographicCamera/de.md) sein, aber der Befehl funktioniert auch, wenn die Ansicht im [perspektivischen Modus](Std_PerspectiveCamera/de.md) ist.

![](images/Std_ViewIsometric_example.svg ) 
*Das [Achsenkreuz](Std_AxisCross/de.md) und ein Würfel in isometrischer Ansicht*



## Anwendung

1.  Es gibt mehrere Möglichkeiten, den Befehl aufzurufen:
    -   Die Schaltfläche **<img src="images/Std_ViewIsometric.svg" width=16px> [Isometrisch](Std_ViewIsometric/de.md)** drücken.
    -   Den Menüeintrag **Ansicht → Standardansichten → Axonometrisch → Isometrisch** auswählen.
    -   Die Menüoption **Standardansichten → Axonometrisch → Isometrisch** im Kontextmenü der [3D-Ansicht](3D_view/de.md) auswählen.
    -   Die Menüoption **<img src="images/Std_ViewIsometric.svg" width=16px> Isometrisch** im Miniwürfelmenü des [Navigationswürfels](Navigation_Cube/de.md) auswählen.
    -   Das Tastaturkürzel: **0**.



## Skripten

Siehe auch: [Autogenerierte API-Dokumentation](https://freecad.github.io/SourceDoc/) und [Grundlagen der Skripterstellung in FreeCAD](FreeCAD_Scripting_Basics/de.md).

Die Methode `viewIsometric` des View-Objekts wird verwendet, um die Ansicht auf isometrisch zu ändern. Die Methoden `viewDimetric` und `viewTrimetric` stehen auch zur Verfügung.


```python
import FreeCADGui

view = FreeCADGui.ActiveDocument.ActiveView
view.viewIsometric()
```



---
⏵ [documentation index](../README.md) > Std ViewIsometric/de
