---
title: Préparer votre client Microsoft Office 365
description: Dans ce module, découvrez comment bien démarrer avec Teams dans Microsoft 365 et créer votre environnement de développement
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: c5ebc7d36f73978e1cd954c7be8d7ac3595ba68e
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243583"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Préparer votre client Microsoft Office 365

Les abonnés Microsoft 365 peuvent développer des applications pour Microsoft Teams avec l’un des plans suivants :

* De base
* Standard
* Entreprise E1, E3 et E5
* Developer
* Éducation, Éducation Plus et Éducation E5

> [!NOTE]
>
> * Pour plus d’informations sur les abonnements Microsoft 365, consultez [plans](https://products.office.com/business/compare-more-office-365-for-business-plans).
> * Teams est également disponible pour les clients qui se sont abonnés à E4 avant sa [mise hors service](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

## <a name="create-your-development-environment"></a>Créer votre environnement de développement

Si vous n’avez pas de compte Microsoft 365, vous pouvez vous inscrire pour un abonnement au [Programme pour les développeurs Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program). L’abonnement est gratuit pendant 90 jours et continue de se renouveler tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement Visual Studio Enterprise ou Professionnel, les deux programmes incluent un abonnement gratuit Microsoft 365 [développeur](https://aka.ms/MyVisualStudioBenefits). Il est actif tant que votre abonnement Visual Studio est actif. Pour plus d’informations, voir [Configuration d’un abonnement Microsoft 365 Développeur](/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-teams-for-your-organization"></a>Activer Teams pour votre organisation

Activez Teams pour votre organisation et pour plus d’informations, consultez [activation de Teams pour votre organisation](/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Activer les applications Teams personnalisées et activer le chargement d’applications personnalisées

Pour activer le téléchargement d'applications personnalisées ou le chargement indépendant pour votre locataire développeur :

1. Connectez-vous à [Centre d’administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur.

2. Sélectionnez **Afficher tout** > **Teams**.

    ![Menu du Centre d’administration](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > L’affichage de l’option Teams peut prendre **jusqu’à** 24 heures. Vous pouvez [charger votre application personnalisée dans un environnement Teams](/microsoftteams/upload-custom-apps#validate) à des fins de test et de validation à l’heure indiquée.

3. Accédez aux stratégies **d’installation globales** >  des **applications** >  Teams.

   ![Activer la vue chargement indépendant](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Définissez le bouton bascule **Charger des applications personnalisées** sur la position **Activé**.

5. Sélectionnez **Enregistrer**. Votre locataire de test peut autoriser le chargement indépendant d’applications personnalisées.

    > [!Note]
    > L’activation du chargement indépendant peut prendre jusqu’à 24 heures. En attendant, vous pouvez utiliser le **chargement pour \<your tenant>** afin de tester votre application. Pour charger le fichier de package .zip de l’application, consultez [Charger des applications personnalisées](/microsoftteams/upload-custom-apps#upload).

    ![Télécharger la vue d’application](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Pour plus d’informations sur la façon dont ces paramètres interagissent, consultez [gérer les stratégies d’application personnalisées et les paramètres dans Teams](/microsoftteams/teams-custom-app-policies-and-settings) et [gérer les stratégies de configuration des applications dans Teams](/microsoftteams/teams-app-setup-policies).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Choix d’une configuration de test](~/concepts/build-and-test/debug.md)

## <a name="see-also"></a>Voir aussi

* [Ajouter des données de test à votre locataire de test Microsoft 365](~/concepts/build-and-test/test-data.md)
* [Microsoft 365 Multi-Geo](/microsoft-365/enterprise/microsoft-365-multi-geo?view=o365-worldwide&preserve-view=true)
