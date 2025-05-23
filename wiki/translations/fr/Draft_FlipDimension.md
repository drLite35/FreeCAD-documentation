---
 GuiCommand:
   Name: Draft FlipDimension
   Name/fr: Draft Inverser le texte de la dimension
   MenuLocation: Modification , Inverser le texte de la dimension
   Workbenches: Draft_Workbench/fr
---

# Draft FlipDimension/fr

## Description

La commande <img alt="" src=images/Draft_FlipDimension.svg  style="width:24px;"> **Draft Inverser le texte de la dimension** fait pivoter le texte de la dimension d\'une [Draft Dimension](Draft_Dimension/fr.md) sélectionnée de 180° autour de la ligne de la dimension. Elle peut être utilisée pour corriger les dimensions dont le texte apparaît en miroir. La commande ne fonctionne pas correctement pour les dimensions angulaires.



## Utilisation

1.  Sélectionner une ou plusieurs [Draft Dimensions](Draft_Dimension/fr.md).
2.  Il existe plusieurs façons de lancer la commande :
    -   Appuyer sur le bouton **<img src="images/Draft_FlipDimension.svg" width=16px> [Inverser le texte de la dimension](Draft_FlipDimension/fr.md)**.
    -   Sélectionner l\'option **Modification → <img src="images/Draft_FlipDimension.svg" width=16px> Inverser le texte de la dimension** du menu.



## Remarques

-   Les [Draft Dimensions](Draft_Dimension/fr.md) possèdent également une propriété **Flip Text**. Lorsqu\'elle est mise à `True`, le texte est tourné de 180° autour de la direction normale. Ceci peut être combiné avec l\'effet de cette commande.



## Script

Voir aussi : [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) et [FreeCAD Débuter avec les scripts](FreeCAD_Scripting_Basics/fr.md).

Pour inverser une [Draft Dimension](Draft_Dimension/fr.md), inversez sa propriété `Normal`.

Exemple :


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

p1 = App.Vector(0, 0, 0)
p2 = App.Vector(1000, 0, 0)
p3 = App.Vector(500, 300, 0)
dimension = Draft.make_dimension(p1, p2, p3)
dimension.ViewObject.FontSize = 200

dimension.Normal = dimension.Normal.negative()
doc.recompute()
```



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft FlipDimension/fr
