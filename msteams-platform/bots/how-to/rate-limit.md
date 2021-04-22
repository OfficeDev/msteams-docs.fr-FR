---
title: Optimisez votre robot grâce à la limitation du débit dans Teams
description: Limitation des taux et meilleures pratiques dans Microsoft Teams
ms.topic: conceptual
keywords: Limitation des taux de bots teams
ms.openlocfilehash: 690d09e4a3b611c024f32d3776ca73e42d63ee7f
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922502"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a>Optimisez votre robot grâce à la limitation du débit dans Teams

La limitation des taux est une méthode pour limiter les messages à une certaine fréquence maximale. En règle générale, votre application doit limiter le nombre de messages qu'elle publie à une conversation individuelle ou à une conversation de canal. Cela garantit une expérience optimale et les messages n'apparaissent pas comme courrier indésirable pour vos utilisateurs.

Pour protéger Microsoft Teams et ses utilisateurs, les API de bot fournissent une limite de taux pour les demandes entrantes. Les applications qui vont au-dessus de cette limite reçoivent un `HTTP 429 Too Many Requests` état d'erreur. Toutes les demandes sont soumises à la même stratégie de limitation des taux, y compris l'envoi de messages, les listes de canaux et les extractions de listes.

Comme les valeurs exactes des limites de taux sont sujettes à modification, votre application doit implémenter le comportement d'insé backoff approprié lorsque l'API renvoie `HTTP 429 Too Many Requests` .

## <a name="handle-rate-limits"></a>Gérer les limites de taux

Lors de l'émission d'une opération du SDK Bot Builder, vous pouvez gérer et `Microsoft.Rest.HttpOperationException` vérifier le code d'état.

Le code suivant illustre un exemple de gestion des limites de taux :

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

Une fois que vous avez géré les limites de taux pour les bots, vous pouvez gérer les réponses à l'aide `HTTP 429` d'un retour exponentiel.

## <a name="handle-http-429-responses"></a>Gérer les `HTTP 429` réponses

En règle générale, vous devez prendre des précautions simples pour éviter de recevoir des `HTTP 429` réponses. Par exemple, évitez d'émettre plusieurs demandes à la même conversation personnelle ou de canal. Créez plutôt un lot de demandes d'API.

Il est recommandé d'utiliser un retour exponentiel avec une gigue aléatoire pour gérer les 429. Cela garantit que plusieurs demandes n'introduisent pas de collisions lors des nouvelles tentatives.

Une fois que vous `HTTP 429` avez géré les réponses, vous pouvez passer par l'exemple pour détecter les exceptions temporaires.

## <a name="detect-transient-exceptions-example"></a>Exemple de détection d'exceptions temporaires

Le code suivant illustre un exemple d'utilisation du blocage exponentiel à l'aide du bloc d'application de gestion des pannes temporaires :

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
    {
        // List of error codes to retry on
        List<int> transientErrorStatusCodes = new List<int>() { 429 };

        public bool IsTransient(Exception ex)
        {
            if (ex.Message.Contains("429"))
                return true;

            var httpOperationException = ex as HttpOperationException;
            if (httpOperationException != null)
            {
                return httpOperationException.Response != null &&
                        transientErrorStatusCodes.Contains((int)httpOperationException.Response.StatusCode);
            }

            return false;
        }
    }
