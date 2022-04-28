---
title: Étendre une extension de message Teams sur Microsoft 365
description: Voici comment mettre à jour votre extension de message Teams basée sur la recherche pour qu’elle s’exécute dans Outlook
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: 3bab70d85d071763ffbbae7cb1dae11534d0e812
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104538"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Étendre une extension de message Teams sur Microsoft 365

> [!NOTE]
> *L’extension d’un message Teams sur Microsoft 365* est actuellement disponible uniquement en [préversion publique pour les développeurs](../resources/dev-preview/developer-preview-intro.md). Les fonctionnalités incluses dans l’aperçu peuvent ne pas être terminées et peuvent faire l’objet de modifications avant de devenir disponibles dans la version publique. Elles sont fournies uniquement à des fins de test et d’exploration. Elles ne doivent pas être utilisées dans les applications de production.

Les [extensions de message basées sur la](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) recherche permettent aux utilisateurs de rechercher dans un système externe et de partager des résultats via la zone de composition du client Microsoft Teams. En [étendant vos applications Teams sur Microsoft 365 (préversion),](overview.md) vous pouvez désormais apporter vos extensions de message Teams basées sur la recherche à Outlook pour Windows expériences de bureau et web.

Le processus de mise à jour de votre extension de message de Teams basée sur la recherche pour exécuter Outlook implique les étapes suivantes :

> [!div class="checklist"]
>
> * Mettre à jour le manifeste de votre application
> * Ajouter un canal Outlook pour votre bot
> * Charger une version test de votre application mise à jour dans Teams

Le reste de ce guide vous guide tout au long de ces étapes et vous montre comment afficher un aperçu de votre extension de message dans Outlook pour Windows bureau et web.

## <a name="prerequisites"></a>Conditions préalables

Pour suivre ce didacticiel, vous avez besoin des éléments suivants :

* Un locataire de bac à sable Microsoft 365 Developer Program
* Votre locataire de bac à sable inscrit dans *Office 365 versions ciblées*
* Un environnement de test avec des applications Office installées à partir du *canal bêta* Microsoft 365 Apps
* code Microsoft Visual Studio avec l’extension Teams Shared Computer Toolkit (préversion) (facultatif)

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>Préparer votre extension de message pour la mise à niveau

Si vous disposez d’une extension de message existante, effectuez une copie ou une branche de votre projet de production pour tester et mettre à jour votre ID d’application dans le manifeste de l’application afin d’utiliser un nouvel identificateur (distinct de l’ID d’application de production).

