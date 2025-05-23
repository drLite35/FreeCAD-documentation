---
 GuiCommand:
   Name/ru: Экспорт листа в DXF
   Name: TechDraw_ExportPageDXF
   MenuLocation: TechDraw , Экспорт листа в DXF
   Workbenches: TechDraw_Workbench/ru
   Version: 0.18
   SeeAlso: TechDraw_ExportPageSVG/ru, Draft_DXF/ru
---

# TechDraw ExportPageDXF/ru


</div>



## Описание

The **TechDraw ExportPageDXF tool** saves a drawing page as a [DXF](DXF.md) file.



## Применение

1.  If there are multiple drawing pages in the document: optionally activate the desired page by selecting it in the [Tree view](Tree_view.md).
2.  There are several ways to invoke the tool:
    -   Press the **<img src="images/TechDraw_ExportPageDXF.svg" width=16px> [Export Page as DXF](TechDraw_ExportPageDXF.md)** button.
    -   Select the **TechDraw → Page  → <img src="images/TechDraw_ExportPageDXF.svg" width=16px> Export Page as DXF** option from the menu.
    -   If a page is displayed in the [Main view area](Main_view_area.md): right-click the page\'s window and select the **Export DXF** option from the context menu.
3.  If there are multiple drawing pages in the document and you have not yet activated a page, the **Page Chooser** dialog box opens:
    1.  Select the desired page.
    2.  Press the **OK** button.
4.  The **Save DXF file** dialog box opens.
5.  Select a location and file name.



### Ограничения

-   Radial and Diameter dimensions will only export properly if they are \"inside\" the arc.
-   Scaling is not supported. The DXF will be drawn in the actual size of the TechDraw page.
-   Units are not supported. The DXF will be drawn in millimeters (mm). Dimension text will be shown exactly as displayed in TechDraw.
-   TechDraw can\'t export a [Insert Draft Workbench Object](TechDraw_DraftView.md) or an [Insert Arch Workbench Object](TechDraw_ArchView.md) to DXF. These views are [SVG](SVG.md) elements generated internally by the [Draft Workbench](Draft_Workbench.md), so there is no geometrical shape to export. To export a view as DXF, it must have been created with [Insert View](TechDraw_View.md) or [Insert Projection Group](TechDraw_ProjectionGroup.md). For example, select an [Arch SectionPlane](Arch_SectionPlane.md), then use [Draft Shape2DView](Draft_Shape2DView.md) to create a flat projection shape, and then use [Insert View](TechDraw_View.md) on this object. Alternatively, select the objects from the tree view or the 3D viewport, and export to DXF using **File → [Export](Std_Export.md)**.
-   The title block of a page is an [SVG](SVG.md) template as well, so it will not be exported to DXF either.
-   In general, TechDraw can only export to DXF those elements that are supported by the `Import::ImpExpDxfWrite` class of the [Import Module](Draft_DXF.md).



## Примечания

-   This function exports the R12 (AC1009) and R14 (AC1014) versions of [DXF](DXF.md).
    -   R12 is an older, simpler version of the standard, but should be readable by most other software.
    -   R14 is the default version. It includes support for splines and ellipses among other things.
-   These parameters affect the output:
    -   
        **Tools → Edit parameters → BaseApp/Preferences/Mod/Import → DxfVersionOut**
        
        . This is an integer value. Valid entries are 12 or 14. The default is 14.

    -   
        **Tools → Edit parameters → BaseApp/Preferences/Mod/Import → DiscretizeEllipses**
        
        . This is a boolean value. If `True`, splines and ellipses are converted to polylines; if `False`, splines and ellipses are written as splines and ellipses objects. The default is `False`. If the DxfVersionOut parameter is 12, splines and ellipses are always converted to polylines.

    -   
        **Tools → Edit parameters → BaseApp/Preferences/Mod/Import → maxsegmentlength**
        
        . This is a float value. If splines and ellipses are converted to polylines this parameter determines the segment length.



## Программирование


**См. так же:**

[TechDrawGui API](TechDrawGui_API/ru.md) и [Основы составления скриптов FreeCAD](FreeCAD_Scripting_Basics/ru.md).

The SaveDXF tool can be used in [macros](Macros.md) and from the [Python](Python.md) console by using the following functions:


```python
TechDraw.writeDXFPage(page,filename)
```


<div class="mw-translate-fuzzy">





</div>


{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw ExportPageDXF/ru
