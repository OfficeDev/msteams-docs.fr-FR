## <a name="prerequisites"></a>Conditions préalables

- Pour effectuer ce démarrage rapide, vous aurez besoin d’un client Microsoft 365 et d’une équipe configurée avec autoriser le téléchargement *d’applications* personnalisées activée. Pour plus d’informations, voir [Préparer Microsoft 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)
  - Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire à un abonnement gratuit via le programme [pour les développeurs Microsoft.](https://developer.microsoft.com/en-us/microsoft-365/dev-program) L’abonnement reste actif tant que vous l’utilisez pour le développement en cours.

- Vous utiliserez App Studio pour importer votre application dans Teams. Pour installer App Studio, sélectionnez **App** Store dans le coin inférieur gauche de ![ l’application Teams et ](~/assets/images/tab-images/storeApp.png) recherchez App Studio. Une fois que vous avez trouvé la vignette, sélectionnez-la et choisissez d’installer dans la boîte de dialogue fenêtre pop-up.

En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :

- Version actuelle de l Visual Studio ide avec la charge de travail de développement **.NET CORE sur plusieurs** plateformes installée. Si vous n’avez pas encore Visual Studio, vous pouvez télécharger et installer la dernière version [Microsoft Visual Studio Community](https://visualstudio.microsoft.com/downloads) gratuitement.

- Outil de proxy inverse [ngrok.](https://ngrok.com) Vous utiliserez ngrok pour créer un tunnel vers les points de terminaison HTTPS disponibles publiquement de votre serveur web exécutant localement. Vous pouvez [le télécharger ici.](https://ngrok.com/download)
