---
 GuiCommand:
   Name: Std FreezeViews
   Name/fr: Std Figer l'affichage
   MenuLocation: Affichage , Figer l'affichage , ...
   Workbenches: Tous
   SeeAlso: Std_StoreWorkingView/fr, Std_RecallWorkingView/fr, Std_ViewIvIssueCamPos/fr
---

# Std FreezeViews/fr



## Introduction

FreeCAD peut mémoriser les paramètres de la caméra jusqu\'à 50 \"vues figées\". Les options de menu relatives aux vues figées se trouvent dans le sous-menu **Affichage → Figer l'affichage**. Les vues figées ne sont pas enregistrées dans le document. Si elles ne sont pas enregistrées avec l\'option de menu **[Enregistrer les vues](#Enregistrer_les_vues.md)**, elles seront perdues à la fermeture de l\'application FreeCAD.



## Enregistrer les vues 

### Description

L\'option de menu **Enregistrer les vues\...** enregistre toutes les vues figées existantes dans un fichier avec l\'extension ***.cam**.



### Utilisation

1.  Pour utiliser cette option, une ou plusieurs vues figées doivent exister. Une vue figée est créée avec l\'option de menu **[Figer l\'affichage](#Figer_l.27affichage.md)**.
2.  Sélectionnez l\'option **Affichage → Figer l'affichage → Enregistrer les vues...** du menu.
3.  Entrez un nom de fichier dans la fenêtre de dialogue.
4.  Appuyez sur le bouton **Enregistrer**.

### Options

-   Appuyez sur **Échap** ou sur le bouton **Annuler** pour annuler la commande.



## Charger les vues 

### Description 

L\'option du menu **Charger les vues\...** charge les vues figées à partir d\'un fichier avec l\'extension ***.cam**. Toutes les vues figées existantes seront supprimées.



### Utilisation 

1.  Sélectionnez l\'option **Affichage → Figer l'affichage → Charger les vues...** du menu.
2.  Appuyez sur le bouton **Oui** dans la fenêtre de dialogue Restaurer les vues pour confirmer que vous souhaitez perdre toutes les vues figées existantes.
3.  Sélectionner un fichier.
4.  Appuyez sur le bouton **Ouvrir**.

### Options 

-   Si la fenêtre de dialogue Restaurer les vues s\'affiche, appuyez sur **Échap** ou sur le bouton **Non** pour annuler la commande.
-   Si la fenêtre de dialogue du fichier s\'affiche, appuyez sur **Échap** ou sur le bouton **Annuler** pour abandonner la commande.



## Figer l\'affichage 

### Description 

L\'option de menu **Figer l\'affichage** enregistre les paramètres en cours de la caméra (direction, zoom, etc.) de la [vue 3D](3D_view/fr.md) dans une nouvelle entrée de la liste des vues figées. La liste des vues figées peut contenir jusqu\'à 50 vues figées.



### Utilisation 

1.  Il existe plusieurs façons de lancer cette option :
    -   Sélectionnez l\'option **Affichage → Figer l'affichage → Charger les vues...** du menu.
    -   Utilisez le raccourci clavier : **Maj**+**F**.
2.  La nouvelle vue figée peut être sélectionnée dans le sous-menu **Affichage → Figer l'affichage**.



## Effacer les vues 

### Description 

L\'option de menu **Effacer les vues** supprime toutes les vues figées existantes.



### Utilisation 

1.  Sélectionnez l\'option **Affichage → Figer l'affichage → Effacer les vues** du menu.



## Restaurer la vue 

### Description 

Pour chaque vue figée, une option **Vue de restauration** est ajoutée avec laquelle elle peut être restaurée. Les options sont numérotées: **Restore view 1** - **Restore view 50**.



### Utilisation 

1.  Il existe plusieurs façons de lancer cette option :
    -   Sélectionnez l\'option **Affichage → Figer l'affichage → Restaurer la vue** du menu.
    -   Pour les 9 premières vues figées: utilisez le raccourci clavier : **Ctrl**+**1** - **Ctrl**+**9**.



---
⏵ [documentation index](../README.md) > Std FreezeViews/fr
