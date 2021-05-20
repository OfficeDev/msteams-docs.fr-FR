---
title: Format de message bot
description: Décrit les détails de la mise en forme des messages bot
keywords: scénarios équipes canalise le message bot de conversation
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
# <a name="message-formatting-for-bots"></a>Formatage de messages pour les bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Vous pouvez définir la propriété [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) optionnelle pour contrôler la façon dont le contenu texte de votre message est rendu.

Microsoft Teams prend en charge les options de mise en forme suivantes :

| Valeur TextFormat | Description |
| --- | --- |
| plaine | Le texte doit être traité comme du texte brut sans que le formatage ne soit appliqué du tout. |
| Markdown | Le texte doit être traité comme le formatage Markdown et rendu sur le canal le cas échéant; voir [Formater le contenu du texte pour](#formatting-text-content) les styles pris en charge. |
| xml xml xml | Le texte est simple balisage XML; voir [Formater le contenu du texte pour](#formatting-text-content) les styles pris en charge. |

## <a name="formatting-text-content"></a>Formatage du contenu du texte

Microsoft Teams prend en charge un sous-ensemble de balises de formatage Markdown et XML (HTML).

À l’heure actuelle, les limitations suivantes s’appliquent :

* Les messages texte uniquement ne supportent pas le formatage de table.
* Les cartes riches soutiennent le formatage dans la propriété de texte seulement, pas dans les propriétés de titre ou de sous-titre.
* Les cartes riches ne supportent pas Markdown ou le formatage de table.

## <a name="cross-platform-support"></a>Support interplateforme

Pour vous assurer que votre formatage fonctionne sur toutes les plateformes prises en charge par Microsoft Teams, sachez que certains styles ne sont pas actuellement pris en charge sur toutes les plateformes.

| Style                     | Messages texte uniquement | Cartes riches (XML seulement) |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| en-tête (niveaux 1 &ndash; 3) | ✖ | ✔ |
| strikethrough             | ✖ | ✔ |
| règle horizontale           | ✖ | ✖ |
| liste non ordonnée            | ✖ | ✔ |
| liste commandée              | ✖ | ✔ |
| texte préformaté         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| lien hypertexte                 | ✔ | ✔ |
| lien d’image                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>Support par plateforme individuelle

La prise en charge du formatage texte varie selon le type de message et par plate-forme.

### <a name="text-only-messages"></a>Messages texte uniquement

| Style                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| en-tête (niveaux 1 &ndash; 3) | ✖ | ✖ | ✖ |
| strikethrough             | ✔ | ✔ | ✖ |
| règle horizontale           | ✖ | ✖ | ✖ |
| liste non ordonnée            | ✔ | ✖ | ✖ |
| liste commandée              | ✔ | ✖ | ✖ |
| texte préformaté         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| lien hypertexte                 | ✔ | ✔ | ✔ |
| lien d’image                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Cartes

Pour plus d’informations, consultez [le formatage des cartes pour](~/task-modules-and-cards/cards/cards-format.md) le support dans les cartes.
