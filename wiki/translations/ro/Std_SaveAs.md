# Std SaveAs/ro
---
 GuiCommand:   Name: Std SaveAs   Name/ro: Std SaveAs   MenuLocation: Std_File_Menu/ro   File , Save as...---


</div>




<div class="mw-translate-fuzzy">

## Descriere

Salvați documentul activ sub un nou nume de fișier.


</div>

The **Std SaveAs** command saves the active document under a new file name.




<div class="mw-translate-fuzzy">

## Utilizare

Alegeți ** File** → **<img src="images/Std_SaveAs.png" width=32px> Save As...** din meniul principal.

Comanda **Save as...** permite salvarea documentului activ din proiectul în curs.

Deschideți o fereastră pentru a defini **path** și **name**: ![](images/FileSaveAs.png )  Salvați documentele de proiect în fișiere separate. Dacă există alte documente în proiect, acestea nu sunt salvate. Numele atribuit documentului pentru ao salva devine și numele folosit pentru rădăcina acelui document din arborele copacului. În salvările ulterioare, dacă se efectuează cu.**Save**, calea și numele definite pentru prima salvare sunt utilizate automat. Pentru a salva fișierul într-o altă locație sau pentru a-i da un nume nou, trebuie să reutilizați comanda **Save as...**.

Când încercați să închideți un document care nu a fost salvat, modificat sau ieșit din FreeCAD cu documentele pe care doriți să le salvați, primiți o alertă: ![](images/UnsavedDocument.png ) 

Folderul/dosarul de destinație al fișierelor salvate poate fi, de asemenea, definit în fila [Std DlgParameter](Std_DlgParameter/ro.md) din meniul **Strumenti → Modifica parametri\... → BaseApp → Preferences → General → FileOpenSavePath**.
![](images/FileOpenSavePath.png ) 

Mai multe opțiuni pot fi găsite în meniu **Modifica → Preferenze → Generale → Documento → Archiviazione**


</div>

1.  Select the **File → <img src="images/Std_SaveAs.svg" width=16px> Save As...** option from the menu.
2.  Enter a filename in the dialog box.
3.  Press the **Save** button.

## Options

-   Press **Esc** or the **Cancel** button to abort the command.

## Notes

-   This command can also be used to save dependency graphs. See [Std DependencyGraph](Std_DependencyGraph.md).

## Scripting

See [Std New](Std_New#Scripting.md).





{{Std Base navi

}}



---
⏵ [documentation index](../README.md) > Std SaveAs/ro
