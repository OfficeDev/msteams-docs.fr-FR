---
title: Configurer les options d’installation par défaut pour votre application
description: Décrit comment spécifier les options d’installation par défaut de votre application et la fonctionnalité par défaut pour les étendues partagées.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: ad59f6645e0d302e973647f9ff63b2898362f6ee
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889089"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a>Configurer les options d’installation par défaut pour Microsoft Teams application

Il est courant qu’une application puisse prendre en charge plusieurs scénarios dans Teams, mais vous l’avez peut-être conçue avec une étendue et une fonctionnalité spécifiques à l’esprit. Par exemple, si votre application est principalement destinée à une utilisation en équipe ou en canal, vous pouvez vous assurer que la première option d’installation que les utilisateurs voient dans le Store est Ajouter **à une équipe.**

:::row:::
   :::column span="2":::

![Exemple d’ajout d’une dropdown d’application](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

Si la fonctionnalité principale de votre application est un bot, vous pouvez également faire du bot la fonctionnalité par défaut lorsqu’un utilisateur installe votre application dans une équipe.

## <a name="configure-your-apps-default-install-scope"></a>Configurer l’étendue d’installation par défaut de votre application

Configurez l’étendue d’installation par défaut de votre application. Vous ne pouvez définir qu’une seule étendue à la fois.

**Pour configurer l’étendue d’installation par défaut dans le manifeste de votre application**

1. Ouvrez le manifeste de votre application et ajoutez la `defaultInstallScope` propriété.
2. Définissez la valeur d’étendue d’installation par défaut en `personal` tant que , , ou `team` `groupchat` `meetings` .

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> Pour plus d’informations, voir le schéma [de manifeste d’application.](~/resources/schema/manifest-schema.md)

## <a name="configure-the-default-capability-for-shared-scopes"></a>Configurer la fonctionnalité par défaut pour les étendues partagées

Configurez la fonctionnalité par défaut lorsque votre application est installée pour une équipe, une réunion ou une conversation de groupe.

> [!NOTE]
> `defaultGroupCapability` fournit la fonctionnalité par défaut qui sera ajoutée à l’équipe, au groupchat ou à la réunion. Sélectionnez un onglet, un bot ou un connecteur comme fonctionnalité par défaut pour votre application, mais vous devez vous assurer que vous avez fourni la fonctionnalité sélectionnée dans la définition de votre application.

**Pour configurer les détails dans le manifeste de l’application**

1. Ouvrez le manifeste de votre application et `defaultGroupCapability` ajoutez-y la propriété.
2. Définissez une valeur `team` de `groupchat` , ou `meetings` .
3. Pour la fonctionnalité de groupe sélectionnée, les fonctionnalités de groupe disponibles `bot` sont, `tab` ou `connector` . 

    > [!NOTE]
    > Vous ne pouvez sélectionner qu’une seule fonctionnalité par défaut, ou pour la `bot` `tab` fonctionnalité de groupe `connector` sélectionnée.

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> Pour plus d’informations, voir le schéma [de manifeste d’application.](~/resources/schema/manifest-schema.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer votre package d’application](~/concepts/build-and-test/apps-package.md)
