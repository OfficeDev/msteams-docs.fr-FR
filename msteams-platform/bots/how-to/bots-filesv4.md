---
title: Envoyez et recevez des fichiers par le biais du robot
description: Apprenez à envoyer et à recevoir des fichiers par le biais du robot en utilisant les API graphiques pour les scopes personnels, de canal et de discussion de groupe. Utilisez les API des robots Teams à l'aide d'échantillons de code basés sur le SDK v4 du cadre des robots.
keywords: équipes robots fichiers envoyer recevoir
ms.date: 05/20/2019
ms.localizationpriority: high
ms.topic: how-to
ms.openlocfilehash: 102bdeb2cd05882266299f7962a6b69b1ecfa37c
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111212"
---
# <a name="send-and-receive-files-through-the-bot"></a>Envoyez et recevez des fichiers par le biais du robot

> [!IMPORTANT]
> Les articles de ce document sont basés sur le Bot Framework SDK v4.

Il y a deux façons d'envoyer des fichiers à un robot et de recevoir des fichiers de celui-ci :

* [**Utilisez les API graphiques de Microsoft :**](#use-the-graph-apis) Cette méthode fonctionne pour les robots dans toutes les portées de Microsoft Teams :
  * `personal`
  * `channel`
  * `groupchat`

* [**Utilisez les API des robots Teams :**](#use-the-teams-bot-apis)Celles-ci ne prennent en charge que les fichiers en`personal` contexte.

## <a name="use-the-graph-apis"></a>Utiliser les API graphiques

Publier des messages avec des cartes jointes qui font référence à des fichiers SharePoint existants, en utilisant les API graphiques pour [OneDrive et SharePoint](/onedrive/developer/rest-api/). Pour utiliser les API graphiques, obtenez l'accès à l'un des éléments suivants par le biais du flux d'autorisation OAuth 2.0 standard :

* Le dossier OneDrive d'un utilisateur pour `personal` et `groupchat` fichiers.
* Les fichiers dans le canal d'une équipe pour `channel` les fichiers.

Les API graphiques fonctionnent dans toutes les portées de Teams. Pour plus d'informations, voir [la section Envoyer des pièces jointes aux messages de conversation](/graph/api/chatmessage-post?view=graph-rest-beta&tabs=http#example-4-file-attachments&preserve-view=true).

Vous pouvez également envoyer des fichiers à un robot et en recevoir de celui-ci à l'aide des API de robots Teams.

## <a name="use-the-teams-bot-apis"></a>Utiliser les API des robots Teams

> [!NOTE]
> Les API des robots de l'équipe ne fonctionnent que dans le `personal`contexte. Ils ne fonctionnent pas dans le `channel`contexte`groupchat` ou.

Grâce aux API de Teams, le robot peut envoyer et recevoir directement des fichiers avec les utilisateurs dans le contexte, également connu sous le nom de `personal` conversations personnelles . Mettre en œuvre des fonctionnalités, telles que le rapport de dépenses, la reconnaissance d'images, l'archivage de fichiers et les signatures électroniques impliquant l'édition du contenu des fichiers. Les fichiers partagés dans Teams apparaissent généralement sous forme de cartes et permettent une visualisation riche dans l'application.

Les sections suivantes décrivent comment envoyer le contenu d'un fichier en tant qu'interaction directe avec l'utilisateur, comme l'envoi d'un message. Cette API est fournie dans le cadre de la plateforme de robots Teams.

### <a name="configure-the-bot-to-support-files"></a>Configurer le robot pour qu'il prenne en charge les fichiers

Pour envoyer et recevoir des fichiers dans le robot, définissez la `supportsFiles`propriété dans le manifeste à`true`. Cette propriété est décrite dans la section des [robots](~/resources/schema/manifest-schema.md#bots) de la référence du manifeste.

La définition ressemble à ceci, `"supportsFiles": true`. Si le robot n'est pas activé, `supportsFiles`les fonctions énumérées dans cette section ne fonctionnent pas.

### <a name="receive-files-in-personal-chat"></a>Recevoir des fichiers en conversation personnelle

Lorsqu'un utilisateur envoie un fichier au robot, celui-ci est d'abord téléchargé vers le stockage OneDrive for business de l'utilisateur. Le robot reçoit alors un message d'activité notifiant l'utilisateur du téléchargement de l'utilisateur. L'activité contient les métadonnées du fichier, telles que son nom et l'URL du contenu. L'utilisateur peut lire directement cette URL pour récupérer son contenu binaire.

#### <a name="message-activity-with-file-attachment-example"></a>Exemple d'activité de message avec pièce jointe

Le code suivant montre un exemple d'activité de message avec pièce jointe :

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.file.download.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "downloadUrl" : "https://download.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C9D",
      "fileType": "txt",
      "etag": "123"
    }
  }]
}
```

Le tableau suivant décrit les propriétés du contenu de la pièce jointe :

| Propriété | Objectif |
| --- | --- |
| `downloadUrl` | URL OneDrive pour récupérer le contenu du fichier. L'utilisateur peut émettre une demande `HTTP GET`directement à partir de cette URL. |
| `uniqueId` | Identifiant unique du fichier. Il s'agit de la pièce d'identité du lecteur OneDrive, dans le cas où l'utilisateur envoie un fichier au robot. |
| `fileType` | Type de fichier, tel que .pdf ou .docx. |

En guise de meilleure pratique, accusez réception du téléchargement du fichier en envoyant un message à l'utilisateur.

### <a name="upload-files-to-personal-chat"></a>Télécharger fichiers à une conversation personnelle

Pour télécharger un fichier vers un utilisateur :

1. Envoyer un message à l'utilisateur pour lui demander la permission d'écrire dans le fichier. Ce message doit contenir une `FileConsentCard`pièce jointe avec le nom du fichier à télécharger.
2. Si l'utilisateur accepte le téléchargement du fichier, le robot reçoit une activité d'invocation avec une URL de localisation.
3. Pour transférer le fichier, le robot exécute un `HTTP POST`directement dans l'URL de l'emplacement fourni.
4. Si vous le souhaitez, vous pouvez supprimer la carte de consentement initiale si vous ne voulez pas que l'utilisateur accepte d'autres téléchargements du même fichier.

#### <a name="message-requesting-permission-to-upload"></a>Message demandant l'autorisation de télécharger

Le message de bureau suivant contient un objet de pièce jointe simple demandant à l'utilisateur l'autorisation de télécharger le fichier :

:::image type="content" source="../../assets/images/bots/bot-file-consent-card.png" alt-text="Carte de consentement demandant à l'utilisateur la permission de télécharger un fichier"lightbox="../../assets/images/bots/bot-file-consent-card.png"border="true":::

Le message mobile suivant contient un objet attaché demandant à l'utilisateur l'autorisation de télécharger le fichier :

<img src="../../assets/images/bots/mobile-bot-file-consent-card.png" alt="Consent card requesting user permission to upload file on mobile" width="350"/>

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.consent",
    "name": "file_example.txt",
    "content": {
      "description": "<Purpose of the file, such as: this is your monthly expense report>",
      "sizeInBytes": 1029393,
      "acceptContext": {
      },
      "declineContext": {
      }
    }
  }]
}
```

