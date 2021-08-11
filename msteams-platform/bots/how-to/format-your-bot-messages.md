---
title: Formatez vos messages robots.
author: surbhigupta
description: Ajouter une mise en forme enrichie à vos messages de bot
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: fba55b6b08785d375f80923133d3af70434cbaf57adf8feaf4e9f50f478f5e61
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705600"
---
# <a name="format-your-bot-messages"></a>Formatez vos messages robots.

La mise en forme des messages vous permet de mettre en avant les meilleurs messages du bot. Vous pouvez mettre en forme vos messages de bot pour inclure des cartes enrichies qui sont des pièces jointes qui contiennent des éléments interactifs, tels que des boutons, du texte, des images, de l’audio, de la vidéo, etc.

## <a name="format-text-content"></a>Mise en forme du contenu de texte

Pour mettre en forme vos messages de bot, vous pouvez définir la propriété facultative pour contrôler le rendu du contenu texte de votre [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) message bot.

Microsoft Teams prend en charge les options de mise en forme suivantes :

| `TextFormat` value | Description |
| --- | --- |
| plain | Le texte doit être traité comme du texte brut sans mise en forme appliquée.|
| Markdown | Le texte doit être traité comme une mise en forme markdown et restituer sur le canal selon le cas. |
| xml | Le texte est un simple markup XML. |

Teams prend en charge un sous-ensemble de balises de mise en forme XML ou HTML et markdown.

Actuellement, les limitations suivantes s’appliquent à la mise en forme :

* Les messages texte uniquement ne sont pas en charge de la mise en forme des tableaux.
* Les cartes enrichies ne peuvent être formatées que dans la propriété de texte, et non dans les propriétés de titre ou de sous-titre.
* Les cartes enrichies ne prisent pas en charge le markdown ou la mise en forme de tableau.

Après avoir formaté le contenu du texte, assurez-vous que votre mise en forme fonctionne sur toutes les plateformes Microsoft Teams.

## <a name="cross-platform-support"></a>Prise en charge sur plusieurs plateformes

Certains styles ne sont actuellement pas pris en charge sur toutes les plateformes. Le tableau suivant fournit une liste des styles et ceux qui sont pris en charge dans les messages texte uniquement et les cartes enrichies :

| Style                     | Messages texte uniquement | Cartes enrichies - XML uniquement |
| ---                       | :---: | :---: |
| Gras                      | ✔ | ✖ |
| Italic                    | ✔ | ✔ |
| En-tête (niveaux 1 &ndash; 3) | ✖ | ✔ |
| Barré             | ✖ | ✔ |
| Règle horizontale           | ✖ | ✖ |
| Liste non triée            | ✖ | ✔ |
| Liste triée              | ✖ | ✔ |
| Texte préformaté         | ✔ | ✔ |
| Blockquote                | ✔ | ✔ |
| Lien hypertexte                 | ✔ | ✔ |
| Lien vers l’image                | ✔ | ✖ |

Après avoir vérifié la prise en charge sur plusieurs plateformes, assurez-vous que la prise en charge par des plateformes individuelles est également disponible.

## <a name="support-by-individual-platform"></a>Prise en charge par plateforme individuelle

La prise en charge de la mise en forme du texte varie selon le type de message et la plateforme.

### <a name="text-only-messages"></a>Messages texte uniquement

Le tableau suivant fournit une liste des styles et ceux qui sont pris en charge sur ordinateur de bureau, iOS et Android :

| Style                     | Bureau | iOS | Android |
| ---                       | :---: | :---: | :---: |
| Gras                      | ✔ | ✔ | ✔ |
| Italic                    | ✔ | ✔ | ✔ |
| En-tête (niveaux 1 &ndash; 3) | ✖ | ✖ | ✖ |
| Barré             | ✔ | ✔ | ✖ |
| Règle horizontale           | ✖ | ✖ | ✖ |
| Liste non triée            | ✔ | ✖ | ✖ |
| Liste triée              | ✔ | ✖ | ✖ |
| Texte préformaté         | ✔ | ✔ | ✔ |
| Blockquote                | ✔ | ✔ | ✔ |
| Lien hypertexte                 | ✔ | ✔ | ✔ |
| Lien vers l’image                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Cartes

Pour la prise en charge de la carte, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Mettre à jour et supprimer des messages de bot](~/bots/how-to/update-and-delete-bot-messages.md)
