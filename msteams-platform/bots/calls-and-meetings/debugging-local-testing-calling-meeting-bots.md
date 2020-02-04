---
title: Comment développer des robots d’appels et de réunions en ligne sur votre PC local
description: Découvrez comment vous pouvez également utiliser ngrok pour développer des appels et des robots de réunions en ligne sur votre PC local.
keywords: tunnel ngrok de développement local
ms.date: 11/18/2018
ms.openlocfilehash: b6cd2ba5a3866da8085b3da42377ab9e21f12f5f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673956"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="21f2e-104">Comment développer des robots d’appels et de réunions en ligne sur votre PC local</span><span class="sxs-lookup"><span data-stu-id="21f2e-104">How to develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="21f2e-105">Dans [exécuter et déboguer votre application](../../concepts/build-and-test/debug.md) , nous expliquons comment utiliser [ngrok](https://ngrok.com) pour créer un tunnel entre votre ordinateur local et Internet.</span><span class="sxs-lookup"><span data-stu-id="21f2e-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="21f2e-106">Dans cette rubrique, Découvrez comment vous pouvez également utiliser ngrok et votre PC local pour développer des robots qui prennent en charge les appels et les réunions en ligne.</span><span class="sxs-lookup"><span data-stu-id="21f2e-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="21f2e-107">Les robots de messagerie utilisent le protocole HTTP, mais les appels et les robots de réunion en ligne utilisent le protocole TCP de niveau inférieur.</span><span class="sxs-lookup"><span data-stu-id="21f2e-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="21f2e-108">Ngrok prend en charge les tunnels TCP en plus des tunnels HTTP ; vous découvrirez comment, ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="21f2e-108">Ngrok supports TCP tunnels in addition to HTTP tunnels; you'll learn how, below.</span></span>

## <a name="configuring-ngrokyml"></a><span data-ttu-id="21f2e-109">Configuration de ngrok. yml</span><span class="sxs-lookup"><span data-stu-id="21f2e-109">Configuring ngrok.yml</span></span>

