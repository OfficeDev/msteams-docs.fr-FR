---
title: Préparer votre client Microsoft Office 365
description: Comment commencer à prendre en Teams dans Microsoft 365
ms.topic: how-to
ms.localizationpriority: medium
keywords: Configurer le Microsoft 365 de Teams client
ms.openlocfilehash: 2b7da66460df12efd1e3c5bd45a9dfa6572e4b4c
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888152"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Préparer votre client Microsoft Office 365

Microsoft 365 abonnés peuvent développer des applications pour Microsoft Teams avec l’un des plans suivants :

* De base
* Standard
* Enterprise E1, E3 et E5
* Développeur
* Éducation, Éducation Plus et Éducation E5

> [!NOTE]
> * Pour plus d’informations sur Microsoft 365 abonnements, consultez [les plans.](https://products.office.com/business/compare-more-office-365-for-business-plans)
> * Teams est également disponible pour les clients qui ont souscrit à L’E4 avant son [retrait.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)

## <a name="create-your-development-environment"></a>Créer votre environnement de développement

Si vous n’avez pas de compte Microsoft 365, vous devez vous inscrire à un abonnement [Microsoft 365 programme pour les développeurs.](https://developer.microsoft.com/microsoft-365/dev-program) L’abonnement est gratuit pendant 90 jours et continue à être renouvelé tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement Visual Studio Enterprise ou Professional, les deux programmes incluent un abonnement Microsoft 365 [développeur gratuit.](https://aka.ms/MyVisualStudioBenefits) Il est actif tant que votre abonnement Visual Studio est actif. Pour plus d’informations, [voir configurer un abonnement Microsoft 365 développeur.](/office/developer-program/office-365-developer-program-get-started)

## <a name="enable-teams-for-your-organization"></a>Activer Teams pour votre organisation

Activez Teams pour votre organisation et pour plus d’informations, consultez [l’Teams pour votre organisation.](/microsoftteams/enable-features-office-365)

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Activer les applications Teams personnalisées et activer le téléchargement d’applications personnalisées

**Pour activer le chargement ou le chargement indépendant de l’application personnalisée pour votre client développeur**

1. Connectez-vous [Centre d'administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur.

2. Sélectionnez **Afficher**  >  **tous les Teams**.

    ![Menu Centre d’administration](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > L’option d’Teams peut prendre  jusqu’à 24 heures. Vous pouvez [charger votre application personnalisée dans un environnement Teams pour](/microsoftteams/upload-custom-apps#validate) les tests et la validation à ce moment-là.

3. Accédez à **Teams des stratégies**  >  **d’installation d’applications**  >  **globales.**

   ![Activer l’affichage sideload](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Basculez Télécharger **applications personnalisées** à la position **Sur.**

5. Sélectionnez **Enregistrer**. Votre client test peut autoriser le chargement de version test d’une application personnalisée.

    > [!Note]
    > Le chargement de version secondaire peut prendre jusqu’à 24 heures pour être actif. En attendant, vous pouvez utiliser le **chargement pour \<your tenant>** tester votre application. Pour télécharger le fichier .zip package de l’application, voir [télécharger des applications personnalisées.](/microsoftteams/upload-custom-apps#upload)

    ![Télécharger’application](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Pour plus d’informations sur l’interaction de ces paramètres, voir gérer les stratégies et paramètres d’application [personnalisés](/microsoftteams/teams-custom-app-policies-and-settings) dans Teams et gérer les stratégies de configuration d’application [dans Teams](/microsoftteams/teams-app-setup-policies).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"] 
> [Choix d’une configuration de test](~/concepts/build-and-test/debug.md)

## <a name="see-also"></a>Voir aussi

[Ajouter des données de test à votre client Microsoft 365 test](~/concepts/build-and-test/test-data.md)
