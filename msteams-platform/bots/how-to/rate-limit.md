---
title: Optimiser votre bot avec une limite de taux dans Teams
description: Limitation des taux et meilleures pratiques dans Microsoft Teams
ms.topic: conceptual
keywords: limitation des taux de bots teams
ms.openlocfilehash: 245c51fc736e5f888299535c3e50ec6232183623
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696996"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="0ccb3-104">Optimiser votre bot avec une limite de taux dans Teams</span><span class="sxs-lookup"><span data-stu-id="0ccb3-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="0ccb3-105">La limitation des taux est une méthode pour limiter les messages à une certaine fréquence maximale.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="0ccb3-106">En règle générale, votre application doit limiter le nombre de messages qu'elle publie à une conversation individuelle ou à une conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="0ccb3-107">Cela garantit une expérience optimale et les messages n'apparaissent pas comme courrier indésirable pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="0ccb3-108">Pour protéger Microsoft Teams et ses utilisateurs, les API de bot fournissent une limite de taux pour les demandes entrantes.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="0ccb3-109">Les applications qui vont au-dessus de cette limite reçoivent un `HTTP 429 Too Many Requests` état d'erreur.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="0ccb3-110">Toutes les demandes sont soumises à la même stratégie de limitation des taux, y compris l'envoi de messages, les listes d'envoi et les extractions de listes.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="0ccb3-111">Comme les valeurs exactes des limites de taux sont sujettes à modification, votre application doit implémenter le comportement d'insé backoff approprié lorsque l'API renvoie `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="0ccb3-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="0ccb3-112">Gérer les limites de taux</span><span class="sxs-lookup"><span data-stu-id="0ccb3-112">Handle rate limits</span></span>

<span data-ttu-id="0ccb3-113">Lors de l'émission d'une opération du SDK Bot Builder, vous pouvez gérer et `Microsoft.Rest.HttpOperationException` vérifier le code d'état.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="0ccb3-114">Le code suivant illustre un exemple de gestion des limites de taux :</span><span class="sxs-lookup"><span data-stu-id="0ccb3-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="0ccb3-115">Une fois que vous avez géré les limites de taux pour les bots, vous pouvez gérer les réponses à l'aide `HTTP 429` d'un retour exponentiel.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="0ccb3-116">Gérer les `HTTP 429` réponses</span><span class="sxs-lookup"><span data-stu-id="0ccb3-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="0ccb3-117">En règle générale, vous devez prendre des précautions simples pour éviter de recevoir des `HTTP 429` réponses.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="0ccb3-118">Par exemple, évitez d'émettre plusieurs demandes à la même conversation personnelle ou de canal.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="0ccb3-119">Créez plutôt un lot de demandes d'API.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="0ccb3-120">Il est recommandé d'utiliser un retour exponentiel avec une gigue aléatoire pour gérer les 429.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="0ccb3-121">Cela garantit que plusieurs demandes n'introduisent pas de collisions lors des nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="0ccb3-122">Une fois que vous `HTTP 429` avez géré les réponses, vous pouvez passer par l'exemple pour détecter les exceptions temporaires.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="0ccb3-123">Exemple de détection d'exceptions temporaires</span><span class="sxs-lookup"><span data-stu-id="0ccb3-123">Detect transient exceptions example</span></span>

<span data-ttu-id="0ccb3-124">Le code suivant illustre un exemple d'utilisation du blocage exponentiel à l'aide du bloc d'application de gestion des erreurs temporaires :</span><span class="sxs-lookup"><span data-stu-id="0ccb3-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="0ccb3-125">Vous pouvez effectuer des tentatives de retour et des tentatives à l'aide de [la gestion des erreurs temporaires.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)</span><span class="sxs-lookup"><span data-stu-id="0ccb3-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="0ccb3-126">Pour obtenir des instructions sur l'obtention et l'installation du package NuGet, voir l'ajout du bloc d'application de gestion des erreurs [temporaires à votre solution.](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="0ccb3-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="0ccb3-127">Voir aussi [la gestion des erreurs temporaires.](/azure/architecture/best-practices/transient-faults)</span><span class="sxs-lookup"><span data-stu-id="0ccb3-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="0ccb3-128">Après avoir découvert l'exemple de détection d'exceptions temporaires, prenons l'exemple de la fonction d'inserrable exponentielle.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="0ccb3-129">Vous pouvez utiliser l'arrêt exponentiel au lieu de réessayer en cas d'échec.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="0ccb3-130">Exemple de mise en arrière</span><span class="sxs-lookup"><span data-stu-id="0ccb3-130">Backoff example</span></span>

