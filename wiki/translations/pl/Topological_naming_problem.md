# Topological naming problem/pl
## Wprowadzenie




Problem z **nazewnictwem topologicznym** w programie FreeCAD odnosi się do kwestii zmiany wewnętrznej nazwy kształtu po wykonaniu operacji modelowania *(wyciągnięcie, wycięcie, połączenie, fazka, zaokrąglenie, itp.)*. Spowoduje to, że inne właściwości parametryczne, które zależą od tego kształtu, zostaną uszkodzone lub niepoprawnie obliczone. Ten problem dotyczy wszystkich obiektów w programie FreeCAD, ale jest szczególnie zauważalny podczas budowania brył za pomocą środowiska pracy <img alt="" src=images/Workbench_PartDesign.svg  style="width:24px;"> [Projekt Części](PartDesign_Workbench/pl.md), oraz podczas wymiarowania tych brył za pomocą środowiska<img alt="" src=images/Workbench_TechDraw.svg  style="width:24px;"> [Rysunek Techniczny](TechDraw_Workbench/pl.md).

-   W środowisku pracy <img alt="" src=images/Workbench_PartDesign.svg  style="width:24px;"> [Projekt Części](PartDesign_Workbench/pl.md), jeśli element jest obsługiwany na powierzchni *(lub krawędzi lub wierzchołku)*, element może zostać uszkodzony, jeśli bazowa bryła zmieni rozmiar lub orientację, ponieważ oryginalna powierzchnia *(lub krawędź lub wierzchołek)* może zostać wewnętrznie przemianowana.
-   W przypadku środowiska <img alt="" src=images/Workbench_TechDraw.svg  style="width:24px;"> [Rysunek Techniczny](TechDraw_Workbench/pl.md), jeżeli wymiar mierzy długość rzutowanej krawędzi, wymiar może zostać uszkodzony, jeżeli model 3D zostanie zmodyfikowany, ponieważ wierzchołki mogą zostać przemianowane, zmieniając w ten sposób mierzoną krawędź.

Kwestia nazewnictwa topologicznego jest złożonym problemem w modelowaniu CAD, który wynika ze sposobu, w jaki wewnętrzne procedury programu FreeCAD obsługują aktualizacje kształtów geometrycznych utworzonych za pomocą [jądra OCCT](OpenCASCADE/pl.md). Ten problem nie występuje tylko we FreeCAD. Jest on ogólnie obecny w oprogramowaniu CAD, ale większość innych środowisk tego typu używa heurystyk do redukcji wpływu tego problemu na użytkowników.

