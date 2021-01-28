---
title: Déboguer votre robot d’appel et de réunion localement
description: Découvrez comment vous pouvez également utiliser ngrok pour développer des appels et des bots de réunion en ligne sur votre PC local.
ms.topic: how-to
keywords: tunnel ngrok de développement local
ms.date: 11/18/2018
ms.openlocfilehash: e9b77df18c8d80f02134dc7912b5796023082039
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014305"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="2e6eb-104">Comment développer des bots d’appels et de réunions en ligne sur votre PC local</span><span class="sxs-lookup"><span data-stu-id="2e6eb-104">How to develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="2e6eb-105">Dans [Exécuter et déboguer votre application,](../../concepts/build-and-test/debug.md) nous expliquons comment utiliser [ngrok](https://ngrok.com) pour créer un tunnel entre votre ordinateur local et Internet.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="2e6eb-106">Dans cette rubrique, découvrez comment vous pouvez également utiliser ngrok et votre PC local pour développer des bots qui prendre en charge les appels et les réunions en ligne.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="2e6eb-107">Les bots de messagerie utilisent le protocole HTTP, mais les appels et les bots de réunion en ligne utilisent le protocole TCP de niveau inférieur.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="2e6eb-108">Ngrok prend en charge les tunnel TCP en plus des tunnelES HTTP ; Vous découvrirez comment, ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-108">Ngrok supports TCP tunnels in addition to HTTP tunnels; you'll learn how, below.</span></span>

## <a name="configuring-ngrokyml"></a><span data-ttu-id="2e6eb-109">Configuration de ngrok.yml</span><span class="sxs-lookup"><span data-stu-id="2e6eb-109">Configuring ngrok.yml</span></span>

<span data-ttu-id="2e6eb-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="2e6eb-111">Une fois que vous êtes connecté, allez dans le tableau [de bord](https://dashboard.ngrok.com) et obtenez votre authtoken.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-111">Once you've logged in, go to the [dashboard](https://dashboard.ngrok.com) and get your authtoken.</span></span>

