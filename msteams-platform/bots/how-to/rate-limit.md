---
title: Limitation du débit
description: Limitation du débit et meilleures pratiques dans Microsoft teams
keywords: limitation du débit des robots teams
ms.openlocfilehash: 2e401b59df075688cb6d459a881e6b813f2cf8e6
ms.sourcegitcommit: b3962a7b36f260aef1af9124d14d71ae08b01ac4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/28/2020
ms.locfileid: "47303709"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="b4bc0-104">Optimiser votre robot : limitation du débit et meilleures pratiques dans Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="b4bc0-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="b4bc0-105">En règle générale, votre application doit limiter le nombre de messages qu’elle publie à une conversation individuelle ou à une conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="b4bc0-106">Cela garantit une expérience optimale qui ne paraît pas « assimilation de courrier indésirable » à vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="b4bc0-107">Pour protéger Microsoft teams et ses utilisateurs, les API bot débitent les requêtes entrantes.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="b4bc0-108">Les applications qui dépassent cette limite reçoivent un `HTTP 429 Too Many Requests` État d’erreur.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="b4bc0-109">Toutes les demandes sont soumises à la même stratégie de limitation de débit, y compris l’envoi de messages, les énumérations de canaux et les extractions de la liste.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="b4bc0-110">Étant donné que les valeurs exactes des limites de débit sont sujettes à modification, nous vous recommandons que votre application implémente le comportement d’interruption approprié lors du retour de l’API `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="b4bc0-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="b4bc0-111">Limites de taux de prise en charge</span><span class="sxs-lookup"><span data-stu-id="b4bc0-111">Handling rate limits</span></span>

<span data-ttu-id="b4bc0-112">Lors de l’exécution d’un kit de développement logiciel (SDK) de générateur de robots, vous pouvez gérer `Microsoft.Rest.HttpOperationException` et vérifier le code d’État.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="b4bc0-113">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="b4bc0-113">Best practices</span></span>

