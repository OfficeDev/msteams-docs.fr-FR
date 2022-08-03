---
title: Partager dans Teams à partir d’une application ou d’un onglet personnel
description: Découvrez comment activer le bouton Partager vers Teams sur votre application ou onglet personnel, les limitations et l’expérience de l’utilisateur final.
ms.topic: reference
ms.localizationpriority: medium
ms.openlocfilehash: 5d70c8d399b4a065419341bc24763f7aa0f50af6
ms.sourcegitcommit: 990a36fb774e614146444d4adaa2c9bcdb835998
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2022
ms.locfileid: "67232196"
---
# <a name="share-to-teams-from-personal-app-or-tab"></a>Partager dans Teams à partir d’une application ou d’un onglet personnel

Le partage vers Teams permet aux utilisateurs de partager le contenu à partir d’une application ou d’un onglet personnel vers un autre utilisateur, groupe ou canal dans Teams. Les utilisateurs peuvent sélectionner Partager vers Teams pour lancer l’expérience Partager vers Teams dans une fenêtre contextuelle. La fenêtre contextuelle permet aux utilisateurs d’ajouter un autre utilisateur, groupe ou canal pour partager le contenu.

L’image suivante montre la fenêtre contextuelle Partager vers Teams :

:::image type="content" source="../../assets/images/share-to-teams/share-to-teams.PNG" alt-text="share-to-teams-pop-up":::

## <a name="enable-share-to-teams-button"></a>Bouton Activer partager vers Teams

> [!NOTE]
> Vérifiez que vous [disposez du Kit de développement logiciel (SDK) client JavaScript Microsoft Teams](../../tabs/how-to/using-teams-client-sdk.md) ou du [Kit de développement logiciel (SDK) client JavaScript Microsoft Teams v2 (](../../tabs/how-to/using-teams-client-sdk.md)`@microsoft/teams-js@1.11.0-beta.7`ou version ultérieure) pour activer Share to Teams pour votre application ou onglet personnel.

Pour activer Share to Teams :

1. Créez une application ou un onglet personnel avec le **Kit de développement logiciel (SDK) client Javascript Teams**.

2. Bouton Créer un **partage vers Teams** .

3. Sur le bouton Partager vers Teams, appelez `microsoftTeams.sharing.shareWebContent` avec une charge utile de contenu.

L’exemple suivant explique comment créer une charge utile de contenu :

```json
microsoftTeams.sharing.shareWebContent({
        content: [
          {
            type: 'URL',
            url: '<URL to be shared>',
            message: 'Default message to be loaded in the compose box',
            preview: true
          }
        ]
      });
```

La charge utile contient les paramètres suivants :

| Nom de la propriété | Objectif |
|---|---|
| `type` | Le type doit être `URL` |
| `url` | `URL` à partager |
|`message`| Message par défaut à charger dans la zone de composition |
| `preview` | Définir pour `true` activer la préversion d’URL |

L’image suivante montre l’option Partager vers Teams :

:::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="share-to-teams-button":::

## <a name="response-codes"></a>Codes de réponse

Le tableau suivant présente les codes de réponse :

|Code de réponse|Description|
|---|---|
| **100** | API non prise en charge dans la plateforme actuelle. |
| **404** | Le fichier spécifié est introuvable à l’emplacement donné. |
| **500** | Erreur interne rencontrée lors de l’exécution de l’opération requise. |
| **501** | L’API n’est pas prise en charge dans le contexte actuel. |
| **1 000** | Autorisations refusées par l’utilisateur. |
| **2000** | Problème réseau. |
| **3000** | Le matériel sous-jacent ne prend pas en charge la fonctionnalité. |
| **4000** | Un ou plusieurs arguments ne sont pas valides. |
| **5000** | L’utilisateur n’est pas autorisé pour cette opération. |
| **6000** | Impossible de terminer l’opération en raison de ressources insuffisantes. |
| **7000** | La plateforme a limité la demande en raison de l’appel trop fréquent de l’API. |
| **8000** | L’utilisateur a abandonné l’opération. |
| **9000** | Le code de plateforme est ancien et n’implémente pas cette API. |
| **10 000** | La valeur de retour est trop grande et a dépassé nos limites de taille. |

## <a name="limitations"></a>Limites

Les limitations pour ajouter le bouton Partager à Teams :

* Le bouton Partager vers Teams peut être hébergé ou incorporé dans une application s’exécutant dans Teams.
* Vous pouvez ajouter le bouton Partager à Teams à l’application créée à l’aide du **Kit de développement logiciel (SDK) client Javascript Teams**.

## <a name="end-user-share-to-teams-experience"></a>Expérience share to Teams de l’utilisateur final

Une fois que vous avez activé le bouton Partager vers teams sur l’application ou l’onglet personnel, vous pouvez partager le contenu. Pour y accéder, procédez comme suit :

1. Ouvrez une application ou un onglet personnel, puis **sélectionnez Partager dans Teams**.

    :::image type="content" source="../../assets/images/share-to-teams/share-button.PNG" alt-text="share-to-teams-button":::

2. Ajoutez un autre utilisateur, groupe ou canal pour partager le contenu.

    :::image type="content" source="../../assets/images/share-to-teams/add-recepient.PNG" alt-text="add-recipient":::

    > [!NOTE]
    > Vous pouvez ajouter une note en **disant quelque chose à ce sujet**.

3. Sélectionnez **Partager**.

   :::image type="content" source="../../assets/images/share-to-teams/add-notes.PNG" alt-text="add-note":::

4. Sélectionnez **Affichage** pour accéder à la conversation dans laquelle le lien a été partagé.

   :::image type="content" source="../../assets/images/share-to-teams/link-shared.PNG" alt-text="share-to-teams-link-shared":::

## <a name="see-also"></a>Voir aussi

* [Partager vers Teams à partir d’applications web](share-to-teams-from-web-apps.md)
* [Créer un onglet personnel](../../tabs/how-to/create-personal-tab.md)
