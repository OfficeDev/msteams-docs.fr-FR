---
title: 'Prise en main : créer votre premier bot de conversation'
author: adrianhall
description: Créez un bot de conversation pour Microsoft Teams à l’aide du Kit de ressources Teams.
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: 96bbddd99b6901a4b92e1e2f2dc98482c755dc66
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254250"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a>Créer votre premier bot de conversation pour Microsoft Teams

Dans ce didacticiel, vous découvrirez comment créer, exécuter et déployer une application bot Teams. Un bot agit en tant qu’intermédiaire entre un utilisateur Teams et un service web.  Les utilisateurs peuvent converser avec un bot pour obtenir rapidement des informations, initier des flux de travail ou tout autre action que votre service web peut effectuer. 

## <a name="before-you-begin"></a>Avant de commencer

Assurez-vous que votre environnement de développement est installé en installant les conditions préalables.

> [!div class="nextstepaction"]
> [Conditions préalables](prerequisites.md)

## <a name="create-your-project"></a>Créer votre projet

Utilisez le Kit de ressources Teams pou créer votre premier projet :

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Ouvrez Visual Studio Code.
1. Sélectionnez l Teams dans la barre latérale pour ouvrir le Teams Shared Computer Toolkit.

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Icône Teams dans la barre latérale Visual Studio Code.":::

1. Sélectionnez **Création d’un projet**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Emplacement du lien Création d’un projet dans la barre latérale du Kit de ressources Teams.":::

1. Sélectionnez **Créer une application Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Démarrage de l’Assistant pour la Création d’un projet":::

1. Dans la section **Sélectionner des fonctionnalités,** **sélectionnez Bot,** désélectionner **l’onglet** et **sélectionner OK.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. Dans la section **Inscription du** bot, **sélectionnez Créer une nouvelle inscription de bot.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Sélectionner l’inscription d’un nouveau bot":::

1. Dans la section **Langage de** programmation, **sélectionnez JavaScript.**

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. Sélectionnez un dossier d’espace de travail.  Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.

1. Entrez un nom approprié pour votre application, tel que `helloworld`.  Le nom de l’application doit contenir uniquement des caractères alphanumériques.  Appuyez sur **Entrer** pour continuer.

Votre application Teams est créée en quelques secondes.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

Utilisez le CLI `teamsfx` pou créer votre premier projet.  Commencez à partir du dossier dans lequel vous souhaitez créer le dossier du projet.

``` bash
teamsfx new
```

Le CLI parcourt quelques questions pour créer le projet.  Chaque question vous indiquera comment y répondre (par exemple, utiliser les touches de direction pour sélectionner une option).  Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.

1. Sélectionnez **Créer une application Teams**.
1. Sélectionnez **Bot** et désélection **de l’onglet.**
1. Sélectionner **Créer l’inscription d’un nouveau bot**.
1. Sélectionnez **JavaScript** comme langage de programmation.
1. Appuyez sur **Entrée** pour sélectionner le dossier de l’espace de travail par défaut.
1. Entrez un nom approprié pour votre application, tel que `helloworld`.  Le nom de l’application doit contenir des caractères alphanumériques uniquement.

Une fois toutes les questions auxquelles vous avez répondu, votre projet est créé.

---

## <a name="take-a-tour-of-the-source-code"></a>Suivre une visite guidée du code source

Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).

