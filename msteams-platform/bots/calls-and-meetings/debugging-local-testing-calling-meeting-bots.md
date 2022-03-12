---
title: Déboguer votre robot d’appel et de réunion localement
description: Découvrez comment vous pouvez également utiliser ngrok pour développer des appels et des bots de réunion en ligne sur votre PC local.
ms.topic: how-to
ms.localizationpriority: medium
keywords: tunnel ngrok de développement local
ms.date: 11/18/2018
ms.openlocfilehash: c55ec6e5d7296f4ee04ae3ad3de0f9bb82cfd276
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453361"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Développer des bots d’appels et de réunion en ligne sur votre PC local

Dans [Exécuter et déboguer votre application](../../concepts/build-and-test/debug.md) , nous expliquons comment utiliser [ngrok](https://ngrok.com) pour créer un tunnel entre votre ordinateur local et Internet. Dans cette rubrique, découvrez comment utiliser ngrok et votre PC local pour développer des bots qui peuvent prendre en charge les appels et les réunions en ligne.

Les bots de messagerie utilisent le protocole HTTP, mais les appels et les bots de réunion en ligne utilisent le protocole TCP de niveau inférieur. Ngrok prend en charge les tunnel TCP en plus des tunnelES HTTP.

## <a name="configure-ngrokyml"></a>Configurer ngrok.yml

Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account. Une fois que vous vous êtes inscrit, allez dans le tableau [de bord](https://dashboard.ngrok.com) et obtenez votre jeton d’th.

Créez un fichier de configuration `ngrok.yml` ngrok et ajoutez la ligne suivante. Pour plus d’informations sur l’emplacement du fichier, voir [ngrok](https://ngrok.com/docs#config) :

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>Configurer la signalisation

Dans [les bots](./calls-meetings-bots-overview.md) d’appels et de réunions en ligne, nous avons abordé la signalisation d’appel sur la façon dont les bots détectent et répondent aux nouveaux appels et événements au cours d’un appel. Les événements de signalisation d’appel sont envoyés via HTTP POST au point de terminaison d’appel du bot.

Comme avec l’API de messagerie du bot, pour que la plateforme multimédia en temps réel parle à votre bot, votre bot doit être accessible sur Internet. Ngrok rend cela simple. Ajoutez les lignes suivantes à votre ngrok.yml :

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>Configurer un média local

> [!NOTE]
> Cette section est uniquement requise pour les robots multimédias hébergés par l’application et peut être ignorée si vous n’hébergez pas vous-même le média.

Le média hébergé par l’application utilise des certificats et des tunnel TCP. Les étapes suivantes sont requises :

1. Les points de terminaison TCP publics de Ngrok ont des URL fixes. Ils sont `0.tcp.ngrok.io`, `1.tcp.ngrok.io`et ainsi de suite. Vous devez avoir une entrée CNAME DNS pour votre service qui pointe vers ces URL. Par exemple, supposons que fait `0.bot.contoso.com` référence à `0.tcp.ngrok.io`, `1.bot.contoso.com` fait `1.tcp.ngrok.io`référence à, et ainsi de suite.
2. Un certificat SSL est requis pour vos URL. Pour faciliter la tâche, utilisez un certificat SSL délivré à un domaine de caractères wild card. Dans ce cas, ce serait `*.bot.contoso.com`. Ce certificat SSL est validé par le SDK multimédia, il doit donc correspondre à l’URL publique de votre bot. Notez l’empreinte numérique et installez-la dans les certificats de votre ordinateur.
3. À présent, définissez un tunnel TCP pour que le trafic soit transmis à l’host local. Écrivez les lignes suivantes dans votre ngrok.yml :

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Démarrer ngrok

Maintenant que la configuration ngrok est prête, lancez-la :

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

Cela démarre ngrok et définit les URL publiques qui fournissent les tunnel à votre localhost. Voici un exemple de sortie :

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

Voici le `12345` port de signalisation, `8445` le port hébergé par l’application et `12332` le port multimédia distant exposé par ngrok. Notez que nous avons un forwarding de `1.bot.contoso.com` .`1.tcp.ngrok.io` Il sera utilisé comme URL multimédia pour le bot. Bien entendu, ces numéros de port ne sont que des exemples et vous pouvez utiliser n’importe quel port disponible.

### <a name="update-code"></a>Mise à jour du code

Une fois ngrok opérationnel, mettez à jour le code pour utiliser la config que vous viennent de configurer.

#### <a name="update-signaling"></a>Mise à jour de la signalisation

Dans l’appel botBuilder, modifiez l’URL `NotificationUrl` de signalisation fournie par ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Remplacez le signal par celui fourni par ngrok `NotificationEndpoint` et par le chemin d’accès du contrôleur qui reçoit la notification.

> [!IMPORTANT]
>
> * L’URL doit `SetNotificationUrl` être HTTPS.
>
> Votre instance locale doit être à l’écoute du trafic HTTP sur le port de signalisation. Les demandes faites par la plateforme d’appels et de réunions en ligne atteindront le bot en tant que trafic HTTP localhost, sauf si le chiffrement de bout en bout est installé.

#### <a name="update-media"></a>Mettre à jour le média

Mettez à jour les informations `MediaPlatformSettings` suivantes :

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
> L’empreinte numérique du certificat fournie dans le doit `MediaPlatformSettings` correspondre au FQDN du service. C’est pourquoi les entrées DNS sont requises.

## <a name="caveats"></a>Avertissements

* Les comptes gratuits Ngrok **ne fournissent** pas de chiffrement de bout en bout. Les données HTTPS se terminent à l’URL ngrok et les données sont non chiffrées de ngrok à `localhost`. Si vous avez besoin d’un chiffrement de bout en bout, envisagez un compte ngrok payant. Voir [les tunneles TLS](https://ngrok.com/docs#tls) pour obtenir la procédure de configuration des tunnel de bout en bout sécurisés.
* Étant donné que l’URL de rappel du bot est dynamique, les scénarios d’appels entrants nécessitent que vous mettez fréquemment à jour vos points de terminaison ngrok. Une façon de résoudre ce problème consiste à utiliser un compte ngrok payant qui fournit des sous-domaine fixes vers lesquels vous pouvez pointer votre bot et la plateforme.
* Les tunneles Ngrok peuvent également être utilisés avec [Azure Service Fabric](/azure/service-fabric/service-fabric-overview). Pour obtenir un exemple de la façon de le faire, voir [l’exemple d’application HueBot](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples/HueBot/HueBot).
