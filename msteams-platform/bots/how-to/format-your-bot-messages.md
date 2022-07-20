---
title: Formatez vos messages robots.
author: surbhigupta
description: Dans ce module, découvrez comment ajouter une mise en forme et des styles enrichis à vos messages de bot, tels que la barre d’accès, la liste ordonnée et non triée, le lien hypertexte, le lien d’image, etc.
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 43a64a5ab7d44058831b643f2516839c248e9af1
ms.sourcegitcommit: 904cca011c3f27d1d90ddd80c3d0300a8918e412
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/20/2022
ms.locfileid: "66895481"
---
# <a name="format-your-bot-messages"></a>Formatez vos messages robots.

La mise en forme des messages vous permet de tirer le meilleur parti des messages du bot. Vous pouvez mettre en forme vos messages de bot pour inclure des cartes enrichies sous forme de pièces jointes qui contiennent des éléments interactifs, tels que des boutons, du texte, des images, de l’audio, de la vidéo, etc.

> [!NOTE]
> La limite de taille des messages du bot est de 40 Ko. Si la limite de taille du message du bot dépasse 40 Ko, le bot reçoit un code d’état `413` (RequestEntityTooLarge), qui contient le code `MessageSizeTooBig`d’erreur. La limite de taille des messages du bot inclut la charge utile de message entière encodée en UTF-16 et n’inclut pas les images encodées en base 64.

## <a name="format-text-content"></a>Mettre en forme le contenu de texte

Pour mettre en forme vos messages de bot, vous pouvez définir la propriété facultative [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) pour contrôler le rendu du contenu texte de votre message de bot.

Microsoft Teams prend en charge les options de mise en forme suivantes :

| Valeur `TextFormat` | Description |
| --- | --- |
| plaine | Le texte doit être traité comme un texte brut sans aucune mise en forme appliquée.|
| Markdown | Le texte doit être traité comme une mise en forme Markdown et rendu sur le canal le cas échéant. |
| xml | Le texte est un balise XML simple. |

Teams prend en charge un sous-ensemble de balises de mise en forme XML ou HTML et Markdown.

Actuellement, les limitations suivantes s’appliquent à la mise en forme :

* Les messages texte uniquement ne prennent pas en charge la mise en forme des tables.
* Les cartes enrichies prennent uniquement en charge la mise en forme dans la propriété de texte, et non dans les propriétés de titres ou de sous-titres.
* Les cartes enrichies ne prennent pas en charge la mise en forme markdown ou table.

Après avoir mis en forme du contenu texte, assurez-vous que votre mise en forme fonctionne sur toutes les plateformes prises en charge par Teams.

## <a name="cross-platform-support"></a>Prise en charge multiplateforme

Certains styles ne sont actuellement pas pris en charge sur toutes les plateformes. Le tableau suivant fournit la liste des styles, ainsi que ceux pris en charge dans les messages texte uniquement et les cartes enrichies :

| Style                     | Messages texte uniquement | Cartes enrichies : XML uniquement |
| ---                       | :---: | :---: |
| Gras                      | ✔️️ | ❌ |
| Italic                    | ✔️ | ✔️ |
| En-tête (niveaux 1&ndash;3) | ❌ | ✔️ |
| Barré             | ❌ | ✔️ |
| Règle horizontale           | ❌ | ❌ |
| Liste non triée            | ❌ | ✔️ |
| Liste triée              | ❌ | ✔️ |
| Texte préformaté         | ✔️ | ✔️ |
| Blockquote                | ✔️ | ✔️ |
| Lien hypertexte                 | ✔️ | ✔️ |
| Lien d’image                | ❌ | ❌ |

Une fois la prise en charge multiplateforme effectuée, vérifiez que la prise en charge par des plateformes individuelles est également disponible.

## <a name="support-by-individual-platform"></a>Prise en charge par une plateforme individuelle

La prise en charge de la mise en forme de texte varie selon le type de message et la plateforme.

### <a name="text-only-messages"></a>Messages texte uniquement

Le tableau suivant fournit la liste des styles pris en charge sur des ordinateurs de bureau, iOS et Android :

| Style                     | Ordinateur de bureau | iOS | Android |
| ---                       | :---: | :---: | :---: |
| Gras                      | ✔️ | ✔️ | ✔️ |
| Italic                    | ✔️ | ✔️ | ✔️ |
| En-tête (niveaux 1&ndash;3) | ❌ | ❌ | ❌ |
| Barré             | ✔️ | ✔️ | ❌ |
| Règle horizontale           | ❌ | ❌ | ❌ |
| Liste non triée            | ✔️ | ❌ | ❌ |
| Liste triée              | ✔️ | ❌ | ❌ |
| Texte préformaté         | ✔️ | ✔️ | ✔️ |
| Blockquote                | ✔️ | ✔️ | ✔️ |
| Lien hypertexte                 | ✔️ | ✔️ | ✔️ |
| Lien d’image                | ❌ | ❌ | ❌ |

### <a name="cards"></a>Cartes

Pour la prise en charge des cartes, voir la [mise en forme de cartes](~/task-modules-and-cards/cards/cards-format.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Mettre à jour et supprimer des messages de bot](~/bots/how-to/update-and-delete-bot-messages.md)
