---
title: Configurer les options d'installation par défaut pour votre application
description: Indique comment spécifier les options d'installation par défaut de votre application.
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: a4b70df70c7b9442e29953dae8a8c4e892cb72c1
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946487"
---
# <a name="add-a-default-install-scope-and-group-capability"></a>Ajouter une étendue d'installation et une fonctionnalité de groupe par défaut

Il est courant qu'une application puisse prendre en charge plusieurs scénarios dans Teams, mais vous l'avez peut-être conçue avec une étendue et une fonctionnalité spécifiques à l'esprit. Par exemple, si votre application est principalement destinée à une utilisation en équipe ou en canal, vous pouvez vous assurer que la première option d'installation que les utilisateurs voient dans le Store est Ajouter **à une équipe.**

![Ajouter une application](../../assets/images/compose-extensions/addanapp.png)

Si la fonctionnalité principale de votre application est un bot, vous pouvez également faire du bot la fonctionnalité par défaut lorsqu'un utilisateur installe votre application dans une équipe. 

## <a name="configure-your-apps-default-install-scope"></a>Configurer l'étendue d'installation par défaut de votre application

Configurez l'étendue d'installation par défaut de votre application. Vous ne pouvez définir qu'une seule étendue à la fois.

**Pour configurer l'étendue d'installation par défaut dans le manifeste de votre application**

1. Ouvrez le manifeste de votre application et ajoutez la `defaultInstallScope` propriété.
2. Définissez une valeur `personal` de `team` , ou `groupchat` `meetings` (voir un exemple ci-dessous).

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> Pour plus d'informations, voir le schéma [de manifeste d'application.](~/resources/schema/manifest-schema.md)

## <a name="configure-the-default-capability-for-shared-scopes"></a>Configurer la fonctionnalité par défaut pour les étendues partagées

Configurez la fonctionnalité par défaut lorsque votre application est installée pour une équipe, une réunion ou une conversation.

**Pour configurer les détails dans le manifeste de l'application**

1. Ouvrez le manifeste de votre application et `defaultGroupCapability` ajoutez-y la propriété.
2. Enregistrez les mises à jour.

    Voici un exemple JSON :

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```
> [!NOTE]
> Pour plus d'informations sur le schéma complet, voir [schéma de manifeste.](~/resources/schema/manifest-schema.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Choisir comment distribuer votre application](overview.md)
