---
title: Enregistrer le bot d’appels et de réunions pour Microsoft Teams
description: Dans ce module, découvrez comment inscrire un nouveau bot d’appel audio/vidéo pour Microsoft Teams, créer un bot ou ajouter une fonctionnalité d’appel et ajouter des autorisations de graphe.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 74e786850f11a77cea5cc0980febb56d550ae671
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143794"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>Enregistrer le bot d’appels et de réunions pour Microsoft Teams

Un bot qui participe à des appels audio ou vidéo et à des réunions en ligne est un bot Microsoft Teams normal avec les fonctionnalités supplémentaires suivantes utilisées pour inscrire le bot :

* Il existe une nouvelle version du manifeste d’application Teams avec deux paramètres supplémentaires, `supportsCalling` et `supportsVideo`. Ces paramètres sont inclus dans le schéma de manifeste [pour Microsoft Teams](../../resources/schema/manifest-schema.md).
* [Microsoft Graph autorisations](./registering-calling-bot.md#add-graph-permissions) doivent être configurées pour l’ID d’application Microsoft de votre bot.
* Les autorisations des API d’appels et de réunions en ligne Graph nécessitent le consentement de l’administrateur client.

## <a name="new-manifest-settings"></a>Nouveaux paramètres de manifeste

Les bots d’appels et de réunions en ligne ont les deux paramètres supplémentaires suivants dans le fichier manifest.json qui activent l’audio ou la vidéo pour votre bot dans Teams.

* `bots[0].supportsCalling`. S’il est présent et défini sur `true`, Teams permet à votre bot de participer à des appels et des réunions en ligne.
* `bots[0].supportsVideo`. S’il est présent et défini sur `true`, Teams sait que votre bot prend en charge la vidéo.

Si vous souhaitez que votre IDE valide correctement le schéma manifest.json pour vos appels et bot de réunions pour ces valeurs, vous pouvez modifier l’attribut `$schema` comme suit :

```json
"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
```

La section suivante vous permet de créer un bot ou d’ajouter des fonctionnalités d’appel à votre bot existant.

## <a name="create-new-bot-or-add-calling-capabilities"></a>Créer un bot ou ajouter des fonctionnalités d’appel

Pour plus d’informations sur la création de bots, consultez [créer un bot pour Teams](../how-to/create-a-bot-for-teams.md).

Pour créer un bot pour Teams :

1. Utilisez ce lien pour créer un bot, `https://dev.botframework.com/bots/new`. Sinon, si vous sélectionnez le bouton **Créer un bot** dans le portail Bot Framework, vous créez votre bot dans Microsoft Azure, pour lequel vous devez disposer d’un compte Azure.
1. Ajoutez le canal Teams.
1. Sélectionnez l’onglet **Appel** dans la page du canal Teams. Sélectionnez **Activer l’appel**, puis mettez à jour **webhook (pour appeler)** avec votre URL HTTPS où vous recevez des notifications entrantes, par exemple `https://contoso.com/teamsapp/api/calling`. Pour plus d’informations, consultez [configuration des canaux](/bot-framework/portal-configure-channels).

    ![Configurer les informations de canal Teams](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

La section suivante fournit la liste des autorisations d’application prises en charge pour les appels et les réunions en ligne.

## <a name="add-graph-permissions"></a>Ajouter des autorisations Graph

Graph fournit des autorisations granulaires pour contrôler l’accès des applications aux ressources. Vous décidez des autorisations pour Graph que demande votre application. Les API d’appel Graph prennent en charge les autorisations d’application, qui sont utilisées par les applications qui s’exécutent sans utilisateur connecté. Un administrateur client doit accorder son consentement aux autorisations d’application.

### <a name="application-permissions-for-calls"></a>Autorisations d’application pour les appels

Le tableau suivant fournit la liste des autorisations d’application pour les appels :

|Autorisation    |Chaîne d’affichage   |Description |Autorisation de l’administrateur requise |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| Calls.Initiate.All |Lancer les appels sortants 1:1 depuis l’application aperçu. |Permet à l’application de passer des appels sortants à un seul utilisateur et de transférer des appels à des utilisateurs dans l’annuaire de votre organisation, sans utilisateur connecté.|Oui|
| Calls.InitiateGroupCall.All |Lancer les appels de groupe sortants 1:1 depuis l’application aperçu. |Permet à l’application de passer des appels sortants à plusieurs utilisateurs et d’ajouter des participants à des réunions dans votre organisation, sans utilisateur connecté.|Oui|
| Calls.JoinGroupCall.All |Rejoignez des appels de groupe et des réunions en tant qu’aperçu d’application. |Permet à l’application de rejoindre les appels de groupe et les réunions planifiées dans votre organisation, sans utilisateur connecté. L’application est jointe avec les privilèges d’un utilisateur d’annuaire aux réunions dans votre locataire.|Oui|
| Calls.JoinGroupCallasGuest.All |Rejoignez des appels de groupe et des réunions en tant qu’aperçu invité. |Permet à l’application de rejoindre anonymement les appels de groupe et les réunions planifiées dans votre organisation, sans utilisateur connecté. L’application est jointe en tant qu’invité aux réunions de votre locataire.|Oui|
| Calls.AccessMedia.All |Accédez aux flux multimédias dans un appel en tant qu’aperçu d’application. |Permet à l’application d’obtenir un accès direct aux flux multimédias dans un appel, sans utilisateur connecté.|Oui|

> [!IMPORTANT]
> Vous ne pouvez pas utiliser l’API Media Access pour enregistrer ou conserver le contenu multimédia à partir d’appels ou de réunions auxquels votre application accède ou dériver des données de cet enregistrement ou enregistrement de contenu multimédia. Vous devez d’abord appeler [`updateRecordingStatus`l’API](/graph/api/call-updaterecordingstatus) pour indiquer que l’enregistrement a commencé et recevoir une réponse réussie de cette API. Si votre application commence à enregistrer une réunion ou un appel, elle doit terminer l’enregistrement avant d’appeler l’API `updateRecordingStatus` pour indiquer que l’enregistrement est terminé.

### <a name="application-permissions-for-online-meetings"></a>Autorisations d’application pour les réunions en ligne

Le tableau suivant fournit la liste des autorisations d’application pour les réunions en ligne :

|Autorisation    |Chaîne d’affichage   |Description |Autorisation de l’administrateur requise |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |Lire les détails de la réunion en ligne à partir de la préversion de l’application|Permet à l’application de lire tous les détails de la réunion en ligne dans votre organisation, sans utilisateur connectée.|Oui|
| OnlineMeetings.ReadWrite.All |Lire et créer des réunions en ligne à partir de la préversion de l’application pour le compte d’un utilisateur|Permet à l’application de créer des réunions en ligne dans votre organisation pour le compte d’un utilisateur, sans utilisateur connecté.|Oui|

### <a name="assign-permissions"></a>Attribuer des autorisations

Vous devez configurer les autorisations d’application pour votre bot à l’avance à l’aide de l' [Portail Microsoft Azure](https://portal.azure.com) si vous préférez utiliser le point de terminaison [Microsoft Azure Active Directory (Azure AD) V1](/azure/active-directory/develop/azure-ad-endpoint-comparison).

### <a name="get-tenant-administrator-consent"></a>Obtenir le consentement de l’administrateur client

Pour les applications utilisant le point de terminaison Azure AD V1, un administrateur client peut donner son consentement aux autorisations d’application à l’aide du [Portail Microsoft Azure](https://portal.azure.com) lorsque votre application est installée dans son organisation. Vous pouvez également fournir une expérience d’inscription dans votre application par le biais de laquelle les administrateurs peuvent donner leur consentement aux autorisations que vous avez configurées. Une fois que le consentement de l’administrateur est enregistré par Azure AD, votre application peut demander des jetons sans avoir à demander à nouveau le consentement.

Vous pouvez vous appuyer sur un administrateur pour accorder les autorisations dont votre application a besoin au [Portail Microsoft Azure](https://portal.azure.com). Une meilleure option consiste à fournir une expérience d’inscription pour les administrateurs à l’aide du point de terminaison Azure AD V2 `/adminconsent` . Pour plus d’informations, consultez [instructions sur la construction d’une URL de consentement administrateur](/graph/auth-v2-service#3-get-administrator-consent).

> [!NOTE]
> Pour construire l’URL de consentement de l’administrateur client, un URI de redirection ou une URL de réponse configuré dans le [portail d’inscription d’application](https://apps.dev.microsoft.com/) est requis. Pour ajouter des URL de réponse pour votre bot, accédez à l’inscription de votre bot, choisissez **Options avancées** > **Modifier le manifeste d’application**. Ajoutez votre URL de redirection à la collection `replyUrls`.

> [!IMPORTANT]
> Chaque fois que vous apportez une modification aux autorisations de votre application, vous devez également répéter le processus de consentement de l’administrateur. Les modifications apportées dans le portail d’inscription d’application ne sont pas répercutées tant que le consentement n’a pas été réappliqué par l’administrateur du locataire.

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **Graph** |
|---------------|----------|--------|
| Appeler et rencontrer un bot | L’exemple d’application montre comment le bot peut créer un appel, participer à une réunion et transférer un appel. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-calling-meeting/csharp) |

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../sbs-calling-and-meeting.yml) pour configurer l’appel et la réunion dans un bot.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Notifications d’appel entrant](~/bots/calls-and-meetings/call-notifications.md)

## <a name="see-also"></a>Voir aussi

* [Notifications d’appel entrant](~/bots/calls-and-meetings/call-notifications.md)
* [développer des bots d’appel et de réunion en ligne sur votre PC local](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
* [Afficher l’autorisation d’application et accorder le consentement de l’administrateur](/MicrosoftTeams/app-permissions-admin-center)
