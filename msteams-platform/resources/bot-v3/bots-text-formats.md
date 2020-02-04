---
title: Mise en forme de texte prise en charge dans les conversations
description: Décrit la prise en charge de la mise en forme du texte dans les conversations de bot
keywords: messagerie conversations des robots
ms.date: 03/29/2018
ms.openlocfilehash: cc6cba697a1f6907bfb13b94740e7bf9e92596da
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673569"
---
# <a name="formatting-bot-messages"></a>Mise en forme des messages du bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Vous pouvez définir la propriété [`TextFormat`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) Optional pour contrôler le rendu du contenu de texte de votre message.

Microsoft teams prend en charge les options de mise en forme suivantes :

| Valeur FormatTexte | Description |
| --- | --- |
| puce | Le texte doit être traité comme du texte brut sans mise en forme appliquée |
| Markdown | Le texte doit être traité comme un format de démarque et affiché sur le canal, selon le cas ; Voir [mise en forme du contenu de texte](#formatting-text-content) pour les styles pris en charge |
| langage | Le texte est un balisage XML simple ; Voir [mise en forme du contenu de texte](#formatting-text-content) pour les styles pris en charge |

## <a name="formatting-text-content"></a>Mise en forme du contenu de texte

Microsoft teams prend en charge un sous-ensemble de balises de mise en forme de démarque et XML (HTML).

Actuellement, les limitations suivantes s’appliquent :

* Les messages en texte seul ne prennent pas en charge la mise en forme de tableau

Pour plus d’informations sur la mise en forme dans les cartes, voir la [référence des cartes teams](~/task-modules-and-cards/cards/cards-reference.md).

### <a name="cross-platform-support"></a>Prise en charge multiplateforme

Pour vous assurer que votre mise en forme fonctionne sur toutes les plateformes prises en charge par Microsoft Teams, sachez que certains styles ne sont actuellement pas pris en charge sur toutes les plateformes.

| Style                     | Messages en texte seul | Cartes (XML uniquement) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| en-tête (&ndash;niveaux 1 à 3) | ✖                  | ✔                |
| doubles             | ✖                  | ✔                |
| règle horizontale           | ✖                  | ✖                |
| liste non triée            | ✖                  | ✔                |
| liste triée              | ✖                  | ✔                |
| texte déjà mis en forme         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| lien hypertexte                 | ✔                  | ✔                |
| lien de l’image                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Prise en charge par plateforme individuelle

La prise en charge de la mise en forme du texte varie en fonction du type de message et de la plateforme.

#### <a name="text-only-messages"></a>Messages en texte seul

| Style                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| en-tête (&ndash;niveaux 1 à 3) | ✖       | ✖   | ✖       |
| doubles             | ✔       | ✔   | ✖       |
| règle horizontale           | ✖       | ✖   | ✖       |
| liste non triée            | ✔       | ✖   | ✖       |
| liste triée              | ✔       | ✖   | ✖       |
| texte déjà mis en forme         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| lien hypertexte                 | ✔       | ✔   | ✔       |
| lien de l’image                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Exemples de mise en forme de texte

| Style | Exemple | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| en-tête (&ndash;niveaux 1 à 3) | **Text** | `### Text` | `<h3>Text</h3>` |
| doubles | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| liste non triée | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| liste triée | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| texte déjà mis en forme | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| lien de l’image | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
