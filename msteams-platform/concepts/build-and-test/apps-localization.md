---
title: Localisation de votre application
description: Décrit les considérations à prendre en compte pour la Microsoft Teams application.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publish store office publishing AppSource localization language
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566046"
---
# <a name="localization-for-microsoft-teams-apps"></a>Localisation pour les applications Microsoft Teams de recherche

Lorsque vous localisez votre Microsoft Teams, vous devez prendre en compte les considérations suivantes :

1. Votre Teams dans le Store (le cas échéant).
1. Chaînes orientées utilisateur final dans le manifeste de votre application. Par exemple, commandes de bot.
1. Réponse au texte local envoyé par vos utilisateurs.

## <a name="localizing-your-appsource-listing"></a>Localisation de votre liste AppSource

Si vous publiez dans le Store, vous devez savoir que la recherche dans AppSource n’est pas encore prise en charge. Toutefois, en vue de la prise en charge des listes localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre liste. Actuellement, seules les informations de langue par défaut (anglais) que vous fournissez dans [l’Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) pour votre liste s’affichent dans la liste du site web [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) pour votre application.

### <a name="example-of-configuring-localization"></a>Exemple de configuration de la localisation

Pour configurer une langue supplémentaire pour votre application, dans [l’Partner Center,](/office/dev/store/submit-to-appsource-via-partner-center)sélectionnez l’anglais et la langue supplémentaire de l’application. Le français est utilisé dans cet exemple :

1. Ajouter l’anglais
    * Remplissez le nom de l’application.
    * Remplissez une brève description de l’application en anglais.
    * Remplissez la description longue de l’application en anglais.
    * Dans la description longue, ajoutez également la ligne « Cette application est disponible en français ».
    * Télécharger images de l’interface utilisateur de votre application (en anglais).
2. Ajouter le français
    * Remplissez le nom de l’application.
    * Remplissez une brève description de l’application en français.
    * Remplissez la description longue de l’application en français.
    * Télécharger images de l’interface utilisateur de votre application (en français).

Les images que vous téléchargez avec l’anglais seront utilisées dans AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Localisation des chaînes dans le manifeste de votre application

Vous devez utiliser le Microsoft Teams d’application v1.5+ pour localiser correctement votre application. Pour ce faire, vous pouvez définir l’attribut de votre manifest.jssur « ' » et mettre à jour la propriété « manifestVersion » sur `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json « 1.7 ».

### <a name="example-manifestjson-change"></a>Exemple manifest.jsmodification

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

Vous souhaitez ensuite ajouter la propriété « localizationInfo » avec la langue par défaut que votre application prend en charge. La langue par défaut est utilisée comme langue de base finale si les paramètres client de l’utilisateur ne correspondent à aucune de vos autres langues.

### <a name="example-manifestjson-change"></a>Exemple manifest.jsmodification

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de toutes les chaînes orientées utilisateur dans votre manifeste. Ces fichiers doivent adhérer au schéma [JSON](../../resources/schema/localization-schema.md) du fichier de localisation et ils doivent être ajoutés à la propriété « localizationInfo » de votre manifeste. Chaque fichier correspond à une balise de langue que le client Teams utilise pour choisir les chaînes appropriées. La balise de langue prend la forme, mais il est recommandé d’omettre la partie pour cibler toutes les régions qui prennent en charge <language> - <region> la <region> langue souhaitée.

Le client Teams appliquera les chaînes dans cet ordre : chaînes de langue par défaut -> chaînes de langue de l’utilisateur uniquement -> langue de l’utilisateur + chaînes de région de l’utilisateur.

Par exemple, vous fournissez une langue par défaut « fr » (français, toutes les régions) et des fichiers linguistiques supplémentaires pour « en » (anglais, toutes les régions) et « en-gb » (anglais, Grande-France). Si la langue de l’utilisateur est définie sur « en-gb » :

1. Le Teams client prend les chaînes « fr » pour les réécrire par les chaînes « en ».
2. Overwrite those with the 'en-gb' strings.

Si la langue de l’utilisateur est définie sur « en-ca » : 

1. Le Teams client prend les chaînes « fr » pour les réécrire par les chaînes « en ».
2. Étant donné qu’aucune localisation « en-ca » n’est fournie, les localisations « en » seront utilisées.

Si la langue de l’utilisateur est définie sur « es-es » (es-es), le client Teams prend les chaînes « fr » et ne les remplace par aucun des fichiers de langue.

Par conséquent, il est vivement recommandé de fournir des traductions linguistiques de niveau supérieur uniquement dans votre manifeste ('en' au lieu de « en-us » ) et de fournir uniquement des substitutions au niveau de la région pour les chaînes qui en ont besoin.

### <a name="example-manifestjson-change"></a>Exemple manifest.jsmodification

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

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a>Gestion des envois de texte localisées de vos utilisateurs

Si vous fournissez des versions localisées de votre application, il est très probable que vos utilisateurs répondent avec la même langue. Teams ne traduit pas les soumissions de l’utilisateur dans la langue par défaut, votre application devra donc gérer cela. Par exemple, si vous fournissez une valeur localisée, les réponses à votre bot seront le texte localisée de la commande, et non `commandList` la langue par défaut. Votre application devra répondre de manière appropriée.

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | .NET |
|-------------|-------------|------|
| Localisation d’application | Microsoft Teams’application à l’aide du bot et de l’onglet. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


