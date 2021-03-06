---
title: Déboguer votre robot d’appel et de réunion localement
description: Découvrez comment vous pouvez également utiliser ngrok pour développer des appels et des bots de réunion en ligne sur votre PC local.
ms.topic: how-to
localization_priority: Normal
keywords: tunnel ngrok de développement local
ms.date: 11/18/2018
ms.openlocfilehash: 0f29f77e5030a7dbef9e8f7cefae4e055b7cc5b5
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020161"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Développer des bots d’appels et de réunion en ligne sur votre PC local

Dans [Exécuter et déboguer votre application,](../../concepts/build-and-test/debug.md) nous expliquons comment utiliser [ngrok](https://ngrok.com) pour créer un tunnel entre votre ordinateur local et Internet. Dans cette rubrique, découvrez comment vous pouvez également utiliser ngrok et votre PC local pour développer des bots qui prendre en charge les appels et les réunions en ligne.

Les bots de messagerie utilisent le protocole HTTP, mais les appels et les bots de réunion en ligne utilisent le protocole TCP de niveau inférieur. Ngrok prend en charge les tunnel TCP en plus des tunnelES HTTP. 

## <a name="configure-ngrokyml"></a>Configurer ngrok.yml

Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account. Une fois que vous vous êtes inscrit, allez dans le tableau [de bord](https://dashboard.ngrok.com) et obtenez votre jeton d’th.

Créez un fichier de configuration ngrok `ngrok.yml` et ajoutez la ligne suivante. Pour plus d’informations sur l’emplacement du fichier, voir [ngrok](https://ngrok.com/docs#config):

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>Configurer la signalisation

Dans [les bots d’appels](./calls-meetings-bots-overview.md)et de réunions en ligne, nous avons abordé la signalisation des appels sur la façon dont les bots détectent et répondent aux nouveaux appels et événements au cours d’un appel. Les événements de signalisation d’appel sont envoyés via HTTP POST au point de terminaison d’appel du bot.

Comme avec l’API de messagerie du bot, pour que la plateforme multimédia en temps réel parle à votre bot, votre bot doit être accessible sur Internet. Ngrok rend cela simple. Ajoutez les lignes suivantes à votre ngrok.yml :

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>Configurer un média local

> [!NOTE]
> Cette section est uniquement requise pour les robots multimédias hébergés par l’application et peut être ignorée si vous n’hébergez pas de médias vous-même.

Le média hébergé par l’application utilise des certificats et des tunnel TCP. Les étapes suivantes sont requises :

1. Les points de terminaison TCP publics de Ngrok ont des URL fixes. Ils `0.tcp.ngrok.io` `1.tcp.ngrok.io` sont, et ainsi de suite. Vous devez avoir une entrée CNAME DNS pour votre service qui pointe vers ces URL. Par exemple, supposons que `0.bot.contoso.com` fait référence à , fait référence `0.tcp.ngrok.io` `1.bot.contoso.com` `1.tcp.ngrok.io` à, et ainsi de suite.
2. Un certificat SSL est requis pour vos URL. Pour faciliter la tâche, utilisez un certificat SSL délivré à un domaine de caractères wild card. Dans ce cas, ce serait `*.bot.contoso.com` . Ce certificat SSL est validé par le SDK multimédia, il doit donc correspondre à l’URL publique de votre bot. Notez l’empreinte numérique et installez-la dans les certificats de votre ordinateur.
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

Voici le port de signalisation, le port hébergé par l’application et le port multimédia distant exposé `12345` `8445` par `12332` ngrok. Notez que nous avons un va-et-vient `1.bot.contoso.com` de `1.tcp.ngrok.io` . Il sera utilisé comme URL multimédia pour le bot. Bien entendu, ces numéros de port ne sont que des exemples et vous pouvez utiliser n’importe quel port disponible.

### <a name="update-code"></a>Mise à jour du code

Une fois ngrok en cours d’exécution, mettez à jour le code pour utiliser la config que vous vient de configurer.

#### <a name="update-signaling"></a>Mise à jour de la signalisation

Dans l’appel botBuilder, modifiez l’URL de signalisation fournie `NotificationUrl` par ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Remplacez le signal par celui fourni par ngrok et par le chemin d’accès du contrôleur `NotificationEndpoint` qui reçoit la notification.

> [!IMPORTANT]
> * L’URL `SetNotificationUrl` doit être HTTPS.
> 
> Votre instance locale doit être à l’écoute du trafic HTTP sur le port de signalisation. Les demandes faites par la plateforme d’appels et de réunions en ligne atteindront le bot en tant que trafic HTTP localhost, sauf si le chiffrement de bout en bout est installé.

#### <a name="update-media"></a>Mettre à jour un support

Mettez à jour `MediaPlatformSettings` les informations suivantes :

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

- Les comptes gratuits Ngrok **ne fournissent** pas de chiffrement de bout en bout. Les données HTTPS se terminent à l’URL ngrok et les données sont non chiffrées de ngrok à `localhost` . Si vous avez besoin d’un chiffrement de bout en bout, envisagez un compte ngrok payant. Voir [les tunneles TLS](https://ngrok.com/docs#tls) pour obtenir la procédure de configuration des tunnel de bout en bout sécurisés.
- Étant donné que l’URL de rappel du bot est dynamique, les scénarios d’appels entrants nécessitent que vous mettez fréquemment à jour vos points de terminaison ngrok. Une façon de résoudre ce problème consiste à utiliser un compte ngrok payant qui fournit des sous-domaine fixes vers lesquels vous pouvez pointer votre bot et la plateforme.
- Les tunneles Ngrok peuvent également être utilisés avec [Azure Service Fabric](/azure/service-fabric/service-fabric-overview). Pour obtenir un exemple de la façon de le faire, voir l’exemple [d’application HueBot.](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)
