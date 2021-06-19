---
title: Consentement spécifique aux ressources dans Teams
description: Décrit le consentement spécifique aux ressources Teams et comment en tirer parti.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: autorisation OAuth OAuth SSO AAD rsc Graph
ms.openlocfilehash: 31e3dd0c33e548acd35d86492718875d45931d0b
ms.sourcegitcommit: 60a8d314e4fb48f6789d79dbc2f69321aaff99d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2021
ms.locfileid: "53022977"
---
# <a name="resource-specific-consent-rsc"></a>Consentement spécifique aux ressources (RSC)

> [!NOTE]
> Le consentement spécifique aux ressources pour l’étendue de conversation est disponible en [prévisualisation publique pour les](../../resources/dev-preview/developer-preview-intro.md) développeurs uniquement.

Le consentement spécifique aux ressources (RSC) est une intégration d’API Microsoft Teams et Microsoft Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des ressources spécifiques (équipes ou conversations) au sein d’une organisation. Le modèle d’autorisations de consentement spécifique  aux ressources (RSC) permet aux propriétaires d’équipe et de *conversation* d’accorder le consentement d’une application pour accéder aux données d’une équipe et aux données d’une conversation, et/ou de les modifier, respectivement. Les autorisations RSC précises définissent ce qu’une application peut faire au sein d’une ressource spécifique :

## <a name="resource-specific-permissions"></a>Autorisations spécifiques aux ressources

### <a name="resource-specific-permissions-for-a-team"></a>Autorisations spécifiques aux ressources pour une équipe
|Autorisation de l’application| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtenez les paramètres de cette équipe.|
|TeamSettings.ReadWrite.Group|Mettez à jour les paramètres de cette équipe.|
|ChannelSettings.Read.Group|Obtenez les noms de canaux, les descriptions des canaux et les paramètres de canal de cette équipe.|
|ChannelSettings.ReadWrite.Group|Mettez à jour les noms de canaux, les descriptions des canaux et les paramètres de canal de cette équipe.|
|Channel.Create.Group|Créer des canaux au sein de cette équipe. |
|Channel.Delete.Group|Supprimez les canaux de cette équipe. |
|ChannelMessage.Read.Group |Obtenez les messages de canal de cette équipe. |
|TeamsAppInstallation.Read.Group|Obtenez la liste des applications installées de cette équipe.|
|TeamsTab.Read.Group|Obtenez la liste des onglets de cette équipe.|
|TeamsTab.Create.Group|Créer des onglets au sein cette équipe. |
|TeamsTab.ReadWrite.Group|Mettez à jour les onglets de cette équipe. |
|TeamsTab.Delete.Group|Supprimer les onglets de cette équipe. |
|TeamMember.Read.Group|Obtenez les membres de cette équipe. |

