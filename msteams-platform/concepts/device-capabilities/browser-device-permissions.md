---
title: Autorisations de périphérique pour le navigateur
keywords: autorisations des fonctionnalités des applications Teams
description: Récupérer en toute sécurité la prise en charge des autorisations d’appareil pour les applications dans notre client web
localization_priority: Normal
ms.topic: how-to
ms.openlocfilehash: 32ccdc732fb05b82ab36b631c5e35f25f8c6c7dc
ms.sourcegitcommit: db529cdf7e9195fa45b9065c50f5381770cc3711
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/11/2021
ms.locfileid: "60912184"
---
# <a name="device-permissions-for-the-browser"></a>Autorisations de périphérique pour le navigateur

> [!NOTE]
> La modification de la façon dont les autorisations d’appareil sont gérées dans le navigateur est actuellement disponible en [prévisualisation publique pour les](../../resources/dev-preview/developer-preview-intro.md) développeurs uniquement. Cette modification sera généralement disponible d’ici le 01 février 2022.

Les applications qui nécessitent des autorisations d’appareil, telles que l’accès à l’appareil photo ou au microphone, exigent désormais que les utilisateurs accordent manuellement leur consentement au niveau de chaque application dans le navigateur web. Auparavant, le navigateur géré comment ces autorisations ont été accordées, mais maintenant ces autorisations seront gérées dans Microsoft Teams. Cela a une incidence sur la façon dont vous concevez votre application s’ils requièrent ces autorisations dans le navigateur.

## <a name="change-in-behavior"></a>Modification du comportement
Si votre application a déclaré qu’elle a besoin d’autorisations d’appareil dans votre manifeste [d’application,](native-device-permissions.md)les utilisateurs disposeront d’une option « Autorisations d’application » dans laquelle ils peuvent activer les autorisations d’appareil d’une application. L’option « autorisations d’application » se trouve dans les applications personnelles, les boîtes de dialogue de module de tâche et les onglets dans les conversations, les canaux ou les réunions.

### <a name="personal-apps-and-task-module-dialogs"></a>Applications personnelles et boîtes de dialogue de module de tâche
Le paramètre « autorisations d’application » se trouve en haut à droite.
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

### <a name="chat-channel-or-meeting-tabs"></a>Onglets Conversation, Canal ou Réunion
Le paramètre « Autorisations de l’application » se trouve dans ladown de l’onglet.
![Drop-down Des autorisations d’application](../../assets/images/tabs/drop-downapppermissions.png)

Un utilisateur devra activer ces autorisations dans le navigateur pour que ces autorisations prennent effet. Lorsqu’un utilisateur modifie les autorisations d’appareil d’une application dans le navigateur, il est invité à recharger l’application dans Teams. Il est important de faire en sorte que les utilisateurs sachent où aller pour activer ces autorisations dans Microsoft Teams.

## <a name="recommendation"></a>Recommandation
Microsoft Teams applications qui nécessitent des autorisations d’appareil dans le navigateur sont censés afficher des instructions aux utilisateurs sur l’endroit où trouver et activer ces autorisations dans l’interface Teams utilisateur. Selon le contexte dans lequel votre application est en cours d’exécution, vous devez vous assurer que vos instructions pointent l’utilisateur vers un emplacement correct pour accéder à ces autorisations, car elles diffèrent pour les applications personnelles, les boîtes de dialogue de module de tâche et les onglets dans les conversations, les canaux ou les réunions.

<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="see-also"></a>Voir aussi

* [Vue d’ensemble des fonctionnalités des appareils](device-capabilities-overview.md)
* [Demande des autorisations d’appareil](native-device-permissions.md)
