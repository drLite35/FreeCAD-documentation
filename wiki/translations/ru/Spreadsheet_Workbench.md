# Spreadsheet Workbench/ru
<div class="mw-translate-fuzzy">





</div>

<img alt="Логотип верстака электронных таблиц" src=images/Workbench_Spreadsheet.svg  style="width:128px;">



## Введение

<img alt="" src=images/Workbench_Spreadsheet.svg  style="width:24px;"> [Верстак электронных таблиц](Spreadsheet_Workbench/ru.md) позволяет создать и редактировать электронные таблицы, использовать данные из электронной таблицы как параметр в модели, заполнять таблицу данными из модели, выполнять вычисления, и экспортировать данные в другие приложения текстовых таблиц, такие как LibreOffice или Microsoft Excel.




<img alt="" src=images/Spreadsheet_screenshot.jpg  style="width:600px;"> 
*Таблица с определенными ячейками, заполненными текстом и значениями.*



## Инструменты

-   <img alt="" src=images/Spreadsheet_CreateSheet.svg  style="width:24px;"> [Create sheet](Spreadsheet_CreateSheet/ru.md): создать новую электронную таблицу.

-   <img alt="" src=images/Spreadsheet_Import.svg  style="width:24px;"> [Import](Spreadsheet_Import.md): import a CSV file into a spreadsheet.

-   <img alt="" src=images/Spreadsheet_Export.svg  style="width:24px;"> [Export](Spreadsheet_Export.md): export a CSV file from a spreadsheet.

-   <img alt="" src=images/Spreadsheet_MergeCells.svg  style="width:24px;"> [Merge cells](Spreadsheet_MergeCells.md): merge selected cells.

-   <img alt="" src=images/Spreadsheet_SplitCell.svg  style="width:24px;"> [Split cell](Spreadsheet_SplitCell.md): split previously merged cells.

-   <img alt="" src=images/Spreadsheet_AlignLeft.svg  style="width:24px;"> [Align left](Spreadsheet_AlignLeft.md): align the contents of selected cells to the left.

-   <img alt="" src=images/Spreadsheet_AlignCenter.svg  style="width:24px;"> [Align center](Spreadsheet_AlignCenter.md): align the contents of selected cells to the center horizontally.

-   <img alt="" src=images/Spreadsheet_AlignRight.svg  style="width:24px;"> [Align right](Spreadsheet_AlignRight.md): align the contents of selected cells to the right.

-   <img alt="" src=images/Spreadsheet_AlignTop.svg  style="width:24px;"> [Align top](Spreadsheet_AlignTop.md): align the contents of selected cells to the top.

-   <img alt="" src=images/Spreadsheet_AlignVCenter.svg  style="width:24px;"> [Align vertical center](Spreadsheet_AlignVCenter.md): align the contents of selected cells to the center vertically.

-   <img alt="" src=images/Spreadsheet_AlignBottom.svg  style="width:24px;"> [Align bottom](Spreadsheet_AlignBottom.md): top align the contents of selected cells to the bottom.

-   <img alt="" src=images/Spreadsheet_StyleBold.svg  style="width:24px;"> [Style bold](Spreadsheet_StyleBold.md): toggle the contents of selected cells to/from bold.

-   <img alt="" src=images/Spreadsheet_StyleItalic.svg  style="width:24px;"> [Style italic](Spreadsheet_StyleItalic.md): toggle the contents of selected cells to/from italic.

-   <img alt="" src=images/Spreadsheet_StyleUnderline.svg  style="width:24px;"> [Style underline](Spreadsheet_StyleUnderline.md): toggle the contents of selected cells to/from underlined.


<div class="mw-translate-fuzzy">

-   <img alt="" src=images/Spreadsheet_SetAlias.svg  style="width:24px;"> [Set alias](Spreadsheet_SetAlias/ru.md): установить псевдоним для выбранных ячеек.


</div>


<div class="mw-translate-fuzzy">

-    **Black**и **White** устанавливают цвета переднего и заднего плана выбранных ячеек.


</div>

## Preferences

-   <img alt="" src=images/Preferences-spreadsheet.svg  style="width:32px;"> [Preferences](Spreadsheet_Preferences.md): the preferences for the Spreadsheet Workbench. <small>(v0.20)</small> 

## Removing cells can be dangerous 

Note that deleting or removing cells with data can break the spreadsheet and your model if it relies on the spreadheet. You are not prewarned if this happens.

## Insert and remove rows and columns 

