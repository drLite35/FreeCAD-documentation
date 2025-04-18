---
 GuiCommand:
   Name: TechDraw ExportPageSVG
   Name/fr: TechDraw Exporter au format SVG
   MenuLocation: TechDraw , Page , Exporter une page au format SVG
   Workbenches: TechDraw_Workbench/fr
   Version: 0.19
   SeeAlso: TechDraw_Templates/fr, Draft_SVG/fr
---

# TechDraw ExportPageSVG/fr

## Description

L\'outil **TechDraw Exporter au format SVG** enregistre la page de dessin en cours sous forme de fichier [SVG](SVG/fr.md).



## Utilisation

1.  S\'il y a plusieurs pages de dessin dans le document : vous pouvez activer la page souhaitée en la sélectionnant dans la [vue arborescente](Tree_view/fr.md).
2.  Il y a plusieurs façons de lancer l\'outil :
    -   Appuyez sur le **<img src="images/TechDraw_ExportPageSVG.svg" width=16px> [Exporter une page au format SVG](TechDraw_ExportPageSVG/fr.md)**.
    -   Sélectionnez l\'option **TechDraw → Page → <img src="images/TechDraw_ExportPageSVG.svg" width=16px> Exporter une page au format SVG** du menu.
    -   Si une page est affichée dans la [zone de vue principale](Main_view_area/fr.md) : cliquez avec le bouton droit de la souris sur la fenêtre de la page et sélectionnez l\'option **Exporter en SVG** dans le menu contextuel.
3.  S\'il y a plusieurs pages de dessin dans le document et que vous n\'avez pas encore activé une page, la fenêtre de dialogue **Sélecteur de pages** s\'ouvre :
    1.  Sélectionnez la page désirée.
    2.  Appuyez sur le bouton **OK**.
4.  La fenêtre de dialogue **Exporter la page en SVG** s\'ouvre.
    1.  Sélectionnez un emplacement et un nom de fichier.



## Remarques

-   Les modèles [TechDraw Hachures par motifs](TechDraw_Hatch/fr.md) ne sont pas exportés vers [SVG](SVG/fr.md) en raison d\'une limitation de la prise en charge SVG de Qt4.
-   Les positions et tailles de texte ne sont pas correctes dans le fichier exporté. L\'utilisation de la police par défaut \"système\" dans le dessin améliore considérablement le problème de taille.



## Script

Voir aussi : [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) et [FreeCAD Débuter avec les scripts](FreeCAD_Scripting_Basics/fr.md).

L\'outil Exporter au format SVG peut être utilisé dans des [macros](Macros/fr.md) et à partir de la console [Python](Python/fr.md) à l\'aide des fonctions suivantes:


```python
TechDrawGui.exportPageAsSvg(DrawPageObject,FilePath)
```

Notez que le module FreeCADGui doit être actif pour utiliser cette fonction.





{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw ExportPageSVG/fr
