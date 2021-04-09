---
title: Tester les autorisations de consentement spécifiques aux ressources dans Teams
description: Détails du test du consentement spécifique aux ressources dans Teams à l’aide de Postman
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: Teams Authorization OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 0d3d1c895c77bb417a9fdd84e319103485aa8944
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634706"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Tester les autorisations de consentement spécifiques aux ressources dans Teams

Le consentement spécifique aux ressources (RSC) est une intégration d’API Microsoft Teams et Graph qui permet à votre application d’utiliser des points de terminaison d’API pour gérer des équipes spécifiques au sein d’une organisation. Pour plus d’informations, voir consentement spécifique aux [ressources (RSC) — API Microsoft Teams Graph](resource-specific-consent.md).

> [!NOTE]
> Pour tester les autorisations RSC, votre fichier manifeste d’application Teams doit inclure une clé **webApplicationInfo** remplie avec les champs suivants :
>
> - **id**: votre ID d’application Azure AD, voir Inscrire votre [application dans le portail Azure AD.](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
> - **ressource**: n’importe quelle chaîne, voir la note dans  [mettre à jour le manifeste de votre application Teams](resource-specific-consent.md#update-your-teams-app-manifest)
> - **autorisations d’application**: autorisations RSC pour votre application, voir [Autorisations propres aux ressources.](resource-specific-consent.md#resource-specific-permissions)

```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

> [!IMPORTANT]
> Dans le manifeste de votre application, incluez uniquement les autorisations RSC dont vous souhaitez que votre application soit propriétaire.

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>Test des autorisations RSC ajoutées à l’aide de l’application Postman

Pour vérifier si les autorisations RSC sont honorées par la charge utile de demande d’API, vous devez copier le code de [test JSON RSC](test-rsc-json-file.md) dans votre environnement local et mettre à jour les valeurs suivantes :

* `azureADAppId`: ID d’application Azure AD de votre application
* `azureADAppSecret`: Votre secret d’application Azure AD (mot de passe)
* `token_scope`: l’étendue est requise pour obtenir un jeton : définissez la valeur sur https://graph.microsoft.com/.default
* `teamGroupId`: vous pouvez obtenir l’ID de groupe d’équipe à partir du client Teams comme suit :

  > [!div class="checklist"]
  >
  > * Dans le client Teams, sélectionnez **Teams** dans la barre de navigation à l’extrême gauche.
  > * Sélectionnez l’équipe où l’application est installée dans le menu déroulant.
  > * Sélectionnez **l’icône Options** supplémentaires (&#8943;)
  > * Sélectionnez **Obtenir un lien vers l’équipe** 
  > * Copiez et enregistrez la **valeur groupId** à partir de la chaîne.

### <a name="use-postman"></a>Utiliser Postman

1. Ouvrez [l’application Postman.](https://www.postman.com)
2. Sélectionnez   >  **le fichier**  >  **d’importation de** fichiers pour télécharger le fichier JSON mis à jour à partir de votre environnement.  
3. Sélectionnez **l’onglet Collections.** 
4. Sélectionnez le chevron en regard du test RSC pour développer l’affichage des **>** détails et afficher les demandes d’API. 

Exécutez l’ensemble de la collection d’autorisations pour chaque appel d’API. Les autorisations que vous avez spécifiées dans le manifeste de votre application doivent réussir, tandis que celles qui ne sont pas spécifiées doivent échouer avec un code d’état HTTP 403. Vérifiez tous les codes d’état de réponse pour vérifier que le comportement des autorisations RSC dans votre application répond aux attentes.

> [!NOTE]
> Pour tester des appels d’API DELETE et READ spécifiques, ajoutez ces scénarios d’instance au fichier JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Tester les autorisations RSC révoquées à l’aide [de Postman](https://www.postman.com/)

1. Désinstallez l’application de l’équipe spécifique.
2. Suivez les étapes pour [tester les autorisations RSC ajoutées à l’aide de Postman](#test-added-rsc-permissions-using-the-postman-app).
3. Vérifiez tous les codes d’état de réponse pour confirmer que les appels d’API spécifiques, qui ont réussi, ont échoué avec un code d’état **HTTP 403**.

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [API Microsoft Graph et Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

