---
title: Concevoir votre application avec des composants d’interface utilisateur avancés
author: heath-hamilton
description: Découvrez les composants de l’interface utilisateur Teams, tels que la barre de navigation, la barre de notification, l’affichage intermédiaire, ainsi que les cas d’utilisation pertinents.
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: reference
ms.openlocfilehash: d0c95c680e4cbf81776ebe7d5b0a580b5cff7d2d
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027346"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>Conception de votre application Microsoft Teams avec des composants d’interface utilisateur avancés

Les composants suivants sont une combinaison de [composants d’interface utilisateur de base](~/concepts/design/design-teams-app-basic-ui-components.md) que vous pouvez utiliser pour les situations de conception Teams courantes, telles que la navigation.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Basé sur [Fluent UI](https://fluentsite.z22.web.core.windows.net/), le Kit d’interface utilisateur Microsoft Teams inclut des composants et des modèles conçus spécifiquement pour la création d’applications Teams. Dans le kit d’interface utilisateur, vous pouvez récupérer et insérer les composants répertoriés ici directement dans votre conception et voir d’autres exemples d’utilisation de chaque composant.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>Barre de navigation

Les barres de navigation sont une aide à la navigation qui transmet la hiérarchie de votre application. Ils aident les utilisateurs à comprendre comment la page qu’ils consultent s’intègre à l’expérience globale et à se permettre un accès en un clic aux niveaux supérieurs de cette hiérarchie.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Communiquer la hiérarchie
* Navigation

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="L’exemple montre un modèle de navigation sur mobile.":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="L’exemple montre un modèle de navigation sur le bureau.":::

## <a name="left-nav"></a>Navigation gauche

Utilisez la navigation de gauche pour parcourir plusieurs pages dans votre onglet Teams. Dans l’exemple suivant, la navigation gauche se trouve entre la liste de canaux et le contenu de l’onglet.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Parcourez plusieurs pages dans un onglet Teams.
* Décomposez les applications complexes en plusieurs pages.

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="L’exemple montre un modèle de navigation gauche sur mobile.":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="L’exemple montre un modèle de navigation gauche sur le bureau.":::

## <a name="notification-bar"></a>Barre de notification

Une barre de notification est une zone dédiée pour afficher un bref message important qui ne nécessite pas que l’utilisateur prenne des mesures immédiates. Des couleurs et des icônes d’arrière-plan spécifiques sont associées à des types de messages spécifiques (voir ci-dessous).

Vous pouvez implémenter une barre de notification à l’aide du composant [d’alerte](https://fluentsite.z22.web.core.windows.net/0.59.0/components/alert/definition) Fluent UI.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Messages critiques, erreurs et avertissements
* Messages de réussite
* Messages d’information ou promotionnels

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="L’exemple montre un modèle d’interface utilisateur de barre de notification sur mobile.":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="L’exemple montre des modèles d’interface utilisateur de barre de notification sur le bureau.":::

## <a name="stage-view"></a>vue des étapes

L’affichage intermédiaire permet aux utilisateurs de voir du contenu, comme une image, un fichier ou un site web, sur une grande surface dans Teams sans changer de contexte. Ce composant est principalement destiné à l’affichage du contenu. Ne l’utilisez pas pour des interactions complexes.

Découvrez comment implémenter la [vue d’étape](~/tabs/tabs-link-unfurling.md).

### <a name="top-use-cases"></a>Principaux cas d’usage

* Afficher du contenu dans une grande surface dans Teams au lieu d’une autre application ou navigateur
* Média à la une ou tout autre contenu enrichi

### <a name="mobile"></a>Mobile

Votre application peut lancer une étape à partir d’une carte adaptative, d’un lien partagé ou de composants visuels (par exemple, un graphique).

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="Exemple montrant un modèle d’étape sur mobile.":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="L’exemple montre un modèle d’étape sur le bureau.":::

## <a name="toolbar"></a>Barre d'outils

Une barre d’outils est un conteneur permettant de regrouper un ensemble de contrôles.

### <a name="top-use-cases"></a>Principaux cas d’usage

* Actions contextuelles sur le contenu de l’application.
* Filtre contextuel et recherche.
* Navigation et navigation.

### <a name="mobile"></a>Mobile

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="L’exemple montre un modèle de barre d’outils sur mobile.":::

### <a name="desktop"></a>Ordinateur de bureau

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="L’exemple montre un modèle de barre d’outils sur le bureau.":::
