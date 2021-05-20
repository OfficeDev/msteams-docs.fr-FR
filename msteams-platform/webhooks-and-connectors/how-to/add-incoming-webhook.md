---
title: Publier des demandes externes pour Microsoft Teams avec les webhooks entrants
author: laujan
description: comment ajouter webhook entrant à l Teams app
keywords: les équipes onglets webhook sortant
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bb2306cb57c069d3bed06702495da2775694643a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566816"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>Publier des demandes externes pour Teams avec les webhooks entrants

## <a name="what-are-incoming-webhooks-in-teams"></a>Qu’est-ce que les Teams ?

Les webhooks entrants sont un type spécial de connecteur en Teams qui fournissent un moyen simple pour une application externe de partager du contenu dans les canaux de l’équipe et sont souvent utilisés comme outils de suivi et de notification. Teams fournit une URL unique à laquelle vous envoyez une charge utile JSON avec le message que vous souhaitez POSTER, généralement dans un format de carte. Les cartes sont des conteneurs d’interface utilisateur (interface utilisateur) qui contiennent du contenu et des actions liées à un seul sujet et sont un moyen de présenter les données des messages d’une manière cohérente. Teams utilise des cartes dans trois capacités :

* Bots
* Extensions de messagerie
* Connecteurs

## <a name="incoming-webhook-key-features"></a>Fonctionnalités clés webhook entrantes

| Fonctionnalité | Description |
| ------- | ----------- |
|Configuration étendue|Les webhooks entrants sont étendues et configurées au niveau du canal. Par exemple, les webhooks sortants sont étendues et configurées au niveau de l’équipe.|
|Définitions sécurisées des ressources|Les messages sont formatés sous forme de charges utiles JSON. Cette structure de messagerie déclarative empêche l’injection de code malveillant car il n’y a pas d’exécution de code sur le client.|
|Support de messagerie actionnable|Si vous choisissez d’envoyer des messages via des cartes, vous devez utiliser le format **de carte de message actionnable.** Les cartes de messages actionnables sont prises en charge dans tous les Office 365, y compris Teams. Voici des liens vers la référence [de la carte de message actionnable Legacy et](/outlook/actionable-messages/message-card-reference) le terrain de jeu de la carte [Message](https://messagecardplayground.azurewebsites.net).|
|Support de messagerie HTTPS indépendant| Les cartes sont un excellent moyen de présenter l’information d’une manière claire et cohérente. Tout outil ou framework qui peut envoyer des demandes HTTPS POST peut envoyer des messages à Teams via un webhook entrant.|
|Support Markdown|Tous les champs de texte dans les cartes de messagerie actionnables soutiennent markdown de base. **N’utilisez pas de balisage HTML dans vos cartes**. Le code HTML est ignoré et traité comme texte brut.|

> [!Note]
> Teams, les extensions de messagerie, les webhooks entrants et les cartes adaptatives de prise en charge du cadre Bot, un cadre de plate-forme inter-cartes ouvert. [Teams connecteurs ne supportent](../../webhooks-and-connectors/how-to/connectors-creating.md) pas actuellement les cartes adaptatives. Toutefois, il est possible de créer un flux [qui](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) affiche des cartes adaptatives sur un canal Teams’eau.

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>Ajouter un webhook entrant à un canal Teams web

> [!Important]  
> Si les autorisations **de membre Paramètres de votre** équipe  =>  **permettent** aux membres  =>  **de créer, de mettre à jour et de supprimer des connecteurs,** n’importe quel membre de l’équipe peut ajouter, modifier ou supprimer un connecteur.

**Pour ajouter un webhook entrant**

1. Accédez au canal où vous souhaitez ajouter le webhook et sélectionnez (&#8226;&#8226;&#8226;) *Plus d’options à* partir de la barre de navigation supérieure.
1. Choisissez **connecteurs** dans le menu drop-down et recherchez **le Webhook entrant.**
1. Sélectionnez le bouton **Configure,** fournissez un nom et, en option, téléchargez un avatar d’image pour votre webhook.
1. La fenêtre de dialogue présentera une URL unique qui sera cartographique sur le canal. Assurez-vous que **vous copiez et enregistrez l’URL**, vous devrez la fournir au service extérieur.
1. Sélectionnez **le bouton** Done. Le webhook sera disponible dans le canal de l’équipe.

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>Supprimer un webhook entrant d’un canal Teams web

**Pour supprimer un webhook entrant**

1. Accédez au canal où le webhook a été ajouté et sélectionnez (&#8226;&#8226;&#8226;) *Plus d’options à* partir de la barre de navigation supérieure.
1. Choisissez **connecteurs** dans le menu drop-down.
1. Sur la gauche, sous **Manage**, choisissez **Configured**.
1. Sélectionnez *le numéro Configuré* pour voir une liste de vos connecteurs actuels.
1. Sélectionnez **Gérer** à côté du connecteur que vous souhaitez supprimer.
1. Sélectionnez **le bouton** Supprimer et vous serez présenté avec une boîte de dialogue *Supprimer* la configuration.
1. En option, remplissez les champs de boîte de dialogue et les cases à cocher avant de sélectionner **le bouton Supprimer.** Le webhook sera supprimé du canal de l’équipe.

## <a name="distribution"></a>Distribution

Vous avez trois options pour distribuer votre webhook entrant :

* Configurez un webhook entrant directement pour votre équipe.
* Ajoutez une page de configuration et enveloppez votre webhook entrant dans [un connecteur O365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* Emballez et publiez votre connecteur dans le cadre de [votre soumission AppSource.](~/concepts/deploy-and-publish/office-store-guidance.md)

## <a name="see-also"></a>Voir aussi

[Envoi de messages aux connecteurs et aux webhooks](~/webhooks-and-connectors/how-to/connectors-using.md)
