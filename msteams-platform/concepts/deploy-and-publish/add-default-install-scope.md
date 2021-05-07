---
title: Configurer les options d’installation par défaut pour votre application
description: Indique comment spécifier les options d’installation par défaut de votre application.
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 561a4f2910e703db5ffce6176f6177dfd661d2ce
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230931"
---
# <a name="configure-default-install-options-for-your-microsoft-teams-app"></a><span data-ttu-id="e367e-103">Configurer les options d’installation par défaut pour Microsoft Teams application</span><span class="sxs-lookup"><span data-stu-id="e367e-103">Configure default install options for your Microsoft Teams app</span></span>

<span data-ttu-id="e367e-104">Il est courant qu’une application puisse prendre en charge plusieurs scénarios dans Teams, mais vous l’avez peut-être conçue avec une étendue et une fonctionnalité spécifiques à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="e367e-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="e367e-105">Par exemple, si votre application est principalement destinée à une utilisation en équipe ou en canal, vous pouvez vous assurer que la première option d’installation que les utilisateurs voient dans le Store est Ajouter **à une équipe.**</span><span class="sxs-lookup"><span data-stu-id="e367e-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

:::row:::
   :::column span="2":::

![Exemple d’ajout d’une dropdown d’application](../../assets/images/compose-extensions/addanapp.png)

   :::column-end:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

<span data-ttu-id="e367e-107">Si la fonctionnalité principale de votre application est un bot, vous pouvez également faire du bot la fonctionnalité par défaut lorsqu’un utilisateur installe votre application dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="e367e-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span>

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="e367e-108">Configurer l’étendue d’installation par défaut de votre application</span><span class="sxs-lookup"><span data-stu-id="e367e-108">Configure your app's default install scope</span></span>

<span data-ttu-id="e367e-109">Configurez l’étendue d’installation par défaut de votre application.</span><span class="sxs-lookup"><span data-stu-id="e367e-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="e367e-110">Vous ne pouvez définir qu’une seule étendue à la fois.</span><span class="sxs-lookup"><span data-stu-id="e367e-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="e367e-111">**Pour configurer l’étendue d’installation par défaut dans le manifeste de votre application**</span><span class="sxs-lookup"><span data-stu-id="e367e-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="e367e-112">Ouvrez le manifeste de votre application et ajoutez la `defaultInstallScope` propriété.</span><span class="sxs-lookup"><span data-stu-id="e367e-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="e367e-113">Définissez la valeur d’étendue d’installation par défaut comme `personal` , , `team` ou `groupchat` `meetings` .</span><span class="sxs-lookup"><span data-stu-id="e367e-113">Set default install scope value as, either `personal`, `team`, `groupchat`, or `meetings`.</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="e367e-114">Pour plus d’informations, voir le schéma [de manifeste d’application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="e367e-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="e367e-115">Configurer la fonctionnalité par défaut pour les étendues partagées</span><span class="sxs-lookup"><span data-stu-id="e367e-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="e367e-116">Configurez la fonctionnalité par défaut lorsque votre application est installée pour une équipe, une réunion ou une conversation de groupe.</span><span class="sxs-lookup"><span data-stu-id="e367e-116">Configure the default capability when your app is installed for a team, meeting, or groupchat.</span></span>

> [!NOTE]
> <span data-ttu-id="e367e-117">`defaultGroupCapability` fournit la fonctionnalité par défaut qui sera ajoutée à l’équipe, au groupchat ou à la réunion.</span><span class="sxs-lookup"><span data-stu-id="e367e-117">`defaultGroupCapability` provides the default capability that will be added to the team, groupchat, or meeting.</span></span> <span data-ttu-id="e367e-118">Sélectionnez un onglet, un bot ou un connecteur comme fonctionnalité par défaut pour votre application, mais vous devez vous assurer que vous avez fourni la fonctionnalité sélectionnée dans la définition de votre application.</span><span class="sxs-lookup"><span data-stu-id="e367e-118">Select a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

<span data-ttu-id="e367e-119">**Pour configurer les détails dans le manifeste de l’application**</span><span class="sxs-lookup"><span data-stu-id="e367e-119">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="e367e-120">Ouvrez le manifeste de votre application et `defaultGroupCapability` ajoutez-y la propriété.</span><span class="sxs-lookup"><span data-stu-id="e367e-120">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="e367e-121">Définissez une valeur `team` de `groupchat` , ou `meetings` .</span><span class="sxs-lookup"><span data-stu-id="e367e-121">Set a value of `team`, `groupchat`, or `meetings`.</span></span>
3. <span data-ttu-id="e367e-122">Pour la fonctionnalité de groupe sélectionnée, les fonctionnalités de groupe disponibles `bot` sont, `tab` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="e367e-122">For the selected group capability, the available group capabilities are, `bot`, `tab`, or `connector`.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="e367e-123">Vous ne pouvez sélectionner qu’une seule fonctionnalité par défaut, ou pour la `bot` `tab` fonctionnalité de groupe `connector` sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="e367e-123">You can select only one default capability, `bot`, `tab`, or `connector` for the selected group capability.</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> <span data-ttu-id="e367e-124">Pour plus d’informations, voir le schéma [de manifeste d’application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="e367e-124">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="e367e-125">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="e367e-125">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e367e-126">Créer votre package d’application</span><span class="sxs-lookup"><span data-stu-id="e367e-126">Create your app package</span></span>](~/concepts/build-and-test/apps-package.md)
