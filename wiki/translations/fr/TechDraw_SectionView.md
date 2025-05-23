---
 GuiCommand:
   Name: TechDraw SectionView
   Name/fr: TechDraw Vue en coupe
   MenuLocation: TechDraw , Vues de Techdraw , Insérer une vue en coupe
   Workbenches: TechDraw_Workbench/fr
   SeeAlso: TechDraw_ComplexSection/fr, TechDraw_View/fr
---

# TechDraw SectionView/fr

## Description

L\'outil **TechDraw Vue en coupe** insère une vue en coupe transversale basée sur une vue de la pièce existante.

<img alt="" src=images/TechDraw_section_ANSI.png  style="width:350px;">
<img alt="" src=images/TechDraw_section_ISO.png  style="width:350px;"> 
*Vue en coupe déjà placée qui montre les trous internes et une surface de coupe hachurée.<br>
L'image du haut montre le format de flèche ANSI.<br>
L'image du bas montre le format de flèche ISO.*



## Utilisation

1.  Sélectionnez une vue de la pièce dans la [vue 3D](3D_view/fr.md) ou la [vue en arborescence](Tree_view/fr.md).
2.  Il existe plusieurs façons de lancer l\'outil :
    -   Appuyez sur le bouton **<img src="images/TechDraw_SectionView.svg" width=16px> [Insérer une vue en coupe](TechDraw_SectionView/fr.md)**.
    -   Sélectionnez l\'option **TechDraw → Vues de Techdraw → <img src="images/TechDraw_SectionView.svg" width=16px> Insérer une vue en coupe** du menu.
3.  Un panneau de tâches s\'ouvre et vous aide à calculer les différentes propriétés. Des valeurs raisonnables pour la direction de la vue sont calculées, mais elles peuvent être modifiées.

![](images/TechDraw_Section_Taskview.png ) 
*Fenêtre de dialogue pour définir la zone de la vue en coupe*



## Propriétés

Voir aussi : [Éditeur de propriétés](Property_editor/fr.md)

Dans les propriétés de **Base View**, vous pouvez modifier l\'apparence de la ligne de la coupe.

Une vue de coupe, en fait un objet {{Incode|TechDraw::DrawViewSection}}, est dérivée d\'une [vue de Part](TechDraw_View/fr#Propriétés_Vue_de_Part.md), objet {{Incode|TechDraw::DrawViewPart}}, et hérite de toutes ses propriétés. Elle possède également les propriétés supplémentaires suivantes :



### Données


{{TitleProperty|Appearance}}

-    **Section Line Stretch|FloatConstraint**: ajuste la longueur de la ligne de la coupe. {{Value|1.0}} est la longueur normale, {{Value|1.1}} serait 10% plus longue, {{Value|0.9}} serait 10% plus courte. {{Version/fr|1.0}}


{{TitleProperty|Cut Operation}}

-    **Fuse Before Cut|Bool**: fusionne les formes sources avant d\'effectuer la coupe de section.

-    **Trim After Cut|Bool**: découpe la forme résultante après le découpage de section pour supprimer les morceaux indésirables. {{Version/fr|0.21}}

-    **Use Previous Cut|Bool**: permet d\'utiliser la forme découpée dans la vue de base au lieu de l\'objet original. {{Version/fr|1.0}}


{{TitleProperty|Cut Surface Format}}

-    **Cut Surface Display|Enumeration**: apparence de la surface de coupe. Options :

    -   
        {{Value|Hide}}
        
        : masque la surface découpée, seul le contour sera affiché.

    -   
        {{Value|Color}}
        
        : colore la surface de coupe en utilisant le paramètre **Cut Surface Color** dans les [TechDraw Préférences](TechDraw_Preferences/fr.md).

    -   
        {{Value|SvgHatch}}
        
        : hachure la section coupée en utilisant une [Hachure](TechDraw_Hatch/fr.md).

    -   
        {{Value|PatHatch}}
        
        : hachure la coupe de section en utilisant une [Hachure géométrique](TechDraw_GeometricHatch/fr.md).

-    **File Hatch Pattern|File**: chemin complet vers le fichier de motif de hachures SVG.

-    **File Geom Pattern|File**: chemin complet du fichier de motif PAT.

-    **Svg Included|FileIncluded**: chemin complet vers le fichier de motif de hachures SVG inclus.

-    **Pat Included|FileIncluded**: chemin complet vers le fichier de modèle PAT inclus.

-    **Name Geom Pattern|String**: nom du modèle PAT à utiliser.

-    **Hatch Scale|Float**: réglage de la taille du motif de hachures.

