---
title: Localisation des applications d’équipe
description: Décrit les problèmes liés à la localisation de votre application
keywords: teams publier le magasin Office publication AppSource langue de localisation
ms.date: 05/15/2018
ms.openlocfilehash: 8d14da5c773bcc422081b50fc530a32163260b4a
ms.sourcegitcommit: 81ac2a1070d16e20ae0e4cb6137dce09b31914af
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/16/2020
ms.locfileid: "45152678"
---
# <a name="localization-for-microsoft-teams-apps"></a>Localisation pour les applications Microsoft teams

Lors de la localisation de votre application Microsoft Teams, vous devez prendre en compte trois éléments principaux.

1. Votre AppSource Listing (si vous effectuez une publication sur le magasin d’applications).
1. L’utilisateur final a accès à des chaînes dans votre manifeste de l’application (par exemple, commandes de bot).
1. Réponse au texte localisé envoyé par vos utilisateurs.

## <a name="localizing-your-appsource-listing"></a>Localisation de votre liste AppSource

Si vous effectuez une publication sur App Store, vous devez savoir que la localisation de votre liste AppSource n’est pas encore prise en charge. Toutefois, en vue de la prise en charge des listes localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre annonce. Actuellement, seules les informations de langue par défaut (anglais) que vous fournissez dans le [Centre des partenaires](/office/dev/store/submit-to-appsource-via-partner-center) pour votre liste apparaîtront dans la liste de [sites Web AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) de votre application.

Pour configurer une langue supplémentaire pour votre application, dans le [Centre de partenaires](/office/dev/store/submit-to-appsource-via-partner-center), sélectionnez anglais et la langue supplémentaire de l’application. Le français est utilisé dans cet exemple.

1. Ajouter une langue anglaise
    * Renseignez le nom de l’application.
    * Entrez une brève description de l’application en anglais.
    * Renseignez la description longue de l’application en anglais.
    * Dans la description longue, ajoutez également la ligne « cette application est disponible en français ».
    * Téléchargez les images de l’interface utilisateur de votre application (en anglais).
2. Ajouter la langue française
    * Renseignez le nom de l’application.
    * Entrez une brève description de l’application en français.
    * Renseignez la description longue de l’application en français.
    * Téléchargez les images de l’interface utilisateur de votre application (en français).

Les images que vous chargez avec la langue anglaise seront celles utilisées dans AppSource.

## <a name="localizing-the-strings-in-your-app-manifest"></a>Localisation des chaînes dans le manifeste de votre application

Vous devez utiliser le schéma d’application Microsoft teams v 1.5 + pour localiser correctement votre application. Pour ce faire, définissez l' `$schema` attribut de votre manifest.jssur' https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json 'et mettez à jour la propriété’manifestVersion’sur' 1,7 '.

### <a name="example-manifestjson-change"></a>Exemple manifest.jsen modification

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

Vous pouvez ensuite ajouter la propriété « localizationInfo » avec la langue par défaut prise en charge par votre application. La langue par défaut est utilisée comme langue de secours finale si les paramètres du client de l’utilisateur ne correspondent à aucune de vos langues supplémentaires.

### <a name="example-manifestjson-change"></a>Exemple manifest.jsen modification

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

Vous pouvez fournir des fichiers. JSON supplémentaires avec des traductions de toutes les chaînes accessibles par l’utilisateur dans votre manifeste. Ces fichiers doivent adhérer au [schéma JSON fichier de localisation](../../resources/schema/localization-schema.md) et ils doivent être ajoutés à la propriété « localizationInfo » de votre manifeste. Chaque fichier correspond à une balise de langue que le client teams utilise pour choisir les chaînes appropriées. La balise de langue prend la forme <language> - <region> , mais il est recommandé d’omettre la <region> partie pour cibler toutes les régions qui prennent en charge la langue souhaitée.

Le client teams applique les chaînes dans l’ordre suivant : chaînes de langue par défaut-> langue de l’utilisateur uniquement chaînes-> langue de l’utilisateur + chaînes de région de l’utilisateur.

Par exemple, vous fournissez une langue par défaut de « fr » (français, toutes les régions) et des fichiers de langue supplémentaires pour « en » (anglais, toutes les régions) et « en-GB » (anglais, Grande-Bretagne). Si la langue de l’utilisateur est définie sur « en-GB » :

1. Le client teams prendra les chaînes « fr » les remplacer par les chaînes « en ».
2. Remplacez ceux-ci par les chaînes « en-GB ».

Si la langue de l’utilisateur est définie sur « en-ca » : 

1. Le client teams prendra les chaînes « fr » les remplacer par les chaînes « en ».
2. Étant donné qu’aucune localisation « en-ca » n’est fournie, les localisations « en » seront utilisées.

Si la langue de l’utilisateur est définie sur « es-es », le client teams prend les chaînes « fr » et ne les remplace pas par l’un des fichiers de langue.

Par conséquent, il est vivement recommandé de fournir des traductions de niveau supérieur, de langue uniquement dans votre manifeste (« en » au lieu de « en-US ») et de fournir uniquement des substitutions au niveau de la région pour les quelques chaînes qui en ont besoin.

### <a name="example-manifestjson-change"></a>Exemple manifest.jsen modification

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

### <a name="example-localization-json-file"></a>Exemple de fichier Localization. JSON

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a>Gestion des envois de texte localisés provenant de vos utilisateurs

Si vous fournissez des versions localisées de votre application, il est fort probable que vos utilisateurs y répondront dans la même langue. Teams ne reconvertit pas les soumissions de l’utilisateur vers la langue par défaut, de sorte que votre application doit gérer cela. Par exemple, si vous fournissez une localisation `commandList` , les réponses à votre bot seront le texte localisé de la commande, pas la langue par défaut. Votre application doit répondre de manière appropriée.
