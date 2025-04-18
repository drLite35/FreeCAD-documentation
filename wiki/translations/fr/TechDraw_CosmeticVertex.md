---
 GuiCommand:
   Name: TechDraw CosmeticVertex
   Name/fr: TechDraw Point cosmétique
   MenuLocation: TechDraw , Ajouter des sommets , Ajouter un sommet cosmétique
   Workbenches: TechDraw_Workbench/fr
   Version: 0.19
   SeeAlso: TechDraw_Midpoints/fr, TechDraw_Quadrants/fr
---

# TechDraw CosmeticVertex/fr

## Description

L\'outil **TechDraw Point cosmétique** ajoute un [Vertex](Glossary/fr#V.md) (sommet) qui ne fait pas partie de la géométrie d\'origine à une vue. Ce point se comporte comme n\'importe quel autre point et peut être utilisé pour le dimensionnement.

<img alt="" src=images/TechDraw_CosmeticVertex_Sample.png  style="width:300px;"> 
*Point cosmétique utilisé pour créer une dimension supplémentaire*



## Utilisation

1.  Sélectionnez une vue.
2.  Il y a plusieurs façons de lancer l\'outil :
    -   Appuyez sur le bouton **<img src="images/TechDraw_CosmeticVertex.svg" width=16px> [Add Cosmetic Vertex](TechDraw_CosmeticVertex.md)**.
    -   Sélectionnez l\'option **TechDraw → Ajouter des sommets → <img src="images/TechDraw_CosmeticVertex.svg" width=16px> Ajouter un sommet cosmétique** dans le menu.
3.  Un panneau de tâches s\'ouvre.
4.  Appuyez sur le bouton **Sélectionneur de points** et choisissez un point sur la page. Appuyez sur le bouton **Annuler la sélection** pour annuler cette opération.
5.  Modifiez ou spécifiez les coordonnées X et Y du point. Les coordonnées sont relatives au centre de la vue.
6.  Appuyez sur le bouton **OK**.



## Remarques

-   Vous ne pouvez pas modifier la position d\'un sommet cosmétique existant. Pour l\'instant, il n\'y a pas d\'autre moyen que de le supprimer et d\'en créer un nouveau.



## Propriétés

Les points cosmétiques n\'ont pas de propriétés propres car ils ne sont pas des objets du document. Ils partagent les paramètres de couleur et de taille avec des points de géométrie réguliers.



## Script

Voir aussi : [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) et [FreeCAD Débuter avec les scripts](FreeCAD_Scripting_Basics/fr.md).

Les points cosmétiques sont accessibles par les [macros](Macros/fr.md) ou par la console [Python](Python/fr.md).


```python
dvp = App.ActiveDocument.View
org = App.Vector(0.0, 0.0, 0.0)
dvp.makeCosmeticVertex(org);

#lines too!
start = FreeCAD.Vector (1.0, 5.0, 0.0)
end = FreeCAD.Vector(1.0, -5.0, 0.0)
style = 2
weight = 0.75
pyGreen = (0.0, 0.0, 1.0, 0.0)
dvp.makeCosmeticLine(start,end,style, weight, pyGreen)
```





{{TechDraw Tools navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw CosmeticVertex/fr
