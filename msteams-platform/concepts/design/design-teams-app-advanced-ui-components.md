---
title: Concevoir votre application avec des composants d’interface utilisateur avancés
author: heath-hamilton
description: Découvrez les composants d’interface utilisateur utilisés dans Teams .
ms.author: surbhigupta
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 6f2bd9cd237751adb15db45bbd6e3cdfea35ce09
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328078"
---
# <a name="designing-your-microsoft-teams-app-with-advanced-ui-components"></a>Conception de votre application Microsoft Teams avec des composants d’interface utilisateur avancés

Les composants suivants sont une combinaison de [composants](~/concepts/design/design-teams-app-basic-ui-components.md) d’interface utilisateur de base que vous pouvez utiliser pour les situations Teams conception courantes, telles que la navigation.

## <a name="microsoft-teams-ui-kit"></a>Kit d’interface utilisateur de Microsoft Teams

Basé sur <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent’interface</a>utilisateur, le kit Microsoft Teams’interface utilisateur inclut des composants et des modèles spécifiquement conçus pour créer des applications Teams. Dans le kit d’interface utilisateur, vous pouvez récupérer et insérer les composants répertoriés ici directement dans votre conception et voir d’autres exemples d’utilisation de chaque composant.

> [!div class="nextstepaction"]
> [Obtenir le Kit d’interface utilisateur de Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="breadcrumb"></a>Barre de navigation

Les barre de navigation sont une aide à la navigation qui véhicule la hiérarchie de votre application. Ils aident les utilisateurs à comprendre comment la page qu’ils affichent s’intègre à l’expérience globale et offrent un accès en un clic aux niveaux supérieurs de cette hiérarchie.

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Hiérarchie de communication
* Navigation

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="L’exemple montre un modèle de lacrumb sur le bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-breadcrumb.png" alt-text="L’exemple montre un modèle de lacrumb sur mobile." border="false":::

---

## <a name="left-nav"></a>Navigation gauche

Utilisez le navigation de gauche pour parcourir plusieurs pages dans votre onglet Teams de navigation. Dans l’exemple suivant, le navigation gauche se trouve entre la liste de canaux et le contenu de l’onglet.

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Parcourez plusieurs pages dans un Teams onglet.
* Décomposez les applications complexes en plusieurs pages.

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="L’exemple montre un modèle de navigation gauche sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-left-nav.png" alt-text="L’exemple montre un modèle de navigation gauche sur un appareil mobile." border="false":::

---

## <a name="notification-bar"></a>Barre de notification

Une barre de notification est une zone dédiée à l’affichage de messages brefs et importants qui ne nécessitent pas que l’utilisateur prenne des mesures immédiates. Des icônes et des couleurs d’arrière-plan spécifiques sont associées à des types de messages spécifiques (voir ci-dessous).

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Messages critiques, erreurs et avertissements
* Messages de réussite
* Messages d’information ou promotionnels

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="L’exemple montre les modèles d’interface utilisateur de la barre de notification sur le bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-notification-bar.png" alt-text="Exemple de modèle d’interface utilisateur de barre de notification sur mobile." border="false":::

---

## <a name="stage"></a>Phase

L’étape permet aux utilisateurs d’afficher du contenu, tel qu’une image, un fichier ou un site web, sur une grande surface Teams sans changer de contexte. L’étape est principalement destinée à l’affichage du contenu. N’utilisez pas de phase pour les interactions complexes.

Découvrez comment implémenter [l’étape.](~/tabs/tabs-link-unfurling.md)

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Afficher le contenu sur une grande surface dans Teams au lieu d’une autre application ou navigateur
* Média à la une ou autre contenu enrichi

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="L’exemple montre un modèle d’étape sur ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

Votre application peut lancer une étape à partir d’une carte adaptative, d’un lien partagé ou de composants visuels (tels qu’un graphique).

:::image type="content" source="../../assets/images/ui-templates/mobile-stage.png" alt-text="L’exemple montre un modèle d’étape sur mobile." border="false":::

---

## <a name="toolbar"></a>Barre d'outils

Une barre d’outils est un conteneur permettant de grouper un ensemble de contrôles.

### <a name="top-use-cases"></a>Cas d’utilisation principaux

* Actions contextuelles sur le contenu de l’application
* Filtre contextuel et recherche
* Navigation et barre de navigation

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="L’exemple montre un modèle de barre d’outils sur un ordinateur de bureau." border="false":::

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-toolbar.png" alt-text="L’exemple montre un modèle de barre d’outils sur mobile." border="false":::

---
