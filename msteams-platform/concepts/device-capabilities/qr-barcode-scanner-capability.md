---
title: Intégrer la fonctionnalité de scanneur QR ou code-barres
author: Rajeshwari-v
description: Comment utiliser kit de développement logiciel (SDK) client JavaScript Teams pour tirer parti de la fonctionnalité QR ou du détecteur de codes-barres
keywords: camera media qr code qrcode bar code code-barres détecteur analyse fonctionnalités native appareil autorisations
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 1a8b89754ddf4f04fb2cc6f5890d8ce4c3f25dab
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757716"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>Intégrer la fonctionnalité de scanneur QR ou code-barres

Le code-barres est une méthode de représentation des données sous une forme visuelle et lisible par l’ordinateur. Le code-barres contient des informations sur un produit, telles qu’un type, une taille, un fabricant et un pays d’origine sous la forme de barres et d’espaces. Le code est lu à l’aide du détecteur optique sur votre appareil photo natif. Pour une expérience collaborative plus riche, vous pouvez intégrer la fonctionnalité de QR ou de détecteur de codes-barres fournie dans la plateforme Teams à votre application Teams.

Vous pouvez utiliser [Microsoft Teams SDK client JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), qui fournit les outils nécessaires à votre application pour accéder aux [fonctionnalités d’appareil natif](native-device-permissions.md) de l’utilisateur. Utilisez l’API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) pour intégrer la fonctionnalité de détecteur dans votre application.

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>Avantage de l’intégration de la fonctionnalité QR ou du détecteur de codes-barres

Voici les avantages de l’intégration des fonctionnalités de QR ou de détecteur de codes-barres :

* L’intégration permet aux développeurs d’applications web sur Teams plateforme de tirer parti des fonctionnalités d’analyse QR ou de code-barres avec Teams kit de développement logiciel (SDK) client JavaScript.
* Avec cette fonctionnalité, l’utilisateur doit uniquement aligner un QR ou un code-barres dans un cadre au centre de l’interface utilisateur du scanneur et le code est analysé automatiquement. Les données stockées sont partagées avec l’application web appelante. Cela évite les désagréments et les erreurs humaines liés à la saisie manuelle de codes de produit longs ou d’autres informations pertinentes.

Pour intégrer la fonctionnalité de QR ou de détecteur de codes-barres, vous devez mettre à jour le fichier manifeste de l’application et appeler l’API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) . Pour une intégration efficace, vous devez avoir une bonne compréhension d’[extrait de code](#code-snippet) pour appeler l’API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_), ce qui vous permet d’utiliser la fonctionnalité QR native ou le détecteur de codes-barres. L’API génère une erreur pour une norme de code-barres non prise en charge.
Il est important de vous familiariser avec les [erreurs de réponse d’API](#error-handling) pour gérer les erreurs dans votre application Teams.

> [!NOTE]
> Actuellement, la prise en charge de Microsoft Teams pour QR et le détecteur de code-barres QR est disponible uniquement pour les clients mobiles.

## <a name="update-manifest"></a>Mise à jour du manifeste

Mettez à jour le fichier [manifest.json](../../resources/schema/manifest-schema.md#devicepermissions) de votre application Teams en ajoutant la `devicePermissions`propriété et en spécifiant`media`. Il permet à votre application de demander aux utilisateurs les autorisations requises avant de commencer à utiliser la fonctionnalité QR ou le détecteur de codes-barres. La mise à jour du manifeste de l’application est la suivante :

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> L’invite **d’autorisations de demande** s’affiche automatiquement lorsqu’une API Teams pertinente est lancée. Pour plus d'informations, reportez-vous à la section [Demander les autorisations du périphérique](native-device-permissions.md).

## <a name="scanbarcode-api"></a>API ScanBarCode

L’API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_) appelle le contrôle détecteur qui permet à l’utilisateur d’analyser différents types de code-barres et retourne le résultat sous forme de chaîne.

Pour personnaliser l’expérience d’analyse du code-barres, la [configuration de code-barres](/javascript/api/@microsoft/teams-js/microsoftteams.media.barcodeconfig?view=msteams-client-js-latest&preserve-view=true) facultatives sont transmises en entrée à l’API [scanBarCode](/javascript/api/@microsoft/teams-js/microsoftteams.media?view=msteams-client-js-latest&preserve-view=true#scanBarCode__error__SdkError__decodedText__string_____void__BarCodeConfig_). Vous pouvez spécifier l’intervalle de délai d’expiration de l’analyse en secondes à l’aide de `timeOutIntervalInSec`. Sa valeur par défaut est 30 secondes et la valeur maximale est 60 secondes.

L’API **scanBarCode()** prend en charge les types de code-barres suivants :

| Type de code-barres | Pris en charge sur Android | Pris en charge sur iOS |
| ---------- | ---------- | ------------ |
| Barre de code | Oui | Non |
| Code 39 | Oui | Oui |
| Code 93 | Oui | Oui |
| Code 128 | Oui | Oui |
| EAN-13 | Oui | Oui |
| EAN-8 | Oui | Oui |
| ITF | Non | Oui |
| Code QR | Oui | Oui |
| RSS développé | Oui | Non |
| RSS-14 | Oui | Non |
| UPC-A | Oui | Oui |
| UPC-E | Oui | Oui |

L’image suivante illustre l’expérience d’application web de la fonctionnalité QR ou de détecteur de codes-barres :

![expérience d’application web pour la fonctionnalité qr ou détecteur de codes-barres](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>Gestion des erreurs

Vous devez vous assurer de traiter ces erreurs de manière appropriée dans votre application Teams. Le tableau suivant répertorie les codes d'erreur et les conditions dans lesquelles les erreurs sont générées :

|Code d’erreur |  Nom de l’erreur     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L’API n’est pas prise en charge sur la plateforme actuelle.|
| **500** | INTERNAL_ERROR | Une erreur interne a été rencontrée lors de l'exécution de l'opération requise.|
| **1 000** | PERMISSION_DENIED |L’autorisation est refusée par l’utilisateur.|
| **3000** | NO_HW_SUPPORT | Le matériel sous-jacent ne prend pas en charge la fonctionnalité.|
| **4000** | ARGUMENTS NON VALIDES | Un ou plusieurs arguments ne sont pas valides.|
| **8000** | USER_ABORT |L’utilisateur abandonne l’opération.|
| **8001** | OPERATION_TIMED_OUT | Impossible de détecter le code-barres dans l’intervalle de temps donné.|
| **9000** | OLD_PLATFORM | Le code de plateforme est obsolète et n’implémente pas cette API.|

## <a name="code-snippet"></a>Extrait de code

**Appel d’`ScanBarCode()` API** pour l’analyse de QR ou code-barres à l’aide de la caméra :

```javascript
const config: microsoftTeams.media.BarCodeConfig = {
  timeOutIntervalInSec: 30};
microsoftTeams.media.scanBarCode((error: microsoftTeams.SdkError, decodedText: string) => {
  if (error) {
    if (error.message) {
      output(" ErrorCode: " + error.errorCode + error.message);
    } else {
      output(" ErrorCode: " + error.errorCode);
    }
  } else if (decodedText) {
    output(decodedText);
  }
}, config);
```

## <a name="see-also"></a>Voir aussi

* [Intégrer les fonctionnalités médias](mobile-camera-image-permissions.md)
* [Intégrer les fonctionnalités d’emplacement sur Teams](location-capability.md)
* [Intégrer le sélecteur de personnes dans Teams](people-picker-capability.md)