```

Vous pouvez effectuer des tentatives de retour et des tentatives à l'aide de [la gestion des erreurs temporaires.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29) Pour obtenir des instructions sur l'obtention et l'installation du package NuGet, voir l'ajout du bloc d'application de gestion des erreurs [temporaires à votre solution.](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN) Voir aussi [la gestion des erreurs temporaires.](/azure/architecture/best-practices/transient-faults)

Après avoir passé en détail l'exemple de détection des exceptions temporaires, prenons l'exemple de la fonction de retour exponentiel. Vous pouvez utiliser l'arrêt exponentiel au lieu de réessayer en cas d'échec.

## <a name="backoff-example"></a>Exemple de mise en arrière

En plus de détecter les limites de taux, vous pouvez également effectuer une coupure exponentielle.

Le code suivant illustre un exemple de coupure exponentielle :

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

Vous pouvez également exécuter une méthode `System.Action` avec la stratégie de nouvelle tentative décrite dans cette section. La bibliothèque référencé vous permet également de spécifier un intervalle fixe ou un mécanisme d'interruption linéaire.

Stockez la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs au moment de l'exécuter.

Pour plus d'informations, [voir les modèles de nouvelle tentative.](/azure/architecture/patterns/retry)

Vous pouvez également gérer la limite de taux à l'aide de la limite par bot par thread.

## <a name="per-bot-per-thread-limit"></a>Par bot par limite de thread

La limite par bot par thread contrôle le trafic qu'un bot est autorisé à générer dans une seule conversation. Une conversation est 1:1 entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe. Ainsi, si l'application envoie un message bot à chaque utilisateur, la limite de thread ne se limite pas.

>[!NOTE]
> * La limite de thread de 3 600 secondes et 1 800 opérations s'applique uniquement si plusieurs messages de bot sont envoyés à un seul utilisateur. 
> * La limite globale par application et par client est de 30 demandes par seconde (DEMANDES/s). Par conséquent, le nombre total de messages de bot par seconde ne doit pas franchir la limite de thread.
> * Le fractionnement des messages au niveau du service entraîne un nombre de rps supérieur aux attentes. Si vous êtes préoccupé par l'approche des limites, vous devez implémenter la stratégie [de retour à la limite.](#backoff-example) Les valeurs fournies dans cette section sont uniquement à des valeurs d'estimation.

Le tableau suivant fournit les limites par bot par thread :

| Scénario | Période en secondes | Nombre maximal d'opérations autorisées |
| --- | --- | --- |
| Envoyer à la conversation | 1 | 7  |
| Envoyer à la conversation | 2 | 8  |
| Envoyer à la conversation | 30 | 60 |
| Envoyer à la conversation | 3600 | 1800 |
| Créer une conversation | 1 | 7  |
| Créer une conversation | 2 | 8  |
| Créer une conversation | 30 | 60 |
| Créer une conversation | 3600 | 1800 |
| Obtenir les membres de la conversation| 1 | 14  |
| Obtenir les membres de la conversation| 2 | 16  |
| Obtenir les membres de la conversation| 30 | 120 |
| Obtenir les membres de la conversation| 3600 | 3600 |
| Obtenir des conversations | 1 | 14  |
| Obtenir des conversations | 2 | 16  |
| Obtenir des conversations | 30 | 120 |
| Obtenir des conversations | 3600 | 3600 |

>[!NOTE]
> Les versions précédentes et les API sont `TeamsInfo.getMembers` en cours `TeamsInfo.GetMembersAsync` d'utilisation. Ils sont limitées à cinq demandes par minute et retournent un maximum de 10 000 membres par équipe. Pour mettre à jour votre SDK Bot Framework et le code pour utiliser les derniers points de terminaison de l'API paginée, voir Modifications apportées à l'API bot pour les membres d'équipe et [de conversation.](../../resources/team-chat-member-api-changes.md)

Vous pouvez également gérer la limite de taux à l'aide de la limite par thread pour tous les bots.

## <a name="per-thread-limit-for-all-bots"></a>Limite par thread pour tous les bots

La limite par thread pour tous les bots contrôle le trafic que tous les bots sont autorisés à générer au sein d'une conversation unique. Une conversation est en tête à tête entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.

Le tableau suivant fournit la limite par thread pour tous les bots :

| Scénario | Période en secondes | Nombre maximal d'opérations autorisées |
| --- | --- | --- |
| Envoyer à la conversation | 1 | 14  |
| Envoyer à la conversation | 2 | 16  |
| Créer une conversation | 1 | 14  |
| Créer une conversation | 2 | 16  |
| Créer une conversation| 1 | 14  |
| Créer une conversation| 2 | 16  |
| Obtenir les membres de la conversation| 1 | 28 |
| Obtenir les membres de la conversation| 2 | 32 |
| Obtenir des conversations | 1 | 28 |
| Obtenir des conversations | 2 | 32 |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Appels et réunions robots](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

