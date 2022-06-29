---
title: Déployer à partir du cloud
author: MuyangAmigo
description: Dans ce module, découvrez comment déployer une application dans le cloud, Azure ou SharePoint et déployer des applications Teams à l’aide du Kit de ressources Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 607214b329734f143d3bbcd9ede87ca85c9c97bb
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503332"
---
# <a name="deploy-teams-app-to-the-cloud"></a>Déployer l’application Teams dans le cloud

Le Kit de ressources Teams vous aide à déployer ou à charger le code frontal et le code principal de votre application vers vos ressources cloud provisionnées dans Azure.

* L’onglet, tel que les applications frontales, est déployé vers le stockage Azure et configuré pour l’hébergement web statique ou un site SharePoint.
* Les API principales sont déployées vers les fonctions Azure.
* Le bot ou l’extension de message est déployé vers Azure App Service.

## <a name="prerequisite"></a>Conditions préalables

* [Installez le Kit de ressources Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!NOTE]
>
> * Vérifiez que le projet d’application Teams est ouvert dans VS Code.
> * Avant de déployer le code de projet vers le cloud, [approvisionnez les ressources cloud](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Déployer des applications Teams à l’aide du Kit de ressources Teams

Les guides de démarrage vous aident à déployer à l’aide du Kit de ressources Teams. Vous pouvez utiliser les éléments suivants pour déployer votre application Teams :

* [Déployer votre application vers Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Déployer votre extension vers SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workload"></a>Détails sur la charge de travail de l’application Teams

| Charge de travail de l’application Teams | Code source | Artefact de build| Ressource cible |
|-------------|----------|---------------|---------------|
|Onglets avec React </br> Charge de travail frontale| `yourProjectFolder/tabs`| `tabs/build` |Stockage Azure |
|Onglets avec SharePoint </br> Charge de travail frontale | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |Catalogue des applications SharePoint |
|Les API sur Azure Functions </br> Charge de travail principale | `yourProjectFolder/api`| Non applicable |Azure Functions |
|Bots et extensions de message </br> Charge de travail principale | `yourProjectFolder/bot` | Non applicable | Azure App Service |

> [!NOTE]
> Lorsque vous incluez une ressource de gestion d’API Azure dans votre projet et que vous déclenchez le déploiement. Vous pouvez publier vos API dans Azure Functions vers le service de gestion des API Azure.

## <a name="see-also"></a>Voir aussi

* [Ajouter d’autres ressources cloud](add-resource.md)
* [Créer et déployer un service cloud Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Ajouter d’autres fonctionnalités d’application Teams](add-capability.md)
* [Déployer du code de projet avec des pipelines CI/CD](use-CICD-template.md)
* [Gérer plusieurs environnements](TeamsFx-multi-env.md)
* [Collaborer avec d’autres développeurs sur des projets Teams](TeamsFx-collaboration.md)
