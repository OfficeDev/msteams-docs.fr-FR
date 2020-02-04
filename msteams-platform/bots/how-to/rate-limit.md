---
title: Limitation du débit
description: Limitation du débit et meilleures pratiques dans Microsoft teams
keywords: limitation du débit des robots teams
ms.openlocfilehash: 4e9efab539ec7817d259fd6c149c438ba02e3ce5
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673664"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a>Optimiser votre robot : limitation du débit et meilleures pratiques dans Microsoft teams

En règle générale, votre application doit limiter le nombre de messages qu’elle publie à une conversation individuelle ou à une conversation de canal. Cela garantit une expérience optimale qui ne paraît pas « assimilation de courrier indésirable » à vos utilisateurs finaux.

Pour protéger Microsoft teams et ses utilisateurs, les API bot débitent les requêtes entrantes. Les applications qui dépassent cette limite `HTTP 429 Too Many Requests` reçoivent un état d’erreur. Toutes les demandes sont soumises à la même stratégie de limitation de débit, y compris l’envoi de messages, les énumérations de canaux et les extractions de la liste.

Étant donné que les valeurs exactes des limites de débit sont sujettes à modification, nous vous recommandons que votre application implémente le comportement d’interruption approprié lors du retour `HTTP 429 Too Many Requests`de l’API.

## <a name="handling-rate-limits"></a>Limites de taux de prise en charge

Lors de l’exécution d’un kit de développement logiciel ( `Microsoft.Rest.HttpOperationException` SDK) de générateur de robots, vous pouvez gérer et vérifier le code d’État.

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

En règle générale, vous devez prendre des précautions simples pour `HTTP 429` éviter de recevoir des réponses. Par exemple, évitez d’envoyer plusieurs demandes à la même conversation personnelle ou de canal. Au lieu de cela, envisagez le traitement par lots des demandes d’API.

Il est recommandé d’utiliser une interruption exponentielle avec une gigue aléatoire pour gérer 429s. Cela garantit que plusieurs demandes n’introduisent pas de collisions lors des nouvelles tentatives.

## <a name="example-detecting-transient-exceptions"></a>Exemple : détection d’exceptions temporaires

Voici un exemple d’utilisation d’une interruption exponentielle via le bloc d’application de traitement des erreurs passager.

Vous pouvez effectuer une interruption et de nouvelles tentatives à l’aide de [bibliothèques de traitement des erreurs passagères](/previous-versions/msp-n-p/hh680901(v=pandp.50)). Pour obtenir des instructions sur l’obtention et l’installation du package NuGet, voir [Ajout du bloc d’application de traitement des erreurs temporaires à votre solution](/previous-versions/msp-n-p/hh680891(v=pandp.50)) .

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
{
    // List of error codes to retry on
    List<int> transientErrorStatusCodes = new List<int>() { 429 };

    public bool IsTransient(Exception ex)
    {
        var httpOperationException = ex as HttpOperationException;
        if (httpOperationException != null)
        {
            return httpOperationException.Response != null &&
                    transientErrorStatusCodes.Contains((int) httpOperationException.Response.StatusCode);
        }

        return false;
    }
}
```

## <a name="example-backoff"></a>Exemple : intervalle

En plus de détecter les limites de débit, vous pouvez également effectuer une interruption exponentielle.

```csharp
/**
* The first parameter specifies the number of retries before failing the operation.
* The second parameter specifies the minimum and maximum backoff time respectively.
* The last parameter is used to add a randomized  +/- 20% delta to avoid numerous clients retrying simultaneously.
*/
var exponentialBackoffRetryStrategy = new ExponentialBackoff(3, TimeSpan.FromSeconds(2),
                        TimeSpan.FromSeconds(20), TimeSpan.FromSeconds(1));


// Define the Retry Policy
var retryPolicy = new RetryPolicy(new BotSdkTransientExceptionDetectionStrategy(), fixedIntervalRetryStrategy);

//Execute any bot sdk action
await retryPolicy.ExecuteAsync(() => connector.Conversations.ReplyToActivityAsync((Activity)reply)).ConfigureAwait(false);
```

Vous pouvez également effectuer une `System.Action` exécution de méthode à l’aide de la stratégie de nouvelle tentative décrite ci-dessus. La bibliothèque référencée vous permet également de spécifier un intervalle fixe ou un mécanisme d’interruption linéaire.

Nous vous recommandons de stocker la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs lors de l’exécution.

Pour plus d’informations, consultez ce guide pratique sur les différents modèles de nouvelle tentative : [modèle de nouvelle tentative](/azure/architecture/patterns/retry).

## <a name="per-bot-per-thread-limit"></a>Par nombre de threads par robot

>[!NOTE]
>Le fractionnement des messages au niveau du service entraînera une augmentation du nombre de demandes par seconde (RPS). Si vous êtes préoccupé par l’approche des limites, vous devez implémenter la stratégie d’interruption décrite ci-dessus. Les valeurs fournies ci-dessous concernent uniquement l’estimation.

Cette limite contrôle le trafic qu’un bot est autorisé à générer sur une conversation unique. Une conversation est 1:1 entre le bot et l’utilisateur, un groupe de conversation ou un canal dans une équipe.

| **Scénario** | **Période (s)** | **Nombre maximal d’opérations autorisées** |
| --- | --- | --- |
| NewMessage | 1  | 7  |
| NewMessage | 2  | 8  |
| NewMessage | 0,30 | 60 |
| NewMessage | 3600 | 1800 |
| UpdateMessage | 1  | 7  |
| UpdateMessage | 2  | 8  |
| UpdateMessage | 0,30 | 60 |
| UpdateMessage | 3600 | 1800 |
| NewThread | 1  | 7  |
| NewThread | 2  | 8  |
| NewThread | 0,30 | 60 |
| NewThread | 3600 | 1800 |
| GetThreadMembers | 1  | 14  |
| GetThreadMembers | 2  | 16  |
| GetThreadMembers | 0,30 | 120 |
| GetThreadMembers | 3600 | 3600 |
| GetThread | 1  | 14  |
| GetThread | 2  | 16  |
| GetThread | 0,30 | 120 |
| GetThread | 3600 | 3600 |

## <a name="per-thread-limit-for-all-bots"></a>Limite par thread pour tous les robots

Cette limite contrôle le trafic que tous les robots sont autorisés à générer au sein d’une conversation unique. Une conversation est 1:1 entre le bot et l’utilisateur, un groupe de conversation ou un canal dans une équipe.

| **Scénario** | **Période (s)** | **Nombre maximal d’opérations autorisées** |
| --- | --- | --- |
| NewMessage | 1  | 14  |
| NewMessage | 2  | 16  |
| UpdateMessage | 1  | 14  |
| UpdateMessage | 2  | 16  |
| NewThread | 1  | 14  |
| NewThread | 2  | 16  |
| GetThreadMembers | 1  | vingt |
| GetThreadMembers | 2  | 32 |
| GetThread | 1  | vingt |
| GetThread | 2  | 32 |

## <a name="bot-per-data-center-limit"></a>Fonction de robot par centre de données

Cette limite contrôle le trafic qu’un bot est autorisé à générer sur tous les threads dans un centre de données (sur plusieurs clients).

|**Période (s)** | **Nombre maximal d’opérations autorisées** |
| --- | --- |
| 1  | vingtaine |
| 1800 | 8000 |
| 3600 | 15000 |
