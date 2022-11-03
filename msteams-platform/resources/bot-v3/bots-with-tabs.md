---
title: Combiner des bots avec des onglets
description: Dans cet article, vous allez apprendre à utiliser des onglets et des bots ensemble, en construisant des liens profonds vers des onglets dans les messages de votre bot, et à développer des onglets de bots teams.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 03/15/2018
ms.openlocfilehash: f993f3d8deb8b8a781c96627bf63c2eed350e6c8
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833022"
---
# <a name="combine-bots-with-tabs"></a>Combiner des bots avec des onglets

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Les bots et les onglets fonctionnent ensemble et sont souvent combinés en un seul service principal. Cette section décrit les meilleures pratiques et les modèles courants pour l’utilisation des onglets et des bots ensemble.

## <a name="associating-user-identities-across-bot-and-tab"></a>Association d’identités utilisateur entre bot et onglet

Par exemple : supposons que votre application d’onglet utilise un système d’ID propriétaire pour sécuriser son contenu. Supposons que vous disposez également d’un bot qui peut interagir avec l’utilisateur. En règle générale, vous souhaiterez afficher le contenu dans l’onglet qui est spécifique à l’utilisateur qui consulte. Le défi est que l’ID d’utilisateur dans votre système est probablement différent de l’ID utilisateur Microsoft Teams. Comment associez-vous ces deux identités ?
En général, l’approche recommandée consiste à connecter l’utilisateur avec le bot à l’aide du même système d’identité que celui utilisé pour fournir l’authentification pour le contenu de l’onglet. Vous pouvez implémenter via l’action de connexion, qui connecte généralement l’utilisateur via un flux OAuth.

Ce flux fonctionne mieux si votre fournisseur d’identité implémente le protocole OAuth 2.0. Vous pouvez ensuite associer l’ID utilisateur Teams aux informations d’identification de l’utilisateur à partir de votre propre service d’identité.

   :::image type="content" source="../../assets/images/bots/associating_contexts.png" alt-text="Capture d’écran montrant l’association d’identités.":::

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>Création de liens profonds vers des onglets dans les messages de votre bot

Vous souhaitez utiliser des onglets pour afficher davantage de contenu pouvant tenir à l’intérieur d’une carte, ou fournir un moyen d’effectuer des tâches complexes de remplissage de formulaire à l’aide du canevas d’onglet. Par exemple, envisagez de naviguer vers l’onglet lorsque l’utilisateur sélectionne la carte à partir de votre bot. Pour ce faire, vous devez encoder le message de votre bot pour inclure une URL de [lien profond](~/concepts/build-and-test/deep-links.md) , via le balisage ou en tant que cible de l’action openUrl.

Les liens profonds s’appuient sur un entityId, qui est une valeur opaque qui correspond à une entité unique dans votre système. Lorsque l’onglet est créé, vous stockez un état simple. Par exemple, l’indicateur sur votre back-end indiquant que l’onglet est créé dans le canal. Lorsque votre bot construit un message, il peut cibler l’entityId associé à cet onglet.

> [!NOTE]
> Dans les conversations personnelles, étant donné que les onglets sont *statiques* et installés avec l’application, vous pouvez toujours supposer leur existence et ainsi construire des liens profonds en conséquence.

## <a name="sending-notifications-for-tab-updates"></a>Envoi de notifications pour les mises à jour d’onglet

Souvent, vous souhaiterez avertir l’utilisateur final chaque fois qu’une mise à jour ou une action de l’utilisateur se produit dans un onglet. Un exemple de scénario est l’attribution d’une tâche ou d’un ticket à un autre membre de l’équipe, puis la notification de ce membre de l’équipe.

Il existe deux façons de réaliser ce scénario :

1. Si vous souhaitez notifier un canal entier, votre bot peut publier de façon asynchrone un message sur le canal. Il n’existe aucun moyen pour un bot de créer de manière proactive la conversation d’onglet si elle n’a pas été créée avec l’onglet.

2. Si vous souhaitez informer uniquement le destinataire ou les parties intéressées impliquées dans l’action, votre bot peut envoyer un message de conversation personnel à l’utilisateur. Vous devez d’abord vérifier s’il existe une conversation personnelle entre votre bot et l’utilisateur. Si ce n’est pas le cas, vous pouvez appeler `CreateConversation` pour lancer la conversation personnelle.

Dans les deux cas, utilisez les notifications d’événements à bon escient et ne courrierez jamais l’utilisateur avec des mises à jour inutiles.
