---
title: Créer un bot dans Teams
author: clearab
description: Apprendrez à créer un bot Teams
ms.topic: conceptual
localization_priority: Priority
ms.author: anclear
ms.openlocfilehash: 86ef162ceee07b1f66992d6943b22336d717c9f7
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452798"
---
# <a name="create-a-bot-for-microsoft-teams"></a>Créer un bot dans Microsoft Teams

> [!TIP]
> Vous recherchez un moyen plus rapide de commencer ? Créez un [bot](../../build-your-first-app/build-bot.md) à l’aide du kit de ressources Microsoft Teams.

Pour créer un bot de conversation, procédez comme suit :

1. Préparez votre environnement de développement.
1. Créez votre service web.
1. Enregistrez votre service web en tant que bot avec Microsoft Bot Framework.
1. Créez votre manifeste d'application et votre package de l’application.
1. Télécharger votre package dans Microsoft Teams.

La création de votre service web, l'inscription de votre service web et la création de votre package de l'application, avec le Bot Framework, peuvent être effectuées dans n'importe quel ordre. Toutefois, étant donné que les trois éléments sont imbriqués, quel que soit l'ordre dans lequel vous les effectuez, vous devez revenir pour mettre à jour les autres.  Votre inscription nécessite du point de terminaison de la messagerie à partir de votre service web déployé. votre service web nécessite l’ID et le mot de passe créés à partir de votre inscription. Votre manifeste d’application a également besoin de l’ID d’inscription pour connecter les équipes à votre service web.

Au fur et à mesure que vous construisez votre bot, vous passez régulièrement de la modification de votre manifeste d'application au déploiement de code pour votre service web. Lorsque vous utilisez le manifeste de l’application, gardez à l’esprit que vous pouvez soit manipuler manuellement le fichier JSON, soit effectuer des modifications à l’aide de App Studio. Dans les deux cas, vous devez redéployer (télécharger) votre application dans Teams lorsque vous apportez une modification au manifeste. Toutefois, vous n’avez pas besoin de le faire lorsque vous déployez des modifications apportées à votre service web.

Pour plus d’informations sur le Bot Framework, consultez la [Documentation Bot Framework](/azure/bot-service/).

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Créez votre service web

Le cœur de votre bot est votre service web. Celle-ci permet de définir un itinéraire unique, généralement `/api/messages`, sur lequel recevoir toutes les demandes. Pour commencer, vous avez le choix entre plusieurs options :

