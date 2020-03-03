---
title: Limitation du débit
description: Limitation du débit et meilleures pratiques dans Microsoft teams
keywords: limitation du débit des robots teams
ms.openlocfilehash: 145f65a7e17b833e11631dfc219d9f5732f43bc6
ms.sourcegitcommit: 6c692734a382865531a83b9ebd6f604212f484fc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "42371764"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="39ddd-104">Optimiser votre robot : limitation du débit et meilleures pratiques dans Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="39ddd-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="39ddd-105">En règle générale, votre application doit limiter le nombre de messages qu’elle publie à une conversation individuelle ou à une conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="39ddd-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="39ddd-106">Cela garantit une expérience optimale qui ne paraît pas « assimilation de courrier indésirable » à vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="39ddd-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="39ddd-107">Pour protéger Microsoft teams et ses utilisateurs, les API bot débitent les requêtes entrantes.</span><span class="sxs-lookup"><span data-stu-id="39ddd-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="39ddd-108">Les applications qui dépassent cette limite `HTTP 429 Too Many Requests` reçoivent un état d’erreur.</span><span class="sxs-lookup"><span data-stu-id="39ddd-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="39ddd-109">Toutes les demandes sont soumises à la même stratégie de limitation de débit, y compris l’envoi de messages, les énumérations de canaux et les extractions de la liste.</span><span class="sxs-lookup"><span data-stu-id="39ddd-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="39ddd-110">Étant donné que les valeurs exactes des limites de débit sont sujettes à modification, nous vous recommandons que votre application implémente le comportement d’interruption approprié lors du retour `HTTP 429 Too Many Requests`de l’API.</span><span class="sxs-lookup"><span data-stu-id="39ddd-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="39ddd-111">Limites de taux de prise en charge</span><span class="sxs-lookup"><span data-stu-id="39ddd-111">Handling rate limits</span></span>

<span data-ttu-id="39ddd-112">Lors de l’exécution d’un kit de développement logiciel ( `Microsoft.Rest.HttpOperationException` SDK) de générateur de robots, vous pouvez gérer et vérifier le code d’État.</span><span class="sxs-lookup"><span data-stu-id="39ddd-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="39ddd-113">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="39ddd-113">Best practices</span></span>

