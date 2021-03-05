---
title: Intégrer les fonctionnalités médias
description: Comment utiliser le SDK client JavaScript teams pour activer les fonctionnalités multimédias
keywords: Média d’autorisations d’appareil natif des fonctionnalités du microphone d’image de l’appareil photo
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 375d68c7c712b7a8d2f7114b47aae61c889b4197
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449578"
---
# <a name="integrate-media-capabilities"></a>Intégrer les fonctionnalités médias 

Ce document vous guide sur l’intégration des fonctionnalités multimédias. Cette intégration combine les fonctionnalités natives de l’appareil, telles que la **caméra** et **le microphone,** avec la plateforme Teams.  

Vous pouvez utiliser le [SDK client JavaScript Microsoft Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)qui fournit les outils nécessaires pour que votre application accède aux autorisations d’appareil d’un [utilisateur.](native-device-permissions.md) Utilisez les API de fonctionnalité multimédia appropriées pour intégrer  les fonctionnalités natives de l’appareil, telles que la caméra et le **microphone,** à la plateforme Teams dans votre application mobile Microsoft Teams, et créez une expérience plus riche. 

## <a name="advantage-of-integrating-media-capabilities"></a>Avantage de l’intégration des fonctionnalités multimédias

Le principal avantage de l’intégration des fonctionnalités des appareils dans vos applications Teams est qu’il tire parti des contrôles Teams natifs pour offrir une expérience riche et immersive à vos utilisateurs.
Pour intégrer des fonctionnalités multimédias, vous devez mettre à jour le fichier manifeste de l’application et appeler les API de fonctionnalité multimédia. 

