---
title: Étendre une extension de message Teams dans Microsoft 365
description: Dans cet article, vous découvrirez comment mettre à jour l’extension de message Teams basée sur la recherche pour qu’elle s’exécute dans Outlook en mettant à jour le manifeste de l’application, en ajoutant un canal Outlook et en chargeant l’application mise à jour.
ms.date: 05/24/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 2fc0a66683bb5454bfb8fbced64e97618522fce7
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243513"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Étendre une extension de message Teams dans Microsoft 365

Les [message extensions](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) permettent aux utilisateurs de rechercher dans un système externe et de partager des résultats via la zone de message de composition du client Microsoft Teams. En [étendant vos applications Teams à Microsoft 365](overview.md), vous pouvez désormais proposer des extensions de message Teams basées sur la recherche de production pour afficher un aperçu des audiences dans Outlook pour Windows desktop et outlook.com.

Le processus de mise à jour de votre extension de message Teams basée sur la recherche pour exécuter Outlook implique les étapes suivantes :

> [!div class="checklist"]
>
> * Mettez à jour le manifeste de votre application.
> * Ajoutez un canal Outlook pour votre bot.
> * Chargez une version test de votre application mise à jour dans Teams.

Le reste de ce guide vous oriente tout au long de ces étapes et vous montre comment afficher un aperçu de votre extension de message dans Outlook pour Windows desktop et outlook.com.

## <a name="prerequisites"></a>Configuration requise

Pour suivre ce didacticiel, vous avez besoin des éléments suivants :

* Un locataire de bac à sable du programme Microsoft 365 Developer.
* Inscription dans les *Versions ciblées d’Office 365* pour votre client de bac à sable.
* Un environnement de test avec les applications Office installées à partir du *Canal bêta* de Microsoft 365 Apps.
* (Facultatif) Microsoft Visual Studio Code avec l’extension du Kit de ressources Teams.

