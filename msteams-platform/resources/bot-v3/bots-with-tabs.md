---
title: Combiner des bots avec des onglets
description: Décrit comment utiliser les onglets et les bots ensemble
keywords: Développement d’onglets de bots teams
ms.topic: conceptual
localization_priority: Normal
ms.date: 03/15/2018
ms.openlocfilehash: 3273369ad1122355b792dc3d429c3a4eff7e1d47
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566452"
---
# <a name="combine-bots-with-tabs"></a>Combiner des bots avec des onglets

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Les bots et les onglets fonctionnent bien ensemble et sont souvent combinés en un seul service back-end. Cette section décrit les meilleures pratiques et les modèles courants pour l’utilisation des onglets et des bots ensemble.

## <a name="associating-user-identities-across-bot-and-tab"></a>Association d’identités d’utilisateurs entre le bot et l’onglet

Par exemple : supposons que votre application d’onglet utilise un système d’ID propriétaire pour sécuriser son contenu. Supposons que vous avez également un bot qui peut interagir avec l’utilisateur. En règle générale, vous souhaiterez afficher dans l’onglet du contenu spécifique à l’utilisateur d’affichage. La difficulté est que l’ID d’utilisateur dans votre système est probablement différent de l’ID Microsoft Teams’utilisateur. Comment associer ces deux identités ?
En règle générale, l’approche recommandée consiste à signer l’utilisateur avec le bot à l’aide du système d’identité utilisé pour fournir l’authentification pour le contenu de l’onglet. Vous pouvez l’implémenter via l’action de connexion, qui connecte généralement l’utilisateur via un flux OAuth.

Ce flux fonctionne mieux si votre fournisseur d’identité implémente le protocole OAuth 2.0. Vous pouvez ensuite associer l Teams’utilisateur principal aux informations d’identification de l’utilisateur à partir de votre propre service d’identité.

   ![Association d’identités](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>Construction de liens profonds vers des onglets dans les messages à partir de votre bot

Vous pouvez utiliser des onglets pour afficher plus de contenu qu’il n’est possible d’y intégrer dans une carte, ou fournir un moyen d’effectuer des tâches complexes de remplissage de formulaire à l’aide de la zone de dessin de l’onglet. Par exemple, pensez à naviguer l’utilisateur vers l’onglet lorsqu’il clique sur la carte à partir de votre bot. Pour ce faire, vous devez encoder le message de votre bot pour inclure une [URL](~/concepts/build-and-test/deep-links.md) de lien profond, soit par le biais du code, soit comme cible de l’action openUrl.

Les liens profonds reposent sur un entityId, qui est une valeur opaque qui matric une entité unique dans votre système. Lorsque l’onglet est créé, vous stockez dans l’idéal un état simple, par exemple, un indicateur sur votre système arrière indiquant que l’onglet a été créé dans le canal. Lorsque votre bot construit un message, il peut cibler l’entityId associé à cet onglet.

> [!NOTE]
> dans les conversations personnelles, étant donné que les onglets sont « statiques » et installés avec l’application, vous pouvez toujours supposer leur existence et construire des liens profonds en conséquence.

## <a name="sending-notifications-for-tab-updates"></a>Envoi de notifications pour les mises à jour d’onglets

Il est souvent possible d’avertir l’utilisateur final chaque fois qu’une mise à jour ou une action de l’utilisateur se produit dans un onglet. Un exemple de scénario consiste à affecter une tâche ou un ticket à un membre de l’équipe, puis à avertir ce membre de l’équipe.

Il existe deux façons d’atteindre ce scénario :

1. Si vous souhaitez avertir un canal entier, votre bot peut publier de manière asynchrone un message sur le canal. Il n’existe aucun moyen pour un bot de créer de manière proactive la conversation d’onglet si elle n’a pas été créée avec l’onglet.

2. Si vous souhaitez uniquement avertir le destinataire ou les parties concernées impliquées dans l’action, votre bot peut envoyer un message de conversation personnelle à l’utilisateur. Vous devez d’abord vérifier si une conversation personnelle existe entre votre bot et l’utilisateur. Si ce n’est pas le cas, vous `CreateConversation` pouvez appeler pour lancer la conversation personnelle.

Dans les deux cas, utilisez judicieusement les notifications d’événement et ne mettez jamais l’utilisateur en courrier indésirable avec des mises à jour inutiles.
