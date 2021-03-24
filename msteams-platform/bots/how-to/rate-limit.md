---
title: Limitation des taux
description: Limitation des taux et meilleures pratiques dans Microsoft Teams
keywords: limitation des taux de bots teams
ms.openlocfilehash: 840737178234bcd6e2da1925b0031083717e2b91
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034682"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a>Optimiser votre bot : limitation des taux et meilleures pratiques dans Microsoft Teams

En règle générale, votre application doit limiter le nombre de messages qu’elle publie à une conversation individuelle ou à une conversation de canal. Cela garantit une expérience optimale qui ne se sent pas « indésirable » pour vos utilisateurs finaux.

Pour protéger Microsoft Teams et ses utilisateurs, les API de bot limitent la fréquence des demandes entrantes. Les applications qui vont au-dessus de cette limite reçoivent un `HTTP 429 Too Many Requests` état d’erreur. Toutes les demandes sont soumises à la même stratégie de limitation de taux, y compris l’envoi de messages, les listes d’éumérations de canaux et les extractions de listes.

Étant donné que les valeurs exactes des limites de taux sont sujettes à modification, nous recommandons à votre application d’implémenter le comportement d’insé backoff approprié lorsque l’API est de `HTTP 429 Too Many Requests` retour.

## <a name="handling-rate-limits"></a>Gestion des limites de taux

Lors de l’émission d’une opération du SDK Bot Builder, vous pouvez gérer et `Microsoft.Rest.HttpOperationException` vérifier le code d’état.

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

## <a name="best-practices"></a>Meilleures pratiques

En règle générale, vous devez prendre des précautions simples pour éviter de recevoir des `HTTP 429` réponses. Par exemple, évitez d’émettre plusieurs demandes à la même conversation personnelle ou de canal. Envisagez plutôt de traitement par lots des demandes d’API.

Il est recommandé d’utiliser un retour exponentiel avec une gigue aléatoire pour gérer les 429. Cela garantit que plusieurs demandes n’introduisent pas de collisions lors des nouvelles tentatives.

## <a name="example-detecting-transient-exceptions"></a>Exemple : détection d’exceptions temporaires

Voici un exemple d’utilisation du blocage exponentiel via le bloc d’applications de gestion des erreurs temporaires.

Vous pouvez effectuer des tentatives de retour et des tentatives à l’aide [de la gestion des erreurs temporaires.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29) Pour obtenir des instructions sur l’obtention et l’installation du package NuGet, voir [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)). *Voir aussi Gestion* [des erreurs temporaires.](/azure/architecture/best-practices/transient-faults)

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

## <a name="example-backoff"></a>Exemple : mise en arrière

En plus de détecter les limites de taux, vous pouvez également effectuer une limitation exponentielle.

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

Vous pouvez également exécuter une méthode `System.Action` avec la stratégie de nouvelle tentative décrite ci-dessus. La bibliothèque référencé vous permet également de spécifier un intervalle fixe ou un mécanisme d’interruption linéaire.

Nous vous recommandons de stocker la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs au moment de l’exécuter.

Pour plus d’informations, consultez ce guide pratique sur différents modèles de nouvelles tentatives : [Modèle de nouvelle tentative.](/azure/architecture/patterns/retry)

## <a name="per-bot-per-thread-limit"></a>Par bot par limite de thread

>[!NOTE]
>Le fractionnement des messages au niveau du service entraîne des demandes par seconde supérieures aux attentes. Si vous êtes préoccupé par l’approche des limites, vous devez implémenter la stratégie de retour à la limite décrite ci-dessus. Les valeurs fournies ci-dessous sont uniquement à des valeurs d’estimation.

Cette limite contrôle le trafic qu’un bot est autorisé à générer sur une seule conversation. Une conversation est en tête à tête entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.

| **Scénario** | **Période de temps (sec)** | **Nombre maximum d’opérations autorisées** |
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
> Les versions `TeamsInfo.getMembers` précédentes et `TeamsInfo.GetMembersAsync` les API sont en cours d’utilisation. Ils sont limitées à 5 demandes par minute et retournent un maximum de 10 000 membres par équipe. Pour mettre à jour votre SDK Bot Framework et le code pour utiliser les derniers points de terminaison de l’API paginée, voir Modifications apportées à l’API bot pour les membres de l’équipe [et de la conversation.](../../resources/team-chat-member-api-changes.md)

## <a name="per-thread-limit-for-all-bots"></a>Limite par thread pour tous les bots

Cette limite contrôle le trafic que tous les bots sont autorisés à générer au sein d’une seule conversation. Une conversation est en tête à tête entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.

| **Scénario** | **Période de temps (sec)** | **Nombre maximum d’opérations autorisées** |
| --- | --- | --- |
| Envoyer à la conversation | 1 | 14  |
| Envoyer à la conversation | 2 | 16  |
| Créer une conversation | 1 | 14  |
| Créer une conversation | 2 | 16  |
| CreateConversation| 1 | 14  |
| CreateConversation| 2 | 16  |
| Obtenir les membres de la conversation| 1 | 28 |
| Obtenir les membres de la conversation| 2 | 32 |
| Obtenir des conversations | 1 | 28 |
| Obtenir des conversations | 2 | 32 |
