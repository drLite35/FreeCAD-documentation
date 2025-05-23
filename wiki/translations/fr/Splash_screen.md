# Splash screen/fr
## Description

L\'écran de démarrage est une image qui apparaît au démarrage de FreeCAD. Vous pouvez désactiver l\'écran de démarrage dans les [réglages des préférences](Preferences_Editor/fr#Général_2/fr.md) en décochant l\'option **Activer l\'écran de démarrage**.


{{Version/fr|1.0}}

: l\'image de l\'écran d\'accueil est choisie de manière aléatoire parmi plusieurs images, y compris des modèles d\'utilisateurs et des extensions.



## Écran de démarrage personnalisé 

Pour utiliser un écran de démarrage personnalisé, vous devez placer une image nommée **splash_image.png** dans l\'un des répertoires suivants, en fonction du système d\'exploitation :

-   **Linux :** **$XDG_DATA_HOME/FreeCAD/Gui/images/** (normalement cela correspond à **~/.local/share/FreeCAD/Gui/images/**)
-   **Windows :** **%APPDATA%\NFreeCAD\Gui\images** (normalement **C:Úsers\username\AppData\Roaming\FreeCAD\Gui\images**)
-   **MacOS :** **~/Library/Application Support/FreeCAD/Gui/images/**

Le répertoire peut être trouvé en utilisant la commande {{Incode|App.getUserAppDataDir()}} dans la [console Python](Python_console/fr.md). Les dossiers {{Incode|Gui}} et {{Incode|images}} peuvent devoir être créés en premier. Le même écran de démarrage personnalisé sera utilisé pour toutes les versions de FreeCAD sur un ordinateur donné.



---
⏵ [documentation index](../README.md) > [User_Documentation](Category_User_Documentation.md) > Splash screen/fr
