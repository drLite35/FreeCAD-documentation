---
 GuiCommand:
   Name: Std Placement
   Name/de :  Std Positionierung
   MenuLocation: Bearbeiten , Placement...
   Workbenches: Alle
   SeeAlso: Std_Alignment/de, Placement/de
---

# Std Placement/de



## Beschreibung

Der Befehl **Std Positionierung** zeigt den [ Aufgabenbereich](Task_panel/de.md) Placement für ein ausgewähltes Objekt an.

![](images/Std_Placement_taskpanel.png ) 
*Der Aufgabenbereich Placement*



## Anwendung

1.  Ein einzelnes Objekt, das eine {{PropertyData/de|Placement}} besitzt auswählen.

2.  Die Menüoption **Bearbeiten → <img src="images/Std_Placement.svg" width=16px> Placement...** auswählen.

3.  Einen oder mehrere der Translations- und Rotationsparameter ändern.

4.  Mache eins der folgenden:
    -   Die Schaltfläche **OK** drücken, um die Änderungen zu übernehmen und den Aufgabenbereich zu schließen.
    -   Die Schaltfläche **Anwenden** drücken, um die Änderungen zu übernehmen, aber den Aufgabenbereich für weitere Änderungen offen zu lassen.

5.  
    **esc**oder die Schaltfläche **Abbruch** drücken, um die Ausführung abzubrechen. Dies verwirft alle Änderungen, die nicht übernommen wurden.

Der Dialog kann auch durch Klicken auf die Ellipsentaste **...** gestartet werden, die im [Eigenschafteneditor](Property_editor/de.md) erscheint, wenn man auf die {{PropertyData/de|Placement}} klickt.



## Hinweise

-   Für weitere Informationen zu den Positionierungsparametern siehe die Seite [Positionierung](Placement/de.md) und und das Tutorium [Flugzeug](Aeroplane/de.md).
-   Der Drehwinkel kann in der Benutzerschnittstelle (GUI) in Grad eingegeben werden, wird aber intern im Bogenmaß gespeichert, sodass Winkel normalerweise konvertiert werden müssen, wenn sie in Skripten verwendet werden.



## Skripten

Siehe auch: [Autogenerierte API-Dokumentation](https://freecad.github.io/SourceDoc/) und [Grundlagen der Skripterstellung in FreeCAD](FreeCAD_Scripting_Basics/de.md).

Siehe das [Python Skipterstellung Tutorium](Python_scripting_tutorial/de#Vektoren_und_Platzierungen.md).

Eine Positionierung wird intern durch eine Matrix bestimmt; in vielen Fällen ist es einfacher, dies durch zwei Komponenten darzustellen, einem `Base`-Punkt (Vektor) und einem `Rotation`-Wert. `Rotation` selbst hat verschiedene Entsprechungen. Es kann vollständig durch den Wert einer \"[quaternion](https://en.wikipedia.org/wiki/Quaternion)\" `(xi + yj + zk + w)` bestimmt werden. Es kann aber auch durch eine Rotations `Axis` (Einheitsvektor) und eine Rotations `Angle` (Bogenmaß) bestimmt werden.


```python
import FreeCAD as App

doc = App.newDocument()
obj = doc.addObject("Part::Cylinder", "Cylinder")

print(obj.Placement)
# Placement [Pos=(0,0,0), Yaw-Pitch-Roll=(0,0,0)]
print(obj.Placement.Base)
# Vector (0.0, 0.0, 0.0)
print(obj.Placement.Rotation)
# Rotation (0.0, 0.0, 0.0, 1.0)

print(obj.Placement.Rotation.Angle)
# 0.0
print(obj.Placement.Rotation.Axis)
# Vector (0.0, 0.0, 1.0)
print(obj.Placement.Rotation.Q)
# (0.0, 0.0, 0.0, 1.0)
```

Verschiebe den Basispunkt des Objekts und drehe dann das Objekt um 45 Grad um die x-Achse.

Das Modul math stellt eine Methode `radians()` zur Verfügung, mit der einfach von Grad in Bogenmaß umgewandelt werden kann und muss als erstes importiert werden.


```python
import math

obj.Placement.Base = App.Vector(5, 3, 1)
obj.Placement.Rotation.Axis = App.Vector(1, 0, 0)
obj.Placement.Rotation.Angle = math.radians(45)

print(obj.Placement)
# Placement [Pos=(5,3,1), Yaw-Pitch-Roll=(0,0,45)]
print(obj.Placement.Rotation.Q)
# (0.3826834323650898, 0.0, 0.0, 0.9238795325112867)
print(obj.Placement.Matrix)
# Matrix ((1,0,0,5),(0,0.707107,-0.707107,3),(0,0.707107,0.707107,1),(0,0,0,1))
```



---
⏵ [documentation index](../README.md) > Std Placement/de
