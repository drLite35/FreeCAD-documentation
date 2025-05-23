---
 GuiCommand:
   Name: TechDraw Dimension Length
   Name/de: TechDraw Längenmaß
   MenuLocation: TechDraw , Maßeinträge , Längenmaß einfügen
   Workbenches: TechDraw_Workbench/de
   SeeAlso: TechDraw_HorizontalDimension/de, TechDraw_VerticalDimension/de
---

# TechDraw LengthDimension/de



## Beschreibung

Das Werkzeug **TechDraw Längenmaß** fügt einer Ansicht ein lineares Maß hinzu. Das Längenmaß kann der Abstand zwischen zwei Punkten, die Länge einer geraden Kante, der senkrechte Abstand zweier Kanten oder der senkrechte Abstand eines Punkte zu einer Kanten sein.

<img alt="" src=images/TechDraw_Dimension_Length_example.png  style="width:220px;"> 
*Längenmaß, zwischen zwei Punkten gemssen*



## Anwendung

1.  Die Punkte und/oder die Kanten auswählen, die das Maß definieren. Die Geometrie kann in der [3D-Ansicht](3D_view/de.md) ausgewählt werden (die ersten beiden Möglichkeiten) oder in der Zeichnung (alle Möglichkeiten):
    -   Zwei Punkte auswählen.
    -   Eine einzelne gerade Kante auswählen.
    -   Zwei Kanten auswählen. Sind beide Kanten gerade, müssen sie parallel verlaufen. Dies erstellt ein senkrechtes Maß, wenn ein Endpunkt einer Kante senkrecht auf die andere Kante projiziert werden kann (der resultierende Punkt muss wirklich auf der Linie liegen). Sind mehrere Lösungen möglich, wird der Endpunkt verwendet, der sich am nächsten an seinem projizierten Punkt befindet. Gibt es keine gültige senkrechte Projektion, zeigt das Maß den Abstand zwischen den am nächsten zusammenligenden Endpunkten der Kanten an.
    -   Einen Punkt und eine Kante auswählen. Dies erstellt ein senkrechtes Maß. In {{VersionMinus/de|0.21}} ergibt sich nur dann senkrechte Maß, wenn der Punkt senkrecht auf die Kante projiziert werden kann. Andernfalls zeigt das Maß den Abstand des Punktes zum nächstgelegenen Endpunkt der Kante an.
