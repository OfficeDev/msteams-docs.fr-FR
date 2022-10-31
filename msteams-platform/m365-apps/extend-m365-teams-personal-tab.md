---
title: Étendre une application onglet personnel Teams sur Microsoft 365
description: Découvrez comment mettre à jour votre application d’onglet personnel pour qu’elle s’exécute dans Outlook et Office, en plus de Microsoft Teams.
ms.date: 10/10/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 910a94f34d14c8dbb8a35099d438469fea52155b
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789973"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Étendre un onglet personnel Teams sur Microsoft 365

Les onglets personnels offrent un excellent moyen d’améliorer l’expérience Microsoft Teams. À l’aide d’onglets personnels, vous pouvez fournir à un utilisateur l’accès à son application directement dans Teams, sans que l’utilisateur ait à quitter l’expérience ou à se reconnecter. Avec cette préversion, les onglets personnels peuvent s’allumer dans d’autres applications Microsoft 365. Ce tutoriel illustre le processus de prise d’un onglet personnel Teams existant et sa mise à jour pour l’exécuter dans les expériences de bureau et web Outlook et Office, ainsi que dans l’application Office pour Android.

La mise à jour de votre application personnelle pour qu’elle s’exécute dans Outlook et Office implique les étapes suivantes :

> [!div class="checklist"]
>
> * [Mettez à jour le manifeste de votre application](#update-the-app-manifest).
> * [Mettez à jour vos références du SDK TeamsJS](#update-sdk-references).
> * [Modifiez vos en-têtes de stratégie de sécurité du contenu](#configure-content-security-policy-headers).
> * [Mettez à jour votre inscription d’application Microsoft Azure Active Directory (Azure AD) pour l'Sign-On authentification unique (SSO).](#update-azure-ad-app-registration-for-sso)
> * [Charger une version test de votre application mise à jour dans Teams](#sideload-your-app-in-teams).

Le reste de ce guide vous guide tout au long de ces étapes et vous montre comment afficher un aperçu de votre onglet personnel dans d’autres applications Microsoft 365.

## <a name="prerequisites"></a>Configuration requise

Pour suivre ce didacticiel, vous avez besoin des éléments suivants :

* Un locataire de bac à sable du programme Microsoft 365 Developer
* Votre locataire de bac à sable inscrit dans *Office 365 versions ciblées*
* Un ordinateur avec des applications Office installées à partir du *canal bêta* Microsoft 365 Apps
* (Facultatif) Un appareil ou un émulateur Android sur lequel l’application Office pour Android est installée et inscrite dans le *programme bêta*
* (Facultatif) [Teams Shared Computer Toolkit](https://aka.ms/teams-toolkit) extension pour Microsoft Visual Studio Code afin de vous aider à mettre à jour votre code

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Préparer votre onglet personnel pour la mise à niveau

Si vous disposez d’une application d’onglet personnel existante, effectuez une copie ou une branche de votre projet de production à des fins de test et mettez à jour votre ID d’application dans le manifeste de l’application pour utiliser un nouvel identificateur (distinct de l’ID d’application de production, à des fins de test).

Si vous souhaitez utiliser un exemple de code pour suivre ce tutoriel, suivez les étapes de configuration de [l’exemple liste](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) de tâches pour créer une application d’onglet personnel à l’aide de l’extension Teams Toolkit pour Visual Studio Code, puis revenez à cet article pour la mettre à jour pour Microsoft 365.

Vous pouvez également utiliser une application *hello world d’authentification* unique de base déjà activée pour Microsoft 365 dans la section [Démarrage rapide](#quickstart) suivante, puis passer au [chargement indépendant de votre application dans Teams](#sideload-your-app-in-teams).

### <a name="quickstart"></a>Démarrage rapide

Pour commencer avec un [onglet personnel](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365) qui est déjà activé pour s’exécuter dans Outlook et Office, utilisez l’extension Teams Toolkit pour Visual Studio Code.

1. À partir de Visual Studio Code, ouvrez la palette de commandes (`Ctrl+Shift+P`), tapez `Teams: Create a new Teams app`.
1. Sélectionnez l’option **Créer une application Teams** .
1. Sélectionnez **l’onglet personnel activé pour l’authentification unique**.

    :::image type="content" source="images/toolkit-tab-sample.png" alt-text="La capture d’écran est un exemple qui montre l’exemple liste de tâches (fonctionne dans Teams, Outlook et Office) dans le Kit de ressources Teams.":::
1. Sélectionnez le langage de programmation préféré.
1. Sélectionnez un emplacement sur votre ordinateur local pour le dossier de l’espace de travail et entrez le nom de votre application.
1. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et tapez `Teams: Provision in the cloud` pour créer les ressources d’application requises (plan App Service, compte de stockage, application de fonction, identité managée) dans votre compte Azure.
1. Sélectionnez un abonnement et un groupe de ressources.
1. Sélectionnez **Provisionner**.
1. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et tapez `Teams: Deploy to the cloud` pour déployer l’exemple de code sur les ressources approvisionnées dans Azure et démarrer l’application.
1. Sélectionnez **Déployer**.

À partir de là, vous pouvez passer directement à [un chargement indépendant de votre application dans Teams](#sideload-your-app-in-teams) et afficher un aperçu de votre application dans Outlook et Office. (Le manifeste de l’application et les appels d’API TeamsJS ont déjà été mis à jour pour Microsoft 365.)

## <a name="update-the-app-manifest"></a>Mettre à jour le manifeste de l’application

Vous devez utiliser la version `1.13` du schéma du [manifeste de développeur Teams](../resources/schema/manifest-schema.md) pour permettre à votre onglet personnel Teams de s’exécuter dans Outlook et Office.

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

Si vous avez utilisé Teams Toolkit pour créer votre application personnelle, vous pouvez également l'utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les éventuelles erreurs. Ouvrez la palette de commandes (`Ctrl+Shift+P`) et **recherchez Teams : Valider le fichier manifeste**.

## <a name="update-sdk-references"></a>Mettre à jour les références du Kit de développement logiciel (SDK)

Pour s’exécuter dans Outlook et Office, votre application doit référencer le package `@microsoft/teams-js@2.0.0` npm (ou version ultérieure). Bien que le code avec des versions de niveau inférieur soit pris en charge dans Outlook et Office, les avertissements de dépréciation sont enregistrés et la prise en charge des versions de niveau inférieur de TeamsJS dans Outlook et Office cessera finalement.

Vous pouvez utiliser Teams Toolkit pour identifier et automatiser les modifications de code nécessaires à la mise à niveau des versions 1.x TeamsJS vers TeamsJS version 2.x.x. Vous pouvez également effectuer les mêmes étapes manuellement . Pour plus d’informations, reportez-vous au [Kit de développement logiciel (SDK) du client JavaScript Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) .

1. Ouvrez la *palette de commandes* : `Ctrl+Shift+P`.
1. Exécutez la commande `Teams: Upgrade Teams JS SDK and code references`.

Une fois l’opération terminée, votre fichier *package.json* référencera `@microsoft/teams-js@2.0.0` (ou version ultérieure) et vos `*.js/.ts` fichiers et `*.jsx/.tsx` seront mis à jour avec :

> [!div class="checklist"]
>
> * Importer des instructions pour teams-js@2.x.x
> * [Appels de fonction, d’énumération et d’interface](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) pour teams-js@2.x.x
> * `TODO`rappels de commentaires signalant les zones susceptibles d’être affectées par les modifications apportées à [l’interface de contexte](../tabs/how-to/using-teams-client-sdk.md#updates-to-the-context-interface)
> * `TODO` rappels de commentaire pour [convertir des fonctions de rappel en promesses](../tabs/how-to/using-teams-client-sdk.md#callbacks-converted-to-promises)

> [!IMPORTANT]
> Le code dans *.html* fichiers n’est pas pris en charge par les outils de mise à niveau et nécessite des modifications manuelles.

## <a name="configure-content-security-policy-headers"></a>Configurer les en-têtes de stratégie de sécurité du contenu

Comme dans Microsoft Teams, les applications d’onglet sont hébergées dans [des éléments iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) dans les clients web Office et Outlook.

Si votre application utilise des en-têtes de stratégie de [sécurité du contenu](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP), veillez à autoriser tous les [ancêtres de trame](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) suivants dans vos en-têtes CSP :

|Hôte Microsoft 365| autorisation frame-ancestor|
|--|--|
| Équipes | `teams.microsoft.com` |
| Office | `*.microsoft365.com`, `*.office.com` |
| Outlook | `outlook.live.com`, `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Mettre à jour l’inscription d’application Azure AD pour l’authentification unique

L’authentification [unique (SSO) Azure Active Directory (AD)](../tabs/how-to/authentication/tab-sso-overview.md) pour les onglets personnels fonctionne de la même façon dans Office et Outlook que dans Teams. Toutefois, vous devez ajouter plusieurs identificateurs d’application cliente à l’inscription d’application Azure AD de votre application onglet dans le portail *inscriptions d'applications* de votre locataire.

1. Connectez-vous au [portail Microsoft Azure](https://portal.azure.com) avec votre compte de locataire de bac à sable( sandbox).
1. Ouvrez le **panneau inscriptions d'applications**.
1. Sélectionnez le nom de votre application d’onglet personnel pour ouvrir son inscription d’application.
1. Sélectionnez **Exposer une API** (sous *Gérer*).

    :::image type="content" source="images/azure-app-registration-clients.png" alt-text="La capture d’écran est un exemple montrant les ID client d’autorisation à partir du panneau *inscriptions d'applications* sur Portail Azure.":::

1. Dans la section **Applications clientes autorisées** , vérifiez que toutes les valeurs suivantes `Client Id` sont ajoutées :

    |Application client Microsoft 365 | ID du client |
    |--|--|
    |Teams bureau, mobile |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
    |Web Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
    |Office web  |4765445b-32c6-49b0-83e6-1d93765276ca|
    |Version de bureau d’Office  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
    |Office mobile  | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook desktop, mobile | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook web | bc59ab01-8403-45c6-8796-ac3ef710b3e3|

    > [!NOTE]
    > Certaines applications clientes Microsoft 365 partagent des ID client.

## <a name="sideload-your-app-in-teams"></a>Charger une version test de votre application dans Teams

La dernière étape de l’exécution de votre application dans Office et Outlook consiste à charger une version test de votre [package d’application d’onglet](..//concepts/build-and-test/apps-package.md) personnel mis à jour dans Microsoft Teams.

1. Empaquetez votre application Teams ([manifeste](../resources/schema/manifest-schema.md) et [icônes d’application](/microsoftteams/platform/resources/schema/manifest-schema#icons)) dans un fichier zip. Si vous avez utilisé le Kit de ressources Teams pour créer votre application, vous pouvez facilement le faire à l’aide de l’option **Package de métadonnées Zip Teams** dans le menu **Déploiement** du Kit de ressources Teams.

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="« La capture d’écran est un exemple qui montre l’option Zip Teams metadata package » dans l’extension Teams Toolkit pour Visual Studio Code.":::

1. Connectez-vous à Teams avec votre compte client sandbox et basculez en mode *Aperçu développeur* . Sélectionnez le menu des points de suspension (**...**) près de votre profil utilisateur, puis sélectionnez : **À propos de** > **Aperçu développeur**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="La capture d’écran montre comment sélectionner l’option « Developer Preview ».":::

1. Sélectionnez **Applications** pour ouvrir le volet **Gérer vos applications**. Sélectionnez ensuite **Charger une application**.

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="La capture d’écran est un exemple montrant les options Gérer vos applications et Publier une application.":::

1. Choisissez **l’option Charger une application personnalisée** et sélectionnez votre package d’application.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="La capture d’écran est un exemple montrant l’option de chargement de l’application am dans Teams.":::

Une fois qu’il est chargé de manière indépendante dans Teams, votre onglet personnel est disponible dans Outlook et Office. Vous devez vous connecter avec les mêmes informations d’identification que celles que vous avez utilisées pour charger une version test de votre application dans Teams. Lorsque vous exécutez l’application Office pour Android, vous devez redémarrer l’application pour utiliser votre application d’onglet personnel à partir de l’application Office.

Vous pouvez épingler l’application pour un accès rapide, ou vous pouvez trouver votre application dans le menu volant des points de suspension (**...**) parmi les applications récentes dans la barre latérale sur la gauche. L’épinglage d’une application dans Teams ne l’épingle pas en tant qu’application dans Office ou Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Afficher un aperçu de votre onglet personnel dans d’autres expériences Microsoft 365

Voici comment afficher un aperçu de votre application s’exécutant dans Office et Outlook, les clients de bureau web et Windows.

> [!NOTE]
> Si vous utilisez l’exemple d’application Teams Toolkit et le désinstallez de Teams, il est supprimé des catalogues **Autres applications** dans Outlook et Office.

### <a name="outlook-on-windows"></a>Outlook sur Windows

Pour afficher votre application en cours d’exécution dans Outlook sur Windows bureau :

1. Lancez Outlook et connectez-vous à l’aide de votre compte de locataire de développement.
1. Dans la barre latérale, sélectionnez  **Plus d’applications**. Le titre de votre application chargée de manière indépendante apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans Outlook.

    :::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="La capture d’écran est un exemple qui montre l’option de points de suspension (Autres applications) dans la barre latérale du client de bureau Outlook pour afficher vos onglets personnels installés.":::

### <a name="outlook-on-the-web"></a>Outlook sur le web

Pour afficher votre application dans Outlook sur le web :

1. Accédez à [Outlook sur le web](https://outlook.office.com) et connectez-vous à l’aide de votre compte de locataire de développement.
1. Dans la barre latérale, sélectionnez  **Plus d’applications**. Le titre de votre application chargée de manière indépendante apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer et afficher un aperçu de votre application en cours d’exécution dans Outlook sur le web.

    :::image type="content" source="images/outlook-web-more-apps.png" alt-text="La capture d’écran est un exemple qui montre l’option de sélection (Plus d’applications) sur la barre latérale de outlook.com pour afficher vos onglets personnels installés.":::

### <a name="office-on-windows"></a>Office pour Windows

Pour afficher votre application en cours d’exécution dans Office sur Windows bureau :

1. Lancez Office et connectez-vous à l’aide de votre compte de locataire de développement.
1. Sélectionnez l’icône **Applications** dans la barre latérale. Le titre de votre application chargée de manière indépendante apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans Office.

    :::image type="content" source="images/office-desktop-more-apps.png" alt-text="La capture d’écran est un exemple qui montre l’option de sélection (Autres applications) dans la barre latérale du client de bureau Office pour afficher vos onglets personnels installés.":::

### <a name="office-on-the-web"></a>Office sur le web

Pour afficher un aperçu de l’exécution de votre application dans Office sur le Web :

1. Connectez-vous **à office.com** avec les informations d’identification du locataire de test.
1. Sélectionnez l’icône **Applications** dans la barre latérale. Le titre de votre application chargée de manière indépendante apparaît parmi vos applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans Office sur le Web.

    :::image type="content" source="images/office-web-more-apps.png" alt-text="La capture d’écran est un exemple qui montre l’option (Plus d’applications) dans la barre latérale de office.com pour afficher vos onglets personnels installés.":::

### <a name="office-app-for-android"></a>Application Office pour Android

> [!NOTE]
> Avant d’installer l’application, effectuez [les étapes pour installer la dernière version bêta de l’application Office](prerequisites.md#mobile) et faire partie du programme bêta.

Pour afficher votre application en cours d’exécution dans l’application Office pour Android :

1. Lancez l’application Office et connectez-vous à l’aide de votre compte de locataire de développement. Si l’application Office pour Android était déjà en cours d’exécution avant le chargement indépendant de votre application dans Teams, vous devez la redémarrer pour voir dans vos applications installées.
1. Sélectionnez l’icône **Applications** . Votre application chargée de manière indépendante apparaît parmi les applications installées.
1. Sélectionnez l’icône de votre application pour lancer votre application dans l’application Office pour Android.

    :::image type="content" source="images/office-mobile-apps.png" alt-text="La capture d’écran est un exemple montrant l’option « Applications » dans la barre latérale de l’application Office pour afficher vos onglets personnels installés.":::

## <a name="troubleshooting"></a>Résolution des problèmes

Actuellement, un sous-ensemble des types et fonctionnalités d’application Teams est pris en charge dans les clients Outlook et Office. Cette prise en charge s’étend au fil du temps.

Reportez-vous à la [prise en charge de Microsoft 365](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook) pour vérifier la prise en charge de l’hôte pour les différentes fonctionnalités de TeamsJS.

Pour obtenir un résumé général de la prise en charge de l’hôte et de la plateforme Microsoft 365 pour les applications Teams, consultez [Étendre les applications Teams dans Microsoft 365](overview.md).

Vous pouvez vérifier la prise en charge par l’hôte d’une fonctionnalité donnée au moment de l’exécution en appelant la `isSupported()` fonction sur cette fonctionnalité (espace de noms) et en ajustant le comportement de l’application le cas échéant. Cela permet à votre application d’éclairer l’interface utilisateur et les fonctionnalités dans les hôtes qui la prennent en charge et de fournir une expérience de secours appropriée dans les hôtes qui ne le font pas. Pour plus d’informations, consultez [Différencier l’expérience de votre application](../tabs/how-to/using-teams-client-sdk.md#differentiate-your-app-experience).

Utilisez les [canaux de la communauté des développeurs Microsoft Teams](/microsoftteams/platform/feedback) pour signaler les problèmes et fournir des commentaires.

### <a name="debugging"></a>Débogage

À partir du Kit de ressources Teams, vous pouvez Déboguer (`F5`) votre application onglet s’exécutant dans Office et Outlook, en plus de Teams.

:::image type="content" source="images/toolkit-debug-targets.png" alt-text="La capture d’écran est un exemple qui montre le menu déroulant de débogage dans Teams dans le Kit de ressources Teams.":::

Lors de la première exécution du débogage local dans Office ou Outlook, vous êtes invité à vous connecter à votre compte de locataire Microsoft 365 et à installer un certificat de test auto-signé. Vous serez également invité à installer manuellement Teams. Sélectionnez **Installer dans Teams** pour ouvrir une fenêtre de navigateur et installer manuellement votre application. Sélectionnez ensuite **Continuer** pour procéder au débogage de votre application dans Office/Outlook.

:::image type="content" source="images/toolkit-dialog-teams-install.png" alt-text="La capture d’écran est un exemple montrant la boîte de dialogue Kit de ressources à installer dans Teams.":::

Fournissez des commentaires et signalez les problèmes liés à l’expérience de débogage du Kit de ressources Teams dans [Microsoft Teams Framework (TeamsFx).](https://github.com/OfficeDev/TeamsFx/issues)

#### <a name="mobile-debugging"></a>Débogage mobile

Le débogage du Kit de ressources Teams (`F5`) n’est pas encore pris en charge avec l’application Office pour Android. Voici comment déboguer à distance votre application s’exécutant dans l’application Office pour Android :

1. Si vous déboguez à l’aide d’un appareil Android physique, connectez-le à votre machine de développement et activez l’option de [débogage USB](https://developer.android.com/studio/debug/dev-options). Cette option est activée par défaut avec l’émulateur Android.
1. Lancez l’application Office à partir de votre appareil Android.
1. Ouvrez votre profil **Me > Paramètres > Autoriser le débogage**, puis activez l’option **Activer le débogage à distance**.

    :::image type="content" source="images/office-android-enable-remote-debugging.png" alt-text="La capture d’écran est un exemple montrant l’option bascule Activer le débogage à distance.":::

1. Laissez **Paramètres**.
1. Quittez l’écran de votre profil.
1. Sélectionnez **Applications** et lancez votre application chargée de manière indépendante pour qu’elle s’exécute dans l’application Office.
1. Vérifiez que votre appareil Android est connecté à votre machine de développement. À partir de votre machine de développement, ouvrez votre navigateur sur sa page d’inspection DevTools. Par exemple, accédez à `edge://inspect/#devices` dans Microsoft Edge pour afficher une liste de WebViews Android activés pour le débogage.
1. Recherchez l’URL `Microsoft Teams Tab` de votre onglet et sélectionnez **Inspecter** pour commencer à déboguer votre application avec DevTools.

    :::image type="content" source="images/office-android-debug.png" alt-text="La capture d’écran est un exemple qui montre la liste des vues web dans devtool.":::

1. Déboguez votre application d’onglet dans Android WebView. De la même façon, vous [déboguez à distance](/microsoft-edge/devtools-guide-chromium/remote-debugging) un site web standard sur un appareil Android.

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Node.js** |
|---------------|--------------|--------|
| Liste des tâches | Liste de tâches modifiable avec l’authentification unique générée avec React et Azure Functions. Fonctionne uniquement dans Teams (utilisez cet exemple d’application pour essayer le processus de mise à niveau décrit dans ce tutoriel). | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend)  |
| Liste de tâches (Microsoft 365) | Liste de tâches modifiable avec l’authentification unique générée avec React et Azure Functions. Fonctionne dans Teams, Outlook, Office. | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)|
| Éditeur d’images (Microsoft 365) | Créez, modifiez, ouvrez et enregistrez des images à l’aide de Microsoft API Graph. Fonctionne dans Teams, Outlook, Office. | [View](https://github.com/OfficeDev/m365-extensibility-image-editor) |
| Exemple de page de lancement (Microsoft 365) | Illustre l’authentification unique et les fonctionnalités du Kit de développement logiciel (SDK) TeamsJS disponibles dans différents hôtes. Fonctionne dans Teams, Outlook, Office. | [View](https://github.com/OfficeDev/microsoft-teams-library-js/tree/main/apps/sample-app) |
| Application Commandes Northwind | Montre comment utiliser microsoft TeamsJS SDK V2 pour étendre l’application Teams à d’autres applications hôtes Microsoft 365. Fonctionne dans Teams, Outlook, Office. Optimisé pour les appareils mobiles.| [View](https://github.com/microsoft/app-camp/tree/main/experimental/ExtendTeamsforM365) |

## <a name="next-step"></a>Étape suivante

Publiez votre application pour qu’elle soit détectable dans Teams, Outlook et Office :

> [!div class="nextstepaction"]
> [Publier des applications Teams pour Outlook et Office](publish.md)
