---
title: Autorisations de périphérique pour le navigateur
keywords: autorisations des fonctionnalités des applications teams
description: Rétablir en toute sécurité la prise en charge des autorisations d’appareil pour les applications dans notre client web
localization_priority: medium
ms.topic: how-to
ms.openlocfilehash: 0789715aebfd1db0c9d0100ccffb2ff213a10d1d
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756743"
---
# <a name="device-permissions-for-the-browser"></a>Autorisations de périphérique pour le navigateur

Teams application qui nécessite des autorisations d’appareil, telles que l’accès à l’appareil photo ou au microphone, exige maintenant que les utilisateurs accordent manuellement des autorisations par niveau d’application dans le navigateur web. Auparavant, le navigateur gérait la façon d’accorder des autorisations d’accès, mais ces autorisations sont désormais gérées dans Microsoft Teams. Cela a des implications sur la façon dont vous concevez votre application et si elles nécessitent ces autorisations dans le navigateur.

## <a name="enable-apps-device-permissions"></a>Activer les autorisations d’appareil de l’application

Si votre application Teams a déclaré dans le [manifeste de l’application](native-device-permissions.md#specify-permissions) qu’elle a besoin d’autorisations d’appareil, l’option **Autorisations d’application** s’affiche pour que les utilisateurs activent les autorisations d’appareil de l’application. L’option **Autorisations d’application** est disponible dans les fonctionnalités suivantes :

* **Applications personnelles et dialogues de module de tâche** : l’option **Autorisations d’application** est disponible dans le coin supérieur droit de la page.
<img src="../../assets/images/tabs/apppermissions.png" alt="App permissions button" width="800"/>

* **Onglets de conversations, de canaux ou de réunions** : l’option **Autorisations d’application** est disponible dans la liste déroulante de l’onglet. ![Liste déroulante autorisations d’application](../../assets/images/tabs/drop-downapppermissions.png)

Une fois l’option **Autorisations d’application** sélectionnée, une fenêtre contextuelle s’affiche, dans laquelle l’utilisateur peut activer le bouton des autorisations.

Un utilisateur doit activer ces autorisations dans le navigateur pour qu’elles prennent effet. Une fois que l’utilisateur a modifié les autorisations d’appareil de l’application dans le navigateur, il est invité à recharger l’application dans Teams.

> [!IMPORTANT]
> Vous devez informer les utilisateurs de l’emplacement où accéder pour activer ces **Autorisations d’application** dans Microsoft Teams.

## <a name="recommendation"></a>Recommandation

Teams application qui nécessite des autorisations d’appareil dans le navigateur doit afficher des instructions aux utilisateurs sur l’emplacement où trouver et activer ces autorisations dans l’interface utilisateur Teams. Selon le contexte dans lequel votre application s’exécute, vous devez vous assurer que vos instructions pointent l’utilisateur vers l’emplacement approprié pour accéder à ces autorisations. Les autorisations diffèrent pour les applications personnelles, les dialogues de module de tâche, les onglets des conversations, les canaux ou les réunions.

</br>
<img src="../../assets/images/tabs/enable-access.png" alt="Enable camera access" width="800"/>

## <a name="code-sample"></a>Exemple de code

|Exemple de nom | Description | Node.js |
|----------------|-----------------|--------------|
| Autorisations d’appareil de l’onglet pour le navigateur | L’exemple de code illustre comment afficher les autorisations d’appareil pour le navigateur. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-device-permissions/nodejs) |

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../sbs-tab-device-permissions.yml) pour accorder l’autorisation d’appareil de l’onglet dans Microsoft Teams.

## <a name="see-also"></a>Voir aussi

* [Vue d’ensemble des fonctionnalités de l’appareil](device-capabilities-overview.md)
* [Demande des autorisations d’appareil](native-device-permissions.md)
