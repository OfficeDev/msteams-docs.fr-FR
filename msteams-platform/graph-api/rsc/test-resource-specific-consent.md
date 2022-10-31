---
title: Tester les autorisations de consentement spécifiques aux ressources dans Teams
description: Détails du test du consentement spécifique à la ressource dans Teams à l’aide de Postman avec des exemples de code
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams authorization OAuth SSO Microsoft Azure Active Directory (Azure AD) rsc Postman Graph
ms.openlocfilehash: ade66f40662140b86fcc9ae2e185fc10ea09d2f2
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791712"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Tester les autorisations de consentement spécifiques aux ressources dans Teams

> [!NOTE]
> Le consentement spécifique à la ressource pour l’étendue de conversation est disponible dans [préversion publique des développeurs](../../resources/dev-preview/developer-preview-intro.md) uniquement.

Le consentement spécifique à la ressource (RSC) est une intégration de Microsoft Teams et de API Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des équipes— ou des conversations— spécifiques au sein d’une organisation. Pour plus d’informations, consultez [consentement spécifique à la ressource (RSC) — Microsoft Teams API Graph](resource-specific-consent.md).

## <a name="prerequisites"></a>Configuration requise

Vérifiez que vous vérifiez les modifications de manifeste d’application suivantes pour le consentement spécifique à la ressource avant de tester :

<br>

<details>

<summary><b>Autorisations RSC pour le manifeste d’application version 1.12 et ultérieure</b></summary>

Ajoutez une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

|Nom| Type | Description|
|---|---|---|
|`id` |Chaîne |Votre ID d’application Azure AD. Pour plus d’informations, consultez [inscrire votre application dans le portail Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|Chaîne| Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne le fera.|

Spécifiez les autorisations nécessaires à l’application.

|Nom| Type | Description|
|---|---|---|
|`authorization`|Objet|Liste des autorisations dont l’application a besoin pour fonctionner. Pour plus d’informations, consultez [d’autorisation](../../resources/schema/manifest-schema.md#authorization).|

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

Exemple pour RSC dans une conversation

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
> Si l’application est destinée à prendre en charge l’installation dans les étendues d’équipe et de conversation, les autorisations d’équipe et de conversation peuvent être spécifiées dans le même manifeste sous `authorization`.

</details>

<br>

<details>

<summary><b>Autorisations RSC pour le manifeste d’application version 1.11 et antérieure</b></summary>

Ajoutez une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

|Nom| Type | Description|
|---|---|---|
|`id` |Chaîne |Votre ID d’application Azure AD. Pour plus d’informations, consultez [inscrire votre application dans le portail Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|Chaîne| Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne le fera.|
|`applicationPermissions`|Tableau de chaînes|Définir les autorisations pour votre application. Pour plus d’informations, consultez [autorisations spécifiques à la ressource](resource-specific-consent.md#resource-specific-permissions).|

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

Exemple pour RSC dans une conversation

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
> Si l’application est destinée à prendre en charge l’installation dans les étendues d’équipe et de conversation, les autorisations d’équipe et de conversation peuvent être spécifiées dans le même manifeste sous `applicationPermissions`.

</details>

> [!IMPORTANT]
> Dans le manifeste de votre application, incluez uniquement les autorisations RSC que vous souhaitez que votre application ait.

> [!NOTE]
> Si l’application est destinée à accéder aux API d’appel/média, la `webApplicationInfo.Id` doit être l’ID d’application Azure AD d’un [Azure Bot Service](/graph/cloud-communications-get-started#register-a-bot).

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>Tester les autorisations RSC ajoutées à une équipe à l’aide de l’application Postman

Pour vérifier si les autorisations RSC sont respectées par la charge utile de la demande d’API, vous devez copier le code de test JSON [RSC pour les](test-team-rsc-json-file.md) d’équipe dans votre environnement local et mettre à jour les valeurs suivantes :

* `azureADAppId` : ID d’application Azure AD de votre application.
* `azureADAppSecret` : mot de passe de votre application Azure AD.
* `token_scope`: l’étendue est requise pour obtenir un jeton. Définissez la valeur sur `https://graph.microsoft.com/.default`.
* `teamGroupId` : vous pouvez obtenir l’ID de groupe d’équipe à partir du client Teams comme suit :

    1. Dans le client Teams, sélectionnez **Teams** dans la barre de navigation située à l’extrême gauche.
    2. Sélectionnez l’équipe dans laquelle l’application est installée dans le menu déroulant.
    3. Sélectionnez l’icône **Autres options** (&#8943;).
    4. Sélectionnez **Obtenir le lien vers l’équipe**.
    5. Copiez et enregistrez la valeur **groupId** à partir de la chaîne.

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>Tester les autorisations RSC ajoutées à une conversation à l’aide de l’application Postman

Pour vérifier si les autorisations RSC sont respectées par la charge utile de la demande d’API, vous devez copier le code de test JSON [RSC pour les conversations](test-chat-rsc-json-file.md) dans votre environnement local et mettre à jour les valeurs suivantes :

* `azureADAppId` : ID d’application Azure AD de votre application.
* `azureADAppSecret` : mot de passe de votre application Azure AD.
* `token_scope`: l’étendue est requise pour obtenir un jeton. Définissez la valeur sur `https://graph.microsoft.com/.default`.
* `tenantId` : nom ou ID d’objet Azure AD de votre locataire.
* `chatId`: vous pouvez obtenir l’ID du thread de conversation à partir du client *web* Teams comme suit :

    1. Dans le client web Teams, sélectionnez **conversation** dans la barre de navigation située à l’extrême gauche.
    2. Sélectionnez la conversation dans laquelle l’application est installée dans le menu déroulant.
    3. Copiez l’URL web et enregistrez l’ID de thread de conversation à partir de la chaîne.
![ID de thread de conversation à partir de l’URL web.](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>Utiliser Postman

1. Ouvrez l’application [Postman](https://www.postman.com).
2. Sélectionnez **Fichier** > **Importer** > **Importer le fichier** pour charger le fichier JSON mis à jour à partir de votre environnement.  
3. Sélectionnez l’onglet **Collections**.
4. Sélectionnez le chevron **>** à côté de **Test RSC** pour développer la vue détaillée et voir les demandes API.

Exécutez l’intégralité de la collection d’autorisations pour chaque appel d’API. Les autorisations que vous avez spécifiées dans le manifeste de votre application doivent réussir, tandis que celles qui ne sont pas spécifiées doivent échouer avec un code d’état HTTP 403. Vérifiez tous les codes d’état de réponse pour vérifier que le comportement des autorisations RSC dans votre application répond aux attentes.

> [!NOTE]
> Pour tester des appels d’API DELETE et READ spécifiques, ajoutez ces scénarios d’instance au fichier JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Tester les autorisations RSC révoquées à l’aide de [Postman](https://www.postman.com/)

1. Désinstallez l’application de la ressource spécifique.
2. Suivez les étapes pour la conversation ou l’équipe :
    1. [Test a ajouté des autorisations RSC à une équipe à l’aide de Postman](#test-added-rsc-permissions-to-a-team-using-the-postman-app).
    2. [Test a ajouté des autorisations RSC à une conversation à l’aide de Postman](#test-added-rsc-permissions-to-a-chat-using-the-postman-app).
3. Vérifiez tous les codes d’état de réponse pour vérifier que les appels d’API spécifiques **ont échoué avec un code d’état HTTP 403**.

## <a name="see-also"></a>Voir aussi

* [MICROSOFT GRAPH API et Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [Consentement spécifique à la ressource](~/graph-api/rsc/resource-specific-consent.md)
