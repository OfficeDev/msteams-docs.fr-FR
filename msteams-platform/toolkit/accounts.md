---
title: Préparer les comptes à créer des applications Teams client
author: zyxiaoyuer
description: Préparer les comptes à créer des applications Teams client
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 6a215922ff4b89c4afdce187be9b03479e6a54e6
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227967"
---
# <a name="prepare-accounts-to-build-teams-apps"></a>Préparer les comptes à créer des applications Teams client

Pour développer une application Teams, au moins un compte Microsoft 365 avec un abonnement valide est nécessaire. Si vous souhaitez héberger vos ressources back-end sur Azure, un compte Azure est également nécessaire. Le compte Azure est facultatif si votre application existante est hébergée sur un autre fournisseur cloud et que vous souhaitez intégrer l’application existante à Teams plateforme.

## <a name="microsoft-365-account"></a>Microsoft 365 client

Si vous n’avez pas de compte Microsoft 365 existant avec un abonnement valide, vous pouvez en créer un en rejoignant le programme Microsoft 365 [développeur.](https://developer.microsoft.com/microsoft-365/dev-program) Le programme pour les développeurs Microsoft 365 inclut un abonnement pour les développeurs Microsoft 365 E5 qui vous permet de créer votre propre bac à sable, puis de développer des solutions indépendantes de votre environnement de production.

## <a name="azure-account"></a>Compte Azure

Si vous souhaitez héberger des ressources liées à votre application ou accéder à des ressources dans **Azure,** vous devez avoir un abonnement Azure. Vous pouvez [créer un compte gratuit avant](https://azure.microsoft.com/free/) de commencer.

## <a name="join-microsoft-365-developer-program"></a>Rejoindre le Microsoft 365 développeur 

Si vous n’avez pas de compte Microsoft 365, vous devez vous inscrire à un abonnement au programme Microsoft 365 [développeur.](https://developer.microsoft.com/microsoft-365/dev-program) L’abonnement est gratuit pendant 90 jours et continue à être renouvelé tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement Visual Studio Enterprise ou Professional, les deux programmes incluent un abonnement Microsoft 365 [développeur gratuit.](https://aka.ms/MyVisualStudioBenefits) Il est actif tant que votre abonnement Visual Studio est actif. Pour plus d’informations, [voir configurer un abonnement Microsoft 365 développeur.](https://developer.microsoft.com/microsoft-365/dev-program)

1. Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).
2. Sélectionnez **Rejoindre maintenant** et suivez les instructions à l’écran.
3. Dans l’écran d’accueil, **sélectionnez Configurer l’abonnement E5.**
4. Configurer votre compte d’administrateur. Une fois que vous avez terminé, vous devez voir l’écran suivant :

:::image type="content" source="./images/m365-developer-program.png" alt-text="Diagramme shows microsoft m365 program":::

## <a name="accounts-for-microsoft-365-developer-program"></a>Comptes pour le programme Microsoft 365 développeur

Vous pouvez vous inscrire au programme pour les développeurs à l’aide d’un des types de comptes suivants :

- **Compte Microsoft** 

Vous pouvez créer pour un usage personnel : permet d’accéder à tous les produits et services cloud Microsoft orientés grand public, tels que Outlook, Messenger, OneDrive, MSN, Xbox Live ou Microsoft 365. Toute inscription à une boîte aux lettres Outlook.com crée automatiquement un compte Microsoft. Une fois le compte Microsoft créé, celui-ci peut être utilisé pour accéder aux services de cloud computing Microsoft liés aux consommateurs ou à Azure.

- **Compte de travail**

 L’administrateur peut émettre un problème pour une utilisation professionnelle : permet d’accéder à tous les services cloud Microsoft de petite, moyenne et entreprise, tels qu’Azure, Microsoft Intune ou Microsoft 365. Lorsque vous vous inscrivez à l’un de ces services en tant qu’organisation, un répertoire informatique est automatiquement configuré dans Azure Active Directory pour représenter votre organisation.

- **Visual Studio ID**

Vous pouvez créer des abonnements Visual Studio Professional ou Enterprise . Nous vous recommandons d’utiliser cette option pour rejoindre le programme développeur à partir de la galerie Visual Studio pour bénéficier de tous les avantages en tant qu’abonné Visual Studio.

## <a name="teams-customer-app-uploading-sideloading-permission-check"></a>Teams téléchargement d’application client (autorisation de chargement de version de version)

> [!IMPORTANT]
> Pendant le développement, vous devez charger votre application dans votre Teams sans la distribuer. C’est ce que **l’on appelle le chargement de version de version de chargement de version.**

L’une des façons de vérifier si vous avez un compte Teams, vérifiez si vous pouvez télécharger une version de version de chargement de version Teams :

1. Dans le Teams client, sélectionnez **Applications dans** la barre de gauche.
2. Sélectionnez **Gérer vos applications.**
3. Vérifiez si vous pouvez voir l’option **Télécharger une application personnalisée** comme illustré dans l’image :

:::image type="content" source="./images/sideload-check.png" alt-text="Diagramme shows to upload a custom app":::

Si vous ne pouvez **pas Télécharger’une** option d’application personnalisée, cela indique que vous n’avez pas d’autorisation de chargement de version. Sans autorisation de chargement de version d’équipe, vous ne pourrez pas faire de débogage local/distant. Il est donc très important d’obtenir l’autorisation de chargement de version de version de votre compte avant d’en faire le débogage pour Teams application. Si vous êtes administrateur de votre client, vous pouvez ouvrir le paramètre de chargement de version de version pour votre client/organisation, tandis que si vous n’êtes pas administrateur, contactez votre administrateur client pour obtenir l’autorisation.

## <a name="enable-custom-app-uploading-sideloading--for-your-organization"></a>Activer le chargement d’applications personnalisées (chargement de version secondaire) pour votre organisation

> [!IMPORTANT]
> Pour activer le chargement ou le chargement indépendant de l’application personnalisée pour votre client développeur, vous devez être l’administrateur de votre client.

1. Connectez-vous [Centre d'administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur.

2. Sélectionnez **Afficher**  >  **tous les Teams**.

:::image type="content" source="./images/admin-center-teams.png" alt-text="Diagramme shows Teams admin center":::

> [!NOTE]
> L’option d’Teams peut prendre  jusqu’à **24** heures. Vous pouvez [charger votre application personnalisée dans un environnement Teams pour](/microsoftteams/upload-custom-apps) les tests et la validation à ce moment-là.

3. Accédez à **Teams des stratégies**  >  **d’installation d’applications**  >  **globales.**

:::image type="content" source="./images/teams-setup-policy.png" alt-text="Diagramme shows setup policy for Teams":::

4. Basculez Télécharger applications personnalisées à la position **Sur.**

:::image type="content" source="./images/turn-on-sideload.png" alt-text="Diagramme shows to turn on sideload":::

5. Sélectionnez **Enregistrer**. Votre client test peut autoriser le chargement de version test d’une application personnalisée.

:::image type="content" source="./images/save-sideload.png" alt-text="Diagramme shows save option":::

> [!Note]
> Le chargement de version secondaire peut prendre jusqu’à 24 heures pour être actif. En attendant, vous pouvez utiliser [charger pour **votre client]** pour tester votre application. Pour télécharger le fichier .zip package de l’application, voir [télécharger des applications personnalisées.](/microsoftteams/teams-app-setup-policies)

Pour plus d’informations, voir [gérer les stratégies](/microsoftteams/teams-custom-app-policies-and-settings) et paramètres d’application personnalisés dans Teams et gérer les stratégies de configuration d’application dans [Teams](/microsoftteams/teams-app-setup-policies).

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Créer un projet Teams projet](create-new-project.md)

> [!div class="nextstepaction"]
> [Mise en service des ressources cloud](provision.md)
