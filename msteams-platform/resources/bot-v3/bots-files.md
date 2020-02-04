---
title: Envoi et réception de fichiers à partir d’un bot
description: Décrit comment envoyer et recevoir des fichiers à partir d’un bot
keywords: fichiers robots teams envoyer réception
ms.date: 05/20/2019
ms.openlocfilehash: ee26b4031c6022ab30ec5b2b58b42105c2dc6b0f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674021"
---
# <a name="send-and-receive-files-through-your-bot"></a>Envoyer et recevoir des fichiers via votre robot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Il existe deux façons d’envoyer des fichiers vers et à partir d’un bot :

* À l’aide des API Microsoft Graph. Cette méthode fonctionne pour les robots dans toutes les étendues de teams :
  * `personal`
  * `channel`
  * `groupchat`
* À l’aide des API Teams. Ces fichiers ne prennent en charge que dans un seul contexte :
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a>Utilisation des API Microsoft Graph

Vous pouvez publier des messages avec des pièces jointes référençant des fichiers SharePoint existants à l’aide des API Microsoft Graph pour [OneDrive et SharePoint](/onedrive/developer/rest-api/). À l’aide des API Graph, vous devez obtenir l’accès au dossier OneDrive `personal` d' `groupchat` un utilisateur (pour les fichiers et fichiers) ou aux fichiers `channel` des canaux d’une équipe (pour les fichiers) via le flux d’autorisation 2,0 OAuth standard. Cette méthode fonctionne dans toutes les étendues Teams.

## <a name="using-the-teams-bot-apis"></a>Utilisation des API du bot teams

> [!NOTE]
> Cette méthode fonctionne uniquement dans le `personal` contexte. Il ne fonctionne pas dans le `channel` contexte `groupchat` ou.

Votre robot peut directement envoyer et recevoir des fichiers avec des utilisateurs `personal` dans le contexte, également appelés conversations personnelles, à l’aide des API Teams. Cela vous permet de mettre en œuvre des notes de frais, la reconnaissance des images, l’archivage des fichiers, les signatures électroniques et d’autres scénarios impliquant une manipulation directe du contenu des fichiers. Les fichiers partagés dans teams s’affichent généralement sous forme de cartes et permettent un affichage enrichi dans les applications.

Les sections suivantes décrivent la procédure à suivre pour envoyer le contenu d’un fichier à la suite d’une interaction directe avec l’utilisateur, par exemple, l’envoi d’un message. Cette API est fournie dans le cadre de la plateforme Microsoft teams bot.

### <a name="configure-your-bot-to-support-files"></a>Configurer votre bot pour prendre en charge les fichiers

