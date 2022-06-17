---
title: Formatez vos messages robots.
author: surbhigupta
description: Dans ce module, découvrez comment ajouter une mise en forme enrichie à vos messages de bot, comme la barre d’accès, la liste ordonnée et non triée, le lien hypertexte, le lien image, etc.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 3bb58062a449d9122940064416cc621fc65603d1
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143479"
---
# <a name="format-your-bot-messages"></a>Formatez vos messages robots.

La mise en forme des messages vous permet de tirer le meilleur parti des messages du bot. Vous pouvez mettre en forme vos messages de bot pour inclure des cartes enrichies qui sont des pièces jointes qui contenant des éléments interactifs, tels que des boutons, du texte, des images, de l’audio, de la vidéo, etc.

## <a name="format-text-content"></a>Mettre en forme le contenu de texte

Pour mettre en forme vos messages de bot, vous pouvez définir la propriété facultative [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) pour contrôler le rendu du contenu texte de votre message de bot.

Microsoft Teams prend en charge les options de mise en forme suivantes :

| Valeur `TextFormat` | Description |
| --- | --- |
| plaine | Le texte doit être traité comme un texte brut sans aucune mise en forme appliquée.|
| Markdown | Le texte doit être traité comme une mise en forme Markdown et rendu sur le canal le cas échéant. |
| xml | Le texte est un balise XML simple. |

Teams prend en charge un sous-ensemble de balises de mise en forme XML ou HTML et Markdown.

Actuellement, les limitations suivantes s’appliquent à la mise en forme :

* Les messages texte uniquement ne prennent pas en charge la mise en forme des tables.
* Les cartes enrichies prennent uniquement en charge la mise en forme dans la propriété de texte, et non dans les propriétés de titres ou de sous-titres.
* Les cartes enrichies ne prennent pas en charge la mise en forme de tables ou Markdown.

Une fois votre contenu texte mis en forme, vérifiez que votre mise en forme fonctionne sur toutes les plateformes prises en charge par Microsoft Teams.

## <a name="cross-platform-support"></a>Prise en charge multiplateforme

Certains styles ne sont actuellement pas pris en charge sur toutes les plateformes. Le tableau suivant fournit la liste des styles, ainsi que ceux pris en charge dans les messages texte uniquement et les cartes enrichies :

| Style                     | Messages texte uniquement | Cartes enrichies : XML uniquement |
| ---                       | :---: | :---: |
| Gras                      | ✔️️ | ❌ |
| Italic                    | ✔️ | ✔️ |
| En-tête (niveaux 1&ndash;3) | ❌ | ✔️ |
| Barré             | ❌ | ✔️ |
| Règle horizontale           | ❌ | ❌ |
| Liste non triée            | ❌ | ✔️ |
| Liste triée              | ❌ | ✔️ |
| Texte préformaté         | ✔️ | ✔️ |
| Blockquote                | ✔️ | ✔️ |
| Hyperlink                 | ✔️ | ✔️ |
| Lien d’image                | ✔️ | ❌ |

Une fois la prise en charge multiplateforme effectuée, vérifiez que la prise en charge par des plateformes individuelles est également disponible.

## <a name="support-by-individual-platform"></a>Prise en charge par une plateforme individuelle

La prise en charge de la mise en forme de texte varie selon le type de message et la plateforme.

### <a name="text-only-messages"></a>Messages texte uniquement

Le tableau suivant fournit la liste des styles pris en charge sur des ordinateurs de bureau, iOS et Android :

| Style                     | Ordinateur de bureau | iOS | Android |
| ---                       | :---: | :---: | :---: |
| Gras                      | ✔️ | ✔️ | ✔️ |
| Italic                    | ✔️ | ✔️ | ✔️ |
| En-tête (niveaux 1&ndash;3) | ❌ | ❌ | ❌ |
| Barré             | ✔️ | ✔️ | ❌ |
| Règle horizontale           | ❌ | ❌ | ❌ |
| Liste non triée            | ✔️ | ❌ | ❌ |
| Liste triée              | ✔️ | ❌ | ❌ |
| Texte préformaté         | ✔️ | ✔️ | ✔️ |
| Blockquote                | ✔️ | ✔️ | ✔️ |
| Hyperlink                 | ✔️ | ✔️ | ✔️ |
| Lien d’image                | ✔️ | ✔️ | ✔️ |

### <a name="cards"></a>Cartes

Pour la prise en charge des cartes, voir la [mise en forme de cartes](~/task-modules-and-cards/cards/cards-format.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Mettre à jour et supprimer des messages de bot](~/bots/how-to/update-and-delete-bot-messages.md)