Od wersji FreeCAD 0.19 trwają prace nad poprawą obsługi kształtów poprzez dodawanie heurystyk, które zmniejszają wpływ tego typu problemów. [Algorytm nazewnictwa](#Topological_naming_algorithm/pl.md) został zaprojektowany aby zredukować potrzebę ręcznych działań, czasem poprzez automatyczne naprawienie problemów, innym razem prezentując prawdopodobne rozwiązanie a w innych przypadkach chociaż jasno pokazując co spowodowało problem. Pierwsza stabilna wersja programu FreeCAD zawierająca ten nowy algorytm nazewnictwa to 1.0. Z czasem ten algorytm zostanie zastosowany do innych części programu i pojawi się więcej automatycznych i wspieranych napraw w kolejnych wersjach.

Problem nazewnictwa topologicznego najczęściej dotyka i dezorientuje nowych użytkowników programu FreeCAD. W środowisku Projekt Części użytkownik powinien stosować się do najlepszych praktyk omówionych na stronie [Edycja cech](Feature_editing/pl.md). Użycie obiektów [płaszczyzny](PartDesign_Plane/pl.md) oraz [lokalne układy współrzędnych](PartDesign_CoordinateSystem/pl.md) jest zalecane do tworzenia modeli, które nie są podatne na tego typu błędy topologiczne. W środowisku Rysunek Techniczny, użytkownik powinien dodawać wymiary tylko wtedy, gdy model 3D jest kompletny i nie będzie dalej modyfikowany.



## Przykład

1\. W środowisku <img alt="" src=images/Workbench_PartDesign.svg  style="width:24px;"> [Projekt Części](PartDesign_Workbench/pl.md), stwórz <img alt="" src=images/PartDesign_Body.svg  style="width:24px;"> [Zawartość](PartDesign_Body/pl.md), następnie użyj przycisku <img alt="" src=images/PartDesign_NewSketch.svg  style="width:24px;"> [Nowy szkic](PartDesign_NewSketch/pl.md) i wybierz płaszczyznę XY, aby narysować szkic bazowy. Kolejnie zrób <img alt="" src=images/PartDesign_Pad.svg  style="width:24px;"> [wyciągnięcie](PartDesign_Pad/pl.md), aby utworzyć pierwszą bryłę.

<img alt="" src=images/FreeCAD_topological_problem_01_solid.png  style="width:" height="400px;">

2\. Zaznacz górną ścianę poprzedniej bryły, a następnie użyj narzędzia <img alt="" src=images/PartDesign_NewSketch.svg  style="width:24px;"> [Nowy szkic](PartDesign_NewSketch/pl.md), aby narysować kolejny szkic. Kolejnie wykonaj drugie wyciągnięcie.

+++
| <img alt="" src=images/FreeCAD_topological_problem_02_solid_sketch_2.png  style="width:" height="400px;"> | <img alt="" src=images/FreeCAD_topological_problem_03_solid_2.png  style="width:" height="400px;"> |
+++

3\. Wybierz górną płaszczyznę poprzedniego wyciągnięcia i ponownie utwórz szkic oraz wyciągnięcie.

<img alt="" src=images/FreeCAD_topological_problem_04_solid_3.png  style="width:" height="400px;">

4\. Teraz kliknij dwukrotnie drugi szkic i zmodyfikuj go tak, aby jego długość przebiegała wzdłuż kierunku X. W ten sposób zostanie odtworzone drugie wyciągnięcie. Trzeci szkic i wyciągnięcie pozostaną w tym samym miejscu.

+++
| <img alt="" src=images/FreeCAD_topological_problem_05_solid_sketch_2.png  style="width:" height="400px;"> | <img alt="" src=images/FreeCAD_topological_problem_06_solid_2.png  style="width:" height="400px;"> |
+++

<img alt="" src=images/FreeCAD_topological_problem_07_solid_3.png  style="width:" height="400px;">

5\. Teraz ponownie kliknij dwukrotnie drugi szkic i dopasuj jego punkty tak, aby część z nich znalazła się poza granicami zdefiniowanymi przez pierwsze wyciągnięcie. W ten sposób drugie wyciągnięcie obliczy się poprawnie, ale w [widoku drzewa](Tree_view/pl.md) pojawi się błąd w trzecim wyciągnięciu.

+++
| <img alt="" src=images/FreeCAD_topological_problem_08_solid_sketch_2.png  style="width:" height="400px;"> | <img alt="" src=images/FreeCAD_topological_problem_09_solid_2.png  style="width:" height="400px;"> |
+++

![](images/FreeCAD_topological_problem_12_broken_tree.png )

6\. Po uwidocznieniu trzeciego szkicu i wyciągnięcia widać wyraźnie, że obliczanie nowej bryły nie przebiegło poprawnie. Trzeci szkic, zamiast opierać się na górnej powierzchni drugiego wyciągnięcia, pojawia się w dziwnym miejscu, ze swoją normalną skierowaną w kierunku X. Skutkuje to tym, że wyciągnięcie tego szkicu nie jest poprawne, ponieważ wyciągnięcie to byłoby odłączone od reszty <img alt="" src=images/PartDesign_Body.svg  style="width:24px;"> [zawartości](PartDesign_Body/pl.md) bryły, co jest niedozwolone.

Wydaje się, że problem polega na tym, że gdy zmodyfikowano drugi szkic, nazwa górnej powierzchni drugiego wyciągnięcia została zmieniona z `Face13` na `Face14`. Trzeci szkic jest dołączony do `Face13` tak jak pierwotnie, ale ponieważ ta powierzchnia znajduje się teraz z boku (a nie na górze), szkic podąża za jej orientacją i jest teraz nieprawidłowo umieszczony.

+++
| <img alt="" src=images/FreeCAD_topological_problem_10_solid_2_sketch_3.png  style="width:" height="400px;"> | <img alt="" src=images/FreeCAD_topological_problem_11_solid_2_faces.png  style="width:" height="400px;"> |
+++

7\. Aby rozwiązać ten problem, należy ponownie zmapować trzeci szkic do górnej powierzchni. Zaznacz szkic, kliknij wielokropek *(trzy kropki)* obok właściwości **Tryb dołączenia** i ponownie wybierz górną powierzchnię drugiego wyciągnięcia. Wtedy szkic zostanie przeniesiony na wierzch istniejącej bryły, a trzecie wyciągnięcie zostanie wygenerowane bez problemów.

![](images/FreeCAD_topological_problem_13_remap_sketch_2.png )

+++
| <img alt="" src=images/FreeCAD_topological_problem_14_solid_2_sketch_3.png  style="width:" height="400px;"> | <img alt="" src=images/FreeCAD_topological_problem_15_solid_3.png  style="width:" height="400px;"> |
+++

Przemapowanie szkicu w ten sposób może być wykonywane za każdym razem, gdy wystąpi błąd nazewnictwa topologicznego, jednak może to być uciążliwe, jeśli model jest skomplikowany i jest wiele takich szkiców, które wymagają korekty.



## Rozwiązanie

![](images/FreeCAD_topological_problem_16_dependency_graph.png )

[Graf zależności](Std_DependencyGraph/pl.md) jest narzędziem, które jest pomocne w obserwowaniu zależności pomiędzy różnymi zawartościami w dokumencie. Użycie oryginalnego przepływu pracy modelowania ujawnia bezpośrednią zależność, jaka istnieje między szkicami a wyciągnięciami. Podobnie jak w przypadku łańcucha, łatwo zauważyć, że ta bezpośrednia zależność będzie podlegała problemom z nazewnictwem topologicznym, jeśli któreś z ogniw sekwencji ulegnie zmianie.

Jak wyjaśniono na stronie [Edycja cech](Feature_editing/pl.md), rozwiązaniem tego problemu jest bazowanie szkiców nie na powierzchniach, lecz na płaszczyznach globalnego układu współrzędnych [Zawartości](PartDesign_Body/pl.md) lub płaszczyznach konstrukcyjnych dołączonych do tych globalnych płaszczyzn. Używanie płaszczyzn konstrukcyjnych do bazowania pojedynczego szkicu, jak to opisano poniżej, nie jest właściwie konieczne, ponieważ sam szkic może być bezpośrednio dołączony do płaszczyzny globalnej i ma takie same opcje odsunięcia jak płaszczyzna konstrukcyjna. Ale korzystanie z płaszczyzn konstrukcyjnych może mieć sens w przypadku pozycjonowania wielu szkiców.

1\. Zaznacz punkt położenie odniesienia [Zawartości](PartDesign_Body/pl.md) i upewnij się, że jest on widoczny. Następnie wybierz płaszczyznę XY i kliknij w narzędzie [Płaszczyzna](PartDesign_Plane/pl.md). W oknie dialogowym Odsunięcie dołączenia nadaj jej odsunięcie w kierunku Z, tak aby płaszczyzna odniesienia była współpłaszczyznowa z górną powierzchnią pierwszego wyciągnięcia.

2\. Powtórz proces, ale tym razem dodaj większe odsunięcie, tak aby druga płaszczyzna odniesienia była współpłaszczyznowa z górną powierzchnią drugiego wyciągnięcia.




+++
| <img alt="" src=images/FreeCAD_topological_problem_17_datum_plane_1.png  style="width:" height="400px;"> | <img alt="" src=images/FreeCAD_topological_problem_18_datum_plane_2.png  style="width:" height="400px;"> |
+++

3\. Zaznacz drugi szkic, kliknij elipsę obok właściwości **Tryb dołączenia**, a następnie wybierz pierwszą płaszczyznę odniesienia. Płaszczyzna odniesienia jest już odsunięta od płaszczyzny XY zawartości, więc w przypadku szkicu nie jest wymagane dodatkowe odsunięcie Z.

4\. Powtórz tę procedurę z trzecim szkicem i wybierz drugą płaszczyznę odniesienia jako podporę. Również w tym przypadku nie jest konieczne dodatkowe przesunięcie w kierunku Z.

5\. Na wykresie zależności widać teraz, że szkice i wyciągnięcia są obsługiwane przez płaszczyzny odniesienia. Ten model jest bardziej stabilny, ponieważ każdy szkic można modyfikować w zasadzie niezależnie od siebie.

![](images/FreeCAD_topological_problem_19_dependency_graph_datum_planes.png )

6\. Kliknij dwukrotnie drugi szkic i zmodyfikuj jego kształt. Drugie wyciągnięcie powinno zostać natychmiast zaktualizowane, nie powodując problemów topologicznych z trzecim szkicem i trzecim wyciągnięciem.

<img alt="" src=images/FreeCAD_topological_problem_20_independent_solid_2.png  style="width:" height="400px;">

7\. W rzeczywistości każdy szkic można modyfikować bez ingerencji w inne wyciągnięcie. Tak długo, jak wyciągnięcia mają wystarczającą długość wyciskania, tak że dotykają się i tworzą przylegającą bryłę, cała bryła będzie poprawna.

<img alt="" src=images/FreeCAD_topological_problem_21_independent_solids_all.png  style="width:" height="400px;">



## Kompromisy

Dodawanie obiektów punktów odniesienia wymaga więcej pracy od użytkownika, ale w efekcie końcowym daje bardziej stabilne modele, które w mniejszym stopniu podlegają problemowi nazewnictwa topologicznego.

Oczywiście obiekty układu odniesienia można utworzyć przed narysowaniem szkiców i wykonaniem wyciągnięć. Może to być pomocne w wizualizacji przybliżonego kształtu i wymiarów ostatecznej bryły.

Płaszczyzny odniesienia mogą być także oparte na innych płaszczyznach odniesienia. Tworzy to łańcuch zależności, który również może powodować problemy topologiczne. Ponieważ jednak płaszczyzny odniesienia są bardzo prostymi obiektami, ryzyko wystąpienia takich problemów jest mniejsze niż w przypadku, gdy jako podparcie wykorzystuje się powierzchnię obiektu bryłowego.

Obiekty układu odniesienia, [punkty](PartDesign_Point/pl.md), [linie](PartDesign_Line/pl.md), [płaszczyzny](PartDesign_Plane/pl.md) oraz [układy współrzędnych](PartDesign_CoordinateSystem/pl.md), mogą być również przydatne jako geometria odniesienia, czyli jako pomoce wizualne pokazujące ważne cechy modelu, nawet jeśli nie jest do nich bezpośrednio dołączony żaden szkic.



## Algorytm TNP 

Algorytm TNP autorstwa Realthundera opisany w wątku [Topological Naming, My Take](https://forum.freecadweb.org/viewtopic.php?t=27278) na forum, który został wybrany do redukcji wpływu problemu gubienia odniesień, został szeroko przedstawiony jako \"naprawiający problem gubienia odniesień\". To niezamierzenie wprowadziło w błąd wielu użytkowników, sugerując, że korzystanie z technik takich jak geometrie konstrukcyjne, jawne pozycjonowanie szkiców i [edycja cech](Feature_editing/pl#Porady_dotyczące_tworzenia_stabilnych_modeli.md) nie będą już przydatne do tworzenia bardziej stabilnych modeli. Ten algorytm nie ma naprawiać każdego błędu wprowadzonego przez niejasność nazewnictwa topologicznego. Ma za to trzy cele.

1.  Pierwszy i najważniejszy cel to, gdy tylko możliwe, **identyfikacja** zepsutych odniesień ze zmian topologicznych i wyświetlanie błędu użytkowników. Zamiast konieczności przechodzenia przez szereg operacji aby znaleźć pierwszą operację, która odbiega od celu projektu, operacja, która zmienia nazwy będzie automatycznie oznaczona błędem, ułatwiając znacznie ręczną naprawę problemów modelu wprowadzonych przez zmiany w operacjach lub parametrach.
2.  Niekiedy FreeCAD będzie w stanie zidentyfikować **prawdopodobną** poprawkę dla zepsutego odniesienia, tak że gdy użytkownik ręcznie naprawia oznaczone zepsute odniesienie, zaprezentowany będzie kandydat do zaakceptowania lub odrzucenia. Częstym przykładem są operacje kosmetyczne, takie jak zaokrąglenia i sfazowania, gdzie użytkownik może musieć edytować operację i albo zaakceptować proponowany wybór zastąpienia cechy albo zmienić go aby dokonać naprawy.
3.  W niektórych przypadkach, FreeCAD będzie w stanie **automatycznie** naprawić zepsute odniesienia, ponieważ wystarczające informacje o odniesieniu są przechowywane aby mieć dużą pewność, że zastąpienie jest prawidłowe. Przykładowo, podczas szkicowania bezpośrednio na ścianie, algorytm często (ale nie zawsze) prawidłowo naprawi odniesienie do ściany gdy geometria pod spodem jest zmieniana parametrycznie (przy zmienianiu struktury, jak dodawanie lub usuwanie operacji ze środka Zawartości środowiska Projekt Części taka automatyczna naprawa będzie mniej prawdopodobna). Ale FreeCAD zrobi to tylko z dużą pewnością poprawności naprawy, ponieważ błędna automatyczna naprawa może ponownie wprowadzić problem konieczności poszukiwania gdzie problem został wprowadzony aby naprawić modelu po modyfikacji. *Po pierwsze, nie szkodzić.*

We FreeCAD 1.0 implementacja tego algorytmu w oficjalnym wydaniu programu osiągnęła poziom funkcjonalności wersji Linkstage 3 użytkownika Realthunder (w której pierwotnie stworzył algorytm) na moment rozpoczęcia prac nad integracją. Istnieją nowe funkcje programu FreeCAD, które mogłyby korzystać z algorytmu, ale jeszcze tego nie robią i zawsze będzie więcej okazji do dodania poprawek kandydatów i automatycznych napraw. Początkowa praca zaowocowała *fundamentem* do wprowadzenia tych dodatkowych usprawnień z czasem, zarówno w samym programie FreeCAD, jak i w dodatkach do niego.



## Odnośniki internetowe 

-   [Projekt części: Zaokrąglenie - Nazewnictwo topologiczne](PartDesign_Fillet/pl#Nazewnictwo_topologiczne.md).
-   [Topological Naming, My Take](https://forum.freecadweb.org/viewtopic.php?t=27278): możliwe rozwiązanie, autor: realthunder.
-   [Projekt nazewnictwa topologicznego](Topological_Naming_Project/pl.md): pomysł na rozwiązanie problemu, autorstwa ickby.
-   [Skrypty danych topologicznych](Topological_data_scripting/pl.md).
-   [Edycja cech](Feature_editing/pl.md): zawiera alternatywne porady dotyczące stabilnych technik modelowania.
-   [Clarifying and expanding \"Topological Naming Problem\" documentation](https://forum.freecad.org/viewtopic.php?p=770360): Wyjaśnianie oczekiwań dla algorytmu TNP Realthundera wybranego do FreeCAD 1.0.



## Filmy

-   [Dlaczego moje modele FreeCAD się psują? - **Problem nazewnictwa topologicznego**](https://youtu.be/6p2vqEEmWq4): Wideo wyjaśnienie podstawowych zagadnień związanych z [Problem nazewnictwa topologicznego](Topological_naming_problem/pl.md).
-   [FreeCAD jest fundamentalnie uszkodzony! - Co teraz\... Pomóż mi zdecydować\...](https://www.youtube.com/watch?v=QSsVFu929jo): Wideo autorstwa Maker Tales


 {{TechDraw Tools navi}} {{PartDesign Tools navi}}



---
⏵ [documentation index](../README.md) > [Common Questions](Category_Common%20Questions.md) > [TechDraw](Category_TechDraw.md) > [PartDesign](Category_PartDesign.md) > [Part](Category_Part.md) > Topological naming problem/pl