<span data-ttu-id="b4bc0-114">En règle générale, vous devez prendre des précautions simples pour éviter de recevoir des `HTTP 429` réponses.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="b4bc0-115">Par exemple, évitez d’envoyer plusieurs demandes à la même conversation personnelle ou de canal.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="b4bc0-116">Au lieu de cela, envisagez le traitement par lots des demandes d’API.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="b4bc0-117">Il est recommandé d’utiliser une interruption exponentielle avec une gigue aléatoire pour gérer 429s.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="b4bc0-118">Cela garantit que plusieurs demandes n’introduisent pas de collisions lors des nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="b4bc0-119">Exemple : détection d’exceptions temporaires</span><span class="sxs-lookup"><span data-stu-id="b4bc0-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="b4bc0-120">Voici un exemple d’utilisation d’une interruption exponentielle via le bloc d’application de traitement des erreurs passager.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="b4bc0-121">Vous pouvez effectuer une interruption et de nouvelles tentatives à l’aide de la [gestion des erreurs passagère](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="b4bc0-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="b4bc0-122">Pour obtenir des instructions sur l’obtention et l’installation du package NuGet, reportez-vous [à la rubrique Ajout du bloc d’application de traitement des erreurs temporaires à votre solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="b4bc0-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="b4bc0-123">*Voir aussi* [gestion des erreurs passagère](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="b4bc0-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="b4bc0-124">Exemple : intervalle</span><span class="sxs-lookup"><span data-stu-id="b4bc0-124">Example: backoff</span></span>

<span data-ttu-id="b4bc0-125">En plus de détecter les limites de débit, vous pouvez également effectuer une interruption exponentielle.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="b4bc0-126">Vous pouvez également effectuer une `System.Action` exécution de méthode à l’aide de la stratégie de nouvelle tentative décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="b4bc0-127">La bibliothèque référencée vous permet également de spécifier un intervalle fixe ou un mécanisme d’interruption linéaire.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="b4bc0-128">Nous vous recommandons de stocker la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="b4bc0-129">Pour plus d’informations, consultez ce guide pratique sur les différents modèles de nouvelle tentative : [modèle de nouvelle tentative](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="b4bc0-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="b4bc0-130">Par nombre de threads par robot</span><span class="sxs-lookup"><span data-stu-id="b4bc0-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="b4bc0-131">Le fractionnement des messages au niveau du service entraînera une augmentation du nombre de demandes par seconde (RPS).</span><span class="sxs-lookup"><span data-stu-id="b4bc0-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="b4bc0-132">Si vous êtes préoccupé par l’approche des limites, vous devez implémenter la stratégie d’interruption décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="b4bc0-133">Les valeurs fournies ci-dessous concernent uniquement l’estimation.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="b4bc0-134">Cette limite contrôle le trafic qu’un bot est autorisé à générer sur une conversation unique.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="b4bc0-135">Une conversation est 1:1 entre le bot et l’utilisateur, un groupe de conversation ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="b4bc0-136">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="b4bc0-136">**Scenario**</span></span> | <span data-ttu-id="b4bc0-137">**Période de temps (sec)**</span><span class="sxs-lookup"><span data-stu-id="b4bc0-137">**Time-period (sec)**</span></span> | <span data-ttu-id="b4bc0-138">**Nombre maximal d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="b4bc0-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4bc0-139">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-139">Send to Conversation</span></span> | <span data-ttu-id="b4bc0-140">1 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-140">1</span></span> | <span data-ttu-id="b4bc0-141">7 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-141">7</span></span> |
| <span data-ttu-id="b4bc0-142">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-142">Send to Conversation</span></span> | <span data-ttu-id="b4bc0-143">2 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-143">2</span></span> | <span data-ttu-id="b4bc0-144">8 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-144">8</span></span> |
| <span data-ttu-id="b4bc0-145">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-145">Send to Conversation</span></span> | <span data-ttu-id="b4bc0-146">0,30</span><span class="sxs-lookup"><span data-stu-id="b4bc0-146">30</span></span> | <span data-ttu-id="b4bc0-147">60</span><span class="sxs-lookup"><span data-stu-id="b4bc0-147">60</span></span> |
| <span data-ttu-id="b4bc0-148">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-148">Send to Conversation</span></span> | <span data-ttu-id="b4bc0-149">3600</span><span class="sxs-lookup"><span data-stu-id="b4bc0-149">3600</span></span> | <span data-ttu-id="b4bc0-150">1800</span><span class="sxs-lookup"><span data-stu-id="b4bc0-150">1800</span></span> |
| <span data-ttu-id="b4bc0-151">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-151">Create Conversation</span></span> | <span data-ttu-id="b4bc0-152">1 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-152">1</span></span> | <span data-ttu-id="b4bc0-153">7 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-153">7</span></span> |
| <span data-ttu-id="b4bc0-154">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-154">Create Conversation</span></span> | <span data-ttu-id="b4bc0-155">2 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-155">2</span></span> | <span data-ttu-id="b4bc0-156">8 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-156">8</span></span> |
| <span data-ttu-id="b4bc0-157">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-157">Create Conversation</span></span> | <span data-ttu-id="b4bc0-158">0,30</span><span class="sxs-lookup"><span data-stu-id="b4bc0-158">30</span></span> | <span data-ttu-id="b4bc0-159">60</span><span class="sxs-lookup"><span data-stu-id="b4bc0-159">60</span></span> |
| <span data-ttu-id="b4bc0-160">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-160">Create Conversation</span></span> | <span data-ttu-id="b4bc0-161">3600</span><span class="sxs-lookup"><span data-stu-id="b4bc0-161">3600</span></span> | <span data-ttu-id="b4bc0-162">1800</span><span class="sxs-lookup"><span data-stu-id="b4bc0-162">1800</span></span> |
| <span data-ttu-id="b4bc0-163">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-163">Get Conversation Members</span></span>| <span data-ttu-id="b4bc0-164">1 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-164">1</span></span> | <span data-ttu-id="b4bc0-165">14 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-165">14</span></span> |
| <span data-ttu-id="b4bc0-166">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-166">Get Conversation Members</span></span>| <span data-ttu-id="b4bc0-167">2 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-167">2</span></span> | <span data-ttu-id="b4bc0-168">16 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-168">16</span></span> |
| <span data-ttu-id="b4bc0-169">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-169">Get Conversation Members</span></span>| <span data-ttu-id="b4bc0-170">0,30</span><span class="sxs-lookup"><span data-stu-id="b4bc0-170">30</span></span> | <span data-ttu-id="b4bc0-171">120</span><span class="sxs-lookup"><span data-stu-id="b4bc0-171">120</span></span> |
| <span data-ttu-id="b4bc0-172">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-172">Get Conversation Members</span></span>| <span data-ttu-id="b4bc0-173">3600</span><span class="sxs-lookup"><span data-stu-id="b4bc0-173">3600</span></span> | <span data-ttu-id="b4bc0-174">3600</span><span class="sxs-lookup"><span data-stu-id="b4bc0-174">3600</span></span> |
| <span data-ttu-id="b4bc0-175">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="b4bc0-175">Get Conversations</span></span> | <span data-ttu-id="b4bc0-176">1 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-176">1</span></span> | <span data-ttu-id="b4bc0-177">14 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-177">14</span></span> |
| <span data-ttu-id="b4bc0-178">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="b4bc0-178">Get Conversations</span></span> | <span data-ttu-id="b4bc0-179">2 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-179">2</span></span> | <span data-ttu-id="b4bc0-180">16 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-180">16</span></span> |
| <span data-ttu-id="b4bc0-181">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="b4bc0-181">Get Conversations</span></span> | <span data-ttu-id="b4bc0-182">0,30</span><span class="sxs-lookup"><span data-stu-id="b4bc0-182">30</span></span> | <span data-ttu-id="b4bc0-183">120</span><span class="sxs-lookup"><span data-stu-id="b4bc0-183">120</span></span> |
| <span data-ttu-id="b4bc0-184">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="b4bc0-184">Get Conversations</span></span> | <span data-ttu-id="b4bc0-185">3600</span><span class="sxs-lookup"><span data-stu-id="b4bc0-185">3600</span></span> | <span data-ttu-id="b4bc0-186">3600</span><span class="sxs-lookup"><span data-stu-id="b4bc0-186">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="b4bc0-187">Limite par thread pour tous les robots</span><span class="sxs-lookup"><span data-stu-id="b4bc0-187">Per thread limit for all bots</span></span>

<span data-ttu-id="b4bc0-188">Cette limite contrôle le trafic que tous les robots sont autorisés à générer au sein d’une conversation unique.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-188">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="b4bc0-189">Une conversation est 1:1 entre le bot et l’utilisateur, un groupe de conversation ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="b4bc0-189">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="b4bc0-190">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="b4bc0-190">**Scenario**</span></span> | <span data-ttu-id="b4bc0-191">**Période de temps (sec)**</span><span class="sxs-lookup"><span data-stu-id="b4bc0-191">**Time-period (sec)**</span></span> | <span data-ttu-id="b4bc0-192">**Nombre maximal d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="b4bc0-192">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4bc0-193">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-193">Send to Conversation</span></span> | <span data-ttu-id="b4bc0-194">1 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-194">1</span></span> | <span data-ttu-id="b4bc0-195">14 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-195">14</span></span> |
| <span data-ttu-id="b4bc0-196">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-196">Send to Conversation</span></span> | <span data-ttu-id="b4bc0-197">2 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-197">2</span></span> | <span data-ttu-id="b4bc0-198">16 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-198">16</span></span> |
| <span data-ttu-id="b4bc0-199">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-199">Create Conversation</span></span> | <span data-ttu-id="b4bc0-200">1 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-200">1</span></span> | <span data-ttu-id="b4bc0-201">14 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-201">14</span></span> |
| <span data-ttu-id="b4bc0-202">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-202">Create Conversation</span></span> | <span data-ttu-id="b4bc0-203">2 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-203">2</span></span> | <span data-ttu-id="b4bc0-204">16 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-204">16</span></span> |
| <span data-ttu-id="b4bc0-205">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-205">CreateConversation</span></span>| <span data-ttu-id="b4bc0-206">1 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-206">1</span></span> | <span data-ttu-id="b4bc0-207">14 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-207">14</span></span> |
| <span data-ttu-id="b4bc0-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-208">CreateConversation</span></span>| <span data-ttu-id="b4bc0-209">2 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-209">2</span></span> | <span data-ttu-id="b4bc0-210">16 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-210">16</span></span> |
| <span data-ttu-id="b4bc0-211">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-211">Get Conversation Members</span></span>| <span data-ttu-id="b4bc0-212">1 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-212">1</span></span> | <span data-ttu-id="b4bc0-213">vingt</span><span class="sxs-lookup"><span data-stu-id="b4bc0-213">28</span></span> |
| <span data-ttu-id="b4bc0-214">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="b4bc0-214">Get Conversation Members</span></span>| <span data-ttu-id="b4bc0-215">2 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-215">2</span></span> | <span data-ttu-id="b4bc0-216">32</span><span class="sxs-lookup"><span data-stu-id="b4bc0-216">32</span></span> |
| <span data-ttu-id="b4bc0-217">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="b4bc0-217">Get Conversations</span></span> | <span data-ttu-id="b4bc0-218">1 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-218">1</span></span> | <span data-ttu-id="b4bc0-219">vingt</span><span class="sxs-lookup"><span data-stu-id="b4bc0-219">28</span></span> |
| <span data-ttu-id="b4bc0-220">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="b4bc0-220">Get Conversations</span></span> | <span data-ttu-id="b4bc0-221">2 </span><span class="sxs-lookup"><span data-stu-id="b4bc0-221">2</span></span> | <span data-ttu-id="b4bc0-222">32</span><span class="sxs-lookup"><span data-stu-id="b4bc0-222">32</span></span> |
