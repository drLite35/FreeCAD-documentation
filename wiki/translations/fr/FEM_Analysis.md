---
 GuiCommand:
   Name: FEM Analysis
   Name/fr: FEM Conteneur d'analyse
   MenuLocation: Modèle , Conteneur d'analyse
   Workbenches: FEM_Workbench/fr
   Shortcut: **S** **A**
   SeeAlso: FEM_tutorial/fr
---

# FEM Analysis/fr

## Description

L\'analyse FEM peut être considérée comme un conteneur qui contient tous les objets d\'une analyse par éléments finis. Il est obligatoire d\'avoir un conteneur d\'analyse qui contient tous les objets nécessaires. Au moins un des objets suivants (à l\'exception du maillage) est nécessaire pour une analyse mécanique :

-   [Matériau pour solide](FEM_MaterialSolid/fr.md),
-   [Condition de limite fixe](FEM_ConstraintFixed/fr.md), [Condition limite de déplacement](FEM_ConstraintDisplacement/fr.md) ou [Contrainte de corps rigide](FEM_ConstraintRigidBody/fr.md).



## Utilisation

1.  Il existe plusieurs façons de lancer la commande :
    -   Appuyez sur le bouton **<img src="images/FEM_Analysis.svg" width=16px> [Conteneur d'analyse](FEM_Analysis/fr.md)**.
    -   Sélectionnez l\'option **Modèle → <img src="images/FEM_Analysis.svg" width=16px> Conteneur d'analyse** du menu.
    -   Utilisez le raccourci clavier : **S** puis **A**.
2.  Une nouvelle analyse est créée et définie comme active.
3.  D\'autres objets peuvent être ajoutés ou retirés du conteneur de l\'analyse par glisser-déposer.
4.  Pour ajouter de nouveaux objets FEM au document, l\'analyse doit être active. Un double-clic sur le conteneur d\'analyse active l\'analyse.

## Options

-   À ce jour il n\'y a pas d\'option de choix.



## Propriétés

-    **OutpuDir**: spécifie le répertoire de travail pour l\'analyse



## Script

la plupart du code ici est déprécié dans la 0.17.

-   nouvelle analyse


```python
MechanicalAnalysis.makeMechanicalAnalysis( name )
```

-   ajouter un objet à analyser


```python
App.ActiveDocument.MechanicalAnalysis.Member = App.ActiveDocument.MechanicalAnalysis.Member + [ (object) ]
```

-   effacer un objet du conteneur


```python
member = App.ActiveDocument.MechanicalAnalysis.Member
member.remove( documentobject )
 App.ActiveDocument.MechanicalAnalysis.Member = member
```

Exemples : 
```python
import MechanicalAnalysis
analysis = MechanicalAnalysis.makeMechanicalAnalysis("MechanicalAnalysis")
FemGui.setActiveAnalysis(analysis)

addobj = App.ActiveDocument.getObject("MechanicalMaterial")
App.ActiveDocument.MechanicalAnalysis.Member = App.ActiveDocument.MechanicalAnalysis.Member + [addobj]

removeobj = App.ActiveDocument.getObject("MechanicalMaterial")
member = App.ActiveDocument.MechanicalAnalysis.Member
member.remove(removeobj)
App.ActiveDocument.MechanicalAnalysis.Member = member
```





{{FEM Tools navi

}}



---
⏵ [documentation index](../README.md) > [FEM](Category_FEM.md) > FEM Analysis/fr
