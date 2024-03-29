---
title: Vue d’ensemble du kit de ressources Teams
author: zyxiaoyuer
description: Dans ce module, découvrez le Kit de ressources Teams, l’installation du Kit de ressources Teams et le parcours utilisateur du Kit de ressources Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: cb3508bdd22f9d05c48e71b1b90ec4ffbf4c56af
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833162"
---
# <a name="teams-toolkit-overview"></a>Vue d’ensemble du kit de ressources Teams

Teams Toolkit facilite la prise en main du développement d’applications pour Microsoft Teams à l’aide de Visual Studio et Visual Studio Code.

* Commencez par un modèle de projet ou à partir d’un exemple.
* Gagnez du temps d’installation grâce à l’inscription et à la configuration automatisées des applications.
* Exécutez et déboguez dans Teams directement à partir d’outils familiers.
* Valeurs par défaut intelligentes pour l’hébergement dans Azure à l’aide de l’infrastructure en tant que code et de Bicep.
* Créez des configurations uniques telles que dev, test et prod à l’aide de la fonctionnalité Environnements.
* Apportez votre application à votre organisation ou au App Store Teams à l’aide des outils de publication intégrés.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Parcours utilisateur du Kit de ressources Teams" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

## <a name="available-for-visual-studio-and-visual-studio-code"></a>Disponible pour Visual Studio et Visual Studio Code

Teams Toolkit est disponible gratuitement pour Visual Studio Code et prend en charge Visual Studio 2022 Community, Professional et Enterprise. Pour plus d’informations sur l’installation et la configuration, consultez la [documentation Installer Teams Toolkit](./install-Teams-Toolkit.md) .

| Toolkit Teams | Visual Studio | Visual Studio Code |
| - | ------------- | ------------------ |
| Installation | Disponible dans le Visual Studio Installer | Disponible dans vs Marketplace |
| Générer avec | C#, .NET, ASP.NET, Blazor | JavaScript, TypeScript, React, SPFx |

## <a name="features"></a>Fonctionnalités

### <a name="project-templates"></a>Modèles de projets

Teams Toolkit réduit la complexité de la prise en main des modèles pour les scénarios d’application métier courants et les valeurs par défaut intelligentes pour accélérer votre temps de production. Si vous êtes déjà familiarisé avec le développement d’applications Teams, vous pouvez également commencer directement avec des modèles axés sur les fonctionnalités. c’est-à-dire Tab, Bot, Extension de messagerie.

::: zone pivot="visual-studio-code"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app.png" alt-text="Menu Créer une application Teams dans VS Code":::
::: zone-end

::: zone pivot="visual-studio"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app-vs.png" alt-text="Menu Créer une application Teams dans VS Code":::
::: zone-end

### <a name="automatic-registration-and-configuration"></a>Inscription et configuration automatiques

Gagnez du temps et laissez le kit de ressources inscrire automatiquement l’application dans le portail des développeurs Teams et configurer automatiquement des paramètres tels qu’Azure Active Directory lorsque vous exécutez ou déboguez l’application pour la première fois. Connectez-vous avec votre compte Microsoft 365 pour contrôler l’emplacement où l’application est configurée et personnaliser le manifeste Azure AD inclus lorsque vous avez besoin de plus de flexibilité.

::: zone pivot="visual-studio-code"

### <a name="multiple-environments"></a>Plusieurs environnements

Avec les fonctionnalités Environnements, vous pouvez créer différents regroupements de ressources cloud pour simplifier l’exécution et le test de votre application. Utilisez l’environnement « dev » avec votre abonnement Azure ou créez-en un avec un autre abonnement pour la préproduction, le test et la production.

### <a name="quick-access-to-teams-developer-portal"></a>Accès rapide au portail des développeurs Teams

Accédez rapidement au portail des développeurs Teams, où vous pouvez configurer, distribuer et gérer votre application. Pour plus d’informations, consultez [Gérer vos applications Teams à l’aide du portail des développeurs](../concepts/build-and-test/manage-your-apps-in-developer-portal.md).

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="Portail des développeurs":::

::: zone-end

::: zone pivot="visual-studio"

#### <a name="teamsfx-net-sdk-reference-docs"></a>Documentation de référence du Kit de développement logiciel (SDK) .NET TeamsFx

* [Espace de noms Microsoft.Extensions.DependencyInjection](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Espace de noms Microsoft.TeamsFx](/../dotnet/api/Microsoft.TeamsFx)
* [Espace de noms Microsoft.TeamsFx.Configuration](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Espace de noms Microsoft.TeamsFx.Conversation](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Espace de noms Microsoft.TeamsFx.Helper](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## <a name="see-also"></a>Voir aussi

* [Créer une application Teams dans Visual Studio](create-new-project.md)
* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy.md)
