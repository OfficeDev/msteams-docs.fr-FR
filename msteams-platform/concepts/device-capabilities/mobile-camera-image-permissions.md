---
title: Intégrer les fonctionnalités médias
author: Rajeshwari-v
description: Découvrez comment utiliser Teams SDK client JavaScript pour activer les fonctionnalités multimédias à l’aide d’exemples de code.
keywords: fonctionnalités du microphone d’image de caméra api multimédia d’autorisations natives d’appareil
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: c9b31bf6fe97446bfbccdd1861612ec938733f88
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111261"
---
# <a name="integrate-media-capabilities"></a>Intégrer les fonctionnalités médias

Vous pouvez intégrer à votre application Teams des fonctionnalités natives de l'appareil, **telles que l'appareil photo** et le **microphone**. Pour l’intégration, vous pouvez utiliser [Microsoft Teams kit de développement logiciel (SDK) client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), qui fournit les outils nécessaires à votre application pour accéder aux [autorisations d’appareil](native-device-permissions.md) d’un utilisateur. Utilisez les API de fonctionnalité multimédia appropriées pour intégrer les fonctionnalités de l’appareil, telles que **l’appareil photo** et le **microphone**, à la plateforme Teams dans votre application mobile Microsoft Teams, et créez une expérience plus riche.

## <a name="advantage-of-integrating-media-capabilities"></a>Avantage de l’intégration des fonctionnalités multimédias

Le principal avantage de l’intégration des fonctionnalités d’appareil dans vos applications Teams est qu’il tire parti des contrôles Teams natifs pour offrir une expérience riche et immersive à vos utilisateurs.
Pour intégrer les fonctionnalités multimédias, vous devez mettre à jour le fichier manifeste de l’application et appeler les API de fonctionnalité multimédia.

Pour une intégration efficace, vous devez avoir une bonne compréhension des [extraits de code](#code-snippets) pour appeler les API respectives, qui vous permettent d'utiliser les capacités des médias natifs.

Il est important de vous familiariser avec les [erreurs de réponse d’API](#error-handling) pour gérer les erreurs dans votre application Teams.

> [!NOTE]
>
> * Actuellement, la prise en charge par Microsoft Teams des capacités médiatiques n'est disponible que pour les clients mobiles.
> * Actuellement, Teams ne prend pas en charge les autorisations d’appareil pour les applications multi-fenêtres, les onglets et le panneau latéral de la réunion.
> * Les autorisations d’appareil sont différentes dans le navigateur. Pour plus d'informations, consultez la section [Autorisations du périphérique de navigation](browser-device-permissions.md).

## <a name="update-manifest"></a>Mise à jour du manifeste

Mettez à jour votre fichier [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) d’application Teams en ajoutant la `devicePermissions` propriété et en spécifiant `media`. Il permet à votre application de demander les autorisations requises aux utilisateurs avant de commencer à utiliser **l’appareil photo** pour capturer l’image, d’ouvrir la galerie pour sélectionner une image à envoyer en tant que pièce jointe ou d’utiliser le **microphone** pour enregistrer la conversation. La mise à jour du manifeste de l’application est la suivante :

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> L’invite **d’autorisations de demande** s’affiche automatiquement lorsqu’une API Teams pertinente est lancée. Pour plus d'informations, reportez-vous à la section [Demander les autorisations du périphérique](native-device-permissions.md).

## <a name="media-capability-apis"></a>API de capacité média

Les API [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true) et [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) vous permettent d’utiliser les fonctionnalités multimédias natives comme suit :

* Utilisez le **microphone** natif pour permettre aux utilisateurs **d’enregistrer du son** (enregistrement de 10 minutes de conversation) à partir de l’appareil.
* Utilisez le **contrôle caméra** natif pour permettre aux utilisateurs de **capturer et d’attacher des images** en déplacement.
* Utilisez la **prise en charge de la galerie** native pour permettre aux utilisateurs de **sélectionner des images d’appareil** en tant que pièces jointes.
* Utilisez le **contrôle visionneuse d’images** natives pour **afficher un aperçu simultané de plusieurs images** .
* Prendre en charge le **transfert d’images volumineuses** (de 1 Mo à 50 Mo) via le pont du SDK
* La prise **en charge des fonctionnalités d’image avancées** permet aux utilisateurs d’afficher un aperçu et de modifier des images :
  * Analysez les documents, le tableau blanc et les cartes de visite par le biais de l’appareil photo.
  
> [!IMPORTANT]
>
> * Les `selectMedia`api , `getMedia`et `viewImages` , peuvent être appelées à partir de plusieurs surfaces Teams, telles que des modules de tâches, des onglets et des applications personnelles. Pour plus d’informations, consultez [Points d’entrée pour les applications Teams](../extensibility-points.md).
> * `selectMedia` L’API a été étendue pour prendre en charge les propriétés audio et de microphone.

Vous devez utiliser l’ensemble d’API suivant pour activer les fonctionnalités multimédias de votre appareil :

| API      | Description   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Caméra)**| Cette API permet aux utilisateurs de **capturer ou de sélectionner un média à partir de la caméra de l’appareil** et de le retourner à l’application web. Les utilisateurs peuvent modifier, rogner, faire pivoter, annoter ou dessiner sur des images avant la soumission. En réponse à `selectMedia`, l’application web reçoit les ID multimédias des images sélectionnées et une miniature du média sélectionné. Cette API peut être configurée par le biais de la configuration [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) . |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)| Définissez le [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) sur `4` dans `selectMedia`l'API pour accéder à la capacité du microphone. Cette API permet également aux utilisateurs d’enregistrer du son à partir du microphone de l’appareil et de retourner des clips enregistrés à l’application web. Les utilisateurs peuvent suspendre, ré-enregistrer et lire la préversion de l’enregistrement avant la soumission. En réponse à  **toselectMedia**, l’application web reçoit les ID multimédias de l’enregistrement audio sélectionné. <br/> Utilisez `maxDuration`, si vous avez besoin de configurer une durée en minutes pour l’enregistrement de la conversation. La durée actuelle de l’enregistrement est de 10 minutes, après quoi l’enregistrement se termine.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| Cette API récupère le média capturé par `selectMedia` l’API en blocs, quelle que soit la taille du média. Ces blocs sont assemblés et renvoyés à l’application web sous la forme d’un fichier ou d’un objet blob. La segmentation du média en blocs plus petits facilite le transfert de fichiers volumineux. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| Cette API permet à l’utilisateur d’afficher des images en mode plein écran sous la forme d’une liste déroulante.|

