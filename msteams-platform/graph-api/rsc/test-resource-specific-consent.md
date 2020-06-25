---
title: Test du consentement propre à une ressource dans teams
description: Détails de test de consentement propre à une ressource dans teams à l’aide de l’affranchissement
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: How-to
keywords: autorisation teams graphique des messages RSC
ms.openlocfilehash: c1c02c2ba0051193aa459d0df26fadfc9fa55550
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867101"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a>Tester les autorisations de consentement propres aux ressources dans teams

Le consentement propre à la ressource (RSC) est une intégration de Microsoft teams et Graph API qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des équipes spécifiques au sein d’une organisation. *Voir*[consentement propre à la ressource (RSC) — API Microsoft teams Graph](resource-specific-consent.md).  

> [!NOTE]
>Pour tester les autorisations RSC, votre fichier manifeste de l’application teams doit inclure une clé **webApplicationInfo** remplie avec les champs suivants :
>
> - **ID** : votre ID d’application Azure ad, *consultez la rubrique* [enregistrer votre application dans le portail Azure ad](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **ressource** : n’importe quelle chaîne, *consultez* la remarque dans [mettre à jour votre manifeste d’application teams](resource-specific-consent.md#update-your-teams-app-manifest)
> - **autorisations des applications** — autorisations RSC pour votre application, *voir* [autorisations spécifiques aux ressources](resource-specific-consent.md#resource-specific-permissions).

```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
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

>[!IMPORTANT]
>Dans le manifeste de votre application, incluez uniquement les autorisations RSC dont vous souhaitez que votre application ait besoin.

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>Tester les autorisations RSC ajoutées à l’aide de l’application postale

Pour vérifier si les autorisations RSC sont honorées par la charge utile de la demande d’API, vous devez copier le [Code de test JSON RSC](test-rsc-json-file.md) dans votre environnement local et mettre à jour les valeurs suivantes :

1. `azureADAppId`: ID de l’application Azure AD de votre application.
1. `azureADAppSecret`— votre code secret d’application Azure AD (mot de passe)
1. `teamGroupId`— vous pouvez obtenir l’ID de groupe d’équipe à partir du client teams comme suit :

> [!div class="checklist"]
>
> * Dans le client Teams, sélectionnez **teams** dans la barre de navigation la plus à gauche.
> * Dans le menu déroulant, sélectionnez l’équipe où l’application est installée.
> * Sélectionnez l’icône **autres options** (&#8943;)
> * Sélectionnez **obtenir un lien vers une équipe** 
> * Copiez et enregistrez la valeur **GroupID** à partir de la chaîne.

### <a name="using-postman"></a>Utilisation de l’affranchissement

> [!div class="checklist"]
>
> * Ouvrez l’application [post](https://www.postman.com) .
> * Sélectionnez **File**  =>  **fichier**  =>  d'**importation** d’importation de fichier pour télécharger le fichier JSON mis à jour à partir de votre environnement.  
> * Sélectionnez l’onglet **Collections** . 
> * Sélectionnez le Chevron (>) en regard du **RSC de test** pour développer la vue des détails et voir les requêtes de l’API.

Exécutez toute la collection d’autorisations pour chaque appel d’API. Les autorisations que vous avez spécifiées dans votre manifeste de l’application doivent réussir, tandis que celles qui ne sont pas spécifiées doivent échouer avec un code d’état HTTP 403. Vérifiez tous les codes d’état de réponse pour vous assurer que le comportement des autorisations RSC dans votre application répond aux attentes.

>[!NOTE]
>Pour tester des appels d’API de suppression et de lecture spécifiques, ajoutez ces scénarios d’instance au fichier JSON.

## <a name="test--revoked-rsc-permissions-using-postman"></a>Test des autorisations RSC révoquées à l’aide du [post](https://www.postman.com/)

> [!div class="checklist"]
>
> * Désinstallez l’application de l’équipe spécifique.
> * Suivez les étapes ci-dessus pour [tester les autorisations RSC ajoutées à l’aide de l’affranchissement](#test-added-rsc-permissions-using-the-postman-app).
> * Vérifiez tous les codes d’état de réponse pour confirmer que les appels d’API spécifiques ayant réussi ont échoué avec un code d’état HTTP 403.

> [!div class="nextstepaction"]
>
> [En savoir plus sur l’API Graph et Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)
