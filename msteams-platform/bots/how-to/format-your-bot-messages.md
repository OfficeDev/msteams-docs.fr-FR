---
title: Formatez vos messages robots.
author: clearab
description: Ajouter une mise en forme enrichie à vos messages de bot
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 7dc082f4b17e123c9fa000552f02fc913c66dcf7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020904"
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

* Les messages texte uniquement ne sont pas en charge de la mise en forme de tableau.
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
| Hyperlink                 | ✔ | ✔ |
| Lien vers l’image                | ✔ | ✖ |

Après avoir vérifié la prise en charge sur plusieurs plateformes, assurez-vous que la prise en charge par des plateformes individuelles est également disponible.

## <a name="support-by-individual-platform"></a>Prise en charge par plateforme individuelle

La prise en charge de la mise en forme du texte varie selon le type de message et la plateforme.

### <a name="text-only-messages"></a>Messages texte uniquement

Le tableau suivant fournit une liste des styles et ceux qui sont pris en charge sur les ordinateurs de bureau, iOS et Android :

| Style                     | Desktop | iOS | Android |
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
| Hyperlink                 | ✔ | ✔ | ✔ |
| Lien vers l’image                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Cartes

Pour la prise en charge de la carte, voir [mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Mettre à jour et supprimer des messages de bot](~/bots/how-to/update-and-delete-bot-messages.md)
