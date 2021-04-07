---
title: Mise en forme de texte prise en charge dans les conversations
description: Décrit la prise en charge de la mise en forme du texte dans les conversations de bot
keywords: messagerie de conversations de bots
ms.date: 03/29/2018
ms.openlocfilehash: 3ef51a7f6e4e923d83ab746a2dfa1f22464efb93
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596265"
---
# <a name="formatting-bot-messages"></a>Mettre en forme les messages du bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Vous pouvez définir la propriété facultative pour contrôler le rendu du contenu du texte [`TextFormat`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) de votre message.

Microsoft Teams prend en charge les options de mise en forme suivantes :

| Valeur TextFormat | Description |
| --- | --- |
| plain | Le texte doit être traité comme du texte brut sans aucune mise en forme appliquée |
| Markdown | Le texte doit être traité comme une mise en forme Markdown et restituer sur le canal comme il convient . voir [Mise en forme du contenu de texte pour](#formatting-text-content) les styles pris en charge |
| xml | Le texte est un simple markup XML ; voir [Mise en forme du contenu de texte pour](#formatting-text-content) les styles pris en charge |

## <a name="formatting-text-content"></a>Mise en forme du contenu de texte

Microsoft Teams prend en charge un sous-ensemble de balises de mise en forme Markdown et XML (HTML).

Actuellement, les limitations suivantes s’appliquent :

* Les messages texte uniquement ne sont pas en charge la mise en forme de tableau

Pour plus d’informations sur la mise en forme dans les cartes, voir la référence [de carte Teams.](~/task-modules-and-cards/cards/cards-reference.md)

### <a name="cross-platform-support"></a>Prise en charge sur plusieurs plateformes

Pour vous assurer que votre mise en forme fonctionne sur toutes les plateformes pris en charge par Microsoft Teams, sachez que certains styles ne sont actuellement pas pris en charge sur toutes les plateformes.

| Style                     | Messages texte uniquement | Cartes (XML uniquement) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| en-tête (niveaux 1 &ndash; 3) | ✖                  | ✔                |
| strikethrough             | ✖                  | ✔                |
| règle horizontale           | ✖                  | ✖                |
| liste non réordée            | ✖                  | ✔                |
| liste ordered              | ✖                  | ✔                |
| texte préformaté         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| lien hypertexte                 | ✔                  | ✔                |
| lien vers l’image                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Prise en charge par plateforme individuelle

La prise en charge de la mise en forme du texte varie en fonction du type de message et de la plateforme.

#### <a name="text-only-messages"></a>Messages texte uniquement

| Style                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| en-tête (niveaux 1 &ndash; 3) | ✖       | ✖   | ✖       |
| strikethrough             | ✔       | ✔   | ✖       |
| règle horizontale           | ✖       | ✖   | ✖       |
| liste non réordée            | ✔       | ✖   | ✖       |
| liste ordered              | ✔       | ✖   | ✖       |
| texte préformaté         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| lien hypertexte                 | ✔       | ✔   | ✔       |
| lien vers l’image                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Exemples de mise en forme du texte

| Style | Exemple | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| en-tête (niveaux 1 &ndash; 3) | **Text** | `### Text` | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| liste non réordée | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| liste ordered | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| texte préformaté | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| lien vers l’image | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
