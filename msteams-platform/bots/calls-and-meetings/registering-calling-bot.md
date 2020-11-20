---
title: Inscription d’un robot de réunion et d’appel pour Microsoft teams
description: Découvrez comment enregistrer un nouveau robot d’appel audio/vidéo pour Microsoft teams
keywords: appels audio/vidéo vidéo audio/vidéo
ms.openlocfilehash: d38b9584440bcff664bd3a2d4b57e52bc695f1b5
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346846"
---
# <a name="register-a-calling-bot-for-microsoft-teams"></a>Enregistrer un bot appelant pour Microsoft teams

Un bot qui participe à des appels audio/vidéo et des réunions en ligne est un robot Microsoft teams ordinaire avec quelques fonctionnalités supplémentaires :

* Il existe une nouvelle version du manifeste de l’application teams avec deux paramètres supplémentaires, `supportsCalling` et `supportsVideo` . Ces paramètres sont inclus dans la version d' [évaluation du développeur](../../resources/dev-preview/developer-preview-intro.md) du manifeste de l’application Microsoft Teams.
* Les [autorisations Microsoft Graph](./registering-calling-bot.md#add-microsoft-graph-permissions) doivent être configurées pour l’ID d’application Microsoft de votre robot.
* Les autorisations d’appels et d’API de réunions en ligne de Microsoft Graph nécessitent un consentement de l’administrateur client.

Nous allons étudier ce qui précède plus en détail.

## <a name="new-manifest-settings"></a>Nouveaux paramètres de manifeste

Les robots d’appels et de réunions en ligne ont deux paramètres supplémentaires dans la manifest.jssur qui activent l’audio/vidéo pour votre robot dans Teams.

* `bots[0].supportsCalling`. S’il est présent et défini sur `true` , teams permettra à votre bot de participer à des appels et réunions en ligne.
* `bots[0].supportsVideo`. S’il est présent et défini sur `true` , teams sait que votre bot prend en charge la vidéo.

Si vous souhaitez que votre IDE valide correctement les manifest.jssur le schéma de votre appel et de votre robot de réunion pour ces valeurs, vous pouvez modifier l' `$schema` attribut comme suit :

```json
"$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
```

## <a name="creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot"></a>Création d’un nouveau Bot ou ajout de fonctionnalités d’appel à un bot existant

La création d’un nouveau Bot est décrite plus en détail dans la rubrique [créer un bot pour Microsoft teams](../how-to/create-a-bot-for-teams.md) , mais nous allons répéter une partie de celle-ci ici :

1. Utilisez ce lien pour créer un nouveau robot : `https://dev.botframework.com/bots/new` . Si, au lieu de cela, vous sélectionnez le bouton *créer un bot* dans le portail de l’infrastructure bot, vous allez créer votre robot dans Microsoft Azure, pour lequel vous aurez besoin d’un compte Azure.
1. Ajoutez le canal Microsoft Teams. Cliquez sur l’onglet « appel » de la page de la chaîne Microsoft teams et sélectionnez **activer l’appel**, puis mettez à jour **webhook (pour les appels)** avec votre URL https dans laquelle vous recevrez des notifications entrantes, par exemple `https://contoso.com/teamsapp/api/calling` . Reportez-vous à la rubrique [Configuring Channels](/bot-framework/portal-configure-channels) pour plus d’informations sur la configuration des canaux.
  ![Configurer les informations de canal Microsoft teams](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

## <a name="add-microsoft-graph-permissions"></a>Ajouter des autorisations Microsoft Graph

Microsoft Graph expose des autorisations granulaires qui contrôlent l’accès des applications aux ressources. En tant que développeur, vous décidez des autorisations demandées par votre application pour Microsoft Graph.  Les API d’appel Microsoft Graph prennent en charge les _autorisations d’application_, qui sont utilisées par les applications qui s’exécutent sans utilisateur connecté présent.  Un administrateur client doit accorder le consentement aux autorisations d’application. Vous trouverez ci-dessous une liste de ces autorisations :

### <a name="application-permissions-calls"></a>Autorisations d’application : appels

|Autorisation    |Chaîne d’affichage   |Description |Autorisation de l’administrateur requise |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
|_Calls.Initiate.All_|Lancer les appels sortants 1:1 depuis l’application (aperçu)|Permet à l’application de passer des appels sortants à un seul utilisateur et de transférer des appels à des utilisateurs dans l’annuaire de votre organisation, sans utilisateur connecté.|Oui|
|_Calls.InitiateGroupCall.All_|Lancer les appels de groupe sortants 1:1 depuis l’application (aperçu)|Permet à l’application de passer des appels sortants à plusieurs utilisateurs et d’ajouter des participants à des réunions dans votre organisation, sans utilisateur connecté.|Oui|
|_Calls.JoinGroupCall.All_|Participer à des réunions et à des appels de groupe en tant qu’application (aperçu)|Allows the app to join group calls and scheduled meetings in your organization, without a signed-in user. The app will be joined with the privileges of a directory user to meetings in your tenant.|Oui|
|_Calls.JoinGroupCallasGuest.All_|Participer à des réunions et à des appels de groupe en tant qu’invité (aperçu)|Allows the app to anonymously join group calls and scheduled meetings in your organization, without a signed-in user. The app will be joined as a guest to meetings in your tenant.|Oui|
|_Calls. AccessMedia. All_ <sup> _voir ci-dessous_</sup>|Accéder aux flux multimédias dans un appel en tant qu’application (aperçu)|Permet à l’application d’obtenir un accès direct aux flux multimédias dans un appel, sans utilisateur connecté.|Oui|

> [!IMPORTANT]
> Vous **ne pouvez pas** utiliser l’API Microsoft. Graph. Calls. Media pour enregistrer ou conserver un contenu multimédia à partir d’appels ou de réunions auxquels votre bot accède.

### <a name="application-permissions-online-meetings"></a>Autorisations d’application : réunions en ligne

|Autorisation    |Chaîne d’affichage   |Description |Autorisation de l’administrateur requise |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
|_OnlineMeetings.Read.All_|Lire les détails de la réunion en ligne à partir de l’application (aperçu)|Permet à l’application de lire tous les détails de la réunion en ligne dans votre organisation, sans utilisateur connectéé.|Oui|
|_OnlineMeetings.ReadWrite.All_|Lire et créer des réunions en ligne à partir de l’application (aperçu) au nom d’un utilisateur|Permet à l’application de créer des réunions en ligne dans votre organisation au nom d’un utilisateur, sans utilisateur connecté.|Oui|

### <a name="assigning-permissions"></a>Attribution d'autorisations

Si vous préférez utiliser le [point de terminaison Azure ad v1](/azure/active-directory/develop/azure-ad-endpoint-comparison), vous devez configurer les autorisations d’application pour votre robot à l’aide du [portail Azure](https://aka.ms/aadapplist) .

### <a name="getting-tenant-administrator-consent"></a>Obtention du consentement de l’administrateur client

Pour les applications qui utilisent le point de terminaison Azure AD v1, un administrateur client peut accorder des autorisations d’application à l’aide du [portail Azure](https://portal.azure.com) lorsque votre application est installée dans son organisation, ou vous pouvez fournir une expérience d’inscription dans votre application grâce à laquelle les administrateurs peuvent consentir aux autorisations que vous avez configurées. Une fois le consentement de l’administrateur enregistré par Azure AD, votre application peut demander des jetons sans avoir à demander de nouveau l’autorisation.

Vous pouvez compter sur un administrateur pour accorder les autorisations dont votre application a besoin sur le [portail Azure](https://portal.azure.com); Toutefois, il est souvent préférable de fournir une expérience d’abonnement pour les administrateurs à l’aide du point de terminaison Azure AD v2 `/adminconsent` .  Pour plus d’informations, reportez-vous aux [instructions sur la création d’une URL de consentement d’administrateur](https://developer.microsoft.com/graph/docs/concepts/auth_v2_service#3-get-administrator-consent) .

> [!NOTE]
> La construction de l’URL de consentement de l’administrateur client nécessite une URL de redirection/URL de réponse dans le [portail d’inscription des applications](https://apps.dev.microsoft.com/). Pour ajouter des URL de réponse pour votre bot, accédez à votre enregistrement de robot, choisissez Options avancées-> modifier le manifeste d’application.  Ajoutez votre URL de redirection à la `replyUrls` collection.

> [!IMPORTANT]
> Chaque fois que vous modifiez les autorisations de votre application, vous devez également répéter le processus de consentement de l’administrateur. Les modifications apportées dans le portail d’inscription des applications prennent effet uniquement lorsque le consentement a été donné par l’administrateur du client.
