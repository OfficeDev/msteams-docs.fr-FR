---
title: Étendre une application onglet personnel Teams sur Microsoft 365
description: Mettez à jour votre application personnelle pour qu’elle s’exécute dans Outlook et Office. Mettez à jour le manifeste et le Kit de développement logiciel (SDK) TeamsJS V2, modifiez la sécurité du consentement, mettez à jour l’inscription d’application Azure AD pour l’authentification unique.
ms.date: 05/24/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: cb6b7ee27e95045c218805181531ad96a1357f89
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100763"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Étendre un onglet personnel Teams sur Microsoft 365

Les onglets personnels offrent un excellent moyen d’améliorer l’expérience Microsoft Teams. À l’aide d’onglets personnels, vous pouvez fournir à un utilisateur l’accès à son application directement dans Teams, sans que l’utilisateur ait à quitter l’expérience ou à se reconnecter. Avec cette préversion, les onglets personnels peuvent s’allumer dans d’autres applications Microsoft 365. Ce didacticiel montre comment prendre un onglet personnel Teams existant et le mettre à jour pour qu’il s’exécute à la fois dans les expériences de bureau et web Outlook et Office, ainsi que dans l’application Office pour Android.

La mise à jour de votre application personnelle pour qu’elle s’exécute dans Outlook et Office implique les étapes suivantes :

> [!div class="checklist"]
>
> * Mettez à jour le manifeste de votre application.
> * Mettez à jour les références de votre Kit de développement logiciel (SDK) TeamsJS.
> * Modifiez vos en-têtes de stratégie de sécurité du contenu.
> * Mettez à jour l’inscription de votre application Microsoft Azure Active Directory (Azure AD) pour l’authentification unique (SSO).
> * Chargez une version test de votre application mise à jour dans Teams.

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

