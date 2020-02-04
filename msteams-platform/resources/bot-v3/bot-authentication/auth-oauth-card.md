---
title: Utilisation du service Microsoft Azure bot pour l’authentification dans teams
description: Décrit le OAuthCard du service de robots Azure et son utilisation pour l’authentification
keywords: authentification teams OAuthCard service Azure bot de la carte OAuth
ms.openlocfilehash: 0397c45b39470d97c1158b2681462038de618a39
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673845"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Utilisation du service Microsoft Azure bot pour l’authentification dans teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Sans le OAuthCard du service Azure bot, il est compliqué d’implémenter l’authentification dans un bot. Il s’agit d’un défi de pile complète qui implique la création d’une expérience Web, l’intégration avec des fournisseurs OAuth externes, la gestion des jetons et la gestion des appels d’API de serveur à serveur adéquats pour effectuer un flux d’authentification sécurisé. Cela peut entraîner des expériences dépendantes qui nécessitent l’entrée de « nombres magiques ».

Avec le OAuthCard du service Azure bot, il est plus facile pour votre robot de se connecter à vos utilisateurs et d’accéder aux fournisseurs de données externes. Que vous ayez déjà implémenté l’authentification et que vous souhaitiez passer à un autre résultat plus simple ou si vous souhaitez ajouter une authentification à votre service bot pour la première fois, le OAuthCard peut faciliter la tâche.

Les autres rubriques de [l’authentification](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) décrivent l’authentification sans utiliser l’OAuthCard, donc si vous voulez comprendre l’authentification dans teams plus profondément ou si vous ne pouvez pas utiliser le OAuthCard, vous pouvez toujours consulter ces rubriques.

## <a name="support-for-the-oauthcard"></a>Prise en charge du OAuthCard

Il existe actuellement des restrictions quant à l’emplacement où vous pouvez utiliser le OAuthCard. Cela inclut ce qui suit :

* La carte ne fonctionne pas avec l' [accès invité](/MicrosoftTeams/guest-access)
* Il ne fonctionnera pas avec [Microsoft teams gratuitement](https://products.office.com/microsoft-teams/free)
* Il peut uniquement être utilisé pour l’authentification de robot.
* Elle fonctionne uniquement pour les robots inscrits dans le [service Azure bot](https://azure.microsoft.com/services/bot-service/) .

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Comment le service Azure bot m’aide-t-il à m’authentifier ?

Une documentation complète à l’aide de l’OAuthCard est disponible dans la rubrique : [Add Authentication to your bot by Azure bot service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0). Notez que cette rubrique se trouve dans l’ensemble de la documentation de l’infrastructure Azure bot et n’est pas propre à Teams.

Les sections suivantes indiquent comment utiliser le OAuthCard dans Teams.

## <a name="main-benefits-for-teams-developers"></a>Principaux avantages pour les développeurs de teams

L’OAuthCard aide à l’authentification des manières suivantes :

* Fournit un flux d’authentification Web out-of-Box : vous n’avez plus à écrire et à héberger une page Web pour diriger vers des expériences de connexion externes ou fournir une redirection.
* Est transparent pour les utilisateurs finals : effectuez l’expérience de connexion complète directement dans Teams.
* Inclut une gestion des jetons simplifiée : vous n’avez plus besoin d’implémenter un système de stockage des jetons : le service bot prend en charge la mise en cache des jetons et fournit un mécanisme sécurisé pour l’extraction de ces jetons.
* Est pris en charge par les kits de développement logiciel complets : facile à intégrer et à consommer à partir de votre service bot.
* Dispose de la prise en charge de nombreux fournisseurs OAuth populaires, comme Azure AD/MSA, Facebook et Google.

## <a name="when-should-i-implement-my-own-solution"></a>Quand dois-je implémenter ma propre solution ?

Étant donné que les jetons d’accès sont des informations sensibles, il est possible que vous ne souhaitiez pas les stocker dans un service externe. Dans ce cas, vous pouvez toujours implémenter votre propre système de gestion des jetons et l’expérience de connexion dans Teams, comme décrit dans les autres rubriques relatives à l' [authentification](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) Teams.

## <a name="getting-started-with-oauthcard-in-teams"></a>Prise en main de OAuthCard dans teams

> [!NOTE]
> Ce guide utilise le kit de développement logiciel (SDK) de robot v3. Vous pouvez trouver l’implémentation v4 [ici](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp). Vous devrez tout de même créer un manifeste et inclure token.botframework.com dans la `validDomains` section, car dans le cas contraire, le bouton de connexion n’ouvrira pas la fenêtre d’authentification. Utilisez l' [application Studio](~/concepts/build-and-test/app-studio-overview.md) pour générer votre manifeste.

Vous devez tout d’abord configurer votre service Azure bot pour configurer des fournisseurs d’authentification externes. Pour plus d’informations, consultez la procédure de [Configuration des fournisseurs d’identité](~/concepts/authentication/configure-identity-provider.md) .

Pour activer l’authentification à l’aide du service Azure bot, vous devez effectuer ces ajouts à votre code :

1. Incluez token.botframework.com dans `validDomains` la section du manifeste de votre application car teams intégrera la page de connexion du service bot.
2. Récupérez le jeton du service bot chaque fois que votre bot a besoin d’accéder à des ressources authentifiées. Si aucun jeton n’est disponible, envoyez un message avec un OAuthCard à l’utilisateur pour lui demander de se connecter au service externe.
3. Gérer l’activité de fin de connexion. Cela garantit que la demande d’authentification et le jeton sont associés à l’utilisateur qui interagit actuellement avec votre bot.
4. Récupérez le jeton chaque fois que votre bot doit effectuer des actions authentifiées, telles que l’appel d’API REST externes.

Dans votre code de boîte de dialogue, vous devez ajouter cet extrait de code (C#), qui recherche un jeton d’accès existant :

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

S’il n’existe pas de jeton d’accès, votre code enverra un message avec un OAuthCard à l’utilisateur :

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

Pour gérer l’activité de connexion terminée, vous devez traiter cet appel :

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

Dans votre code de boîte de dialogue, vous pouvez ensuite récupérer le jeton à partir du service d’authentification du robot :

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

## <a name="using-oauthcard-with-messaging-extensions"></a>Utilisation de OAuthCard avec les extensions de messagerie

Vous pouvez également utiliser le service de robot Azure pour connecter des fournisseurs tiers à votre extension de messagerie. Le flux est le même qu’avec un bot, sauf au lieu de renvoyer un OAuthCard, votre service renverra une invite de connexion.

L’extrait de code suivant (C#) illustre comment concevoir la réponse de connexion :

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

Notez que dans l’exemple ci-dessus, vous devez passer l' `GetSignInLinkAsync` appel directement par `client.OAuthApi` rapport à la propriété.

Lorsque l’utilisateur réussit la séquence de connexion, votre service reçoit une autre demande d’appel contenant la requête de l’utilisateur d’origine, ainsi qu’une chaîne de paramètres d’état contenant le « code magique ». Vous pouvez maintenant extraire le jeton à l’aide de cette chaîne, ainsi que l’ID d’utilisateur et le nom de connexion.

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
