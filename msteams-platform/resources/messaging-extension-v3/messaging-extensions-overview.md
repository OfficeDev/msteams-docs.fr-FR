---
title: Développer des extensions de messagerie
description: Décrit la mise en place des extensions de messagerie dans Microsoft Teams
ms.topic: overview
keywords: extensions de messagerie teams
ms.openlocfilehash: 1eb75371b1a8adbeadbcbdbc0d06c7d88f2f1ccc
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696548"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="9882f-104">Développer des extensions de messagerie pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9882f-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="9882f-105">Les extensions de messagerie sont un moyen puissant pour les utilisateurs d'interagir avec votre application à partir de Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9882f-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="9882f-106">Avec cette fonctionnalité, les utilisateurs peuvent interroger ou publier des informations à partir de votre service et publier ces informations, sous forme de cartes, directement dans un message.</span><span class="sxs-lookup"><span data-stu-id="9882f-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![Exemple de carte d'extension de messagerie](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="9882f-108">Les extensions de messagerie apparaissent en bas de la zone de composition.</span><span class="sxs-lookup"><span data-stu-id="9882f-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="9882f-109">Quelques-uns sont intégrés, tels que Emoji, Giphy et Autocollant.</span><span class="sxs-lookup"><span data-stu-id="9882f-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="9882f-110">Choisissez le **bouton Plus d'options** **(&#8943;)** pour voir d'autres extensions de messagerie, y compris celles que vous ajoutez à partir de la galerie d'applications ou que vous téléchargez vous-même.</span><span class="sxs-lookup"><span data-stu-id="9882f-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="9882f-111">Comment utiliser les extensions de messagerie ?</span><span class="sxs-lookup"><span data-stu-id="9882f-111">How would you use messaging extensions?</span></span> <span data-ttu-id="9882f-112">Voici quelques possibilités :</span><span class="sxs-lookup"><span data-stu-id="9882f-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="9882f-113">Éléments de travail et bogues</span><span class="sxs-lookup"><span data-stu-id="9882f-113">Work items and bugs</span></span>
* <span data-ttu-id="9882f-114">Tickets de support client</span><span class="sxs-lookup"><span data-stu-id="9882f-114">Customer support tickets</span></span>
* <span data-ttu-id="9882f-115">Graphiques et rapports d'utilisation</span><span class="sxs-lookup"><span data-stu-id="9882f-115">Usage charts and reports</span></span>
* <span data-ttu-id="9882f-116">Images et contenu multimédia</span><span class="sxs-lookup"><span data-stu-id="9882f-116">Images and media content</span></span>
* <span data-ttu-id="9882f-117">Opportunités de vente et prospects</span><span class="sxs-lookup"><span data-stu-id="9882f-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="9882f-118">Types d'extensions de messagerie</span><span class="sxs-lookup"><span data-stu-id="9882f-118">Types of messaging extensions</span></span>

<span data-ttu-id="9882f-119">Il existe principalement deux types d'extensions de messagerie que vous pouvez créer pour Teams aujourd'hui.</span><span class="sxs-lookup"><span data-stu-id="9882f-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="9882f-120">Les rubriques suivantes vous guident tout au long du processus de création :</span><span class="sxs-lookup"><span data-stu-id="9882f-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="9882f-121">[Extensions de messagerie basées sur la recherche](~/resources/messaging-extension-v3/search-extensions.md): interrogez votre service pour obtenir des informations et insérez-les dans un message.</span><span class="sxs-lookup"><span data-stu-id="9882f-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="9882f-122">Exemple : Rechercher un élément de travail</span><span class="sxs-lookup"><span data-stu-id="9882f-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="9882f-123">[Extensions de messagerie basées sur l'action](~/resources/messaging-extension-v3/create-extensions.md): collecter des informations auprès de l'utilisateur et publier dans un service tiers.</span><span class="sxs-lookup"><span data-stu-id="9882f-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="9882f-124">Exemple : Créer un élément de travail</span><span class="sxs-lookup"><span data-stu-id="9882f-124">Example: Create a work item</span></span>
