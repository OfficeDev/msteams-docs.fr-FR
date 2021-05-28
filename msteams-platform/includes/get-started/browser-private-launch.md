### <a name="optional-adjust-your-browser-launch-settings"></a>(Facultatif) Ajuster les paramètres de lancement de votre navigateur

Lorsque vous développez une Teams, il est courant d’exécuter votre application dans un autre client développeur ou avec d’autres informations d’identification.  Les Microsoft Edge et Google Chrome fournissent des fonctionnalités pour ajuster les paramètres de lancement de votre navigateur.  Par exemple, pour mettre à jour le projet pour prendre en charge le mode InPrivate (Microsoft Edge), ouvrez le `.vscode/launch.json` fichier dans votre projet.  Recherchez les paramètres de lancement appropriés et ajoutez le bloc suivant à chacun d’eux :

``` json
"runtimeArgs": [ "--inprivate" ]
```

Par exemple, le paramètre de lancement pour l’exécution locale se ressemble à ceci :

``` json
{
   "name": "Start and Attach to Frontend (Edge)",
   "type": "pwa-msedge",
   "request": "launch",
   "url": "https://teams.microsoft.com/_#/l/app/${localTeamsAppId}?installAppPackage=true",
   "preLaunchTask": "Start Frontend",
   "postDebugTask": "Stop All Services",
   "presentation": {
         "group": "all",
         "hidden": true
   },
   "runtimeArgs": [ "--inprivate" ]
},
```

Vous pouvez également configurer votre navigateur pour qu’il utilise le dernier profil connu. [Créez un profil dans](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) Microsoft Edge.  Ajustez ensuite les paramètres pour utiliser le dernier profil connu pour les nouveaux liens :

- Dans Microsoft Edge, ouvrez `edge://settings/profiles/multiProfileSettings` .
- Désactiver le **basculement automatique des profils.**
- Pour le profil **par défaut pour les liens externes,** **sélectionnez Dernier utilisé (par défaut).**

Assurez-vous que votre navigateur est ouvert au profil correct avant de déboguer votre application.
