---
title: Préparer votre client Office 365
description: Prise en main de teams dans Office 365
keywords: Configurer le chargement des équipes client Office 365
ms.openlocfilehash: 62cd640196631f50c72762253ff1bd75a143337d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673902"
---
# <a name="prepare-your-office-365-tenant"></a>Préparer votre client Office 365

Pour développer des applications pour Microsoft Teams, vous devez être un [client Office 365 avec l’un des plans suivants](https://products.office.com/business/compare-more-office-365-for-business-plans).

* Business Essentials
* Business Premium
* Entreprise E1, E3 et E5
* Développeur
* Éducation, éducation plus et éducation E5

Microsoft teams est également disponible pour les clients qui ont acheté E4 avant sa retraite.

## <a name="just-need-a-development-environment"></a>Vous avez besoin d’un environnement de développement ?

Si vous ne disposez pas d’un compte Office 365, vous pouvez vous inscrire au [programme pour les développeurs office 365](https://dev.office.com/devprogram) pour obtenir un service *gratuit* 90 jours (vous pouvez le renouveler aussi longtemps que vous l’utilisez pour une activité de développement) client Office 365 développeur. Ce compte peut uniquement être utilisé à des fins de test. Pour plus d’informations sur [la configuration de vos comptes de test](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US).

## <a name="enable-microsoft-teams-for-your-organization"></a>Activer Microsoft teams pour votre organisation

Si Microsoft teams n’est pas encore activé pour votre organisation, vous devez tout d’abord le faire. Consultez nos conseils détaillés pour [l’activation de teams pour votre organisation](/microsoftteams/how-to-roll-out-teams).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Activer les applications de teams personnalisées et activer le téléchargement de l’application personnalisée

> Remarque : Si vous utilisez une organisation de développement O365 pour créer votre application, ces paramètres doivent déjà être configurés pour vous permettre de créer, de charger et de tester votre application.

Il y a trois paramètres impliqués dans l’activation des applications personnalisées et le téléchargement d’applications personnalisées :

* **Paramètre de l’application personnalisée** à l’échelle de l’Organisation : ce paramètre active ou désactive les applications personnalisées pour votre organisation. Il doit être activé. 
* **Paramètre de l’application personnalisée d’équipe** : ce paramètre est pour chaque équipe individuelle dans Microsoft Teams. Si vous souhaitez installer votre application pour une équipe spécifique, celle-ci doit être activée pour cette équipe.
* **Stratégie d’application personnalisée** par l’utilisateur : cet ensemble de paramètres contrôle les autorisations d’un utilisateur individuel. Vous devez activer cette activation pour les utilisateurs qui souhaitent télécharger des applications personnalisées.

Pour plus d’informations sur le mode d’interaction de ces paramètres, consultez la rubrique [Manage Custom App Policies and Settings in Microsoft teams](/MicrosoftTeams/teams-custom-app-policies-and-settings).
