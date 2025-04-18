---
 GuiCommand:
   Name: Std DependencyGraph
   Name/pl: Std: Graf zależności
   MenuLocation: Przybory , Graf zależności ...
   Workbenches: wszystkie
   SeeAlso: Std_ExportDependencyGraph/pl
---

# Std DependencyGraph/pl



## Opis

Polecenie **Graf zależności** wyświetla zależności pomiędzy obiektami w aktywnym dokumencie w postaci *wykresu zależności*. W przeciwieństwie do [Widoku drzewa](Tree_view/pl.md), obiekty są wymienione w odwrotnym porządku chronologicznym, z obiektem utworzonym jako pierwszy na dole.

Może on być przydatny przy analizie dokumentu FreeCAD i lokalizowaniu rozwidleń w drzewie. Układ grafu zależności zależy od tego, w którym środowisku pracy zostały utworzone obiekty w dokumencie. Na przykład model wykonany wyłącznie w środowisku [Projekt Części](PartDesign_Workbench/pl.md) może wyświetlać liniowy wykres zależności z jedną pionową gałęzią. Model wykonany za pomocą działań w środowisku [Część](Part_Workbench/pl.md) będzie miał wiele gałęzi, ale dla pojedynczej części połączą się one u góry po przeprowadzonych operacjach [logicznych](Part_Boolean/pl.md). Jeśli tak się nie stanie, oznacza to, że są to osobne obiekty.

Graf zależności jest wyłącznie narzędziem wizualizacji, dlatego nie można go edytować. Podlega automatycznej aktualizacji w przypadku wprowadzenia zmian w modelu.

<img alt="" src=images/Std_DependencyGraph_example.svg  style="width:400px;"> 
*Przykład grafu zależności z korpusem Projekt Części po lewej stronie i obiektem utworzonym za pomocą operacji środowiska Część po prawej stronie.*



## Instalacja