<span data-ttu-id="0ccb3-131">En plus de détecter les limites de taux, vous pouvez également effectuer une coupure exponentielle.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="0ccb3-132">Le code suivant illustre un exemple de coupure exponentielle :</span><span class="sxs-lookup"><span data-stu-id="0ccb3-132">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="0ccb3-133">Vous pouvez également exécuter une méthode `System.Action` avec la stratégie de nouvelle tentative décrite dans cette section.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="0ccb3-134">La bibliothèque référencé vous permet également de spécifier un intervalle fixe ou un mécanisme d'interruption linéaire.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="0ccb3-135">Stockez la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs au moment de l'exécuter.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="0ccb3-136">Pour plus d'informations, [voir les modèles de nouvelle tentative.](/azure/architecture/patterns/retry)</span><span class="sxs-lookup"><span data-stu-id="0ccb3-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="0ccb3-137">Vous pouvez également gérer la limite de taux à l'aide de la limite par bot par thread.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="0ccb3-138">Par bot par limite de thread</span><span class="sxs-lookup"><span data-stu-id="0ccb3-138">Per bot per thread limit</span></span>

>[!NOTE]
> <span data-ttu-id="0ccb3-139">Le fractionnement des messages au niveau du service entraîne des demandes par seconde supérieures aux attentes.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-139">Message splitting at the service level results in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="0ccb3-140">Si vous êtes préoccupé par l'approche des limites, vous devez implémenter la stratégie [de retour à la limite.](#backoff-example)</span><span class="sxs-lookup"><span data-stu-id="0ccb3-140">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="0ccb3-141">Les valeurs fournies dans cette section sont uniquement à des valeurs d’estimation.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-141">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="0ccb3-142">La limite par bot par thread contrôle le trafic qu’un bot est autorisé à générer sur une seule conversation.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-142">The per bot per thread limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="0ccb3-143">Une conversation est en tête à tête entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-143">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="0ccb3-144">Le tableau suivant fournit les limites par bot par thread :</span><span class="sxs-lookup"><span data-stu-id="0ccb3-144">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="0ccb3-145">Scénario</span><span class="sxs-lookup"><span data-stu-id="0ccb3-145">Scenario</span></span> | <span data-ttu-id="0ccb3-146">Période en secondes</span><span class="sxs-lookup"><span data-stu-id="0ccb3-146">Time period in seconds</span></span> | <span data-ttu-id="0ccb3-147">Nombre maximal d’opérations autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccb3-147">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccb3-148">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-148">Send to conversation</span></span> | <span data-ttu-id="0ccb3-149">1</span><span class="sxs-lookup"><span data-stu-id="0ccb3-149">1</span></span> | <span data-ttu-id="0ccb3-150">7 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-150">7</span></span> |
| <span data-ttu-id="0ccb3-151">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-151">Send to conversation</span></span> | <span data-ttu-id="0ccb3-152">2</span><span class="sxs-lookup"><span data-stu-id="0ccb3-152">2</span></span> | <span data-ttu-id="0ccb3-153">8 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-153">8</span></span> |
| <span data-ttu-id="0ccb3-154">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-154">Send to conversation</span></span> | <span data-ttu-id="0ccb3-155">30</span><span class="sxs-lookup"><span data-stu-id="0ccb3-155">30</span></span> | <span data-ttu-id="0ccb3-156">60</span><span class="sxs-lookup"><span data-stu-id="0ccb3-156">60</span></span> |
| <span data-ttu-id="0ccb3-157">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-157">Send to conversation</span></span> | <span data-ttu-id="0ccb3-158">3600</span><span class="sxs-lookup"><span data-stu-id="0ccb3-158">3600</span></span> | <span data-ttu-id="0ccb3-159">1800</span><span class="sxs-lookup"><span data-stu-id="0ccb3-159">1800</span></span> |
| <span data-ttu-id="0ccb3-160">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-160">Create conversation</span></span> | <span data-ttu-id="0ccb3-161">1</span><span class="sxs-lookup"><span data-stu-id="0ccb3-161">1</span></span> | <span data-ttu-id="0ccb3-162">7 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-162">7</span></span> |
| <span data-ttu-id="0ccb3-163">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-163">Create conversation</span></span> | <span data-ttu-id="0ccb3-164">2</span><span class="sxs-lookup"><span data-stu-id="0ccb3-164">2</span></span> | <span data-ttu-id="0ccb3-165">8 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-165">8</span></span> |
| <span data-ttu-id="0ccb3-166">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-166">Create conversation</span></span> | <span data-ttu-id="0ccb3-167">30</span><span class="sxs-lookup"><span data-stu-id="0ccb3-167">30</span></span> | <span data-ttu-id="0ccb3-168">60</span><span class="sxs-lookup"><span data-stu-id="0ccb3-168">60</span></span> |
| <span data-ttu-id="0ccb3-169">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-169">Create conversation</span></span> | <span data-ttu-id="0ccb3-170">3600</span><span class="sxs-lookup"><span data-stu-id="0ccb3-170">3600</span></span> | <span data-ttu-id="0ccb3-171">1800</span><span class="sxs-lookup"><span data-stu-id="0ccb3-171">1800</span></span> |
| <span data-ttu-id="0ccb3-172">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-172">Get conversation members</span></span>| <span data-ttu-id="0ccb3-173">1</span><span class="sxs-lookup"><span data-stu-id="0ccb3-173">1</span></span> | <span data-ttu-id="0ccb3-174">14 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-174">14</span></span> |
| <span data-ttu-id="0ccb3-175">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-175">Get conversation members</span></span>| <span data-ttu-id="0ccb3-176">2</span><span class="sxs-lookup"><span data-stu-id="0ccb3-176">2</span></span> | <span data-ttu-id="0ccb3-177">16 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-177">16</span></span> |
| <span data-ttu-id="0ccb3-178">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-178">Get conversation members</span></span>| <span data-ttu-id="0ccb3-179">30</span><span class="sxs-lookup"><span data-stu-id="0ccb3-179">30</span></span> | <span data-ttu-id="0ccb3-180">120</span><span class="sxs-lookup"><span data-stu-id="0ccb3-180">120</span></span> |
| <span data-ttu-id="0ccb3-181">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-181">Get conversation members</span></span>| <span data-ttu-id="0ccb3-182">3600</span><span class="sxs-lookup"><span data-stu-id="0ccb3-182">3600</span></span> | <span data-ttu-id="0ccb3-183">3600</span><span class="sxs-lookup"><span data-stu-id="0ccb3-183">3600</span></span> |
| <span data-ttu-id="0ccb3-184">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0ccb3-184">Get conversations</span></span> | <span data-ttu-id="0ccb3-185">1</span><span class="sxs-lookup"><span data-stu-id="0ccb3-185">1</span></span> | <span data-ttu-id="0ccb3-186">14 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-186">14</span></span> |
| <span data-ttu-id="0ccb3-187">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0ccb3-187">Get conversations</span></span> | <span data-ttu-id="0ccb3-188">2</span><span class="sxs-lookup"><span data-stu-id="0ccb3-188">2</span></span> | <span data-ttu-id="0ccb3-189">16 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-189">16</span></span> |
| <span data-ttu-id="0ccb3-190">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0ccb3-190">Get conversations</span></span> | <span data-ttu-id="0ccb3-191">30</span><span class="sxs-lookup"><span data-stu-id="0ccb3-191">30</span></span> | <span data-ttu-id="0ccb3-192">120</span><span class="sxs-lookup"><span data-stu-id="0ccb3-192">120</span></span> |
| <span data-ttu-id="0ccb3-193">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0ccb3-193">Get conversations</span></span> | <span data-ttu-id="0ccb3-194">3600</span><span class="sxs-lookup"><span data-stu-id="0ccb3-194">3600</span></span> | <span data-ttu-id="0ccb3-195">3600</span><span class="sxs-lookup"><span data-stu-id="0ccb3-195">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="0ccb3-196">Les versions `TeamsInfo.getMembers` précédentes et `TeamsInfo.GetMembersAsync` les API sont en cours d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-196">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="0ccb3-197">Ils sont limitées à cinq demandes par minute et retournent un maximum de 10 000 membres par équipe.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-197">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="0ccb3-198">Pour mettre à jour votre SDK Bot Framework et le code pour utiliser les derniers points de terminaison de l'API paginée, voir Modifications apportées à l'API bot pour les membres de l'équipe [et de la conversation.](../../resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="0ccb3-198">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="0ccb3-199">Vous pouvez également gérer la limite de taux à l'aide de la limite par thread pour tous les bots.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-199">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="0ccb3-200">Limite par thread pour tous les bots</span><span class="sxs-lookup"><span data-stu-id="0ccb3-200">Per thread limit for all bots</span></span>

