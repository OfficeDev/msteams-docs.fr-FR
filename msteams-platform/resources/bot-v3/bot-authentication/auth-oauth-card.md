---
title: Utilisation d’Azure Bot Service pour l’authentification dans Teams
description: Décrit OAuthCard azure Bot Service et son utilisation pour l’authentification
ms.topic: conceptual
localization_priority: Normal
keywords: Authentification teams OAuthCard OAuth carte Azure Bot Service
ms.openlocfilehash: 3d0df4f04625c5be3468d12319b54096ae06de90
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020680"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Utilisation d’Azure Bot Service pour l’authentification dans Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Sans OAuthCard du service Azure Bot, il est compliqué d’implémenter l’authentification dans un bot. Il s’agit d’un défi à pile complète qui implique la création d’une expérience web, l’intégration avec des fournisseurs OAuth externes, la gestion des jetons et la gestion des appels d’API de serveur à serveur pour terminer le flux d’authentification en toute sécurité. Cela peut entraîner des expériences complexes nécessitant l’entrée de « nombres magiques ».

Avec OAuthCard d’Azure Bot Service, il est plus facile pour votre bot Teams de se connecter à vos utilisateurs et d’accéder à des fournisseurs de données externes. Que vous avez déjà implémenté l’authentification et que vous souhaitez basculer vers quelque chose de plus simple, ou si vous cherchez à ajouter l’authentification à votre service de bot pour la première fois, OAuthCard peut faciliter la tâche.

D’autres [](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) rubriques de l’authentification décrivent l’authentification sans utiliser OAuthCard. Ainsi, si vous souhaitez mieux comprendre l’authentification dans Teams ou si vous ne pouvez pas utiliser OAuthCard, vous pouvez toujours vous référer à ces rubriques.

## <a name="support-for-the-oauthcard"></a>Prise en charge d’OAuthCard

Il existe actuellement certaines restrictions quant à l’endroit où vous pouvez utiliser OAuthCard. Elles incluent les éléments suivants :

