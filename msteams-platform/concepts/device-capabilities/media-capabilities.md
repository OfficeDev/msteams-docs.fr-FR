---
title: Intégrer les fonctionnalités médias
author: Rajeshwari-v
description: Découvrez comment utiliser Teams kit de développement logiciel (SDK) client JavaScript pour activer les fonctionnalités multimédias à l’aide d’exemples de code et découvrir l’avantage de l’intégration des fonctionnalités multimédias.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 366c58ac283e687f8a297b8701b932f99550574e
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190235"
---
# <a name="integrate-media-capabilities"></a>Intégrer les fonctionnalités médias

Vous pouvez intégrer des fonctionnalités d’appareil natif, telles que la caméra et le microphone, à votre application Teams. Pour l’intégration, vous pouvez utiliser [Microsoft Teams kit de développement logiciel (SDK) client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) qui fournit les outils nécessaires à votre application pour accéder aux [autorisations d’un utilisateur sur l’appareil](native-device-permissions.md). Utilisez les API de fonctionnalité multimédia appropriées pour intégrer les fonctionnalités de l’appareil, telles que l’appareil photo et le microphone, à la plateforme Teams dans votre application Microsoft Teams, et créez une expérience plus riche. La fonctionnalité multimédia est disponible pour Teams client web, de bureau et mobile. Pour intégrer les fonctionnalités multimédias, vous devez mettre à jour le fichier manifeste de l’application et appeler les API de fonctionnalité multimédia.

Pour une intégration efficace, vous devez avoir une bonne compréhension des [extraits de code](#code-snippets) pour appeler les API respectives, qui vous permettent d'utiliser les capacités des médias natifs. Il est important de vous familiariser avec les [erreurs de réponse d’API](#error-handling) pour gérer les erreurs dans votre application Teams.

## <a name="advantages"></a>Avantages

Le principal avantage de l’intégration des fonctionnalités d’appareil dans vos applications Teams est qu’il tire parti des contrôles Teams natifs pour offrir une expérience riche et immersive à vos utilisateurs. Les scénarios suivants présentent les avantages des fonctionnalités multimédias :

* Permettre à l’utilisateur de capturer les maquettes approximatives dessinées sur un tableau blanc physique via le téléphone cellulaire et d’utiliser les images capturées comme options de sondage dans Teams conversation de groupe.

* Autoriser l’utilisateur à enregistrer le message audio et à l’attacher à un ticket d’incident.

* Permettre à l’utilisateur d’analyser les documents physiques à partir du smartphone pour déposer une demande d’assurance automobile.

> [!NOTE]
>
> * Actuellement, Teams ne prend pas en charge les autorisations d’appareil dans la fenêtre de conversation contextuelle, les onglets et le panneau côté réunion.</br>
> * Les autorisations d’appareil sont différentes dans le navigateur. Pour plus d'informations, voir les [autorisations d'appareil de navigation](browser-device-permissions.md).
> * L’invite d’autorisations de demande s’affiche automatiquement sur un appareil mobile lorsqu’une API Teams pertinente est lancée. Pour plus d'informations, reportez-vous à la section [Demander les autorisations de l'appareil](native-device-permissions.md).

## <a name="update-manifest"></a>Mise à jour du manifeste

Mettez à jour le fichier [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) de votre application Teams en ajoutant la `devicePermissions`propriété et en spécifiant`media`. Il permet à votre application de demander les autorisations requises aux utilisateurs avant de commencer à utiliser l’appareil photo pour capturer l’image, d’ouvrir la galerie pour sélectionner une image à envoyer en tant que pièce jointe ou d’utiliser le microphone pour enregistrer la conversation. La mise à jour du manifeste de l’application est la suivante :

``` json
"devicePermissions": [
    "media",
],
```

## <a name="media-capability-apis"></a>API de capacité média

Les API [selectMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true) et [viewImages](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true) vous permettent d’utiliser les fonctionnalités multimédias natives comme suit :

* Utilisez le **microphone** natif pour permettre aux utilisateurs **d’enregistrer du son** (enregistrement de 10 minutes de conversation) à partir de l’appareil.
* Utilisez le **contrôle caméra** natif pour permettre aux utilisateurs de **capturer et d’attacher des images** en déplacement.
* Utilisez la **prise en charge de la galerie** native pour permettre aux utilisateurs de **sélectionner des images d’appareil** en tant que pièces jointes.
* Utilisez le **contrôle visionneuse d’images** natives pour **afficher un aperçu simultané de plusieurs images** .
* Prendre en charge le **transfert d’images volumineuses** (de 1 Mo à 50 Mo) via le pont du SDK
* Prenez en charge **les fonctionnalités d’image avancées** en permettant aux utilisateurs d’afficher un aperçu et de modifier des images.
* Analysez les documents, le tableau blanc et les cartes de visite par le biais de l’appareil photo.
  
> [!IMPORTANT]
>
> * Les `selectMedia`api , `getMedia`et `viewImages` , peuvent être appelées à partir de plusieurs surfaces Teams, telles que des modules de tâches, des onglets et des applications personnelles. Pour plus d’informations, consultez [Points d’entrée pour les applications Teams](../extensibility-points.md).</br>
> * `selectMedia` L’API prend en charge les fonctionnalités de caméra et de microphone par le biais de différentes configurations d’entrée.
> * L’API `selectMedia` permettant d’accéder à la fonctionnalité de microphone prend uniquement en charge les clients mobiles.

