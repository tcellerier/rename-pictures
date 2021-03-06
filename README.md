# Script pour renommer les photos à leur date de création EXIF 

## Auteur
* v 1.2
* Nov 2018
* Thomas Cellerier

## Exécution
* En ligne de commande : ./rename_photos_bydate.sh
ou
./rename_photos_bydate.sh full_path_folder

* Ou utilisation du menu "Quick action" sur le dossier à traiter. Pour cela, dans Automator, créer un Workflow Apple script "Quick Action" avec ce script :
```
on run {input, parameters}
	
	set userName to do shell script "whoami"
	set folder_path to POSIX path of (item 1 of input)
	if application "Terminal" is running then 
		tell application "Terminal"
			activate
			do script with command "/Users/" & userName & "/Pictures/rename_photos_bydate.sh '" & folder_path & "'"
		end tell
	else
		tell application "Terminal"
			activate
			do script with command "/Users/" & userName & "/Pictures/rename_photos_bydate.sh '" & folder_path & "'" in window 1
		end tell
	end if
	
end run
```

## Description
* MAC OS uniquement
* Tri et renomme les photos/vidéos au format 20180129-001.jpg en 2 étapes :
  * 1. Copie tous les fichiers vers le format YYYYMMDD_HHMMSS (date EXIF et sinon date création fichier) dans un sous-dossier 
  * 2. Renomme les fichiers créés en étape 1 au format YYYYMMDD-nnn (fichiers qui sont donc correctement triés à partir de leur nom)
 
## Fontionnalités clefs
* Si le fichier est une live vidéo .mov Apple, le nom définitif de la vidéo est identique au nom de la photo correspondante
* Si le fichier renommé existe déjà, on incrémente un compteur nnn
