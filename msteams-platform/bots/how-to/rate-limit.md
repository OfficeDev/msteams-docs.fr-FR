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
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="799fe-104">Optimisez votre robot grâce à la limitation du débit dans Teams</span><span class="sxs-lookup"><span data-stu-id="799fe-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="799fe-105">La limitation des taux est une méthode pour limiter les messages à une certaine fréquence maximale.</span><span class="sxs-lookup"><span data-stu-id="799fe-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="799fe-106">En règle générale, votre application doit limiter le nombre de messages qu'elle publie à une conversation individuelle ou à une conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="799fe-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="799fe-107">Cela garantit une expérience optimale et les messages n'apparaissent pas comme courrier indésirable pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="799fe-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="799fe-108">Pour protéger Microsoft Teams et ses utilisateurs, les API de bot fournissent une limite de taux pour les demandes entrantes.</span><span class="sxs-lookup"><span data-stu-id="799fe-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="799fe-109">Les applications qui vont au-dessus de cette limite reçoivent un `HTTP 429 Too Many Requests` état d'erreur.</span><span class="sxs-lookup"><span data-stu-id="799fe-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="799fe-110">Toutes les demandes sont soumises à la même stratégie de limitation des taux, y compris l'envoi de messages, les listes de canaux et les extractions de listes.</span><span class="sxs-lookup"><span data-stu-id="799fe-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="799fe-111">Comme les valeurs exactes des limites de taux sont sujettes à modification, votre application doit implémenter le comportement d'insé backoff approprié lorsque l'API renvoie `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="799fe-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="799fe-112">Gérer les limites de taux</span><span class="sxs-lookup"><span data-stu-id="799fe-112">Handle rate limits</span></span>

<span data-ttu-id="799fe-113">Lors de l'émission d'une opération du SDK Bot Builder, vous pouvez gérer et `Microsoft.Rest.HttpOperationException` vérifier le code d'état.</span><span class="sxs-lookup"><span data-stu-id="799fe-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="799fe-114">Le code suivant illustre un exemple de gestion des limites de taux :</span><span class="sxs-lookup"><span data-stu-id="799fe-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="799fe-115">Une fois que vous avez géré les limites de taux pour les bots, vous pouvez gérer les réponses à l'aide `HTTP 429` d'un retour exponentiel.</span><span class="sxs-lookup"><span data-stu-id="799fe-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="799fe-116">Gérer les `HTTP 429` réponses</span><span class="sxs-lookup"><span data-stu-id="799fe-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="799fe-117">En règle générale, vous devez prendre des précautions simples pour éviter de recevoir des `HTTP 429` réponses.</span><span class="sxs-lookup"><span data-stu-id="799fe-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="799fe-118">Par exemple, évitez d'émettre plusieurs demandes à la même conversation personnelle ou de canal.</span><span class="sxs-lookup"><span data-stu-id="799fe-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="799fe-119">Créez plutôt un lot de demandes d'API.</span><span class="sxs-lookup"><span data-stu-id="799fe-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="799fe-120">Il est recommandé d'utiliser un retour exponentiel avec une gigue aléatoire pour gérer les 429.</span><span class="sxs-lookup"><span data-stu-id="799fe-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="799fe-121">Cela garantit que plusieurs demandes n'introduisent pas de collisions lors des nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="799fe-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="799fe-122">Une fois que vous `HTTP 429` avez géré les réponses, vous pouvez passer par l'exemple pour détecter les exceptions temporaires.</span><span class="sxs-lookup"><span data-stu-id="799fe-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="799fe-123">Exemple de détection d'exceptions temporaires</span><span class="sxs-lookup"><span data-stu-id="799fe-123">Detect transient exceptions example</span></span>

