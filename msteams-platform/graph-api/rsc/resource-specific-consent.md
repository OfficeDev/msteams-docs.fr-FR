---
title: Activer le consentement spécifique à la ressource dans Teams
description: Dans ce module, découvrez le consentement spécifique aux ressources dans Microsoft Teams et comment en tirer parti.
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: f311723aa6bdb9fc95207169b7ab55434d246509
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66144354"
---
# <a name="resource-specific-consent"></a>Consentement spécifique à la ressource

> [!NOTE]
> Le consentement spécifique à la ressource pour l’étendue de conversation est disponible dans [préversion publique des développeurs](../../resources/dev-preview/developer-preview-intro.md) uniquement.

Le consentement spécifique à la ressource (RSC) est une intégration d’API Microsoft Teams et Microsoft Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des ressources spécifiques, équipes ou conversations, au sein d’une organisation. Le modèle d’autorisations RSC permet aux *propriétaires d’équipe* et aux *propriétaires de conversation* d’accorder le consentement pour qu’une application puisse accéder aux données d’une équipe et les modifier, respectivement.

**Remarque :** Si une conversation est associée à une réunion ou à un appel, les autorisations RSC appropriées s’appliquent également à ces ressources.

## <a name="resource-specific-permissions"></a>Autorisations spécifiques à la ressource

Les autorisations RSC granulaires spécifiques à Teams définissent ce qu’une application peut faire dans une ressource spécifique.

### <a name="resource-specific-permissions-for-a-team"></a>Autorisations spécifiques aux ressources pour une équipe

|Autorisation d’application| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtenez les paramètres de cette équipe.|
|TeamSettings.ReadWrite.Group|Mettez à jour les paramètres de cette équipe.|
|ChannelSettings.Read.Group|Obtenez les noms de canaux, les descriptions de canal et les paramètres de canal de cette équipe.|
|ChannelSettings.ReadWrite.Group|Mettez à jour les noms des canaux de cette équipe, les descriptions des canaux et les paramètres des canaux sans utilisateur connecté.|
|Channel.Create.Group|Créer des canaux au sein de cette équipe. |
|Channel.Delete.Group|Supprimer des canaux dans cette équipe. |
|ChannelMessage.Read.Group |Obtenez les messages de canal de cette équipe. |
|TeamsAppInstallation.Read.Group|Obtenez la liste des applications installées de cette équipe.|
|TeamsTab.Read.Group|Obtenez la liste des onglets de cette équipe.|
|TeamsTab.Create.Group|Créer des onglets au sein cette équipe. |
|TeamsTab.ReadWrite.Group|Mettez à jour les onglets de cette équipe. |
|TeamsTab.Delete.Group|Supprimer les onglets de cette équipe. |
|TeamMember.Read.Group|Obtenez les membres de cette équipe. |
|TeamsActivity.Send.Group|Créer des notifications dans les flux d’activité des utilisateurs de cette équipe. |

