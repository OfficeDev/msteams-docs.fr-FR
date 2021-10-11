---
title: Créer une extension de messagerie à l’aide de App Studio
author: surbhigupta
description: Découvrez comment créer une extension Microsoft Teams messagerie à l’aide d’App Studio.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 6b7de5b5178d893e391b0e97a699f1cba029d59d
ms.sourcegitcommit: c04a1a792773a9d5c61169c5702d94a8c478ad1c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2021
ms.locfileid: "60260645"
---
# <a name="create-a-messaging-extension-using-app-studio"></a>Créer une extension de messagerie à l’aide de App Studio

> [!TIP]
> Vous recherchez un moyen plus rapide de commencer ? Créez [une extension de messagerie à l’aide](../build-your-first-app/build-messaging-extension.md) Microsoft Teams Shared Computer Toolkit.

À un niveau élevé, vous devez effectuer les étapes suivantes pour créer une extension de messagerie.

1. Préparer votre environnement de développement
2. Créer et déployer votre service web (tout en développant un service de tunneling comme ngrok pour l’exécuter localement)
3. Inscrivez votre service web à l’aide de Bot Framework
4. Créer votre package d’application
5. Télécharger votre package dans Microsoft Teams

La création de votre service web, la création de votre package d’application et l’inscription de votre service web avec Bot Framework peuvent être réalisées dans n’importe quel ordre. Étant donné que ces trois éléments sont si dispersés, quel que soit l’ordre dans lequel vous les faites, vous devrez revenir pour mettre à jour les autres. Votre inscription nécessite le point de terminaison de messagerie de votre service web déployé, et votre service web a besoin de l’ID et du mot de passe créés à partir de votre inscription. Votre manifeste d’application a également besoin de cet ID pour se connecter Teams à votre service web.

Lorsque vous construisez votre extension de messagerie, vous allez régulièrement passer de la modification du manifeste de votre application au déploiement de code dans votre service web. Lorsque vous travaillez avec le manifeste de l’application, n’oubliez pas que vous pouvez manipuler manuellement le fichier JSON ou apporter des modifications via App Studio. Dans les deux cas, vous devez re-déployer (télécharger) votre application dans Teams lorsque vous modifiez le manifeste, mais vous n’avez pas besoin de le faire lorsque vous déployez les modifications apportées à votre service web.

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a>Créez votre service web

Le cœur de votre extension de messagerie est votre service web. Il définit un itinéraire unique, `/api/messages` généralement, pour recevoir toutes les demandes. Si vous débutez à partir de zéro, vous avez le choix entre plusieurs options.

