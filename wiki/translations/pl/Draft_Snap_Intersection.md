---
 GuiCommand:
   Name: Draft Snap Intersection
   Name/pl: Rysunek Roboczy: Przyciągnij do punktu przecięcia
   MenuLocation: Przyciąganie , Przyciągnij do punktu przecięcia
   Workbenches: Draft_Workbench/pl, BIM_Workbench/pl
   SeeAlso: Draft_Snap/pl, Draft_Snap_Lock/pl
---

# Draft Snap Intersection/pl



## Opis

Polecenie <img alt="" src=images/Draft_Snap_Intersection.svg  style="width:24px;"> **Przyciągnij do punktu przecięcia** przyciąga do punktu przecięcia dwóch krawędzi. Krawędzie mogą należeć do obiektów środowiska [Rysunek Roboczy](Draft_Workbench/pl.md) lub [BIM](BIM_Workbench/pl.md), ale także do obiektów utworzonych za pomocą innych [środowisk pracy](Workbenches/pl.md).

Ta opcja przyciągania znajdzie również przecięcia (przedłużonych) prostych krawędzi, jeśli <img alt="" src=images/Draft_Snap_WorkingPlane.svg  style="width:16px;"> [przyciąganie do płaszczyzny roboczej](Draft_Snap_WorkingPlane/pl.md) jest również aktywne.

![](images/Draft_Snap_Intersection_example.png ) 
*Przyciąganie drugiego punktu linii do przecięcia dwóch krawędzi.*



## Użycie

Ogólne informacje na temat przyciągania można znaleźć na stronie [Przyciąganie](Draft_Snap/pl.md).

1.  Upewnij się, że przyciąganie jest włączone. Więcej informacji na ten temat znajduje się na stronie <img alt="" src=images/Draft_Snap_Lock.svg  style="width:16px;"> [Przełącz przyciąganie](Draft_Snap_Lock/pl.md).
2.  Jeśli opcja **przyciąganie do punktu przecięcia** nie jest aktywna, wykonaj jedną z poniższych czynności:
    -   Naciśnij przycisk **<img src="images/Draft_Snap_Intersection.svg" width=16px> [Przyciągnij do punktu przecięcia](Draft_Snap_Intersection/pl.md)** na pasku narzędzi przyciągania.
    -   [Środowisko pracy Rysunek Roboczy](Draft_Workbench/pl.md): Przytrzymaj przycisk **<img src="images/Draft_Snap_Lock.svg" width=x16px><img src="images/Toolbar_flyout_arrow.svg" width=x16px>
** na pasku [widżetu przyciągania](Draft_snap_widget/pl.md) i w otwartym menu wybierz opcję **<img src="images/Draft_Snap_Intersection.svg" width=16px> Przyciągnij do punktu przecięcia**
    -   [Środowisko pracy BIM](BIM_Workbench/pl.md): Wybierz opcję **Przyciąganie → <img src="images/Draft_Snap_Intersection.svg" width=16px> Przyciągnij do punktu przecięcia** z menu lub z menu kontekstowego [widoku 3D](3D_view/pl.md).
3.  Wybierz polecenie środowiska pracy Rysunek Roboczy lub BIM, aby utworzyć geometrię.
4.  Pamiętaj, że możesz również zmienić opcje przyciągania, gdy polecenie jest aktywne.
5.  Przesuń kursor nad okrągłą krawędź.
6.  Krawędź zostanie podświetlona.
7.  Jeśli zostanie znaleziony punkt główny, zostanie on zaznaczony, a ikona <img alt="" src=images/Draft_Snap_Intersection.svg  style="width:16px;"> zostanie wyświetlona w pobliżu kursora.
8.  Opcjonalnie przesuń kursor bliżej innego punktu odniesienia, aby wybrać ten punkt.
9.  Kliknij, aby potwierdzić punkt.



## Ustawienia

Zobacz stronę [Przyciąganie](Draft_Snap/pl#Ustawienia.md) aby uzyskać więcej informacji.



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft Snap Intersection/pl
