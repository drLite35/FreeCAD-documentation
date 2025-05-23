---
 GuiCommand:
   Name: TechDraw DimensionRepair
   Name/de: TechDraw Maßreparatur
   MenuLocation: TechDraw , Maßeinträge , Maßreferenzen reparieren
   Workbenches: TechDraw_Workbench/de
   Version: 0.21
   SeeAlso: TechDraw_LengthDimension/de
---

# TechDraw DimensionRepair/de



## Beschreibung

Das Werkzeug **TechDraw Maßreparatur** kann die 2D- oder 3D-Geometriereferenzen eines Maßes anpassen. Solche Referenzen können aufgrund des \"[Problems der topologischen Benennung](Topological_naming_problem/de.md)\" oder durch das Ausblenden verdeckter Kanten ungültig werden.

Siehe [TechDraw Längenmaß](TechDraw_LengthDimension/de#Begrenzungen.md) für Weiteres über Maße und das Problem der topologische Benennung.



## Anwendung

1.  Das Maß, das korrigiert werden soll, auswählen und wahlweise die neuen Geometriereferenzen wie Punkte oder Kanten in der TechDraw-Ansicht oder in der [3D-Ansicht](3D_view/de.md) auswählen.
2.  Es gibt mehrere Möglichkeiten, das Werkzeug aufzurufen:
    -   Die Schaltfläche **<img src="images/TechDraw_DimensionRepair.svg" width=16px> [Maßreferenzen reparieren](TechDraw_DimensionRepair/de.md)** drücken.
    -   Den Menüeintrag **TechDraw → Maßeinträge → <img src="images/TechDraw_DimensionRepair.svg" width=16px> Maßreferenzen reparieren** auswählen.
3.  Der Aufgabenbereich **Maß Reparieren** wird geöffnet und zeigt das ausgewählte Maß und die aktuellen Maßreferenzen an.
4.  Wenn noch nicht erfolgt, neue Geometriereferenzen auswählen.
5.  Die Schaltfläche **Referenzen durch aktuelle Auswahl ersetzen** drücken.
6.  Die Schaltfläche **OK** drücken, um das Maß zu aktualisieren.
7.  Wurden 3D-Referenzen ausgewählt: Wahlweise die {{PropertyData/de|Measure Type}} des Maßes auf {{Value|True}} setzen.



## Skripten

Siehe auch: [Autogenerierte API-Dokumentation](https://freecad.github.io/SourceDoc/) und [Grundlagen der Skripterstellung in FreeCAD](FreeCAD_Scripting_Basics/de.md).

Das Werkzeug TechDraw Maßreparatur kann nicht in [Makros](Macros/de.md) oder von der [Python](Python/de.md)-Konsole aus verwendet werden. Maßreferenz-Eigenschaften können mit Hilfe von Python aktualisiert werden.





{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw DimensionRepair/de
