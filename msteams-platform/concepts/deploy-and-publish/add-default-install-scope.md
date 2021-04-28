---
title: Configurer les options d'installation par défaut pour votre application
description: Indique comment spécifier les options d'installation par défaut de votre application.
ms.topic: how-to
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 0afcce50a4779421016c23c4ec4e3d25cc3401d1
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058613"
---
# <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="516c5-103">Ajouter une étendue d'installation et une fonctionnalité de groupe par défaut</span><span class="sxs-lookup"><span data-stu-id="516c5-103">Add a default install scope and group capability</span></span>

<span data-ttu-id="516c5-104">Il est courant qu'une application puisse prendre en charge plusieurs scénarios dans Teams, mais vous l'avez peut-être conçue avec une étendue et une fonctionnalité spécifiques à l'esprit.</span><span class="sxs-lookup"><span data-stu-id="516c5-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="516c5-105">Par exemple, si votre application est principalement destinée à une utilisation en équipe ou en canal, vous pouvez vous assurer que la première option d'installation que les utilisateurs voient dans le Store est Ajouter **à une équipe.**</span><span class="sxs-lookup"><span data-stu-id="516c5-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

![Ajouter une application](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="516c5-107">Si la fonctionnalité principale de votre application est un bot, vous pouvez également faire du bot la fonctionnalité par défaut lorsqu'un utilisateur installe votre application dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="516c5-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span>

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="516c5-108">Configurer l'étendue d'installation par défaut de votre application</span><span class="sxs-lookup"><span data-stu-id="516c5-108">Configure your app's default install scope</span></span>

<span data-ttu-id="516c5-109">Configurez l'étendue d'installation par défaut de votre application.</span><span class="sxs-lookup"><span data-stu-id="516c5-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="516c5-110">Vous ne pouvez définir qu'une seule étendue à la fois.</span><span class="sxs-lookup"><span data-stu-id="516c5-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="516c5-111">**Pour configurer l'étendue d'installation par défaut dans le manifeste de votre application**</span><span class="sxs-lookup"><span data-stu-id="516c5-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="516c5-112">Ouvrez le manifeste de votre application et ajoutez la `defaultInstallScope` propriété.</span><span class="sxs-lookup"><span data-stu-id="516c5-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="516c5-113">Définissez la valeur d'étendue d'installation par défaut en `personal` tant que , , ou `team` `groupchat` `meetings` .</span><span class="sxs-lookup"><span data-stu-id="516c5-113">Set default install scope value as, either `personal`, `team`, `groupchat`, or `meetings`.</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="516c5-114">Pour plus d'informations, voir le schéma [de manifeste d'application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="516c5-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="516c5-115">Configurer la fonctionnalité par défaut pour les étendues partagées</span><span class="sxs-lookup"><span data-stu-id="516c5-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="516c5-116">Configurez la fonctionnalité par défaut lorsque votre application est installée pour une équipe, une réunion ou une conversation de groupe.</span><span class="sxs-lookup"><span data-stu-id="516c5-116">Configure the default capability when your app is installed for a team, meeting, or groupchat.</span></span>

> [!NOTE]
> <span data-ttu-id="516c5-117">`defaultGroupCapability` fournit la fonctionnalité par défaut qui sera ajoutée à l'équipe, au groupchat ou à la réunion.</span><span class="sxs-lookup"><span data-stu-id="516c5-117">`defaultGroupCapability` provides the default capability that will be added to the team, groupchat, or meeting.</span></span> <span data-ttu-id="516c5-118">Sélectionnez un onglet, un bot ou un connecteur comme fonctionnalité par défaut pour votre application, mais vous devez vous assurer que vous avez fourni la fonctionnalité sélectionnée dans la définition de votre application.</span><span class="sxs-lookup"><span data-stu-id="516c5-118">Select a tab, bot, or connector as the default capability for your app, but you must ensure that you have provided the selected capability in your app definition.</span></span>

<span data-ttu-id="516c5-119">**Pour configurer les détails dans le manifeste de l'application**</span><span class="sxs-lookup"><span data-stu-id="516c5-119">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="516c5-120">Ouvrez le manifeste de votre application et `defaultGroupCapability` ajoutez-y la propriété.</span><span class="sxs-lookup"><span data-stu-id="516c5-120">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="516c5-121">Définissez une valeur `team` de `groupchat` , ou `meetings` .</span><span class="sxs-lookup"><span data-stu-id="516c5-121">Set a value of `team`, `groupchat`, or `meetings`.</span></span>
3. <span data-ttu-id="516c5-122">Pour la fonctionnalité de groupe sélectionnée, les fonctionnalités de groupe disponibles `bot` sont, `tab` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="516c5-122">For the selected group capability, the available group capabilities are, `bot`, `tab`, or `connector`.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="516c5-123">Vous ne pouvez sélectionner qu'une seule fonctionnalité par défaut, ou pour la `bot` `tab` fonctionnalité de groupe `connector` sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="516c5-123">You can select only one default capability, `bot`, `tab`, or `connector` for the selected group capability.</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```

> [!NOTE]
> <span data-ttu-id="516c5-124">Pour plus d'informations, voir le schéma [de manifeste d'application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="516c5-124">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="516c5-125">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="516c5-125">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="516c5-126">Choisir comment distribuer votre application</span><span class="sxs-lookup"><span data-stu-id="516c5-126">Choose how to distribute your app</span></span>](overview.md)
