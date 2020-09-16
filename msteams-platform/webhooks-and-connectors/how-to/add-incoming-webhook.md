---
title: Publier des demandes externes à Microsoft teams avec des webhooks entrants
author: laujan
description: procédure d’ajout d’une application webhook entrante à teams
keywords: onglet teams webhook sortant *
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 3aa795170af9695fc375043c94e794f814b38646
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819066"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a>Publier des demandes externes dans teams avec des webhooks entrants

## <a name="what-are-incoming-webhooks-in-teams"></a>Qu’est-ce qu’un webhook entrant dans teams ?

Les webhooks entrants sont des types de connecteur spéciaux dans teams qui offrent un moyen simple pour une application externe de partager le contenu des canaux d’équipe et sont souvent utilisés comme outils de suivi et de notification. Teams fournit une URL unique à laquelle vous envoyez une charge utile JSON avec le message que vous souhaitez publier, généralement sous la forme d’une carte. Les cartes sont des conteneurs d’interface utilisateur (IU) qui contiennent du contenu et des actions liées à une seule rubrique et sont un moyen de présenter les données de message de manière cohérente. Teams utilise des cartes dans les trois fonctionnalités suivantes :

* Bots
* Extensions de messagerie
* Connecteurs

## <a name="incoming-webhook-key-features"></a>Fonctionnalités de clés webhook entrantes

| Fonctionnalité | Description |
| ------- | ----------- |
|Configuration étendue|Les webhooks entrants sont étendus et configurés au niveau du canal (par exemple, des webhooks sortants sont étendus et configurés au niveau de l’équipe).|
|Définitions de ressources sécurisées|Les messages sont mis en forme comme charges utiles JSON. Cette structure de messagerie déclarative empêche l’injection de code malveillant lorsqu’il n’y a pas d’exécution de code sur le client.|
|Prise en charge de la messagerie actionnable|Si vous choisissez d’envoyer des messages via des cartes, vous devez utiliser le format de **carte de message** intégrant des actions. Les cartes de message actionnables sont prises en charge dans tous les groupes Office 365, y compris Teams. Voici des liens vers la [référence de carte de message actionnable héritée](/outlook/actionable-messages/message-card-reference) et le [laboratoire de carte de message](https://messagecardplayground.azurewebsites.net).|
|Prise en charge de la messagerie HTTPs indépendante| Les cartes sont un excellent moyen de présenter des informations de façon claire et cohérente. Tout outil ou infrastructure pouvant envoyer des requêtes POST HTTPs peut envoyer des messages à teams via un webhook entrant.|
|Prise en charge des démarques|Tous les champs de texte des cartes de messagerie actionnable prennent en charge la démarque de base. **N’utilisez pas de balises HTML dans vos cartes**. Le code HTML est ignoré et traité comme texte brut.|

> [!Note]  
> Les robots Teams, les extensions de messagerie et l’infrastructure de robot prennent en charge les cartes adaptatives, une infrastructure de plateformes entre cartes ouverte. Les connecteurs Teams ne prennent actuellement pas en charge les cartes adaptatives. Toutefois, il est possible de créer un [flux](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) qui publie des cartes adaptatives sur un canal Teams.

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a>Ajouter un webhook entrant à un canal teams

> [!Important]  
> Si les autorisations membres des **paramètres**de votre équipe  =>  **Member permissions**  =>  **permettent aux membres de créer, mettre à jour et supprimer des connecteurs** , tous les membres de l’équipe peuvent ajouter, modifier ou supprimer un connecteur.

1. Accédez au canal auquel vous souhaitez ajouter le webhook et sélectionnez (&#8226;&#8226;&#8226;) d' *autres options* dans la barre de navigation supérieure.
1. Dans le menu déroulant, sélectionnez **connecteurs** , puis recherchez **webhook entrant**.
1. Sélectionnez le bouton **configurer** , entrez un nom, puis, si vous le souhaitez, téléchargez une image avatar pour votre webhook.
1. La fenêtre de la boîte de dialogue présente une URL unique qui se mappe sur le canal. Assurez-vous que vous **Copiez et enregistrez l’URL**, vous devrez la fournir au service externe.
1. Sélectionnez le bouton **Terminer** . Le webhook sera disponible dans le canal d’équipe.

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a>Supprimer un webhook entrant d’un canal teams

1. Accédez au canal où le webhook a été ajouté et sélectionnez (&#8226;&#8226;&#8226;) d' *autres options* dans la barre de navigation supérieure.
1. Dans le menu déroulant, sélectionnez **connecteurs** .
1. À gauche, sous **gérer**, sélectionnez **configuré**.
1. Sélectionnez le *numéro configuré* pour afficher la liste de vos connecteurs actuels.
1. Sélectionnez **gérer** en regard du connecteur que vous souhaitez supprimer.
1. Sélectionnez le bouton **supprimer** pour afficher la boîte de dialogue *Supprimer la configuration* .
1. Si vous le souhaitez, renseignez les champs et cases à cocher de la boîte de dialogue avant de cliquer sur le bouton **supprimer** . Le webhook sera supprimé de la chaîne d’équipe.

## <a name="distribution"></a>Distributeurs

Vous disposez de trois options pour distribuer votre webhook entrant :

* Configurez un webhook entrant directement pour votre équipe.
* Ajouter une page de configuration et encapsuler votre webhook entrant dans un [connecteur O365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* Empaquetez et publiez votre connecteur dans le cadre de votre soumission [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) .

## <a name="learn-more"></a>En savoir plus

* [Envoi de messages à des connecteurs et des webhooks](~/webhooks-and-connectors/how-to/connectors-using.md)
