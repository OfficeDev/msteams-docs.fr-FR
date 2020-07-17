---
title: Instructions de conception pour les extensions de messagerie
description: Décrit les instructions pour la création d’extensions de messagerie
keywords: recommandations pour la conception des équipes de référence des extensions de messagerie conseils
author: EmilyyC
ms.author: qinch
ms.openlocfilehash: 5d62646c5757f93cc4f6ae6e089ef3a0918f9eea
ms.sourcegitcommit: 81ac2a1070d16e20ae0e4cb6137dce09b31914af
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/16/2020
ms.locfileid: "45152685"
---
# <a name="start-sharing-with-powerful-messaging-extensions"></a>Démarrer le partage avec des extensions de messagerie puissantes

Les extensions de messagerie sont conçues pour partager du contenu actionnable. Cette fonctionnalité représente le retour sur investissement le plus élevé dans notre pile. Les extensions de messagerie fonctionnent dans les conversations et les canaux, prennent en charge plusieurs points de terminaison de requête, permettent la création de nouvelles entités et travaillent avec Link unfurling pour créer des aperçus de liens personnalisés. Le défi est que si la fonctionnalité est puissante et incroyablement utile, elle ne peut pas être facilement découvrable. Ce guide vous aidera à créer des extensions de messagerie facilement accessibles et exploitées par d’autres utilisateurs.

## <a name="design-guidelines"></a>Instructions de conception

### <a name="show-content-as-a-user-type"></a>Afficher le contenu en tant que type d’utilisateur

Les extensions de messagerie présentent un moyen unique d’utiliser des recherches par Mots clés pour rechercher du contenu actionnable pouvant être partagé avec un ou plusieurs utilisateurs. Cette interaction privilégiée permet aux utilisateurs d’entrer des termes de recherche avec une requête automatique différée comme type d’utilisateur. Ce modèle permet de simuler des résultats suggérés et d’obliger les utilisateurs à taper des caractères minimum.

> [!TIP]
>Il est possible, mais pas souhaitable, d’obliger les utilisateurs à sélectionner `enter` ou `search` avant d’envoyer des requêtes. Bien qu’il y ait moins de contraintes sur le service principal, ce modèle n’est pas une norme et peut dérouter les utilisateurs.

### <a name="consider-zero-term-queries"></a>Prendre en compte les requêtes à zéro terme

Les requêtes à zéro terme sont directement déclenchées par l’action de l’utilisateur, plutôt que par l’utilisateur dans une zone de recherche. Toutes les extensions de messagerie tirent parti de requêtes à zéro terme, généralement basées sur ce que l’utilisateur a vu en dernier sur le service. L’avantage est que la probabilité de partager quelque chose que l’utilisateur dernière Saw est assez élevée. D’autres requêtes à zéro terme peuvent être basées sur le service. Par exemple, `news` peut afficher des extensions de News publiées récemment à partir d’événements récents et à venir.

<img width="450px" title="Onglet nouvelle configuration" src="../../assets/images/messaging-extension/zero-term-query.png" />

### <a name="include-link-unfurling"></a>Inclure le lien unfurling

L’un des moyens les plus courants de partager du contenu dans teams est par le biais d’un lien hypertexte, qu’il s’agisse d’une tâche sur laquelle vous avez travaillé ou d’une vidéo que vous avez trouvée drôle. Lorsqu’un utilisateur partage un lien dans Teams, un aperçu incluant une image, un titre ou une description est affiché. Avec [Link unfurling](../how-to/link-unfurling.md) , vous pouvez désormais personnaliser ces aperçus. Les utilisateurs seront également invités à installer votre application après avoir décidé d’utiliser votre préversion. L’ajout de la fonctionnalité Link unfurling à votre application peut grandement améliorer la détectabilité de votre application.

### <a name="highlight-your-messaging-extension"></a>Mettre en surbrillance votre extension de messagerie

Les extensions de messagerie ne sont pas toujours faciles à trouver. Incluez des captures d’écran d’application dans la page de détails de l’application et votre documentation d’aide pour la fonctionnalité de votre extension de messagerie. Vous pouvez également inclure des *procédures* pour votre extension de messagerie dans les présentations de robots pour mettre en surbrillance l’application entière au-delà des interactions bot.

### <a name="add-actions-on-card"></a>Ajouter des actions sur la carte

N’affiche pas simplement le texte pour les utilisateurs. Qu’ils peuvent interagir avec et qui effectuent l’action suivante. Par exemple, l’application places n’insère pas simplement une carte sur la carte, mais un bouton qui, lorsqu’elle est sélectionnée, indique le mode d’affichage de l’emplacement. Les utilisateurs peuvent effectuer des tâches supplémentaires après avoir obtenu la carte.

<img width="450px" title="Onglet nouvelle configuration" src="../../assets/images/messaging-extension/action-on-card.png" />

### <a name="keep-users-in-the-app-context"></a>Conserver les utilisateurs dans le contexte de l’application

Si une carte n’est pas suffisante et que vous devez fournir un lien pour plus d’informations, envisagez d’ouvrir un onglet au lieu d’ouvrir un navigateur pour une meilleure expérience utilisateur. *Voir* [étendre votre application teams avec un onglet personnalisé](../../tabs/how-to/add-tab.md)
