---
 GuiCommand:
   Name: PartDesign Chamfer
   Name/fr: PartDesign Chanfrein
   MenuLocation: PartDesign , Appliquer une fonction d'habillage , Chanfrein
   Workbenches: PartDesign_Workbench/fr
   SeeAlso: PartDesign_Fillet/fr
---

# PartDesign Chamfer/fr

## Description

L\'outil <img alt="" src=images/PartDesign_Chamfer.svg  style="width:24px;"> **PartDesign Chanfrein** crée des chanfreins sur les arêtes sélectionnées d\'un objet. Il ajoute un objet **Chamfer** au document avec sa représentation correspondante dans la [vue en arborescence](Tree_view/fr.md).



## Utilisation



### Ajouter un chanfrein 

1.  Vous pouvez [activer](PartDesign_Body/fr#Statut_actif.md) le corps à chanfreiner.
2.  Il existe plusieurs façons de sélectionner les arêtes à chanfreiner :
    -   Sélectionnez une ou plusieurs arêtes du corps une par une.
    -   Sélectionnez une ou plusieurs faces du corps pour sélectionner toutes leurs arêtes.
    -   Sélectionnez un élément (généralement le dernier élément) du corps pour sélectionner toutes ses arêtes.
3.  Pour une chaîne d\'arêtes reliées tangentiellement, il suffit de sélectionner une seule arête, le chanfrein se propageant le long de la chaîne.
4.  Il existe plusieurs façons de lancer l\'outil :
    -   Appuyez sur le bouton **<img src="images/PartDesign_Chamfer.svg" width=16px> [Chanfrein](PartDesign_Chamfer/fr.md)**.
    -   Sélectionnez l\'option **PartDesign → Appliquer une fonction d'habillage → <img src="images/PartDesign_Chamfer.svg" width=16px> Chanfrein** du menu.
5.  S\'il n\'y a pas de corps actif, et qu\'il y a deux corps ou plus dans le document, la fenêtre de dialogue **Corps actif requis** s\'ouvrira et vous invitera à en activer un. S\'il n\'y a qu\'un seul corps, il sera activé automatiquement.
6.  Le [panneau des tâches](Task_panel/fr.md) des **Paramètres du chanfrein** s\'ouvre. Voir [Options](#Options.md) pour plus d\'informations.
7.  Appuyez sur le bouton **OK** pour terminer.



### Modifier un chanfrein 

1.  Effectuez l\'une des opérations suivantes :
    -   Double-cliquez sur l\'objet Chamfer dans la [vue en arborescence](Tree_view/fr.md).
    -   Cliquez avec le bouton droit de la souris sur l\'objet Chamfer dans la [vue en arborescence](Tree_view/fr.md) et sélectionnez **Modifier le chanfrein** dans le menu contextuel.
2.  Le [panneau des tâches](Task_panel/fr.md) **Paramètres du chanfrein** s\'ouvre. Voir [Options](#Options.md) pour plus d\'informations.
3.  Appuyez sur le bouton **OK** pour terminer.

## Options

-   Pour ajouter des arêtes, effectuez l\'une des opérations suivantes :
    -   Appuyez sur le bouton **Ajouter** pour commencer à sélectionner des arêtes et/ou des faces dans la [vue 3D](3D_view/fr.md).
    -   Pour sélectionner toutes les arêtes restantes, procédez comme suit :
        1.  Si nécessaire, appuyez sur le bouton **Ajouter**.
        2.  Utilisez le raccourci clavier **Ctrl**+**Shift**+**A**, ou cliquez avec le bouton droit de la souris sur la liste et sélectionnez **Ajouter toutes les arêtes** dans le menu contextuel.
-   Pour supprimer des arêtes, effectuez l\'une des opérations suivantes :
    -   Appuyez sur le bouton **Supprimer** pour commencer à désélectionner les arêtes et/ou les faces dans la [vue 3D](3D_view/fr.md). Les éléments sélectionnés sont surlignés en violet.
    -   Sélectionnez un ou plusieurs éléments dans la liste et appuyez sur la touche **Suppr** ou cliquez avec le bouton droit de la souris sur la liste et sélectionnez **Supprimer** dans le menu contextuel.
-   Spécifier un chanfrein **Type** :
    -   
        **Distance égale**
        
        : distance utilisée pour placer les deux arêtes du chanfrein.

    -   
        **Deux distances**
        
        : deux distances sont utilisées pour placer les arêtes du chanfrein.

    -   
        **Distance et angle**
        
        : distance utilisée pour placer une arête du chanfrein, le placement de l\'autre arête du chanfrein est défini par l\'angle du chanfrein.
-   Appuyez sur le bouton **<img src="images/PartDesign_Flip_Direction.svg" width=16px> Inverser la direction** pour inverser la direction du chanfrein (désactivé pour **Equal distance**).
-   Définissez la **Dimension** du chanfrein.
-   Définissez la **Dimension 2** du chanfrein (disponible uniquement si **Deux distances** est sélectionné).
-   Définissez le **Angle** du chanfrein (disponible uniquement si **Distance et angle** est sélectionné).
-   Cochez la case **Ajouter toutes les arêtes** pour sélectionner tous les arêtes de l\'élément précédent. Ceci désactive la liste de sélection et les boutons associés.



## Remarques

-   Le PartDesign Chanfrein ne doit pas être confondu avec le [Part Chanfrein](Part_Chamfer/fr.md). À moins que vous ne sachiez ce que vous faites, [Part Chanfrein](Part_Chamfer/fr.md) ne doit pas être utilisé sur un corps PartDesign. Voir [Part et PartDesign](Part_and_PartDesign/fr.md).
-   Les chanfreins ne peuvent pas entièrement épouser les faces adjacentes.



## Propriétés

Voir aussi : [Éditeur de propriétés](Property_editor/fr.md)

Un objet Part Chamfer est dérivé d\'un [Part Feature](Part_Feature/fr.md) et hérite de toutes ses propriétés. Il possède également les propriétés supplémentaires suivantes :



### Données


{{Properties_Title|Base}}

-    **Base|LinkSub**: lien vers les arêtes et les faces sélectionnées de l\'élément parent. Peut être un lien vers l\'élément parent uniquement si **Use All Edges** est `True`.

-    **Support Transform|Bool**: si `True`, la forme chanfreinée de la fonction parentale additive/soustractive sera utilisée lorsque l\'objet chanfrein est inclus dans un [motif](PartDesign_Workbench/fr#Outils_de_transformation.md), sinon seule la forme du chanfrein sera utilisée. La valeur par défaut est `False`.

-    **Add Sub Shape|PartShape|hidden**
    

-    **Base Feature|Link|hidden**: lien vers l\'élément parent.

-    **_ Body|LinkHidden|hidden**: lien vers le corps du parent.


{{Properties_Title|Chamfer}}

-    **Chamfer Type|Enumeration**: type de chanfrein : {{value|Equal distance}} (par défaut), {{value|Two distances}} ou {{value|Distance and Angle}}.

-    **Size|QuantityConstraint**: distance du premier chanfrein. La valeur par défaut est {{value|1 mm}}.

-    **Size2|QuantityConstraint**: distance du deuxième chanfrein. Utilisé uniquement si **Chamfer Type** est {{Value|Two distances}}. La valeur par défaut est {{value|1 mm}}.

-    **Angle|Angle**: angle du chanfrein. Utilisé uniquement si **Chamfer Type** est {{Value|Distance and Angle}}. La valeur par défaut est {{value|45 °}}.

-    **Flip Direction|Bool**: si `True`, la direction du chanfrein est inversée. Non utilisé si **Chamfer Type** est {{Value|Equal distance}}. La valeur par défaut est `False`.

-    **Use All Edges|Bool**: si `True`, toutes les arêtes de l\'élément sont chanfreinées et les arêtes spécifiées par **Base** sont ignorées. La valeur par défaut est `False`.


{{Properties_Title|Part Design}}

-    **Refine|Bool**: si `True`, les arêtes redondantes sont supprimées du résultat de l\'opération. La valeur par défaut est déterminée par la préférence **Affiner les modèles automatiquement après une opération sur une esquisse**. Voir [PartDesign Préférences](PartDesign_Preferences/fr#G.C3.A9n.C3.A9ral.md).



## Problèmes connus 

Voir [PartDesign Congé](PartDesign_Fillet/fr#Probl.C3.A8mes_connus.md).





{{PartDesign Tools navi

}}



---
⏵ [documentation index](../README.md) > [PartDesign](PartDesign_Workbench.md) > PartDesign Chamfer/fr
