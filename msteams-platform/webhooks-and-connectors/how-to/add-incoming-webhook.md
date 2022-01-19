---
title: Créer un webhook entrant
author: laujan
description: explique comment ajouter des webhooks entrants à l’application Teams et envoyer des demandes externes à Teams avec des webhooks entrants
keywords: onglets teams webhook sortant
ms.localizationpriority: high
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 308eaf9f08e946f468f02d897ad556681d1cc832
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059762"
---
# <a name="create-incoming-webhook"></a>Créer un webhook entrant

Le webhook entrant permet à toutes les applications externes de partager du contenu dans les canaux Teams. Ces webhooks sont utilisés comme outils de suivi et de notification. Ils fournissent une URL unique à laquelle vous envoyez une charge utile JSON avec un message au format de la carte. Les cartes sont des conteneurs d’interface utilisateur qui incluent du contenu et des actions liées à un seul sujet. Teams utiliser des cartes dans les fonctionnalités suivantes :

* Bots
* Extensions de messagerie
* Connecteurs

## <a name="key-features-of-incoming-webhook"></a>Principales fonctionnalités du webhook entrant

Le tableau suivant fournit les fonctionnalités et la description du webhook entrant :

| Fonctionnalités | Description |
| ------- | ----------- |
|Les cartes adaptatives utilisant un webhook entrant|Les cartes adaptatives peuvent être envoyées via des webhooks entrants. Pour plus d’informations, consultez [Envoyer des cartes adaptatives à l’aide de webhooks entrants.](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)|
|Prise en charge de la messagerie actionnable|Les cartes de message actionnables sont prises en charge dans tous les groupes Office 365, y compris Teams. Si vous envoyez des messages par le biais de cartes, vous devez utiliser le format de carte de message actionnable. Pour plus d’informations, consultez [référence de carte de message actionnable héritée](/outlook/actionable-messages/message-card-reference) et [aire de jeu de cartes de message](https://messagecardplayground.azurewebsites.net).|
|Prise en charge indépendante de la messagerie HTTPS|Les cartes fournissent des informations de manière claire et cohérente. Tout outil ou infrastructure qui peut envoyer des demandes HTTPS POST peut envoyer des messages Teams via un webhook entrant.|
|Prise en charge de Markdown|Tous les champs de texte dans les cartes de messagerie actionnables prennent en charge le markdown de base. N’utilisez pas de balise HTML dans vos cartes. Le code HTML est ignoré et traité comme texte brut.|
|Configuration délimitée|Le webhook entrant est limitée et configurée au niveau du canal.|
|Définitions de ressources sécurisées|Les messages sont formatés en tant que charges utiles JSON. Cette structure de messagerie déclarative empêche l’insertion de code malveillant.|

> [!NOTE]
> * Les bots Teams, les extensions de messagerie, les webhooks entrants et Bot Framework prennent en charge les cartes adaptatives. Les cartes adaptatives sont une infrastructure ouverte de plateforme de cartes croisées qui peut être utilisée sur toutes les plateformes telles que Windows, Android, iOS, etc. Actuellement, les [connecteurs Teams](../../webhooks-and-connectors/how-to/connectors-creating.md) ne prennent pas en charge les cartes adaptatives. Toutefois, il est possible de créer un [flux](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) qui publie des cartes adaptatives sur un canal Teams.
> * Pour plus d’informations sur les cartes et les webhooks, consultez [Cartes adaptatives et Webhooks entrants.](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)

## <a name="create-incoming-webhook"></a>Créer un webhook entrant

**Pour ajouter un webhook entrant à un canal Teams**

1. Accédez au canal dans lequel vous souhaitez ajouter le webhook, puis sélectionnez &#8226;&#8226;&#8226; **Plus d’options** à partir de la barre de navigation supérieure.
1. Sélectionnez **Connecteurs** dans le menu déroulant :

    ![Sélectionner Connecteur](~/assets/images/connectors.png)

1. Recherchez le **Webhook entrant** sélectionnez **Ajouter**.
1. Sélectionnez **Configurer**, fournissez un nom et chargez une image pour votre webhook si nécessaire :

    ![Bouton Configurer](~/assets/images/configure.png)

1. La fenêtre de dialogue présente une URL unique qui est mappée au canal. Pour envoyer des informations à Microsoft Teams, copiez et enregistrez l’URL du webhook et sélectionnez **Terminé** :

    ![URL unique](~/assets/images/url.png)

Le webhook est disponible dans le canal Teams.

Vous pouvez créer et envoyer des messages actionnables via le webhook entrant ou le connecteur Office 365. Pour plus d’informations, consultez [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md).

> [!NOTE]
> Dans Teams, sélectionnez **Paramètres** > **Autorisations des membres** > **Autoriser les membres à créer, mettre à jour et supprimer des connecteurs**, afin que tout membre d’équipe puisse ajouter, modifier ou supprimer un connecteur.

## <a name="remove-incoming-webhook"></a>Supprimer un webhook entrant

**Pour supprimer un webhook entrant d’un canal Teams**

1. Accédez au canal.
1. Sélectionnez&#8226;&#8226;&#8226; **Plus d’options** dans la barre de navigation supérieure.
1. Sélectionnez **Connecteurs** dans le menu déroulant.
1. Sur la gauche, sous **Gérer,** sélectionnez **Configuré**.
1. Sélectionnez le **<*1*> Configuré** pour voir la liste de vos connecteurs actuels :

    ![Webhook configuré](~/assets/images/configured.png)

1. Sélectionnez **Gérer** à côté du connecteur que vous souhaitez supprimer :

    ![Gérer le webhook](~/assets/images/manage.png)

1. Sélectionnez **Supprimer** :

    ![Supprimer un webhook](~/assets/images/remove.png)

    La boîte de dialogue **Supprimer la configuration** s’affiche :

    ![Supprimer la configuration](~/assets/images/removeconfiguration.png)

1. Complétez les champs et les case à cocher de la boîte de dialogue, puis sélectionnez **Supprimer** :

    ![Suppression finale](~/assets/images/finalremove.png)

    Le webhook est supprimé du canal Teams.

## <a name="see-also"></a>Voir aussi

* [Créer un webhook sortant](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Créer un connecteur Office 365](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [Créer et envoyer des messages](~/webhooks-and-connectors/how-to/connectors-using.md)
* [Créer un bouton de partage pour Teams](../../concepts/build-and-test/share-to-teams.md#create-share-to-teams-button)
* [Intégrer les applications Web](~/samples/integrate-web-apps-overview.md)
