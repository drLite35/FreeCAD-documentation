---
 GuiCommand:
   Name: Surface Sections
   Name/fr: Surface Sections
   MenuLocation: Surface , Sections...
   Workbenches: Surface_Workbench/fr
   Version: 0.19
---

# Surface Sections/fr

## Description


**[<img src=images/Surface_Sections.svg style="width:16px"> [Surface Sections](Surface_Sections/fr.md)**

est utilisé pour créer une surface à partir d\'arêtes qui représentent des sections transversales d\'une surface.

<img alt="" src=images/Surface_Sections_edges_example.png  style="width:" height="250px;"> <img alt="" src=images/Surface_Sections_example.png  style="width:" height="250px;">



*À gauche : les arêtes de contrôle (coupes transversales). À droite : la surface produite à partir de ces arêtes.*



## Utilisation

1.  Assurez-vous d\'avoir au moins deux arêtes ou courbes dans l\'espace. Par exemple, ceux-ci peuvent être créés avec des outils de l\'<img alt="" src=images/Workbench_Draft.svg  style="width:24px;"> [atelier Draft](Draft_Workbench/fr.md) ou de l\'<img alt="" src=images/_Workbench_Sketcher.svg  style="width:24px;"> [atelier Sketcher](Sketcher_Workbench/fr.md).
2.  Appuyez sur le bouton **[<img src=images/_Surface_Sections.svg style="width:16px"> [Surface sections](Surface_Sections/fr.md)**.
3.  Appuyez sur **Ajouter une arête**.
4.  Utilisez le pointeur pour sélectionner les arêtes souhaitées dans la [vue 3D](3D_view/fr.md). Un aperçu de la forme finale sera affiché après avoir sélectionné deux arêtes valides.
5.  Appuyez sur **OK** pour terminer l\'opération.

## Options

-    **Ajouter une arête**: appuyez une fois pour commencer à choisir les arêtes dans la [vue 3D](3D_view/fr.md). Chaque ligne telle que les **[<img src=images/Draft_BSpline.svg style="width:16px"> [Draft B-splines](Draft_BSpline/fr.md)** et les **[<img src=images/Sketcher_CreateBSpline.svg style="width:16px"> [Sketcher B-splines](Sketcher_CreateBSpline/fr.md)** peut être choisie ainsi que n\'importe quelle arête des objets solides, comme celles de **[<img src=images/PartDesign_Body.svg style="width:16px"> [PartDesign Corps](PartDesign_Body/fr.md)** et de **[<img src=images/Part_Primitives.svg style="width:16px"> [Part Primitives](Part_Primitives/fr.md)**.

-    **Supprimer une arête**: appuyez une fois pour commencer à choisir les arêtes dans la [vue 3D](3D_view/fr.md). Celles-ci doivent être des arêtes précédemment sélectionnées avec **Ajouter une arête**.

-    **Bouton droit de la souris**: ouvrez le menu contextuel et sélectionnez **Supprimer** ou appuyez sur **Suppr** au clavier pour supprimer l\'arête sélectionné dans la liste.

-    **Glisser**: faites glisser l\'élément sélectionné dans la liste afin de changer l\'ordre dans lequel il sera traité. La liste est traitée de haut en bas.

-   Appuyez sur **Annuler** ou **Échap** pour abandonner l\'opération en cours.



## Propriétés

Les [Surface Sections](Surface_Sections/fr.md) (classe `Surface::Sections`) sont dérivées de la classe de base [Part Feature](Part_Feature/fr.md) (classe `Part::Feature` via la sous-classe `Part::Spline`). Elles partagent donc toutes les propriétés de cette dernière.

Outre les propriétés décrites dans [Part Feature](Part_Feature/fr.md), Surface Section a les propriétés suivantes dans l\'[éditeur de propriétés](Property_editor/fr.md).



### Données


{{TitleProperty|Sections}}

-    {{PropertyData/fr|NSections|LinkSubList}}: une liste d\'arêtes qui seront utilisées pour construire la surface.



### Vue


{{TitleProperty|Base}}

-    **Control Points|Bool**: par défaut `False`. Mis à `True`, elle affichera une superposition avec les points de contrôle de la surface.



## Torsion de la surface 

La forme de la surface dépend de la direction des arêtes choisies. Si des arêtes sont sélectionnées et que le résultat est une surface qui \"se tord\" sur elle-même, l\'une des arêtes peut avoir besoin de sa liste de sommets dans l\'ordre inverse. Voir les informations dans **[<img src=images/Surface_GeomFillSurface.svg style="width:16px"> [Surface Remplir entre les courbes limites](Surface_GeomFillSurface/fr.md)** pour une explication plus complète.

<img alt="" src=images/Surface_twisting_example_smooth.png  style="width:330px;"> <img alt="" src=images/Surface_twisting_example_twisted.png  style="width:330px;">



## Script


**Voir aussi :**

[FreeCAD Script de base](FreeCAD_Scripting_Basics/fr.md).

L\'outil Surface Sections peut être utilisé dans des [macros](Macros/fr.md) et depuis la console [Python](Python/fr.md) en ajoutant l\'objet `Surface::Sections`.

-   Les arêtes à utiliser pour définir la surface doivent être affectées en tant que [LinkSubList](FeaturePython_Custom_Properties/fr#App:_PropertyLinkSubList.md) à la propriété `NSections` de l\'objet.
-   Tous les objets avec des arêtes doivent être calculés avant de pouvoir être utilisés comme entrée pour les propriétés de l\'objet Sections.


```python
import FreeCAD as App
import Draft

doc = App.newDocument()

pl1 = App.Placement()
obj1 = Draft.make_circle(50, placement=pl1, face=False, startangle=0, endangle=180)

pl2 = App.Placement(App.Vector(0, 0, 25), App.Rotation())
obj2 = Draft.make_circle(30, placement=pl2, face=False, startangle=0, endangle=180)

points3 = [App.Vector(18, -10, 50),
           App.Vector(12, 10, 50),
           App.Vector(-12, 10, 50),
           App.Vector(-18, -10, 50)]
obj3 = Draft.make_bspline(points3)

points4 = [App.Vector(15, -20, 100),
           App.Vector(0, 6, 100),
           App.Vector(-15, -20, 100)]
obj4 = Draft.make_bspline(points4)
doc.recompute()

surf = doc.addObject("Surface::Sections", "Surface")
surf.NSections = [(obj1, "Edge1"),
                  (obj2, "Edge1"),
                  (obj3, "Edge1"),
                  (obj4, "Edge1")]
doc.recompute()
```





{{Surface Tools navi

}}



---
⏵ [documentation index](../README.md) > [Surface](Surface_Workbench.md) > Surface Sections/fr
