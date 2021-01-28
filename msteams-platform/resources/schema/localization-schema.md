---
title: Référence du schéma JSON du fichier de localisation
description: Décrit le schéma de localisation pris en charge par le fichier de localisation pour Microsoft Teams
ms.topic: reference
keywords: Localisation du schéma de manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: 696a65de70a63e767f8fcdb040364fe90cde8716
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014599"
---
# <a name="reference-localization-file-json-schema"></a>Référence : schéma JSON du fichier de localisation

Le fichier de localisation de Microsoft Teams décrit les traductions linguistiques qui seront servies en fonction des paramètres de langue du client. Votre fichier doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) . Pour plus d’informations, [voir localisation d’application.](~/concepts/build-and-test/apps-localization.md)

## <a name="sample"></a>Échantillon

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "name.short": "Le App Studio",
  "name.full": "App Studio pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App Studio.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App Studio.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

Le schéma définit les propriétés suivantes :

## <a name="schema"></a>$schema

**URI**

L https:// URL référente au schéma JSON pour le manifeste.

> [!TIP]
> Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code : `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>name.short

**Chaîne, longueur maximale 30**

Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.

## <a name="namefull"></a>name.full

**Chaîne, longueur maximale 100**

Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.

## <a name="descriptionshort"></a>description.short

**Chaîne, longueur maximale 80**

Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.

## <a name="descriptionfull"></a>description.full

**Chaîne, longueur maximale 4000**

Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.

## <a name="statictabs0-910-5name"></a>staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name

**Chaîne, longueur maximale 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="bots0commandlists0-2commands0-9title"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**Chaîne, longueur maximale 32**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="bots0commandlists0-2commands0-9description"></a>bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**Chaîne, longueur maximale 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title

**Chaîne, longueur maximale 32**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description

**Chaîne, longueur maximale 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title

**Chaîne, longueur maximale 32**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description

**Chaîne, longueur maximale 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value

**Chaîne, longueur maximale 512**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title

**Chaîne, longueur maximale 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title

**Chaîne, longueur maximale 64**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.
