---
title: Déployer à partir du cloud
author: MuyangAmigo
description: Dans ce module, découvrez comment déployer une application dans le cloud, Azure ou SharePoint et déployer des applications Teams à l’aide du Kit de ressources Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9ad2c9d16901990344ca521599b94b84b0e76217
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616925"
---
# <a name="deploy-teams-app-to-the-cloud"></a>Déployer l’application Teams dans le cloud

Le Kit de ressources Teams vous aide à déployer ou à charger le code frontal et le code principal de votre application vers vos ressources cloud provisionnées dans Azure. Vous pouvez déployer les éléments suivants dans le cloud :

* L’onglet, tel que les applications frontales, est déployé vers le stockage Azure et configuré pour l’hébergement web statique ou un site SharePoint.
* Les API principales sont déployées vers les fonctions Azure.
* Le bot ou l’extension de message est déployé vers Azure App Service.

  > [!NOTE]
  > Avant de déployer du code d’application dans le cloud Azure, vous devez terminer avec succès [l’approvisionnement des ressources cloud](provision.md).

## <a name="deploy-teams-apps-using-teams-toolkit"></a>Déployer des applications Teams à l’aide du Kit de ressources Teams

Les guides de prise en main vous aident à déployer à l’aide du Kit de ressources Teams. Vous pouvez utiliser les éléments suivants pour déployer votre application Teams :

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
> Lorsque vous incluez une ressource de gestion des API Azure dans votre projet et que vous déclenchez un déploiement, vous pouvez publier vos API dans les fonctions Azure sur le service de gestion des API Azure.

## <a name="see-also"></a>Voir aussi

* [Créer et déployer un service cloud Azure](/azure/cloud-services/cloud-services-how-to-create-deploy-portal)
* [Créer des applications Teams multi-fonctionnalités](add-capability.md)
* [Ajouter des ressources cloud à l’application Microsoft Teams](add-resource.md)
