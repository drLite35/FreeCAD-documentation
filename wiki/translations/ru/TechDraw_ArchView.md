---
 GuiCommand:
   Name/ru: Вставить объект верстака Arch
   Name: TechDraw_ArchView
   MenuLocation: TechDraw , Вставить объект верстака Arch
   Workbenches: TechDraw_Workbench/ru, Arch_Workbench/ru
   SeeAlso: Arch_SectionPlane/ru
---

# TechDraw ArchView/ru


</div>



## Описание

The **TechDraw ArchView** tool inserts an Arch View, a view of an <img alt="" src=images/Arch_SectionPlane.svg  style="width:16px;"> [Arch SectionPlane](Arch_SectionPlane.md), on a [TechDraw page](TechDraw_PageDefault.md).


<small>(v1.0)</small> 

: The [TechDraw View](TechDraw_View.md) tool can also create an Arch View.

<img alt="" src=images/TechDraw_Arch_example.jpg  style="width:500px;">



## Применение

1.  Select an Arch section plane in the [3D view](3D_view.md) or [Tree view](Tree_view.md).
2.  If there are multiple drawing pages in the document: optionally add the desired page to the selection by selecting it in the [Tree view](Tree_view.md).
3.  Select the **TechDraw → Views From Other Workbenches → <img src="images/TechDraw_ArchView.svg" width=16px> Insert BIM Workbench Object** option from the menu.
4.  If there are multiple drawing pages in the document, and if no page is displayed in the [Main view area](Main_view_area.md) and you have not yet selected a page, the **Page Chooser** dialog box opens:
    1.  Select the desired page.
    2.  Press the **OK** button.



## Опции

-   The Arch View is rendered by the [BIM Workbench](BIM_Workbench.md).
-   [Draft Dimensions](Draft_Snap_Dimensions.md), [Draft Texts](Draft_Text.md) and any other 2D (Sketch or Draft) object considered by the section plane is rendered \"as is\" (no intersection or hidden lines) on top of the solid geometry
-   The volume of [Arch Spaces](Arch_Space.md) is not rendered, only the label will be rendered
-   Cut lines, projected lines (if Show Hidden property is set to True) and 2D lines above can be rendered with different line widths. This can be configured in the Arch preferences.
-   The ArchView has two rendering modes:
    -   Wireframe, which uses the OpenCasCade algorithms of the [TechDraw Workbench](TechDraw_Workbench.md), is fast and produces only lines (no face fill possible)
    -   Solid, which is based on the [Painter\'s algorithm](https://en.wikipedia.org/wiki/Painter%27s_algorithm), and is capable of rendering faces filled with their shape color. However, it is much slower and can fail in many situations.

:   The image below illustrates the difference between the two rendering modes:





:   ![](images/TechDraw_Arch_rendering.jpg )

-   Only the base line of [Arch Pipes](Arch_Pipe.md) is rendered, not the full volume of the tube:

:   ![](images/TechDraw_Arch_piping.jpg )

## Notes

The ArchView is rendered within the [BIM Workbench](BIM_Workbench.md), therefore TechDraw has limited control over its appearance. You may need to make changes within Arch to get the representation you want.



## Свойства

See also: [Property editor](Property_editor.md).

An Arch View, formally a {{Incode|TechDraw::DrawViewArch}} object, has the [properties](TechDraw_View#Properties_Part_View.md) that are common to all View types. It also has the following additional properties:

### Data


{{TitleProperty|Arch view}}

-    **Source|Link**: The section plane object to be displayed.

-    **All On|Bool**: If hidden objects must be shown or not. If `False`, only objects that are visible in the 3D view are rendered.

-    **Render Mode|Enumeration**: The render mode to use, {{Value|Solid}} or {{Value|Wireframe}}.

-    **Fill Spaces|Bool**: If `True`, Arch Spaces are shown as a colored area.

-    **Show Hidden|Bool**: If the hidden geometry (the part of the geometry that lies behind the section plane) is shown or not. It will be rendered in dashed line, which can be configured in the Arch preferences.

-    **Show Fill|Bool**: If cut areas must be filled with a grey color or not.

-    **Line Width|Float**: The width of the main lines. Cut lines and projected/2D line widths ratios can be configured in the Arch preferences.

-    **Font Size|Float**: The size of all texts that appear in this view.

-    **Cut Line Width|Float**: Width of the cut lines in this view.

-    **Join Arch|Bool**: If `True`, walls and structures will be fused by material.

-    **Line Spacing|Float**: The spacing between lines to use for multiline texts. <small>(v1.0)</small> 


{{TitleProperty|Drawing view}}

-    **Symbol|String|Hidden**: The SVG code defining this symbol.

-    **Editable Texts|StringList**: Substitution values for the editable strings in this symbol.

-    **Owner|Link**: Feature to which this symbol is attached. <small>(v1.0)</small> 



## Программирование


**См. так же:**

[TechDraw API](TechDraw_API/ru.md) и [Основы составления скриптов FreeCAD](FreeCAD_Scripting_Basics/ru.md).

The ArchView tool can be used in [macros](Macros.md) and from the [Python](Python.md) console by using the following functions:


```python
dv = FreeCAD.ActiveDocument.addObject('TechDraw::DrawViewArch','TestArch')
dv.Source = mySectionPlane
rc = page.addView(dv)
```





{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw ArchView/ru
