---
title: Localisation de votre application
description: Décrit les considérations pour la localisation de votre Microsoft Teams appe.
ms.topic: conceptual
localization_priority: Normal
keywords: les équipes publient le langage de localisation AppSource d’édition de bureau de magasin
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566046"
---
# <a name="localization-for-microsoft-teams-apps"></a>Localisation des applications Microsoft Teams vidéo

Lors de la Microsoft Teams votre application, vous devez tenir compte des éléments suivants :

1. Votre Teams magasin (le cas échéant).
1. L’utilisateur final faisant face à des chaînes dans votre manifeste d’application. Par exemple, les commandes bot.
1. Répondre au texte localisé soumis par vos utilisateurs.

## <a name="localizing-your-appsource-listing"></a>Localisation de votre annonce AppSource

Si vous publiez dans le magasin, vous devez être conscient que la localisation de votre annonce AppSource n’est pas encore prise en charge. Toutefois, en vue de la prise en charge des annonces localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre annonce. Actuellement, seules les informations par défaut (en anglais) que vous fournissez [dans Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) pour votre annonce apparaîtront dans la liste du site Web [d’AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) pour votre application.

### <a name="example-of-configuring-localization"></a>Exemple de localisation configurante

Pour configurer une langue supplémentaire pour votre application, dans [Partner Center, sélectionnez](/office/dev/store/submit-to-appsource-via-partner-center)à la fois l’anglais et la langue supplémentaire de l’application. Français est utilisé dans cet exemple :

1. Ajouter la langue anglaise
    * Remplissez le nom de l’application.
    * Remplissez une courte description de l’application en anglais.
    * Remplissez la longue description de l’application en anglais.
    * Dans la longue description, s’il vous plaît également ajouter la ligne « Cette application est disponible en « Français ».
    * Télécharger les images de votre interface utilisateur (en anglais).
2. Ajouter Français langue
    * Remplissez le nom de l’application.
    * Remplissez une courte description de l’application dans Français.
    * Remplissez la longue description de l’application dans Français.
    * Télécharger les images de l’interface utilisateur de votre application (en Français).

Les images que vous téléchargez avec la langue anglaise seront ceux utilisés dans AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Localisation des chaînes dans le manifeste de votre application

Vous devez utiliser le schéma Microsoft Teams’application v1.5+ pour bien localisér votre application. Vous pouvez le faire en fixant `$schema` l’attribut dans votre manifest.jsdans le fichier https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json à « » et en mettant à jour la propriété « manifestVersion » à « 1,7 ».

### <a name="example-manifestjson-change"></a>Exemple manifest.jssur le changement

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

Vous souhaitez ensuite ajouter la propriété 'localizationInfo' avec le langage par défaut que votre application prend en charge. Le langage par défaut est utilisé comme langue de récupération finale si les paramètres clients de l’utilisateur ne correspondent à aucune de vos langues supplémentaires.

### <a name="example-manifestjson-change"></a>Exemple manifest.jssur le changement

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de tous les utilisateurs faisant face à des chaînes dans votre manifeste. Ces fichiers doivent adhérer au schéma [JSON du fichier de localisation et](../../resources/schema/localization-schema.md) ils doivent être ajoutés à la propriété 'localisationInfo' de votre manifeste. Chaque fichier est corrélé à une balise de langue que Teams client utilise pour choisir les chaînes appropriées. L’étiquette linguistique prend la forme <language> - <region> de, mais il est recommandé d’omettre <region> la partie pour cibler toutes les régions qui soutiennent la langue désirée.

Le Teams client appliquera les chaînes dans cet ordre : chaînes de langage par défaut -> la langue de l’utilisateur ne fait que des chaînes -> langue de l’utilisateur + chaînes de région de l’utilisateur.

Par exemple, vous fournissez une langue par défaut de « fr » (Français, toutes les régions), et des fichiers linguistiques supplémentaires pour « fr » (anglais, toutes les régions) et « en-gb » (anglais, Grande-Bretagne). Si la langue de l’utilisateur est définie sur 'en-gb':

1. Le Teams client prendra les cordes 'fr' les écraser avec les cordes 'en'.
2. Écraser ceux qui ont les cordes 'en-gb'.

Si la langue de l’utilisateur est définie sur « en-ca » : 

1. Le Teams client prendra les cordes 'fr' les écraser avec les cordes 'en'.
2. Comme aucune localisation « en-ca » n’est fournie, les localisations « en » seront utilisées.

Si la langue de l’utilisateur est définie sur « es-es », le client Teams prendra les chaînes « fr » et ne les remplacera pas avec l’un des fichiers linguistiques.

Par conséquent, il est fortement recommandé de fournir des traductions de haut niveau, uniquement en langue dans votre manifeste (« fr » au lieu de « en-us ») et de ne fournir des dérogations au niveau régional pour les quelques chaînes qui en ont besoin.

### <a name="example-manifestjson-change"></a>Exemple manifest.jssur le changement

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

### <a name="example-localization-json-file"></a>Exemple de localisation .json fichier

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

## <a name="handling-localized-text-submissions-from-your-users"></a>Traitement des soumissions de texte localisées de vos utilisateurs

Si vous fournissez des versions localisées de votre application, il est très probable que vos utilisateurs répondront avec la même langue. Teams ne traduit pas les soumissions de l’utilisateur dans la langue par défaut, de sorte que votre application devra gérer cela. Par exemple, si vous fournissez une `commandList` localisée, les réponses à votre bot seront le texte localisé de la commande, pas la langue par défaut. Votre application devra répondre de manière appropriée.

## <a name="code-sample"></a>Exemple de code

| Nom de l’échantillon | Description | .NET |
|-------------|-------------|------|
| Localisation des applications | Microsoft Teams localisation de l’application à l’aide de bot et onglet. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


