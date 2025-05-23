---
 GuiCommand:
   Name/ru: Вставить группу проекций
   Name: TechDraw_ProjectionGroup
   MenuLocation: TechDraw , Вставить группу проекций
   Workbenches: TechDraw_Workbench/ru
   SeeAlso: TechDraw_View/ru, TechDraw_SectionView/ru
---

# TechDraw ProjectionGroup/ru


</div>



## Описание

The **TechDraw ProjectionGroup** tool creates a [multiview projection](https://en.wikipedia.org/wiki/Multiview_projection) of one or more 3D objects, using the traditional [first-](https://en.wikipedia.org/wiki/Multiview_orthographic_projection#First-angle_projection) or [third-angle projection](https://en.wikipedia.org/wiki/Multiview_orthographic_projection#Third-angle_projection). The isometric views of the 4 front corners can also be included.


<small>(v1.0)</small> 

: The [TechDraw View](TechDraw_View.md) tool can also create a Projection Group. It is advisable to use that tool instead.

<img alt="" src=images/TechDraw_ProjGroup_example.png  style="width:400px;"> 
*Three orthogonal views and one isometric view of a solid object*



## Применение

See [TechDraw View](TechDraw_View#Usage_Projection_Group_Item_and_Projection_Group.md), but to invoke the tool select the **TechDraw → TechDraw Views → <img src="images/TechDraw_ProjectionGroup.svg" width=16px> Insert Projection Group** option from the menu.



## Свойства

See also: [Property editor](Property_editor.md).

A Projection Group, formally a {{Incode|TechDraw::DrawProjGroup}} object, has the [properties](TechDraw_View#Properties_Part_View.md) that are common to all View types. It also has the following additional properties:

### Data


{{TitleProperty|Base}}

-    **Source|LinkList**: Links to the drawable objects to be depicted.

-    **XSource|XLinkList**: Links to the drawable objects in an external file.

-    **Anchor|Link**: The central view in the group. Normally the Front view.

-    **ProjectionType|Enumeration**: {{Value|First Angle}} or {{Value|Third Angle}}.


{{TitleProperty|Collection}}

-    **Views|LinkList**: Links to the views in this ProjectionGroup.


{{TitleProperty|Distribute}}

-    **Auto Distribute|Bool**: If `True`, space out individual views automatically. Use `False` to position manually.

-    **spacing X|Length**: Horizontal space between views when automatically positioned. Note that Scale and the size of other views in the group also influence the spacing.

-    **spacing Y|Length**: Vertical space between views when automatically positioned.

## Notes

The ProjectionGroup as a whole inherits X, Y, ScaleType, Scale and Rotation from the basic View.

Individual Views within the group inherit all part view properties, but the ProjectionGroup object controls the scale of all its member Views.

The RotationVector property of individual Views within the group is deprecated as of v0.19. Use XDirection instead.

Note that the central box displays the current projection direction of the primary view. It cannot be used to change the direction.



## Программирование


**См. так же:**

[TechDraw API](TechDraw_API/ru.md) и [Основы составления скриптов FreeCAD](FreeCAD_Scripting_Basics/ru.md).

A Projection Group can be created with [macros](Macros.md) and from the [Python](Python.md) console by using the following functions:


```python
import FreeCAD as App

doc = App.ActiveDocument
cyl = doc.addObject("Part::Cylinder", "Cylinder")
doc.recompute()

page = doc.addObject("TechDraw::DrawPage", "Page")
template = doc.addObject("TechDraw::DrawSVGTemplate", "Template")
template.Template = App.getResourceDir() + "Mod/TechDraw/Templates/A4_LandscapeTD.svg"
page.Template = template

# Toggle the visibility of the page to ensure its width and height are updated (hack):
page.Visibility = False
page.Visibility = True

group = doc.addObject("TechDraw::DrawProjGroup", "ProjGroup")
page.addView(group)
group.Source = [cyl]
group.ProjectionType = "Third Angle"

front_view = group.addProjection("Front") # First projection will become the Anchor.
group.Anchor.Direction = (0, 1, 0)
group.Anchor.RotationVector = (1, 0, 0)

left_view = group.addProjection("Left")
top_view = group.addProjection("Top")

group.X = page.PageWidth / 2
group.Y = page.PageHeight / 2

doc.recompute()
```

Note: The Projection Group should always be added to the Page, {{Incode|page.addView(group)}}, before adding projections to the Group. This allows the Projection Group to use default parameter values derived from the parent page.


<div class="mw-translate-fuzzy">





</div>


{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw ProjectionGroup/ru