Pour envoyer et recevoir des fichiers dans votre robot, vous devez définir la `supportsFiles` propriété dans le manifeste sur. `true` Cette propriété est décrite dans la section [bots](~/resources/schema/manifest-schema.md#bots) de la référence de manifeste.

La définition se présente comme suit : `"supportsFiles": true`. Si votre bot ne s’active `supportsFiles`pas, les fonctionnalités suivantes ne fonctionneront pas.

### <a name="receiving-files-in-personal-chat"></a>Réception de fichiers dans une conversation personnelle

Lorsqu’un utilisateur envoie un fichier à votre bot, le fichier est d’abord téléchargé vers le stockage OneDrive entreprise de l’utilisateur. Votre bot recevra alors une activité de message vous avertissant du chargement de l’utilisateur. L’activité contiendra des métadonnées de fichier, telles que son nom et l’URL de contenu. Vous pouvez lire directement à partir de cette URL pour extraire son contenu binaire.

### <a name="send-and-receive-files-through-bot-on-teams-mobile-app"></a>Envoyer et recevoir des fichiers via un bot sur une application mobile teams
> [!NOTE] 
> L’envoi et la réception de fichiers sur des robots sur des appareils mobiles ne sont pas pris en charge.

#### <a name="message-activity-with-file-attachment-example"></a>Activité des messages avec un exemple de pièce jointe

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

Le tableau suivant décrit les propriétés de contenu de la pièce jointe :

| Propriété | Objectif |
| --- | --- |
| `downloadUrl` | URL OneDrive pour l’extraction du contenu du fichier. Vous pouvez émettre une `HTTP GET` erreur directement à partir de cette URL. |
| `uniqueId` | ID de fichier unique. Il s’agit de l’ID d’élément de lecteur OneDrive, si l’utilisateur envoie un fichier à votre bot. |
| `fileType` | Type d’extension de fichier, tel que PDF ou docx. |

Il est recommandé de reconnaître le téléchargement du fichier en renvoyant un message à l’utilisateur.

### <a name="uploading-files-to-personal-chat"></a>Chargement de fichiers dans la conversation personnelle

Le téléchargement d’un fichier vers un utilisateur implique les étapes suivantes :

1. Envoyer un message à l’utilisateur qui demande l’autorisation d’écriture du fichier. Ce message doit contenir une `FileConsentCard` pièce jointe avec le nom du fichier à télécharger.
2. Si l’utilisateur accepte le téléchargement de fichier, votre bot reçoit une activité d' *appel* avec une URL d’emplacement.
3. Pour transférer le fichier, votre bot effectue directement `HTTP POST` une URL d’emplacement fournie.
4. Vous pouvez également supprimer la carte de consentement d’origine si vous ne souhaitez pas autoriser l’utilisateur à accepter les téléchargements supplémentaires du même fichier.

#### <a name="message-requesting-permission-to-upload"></a>Message demandant l’autorisation de téléchargement

Ce message contient un objet Attachment simple qui demande à l’utilisateur l’autorisation de télécharger le fichier.

![Capture d’écran de la carte de consentement demandant à l’utilisateur de télécharger le fichier](~/assets/images/bots/bot-file-consent-card.png)

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

Le tableau suivant décrit les propriétés de contenu de la pièce jointe :

| Propriété | Objectif |
| --- | --- |
| `description` | Description du fichier. Peut être présenté à l’utilisateur pour décrire son objectif ou pour résumer son contenu. |
| `sizeInBytes` | Fournit à l’utilisateur une estimation de la taille du fichier et de l’espace qu’il prendra dans OneDrive. |
| `acceptContext` | Contexte supplémentaire qui sera transmis silencieusement à votre bot lorsque l’utilisateur acceptera le fichier. |
| `declineContext` | Contexte supplémentaire qui sera transmis silencieusement à votre bot lorsque l’utilisateur refusera le fichier. |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a>Appeler l’activité lorsque l’utilisateur accepte le fichier

Une activité d’appel est envoyée à votre bot si l’utilisateur accepte le fichier. Il contient l’URL de l’espace réservé OneDrive entreprise que votre robot peut ensuite `PUT` émettre dans pour transférer le contenu du fichier. Pour plus d’informations sur le téléchargement vers l’URL OneDrive, lisez cet article : [chargement des octets vers la session de chargement](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).

L’exemple suivant montre une version abrégée de l’activité d’appel que votre bot recevra :

```json
{
  ...

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

De même, si l’utilisateur refuse le fichier, votre bot reçoit l’événement suivant, avec le même nom d’activité global :

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

### <a name="notifying-the-user-about-an-uploaded-file"></a>Notification à l’utilisateur d’un fichier téléchargé

Après avoir téléchargé un fichier sur le OneDrive de l’utilisateur, que vous utilisiez le mécanisme décrit ci-dessus ou les API déléguées par l’utilisateur OneDrive, vous devez envoyer un message de confirmation à l’utilisateur. Ce message doit contenir une `FileCard` pièce jointe sur laquelle l’utilisateur peut cliquer pour en afficher un aperçu, l’ouvrir dans OneDrive ou le télécharger localement.

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

Le tableau suivant décrit les propriétés de contenu de la pièce jointe : 

| Propriété | Objectif |
| --- | --- |
| `uniqueId` | ID d’élément de lecteur OneDrive/SharePoint. |
| `fileType` | Type de fichier, tel que PDF ou docx. |

### <a name="basic-example-in-c"></a>Exemple de base dans C #

L’exemple suivant montre comment gérer les téléchargements de fichiers et envoyer des demandes de consentement de fichier dans la boîte de dialogue de votre robot.

```csharp

// This sample dialog shows two simple flows:
// 1) A silly example of receiving a file from the user, processing the key elements,
//    and then constructing the attachment and sending it back.
// 2) Creating a new file consent card requesting user permission to upload a file.
private async Task MessageReceivedAsync(IDialogContext context, IAwaitable<object> result)
{
    var replyMessage = context.MakeMessage();
    Attachment returnCard;

    var message = await result as Activity;

    // Check to see if the user is sending the bot a file.
    if (message.Attachments != null && message.Attachments.Any())
    {
        var attachment = message.Attachments.First();

        if (attachment.ContentType == FileDownloadInfo.ContentType)
        {
            FileDownloadInfo downloadInfo = (attachment.Content as JObject).ToObject<FileDownloadInfo>();
            if (downloadInfo != null)
            {
                returnCard = CreateFileInfoAttachment(downloadInfo, attachment.Name, attachment.ContentUrl);
                replyMessage.Attachments.Add(returnCard);
            }
        }
    }
    else
    {
        // Illustrates creating a file consent card.
        returnCard = CreateFileConsentAttachment();
        replyMessage.Attachments.Add(returnCard);
    }
    await context.PostAsync(replyMessage);
}


private static Attachment CreateFileInfoAttachment(FileDownloadInfo downloadInfo, string name, string contentUrl)
{
    FileInfoCard card = new FileInfoCard()
    {
        FileType = downloadInfo.FileType,
        UniqueId = downloadInfo.UniqueId
    };

    Attachment att = card.ToAttachment();
    att.ContentUrl = contentUrl;
    att.Name = name;

    return att;
}

private static Attachment CreateFileConsentAttachment()
{
    JObject acceptContext = new JObject();
    // Fill in any additional context to be sent back when the user accepts the file.

    JObject declineContext = new JObject();
    // Fill in any additional context to be sent back when the user declines the file.

    FileConsentCard card = new FileConsentCard()
    {
        AcceptContext = acceptContext,
        DeclineContext = declineContext,
        SizeInBytes = 102635,
        Description = "File description"
    };

    Attachment att = card.ToAttachment();
    att.Name = "Example file";

    return att;
}
```