> [!div class="nextstepaction"]
> [Publier des applications Teams étendues pour Microsoft 365](publish.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>Préparer votre extension de message pour la mise à niveau

Si vous disposez d’une extension de message existante en production, effectuez une copie ou une branche de votre projet pour tester et mettre à jour votre ID d’application dans le manifeste de l’application afin d’utiliser un nouvel identificateur (distinct de l’ID d’application de production, à des fins de test).

Si vous souhaitez utiliser un exemple de code pour suivre le tutoriel complet sur la mise à jour d’une application Teams existante, suivez les étapes de configuration de [l’exemple de recherche d’extension de message Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) pour créer rapidement une extension de message basée sur la recherche Microsoft Teams.

Vous pouvez également utiliser l’application compatible Outlook prête à l’emploi dans la section suivante et ignorer la partie [*Mettre à jour le manifeste de l’application*](#update-the-app-manifest) de ce tutoriel.

### <a name="quickstart"></a>Démarrage rapide

Pour commencer avec un [exemple d’extension de message](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365) déjà activée pour s’exécuter dans Outlook, utilisez l’extension Teams Toolkit pour Visual Studio Code.

1. À partir de Visual Studio Code, ouvrez la palette de commandes (`Ctrl+Shift+P`), tapez `Teams: Create a new Teams app`.
1. Sélectionnez l’option **Créer une application Teams** .
1. Sélectionnez **l’extension de message basée sur la recherche** pour télécharger l’exemple de code d’une extension de message Teams à l’aide du dernier manifeste d’application Teams (version `1.13`).

    :::image type="content" source="images/toolkit-palatte-search-sample.png" alt-text="Tapez « Créer une application Teams » VS Code palette de commandes pour répertorier les exemples d’options Teams":::

    L’exemple est également disponible en tant que *connecteur de recherche NPM* dans la galerie d’exemples du Kit de ressources Teams. Dans le volet Kit de ressources Teams, sélectionnez *Développement* > *Afficher les exemples* > **Connecteur de recherche NPM**.

    :::image type="content" source="images/toolkit-search-sample.png" alt-text="Exemple de connecteur de recherche NPM dans la galerie d’exemples du kit de ressources Teams":::

1. Sélectionnez un emplacement sur votre ordinateur local pour le dossier de l’espace de travail.
1. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et tapez `Teams: Provision in the cloud` pour créer les ressources d’application requises (Azure App Service, plan App Service, Azure Bot et Identité managée) dans votre compte Azure.
1. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et tapez `Teams: Deploy to the cloud` pour déployer l’exemple de code sur les ressources approvisionnées dans Azure et démarrer l’application.

À partir de là, vous pouvez passer directement à [Ajouter un canal Outlook pour que votre bot](#add-an-outlook-channel-for-your-bot) effectue la dernière étape de l’activation de l’extension de message Teams pour fonctionner dans Outlook. (Le manifeste de l’application fait déjà référence à la version correcte, donc aucune mise à jour n’est nécessaire.)

## <a name="update-the-app-manifest"></a>Mettre à jour le manifeste de l’application

Vous devez utiliser la version du schéma du [manifeste du développeur Teams](../resources/schema/manifest-schema.md)`1.13` pour permettre à votre extension de message Teams de s’exécuter dans Outlook.

Vous avez deux options pour mettre à jour le manifeste de votre application :

# <a name="teams-toolkit"></a>[Toolkit Teams](#tab/manifest-teams-toolkit)

1. Ouvrez la palette de commandes : `Ctrl+Shift+P`.
1. Run the `Teams: Upgrade Teams manifest` command and select your app manifest file. Changes will be made in place.

# <a name="manual-steps"></a>[Étapes manuelles](#tab/manifest-manual)

Ouvrez le manifeste de votre application Teams et mettez à jour les `$schema` et `manifestVersion` valeurs suivantes :

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

If you used Teams Toolkit to create your message extension app, you can use it to validate the changes to your manifest file and identify any errors. Open the command palette `Ctrl+Shift+P` and find **Teams: Validate manifest file**.

## <a name="add-an-outlook-channel-for-your-bot"></a>Ajouter un canal Outlook pour votre bot

Dans Microsoft Teams, une extension de message se compose d’un service web que vous hébergez et d’un manifeste d’application, qui définit l’emplacement d’hébergement de votre service web. Le service web tire parti du schéma de messagerie [Bot Framework SDK](/azure/bot-service/bot-service-overview) et du protocole de communication sécurisé via un canal Teams inscrit pour votre bot.

Pour que les utilisateurs interagissent avec votre extension de message à partir d’Outlook, vous devez ajouter un canal Outlook à votre bot :

1. À partir de [Microsoft Portail Azure](https://portal.azure.com) (ou [du portail Bot Framework](https://dev.botframework.com) si vous y êtes inscrit précédemment), accédez à votre ressource de bot.

1. A partir de *Paramètres*, sélectionnez **Canaux**.

1. Sous *Canaux disponibles*, sélectionnez **Outlook**. Sélectionnez l’onglet **Extensions de message**, puis **Appliquer**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Cliquez sur Outlook, sélectionnez l'onglet Extensions de message, puis cliquez sur Enregistrer":::.

1. Vérifiez que votre canal Outlook est répertorié avec Teams dans le volet **Canaux** de votre bot.

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Le volet Azure Bot Channels répertorie les canaux Teams et Outlook":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Mettre à jour l’inscription d’application Microsoft Azure Active Directory (Azure AD) pour l’authentification unique

> [!NOTE]
> Vous pouvez ignorer l’étape si vous utilisez [l’exemple d’application](#quickstart) fourni dans ce tutoriel, car le scénario n’implique pas l’authentification unique Azure Active Directory (AAD).

Azure Active Directory (AD) Single-sign on (SSO) for message extensions works the same way in Outlook [as it does in Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots). However you need to add several client application identifiers to the Azure AD app registration of your bot in your tenant's *App registrations* portal.

1. Connectez-vous à [Portail Azure](https://portal.azure.com) avec votre compte de locataire de bac à sable.
1. Ouvrez **inscriptions d'applications**.
1. Sélectionnez le nom de votre application pour ouvrir son inscription d’application.
1. Sélectionnez **Exposer une API** (sous *Gérer*).
1. Dans la section **applications clientes autorisées** , vérifiez que toutes les valeurs de `Client Id` suivantes sont répertoriées :

   |Application client Microsoft 365 | ID du client |
   |--|--|
   |Bureau et mobile Teams |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
   |Web Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
   |Version de bureau d’Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
   |Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
   |Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>Charger une version test de votre extension de message mise à jour dans Teams

La dernière étape consiste à charger une version test de votre extension de message mise à jour ([package d’application](/microsoftteams/platform/concepts/build-and-test/apps-package)) dans Teams. Une fois l’opération terminée, votre extension de message s’affiche dans votre *Apps* installée à partir de la zone de rédaction du message.

1. Empaquetez votre application Teams ([icônes](/microsoftteams/platform/resources/schema/manifest-schema#icons) de manifeste et d’application) dans un fichier zip. Si vous avez utilisé le Kit de ressources Teams pour créer votre application, vous pouvez facilement le faire à l’aide de l’option **Package de métadonnées Zip Teams** dans le menu *Déploiement* du Kit de ressources Teams.

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Option « Zip Teams metadata package » dans Teams Shared Computer Toolkit extension pour Visual Studio Code":::

1. Connectez-vous à Teams avec votre compte client sandbox et basculez en mode *Aperçu développeur* . Sélectionnez le menu des points de suspension (**...**) près de votre profil utilisateur, puis sélectionnez : **À propos de** > **Aperçu développeur**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Dans le menu des points de suspension Teams, ouvrez « À propos de », puis sélectionnez l’option « Aperçu développeur »":::

1. Sélectionnez **Applications** pour ouvrir le volet **Gérer vos applications**. Sélectionnez Ensuite **Publier une application**.

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="Ouvrez le volet « Gérer vos applications » et sélectionnez « Publier une application »":::

1. Choisissez **Charger une option d’application personnalisée** , sélectionnez votre package d’application et installez-le (*Ajouter*) à votre client Teams.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Option « Charger une application personnalisée » dans Teams":::

Une fois qu’il est chargé par le biais de Teams, votre extension de message est disponible dans outlook.com et Outlook pour Windows Desktop.

## <a name="preview-your-message-extension-in-outlook"></a>Afficher un aperçu de votre extension de message dans Outlook

Voici comment tester votre extension de message en cours d’exécution dans Outlook sur le Bureau Windows et le web.

### <a name="outlook-on-the-web"></a>Outlook sur le web

Pour afficher un aperçu de votre application s’exécutant dans Outlook sur le web :

1. Connectez-vous à [outlook.com](https://www.outlook.com) à l’aide des informations d’identification de votre test client.
1. Sélectionnez **Nouveau message**.
1. Ouvrez **Plus d’applications** menu volant en bas de la fenêtre de composition.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Cliquez sur le menu « Autres applications » en bas de la fenêtre de composition de courrier pour utiliser votre extension de message":::

Your message extension is listed. You can invoke it from there and use it just as you would while composing a message in Teams.

### <a name="outlook"></a>Outlook

Pour afficher un aperçu de votre application en cours d’exécution dans Outlook sur Windows Desktop :

1. Lancez Outlook connecté avec les informations d’identification de votre locataire de test.
1. Sélectionnez **Nouveau message**.
1. Ouvrez le menu volant **Autres applications** dans le ruban supérieur.

    :::image type="content" source="images/outlook-desktop-compose-more-apps.png" alt-text="Cliquez sur « Autres applications » dans le ruban de la fenêtre de composition pour utiliser votre extension de message":::

Votre extension de message est répertoriée, elle ouvre un volet adjacent pour afficher les résultats de la recherche.

## <a name="troubleshooting"></a>Résolution des problèmes

 Bien que votre extension de message mise à jour continuera à fonctionner dans Teams avec une [prise en charge complète des extensions de message](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions), il y a des limitations dans cette première version de l'expérience Outlook à prendre en compte :

* Les extensions de message dans Outlook sont limitées au contexte [*de composition* du courrier](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Même si votre extension de message Teams inclut `commandBox` en tant que *contexte* dans son manifeste, l'aperçu actuel est limité à l'option de composition du courrier (`compose`). L’appel d’une extension de message à partir de la zone *de recherche* Outlook globale n’est pas pris en charge.
* [La commande d’extension de message basée sur des actions](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) n’est pas prise en charge dans Outlook. Si votre application a des commandes basées sur la recherche et l’action, elle apparaîtra dans Outlook, mais le menu d’action ne sera pas disponible.
* L’insertion de plus de cinq [Cartes adaptatives](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) dans un e-mail n’est pas prise en charge ; les cartes adaptatives v1.4 et versions ultérieures ne sont pas prises en charge.
* [Les actions de carte](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) de type `messageBack`, `imBack`, `invoke` et `signin` ne sont pas prises en charge pour les cartes insérées. La prise en charge est limitée à `openURL` : en un clic, l’utilisateur est redirigé vers l’URL spécifiée dans un nouvel onglet.

Utilisez les [canaux de la communauté des développeurs Microsoft Teams](/microsoftteams/platform/feedback) pour signaler les problèmes et fournir des commentaires.

### <a name="debugging"></a>Débogage

Lorsque vous testez votre extension de message, vous pouvez identifier la source (provenant de Teams ou d'Outlook) des requêtes des robots par le [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) de l'objet [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Lorsqu’un utilisateur exécute une requête, votre service reçoit un objet Bot Framework `Activity` standard. L’une des propriétés de l’objet Activity est `channelId`, qui aura la valeur de `msteams` ou `outlook`, en fonction de l’origine de la demande du bot. Pour plus d’informations, consultez  [SDK d’extensions de message basées sur la recherche](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Node.js** |
|---------------|--------------|--------|
| Connecteur de recherche NPM | Utilisez le Kit de ressources Teams pour créer une application d’extension de message. Fonctionne dans Teams, Outlook. |  [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365) |

## <a name="next-step"></a>Étape suivante

Publiez votre application pour qu’elle soit détectable dans Teams, Outlook et Office :

> [!div class="nextstepaction"]
> [Publier des applications Teams pour Outlook et Office](publish.md)
