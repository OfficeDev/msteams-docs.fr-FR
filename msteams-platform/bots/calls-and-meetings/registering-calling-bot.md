---
title: Inscrire les appels et le bot de réunions pour Microsoft Teams
description: Découvrez comment inscrire un nouveau bot d’appel audio/vidéo pour Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: appel d’un média audio/vidéo audio/vidéo de bot
ms.openlocfilehash: 5013ebcbce0bc94199e846f20fc6ee52238d302f1dd1b05872245ef2c6e32d91
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57709567"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>Inscrire les appels et le bot de réunions pour Microsoft Teams

Un bot qui participe à des appels audio ou vidéo et à des réunions en ligne est un bot Microsoft Teams ordinaire avec les fonctionnalités supplémentaires suivantes utilisées pour inscrire le bot :

* Il existe une nouvelle version du manifeste Teams’application avec deux paramètres supplémentaires, `supportsCalling` et `supportsVideo` . Ces paramètres sont inclus dans la [version](../../resources/dev-preview/developer-preview-intro.md) préliminaire du développeur du manifeste Teams’application.
* [Les Graph microsoft](./registering-calling-bot.md#add-graph-permissions) doivent être configurées pour l’ID d’application Microsoft de votre bot.
* Les autorisations Graph appels et les API de réunions en ligne nécessitent le consentement de l’administrateur client.

## <a name="new-manifest-settings"></a>Nouveaux paramètres de manifeste

Les bots d’appels et de réunions en ligne ont les deux paramètres supplémentaires suivants dans le manifest.jsqui activent l’audio ou la vidéo pour votre bot dans Teams.

* `bots[0].supportsCalling`. S’il est présent et qu’il est Teams, il permet à votre bot de `true` participer à des appels et à des réunions en ligne.
* `bots[0].supportsVideo`. S’il est présent et `true` qu’il est Teams que votre bot prend en charge la vidéo.

Si vous souhaitez que votre IDE valide correctement l'manifest.jssur le schéma de vos appels et bot de réunions pour ces valeurs, vous pouvez modifier l’attribut comme `$schema` suit :

```json
"$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
```

La section suivante vous permet de créer un bot ou d’ajouter des fonctionnalités d’appel à votre bot existant.

## <a name="create-new-bot-or-add-calling-capabilities"></a>Créer un bot ou ajouter des fonctionnalités d’appel

Pour plus d’informations sur la création de bots, voir [créer un bot pour Teams](../how-to/create-a-bot-for-teams.md).

**Pour créer un bot pour Teams**

1. Utilisez ce lien pour créer un bot, `https://dev.botframework.com/bots/new` . Sinon, si vous sélectionnez le bouton Créer un **bot** dans le portail Bot Framework, vous créez votre bot dans Microsoft Azure, pour lequel vous devez avoir un compte Azure.
1. Ajoutez le Teams canal de distribution.
1. Sélectionnez **l’onglet** Appel sur la page Teams canal. Sélectionnez **Activer l’appel,** puis mettez **à jour le webhook (pour** l’appel) avec votre URL HTTPS où vous recevez des notifications entrantes, par `https://contoso.com/teamsapp/api/calling` exemple. Pour plus d’informations, voir [la configuration des canaux.](/bot-framework/portal-configure-channels)

    ![Configurer les informations Teams canal de distribution](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

La section suivante fournit une liste des autorisations d’application pris en charge pour les appels et les réunions en ligne.

## <a name="add-graph-permissions"></a>Ajouter Graph autorisations d’autorisation

Le Graph fournit des autorisations granulaires pour contrôler l’accès des applications aux ressources. Vous déterminez les autorisations pour Graph votre application. Les Graph api d’appel de prise en charge des autorisations d’application, qui sont utilisées par les applications qui s’exécutent sans utilisateurs inscrits. Un administrateur client doit donner son consentement aux autorisations d’application.

### <a name="application-permissions-for-calls"></a>Autorisations d’application pour les appels

Le tableau suivant fournit une liste des autorisations d’application pour les appels :

|Autorisation    |Chaîne d’affichage   |Description |Consentement de l’administrateur requis |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| Calls.Initiate.All |Lancez les appels sortants 1:1 à partir de l’aperçu de l’application. |Permet à l’application de passer des appels sortants à un seul utilisateur et de transférer des appels à des utilisateurs dans l’annuaire de votre organisation, sans utilisateur connecté.|Oui|
| Calls.InitiateGroupCall.All |Lancez des appels de groupe sortants à partir de l’aperçu de l’application. |Permet à l’application de passer des appels sortants à plusieurs utilisateurs et d’ajouter des participants à des réunions dans votre organisation, sans utilisateur connecté.|Oui|
| Calls.JoinGroupCall.All |Participer à des appels de groupe et à des réunions en tant qu’aperçu d’application. |Permet à l’application de rejoindre les appels de groupe et les réunions planifiées dans votre organisation, sans utilisateur connecté. L’application est jointe avec les privilèges d’un utilisateur d’annuaire aux réunions dans votre client.|Oui|
| Calls.JoinGroupCallasGuest.All |Participer à des appels de groupe et à des réunions en tant qu’aperçu invité. |Permet à l’application de rejoindre anonymement les appels de groupe et les réunions planifiées dans votre organisation, sans utilisateur connecté. L’application est jointe en tant qu’invité aux réunions dans votre client.|Oui|
| Calls.AccessMedia.All |Accéder aux flux multimédias dans un appel en tant qu’aperçu d’application. |Permet à l’application d’obtenir un accès direct aux flux multimédias dans un appel, sans utilisateur connecté.|Oui|

> [!IMPORTANT]
> Vous ne pouvez pas utiliser l’API Media Access pour enregistrer ou faire persister du contenu multimédia à partir d’appels ou de réunions que votre application accède ou dérive des données de cet enregistrement ou enregistrement de contenu multimédia. Vous devez d’abord appeler [ `updateRecordingStatus` l’API](/graph/api/call-updaterecordingstatus) pour indiquer que l’enregistrement a commencé et recevoir une réponse de réussite de cette API. Si votre application commence à enregistrer une réunion ou un appel, elle doit mettre fin à l’enregistrement avant d’appeler l’API pour indiquer que l’enregistrement `updateRecordingStatus` est terminé.

### <a name="application-permissions-for-online-meetings"></a>Autorisations d’application pour les réunions en ligne

Le tableau suivant fournit une liste des autorisations d’application pour les réunions en ligne :

|Autorisation    |Chaîne d’affichage   |Description |Consentement de l’administrateur requis |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |Lire les détails de la réunion en ligne à partir de l’aperçu de l’application|Permet à l’application de lire les détails d’une réunion en ligne dans votre organisation, sans utilisateur.|Oui|
| OnlineMeetings.ReadWrite.All |Lire et créer des réunions en ligne à partir de l’aperçu de l’application pour le compte d’un utilisateur|Permet à l’application de créer des réunions en ligne dans votre organisation au nom d’un utilisateur, sans utilisateur.|Oui|

### <a name="assign-permissions"></a>Attribuer des autorisations

Vous devez configurer les autorisations d’application pour votre bot à l’avance à l’aide du portail [Azure](https://aka.ms/aadapplist) si vous préférez utiliser le point de terminaison [Azure Active Directory (AAD) V1](/azure/active-directory/develop/azure-ad-endpoint-comparison).

### <a name="get-tenant-administrator-consent"></a>Obtenir le consentement de l’administrateur client

Pour les applications utilisant le point de terminaison AAD V1, un administrateur client peut consentir aux autorisations d’application à l’aide du portail [Azure](https://portal.azure.com) lorsque votre application est installée dans son organisation. Vous pouvez également fournir une expérience d’inscription dans votre application par le biais de laquelle les administrateurs peuvent consentir aux autorisations que vous avez configurées. Une fois le consentement de l’administrateur enregistré par AAD, votre application peut demander des jetons sans avoir à demander à nouveau le consentement.

Vous pouvez compter sur un administrateur pour accorder les autorisations dont votre application a besoin sur le [portail Azure.](https://portal.azure.com) Une meilleure option consiste à fournir une expérience d’inscription aux administrateurs à l’aide du point de terminaison AAD `/adminconsent` V2. Pour plus d’informations, voir [les instructions sur la construction d’une URL de consentement d’administrateur.](https://developer.microsoft.com/graph/docs/concepts/auth_v2_service#3-get-administrator-consent)

> [!NOTE]
> Pour construire l’URL de consentement de l’administrateur client, un URI de redirection configuré ou une URL de réponse dans le portail [d’inscription](https://apps.dev.microsoft.com/) de l’application est requis. Pour ajouter des URL de réponse pour votre bot, accédez à l’inscription de votre bot, choisissez **Options avancées** Modifier le manifeste de  >  **l’application.** Ajoutez votre URL de redirection à la `replyUrls` collection.

> [!IMPORTANT]
> Chaque fois que vous modifiez les autorisations de votre application, vous devez également répéter le processus de consentement de l’administrateur. Les modifications apportées dans le portail d’inscription des applications ne sont pas reflétées tant que l’administrateur du client n’a pas réapplité le consentement.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Notifications d’appel entrant](~/bots/calls-and-meetings/call-notifications.md)
