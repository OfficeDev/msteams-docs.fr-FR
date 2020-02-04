---
title: Envoyer et recevoir des fichiers
author: clearab
description: Comment envoyer et recevoir des fichiers avec votre robot Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e7d703f30dffaf317f22529ab56b76d859ebd8b6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673937"
---
# <a name="send-and-receive-files-with-a-bot"></a>Envoyer et recevoir des fichiers avec un bot

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Cet article explique comment échanger des fichiers avec un utilisateur dans une conversation un-à-un avec votre robot. Vous ne pouvez pas utiliser cette fonctionnalité pour échanger des fichiers dans une conversation d’équipe ou de groupe.

Vous pouvez choisir l’une des deux approches suivantes :

1. **API Microsoft Graph**, qui prend en charge les trois `personal`étendues `channel`:, et`groupchat`
2. Les API de Microsoft **teams bot**, `personal` qui prennent en charge uniquement l’étendue.

> [!NOTE] 
> L’envoi et la réception de fichiers sur des robots sur des appareils mobiles ne sont pas pris en charge.

## <a name="using-the-microsoft-graph-apis"></a>Utilisation des API Microsoft Graph

Vous pouvez publier des messages avec des pièces jointes référençant des fichiers SharePoint existants à l’aide des API Microsoft Graph pour [OneDrive et SharePoint](https://docs.microsoft.com/onedrive/developer/rest-api/). À l’aide des API Graph, vous devez obtenir un accès authentifié via le flux OAuth 2,0 standard pour :

- Dossier OneDrive d’un utilisateur (pour `personal` les `groupchat` fichiers et).
- Ou aux fichiers des canaux d’une équipe (pour `channel` les fichiers). Cette méthode fonctionne dans toutes les étendues Teams.

## <a name="using-the-teams-bot-apis"></a>Utilisation des API du bot teams

Votre robot peut directement envoyer et recevoir des fichiers avec des utilisateurs `personal` dans le contexte, également appelés conversations personnelles, à l’aide des API Teams. Cela vous permet d’implémenter des scénarios tels que la création de notes de frais, la reconnaissance d’image, l’archivage de fichiers, les signatures électroniques et d’autres scénarios impliquant une manipulation directe du contenu de fichier. Les fichiers partagés dans teams s’affichent généralement sous forme de cartes et permettent un affichage enrichi dans les applications.  L’API est fournie dans le cadre de la **plateforme Microsoft teams bot**.

> [!NOTE]
> Cette méthode fonctionne uniquement dans le `personal` contexte. Il ne fonctionne pas dans le `channel` contexte `groupchat` ou.

### <a name="configure-your-bot-to-support-files"></a>Configurer votre bot pour prendre en charge les fichiers

Pour envoyer et recevoir des fichiers dans votre robot, vous devez définir `supportsFiles` la propriété dans le manifeste `true`sur. Cette propriété est décrite dans la section [bots](https://docs.microsoft.com/microsoftteams/platform/resources/schema/manifest-schema#bots
) de la référence de manifeste.

Le paramètre se présente comme suit `"supportsFiles": true`:.

## <a name="invoke-activity-when-the-user-accepts-the-file-upload"></a>Appeler l’activité lorsque l’utilisateur accepte le téléchargement de fichiers

Le fichier est téléchargé vers le stockage **OneDrive** de l’utilisateur après l’émission de l’autorisation de téléchargement. Le bot reçoit une activité de message qui contient les métadonnées de fichier, telles que son nom et l’URL de contenu. Procédez comme suit :

1. Envoyer un message à l’utilisateur qui demande l’autorisation d’écriture du fichier. Ce message doit contenir une `FileConsentCard` pièce jointe avec le nom du fichier à télécharger.

    ![carte d’autorisation de chargement des fichiers bot](../../../assets/images/bots/bot-file-upload-permission-card.png)

2. Si l’utilisateur accepte le téléchargement de fichier, votre bot reçoit une activité d' *appel* avec une URL d’emplacement.
3. Pour transférer le fichier, votre bot effectue directement `HTTP POST` une URL d’emplacement fournie.
4. Vous pouvez également supprimer la carte de consentement d’origine si vous ne souhaitez pas autoriser l’utilisateur à accepter les téléchargements supplémentaires du même fichier.
 
L’exemple suivant montre une version abrégée de l’activité d’appel que votre bot recevra :

```json
{
    "name": "fileConsent/invoke",
    "type": "invoke",
    "timestamp": "2019-10-24T20:22:37.875Z",
    "localTimestamp": "2019-10-24T13:22:37.875-07:00",
    "id": "f:8805947989118514037",

    ...

    "value": {
        "type": "fileUpload",
        "action": "accept",
        "context": {
            "filename": "teams-logo.png"
        },
        "uploadInfo": {
            "contentUrl": "https://contoso.sharepoint.com//personal/<user alias>/Documents/Applications/TeamsFilesBot/teams-logo.png",
            "name": "teams-logo.png",
            "uploadUrl": "https://contoso.sharepoint.com//personal/<user alias>/_api/v2.0/drive/items/01FED6KHQXVVCUCI6XVJCZZMU2WMUSA6JS/uploadSession?guid=<GUID>",
            "uniqueId": "<Unique ID>",
            "fileType": "png"
        }
    },

    "locale": "en-US"
}

```

Le tableau suivant décrit les propriétés de contenu de la pièce jointe :

| Propriété | Objectif |
| --- | --- |
| `uploadUrl` | URL OneDrive pour le téléchargement du contenu du fichier. |
| `uniqueId` | ID de fichier unique. Il s’agit de l’ID d’élément de lecteur OneDrive. |
| `fileType` | Type d’extension de fichier, tel que PDF ou * png * *. |

Il est recommandé de reconnaître le téléchargement du fichier en renvoyant un message à l’utilisateur.

Si l’utilisateur refuse le fichier, votre bot reçoit l’événement suivant, avec le même nom d’activité global :

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "decline",
    "context": {
      ...
    }
  }
}
```

### <a name="notifying-the-user-about-an-uploaded-file"></a>Notification à l’utilisateur d’un fichier téléchargé

Après avoir téléchargé un fichier sur le OneDrive de l’utilisateur, vous devez envoyer un message de confirmation à l’utilisateur. Ce message doit contenir une `FileCard` pièce jointe sur laquelle l’utilisateur peut cliquer pour en afficher un aperçu, l’ouvrir dans OneDrive ou le télécharger localement. Voici un exemple. 

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "uniqueId": "<unique ID>",
      "fileType": "png",
    }
  }]
}

```

