---
 GuiCommand:
   Name: TechDraw PageTemplate
   Name/fr: TechDraw Page à partir d'un modèle
   MenuLocation: TechDraw , Page , Insérer une page à partir d'un modèle
   Workbenches: TechDraw_Workbench/fr
   SeeAlso: TechDraw_PageDefault/fr, TechDraw_Templates/fr
---

# TechDraw PageTemplate/fr

## Description

L\'outil **TechDraw Page à partir d\'un modèle** crée un nouvel objet Page à l\'aide du fichier de modèle sélectionné dans une boîte de dialogue.

Le répertoire de départ de la fenêtre de dialogue peut être spécifié dans les [TechDraw Préférences](TechDraw_Preferences/fr.md).

<img alt="" src=images/A4_Landscape_ISO7200_Pep.svg  style="width:400px;"> 
*L'un des modèles fournis avec TechDraw : A4_Landscape_ISO7200_Pep.svg*



## Utilisation

1.  Un document actif doit exister.
2.  Il y a plusieurs façons de lancer l\'outil :
    -   Appuyez sur le bouton **<img src="images/TechDraw_PageTemplate.svg" width=16px> [Insérer une page à partir d'un modèle](TechDraw_PageTemplate/fr.md)**.
    -   Sélectionnez l\'option **TechDraw → Page → <img src="images/TechDraw_PageTemplate.svg" width=16px> Insérer une page à l'aide d'un modèle** du menu.



## Propriétés

Voir [TechDraw Page par défaut](TechDraw_PageDefault/fr#Propri.C3.A9t.C3.A9s.md).



## Script

Voir aussi : [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) et [Débuter avec les scripts](FreeCAD_Scripting_Basics/fr.md).

Une Page peut être créée à partir de [macros](Macros/fr.md) et à partir de la console [Python](Python/fr.md) à l\'aide des fonctions suivantes :


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



### Champs de texte éditables 


**Voir aussi :**

[TechDraw Modèles](TechDraw_Templates/fr.md) pour plus d\'informations sur la création de modèles.

Une fois qu\'une nouvelle page a été créée, son attribut `Template` contient un dictionnaire `EditableTexts` avec le nom des champs modifiables (keys) et leurs valeurs textuelles. Copiez ce dictionnaire dans une variable, apportez des modifications, puis réaffectez le dictionnaire à l\'attribut `EditableTexts` pour afficher les modifications.


```python
page = FreeCAD.ActiveDocument.Page
texts = page.Template.EditableTexts

for key, value in texts.items():
    print("{0} = {1}".format(key, value))

texts["FC-Title"] = "The title of my page"
page.Template.EditableTexts = texts
```





{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw PageTemplate/fr
