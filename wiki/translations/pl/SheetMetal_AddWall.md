---
 GuiCommand:
   Name: SheetMetal AddWall
   Name/pl: Arkusz Blachy: Utwórz ściankę
   MenuLocation: SheetMetal , Utwórz ściankę
   Workbenches: SheetMetal_Workbench/pl
   Shortcut: **W**
---

# SheetMetal AddWall/pl



## Opis

Polecenie <img alt="" src=images/SheetMetal_AddWall.svg  style="width:24px;"> **Utwórz ścianę** tworzy obrzeża na wybranych krawędziach płyty bazowej. Poprzez zmianę właściwości **kąt** obrzeża można je przekształcić w półokrągłości.

**Obrzeże** składa się z zagięcia walcowego 90° i płaskiej listwy *(ścianki)*.

<img alt="" src=images/SheetMetal_AddWall-12.png  style="width:200px;"> <img alt="" src=images/Button_right.svg  style="width:16px;"> <img alt="" src=images/SheetMetal_AddWall-13.png  style="width:200px;"> 
*Dwie wybrane krawędzie → dwa obrzeża.*

Zresetowanie właściwości **kąt** do około 180° w drugim kroku spowoduje utworzenie *obszycia*.

<img alt="" src=images/SheetMetal_AddWall-14.png  style="width:200px;"> <img alt="" src=images/Button_right.svg  style="width:16px;"> <img alt="" src=images/SheetMetal_AddWall-15.png  style="width:200px;"> 
*Dwie wybrane krawędzie → dwa obszycia.*



## Użycie

1.  Wybierz jedną lub więcej krawędzi elementu bazowego.
2.  Jest kilka sposobów na wywołanie tego polecenia:
    -   Wciśnij przycisk **<img src="images/SheetMetal_AddWall.svg" width=16px> '''Utwórz ściankę'''**.
    -   Wybierz opcję **Sheet Metal → <img src="images/SheetMetal_AddWall.svg" width=16px> Utwórz ściankę** z menu.
    -   Kliknij prawym przyciskiem myszy w [widoku drzewa](Tree_view/pl.md) lub [widoku 3D](3D_view/pl.md) i wybierz opcję **Sheet Metal → <img src="images/SheetMetal_AddWall.svg" width=16px> Utwórz ścianę** z menu kontekstowego.
    -   Użyj skrótu klawiszowego: **W**.
3.  Otwarty zostanie [panel zadań](Task_panel/pl.md) **Flange Parameters** (wprowadzony w wersji 0.5.00).
4.  Opcjonalnie wciśnij przycisk **Wybierz** aby dodać więcej krawędzi.
    -   Wciśnij przycisk **Podgląd** aby zakończyć wybór i wyświetlić zmiany.
5.  Opcjonalnie dostosuj parametry w panelu zadań.
6.  Wciśnij przycisk **OK** aby zakończyć polecenie i zamknąć panel zadań.
7.  Utworzony zostanie obiekt **Bend** składający się z nowego kołnierza na każdej wskazanej krawędzi.
8.  Opcjonalnie dostosuj parametry w [Edytorze właściwości](Property_editor/pl.md).



## Uwagi

Do stworzenia płyty bazowej użyj zamkniętego konturu 2D - najlepiej użyj narzędzia <img alt="" src=images/Sketcher_NewSketch.svg  style="width:16px;"> [Utwórz szikc](Sketcher_NewSketch/pl.md) - i kolejnie <img alt="" src=images/SheetMetal_AddBase.svg  style="width:16px;"> [Utrzurz element bazowy](SheetMetal_AddBase/pl.md).

Alternatywnie płytę bazową (pustą) można utworzyć za pomocą poleceń środowisk pracy <img alt="" src=images/Workbench_Part.svg  style="width:16px;"> [Część](Part_Workbench/pl.md) lub <img alt="" src=images/Workbench_PartDesign.svg  style="width:16px;"> [Projekt Części](PartDesign_Workbench/pl.md).

Aby utworzyć półfabrykat za pomocą środowiska pracy [Część](Part_Workbench/pl.md):

