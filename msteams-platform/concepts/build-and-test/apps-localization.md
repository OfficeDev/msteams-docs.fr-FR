---
title: Localiser votre application
description: Découvrez les considérations relatives à la localisation de votre application Microsoft Teams et à la localisation des chaînes dans votre manifeste d’application.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/15/2018
ms.openlocfilehash: bd8b579178598b1d485e908f80e9590b27652101
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789869"
---
# <a name="localize-your-app"></a>Localiser votre application

Prenez en compte les facteurs suivants pour localiser votre application Microsoft Teams :

1. [localiser votre liste AppSource](#localize-your-appsource-listing).
1. [localisez les chaînes dans le manifeste de votre application](#localize-strings-in-your-app-manifest).
1. [gérer les envois de texte localisés de vos utilisateurs](#handle-localized-text-submissions-from-your-users).

## <a name="localize-your-appsource-listing"></a>Localiser votre description AppSource

Si vous publiez l’application dans le Store, fournissez des métadonnées (descriptions, captures d’écran, nom) dans les langues dans lesquelles vous souhaitez que votre application soit répertoriée et spécifiez explicitement ces langues sur la page **Référencements** de la Place de marché dans l’Espace partenaires. Pour plus d’informations, consultez [avants Microsoft AppSource localisés](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts). Pour prendre en charge les descriptions localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre description. Les informations de langue par défaut que vous fournissez dans [Espace partenaires](/office/dev/store/submit-to-appsource-via-partner-center) pour votre description s’affichent dans le site web [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource est un emplacement unique pour tous les besoins de votre équipe. rassemblez tous les éléments, y compris les conversations, les réunions, les appels, les fichiers et les outils pour permettre un travail d’équipe plus productif.") description de votre application. Actuellement, la langue par défaut est l’anglais.

### <a name="configure-localization"></a>Configurer la localisation

Pour configurer une langue supplémentaire pour votre application, dans [Espace partenaires](/office/dev/store/submit-to-appsource-via-partner-center), sélectionnez l’anglais et la langue supplémentaire de l’application. Français est utilisé comme langue supplémentaire dans l’exemple suivant :

1. Ajouter une langue anglaise
    * Entrez le nom de l’application.
    * Entrez une brève description de l’application en anglais.
    * Entrez la description longue de l’application en anglais.
    * Dans la description longue, entrez : **Cette application est disponible dans Français**.
    * Chargez les images de l’interface utilisateur de votre application (en anglais).
2. Ajouter Français langue
    * Entrez le nom de l’application.
    * Entrez une brève description de l’application dans Français.
    * Entrez la description longue de l’application dans Français.
    * Chargez les images de l’interface utilisateur de votre application (dans Français).

Les images que vous chargez avec la langue anglaise sont utilisées dans AppSource.

## <a name="localize-strings-in-your-app-manifest"></a>Localiser des chaînes dans le manifeste de votre application

Utilisez le schéma d’application Microsoft Teams `v1.5` et versions ultérieures pour localiser votre application. Pour ce faire, définissez l’attribut `$schema` de votre fichier manifest.json sur `https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json` ou version ultérieure et mettez à jour la classe `manifestVersion` propriété à `$schema` version (`1.5` dans ce cas).

Ajoutez la propriété `localizationInfo` avec la langue par défaut prise en charge par votre application. La langue par défaut est utilisée comme langue de secours finale si les paramètres client de l’utilisateur ne correspondent à aucune de vos langues supplémentaires.

> [!NOTE]
> La version du manifeste doit être identique pour les fichiers manifest.json et localization.json.

### <a name="example-manifestjson-change"></a>Exemple de modification de manifest.json

`manifest.json` permet d’ajouter la propriété `localizationInfo` avec le langage par défaut pris en charge par votre application avec `additionalLanguages` :

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "localizationInfo": {
  "defaultLanguageTag": "en",
  "additionalLanguages": [
   {
    "languageTag": "es-mx",
    "file": "es-mx.json"
   }
  ]
 }
  ...
}
```

### <a name="example-localization-json-change"></a>Exemple de modification du fichier .json de localisation

Voici un exemple de localisation .json :

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```

Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de toutes les chaînes accessibles par l’utilisateur dans votre manifeste. Ces fichiers doivent respecter le [schéma JSON du fichier de localisation](../../resources/schema/localization-schema.md) et doivent être ajoutés à la propriété `localizationInfo` de votre manifeste. Chaque fichier est corrélé à une balise de langue que le client Teams utilise pour sélectionner les chaînes appropriées. La balise de langue prend la forme de `<language>-<region>` mais vous pouvez omettre la partie `<region>` pour cibler toutes les régions qui prennent en charge la langue souhaitée.

Le client Teams applique les chaînes dans l’ordre suivant : chaînes de langue par défaut -> chaînes de langue uniquement de l’utilisateur -> langue de l’utilisateur + chaînes de région de l’utilisateur.

Par exemple, vous fournissez une langue par défaut « fr » (Français, toutes les régions) et des fichiers de langue supplémentaires pour « en » (anglais, toutes les régions) et « en-gb » (anglais, Grande-Royaume-Uni), la langue de l’utilisateur est définie sur « en-gb ». Les modifications suivantes ont lieu en fonction de la sélection de la langue :

1. Le client Teams prend les chaînes « fr » et les remplace par les chaînes « en ».
1. Remplacez les chaînes 'en' par les chaînes 'en-gb'.

Si la langue de l’utilisateur est définie sur « en-ca », les modifications suivantes ont lieu en fonction de la sélection de la langue :

1. Le client Teams prend les chaînes « fr » et les remplace par les chaînes « en ».
1. Étant donné qu’aucune localisation « en-ca » n’est fournie, les localisations « en » sont utilisées.

Si la langue de l’utilisateur est définie sur « es-es », le client Teams prend les chaînes « fr ». Le client Teams ne remplace pas les chaînes par les fichiers de langue, car aucune traduction « es » ou « es-es » n’est fournie.

Par conséquent, vous devez fournir des traductions de langue de niveau supérieur uniquement dans votre manifeste. Par exemple, `en` au lieu de `en-us`. Vous devez fournir des remplacements au niveau de la région uniquement pour les quelques chaînes qui en ont besoin.

### <a name="example-manifestjson-change"></a>Exemple de modification de manifest.json

La modification `manifest.json` est illustrée dans l’exemple suivant :

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en",
    "additionalLanguages": [
      {
        "languageTag": "en-gb",
        "file": "en-gb.json"
      },
      {
        "languageTag": "fr",
        "file": "fr.json"
      },
      {
        "languageTag": "pl",
        "file": "pl.json"
      }
    ]
  }
  ...
}
```

### <a name="example-localization-json-file"></a>Exemple de fichier .json de localisation

 La modification `localization.json` est illustrée dans l’exemple suivant :

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "name.short": "Le App",
  "name.full": "App pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

## <a name="handle-localized-text-submissions-from-your-users"></a>Gérer les soumissions de texte localisées de vos utilisateurs

Si vous fournissez des versions localisées de votre application, les utilisateurs répondent avec la même langue. Étant donné que Teams ne traduit pas les soumissions des utilisateurs dans la langue par défaut, votre application doit gérer les réponses de langue localisée. Par exemple, si vous fournissez un `commandList` localisé, les réponses à votre bot sont le texte localisé de la commande, et non la langue par défaut. Votre application doit répondre correctement.

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | .NET | Node.js |
|-------------|-------------|------|------|
| Localisation d’application | Localisation d’applications Teams à l’aide du bot et de l’onglet. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>Voir aussi

* [Localiser la référence de schéma JSON](~/resources/schema/localization-schema.md)
