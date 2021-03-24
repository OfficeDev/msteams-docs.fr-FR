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
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="0695d-104">Optimiser votre bot : limitation des taux et meilleures pratiques dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0695d-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="0695d-105">En règle générale, votre application doit limiter le nombre de messages qu’elle publie à une conversation individuelle ou à une conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="0695d-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="0695d-106">Cela garantit une expérience optimale qui ne se sent pas « indésirable » pour vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="0695d-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="0695d-107">Pour protéger Microsoft Teams et ses utilisateurs, les API de bot limitent la fréquence des demandes entrantes.</span><span class="sxs-lookup"><span data-stu-id="0695d-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="0695d-108">Les applications qui vont au-dessus de cette limite reçoivent un `HTTP 429 Too Many Requests` état d’erreur.</span><span class="sxs-lookup"><span data-stu-id="0695d-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="0695d-109">Toutes les demandes sont soumises à la même stratégie de limitation de taux, y compris l’envoi de messages, les listes d’éumérations de canaux et les extractions de listes.</span><span class="sxs-lookup"><span data-stu-id="0695d-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="0695d-110">Étant donné que les valeurs exactes des limites de taux sont sujettes à modification, nous recommandons à votre application d’implémenter le comportement d’insé backoff approprié lorsque l’API est de `HTTP 429 Too Many Requests` retour.</span><span class="sxs-lookup"><span data-stu-id="0695d-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="0695d-111">Gestion des limites de taux</span><span class="sxs-lookup"><span data-stu-id="0695d-111">Handling rate limits</span></span>

<span data-ttu-id="0695d-112">Lors de l’émission d’une opération du SDK Bot Builder, vous pouvez gérer et `Microsoft.Rest.HttpOperationException` vérifier le code d’état.</span><span class="sxs-lookup"><span data-stu-id="0695d-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="0695d-113">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="0695d-113">Best practices</span></span>