1.  Utwórz bryłę za pomocą:
    -   <img alt="" src=images/Part_Box.svg  style="width:16px;"> [Sześcian](Part_Box/pl.md).
    -   <img alt="" src=images/Part_Extrude.svg  style="width:16px;"> [Wyciągnięcie \...](Part_Extrude/pl.md) z:
        -   <img alt="" src=images/Draft_Rectangle.svg  style="width:16px;"> [Prostokąta](Draft_Rectangle/pl.md) środowiska Rysunek Roboczy.
        -   <img alt="" src=images/Draft_Wire.svg  style="width:16px;"> [Polilinia](Draft_Wire/pl.md) środowiska Rysunek Roboczy.
        -   <img alt="" src=images/Sketcher_NewSketch.svg  style="width:16px;"> [Utwórz szkic](Sketcher_NewSketch/pl.md) środowiska Szkicownik.
2.  Upewnij się, że jeden z wymiarów pudełka lub odległość wytłaczania jest równa grubości blachy.

Aby utworzyć półfabrykat za pomocą środowiska [Projekt Części](PartDesign_Workbench/pl.md):

1.  Utwórz bryłę używając
    -   <img alt="" src=images/PartDesign_AdditiveBox.svg  style="width:16px;"> [Addytywny prostopadłościan](PartDesign_AdditiveBox.md).
    -   <img alt="" src=images/PartDesign_Pad.svg  style="width:16px;"> [Wyciągnięcia](PartDesign_Pad/pl.md) ze <img alt="" src=images/Sketcher_NewSketch.svg  style="width:16px;"> [szkicu](Sketcher_NewSketch/pl.md).
2.  Upewnij się, że jeden z wymiarów prostopadłościanu lub właściwości **Długość** wyciągnięcia jest równy grubości blachy.

Jeśli zaczniesz od utworzenia <img alt="" src=images/PartDesign_Body.svg  style="width:16px;"> [Zawartości](PartDesign_Body/pl.md), możesz mieszać cechy środowiska Arkusz Blachy z cechami środowiska Projekt Części, takimi jak <img alt="" src=images/PartDesign_Pocket.svg  style="width:16px;"> [kieszeń](PartDesign_Pocket/pl.md) lub <img alt="" src=images/PartDesign_Hole.svg  style="width:16px;"> [otwór](PartDesign_Hole/pl.md).



## Właściwości

Zapoznaj się również z informacjami na stronie: [Edytor właściwości](Property_editor/pl.md).

Obiekt Zagięcie środowiska Arkusz Blachy wywodzi się z obiektu [Część: Cecha](Part_Feature/pl.md) lub, jeśli jest w obrębie [Zawartości środowiska Projekt Części](PartDesign_Body/pl.md), z obiektu [Cechy tego środowiska](PartDesign_Feature/pl.md) i dziedziczy wszystkie jego właściwości. Posiada on również następujące dodatkowe właściwości:



### Dane


{{Properties_Title|Parametry}}

-    **Typ gięcia|Enumeration**: \"Typ gięcia\". {{value|Materiał na zewnątrz}} *(domyślnie)*, {{value|Materiał do wewnątrz}}, {{value|Grubość na zewnątrz}}, {{value|Odsunięcie}}.

-    **Specyfikacja długości|Enumeration**: \"Specyfikacja typu długości\". {{value|Leg}} *(domyślnie)*, {{value|Zewnętrzny ostry}}, {{value|Wewnętrzny ostry}}, {{value|Styczny}}. {{Version/pl|0.21}}

-    **Kąt|Angle**: \"Kąt gięcia\". Domyślny kąt: {{value|90,00°}}.

-    **Obiekt bazowy|LinkSub**: \"Obiekt bazowy\". Łącze do płaskiej powierzchni, która ma zostać wygięta.

-    **extend1|Distance**: \"Przedłużenie z lewej strony\". Domyślnie: {{value|0,00 mm}}.

-    **extend2|Distance**: \"Przedłużenie z prawej strony\". Domyślnie: {{value|0,00 mm}}.

-    **Szczelina1|Distance**: \"Szczelina z lewej strony\". Wartość domyślna: {{value|0,00 mm}}.

