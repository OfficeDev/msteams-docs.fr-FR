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
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="4e0f1-104">Optimiser votre robot : limitation du débit et meilleures pratiques dans Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="4e0f1-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="4e0f1-105">En règle générale, votre application doit limiter le nombre de messages qu’elle publie à une conversation individuelle ou à une conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="4e0f1-106">Cela garantit une expérience optimale qui ne paraît pas « assimilation de courrier indésirable » à vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="4e0f1-107">Pour protéger Microsoft teams et ses utilisateurs, les API bot débitent les requêtes entrantes.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="4e0f1-108">Les applications qui dépassent cette limite `HTTP 429 Too Many Requests` reçoivent un état d’erreur.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="4e0f1-109">Toutes les demandes sont soumises à la même stratégie de limitation de débit, y compris l’envoi de messages, les énumérations de canaux et les extractions de la liste.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="4e0f1-110">Étant donné que les valeurs exactes des limites de débit sont sujettes à modification, nous vous recommandons que votre application implémente le comportement d’interruption approprié lors du retour `HTTP 429 Too Many Requests`de l’API.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="4e0f1-111">Limites de taux de prise en charge</span><span class="sxs-lookup"><span data-stu-id="4e0f1-111">Handling rate limits</span></span>

<span data-ttu-id="4e0f1-112">Lors de l’exécution d’un kit de développement logiciel ( `Microsoft.Rest.HttpOperationException` SDK) de générateur de robots, vous pouvez gérer et vérifier le code d’État.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="4e0f1-113">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="4e0f1-113">Best practices</span></span>

<span data-ttu-id="4e0f1-114">En règle générale, vous devez prendre des précautions simples pour `HTTP 429` éviter de recevoir des réponses.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="4e0f1-115">Par exemple, évitez d’envoyer plusieurs demandes à la même conversation personnelle ou de canal.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="4e0f1-116">Au lieu de cela, envisagez le traitement par lots des demandes d’API.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="4e0f1-117">Il est recommandé d’utiliser une interruption exponentielle avec une gigue aléatoire pour gérer 429s.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="4e0f1-118">Cela garantit que plusieurs demandes n’introduisent pas de collisions lors des nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="4e0f1-119">Exemple : détection d’exceptions temporaires</span><span class="sxs-lookup"><span data-stu-id="4e0f1-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="4e0f1-120">Voici un exemple d’utilisation d’une interruption exponentielle via le bloc d’application de traitement des erreurs passager.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="4e0f1-121">Vous pouvez effectuer une interruption et de nouvelles tentatives à l’aide de [bibliothèques de traitement des erreurs passagères](/previous-versions/msp-n-p/hh680901(v=pandp.50)).</span><span class="sxs-lookup"><span data-stu-id="4e0f1-121">You can perform backoff and retries using [Transient Fault Handling libraries](/previous-versions/msp-n-p/hh680901(v=pandp.50)).</span></span> <span data-ttu-id="4e0f1-122">Pour obtenir des instructions sur l’obtention et l’installation du package NuGet, voir [Ajout du bloc d’application de traitement des erreurs temporaires à votre solution](/previous-versions/msp-n-p/hh680891(v=pandp.50)) .</span><span class="sxs-lookup"><span data-stu-id="4e0f1-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/hh680891(v=pandp.50))</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="4e0f1-123">Exemple : intervalle</span><span class="sxs-lookup"><span data-stu-id="4e0f1-123">Example: backoff</span></span>

