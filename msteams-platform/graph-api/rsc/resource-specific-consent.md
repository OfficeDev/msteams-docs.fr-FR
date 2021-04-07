---
title: Consentement spécifique aux ressources dans Teams
description: Décrit le consentement spécifique aux ressources dans Teams et comment en tirer parti.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: Teams Authorization OAuth SSO AAD rsc Graph
ms.openlocfilehash: cf57637dac91fae14473a831e76f868f458d8f27
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596216"
---
# <a name="resource-specific-consent-rsc"></a>Consentement spécifique aux ressources (RSC)

Le consentement spécifique aux ressources (RSC) est une intégration de l’API Microsoft Teams et Microsoft Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des équipes spécifiques au sein d’une organisation. Le modèle d’autorisations de consentement spécifique  aux ressources permet aux propriétaires d’équipes d’accorder l’autorisation à une application d’accéder aux données d’une équipe et/ou de les modifier. Les autorisations RSC précises et spécifiques à Teams définissent ce qu’une application peut faire au sein d’une équipe spécifique :

## <a name="resource-specific-permissions"></a>Autorisations spécifiques aux ressources

|Autorisation de l’application| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtenez les paramètres de cette équipe.|
|TeamSettings.ReadWrite.Group|Mettez à jour les paramètres de cette équipe.|
|ChannelSettings.Read.Group|Obtenez les noms des canaux, les descriptions des canaux et les paramètres de canal pour cette équipe.|
|ChannelSettings.ReadWrite.Group|Mettez à jour les noms des canaux, les descriptions des canaux et les paramètres de canal pour cette équipe.|
|Channel.Create.Group|Créer des canaux au sein de cette équipe.|
|Channel.Delete.Group|Supprimez les canaux de cette équipe.|
|ChannelMessage.Read.Group |Obtenez les messages de canal de cette équipe.|
|TeamsAppInstallation.Read.Group|Obtenez la liste des applications installées de cette équipe.|
|TeamsTab.Read.Group|Obtenir la liste des onglets de cette équipe.|
|TeamsTab.Create.Group|Créer des onglets au sein cette équipe.|
|TeamsTab.ReadWrite.Group|Mettez à jour les onglets de cette équipe.|
|TeamsTab.Delete.Group|Supprimer les onglets de cette équipe.|
|TeamMember.Read.Group|Obtenez les membres de cette équipe.|

>[!NOTE]
>Les autorisations spécifiques aux ressources sont disponibles uniquement pour les applications Teams installées sur le client Teams et ne font actuellement pas partie du portail Azure Active Directory.

## <a name="enable-resource-specific-consent-in-your-application"></a>Activer le consentement spécifique aux ressources dans votre application

Les étapes permettant d’activer RSC dans votre application sont les suivantes :

