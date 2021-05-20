---
title: Consentement spécifique aux ressources en Teams
description: Décrit le consentement spécifique aux ressources Teams et la façon d’en tirer parti.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: les équipes autorisation OAuth SSO AAD rsc Graph
ms.openlocfilehash: dabe0c33013fbb398eee7bf00ac2881cd86e6bc5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566127"
---
# <a name="resource-specific-consent-rsc"></a>Consentement spécifique aux ressources (SRC)

Le consentement spécifique aux ressources (RSC) est une intégration d’API Microsoft Teams et Microsoft Graph qui permet à votre application d’utiliser les paramètres de l’API pour gérer des équipes spécifiques au sein d’une organisation. Le modèle d’autorisations de consentement  spécifique aux ressources permet aux propriétaires d’équipe d’accorder le consentement d’une demande d’accès et/ou de modifier les données d’une équipe. Les autorisations granulaires, Teams spécifiques aux CRS définissent ce qu’une application peut faire au sein d’une équipe spécifique :

## <a name="resource-specific-permissions"></a>Autorisations spécifiques aux ressources

|Autorisation de l’application| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtenez les paramètres de cette équipe.|
|TeamSettings.ReadWrite.Group|Mettez à jour les paramètres de cette équipe.|
|ChannelSettings.Read.Group|Obtenez les noms de canaux, les descriptions de canaux et les paramètres de canal pour cette équipe.|
|ChannelSettings.ReadWrite.Group|Mettez à jour les noms des canaux, les descriptions des canaux et les paramètres des canaux pour cette équipe.|
|Channel.Create.Group|Créer des canaux au sein de cette équipe.|
|Channel.Delete.Group|Supprimez les canaux de cette équipe.|
|ChannelMessage.Read.Group |Obtenez les messages de canal de cette équipe.|
|TeamsAppInstallation.Read.Group|Obtenez une liste des applications installées par cette équipe.|
|TeamsTab.Read.Group|Obtenez une liste des onglets de cette équipe.|
|TeamsTab.Create.Group|Créer des onglets au sein cette équipe.|
|TeamsTab.ReadWrite.Group|Mettez à jour les onglets de cette équipe.|
|TeamsTab.Delete.Group|Supprimer les onglets de cette équipe.|
|TeamMember.Read.Group|Obtenez les membres de cette équipe.|

>[!NOTE]
>Les autorisations spécifiques aux ressources ne sont disponibles que pour Teams applications installées sur le client Teams et ne font actuellement pas partie du portail Azure Active Directory’eau.

## <a name="enable-resource-specific-consent-in-your-application"></a>Activer le consentement spécifique aux ressources dans votre demande

Les étapes d’activation de RSC dans votre application sont les suivantes :

