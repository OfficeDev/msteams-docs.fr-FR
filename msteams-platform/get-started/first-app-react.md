---
title: Prise en main :cCréez votre première application Teams avec React
author: adrianhall
description: Créez rapidement une application Microsoft Teams qui affiche un message « Hello, World ! » message à l’aide du Kit de ressources Microsoft Teams et de React.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: edd7cf8048dd89156b4b91afecb329d91baf3f53
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994113"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a>Créer et exécuter votre première application Microsoft Teams avec React

Dans ce didacticiel, vous allez créer une application Microsoft Teams dans React qui implémente une application personnelle simple pour extraire des informations du Microsoft Graph. Par exemple, une *application personnelle inclut* un ensemble d’onglets inclus pour une utilisation individuelle. Au cours du didacticiel, vous allez découvrir la structure d’une application Teams, comment exécuter une application localement et comment déployer l’application sur Azure.

L'application créée affiche des informations de base sur l'utilisateur actuel. Lorsque l'autorisation est accordée, l'application se connecte au Microsoft Graph en tant qu'utilisateur actuel pour obtenir le profil complet.

## <a name="before-you-begin"></a>Avant de commencer

Assurez-vous que votre environnement de développement est installé en installant les [conditions préalables.](prerequisites.md)

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)

## <a name="create-your-project"></a>Créer votre projet

Utilisez le Kit de ressources Teams pou créer votre premier projet :

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Ouvrez Visual Studio Code.
1. Ouvrez le Kit de ressources Teams en sélectionnant l’icône Teams dans la barre latérale :

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. Sélectionnez **Création d’un projet**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. Sélectionnez **Créer une application Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. À **l’étape Sélectionner les fonctionnalités,** la fonctionnalité **Onglet** est déjà sélectionnée. Appuyez sur **OK**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. À l’étape **Type d’hébergement frontal**, sélectionnez **Azure**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="Capture d’écran présentant comment sélectionner l’hébergement pour votre nouvelle application.":::

1. À l’étape **Ressources cloud**, appuyez sur **OK**.  Nous n’avons pas besoin de ressources cloud supplémentaires pour ce didacticiel.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="Capture d’écran présentant comment ajouter des ressources cloud à votre nouvelle application.":::

1. À l’étape **Langage de programmation**, sélectionnez **JavaScript**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. Sélectionnez un dossier d’espace de travail. Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.

1. Entrez un nom approprié pour votre application, tel que `helloworld`. Le nom de l’application doit contenir des caractères alphanumériques uniquement.  Appuyez sur **Entrer** pour continuer.

Votre application Teams est créée en quelques secondes.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

Utilisez le CLI `teamsfx` pou créer votre premier projet.  Commencez à partir du dossier dans lequel vous souhaitez créer le dossier du projet.

``` bash
teamsfx new
```

Le CLI parcourt quelques questions pour créer le projet. Chaque question vous indique comment y répondre, par exemple, utilisez des touches de direction pour sélectionner une option. Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.

1. Sélectionnez **Créer une application Teams**.
1. Choisissez la fonctionnalité **Onglet**.
1. Sélectionnez l'hébergement frontal **Azure**.
1. Ne sélectionnez aucune ressource cloud.
1. Sélectionnez **JavaScript** comme langage de programmation.
1. Appuyez sur **Entrée** pour sélectionner le dossier de l’espace de travail par défaut.
1. Entrez un nom approprié pour votre application, tel que `helloworld`.  Le nom de l’application doit contenir des caractères alphanumériques uniquement.

Une fois toutes les questions auxquelles vous avez répondu, votre projet est créé.

---

## <a name="take-a-tour-of-the-source-code"></a>Suivre une visite guidée du code source

Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).

Une fois que le Kit de ressources Teams a configuré votre projet, vous disposez des composants pour créer une application personnelle de base pour Teams. Les répertoires et les fichiers du projet s'affichent dans la zone Explorateur de Visual Studio Code.

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="Capture d’écran présentant les fichiers projet d’application pour une application personnelle dans Visual Studio Code.":::

Le Kit de ressources crée automatiquement une structure pour vous dans le répertoire du projet en fonction des fonctionnalités que vous avez ajoutées lors de l’installation. Le Kit de ressources Teams conserve son état pour votre application dans le répertoire `.fx`.  Parmi les autres éléments de ce répertoire :

- Les icônes d’application sont stockées sous forme de fichiers PNG dans `color.png` et `outline.png`.
- Le manifeste de l'application pour la publication sur le portail des développeurs pour Teams est stocké dans `manifest.source.json`.
- Les paramètres que vous avez choisis lors de la création du projet sont stockés dans `settings.json`.

Comme vous avez sélectionné la fonctionnalité d’onglet lors de l’installation, le Kit de ressources Teams génère automatiquement tout le code nécessaire pour un onglet de base dans le répertoire `tabs`. Ce répertoire contient plusieurs fichiers importants :

- `tabs/src/index.jsx` est le point d’entrée de l’application frontale, où le composant principal `App` est rendu avec `ReactDOM.render()`.
- `tabs/src/components/App.jsx` gère le routage d’URL dans votre application. Il appelle le [Kit de développement logiciel (SDK) client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) pour établir une communication entre votre application et Teams.
- `tabs/src/components/Tab.jsx` contient le code pour implémenter l’interface utilisateur de votre application.
- `tabs/src/components/TabConfig.jsx` contient le code pour implémenter l’interface utilisateur qui configure votre application.

