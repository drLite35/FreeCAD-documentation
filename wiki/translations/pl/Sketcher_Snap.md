---
 GuiCommand:
   Name: Sketcher Snap
   Name/pl: Szkicownik: Włącz / wyłącz przyciąganie
   Workbenches: Sketcher_Workbench/pl
   Version: 0.21
   SeeAlso: Sketcher_Grid
---

# Sketcher Snap/pl



## Opis

Narzędzie <img alt="" src=images/Sketcher_Snap.svg  style="width:16px;"> **Przyciąganie szkicownika** włącza przyciąganie we wszystkich szkicach. Poszczególne tryby przyciągania i ustawienia można zmieniać w powiązanym menu.

Przyciąganie działa tylko podczas tworzenia geometrii. Należy pamiętać, że przyciąganie jest tylko pomocą w rysowaniu, nie tworzy dodatkowych wiązań.



## Użycie

1.  Naciśnij przycisk **<img src="images/Sketcher_Snap.svg" width=16px> [Włącz / wyłącz przyciąganie](Sketcher_Snap/pl.md)** aby przełączyć przyciąganie.
2.  Opcjonalnie kliknij strzałkę w dół po prawej stronie przycisku, aby otworzyć menu. Ustawienia w tym menu można zmienić tylko wtedy, gdy przyciąganie jest włączone:
    ![](images/Sketcher_Snap_Menu.png )
    -   Jeżeli zaznaczone jest pole wyboru **Przyciągaj do siatki**, kursor będzie przyciągany do linii siatki i przecięć siatki. Przyciąganie ma miejsce, gdy odległość kursora od linii siatki wynosi 20% odstępu siatki lub mniej. Przyciąganie działa również, gdy siatka jest niewidoczna.

    -   Jeżeli zaznaczone jest pole wyboru **Przyciągaj do obiektów**, kursor będzie przyciągany do krawędzi geometrii oraz punktów środkowych linii i łuków.

    -   
        **Przyciągaj do kąta**
        
        określa kąt przyciągania kursora. Przyciąganie będzie następować przy wielokrotności tej wartości, począwszy od kierunku dodatniej osi X szkicu. Klawisz **Ctrl** musi być przytrzymany do wykonania tego przyciągania. Przyciąganie kątowe działa tylko podczas tworzenia określonej geometrii.



---
⏵ [documentation index](../README.md) > [Sketcher](Sketcher_Workbench.md) > Sketcher Snap/pl