Le tableau suivant décrit les propriétés de contenu de la pièce jointe :

| Propriété | Objectif |
| --- | --- |
| `uniqueId` | ID d’élément de lecteur OneDrive/SharePoint. |
| `fileType` | Type de fichier, tel que PDF ou docx. |

## <a name="example-using-the-bot-framework-sdk"></a>Exemple d’utilisation du kit de développement logiciel de robot Framework

L’exemple suivant montre comment gérer les téléchargements de fichiers et envoyer des demandes de consentement de fichier à l’utilisateur dans la boîte de dialogue du bot. Les extraits de code présentés ci-dessous appartiennent à un exemple exécutable complet que vous pouvez télécharger à cet emplacement : [FileUpload](https://github.com/microsoft/botbuilder-dotnet/tree/master/tests/Teams/FileUpload).

# <a name="cnettabdotnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    bool messageWithFileDownloadInfo = turnContext.Activity.Attachments?[0].ContentType == FileDownloadInfo.ContentType;
    if (messageWithFileDownloadInfo)
    {
        var file = turnContext.Activity.Attachments[0];
        var fileDownload = JObject.FromObject(file.Content).ToObject<FileDownloadInfo>();

        string filePath = Path.Combine("Files", file.Name);

        var client = _clientFactory.CreateClient();
        var response = await client.GetAsync(fileDownload.DownloadUrl);
        using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
        {
            await response.Content.CopyToAsync(fileStream);
        }

        var reply = ((Activity)turnContext.Activity).CreateReply();
        reply.TextFormat = "xml";
        reply.Text = $"Complete downloading <b>{file.Name}</b>";
        await turnContext.SendActivityAsync(reply, cancellationToken);
    }
    else
    {
        string filename = "teams-logo.png";
        string filePath = Path.Combine("Files", filename);
        long fileSize = new FileInfo(filePath).Length;
        await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
    }
}

private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { "filename", filename },
    };

    var fileCard = new FileConsentCard
    {
        Description = "This is the file I want to send you",
        SizeInBytes = filesize,
        AcceptContext = consentContext,
        DeclineContext = consentContext,
    };

    var asAttachment = new Attachment
    {
        Content = fileCard,
        ContentType = FileConsentCard.ContentType,
        Name = filename,
    };

    var replyActivity = turnContext.Activity.CreateReply();
    replyActivity.Attachments = new List<Attachment>() { asAttachment };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}

