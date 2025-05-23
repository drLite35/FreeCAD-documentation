---
 GuiCommand:
   Name: Arch Floor
   Name/fr: Arch Niveau
   MenuLocation: 3D/BIM , Niveau
   Workbenches: BIM_Workbench/fr
   Shortcut: **L** **V**
   SeeAlso: 
---

# Arch Floor/fr

## Description

L\'outil **Arch Niveau** est un type spécial d\'objet de groupe de FreeCAD qui possède quelques propriétés supplémentaires particulièrement adaptées pour la construction de niveaux. Ils ont en particulier une propriété hauteur, que ses objets enfants ([Arch Murs](Arch_Wall/fr.md) et [Arch Structures](Arch_Structure/fr.md)) peuvent utiliser pour définir automatiquement leur propre hauteur. Ils sont principalement utilisés pour organiser votre modèle.

À partir de {{VersionPlus/fr|0.18}}, Arch Niveau est entièrement dérivé de l\'objet [Arch Partie de bâtiment](Arch_BuildingPart/fr.md) qui est un conteneur général permettant d\'organiser un modèle de construction ne se limitant pas aux niveaux ou aux étages. Les anciens objets Floor peuvent être convertis dans le nouveau type en cliquant dessus avec le bouton droit de la souris et en choisissant `Convert to BuildingPart`.



## Utilisation

1.  Sélectionnez un ou plusieurs objets que vous voulez inclure dans votre nouveau niveau.
2.  Lancez la commande Arch Niveau de plusieurs manières :
    -   En appuyant sur le bouton **<img src="images/Arch_Floor.svg" width=16px> [Niveau](Arch_Floor/fr.md)** dans la barre d\'outils.
    -   Utilisation des touches **L** puis **V**.
    -   Utilisation de l\'entrée **3D/BIM → Niveau** du menu supérieur.

## Options

-   Après la création d\'un niveau, vous pouvez ajouter un ou plusieurs objets que vous pouvez copier/coller dans l\'arborescence ou en utilisant l\'outil **<img src="images/Arch_Add.svg" width=16px> [Arch Ajouter un composant](Arch_Add/fr.md)**.
-   Vous pouvez supprimer des objets d\'un niveau en les faisant glisser et en les déposant dans l\'arborescence ou en utilisant l\'outil **<img src="images/Arch_Remove.svg" width=16px> [Arch Supprimer un composant](Arch_Remove/fr.md)**.



## Propriétés

Un objet Niveau partage toutes les propriétés d\'un objet [Arch Partie de bâtiment](Arch_BuildingPart/fr.md) avec **Ifc Type** défini sur `"Building Storey"`.



## Script


**Voir aussi :**

[Arch API](Arch_API/fr.md) et [Débuter avec les scripts FreeCAD](FreeCAD_Scripting_Basics/fr.md).

L\'outil Niveau peut être utilisé dans une [macro](Macros/fr.md) ainsi que dans la console [Python](Python/fr.md) en utilisant la commande :


```python
Floor = makeFloor(objectslist=None, baseobj=None, name="Floor")
```

-   Crée un objet `Floor` à partir de `objectlist` qui est une liste d\'objets.

Exemple :


```python
import FreeCAD, Draft, Arch

p1 = FreeCAD.Vector(0, 0, 0)
p2 = FreeCAD.Vector(2000, 0, 0)
baseline = Draft.makeLine(p1, p2)
baseline2 = Draft.makeLine(p1, -1*p2)

Wall1 = Arch.makeWall(baseline, length=None, width=150, height=2000)
Wall2 = Arch.makeWall(baseline2, length=None, width=150, height=1800)
FreeCAD.ActiveDocument.recompute()

Floor = Arch.makeFloor([Wall1, Wall2])

Building = Arch.makeBuilding([Floor])
Site = Arch.makeSite(Building)
FreeCAD.ActiveDocument.recompute() 
```



---
⏵ [documentation index](../README.md) > [BIM](Category_BIM.md) > Arch Floor/fr