Si vous souhaitez utiliser un exemple de code pour suivre ce didacticiel, suivez les étapes de configuration décrites dans [Teams’exemple de recherche d’extension de message](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) pour créer rapidement une extension de message basée sur la recherche Microsoft Teams. Vous pouvez également commencer avec le même [exemple de recherche d’extensions de message Teams mis à jour pour le Kit de développement logiciel (SDK) TeamsJS v2 (préversion](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365)) et passer à [l’aperçu de votre extension de message dans Outlook](#preview-your-message-extension-in-outlook). L’exemple mis à jour est également disponible dans Teams Shared Computer Toolkit extension : *DevelopmentView* >  *samplesNPM* >  **Search Connector**.

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Exemple de connecteur de recherche NPM dans Teams Shared Computer Toolkit":::

## <a name="update-the-app-manifest"></a>Mettre à jour le manifeste de l’application

Vous devez utiliser le schéma de [manifeste d’aperçu Teams développeur](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) et la `m365DevPreview` version du manifeste pour permettre à votre extension de message Teams de s’exécuter dans Outlook.

Vous disposez de deux options pour mettre à jour le manifeste de votre application :

# <a name="teams-toolkit"></a>[Toolkit Teams](#tab/manifest-teams-toolkit)

1. Ouvrez la *palette de commandes* : `Ctrl+Shift+P`
1. Exécutez la `Teams: Upgrade Teams manifest to support Outlook and Office apps` commande et sélectionnez votre fichier manifeste d’application. Des modifications seront apportées.

# <a name="manual-steps"></a>[Étapes manuelles](#tab/manifest-manual)

Ouvrez le manifeste de votre application Teams et mettez à jour les `$schema` `manifestVersion` valeurs suivantes :

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Si vous avez utilisé Teams Shared Computer Toolkit pour créer votre application d’extension de message, vous pouvez l’utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les erreurs éventuelles. Ouvrez la palette `Ctrl+Shift+P` de commandes et recherchez **Teams : Valider le fichier manifeste** ou sélectionnez l’option dans le menu Déploiement du Teams Shared Computer Toolkit (recherchez l’icône Teams sur le côté gauche de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Shared Computer Toolkit’option « Valider le fichier manifeste » sous le menu « Déploiement »":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Ajouter un canal Outlook pour votre bot

Dans Microsoft Teams, une extension de message se compose d’un service web que vous hébergez et d’un manifeste d’application, qui définit l’emplacement où votre service web est hébergé. Le service web tire parti du schéma de messagerie du Kit de développement logiciel [(SDK) Bot Framework](/azure/bot-service/bot-service-overview) et du protocole de communication sécurisé via un canal Teams inscrit pour votre bot.

Pour que les utilisateurs interagissent avec votre extension de message à partir de Outlook, vous devez ajouter un canal Outlook à votre bot :

1. À partir [du portail Microsoft Azure](https://portal.azure.com) (ou [du portail Bot Framework](https://dev.botframework.com) si vous y êtes inscrit précédemment), accédez à votre ressource de bot.

1. Dans *Paramètres*, sélectionnez **Canaux**.

1. Cliquez sur **Outlook**, sélectionnez l’onglet **Extensions de** message, puis cliquez sur **Enregistrer**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Ajouter un Outlook canal « Extensions de message » pour votre bot à partir du volet Canaux de bot Azure":::

1. Vérifiez que votre canal Outlook est répertorié avec Microsoft Teams dans le volet **Canaux** de votre bot :

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Volet Azure Bot Channels répertoriant les canaux Microsoft Teams et Outlook":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Mettre à jour l’inscription d’application Microsoft Azure Active Directory (Azure AD) pour l’authentification unique

> [!NOTE]
> Vous pouvez ignorer l’étape si vous utilisez [Teams’exemple de recherche d’extension de message](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search), car le scénario n’implique pas Azure Active Directory (AAD) l’authentification unique Sign-On.

Azure Active Directory’authentification unique (SSO) pour les extensions de message fonctionne de la même façon dans Outlook [que dans Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots), toutefois, vous devez ajouter plusieurs identificateurs d’application cliente à l’inscription d’application Azure AD de votre bot dans *le inscriptions d'applications de votre locataire* Portail.

1. Connectez-vous à [Portail Azure](https://portal.azure.com) avec votre compte de locataire de bac à sable( sandbox).
1. Ouvrez **inscriptions d'applications**.
1. Sélectionnez le nom de votre application pour ouvrir son inscription d’application.
1. Sélectionnez  **Exposer une API** (sous *Gérer*).

Dans la section **Applications clientes autorisées** , vérifiez que toutes les valeurs suivantes `Client Id` sont répertoriées :

|Application client Microsoft 365 | ID du client |
|--|--|
|Teams bureau et mobile |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Web Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Version de bureau d’Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>Charger une version test de votre extension de message mise à jour dans Teams

La dernière étape consiste à charger une version test de votre extension de message mise à jour ([package d’application](/microsoftteams/platform/concepts/build-and-test/apps-package)) dans Microsoft Teams. Une fois l’opération terminée, votre extension de message s’affiche dans vos *applications* installées à partir de la zone de composition du message.

1. Empaquetez votre application Teams ([icônes](/microsoftteams/platform/resources/schema/manifest-schema#icons) de manifeste et d’application) dans un fichier zip. Si vous avez utilisé Teams Shared Computer Toolkit pour créer votre application, vous pouvez facilement le faire à l’aide de l’option **de package de métadonnées Zip Teams** dans le menu *Déploiement* de Teams Shared Computer Toolkit :

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Option « Zip Teams metadata package » dans Teams Shared Computer Toolkit extension pour Visual Studio Code":::

1. Connectez-vous à Teams avec votre compte de locataire de bac à sable et vérifiez que vous êtes dans la *préversion du développeur public* en cliquant sur le menu des points de suspension (**...**) par votre profil utilisateur et en ouvrant **About** pour vérifier que l’option *d’aperçu développeur* est activée.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Dans Teams menu points de suspension, ouvrez « À propos » et vérifiez que l’option « Developer Preview » est cochée":::

1. Ouvrez le volet *Applications*, cliquez Télécharger **une application personnalisée**, puis **Télécharger pour moi ou mes équipes**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Bouton « Télécharger une application personnalisée » dans le volet Teams « Applications »":::

1. Sélectionnez votre package d’application, puis cliquez sur *Ouvrir*.

Une fois chargée de manière indépendante via Teams, votre extension de message est disponible dans Outlook sur le web.

## <a name="preview-your-message-extension-in-outlook"></a>Afficher un aperçu de votre extension de message dans Outlook

Vous êtes maintenant prêt à tester votre extension de message en cours d’exécution dans Outlook sur Windows bureau et sur le web. Bien que votre extension de message mise à jour continue à s’exécuter dans Teams avec une [prise en charge complète des fonctionnalités pour les extensions de message](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions), il existe des limitations dans cette préversion précoce de l’expérience Outlook à connaître :

* Les extensions de message dans Outlook sont limitées au contexte de [*composition*](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions) de courrier. Même si votre extension de message Teams inclut `commandBox` comme *contexte* dans son manifeste, la préversion actuelle est limitée à l’option de composition de courrier (`compose`). L’appel d’une extension de message à partir de la zone de *recherche* Outlook globale n’est pas pris en charge.
* [Les commandes d’extension de message basées sur](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) des actions ne sont pas prises en charge dans Outlook. Si votre application a des commandes basées sur la recherche et l’action, elle apparaîtra dans Outlook, mais le menu d’action ne sera pas disponible.
* L’insertion de plus de cinq [cartes adaptatives](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) dans un e-mail n’est pas prise en charge ; Les cartes adaptatives v1.4 et ultérieures ne sont pas prises en charge.
* [Les actions](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) de carte de type `messageBack`, `imBack`, `invoke`et `signin` ne sont pas prises en charge pour les cartes insérées. La prise en charge est limitée à `openURL`: en cliquant, l’utilisateur est redirigé vers l’URL spécifiée dans un nouvel onglet.

Lorsque vous testez votre extension de message, vous pouvez identifier la source (provenant de Teams par rapport à Outlook) des demandes de bot par le [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) de [l’objet Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Lorsqu’un utilisateur exécute une requête, votre service reçoit un objet Bot Framework `Activity` standard. L’une des propriétés de l’objet Activity est `channelId`, qui aura la valeur ou `msteams` `outlook`, selon l’origine de la demande de bot. Pour plus d’informations, consultez le Kit de développement logiciel (  [SDK) des extensions de message basées sur la recherche](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

### <a name="outlook-on-the-web"></a>Outlook sur le web

Pour afficher un aperçu de l’exécution de votre application dans Outlook sur le web :

1. Connectez-vous à [outlook.com](https://www.outlook.com) à l’aide des informations d’identification de votre locataire de test.
1. Sélectionnez **Nouveau message**.
1. Ouvrez le menu volant **Autres applications** en bas de la fenêtre de composition.

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Cliquez sur le menu « Autres applications » en bas de la fenêtre de composition du courrier pour utiliser votre extension de message":::

Votre extension de message est répertoriée. Vous pouvez l’appeler à partir de là et l’utiliser comme vous le feriez lors de la rédaction d’un message dans Teams.

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> Reportez-vous aux dernières mises à jour sur [Microsoft Teams - blog Microsoft 365 développeur](https://devblogs.microsoft.com/microsoft365dev/) pour vérifier si Outlook sur Windows prise en charge de bureau pour Teams applications personnelles est disponible pour votre locataire de test.

Pour afficher un aperçu de l’exécution de votre application dans Outlook sur Windows bureau :

1. Lancez Outlook connecté avec les informations d’identification de votre locataire de test. 1. Cliquez sur **Nouveau courrier électronique**.
1. Ouvrez le menu volant **Plus d’applications** dans le ruban supérieur.

Votre extension de message est répertoriée. Vous pouvez l’appeler à partir de là et l’utiliser comme vous le feriez lors de la rédaction d’un message dans Teams.

## <a name="next-steps"></a>Étapes suivantes

Outlook extensions de message Teams activées sont en préversion et ne sont pas prises en charge pour une utilisation en production. Voici comment distribuer votre extension de message Outlook à des audiences d’aperçu à des fins de test.

### <a name="single-tenant-distribution"></a>Distribution à locataire unique

Outlook et les onglets personnels compatibles avec Office peuvent être distribués à un public en préversion sur un locataire de test (ou de production) de l’une des trois manières suivantes :

#### <a name="teams-client"></a>Client Teams

Dans le menu *Applications*, sélectionnez *Gérer vos applicationsSubmit* >  **une application à votre organisation**. Cela nécessite l’approbation de votre administrateur informatique.

#### <a name="microsoft-teams-admin-center"></a>centre d’administration Microsoft Teams

En tant qu’administrateur Teams, vous pouvez charger et préinstaller le package d’application pour le locataire de votre organisation à partir de [Teams administrateur](https://admin.teams.microsoft.com/). Pour plus d’informations, consultez [Télécharger vos applications personnalisées dans le centre](/MicrosoftTeams/upload-custom-apps) d’administration Microsoft Teams.

#### <a name="microsoft-admin-center"></a>Centre d’administration Microsoft

En tant qu’administrateur général, vous pouvez charger et préinstaller le package d’application à partir de [l’administrateur Microsoft](https://admin.microsoft.com/). Pour plus d’informations, consultez [Tester et déployer Microsoft 365 Apps par des partenaires dans le portail des applications intégrées](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

### <a name="multitenant-distribution"></a>Distribution mutualisée

La distribution vers Microsoft AppSource n’est pas encore prise en charge lors de cette préversion précoce des extensions de message Teams Outlook pour les développeurs.
