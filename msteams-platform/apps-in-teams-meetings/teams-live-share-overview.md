---
title: Vue d’ensemble Live Share
author: surbhigupta
description: Dans ce module, découvrez ce qu’est le Kit de développement logiciel (SDK) Microsoft Live Share et ses scénarios utilisateur.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: 3738ee1037c87f283fd31ebdaba53b57f1784bb2
ms.sourcegitcommit: 134ce9381891e51e6327f1f611fdfd60c90cca18
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/24/2022
ms.locfileid: "67425623"
---
---

# <a name="live-share-sdk"></a>FAQ sur le Kit de développement logiciel (SDK) de Live Share

> [!NOTE]
> Le Kit de développement logiciel (SDK) Live Share est actuellement disponible en [préversion publique pour les développeurs](../resources/dev-preview/developer-preview-intro.md). Vous devez faire partie de la préversion publique du développeur pour que Microsoft Teams utilise Live Share.

Live Share est un Kit de développement logiciel (SDK) conçu pour transformer Teams applications en expériences multi-utilisateurs collaboratives sans écrire de code principal dédié. Live Share intègre en toute transparence les réunions à [Fluid Framework](https://fluidframework.com/). Infrastructure Fluid est une collection de bibliothèques clientes permettant de distribuer et de synchroniser l’état partagé. Live Share fournit un relais [Azure Fluid](/azure/azure-fluid-relay/) gratuit, entièrement managé et prêt à l’emploi, soutenu par la sécurité et l’échelle mondiale de Teams.

> [!div class="nextstepaction"]
> [Prise en main](teams-live-share-quick-start.md)

Live Share inclut une `TeamsFluidClient` classe pour la connexion à un conteneur Fluid spécial associé à chaque réunion en quelques lignes de code. Outre les structures de données fournies par Infrastructure Fluid, Live Share prend également en charge un nouvel ensemble de classes de structures de données distribuées (DDS) afin de simplifier la création d'applications pour les scénarios de réunion courants, tels que la lecture de médias partagés.

:::image type="content" source="../assets/images/teams-live-share/teams-live-share-contoso-video.gif" alt-text="Expérience de partage de vidéos Live Share":::

## <a name="why-build-apps-with-live-share"></a>Pourquoi créer des applications avec Live Share ?

La création d’applications collaboratives peut être difficile, fastidieuse, coûteuse et comprend des exigences de conformité complexes à grande échelle. Les utilisateurs de Teams passent beaucoup de temps à revoir leur travail avec leurs coéquipiers, à regarder des vidéos ensemble et à réfléchir à de nouvelles idées grâce au partage d'écran. Le SDK Live Share vous permet de transformer votre application en quelque chose de plus collaboratif avec un investissement minimal.

Voici quelques-uns des principaux avantages du SDK Live Share :

- Gestion et sécurité des sessions sans souci.
- Structures de données distribuées avec état et sans état.
- Extensions multimédias pour synchroniser facilement la vidéo et l’audio.
- Respecter les privilèges de réunion à l’aide de la vérification de rôle.
- Service gratuit et entièrement managé avec une faible latence.
- Injection intelligente de l'audio.

:::image type="content" source="../assets/images/teams-live-share/Teams-live-share-schematics.png" alt-text="Live Share Teams":::

Pour comprendre si Live Share est adapté à votre scénario collaboratif, il est utile de comprendre les différences entre Live Share et d’autres frameworks collaboratifs, notamment :

- [Sockets web](#web-sockets)
- [Relais Azure Fluid](#azure-fluid-relay)
- [Live Share](#live-share-hosted-service)

### <a name="web-sockets"></a>Sockets web

Les sockets web sont une technologie omniprésente pour la communication en temps réel sur le web, et certaines applications peuvent préférer utiliser leur propre backend web-socket personnalisé. Contrairement aux API REST, les sockets web conservent une connexion ouverte entre un serveur et des clients dans une session.

Comme d’autres services d’API personnalisés, les exigences incluent généralement l’authentification des sessions, le mappage régional, la maintenance et la mise à l’échelle. De nombreux scénarios collaboratifs nécessitent également le maintien de l’état de session sur le serveur, ce qui nécessite une infrastructure de stockage, des résolutions de conflits, etc.

### <a name="azure-fluid-relay"></a>Relais Azure Fluid

[Azure Fluid Relay](/azure/azure-fluid-relay/) est une offre managée pour Fluid Framework qui permet aux développeurs de créer des expériences de collaboration en temps réel et de répliquer l’état sur les clients JavaScript connectés. Microsoft Whiteboard, Loop et OneNote sont tous des exemples d’applications créées avec Fluid Framework aujourd’hui.

Comme d’autres services Azure, Azure Fluid Relay est conçu pour s’adapter à vos besoins individuels de projet avec une complexité minimale. Les exigences incluent le développement d’une histoire d’authentification pour vos conteneurs Fluid et la conformité régionale. Une fois configurés, les développeurs peuvent se concentrer sur la fourniture d’expériences collaboratives de haute qualité.

### <a name="live-share-hosted-service"></a>Service hébergé Live Share

Live Share fournit un service Azure Fluid Relay clé en charge par la sécurité des réunions Microsoft Teams. Les conteneurs Live Share sont limités aux participants à la réunion, conservent les exigences de résidence des locataires et sont accessibles dans quelques lignes de code client.

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { TeamsFluidClient, EphemeralPresence } from "@microsoft/live-share";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema = {
  initialObjects: { presence: EphemeralPresence },
};
const { container } = await client.joinContainer(schema);

// ... ready to start app sync logic
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { TeamsFluidClient, EphemeralPresence } from "@microsoft/live-share";
import { ContainerSchema } from "fluid-framework";

// Join the Fluid container
const client = new TeamsFluidClient();
const schema: ContainerSchema = {
  initialObjects: { presence: EphemeralPresence },
};
const { container } = await client.joinContainer(schema);

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
