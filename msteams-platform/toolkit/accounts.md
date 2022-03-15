---
title: Préparer des comptes pour créer des applications Teams
author: zyxiaoyuer
description: Préparer des comptes pour créer des applications Teams
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 21de5611daacbc00630cd7fa4b2aa3704788ed5e
ms.sourcegitcommit: ca902f505a125641c379a917ee745ab418bd1ce6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2022
ms.locfileid: "63464299"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>Préparer des comptes pour créer des applications Teams

Pour créer une application Teams et la charger, vous devez préparer les comptes suivants :

* [Compte Microsoft 365 avec un abonnement valide.](accounts.md#microsoft-365-account)
* [Compte Azure pour héberger les ressources principales sur Azure](accounts.md#azure-account-to-host-backend-resources).

## <a name="microsoft-365-account"></a>Compte Microsoft 365

Pour créer un compte Microsoft 365, inscrivez-vous à un abonnement au programme Microsoft 365 développeur. L’abonnement est gratuit pendant 90 jours et continue de se renouveler tant que vous l’utilisez pour l’activité de développement.

Si vous avez un abonnement Visual Studio Enterprise ou Professionnel, les deux programmes incluent un abonnement gratuit Microsoft 365 [développeur](https://aka.ms/MyVisualStudioBenefits). Il est actif tant que votre abonnement Visual Studio est actif. Pour plus d’informations, consultez l’[abonnement développeur Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).

### <a name="microsoft-365-developer-program"></a>Programme de développement Microsoft 365

Pour obtenir un compte de développeur Teams gratuit, rejoignez le programme Microsoft 365 développeurs et effectuez les étapes suivantes :

1. Accédez au[Programme pour les développeurs Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
2. Sélectionnez **Rejoindre maintenant**.
3. Sélectionnez **Configurer l’abonnement E5**.
4. Configurez votre compte d’administrateur.

   L’image suivante s’affiche une fois l’abonnement terminé :

    :::image type="content" source="./images/m365-developer-program.png" alt-text="Diagramme qui montre le programme Microsoft 365":::

### <a name="microsoft-365-developer-account-types"></a>Types de comptes de développeur Microsoft 365

Vous pouvez vous inscrire au programme pour les développeurs à l’aide d’un des types de comptes suivants :

- **Compte Microsoft pour un usage personnel**

    Le compte Microsoft vous permet d’accéder aux produits et services cloud Microsoft, tels qu’Outlook, Messenger, OneDrive, MSN, Xbox Live ou Microsoft 365. Vous pouvez vous inscrire à une boîte aux lettres Outlook.com pour créer un compte Microsoft, qui peut être utilisé pour accéder aux services cloud Microsoft ou Azure liés aux consommateurs.

- **Compte professionnel Microsoft pour les entreprises**

     Ce compte permet d’accéder à tous les services cloud Microsoft de petite, moyenne et moyenne entreprise, tels qu’Azure, Microsoft Intune ou Microsoft 365. Lorsque vous vous inscrivez à l’un de ces services en tant qu’organisation, un annuaire cloud est automatiquement approvisionné dans Microsoft Azure Active Directory (Azure AD) pour représenter votre organisation.

- **ID d’utilisateur Visual Studio**

    L’ID d’utilisateur créé pour utiliser Visual Studio Professional ou l’abonnement Entreprise peut être utilisé pour rejoindre le programme de développement au sein de la galerie Visual Studio afin de bénéficier de tous les avantages en tant qu’abonné Visual Studio.

## <a name="azure-account-to-host-backend-resources"></a>Compte Azure pour héberger des ressources principales

Le compte Azure est facultatif si votre application existante est hébergée sur un autre fournisseur de cloud et que vous souhaitez intégrer l’application existante sur la plateforme Teams.

**ID Visual Studio**

Si vous souhaitez héberger les ressources associées à votre application ou accéder aux ressources dans Azure, vous pouvez [créer un compte gratuit](https://azure.microsoft.com/free/) avant de commencer. Vous pouvez également choisir d’héberger vos ressources back-end à l’aide d’un autre fournisseur de cloud ou sur vos propres serveurs s’ils sont disponibles à partir du domaine public.

## <a name="teams-custom-app-upload-or-sideload-permission"></a>Autorisation de chargement ou de chargement de version test d’une application personnalisée Teams

> [!IMPORTANT]
> Après avoir créé l’application, vous devez charger votre application dans Teams sans la distribuer. Ce processus est appelé **chargement indépendant**.

   Vous pouvez vérifier si l’autorisation de chargement indépendant est activée à l’aide de Visual Studio Code ou du client Teams.

* **Vérifier l’autorisation de chargement indépendant à l’aide de Visual Studio Code**

    1. Ouvrez **Visual Studio Code**.
    1. Sélectionnez **Kit de ressources Teams** dans le volet gauche. Si vous ne parvenez pas à voir l’option, vérifiez que vous avez installé l’extension du Kit de ressources Teams.
    1. Sélectionnez **Comptes** et connectez-vous à votre compte Microsoft 365.
    1. Vérifiez si vous pouvez afficher l’option **Chargement indépendant activé** comme illustré dans l’image suivante :

       :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="Activer le chargement indépendant" border="true":::

* **Vérifier l’autorisation de chargement indépendant à l’aide du client Teams**

    1. Ouvrez **Microsoft Teams**.
    2. Sélectionnez **Applications** dans le panneau gauche.
    3. Sélectionnez **Publier une application**.

       :::image type="content" source="../assets/images/teams-toolkit-v2/publish.png" alt-text="Publier une application" border="true":::

    4. Vérifiez si vous pouvez voir l’option **Charger une application personnalisée** comme illustré dans l’image suivante :

       :::image type="content" source="../assets/images/teams-toolkit-v2/upload.png" alt-text="Charger une application personnalisée" border="true":::

        Si vous ne parvenez pas à afficher l’option **Charger une application personnalisée**, cela indique que vous n’avez pas l’autorisation requise pour le chargement indépendant.
        * Pour un administrateur de locataire, activez le paramètre de chargement indépendant pour votre locataire ou organisation dans le Centre d’administration Teams.
        * Si vous n’êtes pas un administrateur de locataire, vous devez contacter votre administrateur de locataire pour activer le chargement indépendant.

### <a name="upload-your-custom-app"></a>Téléchargez votre application personnalisée

> [!IMPORTANT]
> Pour activer le téléchargement d'applications personnalisées ou le sideloading pour votre locataire développeur, vous devez être l'administrateur de votre locataire.

**Pour charger l’application personnalisée**

1. Connectez-vous à [Centre d’administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur.

2. Sélectionnez **Afficher tout** > **Teams**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/5.png" alt-text="afficher tout" border="true":::

   > [!Note]
   > L’affichage de l’option **Teams** peut prendre **jusqu’à** 24 heures. Vous pouvez [charger votre application personnalisée dans un environnement Teams](/microsoftteams/upload-custom-apps) à des fins de test et de validation.

3. Accédez à **Applications Teams** > **Stratégies d’installation**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/3.png" alt-text="définir des stratégies":::

4. Définissez le bouton bascule **Charger des applications personnalisées** sur la position **Activé** .

   :::image type="content" source="../assets/images/teams-toolkit-v2/4.png" alt-text="Bouton bascule":::

5. Sélectionnez **Enregistrer**.

   > [!Note]
   > L’activité du chargement indépendant peut prendre jusqu’à 24 heures. En attendant, vous pouvez utiliser **chargement pour votre client** afin de tester votre application. Pour charger le fichier de package .zip de l’application, consultez [Charger des applications personnalisées](/microsoftteams/teams-app-setup-policies).

Pour plus d’informations, consultez [Gérer les paramètres et les stratégies d’application personnalisés dans Teams](/microsoftteams/teams-custom-app-policies-and-settings) et [Gérer les stratégies de configuration des applications dans Teams](/microsoftteams/teams-app-setup-policies).

## <a name="see-also"></a>Voir aussi

* [Créer une application Teams à l’aide du kit de ressources Teams](create-new-project.md)
* [Provisionner des ressources cloud](provision.md)
* [Déployer l’application Teams dans le cloud](deploy.md)
* [Publier votre application Teams](TeamsFx-collaboration.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)