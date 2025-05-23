---
 GuiCommand:
   Name: Arch Truss
   Name/fr: Arch Treillis
   MenuLocation: 3D/BIM , Treillis
   Workbenches: BIM_Workbench/fr
   Version: 0.19
---

# Arch Truss/fr

## Description

L\'outil **Arch Treillis** crée un objet [Treillis](https://fr.wikipedia.org/wiki/Treillis_(assemblage)) à partir d\'un objet linéaire sélectionné (positionnez une [Draft Ligne](Draft_Line/fr.md) ou [Sketcher Esquisse](Sketcher_NewSketch/fr.md)) ou à partir de zéro, si aucun objet n\'est sélectionné lors du lancement de la commande.

<img alt="" src=images/Arch_Truss_example.png  style="width:600px;">



## Utilisation



### Création à partir d\'un objet sélectionné 

1.  Utilisez l\'atelier de votre choix pour créer une seule ligne
2.  Sélectionnez cette ligne
3.  Appuyez sur le bouton **<img src="images/Arch_Truss.svg" width=16px> [Treillis](Arch_Truss/fr.md)
**
4.  Ajustez les propriétés du treillis à votre convenance



### Création à partir de zéro 

1.  Assurez-vous que rien n\'est sélectionné
2.  Appuyez sur le bouton **<img src="images/Arch_Truss.svg" width=16px> [Treillis](Arch_Truss/fr.md)
**
3.  Cliquez dans la vue 3D pour définir un premier point ou entrez manuellement les coordonnées X, Y et Z
4.  Cliquez dans la vue 3D pour définir un deuxième point ou entrez manuellement les coordonnées X, Y et Z
5.  Ajustez les propriétés du treillis à votre convenance



## Propriétés



### Données

-    **TrussAngle**: angle du treillis

-    **SlantType**: type d\'inclinaison du treillis

-    **Normal**: direction normale du treillis

-    **HeightStart**: hauteur du treillis à la position de départ

-    **HeightEnd**: hauteur du treillis à la position finale

-    **StrutStartOffset**: décalage de démarrage facultatif pour la jambe de force supérieure

-    **StrutEndOffset**: décalage de fin facultatif pour la jambe supérieure

-    **StrutHeight**: hauteur des principaux éléments supérieur et inférieur du treillis

-    **StrutWidth**: largeur des principaux éléments supérieur et inférieur du treillis

-    **RodType**: type de l\'élément central du treillis

-    **RodDirection**: direction des membrures

-    **RodSize**: diamètre ou côté des membrures

-    **RodSections**: nombre de sections des membrures

-    **RodEnd**: si le treillis a une membrure à son extrémité ou non

-    **RodMode**: comment dessiner les membrures



## Script

L\'outil Treillis peut être utilisé dans une [macro](Macros/fr.md) et à partir de la console [Python](Python/fr.md) en utilisant la fonction suivante :


```python
Truss = makeFence([baseobj])
```

Exemple :


```python
import FreeCAD
import Draft
import Arch

p1 = FreeCAD.Vector(0,0,0)
p2 = FreeCAD.Vector(2000,0,0)
baseline = Draft.makeLine(p1,p2)
truss = Arch.makeTruss(baseline)
truss.HeightStart = 200
truss.HeightEnd = 400
# adjust other needed properties
```



---
⏵ [documentation index](../README.md) > [BIM](Category_BIM.md) > Arch Truss/fr
