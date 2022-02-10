---
title: Activer le consentement spécifique aux ressources dans Teams
description: Décrit le consentement spécifique aux ressources Teams et comment en tirer parti.
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: autorisation oAuth d’autorisation oAuth Azure AD rsc Graph
ms.openlocfilehash: dbbda0dced53530c1688faa626bc63fe0bf1be76
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518162"
---
# <a name="resource-specific-consent"></a>Consentement spécifique à la ressource

> [!NOTE]
> Le consentement spécifique aux ressources pour l’étendue de conversation est disponible en [prévisualisation pour les développeurs publics](../../resources/dev-preview/developer-preview-intro.md) uniquement.

Le consentement spécifique aux ressources (RSC) est une intégration d’API Microsoft Teams et Microsoft Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des ressources spécifiques, équipes ou conversations, au sein d’une organisation. Le modèle d’autorisations RSC  permet aux propriétaires d’équipe et de *conversation* d’accorder le consentement d’une application pour accéder aux données d’une équipe et aux données d’une conversation, et de les modifier, respectivement. 

**Remarque :** Si une conversation est associée à une réunion ou à un appel, les autorisations RSC appropriées s’appliquent également à ces ressources.

## <a name="resource-specific-permissions"></a>Autorisations spécifiques aux ressources

Les autorisations Teams RSC précises et spécifiques définissent ce qu’une application peut faire au sein d’une ressource spécifique.

### <a name="resource-specific-permissions-for-a-team"></a>Autorisations spécifiques aux ressources pour une équipe

|Autorisation d’application| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtenez les paramètres de cette équipe.|
|TeamSettings.ReadWrite.Group|Mettez à jour les paramètres de cette équipe.|
|ChannelSettings.Read.Group|Obtenez les noms de canaux, les descriptions des canaux et les paramètres de canal de cette équipe.|
|ChannelSettings.ReadWrite.Group|Mettez à jour les noms de canaux, les descriptions des canaux et les paramètres de canal de cette équipe.|
|Channel.Create.Group|Créer des canaux au sein de cette équipe. |
|Channel.Delete.Group|Supprimez les canaux de cette équipe. |
|ChannelMessage.Read.Group |Obtenez les messages de canal de cette équipe. |
|TeamsAppInstallation.Read.Group|Obtenez la liste des applications installées de cette équipe.|
|TeamsTab.Read.Group|Obtenir la liste des onglets de cette équipe.|
|TeamsTab.Create.Group|Créer des onglets au sein cette équipe. |
|TeamsTab.ReadWrite.Group|Mettez à jour les onglets de cette équipe. |
|TeamsTab.Delete.Group|Supprimer les onglets de cette équipe. |
|TeamMember.Read.Group|Obtenez les membres de cette équipe. |
|TeamsActivity.Send.Group|Créez des notifications dans les flux d’activités des utilisateurs de cette équipe. |