<span data-ttu-id="39ddd-114">En règle générale, vous devez prendre des précautions simples pour `HTTP 429` éviter de recevoir des réponses.</span><span class="sxs-lookup"><span data-stu-id="39ddd-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="39ddd-115">Par exemple, évitez d’envoyer plusieurs demandes à la même conversation personnelle ou de canal.</span><span class="sxs-lookup"><span data-stu-id="39ddd-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="39ddd-116">Au lieu de cela, envisagez le traitement par lots des demandes d’API.</span><span class="sxs-lookup"><span data-stu-id="39ddd-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="39ddd-117">Il est recommandé d’utiliser une interruption exponentielle avec une gigue aléatoire pour gérer 429s.</span><span class="sxs-lookup"><span data-stu-id="39ddd-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="39ddd-118">Cela garantit que plusieurs demandes n’introduisent pas de collisions lors des nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="39ddd-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="39ddd-119">Exemple : détection d’exceptions temporaires</span><span class="sxs-lookup"><span data-stu-id="39ddd-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="39ddd-120">Voici un exemple d’utilisation d’une interruption exponentielle via le bloc d’application de traitement des erreurs passager.</span><span class="sxs-lookup"><span data-stu-id="39ddd-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="39ddd-121">Vous pouvez effectuer une interruption et de nouvelles tentatives à l’aide de la [gestion des erreurs passagère](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="39ddd-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="39ddd-122">Pour obtenir des instructions sur l’obtention et l’installation du package NuGet, reportez-vous [à la rubrique Ajout du bloc d’application de traitement des erreurs temporaires à votre solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="39ddd-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="39ddd-123">*Voir aussi* [gestion des erreurs passagère](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="39ddd-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="39ddd-124">Exemple : intervalle</span><span class="sxs-lookup"><span data-stu-id="39ddd-124">Example: backoff</span></span>

<span data-ttu-id="39ddd-125">En plus de détecter les limites de débit, vous pouvez également effectuer une interruption exponentielle.</span><span class="sxs-lookup"><span data-stu-id="39ddd-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="39ddd-126">Vous pouvez également effectuer une `System.Action` exécution de méthode à l’aide de la stratégie de nouvelle tentative décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="39ddd-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="39ddd-127">La bibliothèque référencée vous permet également de spécifier un intervalle fixe ou un mécanisme d’interruption linéaire.</span><span class="sxs-lookup"><span data-stu-id="39ddd-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="39ddd-128">Nous vous recommandons de stocker la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="39ddd-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="39ddd-129">Pour plus d’informations, consultez ce guide pratique sur les différents modèles de nouvelle tentative : [modèle de nouvelle tentative](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="39ddd-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="39ddd-130">Par nombre de threads par robot</span><span class="sxs-lookup"><span data-stu-id="39ddd-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="39ddd-131">Le fractionnement des messages au niveau du service entraînera une augmentation du nombre de demandes par seconde (RPS).</span><span class="sxs-lookup"><span data-stu-id="39ddd-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="39ddd-132">Si vous êtes préoccupé par l’approche des limites, vous devez implémenter la stratégie d’interruption décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="39ddd-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="39ddd-133">Les valeurs fournies ci-dessous concernent uniquement l’estimation.</span><span class="sxs-lookup"><span data-stu-id="39ddd-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="39ddd-134">Cette limite contrôle le trafic qu’un bot est autorisé à générer sur une conversation unique.</span><span class="sxs-lookup"><span data-stu-id="39ddd-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="39ddd-135">Une conversation est 1:1 entre le bot et l’utilisateur, un groupe de conversation ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="39ddd-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="39ddd-136">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="39ddd-136">**Scenario**</span></span> | <span data-ttu-id="39ddd-137">**Période de temps (sec)**</span><span class="sxs-lookup"><span data-stu-id="39ddd-137">**Time-period (sec)**</span></span> | <span data-ttu-id="39ddd-138">**Nombre maximal d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="39ddd-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
|| <span data-ttu-id="39ddd-139">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-139">1</span></span> | <span data-ttu-id="39ddd-140">7j/7</span><span class="sxs-lookup"><span data-stu-id="39ddd-140">7</span></span> |
| <span data-ttu-id="39ddd-141">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-141">Send to Conversation</span></span> | <span data-ttu-id="39ddd-142">n°2</span><span class="sxs-lookup"><span data-stu-id="39ddd-142">2</span></span> | <span data-ttu-id="39ddd-143">8bits</span><span class="sxs-lookup"><span data-stu-id="39ddd-143">8</span></span> |
| <span data-ttu-id="39ddd-144">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-144">Send to Conversation</span></span> | <span data-ttu-id="39ddd-145">0,30</span><span class="sxs-lookup"><span data-stu-id="39ddd-145">30</span></span> | <span data-ttu-id="39ddd-146">60</span><span class="sxs-lookup"><span data-stu-id="39ddd-146">60</span></span> |
| <span data-ttu-id="39ddd-147">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-147">Send to Conversation</span></span> | <span data-ttu-id="39ddd-148">3600</span><span class="sxs-lookup"><span data-stu-id="39ddd-148">3600</span></span> | <span data-ttu-id="39ddd-149">1800</span><span class="sxs-lookup"><span data-stu-id="39ddd-149">1800</span></span> |
| <span data-ttu-id="39ddd-150">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-150">Create Conversation</span></span> | <span data-ttu-id="39ddd-151">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-151">1</span></span> | <span data-ttu-id="39ddd-152">7j/7</span><span class="sxs-lookup"><span data-stu-id="39ddd-152">7</span></span> |
| <span data-ttu-id="39ddd-153">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-153">Create Conversation</span></span> | <span data-ttu-id="39ddd-154">n°2</span><span class="sxs-lookup"><span data-stu-id="39ddd-154">2</span></span> | <span data-ttu-id="39ddd-155">8bits</span><span class="sxs-lookup"><span data-stu-id="39ddd-155">8</span></span> |
| <span data-ttu-id="39ddd-156">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-156">Create Conversation</span></span> | <span data-ttu-id="39ddd-157">0,30</span><span class="sxs-lookup"><span data-stu-id="39ddd-157">30</span></span> | <span data-ttu-id="39ddd-158">60</span><span class="sxs-lookup"><span data-stu-id="39ddd-158">60</span></span> |
| <span data-ttu-id="39ddd-159">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-159">Create Conversation</span></span> | <span data-ttu-id="39ddd-160">3600</span><span class="sxs-lookup"><span data-stu-id="39ddd-160">3600</span></span> | <span data-ttu-id="39ddd-161">1800</span><span class="sxs-lookup"><span data-stu-id="39ddd-161">1800</span></span> |
| <span data-ttu-id="39ddd-162">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-162">Get Conversation Members</span></span>| <span data-ttu-id="39ddd-163">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-163">1</span></span> | <span data-ttu-id="39ddd-164">14 </span><span class="sxs-lookup"><span data-stu-id="39ddd-164">14</span></span> |
| <span data-ttu-id="39ddd-165">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-165">Get Conversation Members</span></span>| <span data-ttu-id="39ddd-166">n°2</span><span class="sxs-lookup"><span data-stu-id="39ddd-166">2</span></span> | <span data-ttu-id="39ddd-167">16 </span><span class="sxs-lookup"><span data-stu-id="39ddd-167">16</span></span> |
| <span data-ttu-id="39ddd-168">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-168">Get Conversation Members</span></span>| <span data-ttu-id="39ddd-169">0,30</span><span class="sxs-lookup"><span data-stu-id="39ddd-169">30</span></span> | <span data-ttu-id="39ddd-170">120</span><span class="sxs-lookup"><span data-stu-id="39ddd-170">120</span></span> |
| <span data-ttu-id="39ddd-171">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-171">Get Conversation Members</span></span>| <span data-ttu-id="39ddd-172">3600</span><span class="sxs-lookup"><span data-stu-id="39ddd-172">3600</span></span> | <span data-ttu-id="39ddd-173">3600</span><span class="sxs-lookup"><span data-stu-id="39ddd-173">3600</span></span> |
| <span data-ttu-id="39ddd-174">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="39ddd-174">Get Conversations</span></span> | <span data-ttu-id="39ddd-175">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-175">1</span></span> | <span data-ttu-id="39ddd-176">14 </span><span class="sxs-lookup"><span data-stu-id="39ddd-176">14</span></span> |
| <span data-ttu-id="39ddd-177">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="39ddd-177">Get Conversations</span></span> | <span data-ttu-id="39ddd-178">n°2</span><span class="sxs-lookup"><span data-stu-id="39ddd-178">2</span></span> | <span data-ttu-id="39ddd-179">16 </span><span class="sxs-lookup"><span data-stu-id="39ddd-179">16</span></span> |
| <span data-ttu-id="39ddd-180">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="39ddd-180">Get Conversations</span></span> | <span data-ttu-id="39ddd-181">0,30</span><span class="sxs-lookup"><span data-stu-id="39ddd-181">30</span></span> | <span data-ttu-id="39ddd-182">120</span><span class="sxs-lookup"><span data-stu-id="39ddd-182">120</span></span> |
| <span data-ttu-id="39ddd-183">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="39ddd-183">Get Conversations</span></span> | <span data-ttu-id="39ddd-184">3600</span><span class="sxs-lookup"><span data-stu-id="39ddd-184">3600</span></span> | <span data-ttu-id="39ddd-185">3600</span><span class="sxs-lookup"><span data-stu-id="39ddd-185">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="39ddd-186">Limite par thread pour tous les robots</span><span class="sxs-lookup"><span data-stu-id="39ddd-186">Per thread limit for all bots</span></span>

<span data-ttu-id="39ddd-187">Cette limite contrôle le trafic que tous les robots sont autorisés à générer au sein d’une conversation unique.</span><span class="sxs-lookup"><span data-stu-id="39ddd-187">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="39ddd-188">Une conversation est 1:1 entre le bot et l’utilisateur, un groupe de conversation ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="39ddd-188">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="39ddd-189">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="39ddd-189">**Scenario**</span></span> | <span data-ttu-id="39ddd-190">**Période de temps (sec)**</span><span class="sxs-lookup"><span data-stu-id="39ddd-190">**Time-period (sec)**</span></span> | <span data-ttu-id="39ddd-191">**Nombre maximal d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="39ddd-191">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39ddd-192">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-192">Send to Conversation</span></span> | <span data-ttu-id="39ddd-193">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-193">1</span></span> | <span data-ttu-id="39ddd-194">14 </span><span class="sxs-lookup"><span data-stu-id="39ddd-194">14</span></span> |
| <span data-ttu-id="39ddd-195">Envoyer à une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-195">Send to Conversation</span></span> | <span data-ttu-id="39ddd-196">n°2</span><span class="sxs-lookup"><span data-stu-id="39ddd-196">2</span></span> | <span data-ttu-id="39ddd-197">16 </span><span class="sxs-lookup"><span data-stu-id="39ddd-197">16</span></span> |
| <span data-ttu-id="39ddd-198">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-198">Create Conversation</span></span> | <span data-ttu-id="39ddd-199">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-199">1</span></span> | <span data-ttu-id="39ddd-200">14 </span><span class="sxs-lookup"><span data-stu-id="39ddd-200">14</span></span> |
| <span data-ttu-id="39ddd-201">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-201">Create Conversation</span></span> | <span data-ttu-id="39ddd-202">n°2</span><span class="sxs-lookup"><span data-stu-id="39ddd-202">2</span></span> | <span data-ttu-id="39ddd-203">16 </span><span class="sxs-lookup"><span data-stu-id="39ddd-203">16</span></span> |
| <span data-ttu-id="39ddd-204">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-204">CreateConversation</span></span>| <span data-ttu-id="39ddd-205">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-205">1</span></span> | <span data-ttu-id="39ddd-206">14 </span><span class="sxs-lookup"><span data-stu-id="39ddd-206">14</span></span> |
| <span data-ttu-id="39ddd-207">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-207">CreateConversation</span></span>| <span data-ttu-id="39ddd-208">n°2</span><span class="sxs-lookup"><span data-stu-id="39ddd-208">2</span></span> | <span data-ttu-id="39ddd-209">16 </span><span class="sxs-lookup"><span data-stu-id="39ddd-209">16</span></span> |
| <span data-ttu-id="39ddd-210">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-210">Get Conversation Members</span></span>| <span data-ttu-id="39ddd-211">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-211">1</span></span> | <span data-ttu-id="39ddd-212">vingt</span><span class="sxs-lookup"><span data-stu-id="39ddd-212">28</span></span> |
| <span data-ttu-id="39ddd-213">Obtenir des membres de conversation</span><span class="sxs-lookup"><span data-stu-id="39ddd-213">Get Conversation Members</span></span>| <span data-ttu-id="39ddd-214">n°2</span><span class="sxs-lookup"><span data-stu-id="39ddd-214">2</span></span> | <span data-ttu-id="39ddd-215">32</span><span class="sxs-lookup"><span data-stu-id="39ddd-215">32</span></span> |
| <span data-ttu-id="39ddd-216">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="39ddd-216">Get Conversations</span></span> | <span data-ttu-id="39ddd-217">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-217">1</span></span> | <span data-ttu-id="39ddd-218">vingt</span><span class="sxs-lookup"><span data-stu-id="39ddd-218">28</span></span> |
| <span data-ttu-id="39ddd-219">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="39ddd-219">Get Conversations</span></span> | <span data-ttu-id="39ddd-220">n°2</span><span class="sxs-lookup"><span data-stu-id="39ddd-220">2</span></span> | <span data-ttu-id="39ddd-221">32</span><span class="sxs-lookup"><span data-stu-id="39ddd-221">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="39ddd-222">Fonction de robot par centre de données</span><span class="sxs-lookup"><span data-stu-id="39ddd-222">Bot per data center limit</span></span>

<span data-ttu-id="39ddd-223">Cette limite contrôle le trafic qu’un bot est autorisé à générer sur tous les threads dans un centre de données (sur plusieurs clients).</span><span class="sxs-lookup"><span data-stu-id="39ddd-223">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="39ddd-224">**Période de temps (sec)**</span><span class="sxs-lookup"><span data-stu-id="39ddd-224">**Time-period (sec)**</span></span> | <span data-ttu-id="39ddd-225">**Nombre maximal d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="39ddd-225">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="39ddd-226">0,1</span><span class="sxs-lookup"><span data-stu-id="39ddd-226">1</span></span> | <span data-ttu-id="39ddd-227">vingtaine</span><span class="sxs-lookup"><span data-stu-id="39ddd-227">20</span></span> |
| <span data-ttu-id="39ddd-228">1800</span><span class="sxs-lookup"><span data-stu-id="39ddd-228">1800</span></span> | <span data-ttu-id="39ddd-229">8000</span><span class="sxs-lookup"><span data-stu-id="39ddd-229">8000</span></span> |
| <span data-ttu-id="39ddd-230">3600</span><span class="sxs-lookup"><span data-stu-id="39ddd-230">3600</span></span> | <span data-ttu-id="39ddd-231">15000</span><span class="sxs-lookup"><span data-stu-id="39ddd-231">15000</span></span> |
