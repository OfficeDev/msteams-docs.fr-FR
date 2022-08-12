---
title: Utilisation d’Azure Bot Service pour l’authentification dans Teams
description: Décrit azure Bot Service OAuthCard et comment il est utilisé pour l’authentification
ms.topic: conceptual
localization_priority: Normal
keywords: teams authentication OAuthCard OAuth card Azure Bot Service
ms.openlocfilehash: efe05320fc6a0b03b530349b5498fa29d36b47b6
ms.sourcegitcommit: 69a45722c5c09477bbff3ba1520e6c81d2d2d997
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/11/2022
ms.locfileid: "67312232"
---
# <a name="using-azure-bot-service-for-authentication-in-teams"></a>Utilisation d’Azure Bot Service pour l’authentification dans Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Sans OAuthCard d’Azure Bot Service, il est compliqué d’implémenter l’authentification dans un bot. Il s’agit d’un défi de pile complète qui implique la création d’une expérience web, l’intégration à des fournisseurs OAuth externes, la gestion des jetons et la gestion des appels d’API de serveur à serveur appropriés pour terminer le flux d’authentification en toute sécurité. Cela peut entraîner des expériences maladroites nécessitant l’entrée de « nombres magiques ».

Avec OAuthCard d’Azure Bot Service, il est plus facile pour votre bot Teams de connecter vos utilisateurs et d’accéder à des fournisseurs de données externes. Que vous ayez déjà implémenté l’authentification et que vous souhaitiez basculer vers quelque chose de plus simple, ou si vous souhaitez ajouter l’authentification à votre service de bot pour la première fois, OAuthCard peut faciliter la tâche.

D’autres rubriques de [l’authentification](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) décrivent l’authentification sans utiliser OAuthCard. Par conséquent, si vous souhaitez mieux comprendre l’authentification dans Teams ou si vous ne pouvez pas utiliser OAuthCard, vous pouvez toujours faire référence à ces rubriques.

## <a name="support-for-the-oauthcard"></a>Prise en charge d’OAuthCard

Il existe actuellement des restrictions quant à l’emplacement où vous pouvez utiliser OAuthCard. Cela comprend :

