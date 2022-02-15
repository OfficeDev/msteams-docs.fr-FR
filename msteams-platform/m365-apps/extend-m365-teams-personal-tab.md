---
title: Étendre une application Teams onglet personnel à travers Microsoft 365
description: Étendre une application Teams onglet personnel à travers Microsoft 365
ms.date: 11/15/2021
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: medium
ms.openlocfilehash: 9c6c88835dc24c64f93605d09ac15da5409add0f
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821415"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Étendre un onglet Teams’une page à l’autre Microsoft 365

> [!NOTE]
> *L’extension d Teams onglet personnel sur Microsoft 365* est actuellement disponible uniquement en prévisualisation [pour les développeurs publics](../resources/dev-preview/developer-preview-intro.md). Les fonctionnalités incluses dans l’aperçu peuvent ne pas être terminées et peuvent faire l’objet de modifications avant de devenir disponibles dans la version publique. Elles sont fournies uniquement à des fins de test et d’exploration. Elles ne doivent pas être utilisées dans les applications de production.

Les onglets personnels offrent un excellent moyen d’améliorer Microsoft Teams expérience utilisateur. À l’aide d’onglets personnels, vous pouvez fournir à un utilisateur un accès à son application directement dans Teams, sans que l’utilisateur n’a à quitter l’expérience ou à se connecter à nouveau. Avec cet aperçu, les onglets personnels peuvent s’afficher dans d’Microsoft 365 applications. Ce didacticiel illustre le processus de prise d’un onglet personnel Teams existant et sa mise à jour pour qu’il s’exécute à la fois dans les expériences de bureau et web Outlook, ainsi que dans Office sur le Web (office.com).

La mise à jour de votre application personnelle pour qu’elle s’exécute Outlook et Office Home implique les étapes suivantes :

> [!div class="checklist"]
> * Mettre à jour le manifeste de votre application
> * Mettre à jour vos références du SDK TeamsJS 
> * Modifier vos en-têtes de stratégie de sécurité du contenu
> * Mettre à jour Microsoft Azure Active Directory (Azure AD) inscription de l’application pour l’signature unique (SSO)

Le test de votre application nécessite les étapes suivantes :

> [!div class="checklist"]
> * Inscrire votre client Microsoft 365 client dans *les Office 365 de publication ciblées*
> * Configurer votre compte pour accéder aux versions d’aperçu Outlook et Office applications
> * Chargez une version de votre application mise à jour dans Teams

Après ces étapes, votre application doit apparaître dans les versions d’Outlook et Office applications.

## <a name="prerequisites"></a>Prerequisites

Pour terminer ce didacticiel, vous aurez besoin des instructions ci-après :

