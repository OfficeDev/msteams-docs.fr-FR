---
title: Étendre une application onglet personnel Teams sur Microsoft 365
description: Étendre une application onglet personnel Teams sur Microsoft 365
ms.date: 05/24/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: b164231a95c511402431b5d4cdb3c7d0fc6cfdff
ms.sourcegitcommit: 1e77573e47fad51a19545949fdac1241b13052e2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656172"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Étendre un onglet personnel Teams sur Microsoft 365

Les onglets personnels offrent un excellent moyen d’améliorer l’expérience Microsoft Teams. À l’aide d’onglets personnels, vous pouvez fournir à un utilisateur l’accès à son application directement dans Teams, sans que l’utilisateur ait à quitter l’expérience ou à se reconnecter. Avec cette préversion, les onglets personnels peuvent s’allumer dans d’autres applications Microsoft 365. Ce didacticiel illustre le processus de prise d’un onglet personnel Teams existant et de mise à jour pour qu’il s’exécute à la fois dans les expériences de bureau et web Outlook, ainsi que Office sur le Web (office.com).

La mise à jour de votre application personnelle pour qu’elle s’exécute dans Outlook et Office implique les étapes suivantes :

> [!div class="checklist"]
>
> * Mettre à jour le manifeste de l’application
> * Mettre à jour les références de votre Kit de développement logiciel (SDK) TeamsJS
> * Modifier vos en-têtes de stratégie de sécurité du contenu
> * Mettre à jour l’inscription de votre application Microsoft Azure Active Directory (Azure AD) pour l’authentification unique (SSO)
> * Charger une version test de votre application mise à jour dans Teams

Le reste de ce guide vous guide tout au long de ces étapes et vous montre comment afficher un aperçu de votre onglet personnel dans d’autres applications Microsoft 365.

## <a name="prerequisites"></a>Configuration requise

Pour suivre ce didacticiel, vous avez besoin des éléments suivants :

