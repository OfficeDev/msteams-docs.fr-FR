---
title: Recevoir tous les messages de canal avec RSC
author: surbhigupta12
description: Recevoir tous les messages de canal avec des autorisations RSC
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 833bdbc015cf852fcd899ce4e75f742448b89978
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631325"
---
# <a name="receive-all-channel-messages-with-rsc"></a>Recevoir tous les messages de canal avec RSC

> [!NOTE]
> Cette fonctionnalité est actuellement disponible en prévisualisation [pour les développeurs publics](../../../resources/dev-preview/developer-preview-intro.md) uniquement.

Le modèle d’autorisations de consentement spécifique aux ressources(RSC), développé à l’origine pour Teams Graph API, est désormais étendu aux scénarios de bot.

Actuellement, les bots peuvent uniquement recevoir des messages de canal utilisateur lorsqu’ils sont @mentioned. À l’aide de RSC, vous pouvez désormais demander aux propriétaires d’équipe de consentir à ce qu’un bot reçoie des messages utilisateur sur les canaux standard d’une équipe sans @mentioned. Cette fonctionnalité est activée en spécifiant l’autorisation dans le manifeste d’une `ChannelMessage.Read.Group` application Teams RSC. Après la configuration, les propriétaires d’équipe peuvent donner leur consentement pendant le processus d’installation de l’application.

Pour plus d’informations sur l’activation du RSC pour votre application, voir le consentement spécifique à [la ressource dans Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).

## <a name="enable-bots-to-receive-all-channel-messages"></a>Activer les bots pour recevoir tous les messages de canal

`ChannelMessage.Read.Group`L’autorisation RSC est étendue aux bots. Avec le consentement de l’utilisateur, cette autorisation permet aux applications graphiques d’obtenir tous les messages d’une conversation et aux robots de recevoir tous les messages de canal sans être @mentioned.

## <a name="update-app-manifest"></a>Mettre à jour le manifeste de l’application

Pour que votre bot reçoit tous les messages de canal, RSC doit être configuré dans le manifeste Teams’application avec l’autorisation spécifiée `ChannelMessage.Read.Group` dans la `webApplicationInfo` propriété.

![Mettre à jour le manifeste de l’application](~/bots/how-to/conversations/Media/appmanifest.png)

Voici un exemple de `webApplicationInfo` l’objet :

* **id**: ID de votre Azure Active Directory (AAD). Il peut s’en trouver de même que votre ID de bot.
* **ressource**: Toute chaîne. Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur.
* **applicationPermissions**: les autorisations RSC pour votre application doivent `ChannelMessage.Read.Group` être spécifiées. Pour plus d’informations, [voir autorisations spécifiques aux ressources.](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)

Le code suivant fournit un exemple de manifeste d’application :

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team-to-test"></a>Chargement de version test dans une équipe

Pour tester le chargement d’une version test dans une équipe, si tous les messages de canal d’une équipe avec RSC sont reçus sans être @mentioned :

1. Sélectionnez ou créez une équipe.
1. Sélectionnez les &#x25CF;&#x25CF;&#x25CF; dans le volet gauche. Le menu déroulant s’affiche.
1. Sélectionnez **Gérer l’équipe** dans le menu déroulant. Les détails s’affichent.

   ![Gestion des applications en équipe](~/bots/how-to/conversations/Media/managingteam.png)

1. Sélectionner **les applications**. Plusieurs applications s’affichent.
1. Sélectionnez **Télécharger une application personnalisée dans** le coin inférieur droit.

    ![Téléchargement d’une application personnalisée](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. Sélectionnez le package d’application dans la **boîte de** dialogue Ouvrir.
1. Sélectionnez **Ouvrir**.

    ![Sélection d’un package d’application](~/bots/how-to/conversations/Media/selectapppackage.png)

1. Sélectionnez **Ajouter** dans la fenêtre pop-up des détails de l’application pour ajouter le bot à votre équipe sélectionnée.

    ![Ajout du bot](~/bots/how-to/conversations/Media/addingbot.png)

1. Sélectionnez un canal et entrez un message dans le canal pour votre bot.

    Le bot reçoit le message sans être @mentioned.

    ![Le bot reçoit un message](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="see-also"></a>Voir aussi

* [Conversations de robots](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [Consentement spécifique à la ressource](/microsoftteams/resource-specific-consent)
* [Tester le consentement spécifique aux ressources](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Télécharger’application personnalisée dans Teams](~/concepts/deploy-and-publish/apps-upload.md)
