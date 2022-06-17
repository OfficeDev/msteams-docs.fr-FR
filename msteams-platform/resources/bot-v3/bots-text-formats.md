---
title: Mise en forme de texte prise en charge dans les conversations
description: Dans ce module, découvrez la prise en charge de la mise en forme de texte dans les conversations de bot et la mise en forme du contenu texte dans Microsoft Teams
ms.topic: how-to
ms.localizationpriority: medium
ms.date: 03/29/2018
ms.openlocfilehash: 2bec542b678f371e20317d1ea7d11b4e97f52338
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142331"
---
# <a name="formatting-bot-messages"></a>Mettre en forme les messages du bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Vous pouvez définir la propriété [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) facultative pour contrôler le rendu du contenu texte de votre message.

Microsoft Teams prend en charge les options de mise en forme suivantes :

| Valeur TextFormat | Description |
| --- | --- |
| plaine | Le texte doit être traité comme du texte brut sans aucune mise en forme appliquée du tout. |
| Markdown | Le texte doit être traité comme une mise en forme Markdown et affiché sur le canal comme il convient; consultez [Mise en forme du contenu du texte](#formatting-text-content) pour les styles pris en charge. |
| xml | Le texte est un balisage XML simple ; consultez [Mise en forme du contenu du texte](#formatting-text-content) pour les styles pris en charge. |

## <a name="formatting-text-content"></a>Mise en forme du contenu du texte

Microsoft Teams prend en charge un sous-ensemble de balises de mise en forme Markdown et XML (HTML).

Actuellement, les limitations suivantes s’appliquent :
* Les messages texte uniquement ne prennent pas en charge la mise en forme des tables.

Pour plus d’informations sur la mise en forme dans les cartes, consultez [Teams Référence de carte](~/task-modules-and-cards/cards/cards-reference.md).

### <a name="cross-platform-support"></a>Prise en charge multiplateforme

Pour vous assurer que votre mise en forme fonctionne sur toutes les plateformes prises en charge par Microsoft Teams, n’oubliez pas que certains styles ne sont actuellement pas pris en charge sur toutes les plateformes.

| Style                     | Messages texte uniquement | Cartes (XML uniquement) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| en-tête (niveaux 1&ndash;3) | ✖                  | ✔                |
| Barré             | ✖                  | ✔                |
| règle horizontale           | ✖                  | ✖                |
| liste non triée            | ✖                  | ✔                |
| liste ordonnée              | ✖                  | ✔                |
| texte préformaté         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| lien hypertexte                 | ✔                  | ✔                |
| lien d’image                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Prise en charge par une plateforme individuelle

La prise en charge de la mise en forme du texte varie en fonction du type de message et de la plateforme.

#### <a name="text-only-messages"></a>Messages texte uniquement

| Style                     | Ordinateur de bureau | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| en-tête (niveaux 1&ndash;3) | ✖       | ✖   | ✖       |
| Barré             | ✔       | ✔   | ✖       |
| règle horizontale           | ✖       | ✖   | ✖       |
| liste non triée            | ✔       | ✖   | ✖       |
| liste ordonnée              | ✔       | ✖   | ✖       |
| texte préformaté         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| lien hypertexte                 | ✔       | ✔   | ✔       |
| lien d’image                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Exemples de mise en forme de texte

| Style | Exemple | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| en-tête (niveaux 1&ndash;3) | **Text** | `### Text` | `<h3>Text</h3>` |
| Barré | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| liste non triée | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| liste ordonnée | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| texte préformaté | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| lien d’image | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