protected override async Task OnTeamsFileConsentAcceptAsync(ITurnContext<IInvokeActivity> turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    try
    {
        JToken context = JObject.FromObject(fileConsentCardResponse.Context);

        string filePath = Path.Combine("Files", context["filename"].ToString());
        long fileSize = new FileInfo(filePath).Length;
        var client = _clientFactory.CreateClient();
        using (var fileStream = File.OpenRead(filePath))
        {
            var fileContent = new StreamContent(fileStream);
            fileContent.Headers.ContentLength = fileSize;
            fileContent.Headers.ContentRange = new ContentRangeHeaderValue(0, fileSize - 1, fileSize);
            await client.PutAsync(fileConsentCardResponse.UploadInfo.UploadUrl, fileContent, cancellationToken);
        }

        await FileUploadCompletedAsync(turnContext, fileConsentCardResponse, cancellationToken);
    }
    catch (Exception e)
    {
        await FileUploadFailedAsync(turnContext, e.ToString(), cancellationToken);
    }
}

protected override async Task OnTeamsFileConsentDeclineAsync(ITurnContext<IInvokeActivity> turnContext, FileConsentCardResponse fileConsentCardResponse, CancellationToken cancellationToken)
{
    JToken context = JObject.FromObject(fileConsentCardResponse.Context);

    var reply = ((Activity)turnContext.Activity).CreateReply();
    reply.TextFormat = "xml";
    reply.Text = $"Declined. We won't upload file <b>{context["filename"]}</b>.";
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[Machine à écrire/node. js](#tab/typescript)

<!-- From sample: libraries\botbuilder\tests\teams\fileUpload\src\fileUploadBot.ts-->

```typescript

export class FileUploadBot extends TeamsActivityHandler {
    constructor() {
        super();

        this.onMessage(async (context, next) => {
            await this.sendFileCard(context);
            await next();
        });

        this.onMembersAdded(async (context, next) => {
            const membersAdded = context.activity.membersAdded;
            for (const member of membersAdded) {
                if (member.id !== context.activity.recipient.id) {
                    await context.sendActivity('Hello and welcome!');
                }
            }
            await next();
        });
    }

    private async sendFileCard(context: TurnContext): Promise<void> {
        let filename = "file name";
        let fs = require('fs'); 
        let path = require('path');
        let stats = fs.statSync(path.join('files', filename));
        let fileSizeInBytes = stats['size'];

        let fileContext = {
            filename: filename
        };

        let attachment = {
            content: <FileConsentCard>{
                description: 'This is the file I want to send you',
                fileSizeInBytes: fileSizeInBytes,
                acceptContext: fileContext,
                declineContext: fileContext
            },
            contentType: 'application/vnd.microsoft.teams.card.file.consent',
            name: filename
        } as Attachment;

        var replyActivity = this.createReply(context.activity);
        replyActivity.attachments = [ attachment ];
        await context.sendActivity(replyActivity);
    }

    protected async handleTeamsFileConsentAccept(context: TurnContext, fileConsentCardResponse: FileConsentCardResponse): Promise<void> {
        try {
            await this.sendFile(fileConsentCardResponse);
            await this.fileUploadCompleted(context, fileConsentCardResponse);
        }
        catch (err) {
            await this.fileUploadFailed(context, err.toString());
        }
    }

    protected async handleTeamsFileConsentDecline(context: TurnContext, fileConsentCardResponse: FileConsentCardResponse): Promise<void> {
        let reply = this.createReply(context.activity);
        reply.textFormat = "xml";
        reply.text = `Declined. We won't upload file <b>${fileConsentCardResponse.context["filename"]}</b>.`;
        await context.sendActivity(reply);
    }
...

}

