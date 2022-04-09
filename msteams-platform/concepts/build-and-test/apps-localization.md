---
title: Localiser votre application
description: Décrit les considérations relatives à la localisation de votre application Microsoft Teams.
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams publish store office publishing AppSource localization language
ms.date: 05/15/2018
ms.openlocfilehash: 25a7694017cc8002ac23cf7075c59488ceb9773d
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737038"
---
# <a name="localize-your-app"></a>Localiser votre application

Tenez compte des facteurs suivants pour localiser votre application Microsoft Teams :

1. [Localisez votre liste AppSource](#localize-your-appsource-listing).
1. [Localisez les chaînes dans le manifeste de votre application](#localize-strings-in-your-app-manifest).
1. [Gérez les soumissions de texte localisées de vos utilisateurs](#handle-localized-text-submissions-from-your-users).

## <a name="localize-your-appsource-listing"></a>Localiser votre liste AppSource

Si vous publiez l’application dans le Store, fournissez des métadonnées (descriptions, captures d’écran, nom) dans les langues dans lesquelles vous souhaitez que votre application soit répertoriée, et spécifiez explicitement ces langues dans la page **des descriptions** de la Place de marché dans l’Espace partenaires. Pour plus d’informations, consultez les [fronts Microsoft AppSource localisés](/office/dev/store/prepare-localized-solutions#localized-microsoft-appsource-fronts). Pour prendre en charge les descriptions localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre description. Les informations de langue par défaut que vous [fournissez dans l’Espace partenaires](/office/dev/store/submit-to-appsource-via-partner-center) pour votre description s’affichent dans la liste du [site web AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource est un emplacement unique pour tous les besoins de votre équipe. rassemblez tout, y compris les conversations, les réunions, les appels, les fichiers et les outils pour permettre un travail d’équipe plus productif.") de votre application. Actuellement, la langue par défaut est l’anglais.

### <a name="configure-localization"></a>Configurer la localisation

Pour configurer une langue supplémentaire pour votre application, dans [l’Espace partenaires](/office/dev/store/submit-to-appsource-via-partner-center), sélectionnez l’anglais et la langue supplémentaire de l’application. Français est utilisé comme langue supplémentaire dans l’exemple suivant :

1. Ajouter l’anglais
    * Entrez le nom de l’application.
    * Entrez une brève description de l’application en anglais.
    * Entrez la longue description de l’application en anglais.
    * Dans la longue description, entrez : **cette application est disponible dans Français**.
    * Télécharger les images de l’interface utilisateur de votre application (en anglais).
2. Ajouter Français langue
    * Entrez le nom de l’application.
    * Entrez une brève description de l’application dans Français.
    * Entrez la longue description de l’application dans Français.
    * Télécharger les images de l’interface utilisateur de votre application (dans Français).

Les images que vous chargez avec la langue anglaise sont utilisées dans AppSource.

## <a name="localize-strings-in-your-app-manifest"></a>Localiser des chaînes dans le manifeste de votre application

Utilisez le schéma `v1.5` d’application Microsoft Teams et versions ultérieures pour localiser votre application. Pour ce faire, définissez l’attribut `$schema` dans votre fichier manifest.json sur `https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json` ou version ultérieure et mettez à jour la propriété vers `$schema` la `manifestVersion` version (`1.5`dans ce cas).

Ajoutez la `localizationInfo` propriété avec la langue par défaut prise en charge par votre application. La langue par défaut est utilisée comme langue de secours finale si les paramètres client de l’utilisateur ne correspondent à aucune de vos langues supplémentaires.

### <a name="example-manifestjson-change"></a>Exemple de modification manifest.json

Les éléments suivants `manifest.json` permettent d’ajouter la `localizationInfo` propriété avec la langue par défaut prise en charge par votre application, ainsi `additionalLanguages`que :

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

Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de toutes les chaînes accessibles par l’utilisateur dans votre manifeste. Ces fichiers doivent respecter le [schéma JSON du fichier de localisation](../../resources/schema/localization-schema.md) et ils doivent être ajoutés à la `localizationInfo` propriété de votre manifeste. Chaque fichier est corrélé à une balise de langue, que le client Teams utilise pour sélectionner les chaînes appropriées. La balise de langue prend la forme, `<language>-<region>` mais vous pouvez omettre la `<region>` partie pour cibler toutes les régions qui prennent en charge la langue souhaitée.

Le client Teams applique les chaînes dans l’ordre suivant : chaînes de langue par défaut -> chaînes de langue de l’utilisateur uniquement -> langue de l’utilisateur + chaînes de région de l’utilisateur.

Par exemple, vous fournissez une langue par défaut « fr » (Français, toutes les régions) et des fichiers de langue supplémentaires pour « en » (anglais, toutes les régions) et « en-gb » (anglais, Grande-Bretagne), la langue de l’utilisateur est définie sur « en-gb ». Les modifications suivantes ont lieu en fonction de la sélection de la langue :

1. Le client Teams prend les chaînes « fr » et les remplace par les chaînes « en ».
1. Remplacez les chaînes « en » par les chaînes « en-gb ».

Si la langue de l’utilisateur est définie sur « en-ca », les modifications suivantes ont lieu en fonction de la sélection de la langue :

1. Le client Teams prend les chaînes « fr » et les remplace par les chaînes « en ».
1. Étant donné qu’aucune localisation « en-ca » n’est fournie, les localisations « en » sont utilisées.

Si la langue de l’utilisateur est définie sur « es-es », le client Teams prend les chaînes « fr ». Le client Teams ne remplace pas les chaînes par l’un des fichiers de langue, car aucune traduction « es » ou « es-es » n’est fournie.

Par conséquent, vous devez fournir des traductions de langue de niveau supérieur uniquement dans votre manifeste. Par exemple, `en` au lieu de `en-us`. Vous devez fournir des remplacements au niveau de la région uniquement pour les quelques chaînes qui en ont besoin.

### <a name="example-manifestjson-change"></a>Exemple de modification manifest.json

La `manifest.json` modification est illustrée dans l’exemple suivant :

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

 La `localization.json` modification est illustrée dans l’exemple suivant :

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

Si vous fournissez des versions localisées de votre application, les utilisateurs répondent avec la même langue. Comme Teams ne traduit pas les soumissions d’utilisateurs dans la langue par défaut, votre application doit gérer les réponses linguistiques localisées. Par exemple, si vous fournissez un élément localisé `commandList`, les réponses à votre bot sont le texte localisé de la commande, et non la langue par défaut. Votre application doit répondre correctement.

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | .NET | Node.js |
|-------------|-------------|------|------|
| Localisation des applications | Microsoft Teams localisation d’application à l’aide du bot et de l’onglet. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

## <a name="see-also"></a>Voir aussi

[Localiser la référence de schéma JSON](~/resources/schema/localization-schema.md)
