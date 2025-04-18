---
 GuiCommand:Container
|
{{GuiCommand/fr
   Name: FEM ConstraintCurrentDensity
   Name/fr: FEM Densité de courant
   MenuLocation: Modèle , Conditions limites électromagnétiques , Condition limite de densité de courant
   Workbenches: FEM_Workbench/fr
   Version: 0.21
   SeeAlso: FEM_EquationMagnetodynamic/fr, FEM_EquationMagnetodynamic2D/fr
}}
{{GuiCommandFemInfo/fr
   Solvers: Elmer
}}
---

# FEM ConstraintCurrentDensity/fr

## Description

Crée une condition limite FEM pour la densité de courant. À utiliser avec les équations [magnétodynamiques](FEM_EquationMagnetodynamic/fr.md) et [magnétodynamiques 2D](FEM_EquationMagnetodynamic2D/fr.md)



## Utilisation

1.  Appuyez sur le bouton **<img src="images/FEM_ConstraintCurrentDensity.svg" width=16px> [Condition limite de densité de courant](FEM_ConstraintCurrentDensity/fr.md)** ou utilisez le menu **Modèle → Conditions limites électromagnétiques → <img src="images/FEM_ConstraintCurrentDensity.svg" width=16px> Condition limite de densité de courant**.
2.  Appuyez sur le bouton **Ajouter**.
3.  Dans la [vue 3D](3D_view/fr.md), sélectionnez l\'objet auquel la condition de limite doit être appliquée.

## Options

-   **Current density\_\*\_1** : partie réelle/imaginaire de la densité de courant dans la direction des x en A/m².Pour les systèmes de coordonnées autres que cartésien 3D, ce sera la première coordonnée du système au lieu de x.
-   **Current density\_\*\_2** : partie réelle/imaginaire de la densité de courant dans la direction des y en A/m².Pour les systèmes de coordonnées autres que cartésien 3D, ce sera la deuxième coordonnée du système au lieu de y.
-   **Current density\_\*\_3** : partie réelle/imaginaire de la densité de courant dans la direction des z en A/m².Pour les systèmes de coordonnées autres que cartésien 3D, ce sera la troisième coordonnée du système au lieu de z. Si le système de coordonnées n\'a pas de troisième coordonnée, ce paramètre sera ignoré.
-   **Current density\_\*\_\*\_Disabled** : indique si le paramètre correspondant est désactivé (supposé inconnu par le solveur).





{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM ConstraintCurrentDensity/fr
