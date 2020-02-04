---
title: Format du message bot
description: Décrit les détails de la mise en forme des messages bot
keywords: scénarios de teams canaux de conversation de canaux de conversation
ms.date: 05/20/2019
ms.openlocfilehash: eb0d0303d2b414ff84beab73055be5f057fff11c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674020"
---
# <a name="message-formatting-for-bots"></a>Mise en forme des messages pour les robots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Vous pouvez définir la propriété [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) Optional pour contrôler le rendu du contenu de texte de votre message.

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
* Les cartes enrichies prennent en charge la mise en forme uniquement dans la propriété Text, pas dans les propriétés Title ou title.
* Les cartes enrichies ne prennent pas en charge la démarque ou la mise en forme de tableau

## <a name="cross-platform-support"></a>Prise en charge multiplateforme

Pour vous assurer que votre mise en forme fonctionne sur toutes les plateformes prises en charge par Microsoft Teams, sachez que certains styles ne sont actuellement pas pris en charge sur toutes les plateformes.

| Style                     | Messages en texte seul | Cartes riches (XML uniquement) |
| ---                       | :---: | :---: |
| bold                      | ✔ | ✖ |
| italic                    | ✔ | ✔ |
| en-tête (&ndash;niveaux 1 à 3) | ✖ | ✔ |
| doubles             | ✖ | ✔ |
| règle horizontale           | ✖ | ✖ |
| liste non triée            | ✖ | ✔ |
| liste triée              | ✖ | ✔ |
| texte déjà mis en forme         | ✔ | ✔ |
| blockquote                | ✔ | ✔ |
| lien hypertexte                 | ✔ | ✔ |
| lien de l’image                | ✔ | ✖ |

## <a name="support-by-individual-platform"></a>Prise en charge par plateforme individuelle

La prise en charge de la mise en forme du texte varie en fonction du type de message et de la plateforme.

### <a name="text-only-messages"></a>Messages en texte seul

| Style                     | Desktop | iOS | Android |
| ---                       | :---: | :---: | :---: |
| bold                      | ✔ | ✔ | ✔ |
| italic                    | ✔ | ✔ | ✔ |
| en-tête (&ndash;niveaux 1 à 3) | ✖ | ✖ | ✖ |
| doubles             | ✔ | ✔ | ✖ |
| règle horizontale           | ✖ | ✖ | ✖ |
| liste non triée            | ✔ | ✖ | ✖ |
| liste triée              | ✔ | ✖ | ✖ |
| texte déjà mis en forme         | ✔ | ✔ | ✔ |
| blockquote                | ✔ | ✔ | ✔ |
| lien hypertexte                 | ✔ | ✔ | ✔ |
| lien de l’image                | ✔ | ✔ | ✔ |

### <a name="cards"></a>Fiche

Pour plus d’aide, voir [format](~/task-modules-and-cards/cards/cards-format.md) des cartes.