Plusieurs onglets sont requis par le runtime Teams, notamment l’avis de confidentialité, les conditions d’utilisation et les onglets de configuration.  Le code de l’avis de confidentialité et des conditions d’utilisation se trouve dans le même répertoire.

Lorsque vous ajoutez des fonctionnalités cloud, des répertoires supplémentaires sont ajoutés au projet.  Plus particulièrement, le répertoire `api` contient le code de tout Azure Functions que vous écrivez.

## <a name="run-your-app-locally"></a>Exécuter votre application localement

Le Kit de ressources Teams vous permet d’exécuter votre application localement.  Il s’agit de plusieurs parties nécessaires pour fournir l’infrastructure correcte attendue par Teams :

- Une application est inscrite auprès de Azure Active Directory.  Cette application dispose d’autorisations associées à l’emplacement à partir duquel l’application est chargée et aux ressources principales auxquelles elle accède.
- Une API web est hébergée pour faciliter les tâches d’authentification, en agissant comme un proxy entre l’application et Azure Active Directory.  Cette opération est exécutée par Azure Functions Core Tools.  Il est accessible à l’URL `https://localhost:5000`.
- Les ressources HTML, CSS et JavaScript qui composent le serveur frontal de l’application sont hébergées sur un service local. Il est accessible à `https://localhost:3000`.
- Un manifeste d'application est généré et existe dans le portail des développeurs pour Teams.  Teams utilise le manifeste de l’application pour indiquer aux clients connectés où charger l’application.

Une fois cette opération effectuée, l’application peut être chargée dans le client Teams.  Nous utilisons le client web Teams pour voir le code HTML, CSS et JavaScript dans un environnement de développement web standard.

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>Générez et exécutez votre application localement dans Visual Studio Code

Pour créer et exécuter votre application localement :

1. À partir de Visual Studio Code, appuyez sur **F5** pour exécuter votre application dans le mode de débogage.

   > Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.  Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.  Cette finalisation peut prendre entre 3 et 5 minutes.

   Le Shared Computer Toolkit vous invite à installer un certificat local si nécessaire. Ce certificat permet à Teams de charger votre application à partir de `https://localhost`. Sélectionnez Oui lorsque la boîte de dialogue suivante s’affiche :

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="Capture d’écran présentant comment l’invite à installer un certificat SSL pour permettre à Teams de charger votre application à partir de localhost.":::

1. Votre navigateur web commence à exécuter l’application. Si vous êtes invité à ouvrir Teams bureau, sélectionnez **Annuler** pour rester dans le navigateur. Vous pouvez également être invité à basculer vers Teams bureau à d’autres moments ; sélectionnez l Teams’application web lorsque cela se produit.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Capture d’écran présentant la façon de choisir la version web de Teams lors du lancement":::

1. Vous serez peut-être invité à vous connecter.  Dans ce cas, connectez-vous à l'aide de votre compte M365.
1. Lorsque vous êtes invité à installer l’application sur Teams, appuyez sur **Ajouter**.

Votre application s’affiche désormais :

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="Capture d’écran de l’application terminée":::

Vous pouvez faire des activités de débogage normales comme s’il s’avait été une autre application web, telle que la définition de points d’arrêt. L’application prend en charge le rechargement à chaud. Si vous modifiez un fichier dans le projet, la page est rechargée.

<!-- markdownlint-disable MD033 -->
<details>
<summary>Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogueur.</summary>

Lorsque vous appuyez sur F5, le Kit de ressources Teams :

1. Votre application a été inscrite dans Azure Active Directory.
1. *A chargés indépendamment* votre application dans Teams.
1. A démarré votre serveur principal d’application s’exécutant localement en utilisant [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).
1. Démarrage de votre application frontale hébergée localement.
1. Démarré Microsoft Teams dans un navigateur web avec une commande pour indiquer Teams charger l’application de côté à partir `https://localhost:3000/tab` de . Il s’agit de l’URL inscrite dans le manifeste de l’application.

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>Découvrez comment résoudre les problèmes courants lorsque vous exécutez votre application localement.</summary>

Pour exécuter correctement votre application dans Teams, vous devez avoir un compte Teams qui permet le chargement de version test d’une application. Pour plus d’informations sur l’ouverture d’un compte, voir [Conditions préalables](prerequisites.md#enable-sideloading).

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary>Découvrir ce qui se produit lorsque vous avez déployé votre application vers Azure</summary>

Avant le déploiement, l’application s’est exécutée localement :

1. Le serveur principal s’exécute en utilisant **Azure Functions Core Tools**.
1. Le point de terminaison HTTP de l’application, dans lequel Microsoft Teams charge l’application, s’exécute localement.

Le déploiement implique l’approvisionnement de ressources sur un abonnement Azure actif et le déploiement ou le chargement du code frontal et frontal de l’application vers Azure.

1. Le système back-end, s’il est configuré, utilise divers services Azure, notamment Azure App Service et Azure Storage.
1. L’application frontale sera déployée sur un compte de stockage Azure configuré pour l’hébergement web statique.

</details>

## <a name="see-also"></a>Voir aussi

- [Créer une application Teams à l’aide de Blazor](first-app-blazor.md)
- [Créer une application Teams en tant que composant WebPart SharePoint](first-app-spfx.md) (Azure non requis)
- [Créer une application de bot de conversation](first-app-bot.md)
- [Créer une extension de messagerie](first-message-extension.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer une application Teams à l’aide de Blazor](first-app-blazor.md)
