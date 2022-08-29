---
title: Onglets Microsoft Teams
author: surbhigupta
description: Apprenez à créer des onglets, des pages web incorporées dans Microsoft Teams. Créez une page de contenu dans le cadre de l’onglet personnel, canal ou groupe. Apprenez également à créer des onglets avec des cartes adaptatives.
ms.localizationpriority: high
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: d175e9c1a9f8515db57c54503fd3f83cb7970777
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450393"
---
# <a name="build-tabs-for-teams"></a>Créer des onglets pour Teams

Les onglets Teams des pages web sensibles incorporées dans Microsoft Teams. Ce sont de balises HTML `<iframe\>` simples qui pointent vers des domaines déclarés dans le manifeste de l’application et peuvent être ajoutées dans le cadre d’un canal au sein d’une équipe, d’une conversation de groupe ou d’une application personnelle pour un utilisateur individuel. Vous pouvez inclure des onglets personnalisés avec votre application pour incorporer votre propre contenu web dans Teams ou ajouter des fonctionnalités Teams spécifiques à votre contenu web. Pour plus d’informations, consultez [Kit de développement logiciel (SDK) client JavaScript Teams](/javascript/api/overview/msteams-client).

> [!IMPORTANT]
> Actuellement, les onglets personnalisés sont disponibles dans le Cloud de la communauté du secteur public (GCC), Cloud de la communauté du secteur public-High (GCC-High), et le Département de la Défense (DOD).

L’image suivante montre les onglets personnels :

:::image type="content" source="../assets/images/tabs/personaltab.png" alt-text="Onglet personnel" lightbox="../assets/images/tabs/personaltab.png":::

L’image suivante montre les onglets du canal Contoso :

:::image type="content" source="../assets/images/tabs/tabs.png" alt-text="Onglets de canal ou de groupe" lightbox="../assets/images/tabs/tabs.png":::

Il existe quelques conditions préalables que vous devez respecter avant de travailler sur des onglets.

Deux types d’onglets sont disponibles dans Teams, personnel et canal ou groupe. [Les onglets personnels](~/tabs/how-to/create-personal-tab.md), ainsi que les bots d’étendue personnelle, font partie des applications personnelles et sont limités à un seul utilisateur. Ils peuvent être épinglés à la barre de navigation de gauche pour faciliter l’accès. [Les onglets de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md) offrent du contenu aux canaux et aux conversations de groupe, et sont un excellent moyen de créer des espaces de collaboration autour de contenu web dédié.

Vous pouvez [créer une page de contenu](~/tabs/how-to/create-tab-pages/content-page.md) dans le cadre d’un onglet personnel, d’un onglet de canal ou de groupe ou d’un module de tâche. Vous pouvez [créer une page de configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) qui permet aux utilisateurs de configurer une application Microsoft Teams et de l’utiliser pour configurer un onglet de conversation de canal ou de groupe, une extension de messagerie ou un connecteur Office 365. Vous pouvez permettre aux utilisateurs de reconfigurer votre onglet après l’installation et de [créer une page de suppression d’onglets](~/tabs/how-to/create-tab-pages/removal-page.md) pour votre application. Lorsque vous créez une application Teams qui inclut un onglet, vous devez tester le [fonctionnement de votre onglet sur les clients de Teams Android et iOS](~/tabs/design/tabs-mobile.md). Votre onglet doit [obtenir le contexte ](~/tabs/how-to/access-teams-context.md)par le biais d’informations de base, de paramètres régionaux et des informations de thèmes, ainsi que `entityId` ou `subEntityId` qui identifie ce qui se trouve dans l’onglet.

Vous pouvez créer des onglets avec des cartes adaptatives et centraliser toutes les fonctionnalités de l’application Teams en éliminant la nécessité d’un autre système principal pour vos bots et onglets. [Vue des étapes](~/tabs/tabs-link-unfurling.md) est un nouveau composant d’interface utilisateur qui vous permet d’afficher le contenu ouvert en plein écran dans Teams et épinglé sous forme d’onglet. Le service de [déploiement de lien](~/tabs/tabs-link-unfurling.md) existant est mis à jour, de sorte qu’il est utilisé pour transformer les URL en onglet à l’aide d’une carte adaptative et des services de conversation. Vous pouvez [créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md) à l’aide de sous-entités de conversation qui permettent aux utilisateurs d’avoir des conversations sur des sous-entités dans votre onglet, telles que des tâches spécifiques, des patients et des opportunités de vente, au lieu de discuter de l’onglet entier. Vous pouvez modifier les [marges des onglets](~/resources/removing-tab-margins.md) pour améliorer l’expérience du développeur lors de la création d’applications. Vous pouvez faire glisser l’onglet et le placer à la position souhaitée pour échanger les positions de tabulation dans vos applications personnelles et conversations de canal ou de groupe.

> [!NOTE]
> Les **publications** et **fichiers** ne peuvent pas être déplacés de leur position.

## <a name="tab-features"></a>Fonctionnalités de l’onglet

Les fonctionnalités de l’onglet sont les suivantes :

