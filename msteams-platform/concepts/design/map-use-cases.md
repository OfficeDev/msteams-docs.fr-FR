---
title: Cartographiez vos cas d’utilisation pour Teams d’application
author: clearab
description: Identifiez comment les cas d’utilisation de votre application peuvent fonctionner dans le cadre Teams exament.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 179d0a37d72577c36f2cc44a11a8217cb9f016b2
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566109"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a>Cartographiez vos cas d’utilisation pour Teams d’application

Une fois que vous *avez identifié* qui est l’utilisateur *et* quel problème vous résoudrez, il est temps de *décider* comment résoudre le problème. Le *qui,* *quoi ,* et comment complète *le* processus de compréhension et de cartographie de vos cas d’utilisation pour Teams d’application. Vous devez définir la portée de l’application en fonction des réponses que vous avez reçues de l’utilisateur à vos requêtes, puis décider quelle fonctionnalité est la mieux adaptée à la construction de votre application.

> [!NOTE]
> Vous devez avoir une bonne compréhension des [points d’entrée et des éléments d’interface utilisateur](../../concepts/extensibility-points.md) disponibles pour votre application. Vous devez également vous assurer que vous avez examiné [attentivement vos cas d’utilisation.](../../concepts/design/understand-use-cases.md)

## <a name="choose-the-correct-scope-for-your-app"></a>Choisissez la bonne étendue pour votre application

Tout en choisissant la portée de l’application, considérez ce qui suit :

* Une application peut exister à travers les étendues.
* Les fonctionnalités d’application, telles que les extensions de messagerie, suivent les utilisateurs à travers les étendues.
* Les utilisateurs hésitent souvent à ajouter des applications à Teams ou des canaux.
* Les utilisateurs invités peuvent accéder au contenu exposé dans Teams ou les canaux.

Vous pouvez choisir entre la portée personnelle et la portée de l’équipe ou du canal pour votre application en fonction des éléments suivants :

* Pour plus de portée personnelle, posez les questions suivantes :
  * Y a-t-il des interactions individuelles avec l’application requises pour des raisons de confidentialité ou d’autres raisons ? Par exemple, vérifier le solde des congés ou d’autres renseignements personnels.
  * Y aura-t-il une collaboration entre les utilisateurs qui n’auront peut-être pas de Teams? Par exemple, trouver des événements à venir à l’échelle de l’organisation dans une entreprise.
  * Y a-t-il des notifications ou des messages personnalisés qui devront être envoyés à un utilisateur tout au long de l’expérience Teams’application ? Par exemple, des rappels d’approbations ou d’inscriptions.
* Pour une portée partagée (équipe, canal ou chat), posez les questions suivantes :
  * Les informations présentées par l’application, que ce soit dans l’onglet ou par l’intermédiaire d’un bot, sont-ils pertinentes et utiles pour la plupart des membres d’une équipe ? Par exemple, l’application Scrum.
  * Le contexte de l’application pourrait-il changer en fonction de l’équipe dans laquelle elle est ajoutée ? Par exemple, les tâches du planificateur sont différentes selon les équipes. 
  * Est-il possible que tous les membres d’un personnage qui ont besoin de collaborer font partie d’une seule équipe? Par exemple, les agents qui travaillent sur un billet.

Les scénarios suivants vous guideront dans la compréhension de la sélection des points d’entrée et des éléments d’interface utilisateur qui fonctionnent bien avec les Teams d’application :

> [!NOTE]
> Il ne s’agit pas d’une liste exhaustive, mais vous aidera à réfléchir à certaines des possibilités qui s’offrent à vous.

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a>Créer, partager et collaborer sur des éléments d’un système externe

App for Microsoft Teams est un excellent moyen d’interagir avec vos données et il ya une variété de points d’intégration à choisir.

* **Extensions de messagerie avec commandes de recherche**: Recherchez des systèmes externes et partagez les résultats sous forme de carte interactive.

* **Extensions de messagerie avec commandes d’action**: Collectez des informations à insérer dans un magasin de données ou effectuez des recherches avancées.

* **Onglets**: Créez des expériences Web intégrées pour visualiser, travailler et partager des données.

* **Connecteurs et webhooks**: Un moyen simple de pousser les données et d’envoyer des données hors du Teams client.

