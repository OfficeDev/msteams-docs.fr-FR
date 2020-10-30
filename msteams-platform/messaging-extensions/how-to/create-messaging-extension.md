---
title: Créer une extension de messagerie à l’aide d’App Studio
author: clearab
description: Découvrez comment créer une extension de messagerie Microsoft teams à l’aide d’App Studio.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: c3437457f7084d2d768af0f0db5208525c368682
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796182"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>Créer une extension de messagerie à l’aide d’App Studio

> [!TIP]
> Vous recherchez un moyen plus rapide de commencer ? Créer une [extension de messagerie](../../build-your-first-app/build-messaging-extension.md) à l’aide du kit de développement Microsoft Teams.

À un niveau élevé, vous devez effectuer les étapes suivantes pour créer une extension de messagerie.

1. Préparer votre environnement de développement :
2. Créer et déployer votre service Web (tout en développant utiliser un service de tunneling comme ngrok pour l’exécuter localement)
3. Inscrivez votre service web à l’aide de Bot Framework
4. Créer votre package d’application
5. Télécharger votre package dans Microsoft Teams

La création de votre service Web, la création de votre package d’application et l’enregistrement de votre service Web à l’aide de l’infrastructure de robot peuvent être réalisées dans n’importe quel ordre. Étant donné que ces trois éléments sont entrelacés, indépendamment de l’ordre dans lequel vous les effectuez, revenez à la mise à jour des autres. Votre inscription a besoin du point de terminaison de messagerie à partir de votre service Web déployé, et votre service Web a besoin de l’ID et du mot de passe créés à partir de votre inscription. Le manifeste de votre application a également besoin de cet ID pour connecter teams à votre service Web.

Lors de la création de votre extension de messagerie, vous vous déplacez régulièrement entre les modifications de votre manifeste d’application et le déploiement de code dans votre service Web. Lorsque vous utilisez le manifeste de l’application, gardez à l’esprit que vous pouvez manipuler manuellement le fichier JSON ou effectuer des modifications via l’application Studio. Dans les deux cas, vous devez redéployer (Télécharger) votre application dans teams lorsque vous modifiez le manifeste, mais il n’est pas nécessaire de le faire lorsque vous déployez des modifications sur votre service Web.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Créez votre service web

Le cœur de votre extension de messagerie est votre service Web. Il définit un seul itinéraire, généralement `/api/messages` , pour recevoir toutes les demandes sur. Si vous commencez à partir de zéro, vous avez le choix entre plusieurs options.