Aby można było korzystać z poleceń, należy zainstalować oprogramowanie innej firmy o nazwie [Graphviz](http://graphviz.org/). Jeśli nie masz go wstępnie zainstalowanego lub jest on zainstalowany w niekonwencjonalnej lokalizacji, FreeCAD wyświetli następujące okno dialogowe:

![](images/FreeCAD-0.17-missing-Graphviz-error-dialogue.png )

### Windows

Pobierz instalator **graphviz-2.xx** ze [Graphviz strona do pobrania](https://graphviz.org/download/#windows) i uruchom go, aby wykonać instalację. Niektóre starsze wersje wydają się mieć problemy z wyświetlaniem wykresu; wersja 2.38 i nowsze są znane z niezawodności. Wszystkie wydania graphviz można znaleźć w [serwisie Gitlab](https://gitlab.com/graphviz/graphviz/-/releases).



### Mac OS 

Grafviz można zainstalować za pomocą [Homebrew](https://brew.sh/) jeśli używasz macOS w wersji Big Sur *(11) (lub nowszy)*. *(Podczas instalacji Homebrew nie denerwuj się, jeśli MacOS poprosi Cię o zainstalowanie aktualizacji, np. dla narzędzi wiersza poleceń Xcode. Te aktualizacje są wykonywane później przez proces instalacji)*.


{{Code|lang=text|code=
brew install graphviz
}}

Wykona instalację binariów Graphviz w **/usr/local/bin** dla macOS na Intelu, lub **/opt/homebrew** dla macOS na Apple Silicon/ARM. FreeCAD powinien automatycznie znaleźć te lokalizacje. Jeśli program Graphviz nie zostanie znaleziony, zostaniesz poproszony o podanie ścieżki. Niestety nie możemy nawigować bezpośrednio do programu w oknie dialogowym pliku, który pojawia się z poziomu **Przybory → Graf zależności ...**. Istnieją dwie możliwości: Możesz użyć kombinacji klawiszy Cmd+Shift+. aby pokazać ukryte elementy. Lub możesz użyć kombinacji klawiszy Cmd+Shift+G, aby uzyskać pole wprowadzania ścieżki. Wprowadź jedną z tych ścieżek w [konsoli](https://en.wikipedia.org/wiki/Terminal_(macOS)):


{{Code|lang=text|code=
/usr/local/bin
}}

lub:


{{Code|lang=text|code=
/opt/homebrew/bin
}}

i zatwierdzić pole wejściowe oraz okno dialogowe wyboru pliku.

W przypadku, gdy binaria Graphviz są zainstalowane w niestandardowej lokalizacji, spróbuj znaleźć program za pomocą polecenia:


{{Code|lang=text|code=
type dot
}}

Wynikiem będzie coś takiego jak:


{{Code|lang=text|code=
dot is /usr/local/bin/dot
}}

I dlatego możesz powiedzieć programowi FreeCAD, aby szukał w tym katalogu.

Jeśli nie używasz macOS w wersji Big Sur *(11) (lub nowszego)* Homebrew może nie działać, ale możesz użyć [MacPorts](https://www.macports.org/index.php) zamiast tego. Wystarczy pobrać [odpowiednią wersję dla Twojego systemu operacyjnego](https://www.macports.org/install.php). Po zakończeniu instalacji wpisz to polecenie w [konsoli](https://en.wikipedia.org/wiki/Terminal_(macOS)):


{{Code|lang=text|code=
sudo port install graphviz
}}

Wpisz swoje hasło i poczekaj, aż instalacja dobiegnie końca *(z uwagi na zależności może to zająć trochę czasu)*.

Binaria Graphviz mogą znajdować się pod **/usr/local/bin** lub **/opt/local/bin/dot**. FreeCAD może automatycznie znaleźć program Graphviz za pomocą okna dialogowego plików, które pojawia się po wybraniu **Przybory → Graf zależności ...**, jeśli nie wprowadź to polecenie:


{{Code|lang=text|code=
type dot
}}

W rezultacie otrzymamy:


{{Code|lang=text|code=
dot is /opt/local/bin/dot
}}

I możesz wskazać programowi FreeCAD, aby przeszukał ten katalog, jak wyjaśniono wcześniej.

Możliwe jest również uczynienie katalogu *opt* dostępnym za pomocą tego polecenia:


{{Code|lang=text|code=
defaults write com.apple.finder AppleShowAllFiles YES;
}}

wtedy:


{{Code|lang=text|code=
killall Finder /System/Library/CoreServices/Finder.app;
}}

Dlatego możesz nakazać programowi FreeCAD, aby podążał tą ścieżką. Zostało to pomyślnie przetestowane na macOS 10.13 *(High Sierra)*.

### Linux

W większości dystrybucji Linuksa *(Debian / Ubuntu, Fedora, OpenSUSE)* wystarczy zainstalować pakiet graphviz z repozytoriów. Jednak podobnie jak w przypadku Mac / OSX, w przypadkach gdy binaria Graphviz są zainstalowane w niestandardowej lokalizacji, należy spróbować znaleźć program za pomocą polecenia:


{{Code|lang=text|code=
type dot
}}

Może to być coś w rodzaju


{{Code|lang=text|code=
dot is /usr/local/bin/dot
}}

I dlatego możesz wskazać programowi FreeCAD, aby szukał w tym katalogu.



## Użycie

1.  Wybierz z menu opcję **Przybory → <img src="images/Std_DependencyGraph.svg" width=16px> Graf zależności ...**.
2.  W [Głównym obszarze widoku](Main_view_area/pl.md) otworzy się nowa zakładka zatytułowana **Graf zależności**.
3.  Użyj kółka przewijania myszy, aby przybliżyć lub oddalić widok.
4.  Użyj suwaków na dole i po prawej stronie ekranu, aby przesunąć widok. Alternatywnie przytrzymaj lewy przycisk myszy i poruszaj kursorem.



## Zapis

Możesz zapisać wykres zależności:

1.  Upewnij się, że zakładka Graf zależności jest na pierwszym planie.
2.  Wybierz z menu opcję **Plik → [Zapisz](Std_Save/pl.md)** lub **Plik → [Zapisz jako](Std_SaveAs/pl.md)**.
3.  Wprowadź nazwę pliku i wybierz typ pliku (\*.gv, \*.png, \*.bmp, \*.gif, \*.jpg, \*.svg lub \*.pdf).
4.  Naciśnij przycisk **Zapisz**.



## Zasady ogólne 

-   Wykres przedstawia obiekty w odwrotnej kolejności chronologicznej.
-   Kierunek strzałek pokazujących zależności powinien być zawsze skierowany w dół. Strzałka skierowana w górę wskazuje na zależność cykliczną, czyli problem, który należy rozwiązać.
-   Szkic zawierający odnośniki do [zewnętrznej geometrii](Sketcher_External/pl.md) będzie miał liczbę z przyrostkiem \"x\" obok strzałki łączącej go z jego rodzicem, pokazującą liczbę zewnętrznych geometrii powiązanych w szkicu.
-   Obiekty mogą mieć zależności z wieloma rodzicami. Na przykład, dla modelu zbudowanego w środowisku [Projekt Części](PartDesign_Workbench/pl.md), kieszeń może być powiązana ze swoim szkicem i z elementem wyciągnięcia, który był przed nim.
-   Niedozwolone zależności *(np. między operacją środowiska pracy [Rysunek Roboczy](Draft_Workbench/pl.md)/[Część](Part_Workbench/pl.md) i elementem w obrębie Zawartości środowiska Projekt Części)* będą wyświetlone z czerwoną strzałką. Ten typ zależności zwykle pokazuje błąd \'Zależności wychodzą poza dozwolony zakres\' w [widoku raportu](Report_view/pl.md).
-   [Kontener Część](Std_Part/pl.md) i [Zawartość środowiska Projekt Części](PartDesign_Body/pl.md) zamykają swoją zawartość w ramce z tłem o przypadkowym kolorze. Ich początek również zamyka swoją zawartość (standardowe płaszczyzny i osie) w ramce.
-   [Grupa](Std_Group/pl.md) jest wyświetlana jako pojedynczy element połączony ze swoją zawartością.



---
⏵ [documentation index](../README.md) > [3rd_Party](Category_3rd_Party.md) > Std DependencyGraph/pl
