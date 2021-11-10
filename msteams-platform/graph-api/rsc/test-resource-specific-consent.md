---
title: Tester les autorisations de consentement propres aux ressources dans Teams
description: Détails du test du consentement spécifique aux ressources Teams l’aide de Postman avec des exemples de code
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: Autorisation teams OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: fc926e307c2e3ee5d1336c09e264930abe20d9d0
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887719"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Tester les autorisations de consentement propres aux ressources dans Teams

> [!NOTE]
> Le consentement spécifique aux ressources pour l’étendue de conversation est disponible en [prévisualisation pour les](../../resources/dev-preview/developer-preview-intro.md) développeurs publics uniquement.

Le consentement spécifique aux ressources (RSC) est une intégration d’API Microsoft Teams et Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des ressources spécifiques (équipes ou conversations) au sein d’une organisation. Pour plus d’informations, voir consentement spécifique à la [ressource (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).

> [!NOTE]
> Pour tester les autorisations RSC, votre fichier manifeste d’application Teams doit inclure une clé **webApplicationInfo** remplie avec les champs suivants :
>
> - **id :** votre ID Azure AD’application, voir Inscrire votre [application dans le portail Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)
> - **ressource**: n’importe quelle chaîne, voir la remarque dans Mettre à [jour votre Teams manifeste d’application.](resource-specific-consent.md#update-your-teams-app-manifest)
> - **autorisations d’application**: autorisations RSC pour votre application, voir [Autorisations propres aux ressources.](resource-specific-consent.md#resource-specific-permissions)

## <a name="example-for-a-team"></a>Exemple pour une équipe
```json
"webApplicationInfo":{
    "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource":"https://AnyString",
    "applicationPermissions":[
        "TeamSettings.Read.Group",
        "TeamSettings.ReadWrite.Group",
        "ChannelSettings.Read.Group",
        "ChannelSettings.ReadWrite.Group",
        "Channel.Create.Group",
        "Channel.Delete.Group",
        "ChannelMessage.Read.Group",
        "TeamsAppInstallation.Read.Group",
        "TeamsTab.Read.Group",
        "TeamsTab.Create.Group",
        "TeamsTab.ReadWrite.Group",
        "TeamsTab.Delete.Group",
        "TeamMember.Read.Group",
        "TeamsActivity.Send.Group"
    ]
   }
```

## <a name="example-for-a-chat"></a>Exemple pour une conversation
```json
"webApplicationInfo":{
    "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource":"https://AnyString",
    "applicationPermissions":[
        "ChatSettings.Read.Chat",
        "ChatSettings.ReadWrite.Chat",
        "ChatMessage.Read.Chat",
        "ChatMember.Read.Chat",
        "Chat.Manage.Chat",
        "TeamsTab.Read.Chat",
        "TeamsTab.Create.Chat",
        "TeamsTab.Delete.Chat",
        "TeamsTab.ReadWrite.Chat",
        "TeamsAppInstallation.Read.Chat",
        "OnlineMeeting.ReadBasic.Chat",
        "Calls.AccessMedia.Chat",
        "Calls.JoinGroupCalls.Chat",
        "TeamsActivity.Send.Chat"
    ]
   }
```

> [!IMPORTANT]
> Dans le manifeste de votre application, incluez uniquement les autorisations RSC dont vous souhaitez que votre application soit propriétaire.

>[!NOTE]
>Si l’application est destinée à prendre en charge l’installation dans les étendues d’équipe et de conversation, les autorisations d’équipe et de conversation peuvent être spécifiées dans le même manifeste sous `applicationPermissions` .

>Si l’application est destinée à accéder aux API d’appel/de média, il doit s’agit de `webApplicationInfo.Id` l’ID AAD’application [d’un service de bot Azure.](/graph/cloud-communications-get-started#register-a-bot)

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Test ajout d’autorisations RSC à une équipe à l’aide de l’application Postman

Pour vérifier si les autorisations RSC sont honorées par la charge utile de demande d’API, vous devez copier le code de [test JSON RSC](test-team-rsc-json-file.md) pour l’équipe dans votre environnement local et mettre à jour les valeurs suivantes :

* `azureADAppId`: ID d’Azure AD application de votre application.
* `azureADAppSecret`: votre mot Azure AD application.
* `token_scope`: l’étendue est requise pour obtenir un jeton. définissez la valeur sur https://graph.microsoft.com/.default .
* `teamGroupId`: vous pouvez obtenir l’ID de groupe d’équipe à partir du client Teams comme suit :

    1. Dans le Teams client, **sélectionnez Teams** dans la barre de navigation à l’extrême gauche.
    2. Sélectionnez l’équipe où l’application est installée dans le menu déroulant.
    3. Sélectionnez **l’icône Options** supplémentaires (&#8943;).
    4. Sélectionnez **Obtenir un lien vers l’équipe.** 
    5. Copiez et enregistrez **la valeur groupId** à partir de la chaîne.

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Test ajout d’autorisations RSC à une conversation à l’aide de l’application Postman

Pour vérifier si les autorisations RSC sont honorées par la charge utile de demande d’API, vous devez copier le code de [test JSON RSC](test-chat-rsc-json-file.md) pour les conversations dans votre environnement local et mettre à jour les valeurs suivantes :

* `azureADAppId`: ID d’Azure AD application de votre application.
* `azureADAppSecret`: votre mot Azure AD application.
* `token_scope`: l’étendue est requise pour obtenir un jeton. définissez la valeur sur https://graph.microsoft.com/.default .
* `tenantId`: nom ou ID AAD’objet de votre client.
* `chatId`: vous pouvez obtenir l’ID de thread de conversation à partir Teams *client web* comme suit :

    1. Dans le Teams web, sélectionnez **Conversation** dans la barre de navigation à l’extrême gauche.
    2. Sélectionnez la conversation dans laquelle l’application est installée dans le menu déroulant.
    3. Copiez l’URL web et enregistrez l’ID de thread de conversation à partir de la chaîne.
![ID de thread de conversation à partir de l’URL web.](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Utiliser Postman

1. Ouvrez [l’application Postman.](https://www.postman.com)
2. Sélectionnez   >  **le fichier**  >  **d’importation de** fichiers pour télécharger le fichier JSON mis à jour à partir de votre environnement.  
3. Sélectionnez **l’onglet Collections.** 
4. Sélectionnez le chevron en regard du test RSC pour développer l’affichage des **>** détails et afficher les demandes d’API. 

Exécutez l’ensemble de la collection d’autorisations pour chaque appel d’API. Les autorisations que vous avez spécifiées dans le manifeste de votre application doivent réussir, tandis que celles qui ne sont pas spécifiées doivent échouer avec un code d’état HTTP 403. Vérifiez tous les codes d’état de réponse pour vérifier que le comportement des autorisations RSC dans votre application répond aux attentes.

> [!NOTE]
> Pour tester des appels d’API DELETE et READ spécifiques, ajoutez ces scénarios d’instance au fichier JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Tester les autorisations RSC révoquées à l’aide [de Postman](https://www.postman.com/)

1. Désinstallez l’application de la ressource spécifique.
2. Suivez les étapes pour la conversation ou l’équipe : 
    1. [Test a ajouté des autorisations RSC à une équipe à l’aide de Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).
    2. [Test a ajouté des autorisations RSC à une conversation à l’aide de Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).
3. Vérifiez tous les codes d’état de réponse pour vérifier que les appels d’API spécifiques ont échoué avec un code d’état **HTTP 403**.

## <a name="see-also"></a>Voir aussi

* [API et Graph microsoft Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [Consentement spécifique à la ressource](~/graph-api/rsc/resource-specific-consent.md)