Pour plus d’informations, voir autorisations de consentement propres aux ressources [d’équipe.](/graph/permissions-reference#team-resource-specific-consent-permissions)

### <a name="resource-specific-permissions-for-a-chat"></a>Autorisations spécifiques aux ressources pour une conversation
|Autorisation de l’application| Action |
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
| OnlineMeeting.ReadBasic.Chat   | Obtenez les propriétés de base (par exemple, nom, planification, organisateur et lien de connexion) d’une réunion associée à cette conversation. |

Pour plus d’informations, voir Autorisations de consentement propres aux ressources [de conversation.](/graph/permissions-reference#chat-resource-specific-consent-permissions)

>[!NOTE]
>Les autorisations propres aux ressources sont disponibles uniquement pour Teams applications installées sur le client Teams et ne font actuellement pas partie du portail Azure Active Directory.

## <a name="enable-resource-specific-consent-in-your-application"></a>Activer le consentement spécifique aux ressources dans votre application

Les étapes permettant d’activer RSC dans votre application sont les suivantes :

1. [Configurez les paramètres de consentement dans le portail Azure Active Directory.](#configure-consent-settings-in-the-azure-ad-portal)
    1. Configurez les paramètres de consentement du propriétaire [du groupe pour RSC dans une équipe.](#configure-group-owner-consent-settings-for-rsc-in-a-team)
    1. [Configurez les paramètres de consentement de l’utilisateur pour RSC dans une conversation.](#configure-user-consent-settings-for-rsc-in-a-chat)
1. [Inscrivez votre application auprès Plateforme d’identités Microsoft via le portail Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
1. [Examinez vos autorisations d’application dans le portail Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Obtenir un jeton d’accès à partir de la plateforme Microsoft Identity](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Mettez à jour Teams manifeste de votre application.](#update-your-teams-app-manifest)
1. [Installez votre application directement dans Teams](#sideload-your-app-in-teams).
1. [Vérifiez que votre application a ajouté des autorisations RSC.](#check-your-app-for-added-rsc-permissions)
    1. [Vérifiez que votre application a ajouté des autorisations RSC dans une équipe.](#check-your-app-for-added-rsc-permissions-in-a-team)
    1. [Vérifiez que votre application a ajouté des autorisations RSC dans une conversation.](#check-your-app-for-added-rsc-permissions-in-a-chat)

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a>Configurer les paramètres de consentement dans le portail Azure AD

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>Configurer les paramètres de consentement du propriétaire du groupe pour RSC dans une équipe

Vous pouvez activer ou désactiver [le](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) consentement du propriétaire du groupe directement dans le portail Azure :

> [!div class="checklist"]
>
>- Connectez-vous au [portail Azure](https://portal.azure.com) en tant [qu’administrateur général/administrateur d’entreprise.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)  
 > - [Sélectionnez](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** Enterprise applications de consentement  =>  **et**  =>  **d’autorisations Paramètres** de consentement  =>  **utilisateur.**
> - Activer, désactiver ou limiter le consentement de l’utilisateur avec le consentement du propriétaire du groupe étiqueté pour les applications accédant aux données **(la** valeur par défaut est Autoriser le consentement du propriétaire du groupe pour tous les propriétaires **du groupe).** Pour qu’un propriétaire d’équipe installe une application à l’aide de RSC, le consentement du propriétaire du groupe doit être activé pour cet utilisateur.

![Configuration de l’équipe azure rsc](../../assets/images/azure-rsc-team-configuration.png)

Pour activer ou désactiver le consentement du propriétaire du groupe à l’aide de PowerShell, suivez les étapes décrites dans configurer le consentement du propriétaire du groupe à [l’aide de PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>Configurer les paramètres de consentement de l’utilisateur pour RSC dans une conversation

Vous pouvez activer ou désactiver le consentement de [l’utilisateur](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directement dans le portail Azure :

> [!div class="checklist"]
>
>- Connectez-vous au [portail Azure](https://portal.azure.com) en tant [qu’administrateur général/administrateur d’entreprise.](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)  
 > - [Sélectionnez](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** Enterprise applications de consentement  =>  **et**  =>  **d’autorisations Paramètres** de consentement  =>  **utilisateur.**
> - Activer, désactiver ou limiter le consentement de l’utilisateur avec le contrôle étiqueté Consentement de l’utilisateur pour **les applications** (la valeur par défaut est Autoriser le consentement de **l’utilisateur pour les applications).** Pour qu’un membre de conversation installe une application à l’aide de RSC, le consentement de l’utilisateur doit être activé pour cet utilisateur.

![Configuration de conversation rsc Azure](../../assets/images/azure-rsc-chat-configuration.png)

Pour activer ou désactiver le consentement de l’utilisateur à l’aide de PowerShell, suivez les étapes décrites dans Configurer le consentement de l’utilisateur [à l’aide de PowerShell.](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)


## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Inscrire votre application auprès de Plateforme d’identités Microsoft via le portail Azure AD

Le Azure Active Directory web fournit une plateforme centrale pour l’inscription et la configuration de vos applications. Votre application doit être inscrite dans le portail Azure AD pour s’intégrer au Plateforme d’identités Microsoft et appeler les API Microsoft Graph. Pour plus d’informations, voir [Inscrire une application avec le Plateforme d’identités Microsoft](/graph/auth-register-app-v2).

>[!WARNING]
>Un ID d’application Azure AD ne doit pas être partagé entre plusieurs Teams applications. Il doit y avoir un mappage 1:1 entre une application Teams et une application Azure AD. Les tentatives d’installation Teams applications associées au même ID d’application Azure AD entraînent des échecs d’installation/d’utilisation.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Passer en revue vos autorisations d’application dans le portail Azure AD

Accédez à la page **d’inscription**  =>  **de l’application d’accueil** et sélectionnez votre application RSC. Choisissez **les autorisations d’API** dans la barre de navigation de gauche et examinez la liste des autorisations configurées pour votre application. Si votre application effectuera uniquement des appels RSC Graph API, supprimez toutes les autorisations sur cette page. Si votre application doit également effectuer des appels non RSC, conservez ces autorisations selon vos besoins.

>[!IMPORTANT]
>Le portail Azure AD ne peut pas être utilisé pour demander des autorisations RSC. Les autorisations RSC sont actuellement exclusives aux applications Teams installées dans le client Teams et sont déclarées dans le fichier de manifeste d’application Teams (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtenir un jeton d’accès auprès du Plateforme d’identités Microsoft

Pour effectuer des Graph API, vous devez obtenir un jeton d’accès pour votre application à partir de la plateforme d’identité. Pour que votre application puisse obtenir un jeton de la Plateforme d’identités Microsoft, elle doit être inscrite dans le portail Azure AD. Le jeton d’accès contient des informations sur votre application et les autorisations dont elle dispose pour les ressources et les API disponibles via Microsoft Graph.

Vous devez avoir les valeurs suivantes du processus d’inscription Azure AD pour récupérer un jeton d’accès à partir de la plateforme d’identité :

- ID **d’application attribué** par le portail d’inscription de l’application. Si votre application prend en charge l' sign-on unique (SSO), vous devez utiliser le même ID d’application pour votre application et l' sso.
- Clé **secrète client/mot de passe** ou paire clé publique/clé privée **(certificat).** N’est pas nécessaire pour les applications natives.
- URI **de redirection** (ou URL de réponse) pour que votre application reçoie des réponses d’Azure AD.

 *Voir* [Obtenir l’accès au nom d’un utilisateur](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) et Obtenir [l’accès sans utilisateur](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Mettre à jour votre manifeste Teams application

Les autorisations RSC sont déclarées dans votre fichier de manifeste d’application (JSON).  Ajoutez [une clé webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

> [!div class="checklist"]
>
> - **id**  : votre ID d’application Azure AD. Pour plus d’informations, voir [Inscrire votre application dans le portail Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
> - **ressource**  — toute chaîne. Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne le fera.
> - **autorisations d’application** : autorisations RSC pour votre application. Pour plus d’informations, [voir Autorisations spécifiques aux ressources.](resource-specific-consent.md#resource-specific-permissions)

>
>[!IMPORTANT]
> Les autorisations non RSC sont stockées dans le portail Azure. Ne les ajoutez pas au manifeste de l’application.
>

### <a name="example-for-rsc-in-a-team"></a>Exemple pour RSC dans une équipe
```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.ReadWrite.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.ReadWrite.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

### <a name="example-for-rsc-in-a-chat"></a>Exemple de RSC dans une conversation
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
      "OnlineMeeting.ReadBasic.Chat"
    ]
  }
```

>[!NOTE]
>Si l’application est destinée à prendre en charge l’installation dans les étendues d’équipe et de conversation, les autorisations d’équipe et de conversation peuvent être spécifiées dans le même manifeste sous `applicationPermissions` .

## <a name="sideload-your-app-in-teams"></a>Chargez une version de version de votre application dans Teams

Si votre administrateur Teams autorise les téléchargements d’applications personnalisées, vous pouvez charger une version de votre application directement vers une équipe ou une conversation spécifique. [](~/concepts/deploy-and-publish/apps-upload.md)

## <a name="check-your-app-for-added-rsc-permissions"></a>Vérifier l’ajout d’autorisations RSC dans votre application

>[!IMPORTANT]
>Les autorisations RSC ne sont pas attribuées à un utilisateur. Les appels sont effectués avec des autorisations d’application, et non avec des autorisations déléguées par l’utilisateur. Par conséquent, l’application peut être autorisée à effectuer des actions que l’utilisateur ne peut pas effectuer, telles que la suppression d’un onglet. Vous devez examiner l’intention du propriétaire de l’équipe ou du propriétaire de la conversation pour votre cas d’utilisation avant d’effectuer des appels d’API RSC. Pour plus d’informations, [voir Microsoft Teams’API.](/graph/teams-concept-overview)

Une fois l’application installée sur une ressource, vous pouvez utiliser [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) pour afficher les autorisations qui ont été accordées à l’application dans la ressource :

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>Vérifier si votre application a ajouté des autorisations RSC dans une équipe

> [!div class="checklist"]
>
>- Obtenez le **groupId** de l’équipe à partir Teams client.
> - Dans le Teams client, sélectionnez **Teams** la barre de navigation à l’extrême gauche.
> - Sélectionnez l’équipe sur laquelle l’application est installée dans le menu déroulant.
> - Sélectionnez **l’icône Options** supplémentaires (&#8943;).
> - Sélectionnez **Obtenir un lien vers l’équipe.**
> - Copiez et enregistrez la **valeur groupId** à partir de la chaîne.
> - Connectez-vous **Graph Explorer.**
> - Faites un **appel GET** au point de terminaison suivant : `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` . Le `clientAppId` champ de la réponse sera map mapé à l’Teams manifeste de `webApplicationInfo.id` l’application.
  ![Graph’explorateur à l’appel GET pour les autorisations RSC de l’équipe.](../../assets/images/team-graph-permissions.png)

Pour plus d’informations sur la façon d’obtenir des détails sur les applications installées dans une équipe spécifique, voir Obtenir les noms et autres détails des applications installées dans [l’équipe spécifiée.](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>Vérifier si votre application a ajouté des autorisations RSC dans une conversation

> [!div class="checklist"]
>
>- Obtenez l’ID de thread de conversation à partir Teams *client web.*
> - Dans le Teams web, sélectionnez **Conversation** dans la barre de navigation de l’extrême gauche.
> - Sélectionnez la conversation dans laquelle l’application est installée dans le menu déroulant.
> - Copiez l’URL web et enregistrez l’ID de thread de conversation à partir de la chaîne.
![ID de thread de conversation à partir de l’URL web.](../../assets/images/chat-thread-id.png)
> - Connectez-vous **Graph Explorer.**
> - Faites un **appel GET** au point de terminaison suivant : `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` . Le `clientAppId` champ de la réponse sera map mapé à l’Teams manifeste de `webApplicationInfo.id` l’application.
  ![Graph de l’explorateur pour obtenir des autorisations RSC d’appel get.](../../assets/images/chat-graph-permissions.png)

Pour plus d’informations sur la façon d’obtenir des détails sur les applications installées dans une conversation spécifique, voir Obtenir les noms et autres détails des applications installées dans la conversation [spécifiée.](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)

## <a name="code-sample"></a>Exemple de code
| **Exemple de nom** | **Description** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Consentement spécifique à une ressource (RSC) | Utilisez RSC pour appeler Graph API. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a>Voir aussi
 
* [Tester les autorisations de consentement propres aux ressources dans Teams](test-resource-specific-consent.md)
* [Consentement spécifique aux ressources dans Microsoft Teams pour les administrateurs](/MicrosoftTeams/resource-specific-consent)


