---
title: Préparer votre client Microsoft Office 365
description: Comment commencer à travailler avec Teams dans Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Configurer le téléchargement de Microsoft 365 tenant Teams
ms.openlocfilehash: 45d6dfb57fd2faa5bb303aac1dff86be142d0dc2
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019943"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Préparer votre client Microsoft Office 365

Les abonnés Microsoft 365 peuvent développer des applications pour Microsoft Teams avec l'un des plans suivants :

* Basic
* Standard
* Entreprise E1, E3 et E5
* Développeur
* Éducation, Éducation Plus et Éducation E5

> [!NOTE]
> * Pour plus d'informations sur les abonnements Microsoft 365, consultez [les plans.](https://products.office.com/business/compare-more-office-365-for-business-plans)
> * Teams est également disponible pour les clients qui ont souscrit à L'E4 avant son [retrait.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)

## <a name="create-your-development-environment"></a>Créer votre environnement de développement

Si vous n'avez pas de compte Microsoft 365, vous devez vous inscrire à un abonnement au programme pour les développeurs [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program) L'abonnement est gratuit pendant 90 jours et continue à être renouvelé tant que vous l'utilisez pour l'activité de développement. Si vous avez un abonnement Visual Studio Entreprise ou Professionnel, les deux programmes incluent un abonnement microsoft 365 [développeur gratuit.](https://aka.ms/MyVisualStudioBenefits) Il est actif tant que votre abonnement Visual Studio est actif. Pour plus d'informations, [voir configurer un abonnement Microsoft 365 Développeur.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)

## <a name="enable-teams-for-your-organization"></a>Activer Teams pour votre organisation

Activez Teams pour votre organisation et pour plus d'informations, voir [activer Teams pour votre organisation.](/microsoftteams/enable-features-office-365)

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Activer les applications Teams personnalisées et activer le téléchargement d'applications personnalisées

**Pour activer le chargement ou le chargement indépendant de l'application personnalisée pour votre client développeur**

1. Connectez-vous [au Centre d'administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d'identification d'administrateur.

2. Sélectionnez **Afficher toutes les**  >  **équipes.**

    ![Menu Centre d'administration](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > L'apparition de l'option **Teams** peut prendre jusqu'à 24 heures. Vous pouvez [charger votre application personnalisée dans un environnement Teams](/microsoftteams/upload-custom-apps#validate) à des fins de test et de validation à ce moment-là.

3. Accédez aux **stratégies d'installation globales** des applications  >    >  **Teams.**

   ![Activer l'affichage sideload](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Basculez Charger **des applications personnalisées** à la position **Sur.**

5. Sélectionnez **Enregistrer**. Votre client test peut autoriser le chargement de version test d'une application personnalisée.

    > [!Note]
    > Le chargement de version secondaire peut prendre jusqu'à 24 heures. En attendant, vous pouvez utiliser le **chargement pour \<your tenant>** tester votre application. Pour télécharger le fichier de package .zip de l'application, voir [télécharger des applications personnalisées.](/microsoftteams/upload-custom-apps#upload)

    ![Télécharger l'affichage de l'application](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Pour plus d'informations sur l'interaction de ces paramètres, voir gérer les [stratégies](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) et paramètres d'application personnalisés dans Teams et gérer les stratégies de configuration [d'application dans Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"] 
> [Choix d’une configuration de test](~/concepts/build-and-test/debug.md)

