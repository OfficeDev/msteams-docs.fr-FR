---
title: Localiser la référence de schéma JSON
description: Décrit le schéma de localisation pris en charge par le fichier de localisation pour Microsoft Teams à l’aide d’un exemple de schéma
ms.topic: reference
ms.localizationpriority: high
keywords: localisation du schéma du manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: cf55754b5f9b30508bc01184d75f489dc2a5b7b7
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111912"
---
# <a name="localize-json-schema-reference"></a>Localiser la référence de schéma JSON

Le fichier de localisation de Microsoft Teams décrit les traductions de langue servies en fonction des paramètres de langue du client. Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).

> [!TIP]
> Spécifiez le schéma au début de votre manifeste pour activer `IntelliSense` ou un support similaire de votre éditeur de code : `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="example"></a>Exemple

Voici un exemple de schéma JSON de localisation :

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

|Propriété|Type|Longueur maximale|Description|
|---------------|--------|---------|------------------|
|`$schema`|URI|N/A|L’URL https:// fait référence au schéma JSON pour le manifeste.|
|`name.short`|Chaîne|30|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`name.full`|Chaîne|100|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`description.short`|Chaîne|80|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`description.full`|Chaîne|4000|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`staticTabs\\[([0-9]|1[0-5])\\]\\.name`|Chaîne|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title`|Chaîne|32|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description`|Chaîne|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title`|Chaîne|32|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description`|Chaîne|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title`|Chaîne|32|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description`|Chaîne|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value`|Chaîne|512|Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title`|Chaîne|128|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title`|Chaîne|64|Remplace les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.description`|Chaîne|128|Une brève description de la notification.|
|`activities.activityTypes\\[\\b([0-9]|[1-8][0-9]|9[0-9]|1[01][0-9]|12[0-7])\\b]\\.templateText`|Chaîne|128|Exemple : « {actor} a créé la tâche {taskId} pour vous »|

## <a name="see-also"></a>Voir aussi

[Localiser votre application](~/concepts/build-and-test/apps-localization.md)