Le tableau suivant décrit les propriétés du contenu de la pièce jointe :

| Propriété | Objectif |
| --- | --- |
| `description` | Décrit l'objectif du fichier ou résume son contenu. |
| `sizeInBytes` | Fournit à l'utilisateur une estimation de la taille du fichier et de l'espace qu'il occupe dans OneDrive. |
| `acceptContext` | Contexte supplémentaire qui est transmis silencieusement au robot lorsque l'utilisateur accepte le fichier. |
| `declineContext` | Contexte supplémentaire qui est transmis silencieusement au robot lorsque l'utilisateur refuse le fichier. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Invoquer l'activité lorsque l'utilisateur accepte le fichier

Une activité d'invocation est envoyée au robot si et quand l'utilisateur accepte le fichier. Il contient l'URL de remplacement de OneDrive pour entreprises que le robot peut ensuite émettre pour `PUT` transférer le contenu du fichier. Pour plus d'informations sur le téléchargement vers l'URL OneDrive, voir [Télécharger des octets vers la session de téléchargement](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

Le code suivant montre un exemple d'une version concise de l'activité invoquer que le robot reçoit :

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "accept",
    "context": {
    },
    "uploadInfo": {
      "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
      "name": "file_example.txt",
      "uploadUrl": "https://upload.link",
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
      "etag": "123"
    }
  }
}
```

De même, si l'utilisateur refuse le fichier, le robot reçoit l'événement suivant avec le même nom d'activité globale :

```json
{
  "name": "fileConsent/invoke",
  "value": {
    "type": "fileUpload",
    "action": "decline",
    "context": {
    }
  }
}
```

### <a name="notifying-the-user-about-an-uploaded-file"></a>Notifier l'utilisateur d'un fichier téléchargé

Après avoir téléchargé un fichier sur le OneDrive de l'utilisateur, envoyez un message de confirmation à l'utilisateur. Le message doit contenir la pièce jointe suivante `FileCard`que l'utilisateur peut sélectionner, soit pour la prévisualiser ou l'ouvrir dans OneDrive, soit pour la télécharger localement :

```json
{
  "attachments": [{
    "contentType": "application/vnd.microsoft.teams.card.file.info",
    "contentUrl": "https://contoso.sharepoint.com/personal/johnadams_contoso_com/Documents/Applications/file_example.txt",
    "name": "file_example.txt",
    "content": {
      "uniqueId": "1150D938-8870-4044-9F2C-5BBDEBA70C8C",
      "fileType": "txt",
    }
  }]
}
```

Le tableau suivant décrit les propriétés du contenu de la pièce jointe :

| Propriété | Objectif |
| --- | --- |
| `uniqueId` | Identifiant de l'élément du lecteur OneDrive ou SharePoint. |
| `fileType` | Type de fichier, tel que .pdf ou .docx. |

### <a name="fetch-inline-images-from-message"></a>Récupérer les images en ligne du message

Récupérer les images en ligne qui font partie du message en utilisant le jeton d'accès du robot.

:::image type="content" source="../../assets/images/bots/inline-image.png" alt-text="Image en ligne"border="true":::

Le code suivant montre un exemple de récupération d'images en ligne à partir d'un message :

```csharp
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { 
        GetInlineAttachment() 
    };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
