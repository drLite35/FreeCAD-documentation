---
 GuiCommand:
   Name: Draft Snap Special
   Name/de: Draft EinrastenSpezial
   MenuLocation: Einrasten , Einrasten spezial
   Workbenches: Draft_Workbench/de, BIM_Workbench/de
   Version: 0.17
   SeeAlso: Draft_Snap/de, Draft_Snap_Lock/de
---

# Draft Snap Special/de



## Beschreibung

Die Option <img alt="" src=images/Draft_Snap_Special.svg  style="width:24px;"> **Draft EinrastenSpezial** rastet auf, durch das Objekt festgelegten, [speziellen Punkten](#Supported_special_points.md) ein. Die unterstützten Objekte sind [Arch Wände](Arch_Wall/de.md), [Arch Strukturen](Arch_Structure.md) und [Arch Ausstattung](Arch_Equipment.md).

![](images/Draft_Snap_Special_example.png ) 
*Einrasten des zweiten Punktes einer Linie auf einen speziellen Punkt einer [Arch Wand](Arch_Wall/de.md), der ein Knoten ihres Basisobjekts ist*



## Anwendung

Für allgemeine Informationen zum Einrasten (Fangen) siehe [Draft Einrasten](Draft_Snap/de.md).

1.  Einrasten sollte aktiviert sein. Siehe <img alt="" src=images/Draft_Snap_Lock.svg  style="width:16px;"> [Draft EinrastenSperren](Draft_Snap_Lock/de.md).
2.  Ist **Draft EinrastenSpezial** nicht aktiv, gibt es folgende Möglichkeiten:
    -   Die Schaltfläche **<img src="images/Draft_Snap_Special.svg" width=16px> [Einrasten spezial](Draft_Snap_Special.md)** in der Symbolleiste Draft-Einrasten drücken.
    -   [Draft](Draft_Workbench/de.md): Die Schaltfläche **<img src="images/Draft_Snap_Lock.svg" width=x16px><img src="images/Toolbar_flyout_arrow.svg" width=x16px>** im [Draft-Widget Einrasten](Draft_snap_widget/de.md) gedrückt halten und im Ausklappmenü die Option **<img src="images/Draft_Snap_Special.svg" width=16px> Einrasten spezial** auswählen.
    -   [BIM](BIM_Workbench.md): Den Menüeintrag **Einrasten → <img src="images/Draft_Snap_Special.svg" width=16px> Einrasten spezial** auswählen oder die Menüoption im Kontextmenü der [3D-Ansichr](3D_view/de.md) auswählen.
3.  Einen Draft- oder BIM-Befehl auswählen, um die Geometrie zu erstellen.
4.  Man beachte, dass die Einrast-Optionen auch dann geändert werden können, wenn ein Befehl aktiv ist.
5.  Den Mauszeiger über ein unterstütztes Objekt bewegen.
6.  Das Objekt wird hervorgehoben.
7.  Wurde ein spezieller Punkt ermittelt, wird der Punkt markiert und das Symbol <img alt="" src=images/Draft_Snap_Special.svg  style="width:16px;"> wird neben dem Mauszeiger angezeigt.
8.  Sind mehrere spezielle Punkte vorhanden: wahlweise den Mauszeiger näher an einen anderen speziellen Punkt heran bewegen.
9.  Klicken, um den Punkt zu bestätigen.



## Unterstützte spezielle Punkte 

-   Die Knoten des Objekts der {{PropertyData/de|Base}} von <img alt="" src=images/Arch_Wall.svg  style="width:16px;"> [Arch Wänden](Arch_Wall/de.md).
-   Der Punkt der {{PropertyData/de|Placement}} von <img alt="" src=images/Arch_Structure.svg  style="width:16px;"> [Arch Strukturen](Arch_Structure/de.md).
-   Die {{PropertyData/de|Snap Points}} von <img alt="" src=images/Arch_Equipment.svg  style="width:16px;"> [Arch Ausstattungen](Arch_Equipment/de.md).



## Einstellungen

Siehe [Draft-Einrasten](Draft_Snap/de#Einstellungen.md).



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft Snap Special/de
