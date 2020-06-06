---
title: Référence du schéma JSON du fichier de localisation
description: Décrit le schéma de localisation pris en charge par le fichier de localisation pour Microsoft teams
keywords: Localisation de schéma de manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: 14e08c582f065d1b09ff0f4906ca6788037460f1
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590864"
---
# <a name="reference-localization-file-json-schema"></a>Référence : schéma JSON du fichier de localisation

Le fichier de localisation Microsoft teams décrit les traductions de langue qui seront fournies en fonction des paramètres de langue du client. Votre fichier doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) . Pour plus d’informations, consultez la rubrique [Localization App](~/concepts/build-and-test/apps-localization.md).

## <a name="sample"></a>Exemple

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

Le schéma définit les propriétés suivantes :

## <a name="schema"></a>$schema

**URI**

URL https://référençant le schéma JSON du manifeste.

> [!TIP]
> Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code :`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`

## <a name="nameshort"></a>Name. Short

**Chaîne, longueur maximale 30**

Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.

## <a name="namefull"></a>Name. Full

**Chaîne, longueur maxi 100**

Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.

## <a name="descriptionshort"></a>Description. Short

**Chaîne, longueur maxi 80**

Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.

## <a name="descriptionfull"></a>Description. Full

**Chaîne, longueur maxi 4000**

Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.

## <a name="statictabs0-910-5name"></a>staticTabs \\ [([0-9] | 1 [0-5]) \\ ] \\ . nom

**Chaîne, longueur maxi 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="bots0commandlists0-2commands0-9title"></a>robots \\ [0 \\ ] \\ . commandLists \\ [[0-2] \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . title

**Chaîne, longueur maxi 32**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="bots0commandlists0-2commands0-9description"></a>robots \\ [0 \\ ] \\ . commandLists \\ [[0-2] \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Description

**Chaîne, longueur maxi 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9title"></a>composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . title

**Chaîne, longueur maxi 32**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9description"></a>composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Description

**Chaîne, longueur maxi 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9parameters0-4title"></a>composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . title

**Chaîne, longueur maxi 32**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9parameters0-4description"></a>composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . Description

**Chaîne, longueur maxi 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9parameters0-4value"></a>composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . Value

**Chaîne, longueur maxi 512**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a>composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . Choices [ \\ [0-9] \\ ] \\ . title

**Chaîne, longueur maxi 128**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.

## <a name="composeextensions0commands0-9taskinfotitle"></a>composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . TaskInfo \\ . title

**Chaîne, longueur maxi 64**

Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.