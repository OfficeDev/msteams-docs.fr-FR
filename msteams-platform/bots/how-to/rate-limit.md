---
title: Optimisez votre robot grâce à la limitation du débit dans Teams
description: En savoir plus sur la gestion de la limite de débit pour les bots avec une limite par bot par thread et par limite pour tous les bots à l’aide d’exemples de code. En outre, découvrez les meilleures pratiques en matière de limitation du débit dans Microsoft Teams.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: limitation du taux de bots teams
ms.openlocfilehash: a864970bd837ef4af3ccebe0b09ca4d38ac7b76b
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757149"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a>Optimisez votre robot grâce à la limitation du débit dans Teams

La limitation du débit est une méthode permettant de limiter les messages à une certaine fréquence maximale. En règle générale, votre application doit limiter le nombre de messages qu’elle publie dans une conversation ou une conversation de canal individuelle. Cela garantit une expérience optimale et les messages n’apparaissent pas comme du courrier indésirable pour vos utilisateurs.

Pour protéger Microsoft Teams et ses utilisateurs, les API de bot fournissent une limite de débit pour les demandes entrantes. Les applications qui dépassent cette limite reçoivent un état d’erreur `HTTP 429 Too Many Requests`. Toutes les demandes sont soumises à la même stratégie de limitation de débit, y compris l’envoi de messages, d’énumérations de canaux et d’extractions de listes.

Étant donné que les valeurs exactes des limites de débit sont susceptibles d’être modifiées, votre application doit implémenter le comportement d’interruption approprié lorsque l’API retourne `HTTP 429 Too Many Requests`.

## <a name="handle-rate-limits"></a>Gérer les limites de débit

Lors de l’émission d’une opération Bot Builder SDK, vous pouvez gérer `Microsoft.Rest.HttpOperationException` et vérifier le code d’état.

Le code suivant montre un exemple de limites de débit de gestion :

```csharp
try
{
    // Perform Bot Framework operation
    // for example, await connector.Conversations.UpdateActivityAsync(reply);
}
catch (HttpOperationException ex)
{
    if (ex.Response != null && (uint)ex.Response.StatusCode ==  429)
    {
        //Perform retry of the above operation/Action method
    }
}
```

Après avoir géré les limites de débit pour les bots, vous pouvez gérer `HTTP 429` réponses à l’aide d’un backoff exponentiel.

## <a name="handle-http-429-responses"></a>Gérer `HTTP 429` réponses

En général, vous devez prendre des précautions simples pour éviter de recevoir `HTTP 429` réponses. Par exemple, évitez d’émettre plusieurs demandes à la même conversation personnelle ou de canal. Au lieu de cela, créez un lot de demandes d’API.

L’utilisation d’un backoff exponentiel avec une instabilité aléatoire est la méthode recommandée pour gérer les 429. Cela garantit que plusieurs demandes n’introduisent pas de collisions lors des nouvelles tentatives.

Après avoir traité `HTTP 429` réponses, vous pouvez passer en revue l’exemple pour détecter les exceptions temporaires.

> [!NOTE]
> En plus de réessayer le code d’erreur **429**, les codes d’erreur **412**, **502** et **504** doivent également être retentés.

## <a name="detect-transient-exceptions-example"></a>Exemple de détection d’exceptions temporaires

Le code suivant montre un exemple d’utilisation du backoff exponentiel à l’aide du bloc d’application de gestion des erreurs temporaires :

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
    {
        // List of error codes to retry on
        List<int> transientErrorStatusCodes = new List<int>() { 429 };

        public static bool IsTransient(Exception ex)
          {
              if (ex.Message.Contains("429"))
                  return true;

              HttpResponseMessageWrapper? response = null;
              if (ex is HttpOperationException httpOperationException)
              {
                  response = httpOperationException.Response;
              }
              else
              if (ex is ErrorResponseException errorResponseException)
              {
                  response = errorResponseException.Response;
              }
              return response != null && transientErrorStatusCodes.Contains((int)response.StatusCode);
          }
    }
```

Vous pouvez effectuer des backoffs et des nouvelles tentatives à l’aide de [gestion des erreurs temporaires](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29). Pour obtenir des instructions sur l’obtention et l’installation du package NuGet, consultez [ajouter le bloc d’application de gestion des erreurs temporaires à votre solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN). Consultez également de [gestion des erreurs temporaires](/azure/architecture/best-practices/transient-faults).

Une fois que vous avez passé en revue l’exemple de détection des exceptions temporaires, passez par l’exemple de backoff exponentiel. Vous pouvez utiliser le backoff exponentiel au lieu de réessayer en cas d’échec.

## <a name="backoff-example"></a>Exemple d’interruption

En plus de détecter les limites de débit, vous pouvez également effectuer un backoff exponentiel.

Le code suivant montre un exemple de backoff exponentiel :

```csharp
/**
* The first parameter specifies the number of retries before failing the operation.
* The second parameter specifies the minimum and maximum backoff time respectively.
* The last parameter is used to add a randomized  +/- 20% delta to avoid numerous clients retrying simultaneously.
*/
var exponentialBackoffRetryStrategy = new ExponentialBackoff(3, TimeSpan.FromSeconds(2),
                        TimeSpan.FromSeconds(20), TimeSpan.FromSeconds(1));


