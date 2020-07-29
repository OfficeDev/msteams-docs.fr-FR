---
title: Consentement propre à la ressource dans teams
description: Décrit le consentement propre à la ressource dans teams et la façon de l’utiliser.
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Graphique RSC AAD d’authentification unique de teams
ms.openlocfilehash: bf449b338e8c0f42dfef776e533fb6b5ff591529
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434502"
---
# <a name="resource-specific-consent-rsc--developer-preview"></a>Consentement propre à la ressource (RSC) — Aperçu pour les développeurs

>[!NOTE]

>Les autorisations de consentement propres aux ressources sont disponibles dans les clients de bureau et Web après l’activation de l’Aperçu pour les développeurs. Pour plus d’informations, voir [Comment activer l’aperçu](../../resources/dev-preview/developer-preview-intro.md) pour les développeurs.

Le consentement propre à la ressource (RSC) est une intégration de Microsoft teams et Graph API qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des équipes spécifiques au sein d’une organisation. Le modèle d’autorisations RSC (Resource Specification) permet aux *propriétaires d’équipe* d’accorder le consentement d’une application pour accéder à des données d’une équipe et/ou les modifier. Les autorisations de RSC granulaire spécifiques aux équipes définissent ce qu’une application peut faire dans une équipe spécifique :

## <a name="resource-specific-permissions"></a>Autorisations propres aux ressources

|Autorisation de l’application| Action |
| ----- | ----- |
|TeamSettings.Read.Group | Obtenir les paramètres de cette équipe.|
|TeamSettings. Edit. Group|Mettre à jour les paramètres de cette équipe.|
|ChannelSettings.Read.Group|Obtenir les noms de canal, les descriptions de canal et les paramètres de canal de cette équipe.|
|ChannelSettings.Edit.Group|Mettre à jour les noms de canaux, les descriptions de canal et les paramètres de canal de cette équipe.|
|Channel.Create.Group|Créer des canaux au sein de cette équipe.|
|Channel.Delete.Group|Supprimer des canaux dans cette équipe.|
|ChannelMessage.Read.Group |Obtenir les messages du canal de cette équipe.|
|TeamsApp.Read.Group|Obtenir la liste des applications installées de cette équipe.|
|TeamsTab.Read.Group|Obtenir la liste des onglets de cette équipe.|
|TeamsTab.Create.Group|Créer des onglets au sein cette équipe.|
|TeamsTab.Edit.Group|Mettre à jour les onglets de cette équipe.|
|TeamsTab.Delete.Group|Supprimer les onglets de cette équipe.|
|Member.Read.Group|Obtenir les membres de cette équipe.|
|Owner.Read.Group|Obtenir les propriétaires de cette équipe.|

>[!NOTE]
>Les autorisations propres aux ressources ne sont disponibles que pour les applications teams installées sur le client teams et qui ne font actuellement pas partie du portail Azure Active Directory.

## <a name="enable-resource-specific-consent-in-your-application"></a>Activer le consentement propre à la ressource dans votre application

Les étapes à suivre pour activer RSC dans votre application sont les suivantes :

