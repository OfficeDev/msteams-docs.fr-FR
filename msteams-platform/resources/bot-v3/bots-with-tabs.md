---
title: Combiner les bots avec les onglets
description: Décrit comment utiliser les onglets et les bots ensemble
keywords: équipes bots onglets développement
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
# <a name="combine-bots-with-tabs"></a>Combiner les bots avec les onglets

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Les bots et les onglets fonctionnent bien ensemble, et sont souvent combinés en un seul service back-end. Cette section décrit les meilleures pratiques et les modèles communs pour l’utilisation d’onglets et de bots ensemble.

## <a name="associating-user-identities-across-bot-and-tab"></a>Associer les identités des utilisateurs à travers le bot et l’onglet

Par exemple : Supposons que votre application d’onglet utilise un système d’identification propriétaire pour sécuriser son contenu. Supposons que vous avez également un bot qui peut interagir avec l’utilisateur. En règle générale, vous souhaitez afficher le contenu de l’onglet qui est spécifique à l’utilisateur de visualisation. Le défi est que l’iD utilisateur dans votre système est probablement différent de l’Microsoft Teams’utilisateur. Alors, comment associez-vous ces deux identités?
En général, l’approche recommandée consiste à connecter l’utilisateur avec le bot en utilisant le même système d’identité utilisé pour fournir l’authentification pour le contenu de l’onglet. Vous pouvez implémenter cela via l’action de connexion, qui se connecte généralement à l’utilisateur via un flux OAuth.

Ce flux fonctionne mieux si votre fournisseur d’identité implémente le protocole OAuth 2.0. Vous pouvez ensuite associer le Teams utilisateur à l’identifiant de l’utilisateur à partir de votre propre service d’identité.

   ![Associer les identités](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>Construire des liens profonds vers les onglets dans les messages de votre bot

Vous pouvez utiliser des onglets pour afficher plus de contenu que ce qui peut s’insérer à l’intérieur d’une carte, ou fournir un moyen d’effectuer des tâches complexes de remplissage de formulaires à l’aide de la toile d’onglet. Par exemple, envisagez de naviguer sur l’utilisateur à l’onglet quand il ou elle clique sur la carte de votre bot. Pour ce faire, vous devrez coder le message de votre bot pour inclure une URL de [lien profond,](~/concepts/build-and-test/deep-links.md) soit par balisage, soit comme cible de l’action openUrl.

Les liens profonds reposent sur une entityId, qui est une valeur opaque qui cartographie une entité unique dans votre système. Lorsque l’onglet est créé, vous stockez idéalement un état simple, par exemple, drapeau sur votre backend indiquant que l’onglet a été créé dans le canal. Lorsque votre bot construit un message, il peut cibler l’entityId associé à cet onglet.

> [!NOTE]
> dans les chats personnels, parce que les onglets sont « statiques » et installés avec l’application, vous pouvez toujours assumer leur existence et ainsi construire des liens profonds en conséquence.

## <a name="sending-notifications-for-tab-updates"></a>Envoi de notifications pour les mises à jour d’onglets

Souvent, vous souhaitez aviser l’utilisateur final chaque fois qu’une mise à jour ou une action utilisateur se produit dans un onglet. Un scénario d’exemple est l’attribution d’une tâche ou d’un billet à un autre membre de l’équipe, puis l’aviser de ce membre de l’équipe.

Il y a deux façons d’atteindre ce scénario :

1. Si vous souhaitez aviser un canal entier, votre bot peut poster un message asynchrone sur le canal. Il n’y a aucun moyen pour un bot de créer proactivement la conversation onglet si elle n’a pas été créée avec l’onglet.

2. Si vous souhaitez uniquement aviser le destinataire ou les parties intéressées impliquées dans l’action, votre bot peut envoyer un message de chat personnel à l’utilisateur. Vous devez d’abord vérifier si une conversation personnelle entre votre bot et l’utilisateur existe. Sinon, vous pouvez appeler `CreateConversation` pour lancer le chat personnel.

Dans les deux cas, utilisez les notifications d’événements à bon escient et ne spammez jamais l’utilisateur avec des mises à jour inutiles.