Pour une intégration efficace, vous devez bien comprendre les extraits de [code](#code-snippets) pour appeler les API respectives, ce qui vous permet d’utiliser les fonctionnalités multimédias natives.

Il est important de vous familiariser avec les erreurs de [réponse d’API](#error-handling) pour gérer les erreurs dans votre application Teams.

> [!NOTE] 
> Actuellement, la prise en charge des fonctionnalités multimédias par Microsoft Teams est disponible uniquement pour les clients mobiles.

## <a name="update-manifest"></a>Mettre à jour le manifeste

Mettez à jour votre application Teams [manifest.jsfichier en](../../resources/schema/manifest-schema.md#devicepermissions) ajoutant la propriété et en `devicePermissions` spécifiant `media` . Il permet à votre application de demander les autorisations  requises aux utilisateurs avant de commencer à utiliser l’appareil photo pour capturer l’image, d’ouvrir la galerie pour sélectionner une image à soumettre en pièce jointe ou d’utiliser le **microphone** pour enregistrer la conversation.

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> **L’invite Demander des autorisations** s’affiche automatiquement lorsqu’une API Teams pertinente est lancée. Pour plus d’informations, voir [Demander des autorisations d’appareil.](native-device-permissions.md)

## <a name="media-capability-apis"></a>API de fonctionnalité multimédia

Les [API selectMedia,](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)et [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) vous permettent d’utiliser les fonctionnalités multimédias natives comme suit :

* Utilisez le **microphone natif pour** permettre aux utilisateurs d’enregistrer du contenu **audio** (enregistrer 10 minutes de conversation) à partir de l’appareil.
* Utilisez le contrôle **d’appareil photo natif** pour permettre aux utilisateurs de **capturer et d’attacher des images** en mouvement.
* Utilisez la prise **en charge de la galerie native** pour permettre aux utilisateurs de sélectionner des images **d’appareil** en tant que pièces jointes.
* Utilisez le contrôle **visionneuse d’images natives** **pour afficher un aperçu de plusieurs images** à la fois.
* Prise **en charge du transfert d’images** de grande taille (de 1 Mo à 50 Mo) via le pont du SDK.
* Prise en **charge des fonctionnalités d’image avancées** permettant aux utilisateurs d’afficher un aperçu et de modifier des images :
  * Analysez le document, le tableau blanc et les cartes de visite par le biais de l’appareil photo.
  
> [!IMPORTANT]
> * Les API , et les API peuvent être appelés à partir de plusieurs surfaces Teams, telles que les modules de tâche, les `selectMedia` `getMedia` `viewImages` onglets et les applications personnelles. Pour plus d’informations, voir [Points d’entrée pour les applications Teams.](../extensibility-points.md)
> * `selectMedia` L’API a été étendue pour prendre en charge les propriétés de microphone et audio.

Vous devez utiliser l’ensemble d’API suivant pour activer les fonctionnalités multimédias de votre appareil :

| API      | Description   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) **(Appareil photo)**| Cette API permet aux utilisateurs de capturer ou de sélectionner **du contenu multimédia** à partir de l’appareil photo de l’appareil et de le renvoyer à l’application web. Les utilisateurs peuvent modifier, rogner, faire pivoter, annoter ou dessiner sur des images avant l’envoi. En réponse à , l’application web reçoit les ID multimédias des images sélectionnées et une miniature du `selectMedia` média sélectionné. Cette API peut être configurée davantage via la configuration [ImageProps.](/javascript/api/@microsoft/teams-js/imageprops?view=msteams-client-js-latest&preserve-view=true) |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true) (**Microphone**)| Définissez [mediaType sur](/javascript/api/@microsoft/teams-js/mediatype?view=msteams-client-js-latest&preserve-view=true) `4` dans `selectMedia` l’API pour accéder à la fonctionnalité microphone. Cette API permet également aux utilisateurs d’enregistrer du contenu audio à partir du microphone de l’appareil et de renvoyer des clips enregistrés à l’application web. Les utilisateurs peuvent suspendre, ré-enregistrer et lire l’aperçu de l’enregistrement avant la soumission. En réponse à **selectMedia,** l’application web reçoit les ID multimédias de l’enregistrement audio sélectionné. <br/> Utilisez `maxDuration` , si vous avez besoin de configurer une durée en minutes pour l’enregistrement de la conversation. La durée actuelle de l’enregistrement est de 10 minutes, après quoi l’enregistrement se termine.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| Cette API récupère le média capturé par l’API en blocs, quelle que `selectMedia` soit la taille du média. Ces blocs sont assemblés et renvoyés à l’application web en tant que fichier ou blob. La rupture du média en blocs plus petits facilite le transfert de fichiers de grande taille. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| Cette API permet à l’utilisateur d’afficher des images en mode plein écran en tant que liste de défilement.|


**Expérience d’application web pour l’API selectMedia pour la fonctionnalité d’image** 
 ![ Expérience d’appareil photo et d’image dans Teams](../../assets/images/tabs/image-capability.png)

**Expérience d’application web pour l’API selectMedia pour la fonctionnalité de microphone** 
 ![ expérience d’application web pour la fonctionnalité de microphone](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Gestion des erreurs

Vous devez veiller à gérer ces erreurs de manière appropriée dans votre application Teams. Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées : 


|Code d’erreur |  Nom de l’erreur     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge sur la plateforme actuelle.|
| **404** | FILE_NOT_FOUND | Le fichier spécifié n’est pas trouvé à l’emplacement donné.|
| **500** | INTERNAL_ERROR | Une erreur interne est rencontrée lors de l’opération requise.|
| **1000** | PERMISSION_DENIED |L’autorisation est refusée par l’utilisateur.|
| **2000** |NETWORK_ERROR | Problème réseau.|
| **3000** | NO_HW_SUPPORT | Le matériel sous-jacent ne prend pas en charge la fonctionnalité.|
| **4000**| INVALID_ARGUMENTS | Un ou plusieurs arguments ne sont pas valides.|
| **5000** | UNAUTHORIZED_USER_OPERATION | L’utilisateur n’est pas autorisé à effectuer cette opération.|
| **6000** |INSUFFICIENT_RESOURCES | L’opération n’a pas pu être achevée en raison de ressources insuffisantes.|
|**7000** | THROTTLE | La plateforme a limitée la demande car l’API a été fréquemment invoquée.|
|  **8000** | USER_ABORT |L’utilisateur abandonne l’opération.|
| **9000**| OLD_PLATFORM | Le code de plateforme est obsolète et n’implémente pas cette API.|
| **10000**| SIZE_EXCEEDED |  La valeur de retour est trop grande et a dépassé les limites de taille de la plateforme.|

## <a name="code-snippets"></a>Extraits de code

**Appel `selectMedia` API de** capture d’images à l’aide de l’appareil photo :

```javascript
let imageProp: microsoftTeams.media.ImageProps = {
    sources: [microsoftTeams.media.Source.Camera, microsoftTeams.media.Source.Gallery],
    startMode: microsoftTeams.media.CameraStartMode.Photo,
    ink: false,
    cameraSwitcher: false,
    textSticker: false,
    enableFilter: true,
};
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Image,
    maxMediaCount: 10,
    imageProps: imageProp
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    if (attachments) {
        let y = attachments[0];
        img.src = ("data:" + y.mimeType + ";base64," + y.preview);
    }
});
```

**Appel `getMedia` API permettant** de récupérer des médias de grande taille en blocs :

```javascript
let media: microsoftTeams.media.Media = attachments[0]
media.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("image")) {
            img.src = (URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

**Appel `viewImages` API par ID renvoyé par `selectMedia` l’API**:

```javascript
// View images by id:
// Assumption: attachmentArray = select Media API Output
let uriList = [];
if (attachmentArray && attachmentArray.length > 0) {
    for (let i = 0; i < attachmentArray.length; i++) {
        let file = attachmentArray[i];
        if (file.mimeType.includes("image")) {
            let imageUri = {
                value: file.content,
                type: 1,
            }
            uriList.push(imageUri);
        } else {
            alert("File type is not image");
        }
    }
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

**Appel `viewImages` API par URL**:

```javascript
// View Images by URL:
// Assumption 2 urls, url1 and url2
let uriList = [];
if (URL1 != null && URL1.length > 0) {
    let imageUri = {
        value: URL1,
        type: 2,
    }
    uriList.push(imageUri);
}
if (URL2 != null && URL2.length > 0) {
    let imageUri = {
        value: URL2,
        type: 2,
    }
    uriList.push(imageUri);
}
if (uriList.length > 0) {
    microsoftTeams.media.viewImages(uriList, (error: microsoftTeams.SdkError) => {
        if (error) {
            if (error.message) {
                output(" ErrorCode: " + error.errorCode + error.message);
            } else {
                output(" ErrorCode: " + error.errorCode);
            }
        }
    });
} else {
    output("Url list is empty");
}
```

**Appel `selectMedia` et API pour `getMedia` l’enregistrement audio via le microphone**:

```javascript
let mediaInput: microsoftTeams.media.MediaInputs = {
    mediaType: microsoftTeams.media.MediaType.Audio,
    maxMediaCount: 1,
};
microsoftTeams.media.selectMedia(mediaInput, (error: microsoftTeams.SdkError, attachments: microsoftTeams.media.Media[]) => {
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
    // If you want to directly use the audio file (for smaller file sizes (~4MB))    if (attachments) {
    let audioResult = attachments[0];
    var videoElement = document.createElement("video");
    videoElement.setAttribute("src", ("data:" + y.mimeType + ";base64," + y.preview));
    //To use the audio file via get Media API for bigger audio file sizes greater than 4MB        audioResult.getMedia((error: microsoftTeams.SdkError, blob: Blob) => {
    if (blob) {
        if (blob.type.includes("video")) {
            videoElement.setAttribute("src", URL.createObjectURL(blob));
        }
    }
    if (error) {
        if (error.message) {
            alert(" ErrorCode: " + error.errorCode + error.message);
        } else {
            alert(" ErrorCode: " + error.errorCode);
        }
    }
});
```

## <a name="see-also"></a>Voir aussi

> [!div class="nextstepaction"]
> [Intégrer la fonctionnalité de QR ou de scanneur de code-barres dans Teams](qr-barcode-scanner-capability.md)

> [!div class="nextstepaction"]
> [Intégrer des fonctionnalités d’emplacement dans Teams](location-capability.md)