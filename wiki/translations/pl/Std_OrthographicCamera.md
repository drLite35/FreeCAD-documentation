---
 GuiCommand:
   Name: Std OrthographicCamera
   Name/pl: Std: Widok ortogonalny
   MenuLocation: Widok , Widok ortogonalny
   Workbenches: wszystkie
   Shortcut: **V** , **O**
   SeeAlso: Std_PerspectiveCamera/pl
---

# Std OrthographicCamera/pl



## Opis

Polecenie **Widok ortogonalny** przełącza ujęcie widoku w aktywnym oknie [widoku 3D](3D_view/pl.md) w tryb widoku ortogonalnego. W tym trybie obiekty znajdujące się dalej od kamery nie wydają się mniejsze od tych, które znajdują się bliżej.

![](images/Std_OrthographicCamera_example.svg ) 
*Dwa sześciany o tych samych wymiarach w widoku ortogonalnym*



## Użycie

1.  Istnieje kilka sposobów wywołania tego polecenia:
    -   Wybierz z menu opcję **Widok → <img src="images/Std_OrthographicCamera.svg" width=16px> Widok ortogonalny**.
    -   Wybierz opcję **<img src="images/Std_OrthographicCamera.svg" width=16px> Widok ortogonalny** z menu mini kostki [nawigacyjnej](Navigation_Cube/pl.md).
    -   Użyj skrótu klawiaturowego: **V** kolejnie **O**.



## Ustawienia

Zobacz też: [Edytor preferencji](Preferences_Editor/pl.md).

-   Typ ujęcia widoku można zmienić w preferencjach: **Edycja → Preferencje ... → Wyświetlanie → Widok 3D → Typ projekcji**. Wybrany typ będzie używany dla wszystkich widoków 3D wszystkich otwartych dokumentów, a także dla nowych dokumentów.



## Tworzenie skryptów 

Zobacz również stronę: [Dokumentacja API generowana automatycznie](https://freecad.github.io/SourceDoc/) oraz [Podstawy pisania skryptów dla FreeCAD](FreeCAD_Scripting_Basics/pl.md).

Użyj metody `setCameraType` obiektu View aby zmienić widok na ortogonalny lub perspektywę.


```python
import FreeCADGui

view = FreeCADGui.ActiveDocument.ActiveView
view.setCameraType("Perspective")
view.setCameraType("Orthographic")
view.getCameraType()
```



---
⏵ [documentation index](../README.md) > Std OrthographicCamera/pl
