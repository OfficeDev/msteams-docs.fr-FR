---
title: Qu’est-ce que les onglets personnalisés dans Microsoft teams ?
author: laujan
description: Vue d’ensemble des onglets personnalisés sur la plateforme Microsoft teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 77faa5a4b3bf7eede1443317ad8baac4934ebf9a
ms.sourcegitcommit: 646a8224523be7db96f9686e22d420d62d55d4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "42365254"
---
# <a name="what-are-microsoft-teams-custom-tabs"></a>Qu’est-ce que les onglets personnalisés de Microsoft teams ?

Les onglets sont des pages Web intégrant des équipes dans Microsoft Teams. Il s’agit de simples iframes qui pointent vers des domaines déclarés dans le manifeste de l’application et peuvent être ajoutés dans le cadre d’un canal à l’intérieur d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur individuel. Vous pouvez inclure des onglets personnalisés avec votre application pour incorporer votre propre contenu Web dans teams et ajouter une fonctionnalité propre à teams à votre contenu Web. *Voir* [teams JavaScript Client SDK](/javascript/api/overview/msteams-client).

> [!NOTE]
> Chrome 80, planifié pour la publication au début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookies par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies au lieu de vous appuyer sur le comportement par défaut du navigateur. *Voir* [SameSite cookie Attribute (mise à jour 2020)](../resources/samesite-cookie-update.md).

Il existe deux types d’onglets disponibles dans teams Channel/Group et Personal. Un onglet de canal/groupe fournit du contenu à des canaux et des conversations de groupe, et constitue un excellent moyen de créer des espaces de collaboration sur le contenu Web dédié. Les onglets personnels, ainsi que les robots d’étendue personnelle, font partie des applications personnelles et sont étendus à un seul utilisateur. Ils peuvent être épinglés dans la barre de navigation de gauche pour faciliter l’accès.

## <a name="lesser-known-tab-features"></a>Fonctionnalités d’onglet plus petites connues

> [!div class="checklist"]
>
> * Conscience de la liste entière d’une équipe.
> * Si un onglet est ajouté à une application qui a également un bot, le bot est également ajouté à l’équipe.
> * Sensibilisation de l’ID AAD de l’utilisateur actuel.
> * Détection des paramètres régionaux de l’utilisateur pour indiquer la langue, c’est-à-dire `en-us`. 
> * Fonctionnalité SSO, si prise en charge.
> * Possibilité d’utiliser des robots ou des notifications d’application pour établir un lien profond vers l’onglet ou une sous-entité au sein du service, par exemple un élément de travail individuel.
> * Possibilité d’ouvrir un module de tâches à partir de liens dans un onglet.
> * Réutilisation des composants WebPart SharePoint dans l’onglet.

## <a name="tabs-user-scenarios"></a>Scénarios utilisateur onglets

**Scénario :** Ajoutez une ressource Web existante dans Teams. \
**Exemple :** Vous créez un onglet personnel dans votre application de teams qui présente un site Web d’information d’entreprise aux utilisateurs.

**Scénario :** Ajouter des pages de prise en charge à un bot de teams ou à une extension de messagerie. \
**Exemple :** Vous créez des onglets personnels qui fournissent du contenu de pages Web à des utilisateurs.

**Scénario :** Fournir un accès aux éléments avec lesquels vos utilisateurs interagissent régulièrement pour la collaboration et le dialogue de coopération. \
**Exemple :** Vous créez un onglet de canal/groupe avec un lien détaillé vers des éléments individuels.

## <a name="how-do-tabs-work"></a>Fonctionnement des onglets

Un onglet personnalisé est déclaré dans le manifeste de l’application de votre package d’application. Pour chaque page Web que vous souhaitez inclure sous la forme d’un onglet dans votre application, vous définissez une URL et une étendue. En outre, vous devez ajouter le [Kit de développement logiciel (SDK) du client JavaScript teams](/javascript/api/overview/msteams-client) à votre page et appeler `microsoftTeams.initialize()` après le chargement de votre page. Cette opération permettra à teams d’afficher votre page, vous donne accès à des informations spécifiques à Teams (par exemple, si le client teams exécute le thème sombre) et vous permet d’agir en fonction des résultats.

Que vous choisissiez d’exposer votre onglet au sein de la chaîne/du groupe ou de l’étendue personnelle, vous devrez présenter une [page de contenu](~/tabs/how-to/create-tab-pages/content-page.md) html iframe dans votre onglet. Pour les onglets personnels, l’URL de contenu est définie directement dans votre `contentUrl` manifeste par la `staticTabs` propriété dans le tableau. Le contenu de votre onglet sera le même pour tous les utilisateurs.

Pour les onglets canal/groupe, vous devez également créer une page de configuration supplémentaire qui permet aux utilisateurs de configurer votre URL de page de contenu, généralement à l’aide des paramètres de chaîne de requête d’URL pour charger le contenu approprié pour ce contexte. Cela est dû au fait que votre onglet de canal/groupe peut être ajouté à plusieurs équipes ou conversations de groupe différentes. Lors de chaque installation suivante, vos utilisateurs peuvent configurer l’onglet, ce qui vous permet de personnaliser l’expérience en fonction de vos besoins. Lorsque les utilisateurs ajoutent un onglet ou configurent un onglet, une URL est associée à l’onglet présenté dans l’interface utilisateur de teams. La configuration d’un onglet consiste simplement à ajouter des paramètres supplémentaires à cette URL. Par exemple, lorsque vous ajoutez l’onglet de la carte DevOps Azure, la page Configuration vous permet de choisir la carte chargée par l’onglet. L’URL de la page de configuration est `configurationUrl` spécifiée par la `configurableTabs` propriété dans le tableau dans le manifeste de votre application.

Vous pouvez disposer d’un (1) onglet de canal/groupe et jusqu’à seize (16) d’onglets personnels par application.

## <a name="mobile-clients"></a>Clients mobiles

Si vous choisissez d’afficher l’onglet canal/groupe sur les clients mobiles Teams, `setSettings()` la configuration doit avoir une valeur pour `websiteUrl` la propriété (voir ci-dessous). Les onglets personnels sont actuellement disponibles dans l’Aperçu pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md). La prise en charge complète des onglets sur les clients mobiles sera bientôt disponible. Pour préparer la mise à jour, suivez les [instructions pour les onglets sur les appareils mobiles](~/tabs/design/tabs-mobile.md) lors de la création des onglets.