<span data-ttu-id="4e0f1-124">En plus de détecter les limites de débit, vous pouvez également effectuer une interruption exponentielle.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-124">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="4e0f1-125">Vous pouvez également effectuer une `System.Action` exécution de méthode à l’aide de la stratégie de nouvelle tentative décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-125">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="4e0f1-126">La bibliothèque référencée vous permet également de spécifier un intervalle fixe ou un mécanisme d’interruption linéaire.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-126">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="4e0f1-127">Nous vous recommandons de stocker la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-127">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="4e0f1-128">Pour plus d’informations, consultez ce guide pratique sur les différents modèles de nouvelle tentative : [modèle de nouvelle tentative](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="4e0f1-128">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="4e0f1-129">Par nombre de threads par robot</span><span class="sxs-lookup"><span data-stu-id="4e0f1-129">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="4e0f1-130">Le fractionnement des messages au niveau du service entraînera une augmentation du nombre de demandes par seconde (RPS).</span><span class="sxs-lookup"><span data-stu-id="4e0f1-130">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="4e0f1-131">Si vous êtes préoccupé par l’approche des limites, vous devez implémenter la stratégie d’interruption décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-131">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="4e0f1-132">Les valeurs fournies ci-dessous concernent uniquement l’estimation.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-132">The values provided below are for estimation only.</span></span>

<span data-ttu-id="4e0f1-133">Cette limite contrôle le trafic qu’un bot est autorisé à générer sur une conversation unique.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-133">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="4e0f1-134">Une conversation est 1:1 entre le bot et l’utilisateur, un groupe de conversation ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-134">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="4e0f1-135">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="4e0f1-135">**Scenario**</span></span> | <span data-ttu-id="4e0f1-136">**Période (s)**</span><span class="sxs-lookup"><span data-stu-id="4e0f1-136">**Time-period (sec)**</span></span> | <span data-ttu-id="4e0f1-137">**Nombre maximal d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="4e0f1-137">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e0f1-138">NewMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-138">NewMessage</span></span> | <span data-ttu-id="4e0f1-139">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-139">1</span></span> | <span data-ttu-id="4e0f1-140">7 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-140">7</span></span> |
| <span data-ttu-id="4e0f1-141">NewMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-141">NewMessage</span></span> | <span data-ttu-id="4e0f1-142">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-142">2</span></span> | <span data-ttu-id="4e0f1-143">8 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-143">8</span></span> |
| <span data-ttu-id="4e0f1-144">NewMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-144">NewMessage</span></span> | <span data-ttu-id="4e0f1-145">0,30</span><span class="sxs-lookup"><span data-stu-id="4e0f1-145">30</span></span> | <span data-ttu-id="4e0f1-146">60</span><span class="sxs-lookup"><span data-stu-id="4e0f1-146">60</span></span> |
| <span data-ttu-id="4e0f1-147">NewMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-147">NewMessage</span></span> | <span data-ttu-id="4e0f1-148">3600</span><span class="sxs-lookup"><span data-stu-id="4e0f1-148">3600</span></span> | <span data-ttu-id="4e0f1-149">1800</span><span class="sxs-lookup"><span data-stu-id="4e0f1-149">1800</span></span> |
| <span data-ttu-id="4e0f1-150">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-150">UpdateMessage</span></span> | <span data-ttu-id="4e0f1-151">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-151">1</span></span> | <span data-ttu-id="4e0f1-152">7 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-152">7</span></span> |
| <span data-ttu-id="4e0f1-153">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-153">UpdateMessage</span></span> | <span data-ttu-id="4e0f1-154">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-154">2</span></span> | <span data-ttu-id="4e0f1-155">8 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-155">8</span></span> |
| <span data-ttu-id="4e0f1-156">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-156">UpdateMessage</span></span> | <span data-ttu-id="4e0f1-157">0,30</span><span class="sxs-lookup"><span data-stu-id="4e0f1-157">30</span></span> | <span data-ttu-id="4e0f1-158">60</span><span class="sxs-lookup"><span data-stu-id="4e0f1-158">60</span></span> |
| <span data-ttu-id="4e0f1-159">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-159">UpdateMessage</span></span> | <span data-ttu-id="4e0f1-160">3600</span><span class="sxs-lookup"><span data-stu-id="4e0f1-160">3600</span></span> | <span data-ttu-id="4e0f1-161">1800</span><span class="sxs-lookup"><span data-stu-id="4e0f1-161">1800</span></span> |
| <span data-ttu-id="4e0f1-162">NewThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-162">NewThread</span></span> | <span data-ttu-id="4e0f1-163">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-163">1</span></span> | <span data-ttu-id="4e0f1-164">7 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-164">7</span></span> |
| <span data-ttu-id="4e0f1-165">NewThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-165">NewThread</span></span> | <span data-ttu-id="4e0f1-166">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-166">2</span></span> | <span data-ttu-id="4e0f1-167">8 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-167">8</span></span> |
| <span data-ttu-id="4e0f1-168">NewThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-168">NewThread</span></span> | <span data-ttu-id="4e0f1-169">0,30</span><span class="sxs-lookup"><span data-stu-id="4e0f1-169">30</span></span> | <span data-ttu-id="4e0f1-170">60</span><span class="sxs-lookup"><span data-stu-id="4e0f1-170">60</span></span> |
| <span data-ttu-id="4e0f1-171">NewThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-171">NewThread</span></span> | <span data-ttu-id="4e0f1-172">3600</span><span class="sxs-lookup"><span data-stu-id="4e0f1-172">3600</span></span> | <span data-ttu-id="4e0f1-173">1800</span><span class="sxs-lookup"><span data-stu-id="4e0f1-173">1800</span></span> |
| <span data-ttu-id="4e0f1-174">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="4e0f1-174">GetThreadMembers</span></span> | <span data-ttu-id="4e0f1-175">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-175">1</span></span> | <span data-ttu-id="4e0f1-176">14 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-176">14</span></span> |
| <span data-ttu-id="4e0f1-177">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="4e0f1-177">GetThreadMembers</span></span> | <span data-ttu-id="4e0f1-178">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-178">2</span></span> | <span data-ttu-id="4e0f1-179">16 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-179">16</span></span> |
| <span data-ttu-id="4e0f1-180">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="4e0f1-180">GetThreadMembers</span></span> | <span data-ttu-id="4e0f1-181">0,30</span><span class="sxs-lookup"><span data-stu-id="4e0f1-181">30</span></span> | <span data-ttu-id="4e0f1-182">120</span><span class="sxs-lookup"><span data-stu-id="4e0f1-182">120</span></span> |
| <span data-ttu-id="4e0f1-183">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="4e0f1-183">GetThreadMembers</span></span> | <span data-ttu-id="4e0f1-184">3600</span><span class="sxs-lookup"><span data-stu-id="4e0f1-184">3600</span></span> | <span data-ttu-id="4e0f1-185">3600</span><span class="sxs-lookup"><span data-stu-id="4e0f1-185">3600</span></span> |
| <span data-ttu-id="4e0f1-186">GetThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-186">GetThread</span></span> | <span data-ttu-id="4e0f1-187">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-187">1</span></span> | <span data-ttu-id="4e0f1-188">14 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-188">14</span></span> |
| <span data-ttu-id="4e0f1-189">GetThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-189">GetThread</span></span> | <span data-ttu-id="4e0f1-190">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-190">2</span></span> | <span data-ttu-id="4e0f1-191">16 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-191">16</span></span> |
| <span data-ttu-id="4e0f1-192">GetThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-192">GetThread</span></span> | <span data-ttu-id="4e0f1-193">0,30</span><span class="sxs-lookup"><span data-stu-id="4e0f1-193">30</span></span> | <span data-ttu-id="4e0f1-194">120</span><span class="sxs-lookup"><span data-stu-id="4e0f1-194">120</span></span> |
| <span data-ttu-id="4e0f1-195">GetThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-195">GetThread</span></span> | <span data-ttu-id="4e0f1-196">3600</span><span class="sxs-lookup"><span data-stu-id="4e0f1-196">3600</span></span> | <span data-ttu-id="4e0f1-197">3600</span><span class="sxs-lookup"><span data-stu-id="4e0f1-197">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="4e0f1-198">Limite par thread pour tous les robots</span><span class="sxs-lookup"><span data-stu-id="4e0f1-198">Per thread limit for all bots</span></span>

<span data-ttu-id="4e0f1-199">Cette limite contrôle le trafic que tous les robots sont autorisés à générer au sein d’une conversation unique.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-199">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="4e0f1-200">Une conversation est 1:1 entre le bot et l’utilisateur, un groupe de conversation ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="4e0f1-200">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="4e0f1-201">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="4e0f1-201">**Scenario**</span></span> | <span data-ttu-id="4e0f1-202">**Période (s)**</span><span class="sxs-lookup"><span data-stu-id="4e0f1-202">**Time-period (sec)**</span></span> | <span data-ttu-id="4e0f1-203">**Nombre maximal d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="4e0f1-203">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e0f1-204">NewMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-204">NewMessage</span></span> | <span data-ttu-id="4e0f1-205">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-205">1</span></span> | <span data-ttu-id="4e0f1-206">14 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-206">14</span></span> |
| <span data-ttu-id="4e0f1-207">NewMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-207">NewMessage</span></span> | <span data-ttu-id="4e0f1-208">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-208">2</span></span> | <span data-ttu-id="4e0f1-209">16 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-209">16</span></span> |
| <span data-ttu-id="4e0f1-210">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-210">UpdateMessage</span></span> | <span data-ttu-id="4e0f1-211">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-211">1</span></span> | <span data-ttu-id="4e0f1-212">14 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-212">14</span></span> |
| <span data-ttu-id="4e0f1-213">UpdateMessage</span><span class="sxs-lookup"><span data-stu-id="4e0f1-213">UpdateMessage</span></span> | <span data-ttu-id="4e0f1-214">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-214">2</span></span> | <span data-ttu-id="4e0f1-215">16 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-215">16</span></span> |
| <span data-ttu-id="4e0f1-216">NewThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-216">NewThread</span></span> | <span data-ttu-id="4e0f1-217">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-217">1</span></span> | <span data-ttu-id="4e0f1-218">14 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-218">14</span></span> |
| <span data-ttu-id="4e0f1-219">NewThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-219">NewThread</span></span> | <span data-ttu-id="4e0f1-220">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-220">2</span></span> | <span data-ttu-id="4e0f1-221">16 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-221">16</span></span> |
| <span data-ttu-id="4e0f1-222">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="4e0f1-222">GetThreadMembers</span></span> | <span data-ttu-id="4e0f1-223">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-223">1</span></span> | <span data-ttu-id="4e0f1-224">vingt</span><span class="sxs-lookup"><span data-stu-id="4e0f1-224">28</span></span> |
| <span data-ttu-id="4e0f1-225">GetThreadMembers</span><span class="sxs-lookup"><span data-stu-id="4e0f1-225">GetThreadMembers</span></span> | <span data-ttu-id="4e0f1-226">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-226">2</span></span> | <span data-ttu-id="4e0f1-227">32</span><span class="sxs-lookup"><span data-stu-id="4e0f1-227">32</span></span> |
| <span data-ttu-id="4e0f1-228">GetThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-228">GetThread</span></span> | <span data-ttu-id="4e0f1-229">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-229">1</span></span> | <span data-ttu-id="4e0f1-230">vingt</span><span class="sxs-lookup"><span data-stu-id="4e0f1-230">28</span></span> |
| <span data-ttu-id="4e0f1-231">GetThread</span><span class="sxs-lookup"><span data-stu-id="4e0f1-231">GetThread</span></span> | <span data-ttu-id="4e0f1-232">2 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-232">2</span></span> | <span data-ttu-id="4e0f1-233">32</span><span class="sxs-lookup"><span data-stu-id="4e0f1-233">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="4e0f1-234">Fonction de robot par centre de données</span><span class="sxs-lookup"><span data-stu-id="4e0f1-234">Bot per data center limit</span></span>

<span data-ttu-id="4e0f1-235">Cette limite contrôle le trafic qu’un bot est autorisé à générer sur tous les threads dans un centre de données (sur plusieurs clients).</span><span class="sxs-lookup"><span data-stu-id="4e0f1-235">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="4e0f1-236">**Période (s)**</span><span class="sxs-lookup"><span data-stu-id="4e0f1-236">**Time-period (sec)**</span></span> | <span data-ttu-id="4e0f1-237">**Nombre maximal d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="4e0f1-237">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="4e0f1-238">1 </span><span class="sxs-lookup"><span data-stu-id="4e0f1-238">1</span></span> | <span data-ttu-id="4e0f1-239">vingtaine</span><span class="sxs-lookup"><span data-stu-id="4e0f1-239">20</span></span> |
| <span data-ttu-id="4e0f1-240">1800</span><span class="sxs-lookup"><span data-stu-id="4e0f1-240">1800</span></span> | <span data-ttu-id="4e0f1-241">8000</span><span class="sxs-lookup"><span data-stu-id="4e0f1-241">8000</span></span> |
| <span data-ttu-id="4e0f1-242">3600</span><span class="sxs-lookup"><span data-stu-id="4e0f1-242">3600</span></span> | <span data-ttu-id="4e0f1-243">15000</span><span class="sxs-lookup"><span data-stu-id="4e0f1-243">15000</span></span> |
