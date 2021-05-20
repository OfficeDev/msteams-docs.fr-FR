---
title: Formatage de texte pris en charge dans les conversations
description: Décrit le support de mise en forme de texte dans les conversations bot
keywords: bots conversations messagerie
ms.topic: how-to
localization_priority: Normal
ms.date: 03/29/2018
ms.openlocfilehash: dfb91e18a2ad895ae5b48c905046a22449304fc6
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566746"
---
# <a name="formatting-bot-messages"></a>Mettre en forme les messages du bot

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

* Les messages texte uniquement ne supportent pas le formatage de table

Pour plus d’informations sur le formatage dans les cartes, [Teams référence de la carte](~/task-modules-and-cards/cards/cards-reference.md).

### <a name="cross-platform-support"></a>Support interplateforme

Pour vous assurer que votre formatage fonctionne sur toutes les plateformes prises en charge par Microsoft Teams, sachez que certains styles ne sont pas actuellement pris en charge sur toutes les plateformes.

| Style                     | Messages texte uniquement | Cartes (XML seulement) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| en-tête (niveaux 1 &ndash; 3) | ✖                  | ✔                |
| strikethrough             | ✖                  | ✔                |
| règle horizontale           | ✖                  | ✖                |
| liste non ordonnée            | ✖                  | ✔                |
| liste commandée              | ✖                  | ✔                |
| texte préformaté         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| lien hypertexte                 | ✔                  | ✔                |
| lien d’image                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Support par plateforme individuelle

La prise en charge du formatage texte varie selon le type de message et par plate-forme.

#### <a name="text-only-messages"></a>Messages texte uniquement

| Style                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| en-tête (niveaux 1 &ndash; 3) | ✖       | ✖   | ✖       |
| strikethrough             | ✔       | ✔   | ✖       |
| règle horizontale           | ✖       | ✖   | ✖       |
| liste non ordonnée            | ✔       | ✖   | ✖       |
| liste commandée              | ✔       | ✖   | ✖       |
| texte préformaté         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| lien hypertexte                 | ✔       | ✔   | ✔       |
| lien d’image                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Exemples de formatage de texte

| Style | Exemple | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| en-tête (niveaux 1 &ndash; 3) | **Text** | `### Text` | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| liste non ordonnée | <ul><li>text</li><li>text</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| liste commandée | <ol><li>text</li><li>text</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| texte préformaté | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| lien hypertexte | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| lien d’image | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