Vous pouvez également utiliser une application *Hello World* de base pour l’authentification unique déjà activée pour Microsoft 365 dans la section de démarrage rapide suivante, puis passer au [chargement indépendant de votre application dans Teams](#sideload-your-app-in-teams) .

### <a name="quickstart"></a>Démarrage rapide

Pour commencer avec un [onglet personnel](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365) déjà activé pour s’exécuter dans Outlook et Office, utilisez l’extension Teams Toolkit pour Visual Studio Code.

1. À partir de Visual Studio Code, ouvrez la palette de commandes (`Ctrl+Shift+P`), tapez `Teams: Create a new Teams app`.
1. Sélectionnez **l’onglet personnel activé pour l’authentification unique**.

    :::image type="content" source="images/toolkit-tab-sample.png" alt-text="Exemple de liste Todo (fonctionne dans Teams, Outlook et Office) dans Teams Shared Computer Toolkit":::

1. Sélectionnez un emplacement sur votre ordinateur local pour le dossier de l’espace de travail.
1. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et tapez `Teams: Provision in the cloud` pour créer les ressources d’application requises (plan App Service, compte de stockage, application de fonction, identité managée) dans votre compte Azure.
1. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et tapez `Teams: Deploy to the cloud` pour déployer l’exemple de code sur les ressources approvisionnées dans Azure et démarrer l’application.

À partir de là, vous pouvez passer directement au chargement indépendant de [votre application dans Teams](#sideload-your-app-in-teams) et afficher un aperçu de votre application dans Outlook et Office. (Le manifeste de l’application et les appels d’API TeamsJS ont déjà été mis à jour pour Microsoft 365.)

## <a name="update-the-app-manifest"></a>Mettre à jour le manifeste de l’application

Vous devez utiliser la version `1.13` du schéma de [manifeste du développeur Teams](../resources/schema/manifest-schema.md) pour permettre à votre onglet personnel Teams de s’exécuter dans Outlook et Office.

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

Si vous avez utilisé Teams Toolkit pour créer votre application personnelle, vous pouvez également l'utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les éventuelles erreurs. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et recherchez **Teams : Valider le fichier manifeste**.

## <a name="update-sdk-references"></a>Mettre à jour les références du Kit de développement logiciel (SDK)

Pour s’exécuter dans Outlook et Office, votre application doit référencer le package `@microsoft/teams-js@2.0.0` npm (ou version ultérieure). Bien que le code avec des versions de niveau inférieur soit pris en charge dans Outlook et Office, les avertissements de dépréciation sont enregistrés et la prise en charge des versions de niveau inférieur de TeamsJS dans Outlook et Office cessera éventuellement.

Vous pouvez utiliser le Kit de ressources Teams pour identifier et automatiser les modifications de code nécessaires à la mise à niveau de versions 1.x TeamsJS vers TeamsJS version 2.0.0. Vous pouvez également effectuer les mêmes étapes manuellement ; Pour plus d’informations, [reportez-vous au Kit de développement logiciel (SDK) client JavaScript de Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) .

1. Ouvrez la *palette de commandes* : `Ctrl+Shift+P`.
1. Exécutez la commande `Teams: Upgrade Teams JS SDK and code references`.

Une fois l’opération terminée, votre fichier *package.json* fait référence `@microsoft/teams-js@2.0.0` (ou version ultérieure) et vos `*.js/.ts` fichiers sont `*.jsx/.tsx` mis à jour avec :

> [!div class="checklist"]
>
> * Importer des instructions pour teams-js@2.0.0
> * [Appels de fonction, d’énumération et d’interface](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) pour teams-js@2.0.0
> * `TODO`rappels de commentaires signalant les zones susceptibles d’être affectées par les modifications apportées à l’interface [de contexte](../tabs/how-to/using-teams-client-sdk.md#updates-to-the-context-interface)
> * `TODO` rappels de commentaire pour [convertir des fonctions de rappel en promesses](../tabs/how-to/using-teams-client-sdk.md#callbacks-converted-to-promises)

> [!IMPORTANT]
> Le code contenu dans *.html* fichiers n’est pas pris en charge par les outils de mise à niveau et nécessite des modifications manuelles.

## <a name="configure-content-security-policy-headers"></a>Configurer les en-têtes de stratégie de sécurité du contenu

Comme dans Microsoft Teams, les applications onglet sont hébergées dans des [éléments iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) dans les clients web Office et Outlook.

Si votre application utilise des en-têtes de stratégie de [sécurité de contenu](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP), veillez à autoriser tous les [ancêtres frame-ancestors suivants dans vos en-têtes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) CSP :

|Hôte Microsoft 365| autorisation frame-ancestor|
|--|--|
| Équipes | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Mettre à jour l’inscription d’application Azure AD pour l’authentification unique

[L’authentification unique (SSO) Azure Active Directory (AD)](../tabs/how-to/authentication/tab-sso-overview.md) pour les onglets personnels fonctionne de la même façon dans Office et Outlook que dans Teams. Toutefois, vous devez ajouter plusieurs identificateurs d’application cliente à l’inscription d’application Azure AD de votre application onglet dans le portail *inscriptions d'applications* de votre locataire.

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
    |Office web  |4765445b-32c6-49b0-83e6-1d93765276ca|
    |Version de bureau d’Office  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
    |Office mobile  | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Bureau Outlook, mobile | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook web | bc59ab01-8403-45c6-8796-ac3ef710b3e3|

    > [!NOTE]
    > Certaines applications clientes Microsoft 365 partagent des ID clients.

## <a name="sideload-your-app-in-teams"></a>Charger une version test de votre application dans Teams

La dernière étape de l’exécution de votre application dans Office et Outlook consiste à charger de manière indépendante votre [package d’application](..//concepts/build-and-test/apps-package.md) onglet personnel mis à jour dans Microsoft Teams.

1. Empaquetez votre application Teams (icônes [de manifeste](../resources/schema/manifest-schema.md) et [d’application](/microsoftteams/platform/resources/schema/manifest-schema#icons)) dans un fichier zip. Si vous avez utilisé le Kit de ressources Teams pour créer votre application, vous pouvez facilement le faire à l’aide de l’option **Package de métadonnées Zip Teams** dans le menu **Déploiement** du Kit de ressources Teams.

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Option « Zip Teams metadata package » dans Teams Shared Computer Toolkit extension pour Visual Studio Code":::

1. Connectez-vous à Teams avec votre compte client sandbox et basculez en mode *Aperçu développeur* . Sélectionnez le menu des points de suspension (**...**) près de votre profil utilisateur, puis sélectionnez : **À propos de** > **Aperçu développeur**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Dans le menu des points de suspension Teams, ouvrez « À propos de », puis sélectionnez l’option « Aperçu développeur »":::

1. Sélectionnez **Applications** pour ouvrir le volet **Gérer vos applications**. Sélectionnez Ensuite **Publier une application**.

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="Ouvrez le volet « Gérer vos applications » et sélectionnez « Publier une application »":::

1. Choisissez **Charger une option d’application personnalisée** , puis sélectionnez votre package d’application.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Option « Charger une application personnalisée » dans Teams":::

Une fois qu’il est chargé de manière indépendante dans Teams, votre onglet personnel est disponible dans Outlook et Office. Vous devez vous connecter avec les mêmes informations d’identification que celles que vous avez utilisées pour charger de manière indépendante votre application dans Teams. Lorsque vous exécutez l’application Office pour Android, vous devez redémarrer l’application pour utiliser votre application onglet personnel à partir de l’application Office.

Vous pouvez épingler l’application pour un accès rapide, ou vous pouvez trouver votre application dans le menu volant des points de suspension (**...**) parmi les applications récentes dans la barre latérale sur la gauche. L’épinglage d’une application dans Teams ne l’épingle pas en tant qu’application dans Office ou Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Afficher un aperçu de votre onglet personnel dans d’autres expériences Microsoft 365

Voici comment afficher un aperçu de votre application s’exécutant dans les clients De bureau Office et Outlook, web et Windows.

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
1. Dans la barre latérale, sélectionnez  **Autres applications**. Le titre de votre application chargée en version test apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer et afficher un aperçu de votre application en cours d’exécution dans Outlook sur le web.

    :::image type="content" source="images/outlook-web-more-apps.png" alt-text="Cliquez sur l’option points de suspension (« Autres applications ») dans la barre latérale de outlook.com pour afficher vos onglets personnels installés":::.

### <a name="office-on-windows"></a>Office pour Windows

Pour afficher votre application en cours d’exécution dans Office sur Windows bureau :

1. Lancez Office et connectez-vous à l’aide de votre compte de locataire de développement.
1. Sélectionnez l’icône **Applications** dans la barre latérale. Le titre de votre application chargée en version test apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans Office.

    :::image type="content" source="images/office-desktop-more-apps.png" alt-text="Cliquez sur l’option points de suspension (« Autres applications ») dans la barre latérale de Office client de bureau pour afficher vos onglets personnels installés":::.

### <a name="office-on-the-web"></a>Office sur le web

Pour afficher un aperçu de l’exécution de votre application dans Office sur le Web :

1. **Connectez-vous à office.com** avec les informations d’identification du locataire de test.
1. Sélectionnez l’icône **Applications** dans la barre latérale. Le titre de votre application chargée en version test apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans Office sur le Web.

    :::image type="content" source="images/office-web-more-apps.png" alt-text="Cliquez sur l’option « Autres applications » dans la barre latérale de office.com pour afficher vos onglets personnels installés":::

### <a name="office-app-for-android"></a>Application Office pour Android

> [!NOTE]
> Avant d’installer l’application, procédez [comme suit pour installer la dernière version bêta de l’application Office](prerequisites.md#mobile) et faire partie du programme bêta.

Pour afficher votre application s’exécutant dans l’application Office pour Android :

1. Lancez l’application Office et connectez-vous à l’aide de votre compte de locataire de développement. Si l’application Office pour Android était déjà en cours d’exécution avant le chargement indépendant de votre application dans Teams, vous devez la redémarrer pour la voir parmi vos applications installées.
1. Sélectionnez l’icône **Applications** . Votre application chargée en version test apparaît parmi les applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans l’application Office pour Android.

:::image type="content" source="images/office-mobile-apps.png" alt-text="Appuyez sur l’option « Applications » dans la barre latérale de l’application Office pour afficher vos onglets personnels installés":::

## <a name="troubleshooting"></a>Résolution des problèmes

Actuellement, un sous-ensemble de types et de fonctionnalités d’application Teams est pris en charge dans les clients Outlook et Office. Cette prise en charge s’étend au fil du temps.

Reportez-vous à la [prise en charge de Microsoft 365](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook) pour vérifier la prise en charge de l’hôte pour différentes fonctionnalités TeamsJS.

Pour obtenir un résumé global de la prise en charge de l’hôte et de la plateforme Microsoft 365 pour les applications Teams, consultez [Étendre les applications Teams dans Microsoft 365](overview.md).

Vous pouvez vérifier la prise en charge par l’hôte d’une fonctionnalité donnée au moment de l’exécution en appelant la `isSupported()` fonction sur cette fonctionnalité (espace de noms) et en ajustant le comportement de l’application selon les besoins. Cela permet à votre application d’activer l’interface utilisateur et les fonctionnalités des hôtes qui la prennent en charge, et de fournir une expérience de secours appropriée dans les hôtes qui ne le prennent pas en charge. Pour plus d’informations, consultez [Différencier votre expérience d’application](../tabs/how-to/using-teams-client-sdk.md#differentiate-your-app-experience).

Utilisez les [canaux de la communauté des développeurs Microsoft Teams](/microsoftteams/platform/feedback) pour signaler les problèmes et fournir des commentaires.

### <a name="debugging"></a>Débogage

À partir du Kit de ressources Teams, vous pouvez déboguer (`F5`) votre application onglet s’exécutant dans Office et Outlook, en plus de Teams.

:::image type="content" source="images/toolkit-debug-targets.png" alt-text="Choisir parmi les cibles de débogage Teams, Outlook et Office dans le Kit de ressources Teams":::

Lors de la première exécution du débogage local vers Office ou Outlook, vous êtes invité à vous connecter à votre compte de locataire Microsoft 365 et à installer un certificat de test auto-signé. Vous serez également invité à installer manuellement Teams. Sélectionnez **Installer dans Teams** pour ouvrir une fenêtre de navigateur et installer manuellement votre application. Sélectionnez Ensuite **Continuer** pour continuer à déboguer votre application dans Office/Outlook.

:::image type="content" source="images/toolkit-dialog-teams-install.png" alt-text="Boîte à outils - Boîte à outils - Installation de Teams":::

Fournissez des commentaires et signalez les problèmes liés à l’expérience de débogage du Kit de ressources Teams dans [Microsoft Teams Framework (TeamsFx).](https://github.com/OfficeDev/TeamsFx/issues)

#### <a name="mobile-debugging"></a>Débogage mobile

Le débogage Teams Toolkit (`F5`) n’est pas encore pris en charge avec l’application Office pour Android. Voici comment déboguer à distance votre application s’exécutant dans l’application Office pour Android :

1. Si vous déboguez à l’aide d’un appareil Android physique, connectez-le à votre machine de développement et activez l’option [de débogage USB](https://developer.android.com/studio/debug/dev-options). Cette option est activée par défaut avec l’émulateur Android.
1. Lancez l’application Office à partir de votre appareil Android.
1. Ouvrez votre profil **Me > Paramètres > Autoriser le débogage**, puis activez l’option **Activer le débogage à distance**.

    :::image type="content" source="images/office-android-enable-remote-debugging.png" alt-text="Capture d’écran montrant Activer le débogage à distance":::

1. **Paramètres de** sortie.
1. Quittez l’écran de votre profil.
1. Sélectionnez **Applications** et lancez votre application chargée de manière indépendante pour qu’elle s’exécute dans l’application Office.
1. Vérifiez que votre appareil Android est connecté à votre ordinateur de développement. À partir de votre ordinateur de développement, ouvrez votre navigateur sur sa page d’inspection DevTools. Par exemple, accédez à `edge://inspect/#devices` Microsoft Edge pour afficher la liste des webViews Android compatibles avec le débogage.
1. Recherchez l’URL `Microsoft Teams Tab` avec votre onglet et sélectionnez **Inspecter** pour démarrer le débogage de votre application avec DevTools.

    :::image type="content" source="images/office-android-debug.png" alt-text="capture d’écran montrant la liste des vues web dans devtool":::

1. Déboguer votre application onglet dans Android WebView. De la même façon, vous [déboguez à distance](/microsoft-edge/devtools-guide-chromium/remote-debugging) un site web standard sur un appareil Android.

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Node.js** |
|---------------|--------------|--------|
| Liste des tâches | Liste de tâches modifiable avec l’authentification unique générée avec React et Azure Functions. Fonctionne uniquement dans Teams (utilisez cet exemple d’application pour essayer le processus de mise à niveau décrit dans ce didacticiel). | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend)  |
| Todo List (Microsoft 365) | Liste de tâches modifiable avec l’authentification unique générée avec React et Azure Functions. Fonctionne dans Teams, Outlook, Office. | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)|
| Éditeur d’images (Microsoft 365) | Créez, modifiez, ouvrez et enregistrez des images à l’aide de Microsoft API Graph. Fonctionne dans Teams, Outlook, Office. | [View](https://github.com/OfficeDev/m365-extensibility-image-editor) |
| Exemple de page de lancement (Microsoft 365) | Illustre l’authentification SSO et les fonctionnalités du Kit de développement logiciel (SDK) TeamsJS disponibles dans différents hôtes. Fonctionne dans Teams, Outlook, Office. | [View](https://github.com/OfficeDev/microsoft-teams-library-js/tree/main/apps/sample-app) |
| Application Northwind Orders | Montre comment utiliser le Kit de développement logiciel (SDK) Microsoft TeamsJS V2 pour étendre l’application Teams à d’autres applications hôtes M365. Fonctionne dans Teams, Outlook, Office. Optimisé pour les appareils mobiles.| [View](https://github.com/microsoft/app-camp/tree/main/experimental/ExtendTeamsforM365) |

## <a name="next-step"></a>Étape suivante

Publiez votre application pour qu’elle soit détectable dans Teams, Outlook et Office :

> [!div class="nextstepaction"]
> [Publier des applications Teams pour Outlook et Office](publish.md)