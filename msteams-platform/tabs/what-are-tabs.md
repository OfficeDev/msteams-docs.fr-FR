---
title: Que sont les onglets personnalisés Teams ?
author: surbhigupta
description: Vue d’ensemble des onglets personnalisés sur la plateforme Teams web
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 792604c7763628ce0d45b332064e23c14e94aeb2
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069196"
---
# <a name="microsoft-teams-tabs"></a>Onglets Microsoft Teams

Les onglets Teams des pages web sensibles incorporées dans Microsoft Teams. Il s’agit de balises html <iframe simples qui pointent vers des domaines déclarés dans le manifeste de l’application et qui peuvent être ajoutées dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur \> individuel. Vous pouvez inclure des onglets personnalisés avec votre application pour incorporer votre propre contenu web dans Teams ou ajouter Teams fonctionnalités spécifiques à votre contenu web. Pour plus d’informations, [Teams SDK client JavaScript.](/javascript/api/overview/msteams-client)

Deux types d’onglets sont disponibles dans Teams : canal/groupe et personnel. Les onglets de canal/groupe offrent du contenu aux canaux et aux conversations de groupe, et sont un excellent moyen de créer des espaces de collaboration autour de contenu web dédié. Les onglets personnels, ainsi que les bots d’étendue personnelle, font partie des applications personnelles et sont limitées à un seul utilisateur. Ils peuvent être épinglés à la barre de navigation de gauche pour faciliter l’accès.

## <a name="tab-features"></a>Fonctionnalités de l’onglet

> [!div class="checklist"]
>
> * Si un onglet est ajouté à une application qui possède également un bot, le bot est également ajouté à l’équipe.
> * Sensibilisation de l Azure Active Directory (Azure AD) de l’utilisateur actuel.
> * Sensibilisation des paramètres régionaux pour que l’utilisateur indique la langue, c’est-à-dire, `en-us` . 
> * Fonctionnalité d' sign-on unique (SSO), si elle est prise en charge.
> * Possibilité d’utiliser des bots ou des notifications d’application pour créer un lien profond vers l’onglet ou une sous-entité au sein du service, par exemple, un élément de travail individuel.
> * Possibilité d’ouvrir un module de tâche à partir de liens dans un onglet.
> * Réutilisation des SharePoint web dans l’onglet.

## <a name="tabs-user-scenarios"></a>Scénarios utilisateur onglets

**Scénario :** Apportez une ressource web existante à l’Teams. \
**Exemple :** Vous créez un onglet personnel dans votre application Teams qui présente un site web d’entreprise d’information aux utilisateurs.

**Scénario :** Ajouter des pages de support à un bot Teams’extension de messagerie. \
**Exemple :** Vous créez des onglets personnels qui fournissent des *informations sur les* pages web et aident les utilisateurs. 

**Scénario :** Fournir l’accès aux éléments avec qui vos utilisateurs interagissent régulièrement pour le dialogue et la collaboration collaboratifs. \
**Exemple :** Vous créez un onglet canal/groupe avec un lien profond vers des éléments individuels.

## <a name="understand-how-tabs-work"></a>Comprendre le fonctionnement des onglets

