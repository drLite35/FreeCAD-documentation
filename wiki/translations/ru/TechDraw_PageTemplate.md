---
 GuiCommand:
   Name/ru: Вставить страницу используя шаблон
   Name: TechDraw_PageTemplate
   MenuLocation: TechDraw , Вставить страницу используя шаблон
   Workbenches: TechDraw_Workbench/ru
   SeeAlso: TechDraw_PageDefault/ru, TechDraw_Templates/ru
---

# TechDraw PageTemplate/ru


</div>



## Описание

The **TechDraw PageTemplate** tool creates a new Page object using the template file selected from a dialog.

The starting directory for the dialog can be specified in the [TechDraw Preferences](TechDraw_Preferences.md).

<img alt="" src=images/A4_Landscape_ISO7200_Pep.svg  style="width:400px;"> 
*One of the templates that comes with TechDraw: A4_Landscape_ISO7200_Pep.svg*



## Применение

1.  An active document must exist.
2.  There are several ways to invoke the tool:
    -   Press the **<img src="images/TechDraw_PageTemplate.svg" width=16px> [Insert Page using Template](TechDraw_PageTemplate.md)** button.
    -   Select the **TechDraw → Page → <img src="images/TechDraw_PageTemplate.svg" width=16px> Insert Page using Template** option from the menu.



## Свойства

See [TechDraw PageDefault](TechDraw_PageDefault#Properties.md).



## Программирование


**См. так же:**

[TechDraw API](TechDraw_API/ru.md) и [Основы составления скриптов FreeCAD](FreeCAD_Scripting_Basics/ru.md).

A Page based on a selected template can be created with [macros](Macros.md) and from the [Python](Python.md) console by using the following functions:


```python
import FreeCAD as App
from PySide import QtGui

doc = App.ActiveDocument
default_dir = App.getResourceDir() + "Mod/TechDraw/Templates"
param = App.ParamGet("User parameter:BaseApp/Preferences/Mod/TechDraw/Files")
template_dir = param.GetString("TemplateDir", default_dir)

template_file = QtGui.QFileDialog.getOpenFileName(QtGui.QApplication.activeWindow(),
                                                  "Select a Template File", 
                                                  template_dir,
                                                  "Template (*.svg)")
                                                  
page = doc.addObject("TechDraw::DrawPage", "Page")
template = doc.addObject("TechDraw::DrawSVGTemplate", "Template")
template.Template = template_file[0]
page.Template = template

doc.recompute()
```

### Editable text fields 


**See also:**

[TechDraw Templates](TechDraw_Templates.md) for more information on creating templates.

Once a new page has been created, its `Template` attribute holds an `EditableTexts` dictionary with the name of the editable fields (keys) and their textual values. Copy this dictionary to a variable, make changes, and then re-assign the dictionary to the `EditableTexts` attribute to see the changes.


```python
page = FreeCAD.ActiveDocument.Page
texts = page.Template.EditableTexts

for key, value in texts.items():
    print("{0} = {1}".format(key, value))

texts["FC-Title"] = "The title of my page"
page.Template.EditableTexts = texts
```


<div class="mw-translate-fuzzy">





</div>


{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw PageTemplate/ru
