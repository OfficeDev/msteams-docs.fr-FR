---
title: Combiner des robots à des onglets
description: Décrit l’utilisation conjointe des onglets et des bots
keywords: développement des onglets robots teams
ms.date: 03/15/2018
ms.openlocfilehash: 59ae8bc01f82c70dd7ea6869cb870e26acae1293
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673833"
---
# <a name="combine-bots-with-tabs"></a>Combiner des robots à des onglets

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Les robots et les onglets fonctionnent bien ensemble et sont souvent combinés en un seul service principal. Cette section décrit les meilleures pratiques et les modèles courants pour l’utilisation conjointe des onglets et des bots.

## <a name="associating-user-identities-across-bot-and-tab"></a>Association d’identités d’utilisateur entre un bot et un onglet

Par exemple : Supposons que votre application d’onglet utilise un système d’ID propriétaire pour sécuriser son contenu. Supposons que vous avez également un bot qui peut interagir avec l’utilisateur. En règle générale, vous voudrez afficher le contenu sous l’onglet qui est propre à l’utilisateur de l’affichage. Le défi réside dans le fait que l’IDENTIFIant de l’utilisateur dans votre système est probablement différent de l’ID utilisateur Microsoft Teams. Comment associer ces deux identités ?
En règle générale, l’approche recommandée consiste à connecter l’utilisateur à l’aide du robot en utilisant le même système d’identité que celui utilisé pour fournir l’authentification pour le contenu de l’onglet. Vous pouvez implémenter cette opération via l’action de connexion, qui se connecte généralement à l’utilisateur via un flux OAuth.

Ce flux fonctionne mieux si votre fournisseur d’identité implémente le protocole OAuth 2,0. Vous pouvez ensuite associer l’ID d’utilisateur teams aux informations d’identification de l’utilisateur à partir de votre propre service d’identité.

   ![Association d’identités](~/assets/images/bots/associating_contexts.png)

## <a name="constructing-deep-links-to-tabs-in-messages-from-your-bot"></a>Création de liens détaillés vers des onglets dans les messages à partir de votre robot

Vous pouvez utiliser des onglets pour afficher un plus grand nombre de contenu pouvant être contenu dans une carte ou un moyen d’effectuer des tâches complexes de remplissage de formulaires à l’aide de la toile de tabulation. Par exemple, vous pouvez envisager de parcourir l’utilisateur vers l’onglet lorsqu’il clique sur la carte à partir de votre bot. Pour que cela se produise, vous devez coder le message de votre bot afin d’inclure une URL de [lien détaillé](~/concepts/build-and-test/deep-links.md) , soit par balisage, soit comme cible de l’action openUrl.

Les liens détaillés s’appuient sur un entityId, qui est une valeur opaque qui correspond à une entité unique de votre système. Lorsque l’onglet est créé, vous pouvez stocker un état simple (par exemple, un indicateur) sur votre serveur principal, indiquant que l’onglet a été créé dans le canal. Lorsque votre bot construit un message, il peut cibler le entityId associé à cet onglet.

**Remarque :** dans les conversations personnelles, étant donné que les onglets sont « statiques » et installés avec l’application, vous pouvez toujours supposer leur existence et donc créer des liens détaillés en conséquence.

## <a name="sending-notifications-for-tab-updates"></a>Envoi de notifications pour les mises à jour d’onglet

Il est souvent préférable d’avertir l’utilisateur final chaque fois qu’une action de mise à jour ou d’utilisateur se produit dans un onglet. Un exemple de scénario consiste à attribuer une tâche ou un ticket à un membre de l’équipe, puis à avertir ce membre d’équipe.

Il existe deux façons d’atteindre ce scénario :

1. Si vous souhaitez avertir un canal entier, votre bot peut publier de manière asynchrone un message sur le canal. Il n’existe aucun moyen pour un bot de créer de façon proactive la conversation par onglet si elle n’a pas été créée avec l’onglet.

2. Si vous souhaitez uniquement informer le destinataire ou les parties intéressées de l’action, votre robot peut envoyer un message de conversation personnelle à l’utilisateur. Vous devez d’abord vérifier s’il existe une conversation personnelle entre votre robot et l’utilisateur. Si ce n’est pas le `CreateConversation` cas, vous pouvez appeler pour lancer la conversation personnelle.

Dans les deux cas, utilisez les notifications d’événement avec prudence et jamais le courrier indésirable par l’utilisateur avec des mises à jour inutiles.
