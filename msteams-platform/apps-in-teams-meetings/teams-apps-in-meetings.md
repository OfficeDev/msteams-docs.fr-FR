---
title: Applications pour Teams réunions
author: surbhigupta
description: vue d’ensemble des applications dans Teams réunions basées sur le rôle des participants et des utilisateurs
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 0ba475e852b8dc673d33ac818077b3b0951ac5f9
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068574"
---
# <a name="apps-for-teams-meetings"></a><span data-ttu-id="ca918-104">Applications pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="ca918-104">Apps for Teams meetings</span></span>

<span data-ttu-id="ca918-105">Les réunions permettent la collaboration, le partenariat, la communication éclairée et les commentaires partagés dans un forum actif et inclusif.</span><span class="sxs-lookup"><span data-stu-id="ca918-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="ca918-106">L’application de réunion peut offrir une expérience utilisateur pour chaque étape du cycle de vie de la réunion, notamment avant la réunion, en réunion et après la réunion, en fonction de l’état du participant.</span><span class="sxs-lookup"><span data-stu-id="ca918-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting, and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="ca918-107">Les utilisateurs peuvent accéder aux applications pendant les réunions à l’aide de la galerie d’onglets, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ca918-107">The users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="ca918-108">Pré-préparation d’un tableau kanban.</span><span class="sxs-lookup"><span data-stu-id="ca918-108">Pre-stage a Kanban board.</span></span>
* <span data-ttu-id="ca918-109">Lancez une boîte de dialogue actionnable en réunion.</span><span class="sxs-lookup"><span data-stu-id="ca918-109">Launch an in-meeting actionable dialog.</span></span>
* <span data-ttu-id="ca918-110">Créer une enquête post-réunion.</span><span class="sxs-lookup"><span data-stu-id="ca918-110">Create a post-meeting survey.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/nKAy5rNDus4]

<span data-ttu-id="ca918-111">Cet article fournit une vue d’ensemble de l’extensibilité des applications de réunion, des références d’API, de l’activer et de la configurer pour les réunions, ainsi que des scènes personnalisées du mode ensemble dans Teams.</span><span class="sxs-lookup"><span data-stu-id="ca918-111">This article provides an overview of meeting app extensibility, API references, enable and configure apps for meetings, and custom Together Mode scenes in Teams.</span></span>

<span data-ttu-id="ca918-112">Vous pouvez améliorer votre expérience de réunion à l’aide de la fonctionnalité d’extensibilité de réunion, qui vous permet d’intégrer vos applications dans les réunions.</span><span class="sxs-lookup"><span data-stu-id="ca918-112">You can enhance your meeting experience by using the meeting extensibility feature, which enables you to integrate your apps within meetings.</span></span> <span data-ttu-id="ca918-113">Il inclut également différentes étapes d’un cycle de vie de réunion, où vous pouvez intégrer des onglets, des bots et des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="ca918-113">It also includes different stages of a meeting lifecycle, where you can integrate tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="ca918-114">Avec les API d’extensibilité des réunions, vous pouvez identifier différents rôles de participants et types d’utilisateurs, obtenir des événements de réunion, générer des boîtes de dialogue en réunion, etc.</span><span class="sxs-lookup"><span data-stu-id="ca918-114">With meetings extensibility APIs, you can identify different participant roles and user types, get meeting events, generate in-meeting dialogs, and so on.</span></span>

<span data-ttu-id="ca918-115">Pour personnaliser les Teams avec des applications pour les réunions, vous pouvez activer vos applications pour les réunions Teams en mettant à jour votre manifeste d’application et vous pouvez également configurer vos applications pour les scénarios de réunion.</span><span class="sxs-lookup"><span data-stu-id="ca918-115">To customize Teams with apps for meetings, you can enable your apps for Teams meetings by updating your app manifest and you can also configure your apps for meeting scenarios.</span></span>

<span data-ttu-id="ca918-116">La nouvelle fonctionnalité de scènes en mode ensemble personnalisée permet aux utilisateurs de collaborer dans une réunion avec leur équipe au même endroit sans être séparés par des cases.</span><span class="sxs-lookup"><span data-stu-id="ca918-116">The new custom Together Mode scenes feature enables users to collaborate in a meeting with their team in one place without being separated by boxes.</span></span>

## <a name="see-also"></a><span data-ttu-id="ca918-117">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ca918-117">See also</span></span>

* [<span data-ttu-id="ca918-118">Tab</span><span class="sxs-lookup"><span data-stu-id="ca918-118">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="ca918-119">Bot</span><span class="sxs-lookup"><span data-stu-id="ca918-119">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="ca918-120">Extension de la messagerie</span><span class="sxs-lookup"><span data-stu-id="ca918-120">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="ca918-121">Concevoir votre application</span><span class="sxs-lookup"><span data-stu-id="ca918-121">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="ca918-122">Conditions préalables et références d’API pour les applications dans les réunions Teams</span><span class="sxs-lookup"><span data-stu-id="ca918-122">Prerequisites and API references for apps in Teams meetings</span></span>](create-apps-for-teams-meetings.md)
* [<span data-ttu-id="ca918-123">Scènes personnalisées du mode Ensemble</span><span class="sxs-lookup"><span data-stu-id="ca918-123">Custom Together Mode scenes</span></span>](~/apps-in-teams-meetings/teams-together-mode.md)

## <a name="next-step"></a><span data-ttu-id="ca918-124">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="ca918-124">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca918-125">Extensibilité de l’application de réunion</span><span class="sxs-lookup"><span data-stu-id="ca918-125">Meeting app extensibility</span></span>](meeting-app-extensibility.md)
