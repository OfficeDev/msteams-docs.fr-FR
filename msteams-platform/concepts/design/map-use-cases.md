---
title: Map vos cas d’utilisation Teams fonctionnalités de l’application
author: surbhigupta
description: Identifiez comment les cas d’utilisation de votre application peuvent fonctionner au sein Teams expérience utilisateur.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: c424b2c03f71449c5c43adc345ed0197eb6ef247
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720385"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a>Map vos cas d’utilisation Teams fonctionnalités de l’application

Une fois que vous avez  identifié *qui* est l’utilisateur  et quel problème vous allez résoudre, il est temps de décider comment résoudre le problème. *Qui,* *quoi* et *comment* termine le processus de compréhension et de mappage de vos cas d’utilisation Teams fonctionnalités de l’application. Vous devez définir l’étendue de l’application en fonction des réponses que vous avez reçues de l’utilisateur à vos requêtes, puis déterminer la fonctionnalité la plus adaptée pour créer votre application.

> [!NOTE]
> Vous devez bien comprendre les [points d’entrée](../../concepts/extensibility-points.md) et les éléments d’interface utilisateur disponibles pour votre application. Vous devez également vous assurer que vous avez [pris en compte vos cas d’utilisation](../../concepts/design/understand-use-cases.md) avec soin.

## <a name="choose-the-correct-scope-for-your-app"></a>Choisir l’étendue correcte pour votre application

Lors du choix de l’étendue de l’application, prenons en compte les considérations suivantes :

* Une application peut exister dans plusieurs étendues.
* Les fonctionnalités d’application, telles que les extensions de messagerie, suivent les utilisateurs dans toutes les étendues.
* Les utilisateurs ont souvent besoin d’ajouter des applications Teams ou des canaux.
* Les invités peuvent accéder au contenu exposé dans Teams ou canaux.

Vous pouvez choisir entre l’étendue personnelle et l’étendue d’équipe ou de canal pour votre application en fonction des possibilités suivantes :

* Pour l’étendue personnelle, posez-vous les questions suivantes :
  * Existe-t-il des interactions un-à-un avec l’application requises pour des raisons de confidentialité ou pour d’autres raisons ? Par exemple, vérification du solde des congés ou d’autres informations privées.
  * Existe-t-il une collaboration entre les utilisateurs qui n’ont peut-être pas de Teams ? Par exemple, recherche des événements à venir à l’échelle de l’organisation dans une entreprise.
  * Existe-t-il des notifications personnalisées ou des messages qui devront être envoyés à un utilisateur tout au long de l Teams’application ? Par exemple, les rappels pour les approbations ou les inscriptions.
* Pour une étendue partagée (équipe, canal ou conversation), posez-vous les questions suivantes :
  * Les informations présentées par l’application, sous l’onglet ou par le biais d’un bot, sont-ils pertinentes et utiles pour la plupart des membres d’une équipe ? Par exemple, application Scrum.
  * Le contexte de l’application peut-il changer en fonction de l’équipe dans laquelle elle est ajoutée ? Par exemple, les tâches du Planificateur sont différentes dans différentes équipes. 
  * Est-il possible que tous les membres d’une personne qui ont besoin de collaborer font partie d’une seule équipe ? Par exemple, les agents travaillant sur un ticket.

Les scénarios suivants vous guident dans la sélection de points d’entrée et d’éléments d’interface utilisateur qui fonctionnent bien Teams fonctionnalités de l’application :

> [!NOTE]
> Il ne s’agit pas d’une liste exhaustive, mais vous aidera à réfléchir à certaines des possibilités qui s’offrent à vous.

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a>Créer, partager et collaborer sur des éléments dans un système externe

Les applications pour Microsoft Teams sont un excellent moyen d’interagir avec vos données et vous pouvez choisir parmi divers points d’intégration.

* **Extensions de messagerie avec commandes de recherche**: rechercher des systèmes externes et partager les résultats sous forme de carte interactive.

* **Extensions de messagerie avec commandes d’action**: collecter des informations à insérer dans un magasin de données ou effectuer des recherches avancées.

* **Onglets :** créez des expériences web incorporées pour afficher, travailler avec et partager des données.

* **Connecteurs et webhooks**: un moyen simple de transmettre des données et d’envoyer des données hors du client Teams client.