<span data-ttu-id="2e6eb-112">Créez un fichier de configuration ngrok (voir ici pour plus d’informations sur l’emplacement de ce fichier) et `ngrok.yml` ajoutez cette ligne : [](https://ngrok.com/docs#config)</span><span class="sxs-lookup"><span data-stu-id="2e6eb-112">Create an ngrok configuration file `ngrok.yml` (see [here](https://ngrok.com/docs#config) for more information on where this file can be located) and add this line:</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a><span data-ttu-id="2e6eb-113">Configuration de la signalisation</span><span class="sxs-lookup"><span data-stu-id="2e6eb-113">Setting up signaling</span></span>

<span data-ttu-id="2e6eb-114">Dans [les bots d’appels](./calls-meetings-bots-overview.md)et de réunions en ligne, nous avons abordé la signalisation des appels : comment les bots détectent et répondent aux nouveaux appels et événements au cours d’un appel.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-114">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling — how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="2e6eb-115">Les événements de signalisation d’appel sont envoyés via HTTP POST au point de terminaison d’appel du bot.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-115">Call signaling events are sent via HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="2e6eb-116">Comme avec l’API de messagerie du bot, pour que la plateforme multimédia en temps réel parle à votre bot, celui-ci doit être accessible sur Internet.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-116">As with the bot's messaging API, in order for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="2e6eb-117">Ngrok rend cela simple : ajoutez les lignes suivantes à votre ngrok.yml :</span><span class="sxs-lookup"><span data-stu-id="2e6eb-117">Ngrok makes this simple — add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a><span data-ttu-id="2e6eb-118">Configuration d’un média local</span><span class="sxs-lookup"><span data-stu-id="2e6eb-118">Setting up local media</span></span>

> [!NOTE]
> <span data-ttu-id="2e6eb-119">Cette section est uniquement requise pour les robots multimédias hébergés par l’application et peut être ignorée si vous n’hébergez pas de médias vous-même.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-119">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="2e6eb-120">Le média hébergé par l’application utilise des certificats et des tunnel TCP.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-120">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="2e6eb-121">Les étapes suivantes sont requises :</span><span class="sxs-lookup"><span data-stu-id="2e6eb-121">The following steps are required:</span></span>

- <span data-ttu-id="2e6eb-122">Les points de terminaison TCP publics de Ngrok ont des URL fixes.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-122">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="2e6eb-123">Ils `0.tcp.ngrok.io` `1.tcp.ngrok.io` sont, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-123">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="2e6eb-124">Vous devez avoir une entrée CNAME DNS pour votre service qui pointe vers ces URL.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-124">You should have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="2e6eb-125">Dans cet exemple, supposons que `0.bot.contoso.com` fait référence à , fait référence `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` à, etc.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-125">In this example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
- <span data-ttu-id="2e6eb-126">Un certificat SSL est requis pour vos URL.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-126">A SSL certificate is required for your URLs.</span></span> <span data-ttu-id="2e6eb-127">Pour faciliter la tâche, utilisez un certificat SSL délivré à un domaine de caractères wild card.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-127">To make it easy, use a SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="2e6eb-128">Dans ce cas, ce serait `*.bot.contoso.com` .</span><span class="sxs-lookup"><span data-stu-id="2e6eb-128">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="2e6eb-129">Ce certificat SSL est validé par le SDK multimédia. Il doit donc correspondre à l’URL publique de votre bot.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-129">This SSL certificate is validated by the media SDK, so it should match your bot's public URL.</span></span> <span data-ttu-id="2e6eb-130">Notez l’empreinte numérique et installez-la dans les certificats de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-130">Note the thumbprint and install it in your machine certificates.</span></span>
- <span data-ttu-id="2e6eb-131">À présent, configuration d’un tunnel TCP pour le transport du trafic vers localhost.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-131">Now, setup a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="2e6eb-132">Écrivez les lignes suivantes dans votre ngrok.yml :</span><span class="sxs-lookup"><span data-stu-id="2e6eb-132">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="2e6eb-133">Démarrer ngrok</span><span class="sxs-lookup"><span data-stu-id="2e6eb-133">Start ngrok</span></span>

<span data-ttu-id="2e6eb-134">Maintenant que la configuration ngrok est prête, lancez-la :</span><span class="sxs-lookup"><span data-stu-id="2e6eb-134">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="2e6eb-135">Cela démarre ngrok et définit les URL publiques qui fournissent les tunnel à votre localhost.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-135">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="2e6eb-136">La sortie ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="2e6eb-136">The output looks like the following:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="2e6eb-137">Voici le port de signalisation, le port hébergé par l’application et le port multimédia distant exposé `12345` `8445` par `12332` ngrok.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-137">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="2e6eb-138">Notez que nous avons un forwarding de `1.bot.contoso.com` `1.tcp.ngrok.io` .</span><span class="sxs-lookup"><span data-stu-id="2e6eb-138">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="2e6eb-139">Il sera utilisé comme URL multimédia pour le bot.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-139">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="2e6eb-140">Bien entendu, ces numéros de port ne sont que des exemples et vous pouvez utiliser n’importe quel port disponible.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-140">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="2e6eb-141">Mise à jour du code</span><span class="sxs-lookup"><span data-stu-id="2e6eb-141">Update code</span></span>

<span data-ttu-id="2e6eb-142">Une fois ngrok opérationnel, mettez à jour le code pour utiliser la config que vous viennent de configurer.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-142">Once ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="2e6eb-143">Mise à jour de la signalisation</span><span class="sxs-lookup"><span data-stu-id="2e6eb-143">Update signaling</span></span>

- <span data-ttu-id="2e6eb-144">Dans l’appel botBuilder, modifiez l’URL de signalisation fournie `NotificationUrl` par ngrok.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-144">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="2e6eb-145">Remplacez le signal par celui fourni par ngrok et par le chemin d’accès du contrôleur `NotificationEndpoint` qui reçoit la notification.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-145">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> <span data-ttu-id="2e6eb-146">**IMPORTANT**: l’URL `SetNotificationUrl` doit être HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-146">**IMPORTANT**: The URL in `SetNotificationUrl` must be HTTPS.</span></span>

> <span data-ttu-id="2e6eb-147">**IMPORTANT**: votre instance locale doit être à l’écoute du trafic HTTP sur le port de signalisation.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-147">**IMPORTANT**: Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="2e6eb-148">Les demandes faites par la plateforme d’appels et de réunions en ligne atteindront le bot en tant que trafic HTTP localhost, sauf si le chiffrement de bout en bout est installé.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-148">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="2e6eb-149">Mettre à jour un support</span><span class="sxs-lookup"><span data-stu-id="2e6eb-149">Update media</span></span>

<span data-ttu-id="2e6eb-150">Mettez à `MediaPlatformSettings` jour les informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-150">Update your `MediaPlatformSettings` to the following.</span></span>

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
> <span data-ttu-id="2e6eb-151">L’empreinte numérique du certificat fournie ci-dessus doit correspondre au FQDN du service.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-151">The certificate thumbprint provided above should match the Service FQDN.</span></span> <span data-ttu-id="2e6eb-152">C’est pourquoi les entrées DNS sont requises.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-152">That is why the DNS entries are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e6eb-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2e6eb-153">Next steps</span></span>

<span data-ttu-id="2e6eb-154">Votre bot peut désormais s’exécuter localement et tous les flux fonctionnent à partir de votre localhost.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-154">Your bot can now run locally and all the flows work from your localhost.</span></span>

## <a name="caveats"></a><span data-ttu-id="2e6eb-155">Avertissements</span><span class="sxs-lookup"><span data-stu-id="2e6eb-155">Caveats</span></span>

- <span data-ttu-id="2e6eb-156">Les comptes gratuits Ngrok **ne fournissent** pas de chiffrement de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="2e6eb-157">Les données HTTPS se terminent à l’URL ngrok et les données sont non chiffrées de ngrok vers `localhost` .</span><span class="sxs-lookup"><span data-stu-id="2e6eb-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="2e6eb-158">Si vous avez besoin d’un chiffrement de bout en bout, envisagez un compte ngrok payant.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="2e6eb-159">Consultez [les tunnel TLS pour](https://ngrok.com/docs#tls) obtenir la procédure de configuration des tunnel de bout en bout sécurisés.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="2e6eb-160">Étant donné que l’URL de rappel du bot est dynamique, les scénarios d’appels entrants nécessitent que vous mettez fréquemment à jour vos points de terminaison ngrok.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="2e6eb-161">Une façon de résoudre ce problème consiste à utiliser un compte ngrok payant qui fournit des sous-domaine fixes vers lesquels vous pouvez pointer votre bot et la plateforme.</span><span class="sxs-lookup"><span data-stu-id="2e6eb-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="2e6eb-162">Les tunneles Ngrok peuvent également être utilisés [avec Azure Service Fabric.](/azure/service-fabric/service-fabric-overview)</span><span class="sxs-lookup"><span data-stu-id="2e6eb-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="2e6eb-163">Pour obtenir un exemple de la façon de le faire, voir l’exemple [d’application HueBot.](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)</span><span class="sxs-lookup"><span data-stu-id="2e6eb-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
