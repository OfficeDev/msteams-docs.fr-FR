---
title: Déployer à partir du cloud
author: MuyangAmigo
description: Déployer une application dans le cloud, Azure ou SharePoint
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 1d0ade9abed4be212abfb96068626172c4f0f03e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104146"
---
# <a name="deploy-to-the-cloud"></a>Déployer à partir du cloud

Teams Shared Computer Toolkit vous aide à déployer ou à charger le code front-end et back-end dans votre application sur vos ressources cloud provisionnées dans Azure.

* L’onglet, tel que les applications front-end, est déployé sur le stockage Azure et configuré pour l’hébergement web statique ou un site sharepoint.
* Les API back-end sont déployées sur les fonctions Azure.
* Le bot ou l’extension de message est déployé sur Azure App Service.

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!NOTE]
>
> * Vérifiez que vous avez Teams projet d’application ouvert dans VS Code.
> * Avant de déployer du code de projet dans le cloud, [provisionnez les ressources cloud](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Déployer des applications Teams à l’aide de Teams Shared Computer Toolkit

Les guides de prise en main vous aident à déployer à l’aide de Teams Shared Computer Toolkit. Vous pouvez utiliser les éléments suivants pour déployer votre application Teams :

* [Déployer votre application sur Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Déployer votre application sur SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Détails sur Teams charge de travail de l’application

| Teams charge de travail de l’application | Code source | Artefact de build| Ressource cible |
|-------------|----------|---------------|---------------|
|Onglets avec React </br> Charge de travail front-end| `yourProjectFolder/tabs`| `tabs/build` |Stockage Azure |
|Onglets avec SharePoint </br> Charge de travail front-end | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |catalogue d’applications SharePoint |
|API sur les fonctions Azure </br> Charge de travail principale | `yourProjectFolder/api`| Non applicable |Fonctions Azure |
|Bots et extensions de message </br> Charge de travail principale | `yourProjectFolder/bot` | Non applicable | Azure App Service |

> [!NOTE]
> Lorsque vous incluez une ressource de gestion des API Azure dans votre projet et que vous déclenchez le déploiement. Vous pouvez publier vos API dans azure functions sur le service de gestion des API Azure.

## <a name="see-also"></a>Voir aussi

* [Ajouter d’autres ressources cloud](add-resource.md)
* [Créer et déployer un service cloud Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Ajouter d’autres fonctionnalités d’application Teams](add-capability.md)
* [Déployer du code de projet avec des pipelines CI/CD](use-CICD-template.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
* [Collaborer avec d’autres développeurs sur des projets Teams](TeamsFx-collaboration.md)
