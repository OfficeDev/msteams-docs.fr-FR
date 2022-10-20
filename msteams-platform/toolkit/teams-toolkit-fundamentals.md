---
title: Vue d’ensemble du kit de ressources Teams
author: zyxiaoyuer
description: Dans ce module, découvrez le Kit de ressources Teams, l’installation de Teams Toolkit et le parcours utilisateur du Kit de ressources Teams
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/24/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 786bfd318f1cefa4329e54b5a19cba89a823bb5b
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615337"
---
# <a name="teams-toolkit-overview"></a>Vue d’ensemble du kit de ressources Teams

Teams Toolkit facilite la prise en main du développement d’applications pour Microsoft Teams à l’aide de Visual Studio et Visual Studio Code.

* Démarrer avec un modèle de projet ou à partir d’un exemple
* Gagner du temps d’installation avec l’inscription et la configuration automatisées des applications
* Exécuter et déboguer vers Teams directement à partir d’outils familiers
* Valeurs par défaut intelligentes pour l’hébergement dans Azure à l’aide de l’infrastructure en tant que code et de Bicep
* Créer des configurations uniques comme dev, test et prod à l’aide de la fonctionnalité Environnements
* Apporter votre application à votre organisation ou au App Store Teams à l’aide d’outils de publication intégrés

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png" alt-text="Parcours utilisateur du Kit de ressources Teams" lightbox="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey2.png":::

## <a name="available-for-visual-studio-and-visual-studio-code"></a>Disponible pour Visual Studio et Visual Studio Code

Teams Toolkit est disponible gratuitement pour Visual Studio Code et prend en charge Visual Studio 2022 Community, Professional et Enterprise. Pour plus d’informations sur l’installation et l’installation, consultez la [documentation install Teams Toolkit](./install-Teams-Toolkit.md) .

| Toolkit Teams | Visual Studio | Visual Studio Code |
| - | ------------- | ------------------ |
| Installation | Disponible dans le Visual Studio Installer | Disponible sur la Place de marché VS |
| Générer avec | C#, .NET, ASP.NET, Blazor | JavaScript, TypeScript, React, SPFx |

## <a name="features"></a>Fonctionnalités

### <a name="project-templates"></a>Modèles de projets

Teams Toolkit réduit la complexité de la prise en main des modèles pour les scénarios courants d’application métier et les valeurs par défaut intelligentes pour accélérer votre temps de production. Si vous êtes déjà familiarisé avec le développement d’applications Teams, vous pouvez également commencer directement avec des modèles axés sur les fonctionnalités. c’est-à-dire Tab, Bot, Extension de messagerie.

::: zone pivot="visual-studio-code"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app.png" alt-text="Créer un menu d’application Teams dans VS Code":::
::: zone-end

::: zone pivot="visual-studio"
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create-new-app-vs.png" alt-text="Créer un menu d’application Teams dans VS Code":::
::: zone-end

### <a name="automatic-registration-and-configuration"></a>Inscription et configuration automatiques

Gagnez du temps et laissez le kit de ressources inscrire automatiquement l’application dans le portail des développeurs Teams et configurer automatiquement des paramètres comme Azure Active Directory lors de la première exécution ou débogage de l’application. Connectez-vous avec votre compte Microsoft 365 pour contrôler où l’application est configurée et personnalisez le manifeste Azure AD inclus lorsque vous avez besoin de plus de flexibilité.

::: zone pivot="visual-studio-code"

### <a name="multiple-environments"></a>Plusieurs environnements

Avec les fonctionnalités Environnements, vous pouvez créer différents regroupements de ressources cloud pour simplifier l’exécution et le test de votre application. Utilisez l’environnement « dev » avec votre abonnement Azure ou créez-en un autre avec un autre abonnement pour la préproduction, le test et la production.

### <a name="quick-access-to-teams-developer-portal"></a>Accès rapide au portail des développeurs Teams

Accédez rapidement au portail des développeurs Teams, où vous pouvez configurer, distribuer et gérer votre application. Pour plus d’informations, consultez [gérer vos applications Teams à l’aide du portail des développeurs](../concepts/build-and-test/manage-your-apps-in-developer-portal.md).

:::image type="content" source="../assets/images/teams-toolkit-v2/build-environment-developer-portal-1.png" alt-text="Portail des développeurs":::

::: zone-end

::: zone pivot="visual-studio"

#### <a name="teamsfx-net-sdk-reference-docs"></a>Documentation de référence sur le Kit de développement logiciel (SDK) .NET TeamsFx

* [Espace de noms Microsoft.Extensions.DependencyInjection](/../dotnet/api/Microsoft.Extensions.DependencyInjection)
* [Espace de noms Microsoft.TeamsFx](/../dotnet/api/Microsoft.TeamsFx)
* [Espace de noms Microsoft.TeamsFx.Configuration](/../dotnet/api/Microsoft.TeamsFx.Configuration)
* [Espace de noms Microsoft.TeamsFx.Conversation](/../dotnet/api/Microsoft.TeamsFx.Conversation)
* [Espace de noms Microsoft.TeamsFx.Helper](/../dotnet/api/Microsoft.TeamsFx.Helper)

::: zone-end

## <a name="see-also"></a>Voir aussi

* [Créer une application Teams dans Visual Studio](create-new-teams-app-for-Visual-Studio.md)
* [Provisionner des ressources cloud à l’aide de Visual Studio](provision-cloud-resources.md)
* [Déployer une application Teams dans le cloud à l’aide de Visual Studio](deploy-teams-app.md)
