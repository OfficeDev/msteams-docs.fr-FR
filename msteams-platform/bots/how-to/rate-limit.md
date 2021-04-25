---
title: Optimisez votre robot grâce à la limitation du débit dans Teams
description: Limitation des taux et meilleures pratiques dans Microsoft Teams
ms.topic: conceptual
keywords: Limitation des taux de bots teams
ms.openlocfilehash: 9a30d86a82a591c4a1125632fa7409780effb269
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995854"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="a15c4-104">Optimisez votre robot grâce à la limitation du débit dans Teams</span><span class="sxs-lookup"><span data-stu-id="a15c4-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="a15c4-105">La limitation des taux est une méthode pour limiter les messages à une certaine fréquence maximale.</span><span class="sxs-lookup"><span data-stu-id="a15c4-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="a15c4-106">En règle générale, votre application doit limiter le nombre de messages qu'elle publie à une conversation individuelle ou à une conversation de canal.</span><span class="sxs-lookup"><span data-stu-id="a15c4-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="a15c4-107">Cela garantit une expérience optimale et les messages n'apparaissent pas comme courrier indésirable pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a15c4-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="a15c4-108">Pour protéger Microsoft Teams et ses utilisateurs, les API de bot fournissent une limite de taux pour les demandes entrantes.</span><span class="sxs-lookup"><span data-stu-id="a15c4-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="a15c4-109">Les applications qui vont au-dessus de cette limite reçoivent un `HTTP 429 Too Many Requests` état d'erreur.</span><span class="sxs-lookup"><span data-stu-id="a15c4-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="a15c4-110">Toutes les demandes sont soumises à la même stratégie de limitation des taux, y compris l'envoi de messages, les listes d'envoi et les extractions de listes.</span><span class="sxs-lookup"><span data-stu-id="a15c4-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="a15c4-111">Comme les valeurs exactes des limites de taux sont sujettes à modification, votre application doit implémenter le comportement d'insé backoff approprié lorsque l'API renvoie `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="a15c4-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="a15c4-112">Gérer les limites de taux</span><span class="sxs-lookup"><span data-stu-id="a15c4-112">Handle rate limits</span></span>

<span data-ttu-id="a15c4-113">Lors de l'émission d'une opération du SDK Bot Builder, vous pouvez gérer et `Microsoft.Rest.HttpOperationException` vérifier le code d'état.</span><span class="sxs-lookup"><span data-stu-id="a15c4-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="a15c4-114">Le code suivant illustre un exemple de gestion des limites de taux :</span><span class="sxs-lookup"><span data-stu-id="a15c4-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="a15c4-115">Une fois que vous avez géré les limites de taux pour les bots, vous pouvez gérer les réponses à l'aide `HTTP 429` d'un retour exponentiel.</span><span class="sxs-lookup"><span data-stu-id="a15c4-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="a15c4-116">Gérer les `HTTP 429` réponses</span><span class="sxs-lookup"><span data-stu-id="a15c4-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="a15c4-117">En règle générale, vous devez prendre des précautions simples pour éviter de recevoir des `HTTP 429` réponses.</span><span class="sxs-lookup"><span data-stu-id="a15c4-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="a15c4-118">Par exemple, évitez d'émettre plusieurs demandes à la même conversation personnelle ou de canal.</span><span class="sxs-lookup"><span data-stu-id="a15c4-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="a15c4-119">Créez plutôt un lot de demandes d'API.</span><span class="sxs-lookup"><span data-stu-id="a15c4-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="a15c4-120">Il est recommandé d'utiliser un retour exponentiel avec une gigue aléatoire pour gérer les 429.</span><span class="sxs-lookup"><span data-stu-id="a15c4-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="a15c4-121">Cela garantit que plusieurs demandes n'introduisent pas de collisions lors des nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="a15c4-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="a15c4-122">Une fois que vous `HTTP 429` avez géré les réponses, vous pouvez passer par l'exemple pour détecter les exceptions temporaires.</span><span class="sxs-lookup"><span data-stu-id="a15c4-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

> [!NOTE]
> <span data-ttu-id="a15c4-123">En plus de resserrer le code **d'erreur 429**, les codes d'erreur **412,** **502** et **504** doivent également être retentés.</span><span class="sxs-lookup"><span data-stu-id="a15c4-123">In addition to retyring error code **429**, error codes **412**, **502**, and **504** must also be retried.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="a15c4-124">Exemple de détection d'exceptions temporaires</span><span class="sxs-lookup"><span data-stu-id="a15c4-124">Detect transient exceptions example</span></span>

<span data-ttu-id="a15c4-125">Le code suivant illustre un exemple d'utilisation du blocage exponentiel à l'aide du bloc d'application de gestion des pannes temporaires :</span><span class="sxs-lookup"><span data-stu-id="a15c4-125">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="a15c4-126">Vous pouvez effectuer des tentatives de retour et des tentatives à l'aide de [la gestion des erreurs temporaires.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)</span><span class="sxs-lookup"><span data-stu-id="a15c4-126">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="a15c4-127">Pour obtenir des instructions sur l'obtention et l'installation du package NuGet, voir l'ajout du bloc d'application de gestion des erreurs [temporaires à votre solution.](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="a15c4-127">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="a15c4-128">Voir aussi [la gestion des erreurs temporaires.](/azure/architecture/best-practices/transient-faults)</span><span class="sxs-lookup"><span data-stu-id="a15c4-128">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="a15c4-129">Après avoir passé en détail l'exemple de détection des exceptions temporaires, prenons l'exemple de la fonction de retour exponentiel.</span><span class="sxs-lookup"><span data-stu-id="a15c4-129">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="a15c4-130">Vous pouvez utiliser l'arrêt exponentiel au lieu de réessayer en cas d'échec.</span><span class="sxs-lookup"><span data-stu-id="a15c4-130">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="a15c4-131">Exemple de mise en arrière</span><span class="sxs-lookup"><span data-stu-id="a15c4-131">Backoff example</span></span>

<span data-ttu-id="a15c4-132">En plus de détecter les limites de taux, vous pouvez également effectuer une coupure exponentielle.</span><span class="sxs-lookup"><span data-stu-id="a15c4-132">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="a15c4-133">Le code suivant illustre un exemple de coupure exponentielle :</span><span class="sxs-lookup"><span data-stu-id="a15c4-133">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="a15c4-134">Vous pouvez également exécuter une méthode `System.Action` avec la stratégie de nouvelle tentative décrite dans cette section.</span><span class="sxs-lookup"><span data-stu-id="a15c4-134">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="a15c4-135">La bibliothèque référencé vous permet également de spécifier un intervalle fixe ou un mécanisme d'interruption linéaire.</span><span class="sxs-lookup"><span data-stu-id="a15c4-135">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="a15c4-136">Stockez la valeur et la stratégie dans un fichier de configuration pour affiner et ajuster les valeurs au moment de l'exécuter.</span><span class="sxs-lookup"><span data-stu-id="a15c4-136">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="a15c4-137">Pour plus d'informations, [voir les modèles de nouvelle tentative.](/azure/architecture/patterns/retry)</span><span class="sxs-lookup"><span data-stu-id="a15c4-137">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="a15c4-138">Vous pouvez également gérer la limite de taux à l'aide de la limite par bot par thread.</span><span class="sxs-lookup"><span data-stu-id="a15c4-138">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="a15c4-139">Par bot par limite de thread</span><span class="sxs-lookup"><span data-stu-id="a15c4-139">Per bot per thread limit</span></span>

<span data-ttu-id="a15c4-140">La limite par bot par thread contrôle le trafic qu'un bot est autorisé à générer dans une seule conversation.</span><span class="sxs-lookup"><span data-stu-id="a15c4-140">The per bot per thread limit controls the traffic that a bot is allowed to generate in a single conversation.</span></span> <span data-ttu-id="a15c4-141">Une conversation est 1:1 entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="a15c4-141">A conversation is 1:1 between bot and user, a group chat, or a channel in a team.</span></span> <span data-ttu-id="a15c4-142">Ainsi, si l'application envoie un message bot à chaque utilisateur, la limite de thread ne se limite pas.</span><span class="sxs-lookup"><span data-stu-id="a15c4-142">So, if the application sends one bot message to each user, the thread limit does not throttle.</span></span>

>[!NOTE]
> * <span data-ttu-id="a15c4-143">La limite de thread de 3 600 secondes et 1 800 opérations s'applique uniquement si plusieurs messages de bot sont envoyés à un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a15c4-143">The thread limit of 3600 seconds and 1800 operations applies only if multiple bot messages are sent to a single user.</span></span> 
> * <span data-ttu-id="a15c4-144">La limite globale par application et par client est de 30 demandes par seconde (DEMANDES/s).</span><span class="sxs-lookup"><span data-stu-id="a15c4-144">The global limit per app per tenant is 30 Requests Per Second (RPS).</span></span> <span data-ttu-id="a15c4-145">Par conséquent, le nombre total de messages de bot par seconde ne doit pas franchir la limite de thread.</span><span class="sxs-lookup"><span data-stu-id="a15c4-145">Hence, the total number of bot messages per second must not cross the thread limit.</span></span>
> * <span data-ttu-id="a15c4-146">Le fractionnement des messages au niveau du service entraîne un nombre de rps supérieur aux attentes.</span><span class="sxs-lookup"><span data-stu-id="a15c4-146">Message splitting at the service level results in higher than expected RPS.</span></span> <span data-ttu-id="a15c4-147">Si vous êtes préoccupé par l'approche des limites, vous devez implémenter la stratégie [de retour à la limite.](#backoff-example)</span><span class="sxs-lookup"><span data-stu-id="a15c4-147">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="a15c4-148">Les valeurs fournies dans cette section sont uniquement à des valeurs d'estimation.</span><span class="sxs-lookup"><span data-stu-id="a15c4-148">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="a15c4-149">Le tableau suivant fournit les limites par bot par thread :</span><span class="sxs-lookup"><span data-stu-id="a15c4-149">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="a15c4-150">Scénario</span><span class="sxs-lookup"><span data-stu-id="a15c4-150">Scenario</span></span> | <span data-ttu-id="a15c4-151">Période en secondes</span><span class="sxs-lookup"><span data-stu-id="a15c4-151">Time period in seconds</span></span> | <span data-ttu-id="a15c4-152">Nombre maximal d'opérations autorisées</span><span class="sxs-lookup"><span data-stu-id="a15c4-152">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a15c4-153">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-153">Send to conversation</span></span> | <span data-ttu-id="a15c4-154">1</span><span class="sxs-lookup"><span data-stu-id="a15c4-154">1</span></span> | <span data-ttu-id="a15c4-155">7 </span><span class="sxs-lookup"><span data-stu-id="a15c4-155">7</span></span> |
| <span data-ttu-id="a15c4-156">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-156">Send to conversation</span></span> | <span data-ttu-id="a15c4-157">2</span><span class="sxs-lookup"><span data-stu-id="a15c4-157">2</span></span> | <span data-ttu-id="a15c4-158">8 </span><span class="sxs-lookup"><span data-stu-id="a15c4-158">8</span></span> |
| <span data-ttu-id="a15c4-159">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-159">Send to conversation</span></span> | <span data-ttu-id="a15c4-160">30</span><span class="sxs-lookup"><span data-stu-id="a15c4-160">30</span></span> | <span data-ttu-id="a15c4-161">60</span><span class="sxs-lookup"><span data-stu-id="a15c4-161">60</span></span> |
| <span data-ttu-id="a15c4-162">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-162">Send to conversation</span></span> | <span data-ttu-id="a15c4-163">3600</span><span class="sxs-lookup"><span data-stu-id="a15c4-163">3600</span></span> | <span data-ttu-id="a15c4-164">1800</span><span class="sxs-lookup"><span data-stu-id="a15c4-164">1800</span></span> |
| <span data-ttu-id="a15c4-165">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-165">Create conversation</span></span> | <span data-ttu-id="a15c4-166">1</span><span class="sxs-lookup"><span data-stu-id="a15c4-166">1</span></span> | <span data-ttu-id="a15c4-167">7 </span><span class="sxs-lookup"><span data-stu-id="a15c4-167">7</span></span> |
| <span data-ttu-id="a15c4-168">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-168">Create conversation</span></span> | <span data-ttu-id="a15c4-169">2</span><span class="sxs-lookup"><span data-stu-id="a15c4-169">2</span></span> | <span data-ttu-id="a15c4-170">8 </span><span class="sxs-lookup"><span data-stu-id="a15c4-170">8</span></span> |
| <span data-ttu-id="a15c4-171">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-171">Create conversation</span></span> | <span data-ttu-id="a15c4-172">30</span><span class="sxs-lookup"><span data-stu-id="a15c4-172">30</span></span> | <span data-ttu-id="a15c4-173">60</span><span class="sxs-lookup"><span data-stu-id="a15c4-173">60</span></span> |
| <span data-ttu-id="a15c4-174">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-174">Create conversation</span></span> | <span data-ttu-id="a15c4-175">3600</span><span class="sxs-lookup"><span data-stu-id="a15c4-175">3600</span></span> | <span data-ttu-id="a15c4-176">1800</span><span class="sxs-lookup"><span data-stu-id="a15c4-176">1800</span></span> |
| <span data-ttu-id="a15c4-177">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-177">Get conversation members</span></span>| <span data-ttu-id="a15c4-178">1</span><span class="sxs-lookup"><span data-stu-id="a15c4-178">1</span></span> | <span data-ttu-id="a15c4-179">14 </span><span class="sxs-lookup"><span data-stu-id="a15c4-179">14</span></span> |
| <span data-ttu-id="a15c4-180">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-180">Get conversation members</span></span>| <span data-ttu-id="a15c4-181">2</span><span class="sxs-lookup"><span data-stu-id="a15c4-181">2</span></span> | <span data-ttu-id="a15c4-182">16 </span><span class="sxs-lookup"><span data-stu-id="a15c4-182">16</span></span> |
| <span data-ttu-id="a15c4-183">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-183">Get conversation members</span></span>| <span data-ttu-id="a15c4-184">30</span><span class="sxs-lookup"><span data-stu-id="a15c4-184">30</span></span> | <span data-ttu-id="a15c4-185">120</span><span class="sxs-lookup"><span data-stu-id="a15c4-185">120</span></span> |
| <span data-ttu-id="a15c4-186">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-186">Get conversation members</span></span>| <span data-ttu-id="a15c4-187">3600</span><span class="sxs-lookup"><span data-stu-id="a15c4-187">3600</span></span> | <span data-ttu-id="a15c4-188">3600</span><span class="sxs-lookup"><span data-stu-id="a15c4-188">3600</span></span> |
| <span data-ttu-id="a15c4-189">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="a15c4-189">Get conversations</span></span> | <span data-ttu-id="a15c4-190">1</span><span class="sxs-lookup"><span data-stu-id="a15c4-190">1</span></span> | <span data-ttu-id="a15c4-191">14 </span><span class="sxs-lookup"><span data-stu-id="a15c4-191">14</span></span> |
| <span data-ttu-id="a15c4-192">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="a15c4-192">Get conversations</span></span> | <span data-ttu-id="a15c4-193">2</span><span class="sxs-lookup"><span data-stu-id="a15c4-193">2</span></span> | <span data-ttu-id="a15c4-194">16 </span><span class="sxs-lookup"><span data-stu-id="a15c4-194">16</span></span> |
| <span data-ttu-id="a15c4-195">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="a15c4-195">Get conversations</span></span> | <span data-ttu-id="a15c4-196">30</span><span class="sxs-lookup"><span data-stu-id="a15c4-196">30</span></span> | <span data-ttu-id="a15c4-197">120</span><span class="sxs-lookup"><span data-stu-id="a15c4-197">120</span></span> |
| <span data-ttu-id="a15c4-198">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="a15c4-198">Get conversations</span></span> | <span data-ttu-id="a15c4-199">3600</span><span class="sxs-lookup"><span data-stu-id="a15c4-199">3600</span></span> | <span data-ttu-id="a15c4-200">3600</span><span class="sxs-lookup"><span data-stu-id="a15c4-200">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="a15c4-201">Les versions précédentes et les API sont `TeamsInfo.getMembers` en cours `TeamsInfo.GetMembersAsync` d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="a15c4-201">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="a15c4-202">Ils sont limitées à cinq demandes par minute et retournent un maximum de 10 000 membres par équipe.</span><span class="sxs-lookup"><span data-stu-id="a15c4-202">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="a15c4-203">Pour mettre à jour votre SDK Bot Framework et le code pour utiliser les derniers points de terminaison de l'API paginée, voir Modifications apportées à l'API bot pour les membres de l'équipe [et de la conversation.](../../resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="a15c4-203">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="a15c4-204">Vous pouvez également gérer la limite de taux à l'aide de la limite par thread pour tous les bots.</span><span class="sxs-lookup"><span data-stu-id="a15c4-204">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="a15c4-205">Limite par thread pour tous les bots</span><span class="sxs-lookup"><span data-stu-id="a15c4-205">Per thread limit for all bots</span></span>

<span data-ttu-id="a15c4-206">La limite par thread pour tous les bots contrôle le trafic que tous les bots sont autorisés à générer dans une conversation unique.</span><span class="sxs-lookup"><span data-stu-id="a15c4-206">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="a15c4-207">Une conversation est en tête à tête entre un bot et un utilisateur, une conversation de groupe ou un canal dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="a15c4-207">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="a15c4-208">Le tableau suivant fournit la limite par thread pour tous les bots :</span><span class="sxs-lookup"><span data-stu-id="a15c4-208">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="a15c4-209">Scénario</span><span class="sxs-lookup"><span data-stu-id="a15c4-209">Scenario</span></span> | <span data-ttu-id="a15c4-210">Période en secondes</span><span class="sxs-lookup"><span data-stu-id="a15c4-210">Time period in seconds</span></span> | <span data-ttu-id="a15c4-211">Nombre maximal d'opérations autorisées</span><span class="sxs-lookup"><span data-stu-id="a15c4-211">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a15c4-212">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-212">Send to conversation</span></span> | <span data-ttu-id="a15c4-213">1</span><span class="sxs-lookup"><span data-stu-id="a15c4-213">1</span></span> | <span data-ttu-id="a15c4-214">14 </span><span class="sxs-lookup"><span data-stu-id="a15c4-214">14</span></span> |
| <span data-ttu-id="a15c4-215">Envoyer à la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-215">Send to conversation</span></span> | <span data-ttu-id="a15c4-216">2</span><span class="sxs-lookup"><span data-stu-id="a15c4-216">2</span></span> | <span data-ttu-id="a15c4-217">16 </span><span class="sxs-lookup"><span data-stu-id="a15c4-217">16</span></span> |
| <span data-ttu-id="a15c4-218">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-218">Create conversation</span></span> | <span data-ttu-id="a15c4-219">1</span><span class="sxs-lookup"><span data-stu-id="a15c4-219">1</span></span> | <span data-ttu-id="a15c4-220">14 </span><span class="sxs-lookup"><span data-stu-id="a15c4-220">14</span></span> |
| <span data-ttu-id="a15c4-221">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-221">Create conversation</span></span> | <span data-ttu-id="a15c4-222">2</span><span class="sxs-lookup"><span data-stu-id="a15c4-222">2</span></span> | <span data-ttu-id="a15c4-223">16 </span><span class="sxs-lookup"><span data-stu-id="a15c4-223">16</span></span> |
| <span data-ttu-id="a15c4-224">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-224">Create conversation</span></span>| <span data-ttu-id="a15c4-225">1</span><span class="sxs-lookup"><span data-stu-id="a15c4-225">1</span></span> | <span data-ttu-id="a15c4-226">14 </span><span class="sxs-lookup"><span data-stu-id="a15c4-226">14</span></span> |
| <span data-ttu-id="a15c4-227">Créer une conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-227">Create conversation</span></span>| <span data-ttu-id="a15c4-228">2</span><span class="sxs-lookup"><span data-stu-id="a15c4-228">2</span></span> | <span data-ttu-id="a15c4-229">16 </span><span class="sxs-lookup"><span data-stu-id="a15c4-229">16</span></span> |
| <span data-ttu-id="a15c4-230">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-230">Get conversation members</span></span>| <span data-ttu-id="a15c4-231">1</span><span class="sxs-lookup"><span data-stu-id="a15c4-231">1</span></span> | <span data-ttu-id="a15c4-232">28</span><span class="sxs-lookup"><span data-stu-id="a15c4-232">28</span></span> |
| <span data-ttu-id="a15c4-233">Obtenir les membres de la conversation</span><span class="sxs-lookup"><span data-stu-id="a15c4-233">Get conversation members</span></span>| <span data-ttu-id="a15c4-234">2</span><span class="sxs-lookup"><span data-stu-id="a15c4-234">2</span></span> | <span data-ttu-id="a15c4-235">32</span><span class="sxs-lookup"><span data-stu-id="a15c4-235">32</span></span> |
| <span data-ttu-id="a15c4-236">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="a15c4-236">Get conversations</span></span> | <span data-ttu-id="a15c4-237">1</span><span class="sxs-lookup"><span data-stu-id="a15c4-237">1</span></span> | <span data-ttu-id="a15c4-238">28</span><span class="sxs-lookup"><span data-stu-id="a15c4-238">28</span></span> |
| <span data-ttu-id="a15c4-239">Obtenir des conversations</span><span class="sxs-lookup"><span data-stu-id="a15c4-239">Get conversations</span></span> | <span data-ttu-id="a15c4-240">2</span><span class="sxs-lookup"><span data-stu-id="a15c4-240">2</span></span> | <span data-ttu-id="a15c4-241">32</span><span class="sxs-lookup"><span data-stu-id="a15c4-241">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="a15c4-242">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="a15c4-242">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a15c4-243">Appels et réunions robots</span><span class="sxs-lookup"><span data-stu-id="a15c4-243">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

