---
 GuiCommand:
   Name/ru: Вставка аннотаций форматированным текстом
   Name: TechDraw_RichTextAnnotation
   MenuLocation: TechDraw , Заметки , Вставка аннотаций форматированным текстомs
   Workbenches: TechDraw_Workbench/ru
   Version: 0.19
   SeeAlso: TechDraw_Templates/ru, Draft_SVG/ru, TechDraw_LeaderLine/ru
---

# TechDraw RichTextAnnotation/ru


</div>



## Описание

The **TechDraw RichTextAnnotation** tool adds a formatted annotation block to a [Leaderline](TechDraw_LeaderLine.md) or a View.

<img alt="" src=images/TechDraw_RichTextBlock_sample.png  style="width:220px;"> 
*Stand alone RichTextAnnotation*



## Применение

1.  If there are multiple drawing pages in the document: optionally activate the desired page by selecting it in the [Tree view](Tree_view.md).
2.  To attach the RichTextAnnotation to a [Leaderline](TechDraw_LeaderLine.md), select the line in the [Tree view](Tree_view.md) or on the page.
3.  There are several ways to invoke the tool:
    -   Press the **<img src="images/TechDraw_RichTextAnnotation.svg" width=16px> [Insert Rich Text Annotation](TechDraw_RichTextAnnotation.md)** button.
    -   Select the **TechDraw → Annotations → <img src="images/TechDraw_RichTextAnnotation.svg" width=16px> Insert Rich Text Annotation** option from the menu.
4.  If there are multiple drawing pages in the document and you have not yet activated a page, the **Page Chooser** dialog box opens:
    1.  Select the desired page.
    2.  Press the **OK** button.
5.  A task panel opens.
6.  The task panel allows quick entry of text.
7.  The **Start Rich Text Editor** button opens a full featured editor:
    1.  When done, press the **<img src="images/Document-save.svg" width=16px>** button to save your changes and close the editor.
8.  Press the **OK** button to close the task panel.



## Примечания

-   After creation a RichTextAnnotation can be edited by double clicking it on the page.



## Свойства

-    **X,Y**: The location of the block. Relative to the end of the line if attached to a [Leaderline](TechDraw_LeaderLine.md), otherwise this is the position on the page.

-    **ShowFrame**: Draws an outline around the block.

-    **MaxWidth**: Limits the horizontal size of the block. A value of -1 is for unlimited width.

-    **AnnoText**: The HTML text of the block.



## Программирование


**См. так же:**

[TechDraw API](TechDraw_API/ru.md) и [Основы составления скриптов FreeCAD](FreeCAD_Scripting_Basics/ru.md).

The RichTextAnnotation tool can be used in [macros](Macros.md) and from the [Python](Python.md) console.


```python
myPage = FreeCAD.ActiveDocument().Page
myBase = FreeCAD.ActiveDocument().View
blockObj = FreeCAD.ActiveDocument.addObject('TechDraw::DrawRichAnno','DrawRichAnno')
FreeCAD.activeDocument().myPage.addView(blockObj)
blockObj.X = 5
blockObj.Y = 5
blockObj.AnnoText = myHTMLText
```





{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw RichTextAnnotation/ru