<span data-ttu-id="799fe-124">Le code suivant illustre un exemple d'utilisation du blocage exponentiel à l'aide du bloc d'application de gestion des pannes temporaires :</span><span class="sxs-lookup"><span data-stu-id="799fe-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="799fe-125">Vous pouvez effectuer des tentatives de retour et des tentatives à l'aide de [la gestion des erreurs temporaires.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)</span><span class="sxs-lookup"><span data-stu-id="799fe-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="799fe-126">Pour obtenir des instructions sur l'obtention et l'installation du package NuGet, voir l'ajout du bloc d'application de gestion des erreurs [temporaires à votre solution.](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="799fe-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="799fe-127">Voir aussi [la gestion des erreurs temporaires.](/azure/architecture/best-practices/transient-faults)</span><span class="sxs-lookup"><span data-stu-id="799fe-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="799fe-128">Après avoir passé en détail l'exemple de détection des exceptions temporaires, prenons l'exemple de la fonction de retour exponentiel.</span><span class="sxs-lookup"><span data-stu-id="799fe-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="799fe-129">Vous pouvez utiliser l'arrêt exponentiel au lieu de réessayer en cas d'échec.</span><span class="sxs-lookup"><span data-stu-id="799fe-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="799fe-130">Exemple de mise en arrière</span><span class="sxs-lookup"><span data-stu-id="799fe-130">Backoff example</span></span>

<span data-ttu-id="799fe-131">En plus de détecter les limites de taux, vous pouvez également effectuer une coupure exponentielle.</span><span class="sxs-lookup"><span data-stu-id="799fe-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="799fe-132">Le code suivant illustre un exemple de coupure exponentielle :</span><span class="sxs-lookup"><span data-stu-id="799fe-132">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="799fe-133">Vous pouvez également exécuter une méthode `System.Action` avec la stratégie de nouvelle tentative décrite dans cette section.</span><span class="sxs-lookup"><span data-stu-id="799fe-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="799fe-134">La bibliothèque référencé vous permet également de spécifier un intervalle fixe ou un mécanisme d'interruption linéaire.</span><span class="sxs-lookup"><span data-stu-id="799fe-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="799fe-135">Stockez la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs au moment de l'exécuter.</span><span class="sxs-lookup"><span data-stu-id="799fe-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="799fe-136">Pour plus d'informations, [voir les modèles de nouvelle tentative.](/azure/architecture/patterns/retry)</span><span class="sxs-lookup"><span data-stu-id="799fe-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="799fe-137">Vous pouvez également gérer la limite de taux à l'aide de la limite par bot par thread.</span><span class="sxs-lookup"><span data-stu-id="799fe-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="799fe-138">Par bot par limite de thread</span><span class="sxs-lookup"><span data-stu-id="799fe-138">Per bot per thread limit</span></span>

<span data-ttu-id="799fe-139">La limite par bot par thread contrôle le trafic qu'un bot est autorisé à générer dans une seule conversation.</span><span class="sxs-lookup"><span data-stu-id="799fe-139">The per bot per thread limit controls the traffic that a bot is allowed to generate in a single conversation.</span></span> <span data-ttu-id="799fe-140">Une conversation est 1:1 entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="799fe-140">A conversation is 1:1 between bot and user, a group chat, or a channel in a team.</span></span> <span data-ttu-id="799fe-141">Ainsi, si l'application envoie un message bot à chaque utilisateur, la limite de thread ne se limite pas.</span><span class="sxs-lookup"><span data-stu-id="799fe-141">So, if the application sends one bot message to each user, the thread limit does not throttle.</span></span>