Rows and columns can be inserted or removed by right-clicking a row or column header and selecting the appropriate option from the contex menu. It is possible to select multiple rows or columns first. Either by holding down the **Ctrl** key while selecting the headers, or by holding down the left mouse button and dragging.

## Edit cells 

The content of a cell can be edited by selecting the cell and entering a value in the **Content** inputbox at the top of the window. To edit a cell in-place, select it and press **F2**, or double-click it.

## Delete cells 

To delete one or more cells select them and press **Del**. This will delete their contents, their properties and their aliases. To only delete the content of a cell it should be edited instead.

## Cut and copy-paste cells 

Cut and copy-paste operations can be used on spreadsheets cells. You can use the normal shortcuts for these operations: **Ctrl**+**X**, **Ctrl**+**C** and **Ctrl**+**V** respectively. To select multiple cells hold down the **Ctrl** key while selecting, or hold down the left mouse button and drag to select a rectangular cell range.

The cut and copy operations store the contents, properties and aliases of the cells on the Clipboard. The paste operation writes the data in such a way that the content of the top left cell of the stored data is dropped in the active cell. Other stored content is placed relative to that cell. Formulas are updated accordingly. Aliases are only pasted if they are unique.



### Свойства ячейки 


<div class="mw-translate-fuzzy">

Свойства ячейки электронной таблицы можно редактировать, щелкнув ячейку правой кнопкой мыши. Появится следующий диалог:


</div>

![](images/SpreadsheetCellPropDialog.png )

Как указано на вкладках, можно изменить следующие свойства:


<div class="mw-translate-fuzzy">

