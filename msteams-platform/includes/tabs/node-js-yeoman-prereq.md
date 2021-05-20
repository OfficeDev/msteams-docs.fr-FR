## <a name="prerequisites"></a>Conditions préalables

- Pour compléter ce démarrage rapide, vous aurez besoin d’un Office 365 locataire et d’une équipe configurée avec *autoriser le téléchargement d’applications personnalisées activées.* Pour en savoir plus, [consultez Préparer votre Office 365 locataire.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

  - Si vous n’avez pas actuellement de compte Office 365, vous pouvez vous inscrire à un abonnement gratuit via le programme Office 365 développeur. L’abonnement restera actif tant que vous l’utilisez pour le développement continu. Voir [Bienvenue dans le programme Office 365 développeur de la ville](/office/developer-program/microsoft-365-developer-program).

En outre, ce projet exige que vous avez ce qui suit installé dans votre environnement de développement:

- Tout éditeur de texte ou IDE. Vous pouvez installer et [utiliser Visual Studio Code](https://code.visualstudio.com/download) gratuitement.

- [Node.js/npm](https://nodejs.org/en/). Vous devez utiliser la dernière version LTS. Le nœud Gestionnaire de package (npm) s’installera dans votre système avec l’installation de Node.js.

- Une fois que vous avez installé avec succès Node.js, installez [les paquets Yeoman](https://yeoman.io/) [et gulp-cli](https://www.npmjs.com/package/gulp-cli) en tapant ce qui suit dans votre invite de commande :

    ```bash
    npm install yo gulp-cli --global
    ```

- Installez le Microsoft Teams apps en tapant ce qui suit dans votre invite de commande :

    ```bash
    npm install generator-teams --global
    ```

## <a name="generate-your-project"></a>Générer votre projet

- Ouvrez une invite de commande et créez un nouvel annuaire pour votre projet d’onglet.

- Pour démarrer le générateur, accédez à votre nouvel annuaire et tapez la commande suivante :

    ```bash
    yo teams
    ```

- Ensuite, vous fournirez une série de valeurs qui seront utilisées dans les données de votre application **manifest.jsdans le** fichier :

    ![capture d’écran d’ouverture de générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

    **Quel est le nom de votre solution ?**

    C’est le nom de votre projet. Vous pouvez accepter le nom suggéré en appuyant sur entrer.

    **Où souhaitez-vous placer les fichiers ?**

    Vous êtes actuellement dans votre répertoire de projet. Appuyez sur entrez.

    **Titre de votre projet Microsoft Teams apprappe ?**

    Il s’agit du nom de votre paquet d’application et sera utilisé dans le manifeste et la description de l’application.

    **Votre nom (d’entreprise)? (max 32 caractères)**

    Le nom de votre entreprise sera utilisé dans le manifeste de l’application.

    **Quelle version manifeste souhaitez-vous utiliser ?**

    Sélectionnez le schéma par défaut.

    **Un échafaudage rapide ? (Y/n)**

    La valeur par défaut est oui; entrez **n** pour entrer votre identifiant de partenaire Microsoft.

    **Entrez votre identifiant microsoft partner, si vous en avez un ? (Laisser vide pour sauter)**

    Ce champ n’est pas nécessaire et ne doit être utilisé que si vous faites déjà partie du [Réseau partenaire Microsoft](https://partner.microsoft.com).

    **Qu’est-ce que vous voulez ajouter à votre projet?**

    Sélectionnez ( &ast; ) Un onglet.

    **L’URL où vous hébergez cette solution ?**

    Par défaut, le générateur suggère une URL de sites Web Azure. Vous ne testerez votre application que localement, par conséquent, une URL valide n’est pas nécessaire pour compléter ce démarrage rapide.

    **Souhaitez-vous inclure le cadre de test et les tests initiaux? (y/N)**

    Choisissez **de ne** pas inclure de cadre de test pour ce projet. La valeur par défaut est oui; entrer **n**.

    **Souhaitez-vous utiliser Azure Applications Insights pour la télémétrie ? (y/N)**

    Choisissez **de ne** pas inclure [Azure Application Insights](/azure-docs/articles/azure-monitor/app/app-insights-overview.md). La valeur par défaut est non; entrer **n**.

    **Nom de l’onglet par défaut (max 16 caractères)?**

    Nommez votre onglet. Ce nom d’onglet sera utilisé tout au long de votre projet comme composant de chemin de fichier/URL.
