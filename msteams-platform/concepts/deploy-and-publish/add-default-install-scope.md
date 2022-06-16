---
title: Configurer les options d’installation par défaut pour votre application
description: Découvrez comment spécifier les options d’installation par défaut et la fonctionnalité par défaut de votre application Teams pour les étendues partagées.
ms.topic: how-to
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 9055b765c30f83c4031ad0e2ba5f18f4e747ac3f
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/16/2022
ms.locfileid: "66122900"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a>Configurer les options d’installation par défaut pour votre application Microsoft Teams

Il est courant qu’une application prenne en charge plusieurs scénarios dans Teams, mais vous l’avez peut-être conçue avec une étendue et une fonctionnalité spécifiques à l’esprit. Par exemple, si votre application est principalement destinée à une utilisation d’équipe ou de canal, vous pouvez vous assurer que la première option d’installation que les utilisateurs voient dans le Store est **Ajouter à une équipe**.

:::row:::
   :::column span="2":::

![Exemple d’ajout d’une liste déroulante d’applications](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

Si la fonctionnalité principale de votre application est un bot, vous pouvez également en faire la fonctionnalité par défaut lorsqu’un utilisateur installe votre application dans une équipe.

## <a name="configure-your-apps-default-install-scope"></a>Configurer l’étendue d’installation par défaut de votre application

Configurez l’étendue d’installation par défaut pour votre application. Vous ne pouvez définir qu’une seule étendue à la fois.

Pour configurer l’étendue d’installation par défaut dans le manifeste de votre application :

1. Ouvrez le manifeste de votre application et ajoutez la `defaultInstallScope` propriété.
2. Définissez la valeur d’étendue d’installation par défaut comme , `personal`, `team`ou `groupchat``meetings`.

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> Pour plus d’informations, consultez le [schéma de manifeste de l’application](~/resources/schema/manifest-schema.md).

## <a name="configure-the-default-capability-for-shared-scopes"></a>Configurer la fonctionnalité par défaut pour les étendues partagées

Configurez la fonctionnalité par défaut lorsque votre application est installée pour une équipe, une réunion ou un groupechat.

> [!NOTE]
> `defaultGroupCapability` fournit la fonctionnalité par défaut qui sera ajoutée à l’équipe, au groupchat ou à la réunion. Sélectionnez un onglet, un bot ou un connecteur comme fonctionnalité par défaut pour votre application, mais vous devez vous assurer que vous avez fourni la fonctionnalité sélectionnée dans la définition de votre application.

Pour configurer les détails dans le manifeste de l’application :

1. Ouvrez le manifeste de votre application et ajoutez-y la `defaultGroupCapability` propriété.
2. Définissez une valeur de `team`, `groupchat`ou `meetings`.
3. Pour la fonctionnalité de groupe sélectionnée, les fonctionnalités de groupe disponibles sont , `bot``tab`ou `connector`.

    > [!NOTE]
    > Vous ne pouvez sélectionner qu’une seule fonctionnalité par défaut, `bot``tab`ou `connector` pour la fonctionnalité de groupe sélectionnée.

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> Pour plus d’informations, consultez le [schéma de manifeste de l’application](~/resources/schema/manifest-schema.md).

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer votre package d’application](~/concepts/build-and-test/apps-package.md)
