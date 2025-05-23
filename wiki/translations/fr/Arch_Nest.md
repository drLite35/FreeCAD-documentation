---
 GuiCommand:
   Name: Arch Nest
   Name/fr: Arch Calepinage
   MenuLocation: Utilitaires , Outils pour les panneaux , Calepiner
   Workbenches: BIM_Workbench/fr
   SeeAlso: Arch_Panel/fr, Arch_Panel_Sheet/fr
---

# Arch Nest/fr

## Description

L\'outil **Arch Calepinage** permet de sélectionner une forme plane pour en faire un conteneur, et une série d\'autres formes planes à disposer à l\'intérieur de l\'espace défini par la forme du conteneur. Ceci est généralement nécessaire pour les opérations sur machines CNC, où vous voulez découper une série de pièces dans un panneau de base, et devez organiser ces pièces de la manière la plus compacte possible pour qu\'elles occupent moins d\'espace sur le panneau.

L\'algorithme qui gère l\'outil Calepinage est en constante évolution et n\'est actuellement pas entièrement optimisé. À l\'avenir, la performance de cet outil devrait devenir bien meilleure.

<img alt="" src=images/Arch_Nest_example.jpg  style="width:600px;">

*L\'image ci-dessus montre une série de formes avant et après l\'opération de calepinage.*



## Utilisation

1.  Sélectionnez l\'option **Utilitaires → Outils pour les panneaux → <img src="images/Arch_Nest.svg" width=16px> Calepiner** du menu.
2.  Sélectionnez un objet pour devenir le conteneur. Cet objet doit être plat et pour l\'instant rectangulaire.
3.  Cliquez sur le bouton **Choisir la sélection** pour utiliser cet objet comme conteneur.
4.  Sélectionnez une série d\'autres objets plats que vous souhaitez placer à l\'intérieur du conteneur. Ces objets doivent tous être plats et dans le même plan que le conteneur.
5.  Ajustez les options souhaitées.
6.  Démarrez le processus de calcul.
7.  À la fin du calcul, cliquez sur le bouton **Aperçu** pour créer un aperçu temporaire du résultat.
8.  Si vous souhaitez appliquer le résultat (déplacez et faites pivoter les formes réelles), cliquez sur **OK**.

<img alt="" src=images/Arch_Nest_panel.jpg  style="width:800px;"> 
*Panneau de tâches pour l'outil [Calepinage](Arch_Nest/fr.md)*



## Remarques

-   Tous les objets doivent avoir une face.
-   Pour le moment, l\'outil ne fonctionnera qu\'avec des objets plats ayant tous la même orientation.
-   Pour le moment, le conteneur doit être rectangulaire.
-   Pour le moment, la marge/l\'espace entre les pièces n\'est pas encore implémenté.
-   Le calcul peut prendre beaucoup de temps avec de nombreux objets. Cela sera optimisé dans le futur.



---
⏵ [documentation index](../README.md) > [BIM](Category_BIM.md) > Arch Nest/fr
