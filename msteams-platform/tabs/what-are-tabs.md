---
title: Qu’est-ce que les onglets personnalisés dans Teams ?
author: laujan
description: Vue d’ensemble des onglets personnalisés sur la plateforme Teams
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: d72d70ac97a7da427f22ef7e84c73f235dc395c6
ms.sourcegitcommit: f6e4a303828224a702138753a8e5e27c8a094c82
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/24/2021
ms.locfileid: "51176962"
---
# <a name="what-are-microsoft-teams-tabs"></a>Qu’est-ce que les onglets Microsoft Teams ?

Les onglets sont des pages web sensibles à Teams incorporées dans Microsoft Teams. Il s’agit de balises html <iframe simples qui pointent vers des domaines déclarés dans le manifeste de l’application et qui peuvent être ajoutées dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur \> individuel. Vous pouvez inclure des onglets personnalisés avec votre application pour incorporer votre propre contenu web dans Teams ou ajouter des fonctionnalités spécifiques à Teams à votre contenu web. *Voir le* [SDK client JavaScript teams.](/javascript/api/overview/msteams-client)

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

Que vous choisissiez d’exposer votre onglet dans l’étendue canal/groupe ou personnelle, vous devez présenter une page de contenu HTML <iFrame dans \> votre onglet. [](~/tabs/how-to/create-tab-pages/content-page.md) Pour les onglets personnels, l’URL de contenu est définie directement dans le manifeste de votre application Teams par la `contentUrl` propriété dans le `staticTabs` tableau. Le contenu de votre onglet sera le même pour tous les utilisateurs.

Pour les onglets de canal/groupe, vous devez également créer une page de configuration supplémentaire qui permet aux utilisateurs de configurer l’URL de votre page de contenu, généralement à l’aide des paramètres de chaîne de requête URL pour charger le contenu approprié pour ce contexte. Cela est dû au fait que votre onglet canal/groupe peut être ajouté à plusieurs équipes ou conversations de groupe différentes. Lors de chaque installation ultérieure, vos utilisateurs pourront configurer l’onglet, ce qui vous permettra d’adapter l’expérience selon vos besoins. Lorsque les utilisateurs ajoutent ou configurent un onglet, une URL est associée à l’onglet présenté dans l’interface utilisateur teams. La configuration d’un onglet consiste simplement à ajouter des paramètres supplémentaires à cette URL. Par exemple, lorsque vous ajoutez l’onglet Tableaux Azure, la page de configuration vous permet de choisir le tableau que l’onglet charge. L’URL de la page de configuration est spécifiée par la  `configurationUrl` propriété dans le tableau dans le manifeste de votre `configurableTabs` application.

Vous pouvez avoir plusieurs canaux ou onglets de groupe, et jusqu’à 16 onglets personnels par application.

## <a name="mobile-clients"></a>Clients mobiles

Si vous choisissez que votre onglet de canal ou de groupe apparaisse sur les clients mobiles Teams, la configuration doit avoir une valeur `setSettings()` pour la `websiteUrl` propriété. Pour garantir une expérience utilisateur optimale, vous devez suivre les instructions pour les [onglets](~/tabs/design/tabs-mobile.md) mobiles lors de la création de vos onglets. Les applications [distribuées via Appsource](~/concepts/deploy-and-publish/appsource/publish.md) ont un processus d’approbation distinct pour les clients mobiles. Le comportement par défaut de ces applications est le suivant :

| **Type d’onglet** | **Comportement de l’application si elle est optimisée pour les clients mobiles** | **Comportement de l’application si elle n’est pas optimisée pour les clients mobiles** |
|:-----|:-----|:-----|
| **Onglets statiques** ou **onglets personnels**|L’application apparaît dans la barre inférieure des clients mobiles. Les onglets s’ouvrent dans une vue web dans l’application dans le client Teams. | L’application ne s’affiche pas dans les clients mobiles. |
| **Onglets configurables** | Les onglets s’ouvrent dans une vue web dans l’application dans le client Teams à l’aide du `contentUrl` . | La sélection **de l’onglet** ouvre le contenu à l’aide du navigateur `websiteUrl` web par défaut sur l’appareil. |


> [!NOTE]
>
> * [Les applications soumises à AppSource pour publication sur Teams ](../concepts/deploy-and-publish/overview.md#publish-to-appsource) sont évaluées automatiquement pour la réactivité mobile. Pour toutes les requêtes, teamsubm@microsoft.com.
> * Pour toutes les applications qui ne sont pas distribuées via [AppSource,](../concepts/deploy-and-publish/overview.md)les onglets s’ouvrent dans une vue web dans l’application dans les clients Teams par défaut et aucun processus d’approbation distinct n’est requis.

> [!div class="nextstepaction"]
> [En savoir plus : Demander des autorisations d’appareil](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [En savoir plus : intégrer des fonctionnalités multimédias](../concepts/device-capabilities/mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [En savoir plus : intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams](../concepts/device-capabilities/qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [En savoir plus : intégrer les fonctionnalités d’emplacement dans Teams](../concepts/device-capabilities/location-capability.md)
