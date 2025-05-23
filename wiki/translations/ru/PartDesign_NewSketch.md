---
 GuiCommand:
   Name/ru: Создать эскиз
   Name: PartDesign_NewSketch
   MenuLocation: Sketch , Создать эскиз
   Workbenches: PartDesign_Workbench/ru
   Version: 0.17
   SeeAlso: Sketcher_NewSketch/ru
---

# PartDesign NewSketch/ru



## Описание

Данный инструмент создает новый эскиз. Создает новое [PartDesign Тело](PartDesign_Body/ru.md) чтобы разместить в нем эскиз если такового не существует и автоматически открывает [верстак Sketcher](Sketcher_Workbench/ru.md).

Если вы создаете эскиз в [верстаке PartDesign](PartDesign_Workbench/ru.md), вам стоит использовать этот инструмент вместо **[<img src=images/Sketcher_NewSketch.svg style="width:16px"> [Sketcher Создать эскиз](Sketcher_NewSketch/ru.md)** из [верстака Sketcher](Sketcher_Workbench.md).



## Применение

1.  Нажмите на кнопку**[<img src=images/PartDesign_NewSketch.svg style="width:16px"> [PartDesign Создать эскиз](PartDesign_NewSketch/ru.md)** на панели инструментов PartDesign.
2.  В окне задач находится окно **Выбор элементов операции**. Выберете одну из плоскостей из списка или используя трехмерный вид для лучшего обзора.
3.  Нажмите на кнопку **OK**.
4.  Интерфейс автоматически переключится на верстак Sketcher для редактирования эскиза. Когда вы закроете эскиз, интерфейс вернется к верстаку PartDesign и трехмерному виду, который был до создания эскиза.
5.  В противном случае плоскость на активном теле может, в этом случае эскиз мгновенно создается.



## Опции

-   Чтобы изменить прикрепление существующего эскиза, измените параметр **Map Mode** (смотри [Свойства](#Свойства.md).)

-   Окно *Выбор элементов операции* определяет параметры нового эскиза

:   

    :   <img alt="" src=images/PartDesign.CreateSketch.SelectFeatureDialog.jpeg  style="width:300px;">

    :   Окно *Выбор элементов операции*. С этими параметрами создается эскиз на плоскости XY и разрешает использование элементов того-же тела

Dialog settings

-   Coordinate system box: defines the orientation of the sketch plane
-   Allow Used Features: *TBD*

:   Allow external features options

-   From other bodies of the same part: any elements used in the same body can be referenced
-   From different parts or free features: *TBD*
-   Make independent copy: all other elements will be separate copies, i.e. they will not change when the original changes.
-   Make dependent copy: the elements will be copies, but a dependency to the original elements is kept. This is basically using a [Shapebinder](PartDesign_ShapeBinder.md)
-   Create cross-reference: the linked elements will not be copies, but point to the original elements, e.g. a master sketch. Any changes are reflected to this sketch

To reference any items in the [Workbench Sketcher](Sketcher_Workbench.md) use the **<img src="images/Sketcher_External.svg" width=16px> [External Geometry](Sketcher_External.md)** and **[<img src=images/Sketcher_CarbonCopy.svg style="width:16px"> [CarbonCopy](Sketcher_CarbonCopy.md)** tools. Generally it is recommended to use other sketches as source for references rather than faces or edges, because they are less affected by the Topological Naming Issue.



## Свойства

-    **Map Mode**: mode of attachment of the sketch to another object, usually a plane or a face but can be other types of objects. Click once in the field to reveal a **...** button and press it to open the [Attachment](Part_EditAttachment.md) dialog. If set to Deactivated, the Placement property is enabled.

-    **Placement**: controls the orientation of the sketch in the 3D space; see [placement](Std_Placement.md). Disabled if the sketch is attached through the Map Mode property.


<div class="mw-translate-fuzzy">





</div>


{{PartDesign Tools navi

}}



---
⏵ [documentation index](../README.md) > [PartDesign](PartDesign_Workbench.md) > PartDesign NewSketch/ru
