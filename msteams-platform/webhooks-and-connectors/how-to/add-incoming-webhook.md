---
title: Créer un webhook entrant
author: laujan
description: Ajouter un webhook entrant à l’application Teams et publier toutes les demandes externes à Teams à l’aide de celui-ci
keywords: onglets teams webhook sortant
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 93cdadbbb0e14a174d84a8fd0a71e5b4f77c0af4
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104020"
---
# <a name="create-an-incoming-webhook"></a>Créer un webhook entrant

Un webhook entrant permet aux applications externes de partager du contenu dans les canaux Microsoft Teams. Les webhooks sont utilisés comme outils pour suivre et notifier. Les webhooks fournissent une URL unique pour envoyer une charge utile JSON avec un message au format de carte. Les cartes sont des conteneurs d’interface utilisateur qui incluent du contenu et des actions liées à un seul sujet. Vous pouvez utiliser des cartes dans les fonctionnalités suivantes :

* Bots
* Extensions de messages
* Connecteurs

## <a name="key-features-of-an-incoming-webhook"></a>Fonctionnalités clés d’un webhook entrant

Le tableau suivant fournit les fonctionnalités et la description d’un webhook entrant :

| Fonctionnalités | Description |
| -------- | ----------- |
|Les cartes adaptatives utilisant un webhook entrant | Les cartes adaptatives peuvent être envoyées via des webhooks entrants. Pour plus d’informations, consultez [Envoyer des cartes adaptatives à l’aide de webhooks entrants.](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)|
|Prise en charge de la messagerie actionnable|Les cartes de message actionnables sont prises en charge dans tous les groupes Office 365, y compris Teams. Si vous envoyez des messages par le biais de cartes, vous devez utiliser le format de carte de message actionnable. Pour plus d’informations, consultez [référence de carte de message actionnable héritée](/outlook/actionable-messages/message-card-reference) et [aire de jeu de cartes de message](https://messagecardplayground.azurewebsites.net).|
|Prise en charge indépendante de la messagerie HTTPS|Les cartes fournissent des informations claires et cohérentes. Tout outil ou infrastructure pouvant envoyer des requêtes HTTPS POST peut envoyer des messages à Teams via un webhook entrant.|
|Prise en charge de Markdown|Tous les champs de texte dans les cartes de messagerie actionnables prennent en charge le markdown de base. N’utilisez pas de balise HTML dans vos cartes. Le code HTML est ignoré et traité comme texte brut.|
|Configuration délimitée|Le webhook entrant est limitée et configurée au niveau du canal.|
|Définitions de ressources sécurisées|Les messages sont formatés en tant que charges utiles JSON. Cette structure de messagerie déclarative empêche l’insertion de code malveillant.|

<!--- TBD: A note should be short and eye-catching. No need to put a list item inside a Note or any admonition for that matter. Re-write the below list item.
--->

> [!NOTE]
>
> * Les bots Teams, les extensions de message, le webhook entrant et le Bot Framework prennent en charge les Cartes adaptatives. Les cartes adaptatives sont une infrastructure de plateforme multiplateforme ouverte qui est utilisée sur toutes les plateformes telles que Windows, Android, iOS, etc. Actuellement, les [connecteurs Teams](../../webhooks-and-connectors/how-to/connectors-creating.md) ne prennent pas en charge les cartes adaptatives. Toutefois, il est possible de créer un [flux](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) qui publie des cartes adaptatives sur un canal Teams.
> * Pour plus d’informations sur les cartes et les webhooks, consultez [Cartes adaptatives et Webhooks entrants.](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)

## <a name="create-an-incoming-webhook"></a>Créer un webhook entrant

Pour ajouter un webhook entrant à un canal Teams, procédez comme suit :

1. Ouvrez le canal dans lequel vous souhaitez ajouter le webhook et sélectionnez &#8226;&#8226;&#8226; **Plus d’options** à partir de la barre de navigation supérieure.
1. Sélectionnez **Connecteurs** dans le menu déroulant :

    ![Sélectionner Connecteur](~/assets/images/connectors.png)

1. Recherchez le **Webhook entrant** sélectionnez **Ajouter**.
1. Sélectionnez **Configurer**, fournissez un nom et chargez une image pour votre webhook si nécessaire :

    ![Bouton Configurer](~/assets/images/configure.png)

1. Copiez et enregistrez l’URL de webhook unique présente dans la fenêtre de boîte de dialogue. L’URL est mappée au canal et vous pouvez l’utiliser pour envoyer des informations à Teams. Sélectionnez **Terminé**.

    ![URL unique](~/assets/images/url.png)

Le webhook est disponible dans le canal Teams.

Vous pouvez créer et envoyer des messages actionnables via le webhook entrant ou le connecteur Office 365. Pour plus d’informations, consultez [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md).

> [!NOTE]
> Dans Teams, sélectionnez **Paramètres** > **Autorisations des membres** > **Autoriser les membres à créer, mettre à jour et supprimer des connecteurs**, afin que tout membre d’équipe puisse ajouter, modifier ou supprimer un connecteur.

## <a name="remove-an-incoming-webhook"></a>Supprimer un webhook entrant

Pour supprimer un webhook entrant d’un canal Teams, procédez comme suit :

1. Ouvrez le canal et sélectionnez &#8226;&#8226;&#8226; **Plus d’options** à partir de la barre de navigation supérieure.
1. Sélectionnez **Connecteurs** dans le menu déroulant.
1. Sélectionnez **Configuré** sous **Gérer**.
1. Sélectionnez le **<*1*> Configuré** pour voir la liste de vos connecteurs actuels :

    ![Webhook configuré](~/assets/images/configured.png)

1. Sélectionnez **Gérer** pour le connecteur que vous souhaitez supprimer :

    ![Gérer le webhook](~/assets/images/manage.png)

1. Sélectionnez **Supprimer** pour afficher la boîte de dialogue **Supprimer la configuration** .

    ![Supprimer la configuration](~/assets/images/removeconfiguration.png)

1. Complétez les champs et cases à cocher de la boîte de dialogue, puis sélectionnez **Supprimer**.

    ![Suppression finale](~/assets/images/finalremove.png)

## <a name="see-also"></a>Voir aussi

* [Créer un webhook sortant](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Créer un connecteur Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Partager vers Teams à partir d’applications web](~/concepts/build-and-test/share-to-teams-from-web-apps.md)
* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
