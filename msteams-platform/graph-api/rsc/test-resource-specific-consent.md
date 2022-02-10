---
title: Tester les autorisations de consentement propres aux ressources dans Teams
description: Détails du test du consentement spécifique aux ressources Teams l’aide de Postman avec des exemples de code
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: autorisation OAuth SSO teams Microsoft Azure Active Directory (Azure AD) rsc Postman Graph
ms.openlocfilehash: 15a2a80a8f1ce280b462ed6e6e99242fb30f0dc3
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518120"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Tester les autorisations de consentement propres aux ressources dans Teams

> [!NOTE]
> Le consentement spécifique aux ressources pour l’étendue de conversation est disponible en [prévisualisation pour les développeurs publics](../../resources/dev-preview/developer-preview-intro.md) uniquement.

Le consentement spécifique aux ressources (RSC) est une intégration d’API Microsoft Teams et Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des ressources spécifiques (équipes ou conversations) au sein d’une organisation. Pour plus d’informations, voir [consentement spécifique aux ressources (RSC) — Microsoft Teams Graph API](resource-specific-consent.md).

## <a name="prerequisites"></a>Configuration requise

Assurez-vous de vérifier les modifications de manifeste d’application suivantes pour le consentement spécifique aux ressources avant de tester :

<br>

<details>

<summary><b>Autorisations RSC pour la version 1.12 du manifeste d’application</b></summary>

Ajoutez [une clé webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

|Nom| Type | Description|
|---|---|---|
|`id` |String |Votre ID Microsoft Azure Active Directory (Azure AD) d’application. Pour plus d’informations, voir [inscrire votre application dans le portail Microsoft Azure Active Directory (Azure AD).](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)|
|`resource`|String| Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne le fera.|

Spécifiez les autorisations requises par l’application.

|Nom| Type | Description|
|---|---|---|
|`authorization`|Objet|Liste des autorisations dont l’application a besoin pour fonctionner. Pour plus d’informations, voir [autorisation](../../resources/schema/manifest-schema.md#authorization).|

Exemple pour RSC dans une équipe

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "TeamSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Create.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Delete.Group",
                "type": "Application"
            },
            {
                "name": "ChannelMessage.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Group",
                "type": "Application"
            },
            {
                "name": "TeamMember.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Group",
                "type": "Application"
            }
        ]    
    }
}
```

Exemple de RSC dans une conversation

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChatSettings.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatSettings.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMessage.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMember.Read.Chat",
                "type": "Application"
            },
            {
                "name": "Chat.Manage.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Chat",
                "type": "Application"
            },
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.AccessMedia.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.JoinGroupCalls.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Chat",
                "type": "Application"
            }
        ]    
    }
}
```
    
> [!NOTE]
> Si l’application est destinée à prendre en charge l’installation dans les étendues d’équipe et de conversation, les autorisations d’équipe et de conversation peuvent être spécifiées dans le même manifeste `authorization`sous .

</details>

<br>

<details>

<summary><b>Autorisations RSC pour la version 1.11 ou antérieure du manifeste d’application</b></summary>

Ajoutez [une clé webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

|Nom| Type | Description|
|---|---|---|
|`id` |String |Votre ID Microsoft Azure Active Directory (Azure AD) d’application. Pour plus d’informations, voir [inscrire votre application dans le portail Microsoft Azure Active Directory (Azure AD).](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)|
|`resource`|Chaîne| Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne le fera.|
|`applicationPermissions`|Tableau de chaînes|Autorisations RSC pour votre application. Pour plus d’informations, [voir autorisations spécifiques aux ressources](resource-specific-consent.md#resource-specific-permissions).|

Exemple pour RSC dans une équipe

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
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

Exemple de RSC dans une conversation

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
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

<br>

> [!NOTE]
> Si l’application est destinée à prendre en charge l’installation dans les étendues d’équipe et de conversation, les autorisations d’équipe et de conversation peuvent être spécifiées dans le même manifeste `applicationPermissions`sous .
    
</details>

> [!IMPORTANT]
> Dans le manifeste de votre application, incluez uniquement les autorisations RSC dont vous souhaitez que votre application soit propriétaire.

> [!NOTE]
> Si l’application est destinée à accéder aux API d’appel/multimédia, `webApplicationInfo.Id` il doit s’agit de l’ID d’application Microsoft Azure Active Directory (Azure AD) [d’un service de bot Azure](/graph/cloud-communications-get-started#register-a-bot).

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Test ajout d’autorisations RSC à une équipe à l’aide de l’application Postman

Pour vérifier si les autorisations RSC sont honorées par la charge utile de demande d’API, vous devez copier le [code de test JSON RSC](test-team-rsc-json-file.md) pour l’équipe dans votre environnement local et mettre à jour les valeurs suivantes :

* `azureADAppId`: ID d’Microsoft Azure Active Directory (Azure AD) de votre application.
* `azureADAppSecret`: Votre mot Microsoft Azure Active Directory d’application (Azure AD).
* `token_scope`: l’étendue est requise pour obtenir un jeton. définissez la valeur sur https://graph.microsoft.com/.default.
* `teamGroupId`: vous pouvez obtenir l’ID de groupe d’équipe à partir du client Teams comme suit :

    1. Dans le Teams client, sélectionnez **Teams** dans la barre de navigation à l’extrême gauche.
    2. Sélectionnez l’équipe où l’application est installée dans le menu déroulant.
    3. Sélectionnez **l’icône Options** supplémentaires (&#8943;).
    4. **Sélectionnez Obtenir un lien vers l’équipe**. 
    5. Copiez et enregistrez **la valeur groupId** à partir de la chaîne.

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Test ajout d’autorisations RSC à une conversation à l’aide de l’application Postman

Pour vérifier si les autorisations RSC sont honorées par la charge utile de demande d’API, vous devez copier le [code de test JSON RSC](test-chat-rsc-json-file.md) pour les conversations dans votre environnement local et mettre à jour les valeurs suivantes :

* `azureADAppId`: ID d’Microsoft Azure Active Directory (Azure AD) de votre application.
* `azureADAppSecret`: Votre mot Microsoft Azure Active Directory d’application (Azure AD).
* `token_scope`: l’étendue est requise pour obtenir un jeton. définissez la valeur sur https://graph.microsoft.com/.default.
* `tenantId`: nom ou ID d Microsoft Azure Active Directory (Azure AD) de votre client.
* `chatId`: vous pouvez obtenir l’ID de thread de conversation à partir Teams *client web* comme suit :

    1. Dans le Teams web, sélectionnez **Conversation** dans la barre de navigation à l’extrême gauche.
    2. Sélectionnez la conversation dans laquelle l’application est installée dans le menu déroulant.
    3. Copiez l’URL web et enregistrez l’ID de thread de conversation à partir de la chaîne.
![ID de thread de conversation à partir de l’URL web.](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Utiliser Postman

1. Ouvrez [l’application Postman](https://www.postman.com) .
2. **Sélectionnez fichier** **FileImportImport** >  >  pour télécharger le fichier JSON mis à jour à partir de votre environnement.  
3. Sélectionnez **l’onglet Collections** . 
4. Sélectionnez le chevron **>** en regard du **test RSC** pour développer l’affichage des détails et afficher les demandes d’API.

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