<span data-ttu-id="21f2e-110">Accédez à [ngrok](https://ngrok.com) et inscrivez-vous pour obtenir un compte gratuit ou vous connecter à votre compte existant.</span><span class="sxs-lookup"><span data-stu-id="21f2e-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="21f2e-111">Une fois que vous avez ouvert une session, accédez au [tableau de bord](https://dashboard.ngrok.com) et obtenez votre authToken.</span><span class="sxs-lookup"><span data-stu-id="21f2e-111">Once you've logged in, go to the [dashboard](https://dashboard.ngrok.com) and get your authtoken.</span></span>

<span data-ttu-id="21f2e-112">Créez un `ngrok.yml` [fichier de configuration ngrok (pour plus](https://ngrok.com/docs#config) d’informations sur l’emplacement de ce fichier) et ajoutez la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="21f2e-112">Create an ngrok configuration file `ngrok.yml` (see [here](https://ngrok.com/docs#config) for more information on where this file can be located) and add this line:</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a><span data-ttu-id="21f2e-113">Configuration de la signalisation</span><span class="sxs-lookup"><span data-stu-id="21f2e-113">Setting up signaling</span></span>

<span data-ttu-id="21f2e-114">Dans [les appels et les robots de réunions en ligne](./calls-meetings-bots-overview.md), nous avons abordé la signalisation des appels : comment les robots détectent et répondent aux nouveaux appels et événements au cours d’un appel.</span><span class="sxs-lookup"><span data-stu-id="21f2e-114">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling — how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="21f2e-115">Les événements de signalisation des appels sont envoyés via le protocole HTTP POST au point de terminaison appelant du bot.</span><span class="sxs-lookup"><span data-stu-id="21f2e-115">Call signaling events are sent via HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="21f2e-116">Comme avec l’API de messagerie du bot, pour que la plateforme multimédia en temps réel puisse parler à votre robot, votre robot doit être accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="21f2e-116">As with the bot's messaging API, in order for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="21f2e-117">Ngrok simplifie l’ajout des lignes suivantes à votre Ngrok. yml :</span><span class="sxs-lookup"><span data-stu-id="21f2e-117">Ngrok makes this simple — add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a><span data-ttu-id="21f2e-118">Configuration d’un support local</span><span class="sxs-lookup"><span data-stu-id="21f2e-118">Setting up local media</span></span>

> [!NOTE]
> <span data-ttu-id="21f2e-119">Cette section est uniquement requise pour les robots multimédia hébergés par l’application et peut être ignorée si vous n’hébergez pas de contenu multimédia vous-même.</span><span class="sxs-lookup"><span data-stu-id="21f2e-119">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="21f2e-120">Les supports hébergés par l’application utilisent des certificats et des tunnels TCP.</span><span class="sxs-lookup"><span data-stu-id="21f2e-120">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="21f2e-121">Les étapes suivantes sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="21f2e-121">The following steps are required:</span></span>

- <span data-ttu-id="21f2e-122">Les points de terminaison TCP publics d’Ngrok ont des URL fixes.</span><span class="sxs-lookup"><span data-stu-id="21f2e-122">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="21f2e-123">Il s' `0.tcp.ngrok.io`agit `1.tcp.ngrok.io`de,, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="21f2e-123">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="21f2e-124">Vous devez avoir une entrée DNS CNAMe pour votre service qui pointe vers ces URL.</span><span class="sxs-lookup"><span data-stu-id="21f2e-124">You should have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="21f2e-125">`0.bot.contoso.com` Dans cet exemple, disons qu’il s’agit `0.tcp.ngrok.io`de `1.bot.contoso.com` , fait `1.tcp.ngrok.io`référence à, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="21f2e-125">In this example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
- <span data-ttu-id="21f2e-126">Un certificat SSL est requis pour vos URL.</span><span class="sxs-lookup"><span data-stu-id="21f2e-126">A SSL certificate is required for your URLs.</span></span> <span data-ttu-id="21f2e-127">Pour faciliter l’utilisation d’un certificat SSL délivré à un domaine de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="21f2e-127">To make it easy, use a SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="21f2e-128">Dans ce cas, il s' `*.bot.contoso.com`agit de.</span><span class="sxs-lookup"><span data-stu-id="21f2e-128">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="21f2e-129">Ce certificat SSL étant validé par le kit de développement logiciel (SDK) Media, il doit correspondre à l’URL publique de votre bot.</span><span class="sxs-lookup"><span data-stu-id="21f2e-129">This SSL certificate is validated by the media SDK, so it should match your bot's public URL.</span></span> <span data-ttu-id="21f2e-130">Notez l’empreinte numérique et installez-la dans les certificats de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="21f2e-130">Note the thumbprint and install it in your machine certificates.</span></span>
- <span data-ttu-id="21f2e-131">À présent, configurez un tunnel TCP pour transférer le trafic vers localhost.</span><span class="sxs-lookup"><span data-stu-id="21f2e-131">Now, setup a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="21f2e-132">Écrivez les lignes suivantes dans votre ngrok. yml :</span><span class="sxs-lookup"><span data-stu-id="21f2e-132">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="21f2e-133">Démarrer ngrok</span><span class="sxs-lookup"><span data-stu-id="21f2e-133">Start ngrok</span></span>

<span data-ttu-id="21f2e-134">Maintenant que la configuration de ngrok est prête, lancez-la :</span><span class="sxs-lookup"><span data-stu-id="21f2e-134">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="21f2e-135">Cette opération démarre ngrok et définit les URL publiques qui fournissent les tunnels à votre localhost.</span><span class="sxs-lookup"><span data-stu-id="21f2e-135">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="21f2e-136">La sortie ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="21f2e-136">The output looks like the following:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="21f2e-137">Ici, `12345` est le port de signalisation, `8445` est le port hébergé par l’application et `12332` est le port multimédia distant exposé par ngrok.</span><span class="sxs-lookup"><span data-stu-id="21f2e-137">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="21f2e-138">Notez que nous disposons d’un transfert de `1.bot.contoso.com` vers `1.tcp.ngrok.io`.</span><span class="sxs-lookup"><span data-stu-id="21f2e-138">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="21f2e-139">Il sera utilisé comme l’URL de média pour le bot.</span><span class="sxs-lookup"><span data-stu-id="21f2e-139">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="21f2e-140">Bien entendu, ces numéros de port sont simplement des exemples et vous pouvez utiliser n’importe quel port disponible.</span><span class="sxs-lookup"><span data-stu-id="21f2e-140">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="21f2e-141">Mise à jour du code</span><span class="sxs-lookup"><span data-stu-id="21f2e-141">Update code</span></span>

<span data-ttu-id="21f2e-142">Une fois que ngrok est en cours d’exécution, mettez à jour le code pour utiliser la configuration que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="21f2e-142">Once ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="21f2e-143">Signalisation de mise à jour</span><span class="sxs-lookup"><span data-stu-id="21f2e-143">Update signaling</span></span>

- <span data-ttu-id="21f2e-144">Dans l’appel BotBuilder, modifiez l' `NotificationUrl` URL de signalisation fournie par ngrok.</span><span class="sxs-lookup"><span data-stu-id="21f2e-144">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="21f2e-145">Remplacez le signal par celui fourni par ngrok et `NotificationEndpoint` par le chemin d’accès du contrôleur qui reçoit la notification.</span><span class="sxs-lookup"><span data-stu-id="21f2e-145">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> <span data-ttu-id="21f2e-146">**Important**: l’URL dans `SetNotificationUrl` doit être https.</span><span class="sxs-lookup"><span data-stu-id="21f2e-146">**IMPORTANT**: The URL in `SetNotificationUrl` must be HTTPS.</span></span>

> <span data-ttu-id="21f2e-147">**Important**: votre instance locale doit écouter le trafic http sur le port de signalisation.</span><span class="sxs-lookup"><span data-stu-id="21f2e-147">**IMPORTANT**: Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="21f2e-148">Les demandes effectuées par la plateforme d’appels et de réunions en ligne atteindront le robot comme le trafic HTTP localhost, sauf si le chiffrement de bout en bout est configuré.</span><span class="sxs-lookup"><span data-stu-id="21f2e-148">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="21f2e-149">Mettre à jour le support</span><span class="sxs-lookup"><span data-stu-id="21f2e-149">Update media</span></span>

<span data-ttu-id="21f2e-150">`MediaPlatformSettings` Mettez à jour les éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="21f2e-150">Update your `MediaPlatformSettings` to the following.</span></span>

```csharp
var mediaPlatform = new MediaPlatformSettings
{
    ApplicationId = <Your application id>
    MediaPlatformInstanceSettings = new MediaPlatformInstanceSettings
    {
        CertificateThumbprint = <Your SSL Cert thumbprint>,
        InstanceInternalPort = <Localhost media port>,
        InstancePublicPort = <Ngrok exposed remote media port>,
        InstancePublicIPAddress = new IPAddress(0x0),
        ServiceFqdn = <Media url for bot (eg: 1.bot.contoso.com)>,
    },
}
```

> [!NOTE]
> <span data-ttu-id="21f2e-151">L’empreinte de certificat fournie ci-dessus doit correspondre au nom de domaine complet du service.</span><span class="sxs-lookup"><span data-stu-id="21f2e-151">The certificate thumbprint provided above should match the Service FQDN.</span></span> <span data-ttu-id="21f2e-152">C’est pourquoi les entrées DNS sont requises.</span><span class="sxs-lookup"><span data-stu-id="21f2e-152">That is why the DNS entries are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21f2e-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21f2e-153">Next steps</span></span>

<span data-ttu-id="21f2e-154">Votre robot peut maintenant s’exécuter localement et tous les flux fonctionnent à partir de votre localhost.</span><span class="sxs-lookup"><span data-stu-id="21f2e-154">Your bot can now run locally and all the flows work from your localhost.</span></span>

## <a name="caveats"></a><span data-ttu-id="21f2e-155">Observer lors</span><span class="sxs-lookup"><span data-stu-id="21f2e-155">Caveats</span></span>

- <span data-ttu-id="21f2e-156">Les comptes gratuits Ngrok **ne fournissent pas** de chiffrement de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="21f2e-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="21f2e-157">Les données HTTPs se terminent à l’URL ngrok et les données sont déchiffrées de `localhost`ngrok à.</span><span class="sxs-lookup"><span data-stu-id="21f2e-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="21f2e-158">Si vous avez besoin d’un chiffrement de bout en bout, considérez un compte ngrok payant.</span><span class="sxs-lookup"><span data-stu-id="21f2e-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="21f2e-159">Consultez la rubrique [TLS tunnels](https://ngrok.com/docs#tls) pour obtenir la procédure de configuration de tunnels sécurisés de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="21f2e-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="21f2e-160">Étant donné que l’URL de rappel de bot est dynamique, les scénarios d’appel entrant nécessitent fréquemment de mettre à jour vos points de terminaison ngrok.</span><span class="sxs-lookup"><span data-stu-id="21f2e-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="21f2e-161">Pour résoudre ce problème, vous pouvez utiliser un compte ngrok payant qui fournit des sous-domaines fixes vers lesquels vous pouvez pointer votre robot et la plateforme.</span><span class="sxs-lookup"><span data-stu-id="21f2e-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="21f2e-162">Les tunnels Ngrok peuvent également être utilisés avec [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span><span class="sxs-lookup"><span data-stu-id="21f2e-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="21f2e-163">Pour obtenir un exemple, consultez l' [exemple d’application HueBot](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span><span class="sxs-lookup"><span data-stu-id="21f2e-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
