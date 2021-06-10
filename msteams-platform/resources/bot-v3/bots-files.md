---
title: Envoi et réception de fichiers à partir d’un bot
description: Décrit comment envoyer et recevoir des fichiers à partir d’un bot
keywords: les fichiers de bots teams envoient la réception
ms.topic: how-to
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: f69a6ca9cfcdf3b1e559fbe8cf569accf3166f69
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566480"
---
# <a name="send-and-receive-files-through-your-bot"></a><span data-ttu-id="d3841-104">Envoyer et recevoir des fichiers via votre bot</span><span class="sxs-lookup"><span data-stu-id="d3841-104">Send and receive files through your bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="d3841-105">Il existe deux façons d’envoyer des fichiers vers et à partir d’un bot :</span><span class="sxs-lookup"><span data-stu-id="d3841-105">There are two ways to send files to and from a bot:</span></span>

* <span data-ttu-id="d3841-106">Utilisation des API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="d3841-106">Using the Microsoft Graph APIs.</span></span> <span data-ttu-id="d3841-107">Cette méthode fonctionne pour les bots dans toutes les étendues Teams :</span><span class="sxs-lookup"><span data-stu-id="d3841-107">This method works for bots in all scopes in Teams:</span></span>
  * `personal`
  * `channel`
  * `groupchat`
* <span data-ttu-id="d3841-108">Utilisation des API Teams de données.</span><span class="sxs-lookup"><span data-stu-id="d3841-108">Using the Teams APIs.</span></span> <span data-ttu-id="d3841-109">Ces fichiers ne sont en charge que dans un contexte :</span><span class="sxs-lookup"><span data-stu-id="d3841-109">These only support files in one context:</span></span>
  * `personal`

## <a name="using-the-microsoft-graph-apis"></a><span data-ttu-id="d3841-110">Utilisation des API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="d3841-110">Using the Microsoft Graph APIs</span></span>

<span data-ttu-id="d3841-111">Vous pouvez publier des messages avec des pièces jointes de carte faisant référence à des fichiers SharePoint existants à l’aide des API Microsoft Graph pour OneDrive [et SharePoint](/onedrive/developer/rest-api/).</span><span class="sxs-lookup"><span data-stu-id="d3841-111">You can post messages with card attachments referencing existing SharePoint files using the Microsoft Graph APIs for [OneDrive and SharePoint](/onedrive/developer/rest-api/).</span></span> <span data-ttu-id="d3841-112">L’utilisation des API Graph nécessite l’accès au dossier OneDrive d’un utilisateur (pour et fichiers) ou aux fichiers des canaux d’une équipe (pour les fichiers) via le flux d’autorisation `personal` `groupchat` `channel` OAuth 2.0 standard.</span><span class="sxs-lookup"><span data-stu-id="d3841-112">Using the Graph APIs requires obtaining access to a user's OneDrive folder (for `personal` and `groupchat` files) or the files in a team's channels (for `channel` files) through the standard OAuth 2.0 authorization flow.</span></span> <span data-ttu-id="d3841-113">Cette méthode fonctionne dans toutes les Teams étendues.</span><span class="sxs-lookup"><span data-stu-id="d3841-113">This method works in all Teams scopes.</span></span>

## <a name="using-the-teams-bot-apis"></a><span data-ttu-id="d3841-114">Utilisation des API Teams Bot</span><span class="sxs-lookup"><span data-stu-id="d3841-114">Using the Teams Bot APIs</span></span>

> [!NOTE]
> <span data-ttu-id="d3841-115">Cette méthode fonctionne uniquement dans le `personal` contexte.</span><span class="sxs-lookup"><span data-stu-id="d3841-115">This method works only in the `personal` context.</span></span> <span data-ttu-id="d3841-116">Elle ne fonctionne pas dans le `channel` contexte ou dans le `groupchat` contexte.</span><span class="sxs-lookup"><span data-stu-id="d3841-116">It does not work in the `channel` or `groupchat` context.</span></span>