Vous pouvez utiliser l’une des méthodes suivantes pour créer des onglets :
* [Déclarer un onglet personnalisé dans le manifeste de l’application](#declare-custom-tab-in-app-manifest)
* [Utiliser la carte adaptative pour créer des onglets](#use-adaptive-card-to-build-tabs)

### <a name="declare-custom-tab-in-app-manifest"></a>Déclarer un onglet personnalisé dans le manifeste de l’application

Un onglet personnalisé est déclaré dans le manifeste de l’application de votre package d’application. Pour chaque page web que vous souhaitez inclure en tant qu’onglet dans votre application, vous définissez une URL et une étendue. En outre, vous devez ajouter le [SDK Teams client JavaScript](/javascript/api/overview/msteams-client) à votre page et appeler après le chargement `microsoftTeams.initialize()` de votre page. Cela indique à Teams d’afficher votre page, vous donne accès à des informations spécifiques à Teams (par exemple, si le client Teams exécute le thème *foncé)* et vous permet d’agir en fonction des résultats.

Que vous choisissiez d’exposer votre onglet dans l’étendue canal/groupe ou personnelle, vous devez présenter une page de contenu HTML <iFrame dans \> votre onglet. [](~/tabs/how-to/create-tab-pages/content-page.md) Pour les onglets personnels, l’URL de contenu est définie directement dans Teams manifeste de l’application par la propriété `contentUrl` dans le `staticTabs` tableau. Le contenu de votre onglet sera le même pour tous les utilisateurs.

Pour les onglets de canal/groupe, vous devez également créer une page de configuration supplémentaire qui permet aux utilisateurs de configurer l’URL de votre page de contenu, généralement à l’aide des paramètres de chaîne de requête URL pour charger le contenu approprié pour ce contexte. Cela est dû au fait que votre onglet canal/groupe peut être ajouté à plusieurs conversations d’équipe ou de groupe différentes. Lors de chaque installation ultérieure, vos utilisateurs pourront configurer l’onglet, ce qui vous permettra d’adapter l’expérience selon vos besoins. Lorsque les utilisateurs ajoutent ou configurent un onglet, une URL est associée à l’onglet présenté dans l Teams’interface utilisateur. La configuration d’un onglet consiste simplement à ajouter des paramètres supplémentaires à cette URL. Par exemple, lorsque vous ajoutez l’onglet Azure Boards, la page de configuration vous permet de choisir la carte que l’onglet charge. L’URL de la page de configuration est spécifiée par la  `configurationUrl` propriété dans le tableau dans le manifeste de votre `configurableTabs` application.

Vous pouvez avoir plusieurs canaux ou onglets de groupe, et jusqu’à 16 onglets personnels par application.


### <a name="use-adaptive-card-to-build-tabs"></a>Utiliser la carte adaptative pour créer des onglets

Lorsque vous développez un onglet à l’aide de la méthode traditionnelle, vous devez tenir compte d’éléments, tels que le code HTML, les considérations CSS pour vous sentir natifs, les temps de chargement lents, les contraintes iFrame, la maintenance du serveur et les coûts, etc. Les onglets de carte adaptative sont un nouveau moyen de créer des onglets dans Teams. Au lieu d’incorporer du contenu web dans un iframe, vous pouvez restituer la carte adaptative dans un onglet. Alors que le frontal est restituer en tant que carte adaptative, le système frontal est alimenté par un bot. Le bot est responsable de l’acceptation des demandes et de la réponse appropriée avec la carte adaptative pour le rendu.

## <a name="mobile-clients"></a>Clients mobiles

Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur Teams clients mobiles, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété. Pour garantir une expérience utilisateur optimale, vous devez suivre les instructions pour les [onglets](~/tabs/design/tabs-mobile.md) sur mobile lors de la création de vos onglets. Les [applications distribuées via Teams store ont](~/concepts/deploy-and-publish/appsource/publish.md) un processus d’approbation distinct pour les clients mobiles. Le comportement par défaut de ces applications est le suivant :

| **Fonctionnalité d’application** | **Comportement si l’application est approuvée** | **Comportement si l’application n’est pas approuvée** |
| --- | --- | --- |
| **Onglets personnels** | L’application apparaît dans la barre inférieure des clients mobiles. Les onglets s’ouvrent dans Teams client. | L’application n’apparaît pas dans la barre inférieure des clients mobiles. |
| **Onglets de canal et de groupe** | L’onglet s’ouvre dans le Teams client à l’aide `contentUrl` de . | L’onglet s’ouvre dans un navigateur en dehors du Teams client à `websiteUrl` l’aide. |

> [!NOTE]
> [Les applications soumises à AppSource](../concepts/deploy-and-publish/overview.md#publish-to-appsource) pour publication sur Teams sont évaluées automatiquement pour la réactivité mobile. Pour toutes les requêtes, teamsubm@microsoft.com.
> Pour toutes les applications qui ne sont pas distribuées via [AppSource,](../concepts/deploy-and-publish/overview.md)les onglets s’ouvrent dans une vue web dans l’application au sein des clients Teams par défaut et aucun processus d’approbation distinct n’est requis.
> 
> Le comportement par défaut des applications est applicable uniquement s’il est distribué via Teams store. Par défaut, tous les onglets s’ouvrent dans Teams client.
> Pour lancer une évaluation de votre application pour la convivialité mobile, teamsubm@microsoft.com les détails de votre application.

## <a name="see-also"></a>Voir aussi

* [Demande des autorisations d’appareil](../concepts/device-capabilities/native-device-permissions.md)
* [Intégrer les fonctionnalités médias](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Intégrer une QR ou un scanneur de code-barres](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Intégrer les fonctionnalités d’emplacement](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Conditions requises pour l’onglet](~/tabs/how-to/tab-requirements.md)
