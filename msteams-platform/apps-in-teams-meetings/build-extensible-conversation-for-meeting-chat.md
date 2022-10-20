---
title: Créer une conversation extensible pour la conversation de réunion
author: v-sdhakshina
description: Dans cet article, découvrez comment créer une conversation extensible pour la conversation de réunion Microsoft Teams avec des bots, des cartes et des extensions de message.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: 65fc91d51cd4c740f28d5f33a2ad578f214c20a8
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615400"
---
# <a name="build-extensible-conversation-for-meeting-chat"></a>Créer une conversation extensible pour la conversation de réunion

Vous pouvez rendre les conversations extensibles dans les réunions Microsoft Teams. Les bots, les extensions de message, les cartes et les modules de tâches peuvent être combinés pour offrir une expérience intuitive.

## <a name="bots"></a>Bots

Un bot est également appelé chatbot ou bot de conversation. Il s’agit d’une application qui exécute des tâches simples et répétitives effectuées par des utilisateurs tels que le service clientèle ou le personnel de support technique. L’utilisation quotidienne de bots inclut des bots qui fournissent des informations sur la météo, qui effectuent des réservations au restaurant ou qui fournissent des informations concernant les voyages. Les interactions avec les bots peuvent être des questions et réponses rapides ou des conversations complexes. Un bot doit être activé dans l’étendue `team` d’une réunion de canal et dans l’étendue `groupchat` de tous les autres types de réunion. Pour implémenter des bots, commencez par [générer un bot](/microsoftteams/platform//sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode).

### <a name="bot-apis"></a>API de bot

Le [Bot Framework](https://dev.botframework.com/) est un kit de développement logiciel (SDK) riche utilisé pour créer des bots à l’aide de C#, Java, Python et JavaScript. Si vous disposez déjà d’un bot basé sur le Bot Framework, vous pouvez facilement le modifier pour qu’il fonctionne dans Teams. Utilisez C# ou Node.js pour tirer parti de nos [Kits de développement logiciel](/microsoftteams/platform/).

### <a name="code-samples---bots"></a>Exemples de code - Bots

|Exemple de nom | Description | . NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|
| Bot de conversation Teams | Gestion des événements de messagerie et de conversation | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |
|Échantillons de bottes | Ensemble d’exemples de bots  | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python) |

## <a name="message-extensions"></a>Extensions de messages

Les extensions de message permettent aux utilisateurs d’interagir avec votre service web via des boutons et des formulaires dans le client Teams. Les utilisateurs peuvent rechercher ou lancer des actions dans un système externe à partir de la zone de composition du message, de la zone de commande ou directement à partir d’un message. Vous pouvez renvoyer les résultats de cette interaction au client Teams sous la forme d’une carte richement mise en forme. L’implémentation des extensions de message pour les conversations de réunion n’est pas différente de celle des conversations régulières. Pour implémenter l’extension de message, commencez par [les extensions de message](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions?tabs=dotnet).

## <a name="cards-and-task-modules"></a>Cartes et modules de tâches

Les cartes fournissent aux utilisateurs différents messages visuels, audio et sélectionnables, ainsi qu’une aide dans le flux des conversations. Avec les modules de tâches, vous pouvez créer des expériences contextuelles modales dans Teams. Ils sont particulièrement utiles pour commencer et effectuer des tâches ou pour l’affichage d’informations enrichies, telles que des vidéos ou des tableaux de bord Power business intelligence (BI). Pour plus d’informations, consultez [les cartes de construction et les modules de tâches](/microsoftteams/platform/task-modules-and-cards/cards-and-task-modules).

## <a name="feature-compatibility-by-user-types"></a>Compatibilité des fonctionnalités par types d’utilisateurs

Le tableau suivant fournit les types d’utilisateurs et répertorie les fonctionnalités auxquelles chaque utilisateur peut accéder dans les réunions :

| Type d'utilisateur | Bots | Extensions de messages | Cartes adaptatives | Modules de tâche |
| :-- | :-- | :-- | :-- | :-- |
| Utilisateur in-tenant | Disponible | Disponible | Disponible | Disponible |
| Invité, partie du locataire Azure AD | Non disponible | Non disponible | Les interactions dans la conversation de réunion sont autorisées. | Les interactions dans la conversation de réunion à partir de la carte adaptative sont autorisées. |
| Pour plus d’informations, consultez [les utilisateurs fédérés](/microsoftteams/non-standard-users). | L’interaction est autorisée. L’acquisition, la mise à jour et la suppression ne sont pas autorisées. | Non disponible | Les interactions dans la conversation de réunion sont autorisées. | Les interactions dans la conversation de réunion à partir de la carte adaptative sont autorisées. |
| Utilisateur anonyme | Non disponible | Non disponible | Les interactions dans la conversation de réunion sont autorisées. | Non disponible |

## <a name="see-also"></a>Voir aussi

* [Conception de votre extension de message Microsoft Teams](../messaging-extensions/design/messaging-extension-design.md)
* [Conception de modules de tâches pour votre application Microsoft Teams](../task-modules-and-cards/task-modules/design-teams-task-modules.md)
