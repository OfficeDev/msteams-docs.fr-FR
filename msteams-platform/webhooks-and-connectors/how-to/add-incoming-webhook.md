---
title: Créer un webhook entrant
author: laujan
description: explique comment ajouter des webhooks entrants à Teams’application et publier des demandes externes Teams avec des webhooks entrants
keywords: onglets teams webhook sortant
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c07456288a26e3152a552644b704e2c6e6de38cc
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155519"
---
# <a name="create-incoming-webhook"></a>Créer un webhook entrant

Le webhook entrant permet à toutes les applications externes de partager du contenu Teams canaux. Ces webhooks sont utilisés comme outils de suivi et de notification. Ils fournissent une URL unique à laquelle vous envoyez une charge utile JSON avec un message au format de carte. Les cartes sont des conteneurs d’interface utilisateur qui incluent du contenu et des actions liées à une seule rubrique. Teams utiliser des cartes dans les fonctionnalités suivantes :

* Bots
* Extensions de messagerie
* Connecteurs

## <a name="key-features-of-incoming-webhook"></a>Principales fonctionnalités du webhook entrant

Le tableau suivant fournit les fonctionnalités et la description du webhook entrant :

| Fonctionnalités | Description |
| ------- | ----------- |
|Cartes adaptatives utilisant un webhook entrant|Les cartes adaptatives peuvent être envoyées via des webhooks entrants. Pour plus d’informations, voir [Envoyer des cartes adaptatives à l’aide de webhooks entrants.](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)|
|Prise en charge de la messagerie actionnable|Les cartes de message actionnables sont prises en charge dans tous Office 365 groupes, y compris Teams. Si vous envoyez des messages par le biais de cartes, vous devez utiliser le format de carte de message actionnable. Pour plus d’informations, voir la référence de carte de [message actionnable héritée](/outlook/actionable-messages/message-card-reference) et l’aire de [jeu de carte de message.](https://messagecardplayground.azurewebsites.net)|
|Prise en charge indépendante de la messagerie HTTPS|Les cartes fournissent des informations clairement et de manière cohérente. Tout outil ou infrastructure qui peut envoyer des demandes HTTPS POST peut envoyer des messages Teams via un webhook entrant.|
|Prise en charge de Markdown|Tous les champs de texte dans les cartes de messagerie actionnables prendre en charge markdown de base. N’utilisez pas de balises HTML dans vos cartes. Le code HTML est ignoré et traité comme texte brut.|
|Configuration limitée|Le webhook entrant est limitée et configurée au niveau du canal.|
|Définitions de ressources sécurisées|Les messages sont formatés en tant que charges utiles JSON. Cette structure de messagerie déclarative empêche l’insertion de code malveillant.|

> [!NOTE]
> * Teams bots, extensions de messagerie, webhook entrant et Bot Framework prisent en charge les cartes adaptatives, une infrastructure de plateforme de cartes croisées ouverte. Actuellement, [les connecteurs Teams ne](../../webhooks-and-connectors/how-to/connectors-creating.md) prisent pas en charge les cartes adaptatives. Toutefois, il est possible de créer un [flux](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) qui publie des cartes adaptatives sur Teams canal.
> * Pour plus d’informations sur les cartes et les webhooks, voir [Cartes adaptatives et Webhooks entrants.](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)

## <a name="create-incoming-webhook"></a>Créer un webhook entrant

**Pour ajouter un webhook entrant à un canal Teams web**

1. Go to the channel where you want to add the webhook and select &#8226;&#8226;&#8226; **More options** from the top navigation bar.
1. Sélectionnez **connecteurs** dans le menu déroulant :

    ![Select Connector](~/assets/images/connectors.png)

1. Recherchez **le webhook entrant et** sélectionnez **Ajouter.**
1. Sélectionnez **Configurer,** fournissez un nom et téléchargez une image pour votre webhook si nécessaire :

    ![Bouton Configurer](~/assets/images/configure.png)

1. La fenêtre de boîte de dialogue présente une URL unique qui mase au canal. Copiez et enregistrez l’URL de webhook, pour envoyer des informations Microsoft Teams et sélectionnez **Terminé**:

    ![Unique URL](~/assets/images/url.png)

Le webhook est disponible dans le canal Teams webhook.

> [!NOTE]
> Dans Teams, sélectionnez **Paramètres** autorisations de membre autoriser les membres à créer, mettre à jour et supprimer des  >    >  **connecteurs,** afin que n’importe quel membre d’équipe puisse ajouter, modifier ou supprimer un connecteur.

## <a name="remove-incoming-webhook"></a>Supprimer le webhook entrant

**Pour supprimer un webhook entrant d’un canal Teams web**

1. Go to the channel.
1. Sélectionnez &#8226;&#8226;&#8226; **options supplémentaires dans** la barre de navigation supérieure.
1. Sélectionnez **connecteurs** dans le menu déroulant.
1. Sur la gauche, sous **Gérer,** **sélectionnez Configuré.**
1. Sélectionnez **< *le 1*> configuré pour** voir la liste de vos connecteurs actuels :

    ![Webhook configuré](~/assets/images/configured.png)

1. Sélectionnez **Gérer** en côté du connecteur que vous souhaitez supprimer :

    ![Gérer le webhook](~/assets/images/manage.png)

1. Sélectionnez **Supprimer**:

    ![Supprimer un webhook](~/assets/images/remove.png)

    La **boîte de dialogue Supprimer la configuration** s’affiche :

    ![Supprimer la configuration](~/assets/images/removeconfiguration.png)

1. Complétez les champs et les case à cocher de la boîte de dialogue, puis **sélectionnez Supprimer**:

    ![Suppression finale](~/assets/images/finalremove.png)

    Le webhook est supprimé du canal Teams webhook.

## <a name="see-also"></a>Voir aussi

* [Créer un webhook sortant](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Créer un connecteur Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md)