* Commencez par utiliser l’exemple de bot de conversation Teams dans [C#/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot) ou [JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot).
* Si vous utilisez JavaScript, utilisez le générateur [Yeoman pour Microsoft Teams](https://github.com/OfficeDev/generator-teams) pour structurer votre application d’équipe, y compris votre service web. Ceci est particulièrement utile lorsque vous créez une application Teams qui contient plusieurs bots de conversation.
* Créez votre service web de toutes pièces. Vous pouvez choisir d’ajouter le kit de développement logiciel (SDK) Bot Framework pour votre langue. Vous pouvez également travailler directement avec les charges utiles JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Inscrivez votre service web à l’aide de Bot Framework

> [!IMPORTANT]
> Lorsque vous inscrivez votre service web, assurez-vous d’attribuer au **Nom complet** le nom que vous avez utilisé pour votre **Nom court** dans votre manifeste de l’application. Lorsque votre application est distribuée par téléchargement direct ou via le catalogue d'applications d'une organisation, les messages envoyés à une conversation par votre bot utilisent le **Nom complet** d'inscription plutôt que le **Nom court** de l'application.

L'inscription de votre service web au Bot Framework fournit un canal de communication sécurisé entre le client Teams et votre service web. Le client Teams et votre service Web ne communiquent jamais directement. Au lieu de cela, les messages sont acheminés par le Bot Framework Service (Microsoft Teams utilise une instance distincte de ce service qui est conforme aux normes Office 365).

Deux options s’offrent à vous lorsque vous inscrivez votre service web à l’aide de Bot Framework. Vous pouvez utiliser [App Studio](#using-app-studio) ou le [Portail hérité](#in-the-legacy-portal) pour inscrire votre bot sans utiliser d’abonnement Azure. Ou, si vous avez déjà un abonnement Azure (ou si vous n’avez pas besoin d’en créer un), vous pouvez utiliser [le Portail Microsoft Azure](#with-an-azure-subscription) pour inscrire votre service web.

### <a name="without-an-azure-subscription"></a>Sans abonnement Azure.

Si vous ne souhaitez pas créer votre inscription de bot dans Azure, vous **devez** utiliser ce lien https://dev.botframework.com/bots/newou App Studio. Si vous cliquez sur le bouton *Créer un bot* dans le portail Bot Framework, vous allez créer l'inscription de votre bot dans Microsoft Azure, et vous devrez fournir un abonnement Azure. Pour gérer votre inscription ou la migrer vers un abonnement Azure après la création, accédez à : https://dev.botframework.com/bots.

Lorsque vous modifiez les propriétés d'une inscription existante au Bot Framework non inscrite dans Azure, celui-ci est répertorié dans la colonne « État de la migration » et un bouton bleu « Migrer » vous permet d’accéder au Portail Microsoft Azure. Ne sélectionnez pas le bouton « Migrer », sauf s’il s’agit de ce que vous voulez faire. Au lieu de cela, sélectionnez le **nom** du bot et modifiez ses propriétés :

   ![Modifier les propriétés du bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)

Scénarios dans lesquels vous **devez** faire inscrire votre bot dans Azure (soit en le créant dans le Portail Microsoft Azure, soit via une migration) :

* Vous voulez utiliser le [OAuthPrompt](./authentication/auth-flow-bot.md) de Bot Framework pour l’authentification.
* Vous voulez activer d’autres canaux tels que la conversation web, Direct Line ou Skype.

#### <a name="using-app-studio"></a>Utilisation de App Studio

*App Studio* est une application de Teams qui vous aide à créer des applications Teams, y compris l’inscription de votre service web en tant que bot, la création d’un manifeste d’application et votre package d’application et la mise à jour des paramètres et des configurations. Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes. Consultez [Commencer à gérer App Studio de Teams](../../concepts/build-and-test/app-studio-overview.md).

N’oubliez pas que si vous utilisez App Studio pour inscrire votre service web, vous devez accéder à https://dev.botframework.com/bots pour gérer votre inscription.

#### <a name="in-the-legacy-portal"></a>Dans le portail hérité

Créez votre inscription au bot à l’aide de ce lien : https://dev.botframework.com/bots/new. **Veillez à ajouter Microsoft Teams sous la forme d’un canal à partir de la liste de chaînes proposées après avoir créé votre bot.** N’hésitez pas à réutiliser tout ID d’application Microsoft que vous avez généré si vous avez déjà créé votre package d’application/manifeste.

   ![Page d’inscription de Bot Framework](~/assets/images/bots/bfregister.png)

### <a name="with-an-azure-subscription"></a>Avec un abonnement Azure

Vous pouvez également inscrire votre service web en créant une ressource d’inscription canaux de bots dans le Portail Microsoft Azure.

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

Le [portail Bot Framework](https://dev.botframework.com) est optimisé pour l’inscription des bots dans Microsoft Azure. Voici quelques opérations que vous pouvez prendre en compte :

* Le canal Microsoft Teams pour les bots inscrits sur Azure est **gratuit**. Les messages envoyés sur le canal Teams ne sont PAS pris en compte dans les messages consommés pour le bot.
* Si vous inscrivez votre bot à l’aide de Microsoft Azure, votre code bot n’a pas besoin d’être *hébergé* sur Microsoft Azure.
* Si vous inscrivez un bot à l’aide du Portail Microsoft Azure, vous devez disposer d’un compte Microsoft Azure. Vous pouvez [en créer un gratuitement](https://azure.microsoft.com/free/). Pour vérifier votre identité lorsque vous créez un compte Azure, vous devez fournir une carte de crédit, mais celle-ci ne sera pas débitée. Il est toujours gratuit de créer et d’utiliser des bots avec Microsoft Teams.

## <a name="create-your-app-manifest-and-package"></a>Créez votre manifeste d'application et votre package

Votre [manifeste d’application](~/resources/schema/manifest-schema.md) définit les métadonnées de votre application, les points d’extension utilisés par votre application et les pointeurs vers les services web auxquels les points d’extension se connectent. Vous pouvez utiliser App Studio pour créer votre manifeste d’application ou le créer manuellement.

### <a name="add-using-app-studio"></a>Ajouter à l’aide de App Studio

1. Dans le client Teams, ouvrez App Studio à partir du menu **...** dépassement sur le rail de navigation gauche. Si App Studio n’est pas déjà installé, vous pouvez le faire en le recherchant.
2. Dans l’onglet **Éditeur de manifeste**, sélectionnez **Créer une application** (ou si vous ajoutez un bot à une application existante, vous pouvez importer votre package d’application)
3. Ajoutez les détails de votre application (consultez [définition de schéma de manifeste](~/resources/schema/manifest-schema.md) pour obtenir une description complète de chaque champ).
4. Sous l’onglet **Bots** sélectionnez le bouton **Configuration**.
5. Vous pouvez soit créer une inscription de service web (**Nouveau bot**), soit sélectionner **Bot existant**.
6. Sélectionnez les fonctionnalités et les étendues dont votre bot aura besoin.
7. Si nécessaire, mettez à jour votre adresse de point de terminaison de bot pour qu’elle pointe vers votre bot. Celle-ci doit avoir la forme `https://someplace.com/api/messages`.
8. Vous pouvez également ajouter des [commandes de bot](~/bots/how-to/create-a-bot-commands-menu.md).
9. Vous pouvez également télécharger votre package de l’application terminé à partir de l’onglet **tester et distribuer**.

### <a name="create-it-manually"></a>Créez-le manuellement

Comme pour les onglets et les extensions de messagerie, vous mettez à jour l’[App-manifest](~/resources/schema/manifest-schema.md) pour définir votre bot. Ajoutez une nouvelle structure JSON de niveau supérieur dans votre manifeste d’application avec la propriété `bots`.

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`botId`|String|64 caractères|✔|ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Il peut s’agir d’une ID d’application globale.|
|`needsChannelSelector`|Boolean|||Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique. La valeur par défaut est `false`.|
|`isNotificationOnly`|Boolean|||Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel. La valeur par défaut est `false`.|
|`supportsFiles`|Boolean|||Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle. La valeur par défaut est `false`.|
|`scopes`|Tableau de l’énum|3|✔|Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`). Ces options ne sont pas exclusives.|

Vous pouvez également définir une ou plusieurs listes de commandes que votre bot peut recommander aux utilisateurs. L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type `object`. Vous devez définir une liste de commandes distincte pour chaque étendue prise en charge par votre bot. Pour plus d’informations, *consultez* la rubrique[Menus du Bot](./create-a-bot-commands-menu.md) .

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`items.scopes`|tableau de l’énum|3|✔|Spécifie l’étendue pour laquelle la liste de commandes est valide. Les options sont `team`, `personal` et `groupchat`.|
|`items.commands`|tableau d’objets|10|✔|Ensemble de commandes prises en charge par le bot :<br>`title`: nom de la commande bot (chaîne, 32)<br>`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)|

#### <a name="simple-manifest-example"></a>Exemple de manifeste simple

L’exemple ci-dessous est un objet bot simple, avec deux listes de commandes définies. Il ne s’agit pas de la totalité du fichier manifeste de l’application, uniquement de la partie spécifique aux extensions de messagerie.

```json
...
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
...
```

#### <a name="create-your-app-package-manually"></a>Créer manuellement votre package de l’application

Pour créer un package de l’application, vous devez ajouter votre manifeste d’application et (éventuellement) vos icônes d’application dans un fichier archive .zip. Pour plus d’informations, consultez [Créer votre package d’application](~/concepts/build-and-test/apps-package.md). Assurez-vous que l’archive .zip contient uniquement les fichiers nécessaires et qu'elle ne contient aucune autre structure de dossier.

## <a name="upload-your-package-to-microsoft-teams"></a>Télécharger votre package dans Microsoft Teams

> [!NOTE]
> Pour charger votre robot, l’administrateur de votre client doit d’abord [autoriser le chargement](/microsoftteams/manage-apps#manage-org-wide-app-settings) d’applications tierces ou personnalisées dans Teams.

Si vous utilisez App Studio, vous pouvez installer votre application à partir de l'onglet **Tester et distribuer** de l’**Éditeur de manifeste**. Vous pouvez également installer votre package d’application en cliquant sur le menu `...` dépassement sur le rail gauche de la barre de navigation, en cliquant sur **Autres applications**, puis sur le lien **Télécharger une application personnalisée**. Vous pouvez également importer un manifeste d’application ou un package d’application dans App Studio pour effectuer des mises à jour supplémentaires avant de les télécharger.

## <a name="bots-in-teams-meetings"></a>Robots dans les réunions Teams

Teams prend en charge l’invocation des robots pendant les réunions. Lorsque votre robot reçoit le message d’appel, il peut identifier l’utilisateur et le client grâce à `userId` et `tenantId`. `meetingId` fait partie de l’objet `channelData`. Votre robot peut utiliser `userId` et `meetingId` pour la demande d’API `GetParticipant` afin de récupérer les rôles d’utilisateur.

## <a name="next-steps"></a>Étapes suivantes

* [Concepts de base d’une conversation de bot](./conversations/conversation-basics.md)
* [S’abonner à des événements de conversation](./conversations/subscribe-to-conversation-events.md)
