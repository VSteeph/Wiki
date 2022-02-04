# Unreal

## Reduce Lag:

* Desactiver RealTime rendering (burger Menu)
* Project Settings : Enlever Lumen en Reflection, Shadow Beta et Global Illumination (Si non utilisée)

## Keybinds:

* Ctrl + Space pour le Content Drawer

## Blueprints par Défaut?

En C++ par défaut, cela va créer toute la sln par défaut et aussi un Game Mode qu'on peut ne pas vouloir. Cela limite aussi les naming conventions et la structure donc on peut commencer en blueprint par défaut.

## Troubleshootings

Bug quand on ajoute des elemetns dans des dossiers mais il faut recompiler pour que la classe soit prise en compte. Pour corriger ce bug, on ouvre le content Drawer, click droit sur content, ouvrir dans l'exploreur, ouvrir la solution, aller sur le fichier et enlever le nom du dossier dans le #include du fichier cpp.

Fermer le projet, rebuild le projet et relancer le projet
