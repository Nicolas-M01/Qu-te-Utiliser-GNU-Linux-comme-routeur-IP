# Partage de fichiers (Windows)


## 1. Installe le rôle Serveur de fichiers  
Installer le rôle de "Serveur de fichiers" dans Add roles and features. Et suivre les étapes comme sur les photos

![Capture d'écran 2024-11-25 181151](https://github.com/user-attachments/assets/f62d4655-5472-4ac0-b098-a79a7755c0f3)
![Capture d'écran 2024-11-25 181443](https://github.com/user-attachments/assets/1b7eae2b-1198-4882-9a72-8386b92dab52)
![Capture d'écran 2024-11-25 181608](https://github.com/user-attachments/assets/782c6176-15a5-4d06-bf65-24e18ebdf3cf)
![Capture d'écran 2024-11-25 181850](https://github.com/user-attachments/assets/dbf6dd8c-ab68-4710-9320-a208d32003be)

## 2. Crée un dossier "Documents_Entreprise" à la racine du disque C:  
![Capture d'écran 2024-11-25 182231](https://github.com/user-attachments/assets/b5184826-5302-4a48-8998-d537fc889ded)

## 3.Configure un partage nommé "Docs" pour ce dossier
![Capture d'écran 2024-11-25 182525](https://github.com/user-attachments/assets/b67c7e7a-77df-41b2-b6af-914154cdf7d5)

Attribuer les droits pour ce dossier :  
![Capture d'écran 2024-11-25 183925](https://github.com/user-attachments/assets/fabf0b5b-92ef-4812-8750-3999babf413d)


## 4. Crée trois sous-dossiers : "RH", "Comptabilité" et "Direction"
Directement dans le gestionnaire des dossier/fichiers :  
![image](https://github.com/user-attachments/assets/6335b11a-771e-454f-9f53-34dff509d688)


## 5.Configure les permissions NTFS et de partage pour que :
* Le groupe "RH" ait un accès en lecture/écriture au dossier "RH"
* Le groupe "Comptabilité" ait un accès en lecture/écriture au dossier "Comptabilité"
* Le groupe "Direction" ait un accès en lecture/écriture à tous les dossiers
* Tous les utilisateurs du domaine aient un accès en lecture seule au dossier "Documents_Entreprise"

:flushed: J'ai oublié de le faire au début mais ce n'est pas grave ! :arrow_right: Installer ADDS ( Add roles and features / Active Directory domain Service... )  
Add a new forest / wilders.lan  ... mot de passe... NetBIOS : WILDERS ... Install...
Une fois terminé on va pouvoir créer nos groupe et attribuer les droits.

Tools :arrow_right: Active Directory Users and Computers  
Créer une OU "Personnel", puis Créer nos 3 groupes et les ajouter à cette OU :  
![Capture d'écran 2024-11-25 192006](https://github.com/user-attachments/assets/84f8cd0c-c13c-43cc-9662-ad8cbbecff11)  

Server Manager / Disk / Volume clic droit sur notre dossier doc / New share
  
![Capture d'écran 2024-11-25 195019](https://github.com/user-attachments/assets/1e93e41a-1304-439a-b45b-b5165c4a17f2)
![Capture d'écran 2024-11-25 195316](https://github.com/user-attachments/assets/ad35786e-f3c2-488f-b91c-3c9049ccae75)
![Capture d'écran 2024-11-25 195345](https://github.com/user-attachments/assets/740767fc-346d-4018-9a31-ca9391d0c8b9)
Editer pour chaque groupe créé comme demandé pour chaque dossier.


## 6. Utilise PowerShell pour lister tous les partages sur le serveur
`Commande Get-SmbShare` pour visualiser les documents SMB
![Capture d'écran 2024-11-25 195640](https://github.com/user-attachments/assets/f225bc17-cc57-42d8-95c8-b4cbff337ac6)
