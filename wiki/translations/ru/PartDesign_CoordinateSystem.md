---
 GuiCommand:
   Name/ru: Создать локальную систему координат
   Name: PartDesign_CoordinateSystem
   MenuLocation: PartDesign , Создать локальную систему координат
   Workbenches: PartDesign_Workbench/ru
   Version: 0.18
   SeeAlso: PartDesign_Point/ru, PartDesign_Line/ru, PartDesign_Plane/ru
---

# PartDesign CoordinateSystem/ru


</div>



## Описание

Creates a **local coordinate system** which can be used as reference for other datum geometry. It also helps identify the orientation of the referenced datum geometry in 3D space. ![](images/PartDesign_LocalCoordinateSystem_Example.png ) 
*Local coordinate system originating out of a datum plane's origin.*



## Применение

1.  Press the **[<img src=images/PartDesign_CoordinateSystem.svg style="width:16px"> [Create a local coordinate system](PartDesign_CoordinateSystem.md)** button.
2.  Define Coordinate System parameters. Select a first reference in the 3D view to filter the available attachment modes.
3.  Depending on the selected reference, there may be one or more attachment modes available in the the list. The most likely one will automatically be selected and shown in bold in the list. The text *Attached with mode* along with the attachment mode name will appear in green at the top of the Parameters panel.
4.  To add an additional reference, press the next **Reference** button. Once pressed its label changes to *Selecting\...* until a selection is made.
5.  Select an attachment mode in the list.
6.  Define Attachment Offset values.
7.  Press **OK**.



## Опции

Double-click the **Local_CS** label in the Model tree or right-click and select **Edit datum** in the contextual menu to edit its parameters. For more details about Attachment mode and Attachment offset, see [Attachment](Part_EditAttachment.md).

## Preferences

See [PartDesign Plane](PartDesign_Plane#Preferences.md).



## Свойства



### Данные

-    **MapMode**: lists the attachment mode used.

-    **Attachment Reversed**: indicates if the coordinate system is reversed in orientation.

-    **Attachment Offset**: applies a transformation (translation and rotation) in reference to the attachment placement.

-    **Placement**: indicates the coordinates and alignment of the coordinates system´s origin .

-    **Label**: name given to the object, this name can be changed at convenience.



## Программирование


```python
lcs = App.activeDocument().addObject( 'PartDesign::CoordinateSystem', 'LCS' )
```


<div class="mw-translate-fuzzy">





</div>


{{PartDesign Tools navi

}}



---
⏵ [documentation index](../README.md) > [PartDesign](PartDesign_Workbench.md) > PartDesign CoordinateSystem/ru