Pour plus d’informations, consultez les autorisations [de consentement propres aux ressources d’équipe](/graph/permissions-reference#teams-resource-specific-consent-permissions).

### <a name="resource-specific-permissions-for-a-chat"></a>Autorisations spécifiques aux ressources pour une conversation

Le tableau suivant fournit des autorisations spécifiques aux ressources pour une conversation :

|Autorisation d’application| Action |
| ----- | ----- |
| ChatSettings.Read.Chat         | Obtenez les paramètres de cette conversation.                                    |
| ChatSettings.ReadWrite.Chat    | Mettez à jour les paramètres de cette conversation.                          |
| ChatMessage.Read.Chat          | Obtenez les messages de cette conversation.                                    |
| ChatMember.Read.Chat           | Obtenez les membres de cette conversation.                                     |
| Chat.Manage.Chat               | Gérer cette conversation.                                             |
| TeamsTab.Read.Chat             | Obtenez les onglets de cette conversation.                                        |
| TeamsTab.Create.Chat           | Créer des onglets au sein cette conversation.                                     |
| TeamsTab.Delete.Chat           | Supprimer les onglets de cette conversation.                                      |
| TeamsTab.ReadWrite.Chat        | Gérer les onglets de cette conversation.                                      |
| TeamsAppInstallation.Read.Chat | Obtenir les applications installées dans cette conversation.                   |
| OnlineMeeting.ReadBasic.Chat   | Lisez les propriétés de base, telles que le nom, la planification, l’organisateur, le lien de connexion et les notifications de début/fin, d’une réunion associée à cette conversation. |
| Calls.AccessMedia.Chat         | Accéder aux flux multimédias dans les appels associés à cette conversation ou réunion                                    |
| Calls.JoinGroupCalls.Chat         | Participer aux appels associés à cette conversation ou réunion                                    |
| TeamsActivity.Send.Chat         | Créez des notifications dans les flux d’activités des utilisateurs de cette conversation. |

Pour plus d’informations, voir [autorisations de consentement](/graph/permissions-reference#chat-resource-specific-consent-permissions) propres aux ressources de conversation.

> [!NOTE]
> Les autorisations propres aux ressources sont disponibles uniquement pour les applications Teams installées sur le client Teams et ne font actuellement pas partie du portail Azure Active Directory (AAD).

## <a name="enable-rsc-in-your-application"></a>Activer RSC dans votre application

1. [Configurez les paramètres de consentement dans le portail Azure AD web](#configure-consent-settings-in-the-azure-ad-portal).
    1. [Configurez les paramètres de consentement du propriétaire du groupe pour RSC dans une équipe](#configure-group-owner-consent-settings-for-rsc-in-a-team).
    1. [Configurez les paramètres de consentement de l’utilisateur pour RSC dans une conversation](#configure-user-consent-settings-for-rsc-in-a-chat).
1. [Enregistrez votre application auprès Plateforme d'identités Microsoft l’aide Azure AD portail.](#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)
1. [Examinez vos autorisations d’application dans le Azure AD web](#review-your-application-permissions-in-the-azure-ad-portal).
1. [Obtenez un jeton d’accès à partir de la plateforme d’identité](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Mettez à jour Teams manifeste de votre application](#update-your-teams-app-manifest).
1. [Installez votre application directement dans Teams](#sideload-your-app-in-teams).
1. [Vérifiez que votre application a ajouté des autorisations RSC](#check-your-app-for-added-rsc-permissions).
    1. [Vérifiez que votre application a ajouté des autorisations RSC dans une équipe](#check-your-app-for-added-rsc-permissions-in-a-team).
    1. [Vérifiez que votre application a ajouté des autorisations RSC dans une conversation](#check-your-app-for-added-rsc-permissions-in-a-chat).

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a>Configurer les paramètres de consentement dans le portail Azure AD client

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>Configurer les paramètres de consentement du propriétaire du groupe pour RSC dans une équipe

Vous pouvez activer ou [désactiver le consentement](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) du propriétaire du groupe directement dans Microsoft Azure portail :

1. Connectez-vous au [portail Microsoft Azure en](https://portal.azure.com) tant [qu’administrateur général ou administrateur d’entreprise](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).
1. **Sélectionnez Azure Active Directory** >  **Enterprise applicationsConsent** >  **et les paramètres de consentement permissionsUser** > .[](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)
1. Activer, désactiver ou limiter le consentement de l’utilisateur avec le consentement du propriétaire du groupe étiqueté pour les applications accédant **aux données**. La valeur par défaut **est Autoriser le consentement du propriétaire du groupe pour tous les propriétaires du groupe**. Pour qu’un propriétaire d’équipe installe une application à l’aide de RSC, le consentement du propriétaire du groupe doit être activé pour cet utilisateur.

    ![Configuration de l’équipe Azure RSC](../../assets/images/azure-rsc-team-configuration.png)

En outre, vous pouvez activer ou désactiver le consentement du propriétaire du groupe à l’aide de PowerShell, suivez les étapes décrites dans la configuration du consentement du propriétaire du groupe à l’aide [de PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>Configurer les paramètres de consentement de l’utilisateur pour RSC dans une conversation

Vous pouvez activer ou désactiver le consentement de [l’utilisateur](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directement dans Microsoft Azure portail :

1. Connectez-vous au [portail Microsoft Azure en](https://portal.azure.com) tant [qu’administrateur général ou administrateur d’entreprise](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).
1. **Sélectionnez Azure Active Directory** >  **Enterprise applicationsConsent** >  **et les paramètres de consentement permissionsUser** > .[](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)
1. Activer, désactiver ou limiter le consentement de l’utilisateur avec le consentement utilisateur étiqueté pour **le contrôle pour les applications**. La valeur par défaut **est Autoriser le consentement de l’utilisateur pour les applications**. Pour qu’un membre de conversation installe une application à l’aide de RSC, le consentement de l’utilisateur doit être activé pour cet utilisateur.

    ![Configuration de conversation RSC Azure](../../assets/images/azure-rsc-chat-configuration.png)

En outre, vous pouvez activer ou désactiver le consentement de l’utilisateur à l’aide de PowerShell, suivez les étapes décrites dans la configuration du consentement utilisateur à [l’aide de PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell).

## <a name="register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal"></a>Inscrire votre application auprès d’Plateforme d'identités Microsoft à l’aide du portail Azure AD client

Le portail Azure AD fournit une plateforme centrale pour l’inscription et la configuration de vos applications. Votre application doit être inscrite sur le portail Azure AD pour s’intégrer à la plateforme d’identité et appeler les API Microsoft Graph. Pour plus d’informations, voir [inscrire une application avec la plateforme d’identité](/graph/auth-register-app-v2).

> [!WARNING]
> Un ID Azure AD’application ne doit pas être partagé entre plusieurs Teams applications. Il doit y avoir un mappage 1:1 entre une application Teams et une application Azure AD’application. Les tentatives d’installation Teams applications associées au même ID Azure AD’application entraînent des échecs d’installation ou d’utilisation.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Passer en revue les autorisations de votre application dans le portail Azure AD web

1. Go to the **HomeApp** >  **registrations** page and select your RSC app.
1. Choisissez **les autorisations d’API** dans le volet gauche et recherchez la liste **des autorisations configurées** pour votre application. Si votre application effectue uniquement des appels Graph API RSC, supprimez toutes les autorisations sur cette page. Si votre application effectue également des appels non RSC, conservez ces autorisations selon les besoins.

> [!IMPORTANT]
> Le portail Azure AD ne peut pas être utilisé pour demander des autorisations RSC. Les autorisations RSC sont actuellement exclusives aux applications Teams installées dans le client Teams et sont déclarées dans le fichier de manifeste d’application Teams (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtenir un jeton d’accès auprès du Plateforme d'identités Microsoft

Pour effectuer des Graph API, vous devez obtenir un jeton d’accès pour votre application à partir de la plateforme d’identité. Pour que votre application puisse obtenir un jeton à partir de la plateforme d’identité, elle doit être inscrite dans le Azure AD web. Le jeton d’accès contient des informations sur votre application et les autorisations dont elle dispose pour les ressources et les API disponibles via Microsoft Graph.

Vous devez avoir les valeurs suivantes du processus d Azure AD’inscription pour récupérer un jeton d’accès à partir de la plateforme d’identité :

- **ID d’application attribué** par le portail d’inscription de l’application. Si votre application prend en charge l’sign-on unique (SSO), vous devez utiliser le même ID d’application pour votre application et l’cesso.
- La **clé secrète/mot de passe** client ou une paire de clés publiques ou **privées certificat**. N’est pas nécessaire pour les applications natives.
- **URI de redirection** ou URL de réponse pour que votre application reçoie des réponses de Azure AD.

Pour plus d’informations, voir [obtenir l’accès au nom](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) d’un utilisateur et [obtenir l’accès sans utilisateur](/graph/auth-v2-service).

## <a name="update-your-teams-app-manifest"></a>Mettre à jour le manifeste Teams’application

Les autorisations RSC sont déclarées dans le fichier JSON de manifeste de votre application. 

> [!IMPORTANT]
> Les autorisations autres que RSC sont stockées dans le portail Microsoft Azure web. Ne les ajoutez pas au manifeste de l’application.

### <a name="manifest-changes-for-resource-specific-consent"></a>Modifications de manifeste pour le consentement spécifique aux ressources

<br>

<details>

<summary><b>Autorisations RSC pour la version 1.12 du manifeste d’application</b></summary>

Ajoutez [une clé webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

|Nom| Type | Description|
|---|---|---|
|`id` |String |Votre ID Azure AD’application. Pour plus d’informations, voir [inscrire votre application sur le Azure AD web](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|String| Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne le fera.|

Spécifiez les autorisations requises par l’application.

|Nom| Type | Description|
|---|---|---|
|`authorization`|Objet|Liste des autorisations dont l’application a besoin pour fonctionner. Pour plus d’informations, voir [espace réservé pour l’autorisation de lien dans le manifeste]

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
    
<br>

</details>

<br>

<details>

<summary><b>Autorisations RSC pour la version 1.11 ou antérieure du manifeste d’application</b></summary>

Ajoutez [une clé webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

|Nom| Type | Description|
|---|---|---|
|`id` |String |Votre ID Azure AD’application. Pour plus d’informations, voir [inscrire votre application sur le Azure AD web](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal).|
|`resource`|String| Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne le fera.|
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

> [!NOTE]
> Si l’application est destinée à prendre en charge l’installation dans les étendues d’équipe et de conversation, les autorisations d’équipe et de conversation peuvent être spécifiées dans le même manifeste `applicationPermissions`sous .
    
<br>

</details>

## <a name="sideload-your-app-in-teams"></a>Charger une version test de votre application dans Teams

Si votre administrateur Teams autorise les téléchargements d’applications personnalisées, vous pouvez [](~/concepts/deploy-and-publish/apps-upload.md) charger une version de votre application directement vers une équipe ou une conversation spécifique.

## <a name="check-your-app-for-added-rsc-permissions"></a>Vérifier l’ajout d’autorisations RSC dans votre application

> [!IMPORTANT]
> Les autorisations RSC ne sont pas attribuées à un utilisateur. Les appels sont effectués avec des autorisations d’application, et non avec des autorisations déléguées par l’utilisateur. L’application peut être autorisée à effectuer des actions non autorisées par l’utilisateur, telles que la suppression d’un onglet. Vous devez passer en revue l’intention du propriétaire de l’équipe ou du propriétaire de la conversation pour votre utilisation avant d’effectuer des appels d’API RSC. Pour plus d’informations, [voir Microsoft Teams’API.](/graph/teams-concept-overview)

Une fois l’application installée sur une ressource, vous pouvez utiliser [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) pour afficher les autorisations qui ont été accordées à l’application dans la ressource.

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>Vérifier si votre application a ajouté des autorisations RSC dans une équipe

1. Obtenez le **groupId de l’équipe** à partir Teams.
1. Dans Teams, **sélectionnez Teams** dans le volet le plus à gauche.
1. Sélectionnez l’équipe dans laquelle l’application doit être installée.
1. Sélectionnez les &#x25CF;&#x25CF;&#x25CF; pour cette équipe.
1. **Sélectionnez Obtenir un lien vers l’équipe** dans le menu déroulant d’équipe.
1. Copiez et enregistrez la **valeur groupId** à partir de la boîte de dialogue Obtenir un lien **vers la** boîte de dialogue de l’équipe.
1. Connectez-vous **à Graph Explorer**.
1. Faites un **appel GET** à ce point de terminaison : `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`. Le `clientAppId` champ de la réponse sera map mapé à l’Teams `webApplicationInfo.id` manifeste de l’application.

    ![Graph’explorateur à l’appel GET pour les autorisations RSC de l’équipe](../../assets/images/team-graph-permissions.png)

Pour plus d’informations sur la façon d’obtenir des détails sur les applications installées dans une équipe spécifique, voir obtenir les noms et autres [détails des applications installées dans l’équipe spécifiée](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>Vérifier si votre application a ajouté des autorisations RSC dans une conversation

1. Obtenez l’ID de thread de conversation à partir Teams *client web*.
1. Dans le Teams web, sélectionnez **Conversation** dans le volet le plus à gauche.
1. Sélectionnez la conversation dans laquelle l’application est installée dans le menu déroulant.
1. Copiez l’URL web et enregistrez l’ID de thread de conversation à partir de la chaîne.

    ![ID de thread de conversation à partir de l’URL web](../../assets/images/chat-thread-id.png)

1. Connectez-vous **à Graph Explorer**.
1. Faites un **appel GET** au point de terminaison suivant : `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`. Le `clientAppId` champ de la réponse sera map mapé à l’Teams `webApplicationInfo.id` manifeste de l’application.

    ![Graph’explorateur pour obtenir des autorisations RSC de conversation pour l’appel GET](../../assets/images/chat-graph-permissions.png)

Pour plus d’informations sur la façon d’obtenir des détails sur les applications installées dans une conversation spécifique, voir obtenir les noms et autres [détails des applications installées](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat) dans la conversation spécifiée.

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Resource-Specific consent (RSC) | Utilisez RSC pour appeler Graph API. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>Voir aussi
 
* [Tester les autorisations de consentement propres aux ressources dans Teams](test-resource-specific-consent.md)
* [Consentement spécifique aux ressources dans Microsoft Teams pour les administrateurs](/MicrosoftTeams/resource-specific-consent)
