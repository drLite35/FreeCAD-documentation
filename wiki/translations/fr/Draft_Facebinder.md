---
 GuiCommand:
   Name: Draft Facebinder
   Name/fr: Draft Surface liée
   MenuLocation: Draft : Formes , Surface liée<br><br>BIM : 3D/BIM , Outils 3D génériques , Surface liée
   Workbenches: Draft_Workbench/fr, BIM_Workbench/fr
   Shortcut: Draft : **F** **F**
   Version: 0.14
---

# Draft Facebinder/fr

## Description

La commande <img alt="" src=images/Draft_Facebinder.svg  style="width:24px;"> **Draft Surface liée** crée un objet surface à partir des faces sélectionnées. Une Draft Surface liée est paramétrique, elle sera mise à jour si vous modifiez son ou ses objets sources.

Elle peut être utilisée pour créer une extrusion à partir d\'une combinaison de surfaces. Cette extrusion peut par exemple représenter une finition de mur dans une conception architecturale.

<img alt="" src=images/Draft_facebinder_example.jpg  style="width:400px;"> 
*Surfaces liées créées à partir des faces de murs*



## Utilisation

1.  Sélectionner une ou plusieurs faces.
2.  Il existe plusieurs façons de lancer la commande :
    -   Appuyer sur le bouton **<img src="images/Draft_Facebinder.svg" width=16px> [Surface liée](Draft_Facebinder/fr.md)**.
    -   [Draft](Draft_Workbench/fr.md) : sélectionner l\'option **Formes → <img src="images/Draft_Facebinder.svg" width=16px> Surface liée** du menu.
    -   [BIM](BIM_Workbench/fr.md) : sélectionner l\'option **3D/BIM → Outils 3D génériques → <img src="images/Draft_Facebinder.svg" width=16px> Surface liée** du menu.
    -   Draft : utiliser le raccourci clavier : **F** puis **F**.



## Propriétés

Voir aussi : [Éditeur de propriétés](Property_editor/fr.md)

Un objet Draft Surface liée est dérivé de [Part Feature](Part_Feature/fr.md) et hérite de toutes ses propriétés. Il possède également les propriétés supplémentaires suivantes :



### Données


{{TitleProperty|Draft}}

-    **Area|Area**: (en lecture seule) spécifie la surface totale des faces liées de la surface liée.

-    **Extrusion|Distance**: spécifie l\'épaisseur d\'extrusion de la surface liée.

-    **Faces|LinkSubList**: spécifie les faces liées de la surface liée.

-    **Offset|Distance**: spécifie une distance de décalage à appliquer entre la lime à facettes et les faces originales, avant l\'extrusion.

-    **Remove Splitter|Bool**: spécifie s\'il faut supprimer les lignes de séparation qui divisent les faces coplanaires de la surface liée.

-    **Sew|Bool**: spécifie s\'il faut effectuer une opération de couture topologique sur la surface liée.



### Vue


{{TitleProperty|Draft}}

-    **Pattern|Enumeration**: spécifie le [Draft Motif](Draft_Pattern/fr.md) avec lequel remplir les surfaces liées. Cette propriété ne fonctionne que si **Display Mode** est {{value|Flat Lines}}.

-    **Pattern Size|Float**: spécifie la taille du [Draft Motif](Draft_Pattern/fr.md).



## Script

Voir aussi : [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) et [FreeCAD Débuter avec les scripts](FreeCAD_Scripting_Basics/fr.md).

Pour créer une Draft Surface liée, utilisez la méthode `make_facebinder` ({{Version/fr|0.19}}) du module Draft. Cette méthode remplace la méthode dépréciée `makeFacebinder`.


```python
facebinder = make_facebinder(selectionset)
```

-   Crée un objet `facebinder` à partir du `selectionset` donné qui est une liste de `SelectionObject` tels que ceux renvoyés par `FreeCADGui.Selection.getSelectionEx()`.
    -   
        `selectionset`
        
        peut aussi être un `PropertyLinkSubList`.

Un `PropertyLinkSubList` est une liste de tuples. Chaque tuple contient comme premier élément un `object` et comme deuxième élément une liste (ou tuple) de chaînes. Ces chaînes indiquent les noms des sous-éléments (faces) de cet objet.


```python
PropertyLinkSubList = [tuple1, tuple2, tuple3, ...]
PropertyLinkSubList = [(object1, list1), (object2, list2), (object3, list3), ...]
PropertyLinkSubList = [(object1, ['Face1', 'Face4', 'Face6']), ...]
PropertyLinkSubList = [(object1, ('Face1', 'Face4', 'Face6')), ...]
```

L\'épaisseur de la surface liée peut être ajoutée en écrasant son attribut `Extrusion`. La valeur est entrée en millimètres.

Le placement de la surface liée peut être modifié en remplaçant son attribut `Placement` ou en écrasant ses attributs `Placement.Base` et `Placement.Rotation`.

Exemple :


```python
import FreeCAD as App
import FreeCADGui as Gui
import Draft

doc = App.newDocument()

# Insert a solid box
box = doc.addObject("Part::Box", "Box")
box.Length = 2300
box.Width = 800
box.Height = 1000

# selection = Gui.Selection.getSelectionEx()
selection = [(box, ("Face1", "Face6"))]
facebinder = Draft.make_facebinder(selection)
facebinder.Extrusion = 50

doc.recompute()

facebinder.Placement.Base = App.Vector(1000, -1000, 100)
facebinder.ViewObject.ShapeColor = (0.99, 0.99, 0.4)

doc.recompute()
```



---
⏵ [documentation index](../README.md) > [Draft](Draft_Workbench.md) > Draft Facebinder/fr
