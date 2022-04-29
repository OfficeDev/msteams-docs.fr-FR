---
title: Étendre une application onglet personnel Teams sur Microsoft 365
description: Étendre une application onglet personnel Teams sur Microsoft 365
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: high
ms.openlocfilehash: 873a6fa6207d122581e18cef0ae922ffca87762f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111520"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Étendre un onglet personnel Teams sur Microsoft 365

> [!NOTE]
> *L’extension d’un onglet personnel Teams sur Microsoft 365* est actuellement disponible uniquement en [préversion publique pour les développeurs](../resources/dev-preview/developer-preview-intro.md). Les fonctionnalités incluses dans l’aperçu peuvent ne pas être terminées et peuvent faire l’objet de modifications avant de devenir disponibles dans la version publique. Elles sont fournies uniquement à des fins de test et d’exploration. Elles ne doivent pas être utilisées dans les applications de production.

Les onglets personnels offrent un excellent moyen d’améliorer l’expérience Microsoft Teams. À l’aide d’onglets personnels, vous pouvez fournir à un utilisateur l’accès à son application directement dans Teams, sans que l’utilisateur ait à quitter l’expérience ou à se reconnecter. Avec cette préversion, les onglets personnels peuvent s’allumer dans d’autres applications Microsoft 365. Ce didacticiel illustre le processus de prise d’un onglet personnel Teams existant et de mise à jour pour qu’il s’exécute à la fois dans les expériences de bureau et web Outlook, ainsi que Office sur le Web (office.com).

La mise à jour de votre application personnelle pour qu’elle s’exécute dans Outlook et Office Accueil implique les étapes suivantes :

> [!div class="checklist"]
>
> * Mettre à jour le manifeste de l’application
> * Mettre à jour les références de votre Kit de développement logiciel (SDK) TeamsJS
> * Modifier vos en-têtes de stratégie de sécurité du contenu
> * Mettre à jour l’inscription de votre application Microsoft Azure Active Directory (Azure AD) pour l’authentification unique (SSO)

Le test de votre application nécessite les étapes suivantes :

> [!div class="checklist"]
>
> * Inscrire votre locataire Microsoft 365 dans *Office 365 versions ciblées*
> * Configurer votre compte pour accéder aux versions préliminaires des applications Outlook et Office
> * Charger une version test de votre application mise à jour dans Teams

Après ces étapes, votre application doit apparaître dans les versions préliminaires des applications Outlook et Office.

## <a name="prerequisites"></a>Configuration requise

Pour suivre ce didacticiel, vous avez besoin des éléments suivants :

