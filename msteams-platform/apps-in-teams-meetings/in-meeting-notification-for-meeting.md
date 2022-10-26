---
title: Générer une notification en réunion pour une réunion Teams
author: v-sdhakshina
description: Dans cet article, découvrez comment créer une notification en réunion pour une réunion Microsoft Teams et son exemple de code.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: e62958535fa1bcbcdeb104b5fd5fdd2882250aa3
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699128"
---
# <a name="build-in-meeting-notification-for-teams-meeting"></a>Générer une notification en réunion pour une réunion Teams

La notification en réunion est utilisée pour impliquer les participants et collecter des informations ou des commentaires pendant la réunion. Utilisez une [charge utile de notification en réunion](meeting-apps-apis.md#send-an-in-meeting-notification) pour déclencher une notification en réunion. Dans le cadre de la demande de charge utile de notification, incluez l’URL où le contenu à afficher est hébergé.

Une URL de ressource externe est utilisée pour afficher la notification en réunion. Vous pouvez utiliser la `submitTask` méthode pour envoyer des données dans une conversation de réunion.

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="La capture d’écran est un exemple qui montre comment utiliser une boîte de dialogue en réunion.":::

Vous pouvez également ajouter l’image d’affichage Teams et la carte de contacts de l’utilisateur à la notification en réunion en fonction du jeton `onBehalfOf` avec l’utilisateur NULL et le nom d’affichage transmis dans la charge utile. Voici un exemple de charge utile :

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="Cette capture d’écran montre comment Teams affiche l’image et la carte des personnes sont utilisés avec la boîte de dialogue en réunion." border="true":::

## <a name="code-sample"></a>Exemple de code

Exemple de nom | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Notification en réunion | Montre comment implémenter la notification en réunion à l’aide d’un bot. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../sbs-meeting-content-bubble.yml) pour générer une notification en réunion dans votre réunion Teams.

## <a name="see-also"></a>Voir aussi

* [Onglets générer pour la réunion](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Créer des applications pour la phase de réunion Teams](build-apps-for-teams-meeting-stage.md)
* [Créer une conversation extensible pour la conversation de réunion](build-extensible-conversation-for-meeting-chat.md)
* [Créer des applications pour les utilisateurs anonymes](build-apps-for-anonymous-user.md)
* [API de réunion avancées](meeting-apps-apis.md)
