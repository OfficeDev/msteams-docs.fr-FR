---
title: Obtenir Teams contexte spécifique pour votre bot
author: surbhigupta
description: Comment obtenir le contexte spécifique de Microsoft Team pour votre bot, y compris la liste des conversations, les détails et la liste des canaux.
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 4e3717b5931b673fa52c82b54d9c79380d9ae8d8907c8c2cf51f46499386cb28
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57706268"
---
# <a name="get-teams-specific-context-for-your-bot"></a>Obtenir Teams contexte spécifique pour votre bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Un bot peut accéder à des données de contexte supplémentaires sur une équipe ou une conversation sur laquelle il est installé. Ces informations peuvent être utilisées pour enrichir les fonctionnalités du bot et fournir une expérience plus personnalisée.

## <a name="fetch-the-roster-or-user-profile"></a>Récupérer la liste ou le profil utilisateur

Votre bot peut interroger la liste des membres et leurs profils utilisateur de base, notamment les ID d’utilisateur Teams et les informations de Azure Active Directory (AAD), telles que le nom et objectId. Vous pouvez utiliser ces informations pour corréler les identités des utilisateurs. Par exemple, pour vérifier si un utilisateur s’est connecté à un onglet via les informations d’identification AAD, est membre de l’équipe. Pour obtenir les membres de la conversation, la taille de page minimale ou maximale dépend de l’implémentation. La taille de page inférieure à 50, traitée comme 50 et supérieure à 500, est limitée à 500. Même si vous utilisez la version non pagaisée, elle n’est pas fiable dans les grandes équipes et ne doit pas être utilisée. Pour plus d’informations, voir [les modifications apportées aux API Teams bot pour](~/resources/team-chat-member-api-changes.md)récupérer des membres d’équipe ou de conversation.

L’exemple de code suivant utilise le point de terminaison pagyé pour récupérer la liste :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var members = new List<TeamsChannelAccount>();
        string continuationToken = null;

        do
        {
            var currentPage = await TeamsInfo.GetPagedMembersAsync(turnContext, 100, continuationToken, cancellationToken);
            continuationToken = currentPage.ContinuationToken;
            members.AddRange(currentPage.Members);
         }
         while (continuationToken != null);
     }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            var continuationToken;
            var members = [];

            do {
                var pagedMembers = await TeamsInfo.getPagedMembers(context, 100, continuationToken);
                continuationToken = pagedMembers.continuationToken;
                members.push(...pagedMembers.members);
            }
            while(continuationToken !== undefined)

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[JSON](#tab/json)

Vous pouvez émettre directement une requête GET sur , en utilisant la `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` valeur de comme point de `serviceUrl` terminaison. La valeur est `serviceUrl` stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée pour `serviceUrl` . La charge utile de réponse indique également si l’utilisateur est un utilisateur normal ou anonyme.

```http
GET /v3/conversations/19:meeting_N2QzYTA3YmItYmMwOC00OTJmLThkYzMtZWMzZGU0NGIyZGI0@thread.v2/pagedmembers?pageSize=100&continuationToken=asdfasdfalkdsjfalksjdf

Response body
{
   "continuationToken":"asdfqwerueiqpiewr",
   "members":[
      {
         "id":"29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
         "name":"Anon1 (Guest)",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"anonymous"
      },
      {
         "id":"29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
         "objectId":"76b0b09f-d410-48fd-993e-84da521a597b",
         "givenName":"John",
         "surname":"Patterson",
         "email":"johnp@fabrikam.com",
         "userPrincipalName":"johnp@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      },
      {
         "id":"29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
         "objectId":"6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
         "givenName":"Rick",
         "surname":"Stevens",
         "email":"Rick.Stevens@fabrikam.com",
         "userPrincipalName":"rstevens@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      }
   ]
}
```

* * *

Après avoir récupéré la liste ou le profil utilisateur, vous pouvez obtenir les détails d’un seul membre. Actuellement, pour récupérer des informations pour un ou plusieurs membres d’une conversation ou d’une équipe, utilisez les API Microsoft Teams bot pour C# ou pour les `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API TypeScript.

## <a name="get-single-member-details"></a>Obtenir les détails d’un seul membre

Vous pouvez également récupérer les détails d’un utilisateur particulier à l’aide Teams ID utilisateur, UPN ou ID d’objet AAD.

L’exemple de code suivant est utilisé pour obtenir les détails d’un seul membre :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        const member = await TeamsInfo.getMember(context, encodeURI('someone@somecompany.com'));

        // By calling next() you ensure that the next BotHandler is run.
        await next();
        });
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = await TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[JSON](#tab/json)

Vous pouvez émettre directement une requête GET sur , en utilisant la `/v3/conversations/{conversationId}/members/{userId}` valeur de comme point de `serviceUrl` terminaison. La valeur est `serviceUrl` stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée pour `serviceUrl` . Cela peut être utilisé pour les utilisateurs ordinaires et les utilisateurs anonymes.

Voici l’exemple de réponse pour un utilisateur normal :

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"user"
}
```

Voici l’exemple de réponse pour les utilisateurs anonymes :

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/<anonymous user id>"

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"anonymous"
}
```

