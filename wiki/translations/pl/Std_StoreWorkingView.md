---
 GuiCommand:
   Name: Std StoreWorkingView
   Name/pl: Std: Zachowaj widok
   MenuLocation: Widok , Widoki standardowe , Przechowaj widok roboczy
   Workbenches: wszystkie
   Shortcut: **Shift** + **End**
   Version: 0.21
   SeeAlso: Std_RecallWorkingView/pl, Std_FreezeViews/pl
---

# Std StoreWorkingView/pl



## Opis

Polecenie **Przechowaj widok roboczy** zapisuje ustawienia ujęcia widoku aktywnego okna [widoku 3D](3D_view/pl.md) w tymczasowym widoku roboczym. Widok ten można przywołać za pomocą polecenia [Odtwórz widok](Std_RecallWorkingView/pl.md).

Każdy widok 3D ma swój własny widok roboczy. Zapisanie nowego widoku roboczego spowoduje zastąpienie istniejącego widoku roboczego aktywnego okna widoku 3D. Po zamknięciu widoku 3D jego widok roboczy zostaje utracony.



## Użycie

1.  Upewnij się, że okno [widoku 3D](3D_view/pl.md) jest aktywne.
2.  Polecenie można wywołać na kilka sposobów:
    -   Wybierz z menu opcję **Widok → Widoki standardowe → Przechowaj widok roboczy**.
    -   Użyj skrótu klawiaturowego: **Shift** + **End**.



## Tworzenie skryptów 

Zobacz również stronę: [Dokumentacja API generowana automatycznie](https://freecad.github.io/SourceDoc/) oraz [Podstawy pisania skryptów dla FreeCAD](FreeCAD_Scripting_Basics/pl.md).

Zapisywanie bieżących ustawień ujęcia widoku aktywnego okna widoku 3D w widoku roboczym:


```python
import FreeCADGui

FreeCADGui.runCommand("Std_StoreWorkingView", 0)
```



---
⏵ [documentation index](../README.md) > Std StoreWorkingView/pl
