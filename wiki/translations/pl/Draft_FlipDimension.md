---
 GuiCommand:
   Name: Draft FlipDimension
   Name/pl: Rysunek Roboczy: Odwróć wymiar
   MenuLocation: Modyfikacja , Odwróć wymiar
   Workbenches: Draft_Workbench/pl
---

# Draft FlipDimension/pl



## Opis

Narzędzie <img alt="" src=images/Draft_FlipDimension.svg  style="width:24px;"> **Odwróć wymiar** przerzuca tekst [wymiaru](Draft_Dimension/pl.md) wokół linii wymiarowej o 180°. Można go użyć do korekty wymiarów, których tekst ukazuje się w lustrzanym odbiciu. Polecenie nie działa poprawnie dla wymiarów kątowych.



## Użycie

1.  Wybierz jeden lub więcej [wymiarów](Draft_Dimension/pl.md).
2.  Istnieje kilka sposobów, aby wywołać to polecenie:
    -   Naciśnij przycisk **<img src="images/Draft_FlipDimension.svg" width=24px> '''Odwróć wymiar'''**.
    -   Wybierz z menu opcję **Modyfikacja → <img src="images/Draft_FlipDimension.svg" width=24px> Odwróć wymiar**.



## Uwagi

[Tekst wymiarów](Draft_Dimension/pl.md) posiada również właściwość **Odwróć Tekst** która, gdy ma wartość {{TRUE/pl}}, obraca tekst o 180 stopni względem normalnego kierunku. Można to połączyć z działaniem tej komendy.



## Tworzenie skryptów 

Zobacz również stronę: [Dokumentacja API generowana automatycznie](https://freecad.github.io/SourceDoc/) oraz [Podstawy tworzenia skryptów FreeCAD](FreeCAD_Scripting_Basics/pl.md).

Aby odwrócić [wymiar](Draft_Dimension/pl.md) należy zmienić jego właściwość `Normal`.

Przykład:


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

p1 = App.Vector(0, 0, 0)
p2 = App.Vector(1000, 0, 0)
p3 = App.Vector(500, 300, 0)
dimension = Draft.make_dimension(p1, p2, p3)
dimension.ViewObject.FontSize = 200

dimension.Normal = dimension.Normal.negative()
doc.recompute()
```



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft FlipDimension/pl
