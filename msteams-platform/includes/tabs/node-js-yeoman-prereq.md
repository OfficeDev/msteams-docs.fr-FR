## <a name="prerequisites"></a>Conditions préalables

- Pour terminer ce démarrage rapide, vous aurez besoin d’un client Office 365 et d’une équipe configurée avec l’option *autoriser le téléchargement d’applications personnalisées* . Pour en savoir plus, consultez [la rubrique préparer votre client Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

  - Si vous ne disposez pas d’un compte Office 365, vous pouvez vous inscrire pour obtenir un abonnement gratuit via le programme de développement Office 365. L’abonnement reste actif tant que vous l’utilisez pour le développement continu. Consultez [la page Bienvenue dans le programme pour les développeurs Office 365](/OfficeDev/office-dev-program-docs/docs/office-365-developer-program.md).

De plus, ce projet requiert que les éléments suivants soient installés dans votre environnement de développement :

- N’importe quel éditeur de texte ou IDE. Vous pouvez installer et utiliser [Visual Studio code](https://code.visualstudio.com/download) gratuitement.

- [Node. js/NPM](https://nodejs.org/en/). Vous devez utiliser la dernière version d’LTS. Le gestionnaire de package de nœuds (NPM) s’installe dans votre système avec l’installation de node. js.

- Une fois que vous avez installé node. js, installez les packages [Yeoman](https://yeoman.io/) et [Gulp-CLI](https://www.npmjs.com/package/gulp-cli) en tapant ce qui suit dans votre invite de commandes :

```bash
npm install yo gulp-cli --global
```

- Installez le générateur d’applications Microsoft teams en tapant ce qui suit dans votre invite de commandes :

```bash
npm install generator-teams --global
```

## <a name="generate-your-project"></a>Générer votre projet

- Ouvrez une invite de commandes et créez un nouveau répertoire pour votre projet d’onglet.

- Pour démarrer le générateur, accédez à votre nouveau répertoire et tapez la commande suivante :

```bash
yo teams
```

- Ensuite, vous devez fournir une série de valeurs qui seront utilisées dans le fichier **Manifest. JSON** de votre application :

![capture d’écran d’ouverture du générateur](/microsoftteams/platform/assets/images/tab-images/teamsTabScreenshot.PNG)

**Quel est le nom de votre solution ?**

Il s’agit de votre nom de projet. Vous pouvez accepter le nom suggéré en appuyant sur entrée.

**Où souhaitez-vous placer les fichiers ?**

Vous êtes actuellement dans le répertoire de votre projet. Appuyez sur entrée.

**Titre de votre projet d’application Microsoft teams ?**

Il s’agit du nom de votre package d’application et sera utilisé dans le manifeste de l’application et sa description.

**Votre nom (société) ? (32 caractères max.)**

Le nom de votre société sera utilisé dans le manifeste de l’application.

<br>**Quelle version de manifeste souhaitez-vous utiliser ?**

Sélectionnez le schéma par défaut.

**Entrez votre ID partenaire Microsoft, si vous en avez un ? (Laissez le champ vide pour sauter)**

Ce champ n’est pas obligatoire et doit être utilisé uniquement si vous faites déjà partie du [réseau partenaire de Microsoft](https://partner.microsoft.com).

**Que voulez-vous ajouter à votre projet ?**

&ast; Sélectionnez un onglet.

**L’URL où vous allez héberger cette solution ?**

Par défaut, le générateur suggère une URL de sites Web Azure. Vous testez uniquement votre application localement, par conséquent, une URL valide n’est pas nécessaire pour effectuer ce démarrage rapide.

**Voulez-vous inclure l’infrastructure de test et les tests initiaux ? (o/N)**

Choisissez de **ne pas** inclure d’infrastructure de test pour ce projet. La valeur par défaut est oui ; entrez **n**.

**Voulez-vous utiliser les analyses des applications Azure pour la télémétrie ? (o/N)**

Choisissez de **ne pas** inclure les informations d' [application Azure](/azure-docs/articles/azure-monitor/app/app-insights-overview.md). La valeur par défaut est non ; entrez **n**.

**Nom d’onglet par défaut (16 caractères maximum) ?**

Nommez votre onglet. Ce nom d’onglet sera utilisé dans votre projet en tant que composant de chemin d’accès de fichier/URL.
