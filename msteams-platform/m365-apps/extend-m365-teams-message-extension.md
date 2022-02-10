---
title: Étendre une extension Teams messagerie à travers Microsoft 365
description: Voici comment mettre à jour votre extension de messagerie Teams basée sur la recherche pour qu’elle s’exécute dans Outlook
ms.date: 11/15/2021
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: 410f019beeed078ed51c37c241e08511572e18b8
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518106"
---
# <a name="extend-a-teams-messaging-extension-across-microsoft-365"></a>Étendre une extension Teams messagerie à travers Microsoft 365

> [!NOTE]
> *L’extension d Teams extension de* messagerie Microsoft 365 est actuellement disponible uniquement en prévisualisation [pour les développeurs publics](../resources/dev-preview/developer-preview-intro.md). Les fonctionnalités incluses dans l’aperçu peuvent ne pas être terminées et peuvent faire l’objet de modifications avant de devenir disponibles dans la version publique. Elles sont fournies uniquement à des fins de test et d’exploration. Elles ne doivent pas être utilisées dans les applications de production.

Les [extensions de messagerie basées](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) sur la recherche permettent aux utilisateurs de rechercher un système externe et de partager des résultats via la zone de composition de message du client Microsoft Teams client. En étendant vos applications [Teams sur Microsoft 365 (](overview.md)prévisualisation), vous pouvez désormais apporter vos extensions de messagerie Teams basées sur la recherche à Outlook pour les expériences de bureau et web Windows.

Le processus de mise à jour de votre extension de Teams de messagerie basée sur la Outlook nécessite les étapes suivantes :

> [!div class="checklist"]
> * Mettre à jour le manifeste de votre application
> * Ajouter un canal Outlook pour votre bot
> * Chargez une version de version de votre application mise à jour dans Teams

Le reste de ce guide vous guide tout au long de ces étapes et vous montre comment afficher un aperçu de votre extension de messagerie dans les deux Outlook pour Windows bureau et web.

## <a name="prerequisites"></a>Configuration requise

Pour terminer ce didacticiel, vous aurez besoin des instructions ci-après :

 - Un client Microsoft 365 programme pour les développeurs en bac à sable (sandbox)
 - Votre client bac à sable (sandbox) inscrit *à Office 365 releases ciblées*
 - Un environnement de test avec Office applications installées à partir du canal Microsoft 365 Apps *bêta*
 - Microsoft Visual Studio code avec l’extension Teams Shared Computer Toolkit (prévisualisation) (facultatif)

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)

## <a name="prepare-your-messaging-extension-for-the-upgrade"></a>Préparer votre extension de messagerie pour la mise à niveau

Si vous avez une extension de messagerie existante, faites une copie ou une branche de votre projet de production pour tester et mettez à jour votre ID d’application dans le manifeste de l’application pour utiliser un nouvel identificateur (distinct de l’ID d’application de production).

