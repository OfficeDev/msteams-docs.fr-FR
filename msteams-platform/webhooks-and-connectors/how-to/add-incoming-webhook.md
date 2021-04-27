---
title: Publier des demandes externes à Microsoft Teams avec des webhooks entrants
author: laujan
description: Comment ajouter un webhook entrant à l'application Teams
keywords: onglets teams webhook sortant
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bc4d768751d34ccf305ef99e126159123a83ef3f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018417"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>Publier des demandes externes à Teams avec des webhooks entrants

## <a name="what-are-incoming-webhooks-in-teams"></a>Qu'est-ce que les webhooks entrants dans Teams ?

Les webhooks entrants sont un type spécial de connecteur dans Teams qui offrent un moyen simple pour une application externe de partager du contenu dans les canaux d'équipe et sont souvent utilisés comme outils de suivi et de notification. Teams fournit une URL unique à laquelle vous envoyez une charge utile JSON avec le message que vous souhaitez publier, généralement dans un format de carte. Les cartes sont des conteneurs d'interface utilisateur (IU) qui contiennent du contenu et des actions liées à une seule rubrique et qui sont un moyen de présenter les données des messages de manière cohérente. Teams utilise des cartes dans trois fonctionnalités :

* Bots
* Extensions de messagerie
* Connecteurs

## <a name="incoming-webhook-key-features"></a>Fonctionnalités de clé de webhook entrant

| Fonctionnalité | Description |
| ------- | ----------- |
|Configuration limitée|Les webhooks entrants sont limitées et configurées au niveau du canal (par exemple, les webhooks sortants sont limitées et configurées au niveau de l'équipe).|
|Définitions de ressources sécurisées|Les messages sont formatés en tant que charges utiles JSON. Cette structure de messagerie déclarative empêche l'injection de code malveillant, car il n'y a pas d'exécution de code sur le client.|
|Prise en charge de la messagerie actionnable|Si vous choisissez d'envoyer des messages par le biais de cartes, vous devez utiliser le format **de carte de message actionnable.** Les cartes de message actionnables sont prises en charge dans tous les groupes Office 365, y compris Teams. Voici des liens vers la référence de carte de [message actionnable](/outlook/actionable-messages/message-card-reference) héritée et l'aire [de jeu de carte de message.](https://messagecardplayground.azurewebsites.net)|
|Prise en charge indépendante de la messagerie HTTPS| Les cartes sont un excellent moyen de présenter des informations de manière claire et cohérente. Tout outil ou infrastructure qui peut envoyer des demandes HTTPS POST peut envoyer des messages à Teams via un webhook entrant.|
|Prise en charge de Markdown|Tous les champs de texte dans les cartes de messagerie actionnables prendre en charge markdown de base. **N'utilisez pas de balise HTML dans vos cartes.** Le code HTML est ignoré et traité comme texte brut.|

> [!Note]
> Les bots Teams, les extensions de messagerie, les webhooks entrants et Bot Framework prisent en charge les cartes adaptatives, une infrastructure de plateforme de cartes croisées ouverte. [Les connecteurs Teams ne](../../webhooks-and-connectors/how-to/connectors-creating.md) supportent pas actuellement les cartes adaptatives. Toutefois, il est possible de créer un [flux qui](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) publie des cartes adaptatives sur un canal Teams.

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>Ajouter un webhook entrant à un canal Teams

> [!Important]  
> Si les autorisations du membre **Paramètres** de votre équipe autorisent les membres à créer, mettre à jour et supprimer des connecteurs est sélectionné, tout membre d'équipe peut ajouter, modifier ou supprimer  =>    =>   un connecteur.

1. Accédez au canal où vous souhaitez ajouter le webhook et sélectionnez (&#8226;&#8226;&#8226;) *Plus d'options* dans la barre de navigation supérieure.
1. Choisissez **des connecteurs** dans le menu déroulant et recherchez **Webhook entrant.**
1. Sélectionnez **le bouton Configurer,** fournissez un nom et, éventuellement, téléchargez un avatar d'image pour votre webhook.
1. La fenêtre de boîte de dialogue présente une URL unique qui sera m mapée au canal. Veillez à copier et **à enregistrer l'URL;** vous devrez la fournir au service externe.
1. Sélectionnez **le bouton** Terminé. Le webhook sera disponible dans le canal d'équipe.

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>Supprimer un webhook entrant d'un canal Teams

1. Accédez au canal où le webhook a été ajouté et sélectionnez (&#8226;&#8226;&#8226;) *Plus d'options* dans la barre de navigation supérieure.
1. Choisissez **connecteurs** dans le menu déroulant.
1. On the left, under **Manage**, choose **Configured**.
1. Sélectionnez *le numéro configuré pour* voir la liste de vos connecteurs actuels.
1. Sélectionnez **Gérer** en côté du connecteur que vous souhaitez supprimer.
1. Sélectionnez **le bouton** Supprimer et une boîte de dialogue Supprimer la *configuration* s'est présentée.
1. Vous pouvez également remplir les champs et les case à cocher de la boîte de dialogue avant de sélectionner **le bouton** Supprimer. Le webhook sera supprimé du canal d'équipe.

## <a name="distribution"></a>Distribution

Vous avez trois options pour distribuer votre webhook entrant :

* Configurer un webhook entrant directement pour votre équipe.
* Ajouter une page de configuration et encapsuler votre webhook entrant dans [un connecteur O365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* Packagez et publiez votre connecteur dans le cadre de [votre soumission AppSource.](~/concepts/deploy-and-publish/office-store-guidance.md)

## <a name="learn-more"></a>En savoir plus

* [Envoi de messages à des connecteurs et des webhooks](~/webhooks-and-connectors/how-to/connectors-using.md)