-   Цвет: цвет текста и цвет фона.
-   Выравнивание: выравнивание текста по горизонтали и вертикали
-   Стиль: стиль текста: полужирный, курсив, подчеркивание.
-   Единицы: Отображение единиц измерения для этой ячейки. Прочтите раздел [Единицы измерения](#Единицы_измерения.md) ниже.
-   Псевдоним: Определение [псевдонима](Spreadsheet_SetAlias/ru.md) для этой ячейки. Этот псевдоним можно использовать в формулах ячеек, а также в общих [выражениях](Expressions/ru.md); смотри раздел [данные электронных таблиц в выражениях](#Выражения_в_ячейках.md) для получения дополнительной информации.


</div>



## Выражения в ячейках 


<div class="mw-translate-fuzzy">

Ячейка таблицы может содержать любой текст или выражение. Технически, выражение должно начинаться со знака равенства \'=\'. Однако, таблица пытается быть умной, и если Вы введёте нечто, похожее на выражение, но без начального знака \'=\', он будет добавлен автоматически.


</div>


<div class="mw-translate-fuzzy">

Выражения ячеек могут содержать числа, функции, ссылки на другие ячейки и ссылки на свойства модели. (Но смотрите [текущие ограничения](#Текущие_ограничения.md) ниже). Ссылки на ячейки по их столбцам (ЗАГЛАВНЫЕ буквы) и строкам (числа). На ячейки можно так же ссылаться по их [псевдонимам](#alias_name.md) (см. ниже). Пример: B4 + A6


</div>


<div class="mw-translate-fuzzy">

**Примечание:** Выражения в ячейках обрабатываются FreeCAD как программный код. Поэтому при редактировании ячеек видимое содержимое не следует настройкам дисплея:

-   десятичный разделитель всегда точка
-   число показываемых десятичных чисел может отличаться от [настроек](Preferences_Editor/ru#Единицы_измерения.md)


</div>

Ссылки на объекты в модели описаны в разделе [Ссылки на данные САПР](#Ссылки_на_данные_САПР.md). Использование значений ячеек для определения параметров моделей описано в разделе [Данные таблицы в выражениях](#Данные_таблицы_в_выражениях.md). Насчёт дополнительной информации о выражениях и доступных функциях, смотрите [Выражения](Expressions/ru.md).



## Взаимодействие между электронными таблицами и моделью САПР 

Данные в ячейках электронной таблицы могут использоваться в выражениях параметров модели САПР. Таким образом, электронная таблица может использоваться как источник значений параметров, используемых во всей модели, эффективно собирая значения в одном месте. Когда значения изменяются в электронной таблице, они распространяются по всей модели.

Точно так же свойства из объектов модели САПР могут использоваться в выражениях в ячейках электронной таблицы. Это позволяет использовать такие свойства объекта, как объем или площадь в электронной таблице. Если имя объекта в модели САПР изменяется, изменение автоматически распространяется на все ссылки в выражениях в электронной таблице, использующих изменённое имя.


<div class="mw-translate-fuzzy">

В одном документе можно использовать более одной электронной таблицы; электронным таблицам можно давать присвоенное пользователем имя (переименовывать), как и любому другому объекту.


</div>

FreeCAD will automatically assign a unique name to a spreadsheet when it is created. These names follow the pattern `Spreadsheet`, `Spreadsheet001`, `Spreadsheet002` and so on. The name can not be changed, and it is not visible in the properties of the spreadsheet. It can be used to refer to the spreadsheet in an [Expression](Expressions.md) (see [Spreadsheet data in expressions](#Spreadsheet_data_in_expressions.md) below.)

The label of a spreadsheet is automatically set to the name of the spreadsheet upon creation. Unlike the name, the label can be changed, for example in the properties panel or using the context menu action Rename. By default FreeCAD does not accept duplicate labels, but there is a [preference](Preferences_Editor#Document.md) to override this. Spreadsheets with duplicate labels in the same document cannot be referenced by their label.


<div class="mw-translate-fuzzy">

FreeCAD проверяет на циклические зависимости. Смотрите в разделе [Текущие ограничения](Spreadsheet_Workbench/ru#Текущие_ограничения.md).


</div>



### Ссылки на данные САПР 

Как указано выше, можно ссылаться на данные из модели САПР в выражениях электронной таблицы.


<div class="mw-translate-fuzzy">

В следующей таблице показаны некоторые примеры, предполагающие, что модель имеет функцию с именем «MyCube»:

  Данные САПР                                 Ячейка в таблице               Результат
    
  Параметрическая длинна Куба верстака Part   =MyCube.Length                 Длинна в единицах mm
  Объём Cube                                  =MyCube.Shape.Volume           Объём в mm³ без указания единиц
  Тип формы Cube                              =MyCube.Shape.ShapeType        String: Solid
  Метка Cube                                  =MyCube.Label                  String: MyCube
  Координата X центра масс Cube               =MyCube.Shape.CenterOfMass.x   Координата X в mm без указания единиц


</div>



### Данные таблицы в выражениях 

In order to use spreadsheet data in other parts of FreeCAD, you will usually create an [Expression](Expressions.md) that refers to the spreadsheet and the cell that contains the data you want to use. You can identify spreadsheets by name or by label, and you can identify the cells by address or by alias. Autocompletion is available for all forms of referencing.

++++
|                 | Spreadsheet by Name                                 | Spreadsheet by Label                                   |
+=================+=====================================================+========================================================+
| Cell by Address |                                      |                                         |
|                 | `<nowiki>=Spreadsheet042.B5</nowiki>`      | `<nowiki>=<<MySpreadsheet>>.B5</nowiki>`      |
|                 |                                                  |                                                     |
++++
| Cell by Alias   |                                      |                                         |
|                 | `<nowiki>=Spreadsheet042.MyAlias</nowiki>` | `<nowiki>=<<MySpreadsheet>>.MyAlias</nowiki>` |
|                 |                                                  |                                                     |
++++


<div class="mw-collapsible mw-collapsed">

The recommended way to refer to spreadsheet data is to use the spreadsheet label and cell alias name. For a more in-depth explanation of the pros and cons of the referencing modes, see the expanded section below.


<div class="mw-collapsible-content">

Using the spreadsheet label has the advantage that it can be freely changed to describe the contents of the spreadsheet. It is also easier to identify the spreadsheet that is being used since the text in the expression matches the label shown in the model and property views. If you decide to change the label of a spreadsheet, existing references to the contents of the spreadsheet will be updated, so you won\'t break your expressions by renaming the spreadsheet. The internal name of the spreadsheet is not readily available anywhere except within the expression editor, so if you use the internal name and later decide to rename the spreadsheets, you might have a hard time tracing your expression data back to its source.

Be aware that when you create a new spreadsheet, the name and the label are the same, so it is easy to accidentally use the spreadsheet name instead of the label. A simple way to avoid this is to give the spreadsheet a meaningful name before starting to use it in expressions.

While you may use the row and column number in an expression to reference a cell, best practice is to give the cell an alias name and use that. See [Cell properties](#Cell_properties.md) on how to set the alias. For example, if the data in cell B1 contained the length parameter for an object, an alias name of `MyObject_Length` would allow the value to be referred to as `<<MyParams>>.MyObject_Length` instead of `Spreadsheet.B1`. Besides being much easier to read and understand, alias names are also much easier to change if you decide to adjust the structure of your spreadsheet. Using an alias also has the advantage that it is reasier to see which cells are used to control other parts of the document. Note that FreeCAD will automatically adjust the positional references in expressions if you insert or remove rows and columns in the spreadsheet, so even if you use row and column numbers in an expression, you can insert rows and columns without breaking the references to the surrounding cells.


</div>


</div>

### Complex models and recomputes 

Editing a spreadsheet will trigger a recompute of the 3D model, even if the changes do not affect the model. For a complex model a recompute can take a long time, and having to wait after every single edit is of course quite annoying.

There are three solutions to deal with this:

1.  Temporarily skip recomputes:
    -   In the [Tree view](Tree_view.md) right-click the <img alt="" src=images/Document.svg  style="width:24px;"> document that contains the spreadsheet.
    -   Select the **Skip recomputes** option from the context menu.
    -   There is a big disadvantage to this solution. New values entered in the spreadsheet will not be displayed until the document is recomputed. Instead `#PENDING` is shown.
    -   You can either recompute manually, using the [Std Refresh](Std_Refresh.md) command, or disable **Skip recomputes** when you are done editing.
2.  Use a macro to automatically skip recomputes while editing a spreadsheet:
    -   Download and run [skipSheet.FCMacro](https://forum.freecadweb.org/viewtopic.php?f=8&t=48600#p419301).
    -   This solution saves a few steps compared to the first solution, but also has the mentioned disadvantage.
3.  Put the spreadsheet in a separate [FreeCAD file](File_Format_FCStd.md):
    -   You can reference spreadsheet data from an external **.FCStd** file with this syntax: `<nowiki>=NameOfFile#<<MySpreadsheet>>.MyAlias</nowiki>`.
    -   The advantage of having the spreadsheet in another file over switching off recomputes is that the spreadsheet itself does get recomputed.
    -   The disadvantage is that the model won\'t automatically recompute after changes to the spreadsheet.
    -   In the scenario where you first open the \'spreadsheet\' file, change one or more values and then open the \'model\' file, there won\'t be any indication that the model needs to be recomputed. But if both files are open the [Std Refresh](Std_Refresh.md) icon will update correctly for the \'model\' file after changes to the \'spreadsheet\' file.



## Единицы измерения 

The Spreadsheet has a notion of dimension (units) associated with cell values. A number entered without an associated unit has no dimension. The unit should be entered immediately following the number value, with no intervening space. If a number has an associated unit, that unit will be used in all calculations. For example, the multiplication of two lengths with the unit mm gives an area with the unit mm².

If a cell contains a value which represents a dimension, it should be entered with its associated unit. While in many simple cases one can get by with a dimensionless value, it is unwise to not enter the unit. If a value representing a dimension is entered without its associated unit, there are some sequences of operations which cause FreeCAD to complain of incompatible units in an expression when it appears the expression should be valid. (This may be better understood by viewing [this thread](https://forum.freecadweb.org/viewtopic.php?f=3&t=34713&p=292455#p292438) in the FreeCAD forums.)

You can change the units displayed for a cell value using the [Cell properties dialog](#Cell_properties.md). This does not change the value contained in the cell; it only converts the existing value for display. The value used for calculations does not change, and the results of formulas using the value do not change. For example, a cell containing the value \"5.08cm\" can be displayed as \"2in\" by changing the units tab value to \"in\".

A dimensionless number cannot be changed to a number with a unit by the cell properties dialog. One can put in a unit string, and that string will be displayed; but the cell still contains a dimensionless number. In order to change a dimensionless value to a value with a dimension, the value itself must be re-entered with its associated unit.

Occasionally it may be desirable to get rid of a dimension in an expression. This can be done by multiplying by 1 with a reciprocal unit.



## Импорт и экспорт 

### CSV format 

FreeCAD spreadsheets can be imported and exported to the [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) format which can also be read and written by most other spreadsheet applications such as Microsoft Excel or LibreOffice Calc. See [Spreadsheet Import](Spreadsheet_Import.md) and [Spreadsheet Export](Spreadsheet_Export.md) for more information.

### XLSX format 

Spreadsheets in the Excel-format XLSX can be imported with the [Std Import](Std_Import.md) command or the [Std Open](Std_Open.md) command. The following features are supported:

-   All functions that are also available in the FreeCAD spreadsheet. Other functions give an error in the corresponding cell after import.
-   Alias names for cells.
-   More than one sheet in the Excel-spreadsheet. In this case one FreeCAD spreadsheet is created for each Excel sheet.

Other functionality is not imported into the FreeCAD spreadsheet.

## Printing

To handle the page setup necessary for printing, FreeCAD spreadsheets are printed by inserting them into a [TechDraw Spreadsheet View](TechDraw_SpreadsheetView.md).



## Текущие ограничения 


<div class="mw-translate-fuzzy">

FreeCAD проверяет циклические зависимости. По задумке эта проверка останавливается на уровне объекта электронной таблицы. Как следствие, у вас не должно быть электронной таблицы, содержащей как ячейки, значения которых используются для определения параметров модели, так и ячейки, значения которых используют выходные данные модели. Например, у вас не может быть ячеек, определяющих длину, ширину и высоту объекта, и другой ячейки, которая ссылается на общий объем полученной формы. Это ограничение можно преодолеть с помощью двух электронных таблиц: одна используется в качестве источника данных для входных параметров модели, а другая используется для расчётов на основе результирующих геометрических данных.


</div>

## Cell binding 


<small>(v0.20)</small> 

It is possible to bind the content of cells to other spreadsheet cells. This can be useful when dealing with large tables or to get cell content from another spreadsheet.

### Create binding 

To bind, for example, the cell range A3-C4 to the cell range B1-D2:

1.  Select the cell range A3-C4.
2.  Right-click and select **Bind...** from the context menu.
3.  The **Bind Spreadsheet Cells** dialog opens.
4.  Set the range B1-D2 for the **To cells**:
    ![](images/Spreadsheet_binding-dialog.png )
5.  Press **OK**.
6.  Bound cells have a blue border to highlight the binding.
7.  If you now enter something in cell C1, the same will immediately appear in cell B3.

![](images/Spreadsheet_binding-result.png ) 
*The spreadsheet may now look like this*

### Change binding 

1.  Right-click a bound cell (there is no need to highlight the whole bound range) and select **Bind...** from the context menu.
2.  The **Bind Spreadsheet Cells** dialog opens.
3.  Change one or more options. Note that the **Bind cells**, the bound cell range, cannot be changed.
4.  Press **OK**.

### Remove binding 

1.  Right-click a bound cell (there is no need to highlight the whole bound range) and select **Bind...** from the context menu.
2.  The **Bind Spreadsheet Cells** dialog opens.
3.  Press **Unbind**.

### Notes

-   The **Hide dependency of binding** option can be used to prevent problems with cyclic dependencies between spreadsheets. Selecting it is necessary when, for example, cells in *Spreadsheet A* are bound to *Spreadsheet B*, while cells in *Spreadsheet B*, in turn, are bound to some other cells in *Spreadsheet A*. This option should be used with caution:
    -   Hiding dependencies can be dangerous because broken dependencies can damage your FreeCAD file. For example, when you delete a spreadsheet you will not be warned about hidden dependencies.
    -   When you open a document with a spreadsheet containing a hidden dependency, you will get the spreadsheet marked to be recomputed. This is because a cyclic dependency cannot be recomputed automatically. To recompute the [Std Refresh](Std_Refresh.md) tool must be used.
-   The cell binding has a range check and warns you about mismatched ranges. For example binding 1x3 cells to 3x2 cells cannot work because it is unknown which 3 cells of the original 6 cells should be used.
-   You cannot change the cell range of an existing binding. You must first unbind the cells and then create a new binding.
-   The frame color indicating the binding cannot be changed yet.

## Configuration tables 


<small>(v0.20)</small> 

You can use Spreadsheets to create configuration tables with sets of predefined parameters for your model, and then dynamically change which configuration to use. See the [Configuration Tables](Configuration_Tables.md) tutorial. Read [this Forum post](https://forum.freecadweb.org/viewtopic.php?f=17&t=42183) if you want to know more about the inner workings of this feature.

## Scripting


```python
import Spreadsheet
sheet = App.ActiveDocument.addObject("Spreadsheet::Sheet", "MySpreadsheet")
sheet.Label = "Dimensions"

sheet.set("A1", "10mm")
sheet.recompute()
sheet.get("A1")

sheet.setAlias("B1", "Diameter")
sheet.set("Diameter", "20mm")
sheet.recompute()
sheet.get("Diameter")

# sheet.get() results in an error if the cell is empty.
# sheet.getContents() can be used to check the cell first.
if sheet.getContents("C1"):
    print(sheet.get("C1"))
```


<div class="mw-translate-fuzzy">





</div>


{{Spreadsheet_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [Workbenches](Category_Workbenches.md) > [Spreadsheet](Category_Spreadsheet.md) > Spreadsheet Workbench/ru