* Utilisez l’un de nos [didacticiels](#learn-more) de démarrage rapide qui vous guidera tout au long de la création de votre service web.
* Choisissez l’un des exemples d’extension de messagerie disponibles dans le référentiel d’exemples [Bot Framework](https://github.com/Microsoft/BotBuilder-Samples) à partir de.
* Si vous utilisez JavaScript, utilisez le générateur [Yeoman](https://github.com/OfficeDev/generator-teams) pour Microsoft Teams pour échafauder votre application Teams, y compris votre service web.
* Créez votre service web de toutes pièces. Vous pouvez choisir d’ajouter le kit de développement logiciel (SDK) Bot Framework pour votre langue. Vous pouvez également travailler directement avec les charges utiles JSON.

## <a name="register-your-web-service-with-the-bot-framework"></a>Inscrivez votre service web à l’aide de Bot Framework

Les extensions de messagerie tirez parti du schéma de messagerie et du protocole de communication sécurisée de Bot Framework. Si vous n’en avez pas déjà, vous devrez inscrire votre service web sur Bot Framework. ID de l’application Microsoft (nous l’appellerons ID de bot à partir de l’intérieur de Teams, pour l’identifier à partir d’autres ID d’application que vous pourriez utiliser) et le point de terminaison de messagerie de votre inscription avec Bot Framework sera utilisé dans votre extension de messagerie pour recevoir et répondre aux demandes. Si vous utilisez une inscription existante, veillez à activer le [canal Microsoft Teams.](/azure/bot-service/bot-service-manage-channels.md?preserve-view=true&view=azure-bot-service-4.0)


Si vous suivez l’un des démarrages rapides ou démarrez à partir de l’un des exemples disponibles, vous serez guidé tout au long de l’inscription de votre service web. Si vous souhaitez inscrire manuellement votre service, trois options s’offrent à vous. Si vous choisissez de vous inscrire sans utiliser d’abonnement Azure, vous ne pourrez pas tirer parti du flux d’authentification OAuth simplifié fourni par Bot Framework. Vous pourrez migrer votre inscription vers Azure après sa création.

* Si vous avez un abonnement Azure (ou que vous souhaitez en créer un), vous pouvez inscrire votre service web manuellement à l’aide du portail Azure. Créez une ressource « Inscription des canaux bots ». Vous pouvez choisir le niveau de tarification gratuit, car les messages provenant de Microsoft Teams ne sont pas comptabilisés dans le nombre total de messages par mois.
* Si vous ne souhaitez pas utiliser un abonnement Azure, vous pouvez utiliser le [portail d’inscription hérité.](https://dev.botframework.com/bots/new)
* App Studio peut également vous aider à inscrire votre service web (bot). Les services Web enregistrés via App Studio ne sont pas enregistrés dans Azure. Vous pouvez utiliser le [portail hérité pour](https://dev.botframework.com/bots) afficher, gérer et migrer vos inscriptions.

## <a name="create-your-app-manifest"></a>Créer le manifeste de votre application

Vous pouvez utiliser App Studio pour créer votre manifeste d’application ou le créer manuellement.

### <a name="create-your-app-manifest-using-app-studio"></a>Créer le manifeste de votre application à l’aide d’App Studio

Vous pouvez utiliser l’application App Studio à partir du client Microsoft Teams pour vous aider à créer votre manifeste d’application.

1. Dans le client Teams, ouvrez App Studio à partir du menu **...** dépassement sur le rail de navigation gauche. S’il n’est pas déjà installé, vous pouvez le faire en le recherchant.
2. Sous **l’onglet Éditeur** de manifeste, sélectionnez Créer une application **(ou** si vous ajoutez une extension de messagerie à une application existante, vous pouvez importer votre package d’application)
3. Ajoutez les détails de votre application (consultez [définition de schéma de manifeste](~/resources/schema/manifest-schema.md) pour obtenir une description complète de chaque champ).
4. Sous **l’onglet Extensions de messagerie,** cliquez sur le **bouton Installation.**
5. Vous pouvez créer un nouveau service web (bot) pour votre extension de messagerie à utiliser, ou si vous en avez déjà inscrit un, sélectionnez/ajoutez-le ici.
6. Si nécessaire, mettez à jour votre adresse de point de terminaison de bot pour qu’elle pointe vers votre bot. Celle-ci doit avoir la forme `https://someplace.com/api/messages`.
7. Le **bouton** Ajouter dans la section **Commande** vous guide tout au long de l’ajout de commandes à votre extension de messagerie. Pour plus [d’informations](#learn-more) sur l’ajout de commandes, voir la section En savoir plus. N’oubliez pas que vous pouvez définir jusqu’à 10 commandes pour votre extension de messagerie.
8. La **section Gérer les messages** vous permet d’ajouter un domaine sur le déclenchement de votre messagerie. Pour plus [d’informations, voir](~/messaging-extensions/how-to/link-unfurling.md) déploiement de lien.

À partir de **l’onglet Terminer =** > tester et distribuer, vous pouvez télécharger votre package d’application (qui inclut votre manifeste d’application ainsi que les icônes de votre application) ou installer **le** package.

### <a name="create-your-app-manifest-manually"></a>Créer manuellement le manifeste de votre application

Comme avec les bots et [](~/resources/schema/manifest-schema.md#composeextensions) les onglets, vous mettez à jour le manifeste de votre application pour inclure les propriétés d’extension de messagerie. Ces propriétés régissent l’apparition et le comportement de votre extension de messagerie dans le client Microsoft Teams messagerie. Les extensions de messagerie sont pris en charge à partir de la v1.0 du manifeste.

#### <a name="declare-your-messaging-extension"></a>Déclarer votre extension de messagerie

Pour ajouter une extension de messagerie, incluez une nouvelle structure JSON de niveau supérieur dans le manifeste de votre application avec la `composeExtensions` propriété. Vous créez une extension de messagerie unique pour votre application, avec jusqu’à 10 commandes.

> [!NOTE]
> Le manifeste fait référence aux extensions de messagerie comme `composeExtensions` . Il s’agit de maintenir la compatibilité ascendante.

La définition d’extension est un objet qui a la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? |
|---|---|---|
| `botId` | ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Il doit généralement être identique à l’ID de votre application Teams globale. | Oui |
| `canUpdateConfiguration` | Active **l Paramètres** de menu. | Non |
| `commands` | Tableau de commandes pris en charge par cette extension de messagerie. Vous êtes limité à 10 commandes. | Oui |

#### <a name="define-your-commands"></a>Définir vos commandes

Votre extension de messagerie doit déclarer une ou plusieurs commandes, qui définissent l’endroit où vos utilisateurs peuvent déclencher votre extension de messagerie, ainsi que le type d’interaction. Pour [plus d’informations](#learn-more) sur les commandes d’extension de messagerie, voir plus d’informations.

#### <a name="simple-manifest-example"></a>Exemple de manifeste simple

L’exemple suivant est un objet d’extension de messagerie simple dans le manifeste de l’application avec une commande de recherche. Il ne s’agit pas de la totalité du fichier manifeste de l’application, uniquement de la partie spécifique aux extensions de messagerie. Pour obtenir un exemple [complet, voir](~/resources/schema/manifest-schema.md) schéma de manifeste d’application.

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

#### <a name="complete-app-manifest-example"></a>Exemple de manifeste d’application complet

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a>Ajouter vos handlers de messages d’appel

Lorsque vos utilisateurs déclenchent votre extension de messagerie, vous devez gérer le message d’appel initial, collecter des informations auprès de l’utilisateur, puis traiter ces informations et répondre de manière appropriée. Pour ce faire, vous devez d’abord décider du type de commande que vous souhaitez ajouter à votre extension de messagerie, puis ajouter une [commande d’action](~/messaging-extensions/how-to/action-commands/define-action-command.md) ou ajouter une commande [de recherche.](~/messaging-extensions/how-to/search-commands/define-search-command.md)

## <a name="messaging-extensions-in-teams-meetings"></a>Extensions de messagerie dans Teams réunions

> [!NOTE]
> Si une réunion ou une conversation de groupe a des utilisateurs fédérés dans la liste, Teams l’accès aux extensions de messagerie pour tous les utilisateurs, y compris l’organisateur.

Une fois la réunion commencée, Teams participants peuvent interagir directement avec votre extension de messagerie pendant un appel en direct. Prenons les considérations suivantes lors de la création de votre extension de messagerie en réunion :

1. **Emplacement :** Votre extension de messagerie peut être invoquée à partir de la zone de composition d’un message, de la zone de commande ou @mentioned dans la conversation de réunion.

1. **Métadonnées**. Lorsque votre extension de messagerie est invoquée, elle peut identifier l’utilisateur et le client à partir `userId` de et `tenantId` . `meetingId` fait partie de l’objet `channelData`. Votre application peut utiliser la demande d’API et pour récupérer `userId` `meetingId`  les `GetParticipant` rôles d’utilisateur.

1. **Type de commande**. Si votre extension de message utilise des commandes basées sur [l’action,](../messaging-extensions/what-are-messaging-extensions.md#action-commands)elle doit suivre l’authentification par [authentification](../tabs/how-to/authentication/auth-aad-sso.md) unique des onglets.

1. **Expérience utilisateur**. L’extension de messagerie doit se comporter de la même manière qu’en dehors d’une réunion.

## <a name="next-steps"></a>Prochaines étapes

* [Créer des commandes d'action](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [Créer les commandes de recherche](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [Déploiement de lien](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a>En savoir plus

Essayez-le dans un démarrage rapide :

* Démarrages rapides pour C #
  * [Extension de messagerie avec commandes basées sur l’action](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [Extension de messagerie avec commandes basées sur la recherche](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* Démarrages rapides pour JavaScript
  * [Extension de messagerie avec commandes basées sur l’action](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [Extension de messagerie avec commandes basées sur la recherche](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

En savoir plus sur Teams concepts de développement :

* [Comprendre Teams fonctionnalités de l’application](../concepts/capabilities-overview.md)
* [Que sont les extensions de messagerie ?](../messaging-extensions/what-are-messaging-extensions.md)
