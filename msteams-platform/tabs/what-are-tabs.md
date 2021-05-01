---
title: Que sont les onglets personnalisés Teams ?
author: laujan
description: Vue d'ensemble des onglets personnalisés sur la plateforme Teams web
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 2cdd431a1c4a5a6b98688bba52d1979f7ced38d7
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101666"
---
# <a name="what-are-microsoft-teams-tabs"></a>Que sont Microsoft Teams onglets ?

Les onglets Teams des pages web sensibles incorporées dans Microsoft Teams. Il s'agit de balises html <iframe simples qui pointent vers des domaines déclarés dans le manifeste de l'application et qui peuvent être ajoutées dans le cadre d'un canal au sein d'une équipe, d'une conversation de groupe ou d'une application personnelle pour un utilisateur \> individuel. Vous pouvez inclure des onglets personnalisés avec votre application pour incorporer votre propre contenu web dans Teams ou ajouter Teams fonctionnalités spécifiques à votre contenu web. *Voir* [Teams SDK client JavaScript.](/javascript/api/overview/msteams-client)

Il existe deux types d'onglets disponibles dans Teams : canal/groupe et personnel. Les onglets de canal/groupe offrent du contenu aux canaux et aux conversations de groupe, et sont un excellent moyen de créer des espaces de collaboration autour de contenu web dédié. Les onglets personnels, ainsi que les bots d'étendue personnelle, font partie des applications personnelles et sont limitées à un seul utilisateur. Ils peuvent être épinglés à la barre de navigation de gauche pour faciliter l'accès.

## <a name="lesser-known-tab-features"></a>Fonctionnalités d'onglet moins connues

> [!div class="checklist"]
>
> * Si un onglet est ajouté à une application qui possède également un bot, le bot est également ajouté à l'équipe.
> * Sensibilisation de l Azure Active Directory (Azure AD) de l'utilisateur actuel.
> * Sensibilisation des paramètres régionaux pour que l'utilisateur indique la langue, c'est-à-dire, `en-us` . 
> * Fonctionnalité d' sign-on unique (SSO), si elle est prise en charge.
> * Possibilité d'utiliser des bots ou des notifications d'application pour créer un lien profond vers l'onglet ou une sous-entité au sein du service, par exemple, un élément de travail individuel.
> * Possibilité d'ouvrir un module de tâche à partir de liens dans un onglet.
> * Réutilisation des SharePoint web dans l'onglet.

## <a name="tabs-user-scenarios"></a>Scénarios utilisateur onglets

**Scénario :** Apportez une ressource web existante à l'Teams. \
**Exemple :** Vous créez un onglet personnel dans votre application Teams qui présente un site web d'entreprise d'information aux utilisateurs.

**Scénario :** Ajoutez des pages de support à un bot Teams ou une extension de messagerie. \
**Exemple :** Vous créez des onglets personnels qui fournissent des *informations sur les* pages web et aident les utilisateurs. 

**Scénario :** Fournir l'accès aux éléments avec qui vos utilisateurs interagissent régulièrement pour un dialogue et une collaboration collaboratifs collaboratifs. \
**Exemple :** Vous créez un onglet canal/groupe avec un lien profond vers des éléments individuels.

## <a name="how-do-tabs-work"></a>Comment fonctionnent les onglets ?

Un onglet personnalisé est déclaré dans le manifeste de l'application de votre package d'application. Pour chaque page web que vous souhaitez inclure en tant qu'onglet dans votre application, vous définissez une URL et une étendue. En outre, vous devez ajouter le [SDK Teams client JavaScript](/javascript/api/overview/msteams-client) à votre page et appeler après le chargement `microsoftTeams.initialize()` de votre page. Cela indique à Teams d'afficher votre page, de vous donner accès à des informations spécifiques à Teams (par exemple, si le client Teams exécute le thème *foncé)* et vous permet d'agir en fonction des résultats.

Que vous choisissiez d'exposer votre onglet dans l'étendue canal/groupe ou personnelle, vous devez présenter une page de contenu HTML <iFrame dans \> votre onglet. [](~/tabs/how-to/create-tab-pages/content-page.md) Pour les onglets personnels, l'URL de contenu est définie directement dans Teams manifeste de l'application par la propriété `contentUrl` dans le `staticTabs` tableau. Le contenu de votre onglet sera le même pour tous les utilisateurs.

Pour les onglets de canal/groupe, vous devez également créer une page de configuration supplémentaire qui permet aux utilisateurs de configurer l'URL de votre page de contenu, généralement à l'aide des paramètres de chaîne de requête URL pour charger le contenu approprié pour ce contexte. Cela est dû au fait que votre onglet canal/groupe peut être ajouté à plusieurs équipes ou conversations de groupe différentes. Lors de chaque installation ultérieure, vos utilisateurs pourront configurer l'onglet, ce qui vous permettra d'adapter l'expérience selon vos besoins. Lorsque les utilisateurs ajoutent ou configurent un onglet, une URL est associée à l'onglet présenté dans l Teams'interface utilisateur. La configuration d'un onglet consiste simplement à ajouter des paramètres supplémentaires à cette URL. Par exemple, lorsque vous ajoutez l'onglet Azure Boards, la page de configuration vous permet de choisir la carte que l'onglet charge. L'URL de la page de configuration est spécifiée par la  `configurationUrl` propriété dans le tableau dans le manifeste de votre `configurableTabs` application.

Vous pouvez avoir plusieurs canaux ou onglets de groupe, et jusqu'à 16 onglets personnels par application.

## <a name="mobile-considerations"></a>Considérations sur les appareils mobiles

Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur Teams clients mobiles, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété. Pour garantir une expérience utilisateur optimale, vous devez suivre les instructions pour les [onglets](~/tabs/design/tabs-mobile.md) sur mobile lors de la création de vos onglets. Les [applications distribuées via Teams store ont](~/concepts/deploy-and-publish/appsource/publish.md) un processus d'approbation distinct pour les clients mobiles. Le comportement par défaut de ces applications est le suivant :

| **Fonctionnalité de l'application** | **Comportement si l'application est approuvée** | **Comportement si l'application n'est pas approuvée** |
| --- | --- | --- |
| **Onglets personnels** | L'application apparaît dans la barre inférieure des clients mobiles. Les onglets s'ouvrent dans Teams client. | L'application n'apparaît pas dans la barre inférieure des clients mobiles. |
| **Onglets de canal et de groupe** | L'onglet s'ouvre dans le Teams client à l'aide `contentUrl` de . | L'onglet s'ouvre dans un navigateur en dehors du Teams client à `websiteUrl` l'aide. |

> [!NOTE]
>
> Le comportement par défaut des applications s'applique uniquement s'il est distribué via Teams store. Par défaut, tous les onglets s'ouvrent dans le client Teams client.
> Pour lancer une évaluation de votre application pour la convivialité mobile, teamsubm@microsoft.com les détails de votre application.

## <a name="see-also"></a>Voir aussi

* [Demande des autorisations d’appareil](../concepts/device-capabilities/native-device-permissions.md)
* [Intégrer les fonctionnalités médias](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Intégrer une QR ou un scanneur de code-barres](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Intégrer les fonctionnalités d’emplacement](../concepts/device-capabilities/location-capability.md)
