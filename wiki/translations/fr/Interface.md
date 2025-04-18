# Interface/fr
## Introduction

L'[interface](interface/fr.md) FreeCAD est basée sur Qt, un toolkit d'interface utilisateur graphique bien connu, particulièrement utilisé sous Linux mais également disponible sous Windows et MacOS.

<img alt="" src=images/FreeCAD_interface_base_divisions.svg  style="width:1024px;">



*Interface standard dans v0.19.*

La fenêtre principale de l\'application peut être grossièrement divisée en 11 sections :

1.  La [zone de vue principale](main_view_area/fr.md) qui peut contenir différentes fenêtres à onglets
2.  La [vue 3D](3D_view/fr.md) normalement intégrée dans la [zone de vue principale](main_view_area/fr.md)
3.  La partie supérieure de la [vue combinée](Combo_view/fr.md) qui comprend la [vue en arborescence](Tree_view/fr.md) et le [panneau des tâches](Task_Panel/fr.md)
4.  La partie inférieure de la [vue combinée](Combo_view/fr.md) qui comprend l\'[éditeur de propriétés](Property_editor/fr.md)
5.  La [fenêtre de sélection](selection_view/fr.md)
6.  La [vue rapport](Report_view/fr.md)
7.  La [console Python](Python_console/fr.md)
8.  La [barre d\'état](status_bar/fr.md)
9.  La zone de la barre d\'outils, voir les informations suivantes sur les barres d\'outils
10. Le [sélecteur d\'atelier](Std_Workbench/fr.md) qui est lui-même une barre d\'outils
11. Le [menu standard](Standard_Menu/fr.md)



## Composants de l\'interface 

Comme beaucoup de logiciels, FreeCAD comprend une barre de menu standard, puis une série de barres d\'outils et de panneaux où se trouvent les outils de l\'utilisateur.

### Menus

Les [menus standard](Standard_Menu/fr.md) sont : {{StdMenu|[**Fichier**](Std_File_Menu/fr.md)}}, {{StdMenu|[**Édition**](Std_Edit_Menu/fr.md)}}, {{StdMenu|[**Affichage**](Std_View_Menu/fr.md)}}, {{StdMenu|[**Outils**](Std_Tools_Menu/fr.md)}}, {{StdMenu|[**Macro**](Std_Macro_Menu/fr.md)}}, {{StdMenu|[**Fenêtre**](Std_Windows_Menu/fr.md)}}, {{StdMenu|[**Aide**](Std_Help_Menu/fr.md)}}.



### Barres d\'outils 

Les barres d\'outils standard qui apparaissent dans l\'interface sont :

-   Barre d'outils Fichier : outils pour travailler avec des fichiers, ouvrir des documents, copier, coller, annuler et rétablir des actions.
-   [Barre d'outils Ateliers](Std_Workbench/fr.md) : contient un seul widget pour sélectionner l\'[atelier](workbenches/fr.md) actif.
-   Barre d'outils Macro : outils pour enregistrer, éditer et exécuter [macros](Macros/fr.md).
-   Barre d'outils Vue : outils permettant de contrôler l'apparence des objets dans la [vue 3D](3D_view/fr.md).
-   Barre d\'outils Structure : outils pour organiser les objets dans le document et créer des liens vers des documents supplémentaires.

Celles-ci peuvent être activées ou désactivées en cliquant avec le bouton droit de la souris sur un espace vide de l\'une des barres d\'outils et en choisissant l\'élément souhaité ou par le menu **Affichage → Barres d'outils**.



### Panneaux

Les panneaux principaux permettant de travailler avec des objets sont :

-   [Vue 3D](3D_view/fr.md) : la zone où la géométrie 2D et 3D est dessinée.
-   [Vue combinée](Combo_view/fr.md) : le panneau qui contient la [vue en arborescence](Tree_view/fr.md), le [panneau de tâches](Task_panel/fr.md), et l\'[éditeur de propriété](Property_editor/fr.md).
-   [Vue en arborescence](Tree_view/fr.md): l\'élément qui montre tous les objets du document et leur historique paramétrique.
-   [Panneau de tâches](Task_panel/fr.md) : panneau affichant différentes actions et options en fonction de l\'outil de dessin sélectionné.
-   [Éditeur de propriétés](Property_editor/fr.md) : l\'endroit où les propriétés de l\'objet sont modifiées.
-   [Vue de sélection](Selection_view/fr.md) : panneau affichant les éléments actuellement sélectionnés.
-   [Vue rapport](Report_view/fr.md) : la zone de texte contenant différents messages de l\'application et de ses outils.
-   [Console Python](Python_console/fr.md) : l\'éditeur qui permet de lancer le code de manière interactive dans la console [Python](Python/fr.md) pour voir les résultats dans la [vue 3D](3D_view/fr.md).
-   [Barre d\'état](Status_bar/fr.md) : la barre qui montre certains messages de l\'application et qui a le sélecteur pour la [navigation par la souris](Mouse_navigation/fr.md).
-   [Vue DAG](DAG_view/fr.md): une alternative à la [vue en arborescence](Tree_view/fr.md), qui montre les relations entre différents objets graphiquement.

À l\'exception de la vue 3D, tout peut être activé ou désactivé en cliquant avec le bouton droit de la souris sur un espace vide de l\'une des barres d\'outils supérieures et en choisissant l\'élément souhaité ou par le menu **Affichage → Panneaux**.

Pour activer et désactiver la barre d\'état utiliser le menu, **Affichage → Barre d'état**.



### Autre

Les autres interfaces et fenêtres utiles incluent :

-   [Inspecteur de scène‏‎](Std_SceneInspector/fr.md) : panneau affichant les nœuds Coin3D constituant le [graphe de scène](Scenegraph/fr.md). Pour les utilisateurs expérimentés et les développeurs, il peut être utile de résoudre les opérations manipulant directement la scène et les objets créés dans la [vue 3D](3D_view/fr.md).
-   [Graphe des dépendances](Std_DependencyGraph/fr.md) : une fenêtre affichant le graphe des dépendances de tous les objets du document, créée à l\'aide du programme auxiliaire [Graphviz](https://graphviz.org/). Il est utile de reconnaître les problèmes liés à la création d\'objets, tels que les dépendances circulaires, qui peuvent ne pas être totalement évidents dans la [vue en arborescence](Tree_view/fr.md) ou de la [vue DAG](DAG_view/fr.md).



### Personnalisation

Les barres d'outils peuvent avoir plus ou moins de boutons, et des barres d'outils personnalisées peuvent être créées avec un mélange de différents outils et pour stocker des macros développées.

Ces options sont dans le menu, **Outils → Personnaliser...**. Voir [Personnalisation de l\'interface](Interface_Customization/fr.md).


{{Interface navi

}}



---
⏵ [documentation index](../README.md) > Interface/fr
