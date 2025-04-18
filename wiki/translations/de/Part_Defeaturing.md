---
 GuiCommand:
   Name: Part Defeaturing
   Name/de: Part FormelementEntfernen
   MenuLocation: Part , Formelement entfernen
   Workbenches: Part_Workbench/de
   Version: 0.18
   SeeAlso: Defeaturing_Workbench/de, Macro_Parametric_Defeaturing
---

# Part Defeaturing/de



## Beschreibung

Das Werkzeug **FormelementEntfernen** ist für die Entfernung ausgewählter Formelemente aus dem Modell vorgesehen. In diesem Zusammenhang sind es Formelemente wie Löcher, Vorsprünge, Lücken, Fasen, Verrundungen usw., die sich in dem Modell befinden.

Das Werkzeug \'FormelementEntfernen\' kann in verschiedenen Zusammenhängen sehr nützlich sein:

-   Um einen importierten Festkörper zu bearbeiten, wenn keine Historie der Bearbeitung verfügbar ist.
-   Beheben von Fehlern im Modell, z. B. Füllen von Lücken, Löchern usw.
-   Modellvereinfachung für die numerische Analyse, Anzeige auf mobilen Geräten, usw.

Die entfernten Formelemente werden durch die Verlängerung der angrenzenden Flächen gefüllt, so dass keine unerwarteten Teile im Ergebnis erscheinen sollten. Bitte beachte, dass das Ergebnis eine neue Form ist, die nicht mit dem Original verbunden ist; es ist also nicht-parametrisch.

Um verfügbar zu sein, muss FreeCAD auf Open Cascade 7.3.0 oder höher basieren. Falls es in deiner Version von FreeCAD nicht verfügbar ist, kannst du einen Blick auf die [Merkmal aus einer Form entfernen](Defeaturing_Workbench/de.md) Erweiterung werfen, die ähnliche Funktionen auch mit älteren Versionen von OCC oder FreeCAD anbietet.

![](images/Part_Defeaturing_example.png )



## Anwendung

1.  Die zu entfernende(n) Fläche(n) des Modells auswählen.
2.  Die Schaltfläche **[<img src=images/Part_Defeaturing.svg style="width:16px"> '''Formelement entfernen'''** drücken.
3.  Ein neues Objekt mit der Bezeichnung *\'Defeatured* wird unter Modell in der [Baumansicht](Tree_view/de.md) erstellt und das ursprüngliche Objekt wird ausgeblendet.



## Verweise

-   [3D Model Defeaturing](https://dev.opencascade.org/index.php?q=node/1211), die offizielle Ankündigung auf dem Open Cascade Collaborative Development Portal.





{{Part_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [Part](Part_Workbench.md) > Part Defeaturing/de
