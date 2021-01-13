---
title: Qu’est-ce que les onglets personnalisés dans Teams ?
author: laujan
description: Vue d’ensemble des onglets personnalisés sur la plateforme Teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 64c6e44177f1fb598895f748dbd0ec1c0b1e3aa1
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797889"
---
# <a name="what-are-microsoft-teams-tabs"></a>Qu’est-ce que les onglets Microsoft Teams ?

Les onglets sont des pages web sensibles à Teams incorporées dans Microsoft Teams. Il s’agit de balises iframe HTML <simples qui pointent vers des domaines déclarés dans le manifeste de l’application et qui peuvent être ajoutées dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur \> individuel. Vous pouvez inclure des onglets personnalisés avec votre application pour incorporer votre propre contenu web dans Teams ou ajouter des fonctionnalités spécifiques de Teams à votre contenu web. *Voir le* [SDK client JavaScript teams.](/javascript/api/overview/msteams-client)

> [!NOTE]
> Chrome 80, dont la publication est prévue début 2020, introduit de nouvelles valeurs de cookie et impose des stratégies de cookie par défaut. Il est recommandé de définir l’utilisation prévue pour vos cookies plutôt que de vous appuyer sur le comportement par défaut du navigateur. *Voir* [l’attribut de cookie SameSite (mise à jour 2020).](../resources/samesite-cookie-update.md)

Il existe deux types d’onglets disponibles dans Teams : canal/groupe et personnel. Les onglets de canal/groupe offrent du contenu aux canaux et aux conversations de groupe, et sont un excellent moyen de créer des espaces de collaboration autour de contenu web dédié. Les onglets personnels, ainsi que les bots d’étendue personnelle, font partie des applications personnelles et sont limitées à un seul utilisateur. Ils peuvent être épinglés à la barre de navigation de gauche pour faciliter l’accès.

## <a name="lesser-known-tab-features"></a>Fonctionnalités d’onglet moins connues

> [!div class="checklist"]
>
> * Si un onglet est ajouté à une application qui possède également un bot, le bot est également ajouté à l’équipe.
> * Sensibilisation de l’ID Azure Active Directory (Azure AD) de l’utilisateur actuel.
> * Sensibilisation des paramètres régionaux pour que l’utilisateur indique la langue, c’est-à-dire, `en-us` . 
> * Fonctionnalité d' sign-on unique (SSO), si elle est prise en charge.
> * Possibilité d’utiliser des bots ou des notifications d’application pour créer un lien profond vers l’onglet ou une sous-entité au sein du service, par exemple, un élément de travail individuel.
> * Possibilité d’ouvrir un module de tâche à partir de liens dans un onglet.
> * Réutilisation des composants Web Parts SharePoint dans l’onglet.

## <a name="tabs-user-scenarios"></a>Scénarios utilisateur onglets

**Scénario :** Apportez une ressource web existante dans Teams. \
**Exemple :** Vous créez un onglet personnel dans votre application Teams qui présente un site web d’entreprise d’information aux utilisateurs.

**Scénario :** Ajouter des pages de support à un bot Teams ou une extension de messagerie. \
**Exemple :** Vous créez des onglets personnels qui fournissent des *informations sur les* pages web et aident les utilisateurs. 

**Scénario :** Fournir l’accès aux éléments avec qui vos utilisateurs interagissent régulièrement pour un dialogue et une collaboration collaboratifs collaboratifs. \
**Exemple :** Vous créez un onglet canal/groupe avec un lien profond vers des éléments individuels.

## <a name="how-do-tabs-work"></a>Comment fonctionnent les onglets ?

Un onglet personnalisé est déclaré dans le manifeste de l’application de votre package d’application. Pour chaque page web que vous souhaitez inclure en tant qu’onglet dans votre application, vous définissez une URL et une étendue. En outre, vous devez ajouter le [SDK client JavaScript Teams](/javascript/api/overview/msteams-client) à votre page et appeler après le chargement `microsoftTeams.initialize()` de votre page. Cela indique à Teams d’afficher votre page, de vous donner accès à des informations spécifiques à Teams (par exemple, si le client Teams exécute le thème *foncé)* et vous permet d’agir en fonction des résultats.

Que vous choisissiez d’exposer votre onglet dans l’étendue canal/groupe ou personnelle, vous devez présenter une page de contenu HTML <\> iFrame dans votre onglet. [](~/tabs/how-to/create-tab-pages/content-page.md) Pour les onglets personnels, l’URL de contenu est définie directement dans le manifeste de votre application Teams par la `contentUrl` propriété dans le `staticTabs` tableau. Le contenu de votre onglet sera le même pour tous les utilisateurs.

Pour les onglets de canal/groupe, vous devez également créer une page de configuration supplémentaire qui permet aux utilisateurs de configurer l’URL de votre page de contenu, généralement à l’aide des paramètres de chaîne de requête URL pour charger le contenu approprié pour ce contexte. Cela est dû au fait que votre onglet canal/groupe peut être ajouté à plusieurs équipes ou conversations de groupe différentes. Lors de chaque installation ultérieure, vos utilisateurs pourront configurer l’onglet, ce qui vous permettra d’adapter l’expérience selon vos besoins. Lorsque les utilisateurs ajoutent ou configurent un onglet, une URL est associée à l’onglet présenté dans l’interface utilisateur teams. La configuration d’un onglet consiste simplement à ajouter des paramètres supplémentaires à cette URL. Par exemple, lorsque vous ajoutez l’onglet Tableaux Azure, la page de configuration vous permet de choisir le tableau que l’onglet charge. L’URL de la page de configuration est spécifiée par la  `configurationUrl` propriété dans le tableau dans le manifeste de votre `configurableTabs` application.

Vous pouvez avoir un maximum d’un (1) onglet canal/groupe et jusqu’à 16 (16) onglets personnels par application.

## <a name="mobile-clients"></a>Clients mobiles

Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur les clients mobiles Teams, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété. Pour garantir une expérience utilisateur optimale, vous devez suivre les instructions pour les [onglets](~/tabs/design/tabs-mobile.md) sur mobile lors de la création de vos onglets. Les applications [distribuées via Appsource](~/concepts/deploy-and-publish/appsource/publish.md) ont un processus d’approbation distinct pour les clients mobiles. Le comportement par défaut de ces applications est le suivant :

| **Fonctionnalité d’application** | **Comportement si l’application est approuvée** | **Comportement si l’application n’est pas approuvée** |
| --- | --- | --- |
| **Onglets statiques** | L’application apparaît dans la barre inférieure des clients mobiles. Les onglets s’ouvrent dans le client Teams. | L’application n’apparaît pas dans la barre inférieure des clients mobiles. |
| **Onglets configurables** | L’onglet s’ouvre dans le client Teams à l’aide `contentUrl` de . | L’onglet s’ouvre dans un navigateur en dehors du client Teams à l’aide `websiteUrl` de . |


>[!NOTE]
>
>- Le comportement par défaut des applications s’applique uniquement si elles sont distribuées via AppSource. Il n’existe aucun processus d’approbation pour les applications distribuées via [d’autres méthodes de distribution.](~/concepts/deploy-and-publish/overview.md) Par défaut, tous les onglets s’ouvrent dans le client Teams.
>- Pour lancer une évaluation de votre application pour la convivialité mobile, teamsubm@microsoft.com les détails de votre application.


> [!div class="nextstepaction"]
> [En savoir plus : Demander des autorisations d’appareil](/concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
>[En savoir plus : Autorisations de la galerie d’images et d’appareils photo](/concepts/device-capabilities/mobile-camera-image-permissions.md)
