---
title: Préparer votre environnement de développement de teams
description: Comment configurer votre environnement pour développer des applications teams teams
keywords: Configurer teams Office 365 client Development Development Environment
ms.openlocfilehash: 701c6c110026007cf1670e783348bbdbe1aff498
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651957"
---
# <a name="prepare-your-development-environment"></a>Préparer votre environnement de développement :

Si vous êtes un abonné Office 365, vous pouvez développer des applications pour Microsoft teams à l’aide de l’un des [plans](https://products.office.com/business/compare-more-office-365-for-business-plans)suivants :

* Business Essentials
* Business Premium
* Entreprise E1, E3 et E5
* Développeur
* Éducation, éducation plus et éducation E5

Microsoft teams sera également disponible pour les clients abonnés à E4 avant sa [retraite](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

## <a name="just-need-a-development-environment"></a>Vous avez besoin d’un environnement de développement ?

Si vous ne disposez pas d’un compte Office 365, vous pouvez vous inscrire pour obtenir un abonnement au [programme de développement Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program) . Elle est *gratuite* pendant 90 jours et se renouvelle en permanence tant que vous l’utiliserez pour l’activité de développement. Si vous disposez d’un abonnement Visual Studio *entreprise* ou *professionnel* , les deux programmes incluent un [abonnement de développeur](https://aka.ms/MyVisualStudioBenefits)gratuit Microsoft 365, actif pendant la durée de vie de votre abonnement Visual Studio. *Consultez la rubrique* [configurer un abonnement développeur Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-microsoft-teams-for-your-organization"></a>Activer Microsoft teams pour votre organisation

Si Microsoft teams n’a pas été activé pour votre organisation, vous devez tout d’abord le faire. Consultez nos conseils détaillés pour [l’activation de teams pour votre organisation](https://docs.microsoft.com/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Activer les applications de teams personnalisées et activer le téléchargement de l’application personnalisée

Activez l’application personnalisée chargement pour votre client développeur comme suit :

1. Connectez-vous au [Centre d’administration Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) avec vos informations d’identification d’administrateur. 

2. Sélectionnez **afficher toutes les**  -->  **équipes**. 

![image du menu de dépassement de l’application](~/assets/images/prepare-test-tenant/admin-center.png)

3. Accéder aux stratégies d’installation des **applications teams**  -->  **Setup Policies**  -->  **global (par défaut** à l’échelle de l’organisation)  

![image du menu de dépassement de l’application](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Basculez **charger les applications personnalisées** vers la position **en** place.

Voilà ! Votre client de test autorisera maintenant l’application personnalisée chargement.

> [!Note] 
> L’activation de la chargement peut prendre jusqu’à 24 heures. Pendant un intervalle de temps, vous pouvez utiliser le **chargement pour \<your tenant> ** tester votre application.

![image du menu de dépassement de l’application](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Pour plus d’informations sur la façon dont ces paramètres interagissent, *voir* [gérer les stratégies et les paramètres d’application personnalisés dans Microsoft teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) et [gérer les stratégies de configuration d’application dans Microsoft teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).