* Un locataire de bac à sable du programme Microsoft 365 Developer
* Votre locataire de bac à sable inscrit dans *Office 365 versions ciblées*
* Un ordinateur avec des applications Office installées à partir du *canal bêta* Microsoft 365 Apps
* (Facultatif) [Teams Shared Computer Toolkit](https://aka.ms/teams-toolkit) extension pour Microsoft Visual Studio Code afin de vous aider à mettre à jour votre code

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Préparer votre onglet personnel pour la mise à niveau

Si vous disposez d’une application onglet personnelle existante, effectuez une copie ou une branche de votre projet de production pour tester et mettre à jour votre ID d’application dans le manifeste de l’application afin d’utiliser un nouvel identificateur (distinct de l’ID d’application de production, à des fins de test).

Si vous souhaitez utiliser un exemple de code pour suivre ce didacticiel, suivez les étapes de configuration de [l’exemple de liste Todo](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) pour créer une application onglet personnel à l’aide de l’extension Teams Toolkit pour Visual Studio Code, puis revenez à cet article pour la mettre à jour pour Microsoft 365.

Vous pouvez également utiliser une application Simple Sign-On *Hello World* de base déjà activée Microsoft 365 dans la section de démarrage rapide suivante, puis passer au chargement indépendant de [votre application dans Teams](#sideload-your-app-in-teams).

### <a name="quickstart"></a>Démarrage rapide

Pour commencer avec un [onglet personnel](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365) déjà activé pour s’exécuter dans Outlook et Office, utilisez Teams extension Toolkit pour Visual Studio Code.

1. À partir de Visual Studio Code, ouvrez la palette de commandes (`Ctrl+Shift+P`), tapez `Teams: Create a new Teams app`.
1. Sélectionnez **l’onglet personnel activé pour l’authentification unique**.

    :::image type="content" source="images/toolkit-tab-sample.png" alt-text="Exemple de liste Todo (fonctionne dans Teams, Outlook et Office) dans Teams Shared Computer Toolkit":::

1. Sélectionnez un emplacement sur votre ordinateur local pour le dossier de l’espace de travail.
1. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et tapez `Teams: Provision in the cloud` pour créer les ressources d’application requises (plan App Service, compte Stockage, Application de fonction, Identité managée) dans votre compte Azure.
1. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et tapez `Teams: Deploy to the cloud` pour déployer l’exemple de code sur les ressources approvisionnées dans Azure et démarrer l’application.

À partir de là, vous pouvez passer directement au [chargement indépendant de votre application dans Teams](#sideload-your-app-in-teams) et afficher un aperçu de votre application dans Outlook et Office. (Le manifeste de l’application et les appels d’API TeamsJS ont déjà été mis à jour pour Microsoft 365.)

## <a name="update-the-app-manifest"></a>Mettre à jour le manifeste de l’application

Vous devez utiliser la version `1.13` Teams schéma de [manifeste du développeur](../resources/schema/manifest-schema.md) pour permettre à votre onglet personnel Teams de s’exécuter dans Outlook et Office.

Vous avez deux options pour mettre à jour le manifeste de votre application :

# <a name="teams-toolkit"></a>[Toolkit Teams](#tab/manifest-teams-toolkit)

1. Ouvrez la palette de commandes : `Ctrl+Shift+P`.
1. Exécutez la `Teams: Upgrade Teams manifest` commande et sélectionnez votre fichier manifeste d’application. Des modifications seront apportées.

# <a name="manual-steps"></a>[Étapes manuelles](#tab/manifest-manual)

Ouvrez le manifeste de votre application Teams et mettez à jour les `$schema` et `manifestVersion` valeurs suivantes :

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

Si vous avez utilisé Teams Toolkit pour créer votre application personnelle, vous pouvez également l'utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les éventuelles erreurs. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et recherchez **Teams : Valider le fichier manifeste**.

## <a name="update-sdk-references"></a>Mettre à jour les références du Kit de développement logiciel (SDK)

Pour s’exécuter dans Outlook et Office, votre application doit référencer le package `@microsoft/teams-js@2.0.0` npm (ou version ultérieure). Bien que le code avec des versions de niveau inférieur soit pris en charge dans Outlook et Office, les avertissements de dépréciation sont enregistrés et la prise en charge des versions de niveau inférieur de TeamsJS dans Outlook et Office finiront par cesser.

Vous pouvez utiliser Teams Toolkit pour identifier et automatiser les modifications de code nécessaires à la mise à niveau de versions 1.x TeamsJS vers TeamsJS version 2.0.0. Vous pouvez également effectuer les mêmes étapes manuellement ; Pour plus d’informations, reportez-vous à [Microsoft Teams Kit de développement logiciel (SDK) client JavaScript](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20).

1. Ouvrez la *palette de commandes* : `Ctrl+Shift+P`.
1. Exécutez la commande `Teams: Upgrade Teams JS SDK and code references`.

Une fois l’opération terminée, votre fichier *package.json* fait référence `@microsoft/teams-js@2.0.0` (ou version ultérieure) et vos `*.js/.ts` fichiers sont `*.jsx/.tsx` mis à jour avec :

> [!div class="checklist"]
> * Importer des instructions pour teams-js@2.0.0
> * [Appels de fonction, d’énumération et d’interface](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) pour teams-js@2.0.0
> * `TODO`rappels de commentaires signalant les zones susceptibles d’être affectées par les modifications apportées à l’interface [de contexte](../tabs/how-to/using-teams-client-sdk.md#updates-to-the-context-interface)
> * `TODO` rappels de commentaire pour [convertir des fonctions de rappel en promesses](../tabs/how-to/using-teams-client-sdk.md#callbacks-converted-to-promises)

> [!IMPORTANT]
> Le code contenu dans *.html* fichiers n’est pas pris en charge par les outils de mise à niveau et nécessite des modifications manuelles.

## <a name="configure-content-security-policy-headers"></a>Configurer les en-têtes de stratégie de sécurité du contenu

Comme dans Microsoft Teams, les applications d’onglet sont hébergées dans des [éléments iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) dans Office et Outlook clients web.

Si votre application utilise des en-têtes de stratégie [de sécurité de contenu](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (fournisseur de solutions Cloud), veillez à autoriser tous les [ancêtres frame-ancestors suivants dans vos en-têtes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) fournisseur de solutions Cloud :

|Hôte Microsoft 365| autorisation frame-ancestor|
|--|--|
| Équipes | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Mettre à jour l’inscription d’application Azure AD pour l’authentification unique

[Azure Active Directory (AD) Authentification unique (SSO)](../tabs/how-to/authentication/auth-aad-sso.md) pour les onglets personnels fonctionne de la même façon dans Office et Outlook que dans Teams. Toutefois, vous devez ajouter plusieurs identificateurs d’application cliente à l’inscription d’application Azure AD de votre application onglet dans le portail *inscriptions d'applications* de votre locataire.

1. Connectez-vous au [portail Microsoft Azure](https://portal.azure.com) avec votre compte de locataire de bac à sable( sandbox).
1. Ouvrez le **panneau inscriptions d'applications**.
1. Sélectionnez le nom de votre application d’onglet personnel pour ouvrir son inscription d’application.
1. Sélectionnez **Exposer une API** (sous *Gérer*).

    :::image type="content" source="images/azure-app-registration-clients.png" alt-text="Autoriser les ID clients à partir du panneau *inscriptions d'applications* sur Portail Azure":::

1. Dans la section **Applications clientes autorisées** , vérifiez que toutes les valeurs suivantes `Client Id` sont ajoutées :

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

La dernière étape de l’exécution de votre application dans Office et Outlook consiste à charger de manière indépendante votre [package d’application](..//concepts/build-and-test/apps-package.md) onglet personnel mis à jour dans Microsoft Teams.

1. Empaquetez votre application Teams (icônes [de manifeste](../resources/schema/manifest-schema.md) et [d’application](/microsoftteams/platform/resources/schema/manifest-schema#icons)) dans un fichier zip. Si vous avez utilisé teams Toolkit pour créer votre application, vous pouvez facilement le faire à l’aide de l’option **package de métadonnées Zip Teams** dans le menu *Deployment* du Kit de ressources Teams :

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Option « Zip Teams metadata package » dans Teams Shared Computer Toolkit extension pour Visual Studio Code":::

1. Connectez-vous à Teams avec votre compte de locataire de bac à sable et basculez en mode *Developer Preview*. Sélectionnez le menu des points de suspension (**...**) en fonction de votre profil utilisateur, puis sélectionnez : À propos de > **aperçu du développeur**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Dans Teams menu points de suspension, ouvrez « À propos » et sélectionnez l’option « Aperçu du développeur ».":::

1. Sélectionnez *Applications* pour ouvrir le volet **Gérer vos applications** . Sélectionnez Ensuite **Publier une application**.

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="Ouvrez le volet « Gérer vos applications », puis sélectionnez « Publier une application »":::

1. Choisissez **Télécharger une option d’application personnalisée**, puis sélectionnez votre package d’application.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Option « Télécharger une application personnalisée » dans Teams":::

Une fois qu’il est chargé à Teams, votre onglet personnel est disponible dans Outlook et Office. Veillez à vous connecter avec les mêmes informations d’identification que vous avez utilisées pour vous connecter à Teams pour charger une version test de votre application.

Vous pouvez épingler l’application pour un accès rapide, ou vous pouvez trouver votre application dans le menu volant des points de suspension (**...**) parmi les applications récentes dans la barre latérale sur la gauche. Épinglage d’une application dans Teams ne l’épinglez pas en tant qu’application dans Office ou Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Afficher un aperçu de votre onglet personnel dans d’autres expériences Microsoft 365

Voici comment afficher un aperçu de votre application s’exécutant dans Office et Outlook, les clients de bureau web et Windows.

> [!NOTE]
> La désinstallation de votre application de Teams la supprime également des catalogues **Plus d’applications** dans Outlook et Office. Si vous utilisez l’exemple d’application Teams Toolkit fourni ci-dessus.

### <a name="outlook-on-windows"></a>Outlook sur Windows

Pour afficher votre application en cours d’exécution dans Outlook sur Windows bureau :

1. Lancez Outlook et connectez-vous à l’aide de votre compte de locataire de développement.
1. Dans la barre latérale, sélectionnez  **Autres applications**. Le titre de votre application chargée en version test apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans Outlook.

    :::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Cliquez sur l’option points de suspension (« Autres applications ») dans la barre latérale de Outlook client de bureau pour afficher vos onglets personnels installés":::

### <a name="outlook-on-the-web"></a>Outlook sur le web

Pour afficher votre application dans Outlook sur le web :

1. Accédez à [Outlook sur le web](https://outlook.office.com) et connectez-vous à l’aide de votre compte de locataire de développement.
1. Sélectionnez les points de suspension (**...**) dans la barre latérale. Le titre de votre application chargée en version test apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer et afficher un aperçu de votre application en cours d’exécution dans Outlook sur le web.

    :::image type="content" source="images/outlook-web-more-apps.png" alt-text="Cliquez sur l’option points de suspension (« Autres applications ») dans la barre latérale de outlook.com pour afficher vos onglets personnels installés":::.

### <a name="office-on-windows"></a>Office pour Windows

Pour afficher votre application en cours d’exécution dans Office sur Windows bureau :

1. Lancez Office et connectez-vous à l’aide de votre compte de locataire de développement.
1. Sélectionnez les points de suspension (**...**) dans la barre latérale. Le titre de votre application chargée en version test apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans Office.

    :::image type="content" source="images/office-desktop-more-apps.png" alt-text="Cliquez sur l’option points de suspension (« Autres applications ») dans la barre latérale de Office client de bureau pour afficher vos onglets personnels installés":::.

### <a name="office-on-the-web"></a>Office sur le web

Pour afficher un aperçu de l’exécution de votre application dans Office sur le Web :

1. **Connectez-vous à office.com** avec les informations d’identification du locataire de test.
1. Sélectionnez l’icône **Applications** dans la barre latérale. Le titre de votre application chargée en version test apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans Office sur le Web.

    :::image type="content" source="images/office-web-more-apps.png" alt-text="Cliquez sur l’option « Autres applications » dans la barre latérale de office.com pour afficher vos onglets personnels installés":::

## <a name="troubleshooting"></a>Résolution des problèmes

Actuellement, un sous-ensemble de types et de fonctionnalités d’application Teams sont pris en charge dans les clients Outlook et Office. Cette prise en charge s’étend au fil du temps.

Reportez-vous à [Microsoft 365 prise en charge](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook) pour vérifier la prise en charge de l’hôte pour différentes fonctionnalités TeamsJS.

Pour obtenir un résumé global de Microsoft 365 prise en charge de l’hôte et de la plateforme pour les applications Teams, consultez [Étendre Teams applications sur Microsoft 365](overview.md).

Vous pouvez vérifier la prise en charge par l’hôte d’une fonctionnalité donnée au moment de l’exécution en appelant la `isSupported()` fonction sur cette fonctionnalité (espace de noms) et en ajustant le comportement de l’application selon les besoins. Cela permet à votre application d’activer l’interface utilisateur et les fonctionnalités des hôtes qui la prennent en charge, et de fournir une expérience de secours appropriée dans les hôtes qui ne le prennent pas en charge. Pour plus d’informations, consultez [Différencier votre expérience d’application](../tabs/how-to/using-teams-client-sdk.md#differentiate-your-app-experience).

Utilisez les [Microsoft Teams canaux de la communauté des développeurs](/microsoftteams/platform/feedback) pour signaler les problèmes et fournir des commentaires.

### <a name="debugging"></a>Débogage

À partir de Teams Toolkit, vous pouvez déboguer (`F5`) votre application onglet s’exécutant dans Office et Outlook, en plus de Teams.

:::image type="content" source="images/toolkit-debug-targets.png" alt-text="Choisissez parmi Teams, Outlook et Office cibles de débogage dans Teams Toolkit":::

Lors de la première exécution du débogage local pour Office ou Outlook, vous êtes invité à vous connecter à votre compte de locataire Microsoft 365 et à installer un certificat de test auto-signé. Vous serez également invité à installer manuellement Teams. Sélectionnez **Installer dans Teams** pour ouvrir une fenêtre de navigateur et installer manuellement votre application. Cliquez ensuite sur **Continuer** pour continuer à déboguer votre application dans Office/Outlook.

:::image type="content" source="images/toolkit-dialog-teams-install.png" alt-text="Boîte de dialogue Boîte à outils Teams installer":::

Fournissez des commentaires et signalez les problèmes liés à l’expérience de débogage Teams Toolkit dans [Microsoft Teams Framework (TeamsFx).](https://github.com/OfficeDev/TeamsFx/issues)

## <a name="next-step"></a>Étape suivante

Publiez votre application pour qu’elle soit détectable dans Teams, Outlook et Office :

> [!div class="nextstepaction"]
> [Publier des applications Teams pour Outlook et Office](publish.md)

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Node.js** |
|---------------|--------------|--------|
| Liste des tâches | Liste de tâches modifiable avec l’authentification unique générée avec React et Azure Functions. Fonctionne uniquement dans Teams (utilisez cet exemple d’application pour essayer le processus de mise à niveau décrit dans ce didacticiel). | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend)  |
| Todo List (Microsoft 365) | Liste de tâches modifiable avec l’authentification unique générée avec React et Azure Functions. Fonctionne dans Teams, Outlook, Office. | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)|
| Éditeur d’images (Microsoft 365) | Créez, modifiez, ouvrez et enregistrez des images à l’aide de Microsoft API Graph. Fonctionne dans Teams, Outlook, Office. | [View](https://github.com/OfficeDev/m365-extensibility-image-editor) |