* Si un onglet est ajouté à une application qui possède également un bot, le bot est également ajouté à l’équipe.
* Sensibilisation de l’ID Microsoft Azure Active Directory (Azure AD) de l’utilisateur actuel.
* Sensibilisation des paramètres régionaux pour que l’utilisateur indique la langue qui est `en-us`
* Fonctionnalité d' authentification unique (SSO), si prise en charge.
* Possibilité d’utiliser des bots ou des notifications d’application pour créer un lien profond vers l’onglet ou une sous-entité au sein du service, par exemple un élément de travail individuel.
* Possibilité d’ouvrir un module de tâche à partir de liens dans un onglet.
* Réutilisation des composants WebParts SharePoint dans l’onglet.

## <a name="tabs-user-scenarios"></a>Scénarios utilisateur des onglets

**Scénario :** Apportez une ressource web existante dans Teams. \
**Exemple :** Vous créez un onglet personnel dans votre application Teams qui présente un site web d’entreprise d’information aux utilisateurs.

**Scénario :** Ajouter des pages de support à un bot Teams ou une extension de messagerie. \
**Exemple :** Vous créez des onglets personnels qui fournissent des **sur** et **aide** au contenu des pages web aux utilisateurs.

**Scénario :** Fournir l’accès aux éléments avec qui vos utilisateurs interagissent régulièrement à des fins de dialogue et de collaboration collaboratifs. \
**Exemple :** Vous créez un onglet de canal ou de groupe avec un lien profond vers des éléments individuels.

## <a name="understand-how-tabs-work"></a>Comprendre le fonctionnement des onglets

Vous pouvez utiliser l’une des méthodes suivantes pour créer des onglets :

* [Déclarer un onglet personnalisé dans le manifeste de l’application](#declare-custom-tab-in-app-manifest)
* [Utiliser la carte adaptative pour créer des onglets](~/tabs/how-to/build-adaptive-card-tabs.md)

### <a name="declare-custom-tab-in-app-manifest"></a>Déclarer un onglet personnalisé dans le manifeste de l’application

Un onglet personnalisé est déclaré dans le manifeste de l’application de votre package d’application. Pour chaque page web que vous souhaitez inclure en tant qu’onglet dans votre application, vous définissez une URL et une étendue. En outre, vous pouvez ajouter le [SDK client JavaScript Teams](/javascript/api/overview/msteams-client) à votre page, et appeler `microsoftTeams.initialize()`après le chargement de votre page. Teams affiche votre page et donne accès à des informations spécifiques à Teams, par exemple le client Teams exécute le thème sombre.

Que vous choisissiez d’exposer votre onglet au sein du canal ou du groupe, ou dans une portée personnelle, vous devez présenter une \>[page de contenu](~/tabs/how-to/create-tab-pages/content-page.md) HTML <iframe dans votre onglet. Pour les onglets personnels, l’URL de contenu est définie directement dans le manifeste de votre application Teams par la propriété `contentUrl` du tableau `staticTabs`. Le contenu de votre onglet est le même pour tous les utilisateurs.

Pour les onglets de canal ou de groupe, vous pouvez également créer une page de configuration supplémentaire. Cette page vous permet de configurer l’URL de la page de contenu, généralement à l’aide de paramètres de chaîne de requête d’URL pour charger le contenu approprié pour ce contexte. Cela est dû au fait que votre onglet de canal ou de groupe peut être ajouté à plusieurs conversations d’équipe ou de groupe. À chaque installation ultérieure, vos utilisateurs peuvent configurer l’onglet, ce qui vous permet d’adapter l’expérience selon les besoins. Lorsque les utilisateurs ajoutent ou configurent un onglet, une URL est associée à l’onglet présenté dans l’interface utilisateur Teams. La configuration d’un onglet ajoute simplement des paramètres supplémentaires à cette URL. Par exemple, lorsque vous ajoutez l’onglet Azure Boards, la page de configuration vous permet de choisir le tableau chargé par l’onglet. L’URL de la page de configuration est spécifiée par la `configurationUrl` propriété dans le `configurableTabs`tableau dans le manifeste de votre application.

Vous pouvez avoir plusieurs canaux ou onglets de groupe, et jusqu’à 16 onglets personnels par application.

### <a name="tools-to-build-tabs"></a>Outils pour créer des onglets

* [Kit de ressources Microsoft Teams pour Microsoft Visual Studio Code](../toolkit/visual-studio-code-overview.md)
* [Extension de kit de ressources Teams pour Visual Studio](../toolkit/visual-studio-overview.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Conditions préalables](~/tabs/how-to/tab-requirements.md)

## <a name="see-also"></a>Voir aussi

* [Onglets personnalisés dans Microsoft Teams](/microsoftteams/built-in-custom-tabs#develop-custom-tabs)
* [Demande des autorisations d’appareil](../concepts/device-capabilities/native-device-permissions.md)
* [Intégrer les fonctionnalités médias](../concepts/device-capabilities/media-capabilities.md)
* [Intégrer un détecteur de QR ou de code-barres](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [Intégrer les fonctionnalités d’emplacement](../concepts/device-capabilities/location-capability.md)
* [Onglets sur les appareils mobiles](design/tabs-mobile.md#tabs-on-mobile)