* La carte ne fonctionne pas avec [l’accès invité](/MicrosoftTeams/guest-access).
* Cela ne fonctionnera pas avec [Microsoft Teams gratuit](https://products.office.com/microsoft-teams/free).
* Il ne peut être utilisé que pour l’authentification de bot.
* Il fonctionne uniquement pour les bots inscrits dans azure [Bot Service](https://azure.microsoft.com/services/bot-service/).

## <a name="how-does-the-azure-bot-service-help-me-do-authentication"></a>Comment Azure Bot Service m’aide-t-il à effectuer l’authentification ?

La documentation complète utilisant OAuthCard est disponible dans la rubrique : [Ajouter l’authentification à votre bot via Azure Bot Service](/azure/bot-service/bot-builder-tutorial-authentication?view=azure-bot-service-3.0&preserve-view=true). Notez que cette rubrique se trouve dans l’ensemble de documentation Azure Bot Framework et qu’elle n’est pas spécifique à Teams.

Les sections suivantes expliquent comment utiliser OAuthCard dans Teams.

## <a name="main-benefits-for-teams-developers"></a>Principaux avantages pour les développeurs Teams

OAuthCard facilite l’authentification des manières suivantes :

* Fournit un flux d’authentification web out-of-box : vous n’avez plus besoin d’écrire et d’héberger une page web pour diriger vers des expériences de connexion externes ou fournir une redirection.
* Est transparent pour les utilisateurs finaux : effectuez l’expérience de connexion complète directement dans Teams.
* Inclut une gestion facile des jetons : vous n’avez plus besoin d’implémenter un système de stockage de jetons . Au lieu de cela, le Bot Service s’occupe de la mise en cache des jetons et fournit un mécanisme sécurisé pour extraire ces jetons.
* Est pris en charge par des kits de développement logiciel (SDK) complets : faciles à intégrer et à utiliser à partir de votre service de bot.
* Offre une prise en charge out-of-box pour de nombreux fournisseurs OAuth populaires, tels qu’Azure AD/MSA, Facebook et Google.

## <a name="when-should-i-implement-my-own-solution"></a>Quand dois-je implémenter ma propre solution ?

Étant donné que les jetons d’accès sont des informations sensibles, vous ne souhaiterez peut-être pas les stocker dans un service externe. Dans ce cas, vous pouvez choisir d’implémenter votre propre système de gestion des jetons et votre expérience de connexion dans Teams, comme décrit dans les autres rubriques sur [l’authentification](~/resources/bot-v3/bot-authentication/auth-flow-bot.md) Teams.

## <a name="getting-started-with-oauthcard-in-teams"></a>Bien démarrer avec OAuthCard dans Teams

> [!NOTE]
> Ce guide utilise le Kit de développement logiciel (SDK) Bot Framework v3. Vous trouverez l’implémentation v4 [ici](/azure/bot-service/bot-builder-authentication?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true). Vous devez toujours créer un manifeste et inclure token.botframework.com dans la `validDomains` section, car sinon, le bouton Connexion n’ouvre pas la fenêtre d’authentification. Utilisez le [portail des développeurs](~/concepts/build-and-test/teams-developer-portal.md) pour générer votre manifeste.

Vous devez d’abord configurer votre service de bot Azure pour configurer des fournisseurs d’authentification externes. Pour plus [d’informations, consultez Configuration des fournisseurs d’identité](~/concepts/authentication/configure-identity-provider.md) .

Pour activer l’authentification à l’aide d’Azure Bot Service, vous devez ajouter ces ajouts à votre code :

1. Incluez token.botframework.com dans la `validDomains` section du manifeste de votre application, car Teams incorporera la page de connexion du Bot Service.
2. Récupérez le jeton à partir du Bot Service chaque fois que votre bot doit accéder aux ressources authentifiées. Si aucun jeton n’est disponible, envoyez un message avec un OAuthCard à l’utilisateur qui lui demande de se connecter au service externe.
3. Gérez l’activité de saisie semi-automatique de connexion. Cela garantit que la demande d’authentification et le jeton sont associés à l’utilisateur qui interagit actuellement avec votre bot.
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

S’il n’existe pas de jeton d’accès, votre code envoie ensuite un message avec un OAuthCard à l’utilisateur :

```CSharp
private async Task SendOAuthCardAsync(IDialogContext context, Activity activity)
{
    await context.PostAsync($"To do this, you'll first need to sign in.");

    var reply = await context.Activity.CreateOAuthReplyAsync(_connectionName, _signInMessage, _buttonLabel).ConfigureAwait(false);
    await context.PostAsync(reply);

    context.Wait(WaitForToken);
}
```

Pour gérer l’activité de connexion terminée, vous devez traiter cet appel :

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

Dans votre code de boîte de dialogue, vous pouvez ensuite récupérer le jeton auprès du service d’authentification bot :

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

## <a name="using-oauthcard-with-messaging-extensions"></a>Utilisation d’OAuthCard avec des extensions de messagerie

Vous pouvez également utiliser Azure Bot Service pour connecter des fournisseurs tiers à votre extension de messagerie. Le flux est le même qu’avec un bot, sauf qu’au lieu de retourner une carte OAuthCard, votre service retourne une invite de connexion.

L’extrait de code suivant (C#) montre comment créer la réponse de connexion :

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

Notez que dans l’exemple ci-dessus, vous devez effectuer l’appel directement `GetSignInLinkAsync` sur la `client.OAuthApi` propriété.

Lorsque l’utilisateur termine correctement la séquence de connexion, votre service reçoit une autre requête Invoke contenant la requête utilisateur d’origine, ainsi qu’une chaîne de paramètre d’état contenant le « code magique ». Vous pouvez maintenant extraire le jeton à l’aide de cette chaîne, ainsi que l’ID d’utilisateur et le nom de connexion.

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