* **Modules de tâches : Formulaires** modaux interactifs où vous en avez besoin pour collecter ou afficher des informations.

## <a name="initiate-workflows-and-processes"></a>Initier des workflows et des processus

Parfois, vous avez juste besoin d’un moyen rapide de démarrer un processus ou un flux de travail dans un système externe.

* **Commandes d’action d’extensions de** messagerie : Déclenchez à partir de messages, permettant à vos utilisateurs d’envoyer rapidement le contenu d’un message à vos services Web.

* **Modules de tâches**: Ouvrez-les à partir d’un onglet, d’un bot ou d’une extension de messagerie pour collecter des informations avant d’amorcer un workflow.

* **Bots conversationnels**: Interagissez avec vos utilisateurs à travers du texte et des cartes riches.

* **Webhooks sortants**: Un bon choix pour une simple interaction de va-et-vient lorsque vous n’avez pas besoin de construire un bot conversationnel entier.

## <a name="send-notifications-and-alerts"></a>Envoyer des notifications et des alertes

Envoyez des notifications et des alertes asynchrones à vos utilisateurs dans Teams. Utilisez des cartes interactives pour fournir un accès rapide aux actions couramment utilisées et des liens vers des informations supplémentaires.

* **Bots conversationnels**: Envoyez des messages proactifs aux groupes, canaux ou utilisateurs individuels.

* **Connecteurs et webhooks entrants : Permettre à** un canal de s’abonner pour recevoir des messages. Un connecteur permet aux utilisateurs d’adapter l’abonnement avec une page de configuration.

## <a name="ask-questions-and-get-answers"></a>Posez des questions et obtenez des réponses

Les gens ont des questions et vous avez probablement beaucoup de réponses stockées quelque part. Malheureusement, il est souvent assez difficile de relier les deux.

* **Bots conversationnels**: Traitement du langage naturel, IA, apprentissage automatique et tous les mots à la mode. Utilisez un bot alimenté par le cloud intelligent pour connecter vos utilisateurs aux réponses dont ils ont besoin.

* **Onglets**: Intégriez votre portail Web existant dans Teams ou créez une version Teams spécifique pour des fonctionnalités supplémentaires.

## <a name="get-social"></a>Obtenez social

Une plate-forme de collaboration est intrinsèquement une plate-forme sociale. Laissez votre côté créatif être libre et ajouter un peu de plaisir dans votre lieu de travail. Tous les utilisateurs doivent être en mesure d’envoyer des blagues, donner des félicitations, obtenir quelques mèmes, jes quelques emojis, ou toute autre chose qui frappe votre fantaisie.

## <a name="think-in-terms-of-a-single-page-app"></a>Pensez en termes d’une application d’une seule page

Les onglets sont des pages Web intégrées. À peu près tout ce que vous pouvez faire dans un SPA, vous pouvez le faire dans un onglet dans Teams. Assurez-vous juste de prêter attention à la portée. Les onglets de groupe et de canal sont pour les expériences partagées et les onglets personnels sont pour des expériences personnelles. La liste des choses de l’équipe va sur l’onglet canal et la liste de vos affaires va dans l’onglet personnel.

## <a name="start-small"></a>Commencez petit

Vous ne savez pas par où commencer? Vous vous sentez un peu dépassé par la variété impressionnante d’options qui s’offrent à vous? Vous devez choisir une fonctionnalité de base de votre application et commencer par là. Une fois que vous avez une idée de la circulation de l’information à travers les différents contextes Teams, il est beaucoup plus simple d’imaginer une interaction plus complexe.

## <a name="put-it-all-together"></a>Mettez tout cela ensemble

Cela étant dit, les meilleures applications combinent généralement plusieurs fonctionnalités, créant une application qui engage les utilisateurs dans le bon contexte avec les bonnes fonctionnalités au bon moment. Vous ne devez pas forcer toute fonctionnalité dans un endroit où elle n’a pas sa place. Ce n’est pas parce que vous avez un bon bot conversationnel en personne que vous l’ajoutez à une équipe. Différents points d’extensibilité sont bons pour différentes choses, jouer à leurs forces pour créer une application réussie.

## <a name="see-also"></a>Voir aussi

[Créer des applications pour Microsoft Teams](../../overview.md)