Une extension de messagerie utilise [Bot Framework](https://docs.botframework.com) pour autoriser l’utilisateur à interagir avec votre service via une conversation.  Après structuration, votre projet ressemble à ceci :

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="Disposition de fichier d’un projet bot.":::

Le code bot est stocké dans le répertoire `bot`.  Le `bot/teamsBot.js` est le point d’entrée principal pour le bot et les boîtes de dialogue sont stockées dans le répertoire `dialogs`.

> [!Tip]
> Familiarisez-vous avec les bots en dehors de Teams avant d’intégrer votre premier bot dans Teams.  Vous trouverez d’autres informations sur les bots en examinant les didacticiels [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).

## <a name="run-your-app-locally"></a>Exécuter votre application localement

Le Kit de ressources Teams vous permet d’héberger votre application localement.  Pour ce faire :

- Une application Azure Active Directory est inscrite dans le client M365.
- Un manifeste d’application est soumis au Centre des développeurs pour Teams.
- Une API est exécutée à l’aide d’Azure Functions Core Tools pour prendre en charge votre application.
- [ngrok](https://ngrok.io) est installé et utilisé pour fournir un tunnel entre Teams et votre code bot.

Pour créer et exécuter votre application localement :

1. À Visual Studio Code, appuyez sur la **touche F5** pour exécuter votre application en mode débogage.

   > Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.  Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.  Cette finalisation peut prendre entre 3 et 5 minutes.

1. Votre navigateur web commence à exécuter l’application. Si vous êtes invité à ouvrir Teams bureau, sélectionnez **Annuler** pour rester dans le navigateur. Vous pouvez également être invité à basculer vers Teams bureau à d’autres moments ; sélectionnez l Teams’application web lorsque cela se produit.

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="Capture d’écran présentant la façon de choisir la version web de Teams lors du lancement":::

1. Vous serez peut-être invité à vous connecter.  Dans ce cas, connectez-vous à l'aide de votre compte M365.
1. Lorsque vous y invitez l’application sur Teams, sélectionnez **Ajouter.**

   Une fois l’application chargée, vous êtes directement conduit à une session de conversation avec le bot.  Vous pouvez taper `intro` pour afficher une carte d’introduction et `show` pour présenter vos informations à partir de Microsoft Graph.  (Ceci nécessite une approbation d’autorisations supplémentaire).

   Le débogage fonctionne comme prévu. Essayez vous-même. Ouvrez le fichier `bot/dialogs/rootDialog.js`, puis localisez la méthode `triggerCommand(...)`.  Définissez un point d’arrêt sur le cas par défaut.  Puis tapez du texte.

<!-- markdownlint-disable MD033 -->
<details>
<summary>Découvrez ce qui se produit lorsque vous exécutez votre application localement dans le débogueur.</summary>

Lorsque vous appuyez sur **la touche F5,** le Teams Shared Computer Toolkit :

1. Inscrit votre application avec Azure Active Directory.
1. Inscrit votre application pour le « chargement de version latéral » dans Microsoft Teams.
1. Démarre le système principal de votre application en cours d’exécution localement à [l’aide des outils Azure Function Core](/azure/azure-functions/functions-run-local?#start).
1. Démarre un tunnel ngrok pour Teams communiquer avec votre application.
1. Démarre Microsoft Teams avec une commande pour indiquer Teams charger une version de version de l’application.

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>Découvrez comment résoudre les problèmes courants lorsque vous exécutez votre application localement.</summary>

Pour exécuter correctement votre application dans Teams, vous devez avoir un compte de développement Microsoft 365 qui permet le chargement de version test d’une application. Pour plus d’informations sur l’ouverture d’un compte, voir [Conditions préalables](prerequisites.md#enable-sideloading).

> [!TIP]
> Vérifier l’absence de problèmes avant de charger la version test de votre application en utilisant [l’outil de validation d’application](https://dev.teams.microsoft.com/appvalidation.html) qui est inclus dans le kit de ressources. Corrigez les erreurs pour charger correctement la version test de l’application.
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary>Découvrir ce qui se produit lorsque vous avez déployé votre application vers Azure</summary>

Avant le déploiement, l’application s’est exécutée localement :

1. Le serveur principal s’exécute en utilisant _Azure Functions Core Tools_.
1. Le point de terminaison HTTP de l’application, dans lequel Microsoft Teams charge l’application, s’exécute localement.

   Le déploiement implique la mise en service de ressources sur un abonnement Azure actif et le déploiement (chargement) du code du serveur principal et du serveur frontal pour l’application vers Azure. Le serveur principal utilise une variété de services Azure, notamment Azure App Service et Azure Bot Service.

</details>

## <a name="see-also"></a>Voir aussi

* [Présentation des didacticiels](code-samples.md) 
* [Créer une application à l’aide React](first-app-react.md)
* [Créer une application à l’aide de Blazor](first-app-blazor.md)
* [Créer une application à l’aide SPFx](first-app-spfx.md)
* [Créer une application en utilisant C# ou .NET](get-started-dotnet-app-studio.md)
* [Créer une application en utilisant Node.js](get-started-nodejs-app-studio.md)
* [Créer une application à l’aide du générateur Yeoman](get-started-yeoman.md)
* [Créer une extension de messagerie](first-message-extension.md)
* [Exemples de code](https://github.com/OfficeDev/Microsoft-Teams-Samples)