```

### <a name="basic-example-in-c"></a>Exemple de base en C#

Le code suivant montre un exemple de la façon de gérer les téléchargements de fichiers et d'envoyer des demandes de consentement de fichiers dans le dialogue du robot :

```csharp

protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Attachments?[0].ContentType.Contains("image/*") == true)
    {
        // Inline image.
        await ProcessInlineImage(turnContext, cancellationToken);
    }
    else
    {
        string filename = "teams-logo.png";
        string filePath = Path.Combine("Files", filename);
        long fileSize = new FileInfo(filePath).Length;
        await SendFileCardAsync(turnContext, filename, fileSize, cancellationToken);
    }
}
private async Task ProcessInlineImage(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var attachment = turnContext.Activity.Attachments[0];
    var client = _clientFactory.CreateClient();
    // Get Bot's access token to fetch inline image. 
    var token = await new MicrosoftAppCredentials(microsoftAppId, microsoftAppPassword).GetTokenAsync();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    var responseMessage = await client.GetAsync(attachment.ContentUrl);
    // Save the inline image to Files directory.
    var filePath = Path.Combine("Files", "ImageFromUser.png");
    using (var fileStream = new FileStream(filePath, FileMode.Create, FileAccess.Write, FileShare.None))
    {
        await responseMessage.Content.CopyToAsync(fileStream);
    }
    // Create reply with image.
    var reply = MessageFactory.Text($"Attachment of {attachment.ContentType} type and size of {responseMessage.Content.Headers.ContentLength} bytes received.");
    reply.Attachments = new List<Attachment>() { GetInlineAttachment() };
    await turnContext.SendActivityAsync(reply, cancellationToken);
}
private static Attachment GetInlineAttachment()
{
    var imagePath = Path.Combine("Files", "ImageFromUser.png");
    var imageData = Convert.ToBase64String(File.ReadAllBytes(imagePath));
    return new Attachment
    {
        Name = @"ImageFromUser.png",
        ContentType = "image/png",
        ContentUrl = $"data:image/png;base64,{imageData}",
    };
}
private async Task SendFileCardAsync(ITurnContext turnContext, string filename, long filesize, CancellationToken cancellationToken)
{
    var consentContext = new Dictionary<string, string>
    {
        { 
            "filename", filename 
        },
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
```

## <a name="code-sample"></a>Exemple de code

L'exemple de code suivant montre comment obtenir le consentement de fichiers et télécharger des fichiers vers Teams à partir d'un robot :

|**Exemple de nom** | **Description** | **.NET** | **Javascript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| File upload | Démontre comment obtenir le consentement de fichiers et télécharger des fichiers vers Teams à partir d'un robot. Et aussi, comment recevoir un fichier envoyé à un robot. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/csharp_dotnetcore/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/56.teams-file-upload) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/python/56.teams-file-upload) |

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide étape par étape](../../sbs-file-handling-in-bot.yml) pour télécharger un fichier dans Teams à l'aide d'un robot.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Optimisez votre robot grâce à la limitation du débit dans Teams](~/bots/how-to/rate-limit.md)
