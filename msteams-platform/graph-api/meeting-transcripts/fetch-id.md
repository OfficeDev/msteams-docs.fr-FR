---
title: Obtenir l’ID de réunion et l’ID d’organisateur pour récupérer les transcriptions de réunion
description: Décrit le processus d’obtention de l’ID de réunion et de l’ID d’organisateur pour récupérer les transcriptions de réunion
ms.localizationpriority: high
ms.topic: concept
ms.openlocfilehash: 8be611f72a1ddac84bbe596a1bfc00621cb7c038
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027311"
---
# <a name="obtain-meeting-id-and-organizer-id"></a>Obtenir l’ID de réunion et l’ID d’organisateur

Votre application peut récupérer les transcriptions d’une réunion à l’aide de l’ID de réunion et de l’ID utilisateur de l’organisateur de la réunion, également appelé ID d’organisateur. Les API REST Graph récupèrent les transcriptions en fonction de l’ID de réunion et de l’ID d’organisateur qui sont passés en tant que paramètres dans l’API.

> [!NOTE]
> L’ID de réunion pour les réunions planifiées peut expirer dans quelques jours s’il n’est pas utilisé. Elle peut être relancée à l’aide de l’URL de la réunion pour rejoindre la réunion. Pour plus d’informations sur la chronologie d’expiration des réunions pour différents types de réunions, consultez [Expiration de la réunion](/microsoftteams/limits-specifications-teams#meeting-expiration).

Pour obtenir l’ID de réunion et l’ID d’organisateur pour récupérer la transcription, choisissez l’une des deux méthodes suivantes :

- [S'abonner aux notifications de changement](#subscribe-to-change-notifications)
- [Utiliser Bot Framework](#use-bot-framework-to-get-meeting-id-and-organizer-id)

### <a name="subscribe-to-change-notifications"></a>S'abonner aux notifications de changement

Vous pouvez vous abonner à votre application pour recevoir des notifications de modification pour les événements de réunion planifiés. Lorsque votre application est avertie des événements de réunion abonnés, elle peut obtenir des transcriptions, si elle est autorisée via les autorisations Azure AD requises.

Votre application reçoit une notification pour le type d’événements de réunion auxquels elle est abonnée :

- [Notification au niveau de l’utilisateur](#obtain-meeting-details-using-user-level-notification)
- [Notification au niveau du locataire](#obtain-meeting-details-using-tenant-level-notification)

Lorsque votre application est avertie d’un événement de réunion abonné, elle peut récupérer l’ID et l’ID de l’organisateur de la réunion à partir du message de notification. En fonction des détails de la réunion obtenus, votre application peut extraire les transcriptions de la réunion une fois la réunion terminée.

#### <a name="obtain-meeting-details-using-user-level-notification"></a>Obtenir les détails de la réunion à l’aide d’une notification au niveau de l’utilisateur

Choisissez d’abonner votre application aux notifications au niveau de l’utilisateur pour obtenir les transcriptions de l’événement de réunion d’un utilisateur particulier. Lorsqu’une réunion est planifiée pour cet utilisateur, votre application est avertie. Votre application peut également recevoir des notifications de réunion à l’aide d’événements de calendrier.

Pour vous abonner à des événements de calendrier de votre application, consultez [notifications de modification pour les ressources Outlook dans Microsoft Graph](/graph/outlook-change-notifications-overview).

Utilisez l’exemple suivant pour vous abonner aux notifications au niveau de l’utilisateur :

```http
    
POST https://graph.microsoft.com/v1.0/subscriptions/
{
    "changeType": "created,updated,deleted",
    "notificationUrl": "https://webhook.azurewebsites.net/api/send/myNotifyClient",
    "resource": "users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events",
    "expirationDateTime": "2022-05-05T14:58:56.7951795+00:00",
    "clientState": "ClientSecret",
    "includeResourceData": false
}
```

Lorsque votre application est avertie d’un événement de réunion abonnée, elle recherche l’ID d’événement de calendrier dans la notification. Utilisez l’ID d’événement pour récupérer `JoinWebUrl` un ID de conversation spécifique et vous abonner à ses messages. Une fois que votre application s’est abonnée aux messages de conversation, suivez les [étapes fournies pour les notifications au niveau du locataire](#obtain-meeting-details-using-tenant-level-notification) afin d’obtenir l’ID de réunion et l’ID d’organisateur.

Pour obtenir l’ID de réunion et l’ID d’organisateur à partir d’une notification au niveau de l’utilisateur :

1. **Obtenir l’ID d’événement** : votre application obtient la `eventId` propriété à partir de la charge utile de notification.

    <details>
    <summary><b>Exemple</b> : Charge utile de notification</summary>

    ```json
    {
        "subscriptionId": "ef30cdc6-b5ae-4702-b924-f458fd9e5fc3",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "clientState": "ClientSecret",
        "subscriptionExpirationDateTime": "2022-05-05T07:54:53.1886542-07:00",
        "resource": "Users/1273a016-201d-4f95-8083-1b7f99b3edeb/Events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",
        "resourceData": {}
    }
    ```

    Dans cet exemple, le `eventID` contenu est `resource` *AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=*.
    </details>

2. **Obtenir l’URL de la réunion** : utilisez l’ID d’événement pour récupérer `joinUrl` l’URL de la réunion.

    Pour plus d’informations, consultez [l’événement Get](/graph/api/event-get).

    Utilisez l’exemple suivant pour demander l’URL de la réunion :

    ```http
    GET https://graph.microsoft.com/v1.0/users/1273a016-201d-4f95-8083-1b7f99b3edeb/events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=
    ```

    La charge utile de réponse contient `joinURL`.

    <details>
    <summary><b>Exemple</b> : charge utile de réponse pour obtenir l’URL de la réunion</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events/$entity",
        "@odata.etag": "W/\"xRVh47aDEU6na1ckNYfMiwABb2Twsg==\"",
        "id": "AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",    
        "start": {
            "dateTime": "2022-05-06T15:00:00.0000000",
            "timeZone": "UTC"
        },
        "end": {
            "dateTime": "2022-05-06T15:30:00.0000000",
            "timeZone": "UTC"
        },
            
        "onlineMeeting": {
            "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MjExYzJiMTItZDY1MS00ZGZkLWE5YzQtZTBmNWI1MDg2M2Uw%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%221273a016-201d-4f95-8083-1b7f99b3edeb%22%7d",
            "conferenceId": "438824583",
            "tollNumber": "+1 213-279-1007"
        }    
    }
    ```

    </details>

    L’URL de la réunion est contenue dans `joinUrl`.

3. **Obtenir l’ID de thread de conversation** : utilisez l’URL de réunion obtenue `joinUrl` pour obtenir l’ID du fil de conversation. Spécifiez cette URL de réunion comme valeur pour le paramètre lors de l’extraction `joinWebUrl` de la réunion associée.

    Utilisez l’exemple suivant pour demander l’ID de thread :

    ``` http
    GET https://graph.microsoft.com/v1.0/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    La charge utile de réponse contient le `threadID` membre dans la `chatInfo` propriété.
    <br>
    <details>
    <summary><b>Exemple</b> : Charge utile de réponse avec iD de thread</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

    L’ID de conversation est contenu dans `threadId`.

4. **S’abonner aux messages de conversation** : utilisez l’ID de conversation pour vous abonner à votre application afin de recevoir des messages de conversation pour cette réunion particulière. Pour plus d’informations, consultez [S’abonner aux messages dans une conversation](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-in-a-chat).

    Si vous souhaitez que votre application s’abonne à des messages avec du texte spécifique, consultez [S’abonner aux messages d’une conversation contenant du texte spécifique](/graph/teams-changenotifications-chatmessage#example-2-subscribe-to-messages-in-a-chat-that-contain-certain-text).

5. Suivez les [étapes des notifications au niveau du locataire](#obtain-meeting-details-using-tenant-level-notification) pour obtenir l’ID de réunion et l’ID d’organisateur.

#### <a name="obtain-meeting-details-using-tenant-level-notification"></a>Obtenir les détails de la réunion à l’aide d’une notification au niveau du locataire

Les notifications au niveau du locataire sont utiles si votre application est autorisée à accéder à toutes les transcriptions de réunion dans le locataire. Abonnez-vous à votre application pour être avertie des événements lors du démarrage de la transcription ou de la fin de l’appel pour les réunions Teams en ligne planifiées. Une fois la réunion terminée, votre application peut accéder à la transcription de la réunion et la récupérer.

Pour vous abonner à des notifications au niveau du locataire, consultez [Obtenir des notifications de modification](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-across-all-chats).

Lorsque votre application est avertie des événements de réunion abonnés, elle recherche dans les notifications la transcription démarrée et les événements de fin de réunion. Ces événements contiennent l’ID de conversation, qui est utilisé pour obtenir l’entité de conversation, puis l’ID de réunion et l’ID d’organisateur.

Pour obtenir l’ID de réunion et l’ID d’organisateur à partir d’une notification au niveau du locataire :

1. **Obtenir l’ID de conversation** : votre application obtient la `chatId` propriété de la notification pour effectuer des appels ultérieurs. Votre application peut obtenir l’ID de conversation à partir des charges utiles de :

    - Événement de démarrage de la transcription : `callTranscriptEventMessageDetail` type d’événement

        <details>
        <summary><b>Exemple</b> : Charge utile pour l’événement de démarrage de la transcription</summary>

        ```json
        {
        "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787549174')",
        "contentDecryptedBySimulator": {
            "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
            "messageType": "systemEventMessage",
            "createdDateTime": "2022-04-12T18:19:09.174Z",
            "lastModifiedDateTime": "2022-04-12T18:19:09.174Z",
            "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
            "body": {
                "contentType": "html",
                "content": "<systemEventMessage/>"
            },
            "channelIdentity": null,
            "eventDetail": {
                "@odata.type": "#Microsoft.Teams.GraphSvc.callTranscriptEventMessageDetail",
                "callId": "16481de8-3262-419b-abc7-0139e6239515",
                "callTranscriptICalUid": "",
                "meetingOrganizer": {
                    "application": null,
                    "device": null,
                    "user": {
                    "userIdentityType": "aadUser",
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null
                        }
                    }
                }
            },
            "encryptedContent": {}
        }
        ```

        </details>

    - Événement de fin d’appel :  `callEndedEventMessageDetail` type d’événement

        <details>
        <summary><b>Exemple</b> : Charge utile pour l’événement de fin d’appel</summary>

        ```json
        {
            "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
            "changeType": "created",
            "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
            "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787585457')",
            "resourceData": {},
            "contentDecryptedBySimulator": {
                "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
                "createdDateTime": "2022-04-12T18:19:45.457Z",
                "lastModifiedDateTime": "2022-04-12T18:19:45.457Z",     
                "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
                "eventDetail": {
                    "@odata.type": "#Microsoft.Teams.GraphSvc.callEndedEventMessageDetail",
                    "callId": null,
                    "callDuration": "PT1M44S",
                    "callEventType": "meeting",
                    "callParticipants": [
                    ],
                    "initiator": {
        
                    }
                }
            },
            "encryptedContent": {
                    
            }
        }
        ```

        </details>

2. **Obtenir l’entité de conversation** : votre application peut récupérer l’entité de conversation à l’aide de l’ID de conversation obtenu à l’étape 1. Utilisez l’entité de conversation pour obtenir l’URL permettant de rejoindre l’appel. Le `joinWebUrl` membre de la `onlineMeetingInfo` propriété contient cette URL et est utilisé pour obtenir l’ID de réunion éventuellement. L’ID d’organisateur fait également partie de la charge utile de la réponse.

    Pour plus d’informations sur l’entité de conversation, consultez [Obtenir une conversation](/graph/api/chat-get).

    Utilisez l’exemple suivant pour demander l’entité de conversation en fonction de l’ID de conversation :

    ``` http
    GET https://graph.microsoft.com/v1.0/chats/19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2
    ```

    La charge utile de réponse contient les éléments suivants :

    - **ID de l’organisateur** : il est contenu dans le `id` membre de la `organizer` propriété dans la charge utile de réponse.
    - **URL de l’appel de réunion** : cette URL est utilisée pour récupérer l’ID de réunion, et elle est disponible dans la charge utile de réponse dans l’un des deux scénarios :
        - Si la réunion est une réunion Teams en ligne, le `joinWebUrl` membre de la `onlineMeetingInfo` propriété contient cette URL.
        - Si la réunion n’a pas été créée en tant que réunion en ligne à partir du client Teams ou du client Outlook, elle contient le `calendarEventId` membre dans la `onlineMeetingInfo` propriété. Votre application peut utiliser le `calendarEventId` pour obtenir `joinUrl`, qui est le même que `joinWebUrl`.

      Pour plus d’informations sur les événements, consultez [Obtenir un événement](/graph/api/event-get?view=graph-rest-1.0&tabs=http&preserve-view=true).

      Exemples de scénarios de charge utile de réponse en fonction du type d’URL de la réunion de participation :

        - Réunion Teams en ligne où `joinWebUrl` est disponible

            <details>
            <summary><b>Exemple</b> : Charge utile de réponse pour une réunion en ligne</b></summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2",
                "topic": "Test Meet Create Online Meeting",
                "createdDateTime": "2022-04-14T11:30:45.903Z",
                "lastUpdatedDateTime": "2022-04-26T06:27:45.265Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                "calendarEventId": null,
                    "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

        - Réunion planifiée via le client Teams ou le client Outlook, non marquée comme réunion en ligne lorsque celle-ci `calendarEventId` est disponible

            <details>
            <summary><b>Exemple</b> : Charge utile de réponse pour la réunion non marquée comme étant en ligne</summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm@thread.v2",
                "topic": "Non Online Meeting Teams Client",
                "createdDateTime": "2022-04-26T09:43:23.711Z",
                "lastUpdatedDateTime": "2022-04-26T09:43:46.157Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                    "calendarEventId": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYeAAA=",
                    "joinWebUrl": null,
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

            - Utilisez l’exemple suivant pour obtenir `joinWebUrl` à partir des éléments suivants `calendarEventId`:

              ``` http
                GET https://graph.microsoft.com/beta/users/14b779ae-cb64-47e7-a512-52fd50a4154d/events/AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=
              ```

              Dans cet exemple :

                - L’ID de l’organisateur est *14b779ae-cb64-47e7-a512-52fd50a4154d*.

              La charge utile de réponse de cette requête contient `joinUrl` dans la `onlineMeeting` propriété.

                > [!NOTE]
                > `joinUrl` est identique à `joinWebUrl`.

              <br>
              <details>
              <summary><b>Exemple</b> : charge utile de réponse qui contient l’URL de participation à la réunion</summary>

              ```json
              {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/events/$entity",
                "@odata.etag": "W/\"bMMOQZSMbU+4hcmFq11dwAAAkc3Tmw==\"",
                "id": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=",    
                "start": {
                    "dateTime": "2022-04-26T10:30:00.0000000",
                    "timeZone": "UTC"
                },
                "end": {
                    "dateTime": "2022-04-26T11:00:00.0000000",
                    "timeZone": "UTC"
                },    
                "onlineMeeting": {
                    "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d"
                },
                "calendar@odata.associationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')/$ref",
                "calendar@odata.navigationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')"
                }
                ```

              </details>

3. **Obtenir l’ID de réunion** : à présent, votre application peut utiliser `joinWebUrl` pour obtenir l’ID de réunion.

    Utilisez l’exemple suivant pour demander l’ID de réunion en ligne :

    ``` http
    GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    La charge utile de réponse contient l’ID de réunion dans le `id` membre de la `value` propriété.
    <br>
    <details>
    <summary><b>Exemple</b> : charge utile de réponse avec ID de réunion</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

4. **Extraire la transcription** : l’ID d’organisateur et l’ID de réunion obtenus dans les étapes 2 et 3 permettent à votre application d’extraire les transcriptions de cet événement de réunion particulier.

    Pour extraire des transcriptions, vous devez :

    1. **Récupérez l’ID de transcription en fonction de l’ID de l’organisateur et de la réunion** :

       Utilisez l’exemple suivant pour demander l’ID de transcription :

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts
        ```

        Dans cet exemple :

        - L’ID de réunion est inclus comme valeur pour `onlineMeetings`: *MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bW VldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM 1pqWTJAdGhyZWFkLnYy*.
        - L’ID de l’organisateur est *14b779ae-cb64-47e7-a512-52fd50a4154d*.

        La charge utile de réponse contient l’ID de transcription pour l’ID de réunion et l’ID d’organisateur dans le `id` membre de la `value` propriété.
        <br>
        <details>
        <summary><b>Exemple</b> : Charge utile de réponse pour obtenir l’ID de transcription</summary>

        ```json
        {
            "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts",
            "@odata.count": 1,
            "value": [
                {
                    "id": "MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh",
                    "createdDateTime": "2022-04-14T11:34:39.5662792Z"
                }
            ]
        }
        ```

        Dans cet exemple, l’ID de transcription est *MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh*.

        </details>

    1. **Accédez à la transcription de la réunion et obtenez-la en fonction de l’ID de transcription** :

        Utilisez l’exemple suivant pour demander les transcriptions d’une réunion spécifique au `.vtt` format suivant :

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts('MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh')/content?$format=text/vtt
        ```

        La charge utile de réponse contiendra les transcriptions au `.vtt` format.

### <a name="use-bot-framework-to-get-meeting-id-and-organizer-id"></a>Utiliser Bot Framework pour obtenir l’ID de réunion et l’ID d’organisateur

Votre application peut utiliser Bot Framework pour obtenir l’ID de réunion et l’ID d’organisateur. Le bot peut recevoir automatiquement des événements de début ou de fin de réunion à partir de toutes les réunions créées dans tous les canaux en ajoutant  au manifeste pour l’autorisation RSC.

Utilisez l’exemple suivant pour obtenir l’ID de réunion et l’ID d’organisateur à l’aide d’une application bot :

```json
GET /v1/meetings/{meetingId}
```

La charge utile de réponse contient :

- ID de réunion dans le `msGraphResourceId` membre de la `details` propriété.
- ID de l’organisateur dans le `id` membre de la `organizer` propriété.
<br>
<details>
<summary><b>Exemple</b> : charge utile de réponse pour obtenir les détails de la réunion</b></summary>

```json
{
  details: {
    id: "MCMxOTptZWV0aW5nX05XTTFNVEk1TnpNdE5qZ3pNeTAwWVdRNExUaG1PV1F0WlRnM01UQm1PVGczWW1VekB0aHJlYWQudjIjMA==",
    msGraphResourceId: "MSo2NzAyYWZiNi0xMDliLTRjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVldGluZ19OV00xTVRJNU56TXROamd6TXkwMFlXUTRMVGhtT1dRdFpUZzNNVEJtT1RnM1ltVXpAdGhyZWFkLnYy",
    scheduledStartTime: {
    },
    scheduledEndTime: {
    },
    joinUrl: "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz%40thread.v2/0?context=%7b%22Tid%22%3a%22b3cdf1c8-024a-49e2-a994-f67f830b02f3%22%2c%22Oid%22%3a%226702afb6-109b-4c32-a141-6e65469502b9%22%7d",
    title: "Testing meeting bot 1 - Hun",
    type: "Scheduled",
  },
  conversation: {
    id: "19:meeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz@thread.v2",
    isGroup: true,
    conversationType: "groupChat",
  },
  organizer: {
    id: "29:1VZkVr77S3GW_RdAXKrfgFeytpqMegL3tkKvEbwrPqoCVvmqrlKtVrfKWUY7xIM-bZIx4Sq-p1MjdjSZnb5W20w",
    tenantId: "b3cdf1c8-024a-49e2-a994-f67f830b02f3",
    aadObjectId: "6702afb6-109b-4c32-a141-6e65469502b9",
  },
}
```

Dans cet exemple :

- L’ID de réunion est inclus comme valeur pour `msGraphResourceId`: *MSo2NzAyYWZiNi0xMDliLTRjMjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVl dGluZ19OV00xTVRJNU56TXROamd6TXkwMFlXUTRMVGhtT1dRdFpUZzNNVEJtT1RnM 1ltVXpAdGhyZWFkLnYy*.
- L’ID d’organisateur est contenu comme valeur pour `aadObjectId` `organizer`:  *6702afb6-109b-4c32-a141-6e65469502b9*.

</details>

Une fois que votre application a obtenu l’ID de réunion et l’ID d’organisateur, elle déclenche les API Graph pour extraire le contenu de la transcription à l’aide de ces détails de réunion.

### <a name="code-samples"></a>Exemples de code

Vous pouvez essayer l’exemple de code suivant pour une application bot :

| **Exemple de nom** | **Description** | **C#** | **Node.js** |
|----------------|-----------------|--------------|--------------|--------------|
| Transcription de réunion | Il s’agit d’un exemple d’application qui montre comment obtenir transcript à l’aide de API Graph et l’afficher dans le module de tâche. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/nodejs) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [API Graph pour extraire des transcriptions](/graph/api/resources/calltranscript)
