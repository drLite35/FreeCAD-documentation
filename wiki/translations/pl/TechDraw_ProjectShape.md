---
 GuiCommand:
   Name: TechDraw ProjectShape
   Name/pl: Rysunek Techniczny: Rzutowanie kształtów
   MenuLocation: Rysunek Techniczny , Widoki , Rzutowanie kształtów ...
   Workbenches: TechDraw_Workbench/pl
   Shortcut: 
   Version: 0.20
   SeeAlso: Draft_Shape2DView/pl
---

# TechDraw ProjectShape/pl



## Opis

Narzędzie **Rzutowanie kształtów** tworzy rzuty kształtów. Rzuty tworzone są w oknie [widoku 3D](3D_view/pl.md), a nie na [stronie rysunku technicznego](TechDraw_PageDefault/pl.md).

![](images/ProjectShape1_it.png )



## Użycie

1.  Opcjonalnie obróć [3D view](3D_view/pl.md). Obiekty będą rzutowane na płaszczyznę równoległą do ekranu, tj. wzdłuż kierunku kamery widoku 3D, który jest używany jako domyślna właściwość **kierunek**.
2.  Wybierz jeden lub więcej obiektów. Dla każdego obiektu zostanie utworzona osobny rzut.
3.  Istnieje kilka sposobów na wywołanie narzędzia:
    -   Naciśnij przycisk **<img src="images/TechDraw_ProjectShape.svg" width=16px> '''Rzutowanie kształtów ...'''**.
    -   Wybierz z menu opcję **Rysunek Techniczny → Widoki → <img src="images/TechDraw_ProjectShape.svg" width=16px> Rzutowanie kształtów ...**.
4.  Otwiera się panel zadań **Rzutowanie kształtów**. Zobacz też sekcję [właściwości](#Właściwości.md).
5.  Ustawić żądane opcje.
6.  Wybrane opcje nie powinny skutkować pustym rzutem, ponieważ spowodują błąd. Na przykład dla obiektu posiadającego tylko ostre krawędzie, takiego jak [prostopadłościan](Part_Box/pl.md), należy zaznaczyć opcję **Widoczne ostre krawędzie** i/lub **Ukryte ostre krawędzie**.
7.  Naciśnij przycisk **OK**.
8.  Rzut zostaje umieszczony na płaszczyźnie XY.
9.  Opcjonalnie zmień właściwość rzutu **Umiejscowienie** i / lub **Kierunek**.



## Właściwości

Obiekt **Rzutowanie kształtów** wywodzi się z obiektu [Część: Cecha](Part_Feature/pl.md) i dziedziczy wszystkie jego właściwości. Posiada on również następujące dodatkowe właściwości:



### Dane


{{TitleProperty|Rzutowanie}}

-    **Źródło|Link**: Kształt, który ma być rzutowany.

-    **Kierunek|Vector**: Kierunek rzutowania. Jest to wektor normalny płaszczyzny projekcji.

-    **VCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, to widoczne ostre krawędzie są pokazywane. Przykład: wszystkie krawędzie [prostopadłościanu](Part_Box/pl.md).

-    **Rg1 Line VCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, widoczne gładkie krawędzie są pokazywane. Przykład: krawędzie między zaokrągleniem a sąsiednimi ścianami.

-    **Rg NLine VCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, pokazane są widoczne krawędzie szyte. Przykład: szew ściany cylindrycznej 360°.

-    **Out Line VCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, pokazywane są widoczne krawędzie konturowe *(które nie są ostre)*. Przykład: widok boczny [walca](Part_Cylinder.md) ma dwie takie krawędzie.

-    **Iso Line VCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, widoczne izoparametry są wyświetlane. Obecnie nie działa.

-    **HCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, pokazywane są ukryte ostre krawędzie.

-    **Rg1 Line HCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, pokazane są ukryte gładkie krawędzie.

-    **Rg NLine HCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, pokazane są ukryte krawędzie szyte.

-    **Out Line HCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, pokazywane są ukryte krawędzie konturowe.

-    **Iso Line HCompound|Bool**: Jeśli opcja ma wartość {{TRUE/pl}}, pokazywane są ukryte izoparametry. Obecnie nie działa.





{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw ProjectShape/pl
