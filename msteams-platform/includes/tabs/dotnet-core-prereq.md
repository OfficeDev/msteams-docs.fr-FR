## <a name="prerequisites"></a>Conditions préalables

- Pour terminer ce démarrage rapide, vous aurez besoin d’un client Office 365 et d’une équipe configurée avec l’option *autoriser le téléchargement d’applications personnalisées* . Pour en savoir plus, consultez [la rubrique préparer votre client Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).
  - Si vous ne disposez pas d’un compte Office 365, vous pouvez vous inscrire pour obtenir un abonnement gratuit via le [programme de développement office 365](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program). L’abonnement reste actif tant que vous l’utilisez pour le développement continu.

- Vous utiliserez App Studio pour importer votre application dans Teams. Pour installer App Studio, **sélectionnez App** ![Store](~/assets/images/tab-images/storeApp.png) app dans le coin inférieur gauche de l’application Teams, puis recherchez App Studio. Une fois que vous avez trouvé la vignette, sélectionnez-la et choisissez installer dans la boîte de dialogue fenêtre contextuelle.

De plus, ce projet requiert que les éléments suivants soient installés dans votre environnement de développement :

- Version actuelle de l’IDE Visual Studio avec la charge de travail de **développement multiplateforme .net** . Si vous ne disposez pas encore de Visual Studio, vous pouvez télécharger et installer la dernière version de la [communauté Microsoft Visual Studio](https://visualstudio.microsoft.com/downloads) gratuitement.

- Outil de proxy inverse [ngrok](https://ngrok.com) . Vous utiliserez ngrok pour créer un tunnel vers les points de terminaison HTTPs HTTPs disponibles localement pour votre serveur Web. Vous pouvez [le télécharger ici](https://ngrok.com/download).
