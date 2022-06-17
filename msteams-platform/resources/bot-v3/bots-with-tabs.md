---
title: Combiner des bots avec des onglets
description: Dans cet article, vous allez apprendre à utiliser des onglets et des bots ensemble, en construisant des liens profonds vers des onglets dans les messages de votre bot et le développement d’onglets de bots Teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 03/15/2018
ms.openlocfilehash: f8199b65fded8c43af45cb303a400652e5516db2
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142093"
---
# <a name="combine-bots-with-tabs"></a>Combiner des bots avec des onglets

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Les bots et les onglets fonctionnent ensemble et sont souvent combinés en un seul service principal. Cette section décrit les meilleures pratiques et les modèles courants pour l’utilisation conjointe d’onglets et de bots.

## <a name="associating-user-identities-across-bot-and-tab"></a>Association d’identités utilisateur entre le bot et l’onglet

Par exemple : supposons que votre application tabulation utilise un système d’ID propriétaire pour sécuriser son contenu. Supposons que vous disposez également d’un bot qui peut interagir avec l’utilisateur. En règle générale, vous souhaiterez afficher le contenu dans l’onglet qui est spécifique à l’utilisateur d’affichage. Le défi est que l’ID d’utilisateur dans votre système est probablement différent de l’ID d’utilisateur Microsoft Teams. Comment associez-vous ces deux identités ?
En général, l’approche recommandée consiste à connecter l’utilisateur avec le bot à l’aide du même système d’identité que celui utilisé pour fournir l’authentification pour le contenu de l’onglet. Vous pouvez implémenter via l’action de connexion, qui se connecte généralement à l’utilisateur via un flux OAuth.

Ce flux fonctionne mieux si votre fournisseur d’identité implémente le protocole OAuth 2.0. Vous pouvez ensuite associer l’ID d’utilisateur Teams aux informations d’identification de l’utilisateur à partir de votre propre service d’identité.

   ![Association d’identités](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>Construction de liens profonds vers des onglets dans les messages de votre bot

Vous souhaitez utiliser des onglets pour afficher plus de contenu que possible à l’intérieur d’une carte, ou fournir un moyen d’effectuer des tâches complexes de remplissage de formulaires à l’aide du canevas d’onglet. Par exemple, envisagez d’accéder à l’onglet de l’utilisateur lorsqu’il clique sur la carte à partir de votre bot. Pour ce faire, vous devez encoder le message de votre bot pour inclure une URL de [lien profond](~/concepts/build-and-test/deep-links.md) , par le biais du balisage ou en tant que cible de l’action openUrl.

Les liens profonds s’appuient sur un entityId, qui est une valeur opaque qui est mappée à une entité unique dans votre système. Lorsque l’onglet est créé, vous stockez idéalement un état simple. Par exemple, indicateur sur votre back-end indiquant que l’onglet a été créé dans le canal. Lorsque votre bot construit un message, il peut cibler l’entityId associé à cet onglet.

> [!NOTE]
> dans les conversations personnelles, étant donné que les onglets sont « statiques » et installés avec l’application, vous pouvez toujours supposer leur existence et ainsi construire des liens profonds en conséquence.

## <a name="sending-notifications-for-tab-updates"></a>Envoi de notifications pour les mises à jour d’onglets

Vous souhaiterez souvent avertir l’utilisateur final chaque fois qu’une mise à jour ou une action de l’utilisateur se produit dans un onglet. Un exemple de scénario consiste à attribuer une tâche ou un ticket à un autre membre de l’équipe, puis à informer ce membre de l’équipe.

Il existe deux façons d’atteindre ce scénario :

1. Si vous souhaitez notifier un canal entier, votre bot peut publier un message de manière asynchrone sur le canal. Il n’existe aucun moyen pour un bot de créer de manière proactive la conversation d’onglet si elle n’a pas été créée avec l’onglet.

2. Si vous souhaitez uniquement informer le destinataire ou les parties intéressées impliquées dans l’action, votre bot peut envoyer un message de conversation personnel à l’utilisateur. Vous devez d’abord vérifier si une conversation personnelle existe entre votre bot et l’utilisateur. Si ce n’est pas le cas, vous pouvez appeler `CreateConversation` pour lancer la conversation personnelle.

Dans les deux cas, utilisez les notifications d’événements avec sagesse et ne spam jamais l’utilisateur avec des mises à jour inutiles.