-    **Szczelina2|Distance**: \"Szczelina z prawej strony\". Wartość domyślna: {{value|0,00 mm}}.

-    **odwróć|Bool**: \"Odwrócony kierunek zagięcia\". Wartość domyślna: {{FALSE/pl}}.

-    **Długość|Length**: \"Długość ściany\". Wartość domyślna: {{value|10,00 mm}}.

-    **Promień|Length**: \"Promień zgięcia\", domyślna wartość zależy od właściwości promienia cechy nadrzędnej:

    -   Ta właściwość nie istnieje: Ta właściwość jest ustawiona na {{value|1,00 mm}}.
    -   Ta właściwość zawiera wartość numeryczną: Wyrażenie wiążące tą właściwość jest wstawiane do ten właściwości.
    -   Ta właściwość zawiera wyrażenie: Wyrażenie jest kopiowane do tej właściwości.


{{Properties_Title|Parametry Ex}}

-    **Automatyczne ścięcie|Bool**: \"Włącz automatyczne ukosowanie\". Domyślnie: {{TRUE/pl}}.

-    **Współczynnik K|FloatConstraint**: \"Położenie linii neutralnej. Uwaga: Korzystanie ze standardów ANSI, nie DIN.\".  Domyślnie: {{value|0,50}}. Współczynnik K *(znany również jako współczynnik neutralny)* dla zgięcia. Używany do obliczania naddatku na zginanie podczas rozkładania.

-    **max Odległość wysuwu|Length**: \"Maksymalny wysuw przy automatycznym ścinaniu\". Domyślnie: {{value|5,00 mm}}.

-    **min Szczelina|Length**: \"Minimalna szczelina przy automatycznym ścinaniu\". Domyślnie: {{value|0,20 mm}}.

-    **min Szczelina podcięcia|Length**: \"Minimalna szczelina do podcięcia\". Domyślnie: {{value|1,00 mm}}.

-    **Odsunięcie|Distance**: \"Odsunięcie zagięcie\". Domyślnie: {{value|0,00 mm}}.

-    **Rozwiń|Bool**: \"Pokazuje widok rozwinięcia bieżącego zagięcia\". Domyślnie:  wartość {{TRUE/pl}} powoduje rozwinięcie zagięcia.


{{Properties_Title|Parametry Ex2}}

-    **Szkic|Link**: \"Obiekt Szkicu\".

-    **ObróćSzkic|Bool**: \"Odwróć kierunek szkicu\". Wartość domyślna: {{FALSE/pl}}.

-    **OdwróćSzkic|Bool**: \"Odwróć początek szkicu\". Wartość domyślna: {{FALSE/pl}}.


{{Properties_Title|Parametry Ex3}}

-    **Lista długości|FloatList**: \"Lista długości ścian\". Wartość domyślna: {{value|[10.00]}}.

-    **Lista A zgięć|FloatList**: \"Lista kątów gięcia\". Wartość domyślna: {{value|[90.00]}}.


{{Properties_Title|Parametery kąta zagięcia}}

-    **Kąt zagięcia 1|Angle**: \"Kąt zagięcia z lewej strony\". Domyślny kąt: {{value|0,00°}}.

-    **Kąt zagięcia 2|Angle**: \"Kąt zagięcia z prawej strony\". Domyślny kąt: {{value|0,00°}}.


{{Properties_Title|Parametry perforacji}}

-    **Nonperforation Max Length|Length**: \"Maksymalna długość bez perforacji\". Domyślnie: {{value|5 mm}}.

-    **Perforate|Bool**: \"Włącz perforacje\". Domyślnie: {{FALSE/pl}}.

-    **Perforation Angle|Angle**: \"Kąt perforacji\". Domyślnie: {{value|0 °}}.

-    **Perforation initial Length|Length**: \"Początkowa długość perforacji\". Domyślnie: {{value|5 mm}}.

-    **Perforation Max Length|Length**: \"Maksymalna długość perforacji\". Domyślnie: {{value|5 mm}}.


{{Properties_Title|Parametry reliefu}}

-    **Współczynnik podcięcia|Float**: \"Współczynnik podcięcia\". Wartość domyślna: {{value|0,70}}.