1. [Configurez les paramètres de consentement du propriétaire du groupe dans le portail Azure Active Directory](#configure-group-owner-consent-settings-in-the-azure-ad-portal).
1. [Enregistrez votre application avec Microsoft Identity Platform via le portail Azure ad](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
1. [Vérifier les autorisations de votre application dans le portail Azure AD](#review-your-application-permissions-in-the-azure-ad-portal)
1. [Obtenir un jeton d’accès à partir de la plateforme d’identité Microsoft](#obtain-an-access-token-from-the-microsoft-identity-platform).
1. [Mettez à jour le manifeste d’application de teams](#update-your-teams-app-manifest).
1. [Installez votre application directement dans teams](#install-your-app-directly-in-teams).
1. [Vérifiez que votre application dispose des autorisations RSC ajoutées](#check-your-app-for-added-rsc-permissions).

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>Configurer les paramètres de consentement du propriétaire du groupe dans le portail Azure AD

Vous pouvez activer ou désactiver le [consentement du propriétaire de groupe](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directement dans le portail Azure :

> [!div class="checklist"]
>
>- Connectez-vous au [portail Azure](https://portal.azure.com) en tant qu’administrateur général [/administrateur de société](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).  
 > - Sélectionnez **Azure Active Directory**  => **Enterprise applications**  => **paramètres utilisateur**des applications d’entreprise Azure Active Directory.
> - Activer, désactiver ou limiter le consentement de l’utilisateur avec le contrôle étiqueté **les utilisateurs peuvent consentir aux applications d’accéder aux données de l’entreprise pour les groupes qu’ils possèdent** (cette fonctionnalité est activée par défaut).

![configuration de RSC Azure](../../assets/images/azure-rsc-configuration.svg)

| Valeur | Description|
|--- | --- |
|Oui | Activer le consentement propre au groupe pour tous les propriétaires de groupe.|
|Non |Désactivez le consentement propre au groupe pour tous les utilisateurs.| 
|Peu | Activer le consentement propre au groupe pour les membres d’un groupe sélectionné.|

Pour activer ou désactiver le consentement du propriétaire d’un groupe dans le portail Azure à l’aide de PowerShell, suivez les étapes décrites dans [configurer le consentement du propriétaire du groupe à l’aide de PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>Enregistrer votre application avec Microsoft Identity Platform via le portail Azure AD

Le portail Azure Active Directory fournit une plateforme centrale pour vous inscrire et configurer vos applications. Votre application doit être enregistrée dans le portail Azure AD pour être intégrée à la plateforme d’identité Microsoft et aux API Graph de l’appel. *Consultez la rubrique* [enregistrer une application avec la plateforme d’identité Microsoft](/graph/auth-register-app-v2).

>[!WARNING]
>N’enregistrez pas plusieurs applications teams sur le même ID d’application Azure AD. L’ID de l’application doit être unique pour chaque application. Les tentatives d’installation de plusieurs applications sur le même ID d’application échouent.

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>Vérifier les autorisations de votre application dans le portail Azure AD

Accédez à la **Home**  =>  page**inscriptions des applications** personnelles et sélectionnez votre application RSC. Sélectionnez **autorisations d’API** dans la barre de navigation de gauche et examinez la liste des autorisations configurées pour votre application. Si votre application effectue uniquement des appels de graphique RSC, supprimez toutes les autorisations sur cette page. Si votre application effectue également des appels non RSC, conservez ces autorisations autant que nécessaire.

>[!IMPORTANT]
>Le portail Azure AD ne peut pas être utilisé pour demander des autorisations RSC. Les autorisations RSC sont actuellement exclusives aux applications teams installées dans le client teams et déclarées dans le fichier de manifeste de l’application (JSON).

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>Obtenir un jeton d’accès à partir de la plateforme d’identité Microsoft

Pour effectuer des appels d’API Graph, vous devez obtenir un jeton d’accès pour votre application à partir de la plateforme d’identité. Pour que votre application puisse obtenir un jeton à partir de la plateforme d’identité Microsoft, elle doit être enregistrée dans le portail Azure AD. Le jeton d’accès contient des informations sur votre application et les autorisations dont elle dispose pour les ressources et les API disponibles via Microsoft Graph.

Vous devez avoir les valeurs suivantes du processus d’inscription Azure AD pour récupérer un jeton d’accès à partir de la plateforme d’identité :

- ID de l' **application** affecté par le portail d’inscription des applications. Si votre application prend en charge l’authentification unique (SSO), vous devez utiliser le même ID d’application pour votre application et votre authentification unique.
- La clé secrète ou le **mot de passe du client** ou une paire de clés publique/privée (**certificat**). N’est pas nécessaire pour les applications natives.
- Un **URI de redirection** (ou URL de réponse) pour que votre application reçoive des réponses d’Azure ad.

 *Voir* [obtenir l’accès de la part d’un utilisateur](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) et [obtenir l’accès sans utilisateur](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>Mettre à jour le manifeste d’application de teams

Les autorisations RSC sont déclarées dans votre fichier de manifeste d’application (JSON).  Ajoutez une clé [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) à votre manifeste d’application avec les valeurs suivantes :

> [!div class="checklist"]
>
> - **ID** : votre ID d’application Azure ad. *Voir* [enregistrer votre application dans le portail Azure ad](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **ressource** : n’importe quelle chaîne. Ce champ n’a aucune opération dans RSC, mais doit être ajouté et avoir une valeur pour éviter une réponse d’erreur ; n’importe quelle chaîne fera.
> - **autorisations d’application** — autorisations RSC pour votre application. *Voir* [autorisations propres aux ressources](resource-specific-consent.md#resource-specific-permissions).

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
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="install-your-app-directly-in-teams"></a>Installer votre application directement dans teams

Une fois que vous avez créé votre application, vous pouvez [charger votre package d’application](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directement dans une équipe spécifique.  Pour ce faire, le paramètre de stratégie **charger des applications personnalisées** doit être activé dans le cadre des stratégies de configuration d’application personnalisées. *Voir* [paramètres de stratégie d’application personnalisée](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).

## <a name="check-your-app-for-added-rsc-permissions"></a>Vérifiez si votre application dispose d’autorisations RSC ajoutées

>[!IMPORTANT]
>Les autorisations RSC ne sont pas attribuées à un utilisateur. Les appels sont effectués avec des autorisations d’application, et non avec des autorisations déléguées par l’utilisateur. Par conséquent, l’application peut être autorisée à effectuer des actions que l’utilisateur ne peut pas, comme la création d’un canal ou la suppression d’un onglet. Vous devez examiner l’intention du propriétaire de l’équipe pour votre cas d’utilisation avant d’effectuer des appels d’API RSC. *Consultez la rubrique* [vue d’ensemble de l’API Microsoft teams](/graph/teams-concept-overview).

Une fois que l’application a été installée dans une équipe, vous pouvez utiliser l’afficheur [Graph](https://developer.microsoft.com/graph/graph-explorer) pour afficher les autorisations qui ont été accordées à l’application dans une équipe :

> [!div class="checklist"]
>
>- Obtenir le **GroupID** de l’équipe à partir du client Teams.
> - Dans le client Teams, sélectionnez **teams** dans la barre de navigation la plus à gauche.
> - Dans le menu déroulant, sélectionnez l’équipe où l’application est installée.
> - Sélectionnez l’icône **autres options** (&#8943;).
> - Sélectionnez **obtenir un lien vers une équipe**.
> - Copiez et enregistrez la valeur **GroupID** à partir de la chaîne.
> - Connectez-vous à l’afficheur **Graph**.
> - Effectuer un appel **Get** vers le point de terminaison suivant : `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` . Le champ clientAppId dans la réponse est mappé sur l’appId spécifié dans le manifeste de l’application Teams.

 ![Réponse de l’Explorateur Graph pour obtenir un appel.](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a>Tester le consentement propre à la ressource
 
> [!div class="nextstepaction"]
> [**Tester les autorisations de consentement propres aux ressources dans teams**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Rubrique connexe pour les administrateurs teams

> [!div class="nextstepaction"]
> [**Consentement propre à la ressource dans Microsoft teams pour les administrateurs**](/MicrosoftTeams/resource-specific-consent)
> 
