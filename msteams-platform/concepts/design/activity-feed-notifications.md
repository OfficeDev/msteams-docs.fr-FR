---
title: Conception des notifications du flux d'activités
author: heath-hamilton
description: 'Découvrez comment concevoir des notifications de flux d’activité pour votre application Teams et obtenir le Kit d’interface utilisateur Teams. Développer des notifications à partir du canal Teams dans Visual Studio C #'
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 9a17027f7dd68993a118f24bb23cfff0a56651e1
ms.sourcegitcommit: 4ba6392eced76ba6baeb6d6dd9ba426ebf4ab24f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/21/2022
ms.locfileid: "66919766"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>Conception de notifications de flux d’activité pour votre application Microsoft Teams

Le flux d’activité permet aux utilisateurs d’accéder à leurs notifications dans Microsoft Teams. Le flux conserve les notifications des quatre dernières semaines.

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="L’exemple montre une notification d’application qui s’affiche dans le flux d’activité Teams sur mobile.":::

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="L’exemple montre une notification d’application qui s’affiche dans le flux d’activité Teams.":::

---

## <a name="anatomy"></a>Anatomie

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Concevoir l’anatomie de la notification de flux d’activité Teams.":::

|Compteur|Description|
|----------|-----------|
|1|**Avatar** : montre qui a initié l’activité.|
|2|**Type d’activité/icône d’application** : représente le type d’activité. Pour les notifications d’application, l’icône de ligne est remplacée par une icône d’application.|
|3|**Titre (première ligne) : Acteur + raison** : *Acteur* : nom de l’utilisateur ou de l’application qui a lancé l’activité. *Motif* : décrit l’activité.|
|4|**Horodatage** : indique quand l’activité s’est produite.|
|5|**Emplacement (deuxième ligne)** : indique où l’activité s’est produite dans Teams.|
|6|**Aperçu du texte (troisième ligne)** : affiche une ligne tronquée à partir du début de la notification.|

## <a name="types-of-activity-feed-notification-cards"></a>Types de cartes de notification de flux d’activité

Les variantes suivantes montrent les types de cartes de notification de flux d’activité que vous pouvez afficher. Le logo de l’application remplace l’avatar utilisateur pour les notifications générées par l’application.

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Variantes des cartes de flux d’activité Teams.":::

## <a name="manage-activity-feed-notifications"></a>Gérer les notifications de flux d’activité

Les utilisateurs peuvent gérer les notifications envoyées à partir de votre application dans la page des paramètres Teams.

## <a name="related-system-notifications"></a>Notifications système associées

Chaque activité génère une notification système. Ce qui s’affiche dépend de ce que l’utilisateur configure dans ses paramètres de notification. Les utilisateurs peuvent également choisir un style de notification en fonction de leur système d’exploitation.

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Variantes des cartes de flux d’activité Teams sur Android et iOS.":::

|Compteur|Description|
|----------|-----------|
|1|Android|
|2|iOS|

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="Variantes de cartes d’activité Teams sur différents systèmes d’exploitation.":::

|Compteur|Description|
|----------|-----------|
|1|Teams personnalisé|
|2|Windows|
|3|Mac|

---

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../sbs-graphactivity-feedbroadcast.yml) pour envoyer des notifications de flux d’activité dans Teams.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Implémenter des notifications de flux d’activité](/graph/teams-send-activityfeednotifications)
