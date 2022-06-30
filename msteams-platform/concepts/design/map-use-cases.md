---
title: Mappez vos cas d’usage aux fonctionnalités et fonctionnalités de l’application Teams
author: surbhigupta
description: Identifiez comment les cas d’utilisation de votre application peuvent fonctionner dans l’expérience Teams, les fonctionnalités et les fonctionnalités de l’application ; mappez les cas d’usage courants avec des fonctionnalités.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 50298ec41a6f5f6a4ca0ecfcf3b0570762d2720c
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2022
ms.locfileid: "66557854"
---
# <a name="map-your-use-cases-to-teams-app-features"></a>Mappez votre cas d’usage aux fonctionnalités Teams

Un cas d’usage bien défini vous permet de représenter l’infrastructure des fonctionnalités souhaitées dans l’application Teams. Une fois que vous avez déterminé les exigences de l’utilisateur, définissez l’étendue et la fonctionnalité Teams les mieux adaptées à votre application.

Vous pouvez mapper votre cas d’utilisation en fonction des éléments suivants :

* Partage et collaboration sur des éléments dans un système externe.
* Démarrage des flux de travail et envoi de notifications aux utilisateurs.
* Utilisation de plateformes sociales, bots conversationnels et combinaison de plusieurs fonctionnalités.

## <a name="common-use-cases-mapped-to-teams-capabilities"></a>Cas d’usage courants mappés aux fonctionnalités Teams

L’étape suivante consiste à faire correspondre les cas d’usage avec les fonctionnalités de l’application.

Voici une liste des scénarios utilisateur courants mappés aux fonctionnalités Teams. Il ne s’agit pas d’une liste exhaustive, mais elle vous aidera à réfléchir à certaines des possibilités qui s’offrent à vous.
</br>
</br>
<details>
<summary>Créer, partager et collaborer sur des éléments dans un système externe</summary>

Applications pour interagir avec vos données

| **Si vous voulez...** | **Essayez ceci...** |
| --- | --- |
| Recherchez des systèmes externes et partagez les résultats sous forme de carte interactive. | Extensions de messagerie avec des commandes de recherche |
| Collectez des informations à insérer dans un magasin de données ou exécuter des recherches avancées. | Extensions de messagerie avec commandes d’action |
| Créez des expériences web incorporées pour afficher, utiliser et partager des données. | Onglets |
| Envoyez (push) des données et envoyez des données à partir du client Teams. | Connecteurs et webhooks|
| Formulaires modaux interactifs où que vous en ayez besoin pour collecter ou afficher des informations. | Modules de tâche |

</details>
</br>
<details>
<summary>Lancez des flux de travail et des processus</summary>

Un moyen rapide de démarrer un processus ou un flux de travail dans un système externe.

| **Si vous voulez...** | **Essayez ceci...** |
| --- | --- |
| Déclenchez des messages, ce qui permet à vos utilisateurs d’envoyer rapidement le contenu d’un message à vos services web. | Extensions de messagerie de commandes d’action |
| Ouvrez des messages à partir d’un onglet, d’un bot, ou d’une extension de messagerie pour collecter des informations avant de lancer un flux de travail. | Modules de tâche |
| Interagissez avec vos utilisateurs via du texte et des cartes enrichies. | Bots conversationnels |
| Un bon choix pour une interaction simple de va-et-vient quand vous n’avez pas besoin de créer un bot conversationnel entier. |  Webhooks sortants |

</details>
</br>
<details>
<summary>Envoyer des notifications et des alertes</summary>

Envoyez des notifications et des alertes asynchrones à vos utilisateurs dans Teams.

| **Si vous voulez...** | **Essayez ceci...** |
| --- | --- |
| Envoyez des messages proactifs à des groupes, des canaux ou des utilisateurs individuels. | Bots conversationnels |
| Autorisez un canal à s’abonner pour recevoir des messages. Un connecteur permet aux utilisateurs d’adapter l’abonnement à une page de configuration. | Connecteurs et webhooks entrants |

</details>
</br>
<details>
<summary>Poser des questions et obtenir des réponses</summary>

Communiquer avec vos utilisateurs et résoudre leurs requêtes

| **Si vous voulez...** | **Essayez ceci...** |
| --- | --- |
| Traitement en langage naturel, IA, Machine Learning et tous les mots à la mode. Utilisez un bot optimisé par le cloud intelligent pour connecter vos utilisateurs aux réponses dont ils ont besoin. | Bots conversationnels |
| Incorporez votre portail web existant dans Teams ou créez une version spécifique à Teams pour ajouter des fonctionnalités. | Onglets |

</details>

## <a name="app-capabilities-mapped-to-features"></a>Fonctionnalités d’application mappées aux fonctionnalités

La plateforme Microsoft Teams offre une grande variété de fonctionnalités. Chaque fonctionnalité est un moyen d’interagir avec vos utilisateurs qui rend la fonctionnalité d’application Teams pertinente pour les besoins de l’utilisateur.

Examinons comment les fonctionnalités Teams activent différentes fonctionnalités pour votre application.

:::image type="content" source="../../assets/images/overview/teams-apps-capabilities.png" alt-text="Image montrant les fonctionnalités Teams":::

Par exemple :

* Utilisez la fonctionnalité **onglet** pour afficher les modules de tâches, demander des autorisations d’appareil, afficher <`iframe`> contenu ou utiliser des liens profonds.
* Utilisez la fonctionnalité **extension de messagerie** pour envoyer des cartes, déployer des liens ou prendre des mesures sur les messages.

## <a name="see-also"></a>Voir aussi

* [Liste de vérification de planification](../design/planning-checklist.md)
* [Créer votre première application Microsoft Teams](../../get-started/get-started-overview.md)