Le tableau suivant répertorie un ensemble d’API pour activer les fonctionnalités multimédias de votre appareil :

| API      | Description   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Caméra)**| Cette API permet aux utilisateurs de **capturer ou de sélectionner un média à partir de la caméra de l’appareil** et de le retourner à l’application web. Les utilisateurs peuvent modifier, rogner, faire pivoter, annoter ou dessiner sur des images avant la soumission. En réponse à `selectMedia`, l’application web reçoit les ID multimédias des images sélectionnées et une miniature du média sélectionné. Cette API peut être configurée par le biais de la configuration [ImageProps](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageprops?view=msteams-client-js-latest&preserve-view=true) . |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.media?view=msteams-client-js-latest&preserve-view=true) (**Microphone**)| Définissez [mediaType](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediatype?view=msteams-client-js-latest&preserve-view=true) sur l’API `selectMedia` pour accéder à `4` la fonctionnalité de microphone. Cette API permet également aux utilisateurs d’enregistrer du son à partir du microphone de l’appareil et de retourner des clips enregistrés à l’application web. Les utilisateurs peuvent suspendre, ré-enregistrer et lire la préversion de l’enregistrement avant la soumission. En réponse à  **toselectMedia**, l’application web reçoit les ID multimédias de l’enregistrement audio sélectionné. <br/> Utilisez `maxDuration`, si vous avez besoin de configurer une durée en minutes pour l’enregistrement de la conversation. La durée actuelle de l’enregistrement est de 10 minutes, après quoi l’enregistrement se termine.  |
| [**getMedia**](/javascript/api/@microsoft/teams-js/microsoftteams.media.mediachunk?view=msteams-client-js-latest&preserve-view=true)| Cette API récupère le média capturé par `selectMedia` l’API en blocs, quelle que soit la taille du média. Ces blocs sont assemblés et renvoyés à l’application web sous la forme d’un fichier ou d’un objet blob. La segmentation du média en blocs plus petits facilite le transfert de fichiers volumineux. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/microsoftteams.media.imageuri?view=msteams-client-js-latest&preserve-view=true)| Cette API permet à l’utilisateur d’afficher des images en mode plein écran sous la forme d’une liste déroulante.|

# <a name="mobile"></a>[Mobile](#tab/mobile)

L’image suivante illustre l’expérience d’application web de l’API `selectMedia` pour la fonctionnalité d’image :

:::image type="content" source="~/assets/images/tabs/media-capability-mobile2.png" alt-text="Illustration montrant la fonctionnalité d’image pour mobile." border="true":::

> [!NOTE]
>
> Sur les appareils avec Android version inférieure à 7, l’API `selectMedia` lance l’expérience de caméra native Android au lieu de l’expérience de caméra native Teams.

L’image suivante illustre l’expérience d’application web de l’API `selectMedia` pour la fonctionnalité de microphone :

:::image type="content" source="~/assets/images/tabs/microphone-capability.png" alt-text="Illustration montrant la fonctionnalité de microphone pour mobile." border="true":::

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

L’image suivante illustre l’expérience d’application web de l’API `selectMedia` pour la fonctionnalité d’image :

:::image type="content" source="~/assets/images/tabs/media-capability-desktop1.png" alt-text="Illustration montrant la fonctionnalité multimédia pour le bureau." border="true":::

---

## <a name="error-handling"></a>Gestion des erreurs

Veillez à gérer ces erreurs de manière appropriée dans votre application Teams. Le tableau suivant répertorie les codes d’erreur et les descriptions sous lesquels les erreurs sont générées :

|Code d’erreur |  Nom de l’erreur     | Description|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge sur la plateforme actuelle.|
| **404** | FILE_NOT_FOUND | Le fichier spécifié est introuvable à l’emplacement donné.|
| **500** | INTERNAL_ERROR | Une erreur interne a été rencontrée lors de l'exécution de l'opération requise.|
| **1 000** | PERMISSION_DENIED |L’autorisation est refusée par l’utilisateur.|
| **3000** | NO_HW_SUPPORT | Le matériel ne prend pas en charge la fonctionnalité.|
| **4000**| ARGUMENTS NON VALIDES | Un ou plusieurs arguments ne sont pas valides.|
|  **8000** | USER_ABORT |L’utilisateur abandonne l’opération.|
| **9000**| OLD_PLATFORM | Le code de plateforme est obsolète et n’implémente pas cette API.|
| **10 000**| SIZE_EXCEEDED |  La valeur de retour est trop grande et a dépassé les limites de la taille de la plateforme.|

## <a name="code-snippets"></a>Extraits de code

* Appeler `selectMedia` l’API pour capturer des images à l’aide de l’appareil photo :

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

* Appeler `getMedia` l’API pour récupérer des supports volumineux en blocs :

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

* Appeler `viewImages` l’API par ID, qui est retournée par `selectMedia` l’API :

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

* Appeler `viewImages` l’API par URL :

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

* Appel `selectMedia` et `getMedia` API pour l’enregistrement audio via le microphone :

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
* [Intégrer Sélecteur de personnes](people-picker-capability.md)
* [Exigences et considérations relatives aux bots multimédias hébergés par l’application](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