>[!NOTE]
> * <span data-ttu-id="799fe-142">La limite de thread de 3 600 secondes et 1 800 opérations s'applique uniquement si plusieurs messages de bot sont envoyés à un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="799fe-142">The thread limit of 3600 seconds and 1800 operations applies only if multiple bot messages are sent to a single user.</span></span> 
> * <span data-ttu-id="799fe-143">La limite globale par application et par client est de 30 demandes par seconde (DEMANDES/s).</span><span class="sxs-lookup"><span data-stu-id="799fe-143">The global limit per app per tenant is 30 Requests Per Second (RPS).</span></span> <span data-ttu-id="799fe-144">Par conséquent, le nombre total de messages de bot par seconde ne doit pas franchir la limite de thread.</span><span class="sxs-lookup"><span data-stu-id="799fe-144">Hence, the total number of bot messages per second must not cross the thread limit.</span></span>
> * <span data-ttu-id="799fe-145">Le fractionnement des messages au niveau du service entraîne un nombre de rps supérieur aux attentes.</span><span class="sxs-lookup"><span data-stu-id="799fe-145">Message splitting at the service level results in higher than expected RPS.</span></span> <span data-ttu-id="799fe-146">Si vous êtes préoccupé par l'approche des limites, vous devez implémenter la stratégie [de retour à la limite.](#backoff-example)</span><span class="sxs-lookup"><span data-stu-id="799fe-146">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="799fe-147">Les valeurs fournies dans cette section sont uniquement à des valeurs d'estimation.</span><span class="sxs-lookup"><span data-stu-id="799fe-147">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="799fe-148">Le tableau suivant fournit les limites par bot par thread :</span><span class="sxs-lookup"><span data-stu-id="799fe-148">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="799fe-149">Scénario</span><span class="sxs-lookup"><span data-stu-id="799fe-149">Scenario</span></span> | <span data-ttu-id="799fe-150">Période en secondes</span><span class="sxs-lookup"><span data-stu-id="799fe-150">Time period in seconds</span></span> | <span data-ttu-id="799fe-151">Nombre maximal d'opérations autorisées</span><span class="sxs-lookup"><span data-stu-id="799fe-151">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="799fe-152">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-152">Send to conversation</span></span> | <span data-ttu-id="799fe-153">1</span><span class="sxs-lookup"><span data-stu-id="799fe-153">1</span></span> | <span data-ttu-id="799fe-154">7 </span><span class="sxs-lookup"><span data-stu-id="799fe-154">7</span></span> |
| <span data-ttu-id="799fe-155">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-155">Send to conversation</span></span> | <span data-ttu-id="799fe-156">2</span><span class="sxs-lookup"><span data-stu-id="799fe-156">2</span></span> | <span data-ttu-id="799fe-157">8 </span><span class="sxs-lookup"><span data-stu-id="799fe-157">8</span></span> |
| <span data-ttu-id="799fe-158">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-158">Send to conversation</span></span> | <span data-ttu-id="799fe-159">30</span><span class="sxs-lookup"><span data-stu-id="799fe-159">30</span></span> | <span data-ttu-id="799fe-160">60</span><span class="sxs-lookup"><span data-stu-id="799fe-160">60</span></span> |
| <span data-ttu-id="799fe-161">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-161">Send to conversation</span></span> | <span data-ttu-id="799fe-162">3600</span><span class="sxs-lookup"><span data-stu-id="799fe-162">3600</span></span> | <span data-ttu-id="799fe-163">1800</span><span class="sxs-lookup"><span data-stu-id="799fe-163">1800</span></span> |
| <span data-ttu-id="799fe-164">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-164">Create conversation</span></span> | <span data-ttu-id="799fe-165">1</span><span class="sxs-lookup"><span data-stu-id="799fe-165">1</span></span> | <span data-ttu-id="799fe-166">7 </span><span class="sxs-lookup"><span data-stu-id="799fe-166">7</span></span> |
| <span data-ttu-id="799fe-167">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-167">Create conversation</span></span> | <span data-ttu-id="799fe-168">2</span><span class="sxs-lookup"><span data-stu-id="799fe-168">2</span></span> | <span data-ttu-id="799fe-169">8 </span><span class="sxs-lookup"><span data-stu-id="799fe-169">8</span></span> |
| <span data-ttu-id="799fe-170">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-170">Create conversation</span></span> | <span data-ttu-id="799fe-171">30</span><span class="sxs-lookup"><span data-stu-id="799fe-171">30</span></span> | <span data-ttu-id="799fe-172">60</span><span class="sxs-lookup"><span data-stu-id="799fe-172">60</span></span> |
| <span data-ttu-id="799fe-173">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-173">Create conversation</span></span> | <span data-ttu-id="799fe-174">3600</span><span class="sxs-lookup"><span data-stu-id="799fe-174">3600</span></span> | <span data-ttu-id="799fe-175">1800</span><span class="sxs-lookup"><span data-stu-id="799fe-175">1800</span></span> |
| <span data-ttu-id="799fe-176">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-176">Get conversation members</span></span>| <span data-ttu-id="799fe-177">1</span><span class="sxs-lookup"><span data-stu-id="799fe-177">1</span></span> | <span data-ttu-id="799fe-178">14 </span><span class="sxs-lookup"><span data-stu-id="799fe-178">14</span></span> |
| <span data-ttu-id="799fe-179">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-179">Get conversation members</span></span>| <span data-ttu-id="799fe-180">2</span><span class="sxs-lookup"><span data-stu-id="799fe-180">2</span></span> | <span data-ttu-id="799fe-181">16 </span><span class="sxs-lookup"><span data-stu-id="799fe-181">16</span></span> |
| <span data-ttu-id="799fe-182">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-182">Get conversation members</span></span>| <span data-ttu-id="799fe-183">30</span><span class="sxs-lookup"><span data-stu-id="799fe-183">30</span></span> | <span data-ttu-id="799fe-184">120</span><span class="sxs-lookup"><span data-stu-id="799fe-184">120</span></span> |
| <span data-ttu-id="799fe-185">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-185">Get conversation members</span></span>| <span data-ttu-id="799fe-186">3600</span><span class="sxs-lookup"><span data-stu-id="799fe-186">3600</span></span> | <span data-ttu-id="799fe-187">3600</span><span class="sxs-lookup"><span data-stu-id="799fe-187">3600</span></span> |
| <span data-ttu-id="799fe-188">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="799fe-188">Get conversations</span></span> | <span data-ttu-id="799fe-189">1</span><span class="sxs-lookup"><span data-stu-id="799fe-189">1</span></span> | <span data-ttu-id="799fe-190">14 </span><span class="sxs-lookup"><span data-stu-id="799fe-190">14</span></span> |
| <span data-ttu-id="799fe-191">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="799fe-191">Get conversations</span></span> | <span data-ttu-id="799fe-192">2</span><span class="sxs-lookup"><span data-stu-id="799fe-192">2</span></span> | <span data-ttu-id="799fe-193">16 </span><span class="sxs-lookup"><span data-stu-id="799fe-193">16</span></span> |
| <span data-ttu-id="799fe-194">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="799fe-194">Get conversations</span></span> | <span data-ttu-id="799fe-195">30</span><span class="sxs-lookup"><span data-stu-id="799fe-195">30</span></span> | <span data-ttu-id="799fe-196">120</span><span class="sxs-lookup"><span data-stu-id="799fe-196">120</span></span> |
| <span data-ttu-id="799fe-197">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="799fe-197">Get conversations</span></span> | <span data-ttu-id="799fe-198">3600</span><span class="sxs-lookup"><span data-stu-id="799fe-198">3600</span></span> | <span data-ttu-id="799fe-199">3600</span><span class="sxs-lookup"><span data-stu-id="799fe-199">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="799fe-200">Les versions précédentes et les API sont `TeamsInfo.getMembers` en cours `TeamsInfo.GetMembersAsync` d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="799fe-200">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="799fe-201">Ils sont limitées à cinq demandes par minute et retournent un maximum de 10 000 membres par équipe.</span><span class="sxs-lookup"><span data-stu-id="799fe-201">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="799fe-202">Pour mettre à jour votre SDK Bot Framework et le code pour utiliser les derniers points de terminaison de l'API paginée, voir Modifications apportées à l'API bot pour les membres d'équipe et [de conversation.](../../resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="799fe-202">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="799fe-203">Vous pouvez également gérer la limite de taux à l'aide de la limite par thread pour tous les bots.</span><span class="sxs-lookup"><span data-stu-id="799fe-203">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="799fe-204">Limite par thread pour tous les bots</span><span class="sxs-lookup"><span data-stu-id="799fe-204">Per thread limit for all bots</span></span>