1. [Configurez les paramètres de consentement](#configure-group-owner-consent-settings-in-the-azure-ad-portal)du propriétaire du groupe dans le portail Azure Active Directory.
1. [Inscrivez votre application auprès de la plateforme d’identités Microsoft via le portail Azure AD.](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
1. [Examinez vos autorisations d’application dans le portail Azure AD.](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Obtenir un jeton d’accès à partir de la plateforme Microsoft Identity](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Mettez à jour le manifeste de votre application Teams.](#update-your-teams-app-manifest)
1. [Installez votre application directement dans Teams.](#install-your-app-directly-in-teams)
1. [Vérifiez que votre application a ajouté des autorisations RSC.](#check-your-app-for-added-rsc-permissions)

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Configurer les paramètres de consentement du propriétaire du groupe dans le portail Azure AD

Vous pouvez activer ou désactiver [le](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) consentement du propriétaire du groupe directement dans le portail Azure :

> [!div class="checklist"]
>
>- Connectez-vous au [portail Azure](https://portal.azure.com) en tant [qu’administrateur général/administrateur d’entreprise.](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)  
 > - [Sélectionnez](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) les paramètres de consentement et d’autorisations des applications **Azure Active Directory**  =>    =>    =>  Enterprise.
> - Activer, désactiver ou limiter le consentement de l’utilisateur avec le consentement du propriétaire du groupe étiqueté pour les applications accédant aux données **(la** valeur par défaut est Autoriser le consentement du propriétaire du groupe pour tous les propriétaires **du groupe).** Pour qu’un propriétaire d’équipe installe une application à l’aide de RSC, le consentement du propriétaire du groupe doit être activé pour cet utilisateur.

![configuration azure rsc](../../assets/images/azure-rsc-configuration.png)

Pour activer ou désactiver le consentement du propriétaire du groupe à l’aide de PowerShell, suivez les étapes décrites dans configurer le consentement du propriétaire du groupe à [l’aide de PowerShell.](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Inscrire votre application sur la plateforme d’identités Microsoft via le portail Azure AD

Le portail Azure Active Directory fournit une plateforme centrale pour l’inscription et la configuration de vos applications. Votre application doit être inscrite dans le portail Azure AD pour s’intégrer à la plateforme d’identités Microsoft et appeler les API Microsoft Graph. *Voir* [Inscrire une application avec la plateforme d’identités Microsoft.](/graph/auth-register-app-v2)

>[!WARNING]
>N’inscrivez pas plusieurs applications Teams sur le même ID d’application Azure AD. L’ID d’application doit être unique pour chaque application. Les tentatives d’installation de plusieurs applications sur le même ID d’application échouent.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Passer en revue vos autorisations d’application dans le portail Azure AD

Accédez à la page  =>  **d’inscription de l’application d’accueil** et sélectionnez votre application RSC. Choisissez **les autorisations d’API** dans la barre de navigation de gauche et examinez la liste des autorisations configurées pour votre application. Si votre application effectuera uniquement des appels d’API RSC Graph, supprimez toutes les autorisations sur cette page. Si votre application doit également effectuer des appels non RSC, conservez ces autorisations selon vos besoins.

>[!IMPORTANT]
>Le portail Azure AD ne peut pas être utilisé pour demander des autorisations RSC. Les autorisations RSC sont actuellement exclusives aux applications Teams installées dans le client Teams et sont déclarées dans le fichier de manifeste d’application (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtenir un jeton d’accès à partir de la plateforme d’identités Microsoft

Pour effectuer des appels d’API Graph, vous devez obtenir un jeton d’accès pour votre application à partir de la plateforme d’identité. Pour que votre application puisse obtenir un jeton auprès de la plateforme d’identités Microsoft, elle doit être inscrite dans le portail Azure AD. Le jeton d’accès contient des informations sur votre application et les autorisations dont elle dispose pour les ressources et les API disponibles via Microsoft Graph.

Vous devez avoir les valeurs suivantes du processus d’inscription Azure AD pour récupérer un jeton d’accès à partir de la plateforme d’identité :

- ID **d’application attribué** par le portail d’inscription de l’application. Si votre application prend en charge l' sign-on unique (SSO), vous devez utiliser le même ID d’application pour votre application et l' sso.
- Clé **secrète client/mot de passe** ou paire clé publique/clé privée **(certificat).** N’est pas nécessaire pour les applications natives.
- URI **de redirection** (ou URL de réponse) pour que votre application reçoie des réponses d’Azure AD.

 *Voir* [Obtenir l’accès au nom d’un utilisateur](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) et Obtenir [l’accès sans utilisateur](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Mettre à jour le manifeste de votre application Teams

Les autorisations RSC sont déclarées dans votre fichier de manifeste d’application (JSON).  Ajoutez [une clé webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) au manifeste de votre application avec les valeurs suivantes :

> [!div class="checklist"]
>
> - **id** : votre ID d’application Azure AD. *Voir* Inscrire votre [application dans le portail Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
> - **ressource**  : toute chaîne. Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne le fera.
> - **autorisations d’application** : autorisations RSC pour votre application. *Voir* [Autorisations spécifiques aux ressources.](resource-specific-consent.md#resource-specific-permissions)

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

## <a name="install-your-app-directly-in-teams"></a>Installer votre application directement dans Teams

Une fois que vous avez créé votre application, vous pouvez charger votre [package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) d’application directement vers une équipe spécifique.  Pour ce faire, le paramètre **de** stratégie Télécharger des applications personnalisées doit être activé dans le cadre des stratégies de configuration d’application personnalisées. *Voir Paramètres* [de stratégie d’application personnalisée.](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)

## <a name="check-your-app-for-added-rsc-permissions"></a>Vérifier l’ajout d’autorisations RSC dans votre application

>[!IMPORTANT]
>Les autorisations RSC ne sont pas attribuées à un utilisateur. Les appels sont effectués avec des autorisations d’application, et non avec des autorisations déléguées par l’utilisateur. Par conséquent, l’application peut être autorisée à effectuer des actions que l’utilisateur ne peut pas effectuer, telles que la création d’un canal ou la suppression d’un onglet. Vous devez examiner l’intention du propriétaire de l’équipe pour votre cas d’utilisation avant d’effectuer des appels d’API RSC. *Voir la* [vue d’ensemble de l’API Microsoft Teams.](/graph/teams-concept-overview)

Une fois l’application installée dans une équipe, vous pouvez utiliser l’Afficheur [Graph](https://developer.microsoft.com/graph/graph-explorer)  pour afficher les autorisations qui ont été accordées à l’application dans une équipe :

> [!div class="checklist"]
>
>- Obtenez le **groupId** de l’équipe à partir du client Teams.
> - Dans le client Teams, sélectionnez **Teams** dans la barre de navigation de l’extrême gauche.
> - Sélectionnez l’équipe sur laquelle l’application est installée dans le menu déroulant.
> - Sélectionnez **l’icône Options** supplémentaires (&#8943;).
> - Sélectionnez **Obtenir un lien vers l’équipe.**
> - Copiez et enregistrez **la valeur groupId** à partir de la chaîne.
> - Connectez-vous **à l’Afficheur Graph.**
> - Faites un **appel GET** au point de terminaison suivant : `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . Le champ clientAppId de la réponse sera map mapé à l’appId spécifié dans le manifeste de l’application Teams.
  ![Réponse de l’explorateur graphe à l’appel GET.](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>Exemple de code
| **Exemple de nom** | **Description** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Consentement spécifique à une ressource (RSC) | Utilisez RSC pour appeler des API Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="test-resource-specific-consent"></a>Tester le consentement spécifique aux ressources
 
> [!div class="nextstepaction"]
> [**Tester les autorisations de consentement spécifiques aux ressources dans Teams**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Rubrique connexe pour les administrateurs Teams

> [!div class="nextstepaction"]
> [**Consentement spécifique aux ressources dans Microsoft Teams pour les administrateurs**](/MicrosoftTeams/resource-specific-consent)
> 

