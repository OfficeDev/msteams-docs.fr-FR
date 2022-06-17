---
title: Format du message bot
description: Dans ce module, découvrez les détails de la mise en forme des messages de bot
ms.topic: reference
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 9121573dfa6f5c7a96f04ed16bcb0d41de0b5c34
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143332"
---
# <a name="message-formatting-for-bots"></a>Mise en forme des messages pour les bots

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
* Les cartes enrichies prennent uniquement en charge la mise en forme dans la propriété de texte, et non dans les propriétés de titres ou de sous-titres.
* Les cartes enrichies ne prennent pas en charge la mise en forme markdown ou table.

## <a name="cross-platform-support"></a>Prise en charge multiplateforme

Pour vous assurer que votre mise en forme fonctionne sur toutes les plateformes prises en charge par Microsoft Teams, n’oubliez pas que certains styles ne sont actuellement pas pris en charge sur toutes les plateformes.

| Style                     | Messages texte uniquement | Cartes enrichies (XML uniquement) |
| ---                       | :---: | :---: |
| bold                      | ✔️️ | ❌ |
| italic                    | ✔️ | ✔️ |
| en-tête (niveaux 1&ndash;3) | ❌ | ✔️ |
| Barré             | ❌ | ✔️ |
| règle horizontale           | ❌ | ❌ |
| liste non triée            | ❌ | ✔️ |
| liste ordonnée              | ❌ | ✔️ |
| texte préformaté         | ✔️ | ✔️ |
| blockquote                | ✔️ | ✔️ |
| lien hypertexte                 | ✔️ | ✔️ |
| lien d’image                | ✔️ | ❌ |

## <a name="support-by-individual-platform"></a>Prise en charge par une plateforme individuelle

La prise en charge de la mise en forme du texte varie en fonction du type de message et de la plateforme.

### <a name="text-only-messages"></a>Messages texte uniquement

| Style                     | Ordinateur de bureau | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔️ | ✔️ | ✔️ |
| italic                    | ✔️ | ✔️ | ✔️ |
| en-tête (niveaux 1&ndash;3) | ❌ | ❌ | ❌ |
| Barré             | ✔️ | ✔️ | ❌ |
| règle horizontale           | ❌ | ❌ | ❌ |
| liste non triée            | ✔️ | ❌ | ❌ |
| liste ordonnée              | ✔️ | ❌ | ❌ |
| texte préformaté         | ✔️ | ✔️ | ✔️ |
| blockquote                | ✔️ | ✔️ | ✔️ |
| lien hypertexte                 | ✔️ | ✔️ | ✔️ |
| lien d’image                | ✔️ | ✔️ | ✔️ |

### <a name="cards"></a>Cartes

Pour plus d’informations, consultez [Mise en forme des cartes](~/task-modules-and-cards/cards/cards-format.md) pour la prise en charge des cartes.
