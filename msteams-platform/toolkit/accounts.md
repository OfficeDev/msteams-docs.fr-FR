---
title: Préparer les comptes à créer des applications Teams client
author: zyxiaoyuer
description: Préparer les comptes à créer des applications Teams client
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 302cac17ae6905899e43a8768882f61f0a2b9056
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518323"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>Préparer les comptes à créer des applications Teams client

Pour développer Teams’application, vous avez besoin d’au moins un compte Microsoft 365 avec un abonnement valide. Si vous souhaitez héberger vos ressources back-end sur Azure, vous avez besoin d’un compte Azure. Le compte Azure est facultatif si votre application existante est hébergée sur un autre fournisseur cloud et que vous souhaitez intégrer l’application existante à Teams plateforme.

## <a name="microsoft-365-account"></a>Microsoft 365 compte

Si vous n’avez pas de compte Microsoft 365 existant avec un abonnement valide, vous pouvez en créer un en rejoignant le programme Microsoft 365 [développeur](https://developer.microsoft.com/microsoft-365/dev-program). Le programme Microsoft 365 développeur inclut un abonnement Microsoft 365 E5 développeur que vous pouvez utiliser pour créer votre propre bac à sable et développer des solutions indépendantes de votre environnement de production.

## <a name="azure-account"></a>Compte Azure

Si vous souhaitez héberger des ressources liées à votre application ou accéder à des ressources dans Azure, vous devez avoir un abonnement Azure. Vous pouvez [créer un compte gratuit avant](https://azure.microsoft.com/free/) de commencer.

## <a name="join-microsoft-365-developer-program"></a>Rejoindre Microsoft 365 programme pour les développeurs 

Si vous n’avez pas de compte Microsoft 365, vous devez vous inscrire à un abonnement au programme Microsoft 365 [développeur](https://developer.microsoft.com/microsoft-365/dev-program). L’abonnement est gratuit pendant 90 jours et continue à être renouvelé tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement Visual Studio Enterprise ou Professional, les deux programmes incluent un abonnement Microsoft 365 [développeur gratuit](https://aka.ms/MyVisualStudioBenefits). Il est actif tant que votre abonnement Visual Studio est actif. Pour plus d’informations, [voir configurer un abonnement Microsoft 365 développeur.](https://developer.microsoft.com/microsoft-365/dev-program)

1. Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).
2. **Sélectionnez Rejoindre maintenant**.
3. **Sélectionnez Configurer l’abonnement E5**.
4. Configurer votre compte d’administrateur. Une fois que vous avez terminé, vous devez voir l’écran suivant :

:::image type="content" source="./images/m365-developer-program.png" alt-text="Diagramme  shows Microsoft 365 program":::

## <a name="accounts-for-microsoft-365-developer-program"></a>Comptes pour le programme Microsoft 365 développeur

Vous pouvez vous inscrire au programme pour les développeurs à l’aide d’un des types de comptes suivants :

- **Compte Microsoft pour une utilisation personnelle** 

  Permet d’accéder à tous les produits et services cloud Microsoft orientés consommateurs, tels que Outlook, Messenger, OneDrive, MSN, Xbox Live ou Microsoft 365. Toute inscription à une boîte aux lettres Outlook.com crée automatiquement un compte Microsoft. Une fois le compte Microsoft créé, celui-ci peut être utilisé pour accéder aux services de cloud computing Microsoft liés aux consommateurs ou à Azure.

- **Compte de travail pour les entreprises**

  Permet d’accéder à tous les services cloud Microsoft de niveau petite, moyenne et entreprise, tels qu’Azure, Microsoft Intune ou Microsoft 365. Lorsque vous vous inscrivez à l’un de ces services en tant qu’organisation, un annuaire informatique est automatiquement mis en service dans Microsoft Azure Active Directory (Azure AD) pour représenter votre organisation.

- **Visual Studio ID**

  Vous pouvez créer des abonnements Visual Studio Professional ou Enterprise . Nous vous recommandons d’utiliser cette option pour rejoindre le programme développeur à partir de la galerie Visual Studio pour bénéficier de tous les avantages en tant qu’abonné Visual Studio.

## <a name="teams-customer-app-upload-or-sideload-permission"></a>Teams’autorisation de chargement ou de chargement de version de version de chargement d’une application client

> [!IMPORTANT]
> Pendant le développement, vous devez charger votre application dans votre Teams sans la distribuer. C’est ce que **l’on appelle le chargement de version de version de chargement.**

La liste suivante fournit des étapes pour vérifier si l’autorisation de chargement de version de version de l’application est activée. Les deux méthodes sont les suivantes :

* **Pour utiliser du code Microsoft Visual studio**

    1. **Ouvrez Visual Studio Code**.
    1. Sélectionnez **Teams Shared Computer Toolkit** dans le panneau gauche.
    1. **Sélectionnez Comptes et** connectez-vous à votre compte Microsoft 365 client.
    1. Vérifiez si vous pouvez voir l’option **Chargement de version side activée** , comme illustré dans l’image :

       :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="Activer le chargement de version de version":::

* **Pour utiliser Teams compte**

    1. Ouvrez **Microsoft Teams**.
    2. Sélectionnez **Applications dans** la barre de gauche.
    3. **Sélectionnez Publier une application**.

       :::image type="content" source="../assets/images/teams-toolkit-v2/publish.png" alt-text="Publier une application":::

    4. Vérifiez si vous pouvez voir l’option **Télécharger une application personnalisée** comme illustré dans l’image :

       :::image type="content" source="../assets/images/teams-toolkit-v2/upload.png" alt-text="Télécharger une application personnalisée":::

Si vous ne pouvez pas voir **Télécharger’une** option d’application personnalisée, cela indique que vous n’êtes pas autorisé à recharger une version de version de chargement de version. Sans autorisation de chargement de version d’équipe, vous ne pourrez pas faire de débogage local ou distant. Il est donc très important d’obtenir l’autorisation de chargement de version de version de votre compte avant d’en faire le débogage pour Teams application. Si vous êtes administrateur de votre client, vous pouvez ouvrir le paramètre de chargement de version secondaire pour votre client ou organisation. Si vous n’êtes pas un administrateur, contactez votre administrateur client pour obtenir l’autorisation.

## <a name="enable-custom-app-uploading-for-your-organization"></a>Activer le chargement d’applications personnalisées pour votre organisation

> [!IMPORTANT]
> Pour activer le chargement ou le chargement indépendant de l’application personnalisée pour votre client développeur, vous devez être l’administrateur de votre client.

1. Connectez-vous [Centre d'administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur.

2. **Sélectionnez Afficher** >  **tout Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/5.png" alt-text="afficher tout":::

> [!NOTE]
> L’option d’Teams peut prendre jusqu’à  **24** heures. Vous pouvez [charger votre application personnalisée dans un environnement Teams de](/microsoftteams/upload-custom-apps) test et de validation à ce moment-là.

3. Accédez à **Teams appsSetup** >  **PoliciesGlobal** > .

   :::image type="content" source="../assets/images/teams-toolkit-v2/3.png" alt-text="set bolies":::

4. Basculez Télécharger applications personnalisées à **la position Sur**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/4.png" alt-text="bascule":::

5. Sélectionnez **Enregistrer**. 

> [!Note]
> Le chargement de version secondaire peut prendre jusqu’à 24 heures pour être actif. En attendant, vous pouvez utiliser le **chargement pour votre client** pour tester votre application. Pour télécharger le fichier .zip package de l’application, voir [télécharger des applications personnalisées](/microsoftteams/teams-app-setup-policies).

Pour plus d’informations, voir [gérer les stratégies et paramètres](/microsoftteams/teams-custom-app-policies-and-settings) d’application personnalisés dans Teams et gérer les stratégies de configuration [d’application dans Teams](/microsoftteams/teams-app-setup-policies).

## <a name="see-also"></a>Voir aussi

* [Créer un projet Teams projet](create-new-project.md)
* [Provisionner des ressources cloud](provision.md)
