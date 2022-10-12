---
title: Vue d’ensemble Live Share
author: surbhigupta
description: Dans ce module, découvrez ce qu’est le Kit de développement logiciel (SDK) Microsoft Live Share et ses scénarios utilisateur.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 38157dea1c2d24b82cf1f48829639fd1d92392c1
ms.sourcegitcommit: 0fa0bc081da05b2a241fd8054488d9fd0104e17b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2022
ms.locfileid: "68552526"
---
---

# <a name="live-share-sdk"></a>FAQ sur le Kit de développement logiciel (SDK) de Live Share

> [!VIDEO https://www.youtube.com/embed/971YIvosuUk]

Live Share est un Kit de développement logiciel (SDK) conçu pour transformer Teams applications en expériences multi-utilisateurs collaboratives sans écrire de code principal dédié. Avec Live Share, vos utilisateurs peuvent co-regarder, co-créer et co-modifier pendant les réunions.

Parfois, le partage d’écran ne suffit pas, c’est pourquoi Microsoft a créé des outils tels que PowerPoint Live et tableau blanc directement dans Teams. En plaçant votre application web directement au centre de l’interface de réunion, vos utilisateurs peuvent collaborer en toute transparence pendant les réunions et les appels.

> [!div class="nextstepaction"]
> [Prise en main](teams-live-share-quick-start.md)

## <a name="feature-overview"></a>Vue d’ensemble des fonctionnalités

Live Share propose trois packages qui prennent en charge des scénarios collaboratifs illimités. Ces packages exposent un ensemble de structures de données distribuées (DDS), y compris des blocs de construction primitifs et des scénarios clés en la matière.

Live Share intègre en toute transparence les réunions à [Fluid Framework](https://fluidframework.com/). Infrastructure Fluid est une collection de bibliothèques clientes permettant de distribuer et de synchroniser l’état partagé. Live Share fournit un relais [Azure Fluid](/azure/azure-fluid-relay/) gratuit, entièrement managé et prêt à l’emploi, soutenu par la sécurité et l’échelle mondiale de Teams.

### <a name="live-share-core"></a>Live Share Core

Live Share permet de se connecter à un conteneur Fluid spécial associé à chaque réunion en quelques lignes de code. Outre les structures de données fournies par Fluid Framework, Live Share prend également en charge un nouvel ensemble de classes DDS pour simplifier la synchronisation de l’état de l’application dans les réunions.

Les fonctionnalités prises en charge par le package de base Live Share sont les suivantes :

- Participez à la session Live Share d’une réunion avec `LiveShareClient`.
- Suivez la présence de la réunion et synchronisez les métadonnées utilisateur avec `LivePresence`.
- Envoyez des événements en temps réel à d’autres clients de la session avec `LiveEvent`.
- Coordonner l’état de l’application qui disparaît lorsque les utilisateurs quittent la session avec `LiveState`.
- Synchronisez un minuteur de compte à rebours avec `LiveTimer`.
- Tirez parti de n’importe quelle fonctionnalité de Fluid Framework, telle que `SharedMap` .`SharedString`

Vous trouverez plus d’informations sur ce package dans la [page des fonctionnalités principales](./teams-live-share-capabilities.md).

### <a name="live-share-media"></a>Live Share Media

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="Expérience de partage de vidéos Live Share":::

La vidéo et l’audio sont des parties instrumentales du monde moderne et du lieu de travail. Live Share Media permet la **synchronisation de média** pour n’importe quel lecteur multimédia avec seulement quelques lignes de code. En synchronisant le média à l’état du lecteur et la couche de contrôles de transport, vous pouvez attribuer individuellement des vues, tout en fournissant la qualité la plus élevée possible disponible via votre application. Étant donné que Microsoft ne retranscrit pas votre contenu multimédia, vos exigences en matière de licences et d’accès sont conservées intactes.

Les fonctionnalités prises en charge par les médias Live Share sont les suivantes :

- Synchronisez l’état du lecteur multimédia et suivez avec `MediaPlayerSynchronizer`.
- Ajustements intelligents du volume multimédia au fur et à mesure que les utilisateurs parlent pendant la réunion.
- Limitez les utilisateurs qui peuvent modifier l’état du lecteur.
- Suspendez et reprenez la synchronisation des médias à la volée ou aux points d’attente planifiés.

Vous trouverez plus d’informations sur ce package sur la [page multimédia Live Share](./teams-live-share-media-capabilities.md).

> [!NOTE]
> Live Share ne retranscrit pas le contenu multimédia. Il est conçu pour être utilisé avec des lecteurs web incorporés, tels que HTML5 `<video>` ou Azure Media Player.

### <a name="live-share-canvas"></a>Canevas Live Share

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Live Share Teams":::

Lors de la collaboration dans des réunions, il est essentiel que les utilisateurs puissent faire ressortir et mettre en évidence le contenu à l’écran. Le canevas Live Share facilite l’ajout d’entrée manuscrite, de pointeurs laser et de curseurs à votre application pour une collaboration transparente.

Les fonctionnalités prises en charge par le canevas Live Share sont les suivantes :

- Ajoutez une collaboration `<canvas>` à votre application avec `LiveCanvas`.
- Transmettez des idées à l’aide des outils de stylet, de surligne, de trait et de flèche.
- Présentez efficacement à l’aide du pointeur laser.
- Suivez les curseurs de la souris en temps réel.
- Configurez les paramètres des appareils variables et affichez les états.
- Utilisez des entrées de souris, d’interaction tactile et de stylet entièrement prises en charge.

Vous trouverez plus d’informations sur ce package sur la [page de canevas Live Share](./teams-live-share-canvas.md).

## <a name="why-build-apps-with-live-share"></a>Pourquoi créer des applications avec Live Share ?

La création d’applications collaboratives peut être difficile, fastidieuse, coûteuse et comprend des exigences de conformité complexes à grande échelle. Les utilisateurs de Teams passent beaucoup de temps à revoir leur travail avec leurs coéquipiers, à regarder des vidéos ensemble et à réfléchir à de nouvelles idées grâce au partage d'écran. Le SDK Live Share vous permet de transformer votre application en quelque chose de plus collaboratif avec un investissement minimal.

Voici quelques-uns des principaux avantages du SDK Live Share :

- Gestion et sécurité des sessions sans souci.
- Structures de données distribuées avec état et sans état.
- Extensions multimédias pour synchroniser facilement la vidéo et l’audio.
- Entrée manuscrite à clé de tour, pointeurs laser et curseurs.
- Respecter les privilèges de réunion à l’aide de la vérification de rôle.
- Service gratuit et entièrement managé avec une faible latence.

Pour comprendre si Live Share est adapté à votre scénario collaboratif, il est utile de comprendre les différences entre Live Share et d’autres frameworks collaboratifs, notamment :

- [Sockets web](#web-sockets)
- [Relais Azure Fluid](#azure-fluid-relay)
- [Live Share](#live-share-hosted-service)

### <a name="web-sockets"></a>Sockets web

Les sockets web sont une technologie omniprésente pour la communication en temps réel sur le web, et certaines applications peuvent préférer utiliser leur propre backend web-socket personnalisé. Contrairement aux API REST, les sockets web conservent une connexion ouverte entre un serveur et des clients dans une session.

Comme d’autres services d’API personnalisés, les exigences incluent généralement l’authentification des sessions, le mappage régional, la maintenance et la mise à l’échelle. De nombreux scénarios collaboratifs nécessitent également le maintien de l’état de session sur le serveur, ce qui nécessite une infrastructure de stockage, des résolutions de conflits, etc.

En utilisant Live Share, vous obtenez toute la puissance des sockets web sans aucune surcharge.

### <a name="azure-fluid-relay"></a>Relais Azure Fluid

[Azure Fluid Relay](/azure/azure-fluid-relay/) est une offre managée pour Fluid Framework qui permet aux développeurs de créer des expériences de collaboration en temps réel et de répliquer l’état sur les clients JavaScript connectés. Microsoft Whiteboard, Loop et OneNote sont tous des exemples d’applications créées avec Fluid Framework aujourd’hui.

Comme d’autres services Azure, Azure Fluid Relay est conçu pour s’adapter à vos besoins individuels de projet avec une complexité minimale. Les exigences incluent le développement d’une histoire d’authentification pour vos conteneurs Fluid et la conformité régionale. Une fois configurés, les développeurs peuvent se concentrer sur la fourniture d’expériences collaboratives de haute qualité.

### <a name="live-share-hosted-service"></a>Service hébergé Live Share

Live Share fournit un service Azure Fluid Relay clé en charge par la sécurité des réunions Microsoft Teams. Les conteneurs Live Share sont limités aux participants à la réunion, conservent les exigences de résidence des locataires et sont accessibles dans quelques lignes de code client.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { presence: LivePresence },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient, LivePresence } from "@microsoft/live-share";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { presence: LivePresence },
};
const { container } = await liveShare.joinContainer(schema);

// ... ready to start app sync logic
```

---

> [!IMPORTANT]
> Toutes les données envoyées ou stockées via le service Azure Fluid Relay hébergé du Kit de développement logiciel (SDK) Live Share sont accessibles jusqu’à 24 heures. Si vous souhaitez en savoir plus, veuillez consulter la rubrique [FAQ sur Live Share](teams-live-share-faq.md).

#### <a name="using-a-custom-azure-fluid-relay-service"></a>Utilisation d’un service Azure Fluid Relay personnalisé

Bien que la plupart d’entre vous trouvent préférable d’utiliser notre service hébergé gratuit, il existe toujours des situations où il est avantageux d’utiliser votre propre service Azure Fluid Relay pour votre application Live Share.

Envisagez d’utiliser un service personnalisé si vous :

- Exiger le stockage des données dans des conteneurs Fluid au-delà de la durée de vie d’une réunion.
- Transmettez des données sensibles via le service qui nécessite une stratégie de sécurité personnalisée.
- Développez des fonctionnalités via Fluid Framework, par exemple, `SharedMap`pour votre application en dehors de Teams.

Pour plus d’informations, consultez le [guide pratique](./teams-live-share-how-to/how-to-custom-azure-fluid-relay.md) du service Relais Azure Fluid personnalisé.

## <a name="user-scenarios"></a>Scénarios utilisateur

| Scénario                                                                                | Exemple                                                                                                                                                                                            |
| :-------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Lors d’une révision marketing, un utilisateur souhaite recueillir des commentaires sur sa dernière modification vidéo. | L’utilisateur partage la vidéo à la phase de réunion et démarre la vidéo. Si nécessaire, l’utilisateur suspend la vidéo pour discuter de la scène et les participants dessinent sur des parties de l’écran pour mettre en évidence les points clés. |
| Un responsable de projet joue à Agile Poker avec son équipe lors de la planification.                    | Manager partage une application Agile Poker à la phase de réunion qui permet de jouer au jeu de planification jusqu’à ce que l’équipe ait un consensus.                                                                        |
| Un conseiller financier examine les documents PDF avec les clients avant de signer.                  | Le conseiller financier partage le contrat PDF à la phase de réunion. Tous les participants peuvent voir les curseurs et le texte mis en surbrillance dans le PDF, après quoi les deux parties signent l’accord.        |

> [!IMPORTANT]
> Live Share est concédé sous licence sous la [licence du Kit de développement logiciel (SDK) Microsoft Live Share](https://github.com/microsoft/live-share-sdk/blob/main/LICENSE). Pour utiliser ces fonctionnalités dans votre application, vous devez d’abord lire et accepter ces termes.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Prise en main](teams-live-share-quick-start.md)

## <a name="see-also"></a>Voir aussi

- [Référentiel GitHub](https://github.com/microsoft/live-share-sdk)
- [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Documents de référence du Kit de développement logiciel (SDK) Live Share Media](/javascript/api/@microsoft/live-share-media/)
- [Fonctionnalités de Live Share](teams-live-share-capabilities.md)
- [Fonctionnalités média de Live Share](teams-live-share-media-capabilities.md)
- [FAQ sur Live Share](teams-live-share-faq.md)
- [Applications Teams dans les réunions](teams-apps-in-meetings.md)
