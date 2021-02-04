---
title: Préparer votre client Microsoft Office 365
description: Comment commencer à travailler avec Teams dans Microsoft 365
ms.topic: how-to
keywords: Configurer le téléchargement de Microsoft 365 tenant Teams
ms.openlocfilehash: 50765271b93edd380d1c23672289b618baf1d346
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093942"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Préparer votre client Microsoft Office 365

Si vous êtes abonné à Microsoft 365, vous pouvez développer des applications pour Microsoft Teams avec l’un des [plans suivants](https://products.office.com/business/compare-more-office-365-for-business-plans):

* Basic
* Standard
* Entreprise E1, E3 et E5
* Developer
* Éducation, Éducation Plus et Éducation E5

Microsoft Teams sera également disponible pour les clients qui ont souscrit à L’E4 avant son [retrait.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)

## <a name="just-need-a-development-environment"></a>Vous avez simplement besoin d’un environnement de développement ?

Si vous n’avez pas encore de compte Microsoft 365, vous pouvez vous inscrire à un abonnement au programme pour les développeurs [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program) Il est *gratuit pendant* 90 jours et est continuellement renouvelé tant que vous l’utilisez pour l’activité de développement. Si vous avez un abonnement  Visual Studio *Entreprise* ou Professionnel, les deux programmes incluent un abonnement microsoft 365 [](https://aka.ms/MyVisualStudioBenefits)développeur gratuit, actif pendant toute la durée de vie de Visual Studio abonnement. *Voir* [Configurer un abonnement Microsoft 365 Développeur.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)

## <a name="enable-microsoft-teams-for-your-organization"></a>Activer Microsoft Teams pour votre organisation 

Si Microsoft Teams n’a pas été activé pour votre organisation, vous devez d’abord le faire. Jetez un œil à nos conseils détaillés pour [l’activation de Teams pour votre organisation.](/microsoftteams/enable-features-office-365)

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Activer les applications Teams personnalisées et activer le chargement d’applications personnalisées

Activer le chargement indépendant d’une application personnalisée pour votre client développeur comme suit :

1. Connectez-vous au Centre d’administration [Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur. 

2. Sélectionnez **Afficher toutes les**  -->  **équipes.** 

![image du menu centre d’administration](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> L’apparition de l’option « Teams » peut prendre jusqu’à 24 heures. Pendant l’intervalle, vous pouvez [charger votre application personnalisée dans un](/microsoftteams/upload-custom-apps#validate) environnement Teams à des fins de test et de validation.

3. Accéder aux **stratégies d’installation** des applications Teams à  -->  **l’échelle**  -->  **globale (par défaut à l’échelle de l’organisation)**  

![activer l’affichage sideload](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Basculez le **chargement d’applications personnalisées** à **la** position sur.

5. Sélectionnez **Enregistrer** pour enregistrer les modifications.

Voilà ! Votre client test autorise désormais le chargement de version test de l’application personnalisée.

> [!Note] 
> Le chargement de version latéral peut prendre jusqu’à 24 heures. Pendant l’intervalle, vous pouvez utiliser **le chargement pour \<your tenant>** tester votre application.

![affichage updload de l’application](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Pour plus d’informations sur l’interaction de ces paramètres, voir , Gérer les stratégies et paramètres d’application [personnalisés](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) dans Microsoft Teams et Gérer les stratégies de configuration d’application [dans Microsoft Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)