* Un client Microsoft 365 programme pour les développeurs en bac à sable (sandbox)
* Votre client bac à sable (sandbox) inscrit *à Office 365 releases ciblées*
* Ordinateur avec des applications Office installées à partir du canal Microsoft 365 Apps *bêta*
* (Facultatif) [Teams Shared Computer Toolkit](https://aka.ms/teams-toolkit) d’extension Microsoft Visual Studio code pour vous aider à mettre à jour votre code

> [!div class="nextstepaction"]
> [Installer les composants prérequis](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Préparer votre onglet personnel pour la mise à niveau

Si vous avez une application d’onglet personnel existante, faites une copie ou une branche de votre projet de production pour tester et mettez à jour votre ID d’application dans le manifeste de l’application pour utiliser un nouvel identificateur (distinct de l’ID d’application de production).

Si vous souhaitez utiliser un exemple de code pour suivre ce didacticiel, suivez les étapes de configuration de l’exemple de mise en route avec la liste de [todos](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) pour créer une application d’onglet personnel à l’aide de l’extension Teams Shared Computer Toolkit pour Visual Studio Code. Vous pouvez également commencer avec le même exemple de liste de todos mis à jour pour l’aperçu du [SDK TeamsJS v2](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365) et passer à l’aperçu de votre onglet personnel dans [d’autres Microsoft 365 expériences](#preview-your-personal-tab-in-other-microsoft-365-experiences). L’exemple mis à jour est également disponible dans Teams Shared Computer Toolkit extension : *DevelopmentView* >  *samplesTodo* >  **List (Works in Teams, Outlook and Office)**.

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="Exemple de liste de todos (fonctionne dans Teams, Outlook et Office) dans Teams Shared Computer Toolkit":::


## <a name="update-the-app-manifest"></a>Mettre à jour le manifeste de l’application

Vous devez utiliser le schéma de manifeste d’aperçu [du développeur Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) `Microsoft 365 DevPreview` et la version du manifeste pour permettre à votre onglet personnel Teams de s’exécuter dans Office et Outlook.

Vous pouvez utiliser Teams Shared Computer Toolkit pour mettre à jour le manifeste de votre application ou appliquer les modifications manuellement :

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

Si vous avez utilisé Teams Shared Computer Toolkit pour créer votre application personnelle, vous pouvez également l’utiliser pour valider les modifications apportées à votre fichier manifeste et identifier les erreurs éventuelles. Ouvrez la palette `Ctrl+Shift+P` de commandes et recherchez **Teams :** Valider le fichier manifeste ou sélectionnez l’option dans le menu Déploiement de l’Teams Shared Computer Toolkit (recherchez l’icône Teams sur le côté gauche de Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams Shared Computer Toolkit’option « Valider le fichier manifeste » sous le menu « Déploiement »":::

## <a name="update-sdk-references"></a>Mettre à jour les références du SDK

Pour s’exécuter Outlook et Office, votre application doit dépendre du package `@microsoft/teams-js@2.0.0-beta.1` npm (ou d’une version *bêta* ultérieure). Bien que le code avec des versions `@microsoft/teams-js` de niveau bas soit pris en charge dans Outlook et Office, les avertissements de suppression seront consignés et la prise en charge des versions `@microsoft/teams-js` de niveau bas dans Outlook et Office cessera.

Vous pouvez utiliser Teams Shared Computer Toolkit pour automatiser certaines des modifications de code afin d’adopter la version `@microsoft/teams-js`suivante de , mais si vous souhaitez réaliser les étapes manuellement, voir [Microsoft Teams JavaScript client SDK Preview](using-teams-client-sdk-preview.md) pour plus d’informations.

1. Ouvrez *la palette de commandes* : `Ctrl+Shift+P`
1. Exécuter la commande `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

Une fois l’exécution terminée, `package.json` l’utilitaire aura mis à jour votre fichier avec la dépendance du SDK TeamsJS (`@microsoft/teams-js@2.0.0-beta.1`ou version ultérieure), `*.jsx/.tsx` `*.js/.ts` et vos fichiers et vos fichiers seront mis à jour avec :

> [!div class="checklist"]
> * `package.json` références à la prévisualisation du SDK TeamsJS
> * Instructions Import pour l’aperçu du SDK TeamsJS
> * [Appels de fonction, d’enum et d’interface](using-teams-client-sdk-preview.md#apis-organized-into-capabilities) vers l’aperçu du SDK TeamsJS
> * `TODO` rappels de commentaires pour passer en revue les zones qui peuvent être touchées par les modifications [de l’interface](using-teams-client-sdk-preview.md#updates-to-the-context-interface) context
> * `TODO` commenter les rappels pour [s’assurer que la conversion en fonctions de promesses](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) à partir de fonctions de style de rappel s’est bien passé sur chaque site d’appel trouvé par l’outil

> [!IMPORTANT]
> Le *code.htmlfichiers* de mise à niveau n’est pas pris en charge par les outils de mise à niveau et nécessite des modifications manuelles.

> [!NOTE]
> Si vous souhaitez mettre à jour manuellement votre code, voir Microsoft Teams prévisualisation du [SDK client JavaScript](using-teams-client-sdk-preview.md) pour en savoir plus sur les modifications requises.

## <a name="configure-content-security-policy-headers"></a>Configurer les en-têtes de stratégie de sécurité du contenu

[Comme dans Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs), les applications d’onglets sont hébergées dans (éléments [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)) Office clients web Outlook web.

Si votre application utilise des en-têtes de stratégie de sécurité du [contenu (](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) CSP), assurez-vous que vous autorisez tous les ancêtres d’images suivants dans vos [en-têtes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) CSP :

|Microsoft 365 hôte| autorisation frame-ancêtre|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Mettre à jour Azure AD’inscription de l’application pour l’sso

Azure Active Directory L’signature unique (SSO) pour les onglets personnels fonctionne de la même manière dans Office et Outlook que dans [Teams](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso), mais vous devez ajouter plusieurs identificateurs d’application client à l’inscription de l’application Azure AD de votre application onglet dans le portail d’inscription des applications de votre client.

1. Connectez-vous [Microsoft Azure portail avec](https://portal.azure.com) votre compte client en bac à sable.
1. Ouvrez le **blade d’inscription de l’application** .
1. Sélectionnez le nom de votre application d’onglet personnel pour ouvrir son inscription. 
1. **Sélectionnez Exposer une API** (sous *Gérer*).

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="Autoriser les ID clients à partir du blade *App registrations* sur le portail Azure":::

Dans la section **Applications clientes autorisées** , assurez-vous que toutes les valeurs `Client Id` suivantes sont ajoutées :

|Microsoft 365 application cliente | ID du client |
|--|--|
|Teams bureau, mobile |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams web |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Office.com  |4345a7b9-9a63-4910-a426-35363201d503|
|Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
|Office bureau  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
|Version de bureau d’Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-0000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>Charger une version test de votre application dans Teams

La dernière étape consiste à recharger une version de votre onglet personnel mis à jour ([package](/microsoftteams/platform/concepts/build-and-test/apps-package) d’application) dans Microsoft Teams. Une fois terminée, votre application peut s’exécuter dans Office et Outlook, en plus de Teams.

1. Compressez votre application Teams ([icônes de manifeste et d’application](/microsoftteams/platform/resources/schema/manifest-schema#icons)) dans un fichier zip. Si vous avez utilisé Teams Shared Computer Toolkit pour créer votre application, vous pouvez facilement le faire à l’aide de l’option package de métadonnées **Zip Teams** dans *le menu Déploiement* de Teams Shared Computer Toolkit ou dans la palette `Ctrl+Shift+P` de commandes de Visual Studio Code :

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Option « Zip Teams package de métadonnées » dans l’extension Teams Shared Computer Toolkit pour Visual Studio Code":::

1. Connectez-vous Teams avec votre compte client en bac à sable et assurez-vous que vous êtes sur la prévisualisation du développeur public. Vous pouvez vérifier que vous êtes sur l’aperçu dans le client Teams en cliquant sur le menu des ellipses (**...**) en fonction de votre profil utilisateur et  en ouvrant Sur le point de vérifier que l’option d’aperçu développeur est surliée.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="À Teams menu des ellipses, ouvrez « À propos de » et vérifiez que l’option « Aperçu développeur » est cochée":::

1. Ouvrez *le* volet Applications, puis cliquez **Télécharger une application** personnalisée, **puis Télécharger pour moi ou mes équipes**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Bouton « Télécharger application personnalisée » dans le volet Teams applications":::

1. Sélectionnez votre package d’application, puis cliquez sur *Ouvrir*.

Une fois le chargement de version Teams, votre onglet personnel sera disponible dans Outlook et Office. N’oubliez pas de vous connectez avec les mêmes informations d’identification que vous avez utilisées pour le chargement de version de version de votre application dans Teams.

Vous pouvez épingler l’application pour un accès rapide ou trouver votre application dans les ellipses (**...**) parmi les applications récentes dans la barre latérale à gauche.

> [!NOTE]
> L’épinglage d’une application Teams ne l’épingle pas en tant qu’application dans Office.com ou Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Afficher un aperçu de votre onglet personnel dans d’autres Microsoft 365 expériences

Lorsque vous Teams mis à niveau votre onglet personnel et que vous le chargez de nouveau dans Teams, il s’exécute également sur les clients de bureau et web Outlook et les clients Office sur le Web (office.com). Voici comment l’afficher en prévisualisation à partir de ces Microsoft 365 expériences utilisateur.

### <a name="outlook"></a>Outlook

Pour afficher votre application s’exécutant Outlook sur Windows bureau, lancez Outlook et connectez-vous à l’aide de votre compte de client dev. Cliquez sur les ellipses (**...**) dans la barre latérale. Le titre de votre application installée s’affiche parmi vos applications installées.

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Cliquez sur l’option « Autres applications » sur la barre latérale du client de bureau Office pour voir vos onglets personnels installés":::

Cliquez sur l’icône de votre application pour lancer votre application dans Outlook.

### <a name="outlook-on-the-web"></a>Outlook sur le web

Pour afficher votre application dans Outlook sur le web, visitez https://outlook.office.com et connectez-vous à l’aide de votre compte de client dev. Cliquez sur les ellipses (**...**) dans la barre latérale. Le titre de votre application installée s’affiche parmi vos applications installées.

:::image type="content" source="images/outlook-web-more-apps.png" alt-text="Cliquez sur l’option « Autres applications » sur la barre latérale de outlook.com pour voir vos onglets personnels installés":::

Cliquez sur l’icône de votre application pour lancer et afficher un aperçu de votre application s’exécutant Outlook sur le web.

### <a name="office-on-the-web"></a>Office sur le web

> [!IMPORTANT]
> Reportez-vous aux dernières mises à jour du [blog Microsoft Teams - Microsoft 365 Developer](https://devblogs.microsoft.com/microsoft365dev/) pour vérifier si la prise en charge de Office.com pour Teams applications personnelles est disponible pour votre client test.

Pour afficher un aperçu de votre application en cours d Office sur le Web, connectez-vous office.com avec les informations d’identification du client de test. Cliquez sur les ellipses (**...**) dans la barre latérale. Le titre de votre application installée s’affiche parmi vos applications installées.

Cliquez sur l’icône de votre application pour lancer votre application dans Office Accueil.

## <a name="next-steps"></a>Prochaines étapes

Outlook- et Office onglets personnels activés sont en prévisualisation et ne sont pas pris en charge pour une utilisation en production. Voici comment distribuer votre application d’onglet personnel pour afficher un aperçu des audiences à des fins de test.

### <a name="single-tenant-distribution"></a>Distribution d’un seul client

Outlook onglets personnels Office et activés pour l’aperçu peuvent être distribués à une audience en prévisualisation sur un client de test (ou de production) de l’une des trois manières ci-après :

#### <a name="teams-client"></a>Teams client

Dans le menu *Applications*, *sélectionnez Gérer vos applicationsSoumettre* >  **une application dans votre organisation**. Cela nécessite l’approbation de votre administrateur informatique.

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams Admin Center

En tant qu’administrateur Teams, vous pouvez télécharger et préinstaller le package d’application pour le client de votre organisation à partir de https://admin.teams.microsoft.com/. [Consultez Télécharger vos applications personnalisées dans le Centre d Microsoft Teams’administration Windows pour](/MicrosoftTeams/upload-custom-apps) plus d’informations.

#### <a name="microsoft-admin-center"></a>Centre d’administration Microsoft

En tant qu’administrateur général, vous pouvez télécharger et préinstaller le package d’application à partir de https://admin.microsoft.com/. Pour [plus d’informations, voir Tester et déployer Microsoft 365 Apps par](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) des partenaires dans le portail des applications intégrées.

### <a name="multi-tenant-distribution"></a>Distribution multi-locataires

La distribution dans Microsoft AppSource n’est pas prise en charge pendant cette prévisualisation préliminaire pour les développeurs des Outlook et Office activées Teams onglets personnels.
