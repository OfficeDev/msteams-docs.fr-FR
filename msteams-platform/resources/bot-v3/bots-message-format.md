---
title: Format de message du bot
description: Décrit les détails de la mise en forme des messages du bot
keywords: teams scenarios channels conversation bot message
ms.topic: reference
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: a9566331b259ba77f6770ff6394e8a788769af5d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566473"
---
# <a name="message-formatting-for-bots"></a>Mise en forme des messages pour les bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Vous pouvez définir la propriété facultative pour contrôler le rendu du contenu du [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) texte de votre message.

Microsoft Teams prend en charge les options de mise en forme suivantes :

| Valeur TextFormat | Description |
| --- | --- |
| plain | Le texte doit être traité comme du texte brut sans aucune mise en forme appliquée. |
| Markdown | Le texte doit être traité comme une mise en forme Markdown et restituer sur le canal selon le cas . voir [Mise en forme du contenu de texte](#formatting-text-content) pour les styles pris en charge. |
| xml | Le texte est un simple markup XML ; voir [Mise en forme du contenu de texte](#formatting-text-content) pour les styles pris en charge. |

## <a name="formatting-text-content"></a>Mise en forme du contenu de texte

Microsoft Teams prend en charge un sous-ensemble de balises de mise en forme Markdown et XML (HTML).

Actuellement, les limitations suivantes s’appliquent :

* Les messages texte uniquement ne sont pas en charge de la mise en forme des tableaux.
* Les cartes enrichies ne peuvent être formatées que dans la propriété de texte, et non dans les propriétés de titre ou de sous-titre.
* Les cartes enrichies ne prisent pas en charge la mise en forme Markdown ou table.

## <a name="cross-platform-support"></a>Prise en charge sur plusieurs plateformes

Pour vous assurer que votre mise en forme fonctionne sur toutes les plateformes Microsoft Teams, sachez que certains styles ne sont actuellement pas pris en charge sur toutes les plateformes.

| Style                     | Messages texte uniquement | Cartes enrichies (XML uniquement) |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| en-tête (niveaux 1 &ndash; 3) | ✖ | ✔ |
| strikethrough             | ✖ | ✔ |
| règle horizontale           | ✖ | ✖ |
| liste non réordée            | ✖ | ✔ |
| liste ordered              | ✖ | ✔ |
| texte préformaté         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| lien hypertexte                 | ✔ | ✔ |
| lien vers l’image                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>Prise en charge par plateforme individuelle

La prise en charge de la mise en forme du texte varie en fonction du type de message et de la plateforme.

### <a name="text-only-messages"></a>Messages texte uniquement

| Style                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| en-tête (niveaux 1 &ndash; 3) | ✖ | ✖ | ✖ |
| strikethrough             | ✔ | ✔ | ✖ |
| règle horizontale           | ✖ | ✖ | ✖ |
| liste non réordée            | ✔ | ✖ | ✖ |
| liste ordered              | ✔ | ✖ | ✖ |
| texte préformaté         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| lien hypertexte                 | ✔ | ✔ | ✔ |
| lien vers l’image                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Cartes

Pour plus d’informations, [voir Formatage de carte](~/task-modules-and-cards/cards/cards-format.md) pour la prise en charge dans les cartes.