<span data-ttu-id="0ccb3-201">La limite par thread pour tous les bots contrôle le trafic que tous les bots sont autorisés à générer dans une conversation unique.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-201">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="0ccb3-202">Une conversation est en tête à tête entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="0ccb3-202">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="0ccb3-203">Le tableau suivant fournit la limite par thread pour tous les bots :</span><span class="sxs-lookup"><span data-stu-id="0ccb3-203">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="0ccb3-204">Scénario</span><span class="sxs-lookup"><span data-stu-id="0ccb3-204">Scenario</span></span> | <span data-ttu-id="0ccb3-205">Période en secondes</span><span class="sxs-lookup"><span data-stu-id="0ccb3-205">Time period in seconds</span></span> | <span data-ttu-id="0ccb3-206">Nombre maximal d'opérations autorisées</span><span class="sxs-lookup"><span data-stu-id="0ccb3-206">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ccb3-207">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-207">Send to conversation</span></span> | <span data-ttu-id="0ccb3-208">1</span><span class="sxs-lookup"><span data-stu-id="0ccb3-208">1</span></span> | <span data-ttu-id="0ccb3-209">14 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-209">14</span></span> |
| <span data-ttu-id="0ccb3-210">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-210">Send to conversation</span></span> | <span data-ttu-id="0ccb3-211">2</span><span class="sxs-lookup"><span data-stu-id="0ccb3-211">2</span></span> | <span data-ttu-id="0ccb3-212">16 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-212">16</span></span> |
| <span data-ttu-id="0ccb3-213">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-213">Create conversation</span></span> | <span data-ttu-id="0ccb3-214">1</span><span class="sxs-lookup"><span data-stu-id="0ccb3-214">1</span></span> | <span data-ttu-id="0ccb3-215">14 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-215">14</span></span> |
| <span data-ttu-id="0ccb3-216">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-216">Create conversation</span></span> | <span data-ttu-id="0ccb3-217">2</span><span class="sxs-lookup"><span data-stu-id="0ccb3-217">2</span></span> | <span data-ttu-id="0ccb3-218">16 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-218">16</span></span> |
| <span data-ttu-id="0ccb3-219">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-219">Create conversation</span></span>| <span data-ttu-id="0ccb3-220">1</span><span class="sxs-lookup"><span data-stu-id="0ccb3-220">1</span></span> | <span data-ttu-id="0ccb3-221">14 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-221">14</span></span> |
| <span data-ttu-id="0ccb3-222">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-222">Create conversation</span></span>| <span data-ttu-id="0ccb3-223">2</span><span class="sxs-lookup"><span data-stu-id="0ccb3-223">2</span></span> | <span data-ttu-id="0ccb3-224">16 </span><span class="sxs-lookup"><span data-stu-id="0ccb3-224">16</span></span> |
| <span data-ttu-id="0ccb3-225">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-225">Get conversation members</span></span>| <span data-ttu-id="0ccb3-226">1</span><span class="sxs-lookup"><span data-stu-id="0ccb3-226">1</span></span> | <span data-ttu-id="0ccb3-227">28</span><span class="sxs-lookup"><span data-stu-id="0ccb3-227">28</span></span> |
| <span data-ttu-id="0ccb3-228">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="0ccb3-228">Get conversation members</span></span>| <span data-ttu-id="0ccb3-229">2</span><span class="sxs-lookup"><span data-stu-id="0ccb3-229">2</span></span> | <span data-ttu-id="0ccb3-230">32</span><span class="sxs-lookup"><span data-stu-id="0ccb3-230">32</span></span> |
| <span data-ttu-id="0ccb3-231">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0ccb3-231">Get conversations</span></span> | <span data-ttu-id="0ccb3-232">1</span><span class="sxs-lookup"><span data-stu-id="0ccb3-232">1</span></span> | <span data-ttu-id="0ccb3-233">28</span><span class="sxs-lookup"><span data-stu-id="0ccb3-233">28</span></span> |
| <span data-ttu-id="0ccb3-234">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="0ccb3-234">Get conversations</span></span> | <span data-ttu-id="0ccb3-235">2</span><span class="sxs-lookup"><span data-stu-id="0ccb3-235">2</span></span> | <span data-ttu-id="0ccb3-236">32</span><span class="sxs-lookup"><span data-stu-id="0ccb3-236">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="0ccb3-237">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="0ccb3-237">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0ccb3-238">Bots d'appels et de réunions</span><span class="sxs-lookup"><span data-stu-id="0ccb3-238">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

