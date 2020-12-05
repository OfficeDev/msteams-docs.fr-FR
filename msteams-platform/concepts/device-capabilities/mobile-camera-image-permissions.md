---
title: Fonctionnalités de l’appareil photo et de l’image dans teams
description: Comment utiliser le kit de développement logiciel (SDK) du client JavaScript teams pour activer les fonctionnalités d’image et de caméra natives
keywords: fonctionnalités de l’image de l’appareil photo natives
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d0ca4dc9c289ec525aa99ea0e156a9f91f5b5d4a
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576873"
---
# <a name="camera-and-image-capabilities-in-teams"></a>Fonctionnalités de l’appareil photo et de l’image dans teams

>[!IMPORTANT]
>
> * Actuellement, la prise en charge de teams pour les fonctionnalités d’image et de caméra est uniquement disponible pour les clients mobiles.
>* Les `selectMedia` `getMedia` API, et `viewImages` peuvent être appelées à partir de plusieurs surfaces Teams, telles que des modules de tâches, des onglets et des applications personnelles. Pour plus d’informations, _consultez la rubrique_ [points d’entrée pour les applications teams](../extensibility-points.md)

Vous pouvez utiliser le  [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)pour intégrer facilement les fonctionnalités de caméra et d’image dans votre application mobile Microsoft Teams. Le kit de développement logiciel (SDK) fournit les outils nécessaires à votre application pour accéder aux autorisations de l' [appareil](native-device-permissions.md?tabs=desktop#device-permissions) d’un utilisateur et créer une expérience plus riche.

Les API [selectMedia](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true), [getMedia](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)et [viewImages](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true) vous permettent d’utiliser les fonctionnalités de caméra/image natives comme suit :

* Utilisez le **contrôle** de la caméra native pour permettre aux utilisateurs de **capturer et de joindre des images** en déplacement.
* Utilisez la **prise en charge** de la Galerie native pour permettre aux utilisateurs de **Sélectionner des images d’appareil** en pièces jointes.
* Utilisez **le contrôle** de l’afficheur d’images natives pour afficher un **aperçu de plusieurs images** à la fois.
* Prise en charge du **transfert d’image volumineux** (jusqu’à 50 Mo) via le pont SDK
* Prise en charge des **fonctionnalités d’image avancées** permettant aux utilisateurs de prévisualiser et de modifier les images :
  * Numérisez un document, un tableau blanc, des cartes de visite, etc., via l’appareil photo.
  * Rogner et faire pivoter les images.
  * Ajouter du texte, de l’entrée manuscrite ou une annotation à main levée à l’image.

## <a name="get-started"></a>Prise en main

Mettez à jour votre application teams [manifest.jssur](../../resources/schema/manifest-schema.md#devicepermissions) fichier en ajoutant la `devicePermissions`  propriété et en spécifiant `media` . Cela permet à votre application de demander aux utilisateurs finaux les autorisations requises avant d’utiliser l’appareil photo pour capturer l’image ou ouvrir la Galerie pour sélectionner une image à envoyer en tant que pièce jointe.

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> L’invite _demander des autorisations_ s’affiche automatiquement lorsqu’une API teams pertinente est initiée. Pour plus d’informations, *consultez la rubrique* [Request Device permissions](native-device-permissions.md).

## <a name="using-camera-and-image-capability-apis"></a>Utilisation des API de fonctionnalité d’image et de caméra

Vous pouvez utiliser l’ensemble d’API suivant pour activer les fonctionnalités de l’appareil photo et du périphérique d’image :

| API      | Description   |
| --- | --- |
| [**selectMedia**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest&branch=master#selectMedia_MediaInputs___error__SdkError__attachments__Media_______void_&preserve-view=true)| Cette API permet aux utilisateurs de **capturer ou de sélectionner des médias à partir d’un périphérique natif** et de revenir à l’application Web. Les utilisateurs peuvent choisir de modifier, découper, faire pivoter, annoter ou dessiner sur des images avant leur envoi. En réponse à **selectMedia**, l’application Web reçoit les ID de médias des images sélectionnées et peut recevoir une miniature du média sélectionné. |
| [**getMedia**](/javascript/api/@microsoft/teams-js/_media?view=msteams-client-js-latest&branch=master#getMedia__error__SdkError__blob__Blob_____void_&preserve-view=true)| Cette API récupère le média dans des segments quelle que soit la taille. Ces segments sont assemblés et renvoyés à l’application Web sous la forme d’un fichier/BLOB. Avec cette API, une image est divisée en morceaux plus petits pour faciliter le transfert d’image volumineux. |
| [**viewImages**](/javascript/api/@microsoft/teams-js/media?view=msteams-client-js-latest#viewImages_ImageUri_____error___SdkError_____void_&preserve-view=true)| Cette API permet à l’utilisateur d’afficher des images en mode plein écran sous la forme d’une liste déroulante.|

**Expérience des applications Web pour l’API selectMedia** 
 ![ appareil photo et image de l’appareil dans teams](../../assets/images/tabs/image-capability-screenshot.jpg)

## <a name="error-handling"></a>Gestion des erreurs

Vous devez comprendre les codes d’erreur de réponse de l’API et les gérer de manière appropriée. Vous trouverez ci-dessous la liste des codes d’erreur pouvant être renvoyés par la plateforme :

|Code d'erreur |  Nom de l’erreur     | Condition|
| --- | --- | --- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge dans la plateforme actuelle.|
| **404** | FILE_NOT_FOUND | Le fichier spécifié est introuvable à l’emplacement donné.|
| **500** | INTERNAL_ERROR | Une erreur interne s’est produite lors de l’exécution de l’opération requise.|
| **1000** | PERMISSION_DENIED |Autorisations refusées par l’utilisateur.|
| **2000** |NETWORK_ERROR | Problème réseau.|
| **3000** | NO_HW_SUPPORT | Le matériel sous-jacent ne prend pas en charge la fonctionnalité.|
| **4000**| INVALID_ARGUMENTS | Un ou plusieurs arguments ne sont pas valides.|
| **5000** | UNAUTHORIZED_USER_OPERATION | L’utilisateur n’est pas autorisé à effectuer cette opération.|
| **6000** |INSUFFICIENT_RESOURCES | L’opération n’a pas pu aboutir en raison de ressources insuffisantes.|
|**7000** | THROTTLE | La plateforme limite la demande, car l’API a été appelée trop fréquemment.|
|  **8000** | USER_ABORT |L’utilisateur a abandonné l’opération.|
| **9000**| OLD_PLATFORM | Le code de plateforme est obsolète et n’implémente pas cette API.|
| **10000**| SIZE_EXCEEDED |  La valeur renvoyée est trop importante et a dépassé les limites de taille de plateforme.|

## <a name="sample-code-snippets"></a>Exemples d’extraits de code

**API d’appel `selectMedia`**

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

**API d’appel `getMedia`**

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

**`viewImages`API d’appel par ID**

```javascript
view images by id:
    assumption: attachmentArray = select Media API Outputlet uriList = [];
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

**Appel de l’API viewImages par URL**

```javascript
View Images by URL:
    // Assumption 2 urls, url1 and url2let uriList = [];
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
}
```
