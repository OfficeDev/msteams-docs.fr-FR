---
title: Préparer votre client Office 365
description: Prise en main de teams dans Office 365
keywords: Configurer le chargement des équipes client Office 365
ms.openlocfilehash: 35f102223a5f8e6a8e12268e22aedca07a61b1fa
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120268"
---
# <a name="prepare-your-office-365-tenant"></a>Préparer votre client Office 365

Si vous êtes un abonné Office 365, vous pouvez développer des applications pour Microsoft teams à l’aide de l’un des [plans](https://products.office.com/business/compare-more-office-365-for-business-plans)suivants :

* Business Essentials
* Business Premium
* Entreprise E1, E3 et E5
* Développeur
* Éducation, éducation plus et éducation E5

Microsoft teams sera également disponible pour les clients abonnés à E4 avant sa [retraite](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

## <a name="just-need-a-development-environment"></a>Vous avez besoin d’un environnement de développement ?

Si vous ne disposez pas d’un compte Office 365, vous pouvez vous inscrire pour obtenir un abonnement [office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) . Elle est *gratuite* pendant 90 jours et se renouvelle en permanence tant que vous l’utiliserez pour l’activité de développement. Si vous disposez d’un abonnement Visual Studio *entreprise* ou *professionnel* , les deux programmes incluent un abonnement Office 365 [développeur](https://aka.ms/MyVisualStudioBenefits)gratuit, actif pendant toute la durée de votre abonnement Visual Studio. *Consultez la rubrique* [configurer un abonnement développeur Microsoft 365](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-microsoft-teams-for-your-organization"></a>Activer Microsoft teams pour votre organisation

Si Microsoft teams n’a pas été activé pour votre organisation, vous devez tout d’abord le faire. Consultez nos conseils détaillés pour [l’activation de teams pour votre organisation](https://docs.microsoft.com/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Activer les applications de teams personnalisées et activer le téléchargement de l’application personnalisée

> [!Note] 
> Si vous utilisez la plateforme de développement Office 365 pour créer votre application, ces paramètres doivent déjà être configurés pour vous permettre de créer, de télécharger et de tester votre application.

Trois paramètres sont pertinents pour activer les applications personnalisées et le téléchargement d’applications personnalisées :

* **Paramètre** =>  => **de** l’application personnalisée à l’échelle de l’organisation autoriser une**interaction avec des applications personnalisées**: ce paramètre active ou désactive les applications personnalisées pour votre organisation. Il doit être activé. 
* **Paramètre** => de l’application personnalisée d’équipe => **autoriser les membres à télécharger des applications personnalisées****activées ou désactivées** : ce paramètre s’applique à chaque équipe individuelle dans Microsoft Teams. Si vous souhaitez installer votre application pour une équipe spécifique, celle-ci doit être activée pour cette équipe.
* **La stratégie** => d’application personnalisée utilisateur**peut télécharger des applications** => personnalisées**activées ou désactivées** : ce paramètre contrôle les autorisations d’un utilisateur individuel. Vous devrez activer ceci pour les personnes qui sont autorisées à télécharger des applications personnalisées.

Pour plus d’informations sur la façon dont ces paramètres interagissent, *voir* [gérer les stratégies et les paramètres d’application personnalisée dans Microsoft teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) et [gérer les stratégies de configuration d’application dans Microsoft teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).