Pour plus d’informations, consultez [autorisations de consentement spécifiques aux ressources de l’équipe](/graph/permissions-reference#teams-resource-specific-consent-permissions).

### <a name="resource-specific-permissions-for-a-chat"></a>Autorisations spécifiques aux ressources pour une conversation

Le tableau suivant fournit des autorisations spécifiques aux ressources pour une conversation :

|Autorisation d’application| Action |
| ----- | ----- |
| ChatSettings.Read.Chat         | Obtenez les paramètres de cette conversation.                                    |
| ChatSettings.ReadWrite.Chat    | Lire les paramètres de cette équipe.                          |
| ChatMessage.Read.Chat          | Obtenez les messages de cette conversation.                                    |
| ChatMember.Read.Chat           | Obtenez les membres de cette conversation.                                     |
| Chat.Manage.Chat               | Gérer cette conversation.                                             |
| TeamsTab.Read.Chat             | Obtenez les onglets de cette conversation.                                        |
| TeamsTab.Create.Chat           | Créer des onglets au sein cette conversation.                                     |
| TeamsTab.Delete.Chat           | Supprimer les onglets de cette conversation.                                      |
| TeamsTab.ReadWrite.Chat        | Gérer les onglets de cette conversation.                                      |
| TeamsAppInstallation.Read.Chat | Obtenez les applications installées dans cette conversation.                   |
| OnlineMeeting.ReadBasic.Chat   | Lecture des propriétés de base, telles que le nom, la planification, l’organisateur, le lien de jointure et les notifications de début/fin, d’une réunion associée à cette conversation. |
| Calls.AccessMedia.Chat         | Accéder aux flux multimédias dans les appels associés à cette conversation ou réunion                                    |
| Calls.JoinGroupCalls.Chat         | Participer aux appels associés à cette conversation ou réunion                                    |
| TeamsActivity.Send.Chat         | Créer des notifications dans les flux d’activité des utilisateurs de cette conversation. |

Pour plus d’informations, consultez [autorisations de consentement spécifiques à la ressource de conversation](/graph/permissions-reference#chat-resource-specific-consent-permissions).

> [!NOTE]
> Les autorisations spécifiques aux ressources sont uniquement disponibles pour les applications Teams installées sur le client Teams et ne font actuellement pas partie du portail Azure Active Directory (AAD).

## <a name="enable-rsc-in-your-application"></a>Activer RSC dans votre application

1. [Configurer les paramètres de consentement dans le portail Azure AD](#configure-consent-settings-in-the-azure-ad-portal).
    1. [Configurer les paramètres de consentement du propriétaire du groupe pour RSC dans une équipe](#configure-group-owner-consent-settings-for-rsc-in-a-team).
    1. [Configurer les paramètres de consentement utilisateur pour RSC dans une conversation](#configure-user-consent-settings-for-rsc-in-a-chat).
1. [Inscrire votre application auprès de la plateforme d’identités Microsoft à l’aide du portail Azure AD](#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).
1. [Passez en revue les autorisations de votre application dans le portail Azure AD](#review-your-application-permissions-in-the-azure-ad-portal).
1. [Obtenez un jeton d’accès à partir de la plateforme d’identités](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Mettre à jour le manifeste de votre application Teams](#update-your-teams-app-manifest).
1. [Installez votre application directement dans Teams](#sideload-your-app-in-teams).
1. [Vérifiez que votre application a ajouté des autorisations RSC](#check-your-app-for-added-rsc-permissions).
    1. [Vérifiez que votre application a ajouté des autorisations RSC dans une équipe](#check-your-app-for-added-rsc-permissions-in-a-team).
    1. [Vérifiez que votre application a ajouté des autorisations RSC dans une conversation](#check-your-app-for-added-rsc-permissions-in-a-chat).

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a>Configurer les paramètres de consentement dans le portail Azure AD

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>Configurer les paramètres de consentement du propriétaire du groupe pour RSC dans une équipe

Vous pouvez activer ou désactiver [le consentement du propriétaire du groupe](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directement dans le Portail Microsoft Azure :

1. Connectez-vous au [Portail Azure](https://portal.azure.com) en tant qu’administrateur général [ou administrateur d’entreprise](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).
1. Sélectionnez **Azure Active Directory** > **Applications d’entreprise** > **Consentement et autorisations** > [**Paramètres de consentement utilisateur**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).
1. Activez, désactivez ou limitez le consentement de l’utilisateur avec le contrôle étiqueté **consentement du propriétaire du groupe pour les applications accédant aux données**. La valeur par défaut est **Autoriser le consentement du propriétaire du groupe pour tous les propriétaires de groupe**. Pour qu’un propriétaire d’équipe installe une application à l’aide de RSC, le consentement du propriétaire du groupe doit être activé pour cet utilisateur.

    ![Configuration de l’équipe Azure RSC](../../assets/images/azure-rsc-team-configuration.png)

En outre, vous pouvez activer ou désactiver le consentement du propriétaire du groupe à l’aide de PowerShell. Suivez les étapes décrites dans [configurer le consentement du propriétaire du groupe à l’aide de PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>Configurer les paramètres de consentement de l’utilisateur pour RSC dans une conversation

Vous pouvez activer ou désactiver le[consentement de l’utilisateur](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directement dans le Portail Azure :

1. Connectez-vous au [Portail Azure](https://portal.azure.com) en tant qu’administrateur général [ou administrateur d’entreprise](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).
1. Sélectionnez **Azure Active Directory** > **Applications d’entreprise** > **Consentement et autorisations** > [**Paramètres de consentement utilisateur**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).
1. Activez, désactivez ou limitez le consentement de l’utilisateur avec le contrôle étiqueté **Consentement de l’utilisateur pour les applications**. La valeur par défaut est **Autoriser le consentement de l’utilisateur pour les applications**. Pour qu’un membre de conversation installe une application à l’aide de RSC, le consentement de l’utilisateur doit être activé pour cet utilisateur.

    ![Configuration de conversation Azure RSC](../../assets/images/azure-rsc-chat-configuration.png)

En outre, vous pouvez activer ou désactiver le consentement de l’utilisateur à l’aide de PowerShell. Suivez les étapes décrites dans [configurer le consentement de l’utilisateur à l’aide de PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell).

## <a name="register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal"></a>Inscrire votre application auprès de la plateforme d’identités Microsoft à l’aide du portail Azure AD

Le portail Azure AD fournit une plateforme centrale pour vous permettre d’inscrire et de configurer vos applications. Votre application doit être inscrite dans le portail Azure AD pour s’intégrer à la plateforme d’identité et appeler des API Microsoft Graph. Pour plus d’informations, consultez [inscrire une application auprès de la plateforme d’identité](/graph/auth-register-app-v2).

> [!WARNING]
> Un ID d’application Azure AD ne doit pas être partagé entre plusieurs applications Teams. Il doit y avoir un mappage 1:1 entre une application Teams et une application Azure AD. Les tentatives d’installation de plusieurs applications Teams associées au même ID d’application Azure AD entraînent des échecs d’installation ou d’exécution.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Passer en revue les autorisations de votre application dans le portail Azure AD

1. Accédez à la page **Accueil** >  **inscriptions d'applications** et sélectionnez votre application RSC.
1. Choisissez **autorisations d’API** dans le volet gauche et parcourez la liste des **autorisations configurées** pour votre application. Si votre application effectue uniquement des appels RSC API Graph, supprimez toutes les autorisations sur cette page. Si votre application effectue également des appels non RSC, conservez ces autorisations en fonction des besoins.

> [!IMPORTANT]
> Le portail Azure AD ne peut pas être utilisé pour demander des autorisations RSC. Les autorisations RSC sont actuellement exclusives aux applications Teams installées dans le client Teams et sont déclarées dans le fichier manifeste d’application Teams (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtenir un jeton d’accès à partir de la plateforme d’identités Microsoft

Pour effectuer API Graph appels, vous devez obtenir un jeton d’accès pour votre application à partir de la plateforme d’identité. Pour que votre application puisse obtenir un jeton à partir de la plateforme d’identité, elle doit être inscrite dans le portail Azure AD. Le jeton d’accès contient des informations sur votre application et les autorisations dont elle dispose pour les ressources et les API disponibles via Microsoft Graph.

Vous devez disposer des valeurs suivantes à partir du processus d’inscription Azure AD pour récupérer un jeton d’accès à partir de la plateforme d’identité :

* L’**ID d’application** affecté par le portail d’inscription des applications. Si votre application prend en charge l’authentification unique (SSO), vous devez utiliser le même ID d’application pour votre application et l’authentification unique.
* La clé secrète **client/mot de passe** ou paire de clés publique ou privée qui est **Certificate**. N’est pas nécessaire pour les applications natives.
* **URI de redirection** ou URL de réponse pour que votre application reçoive des réponses de Azure AD.

Pour plus d’informations, consultez [obtenir l’accès au nom d’un utilisateur](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) et [obtenir l’accès sans utilisateur](/graph/auth-v2-service).

## <a name="update-your-teams-app-manifest"></a>Mettre à jour le manifeste de votre application Teams

Les autorisations RSC sont déclarées dans le fichier JSON du manifeste de votre application.

> [!IMPORTANT]
> Les autorisations non RSC sont stockées dans le Portail Azure. Ne les ajoutez pas au manifeste de l’application.

### <a name="manifest-changes-for-resource-specific-consent"></a>Modifications du manifeste pour le consentement spécifique à la ressource

<br>

<details>

<summary><b>Autorisations RSC pour le manifeste d’application version 1.12</b></summary>

Ajoutez une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

|Nom| Type | Description|
|---|---|---|
|`id` |Chaîne |Votre ID d’application Azure AD. Pour plus d’informations, consultez [inscrire votre application dans le portail Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|Chaîne| Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne le fera.|

Spécifiez les autorisations nécessaires à l’application.

|Nom| Type | Description|
|---|---|---|
|`authorization`|Objet|Liste des autorisations dont l’application a besoin pour fonctionner. Pour plus d’informations, consultez [espace réservé pour l’autorisation de lien dans le manifeste]

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

<br>

</details>

<br>

<details>

<summary><b>Autorisations RSC pour le manifeste d’application version 1.11 ou antérieure</b></summary>

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

> [!NOTE]
> Si l’application est destinée à prendre en charge l’installation dans les étendues d’équipe et de conversation, les autorisations d’équipe et de conversation peuvent être spécifiées dans le même manifeste sous `applicationPermissions`.

<br>

</details>

## <a name="sideload-your-app-in-teams"></a>Charger une version test de votre application dans Teams

Si votre administrateur Teams autorise les chargements d’applications personnalisées, vous pouvez [charger une version test de votre application](~/concepts/deploy-and-publish/apps-upload.md) directement à une équipe ou à une conversation spécifique.

## <a name="check-your-app-for-added-rsc-permissions"></a>Vérifier si votre application dispose d’autorisations RSC ajoutées

> [!IMPORTANT]
> Les autorisations RSC ne sont pas attribuées à un utilisateur. Les appels sont effectués avec des autorisations d’application, et non avec des autorisations déléguées par l’utilisateur. L’application peut être autorisée à effectuer des actions que l’utilisateur ne peut pas effectuer, telles que la suppression d’un onglet. Vous devez examiner l’intention du propriétaire de l’équipe ou du propriétaire de la conversation pour votre utilisation avant d’effectuer des appels d’API RSC. Pour plus d’informations, consultez [vue d’ensemble de l’API Microsoft Teams](/graph/teams-concept-overview).

Une fois l’application installée sur une ressource, vous pouvez utiliser [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) pour afficher les autorisations qui ont été accordées à l’application dans la ressource.

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>Vérifier que votre application a ajouté des autorisations RSC dans une équipe

1. Obtenez le **groupId** de l’équipe à partir de Teams.
1. Dans Teams, sélectionnez **Teams** dans le volet le plus à gauche.
1. Sélectionnez l’équipe dans laquelle l’application doit être installée.
1. Sélectionnez les points de suspension &#x25CF;&#x25CF;&#x25CF; pour cette équipe.
1. Sélectionnez **Obtenir un lien vers l’équipe** dans le menu déroulant De l’équipe.
1. Copiez et enregistrez la valeur **groupId** à partir de la boîte de dialogue contextuelle **Obtenir un lien vers l’équipe** boîte de dialogue contextuelle.
1. Connectez-vous à **l’Explorateur Graph**.
1. Effectuez un appel **GET** à ce point de terminaison : `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`. Le champ `clientAppId` dans la réponse est mappé au `webApplicationInfo.id` spécifié dans le manifeste de l’application Teams.

    ![Afficheur Graph réponse à l’appel GET pour les autorisations RSC d’équipe](../../assets/images/team-graph-permissions.png)

Pour plus d’informations sur la façon d’obtenir des détails sur les applications installées dans une équipe spécifique, consultez [obtenir les noms et autres détails des applications installées dans l’équipe spécifiée](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>Vérifier que votre application a ajouté des autorisations RSC dans une conversation

1. Obtenez l’ID de thread de conversation à partir du client *web* Teams.
1. Dans le client web Teams, sélectionnez **conversation** dans le volet le plus à gauche.
1. Sélectionnez la conversation dans laquelle l’application est installée dans le menu déroulant.
1. Copiez l’URL web et enregistrez l’ID de thread de conversation à partir de la chaîne.

    ![ID de thread de conversation à partir de l’URL web](../../assets/images/chat-thread-id.png)

1. Connectez-vous à **l’Explorateur Graph**.
1. Effectuez un appel **GET** au point de terminaison suivant : `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`. Le champ `clientAppId` dans la réponse est mappé au `webApplicationInfo.id` spécifié dans le manifeste de l’application Teams.

    ![Afficheur Graph réponse à l’appel GET pour les autorisations RSC de conversation](../../assets/images/chat-graph-permissions.png)

Pour plus d’informations sur la façon d’obtenir les détails des applications installées dans une conversation spécifique, consultez [obtenir les noms et d’autres détails des applications installées dans la conversation spécifiée](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat).

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Consentement spécifique à la ressource (RSC) | Utilisez RSC pour appeler les API Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>Voir aussi

* [Tester les autorisations de consentement spécifiques aux ressources dans Teams](test-resource-specific-consent.md)
* [Consentement spécifique à la ressource dans Microsoft Teams pour les administrateurs](/MicrosoftTeams/resource-specific-consent)
