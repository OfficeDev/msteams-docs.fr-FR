---
title: Conception de notifications de flux d’activités
author: heath-hamilton
description: Découvrez comment concevoir des notifications de flux d’activités pour votre application Teams et obtenir le kit Microsoft Teams’interface utilisateur.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 7bc5527a4ac849ab6a46692da85b051f86606f92
ms.sourcegitcommit: 306b6e8cb3aac8bfda10ef3999467a797d64539d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/20/2021
ms.locfileid: "58408551"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>Conception de notifications de flux d’activités pour Microsoft Teams application

Le flux d’activités permet aux utilisateurs d’accéder à leurs notifications Microsoft Teams. Le flux conserve les notifications des quatre semaines passées.

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="Un exemple montre une notification d’application qui s’affiche dans le flux d Teams sur mobile." border="false":::

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="Un exemple montre une notification d’application qui s’affiche dans le flux Teams’activité." border="false":::

---

## <a name="anatomy"></a>Anatomie

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Concevoir l’anatomie de la notification Teams flux d’activités." border="false":::

|Compteur|Description|
|----------|-----------|
|1|**Avatar**: indique qui a initié l’activité.|
|2|**Icône type d’activité/application**: représente le type d’activité. Pour les notifications d’application, l’icône de ligne est remplacée par une icône d’application.|
|3|**Titre (première ligne) : Actor + reason**: *Actor*: Nom de l’utilisateur ou de l’application qui a initié l’activité. *Raison*: décrit l’activité.|
|4 |**Timestamp :** indique quand l’activité s’est produite.|
|5 |**Emplacement (deuxième ligne)**: indique où l’activité s’est produite Teams.|
|6 |**Informations tertiaires (troisième ligne)**: Facultatif. Affiche un aperçu de texte ou des informations supplémentaires.|

## <a name="types-of-activity-feed-notification-cards"></a>Types de cartes de notification de flux d’activités

Les variantes suivantes montrent les types de cartes de notification de flux d’activités que vous pouvez afficher. Le logo de l’application remplace l’avatar de l’utilisateur pour les notifications générées par l’application.

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Variantes de Teams de flux d’activités." border="false":::

## <a name="manage-activity-feed-notifications"></a>Gérer les notifications de flux d’activités

Les utilisateurs peuvent gérer les notifications envoyées à partir de votre application dans la page Teams paramètres.

## <a name="related-system-notifications"></a>Notifications système associées

Chaque activité génère une notification système. Ce qui s’affiche dépend de ce que l’utilisateur configure dans ses paramètres de notification. Les utilisateurs peuvent également choisir un style de notification en fonction de leur système d’exploitation.

# <a name="mobile"></a>[Mobile](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Variantes de Teams de flux d’activités sur Android et iOS." border="false":::

|Compteur|Description|
|----------|-----------|
|1|Android|
|2|iOS|

# <a name="desktop"></a>[Imprimante de bureau](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="Variantes de cartes Teams d’activité sur différents systèmes d’exploitation." border="false":::

|Compteur|Description|
|----------|-----------|
|1|Teams personnalisée|
|2|Windows|
|3|Mac|

---

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Implémenter des notifications de flux d’activités](/graph/teams-send-activityfeednotifications)
