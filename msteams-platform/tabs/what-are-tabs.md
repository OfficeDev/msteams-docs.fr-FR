---
title: Onglets Microsoft Teams
author: surbhigupta
description: Vue d’ensemble des onglets personnalisés sur la plateforme Teams web
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bde45728a957bee3aa06752328943fe13d1fa3fe
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179917"
---
# <a name="microsoft-teams-tabs"></a>Onglets Microsoft Teams

Les onglets Teams des pages web sensibles incorporées dans Microsoft Teams. Il s’agit de balises html <iframe simples qui pointent vers des domaines déclarés dans le manifeste de l’application et qui peuvent être ajoutées dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur \> individuel. Vous pouvez inclure des onglets personnalisés avec votre application pour incorporer votre propre contenu web dans Teams ou ajouter Teams fonctionnalités spécifiques à votre contenu web. Pour plus d’informations, [Teams SDK client JavaScript.](/javascript/api/overview/msteams-client)

L’image suivante montre les onglets personnels :

![Onglets personnels](../assets/images/tabs/personaltab.png)

L’image suivante montre les onglets du canal Contoso :

![Onglets de canal ou de groupe](../assets/images/tabs/tabs.png)

> [!VIDEO https://www.youtube-nocookie.com/embed/Jw6i7Mkt0dg]


> [!VIDEO https://www.youtube-nocookie.com/embed/T2a8yJC3VcQ]

Il existe quelques conditions préalables que vous devez respecter avant de travailler sur des onglets.

Deux types d’onglets sont disponibles dans Teams, personnel et canal ou groupe. [Les onglets personnels,](~/tabs/how-to/create-personal-tab.md)ainsi que les bots d’étendue personnelle, font partie des applications personnelles et sont limitées à un seul utilisateur. Ils peuvent être épinglés à la barre de navigation de gauche pour faciliter l’accès. [Les onglets](~/tabs/how-to/create-channel-group-tab.md) de canal ou de groupe offrent du contenu aux canaux et aux conversations de groupe, et sont un excellent moyen de créer des espaces de collaboration autour de contenu web dédié.

Vous pouvez [créer une page de contenu](~/tabs/how-to/create-tab-pages/content-page.md) dans le cadre d’un onglet personnel, d’un onglet de canal ou de groupe ou d’un module de tâche. Vous pouvez créer une page de [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) qui permet aux utilisateurs de configurer une application Microsoft Teams et de l’utiliser pour configurer un onglet de conversation de canal ou de groupe, une extension de messagerie ou un connecteur Office 365. Vous pouvez permettre aux utilisateurs de reconfigurer votre onglet après l’installation et de créer une [page](~/tabs/how-to/create-tab-pages/removal-page.md) de suppression d’onglets pour votre application. Lorsque vous créez une application Teams qui inclut un onglet, vous devez tester le fonctionnement de votre onglet sur les clients Teams [Android et iOS.](~/tabs/design/tabs-mobile.md) Votre onglet doit obtenir [le contexte par](~/tabs/how-to/access-teams-context.md) le biais d’informations de base, de paramètres régionaux et de thèmes, ou qui identifie ce qui se trouve dans `entityId` `subEntityId` l’onglet.

Vous pouvez créer des onglets avec des cartes adaptatives et centraliser toutes les fonctionnalités de l’application Teams en éliminant la nécessité d’un autre système principal pour vos bots et onglets. [Stage View](~/tabs/tabs-link-unfurling.md) est un nouveau composant d’interface utilisateur qui vous permet d’afficher le contenu ouvert en plein écran en Teams et épinglé sous la forme d’un onglet. Le [service](~/tabs/tabs-link-unfurling.md) de déploiement de lien existant est mis à jour de sorte qu’il soit utilisé pour transformer les URL en onglet à l’aide d’une carte adaptative et des services de conversation. Vous pouvez créer des [onglets](~/tabs/how-to/conversational-tabs.md) de conversation à l’aide de sous-entités de conversation qui permettent aux utilisateurs d’avoir des conversations sur des sous-entités dans votre onglet, telles que des tâches spécifiques, des patients et des opportunités de vente, au lieu de discuter de l’onglet entier. Vous pouvez modifier les [marges des onglets](~/resources/removing-tab-margins.md) pour améliorer l’expérience du développeur lors de la création d’applications.

## <a name="tab-features"></a>Fonctionnalités de l’onglet

Les fonctionnalités de l’onglet sont les suivantes :

* Si un onglet est ajouté à une application qui possède également un bot, le bot est également ajouté à l’équipe.
* Sensibilisation de Azure Active Directory (AAD) de l’utilisateur actuel.
* Sensibilisation des paramètres régionaux pour que l’utilisateur indique la langue qui est `en-us` .
* Fonctionnalité d' sign-on unique (SSO), si elle est prise en charge.
* Possibilité d’utiliser des bots ou des notifications d’application pour créer un lien profond vers l’onglet ou une sous-entité au sein du service, par exemple un élément de travail individuel.
* Possibilité d’ouvrir un module de tâche à partir de liens dans un onglet.
* Réutilisation des SharePoint web dans l’onglet.

## <a name="tabs-user-scenarios"></a>Scénarios utilisateur onglets

**Scénario :** Apportez une ressource web existante à l’Teams. \
**Exemple :** Vous créez un onglet personnel dans votre application Teams qui présente un site web d’entreprise d’information aux utilisateurs.

**Scénario :** Ajoutez des pages de support à un bot Teams ou une extension de messagerie. \
**Exemple :** Vous créez des onglets personnels qui fournissent des **informations sur les** pages web et aident les utilisateurs. 

**Scénario :** Fournir l’accès aux éléments avec qui vos utilisateurs interagissent régulièrement pour un dialogue et une collaboration collaboratifs collaboratifs. \
**Exemple :** Vous créez un onglet de canal ou de groupe avec un lien profond vers des éléments individuels.

## <a name="understand-how-tabs-work"></a>Comprendre le fonctionnement des onglets

Vous pouvez utiliser l’une des méthodes suivantes pour créer des onglets :

* [Déclarer un onglet personnalisé dans le manifeste de l’application](#declare-custom-tab-in-app-manifest)
* [Utiliser la carte adaptative pour créer des onglets](~/tabs/how-to/build-adaptive-card-tabs.md)

### <a name="declare-custom-tab-in-app-manifest"></a>Déclarer un onglet personnalisé dans le manifeste de l’application

Un onglet personnalisé est déclaré dans le manifeste de l’application de votre package d’application. Pour chaque page web que vous souhaitez inclure en tant qu’onglet dans votre application, vous définissez une URL et une étendue. En outre, vous pouvez ajouter Teams [SDK client JavaScript](/javascript/api/overview/msteams-client) à votre page et appeler après le chargement `microsoftTeams.initialize()` de votre page. Teams affiche votre page et donne accès à Teams informations spécifiques, par exemple le client Teams exécute le thème foncé.

Que vous choisissiez d’exposer votre onglet dans le canal ou le groupe, ou dans l’étendue personnelle, vous devez présenter une page de contenu HTML <\> iFrame dans votre onglet. [](~/tabs/how-to/create-tab-pages/content-page.md) Pour les onglets personnels, l’URL de contenu est définie directement dans Teams manifeste de l’application par la propriété `contentUrl` dans le `staticTabs` tableau. Le contenu de votre onglet est le même pour tous les utilisateurs.

Pour les onglets de canal ou de groupe, vous pouvez également créer une page de configuration supplémentaire. Cette page vous permet de configurer l’URL de la page de contenu, généralement en utilisant des paramètres de chaîne de requête d’URL pour charger le contenu approprié pour ce contexte. Cela est dû au fait que votre onglet de canal ou de groupe peut être ajouté à plusieurs conversations d’équipe ou de groupe. Lors de chaque installation ultérieure, vos utilisateurs peuvent configurer l’onglet, ce qui vous permet d’adapter l’expérience selon les besoins. Lorsque les utilisateurs ajoutent ou configurent un onglet, une URL est associée à l’onglet présenté dans l’interface Teams’utilisateur. La configuration d’un onglet ajoute simplement des paramètres supplémentaires à cette URL. Par exemple, lorsque vous ajoutez l’onglet Azure Boards, la page de configuration vous permet de choisir la carte à laquelle l’onglet se charge. L’URL de la page de configuration est spécifiée par la  `configurationUrl` propriété dans le tableau dans le manifeste de votre `configurableTabs` application.

Vous pouvez avoir plusieurs canaux ou onglets de groupe et jusqu’à 16 onglets personnels par application.

## <a name="see-also"></a>Voir aussi

* [Demande des autorisations d’appareil](../concepts/device-capabilities/native-device-permissions.md)
* [Intégrer les fonctionnalités médias](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Intégrer une QR ou un scanneur de code-barres](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Intégrer les fonctionnalités d’emplacement](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Conditions préalables](~/tabs/how-to/tab-requirements.md)
