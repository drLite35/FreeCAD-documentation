---
 GuiCommand:
   Name: TechDraw ExportPageDXF
   Name/fr: TechDraw Exporter au format DXF
   MenuLocation: TechDraw , Page , Exporter une page au format DXF
   Workbenches: TechDraw_Workbench/fr
   Version: 0.18
   SeeAlso: TechDraw_ExportPageSVG/fr, Draft_DXF/fr
---

# TechDraw ExportPageDXF/fr

## Description

L\'outil **TechDraw Exporter la page en Dxf** enregistre une page de dessin en un fichier au format [DXF](DXF/fr.md)



## Utilisation

1.  S\'il y a plusieurs pages de dessin dans le document : activez la page souhaitée en la sélectionnant dans la [vue arborescente](Tree_view/fr.md).
2.  Il y a plusieurs façons de lancer l\'outil :
    -   Appuyez sur le **<img src="images/TechDraw_ExportPageDXF.svg" width=16px> [Exporter une page au format DXF](TechDraw_ExportPageDXF/fr.md)**.
    -   Sélectionnez l\'option **TechDraw → Page → <img src="images/TechDraw_ExportPageDXF.svg" width=16px> Exporter une page au format DXF** du menu.
    -   Si une page est affichée dans la [zone de vue principale](Main_view_area/fr.md) : cliquez avec le bouton droit de la souris sur la fenêtre de la page et sélectionnez l\'option **Exporter en DXF** dans le menu contextuel.
3.  S\'il y a plusieurs pages de dessin dans le document et que vous n\'avez pas encore activé une page, la fenêtre de dialogue **Sélecteur de pages** s\'ouvre :
    1.  Sélectionnez la page désirée.
    2.  Appuyez sur le bouton **OK**.
4.  La fenêtre de dialogue **Enregistrer le fichier DXF** s\'ouvre.
5.  Sélectionnez un emplacement et un nom de fichier.

### Limitations

-   Les dimensions radiales et de diamètre ne s\'exporteront correctement que si elles sont \"à l\'intérieur\" de l\'arc.
-   La mise à l\'échelle n\'est pas prise en charge. Le DXF sera dessiné dans la taille réelle de la page TechDraw.
-   Les unités ne sont pas prises en charge. Le DXF sera dessiné en millimètres (mm). Le texte de cote sera affiché exactement tel qu\'il est affiché dans TechDraw.
-   TechDraw ne peut pas exporter un [TechDraw Vue d\'un objet Draft](TechDraw_DraftView/fr.md) ou une [TechDraw Vue d\'un objet Arch](TechDraw_ArchView/fr.md) vers DXF. Ces vues sont des éléments [SVG](SVG/fr.md) générés en interne par l\'[atelier Draft](Draft_Workbench/fr.md), il n\'y a donc pas de forme géométrique à exporter. Pour exporter une vue au format DXF, elle doit avoir été créée avec [TechDraw Vue](TechDraw_View/fr.md) ou [TechDraw Projection de groupe](TechDraw_ProjectionGroup/fr.md). Par exemple, sélectionnez un [Arch Plan de coupe](Arch_SectionPlane/fr.md), puis utilisez [Draft Vue 2D d\'une forme](Draft_Shape2DView/fr.md) pour créer une forme de projection plate, puis utilisez [TechDraw Vue](TechDraw_View/fr.md) sur cet objet. Vous pouvez également sélectionner les objets dans l\'arborescence ou la fenêtre 3D et exporter vers DXF à l\'aide de **Fichier → [Export](Std_Export/fr.md)**.
-   Le cartouche d\'une page est également un modèle [SVG](SVG/fr.md), il ne sera donc pas non plus exporté vers DXF.
-   En général, TechDraw ne peut exporter vers DXF que les éléments pris en charge par la classe `Import::ImpExpDxfWrite` du [Module d\'importation](Draft_DXF/fr.md).



## Remarques

-   Cette fonction exporte les versions R12 (AC1009) et R14 (AC1014) de [DXF](DXF/fr.md).
    -   R12 est une version plus ancienne et plus simple de la norme mais devrait être lisible par la plupart des autres logiciels.
    -   R14 est la version par défaut. Elle inclut entre autres la prise en charge des splines et des ellipses.
-   Ces paramètres affectent la sortie:
    -   
        **Outils → Editer paramètres → BaseApp/Preferences/Mod/Import → DxfVersionOut**
        
        . Il s\'agit d\'une valeur entière. Les entrées valides sont 12 ou 14. La valeur par défaut est 14.

    -   
        **Outils → Editer paramètres → BaseApp/Preferences/Mod/Import → DiscretizeEllipses**
        
        . Il s\'agit d\'une valeur booléenne. Si `True`, les splines et les ellipses sont converties en polylignes; si `False`, les splines et les ellipses sont écrites en tant qu\'objets splines et ellipses. Par défaut `False`. Si le paramètre DxfVersionOut est 12, les splines et les ellipses sont toujours converties en polylignes.

    -   
        **Outils → Editer paramètres → BaseApp/Preferences/Mod/Import → maxsegmentlength**
        
        . Il s\'agit d\'une valeur flottante. Si les splines et les ellipses sont converties en polylignes, ce paramètre détermine la longueur du segment.



## Script

Voir aussi : [Autogenerated API documentation](https://freecad.github.io/SourceDoc/) et [FreeCAD Débuter avec les scripts](FreeCAD_Scripting_Basics/fr.md).

L\'outil Sauvegarder en DXF peut être utilisé dans des [macros](Macros/fr.md) et à partir de la console [Python](Python/fr.md) à l\'aide des fonctions suivantes:


```python
TechDraw.writeDXFPage(page,filename)
```





{{TechDraw_Tools_navi

}}



---
⏵ [documentation index](../README.md) > [TechDraw](TechDraw_Workbench.md) > TechDraw ExportPageDXF/fr