* La carte ne fonctionne pas avec [l’accès invité](/MicrosoftTeams/guest-access)
* Elle ne fonctionne pas avec [Microsoft Teams gratuite](https://products.office.com/microsoft-teams/free)
* Il peut uniquement être utilisé pour l’authentification bot
* Elle fonctionne uniquement pour les bots inscrits dans [le service Azure Bot](https://azure.microsoft.com/services/bot-service/)

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Comment azure Bot Service m’aide-t-il à l’authentification ?

La documentation complète utilisant OAuthCard est disponible dans la rubrique : Ajouter [l’authentification](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true)à votre bot via Azure Bot Service . Notez que cette rubrique se trouve dans l’ensemble de documentation Azure Bot Framework et n’est pas spécifique à Teams.

Les sections suivantes indiquent comment utiliser OAuthCard dans Teams.

## <a name="main-benefits-for-teams-developers"></a>Principaux avantages pour les Teams développeurs

OAuthCard facilite l’authentification des manières suivantes :

* Fournit un flux d’authentification web pré-fourni : vous n’avez plus besoin d’écrire et d’héberger une page web pour diriger vers des expériences de connexion externes ou fournir une redirection.
* Est transparent pour les utilisateurs finaux : terminez l’expérience de la Teams.
* Inclut une gestion simple des jetons : vous n’avez plus besoin d’implémenter un système de stockage de jetons . Au lieu de cela, le service bot s’occupe de la mise en cache des jetons et fournit un mécanisme sécurisé pour récupérer ces jetons.
* Est pris en charge par des SDK complets : faciles à intégrer et à utiliser à partir de votre service de bot.
* Offre une prise en charge préétent e pour de nombreux fournisseurs OAuth populaires, tels qu’Azure AD/MSA, Facebook et Google.

## <a name="when-should-i-implement-my-own-solution"></a>Quand dois-je implémenter ma propre solution ?

Étant donné que les jetons d’accès sont des informations sensibles, vous ne souhaitez peut-être pas les stocker dans un service externe. Dans ce cas, vous pouvez choisir d’implémenter votre propre système de gestion des jetons et [](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) votre expérience de connexion au sein de Teams, comme décrit dans le reste des rubriques sur l’authentification Teams.

## <a name="getting-started-with-oauthcard-in-teams"></a>Mise en place d’OAuthCard dans Teams

> [!NOTE]
> Ce guide utilise le SDK Bot Framework v3. Vous trouverez l’implémentation v4 [ici.](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) Vous devrez toujours créer un manifeste et inclure des token.botframework.com dans la section, car sinon, le bouton Se connecter n’ouvrira pas `validDomains` la fenêtre d’authentification. Utilisez [App Studio pour](~/concepts/build-and-test/app-studio-overview.md) générer votre manifeste.

Vous devez d’abord configurer votre service de bot Azure pour configurer des fournisseurs d’authentification externes. Lisez [Configuration des fournisseurs d’identité pour](~/concepts/authentication/configure-identity-provider.md) obtenir la procédure détaillée.

Pour activer l’authentification à l’aide d’Azure Bot Service, vous devez ajouter ces ajouts à votre code :

1. Incluez token.botframework.com dans la section du manifeste de votre application, car Teams incorporera la page de connexion `validDomains` du bot Service.
2. Récupérer le jeton à partir du service bot chaque fois que votre bot doit accéder aux ressources authentifiées. Si aucun jeton n’est disponible, envoyez un message avec un OAuthCard à l’utilisateur lui demandant de se connecter au service externe.
3. Gérer l’activité d’achèvement de connexion. Cela garantit que la demande d’authentification et le jeton sont associés à l’utilisateur qui interagit actuellement avec votre bot.
4. Récupérez le jeton chaque fois que votre bot doit effectuer des actions authentifiées, telles que l’appel d’API REST externes.

Dans votre code de boîte de dialogue, vous devez ajouter cet extrait de code (C#), qui recherche un jeton d’accès existant :

```CSharp
// First ask Bot Service if it already has a token for this user
var token = await context.GetUserTokenAsync(ConnectionName).ConfigureAwait(false);
if (token != null)
{
    // use the token to do exciting things!
}
else
{
    // If Bot Service does not have a token, send an OAuth card to sign in 
    await SendOAuthCardAsync(context, (Activity)context.Activity);
}
```

Si un jeton d’accès n’existe pas, votre code envoie ensuite un message avec OAuthCard à l’utilisateur :

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

Pour gérer l’activité de connexion terminée, vous devez traiter cet Appel :

```CSharp
if (activity.Name == "signin/verifyState")
{
  // We do this so that we can pass handling to the right logic in the dialog. You can
  // set this to be whatever string you want.
  activity.Text = "loginComplete";
  await Conversation.SendAsync(activity, () => new Dialogs.RootDialog());

  return Request.CreateResponse(HttpStatusCode.OK);
}
```

Dans votre code de boîte de dialogue, vous pouvez ensuite récupérer le jeton à partir du service d’authentification bot :

```CSharp
if (text.Contains("loginComplete"))
  {
    // Handle login completion event.
    JObject ctx = activity.Value as JObject;

    if (ctx != null)
    {
      string code = ctx["state"].ToString();

      var oauthClient = activity.GetOAuthClient();
      var token = await oauthClient.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, magicCode: code).ConfigureAwait(false);
      if (token != null)
      {
        // Make whatever API calls here you want
        await context.PostAsync($"Success! You are now signed in.");
      }
    }
  // Need to respond to the Invoke.
  return;
}
```

## <a name="using-oauthcard-with-messaging-extensions"></a>Utilisation d’OAuthCard avec les extensions de messagerie

Vous pouvez également utiliser Azure Bot Service pour connecter des fournisseurs tiers à votre extension de messagerie. Le flux est le même qu’avec un bot, sauf qu’au lieu de renvoyer un OAuthCard, votre service retournera une invite de connexion.

L’extrait de code suivant (C#) illustre comment créer la réponse de connexion :

```CSharp
var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName).ConfigureAwait(false);

if (token == null)
{
  // Send the login response with the auth link.
  string link = await client.OAuthApi.GetSignInLinkAsync(activity, ConnectionName);

  response = new ComposeExtensionResponse()
  {
    ComposeExtension = new ComposeExtensionResult()
  };
  response.ComposeExtension.Type = "auth";
  response.ComposeExtension.SuggestedActions = new ComposeExtensionSuggestedAction()
  {
    Actions = new List<CardAction>()
      {
        new CardAction(ActionTypes.OpenUrl, title: "Sign into this app", value: link)
      }
    };
  return response;
}
```

Notez que dans l’exemple ci-dessus, vous devez effectuer l’appel `GetSignInLinkAsync` directement par rapport à la `client.OAuthApi` propriété.

Lorsque l’utilisateur termine correctement la séquence de connexion, votre service reçoit une autre demande Invoke contenant la requête utilisateur d’origine, ainsi qu’une chaîne de paramètre d’état contenant le « code magique ». Vous pouvez maintenant récupérer le jeton à l’aide de cette chaîne, ainsi que l’ID d’utilisateur et le nom de connexion.

```CSharp
var query = activity.GetComposeExtensionQueryData();
JObject data = activity.Value as JObject;

var client = activity.GetOAuthClient();

// Check if the request comes with login state
if (data != null && data["state"] != null)
{
  var token = await client.OAuthApi.GetUserTokenAsync(activity.From.Id, ConnectionName, data["state"].ToString());

  // Do stuff with the token here.

}
```