2.  Wurde Geometrie in der 3D-Ansicht ausgewählt, muss die korrekte TechDraw-Ansicht durch Auswählen in der [Baumansicht](Tree_view/de.md) zur Auswahl hinzugefügt werden.
3.  Es gibt mehrere Möglichkeiten, das Werkzeug aufzurufen:
    -   
        {{Version/de|1.0}}
        
        : Ist die [Einstellung](TechDraw_Preferences/de#Maßeinträge.md) **Maß-Werkzeuge** auf {{Value|Einzelnes Werkzeug}} (Standardeinstellung) gesetzt: Den Nach-unten-Pfeil rechts neben der Schaltfläche **<img src="images/TechDraw_Dimension.svg" width=|x16px> <img src="images/Toolbar_flyout_arrow.svg" width=x16px>** drücken und die Menüoption **<img src="images/TechDraw_LengthDimension.svg" width=16px> Längenmaß einfügen** in der Ausklappliste auswählen.

    -   Hat die Einstellung einen anderen Wert (und in {{VersionMinus/de|0.21}}): Die Schaltfläche **<img src="images/TechDraw_LengthDimension.svg" width=16px> [Längenmaß einfügen](TechDraw_LengthDimension/de.md)** drücken.

    -   Den Menüeintrag **TechDraw → Maßeinträge → <img src="images/TechDraw_LengthDimension.svg" width=16px> Längenmaß einfügen** auswählen.
4.  Ein Maß wird zur Ansicht hinzugefügt.
5.  Das Maß kann an die gewünschte Position gezogen werden.
6.  Falls erforderlich, können Toleranzen, wie auf der [GD&T-Seite](TechDraw_Geometric_dimensioning_and_tolerancing/de#Toleranzen.md) beschrieben, hinzugefügt werden.



### 3D-Abmessungen anzeigen 

Das Maß zeigt anfangs die projizierte Länge an (d.h. wie auf der Zeichnung dargestellt). Wenn gefordert und wenn das Maß auf 3D-Referenzen basiert, kann es auf die Anzeige der wahren 3D-Länge umgestellt werden, indem seine {{PropertyData/de|Measure Type}} auf {{Value|True}} gesetzt wird. Damit ein Maß auf 3D-Referenzen basiert, wird bei seiner Erstellung die Geometrie in der [3D-Ansicht](3D_view/de.md) ausgewählt oder es wird das Werkzeug <img alt="" src=images/TechDraw_DimensionRepair.svg  style="width:16px;"> [TechDraw Maßreparatur](TechDraw_DimensionRepair/de.md) zur Aktualisierung vorhandener Maße verwendet.



### Eigenschaften anpassen 

Um die Eigenschaften eines Maßes (Dimension-Objekt) zu ändern, wird es in der Zeichnung oder in der [Baumansicht](Tree_view/de.md) doppelt angeklickt. Dadurch wird der [Dialog Maßeintrag](#Dialog_Maßeintrag.md) geöffnet.



## Dialog Maßeintrag 

![](images/TechDraw_DimensionDialog.png )

Der Dialog Maßeintrag ermöglicht die folgenden Einstellungen:



### Toleranzen

-   **Theoretisch genau**: Wenn diese Option aktiviert ist, wird das Maß als theoretisch genaues Maß angegeben. Als solches darf es keine Toleranzen aufweisen. Das Maß wird durch einen Rahmen um den Wert dargestellt: <img alt="" src=images/TechDraw_theoretically_exact.png  style="width:100px;">

-   **Symmetrische Toleranz**: Falls aktiviert, sind das obere und das untere Abmaß gleich und der negierte Wert des oberen Abmaßes wird für das untere Abmaß benutzt. Dargestellt wird es <img alt="" src=images/TechDraw_equal-tolerance.png  style="width:100px;">, anderenfalls <img alt="" src=images/TechDraw_Non-equal-tolerance.png  style="width:80px;">.

-   **Oberes Abmaß**: Der Wert, um den die Abmessung größer sein darf.

-   **Unteres Abmaß**: Der Wert, um den die Abmessung kleiner sein darf.



### Formatierung

-   **Formatspezifizierer**: Wie die Maßzahl formatiert werden soll. Standardspezifizierer ist {{Value|%.xf}}, wobei {{Value|x}} die Anzahl der Dezimalstellen angibt. Details zur Formatierungssyntax findet man unter [printf format string](https://en.wikipedia.org/wiki/Printf_format_string) (engl.). Es gibt noch ein zusätzliches {{Value|%w}} Format, das die festgelegte Anzahl von Ziffern nach dem Dezimaltrennzeichen ausgibt und die am Ende stehenden Nullen entfernt. Zum Beispiel heißt {{Value|%.2w}}, dass höchstens 2 Dezimalstellen ausgegeben und alle Nullen am Ende abgeschnitten werden.

-   **Beliebiger Text**: Falls aktiviert, wird die Bemaßung durch den Inhalt des **Formatspezifizierer**-Feldes ersetzt.

-   **Formatspezifizierer für das obere Abmaß**: Wie das obere Abmaß formatiert werden soll. Standardspezifizierer ist {{Value|%.xf}}, wobei {{Value|x}} die Anzahl der Dezimalstellen angibt. Details zur Formatierungssyntax findet man unter [printf format string](https://en.wikipedia.org/wiki/Printf_format_string) (engl.).

-   **Formatspezifizierer für das untere Abmaß**: Wie das untere Abmaß formatiert werden soll. Standardspezifizierer ist {{Value|%.xf}}, wobei {{Value|x}} die Anzahl der Dezimalstellen angibt. Details zur Formatierungssyntax findet man unter [printf format string](https://en.wikipedia.org/wiki/Printf_format_string) (engl.).

-   **Beliebiger Toleranztext**: Falls aktiviert, werden die Toleranzen durch den Inhalt der **Übertoleranz Formatspezifizierer**- und **Untertoleranz Formatspezifizierer**-Felder ersetzt.



### Anzeigeformat

-   **Maßpfeile umdrehen**: Dreht die Richtung um, in die die Bemaßungspfeile zeigen. Als Vorgabe sind sie innerhalb der/des Bemaßungslinie/-bogens und zeigen nach außen.

-   **Farbe**: Die Farbe für Linien und Texte.

-   **Schrifthöhe**: Die Größe des Bemaßungstextes.

-   **Zeichnungsstil**: Gibt den Standard (und dessen Stil) an, nach dem die Bemaßung gezeichnet wird. Siehe die Eigenschaft [**Standard und Stil**](#View.md) für Einzelheiten.



### Linien

-   **Winkel überschreiben**: Wenn angehakt, werden die gewöhnlichen Winkel für Maßlinie und Maßhilfslinie durch die angegebenen Werte überschrieben.

-   **Maßlinienwinkel**: Vorgabewert für den Winkel zwischen Maßlinie und der X-Achse der Ansich (in Grad).

-   **Standardwert verwenden**: Setzt den Maßlinienwinkel auf den üblichen Winkel.

-   **Auswahl verwenden**: Setzt den Maßlinienwinkel entsprechend dem Winkel der ausgewählten Kante (oder der 2 Knotenpunkte) in der Ansicht.

-   **Maßhilfslinienwinkel**: Vorgabewert für den Winkel zwischen Maßhilfslinie und der X-Achse der Ansicht (in Grad).

-   **Standardwert verwenden**: Setzt den Maßhilfslinienwinkel auf den üblichen Winkel.

-   **Auswahl verwenden**: Setzt den Maßhilfslinienwinkel entsprechend dem Winkel der ausgewählten Kante (oder der 2 Knotenpunkte) in der Ansicht.



## Begrenzungen

Dimension-Objekte (Maße) sind anfällig für das \"[Topological-Naming-Problem](topological_naming_problem/de.md)\" (Problem der topologischen Benennung). Das bedeutet, dass bei einer Änderung der 3D-Geometrie die Flächen und Kanten des Modells intern umbenannt werden könnten. Wenn ein Maß an eine Kante angehängt wird, die dann geändert wird, kann das Maß unbrauchbar werden. Im Allgemeinen ist es nicht möglich, die projizierten 2D-Maße mit den tatsächlichen 3D-Objekten synchronisiert zu halten.

Es wird daher empfohlen, Maße hinzuzufügen, wenn das 3D-Modell nicht mehr verändert wird.



### Zwischenlösung

Soll eine TechDraw-Ansicht erstellt werden, mit Maßen, die nicht unbrauchbar werden, musst ein Objekt bemaßt werden, das sich nicht ändert:

-   Eine nicht parametrische Kopie des Objekts erstellen, die mit [Part EinfacheKopie](Part_SimpleCopy/de.md) projiziert werden soll.
-   Diese Kopie auswählen, dann [TechDraw Ansicht](TechDraw_View/de.md) verwenden und die gewünschten Maße hinzufügen.
-   Wenn das ursprüngliche 3D-Modell geändert wird, wirken sich die Änderungen weder auf die einfache Kopie noch auf die Maße in der TechDraw-Ansicht aus.

Siehe [Leitbemaßungen](TechDraw_LandmarkDimension/de.md) für einen weiteren Ansatz zur Umgehung des Problems der topologischen Benennung.



## Hinweise

-   **Kantenauswahl**. Die Auswahl von Kanten kann schwierig sein. Der Auswahlbereich für Kanten kann durch Ändern der Einstellung [Auswahlbereich für Kanten](TechDraw_Preferences/de#Erweitert.md) angepasst werden.
-   **Nachkommastellen**. Maße verwenden standardmäßig die globale Einstellung der Dezimalstellen. Diese kann in den [Einstellungen](TechDraw_Preferences/de#Bemaßungen.md) oder durch Ändern der Eigenschaft FormatSpec geändert werden.
-   **Mehrere Objekte**. Ansichten können mehrere 3D-Objekte als Quelle enthalten. Maße können zwischen Geometrien verschiedener Objekte der Ansicht erstellt werden (z.B. von Object1.Vertex0 bis Object2.Vertex3).



## Eigenschaften



### Daten


{{Properties_Title/de|Basis}}

-    {{PropertyData/de|References 2D|LinkSubList}}: 2D-Objekt(e) der Zeichnungsansicht, auf denen das Maß basiert. Wird verwendet, wenn die {{PropertyData/de|Measure Type}} auf {{Value|Projected}} gesetzt ist.

-    {{PropertyData/de|References 3D|LinkSubList}}: 3D Objekt(e) auf denen das Maß basiert. Wird verwendet, wenn die {{PropertyData/de|Measure Type}} auf {{Value|True}} gesetzt ist.

-    {{PropertyData/de|Type|Enumeration}}: Länge, Radius, Durchmesser usw. Wird normalerweise nicht vom Endanwender geändert.

-    {{PropertyData/de|MeasureType|Enumeration}}: Wie die Messung durchgeführt wird.

:   

    :   True - basierend auf 3D-Geometrie
    :   Projected - basierend auf 2D-Geometrie der Zeichnungsansicht.

-    {{PropertyData/de|Theoretical Exact|Bool}}: Gibt ein theoretisch genaues Maß (Nennmaß ohne Toleranzen) an.

:   

    :   
        `False`
        
        \- standardmäßig ein normales Maß, eventuell mit Toleranzen.

    :   
        `True`
        
        \- ein theoretischer Wert. Als solcher darf er keine Toleranzen aufweisen. Der Wert ist durch einen rechteckigen Rahmen um die Maßzahl gekennzeichnet.

-    {{PropertyData/de|Equal Tolerance|Bool}}(Symmetrische Toleranz): Falls oberes und unteres Abmaß gleich sind, wird der negative Wert des oberen Abmaßes als unteres Abmaß benutzt.

:   

    :   
        `True`
        
        \- der negierte Wert von {{PropertyData/de|Over Tolerance}} (oberes Abmaß) wird als {{PropertyData/de|Under Tolerance}} (unteres Abmaß) benutzt. Die Anzeige zeigt <img alt="" src=images/TechDraw_equal-tolerance.png  style="width:100px;">.

    :   
        `False`
        
        \- der Wert von {{PropertyData/de|Under Tolerance}} wird benutzt. Die Anzeige zeigt <img alt="" src=images/TechDraw_Non-equal-tolerance.png  style="width:80px;">.

-    {{PropertyData/de|Over Tolerance|QuantityConstraint}}(oberes Abmaß): Der Betrag, um den das Maß größer sein darf.

-    {{PropertyData/de|Under Tolerance|QuantityConstraint}}(unteres Abmaß): Der Betrag, um den das Maß kleiner sein darf.

-    {{PropertyData/de|Inverted|Bool}}: Gibt an, ob das Maß einen üblichen oder einen invertierten Wert darstellt.

:   

    :   
        `False`
        
        \- der gewöhnliche Wert wird verwendet. Für Länge ist es eine positive Zahl, für Winkel der schräggestellte Wert (0° - 180°).

    :   
        `True`
        
        \- der umgekehrte Wert wird verwendet. Für Länge eine negative Zahl, für Winkel der Reflexwert (180° - 360°).

-    {{PropertyData/de|X}}: Horizontale Position des Maßtexts relativ zur Ansicht.

-    {{PropertyData/de|Y}}: Vertikale Position des Maßtexts relativ zur Ansicht.

-    {{PropertyData/de|Lock Position|Bool|Hidden}}: Wenn `True`, wird die Position des Maßtextes fixiert.

-    {{PropertyData/de|Rotation|Angle|Hidden}}: Schreibgeschützt.

-    {{PropertyData/de|Scale Type|Enumeration|Hidden}}: Schreibgeschützt.

-    {{PropertyData/de|Scale|FloatConstant|Hidden}}: Schreibgeschützt.

-    {{PropertyData/de|Caption|String|Hidden}}: Nicht verwendet.


{{Properties_Title/de|Format}}

-    {{PropertyData/de|Format Spec|String}}: Wie die Maßzahl formatiert sein wird. Siehe [Formatierung](#Formatierung.md).

-    {{PropertyData/de|Format Spec Over Tolerance|String}}: Wie {{PropertyData/de|Format Spec}}, aber für obere Abmaße.

-    {{PropertyData/de|Format Spec Under Tolerance|String}}: Wie {{PropertyData/de|Format Spec}}, aber für untere Abmaße.

-    {{PropertyData/de|Arbitrary|Bool}}: Gibt an, ob die Maßzahl durch den Inhalt von **Format Spec** ersetzt wird.

:   

    :   
        `False`
        
        \- der Inhalt von **Format Spec** wird zur Formatierung der Maßzahl verwendet.

    :   
        `True`
        
        \- der Inhalt von **Format Spec** wird anstatt der Maßzahl als Text angezeigt.

-    {{PropertyData/de|Arbitrary Tolerances|Bool}}: Wie {{PropertyData/de|Arbitrary}}, aber für die Toleranz.


{{Properties_Title/de|Override}}

-    {{PropertyData/de|Angle Override|Bool}}: Gibt an, ob die Richtung der Maßlinien und Maßhilfslinien überschrieben wird.

:   

    :   
        `False`
        
        \- die Richtungen werden wie üblich berechnet.

    :   
        `True`
        
        \- die Richtungen werden mit den Werten der Eigenschaften Line Angle und Extension Angle überschrieben.

-    {{PropertyData/de|Line Angle|Angle}}: Winkel zwischen Maßlinie und der X-Achse der Ansicht (in Grad).

-    {{PropertyData/de|Extension Angle|Angle}}: Winkel zwischen Maßlinie(n) und der X-Achse der Ansicht (in Grad).


{{Properties_Title|References}}

-    {{PropertyData/de|Saved Geometry|TopoShapeList|Hidden}}: Referenzgeometrie. {{Version/de|0.21}}



### Ansicht


{{TitleProperty|Basis}}

-    {{PropertyView/de|Keep Label|Bool}}: Nicht verwendet.

-    {{PropertyView/de|Stack Order|Integer}}: Angabe der Lage über oder unter anderen Zeichnungsobjekten. {{Version/de|0.21}}


{{Properties_Title|Dimension Format}}

-    {{PropertyView/de|Arrowsize|Length}}: Die Größe der Maßpfeile. {{Version/de|0.21}}

-    {{PropertyView/de|Color}}(Farbe): Farbe für Linien und Text.

-    {{PropertyView/de|Flip Arrowheads}}(Pfeilspitzen umkehren): Standardmäßig zeigen bei *innerhalb* der Maßlinie/des Bogens plazierten Maßzahlen die Maßpfeile *nach außen*. Wird die Maßzahl *außerhalb* der Maßlinie/des Bogens platziert, zeigen die Maßpfeile *nach innen*.

:   

    :   
        `False`
        
        \- Wählt die Richtung der Maßpfeile automatisch nach der obigen Regel aus.

    :   
        `True`
        
        \- Dreht die automatisch gewählte Richtung um.

-    {{PropertyView/de|Font|Font}}: Der Name der Schriftart für die Maßeinträge.

-    {{PropertyView/de|Fontsize|Length}}(Schrifthöhe): Höhe des Maßtextes.

-    {{PropertyView/de|Gap Factor ASME|Float}}(Lückenfaktor ASME): Legt die Weite der Lücke zwischen Geometrie und Anfang der Maßhilfslinie fest. Dieser Wert mal der Linienbreite (Line Width) ergibt die Weite der Lücke. {{Version/de|0.21}}

-    {{PropertyView/de|Gap Factor ISO|Float}}(Lückenfaktor ISO): Legt die Weite der Lücke zwischen Geometrie und Anfang der Maßhilfslinie fest. Dieser Wert mal der Linienbreite (Line Width) ergibt die Weite der Lücke. {{Version/de|0.21}}

-    {{PropertyView/de|Line Spacing Factor|Float}}(Abstandsfaktor): Stellt den Abstand zwischen Maßzahl und Maßlinie ein. Der Abstand ergibt sich aus diesem Wert mal der Linienbreite. {{Version/de|0.21}}

-    {{PropertyView/de|Line Width}}(Linienbreite): Maßlinienstärke.

-    {{PropertyView/de|Rendering Extent}}(Darstellungsergänzung): Eher universelle Eigenschaft, die angibt, wie viel Platz ein Maßeintrag einnehmen darf:

:   

    :   None - Es werden keine Linien oder Pfeile gezeichnet, sondern nur die nackte Maßzahl dargestellt.
    :   Minimal - Für Längen und Winkel wird eine Hinweislinie (einseitige Maßlinienbegrenzung) gezeichnet, die die Maßzahl mit einer *virtuellen Maßhilfslinie* verbindet. Die Maßhilfslinie selbst wird nicht hinzugefügt.
    :   Durchmesser werden mit Confined-Ergänzung, Radien mit Reduced-Ergänzung dargestellt.
    :   Confined - Für Längen und Winkel wird eine Maßlinie (gerade, oder Bogen) mit beidseitigen Maßlinienbegrenzungen dargestellt, die die *virtuellen Maßhilfslinien* des Start- und Endpunktes verbindet, wobei die Maßhilfslinien selbst nicht hinzugefügt werden.
    :   Durchmesser werden mit einer Maßlinie mit mindestens einer Maßlinienbegrenzung von der Maßzahl zum nächsten Punkt auf dem Kreis gezeichnet, Radien wie bei der Reduced<-Ergänzung.
    :   Reduced - Für Längen und Winkel wird eine Hinweislinie (einseitige Maßlinienbegrenzung) gezeichnet, die die Maßzahl mit der ebenfalls gezeichneten Maßhilfslinie verbindet.
    :   Durchmesser werden mit einer Hinweislinie (einseitige Maßlinienbegrenzung) von der Maßzahl zum nächsten Punkt auf dem Kreis, Radien mit einer Maßlinie mit mindestens einer Maßlinienbegrenzung von der Maßzahl zum nächsten Punkt auf dem Kreis gezeichnet.
    :   Normal - Der Standardwert. Für Längen und Winkel wird eine Maßlinie (gerade, oder Bogen) mit beidseitigen Maßlinienbegrenzungen dargestellt, die die Maßhilfslinien verbindet, und die Maßhilfslinien selbst auch.
    :   Durchmesser werden mit einer Maßlinie mit beidseitigen Maßlinienbegrenzungen dargestellt, die über den Mittelpunkt verlaufen und zwei Punkte auf dem Kreis verbinden.
    :   Radien werden mit einer Hinweislinie (einseitige Maßlinienbegrenzung) vom Mittelpunkt zum nächsten Punkt auf dem Kreisbogen gezeichnet.
    :   Expanded - Nur Durchmesser unterstützen diesen Wert, so dass sie horizontalen oder vertikalen Längenmaßen ähnlich dargestellt werden. Andere Maßarten werden wie bei der Normal-Ergänzung dargestellt.

-    {{PropertyView/de|Standard And Style|Enumeration}}(Standard und Stil): Gibt die Norm (und deren Ausführungsart) an, nach der Maßeingeträge erfolgen:

:   

    :   <img alt="Unterschiede zwischen den unterstützten Normen" src=images/TechDraw_Dimension_standardization.png  style="width:500px;">

    :   ISO Oriented - Darstellung nach ISO 129-1; Text wird so gedreht, dass er parallel zur Tangente an die Maßlinie liegt.

    :   ISO Referencing - Darstellung nach ISO 129-2; der Text steht immer horizontal, oberhalb einer kürzest möglichen Bezugslinie.

    :   ASME Inlined - Darstellung nach ASME Y14.5M, der Text steht horizontal, in einem Ausbruch innerhalb der Maßlinie oder des Bogens eingefügt.

    :   ASME Referencing - Darstellung nach ASME Y14.5M, der Text steht horizontal, mittig am Ende einer Bezugslinie.



## Skripten

Siehe auch: [Autogenerierte API-Dokumentation](https://freecad.github.io/SourceDoc/) und [Grundlagen der Skripterstellung in FreeCAD](FreeCAD_Scripting_Basics/de.md).

Das Werkzeug Längenmaß kann in [Makros](Macros/de.md) und von der [Python](Python/de.md)-Konsole aus mit den folgenden Funktionen verwendet werden:


```python
dim1 = FreeCAD.ActiveDocument.addObject("TechDraw::DrawViewDimension", "Dimension")
dim1.Type = "Distance"
dim1.References2D=[(view1, "Edge1")]
page.addView(dim1)
```





{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw LengthDimension/de
