## <a name="prerequisites"></a>Conditions préalables

- Pour effectuer ce démarrage rapide, vous aurez besoin d’un client Office 365 et d’une équipe configurée avec autoriser le téléchargement *d’applications* personnalisées activée. Pour plus d’informations, voir [Préparer Office 365 client.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

  - Si vous n’avez pas de compte Office 365, vous pouvez vous inscrire à un abonnement gratuit via le programme Office 365 développeur. L’abonnement reste actif tant que vous l’utilisez pour le développement en cours. Voir [Bienvenue dans le programme Office 365 développeur.](/office/developer-program/microsoft-365-developer-program)

En outre, ce projet nécessite que les logiciels suivants sont installés dans votre environnement de développement :

- N’importe quel éditeur de texte ou IDE. Vous pouvez installer et utiliser [Visual Studio Code](https://code.visualstudio.com/download) gratuitement.

- [Node.js/npm](https://nodejs.org/en/). Vous devez utiliser la dernière version de LTS. Le nœud Gestionnaire de package (npm) s’installera dans votre système avec l’installation de Node.js.

- Une fois que vous avez installé Node.js, installez les packages [Yeoman](https://yeoman.io/) et [gulp-cli](https://www.npmjs.com/package/gulp-cli) en tapant ce qui suit dans votre invite de commandes :

    ```bash
    npm install yo gulp-cli --global
    ```

- Installez le générateur Microsoft Teams Apps en tapant ce qui suit dans votre invite de commandes :

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a>Générer votre projet

- Ouvrez une invite de commandes et créez un répertoire pour votre projet d’onglet.

- Pour démarrer le générateur, accédez à votre nouveau répertoire et tapez la commande suivante :

    ```bash
    yo teams
    ```

- Ensuite, vous allez fournir une série de valeurs qui seront utilisées dans le fichier **manifest.jsvotre** application :

    ![capture d’écran d’ouverture du générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    **Quel est le nom de votre solution ?**

    Il s’agit du nom de votre projet. Vous pouvez accepter le nom suggéré en appuyant sur Entrée.

    **Où souhaitez-vous placer les fichiers ?**

    Vous êtes actuellement dans votre répertoire de projet. Appuyez sur Entrée.

    **Titre de votre Microsoft Teams d’application ?**

    Il s’agit du nom de votre package d’application qui sera utilisé dans le manifeste et la description de l’application.

    **Votre nom (d’entreprise) ? (32 caractères maximum)**

    Le nom de votre société sera utilisé dans le manifeste de l’application.

    **Quelle version de manifeste souhaitez-vous utiliser ?**

    Sélectionnez le schéma par défaut.

    **La échafaudage rapide ? (Y/n)**

    La valeur par défaut est Oui ; entrez **n** pour entrer votre ID partenaire Microsoft.

    **Entrez votre ID partenaire Microsoft, si vous en avez un ? (Laissez vide pour ignorer)**

    Ce champ n’est pas obligatoire et ne doit être utilisé que si vous faites déjà partie de [Microsoft Partner Network](https://partner.microsoft.com).

    **Que voulez-vous ajouter à votre projet ?**

    Sélectionnez ( &ast; ) Un onglet.

    **L’URL dans laquelle vous hébergez cette solution ?**

    Par défaut, le générateur suggère une URL de sites web Azure. Vous testerez uniquement votre application localement, par conséquent, une URL valide n’est pas nécessaire pour effectuer ce démarrage rapide.

    **Souhaitez-vous inclure l’infrastructure test et les tests initiaux ? (y/N)**

    Choisissez **de ne** pas inclure d’infrastructure de test pour ce projet. La valeur par défaut est Oui ; entrez **n**.

    **Voulez-vous utiliser Azure Applications Insights pour la télémétrie ? (y/N)**

    Choisissez **de ne** pas inclure Azure Application [Insights](/azure/azure-monitor/app/app-insights-overview). La valeur par défaut est non ; entrez **n**.

    **Nom de l’onglet par défaut (16 caractères maximum) ?**

    Nommez votre onglet. Ce nom d’onglet sera utilisé dans l’ensemble de votre projet en tant que composant de chemin d’accès fichier/URL.