L’image suivante illustre l’expérience d’application web de l’API `selectMedia` pour la fonctionnalité d’image :

![expérience de l’appareil photo et de l’image dans Teams](../../assets/images/tabs/image-capability.png)

L’image suivante illustre l’expérience d’application web de l’API `selectMedia` pour la fonctionnalité de microphone :

![expérience d’application web pour la fonctionnalité de microphone](../../assets/images/tabs/microphone-capability.png)

## <a name="error-handling"></a>Gestion des erreurs

Vous devez vous assurer de gérer ces erreurs de manière appropriée dans votre application Teams. Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées :

|Code d’erreur |  Nom de l’erreur     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge sur la plateforme actuelle.|
| **404** | FILE_NOT_FOUND | Le fichier spécifié est introuvable à l’emplacement donné.|
| **500** | INTERNAL_ERROR | Une erreur interne se produit lors de l’exécution de l’opération requise.|
| **1 000** | PERMISSION_DENIED |L’autorisation est refusée par l’utilisateur.|
| **3 000** | NO_HW_SUPPORT | Le matériel sous-jacent ne prend pas en charge la fonctionnalité.|
| **4000**| ARGUMENTS NON VALIDES | Un ou plusieurs arguments ne sont pas valides.|
|  **8000** | USER_ABORT |L’utilisateur abandonne l’opération.|
| **9000**| OLD_PLATFORM | Le code de plateforme est obsolète et n’implémente pas cette API.|
| **10 000**| SIZE_EXCEEDED |  La valeur de retour est trop grande et a dépassé les limites de la taille de la plateforme.|

## <a name="code-snippets"></a>Extraits de code

**Appel `selectMedia` API** pour la capture d’images à l’aide de l’appareil photo :

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

**Appel `getMedia` API** pour récupérer des supports volumineux en blocs :

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

**Appel `viewImages` API par ID retourné par `selectMedia` l’API** :

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

**Appel `viewImages` API par URL** :

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

**Appels `selectMedia` et `getMedia` API pour l’enregistrement audio via le microphone** :

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

* [Intégrer le code QR ou la fonctionnalité de scanneur de code-barres dans Teams](qr-barcode-scanner-capability.md)
* [Intégrer les fonctionnalités d’emplacement sur Teams](location-capability.md)
* [Intégrer le sélecteur de personnes dans Teams](people-picker-capability.md)
* [Exigences et considérations relatives aux bots multimédias hébergés par l’application](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
