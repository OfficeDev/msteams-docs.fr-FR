---
title: Conditions préalables à la création de votre application Teams à l’aide de Visual Studio Code
author: zyxiaoyuer
description: Dans ce module, découvrez les prérequis requis pour les outils et le Kit de développement logiciel (SDK)
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 412b7bfedb6ba39f1d38f42aac56cc793ea385b1
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617078"
---
# <a name="prerequisites-for-creating-your-teams-app"></a>Conditions préalables à la création de votre application Teams

Vérifiez que les conditions préalables suivantes sont remplies avant de commencer à créer votre application Teams :

* [Conditions de base pour créer votre application Teams](#basic-requirements-to-build-your-teams-app)
* [Préparer des comptes pour créer votre application Teams](#accounts-to-build-your-teams-app)
* [Autorisation de chargement indépendant](#sideloading-permission)

## <a name="basic-requirements-to-build-your-teams-app"></a>Conditions de base pour créer votre application Teams

Vérifiez que les exigences suivantes sont remplies avant de commencer à créer votre application Teams :

| &nbsp; | Exigences de base | Pour l’utilisation| Pour le type d’environnement|
   | --- | --- | --- |
   | **Obligatoire** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | Toolkit Teams| Extension Microsoft Visual Studio Code qui crée une structure de projet pour votre application. Utilisez la dernière version. | JavaScript et SPFx|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Collaborez avec toutes les personnes avec lesquelles vous travaillez par le biais d’applications pour la conversation, les réunions, les appels, le tout au même endroit.| JavaScript et SPFx|
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | Environnement runtime JavaScript principal. Utilisez la dernière version de LTS v16.| JavaScript et SPFx|
   | &nbsp; |[Gestionnaire de package de nœuds (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx) | Installez et gérez les packages à utiliser dans les applications Node.js et ASP.NET Core.| JavaScript et SPFx|
   | &nbsp; | [Microsoft&nbsp; Edge](https://www.microsoft.com/edge) (recommandé) ou [Google Chrome](https://www.google.com/chrome/) | Un navigateur avec des outils de développement. | JavaScript et SPFx|
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download) | Environnements de build JavaScript, TypeScript ou SharePoint Framework (SPFx). Utilisez la version 1.55 ou ultérieure. | JavaScript et SPFx|
   | **Optional** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | [Azure Tools pour Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) et [Azure CLI](/cli/azure/install-azure-cli) | Accédez aux données stockées ou déployez un serveur principal cloud pour votre application Teams dans Azure. | JavaScript|
   | &nbsp; | [outils de développement React pour Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) OU [outils de développement React pour Microsoft&nbsp;Edge](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil) | Extension DevTools du navigateur pour la bibliothèque JavaScript React open source. | JavaScript|
   | &nbsp; | [Afficheur Microsoft Graph](https://developer.microsoft.com/graph/graph-explorer) | Outil basé sur un navigateur qui vous permet d’exécuter une requête à partir de données Microsoft Graph. | JavaScript et SPFx|
   | &nbsp; | [Documentation pour les développeurs](https://dev.teams.microsoft.com/) | Portail web pour configurer, gérer et distribuer votre application Teams, y compris à votre organisation ou au magasin Teams.| JavaScript et SPFx|

   > [!NOTE]
   >
   > * Le document est testé avec Teams Toolkit version 4.0.0 et Nodejs version 16.
   > * Signet de l’Explorateur Microsoft Graph pour en savoir plus sur les services Microsoft Graph. Cet outil basé sur un navigateur vous permet d’interroger et d’accéder à Microsoft Graph en dehors d’une application.

## <a name="accounts-to-build-your-teams-app"></a>Comptes pour créer votre application Teams

Vérifiez que vous disposez des comptes suivants avant de commencer à créer votre application Teams :

| Comptes | Pour l’utilisation| Pour le type d’environnement|
| --- | --- |
|[Compte Microsoft 365 avec un abonnement valide.](#microsoft-365-developer-program)|Compte de développeur Teams lors du développement d’une application.| JavaScript et SPFx|
|[Compte Azure](accounts.md#azure-account-to-host-backend-resources)|Ressources principales sur Azure.| JavaScript et SPFx|
|[Compte d’administrateur de site de collection SharePoint](#sharepoint-collection-site-administrator-account) |Déploiement pour l’hébergement.| SPFx|

### <a name="microsoft-365-developer-program"></a>Programme de développement Microsoft 365

Pour créer un compte Microsoft 365, inscrivez-vous à un abonnement au programme Microsoft 365 pour les développeurs. L’abonnement est gratuit pendant 90 jours et continue de se renouveler tant que vous l’utilisez pour l’activité de développement.

Si vous disposez d'un abonnement à Visual Studio Enterprise ou Professional, les deux programmes comprennent un abonnement gratuit à Microsoft 365 [pour les développeurs](https://aka.ms/MyVisualStudioBenefits). Il est actif tant que votre abonnement Visual Studio est actif. Pour plus d’informations, consultez l’[abonnement développeur Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).

Vous pouvez vous inscrire au programme pour les développeurs à l’aide d’un des types de comptes suivants :

* **Compte Microsoft pour un usage personnel**

  :::row:::

    :::column span="3":::

       Le compte permet d’accéder aux produits et services cloud Microsoft, tels qu’Outlook, Messenger, OneDrive, MSN, Xbox Live ou Microsoft 365. 

       Vous pouvez vous inscrire à une boîte aux lettres Outlook.com pour créer un compte Microsoft, qui peut être utilisé pour accéder aux services cloud de Microsoft liés au consommateur ou à Azure.

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/personal-account-icon.png" alt-text="compte personnel.":::
   :::column-end:::

  :::row-end:::

* **Compte professionnel Microsoft pour les entreprises**

  :::row:::

    :::column span="3":::

       Le compte fournit l’accès à tous les services cloud Microsoft de petite, moyenne et d’entreprise. Les services incluent Azure, Microsoft Intune ou Microsoft 365. 

       Lorsque vous vous inscrivez à l’un de ces services en tant qu’organisation, un répertoire informatique est automatiquement configuré dans Azure Active Directory pour représenter votre organisation.

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/work-account-icon.png" alt-text="compte professionnel.":::
    :::column-end:::

  :::row-end:::

#### <a name="create-a-free-microsoft-365-developer-account"></a>Créer un compte de développeur Microsoft 365 gratuit

Pour créer un compte de développeur Microsoft 365 gratuit, rejoignez le programme de développement Microsoft 365 et effectuez le compte suivant :

1. Accédez au[Programme pour les développeurs Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
1. Sélectionnez **Rejoindre maintenant**.
1. Configurez votre compte d’administrateur.

   Vous pouvez voir l’image suivante après la fin de l’abonnement :

    :::image type="content" source="../assets/images/teams-toolkit-v2/m365-account.png" alt-text="Compte M365":::

### <a name="azure-account"></a>Compte Azure

Vous avez besoin d’un compte Azure pour héberger une application Teams ou les ressources principales de votre application Teams à l’aide du Kit de ressources Teams dans Visual Studio Code. Vous devez avoir besoin d’un abonnement Azure dans les scénarios suivants :

* Si vous avez déjà une application existante sur un autre fournisseur de cloud que Azure et que vous souhaitez intégrer l’application sur la plateforme Teams, vous devez disposer d’un abonnement Azure.
* Vous pouvez sélectionner un abonnement Azure pour héberger vos ressources principales à l’aide d’un autre fournisseur de cloud, ou sur vos propres serveurs s’ils sont disponibles à partir du domaine public.

> [!NOTE]
> Vous devez [créer un compte gratuit](https://azure.microsoft.com/free/) avant de commencer.

### <a name="sharepoint-collection-site-administrator-account"></a>Compte d’administrateur de site de collection SharePoint

Lors de la création d’une application Teams à l’aide de l’environnement SPFx, vous avez besoin d’un compte d’administrateur de site de collection SharePoint lors du déploiement pour l’hébergement. Si vous utilisez un locataire de programme pour développeurs Microsoft 365, vous pouvez utiliser le compte d’administrateur que vous avez créé à l’époque.

## <a name="sideloading-permission"></a>Autorisation de chargement indépendant

Après avoir créé l’application, vous devez charger votre application dans Teams sans la distribuer. Ce processus est appelé chargement indépendant. Connectez-vous à votre compte Microsoft 365 pour afficher cette option.

Vous pouvez vérifier si l’autorisation de chargement indépendant est activée à l’aide de Visual Studio Code ou du client Teams.

<br>
<details>
<summary><b>Vérifier l’autorisation de chargement indépendant à l’aide de Visual Studio Code</b></summary>

1. Ouvrez **Visual Studio Code**.
1. Sélectionnez l’icône du Kit de ressources :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams dans la barre d’outils du Kit de ressources Teams.

   > [!NOTE]
   > Si vous ne parvenez pas à voir l’option, consultez [Installer Teams Toolkit](install-Teams-Toolkit.md) pour installer l’extension Teams Toolkit dans Visual Studio Code.
1. Sélectionnez **Se connecter à M365** sous **COMPTES** et connectez-vous à votre compte Microsoft 365.

    :::image type="content" source="../assets/images/teams-toolkit-v2/accounts.png" alt-text="détails des comptes":::

1. Vérifiez si vous pouvez afficher l’option **Chargement indépendant activé** comme illustré dans l’image suivante :

    :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="Activer le chargement indépendant":::

</details>
<br>
<details>
<summary><b>Vérifier l’autorisation de chargement indépendant à l’aide du client Teams</b></summary>

1. Dans le client Teams, sélectionnez **Applications**.
1. Sélectionnez **Gérer votre application**.
1. Sélectionnez **Charger une application**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-app.png" alt-text="Publier une application":::

4. Vérifiez si vous pouvez voir l’option **Charger une application personnalisée** comme illustré dans l’image suivante :

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-custom-app1.png" alt-text="Charger une application personnalisée":::

</details>

### <a name="enable-sideloading-using-admin-center"></a>Activer le chargement indépendant à l’aide du Centre d’administration

Si vous ne parvenez pas à afficher l’option **Charger une application personnalisée,** cela indique que vous n’avez pas l’autorisation requise pour le chargement indépendant.

* Pour un administrateur de locataire, activez le paramètre de chargement indépendant pour votre locataire ou organisation dans le Centre d’administration Teams.
* Si vous n’êtes pas un administrateur de locataire, vous devez contacter votre administrateur de locataire pour activer le chargement indépendant.

Si vous disposez de droits d’administrateur, effectuez les étapes suivantes pour charger l’application personnalisée à l’aide du Centre d’administration :

  1. Connectez-vous à [Centre d’administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur.

  1. Sélectionnez l’icône :::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG"::: > **Teams**.

       :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center.png" alt-text="centre Administration Microsoft 365":::

     > [!Note]
     > L’affichage de l’option **Teams** peut prendre **jusqu’à** 24 heures. Vous pouvez [charger votre application personnalisée dans un environnement Teams](/microsoftteams/upload-custom-apps) à des fins de test et de validation.

  1. Connectez-vous au Centre d’administration Microsoft Teams avec vos informations d’identification d’administrateur.
  1. Sélectionnez l’icône :::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG"::: > stratégies **d’installation** **des applications** >  Teams.

     :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center1.png" alt-text="Administration Microsoft 365 center1":::

  1. Sélectionner **Global (par défaut à l’échelle de l’organisation)**

     :::image type="content" source="../assets/images/teams-toolkit-v2/select-manage-policies.png" alt-text="Sélectionner Gérer les stratégies":::

  1. Définissez le bouton bascule **Charger des applications personnalisées** sur la position **Activé** .

     :::image type="content" source="../assets/images/teams-toolkit-v2/Upload-custom-apps.png" alt-text="Charger des applications personnalisées":::

  5. Sélectionnez **Enregistrer**.

     > [!Note]
     > L’activité du chargement indépendant peut prendre jusqu’à 24 heures. En attendant, vous pouvez utiliser **chargement pour votre client** afin de tester votre application. Pour charger le fichier de package .zip de l’application, consultez [Charger des applications personnalisées](/microsoftteams/teams-app-setup-policies).

     Assurez-vous que vous disposez désormais de l’autorisation de chargement indépendant en suivant les étapes mentionnées dans [vérifier l’autorisation de chargement indépendant à l’aide de Visual Studio Code ou du client Teams.](#sideloading-permission)

</details>

## <a name="see-also"></a>Voir aussi

* [Gérer les stratégies d’application personnalisée et les paramètres dans Teams](/microsoftteams/teams-custom-app-policies-and-settings)
* [Gérer les stratégies de mise en application dans Teams](/microsoftteams/teams-app-setup-policies)
* [Charger des applications personnalisées](/microsoftteams/teams-app-setup-policies)
* [Provisionner des ressources cloud à l’aide du Kit de ressources Teams](provision.md)
* [Déployer l’application Teams dans le cloud](deploy.md)