-    **Hatch Rotation|Float**: rotation du motif de hachure en degrés dans le sens anti-horaire. {{Version/fr|0.21}}

-    **Hatch Offset|Vector|Hidden**: décalage du motif de hachure. {{Version/fr|0.21}}


{{TitleProperty|Section}}

-    **Section Symbol|String**: identifiant de cette section.

-    **Base View|Link**: vue sur laquelle est basée cette section.

-    **Section Normal|Vector**: vecteur décrivant la direction normale au plan de coupe.

-    **Section Origin|Vector**: vecteur décrivant un point sur le plan de coupe. Généralement le centroïde de la pièce d\'origine.

-    **Section Direction|Enumeration**: direction dans la vue de base pour cette section. Options : {{Value|Aligned}}, {{Value|Right}}, {{Value|Left}}, {{Value|Up}} ou {{Value|Down}}.



### Vue


{{TitleProperty|Cut Surface}}

-    **Cut Surface Color|Color**: couleur solide pour la mise en évidence de la surface. Utilisé si **Cut Surface Display** est défini sur {{Value|Color}}.

-    **Show Cut Surface|Bool|Hidden**: affiche/masque la surface de coupe.


{{TitleProperty|Surface Hatch}}

-    **Geom Hatch Color|Color**: couleur du motif de hachures géométriques.

-    **Hatch Color|Color**: couleur du motif de hachures Svg.

-    **Hatch Cut Surface|Bool|Hidden**: permet de hachurer la surface de coupe.

-    **Weight Pattern|Float**: poids de ligne du motif de hachures géométriques.



## Remarques

-   **Section Line Format** : deux formats de ligne de section sont pris en charge (comme illustré ci-dessus) et contrôlés par le paramètre de préférence \"Norme de ligne de section\" dans l\'onglet Annotation. L\'option {{Value|ANSI}} utilise des \"flèches tirées\" (connues sous le nom de \"format traditionnel\" dans certains domaines) et l\'option {{Value|ISO}} utilise des \"flèches poussées\" (également connues sous le nom de \"format de la flèche de référence\").
-   **Fuse Before Cut** : l\'opération de coupe échoue parfois à découper les formes sources. Si **Fuse Before Cut** est vrai, les formes sources sont fusionnées en une seule forme avant que l\'opération de section ne soit tentée. Si vous rencontrez des problèmes avec l\'opération de section, essayez d\'inverser cette valeur.
-   **Trim After Cut** : l\'opération d\'ajustement de la coupe laisse parfois derrière elle une partie de la forme source. Si **Trim After Cut** est vrai, une opération d\'ajustement supplémentaire est effectuée sur le résultat de le premier ajustement qui devrait enlever tous les morceaux non désirés.
-   **Cut Surface Display**: la surface de coupe peut être cachée, peinte dans une couleur solide, hachurée en utilisant un motif Svg (par défaut) ou hachurée en utilisant un motif PAT. Voir [TechDraw Hachures](TechDraw_Hatching/fr.md).



## Script

Voir aussi : [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) et [FreeCAD Débuter avec les scripts](FreeCAD_Scripting_Basics/fr.md).

Une Vue en coupe peut être créée à partir de [macros](Macros/fr.md) et de la console [Python](Python/fr.md) en utilisant la fonction suivante :


```python
doc = FreeCAD.ActiveDocument
box = doc.Box
page = doc.Page

view = doc.addObject("TechDraw::DrawViewPart", "View")
page.addView(view)
view.Source = box
view.Direction = (0, 0, 1)

section = doc.addObject("TechDraw::DrawViewSection", "Section")
page.addView(section)
section.Source = box
section.BaseView = view
section.Direction = (0, 1, 0)
section.SectionNormal = (-1, 0, 0)

doc.recompute()
```



## Exemples

Pour plus d\'informations sur les coupes et certains cas d\'utilisation, consultez : [TechDraw Exemples de coupes](TechDraw_Section_Examples/fr.md).

<img alt="" src=images/TechDraw_ExampleSection-10.png  style="width:80px;"> <img alt="" src=images/TechDraw_ExampleSection-13.png  style="width:80px;"> <img alt="" src=images/TechDraw_ExampleSection-15.png  style="width:80px;"> <img alt="" src=images/TechDraw_ExampleSection-17.png  style="width:80px;"> <img alt="" src=images/TechDraw_ExampleSection-34.png  style="width:80px;"> <img alt="" src=images/TechDraw_ExampleSection-35.png  style="width:80px;">





{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw SectionView/fr