* * *

Une fois que vous avez obtenir les détails d’un seul membre, vous pouvez obtenir les détails de l’équipe. Actuellement, pour récupérer des informations pour une équipe, utilisez les API Microsoft Teams bot pour C# `TeamsInfo.GetMemberDetailsAsync` ou `TeamsInfo.getTeamDetails` TypeScript.

## <a name="get-teams-details"></a>Obtenir les détails de l’équipe

Lorsqu’il est installé dans une équipe, votre bot peut interroger des métadonnées sur cette équipe, y compris l’ID de groupe AAD.

L’exemple de code suivant est utilisé pour obtenir les détails de l’équipe :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        TeamDetails teamDetails = await TeamsInfo.GetTeamDetailsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);
        if (teamDetails != null) {
            await turnContext.SendActivityAsync($"The groupId is: {teamDetails.AadGroupId}");
        }
        else {
            await turnContext.SendActivityAsync($"Message did not come from a channel in a team.");
        }
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const teamDetails = await TeamsInfo.getTeamDetails(turnContext);
            if (teamDetails) {
                await turnContext.sendActivity(`The group ID is: ${teamDetails.aadGroupId}`);
            } else {
                await turnContext.sendActivity('This message did not come from a channel in a team.');
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

Vous pouvez émettre directement une requête GET sur , en utilisant la `/v3/teams/{teamId}` valeur de comme point de `serviceUrl` terminaison. La valeur est `serviceUrl` stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée pour `serviceUrl` .

```http
GET /v3/teams/19:ja0cu120i1jod12j@skype.net

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "The Team Name",
    "aadGroupId": "02ce3874-dd86-41ba-bddc-013f34019978"
}
```

* * *

Une fois que vous avez des détails sur l’équipe, vous pouvez obtenir la liste des canaux d’une équipe. Actuellement, pour récupérer des informations pour une liste de canaux dans une équipe, utilisez les API de bot Microsoft Teams pour C# ou pour les `TeamsInfo.GetTeamChannelsAsync` `TeamsInfo.getTeamChannels` API TypeScript.

## <a name="get-the-list-of-channels-in-a-team"></a>Obtenir la liste des canaux d’une équipe

Votre bot peut interroger la liste des canaux d’une équipe.

> [!NOTE]
> * Le nom du canal général par défaut est renvoyé pour `null` autoriser la localisation.
> * L’ID de canal pour le canal général correspond toujours à l’ID d’équipe.

L’exemple de code suivant est utilisé pour obtenir la liste des canaux d’une équipe :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        IEnumerable<ChannelInfo> channels = await TeamsInfo.GetTeamChannelsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);

        await turnContext.SendActivityAsync($"The channel count is: {channels.Count()}");
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const channels = await TeamsInfo.getTeamChannels(turnContext);

            await turnContext.sendActivity(`The channel count is: ${channels.length}`);

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

Vous pouvez émettre directement une requête GET sur , en utilisant la `/v3/teams/{teamId}/conversations` valeur de comme point de `serviceUrl` terminaison. La valeur est `serviceUrl` stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée pour `serviceUrl` .

```http
GET /v3/teams/19%3A033451497ea84fcc83d17ed7fb08a1b6%40thread.skype/conversations

Response body
{
    "conversations": [{
        "id": "19:033451497ea84fcc83d17ed7fb08a1b6@thread.skype",
        "name": null
    }, {
        "id": "19:cc25e4aae50746ecbb11473bba24c70a@thread.skype",
        "name": "Materials"
    }, {
        "id": "19:b7b84cba410c406ba671dbbf5e0a3519@thread.skype",
        "name": "Design"
    }, {
        "id": "19:fc5db2aed489454e8f8c06829ed6c986@thread.skype",
        "name": "Marketing"
    }]
}
```

* * *

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Envoyer et recevoir des fichiers via le bot](~/bots/how-to/bots-filesv4.md)
