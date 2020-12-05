---
title: Qu’est-ce qu’un onglet personnalisé dans teams ?
author: laujan
description: Vue d’ensemble des onglets personnalisés sur la plateforme teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: e89f07133f86b6c0700e6a71d8e53bf6d9831196
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576847"
---
# <a name="what-are-microsoft-teams-custom-tabs"></a>Qu’est-ce que les onglets personnalisés de Microsoft teams ?

Les onglets sont des pages Web intégrant des équipes dans Microsoft Teams. Il s’agit de balises HTML simples <iframe \> qui pointent vers des domaines déclarés dans le manifeste de l’application et peuvent être ajoutés dans le cadre d’un canal à l’intérieur d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur individuel. Vous pouvez inclure des onglets personnalisés avec votre application pour incorporer votre propre contenu Web dans teams ou ajouter une fonctionnalité propre à teams à votre contenu Web. *Voir* [teams JavaScript Client SDK](/javascript/api/overview/msteams-client).

> [!NOTE]
> Chrome 80, planifié pour la publication au début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookies par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies au lieu de vous appuyer sur le comportement par défaut du navigateur. *Voir* [SameSite cookie Attribute (mise à jour 2020)](../resources/samesite-cookie-update.md).

Il existe deux types d’onglets disponibles dans Teams, Channel/Group et Personal. Les onglets canal/groupe livrent du contenu à des canaux et des conversations de groupe, et constituent un excellent moyen de créer des espaces de collaboration sur le contenu Web dédié. Les onglets personnels, ainsi que les robots d’étendue personnelle, font partie des applications personnelles et sont étendus à un seul utilisateur. Ils peuvent être épinglés dans la barre de navigation de gauche pour faciliter l’accès.

## <a name="lesser-known-tab-features"></a>Fonctionnalités d’onglet plus petites connues

> [!div class="checklist"]
>
> * Si un onglet est ajouté à une application qui a également un bot, le bot est également ajouté à l’équipe.
> * Conscience de l’ID Azure Active Directory (Azure AD) de l’utilisateur actuel.
> * Détection des paramètres régionaux de l’utilisateur pour indiquer la langue, c’est-à-dire `en-us` . 
> * Fonctionnalité d’authentification unique (SSO), si prise en charge.
> * Possibilité d’utiliser des robots ou des notifications d’application pour établir un lien profond vers l’onglet ou une sous-entité au sein du service, par exemple un élément de travail individuel.
> * Possibilité d’ouvrir un module de tâches à partir de liens dans un onglet.
> * Réutilisation des composants WebPart SharePoint dans l’onglet.

## <a name="tabs-user-scenarios"></a>Scénarios utilisateur onglets

**Scénario :** Ajoutez une ressource Web existante dans Teams. \
**Exemple :** Vous créez un onglet personnel dans votre application de teams qui présente un site Web d’information d’entreprise aux utilisateurs.

**Scénario :** Ajouter des pages de prise en charge à un bot de teams ou à une extension de messagerie. \
**Exemple :** Vous créez des onglets personnels qui fournissent du *contenu de pages* *Web à* des utilisateurs.

**Scénario :** Fournir un accès aux éléments avec lesquels vos utilisateurs interagissent régulièrement pour la collaboration et le dialogue de coopération. \
**Exemple :** Vous créez un onglet de canal/groupe avec un lien détaillé vers des éléments individuels.

## <a name="how-do-tabs-work"></a>Fonctionnement des onglets

Un onglet personnalisé est déclaré dans le manifeste de l’application de votre package d’application. Pour chaque page Web que vous souhaitez inclure sous la forme d’un onglet dans votre application, vous définissez une URL et une étendue. En outre, vous devez ajouter le [Kit de développement logiciel (SDK) du client JavaScript teams](/javascript/api/overview/msteams-client) à votre page et appeler `microsoftTeams.initialize()` après le chargement de votre page. Cette opération permettra à teams d’afficher votre page, vous donne accès à des informations spécifiques à Teams (par exemple, si le client teams exécute le *thème sombre*) et vous permet d’agir en fonction des résultats.

Que vous choisissiez d’exposer votre onglet au sein de la chaîne/du groupe ou de l’étendue personnelle, vous devez présenter une \> [page de contenu](~/tabs/how-to/create-tab-pages/content-page.md) html <iframe dans votre onglet. Pour les onglets personnels, l’URL de contenu est définie directement dans le manifeste de l’application de teams par la `contentUrl` propriété dans le `staticTabs` tableau. Le contenu de votre onglet sera le même pour tous les utilisateurs.

Pour les onglets canal/groupe, vous devez également créer une page de configuration supplémentaire qui permet aux utilisateurs de configurer votre URL de page de contenu, généralement à l’aide des paramètres de chaîne de requête d’URL pour charger le contenu approprié pour ce contexte. Cela est dû au fait que votre onglet de canal/groupe peut être ajouté à plusieurs équipes ou conversations de groupe différentes. Lors de chaque installation suivante, vos utilisateurs peuvent configurer l’onglet, ce qui vous permet de personnaliser l’expérience en fonction de vos besoins. Lorsque les utilisateurs ajoutent ou configurent un onglet, une URL est associée à l’onglet présenté dans l’interface utilisateur de teams. La configuration d’un onglet consiste simplement à ajouter des paramètres supplémentaires à cette URL. Par exemple, lorsque vous ajoutez l’onglet Forums Azure, la page Configuration vous permet de choisir la carte chargée par l’onglet. L’URL de la page de configuration est spécifiée par la  `configurationUrl` propriété dans le `configurableTabs` tableau dans le manifeste de votre application.

Vous pouvez disposer d’un (1) onglet de canal/groupe et jusqu’à seize (16) d’onglets personnels par application.

## <a name="mobile-clients"></a>Clients mobiles

Si vous choisissez d’afficher l’onglet canal/groupe sur les clients mobiles Teams, la `setSettings()` configuration doit avoir une valeur pour la `websiteUrl` propriété. Pour garantir une expérience utilisateur optimale, suivez les [instructions pour les onglets sur mobile](~/tabs/design/tabs-mobile.md) lors de la création des onglets.

> [!div class="nextstepaction"]
> [En savoir plus : demander des autorisations de périphérique](/concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
>[En savoir plus : autorisations de Galerie d’images et de caméras](/concepts/device-capabilities/mobile-camera-image-permissions.md)