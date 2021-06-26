---
title: Localiser votre application
description: Décrit les considérations à prendre en compte pour la Microsoft Teams application.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publient la langue de localisation d’AppSource de publication office dans le Store
ms.date: 05/15/2018
ms.openlocfilehash: c73188bb24960b9ef0706955d09d23b618c04e5c
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140039"
---
# <a name="localize-your-app"></a>Localiser votre application

Vous devez prendre en compte les facteurs suivants pour trouver votre application Microsoft Teams suivante :

1. [Localisez votre liste AppSource.](#localize-your-appsource-listing)
1. [Localisez les chaînes dans le manifeste de votre application.](#localize-strings-in-your-app-manifest) 
1. [Gérer les envois de texte localisées de vos utilisateurs.](#handle-localized-text-submissions-from-your-users)

## <a name="localize-your-appsource-listing"></a>Localisez votre liste AppSource

Si vous publiez l’application dans le Store, vous devez savoir que la recherche dans AppSource n’est pas encore prise en charge. Pour prendre en charge les listes localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre liste. Les informations de langue par défaut que vous fournissez dans [l’Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) pour votre liste apparaissent dans la liste du site [web AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) de votre application. Actuellement, la langue par défaut est l’anglais.

### <a name="configure-localization"></a>Configurer la localisation

Pour configurer une langue supplémentaire pour votre application, dans [l’Partner Center,](/office/dev/store/submit-to-appsource-via-partner-center)sélectionnez l’anglais et la langue supplémentaire de l’application. Le français est utilisé comme langue supplémentaire dans l’exemple suivant :

1. Ajouter l’anglais
    * Entrez le nom de l’application.
    * Entrez une brève description de l’application en anglais.
    * Entrez la description longue de l’application en anglais.
    * Dans la description longue, entrez : **Cette application est disponible en français.**
    * Télécharger images de l’interface utilisateur de votre application (en anglais).
2. Ajouter le français
    * Entrez le nom de l’application.
    * Entrez une brève description de l’application en français.
    * Entrez la description longue de l’application en français.
    * Télécharger images de l’interface utilisateur de votre application (en français).

Les images que vous téléchargez avec l’anglais sont utilisées dans AppSource.

## <a name="localize-strings-in-your-app-manifest"></a>Localiser les chaînes dans le manifeste de votre application

Vous devez utiliser le schéma Microsoft Teams’application et `v1.5` ultérieurement pour le localiser. Pour ce faire, vous pouvez définir l’attribut de votre manifest.jssur le fichier ou une version supérieure et mettre à jour la propriété en `$schema` **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** version `manifestVersion` `$schema` `1.5` (dans ce cas). 

Vous devez ajouter la `localizationInfo` propriété avec la langue par défaut que votre application prend en charge. La langue par défaut est utilisée comme langue de base finale si les paramètres du client de l’utilisateur ne correspondent à aucune de vos langues supplémentaires.

### <a name="example-manifestjson-change"></a>Exemple manifest.jsmodification

L'manifest.jssuivante permet d’ajouter la propriété avec la langue par défaut que votre application prend en charge `localizationInfo` avec `additionalLanguages` :

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

### <a name="example-localization-json-change"></a>Exemple de modification .json de localisation

Voici un exemple de localisation .json :

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```


Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de toutes les chaînes orientées utilisateur dans votre manifeste. Ces fichiers doivent respecter le schéma [JSON](../../resources/schema/localization-schema.md) du fichier de localisation et ils doivent être ajoutés à la propriété `localizationInfo` de votre manifeste. Chaque fichier est en corrélation avec une balise de langue, que le client Teams utilise pour sélectionner les chaînes appropriées. La balise de langue prend la forme de, mais vous pouvez omettre la partie pour cibler toutes les régions qui prennent en charge `<language>-<region>` `<region>` la langue souhaitée.

Le client Teams applique les chaînes dans l’ordre suivant : chaînes de langue par défaut -> chaînes de langue de l’utilisateur uniquement -> langue de l’utilisateur + chaînes de région de l’utilisateur.

Par exemple, vous fournissez une langue par défaut « fr » (français, toutes les régions) et des fichiers linguistiques supplémentaires pour « en » (anglais, toutes les régions) et « en-gb » (anglais, Grande-France), la langue de l’utilisateur est définie sur « en-gb ». Les modifications suivantes sont apportées en fonction de la sélection de la langue :

1. Le Teams client prend les chaînes « fr » et les overwrite avec les chaînes « en ».
1. Overwrite the 'en' strings with the 'en-gb' strings.

Si la langue de l’utilisateur est définie sur « en-ca », les modifications suivantes ont lieu en fonction de la sélection de la langue : 

1. Le Teams client prend les chaînes « fr » et les overwrite avec les chaînes « en ».
1. Étant donné qu’aucune localisation « en-ca » n’est fournie, les localisations « en » sont utilisées.

Si la langue de l’utilisateur est définie sur es-es, le client Teams prend les chaînes « fr ». Le client Teams ne remplace pas les chaînes par les fichiers de langue car aucune traduction « es » ou « es-es » n’est fournie.

Par conséquent, vous devez fournir des traductions linguistiques de niveau supérieur uniquement dans votre manifeste. Par exemple, « en » au lieu de « en-us ». Vous devez fournir des substitutions au niveau de la région uniquement pour les chaînes qui en ont besoin. 

### <a name="example-manifestjson-change"></a>Exemple manifest.jsmodification

Le manifest.jssur la modification est illustré dans l’exemple suivant :

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

 Le localization.jssur la modification est illustré dans l’exemple suivant :

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

## <a name="handle-localized-text-submissions-from-your-users"></a>Gérer les envois de texte localisées de vos utilisateurs

Si vous fournissez des versions localisées de votre application, les utilisateurs répondent avec la même langue. Comme Teams ne traduit pas les envois de l’utilisateur dans la langue par défaut, votre application doit gérer les réponses linguistiques localisées. Par exemple, si vous fournissez une valeur localisée, les réponses à votre bot sont le texte localisée de la commande, et non `commandList` la langue par défaut. Votre application doit répondre correctement.

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | .NET | Node.js |
|-------------|-------------|------|------|
| Localisation d’application | Microsoft Teams’application à l’aide du bot et de l’onglet. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

