---
title: 'Prise en main : créer votre première extension de messagerie'
author: adrianhall
description: Créez une extension de messagerie pour Microsoft Teams à l’aide du Kit de ressources Teams.
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: 3566bc55c9995a8407b1344fbdb7d1548e210046
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254287"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a>Créez et exécutez votre première extension de messagerie basée sur la recherche dans Microsoft Teams

Dans ce didacticiel, vous  allez apprendre à créer une commande de recherche pour rechercher des données externes et insérer les résultats dans un message. 

Il existe deux types **d’extension de messagerie** Teams :

- Les [commandes de recherche](../messaging-extensions/how-to/search-commands/define-search-command.md) vous permettent d’effectuer une recherche dans des systèmes externes et d’insérer les résultats de la recherche dans un message sous la forme d’une carte.
- Les [commandes d’action](../messaging-extensions/how-to/action-commands/define-action-command.md) vous permettent de présenter vos utilisateurs à l’aide d’un menu contextuel modal pour collecter ou afficher des informations, puis de traiter leur interaction et de renvoyer les informations à Teams.

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

1. Dans la section **Sélectionner des fonctionnalités,** **sélectionnez Extension de message,** **Désélectionner l’onglet** et **sélectionner OK.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="Capture d’écran présentant comment ajouter des fonctionnalités à votre nouvelle application.":::

1. Dans la section **Inscription du** bot, **sélectionnez Créer une nouvelle inscription de bot.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Sélectionner l’inscription d’un nouveau bot":::

   > [!NOTE]
   > Les extensions de messagerie ont recours à des bots pour fournir un dialogue entre l’utilisateur et votre code.

1. Dans la section **Langage de** programmation, **sélectionnez JavaScript.**

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Capture d’écran présentant comment sélectionner le langage de programmation.":::

1. Sélectionnez un dossier d’espace de travail.  Un dossier est créé dans votre dossier d’espace de travail pour le projet que vous créez.

1. Entrez un nom approprié pour votre application, tel que `helloworld`.  Le nom de l’application doit contenir des caractères alphanumériques uniquement.  Appuyez sur **Entrer** pour continuer.

   Votre application Teams est créée en quelques secondes.

# <a name="command-line"></a>[Ligne de commande](#tab/cli)

Utilisez le CLI `teamsfx` pou créer votre premier projet.  Commencez à partir du dossier dans lequel vous souhaitez créer le dossier du projet.

``` bash
teamsfx new
```

Le CLI parcourt quelques questions pour créer le projet.  Chaque question vous indiquera comment y répondre (par exemple, utiliser les touches de direction pour sélectionner une option).  Lorsque vous avez répondu à la question, confirmez votre choix en appuyant sur **Entrée**.

1. Sélectionnez **Créer une application Teams**.
1. Sélectionnez **l’extension de message** et désélectionne **l’onglet**.
1. Sélectionner **Créer l’inscription d’un nouveau bot**.
1. Sélectionnez **JavaScript** comme langage de programmation.
1. Appuyez sur **Entrée** pour sélectionner le dossier de l’espace de travail par défaut.
1. Entrez un nom approprié pour votre application, tel que `helloworld`.  Le nom de l’application doit contenir des caractères alphanumériques uniquement.

   Une fois toutes les questions auxquelles vous avez répondu, votre projet est créé.

---

## <a name="take-a-tour-of-the-source-code"></a>Suivre une visite guidée du code source

Si vous souhaitez ignorer cette section pour le moment, vous pouvez [exécuter votre application localement](#run-your-app-locally).

Une extension de messagerie utilise [Bot Framework](https://docs.botframework.com) pour autoriser l’utilisateur à interagir avec votre service via une conversation.  Après structuration, votre projet ressemble à ceci :

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="Disposition de fichier d’un projet bot.":::

Le code bot est stocké dans le répertoire `bot`.  Le `bot/messageExtensionBot.js` est le principal point d’entrée pour l’extension de messagerie.

> [!Tip]
> Familiarisez-vous avec les bots en dehors de Teams avant d’intégrer votre premier bot dans Teams.  Vous trouverez d’autres informations sur les bots en examinant les didacticiels [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).

## <a name="run-your-app-locally"></a>Exécuter votre application localement

Le Kit de ressources Teams vous permet d’héberger votre application localement.  Pour ce faire :

- Une application Azure Active Directory est inscrite dans le client M365.
- Un manifeste d’application est soumis au Portail des développeurs pour Teams.
- Une API est exécutée à l’aide d’Azure Functions Core Tools pour prendre en charge votre application.
- [ngrok](https://ngrok.io) est installé et utilisé pour fournir un tunnel entre Teams et votre extension de messagerie.

Pour créer et exécuter votre application localement :

1. À Visual Studio Code, appuyez sur la **touche F5** pour exécuter votre application en mode débogage.

   > Lorsque vous exécutez l’application pour la première fois, toutes les dépendances sont téléchargées et l’application est créée.  Une fenêtre de navigateur s’ouvre automatiquement lors la build est terminée.  Cette finalisation peut prendre entre 3 et 5 minutes.

1. Teams sera chargée dans un navigateur web et vous serez invité à vous connecter. Si vous êtes invité à ouvrir Microsoft Teams, sélectionnez Annuler pour rester dans le navigateur. Connectez-vous à votre compte M365.

1. Sélectionnez **Ajouter** pour ajouter l’application à votre compte.

   Une fois l’application chargée, vous êtes directement placé dans une boîte de dialogue de recherche :

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="Votre extension de messagerie basée sur la recherche en action":::

   Tapez un texte dans la zone de recherche, puis sélectionnez l’une des options.  Une carte adaptative s’ajoute à votre zone d’entrée.

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

## <a name="add-a-configuration-page-to-your-messaging-extension"></a>Ajouter une page de configuration à votre extension de messagerie

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a>Exemple de code

La Teams d’authentification de recherche pour les exemples de projets sur GitHub, montrent comment créer des extensions de messagerie qui incluent une page de configuration et l’authentification [bot service](https://github.com/microsoft/BotBuilder-Samples#teams-samples). Les exemples montrent également comment créer des extensions de message qui acceptent les demandes de recherche et retournent les résultats une fois que l’utilisateur s’est inscrit.

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|-----------------|-----------------|-------------|--------------|--------|
| Générateur de bot | Pour créer des extensions de messagerie. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [View]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a>Exemple de code supplémentaire

> [!div class="nextstepaction"]
> [Afficher d’autres exemples Bot Framework sur GitHub](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a>Voir aussi

* [Présentation des didacticiels](code-samples.md) 
* [Créer une application à l’aide React](first-app-react.md)
* [Créer une application à l’aide de Blazor](first-app-blazor.md)
* [Créer une application à l’aide SPFx](first-app-spfx.md)
* [Créer une application en utilisant C# ou .NET](get-started-dotnet-app-studio.md)
* [Créer une application en utilisant Node.js](get-started-nodejs-app-studio.md)
* [Créer une application à l’aide du générateur Yeoman](get-started-yeoman.md)
* [Créer une application de bot de conversation](first-app-bot.md)
* [Exemples de code](https://github.com/OfficeDev/Microsoft-Teams-Samples)