<span data-ttu-id="d3841-117">Votre bot peut directement envoyer et recevoir des fichiers avec des utilisateurs dans le contexte, également appelé conversations personnelles, à l’aide `personal` Teams API.</span><span class="sxs-lookup"><span data-stu-id="d3841-117">Your bot can directly send and receive files with users in the `personal` context, also known as personal chats, using Teams APIs.</span></span> <span data-ttu-id="d3841-118">Cela vous permet d’implémenter des notes de frais, la reconnaissance d’image, l’archivage de fichiers, des signatures e et d’autres scénarios impliquant une manipulation directe du contenu de fichier.</span><span class="sxs-lookup"><span data-stu-id="d3841-118">This lets you implement expense reporting, image recognition, file archival, e-signatures, and other scenarios involving direct manipulation of file content.</span></span> <span data-ttu-id="d3841-119">Les fichiers partagés dans Teams apparaissent généralement sous la main de cartes et permettent un affichage enrichi dans l’application.</span><span class="sxs-lookup"><span data-stu-id="d3841-119">Files shared in Teams typically appear as cards, and allow rich in-app viewing.</span></span>

<span data-ttu-id="d3841-120">Les sections suivantes décrivent comment faire pour envoyer du contenu de fichier suite à une interaction directe de l’utilisateur, comme l’envoi d’un message.</span><span class="sxs-lookup"><span data-stu-id="d3841-120">The following sections describe how to do this to send file content as a result of direct user interaction, like sending a message.</span></span> <span data-ttu-id="d3841-121">Cette API est fournie dans le cadre de la plateforme Microsoft Teams Bot.</span><span class="sxs-lookup"><span data-stu-id="d3841-121">This API is provided as part of the Microsoft Teams Bot Platform.</span></span>

### <a name="configure-your-bot-to-support-files"></a><span data-ttu-id="d3841-122">Configurer votre bot pour prendre en charge les fichiers</span><span class="sxs-lookup"><span data-stu-id="d3841-122">Configure your bot to support files</span></span>

