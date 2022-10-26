---
title: Utiliser les API Graph pour extraire des transcriptions
description: Décrit les API pour extraire des transcriptions de réunion
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: 2142bc1346a032f27d8612f6081156d2c4927e8f
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699177"
---
# <a name="use-graph-apis-to-fetch-transcript"></a>Utiliser les API Graph pour extraire des transcriptions

Utilisez les API REST Graph pour l’extraction de transcriptions d’une réunion particulière. Votre application extrait des transcriptions en fonction de l’identifiant utilisateur de l’organisateur de la réunion et de l’ID de réunion.

Les API suivantes sont utilisées pour extraire des transcriptions :

- [Répertorier des callTranscripts](#list-calltranscripts)
- [Obtenir une callTranscript](#get-calltranscript)
- [Obtenir du contenu de callTranscript](#get-calltranscript-content)

### <a name="list-calltranscripts"></a>Répertorier des callTranscripts

Cette API est utilisée pour obtenir une liste de tous les objets `callTranscript` en fonction de l’identifiant utilisateur et de l’ID de réunion. Elle retourne les métadonnées des transcriptions de la réunion, qui contient l’ID de transcription, ainsi que la date et l’heure de création de cette transcription.

**Requête HTTP**

```http
GET /me/onlineMeetings('{meetingId}')/transcripts
GET /users('{userId}')/onlineMeetings('{meetingId}')/transcripts
```

**Paramètres facultatifs de la requête**

Cette méthode prend en charge les paramètres de requête `$skipToken` et `$top` [OData ](/graph/query-parameters) pour vous permettre de personnaliser la réponse.

**Modèles de requête pris en charge**

| Modèle                | Pris en charge | Syntaxe                                 | Notes |
| ---------------------- | ------- | -------------------------------------- | ----- |
| Pagination côté serveur |     ✓     | `@odata.nextLink`                      | Obtenez un jeton de continuation dans la réponse, lorsqu’un jeu de résultats s’étend sur plusieurs pages. |
| Limite de page             |     ✓     | `/transcripts?$top=20` | Obtenez des transcriptions avec la taille de page 20. La limite de page par défaut est 10. La limite de page maximale est de 100. |

**En-têtes de demande**

| En-tête       | Valeur |
|:---------------|:--------|
| Autorisation  | Bearer {token}. Required.  |

**Corps de la demande**

N’indiquez pas le corps de la demande pour cette méthode.

**Réponse**

Si elle réussit, cette méthode renvoie un code de réponse `200 OK` et une collection d’objets `callTranscript` dans le corps de la réponse.

<br>
<details>
<summary><b>Exemple : Liste de callTranscript</b></summary>
<br>
<b>Demande</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts
```

<br>
<b>Réponse</b>
<br>

> [!NOTE]
> L’objet de réponse affiché ci-après peut être raccourci pour plus de lisibilité.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts",
    "@odata.count": 3,
    "@odata.nextLink": "https://graph.microsoft.com/beta/users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts?$skiptoken=MSMjMCMjMjAyMS0wOS0xNlQxMzo1OToyNy4xMjEwMzgzWg%3d%3d",
    "value": [
        {
            "id": "MSMjMCMjZDAwYWU3NjUtNmM2Yi00NjQxLTgwMWQtMTkzMmFmMjEzNzdh",
            "createdDateTime": "2021-09-17T06:09:24.8968037Z"
        },
        {
            "id": "MSMjMCMjMzAxNjNhYTctNWRmZi00MjM3LTg5MGQtNWJhYWZjZTZhNWYw",
            "createdDateTime": "2021-09-16T18:58:58.6760692Z"
        },
        {
            "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
            "createdDateTime": "2021-09-16T18:56:00.9038309Z"
        }        
    ]
}
```

</details>

### <a name="get-calltranscript"></a>Obtenir une callTranscript

Votre application analyse la liste des ID de transcription, reçus comme réponse de l’API `List callTranscripts`, pour obtenir l’ID de transcription requis. Cette API est utilisée pour obtenir les métadonnées d’une seule transcription basées sur l’identifiant utilisateur, l’ID de réunion et l’ID de transcription.

**Requête HTTP**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
```

**En-têtes de demande**

| En-tête       | Valeur |
|:---------------|:--------|
| Autorisation  | Bearer {token}. Required.  |

**Corps de la demande**

N’indiquez pas le corps de la demande pour cette méthode.

**Réponse**

Si elle réussit, cette méthode renvoie un code de réponse `200 OK` et un objet `callTranscript` dans le corps de la réponse.

<br>
<details>
<summary><b>Exemple : obtenir une callTranscript</b></summary>
<br>
<b>Demande</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4
```

<br>
<b>Réponse</b>
<br>

> [!NOTE]
> L’objet de réponse affiché ci-après peut être raccourci pour plus de lisibilité.

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts/$entity",
    "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
    "createdDateTime": "2021-09-17T06:09:24.8968037Z"
}
```

</details>

### <a name="get-calltranscript-content"></a>Obtenir le contenu d’une callTranscript

Cette API est utilisée pour obtenir la transcription de l’ID de transcription sélectionné qui a été obtenu dans la réponse de l’API `Get callTranscript`. Elle renvoie le contenu de la transcription.

**Requête HTTP**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
```

**Paramètres facultatifs de la requête**

Cette méthode prend en charge le `$format` [paramètre de requête OData](/graph/query-parameters) qui permet une personnalisation de la réponse.

Les types de format pris en charge sont `text/vtt` pour vtt OR `application/vnd.openxmlformats-officedocument.wordprocessingml.document` pour le format docx.

**En-têtes de demande**

| En-tête       | Valeur |
|:---------------|:--------|
| Autorisation  | Bearer {token}. Required.  |
| Accepter  | text/vtt OR  application/vnd.openxmlformats-officedocument.wordprocessingml.document. Facultatif.  |

**Corps de la demande**

N’indiquez pas le corps de la demande pour cette méthode.

**Réponse**

Si elle réussit, cette méthode renvoie un code de réponse `200 OK` et contient des octets pour un objet callTranscript dans le corps de la réponse. L’en-tête `content-type` spécifie le type de contenu de la transcription.

**Exemples**
<br>
<details>
<summary><b>Exemple : obtenir le contenu d’une callTranscript</b></summary>
<br>
<b>Demande</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
```

<br>
<b>Réponse</b>
<br>

La réponse contient des octets pour la transcription dans le corps. L’en-tête `content-type` spécifie le type de contenu de la transcription.

> [!NOTE]
> L’objet de réponse affiché ci-après peut être raccourci pour plus de lisibilité.

```http
HTTP/1.1 200 OK
Content-type: text/vtt

WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>Exemple : obtenir le contenu d’une callTranscript spécifiant le paramètre de requête $format</b></summary>
<br>
<b>Demande</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
 ```

<br>
<b>Réponse</b>
<br>

La réponse contient des octets pour la transcription dans le corps. L’en-tête `content-type` spécifie le type de contenu de la transcription.

> [!NOTE]
> L’objet de réponse affiché ci-après peut être raccourci pour plus de lisibilité.

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>Exemple : obtenir le contenu d’une callTranscript spécifiant l’en-tête Accepter</b></summary>
<br>
<b>Demande</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>Réponse</b>
<br>

La réponse contient des octets pour la transcription dans le corps. L’en-tête `content-Type` spécifie le type de contenu de la transcription.

> [!NOTE]
> L’objet de réponse affiché ci-après peut être raccourci pour plus de lisibilité.

```http
HTTP/1.1 200 OK
Content-type: application/vnd.openxmlformats-officedocument.wordprocessingml.document
    
0:0:0.0 --> 0:0:5.320
User Name
This is a transcript test.
```

</details>
<br>
<details>
<summary><b>Exemple : obtenir le contenu d’une callTranscript avec $format ayant la priorité sur l’en-tête Accepter</b></summary>
<br>
<b>Demande</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>Réponse</b>
<br>

La réponse contient des octets pour la transcription dans le corps. L’en-tête `content-Type` spécifie le type de contenu de la transcription.

> [!NOTE]
> L’objet de réponse affiché ci-après peut être raccourci pour plus de lisibilité.

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
   
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>