<span data-ttu-id="799fe-205">La limite par thread pour tous les bots contrôle le trafic que tous les bots sont autorisés à générer au sein d'une conversation unique.</span><span class="sxs-lookup"><span data-stu-id="799fe-205">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="799fe-206">Une conversation est en tête à tête entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="799fe-206">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="799fe-207">Le tableau suivant fournit la limite par thread pour tous les bots :</span><span class="sxs-lookup"><span data-stu-id="799fe-207">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="799fe-208">Scénario</span><span class="sxs-lookup"><span data-stu-id="799fe-208">Scenario</span></span> | <span data-ttu-id="799fe-209">Période en secondes</span><span class="sxs-lookup"><span data-stu-id="799fe-209">Time period in seconds</span></span> | <span data-ttu-id="799fe-210">Nombre maximal d'opérations autorisées</span><span class="sxs-lookup"><span data-stu-id="799fe-210">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="799fe-211">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-211">Send to conversation</span></span> | <span data-ttu-id="799fe-212">1</span><span class="sxs-lookup"><span data-stu-id="799fe-212">1</span></span> | <span data-ttu-id="799fe-213">14 </span><span class="sxs-lookup"><span data-stu-id="799fe-213">14</span></span> |
| <span data-ttu-id="799fe-214">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-214">Send to conversation</span></span> | <span data-ttu-id="799fe-215">2</span><span class="sxs-lookup"><span data-stu-id="799fe-215">2</span></span> | <span data-ttu-id="799fe-216">16 </span><span class="sxs-lookup"><span data-stu-id="799fe-216">16</span></span> |
| <span data-ttu-id="799fe-217">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-217">Create conversation</span></span> | <span data-ttu-id="799fe-218">1</span><span class="sxs-lookup"><span data-stu-id="799fe-218">1</span></span> | <span data-ttu-id="799fe-219">14 </span><span class="sxs-lookup"><span data-stu-id="799fe-219">14</span></span> |
| <span data-ttu-id="799fe-220">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-220">Create conversation</span></span> | <span data-ttu-id="799fe-221">2</span><span class="sxs-lookup"><span data-stu-id="799fe-221">2</span></span> | <span data-ttu-id="799fe-222">16 </span><span class="sxs-lookup"><span data-stu-id="799fe-222">16</span></span> |
| <span data-ttu-id="799fe-223">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-223">Create conversation</span></span>| <span data-ttu-id="799fe-224">1</span><span class="sxs-lookup"><span data-stu-id="799fe-224">1</span></span> | <span data-ttu-id="799fe-225">14 </span><span class="sxs-lookup"><span data-stu-id="799fe-225">14</span></span> |
| <span data-ttu-id="799fe-226">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-226">Create conversation</span></span>| <span data-ttu-id="799fe-227">2</span><span class="sxs-lookup"><span data-stu-id="799fe-227">2</span></span> | <span data-ttu-id="799fe-228">16 </span><span class="sxs-lookup"><span data-stu-id="799fe-228">16</span></span> |
| <span data-ttu-id="799fe-229">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-229">Get conversation members</span></span>| <span data-ttu-id="799fe-230">1</span><span class="sxs-lookup"><span data-stu-id="799fe-230">1</span></span> | <span data-ttu-id="799fe-231">28</span><span class="sxs-lookup"><span data-stu-id="799fe-231">28</span></span> |
| <span data-ttu-id="799fe-232">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="799fe-232">Get conversation members</span></span>| <span data-ttu-id="799fe-233">2</span><span class="sxs-lookup"><span data-stu-id="799fe-233">2</span></span> | <span data-ttu-id="799fe-234">32</span><span class="sxs-lookup"><span data-stu-id="799fe-234">32</span></span> |
| <span data-ttu-id="799fe-235">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="799fe-235">Get conversations</span></span> | <span data-ttu-id="799fe-236">1</span><span class="sxs-lookup"><span data-stu-id="799fe-236">1</span></span> | <span data-ttu-id="799fe-237">28</span><span class="sxs-lookup"><span data-stu-id="799fe-237">28</span></span> |
| <span data-ttu-id="799fe-238">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="799fe-238">Get conversations</span></span> | <span data-ttu-id="799fe-239">2</span><span class="sxs-lookup"><span data-stu-id="799fe-239">2</span></span> | <span data-ttu-id="799fe-240">32</span><span class="sxs-lookup"><span data-stu-id="799fe-240">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="799fe-241">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="799fe-241">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="799fe-242">Appels et réunions robots</span><span class="sxs-lookup"><span data-stu-id="799fe-242">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