// Define the Retry Policy
var retryPolicy = new RetryPolicy(new BotSdkTransientExceptionDetectionStrategy(), exponentialBackoffRetryStrategy);

//Execute any bot sdk action
await retryPolicy.ExecuteAsync(() => connector.Conversations.ReplyToActivityAsync( (Activity)reply) ).ConfigureAwait(false);
```

Vous pouvez également exécuter une méthode `System.Action` avec la stratégie de nouvelle tentative décrite dans cette section. La bibliothèque référencée vous permet également de spécifier un intervalle fixe ou un mécanisme de backoff linéaire.

Stockez la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs au moment de l’exécution.

Pour plus d’informations, consultez [modèles de nouvelles tentatives](/azure/architecture/patterns/retry).

Vous pouvez également gérer la limite de débit à l’aide de la limite par bot par thread.

## <a name="per-bot-per-thread-limit"></a>Limite par bot par thread

La limite par bot par thread contrôle le trafic qu’un bot est autorisé à générer dans une conversation unique. Une conversation est 1:1 entre le bot et l’utilisateur, une conversation de groupe ou un canal dans une équipe. Par conséquent, si l’application envoie un message de bot à chaque utilisateur, la limite de threads n’est pas limitée.

>[!NOTE]
>
> * La limite de threads de 3 600 secondes et de 1 800 opérations s’applique uniquement si plusieurs messages de bot sont envoyés à un seul utilisateur.
> * La limite globale par application et par locataire est de 50 demandes par seconde (RPS). Par conséquent, le nombre total de messages de bot par seconde ne doit pas dépasser la limite de threads.
> * Le fractionnement des messages au niveau du service entraîne un RPS plus élevé que prévu. Si vous craignez de vous approcher des limites, vous devez mettre en œuvre la [stratégie de backoff](#backoff-example). Les valeurs fournies dans cette section sont uniquement à des fins d’estimation.

Le tableau suivant fournit les limites par bot par thread :

| Scénario | Période en secondes | Nombre maximal d’opérations autorisées |
| --- | --- | --- |
| Envoyer à la conversation | 1 | 7  |
| Envoyer à la conversation | 2 | 8  |
| Envoyer à la conversation | 30 | 60 |
| Envoyer à la conversation | 3600 | 1800 |
| Créer une conversation | 1 | 7  |
| Créer une conversation | 2 | 8  |
| Créer une conversation | 30 | 60 |
| Créer une conversation | 3600 | 1800 |
| Obtenir les membres de la conversation| 1 | 14 |
| Obtenir les membres de la conversation| 2 | 16 |
| Obtenir les membres de la conversation| 30 | 120 |
| Obtenir les membres de la conversation| 3600 | 3600 |
| Obtenir des conversations | 1 | 14 |
| Obtenir des conversations | 2 | 16 |
| Obtenir des conversations | 30 | 120 |
| Obtenir des conversations | 3600 | 3600 |

>[!NOTE]
> Les versions précédentes de `TeamsInfo.getMembers` et `TeamsInfo.GetMembersAsync` API sont dépréciées. Ils sont limités à cinq demandes par minute et retournent un maximum de 10 000 membres par équipe. Pour mettre à jour votre kit de développement logiciel (SDK) Bot Framework et le code afin d’utiliser les derniers points de terminaison d’API paginés, consultez [modifications de l’API bot pour les membres d’équipe et de conversation](../../resources/team-chat-member-api-changes.md).

Vous pouvez également gérer la limite de débit à l’aide de la limite par thread pour tous les bots.

## <a name="per-thread-limit-for-all-bots"></a>Limite par thread pour tous les bots

La limite par thread pour tous les bots contrôle le trafic que tous les bots sont autorisés à générer au sein d’une conversation unique. Conversation 1:1 entre le bot et l’utilisateur, une conversation de groupe ou un canal dans une équipe.

Le tableau suivant fournit la limite par thread pour tous les bots :

| Scénario | Période en secondes | Nombre maximal d’opérations autorisées |
| --- | --- | --- |
| Envoyer à la conversation | 1 | 14 |
| Envoyer à la conversation | 2 | 16 |
| Créer une conversation | 1 | 14 |
| Créer une conversation | 2 | 16 |
| Créer une conversation| 1 | 14 |
| Créer une conversation| 2 | 16 |
| Obtenir les membres de la conversation| 1 | 28 |
| Obtenir les membres de la conversation| 2 | 32 |
| Obtenir des conversations | 1 | 28 |
| Obtenir des conversations | 2 | 32 |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Bots d’appels et réunions](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)