* **Modules de tâche**: formulaires modaux interactifs où vous en avez besoin pour collecter ou afficher des informations.

## <a name="initiate-workflows-and-processes"></a>Démarrer des flux de travail et des processus

Parfois, vous avez simplement besoin d’un moyen rapide pour initier un processus ou un flux de travail dans un système externe.

* **Commandes d’action** des extensions de messagerie : déclencher à partir de messages, ce qui permet à vos utilisateurs d’envoyer rapidement le contenu d’un message à vos services web.

* **Modules de tâche**: ouvrez-les à partir d’un onglet, d’un bot ou d’une extension de messagerie pour collecter des informations avant de lancer un flux de travail.

* **Bots de conversation**: interagissez avec vos utilisateurs par le biais de texte et de cartes enrichies.

* **Webhooks sortants**: un bon choix pour une interaction simple de va-et-vient lorsque vous n’avez pas besoin de créer un bot conversationnel entier.

## <a name="send-notifications-and-alerts"></a>Envoyer des notifications et des alertes

Envoyez des notifications asynchrones et des alertes à vos utilisateurs dans Teams. Utilisez des cartes interactives pour fournir un accès rapide aux actions courantes et des liens vers des informations supplémentaires.

* **Bots de conversation**: envoient des messages proactifs à des groupes, des canaux ou des utilisateurs individuels.

* **Connecteurs et webhooks entrants**: autoriser un canal à s’abonner pour recevoir des messages. Un connecteur permet aux utilisateurs d’adapter l’abonnement avec une page de configuration.

## <a name="ask-questions-and-get-answers"></a>Poser des questions et obtenir des réponses

Les personnes ont des questions et vous avez probablement une grande partie des réponses stockées quelque part. Malheureusement, il est souvent assez difficile de connecter les deux.

* **Bots conversationnels**: traitement du langage naturel, IA, apprentissage automatique et tous les mots-clés. Utilisez un bot optimisé par le cloud intelligent pour connecter vos utilisateurs aux réponses dont ils ont besoin.

* **Onglets**: incorporez votre portail web existant dans Teams ou créez une version spécifique Teams pour ajouter des fonctionnalités.

## <a name="get-social"></a>Obtenir des réseaux sociaux

Une plateforme de collaboration est intrinsèquement une plateforme sociale. Laissez votre côté créatif être libre et ajoutez du plaisir à votre lieu de travail. Tous les utilisateurs doivent être en mesure d’envoyer des images, d’envoyer des félicitations, d’obtenir des mèmes, d’envoyer des emojis ou d’autres choses qui vous semblent l’être.

## <a name="think-in-terms-of-a-single-page-app"></a>Penser en termes d’application à page unique

Les onglets sont des pages web incorporées. À peu près tout ce que vous pouvez faire dans une SPA, vous pouvez le faire dans un onglet Teams. Il vous suffit d’être attentif à l’étendue. Les onglets de groupe et de canal sont pour les expériences partagées et les onglets personnels pour les expériences personnelles. La liste des choses de l’équipe passe sous l’onglet de canal et la liste de vos objets est dans l’onglet personnel.

## <a name="initiate-small"></a>Lancer petit

Vous ne savez pas où lancer ? Vous vous sentez un peu submergé par la grande variété d’options à votre disposition ? Vous devez choisir une fonctionnalité principale de votre application et y lancer l’application. Une fois que vous avez une idée du flux d’informations dans les différents contextes de Teams, il est beaucoup plus simple d’imaginer une interaction plus complexe.

## <a name="put-it-all-together"></a>Mettre tout en place

Cela étant dit, les meilleures applications combinent généralement plusieurs fonctionnalités, créant ainsi une application qui engage les utilisateurs dans le bon contexte avec les fonctionnalités qui leur sont utiles au bon moment. Vous ne devez pas forcer les fonctionnalités à un endroit où elle n’appartient pas. Ce n’est pas parce que vous avez un bon bot de conversation un-à-un que vous l’ajoutez à une équipe. Différents points d’extensibilité sont bons pour différents éléments et jouent sur leurs points forts pour créer une application réussie.

## <a name="see-also"></a>Voir aussi

[Créer votre première application Microsoft Teams de messagerie](../../get-started/get-started-overview.md)