-    **Zastosuj współczynnik poecięcia|Bool**: \"Zastosuj współczynnik podcięcia\". Wartość domyślna: {{FALSE/pl}}.

-    **Typ podcięcia|Enumeration**: \"Typ podcięcia\". {{value|Prostokątne}} *(domyślnie)*, {{value|Zaokrąglone}}. Włączone tylko wtedy, gdy ustawiona jest wartość szczeliny.

-    **PodcięcieD|Length**: \"Głębokość podcięcia\". Domyślnie: {{value|1,00 mm}}. Włączone tylko po ustawieniu wartości szczeliny.

-    **PodcięcieW|Length**: \"Szerokość podcięcia\". Wartość domyślna: {{value|0,80 mm}}. Włączone tylko po ustawieniu wartości szczeliny.



## Przykład

<img alt="" src=images/SheetMetal_AddWall-01.png  style="width:300px;"> 
*Zwykła taca*


<div class="mw-collapsible mw-collapsed">


<div class="mw-collapsible-content">



### Przygotowania

Ta taca jest wykonana z prostokątnego półfabrykatu ze ściankami dodanymi do jego krawędzi. W związku z tym należy wcześniej przygotować jeden szkic konturu półfabrykatu.

<img alt="" src=images/SheetMetal_AddWall-02.png  style="width:200px;"> 
*Tylko prostokątny kontur*



### Przepływ pracy 

1.  Utwórz pusty dokument.
    1.  Wybierz szkic konturu.  <img alt="" src=images/SheetMetal_AddWall-03.png  style="width:240px;">
    2.  Naciśnij przycisk **<img src="images/SheetMetal_AddBase.svg" width=16px> [Utwórz element bazowy](SheetMetal_AddBase/pl.md)**.
        lub użyj skrótu klawiaturowego: **C** + **F**.
        <img alt="" src=images/SheetMetal_AddWall-04.png  style="width:240px;">  
*(Materiał zostanie wyciągnięty w kierunku osi Z)*
2.  Dodaj ściany do krawędzi konturu.
    1.  Wybierz krawędzie obrysu półfabrykatu.
        <img alt="" src=images/SheetMetal_AddWall-05.png  style="width:240px;">.
    2.  Naciśnij przycisk **<img src="images/SheetMetal_AddWall.svg" width=16px> [Utwórz siankę](SheetMetal_AddWall/pl.md)**,
        lub użyj skrótu klawiaturowego: **W**.
        <img alt="" src=images/SheetMetal_AddWall-06.png  style="width:240px;">
    3.  Jeśli zagięcie jest o 90° w dół, ustaw wartość właściwości **Odwróć** na {{true/pl}}, aby odwrócić kierunek *(i **długość** na niższą wartość w przypadku mniejszych ścian)*.
        <img alt="" src=images/SheetMetal_AddWall-01.png  style="width:240px;">
3.  Dodaj więcej ścian.
    1.  Wybierz **górne zewnętrzne krawędzie** tacy.
        <img alt="" src=images/SheetMetal_AddWall-08.png  style="width:240px;">
    2.  Naciśnij przycisk **<img src="images/SheetMetal_AddWall.svg" width=16px> [Utwórz ściankę](SheetMetal_AddWall/pl.md)**,
        lub użyj skrótu klawiaturowego: **W**.
        <img alt="" src=images/SheetMetal_AddWall-09.png  style="width:240px;">
    3.  Ściany są trochę za długie *(ale ładnie przycięte)*, dlatego właściwość **długość** musi być ustawiona na niższą wartość.
        <img alt="" src=images/SheetMetal_AddWall-10.png  style="width:240px;">
    4.  Jeśli lubisz zagięcia odchylane na zewnątrz, ustaw wartość **Odwróć** na {{true/pl}}.
        <img alt="" src=images/SheetMetal_AddWall-11.png  style="width:240px;">

Gotowe!


</div>


</div>



---
⏵ [documentation index](../README.md) > [SheetMetal](Category_SheetMetal.md) > [Addons](Category_Addons.md) > [External Command Reference](Category_External%20Command%20Reference.md) > SheetMetal AddWall/pl
