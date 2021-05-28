### <a name="optional-adjust-your-browser-launch-settings"></a><span data-ttu-id="1b16a-101">(Facultatif) Ajuster les paramètres de lancement de votre navigateur</span><span class="sxs-lookup"><span data-stu-id="1b16a-101">(Optional) Adjust your browser launch settings</span></span>

<span data-ttu-id="1b16a-102">Lorsque vous développez une Teams, il est courant d’exécuter votre application dans un autre client développeur ou avec d’autres informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="1b16a-102">When developing a Teams app, it is common to run your app in an alternate developer tenant or with alternate credentials.</span></span>  <span data-ttu-id="1b16a-103">Les Microsoft Edge et Google Chrome fournissent des fonctionnalités pour ajuster les paramètres de lancement de votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="1b16a-103">Both Microsoft Edge and Google Chrome provide facilities to adjust the launch settings for your browser.</span></span>  <span data-ttu-id="1b16a-104">Par exemple, pour mettre à jour le projet pour prendre en charge le mode InPrivate (Microsoft Edge), ouvrez le `.vscode/launch.json` fichier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="1b16a-104">For example, to update the project to support InPrivate mode (Microsoft Edge), open the `.vscode/launch.json` file in your project.</span></span>  <span data-ttu-id="1b16a-105">Recherchez les paramètres de lancement appropriés et ajoutez le bloc suivant à chacun d’eux :</span><span class="sxs-lookup"><span data-stu-id="1b16a-105">Look for the appropriate launch settings, and add the following block to each one:</span></span>

``` json
"runtimeArgs": [ "--inprivate" ]
```

<span data-ttu-id="1b16a-106">Par exemple, le paramètre de lancement pour l’exécution locale se ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="1b16a-106">For instance, the launch setting for running locally looks like this:</span></span>

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

<span data-ttu-id="1b16a-107">Vous pouvez également configurer votre navigateur pour qu’il utilise le dernier profil connu.</span><span class="sxs-lookup"><span data-stu-id="1b16a-107">Alternatively, you can configure your browser to use the last known profile.</span></span> <span data-ttu-id="1b16a-108">[Créez un profil dans](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) Microsoft Edge.</span><span class="sxs-lookup"><span data-stu-id="1b16a-108">[Create a new profile](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) in Microsoft Edge.</span></span>  <span data-ttu-id="1b16a-109">Ajustez ensuite les paramètres pour utiliser le dernier profil connu pour les nouveaux liens :</span><span class="sxs-lookup"><span data-stu-id="1b16a-109">Then adjust the settings to use the last known profile for new links:</span></span>

- <span data-ttu-id="1b16a-110">Dans Microsoft Edge, ouvrez `edge://settings/profiles/multiProfileSettings` .</span><span class="sxs-lookup"><span data-stu-id="1b16a-110">In Microsoft Edge, open `edge://settings/profiles/multiProfileSettings`.</span></span>
- <span data-ttu-id="1b16a-111">Désactiver le **basculement automatique des profils.**</span><span class="sxs-lookup"><span data-stu-id="1b16a-111">Turn off **Automatic profile switching**.</span></span>
- <span data-ttu-id="1b16a-112">Pour le profil **par défaut pour les liens externes,** **sélectionnez Dernier utilisé (par défaut).**</span><span class="sxs-lookup"><span data-stu-id="1b16a-112">For the **Default profile for external links**, select **Last used (default)**.</span></span>

<span data-ttu-id="1b16a-113">Assurez-vous que votre navigateur est ouvert au profil correct avant de déboguer votre application.</span><span class="sxs-lookup"><span data-stu-id="1b16a-113">Ensure your browser is opened to the correct profile before debugging your app.</span></span>