<span data-ttu-id="d3841-123">Pour envoyer et recevoir des fichiers dans votre bot, vous devez définir la propriété `supportsFiles` dans le manifeste sur `true` .</span><span class="sxs-lookup"><span data-stu-id="d3841-123">In order to send and receive files in your bot, you have to set the `supportsFiles` property in the manifest to `true`.</span></span> <span data-ttu-id="d3841-124">Cette propriété est décrite dans la section [bots](~/resources/schema/manifest-schema.md#bots) de la référence du manifeste.</span><span class="sxs-lookup"><span data-stu-id="d3841-124">This property is described in the [bots](~/resources/schema/manifest-schema.md#bots) section of the Manifest reference.</span></span>

<span data-ttu-id="d3841-125">La définition ressemblera à ceci `"supportsFiles": true` :</span><span class="sxs-lookup"><span data-stu-id="d3841-125">The definition will look like this: `"supportsFiles": true`.</span></span> <span data-ttu-id="d3841-126">Si votre bot n’est pas `supportsFiles` activé, les fonctionnalités suivantes ne fonctionneront pas.</span><span class="sxs-lookup"><span data-stu-id="d3841-126">If your bot does not enable `supportsFiles`, the following features will not work.</span></span>

### <a name="receiving-files-in-personal-chat"></a><span data-ttu-id="d3841-127">Réception de fichiers dans une conversation personnelle</span><span class="sxs-lookup"><span data-stu-id="d3841-127">Receiving files in personal chat</span></span>

<span data-ttu-id="d3841-128">Lorsqu’un utilisateur envoie un fichier à votre bot, le fichier est d’abord téléchargé vers le stockage OneDrive Entreprise’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3841-128">When a user sends a file to your bot, the file is first uploaded to the user's OneDrive for Business storage.</span></span> <span data-ttu-id="d3841-129">Votre bot reçoit ensuite une activité de message vous notifiant du chargement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3841-129">Your bot will then receive a message activity notifying you of the user upload.</span></span> <span data-ttu-id="d3841-130">L’activité contiendra des métadonnées de fichier, telles que son nom et l’URL de contenu.</span><span class="sxs-lookup"><span data-stu-id="d3841-130">The activity will contain file metadata, such as its name and the content URL.</span></span> <span data-ttu-id="d3841-131">Vous pouvez lire directement à partir de cette URL pour récupérer son contenu binaire.</span><span class="sxs-lookup"><span data-stu-id="d3841-131">You can directly read from this URL to fetch its binary content.</span></span>

#### <a name="message-activity-with-file-attachment-example"></a><span data-ttu-id="d3841-132">Exemple d’activité de message avec pièce jointe</span><span class="sxs-lookup"><span data-stu-id="d3841-132">Message activity with file attachment example</span></span>

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

<span data-ttu-id="d3841-133">Le tableau suivant décrit les propriétés de contenu de la pièce jointe :</span><span class="sxs-lookup"><span data-stu-id="d3841-133">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="d3841-134">Propriété</span><span class="sxs-lookup"><span data-stu-id="d3841-134">Property</span></span> | <span data-ttu-id="d3841-135">Objectif</span><span class="sxs-lookup"><span data-stu-id="d3841-135">Purpose</span></span> |
| --- | --- |
| `downloadUrl` | <span data-ttu-id="d3841-136">OneDrive URL de récupération du contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="d3841-136">OneDrive URL for fetching the content of the file.</span></span> <span data-ttu-id="d3841-137">Vous pouvez émettre `HTTP GET` une adresse directement à partir de cette URL.</span><span class="sxs-lookup"><span data-stu-id="d3841-137">You can issue an `HTTP GET` directly from this URL.</span></span> |
| `uniqueId` | <span data-ttu-id="d3841-138">ID de fichier unique.</span><span class="sxs-lookup"><span data-stu-id="d3841-138">Unique file ID.</span></span> <span data-ttu-id="d3841-139">Il s’agit de OneDrive’élément de lecteur, dans le cas où l’utilisateur envoie un fichier à votre bot.</span><span class="sxs-lookup"><span data-stu-id="d3841-139">This will be the OneDrive drive item ID, in the case of the user sending a file to your bot.</span></span> |
| `fileType` | <span data-ttu-id="d3841-140">Type d’extension de fichier, tel que pdf ou docx.</span><span class="sxs-lookup"><span data-stu-id="d3841-140">File extension type, such as pdf or docx.</span></span> |

<span data-ttu-id="d3841-141">En tant que meilleure pratique, vous devez reconnaître le chargement du fichier en renvoyant un message à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3841-141">As a best practice, you should acknowledge the file upload by sending back a message to the user.</span></span>

### <a name="uploading-files-to-personal-chat"></a><span data-ttu-id="d3841-142">Téléchargement de fichiers dans une conversation personnelle</span><span class="sxs-lookup"><span data-stu-id="d3841-142">Uploading files to personal chat</span></span>

<span data-ttu-id="d3841-143">Le téléchargement d’un fichier vers un utilisateur implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="d3841-143">Uploading a file to a user involves the following steps:</span></span>

1. <span data-ttu-id="d3841-144">Envoyez un message à l’utilisateur demandant l’autorisation d’écrire le fichier.</span><span class="sxs-lookup"><span data-stu-id="d3841-144">Send a message to the user requesting permission to write the file.</span></span> <span data-ttu-id="d3841-145">Ce message doit contenir `FileConsentCard` une pièce jointe avec le nom du fichier à télécharger.</span><span class="sxs-lookup"><span data-stu-id="d3841-145">This message must contain a `FileConsentCard` attachment with the name of the file to be uploaded.</span></span>
2. <span data-ttu-id="d3841-146">Si l’utilisateur accepte le téléchargement du fichier, votre bot reçoit une activité *Invoke* avec une URL d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="d3841-146">If the user accepts the file download, your bot will receive an *Invoke* activity with a location URL.</span></span>
3. <span data-ttu-id="d3841-147">Pour transférer le fichier, votre bot effectue une entrée directement dans `HTTP POST` l’URL d’emplacement fournie.</span><span class="sxs-lookup"><span data-stu-id="d3841-147">To transfer the file, your bot performs an `HTTP POST` directly into the provided location URL.</span></span>
4. <span data-ttu-id="d3841-148">Si vous le souhaitez, vous pouvez supprimer la carte de consentement d’origine si vous ne souhaitez pas autoriser l’utilisateur à accepter d’autres téléchargements du même fichier.</span><span class="sxs-lookup"><span data-stu-id="d3841-148">Optionally, you can remove the original consent card if you do not want to allow the user to accept further uploads of the same file.</span></span>

#### <a name="message-requesting-permission-to-upload"></a><span data-ttu-id="d3841-149">Message demandant l’autorisation de téléchargement</span><span class="sxs-lookup"><span data-stu-id="d3841-149">Message requesting permission to upload</span></span>

<span data-ttu-id="d3841-150">Ce message de bureau contient un objet pièce jointe simple demandant l’autorisation de l’utilisateur pour télécharger le fichier :</span><span class="sxs-lookup"><span data-stu-id="d3841-150">This desktop message contains a simple attachment object requesting user permission to upload the file:</span></span>

![Capture d’écran de la carte de consentement demandant à l’utilisateur l’autorisation de télécharger un fichier](../../assets/images/bots/bot-file-consent-card.png)

<span data-ttu-id="d3841-152">Ce message mobile contient un objet de pièce jointe demandant l’autorisation de l’utilisateur pour télécharger le fichier :</span><span class="sxs-lookup"><span data-stu-id="d3841-152">This mobile message contains an attachment object requesting user permission to upload the file:</span></span>

![Capture d’écran de la carte de consentement demandant à l’utilisateur l’autorisation de télécharger un fichier sur un appareil mobile](../../assets/images/bots/mobile-bot-file-consent-card.png)

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

<span data-ttu-id="d3841-154">Le tableau suivant décrit les propriétés de contenu de la pièce jointe :</span><span class="sxs-lookup"><span data-stu-id="d3841-154">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="d3841-155">Propriété</span><span class="sxs-lookup"><span data-stu-id="d3841-155">Property</span></span> | <span data-ttu-id="d3841-156">Objectif</span><span class="sxs-lookup"><span data-stu-id="d3841-156">Purpose</span></span> |
| --- | --- |
| `description` | <span data-ttu-id="d3841-157">Description du fichier.</span><span class="sxs-lookup"><span data-stu-id="d3841-157">Description of the file.</span></span> <span data-ttu-id="d3841-158">Peut être présenté à l’utilisateur pour décrire son objectif ou pour résumer son contenu.</span><span class="sxs-lookup"><span data-stu-id="d3841-158">May be shown to the user to describe its purpose or to summarize its content.</span></span> |
| `sizeInBytes` | <span data-ttu-id="d3841-159">Fournit à l’utilisateur une estimation de la taille du fichier et de la quantité d’espace qu’il prendra dans OneDrive.</span><span class="sxs-lookup"><span data-stu-id="d3841-159">Provides the user an estimate of the file size and the amount of space it will take in OneDrive.</span></span> |
| `acceptContext` | <span data-ttu-id="d3841-160">Contexte supplémentaire qui sera transmis silencieusement à votre bot lorsque l’utilisateur acceptera le fichier.</span><span class="sxs-lookup"><span data-stu-id="d3841-160">Additional context that will be silently transmitted to your bot when the user accepts the file.</span></span> |
| `declineContext` | <span data-ttu-id="d3841-161">Contexte supplémentaire qui sera transmis silencieusement à votre bot lorsque l’utilisateur refusera le fichier.</span><span class="sxs-lookup"><span data-stu-id="d3841-161">Additional context that will be silently transmitted to your bot when the user declines the file.</span></span> |

#### <a name="invoke-activity-when-the-user-accepts-the-file"></a><span data-ttu-id="d3841-162">Appeler l’activité lorsque l’utilisateur accepte le fichier</span><span class="sxs-lookup"><span data-stu-id="d3841-162">Invoke activity when the user accepts the file</span></span>

<span data-ttu-id="d3841-163">Une activité d’appel est envoyée à votre bot si et quand l’utilisateur accepte le fichier.</span><span class="sxs-lookup"><span data-stu-id="d3841-163">An invoke activity is sent to your bot if and when the user accepts the file.</span></span> <span data-ttu-id="d3841-164">Il contient l’URL OneDrive Entreprise’espace réservé que votre bot peut ensuite émettre pour `PUT` transférer le contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="d3841-164">It contains the OneDrive for Business placeholder URL that your bot can then issue a `PUT` into to transfer the file contents.</span></span> <span data-ttu-id="d3841-165">Pour plus d’informations sur le chargement vers l’URL OneDrive, lisez cet article : [Télécharger octets vers la session de chargement.](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session)</span><span class="sxs-lookup"><span data-stu-id="d3841-165">for information on uploading to the OneDrive URL read this article: [Upload bytes to the upload session](/onedrive/developer/rest-api/api/driveitem_createuploadsession#upload-bytes-to-the-upload-session).</span></span>

<span data-ttu-id="d3841-166">L’exemple suivant montre une version abrégée de l’activité d’appel que votre bot recevra :</span><span class="sxs-lookup"><span data-stu-id="d3841-166">The following example shows an abridged version of the invoke activity that your bot will receive:</span></span>

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

<span data-ttu-id="d3841-167">De même, si l’utilisateur refuse le fichier, votre bot recevra l’événement suivant, avec le même nom d’activité globale :</span><span class="sxs-lookup"><span data-stu-id="d3841-167">Similarly, if the user declines the file, your bot will receive the following event, with the same overall activity name:</span></span>

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

### <a name="notifying-the-user-about-an-uploaded-file"></a><span data-ttu-id="d3841-168">Informer l’utilisateur d’un fichier téléchargé</span><span class="sxs-lookup"><span data-stu-id="d3841-168">Notifying the user about an uploaded file</span></span>

<span data-ttu-id="d3841-169">Après avoir téléchargé un fichier sur le OneDrive de l’utilisateur, que vous utilisiez le mécanisme décrit ci-dessus ou des API déléguées par l’utilisateur OneDrive, vous devez envoyer un message de confirmation à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d3841-169">After uploading a file to the user's OneDrive, whether you use the mechanism described above or OneDrive user delegated APIs, you should send a confirmation message to the user.</span></span> <span data-ttu-id="d3841-170">Ce message doit contenir une pièce jointe sur qui l’utilisateur peut cliquer, soit pour l’afficher un aperçu, l’ouvrir dans OneDrive, soit la `FileCard` télécharger localement.</span><span class="sxs-lookup"><span data-stu-id="d3841-170">This message should contain  a `FileCard` attachment that the user can click on, either to preview it, open it in OneDrive, or download locally.</span></span>

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

<span data-ttu-id="d3841-171">Le tableau suivant décrit les propriétés de contenu de la pièce jointe :</span><span class="sxs-lookup"><span data-stu-id="d3841-171">The following table describes the content properties of the attachment:</span></span>

| <span data-ttu-id="d3841-172">Propriété</span><span class="sxs-lookup"><span data-stu-id="d3841-172">Property</span></span> | <span data-ttu-id="d3841-173">Objectif</span><span class="sxs-lookup"><span data-stu-id="d3841-173">Purpose</span></span> |
| --- | --- |
| `uniqueId` | <span data-ttu-id="d3841-174">OneDrive/SharePoint’élément de lecteur.</span><span class="sxs-lookup"><span data-stu-id="d3841-174">OneDrive/SharePoint drive item ID.</span></span> |
| `fileType` | <span data-ttu-id="d3841-175">Type de fichier, tel que pdf ou docx.</span><span class="sxs-lookup"><span data-stu-id="d3841-175">File type, such as pdf or docx.</span></span> |

### <a name="basic-example-in-c"></a><span data-ttu-id="d3841-176">Exemple de base en C #</span><span class="sxs-lookup"><span data-stu-id="d3841-176">Basic example in C#</span></span>

<span data-ttu-id="d3841-177">L’exemple suivant montre comment gérer les téléchargements de fichiers et envoyer des demandes de consentement de fichier dans la boîte de dialogue de votre bot :</span><span class="sxs-lookup"><span data-stu-id="d3841-177">The following sample shows how you can handle file uploads and send file consent requests in your bot's dialog:</span></span>

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
