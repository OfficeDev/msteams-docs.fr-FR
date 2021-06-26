---
title: Localize JSON schema reference
description: Décrit le schéma de localisation pris en charge par le fichier de localisation pour Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: Localisation du schéma de manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: 6e8f666cc6bfa693d7f2f469fc58fd6ee4860a80
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140511"
---
# <a name="localize-json-schema-reference"></a>Localize JSON schema reference

Le Microsoft Teams de localisation décrit les traductions linguistiques qui sont servies en fonction des paramètres de langue du client. Votre fichier doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json) . 

> [!TIP]
> Spécifiez le schéma au début de votre manifeste pour activer ou une prise en charge `IntelliSense` similaire à partir de votre éditeur de code : `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",`

## <a name="example"></a>Exemple 

Voici un exemple de schéma JSON de localisation :

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

|Propriété|Type|Longueur maximale|Description|
|---------------|--------|---------|------------------|
|`$schema`|URI|N/A|L https:// URL référente au schéma JSON pour le manifeste.|
|`name.short`|String|30|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`name.full`|Chaîne|100|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`description.short`|String|80|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`description.full`|String|4000|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|String|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|String|32|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`## bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|String|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|String|32|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|String|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|String|32|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|String|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|String|512|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|String|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|String|64|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|

## <a name="see-also"></a>Voir aussi

> [Localiser votre application](~/concepts/build-and-test/apps-localization.md)
