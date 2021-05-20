---
title: Quels sont les onglets personnalisés dans Teams?
author: laujan
description: Un aperçu des onglets personnalisés sur la plate Teams plateforme
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 19c51d5c30f938dc5368b28b69ffeb29330887b4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566592"
---
# <a name="microsoft-teams-tabs"></a>Onglets Microsoft Teams

Les onglets sont Teams web conscientes des paramètres intégrés dans Microsoft Teams. Il s’agit de balises html <iframe simples \> qui pointent vers des domaines déclarés dans le manifeste de l’application et peuvent être ajoutées dans le cadre d’un canal à l’intérieur d’une équipe, d’un chat de groupe ou d’une application personnelle pour un utilisateur individuel. Vous pouvez inclure des onglets personnalisés avec votre application pour intégrer votre propre contenu Web dans Teams ou ajouter des fonctionnalités spécifiques Teams à votre contenu Web. Pour plus d’informations, [Teams client JavaScript SDK](/javascript/api/overview/msteams-client).

Il existe deux types d’onglets disponibles dans Teams : canal/groupe et personnel. Les onglets canal/groupe fournissent du contenu aux canaux et aux chats de groupe, et sont un excellent moyen de créer des espaces collaboratifs autour de contenus web dédiés. Les onglets personnels, ainsi que les bots à portée personnelle, font partie d’applications personnelles et sont étendues à un seul utilisateur. Ils peuvent être épinglés à la barre de navigation gauche pour un accès facile.

## <a name="tab-features"></a>Caractéristiques de l’onglet

> [!div class="checklist"]
>
> * Si un onglet est ajouté à une application qui a également un bot, le bot est également ajouté à l’équipe.
> * Sensibilisation à Azure Active Directory ID (Azure AD) de l’utilisateur actuel.
> * Sensibilisation locale pour l’utilisateur d’indiquer la langue, c’est-à-dire, `en-us` . 
> * Capacité de signalisation unique (SSO), si elle est prise en charge.
> * Possibilité d’utiliser des bots ou des notifications d’application pour un lien profond vers l’onglet ou vers une sous-entité au sein du service, par exemple, un élément de travail individuel.
> * La possibilité d’ouvrir un module de tâches à partir de liens dans un onglet.
> * Réutilisation des SharePoint web dans l’onglet.

## <a name="tabs-user-scenarios"></a>Onglets scénarios utilisateur

**Scénario:** Apportez une ressource web existante à l’intérieur Teams. \
**Exemple :** Vous créez un onglet personnel dans votre application Teams qui présente un site Web d’entreprise d’information aux utilisateurs.

**Scénario:** Ajoutez des pages de support à une extension Teams bot ou de messagerie. \
**Exemple :** Vous créez des onglets personnels qui fournissent *et aident* *le contenu* des pages Web aux utilisateurs.

**Scénario:** Fournissez l’accès à des éléments avec lesquels vos utilisateurs interagissent régulièrement pour un dialogue coopératif et une collaboration. \
**Exemple :** Vous créez un onglet canal/groupe avec un lien profond vers des éléments individuels.

## <a name="understand-how-tabs-work"></a>Comprendre comment fonctionnent les onglets

Un onglet personnalisé est déclaré dans le manifeste d’application de votre package d’application. Pour chaque page Web que vous souhaitez inclure comme onglet dans votre application, vous définissez une URL et une étendue. En outre, vous devez ajouter le [Teams client JavaScript SDK](/javascript/api/overview/msteams-client) à votre page, et `microsoftTeams.initialize()` appeler après que votre page se charge. Cela indiquera à Teams d’afficher votre page, vous donnera accès à des informations spécifiques à Teams (par exemple si le client Teams est en cours d’exécution *du thème sombre),* et vous permettra de prendre des mesures en fonction des résultats.

Que vous choisissiez d’exposer votre onglet dans le canal/groupe ou dans votre champ d’application personnel, vous devrez présenter une page de contenu HTML <iframe \> dans votre onglet. [](~/tabs/how-to/create-tab-pages/content-page.md) Pour les onglets personnels, l’URL de contenu est définie directement dans Teams manifeste de l’application par `contentUrl` la propriété dans le `staticTabs` tableau. Le contenu de votre onglet sera le même pour tous les utilisateurs.

Pour les onglets canal/groupe, vous devez également créer une page de configuration supplémentaire qui permet aux utilisateurs de configurer l’URL de votre page de contenu, généralement en utilisant les paramètres de chaîne de requêtes URL pour charger le contenu approprié pour ce contexte. C’est parce que votre onglet canal/groupe peut être ajouté à plusieurs équipes différentes ou chats de groupe. Lors de chaque installation ultérieure, vos utilisateurs seront en mesure de configurer l’onglet, vous permettant d’adapter l’expérience au besoin. Lorsque les utilisateurs ajoutent ou configurent un onglet, une URL est associée à l’onglet qui est présenté dans l’interface Teams’utilisateur. Configurer un onglet, c’est simplement ajouter des paramètres supplémentaires à cette URL. Par exemple, lorsque vous ajoutez l’onglet Azure Boards, la page de configuration vous permet de choisir le tableau que l’onglet chargera. L’URL de la page de configuration est spécifiée  `configurationUrl` par la propriété dans le tableau dans votre manifeste `configurableTabs` d’application.

Vous pouvez avoir plusieurs canaux ou onglets de groupe, et jusqu’à seize onglets personnels par application.

## <a name="mobile-considerations"></a>Considérations mobiles

Si vous choisissez d’avoir votre onglet canal ou groupe sur Teams clients mobiles, `setSettings()` la configuration doit avoir une valeur pour la `websiteUrl` propriété. Pour garantir une expérience utilisateur optimale, vous devez suivre les conseils [pour les onglets sur mobile lors de](~/tabs/design/tabs-mobile.md) la création de vos onglets. Les [applications distribuées dans le Teams ont](~/concepts/deploy-and-publish/appsource/publish.md) un processus d’approbation distinct pour les clients mobiles. Le comportement par défaut de ces applications est le suivant :

| **Capacité de l’application** | **Comportement si l’application est approuvée** | **Comportement si l’application n’est pas approuvée** |
| --- | --- | --- |
| **Onglets personnels** | L’application apparaît dans la barre inférieure des clients mobiles. Onglets ouverts dans le Teams client. | L’application n’apparaît pas dans la barre inférieure des clients mobiles. |
| **Onglets canal et groupe** | L’onglet s’ouvre dans le Teams client en utilisant `contentUrl` . | L’onglet s’ouvre dans un navigateur en dehors de la Teams client en utilisant `websiteUrl` . |

> [!NOTE]
>
> Le comportement par défaut des applications n’est applicable que s’il est distribué dans Teams magasin. Par défaut, tous les onglets s’ouvrent dans Teams client.
> Pour commencer une évaluation de votre application pour la convivialité mobile, teindez la main pour teamsubm@microsoft.com les détails de votre application.

## <a name="see-also"></a>Voir aussi

* [Demande des autorisations d’appareil](../concepts/device-capabilities/native-device-permissions.md)
* [Intégrer les fonctionnalités médias](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [Intégrer un scanner QR ou code à barres](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Intégrer les fonctionnalités d’emplacement](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Conditions requises pour l’onglet](~/tabs/how-to/tab-requirements.md)