Si vous souhaitez utiliser un exemple de code pour suivre ce didacticiel, suivez les étapes de configuration de l’exemple de recherche [d’extension](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) de messagerie Teams pour créer rapidement une extension de messagerie basée sur la recherche Microsoft Teams. Vous pouvez également commencer avec le même exemple de recherche d’extensions de messagerie Teams mis à jour pour l’aperçu du [SDK TeamsJS v2](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365) et passer à l’aperçu de votre extension de messagerie [dans Outlook](#preview-your-messaging-extension-in-outlook). L’exemple mis à jour est également disponible dans Teams Shared Computer Toolkit extension : *DevelopmentView* >  *samplesNPM* >  **Search Connector**.

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Exemple de connecteur de recherche NPM dans Teams Shared Computer Toolkit":::

## <a name="update-the-app-manifest"></a>Mettre à jour le manifeste de l’application

Vous devez utiliser le schéma de manifeste d’aperçu [Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) `m365DevPreview` développeur et la version du manifeste pour permettre à votre extension de messagerie Teams de s’exécuter dans Outlook.

Vous avez deux options pour mettre à jour votre manifeste d’application :

# <a name="teams-toolkit"></a>[Toolkit Teams](#tab/manifest-teams-toolkit)

1. Ouvrez *la palette de commandes* : `Ctrl+Shift+P`
1. Exécutez la `Teams: Upgrade Teams manifest to support Outlook and Office apps` commande et sélectionnez votre fichier manifeste d’application. Les modifications seront apportées en place.

# <a name="manual-steps"></a>[Étapes manuelles](#tab/manifest-manual)

Ouvrez votre Teams de l’application et mettez à jour les `$schema` `manifestVersion` valeurs suivantes :

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

Si vous avez utilisé Teams Shared Computer Toolkit pour créer votre application d’extension de messagerie, vous pouvez l’utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les erreurs éventuelles. Ouvrez la palette `Ctrl+Shift+P` de commandes et recherchez **Teams :** Valider le fichier manifeste ou sélectionnez l’option dans le menu Déploiement de l’Teams Shared Computer Toolkit (recherchez l’icône Teams sur le côté gauche de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Shared Computer Toolkit’option « Valider le fichier manifeste » sous le menu « Déploiement »":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Ajouter un canal Outlook pour votre bot

Dans Microsoft Teams, une extension de messagerie se compose d’un service web que vous hébergez et d’un manifeste d’application, qui définit l’endroit où votre service web est hébergé. Le service web tire parti du schéma de messagerie du [SDK Bot Framework](/azure/bot-service/bot-service-overview) et du protocole de communication sécurisée via un canal Teams enregistré pour votre bot.

Pour que les utilisateurs interagissent avec votre extension de messagerie à partir Outlook, vous devez ajouter un canal Outlook à votre bot :

1. À [Microsoft Azure portail (ou](https://portal.azure.com) [portail Bot Framework](https://dev.botframework.com) si vous vous y êtes inscrit précédemment), accédez à votre ressource bot.

1. Dans *Paramètres*, sélectionnez **Canaux**.

1. Cliquez sur **Outlook**, sélectionnez **l’onglet Extensions de** message, puis cliquez sur **Enregistrer**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Ajouter un Outlook canal « Extensions de message » pour votre bot à partir du volet Canaux du bot Azure":::

1. Confirmez que votre canal Outlook est répertorié avec Microsoft Teams dans le volet **Canaux** de votre bot :

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Volet Canaux des bots Azure répertoriant les canaux Microsoft Teams et Outlook’équipe":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Mise à Microsoft Azure Active Directory (Azure AD) d’application pour l’sso

> [!NOTE]
> Vous pouvez ignorer l’étape si vous utilisez un exemple de recherche [d’extension](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) de messagerie Teams, car le scénario n’implique pas l’authentification Azure Active Directory (AAD) Sign-On unique.

Azure Active Directory’signature unique (SSO) pour les extensions de messagerie fonctionne de la même manière dans Outlook que dans [Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots), mais vous devez ajouter plusieurs identificateurs d’application client au Microsoft Azure Active Directory (Azure AD ) inscription de votre bot dans le portail d’inscription *des applications de votre* client.

1. Connectez-vous [Microsoft Azure portail avec](https://portal.azure.com) votre compte client en bac à sable.
1. **Ouvrez les inscriptions de l’application**.
1. Sélectionnez le nom de votre application pour ouvrir son inscription.
1. **Sélectionnez Exposer une API** (sous *Gérer*).

Dans la section **Applications clientes autorisées** , assurez-vous que toutes les valeurs `Client Id` suivantes sont répertoriées :

|Microsoft 365 application cliente | ID du client |
|--|--|
|Teams bureau et mobile |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Version de bureau d’Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-0000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-messaging-extension-in-teams"></a>Chargez une version de votre extension de messagerie mise à jour dans Teams

La dernière étape consiste à recharger une version de votre extension de messagerie mise à jour ([package](/microsoftteams/platform/concepts/build-and-test/apps-package) d’application) dans Microsoft Teams. Une fois terminé, votre extension de messagerie s’affiche dans vos applications installées *à partir* de la zone composer un message.

1. Compressez votre application Teams ([icônes de manifeste et d’application](/microsoftteams/platform/resources/schema/manifest-schema#icons)) dans un fichier zip. Si vous avez utilisé Teams Shared Computer Toolkit pour créer votre application, vous pouvez facilement le faire à l’aide de l’option package de métadonnées **Zip Teams** dans *le menu Déploiement* de Teams Shared Computer Toolkit :

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Option « Zip Teams package de métadonnées » dans l’extension Teams Shared Computer Toolkit pour Visual Studio Code":::

1. Connectez-vous à Teams avec votre compte de client bac à sable et vérifiez que vous êtes dans  la prévisualisation publique du développeur en cliquant sur le menu des ellipses (**...**) en fonction de votre profil utilisateur et en ouvrant Sur le point de vérifier que  l’option d’aperçu développeur est surliée.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="À Teams menu des ellipses, ouvrez « À propos de » et vérifiez que l’option « Aperçu développeur » est cochée":::

1. Ouvrez *le* volet Applications, puis cliquez **Télécharger une application** personnalisée, **puis Télécharger pour moi ou mes équipes**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Bouton « Télécharger application personnalisée » dans le volet Teams applications":::

1. Sélectionnez votre package d’application, puis cliquez sur *Ouvrir*.

Une fois le chargement de version Teams, votre extension de messagerie sera disponible dans Outlook sur le web.

## <a name="preview-your-messaging-extension-in-outlook"></a>Afficher un aperçu de votre extension de messagerie dans Outlook

Vous êtes maintenant prêt à tester votre extension de messagerie en cours d’exécution Outlook sur Windows bureau et sur le web. Bien que votre extension de messagerie mise à jour continue de s’exécuter dans Teams avec une prise en charge complète des [fonctionnalités pour les extensions](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) de messagerie, il existe des limitations dans cet aperçu préliminaire de l’expérience Outlook à prendre en compte :

* Les extensions de messagerie Outlook sont limitées au contexte de [*composition de* messagerie](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Même si votre extension `commandBox` Teams messagerie électronique inclut en tant que  contexte dans son manifeste, l’aperçu actuel est limité à l’option de composition de messagerie (`compose`). L’vot d’une extension de messagerie à partir de la zone Outlook *recherche* n’est pas pris en charge.
* [Les commandes d’extension de messagerie basées](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) sur l’action ne sont pas prises en charge dans Outlook. Si votre application dispose de commandes basées sur la recherche et l’action, elle s’Outlook mais le menu d’action n’est pas disponible.
* L’insertion de plus de cinq [cartes adaptatives](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) dans un e-mail n’est pas prise en charge . Les cartes adaptatives v1.4 et ultérieures ne sont pas pris en charge.
* [Les actions de](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) carte de type `messageBack`, `imBack`et `invoke`ne `signin` sont pas prises en charge pour les cartes insérées. La prise en charge est limitée `openURL`à : sur clic, l’utilisateur est redirigé vers l’URL spécifiée dans un nouvel onglet.

Lorsque vous testez votre extension de messagerie, vous pouvez identifier la source (provenant de Teams par rapport à Outlook) des demandes de bot par [le channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) de l’objet [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Lorsqu’un utilisateur effectue une requête, votre service reçoit un objet Bot Framework `Activity` standard. L’une des propriétés de l’objet Activity `channelId`est , `msteams` `outlook`qui aura la valeur de ou, en fonction de l’origine de la demande de bot. Pour plus d’informations,  [voir le SDK des extensions de messagerie basées sur la recherche](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

### <a name="outlook"></a>Outlook

Pour afficher un aperçu de l’exécution de votre application Outlook sur Windows bureau, Outlook connecté avec les informations d’identification de votre client de test. Cliquez sur **Nouveau courrier électronique**. Ouvrez **le menu volant Plus** d’applications dans le ruban supérieur. Votre extension de messagerie sera répertoriée. Vous pouvez l’appeler à partir de là et l’utiliser comme vous le feriez lors de la composition d’un message Teams.

### <a name="outlook-on-the-web"></a>Outlook sur le web

Pour afficher un aperçu de votre application en cours d Outlook sur le web, connectez-vous [outlook.com](https://www.outlook.com) à l’aide des informations d’identification de votre client de test. Cliquez sur **Nouveau message**. Ouvrez **le menu volant Plus** d’applications en bas de la fenêtre de composition. Votre extension de messagerie sera répertoriée. Vous pouvez l’appeler à partir de là et l’utiliser comme vous le feriez lors de la composition d’un message Teams.

## <a name="next-steps"></a>Prochaines étapes

Outlook extensions de messagerie Teams activées sont en prévisualisation et ne sont pas pris en charge pour une utilisation en production. Voici comment distribuer votre extension de messagerie Outlook pour afficher un aperçu des audiences à des fins de test.

### <a name="single-tenant-distribution"></a>Distribution d’un seul client

Outlook onglets personnels Office et activés pour l’aperçu peuvent être distribués à une audience en prévisualisation sur un client de test (ou de production) de l’une des trois manières ci-après :

#### <a name="teams-client"></a>Teams client

Dans le menu *Applications*, *sélectionnez Gérer vos applicationsSoumettre* >  **une application dans votre organisation**. Cela nécessite l’approbation de votre administrateur informatique.

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams Admin Center

En tant qu’administrateur Teams, vous pouvez télécharger et préinstaller le package d’application pour le client de votre organisation à partir de https://admin.teams.microsoft.com/. [Consultez Télécharger vos applications personnalisées dans le Centre d Microsoft Teams’administration Windows pour](/MicrosoftTeams/upload-custom-apps) plus d’informations.

#### <a name="microsoft-admin-center"></a>Centre d’administration Microsoft

En tant qu’administrateur général, vous pouvez télécharger et préinstaller le package d’application à partir de https://admin.microsoft.com/. Pour [plus d’informations, voir Tester et déployer Microsoft 365 Apps par](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) des partenaires dans le portail des applications intégrées.

### <a name="multi-tenant-distribution"></a>Distribution multi-locataires

La distribution vers Microsoft AppSource n’est pas encore prise en charge pendant cette prévisualisation préliminaire pour les développeurs Outlook extensions de messagerie Teams activées pour les développeurs.
