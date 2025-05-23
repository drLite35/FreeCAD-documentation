---
 GuiCommand:
   Name: CAM Job
   Name/de: CAM Auftrag
   MenuLocation: CAM , Auftrag
   Workbenches: CAM_Workbench/de
   Shortcut: **P** **J**
---

# CAM Job/de



## Beschreibung

Das Werkzeug <img alt="" src=images/CAM_Job.svg  style="width:16px;"> [CAM Auftrag](CAM_Job/de.md) erstellt ein neuen Auftrag (Job-Objekt) im aktiven Dokument; er enthält die folgenden Informationen:

1.  Eine Liste mit Definitionen zur Werkzeugsteuerung, in der die Geometrie, Vorschübe und Geschwindigkeiten für die Pfadbearbeitungswerkzeuge angegeben sind.
2.  Eine schrittweise Arbeitsablaufliste von Pfadoperationen.
3.  Ein Basiskörper - ein Klon, der für den Versatz verwendet wird.
4.  Ein Schaft, der das Rohmaterial darstellt, das im Arbeitsbereich CAM gefräst wird.
5.  Ein Einrichtungsdatenblatt, das die von den Pfadoperationen verwendeten Eingaben, einschließlich statischer Werte und Formeln, enthält.
6.  Konfigurationsparameter, die den Zielpfad des ausgegebenen G-Code Auftrags, den Dateinamen und die Dateierweiterung sowie den [Postprozessor](CAM_Post/de.md) angeben (der zur Erzeugung des entsprechenden Dialekts für die Ziel-CNC-Steuerung und zur Anpassung von Einheiten, Werkzeugänderungen, Parken usw. verwendet wird).



## Anwendung

1.  Es gibt mehrere Möglichkeiten, den Befehl aufzurufen
    -   Die Schaltfläche **<img src="images/CAM_Job.svg" width=16px> [Auftrag](CAM_Job/de.md)** drücken.
    -   Den Menüeintrag **CAM → <img src="images/CAM_Job.svg" width=16px> Auftrag** auswählen.
    -   Das Tastaturkürzel **P** dann **J**.

Der GUI-Dialog Auftrag bearbeiten hat fünf horizontal ausgerichtete Reiter: **Allgemein**, **Ausgabe**, **Einrichtung**, **Werkzeuge**, und **Arbeitsplan**. Der Benutzer kann jederzeit die Optionen **OK** oder **Abbrechen** innerhalb des Dialogs verwenden.



## Allgemein

![](images/Job_1.jpg )

-   **Bezeichnung**: Der Name des Auftragsobjekts wie er in der Baumansicht angezeigt wird.
-   **Modell**: Das Basisobjekt, das durch seine Form die Pfade des Jobs definiert. Wenn es sich um ein PartDesign-Objekt handelt, ist es normalerweise der Body, den Du hier auswählst. Wenn du ein Element in der Baumstruktur *vorher* ausgewählt hast, klicke auf das Symbol \"Auftrag hinzufügen\", das Element ist hier bereits eingetragen. Du kannst es ändern, indem du ein anderes Element aus dem Ausklappmenü auswählst.
-   **Beschreibung**: Du kannst hier einige Notizen zu dem Auftrag hinzufügen. Die Notizen dienen nur zu deiner Information und haben keine Auswirkung auf den Pfad.



## Ausgabe

![](images/Job_2.jpg )

-   **Ausgabedatei**: Lege den Namen, die Erweiterung und den Dateipfad der G-Code-Ausgabe fest. Du kannst die folgenden Platzhalter verwenden:
    -   **%D** Verzeichnis des aktiven Dokuments
    -   **%d** Name des aktiven Dokuments (ohne Erweiterung)
    -   **%M** Makro-Verzeichnis des Benutzers
    -   **%j** Name des Auftrags

-   **Prozessor**: Wähle den [Postprozessor](CAM_Post/de.md) für deine Maschine aus.
-   **Argumente**: Füge bei Bedarf Argumente für den [Postprozessor](CAM_Post/de.md) hinzu.



## Einrichtung

![](images/Job_3.jpg )

-   **Bestand**: Lege die Größe und Form des Rohmaterials fest.
-   **Orientierung**: Ausgewählte Kante oder Fläche wird verwendet, um die Basis oder den Schaft entsprechend zu orientieren.
-   **Ausrichtung**: Wähle einen Knotenpunkt aus, um den Ursprung festzulegen oder die Basis oder das Lager zu verschieben.



## Werkzeuge

![](images/Job_4.jpg )

Füge das/die Werkzeug(e) aus deiner [Werkzeugtabelle](CAM_ToolLibraryEdit/de.md) hinzu, welche du für die Arbeitsgänge bei diesem Auftrag benötigst.

Nachdem ein Werkzeug hinzugefügt wurde, kannst du den Vorschub und die Spindeldrehzahl einstellen/ändern, wenn du bei diesem Auftrag einen anderen Vorschub benötigst. Eine Änderung hier ändert nicht die in der Werkzeugtabelle gespeicherten Parameter.

Das Standardwerkzeug kannst du löschen, wenn du ein eigenes Werkzeug hinzugefügt hast.



## Arbeitsplan

![](images/Job_5.jpg )

Wenn du einen Auftrag hast, der mehr als eine Pfadoperation umfasst, kannst du festlegen, in welcher Reihenfolge die Arbeitsgänge ausgeführt werden sollen. Um die Reihenfolge zu ändern, wähle einen Vorgang aus und drücke die Auf- oder Abwärtstaste.





{{CAM_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [CAM](CAM_Workbench.md) > CAM Job/de
