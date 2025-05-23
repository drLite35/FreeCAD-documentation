---
 GuiCommand:
   Name: Std UnitsCalculator
   Name/pl: Std: Przelicznik jednostek
   MenuLocation: Przybory , Przelicznik jednostek
   Workbenches: wszystkie
---

# Std UnitsCalculator/pl



## Opis

Polecenie **Przelicznik jednostek** otwiera okno dialogowe Przelicznika jednostek. Narzędzie to może być używane do konwersji wartości z jednego systemu miar na inny.

![](images/Std_UnitsCalculator_Dialog.png ) 
*Okno dialogowe Przelicznika jednostek*



## Użycie

1.  Wybierz z menu opcję **Przybory → <img src="images/Std_UnitsCalculator.svg" width=16px> Przelicznik jednostek ...**.
2.  Otwiera się okno dialogowe Przelicznik jednostek. Więcej informacji znajdziesz w sekcji [Opcje](#Opcje.md).
3.  Okno dialogowe jest niemodalne, co oznacza, że może pozostać otwarte podczas dalszej pracy z programem FreeCAD.
4.  Naciśnij przycisk **Zamknij**, aby zamknąć okno dialogowe.



## Opcje



### Wiersz górny 

1.  Wprowadź wartość z jednostkami w pierwszym polu. Na przykład {{Value|10 mm}}.
    -   Jednostki z wykładnikami powinny być wprowadzane przy użyciu notacji {{Value|^}}. Na przykład {{Value|1 m^2}}.
    -   Jeśli wartość wejściowa nie może być rozpoznana lub jeśli jednostki są nieznane, w polu **=\>**\' pojawi się komunikat \"błąd składni\".
2.  Wprowadź jednostki docelowe w polu **jako**. Na przykład {{Value|in}}.
    -   Jeśli jednostki są nieznane, w polu **=\>** pojawi się komunikat \"nieznana jednostka\".
    -   Jeśli jednostki w pierwszym i drugim polu wejściowym nie pasują do siebie, w polu **=\>** pojawi się komunikat o niedopasowaniu jednostek. W przykładzie jednostki pasują, ponieważ \'mm\' i \'in\' są jednostkami długości.
3.  Jeżeli nie ma błędów w danych wejściowych, pole **=\>** natychmiast pokaże wynik. Dla przykładowych wartości wynik to {{Value|0,394 in}}.
4.  Opcjonalnie naciśnij przycisk **Kopiuj**, aby skopiować zawartość pola **=\>** do schowka. Wartość ta może być następnie np. wklejona w panelu zadań programu FreeCAD lub w oknie dialogowym.



### Obszar tekstowy 

1.  Konwersja wykonana w najwyższym wierszu może być skopiowana do obszaru tekstowego poprzez naciśnięcie **Enter** w pierwszym lub drugim polu wejściowym.
2.  Obszar tekstowy może zawierać wiele konwersji, a jego zawartość można zaznaczyć i skopiować do schowka za pomocą skrótu **Ctrl+C** i wykorzystać w innych programach.



### Ilość

1.  Wybierz opcję z listy rozwijanej **System jednostek**. Będzie to docelowy system jednostek. Wybierz **System preferencji** aby użyć systemu jednostek zdefiniowanego w [Preferencje](Preferences_Editor/pl#Jednostki.md).
2.  Wybierz opcję z listy rozwijanej **Kategoria jednostek**.
3.  Wpisz wartość z jednostkami w polu **Ilość**. Jednostki muszą być zgodne z kategorią jednostek.
4.  Kliknij w polu wprowadzania **Miejsca dziesiętne** i naciśnij **Enter**, aby przeliczyć wartość w polu wprowadzania **Ilość**.



## Uwagi

-   Zobacz stronę [Wyrażenia](Expressions/pl#Jednostki.md), aby uzyskać listę wszystkich znanych jednostek.



---
⏵ [documentation index](../README.md) > Std UnitsCalculator/pl