1. [Configurez les paramètres de consentement du propriétaire du groupe dans Azure Active Directory portail .](#configure-group-owner-consent-settings-in-the-azure-ad-portal)
1. [Enregistrez votre application Plateforme d’identités Microsoft via le portail Azure AD](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
1. [Examinez les autorisations de votre application dans le portail Azure AD](#review-your-application-permissions-in-the-azure-ad-portal).
1. [Obtenez un jeton d’accès à partir de la plate-forme Microsoft Identity](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Mettez à jour Teams manifeste de l’application](#update-your-teams-app-manifest).
1. [Installez votre application directement dans Teams](#sideload-your-app-in-teams).
1. [Vérifiez votre application pour obtenir des autorisations RSC ajoutées.](#check-your-app-for-added-rsc-permissions)

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Configurer les paramètres de consentement du propriétaire du groupe dans le portail Azure AD

Vous pouvez activer ou désactiver le consentement [du propriétaire du groupe](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directement sur le portail Azure :

> [!div class="checklist"]
>
>- Connectez-vous au [portail Azure en tant](https://portal.azure.com) [qu’administrateur global/administrateur d’entreprise](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).  
 > - [Sélectionnez](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** Enterprise  =>  **applications Consent** and  =>  **permissions** Paramètres de consentement de  =>  **l’utilisateur**.
> - Activer, désactiver ou limiter le consentement de l’utilisateur avec le consentement du propriétaire **du Groupe étiqueté contrôle pour les applications accédant** aux données (La valeur par défaut est autoriser le consentement du propriétaire du groupe pour tous les propriétaires de **groupe).** Pour qu’un propriétaire d’équipe installe une application à l’aide de RSC, le consentement du propriétaire du groupe doit être activé pour cet utilisateur.

![configuration azure rsc](../../assets/images/azure-rsc-configuration.png)

Pour activer ou désactiver le consentement du propriétaire du groupe à l’aide de PowerShell, suivez les étapes décrites dans [le consentement du propriétaire du groupe Configure à l’aide de PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Enregistrez votre application Plateforme d’identités Microsoft via le portail Azure AD

Le Azure Active Directory fournit une plate-forme centrale pour vous inscrire et configurer vos applications. Votre application doit être enregistrée sur le portail Azure AD pour s’intégrer aux Plateforme d’identités Microsoft et appeler Microsoft Graph API. Pour plus d’informations, [voir Enregistrer une demande auprès de la Plateforme d’identités Microsoft](/graph/auth-register-app-v2).

>[!WARNING]
>N’enregistrez pas Teams applications dans le même identifiant d’application Azure AD. L’id de l’application doit être unique pour chaque application. Les tentatives d’installation de plusieurs applications sur le même id d’application échoueront.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Examinez vos autorisations de demande sur le portail Azure AD

Accédez **à la** page  =>  **d’inscription de l’application** Home et sélectionnez votre application RSC. Choisissez **les autorisations API** à partir de la barre de navigation gauche et examinez la liste des autorisations configurées pour votre application. Si votre application ne fait que des appels RSC Graph API, supprimez toute l’autorisation sur cette page. Si votre application passe également des appels non RSC, conservez ces autorisations au besoin.

>[!IMPORTANT]
>Le portail Azure AD ne peut pas être utilisé pour demander des autorisations RSC. Les autorisations RSC sont actuellement exclusives aux applications Teams dans le client Teams et sont déclarées dans le fichier manifeste de l’application (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtenez un jeton d’accès à partir de la Plateforme d’identités Microsoft

Pour effectuer des Graph api, vous devez obtenir un jeton d’accès pour votre application à partir de la plate-forme d’identité. Avant que votre application puisse obtenir un jeton de la Plateforme d’identités Microsoft, elle doit être enregistrée sur le portail Azure AD. Le jeton d’accès contient des informations sur votre application et les autorisations dont elle dispose pour les ressources et les API disponibles via Microsoft Graph.

Vous devrez avoir les valeurs suivantes du processus d’enregistrement Azure AD pour récupérer un jeton d’accès à partir de la plate-forme d’identité :

- **L’iD d’application** attribué par le portail d’enregistrement de l’application. Si votre application prend en charge une seule inscription (SSO), vous devez utiliser le même identifiant d’application pour votre application et SSO.
- Le  **client secret / mot de** passe ou une paire de clés public / privé (**Certificat**). N’est pas nécessaire pour les applications natives.
- Une **redirection URI** (ou URL de réponse) pour que votre application reçoive des réponses d’Azure AD.

 *Voir* [Obtenir l’accès au nom d’un](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) utilisateur [et obtenir l’accès sans utilisateur](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Mettez à jour votre Teams d’application

Les autorisations RSC sont déclarées dans votre fichier manifeste d’application (JSON).  Ajoutez une [clé webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d’application avec les valeurs suivantes :

> [!div class="checklist"]
>
> - **id**  — votre identifiant d’application Azure AD. Pour plus d’informations, [consultez Inscrivez votre application sur le portail Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **ressource**  — n’importe quelle chaîne. Ce champ n’a pas d’opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur; n’importe quelle chaîne fera l’année.
> - **autorisations d’application** — autorisations RSC pour votre application. Pour plus d’informations, [consultez Autorisations spécifiques aux ressources](resource-specific-consent.md#resource-specific-permissions).

>
>[!IMPORTANT]
> Les autorisations non RSC sont stockées dans le portail Azure. Ne les ajoutez pas au manifeste de l’application.
>

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

## <a name="sideload-your-app-in-teams"></a>Sideload votre application dans Teams

Si votre Teams permet des téléchargements d’applications personnalisés, vous [pouvez sideload votre application](~/concepts/deploy-and-publish/apps-upload.md) directement à une équipe spécifique.

## <a name="check-your-app-for-added-rsc-permissions"></a>Vérifiez l’ajout d’autorisations RSC à votre application

>[!IMPORTANT]
>Les autorisations RSC ne sont pas attribuées à un utilisateur. Les appels sont effectués avec des autorisations d’application, et non avec des autorisations déléguées par l’utilisateur. Ainsi, l’application peut être autorisée à effectuer des actions que l’utilisateur ne peut pas, telles que la création d’un canal ou la suppression d’un onglet. Vous devez examiner l’intention du propriétaire de l’équipe pour votre cas d’utilisation avant de passer des appels api RSC. Pour plus d’informations, [consultez Microsoft Teams aperçu de l’API](/graph/teams-concept-overview).

Une fois que l’application a été installée à une équipe, [vous pouvez utiliser Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) pour afficher les autorisations qui ont été accordées à l’application dans une équipe :

> [!div class="checklist"]
>
>- Obtenez le groupId de **l’équipe** de la Teams client.
> - Dans le Teams client, sélectionnez **Teams** de la barre de navigation d’extrême gauche.
> - Sélectionnez l’équipe où l’application est installée à partir du menu drop-down.
> - Sélectionnez **l’icône Plus d’options** (&#8943;).
> - Sélectionnez **Obtenir un lien vers l’équipe**.
> - Copiez et enregistrez **la valeur groupId** de la chaîne.
> - Connectez-vous **Graph Explorer**.
> - Faites un **appel GET** au point de terminaison suivant : `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . Le champ clientAppId dans la réponse sera la carte de l’appId spécifié dans le manifeste Teams’application.
  ![Graph’explorateur à l’appel GET.](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>Exemple de code
| **Nom de l’échantillon** | **Description** | **.NET (en)** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Consentement spécifique aux ressources (SRC) | Utilisez RSC pour appeler Graph API. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a>Voir aussi
 
* [Testez les autorisations de consentement propres aux ressources Teams](test-resource-specific-consent.md)
* [Consentement spécifique aux ressources en Microsoft Teams pour les administrateurs](/MicrosoftTeams/resource-specific-consent)


