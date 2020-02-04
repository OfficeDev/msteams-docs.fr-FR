---
title: Développer des extensions de messagerie
description: Décrit comment se familiariser avec les extensions de messagerie dans Microsoft teams
keywords: extensions de messagerie des extensions de messagerie teams
ms.openlocfilehash: 6ba8f73d40f795a83f28707ef89c207c5d51d67c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673565"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="8db7f-104">Développer des extensions de messagerie pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="8db7f-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="8db7f-105">Les extensions de messagerie sont un moyen efficace pour les utilisateurs de s’engager avec votre application à partir de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8db7f-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="8db7f-106">Grâce à cette fonctionnalité, les utilisateurs peuvent interroger ou publier des informations à partir de votre service et publier ces informations, sous la forme de cartes, directement dans un message.</span><span class="sxs-lookup"><span data-stu-id="8db7f-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![Exemple de carte d’extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="8db7f-108">Les extensions de messagerie apparaissent au bas de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="8db7f-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="8db7f-109">Quelques-unes sont intégrées, telles que les emoji, les Giphy et les autocollants.</span><span class="sxs-lookup"><span data-stu-id="8db7f-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="8db7f-110">Cliquez sur le bouton **autres options** (**&#8943;**) pour afficher les autres extensions de messagerie, y compris celles que vous ajoutez à partir de la Galerie d’applications ou téléchargez vous-même.</span><span class="sxs-lookup"><span data-stu-id="8db7f-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="8db7f-111">Comment utiliseriez-vous les extensions de messagerie ?</span><span class="sxs-lookup"><span data-stu-id="8db7f-111">How would you use messaging extensions?</span></span> <span data-ttu-id="8db7f-112">Voici quelques possibilités :</span><span class="sxs-lookup"><span data-stu-id="8db7f-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="8db7f-113">Éléments de travail et bogues</span><span class="sxs-lookup"><span data-stu-id="8db7f-113">Work items and bugs</span></span>
* <span data-ttu-id="8db7f-114">Tickets de support client</span><span class="sxs-lookup"><span data-stu-id="8db7f-114">Customer support tickets</span></span>
* <span data-ttu-id="8db7f-115">Graphiques et rapports d’utilisation</span><span class="sxs-lookup"><span data-stu-id="8db7f-115">Usage charts and reports</span></span>
* <span data-ttu-id="8db7f-116">Images et contenu multimédia</span><span class="sxs-lookup"><span data-stu-id="8db7f-116">Images and media content</span></span>
* <span data-ttu-id="8db7f-117">Opportunités de vente et prospects</span><span class="sxs-lookup"><span data-stu-id="8db7f-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="8db7f-118">Types d’extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="8db7f-118">Types of messaging extensions</span></span>

<span data-ttu-id="8db7f-119">Il existe principalement deux types d’extensions de messagerie que vous pouvez créer pour teams dès aujourd’hui.</span><span class="sxs-lookup"><span data-stu-id="8db7f-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="8db7f-120">Les rubriques suivantes vous guideront tout au long du processus de création :</span><span class="sxs-lookup"><span data-stu-id="8db7f-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="8db7f-121">[Extensions de messagerie basées sur la recherche](~/resources/messaging-extension-v3/search-extensions.md): interrogez votre service pour obtenir des informations et insérez-les dans un message.</span><span class="sxs-lookup"><span data-stu-id="8db7f-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="8db7f-122">Exemple : Rechercher un élément de travail</span><span class="sxs-lookup"><span data-stu-id="8db7f-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="8db7f-123">[Extensions de messagerie basées sur les actions](~/resources/messaging-extension-v3/create-extensions.md): collectez des informations auprès de l’utilisateur et publiez-les sur un service tiers.</span><span class="sxs-lookup"><span data-stu-id="8db7f-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="8db7f-124">Exemple : créer un élément de travail</span><span class="sxs-lookup"><span data-stu-id="8db7f-124">Example: Create a work item</span></span>
