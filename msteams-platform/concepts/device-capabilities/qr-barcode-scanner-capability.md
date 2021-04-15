---
title: Intégrer la fonctionnalité de scanneur QR ou code-barres
description: Comment utiliser le SDK client JavaScript teams pour tirer parti des fonctionnalités de QR ou de scanneur de code-barres
keywords: Fonctionnalités natives d'appareil photo qr code qrcode code-barres scanneur de scanneur de codes-barres
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 956d56c9d52785820f95ca2df323d61dcacc586b
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696289"
---
# <a name="integrate-qr-or-barcode-scanner-capability"></a>Intégrer la fonctionnalité de scanneur QR ou code-barres 

Ce document vous guide sur l'intégration de la fonctionnalité de QR ou de scanneur de code-barres. 

Le code-barres est une méthode de représentation des données sous forme visuelle et lisible par l'ordinateur. Le code-barres contient des informations sur un produit, telles qu'un type, une taille, un fabricant et un pays d'origine sous la forme de barres et d'espaces. Le code est lu à l'aide du scanneur optique sur votre appareil photo natif. Pour une expérience de collaboration enrichie, vous pouvez intégrer la fonctionnalité de QR ou de scanneur de code-barres fournie dans la plateforme Teams à votre application Teams.   

Vous pouvez utiliser le [SDK client JavaScript Microsoft Teams,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)qui fournit les outils nécessaires à votre application pour accéder aux fonctionnalités natives de l'appareil de l'utilisateur. [](native-device-permissions.md) Utilisez `scanBarCode` l'API pour intégrer la fonctionnalité de scanneur dans votre application. 

## <a name="advantage-of-integrating-qr-or-barcode-scanner-capability"></a>Avantage de l'intégration des fonctionnalités de QR ou de scanneur de code-barres

Voici les avantages de l'intégration des fonctionnalités de QR ou de scanneur de code-barres : 

* L'intégration permet aux développeurs d'applications web sur la plateforme Teams de tirer parti des fonctionnalités d'analyse de QR ou de code-barres avec le SDK client JavaScript teams.
* Avec cette fonctionnalité, l'utilisateur doit aligner uniquement une QR ou un code-barres dans un cadre au centre de l'interface utilisateur du scanneur et le code est analysé automatiquement. Les données stockées sont partagées avec l'application web d'appel. Cela évite les désagréments et les erreurs humaines liés à la saisie manuelle de codes de produit longs ou d'autres informations pertinentes.

Pour intégrer la fonctionnalité de QR ou de scanneur de code-barres, vous devez mettre à jour le fichier manifeste de l'application et appeler `scanBarCode` l'API. Pour une intégration efficace, vous devez bien comprendre l'extrait de [code](#code-snippet) pour appeler l'API, ce qui vous permet d'utiliser la QR native ou la fonctionnalité de scanneur de `scanBarCode` code-barres. L'API fournit une erreur pour une norme de code-barres non pris en place.
Il est important de vous familiariser avec les erreurs de [réponse d'API](#error-handling) pour gérer les erreurs dans votre application Teams.

> [!NOTE] 
> Actuellement, la prise en charge de la QR ou de la fonctionnalité de scanneur de code-barres par Microsoft Teams est disponible uniquement pour les clients mobiles.

## <a name="update-manifest"></a>Mettre à jour le manifeste

Mettez à jour votre application Teams [manifest.jsfichier en](../../resources/schema/manifest-schema.md#devicepermissions) ajoutant la propriété et en `devicePermissions` spécifiant `media` . Il permet à votre application de demander les autorisations requises aux utilisateurs avant qu'ils commencent à utiliser la QR ou la fonctionnalité de scanneur de code-barres.

``` json
"devicePermissions": [
    "media",
],
```

> [!NOTE]
> **L'invite Demander des autorisations** s'affiche automatiquement lorsqu'une API Teams pertinente est lancée. Pour plus d'informations, voir [Demander des autorisations d'appareil.](native-device-permissions.md)

## <a name="scanbarcode-api"></a>ScanBarCode API

L'API appelle le contrôle scanneur qui permet à l'utilisateur d'analyser différents types de codes-barres et renvoie le résultat sous forme `ScanBarCode` de chaîne.

Pour personnaliser l'expérience d'analyse du code-barres, la configuration facultative du code-barres est transmise en tant qu'entrée à `ScanBarCode` l'API. Vous pouvez spécifier l'intervalle de délai d'analyse en secondes à l'aide `timeOutIntervalInSec` de . Sa valeur par défaut est 30 secondes et la valeur maximale est de 60 secondes.

**L'API scanBarCode()** prend en charge les types de codes-barres suivants :

| Type de code-barres | Pris en charge sur Android | Pris en charge sur iOS |
| ---------- | ---------- | ------------ |
| Barre de code | Oui | Non |
| Code 39 | Oui | Oui | 
| Code 93 | Oui | Oui |
| Code 128 | Oui | Oui |
| EAN-13 | Oui | Oui |
| EAN-8 | Oui | Oui |
| ITF | Non | Oui |
| QR Code | Oui | Oui |
| RSS étendu | Oui | Non |
| RSS-14 | Oui | Non |
| UPC-A | Oui | Oui |
| UPC-E | Oui | Oui |

**Expérience d'application web pour `ScanBarCode` API pour l'expérience d'application** web QR ou de scanneur de code-barres pour la 
 ![ fonctionnalité de scanneur de code-barres ou qr](../../assets/images/tabs/qr-barcode-scanner-capability.png)

## <a name="error-handling"></a>Gestion des erreurs

Vous devez veiller à gérer ces erreurs de manière appropriée dans votre application Teams. Le tableau suivant répertorie les codes d'erreur et les conditions dans lesquelles les erreurs sont générées : 

|Code d’erreur |  Nom de l'erreur     | Condition|
| --------- | --------------- | -------- |
| **100** | NOT_SUPPORTED_ON_PLATFORM | L'API n'est pas prise en charge sur la plateforme actuelle.|
| **500** | INTERNAL_ERROR | Une erreur interne est rencontrée lors de l'opération requise.|
| **1000** | PERMISSION_DENIED |L'autorisation est refusée par l'utilisateur.|
| **3000** | NO_HW_SUPPORT | Le matériel sous-jacent ne prend pas en charge la fonctionnalité.|
| **4000** | INVALID_ARGUMENTS | Un ou plusieurs arguments ne sont pas valides.|
| **8000** | USER_ABORT |L'utilisateur abandonne l'opération.|
| **8001** | OPERATION_TIMED_OUT | Nous n'avons pas pu détecter le code-barres dans l'intervalle de temps donné.|
| **9000** | OLD_PLATFORM | Le code de plateforme est obsolète et n'implémente pas cette API.|

## <a name="code-snippet"></a>Extrait de code

**Appel `ScanBarCode()` API pour** analyser la QR ou le code-barres à l'aide de l'appareil photo :

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

> [!div class="nextstepaction"]
> [Intégrer des fonctionnalités multimédias dans Teams](mobile-camera-image-permissions.md)

> [!div class="nextstepaction"]
> [Intégrer des fonctionnalités d'emplacement dans Teams](location-capability.md)
