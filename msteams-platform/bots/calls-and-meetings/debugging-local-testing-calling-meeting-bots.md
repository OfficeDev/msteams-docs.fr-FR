---
title: Déboguer votre robot d’appel et de réunion localement
description: Découvrez comment utiliser ngrok pour développer des appels et des bots de réunion en ligne sur votre PC local.
ms.topic: how-to
ms.localizationpriority: medium
keywords: tunnel ngrok de développement local
ms.date: 11/18/2018
ms.openlocfilehash: 7f85243e0a5d94711cd303ff542decd3bbc7847a
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757114"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Développer des bots d’appel et de réunion en ligne sur votre PC local

Dans [Exécuter et déboguer votre application](../../concepts/build-and-test/debug.md), nous expliquons comment utiliser [ngrok](https://ngrok.com) pour créer un tunnel entre votre ordinateur local et Internet. Dans cette rubrique, découvrez comment utiliser ngrok et votre PC local pour développer des bots qui prennent en charge les appels et les réunions en ligne.

Les bots de messagerie utilisent HTTP, mais les appels et les bots de réunion en ligne utilisent le protocole TCP de niveau inférieur. Ngrok prend en charge les tunnels TCP en plus des tunnels HTTP.

## <a name="configure-ngrokyml"></a>Configurer ngrok.yml

Accédez à [ngrok](https://ngrok.com) et inscrivez-vous pour obtenir un compte gratuit ou connectez-vous à votre compte existant. Une fois que vous êtes connecté, accédez au [tableau de bord](https://dashboard.ngrok.com) et obtenez votre jeton d’authentification.

Créez un fichier `ngrok.yml` de configuration ngrok et ajoutez la ligne suivante. Pour plus d’informations sur l’emplacement du fichier, consultez [ngrok](https://ngrok.com/docs#config):

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>Configurer la signalisation

Dans [les bots d’appels et de réunions en ligne](./calls-meetings-bots-overview.md), nous avons abordé la signalisation des appels sur la façon dont les bots détectent et répondent aux nouveaux appels et événements pendant un appel. Les événements de signalisation d’appel sont envoyés via HTTP POST au point de terminaison d’appel du bot.

Comme avec l’API de messagerie du bot, pour que la plateforme multimédia en temps réel puisse communiquer avec votre bot, votre bot doit être accessible via Internet. Ngrok simplifie cette opération. Ajoutez les lignes suivantes à votre fichier ngrok.yml :

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>Configurer un média local

> [!NOTE]
> Cette section est uniquement requise pour les bots multimédias hébergés par l’application et peut être ignorée si vous n’hébergez pas de média vous-même.

Le média hébergé par l’application utilise des certificats et des tunnels TCP. Les étapes suivantes sont requises :

1. Les points de terminaison TCP publics de Ngrok ont des URL fixes. Ils sont `0.tcp.ngrok.io`, `1.tcp.ngrok.io`et ainsi de suite. Vous devez disposer d’une entrée CNAME DNS pour votre service qui pointe vers ces URL. Par exemple, supposons `0.bot.contoso.com` fait référence à `0.tcp.ngrok.io`, `1.bot.contoso.com` fait référence à `1.tcp.ngrok.io`, etc.
2. Un certificat SSL est requis pour vos URL. Pour faciliter la tâche, utilisez un certificat SSL émis vers un domaine générique. Dans ce cas, il s’agit de `*.bot.contoso.com`. Ce certificat SSL est validé par le Kit de développement logiciel (SDK) multimédia. Il doit donc correspondre à l’URL publique de votre bot. Notez l’empreinte numérique et installez-la dans vos certificats d’ordinateur.
3. À présent, configurez un tunnel TCP pour transférer le trafic vers localhost. Écrivez les lignes suivantes dans votre fichier ngrok.yml :

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Démarrer ngrok

Maintenant que la configuration ngrok est prête, lancez-la :

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

Cela démarre ngrok et définit les URL publiques, qui fournissent les tunnels à votre localhost. Voici un exemple de sortie :

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

Ici, `12345` est le port de signalisation, `8445` est le port hébergé par l’application, et `12332` est le port multimédia distant exposé par ngrok. Notez que nous avons un transfert de `1.bot.contoso.com` vers `1.tcp.ngrok.io`. Il sera utilisé comme URL du média pour le bot. Bien entendu, ces numéros de port ne sont que des exemples et vous pouvez utiliser n’importe quel port disponible.

### <a name="update-code"></a>Mise à jour du code

Une fois ngrok opérationnel, mettez à jour le code pour utiliser la configuration que vous venez de configurer.

#### <a name="update-signaling"></a>Mettre à jour la signalisation

Dans l’appel BotBuilder, remplacez le `NotificationUrl` par l’URL de signalisation fournie par ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Remplacez le signal par celui fourni par ngrok et le `NotificationEndpoint` par le chemin du contrôleur qui reçoit la notification.

> [!IMPORTANT]
>
> * L’URL dans `SetNotificationUrl` doit être HTTPS.
>
> Votre instance locale doit écouter le trafic HTTP sur le port de signalisation. Les demandes effectuées par la plateforme d’appels et de réunions en ligne atteignent le bot en tant que trafic HTTP localhost, sauf si le chiffrement de bout en bout est configuré.

#### <a name="update-media"></a>Mettre à jour le média

Mettez à jour votre `MediaPlatformSettings` comme suit :

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
> L’empreinte numérique du certificat fournie dans le `MediaPlatformSettings` doit correspondre au nom de domaine complet du service. C’est pourquoi les entrées DNS sont requises.

## <a name="caveats"></a>Avertissements

* Les comptes gratuits Ngrok **ne fournissent pas** de chiffrement de bout en bout . Les données HTTPS se terminent à l’URL ngrok et les flux de données ne sont pas chiffrés à partir de ngrok vers `localhost`. Si vous avez besoin d’un chiffrement de bout en bout, envisagez un compte ngrok payant. Consultez [tunnels TLS](https://ngrok.com/docs#tls) pour connaître les étapes de configuration des tunnels de bout en bout sécurisés.
* Étant donné que l’URL de rappel du bot est dynamique, les scénarios d’appel entrant vous obligent à mettre à jour fréquemment vos points de terminaison ngrok. Une façon de résoudre ce problème consiste à utiliser un compte ngrok payant, qui fournit des sous-domaines fixes vers lesquels vous pouvez pointer votre bot et la plateforme.
* Les tunnels Ngrok peuvent également être utilisés avec [Azure Service Fabric](/azure/service-fabric/service-fabric-overview). Pour obtenir un exemple de procédure, consultez l’exemple d’application [HueBot](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples/HueBot/HueBot).
