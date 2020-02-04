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
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Comment développer des robots d’appels et de réunions en ligne sur votre PC local

Dans [exécuter et déboguer votre application](../../concepts/build-and-test/debug.md) , nous expliquons comment utiliser [ngrok](https://ngrok.com) pour créer un tunnel entre votre ordinateur local et Internet. Dans cette rubrique, Découvrez comment vous pouvez également utiliser ngrok et votre PC local pour développer des robots qui prennent en charge les appels et les réunions en ligne.

Les robots de messagerie utilisent le protocole HTTP, mais les appels et les robots de réunion en ligne utilisent le protocole TCP de niveau inférieur. Ngrok prend en charge les tunnels TCP en plus des tunnels HTTP ; vous découvrirez comment, ci-dessous.

## <a name="configuring-ngrokyml"></a>Configuration de ngrok. yml

Accédez à [ngrok](https://ngrok.com) et inscrivez-vous pour obtenir un compte gratuit ou vous connecter à votre compte existant. Une fois que vous avez ouvert une session, accédez au [tableau de bord](https://dashboard.ngrok.com) et obtenez votre authToken.

Créez un `ngrok.yml` [fichier de configuration ngrok (pour plus](https://ngrok.com/docs#config) d’informations sur l’emplacement de ce fichier) et ajoutez la ligne suivante :

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a>Configuration de la signalisation

Dans [les appels et les robots de réunions en ligne](./calls-meetings-bots-overview.md), nous avons abordé la signalisation des appels : comment les robots détectent et répondent aux nouveaux appels et événements au cours d’un appel. Les événements de signalisation des appels sont envoyés via le protocole HTTP POST au point de terminaison appelant du bot.

Comme avec l’API de messagerie du bot, pour que la plateforme multimédia en temps réel puisse parler à votre robot, votre robot doit être accessible sur Internet. Ngrok simplifie l’ajout des lignes suivantes à votre Ngrok. yml :

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a>Configuration d’un support local

> [!NOTE]
> Cette section est uniquement requise pour les robots multimédia hébergés par l’application et peut être ignorée si vous n’hébergez pas de contenu multimédia vous-même.

Les supports hébergés par l’application utilisent des certificats et des tunnels TCP. Les étapes suivantes sont nécessaires :

- Les points de terminaison TCP publics d’Ngrok ont des URL fixes. Il s' `0.tcp.ngrok.io`agit `1.tcp.ngrok.io`de,, et ainsi de suite. Vous devez avoir une entrée DNS CNAMe pour votre service qui pointe vers ces URL. `0.bot.contoso.com` Dans cet exemple, disons qu’il s’agit `0.tcp.ngrok.io`de `1.bot.contoso.com` , fait `1.tcp.ngrok.io`référence à, et ainsi de suite.
- Un certificat SSL est requis pour vos URL. Pour faciliter l’utilisation d’un certificat SSL délivré à un domaine de caractères génériques. Dans ce cas, il s' `*.bot.contoso.com`agit de. Ce certificat SSL étant validé par le kit de développement logiciel (SDK) Media, il doit correspondre à l’URL publique de votre bot. Notez l’empreinte numérique et installez-la dans les certificats de votre ordinateur.
- À présent, configurez un tunnel TCP pour transférer le trafic vers localhost. Écrivez les lignes suivantes dans votre ngrok. yml :

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Démarrer ngrok

Maintenant que la configuration de ngrok est prête, lancez-la :

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

Cette opération démarre ngrok et définit les URL publiques qui fournissent les tunnels à votre localhost. La sortie ressemble à ce qui suit :

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

Ici, `12345` est le port de signalisation, `8445` est le port hébergé par l’application et `12332` est le port multimédia distant exposé par ngrok. Notez que nous disposons d’un transfert de `1.bot.contoso.com` vers `1.tcp.ngrok.io`. Il sera utilisé comme l’URL de média pour le bot. Bien entendu, ces numéros de port sont simplement des exemples et vous pouvez utiliser n’importe quel port disponible.

### <a name="update-code"></a>Mise à jour du code

Une fois que ngrok est en cours d’exécution, mettez à jour le code pour utiliser la configuration que vous venez de configurer.

#### <a name="update-signaling"></a>Signalisation de mise à jour

- Dans l’appel BotBuilder, modifiez l' `NotificationUrl` URL de signalisation fournie par ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Remplacez le signal par celui fourni par ngrok et `NotificationEndpoint` par le chemin d’accès du contrôleur qui reçoit la notification.

> **Important**: l’URL dans `SetNotificationUrl` doit être https.

> **Important**: votre instance locale doit écouter le trafic http sur le port de signalisation. Les demandes effectuées par la plateforme d’appels et de réunions en ligne atteindront le robot comme le trafic HTTP localhost, sauf si le chiffrement de bout en bout est configuré.

#### <a name="update-media"></a>Mettre à jour le support

`MediaPlatformSettings` Mettez à jour les éléments suivants.

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
> L’empreinte de certificat fournie ci-dessus doit correspondre au nom de domaine complet du service. C’est pourquoi les entrées DNS sont requises.

## <a name="next-steps"></a>Étapes suivantes

Votre robot peut maintenant s’exécuter localement et tous les flux fonctionnent à partir de votre localhost.

## <a name="caveats"></a>Observer lors

- Les comptes gratuits Ngrok **ne fournissent pas** de chiffrement de bout en bout. Les données HTTPs se terminent à l’URL ngrok et les données sont déchiffrées de `localhost`ngrok à. Si vous avez besoin d’un chiffrement de bout en bout, considérez un compte ngrok payant. Consultez la rubrique [TLS tunnels](https://ngrok.com/docs#tls) pour obtenir la procédure de configuration de tunnels sécurisés de bout en bout.
- Étant donné que l’URL de rappel de bot est dynamique, les scénarios d’appel entrant nécessitent fréquemment de mettre à jour vos points de terminaison ngrok. Pour résoudre ce problème, vous pouvez utiliser un compte ngrok payant qui fournit des sous-domaines fixes vers lesquels vous pouvez pointer votre robot et la plateforme.
- Les tunnels Ngrok peuvent également être utilisés avec [Azure Service Fabric](/azure/service-fabric/service-fabric-overview). Pour obtenir un exemple, consultez l' [exemple d’application HueBot](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).