```

<!-- Python samples verify -->

# <a name="pythontabpython"></a>[Python](#tab/python)

```python
class TeamsFileUploadBot(TeamsActivityHandler):
    async def on_message_activity(self, turn_context: TurnContext):
        message_with_file_download = (
            False
            if not turn_context.activity.attachments
            else turn_context.activity.attachments[0].content_type == ContentType.FILE_DOWNLOAD_INFO
        )

        if message_with_file_download:
            # Save an uploaded file locally
            file = turn_context.activity.attachments[0]
            file_download = FileDownloadInfo.deserialize(file.content)
            file_path = "files/" + file.name

            response = requests.get(file_download.download_url, allow_redirects=True)
            open(file_path, "wb").write(response.content)

            reply = self._create_reply(
                turn_context.activity, f"Complete downloading <b>{file.name}</b>", "xml"
            )
            await turn_context.send_activity(reply)
        else:
            # Attempt to upload a file to Teams.  This will display a confirmation to
            # the user (Accept/Decline card).  If they accept, on_teams_file_consent_accept
            # will be called, otherwise on_teams_file_consent_decline.
            filename = "teams-logo.png"
            file_path = "files/" + filename
            file_size = os.path.getsize(file_path)
            await self._send_file_card(turn_context, filename, file_size)

    async def _send_file_card(
            self, turn_context: TurnContext, filename: str, file_size: int
    ):
        """
        Send a FileConsentCard to get permission from the user to upload a file.
        """

        consent_context = {"filename": filename}

        file_card = FileConsentCard(
            description="This is the file I want to send you",
            size_in_bytes=file_size,
            accept_context=consent_context,
            decline_context=consent_context
        )

        as_attachment = Attachment(
            content=file_card.serialize(), content_type=ContentType.FILE_CONSENT_CARD, name=filename
        )

        reply_activity = self._create_reply(turn_context.activity)
        reply_activity.attachments = [as_attachment]
        await turn_context.send_activity(reply_activity)

    async def on_teams_file_consent_accept(
            self,
            turn_context: TurnContext,
            file_consent_card_response: FileConsentCardResponse
    ):
        """
        The user accepted the file upload request.  Do the actual upload now.
        """

        file_path = "files/" + file_consent_card_response.context["filename"]
        file_size = os.path.getsize(file_path)

        headers = {
            "Content-Length": f"\"{file_size}\"",
            "Content-Range": f"bytes 0-{file_size-1}/{file_size}"
        }
        response = requests.put(
            file_consent_card_response.upload_info.upload_url, open(file_path, "rb"), headers=headers
        )

        if response.status_code != 200:
            await self._file_upload_failed(turn_context, "Unable to upload file.")
        else:
            await self._file_upload_complete(turn_context, file_consent_card_response)

    async def on_teams_file_consent_decline(
            self,
            turn_context: TurnContext,
            file_consent_card_response: FileConsentCardResponse
    ):
        """
        The user declined the file upload.
        """

        context = file_consent_card_response.context

        reply = self._create_reply(
            turn_context.activity,
            f"Declined. We won't upload file <b>{context['filename']}</b>.",
            "xml"
        )
        await turn_context.send_activity(reply)

    async def _file_upload_complete(
            self,
            turn_context: TurnContext,
            file_consent_card_response: FileConsentCardResponse
    ):
        """
        The file was uploaded, so display a FileInfoCard so the user can view the
        file in Teams.
        """

        name = file_consent_card_response.upload_info.name

        download_card = FileInfoCard(
            unique_id=file_consent_card_response.upload_info.unique_id,
            file_type=file_consent_card_response.upload_info.file_type
        )

        as_attachment = Attachment(
            content=download_card.serialize(),
            content_type=ContentType.FILE_INFO_CARD,
            name=name,
            content_url=file_consent_card_response.upload_info.content_url
        )

        reply = self._create_reply(
            turn_context.activity,
            f"<b>File uploaded.</b> Your file <b>{name}</b> is ready to download",
            "xml"
        )
        reply.attachments = [as_attachment]

        await turn_context.send_activity(reply)

    async def _file_upload_failed(self, turn_context: TurnContext, error: str):
        reply = self._create_reply(
            turn_context.activity,
            f"<b>File upload failed.</b> Error: <pre>{error}</pre>",
            "xml"
        )
        await turn_context.send_activity(reply)

    def _create_reply(self, activity, text=None, text_format=None):
        return Activity(
            type=ActivityTypes.message,
            timestamp=datetime.utcnow(),
            from_property=ChannelAccount(
                id=activity.recipient.id, name=activity.recipient.name
            ),
            recipient=ChannelAccount(
                id=activity.from_property.id, name=activity.from_property.name
            ),
            reply_to_id=activity.id,
            service_url=activity.service_url,
            channel_id=activity.channel_id,
            conversation=ConversationAccount(
                is_group=activity.conversation.is_group,
                id=activity.conversation.id,
                name=activity.conversation.name,
            ),
            text=text or "",
            text_format=text_format or None,
            locale=activity.locale,
        )


```

---
