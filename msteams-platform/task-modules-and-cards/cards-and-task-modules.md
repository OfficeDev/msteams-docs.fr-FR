---
title: Cartes et modules de tâche
description: Découvrez les types de cartes prises en charge dans les bots pour Teams, telles que les cartes adaptatives, de héros et de miniatures, ainsi que ses actions.
author: surbhigupta12
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 04cdcfedd98bee67babf63231ffdeae6679f7331
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66485446"
---
# <a name="cards-and-task-modules"></a>Cartes et modules de tâche

Les cartes fournissent aux utilisateurs différents messages visuels, audio et sélectionnables, ainsi qu’une aide dans le flux des conversations.

Avec les modules de tâche, vous pouvez créer des expériences contextuelles modales dans Microsoft Teams. Ils sont particulièrement utiles pour commencer et effectuer des tâches ou pour l’affichage d’informations enrichies, telles que des vidéos ou des tableaux de bord Power business intelligence (BI).

Les types de cartes suivants sont pris en charge dans les bots pour Teams :

* Carte adaptative
* Carte Hero
* Carte de liste
* Carte Connecteur Office 365
* Carte de réception
* Carte de connexion
* Carte miniature
* Collections de cartes

Vous pouvez mettre en forme le texte d’une carte à l’aide d’un sous-ensemble de mise en forme XML ou HTML ou Markdown, selon le type de carte.

[Le Sélecteur de personnes dans les cartes adaptatives](cards/people-picker.md) dans la carte adaptative permet de rechercher, sélectionner, réattribuer et présélectionner des utilisateurs dans la conversation ou le canal.

Vous pouvez ajouter et répondre aux actions de carte qui effectuent l’action suivante :

* Ouvrez une URL.
* Envoyer des messages et une charge utile au bot.
* Lancer le flux OAuth.

Vous pouvez fournir une expérience de [recherche dynamique](~/task-modules-and-cards/cards/dynamic-search.md) dans un jeu de données volumineux à l’aide du contrôle typeahead dans les cartes adaptatives et effectuer une recherche statique de typeahead dans un nombre limité de choix. Invoke the task modules in channel or personal tabs, bots, or deep links. L’expérience de votre utilisateur pour tous les flux de travail qui nécessite une entrée de données peut être améliorée en ajoutant un module de tâche à l’onglet de l’utilisateur. Vous pouvez appeler des modules de tâche à partir de bots Teams en utilisant des boutons sur les cartes adaptatives et les cartes Bot Framework.

## <a name="see-also"></a>Voir aussi

* [Cartes](~/task-modules-and-cards/what-are-cards.md)
* [Modules de tâche](~/task-modules-and-cards/what-are-task-modules.md)
