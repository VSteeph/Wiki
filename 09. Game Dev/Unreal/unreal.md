# Unreal

## Reduce Lag:

* Desactiver RealTime rendering (burger Menu)
* Project Settings : Enlever Lumen en Reflection, Shadow Beta et Global Illumination (Si non utilisée)

## Keybinds:

* Ctrl + Space pour le Content Drawer

## Blueprints par Défaut?

En C++ par défaut, cela va créer toute la sln par défaut et aussi un Game Mode qu'on peut ne pas vouloir. Cela limite aussi les naming conventions et la structure donc on peut commencer en blueprint par défaut.

## Random

* Si information apparaisse pas, recompiler, si toujours pas relancer le projet
* Blueprint peut servir un peu de prefab
* Tout ce qui est inherité ne peut pas être delete
* Les inputs sont dans Project Settings Input (1 pour positif, -1 pour inverse pour les inputs d'axe)
* UFONCTION poru le binding
* 

## Random Image
![image](https://user-images.githubusercontent.com/58773222/152567380-49ab36fe-c791-45fd-86d5-542a1b838783.png)

## Methodologie création environnement

Mettre son environnement 
=> Directional Light
=> Sky Light
=> SkyAtmosphere
=> ExponentialHeightFog
=> PostProcessVolumes => Lumen ou non
=> Check Lighting settings (advanced precompute) si Lumen
=> Mettre un Cube et un mannequin pour garder les échellles de grandeur

Potentiellement, mettre l'exposure en manual à 11 et bien coché Infinite extends pour Le PostProcessVolume



## Troubleshootings

Bug quand on ajoute des elemetns dans des dossiers mais il faut recompiler pour que la classe soit prise en compte. Pour corriger ce bug, on ouvre le content Drawer, click droit sur content, ouvrir dans l'exploreur, ouvrir la solution, aller sur le fichier et enlever le nom du dossier dans le #include du fichier cpp.

Fermer le projet, rebuild le projet et relancer le projet