* Un locataire de bac à sable du programme Microsoft 365 Developer
* Votre locataire de bac à sable inscrit dans *Office 365 versions ciblées*
* Un ordinateur avec des applications Office installées à partir du *canal bêta* Microsoft 365 Apps
* (Facultatif) [Teams Shared Computer Toolkit](https://aka.ms/teams-toolkit) extension pour Microsoft Visual Studio Code afin de vous aider à mettre à jour votre code

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Préparer votre onglet personnel pour la mise à niveau

Si vous disposez d’une application onglet personnel existante, effectuez une copie ou une branche de votre projet de production pour tester et mettre à jour votre ID d’application dans le manifeste de l’application pour utiliser un nouvel identificateur (distinct de l’ID d’application de production).

Si vous souhaitez utiliser un exemple de code pour suivre ce didacticiel, suivez les étapes de configuration décrites dans [Prise en main avec l’exemple de liste Todo](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) pour créer une application onglet personnel à l’aide de l’extension Teams Shared Computer Toolkit pour Visual Studio Code. Vous pouvez également commencer avec le même [exemple de liste Todo mis à jour pour le Kit de développement logiciel (SDK) TeamsJS v2 (préversion](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365)) et passer à [l’aperçu de votre onglet personnel dans d’autres expériences Microsoft 365](#preview-your-personal-tab-in-other-microsoft-365-experiences). L’exemple mis à jour est également disponible dans Teams Shared Computer Toolkit extension : *DevelopmentView* >  *samplesTodo* >  **List (Fonctionne dans Teams, Outlook et Office).**

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="Exemple de liste Todo (fonctionne dans Teams, Outlook et Office) dans Teams Shared Computer Toolkit":::

## <a name="update-the-app-manifest"></a>Mettre à jour le manifeste de l’application

Vous devez utiliser le schéma de [manifeste d’aperçu du développeur Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) et la `Microsoft 365 DevPreview` version du manifeste pour permettre à votre onglet personnel Teams de s’exécuter dans Office et Outlook.

Vous pouvez utiliser Teams Shared Computer Toolkit pour mettre à jour le manifeste de votre application ou appliquer les modifications manuellement :

# <a name="teams-toolkit"></a>[Toolkit Teams](#tab/manifest-teams-toolkit)

1. Ouvrez la *palette de commandes* : `Ctrl+Shift+P`
1. Exécutez la `Teams: Upgrade Teams manifest to support Outlook and Office apps` commande et sélectionnez votre fichier manifeste d’application. Des modifications seront apportées.

# <a name="manual-steps"></a>[Étapes manuelles](#tab/manifest-manual)

Ouvrez le manifeste de votre application Teams et mettez à jour les `$schema` et `manifestVersion` valeurs suivantes :

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Si vous avez utilisé Teams Toolkit pour créer votre application personnelle, vous pouvez également l'utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les éventuelles erreurs. Ouvrez la palette `Ctrl+Shift+P` de commandes et recherchez **Teams : Valider le fichier manifeste** ou sélectionnez l’option dans le menu Déploiement du Teams Shared Computer Toolkit (recherchez l’icône Teams sur le côté gauche de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Shared Computer Toolkit’option « Valider le fichier manifeste » sous le menu « Déploiement »":::

## <a name="update-sdk-references"></a>Mettre à jour les références du Kit de développement logiciel (SDK)

Pour s’exécuter dans Outlook et Office, votre application doit dépendre du package `@microsoft/teams-js@2.0.0-beta.1` npm (ou d’une version *bêta* ultérieure). Bien que le code avec des `@microsoft/teams-js` versions de niveau inférieur soit pris en charge dans Outlook et Office, les avertissements de dépréciation sont enregistrés et la prise en charge des `@microsoft/teams-js` versions de niveau inférieur dans Outlook et Office finiront par cesser.

Vous pouvez utiliser Teams Shared Computer Toolkit pour automatiser certaines modifications de code afin d’adopter la version suivante, mais si vous souhaitez effectuer les étapes manuellement, consultez Microsoft Teams version préliminaire du Kit de développement logiciel ([SDK) client JavaScript](using-teams-client-sdk-preview.md) pour plus d’informations`@microsoft/teams-js`.

1. Ouvrez la *palette de commandes* : `Ctrl+Shift+P`
1. Exécutez la commande `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`.

Une fois l’opération terminée, l’utilitaire aura mis à jour votre `package.json` fichier avec la dépendance du Kit de développement logiciel (SDK) TeamsJS (`@microsoft/teams-js@2.0.0-beta.1`ou version ultérieure), et vos fichiers et `*.js/.ts` vous-même `*.jsx/.tsx` seront mis à jour avec :

> [!div class="checklist"]
>
> * `package.json` références à la préversion du Kit de développement logiciel (SDK) TeamsJS
> * Importer des instructions pour la préversion du Kit de développement logiciel (SDK) TeamsJS
> * [Appels de fonction, d’énumération et d’interface](using-teams-client-sdk-preview.md#apis-organized-into-capabilities) vers la préversion du Kit de développement logiciel (SDK) TeamsJS
> * `TODO`rappels de commentaires pour passer en revue les zones susceptibles d’être affectées par les modifications apportées à l’interface [de contexte](using-teams-client-sdk-preview.md#updates-to-the-context-interface)
> * `TODO` rappels de commentaire pour garantir que la [conversion en fonctions promises à partir de fonctions de style de rappel](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) s’est bien passée à chaque site d’appel que l’outil a trouvé.

> [!IMPORTANT]
> Le code contenu dans *.html* fichiers n’est pas pris en charge par les outils de mise à niveau et nécessite des modifications manuelles.

> [!NOTE]
> Si vous souhaitez mettre à jour manuellement votre code, consultez Microsoft Teams version préliminaire du Kit de développement logiciel ([SDK) client JavaScript](using-teams-client-sdk-preview.md) pour en savoir plus sur les modifications requises.

## <a name="configure-content-security-policy-headers"></a>Configurer les en-têtes de stratégie de sécurité du contenu

[Comme dans Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs), les applications d’onglet sont hébergées dans des Office et des clients web Outlook ([éléments iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)).

Si votre application utilise des en-têtes de stratégie de [sécurité de contenu](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP), vérifiez que vous autorisez tous les [ancêtres frame-ancestors suivants dans vos en-têtes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) CSP :

|Hôte Microsoft 365| autorisation frame-ancestor|
|--|--|
| Équipes | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Mettre à jour l’inscription d’application Azure AD pour l’authentification unique

Azure Active Directory Single-sign on (SSO) pour les onglets personnels fonctionne de la même manière dans Office et Outlook [que dans Teams](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso), toutefois, vous devez ajouter plusieurs identificateurs d’application client à l’inscription d’application Azure AD de votre application onglet dans celle de *votre locataire. portail inscriptions d'applications*.

1. Connectez-vous au [portail Microsoft Azure](https://portal.azure.com) avec votre compte de locataire de bac à sable( sandbox).
1. Ouvrez le **panneau inscriptions d'applications**.
1. Sélectionnez le nom de votre application d’onglet personnel pour ouvrir son inscription d’application.
1. Sélectionnez **Exposer une API** (sous *Gérer*).

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="Autoriser les ID clients à partir du panneau *inscriptions d'applications* sur Portail Azure":::

Dans la section **Applications clientes autorisées** , vérifiez que toutes les valeurs suivantes `Client Id` sont ajoutées :

|Application client Microsoft 365 | ID du client |
|--|--|
|Teams bureau, mobile |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Web Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
|Version de bureau d’Office  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
|Version de bureau d’Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>Charger une version test de votre application dans Teams

La dernière étape consiste à charger de manière indépendante votre onglet personnel mis à jour ([package d’application](/microsoftteams/platform/concepts/build-and-test/apps-package)) dans Microsoft Teams. Une fois terminée, votre application sera disponible pour s’exécuter dans Office et Outlook, en plus de Teams.

1. Empaquetez votre application Teams ([icônes](/microsoftteams/platform/resources/schema/manifest-schema#icons) de manifeste et d’application) dans un fichier zip. Si vous avez utilisé Teams Shared Computer Toolkit pour créer votre application, vous pouvez facilement le faire à l’aide de l’option de **package de métadonnées Zip Teams** dans le menu *Déploiement* de Teams Shared Computer Toolkit ou dans la palette `Ctrl+Shift+P` de commandes de Visual Studio Code :

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Option « Zip Teams metadata package » dans Teams Shared Computer Toolkit extension pour Visual Studio Code":::

1. Connectez-vous à Teams avec votre compte de locataire de bac à sable et vérifiez que vous êtes sur la préversion publique du développeur. Vous pouvez vérifier que vous êtes sur la préversion dans le client Teams en cliquant sur le menu des points de suspension (**...**) par votre profil utilisateur et en ouvrant **About** pour vérifier que l’option *d’aperçu développeur* est activée.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Dans Teams menu points de suspension, ouvrez « À propos » et vérifiez que l’option « Developer Preview » est cochée":::

1. Ouvrez le volet *Applications*, cliquez Télécharger **une application personnalisée**, puis **Télécharger pour moi ou mes équipes**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Bouton « Télécharger une application personnalisée » dans le volet Teams « Applications »":::

1. Sélectionnez votre package d’application, puis cliquez sur *Ouvrir*.

Une fois chargé de manière indépendante via Teams, votre onglet personnel est disponible dans Outlook et Office. Veillez à vous connecter avec les mêmes informations d’identification que vous avez utilisées pour charger une version test de votre application dans Teams.

Vous pouvez épingler l’application pour un accès rapide, ou vous pouvez trouver votre application dans le menu volant des points de suspension (**...**) parmi les applications récentes dans la barre latérale sur la gauche.

> [!NOTE]
> L’épinglage d’une application dans Teams ne l’épinglera pas en tant qu’application dans Office.com ou Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Afficher un aperçu de votre onglet personnel dans d’autres expériences Microsoft 365

Lorsque vous mettez à niveau votre onglet personnel Teams et le chargez de manière indépendante dans Teams, il s’exécute dans Outlook sur Windows, sur le web, Office sur Windows et sur le web (office.com). Voici comment la prévisualiser à partir de ces expériences Microsoft 365.

### <a name="outlook-on-windows"></a>Outlook sur Windows

Pour afficher votre application en cours d’exécution dans Outlook sur Windows bureau :

1. Lancez Outlook et connectez-vous à l’aide de votre compte de locataire de développement.
1. Cliquez sur les points de suspension (**...**) dans la barre latérale. Le titre de votre application chargée en version test apparaîtra parmi vos applications installées.
1. Cliquez sur l’icône de votre application pour lancer votre application dans Outlook.

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Cliquez sur l’option points de suspension (« Autres applications ») dans la barre latérale de Outlook client de bureau pour afficher vos onglets personnels installés":::

### <a name="outlook-on-the-web"></a>Outlook sur le web

Pour afficher votre application dans Outlook sur le web :

1. Accédez à [Outlook sur le web](https://outlook.office.com) et connectez-vous à l’aide de votre compte de locataire de développement.
1. Cliquez sur les points de suspension (**...**) dans la barre latérale. Le titre de votre application chargée en version test apparaîtra parmi vos applications installées.
1. Cliquez sur l’icône de votre application pour lancer et afficher un aperçu de votre application en cours d’exécution dans Outlook sur le web.

:::image type="content" source="images/outlook-web-more-apps.png" alt-text="Cliquez sur l’option points de suspension (« Autres applications ») dans la barre latérale de outlook.com pour afficher vos onglets personnels installés":::.

### <a name="office-on-windows"></a>Office pour Windows

Pour afficher votre application en cours d’exécution dans Office sur Windows bureau :

1. Lancez Office et connectez-vous à l’aide de votre compte de locataire de développement.
1. Cliquez sur les points de suspension (**...**) dans la barre latérale. Le titre de votre application chargée en version test apparaîtra parmi vos applications installées.
1. Cliquez sur l’icône de votre application pour lancer votre application dans Office.

:::image type="content" source="images/office-desktop-more-apps.png" alt-text="Cliquez sur l’option points de suspension (« Autres applications ») dans la barre latérale de Office client de bureau pour afficher vos onglets personnels installés":::.

### <a name="office-on-the-web"></a>Office sur le web

Pour afficher un aperçu de l’exécution de votre application dans Office sur le Web :

1. Connectez-vous office.com avec les informations d’identification du locataire de test.
1. Cliquez sur les points de suspension (**...**) dans la barre latérale. Le titre de votre application chargée en version test apparaîtra parmi vos applications installées.
1. Cliquez sur l’icône de votre application pour lancer votre application dans Office sur le Web.

:::image type="content" source="images/office-web-more-apps.png" alt-text="Cliquez sur l’option points de suspension (« Autres applications ») dans la barre latérale de office.com pour afficher vos onglets personnels installés":::.

## <a name="next-steps"></a>Étapes suivantes

Outlook et les onglets personnels compatibles avec Office sont en préversion et ne sont pas pris en charge pour une utilisation en production. Voici comment distribuer votre application d’onglet personnel aux audiences en préversion à des fins de test.

### <a name="single-tenant-distribution"></a>Distribution à locataire unique

Outlook et les onglets personnels compatibles avec Office peuvent être distribués à un public en préversion sur un locataire de test (ou de production) de l’une des trois manières suivantes :

#### <a name="teams-client"></a>Client Teams

Dans le menu *Applications*, sélectionnez *Gérer vos applications* >  **Soumettre une application à votre organisation**. Cela nécessite l’approbation de votre administrateur informatique.

#### <a name="microsoft-teams-admin-center"></a>Centre d’administration Microsoft Teams

En tant qu’administrateur Teams, vous pouvez charger et préinstaller le package d’application pour le locataire de votre organisation à partir de [Teams administrateur](https://admin.teams.microsoft.com/). Pour plus d’informations, consultez [Télécharger vos applications personnalisées dans le centre](/MicrosoftTeams/upload-custom-apps) d’administration Microsoft Teams.

#### <a name="microsoft-admin-center"></a>Centre d’administration Microsoft Corporation

En tant qu’administrateur général, vous pouvez charger et préinstaller le package d’application à partir de [l’administrateur Microsoft](https://admin.microsoft.com/). Pour plus d’informations, consultez [Tester et déployer Microsoft 365 Apps par des partenaires dans le portail des applications intégrées](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

### <a name="multitenant-distribution"></a>Distribution multilocataires

La distribution vers Microsoft AppSource n’est pas prise en charge lors de cette préversion précoce pour les développeurs des onglets personnels Outlook et Office activés Teams.
