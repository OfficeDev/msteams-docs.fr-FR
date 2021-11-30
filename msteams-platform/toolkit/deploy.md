---
title: Déployer dans le cloud
author: MuyangAmigo
description: Déployer dans le cloud
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 3f7dc4b320bccfa8a6017f87045b27a37d8199f7
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227697"
---
# <a name="deploy-to-the-cloud"></a>Déployer dans le cloud

Teams Shared Computer Toolkit vous permet de déployer ou de télécharger le code frontal et le code frontal dans votre application vers vos ressources cloud mises en service dans Azure.

* L’onglet, tel que les applications frontales, est déployé sur le stockage Azure et configuré pour l’hébergement web statique ou un site SharePoint web.
* Les API principale sont déployées dans les fonctions Azure.
* Le bot ou l’extension de messagerie est déployé sur Azure App Service.

## <a name="prerequisite"></a>Conditions préalables

* [Installez Teams Shared Computer Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) version v3.0.0+.

> [!TIP]
> Un projet d’application Teams doit déjà être ouvert dans du code VS.

> [!NOTE]
> Avant de déployer le code de projet sur le cloud, effectuez d’abord les étapes de mise en [service des ressources cloud.](provision.md)


## <a name="deploy-teams-apps-using-teams-toolkit"></a>Déployer des Teams à l’aide Teams Shared Computer Toolkit

Dans les didacticiels de mise en place, il existe des guides pas à pas sur la façon de déployer à l’aide Teams Shared Computer Toolkit. Vous pouvez utiliser les applications suivantes pour déployer votre Teams suivante :

* [Déployer votre application sur Azure](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)
* [Déployer votre application sur SharePoint](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)

## <a name="details-on-teams-app-workloads"></a>Détails sur les charges Teams d’application

| Teams charges de travail des applications| Code source | Créer Artifacts| Ressources cibles |
|-------------|----------|---------------|---------------|
|Onglets avec React </br> Charge de travail frontale| `yourProjectFolder/tabs`| `tabs/build` |Stockage Azure |
|Onglets avec SharePoint </br> Charge de travail frontale | `yourProjectFolder/SPFx`| `SPFx/sharepoint/solution` |SharePoint catalogue d’applications |
|API sur les fonctions Azure </br> Charge de travail du back-end | `yourProjectFolder/api`| N/A |Azure Functions |
|Bots et extensions de messagerie </br> Charge de travail du back-end | `yourProjectFolder/bot` | N/A | Azure App Service |

> [!NOTE]
> Lorsque vous incluez une ressource de gestion d’API Azure dans votre projet et déclenchez le déploiement. Vous pouvez publier vos API dans les fonctions Azure dans le service de gestion des API Azure.

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Ajouter des ressources cloud supplémentaires](add-resource.md)

> [!div class="nextstepaction"]
> [Ajouter des fonctionnalités Teams’application](add-capability.md)

> [!div class="nextstepaction"]
> [Déployer du code de projet avec des pipelines CI/CD](use-CICD-template.md)

> [!div class="nextstepaction"]
> [Gérer plusieurs environnements](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [Collaborer avec d’autres développeurs sur Teams projet](TeamsFx-collaboration.md)