* Utilisez l’un de nos didacticiels [QuickStartES](#learn-more) qui vous guideront tout au long de la création de votre service Web.
* Choisissez l’un des exemples d’extensions de messagerie disponibles dans l’exemple de référentiel de l' [infrastructure bot](https://github.com/Microsoft/BotBuilder-Samples) à partir duquel démarrer.
* Si vous utilisez JavaScript, utilisez le [Générateur Yeoman pour Microsoft teams](https://github.com/OfficeDev/generator-teams) pour générer la structure de votre application Teams, y compris votre service Web.
* Créez votre service web de toutes pièces. Vous pouvez choisir d’ajouter le kit de développement logiciel (SDK) Bot Framework pour votre langue. Vous pouvez également travailler directement avec les charges utiles JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Inscrivez votre service web à l’aide de Bot Framework

Les extensions de messagerie tirent parti du schéma de messagerie et du protocole de communication sécurisé de l’infrastructure bot. Si vous n’en avez pas encore, vous devez enregistrer votre service Web sur l’infrastructure de robot. ID de l’application Microsoft (il s’agit de l’ID de votre robot de l’intérieur de teams, pour l’identifier à partir d’autres ID d’application que vous pouvez utiliser) et le point de terminaison de messagerie que votre inscription à l’infrastructure de robot sera utilisé dans votre extension de messagerie pour recevoir et répondre aux demandes. Si vous utilisez une inscription existante, veillez à [activer le canal Microsoft teams](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).

Si vous suivez l’un des Démarrages rapides ou l’un des exemples disponibles, vous serez guidé lors de l’inscription de votre service Web. Si vous souhaitez inscrire manuellement votre service, vous disposez de trois options pour le faire. Si vous choisissez de vous inscrire sans utiliser d’abonnement Azure, vous ne serez pas en mesure de tirer parti du flux d’authentification OAuth simplifié fourni par l’infrastructure bot. Vous serez en mesure de migrer votre inscription vers Azure après sa création.

* Si vous disposez d’un abonnement Azure (ou que vous souhaitez en créer un), vous pouvez inscrire votre service Web manuellement à l’aide du portail Azure. Créez une ressource « inscription des canaux de robots ». Vous pouvez choisir le niveau de tarification libre, car les messages de Microsoft Teams ne sont pas pris en compte dans votre nombre total de messages autorisés par mois.
* Si vous ne souhaitez pas utiliser d’abonnement Azure, vous pouvez utiliser le [portail d’inscription hérité](https://dev.botframework.com/bots/new).
* App Studio peut également vous aider à enregistrer votre service Web. Les services Web inscrits via l’application Studio ne sont pas enregistrés dans Azure. Vous pouvez utiliser le [portail hérité](https://dev.botframework.com/bots) pour afficher, gérer et migrer vos enregistrements.

## <a name="create-your-app-manifest"></a>Créer le manifeste de votre application

Vous pouvez utiliser App Studio pour créer votre manifeste d’application ou le créer manuellement.

### <a name="create-your-app-manifest-using-app-studio"></a>Créer votre manifeste d’application à l’aide d’App Studio

Vous pouvez utiliser l’application App Studio à partir du client Microsoft teams pour vous aider à créer votre manifeste d’application.

1. Dans le client Teams, ouvrez App Studio à partir du menu **...** dépassement sur le rail de navigation gauche. S’il n’est pas déjà installé, vous pouvez le faire en le recherchant.
2. Dans l’onglet **éditeur de manifeste** , sélectionnez **créer une nouvelle application** (ou si vous ajoutez une extension de messagerie à une application existante, vous pouvez importer votre package d’application)
3. Ajoutez les détails de votre application (consultez [définition de schéma de manifeste](~/resources/schema/manifest-schema.md) pour obtenir une description complète de chaque champ).
4. Sous l’onglet **extensions de messagerie** , cliquez sur le bouton **configuration** .
5. Vous pouvez créer un nouveau service Web pour votre extension de messagerie à utiliser ou, si vous en avez déjà enregistré un, sélectionnez-le.
6. Si nécessaire, mettez à jour votre adresse de point de terminaison de bot pour qu’elle pointe vers votre bot. Celle-ci doit avoir la forme `https://someplace.com/api/messages`.
7. Le bouton **Ajouter** de la section **commande** vous guide tout au long de l’ajout de commandes à votre extension de messagerie. Pour plus d’informations sur l’ajout de commandes, voir la section [en savoir plus](#learn-more) . N’oubliez pas que vous pouvez définir jusqu’à 10 commandes pour votre extension de messagerie.
8. La section **gestionnaires de messages** vous permet d’ajouter un domaine sur lequel votre messagerie se déclenchera. Pour plus d’informations, voir [Link unfurling](~/messaging-extensions/how-to/link-unfurling.md) .

À partir de l’onglet **Terminer => test et distribution** , vous pouvez **Télécharger** votre package d’application (ce qui inclut le manifeste de votre application, ainsi que les icônes de votre application) ou **installer** le package.

### <a name="create-your-app-manifest-manually"></a>Création manuelle de votre manifeste d’application

Comme avec les robots et les onglets, vous mettez à jour le [manifeste d’application](~/resources/schema/manifest-schema.md#composeextensions) de votre application afin d’inclure les propriétés d’extension de messagerie. Ces propriétés déterminent la façon dont votre extension de messagerie apparaît et se comporte dans le client Microsoft Teams. Les extensions de messagerie sont prises en charge à partir de la version 1.0 du manifeste.

#### <a name="declare-your-messaging-extension"></a>Déclarer votre extension de messagerie

Pour ajouter une extension de messagerie, incluez une nouvelle structure JSON de niveau supérieur dans le manifeste de votre application avec la `composeExtensions` propriété. Vous créez une extension de messagerie unique pour votre application, avec un maximum de 10 commandes.

> [!NOTE]
> Le manifeste fait référence aux extensions de messagerie en tant que `composeExtensions` . Cela permet de conserver une compatibilité descendante.

La définition d’extension est un objet de la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? |
|---|---|---|
| `botId` | ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Il doit en principe être identique à l’ID de votre application globale de teams. | Oui |
| `canUpdateConfiguration` | Active l’élément de menu **paramètres** . | Non |
| `commands` | Tableau de commandes pris en charge par cette extension de messagerie. Vous êtes limité à 10 commandes. | Oui |

#### <a name="define-your-commands"></a>Définir vos commandes

Votre extension de messagerie doit déclarer une ou plusieurs commandes, qui définissent l’emplacement où vos utilisateurs peuvent déclencher votre extension de messagerie, ainsi que le type d’interaction. Pour plus d’informations sur les commandes d’extension de messagerie, consultez la rubrique [en savoir plus](#learn-more) .

#### <a name="simple-manifest-example"></a>Exemple de manifeste simple

L’exemple ci-dessous est un simple objet d’extension de messagerie dans le manifeste de l’application avec une commande de recherche. Il ne s’agit pas de la totalité du fichier manifeste de l’application, uniquement de la partie spécifique aux extensions de messagerie. Consultez le [schéma de manifeste d’application](~/resources/schema/manifest-schema.md) pour obtenir un exemple complet.

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

## <a name="add-your-invoke-message-handlers"></a>Ajouter vos gestionnaires de messages d’appel

Lorsque vos utilisateurs déclenchent votre extension de messagerie, vous devez gérer le message d’appel initial, recueillir des informations auprès de l’utilisateur, puis traiter ces informations et y répondre de manière appropriée. Pour ce faire, vous devez d’abord déterminer le type de commandes que vous souhaitez ajouter à votre extension de messagerie et [Ajouter une commande action](~/messaging-extensions/how-to/action-commands/define-action-command.md) ou [Ajouter une commande de recherche](~/messaging-extensions/how-to/search-commands/define-search-command.md).

## <a name="messaging-extensions-in-teams-meetings"></a>Extensions de messagerie dans les réunions teams

Une fois qu’une réunion commence, les participants peuvent interagir directement avec votre extension de messagerie lors d’un appel en direct. Tenez compte des éléments suivants lors de la création de votre extension de messagerie dans une réunion :

1. **Emplacement :** Votre extension de messagerie peut être appelée à partir de la zone de message de composition, de la zone de commande ou de la @mentioned dans la conversation de réunion.

1. **Métadonnées** . Lorsque votre extension de messagerie est appelée, elle peut identifier l’utilisateur et le client à partir de `userId` et `tenantId` . `meetingId` fait partie de l’objet `channelData`. Votre application peut utiliser le `userId` et `meetingId`  pour la `GetParticipant` demande d’API afin de récupérer les rôles d’utilisateur.

1. **Type de commande** . Si votre extension de message utilise des [commandes basées sur l’action](../../messaging-extensions/what-are-messaging-extensions.md#action-commands), elle doit suivre l’authentification [unique](../../tabs/how-to/authentication/auth-aad-sso.md) des onglets.

1. **Expérience utilisateur** . L’extension de messagerie doit ressembler et se comporter de la même manière qu’en dehors d’une réunion.

## <a name="next-steps"></a>Étapes suivantes

* [Créer des commandes d’action](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Créer des commandes de recherche](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Déploiement de lien](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>En savoir plus

Essayez-le dans un démarrage rapide :

* Démarrages rapides pour C #
  * [Extension de messagerie avec des commandes basées sur l’action](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Extension de messagerie avec des commandes basées sur la recherche](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* Démarrages rapides pour JavaScript
  * [Extension de messagerie avec des commandes basées sur l’action](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Extension de messagerie avec des commandes basées sur la recherche](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

En savoir plus sur les concepts de développement de teams :

* [Comprendre les fonctionnalités des applications teams](../../concepts/capabilities-overview.md)
* [Qu’est-ce que les extensions de messagerie ?](~/messaging-extensions/what-are-messaging-extensions.md)
