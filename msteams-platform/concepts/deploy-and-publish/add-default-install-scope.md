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
# <a name="add-a-default-install-scope-and-group-capability"></a><span data-ttu-id="1e1a3-103">Ajouter une étendue d'installation et une fonctionnalité de groupe par défaut</span><span class="sxs-lookup"><span data-stu-id="1e1a3-103">Add a default install scope and group capability</span></span>

<span data-ttu-id="1e1a3-104">Il est courant qu'une application puisse prendre en charge plusieurs scénarios dans Teams, mais vous l'avez peut-être conçue avec une étendue et une fonctionnalité spécifiques à l'esprit.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-104">It’s common for an app to support multiple scenarios in Teams, but you may have designed it with a specific scope and capability in mind.</span></span> <span data-ttu-id="1e1a3-105">Par exemple, si votre application est principalement destinée à une utilisation en équipe ou en canal, vous pouvez vous assurer que la première option d'installation que les utilisateurs voient dans le Store est Ajouter **à une équipe.**</span><span class="sxs-lookup"><span data-stu-id="1e1a3-105">For example, if your app is primarily for team or channel use, you can make sure that the first install option users see in the store is **Add to a team**.</span></span>

![Ajouter une application](../../assets/images/compose-extensions/addanapp.png)

<span data-ttu-id="1e1a3-107">Si la fonctionnalité principale de votre application est un bot, vous pouvez également faire du bot la fonctionnalité par défaut lorsqu'un utilisateur installe votre application dans une équipe.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-107">If your app's primary capability is a bot, you can also make the bot the default capability when a user installs your app to a team.</span></span> 

## <a name="configure-your-apps-default-install-scope"></a><span data-ttu-id="1e1a3-108">Configurer l'étendue d'installation par défaut de votre application</span><span class="sxs-lookup"><span data-stu-id="1e1a3-108">Configure your app's default install scope</span></span>

<span data-ttu-id="1e1a3-109">Configurez l'étendue d'installation par défaut de votre application.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-109">Configure the default install scope for your app.</span></span> <span data-ttu-id="1e1a3-110">Vous ne pouvez définir qu'une seule étendue à la fois.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-110">You can set only one scope at a time.</span></span>

<span data-ttu-id="1e1a3-111">**Pour configurer l'étendue d'installation par défaut dans le manifeste de votre application**</span><span class="sxs-lookup"><span data-stu-id="1e1a3-111">**To configure the default install scope in your app manifest**</span></span>

1. <span data-ttu-id="1e1a3-112">Ouvrez le manifeste de votre application et ajoutez la `defaultInstallScope` propriété.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-112">Open your app manifest and add the `defaultInstallScope` property.</span></span>
2. <span data-ttu-id="1e1a3-113">Définissez une valeur `personal` de `team` , ou `groupchat` `meetings` (voir un exemple ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="1e1a3-113">Set a value of `personal`, `team`, `groupchat`, or `meetings` (see an example below).</span></span>

    ```json
    "defaultInstallScope": "meetings",
    ```

> [!NOTE]
> <span data-ttu-id="1e1a3-114">Pour plus d'informations, voir le schéma [de manifeste d'application.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="1e1a3-114">For more information, see the [app manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="configure-the-default-capability-for-shared-scopes"></a><span data-ttu-id="1e1a3-115">Configurer la fonctionnalité par défaut pour les étendues partagées</span><span class="sxs-lookup"><span data-stu-id="1e1a3-115">Configure the default capability for shared scopes</span></span>

<span data-ttu-id="1e1a3-116">Configurez la fonctionnalité par défaut lorsque votre application est installée pour une équipe, une réunion ou une conversation.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-116">Configure the default capability when your app is installed for a team, meeting, or chat.</span></span>

<span data-ttu-id="1e1a3-117">**Pour configurer les détails dans le manifeste de l'application**</span><span class="sxs-lookup"><span data-stu-id="1e1a3-117">**To configure details in app manifest**</span></span>

1. <span data-ttu-id="1e1a3-118">Ouvrez le manifeste de votre application et `defaultGroupCapability` ajoutez-y la propriété.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-118">Open your app manifest and add the `defaultGroupCapability` property to it.</span></span>
2. <span data-ttu-id="1e1a3-119">Enregistrez les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="1e1a3-119">Save the updates.</span></span>

    <span data-ttu-id="1e1a3-120">Voici un exemple JSON :</span><span class="sxs-lookup"><span data-stu-id="1e1a3-120">Following is a JSON example:</span></span>

    ```json
    "defaultGroupCapability": {
        "team": "bot",
        "groupchat": "bot",
        "meetings": "tab"
    }
    ```
> [!NOTE]
> <span data-ttu-id="1e1a3-121">Pour plus d'informations sur le schéma complet, voir [schéma de manifeste.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="1e1a3-121">For information on full schema, see [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="1e1a3-122">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="1e1a3-122">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e1a3-123">Choisir comment distribuer votre application</span><span class="sxs-lookup"><span data-stu-id="1e1a3-123">Choose how to distribute your app</span></span>](overview.md)
