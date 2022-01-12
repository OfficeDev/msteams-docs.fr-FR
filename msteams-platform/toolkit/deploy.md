---
title: Déployer dans le cloud
author: MuyangAmigo
description: Déployer dans le cloud
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 0eeda4842ad3f0443d46b5075b1520b0042130ec
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768377"
---
# <a name="deploy-to-the-cloud"></a>Déployer dans le cloud

Teams Shared Computer Toolkit vous permet de déployer ou de télécharger le code frontal et le code frontal dans votre application vers vos ressources cloud mises en service dans Azure.

* L’onglet, tel que les applications frontales, est déployé sur le stockage Azure et configuré pour l’hébergement web statique ou un site sharepoint.
* Les API principale sont déployées sur les fonctions Azure.
* Le bot ou l’extension de messagerie est déployé sur le service d’application Azure.

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!NOTE]
> * Assurez-vous que Teams projet d’application est ouvert dans du code VS.
> * Avant de déployer le code de projet sur le cloud, [provisionnez les ressources cloud.](provision.md)

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Déployer des Teams à l’aide Teams Shared Computer Toolkit

Les guides de mise en place vous aident à déployer à l’aide Teams Shared Computer Toolkit. Vous pouvez utiliser les applications suivantes pour déployer votre Teams suivante :
* [Déployer votre application sur Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Déployer votre application sur SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Détails sur la charge Teams d’application

| Teams charge de travail de l’application | Code source | Artefact de build| Ressource cible |
|-------------|----------|---------------|---------------|
|Onglets avec React </br> Charge de travail frontale| `yourProjectFolder/tabs`| `tabs/build` |Stockage Azure |
|Onglets avec SharePoint </br> Charge de travail frontale | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint catalogue d’applications |
|API sur les fonctions Azure </br> Charge de travail du back-end | `yourProjectFolder/api`| Non applicable |Fonctions Azure |
|Bots et extensions de messagerie </br> Charge de travail du back-end | `yourProjectFolder/bot` | Non applicable | Service d’application Azure |

> [!NOTE]
> Lorsque vous incluez une ressource de gestion d’API Azure dans votre projet et déclenchez le déploiement. Vous pouvez publier vos API dans les fonctions Azure dans le service de gestion des API Azure.

## <a name="see-also"></a>Voir aussi

* [Ajouter des ressources cloud supplémentaires](add-resource.md)
* [Ajouter des fonctionnalités Teams’application](add-capability.md)
* [Déployer du code de projet avec des pipelines CI/CD](use-CICD-template.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
* [Collaborer avec d’autres développeurs sur Teams projet](TeamsFx-collaboration.md)