<span data-ttu-id="0695d-114">En règle générale, vous devez prendre des précautions simples pour éviter de recevoir des `HTTP 429` réponses.</span><span class="sxs-lookup"><span data-stu-id="0695d-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="0695d-115">Par exemple, évitez d’émettre plusieurs demandes à la même conversation personnelle ou de canal.</span><span class="sxs-lookup"><span data-stu-id="0695d-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="0695d-116">Envisagez plutôt de traitement par lots des demandes d’API.</span><span class="sxs-lookup"><span data-stu-id="0695d-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="0695d-117">Il est recommandé d’utiliser un retour exponentiel avec une gigue aléatoire pour gérer les 429.</span><span class="sxs-lookup"><span data-stu-id="0695d-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="0695d-118">Cela garantit que plusieurs demandes n’introduisent pas de collisions lors des nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="0695d-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="0695d-119">Exemple : détection d’exceptions temporaires</span><span class="sxs-lookup"><span data-stu-id="0695d-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="0695d-120">Voici un exemple d’utilisation du blocage exponentiel via le bloc d’applications de gestion des erreurs temporaires.</span><span class="sxs-lookup"><span data-stu-id="0695d-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="0695d-121">Vous pouvez effectuer des tentatives de retour et des tentatives à l’aide [de la gestion des erreurs temporaires.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)</span><span class="sxs-lookup"><span data-stu-id="0695d-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="0695d-122">Pour obtenir des instructions sur l’obtention et l’installation du package NuGet, voir [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span><span class="sxs-lookup"><span data-stu-id="0695d-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="0695d-123">*Voir aussi Gestion* [des erreurs temporaires.](/azure/architecture/best-practices/transient-faults)</span><span class="sxs-lookup"><span data-stu-id="0695d-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="0695d-124">Exemple : mise en arrière</span><span class="sxs-lookup"><span data-stu-id="0695d-124">Example: backoff</span></span>

<span data-ttu-id="0695d-125">En plus de détecter les limites de taux, vous pouvez également effectuer une limitation exponentielle.</span><span class="sxs-lookup"><span data-stu-id="0695d-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="0695d-126">Vous pouvez également exécuter une méthode `System.Action` avec la stratégie de nouvelle tentative décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0695d-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="0695d-127">La bibliothèque référencé vous permet également de spécifier un intervalle fixe ou un mécanisme d’interruption linéaire.</span><span class="sxs-lookup"><span data-stu-id="0695d-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="0695d-128">Nous vous recommandons de stocker la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs au moment de l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="0695d-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="0695d-129">Pour plus d’informations, consultez ce guide pratique sur différents modèles de nouvelles tentatives : [Modèle de nouvelle tentative.](/azure/architecture/patterns/retry)</span><span class="sxs-lookup"><span data-stu-id="0695d-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="0695d-130">Par bot par limite de thread</span><span class="sxs-lookup"><span data-stu-id="0695d-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="0695d-131">Le fractionnement des messages au niveau du service entraîne des demandes par seconde supérieures aux attentes.</span><span class="sxs-lookup"><span data-stu-id="0695d-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="0695d-132">Si vous êtes préoccupé par l’approche des limites, vous devez implémenter la stratégie de retour à la limite décrite ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="0695d-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="0695d-133">Les valeurs fournies ci-dessous sont uniquement à des valeurs d’estimation.</span><span class="sxs-lookup"><span data-stu-id="0695d-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="0695d-134">Cette limite contrôle le trafic qu’un bot est autorisé à générer sur une seule conversation.</span><span class="sxs-lookup"><span data-stu-id="0695d-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="0695d-135">Une conversation est en tête à tête entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="0695d-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="0695d-136">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="0695d-136">**Scenario**</span></span> | <span data-ttu-id="0695d-137">**Période de temps (sec)**</span><span class="sxs-lookup"><span data-stu-id="0695d-137">**Time-period (sec)**</span></span> | <span data-ttu-id="0695d-138">**Nombre maximum d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="0695d-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0695d-139">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-139">Send to Conversation</span></span> | <span data-ttu-id="0695d-140">1</span><span class="sxs-lookup"><span data-stu-id="0695d-140">1</span></span> | <span data-ttu-id="0695d-141">7 </span><span class="sxs-lookup"><span data-stu-id="0695d-141">7</span></span> |
| <span data-ttu-id="0695d-142">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-142">Send to Conversation</span></span> | <span data-ttu-id="0695d-143">2</span><span class="sxs-lookup"><span data-stu-id="0695d-143">2</span></span> | <span data-ttu-id="0695d-144">8 </span><span class="sxs-lookup"><span data-stu-id="0695d-144">8</span></span> |
| <span data-ttu-id="0695d-145">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-145">Send to Conversation</span></span> | <span data-ttu-id="0695d-146">30</span><span class="sxs-lookup"><span data-stu-id="0695d-146">30</span></span> | <span data-ttu-id="0695d-147">60</span><span class="sxs-lookup"><span data-stu-id="0695d-147">60</span></span> |
| <span data-ttu-id="0695d-148">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-148">Send to Conversation</span></span> | <span data-ttu-id="0695d-149">3600</span><span class="sxs-lookup"><span data-stu-id="0695d-149">3600</span></span> | <span data-ttu-id="0695d-150">1800</span><span class="sxs-lookup"><span data-stu-id="0695d-150">1800</span></span> |
| <span data-ttu-id="0695d-151">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-151">Create Conversation</span></span> | <span data-ttu-id="0695d-152">1</span><span class="sxs-lookup"><span data-stu-id="0695d-152">1</span></span> | <span data-ttu-id="0695d-153">7 </span><span class="sxs-lookup"><span data-stu-id="0695d-153">7</span></span> |
| <span data-ttu-id="0695d-154">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-154">Create Conversation</span></span> | <span data-ttu-id="0695d-155">2</span><span class="sxs-lookup"><span data-stu-id="0695d-155">2</span></span> | <span data-ttu-id="0695d-156">8 </span><span class="sxs-lookup"><span data-stu-id="0695d-156">8</span></span> |
| <span data-ttu-id="0695d-157">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-157">Create Conversation</span></span> | <span data-ttu-id="0695d-158">30</span><span class="sxs-lookup"><span data-stu-id="0695d-158">30</span></span> | <span data-ttu-id="0695d-159">60</span><span class="sxs-lookup"><span data-stu-id="0695d-159">60</span></span> |
| <span data-ttu-id="0695d-160">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-160">Create Conversation</span></span> | <span data-ttu-id="0695d-161">3600</span><span class="sxs-lookup"><span data-stu-id="0695d-161">3600</span></span> | <span data-ttu-id="0695d-162">1800</span><span class="sxs-lookup"><span data-stu-id="0695d-162">1800</span></span> |
| <span data-ttu-id="0695d-163">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-163">Get Conversation Members</span></span>| <span data-ttu-id="0695d-164">1</span><span class="sxs-lookup"><span data-stu-id="0695d-164">1</span></span> | <span data-ttu-id="0695d-165">14 </span><span class="sxs-lookup"><span data-stu-id="0695d-165">14</span></span> |
| <span data-ttu-id="0695d-166">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-166">Get Conversation Members</span></span>| <span data-ttu-id="0695d-167">2</span><span class="sxs-lookup"><span data-stu-id="0695d-167">2</span></span> | <span data-ttu-id="0695d-168">16 </span><span class="sxs-lookup"><span data-stu-id="0695d-168">16</span></span> |
| <span data-ttu-id="0695d-169">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-169">Get Conversation Members</span></span>| <span data-ttu-id="0695d-170">30</span><span class="sxs-lookup"><span data-stu-id="0695d-170">30</span></span> | <span data-ttu-id="0695d-171">120</span><span class="sxs-lookup"><span data-stu-id="0695d-171">120</span></span> |
| <span data-ttu-id="0695d-172">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-172">Get Conversation Members</span></span>| <span data-ttu-id="0695d-173">3600</span><span class="sxs-lookup"><span data-stu-id="0695d-173">3600</span></span> | <span data-ttu-id="0695d-174">3600</span><span class="sxs-lookup"><span data-stu-id="0695d-174">3600</span></span> |
| <span data-ttu-id="0695d-175">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0695d-175">Get Conversations</span></span> | <span data-ttu-id="0695d-176">1</span><span class="sxs-lookup"><span data-stu-id="0695d-176">1</span></span> | <span data-ttu-id="0695d-177">14 </span><span class="sxs-lookup"><span data-stu-id="0695d-177">14</span></span> |
| <span data-ttu-id="0695d-178">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0695d-178">Get Conversations</span></span> | <span data-ttu-id="0695d-179">2</span><span class="sxs-lookup"><span data-stu-id="0695d-179">2</span></span> | <span data-ttu-id="0695d-180">16 </span><span class="sxs-lookup"><span data-stu-id="0695d-180">16</span></span> |
| <span data-ttu-id="0695d-181">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0695d-181">Get Conversations</span></span> | <span data-ttu-id="0695d-182">30</span><span class="sxs-lookup"><span data-stu-id="0695d-182">30</span></span> | <span data-ttu-id="0695d-183">120</span><span class="sxs-lookup"><span data-stu-id="0695d-183">120</span></span> |
| <span data-ttu-id="0695d-184">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0695d-184">Get Conversations</span></span> | <span data-ttu-id="0695d-185">3600</span><span class="sxs-lookup"><span data-stu-id="0695d-185">3600</span></span> | <span data-ttu-id="0695d-186">3600</span><span class="sxs-lookup"><span data-stu-id="0695d-186">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="0695d-187">Les versions `TeamsInfo.getMembers` précédentes et `TeamsInfo.GetMembersAsync` les API sont en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="0695d-187">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="0695d-188">Ils sont limitées à 5 demandes par minute et retournent un maximum de 10 000 membres par équipe.</span><span class="sxs-lookup"><span data-stu-id="0695d-188">They will be throttled to 5 requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="0695d-189">Pour mettre à jour votre SDK Bot Framework et le code pour utiliser les derniers points de terminaison de l’API paginée, voir Modifications apportées à l’API bot pour les membres de l’équipe [et de la conversation.](../../resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="0695d-189">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="0695d-190">Limite par thread pour tous les bots</span><span class="sxs-lookup"><span data-stu-id="0695d-190">Per thread limit for all bots</span></span>

<span data-ttu-id="0695d-191">Cette limite contrôle le trafic que tous les bots sont autorisés à générer au sein d’une seule conversation.</span><span class="sxs-lookup"><span data-stu-id="0695d-191">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="0695d-192">Une conversation est en tête à tête entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="0695d-192">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="0695d-193">**Scénario**</span><span class="sxs-lookup"><span data-stu-id="0695d-193">**Scenario**</span></span> | <span data-ttu-id="0695d-194">**Période de temps (sec)**</span><span class="sxs-lookup"><span data-stu-id="0695d-194">**Time-period (sec)**</span></span> | <span data-ttu-id="0695d-195">**Nombre maximum d’opérations autorisées**</span><span class="sxs-lookup"><span data-stu-id="0695d-195">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0695d-196">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-196">Send to Conversation</span></span> | <span data-ttu-id="0695d-197">1</span><span class="sxs-lookup"><span data-stu-id="0695d-197">1</span></span> | <span data-ttu-id="0695d-198">14 </span><span class="sxs-lookup"><span data-stu-id="0695d-198">14</span></span> |
| <span data-ttu-id="0695d-199">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-199">Send to Conversation</span></span> | <span data-ttu-id="0695d-200">2</span><span class="sxs-lookup"><span data-stu-id="0695d-200">2</span></span> | <span data-ttu-id="0695d-201">16 </span><span class="sxs-lookup"><span data-stu-id="0695d-201">16</span></span> |
| <span data-ttu-id="0695d-202">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-202">Create Conversation</span></span> | <span data-ttu-id="0695d-203">1</span><span class="sxs-lookup"><span data-stu-id="0695d-203">1</span></span> | <span data-ttu-id="0695d-204">14 </span><span class="sxs-lookup"><span data-stu-id="0695d-204">14</span></span> |
| <span data-ttu-id="0695d-205">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-205">Create Conversation</span></span> | <span data-ttu-id="0695d-206">2</span><span class="sxs-lookup"><span data-stu-id="0695d-206">2</span></span> | <span data-ttu-id="0695d-207">16 </span><span class="sxs-lookup"><span data-stu-id="0695d-207">16</span></span> |
| <span data-ttu-id="0695d-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="0695d-208">CreateConversation</span></span>| <span data-ttu-id="0695d-209">1</span><span class="sxs-lookup"><span data-stu-id="0695d-209">1</span></span> | <span data-ttu-id="0695d-210">14 </span><span class="sxs-lookup"><span data-stu-id="0695d-210">14</span></span> |
| <span data-ttu-id="0695d-211">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="0695d-211">CreateConversation</span></span>| <span data-ttu-id="0695d-212">2</span><span class="sxs-lookup"><span data-stu-id="0695d-212">2</span></span> | <span data-ttu-id="0695d-213">16 </span><span class="sxs-lookup"><span data-stu-id="0695d-213">16</span></span> |
| <span data-ttu-id="0695d-214">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-214">Get Conversation Members</span></span>| <span data-ttu-id="0695d-215">1</span><span class="sxs-lookup"><span data-stu-id="0695d-215">1</span></span> | <span data-ttu-id="0695d-216">28</span><span class="sxs-lookup"><span data-stu-id="0695d-216">28</span></span> |
| <span data-ttu-id="0695d-217">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0695d-217">Get Conversation Members</span></span>| <span data-ttu-id="0695d-218">2</span><span class="sxs-lookup"><span data-stu-id="0695d-218">2</span></span> | <span data-ttu-id="0695d-219">32</span><span class="sxs-lookup"><span data-stu-id="0695d-219">32</span></span> |
| <span data-ttu-id="0695d-220">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0695d-220">Get Conversations</span></span> | <span data-ttu-id="0695d-221">1</span><span class="sxs-lookup"><span data-stu-id="0695d-221">1</span></span> | <span data-ttu-id="0695d-222">28</span><span class="sxs-lookup"><span data-stu-id="0695d-222">28</span></span> |
| <span data-ttu-id="0695d-223">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0695d-223">Get Conversations</span></span> | <span data-ttu-id="0695d-224">2</span><span class="sxs-lookup"><span data-stu-id="0695d-224">2</span></span> | <span data-ttu-id="0695d-225">32</span><span class="sxs-lookup"><span data-stu-id="0695d-225">32</span></span> |
