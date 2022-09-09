---
title: Teams Connect canaux partagés
author: Rajeshwari-v
description: Découvrez Teams Connect canaux partagés pour collaborer en toute sécurité avec des utilisateurs internes et externes dans un espace partagé sans changer de locataire.
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: f063be5bce83484a259e67e94f4caa73ef8afa76
ms.sourcegitcommit: bd30d33af59dd870a309ae72b4c4496c9c1f920d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/09/2022
ms.locfileid: "67635314"
---
# <a name="microsoft-teams-connect-shared-channels"></a>Microsoft Teams Connect canaux partagés

Microsoft Teams Connect canaux partagés permettent aux membres d’un canal de collaborer avec des utilisateurs au sein d’autres équipes et organisations. Vous pouvez créer et partager un canal partagé avec :

* Membres d’une autre équipe au sein de la même organisation.
* Individus au sein d’une même organisation.
* Individus et autres équipes d’autres organisations.

Teams Connect canaux partagés facilitent la collaboration sécurisée en toute transparence. Autoriser les utilisateurs externes en dehors de votre organisation à collaborer avec des utilisateurs internes dans Teams sans modifier leur contexte utilisateur. Améliorez l’expérience utilisateur contrairement à l’utilisation de comptes invités. Par exemple, les membres doivent se déconnecter de Teams et se reconnecter à l’aide d’un compte invité. Les applications Teams étendent l’espace de collaboration puissant.

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="Diagramme montrant l’équipe B de l’organisation A et l’équipe C de l’organisation B qui collaborent dans un canal partagé en tant qu’équipe A." border="true" :::

## <a name="enable-your-app-for-shared-channels"></a>Activer votre application pour les canaux partagés

SupportedChannelTypes est une propriété facultative qui active votre application dans des canaux non standard. Si votre application prend en charge l’étendue de l’équipe et que la propriété est définie, Teams active votre application dans chaque type de canal en conséquence. Les canaux privés et partagés sont actuellement pris en charge. Pour plus d’informations, consultez [supportedChannelTypes](../../resources/schema/manifest-schema.md#supportedchanneltypes).

```JSON
"supportedChannelTypes": {
      "type": "array",
      "description": "List of ‘non-standard’ channel types that the app supports. Note: Channels of standard type are supported by default if the app supports team scope. ",
      "maxItems": 2,
      "items": { 
        "enum": [
          "sharedChannels",
          "privateChannels"
        ]
      }
    }
```

> [!NOTE]
>
> * Si votre application prend en charge l’étendue de l’équipe, elle fonctionne dans les canaux standard, quelles que soient les valeurs définies dans cette propriété.
> * Votre application devra peut-être tenir compte des propriétés uniques de chacun de ces types de canaux pour fonctionner correctement.

## <a name="get-context-for-shared-channels"></a>Obtenir le contexte pour les canaux partagés

Lorsque l’expérience utilisateur de contenu est chargée dans un canal partagé, utilisez les données reçues de l’appel pour les modifications de `getContext` canal partagé. `getContext` l’appel publie deux nouvelles propriétés, `hostTeamGroupID` qui `hostTenantID`sont utilisées pour récupérer l’appartenance au canal à l’aide des API Microsoft Graph. `hostTeam` est l’équipe qui crée le canal partagé.

Pour plus d’informations sur l’activation de votre onglet, consultez :

* [Obtenir le contexte de votre onglet pour les canaux privés](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [Obtenir le contexte dans les canaux partagés](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

## <a name="apps-and-permissions-in-shared-channels"></a>Applications et autorisations dans les canaux partagés

Vous pouvez collaborer avec des membres externes en dehors de votre organisation à l’aide de canaux partagés. Les autorisations d’application dans les canaux partagés suivent la liste des applications de l’équipe hôte et la stratégie d’application du locataire hôte.

> [!NOTE]
> [L’API de notification de flux d’activité](/graph/teams-send-activityfeednotifications) ne prend pas en charge les notifications interlocataires pour les applications dans un canal partagé.

## <a name="get-shared-channel-membership"></a>Obtenir l’appartenance au canal partagé

Vous pouvez obtenir l’appartenance directe au canal partagé en suivant les `hostTeamGroupID` étapes ci-dessous `getContext` :

1. Obtenir des membres directs avec [l’API DES membres du canal GET](/graph/api/channel-list-members?view=graph-rest-beta&tabs=http&preserve-view=true) .

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. Obtenez chaque équipe partagée avec l’API GET `sharedWithTeams` .

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams
    ```

3. Utilisez les membres GET de chaque équipe partagée (Équipe X) avec l’API GET `sharedWithTeams` .

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams/{teamX}/members
    ```

## <a name="classify-members-in-the-shared-channel-as-in-tenant-or-out-tenant"></a>Classifier les membres dans le canal partagé en tant qu’utilisateurs locataires ou out-tenants

Vous pouvez classer les membres en tant que membres in-tenant ou out-tenant en `tenantID` comparant le membre ou l’équipe avec `hostTeamTenantID` les éléments suivants :

1. Obtenez le membre que vous souhaitez comparer.

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. Utilisez `getContext`, comparez le `tenantID` membre à la `hostTenantID` propriété.

## <a name="azure-ad-native-identity"></a>Identité native Azure AD

Les applications doivent fonctionner entre locataires lors de l’installation et de l’utilisation. Le tableau suivant répertorie les types de canaux et leurs ID de groupe correspondants :

|Type de canal| groupId | hostTeamGroupId |
|----------|---------|-----------------|
|Regular | ID de groupe Azure AD d’équipe | ID de groupe Azure AD d’équipe |
|Shared | Vide | ID de groupe Azure AD de l’équipe hôte |

## <a name="see-also"></a>Voir aussi

* [Créer des onglets pour Teams](../../tabs/what-are-tabs.md)
* [Schéma du manifeste d’application pour Teams](../../resources/schema/manifest-schema.md)
* [Canaux partagés dans Microsoft Teams](/MicrosoftTeams/shared-channels)
* [Stratégie de rétention pour les emplacements Teams](/microsoft-365/compliance/create-retention-policies)
