---
title: Applications pour Teams réunions
author: laujan
description: vue d’ensemble des applications dans Teams réunions basées sur le rôle des participants et des utilisateurs
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: Api de rôle d’utilisateur participant aux réunions teams apps
ms.openlocfilehash: 1fdf3d55219d80d6953ffa0865b223dd626053f6
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649663"
---
# <a name="apps-for-teams-meetings"></a><span data-ttu-id="a8aa6-104">Applications pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="a8aa6-104">Apps for Teams meetings</span></span>

<span data-ttu-id="a8aa6-105">Les réunions permettent la collaboration, le partenariat, la communication éclairée et les commentaires partagés dans un forum actif et inclusif.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="a8aa6-106">L’application de réunion peut offrir une expérience utilisateur pour chaque étape du cycle de vie de la réunion, y compris l’expérience de pré-réunion, de réunion et d’application post-réunion, en fonction de l’état du participant.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting, and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="a8aa6-107">Les utilisateurs peuvent accéder aux applications pendant les réunions à l’aide de la galerie d’onglets, par exemple :</span><span class="sxs-lookup"><span data-stu-id="a8aa6-107">The users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="a8aa6-108">Pré-préparation d’un tableau kanban.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-108">Pre-stage a Kanban board.</span></span>
* <span data-ttu-id="a8aa6-109">Lancez une boîte de dialogue actionnable en réunion.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-109">Launch an in-meeting actionable dialog.</span></span>
* <span data-ttu-id="a8aa6-110">Créer une enquête post-réunion.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-110">Create a post-meeting survey.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/nKAy5rNDus4]

<span data-ttu-id="a8aa6-111">Cet article fournit une vue d’ensemble de l’extensibilité des applications de réunion, des références d’API, de l’activer et de la configurer pour les réunions et du mode Ensemble dans Teams.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-111">This article provides an overview of meeting app extensibility, API references, enable and configure apps for meetings, and Together Mode in Teams.</span></span>

<span data-ttu-id="a8aa6-112">Vous pouvez améliorer votre expérience de réunion à l’aide de la fonctionnalité d’extensibilité de réunion, qui vous permet d’intégrer vos applications dans les réunions.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-112">You can enhance your meeting experience by using the meeting extensibility feature, which enables you to integrate your apps within meetings.</span></span> <span data-ttu-id="a8aa6-113">Il inclut également différentes étapes d’un cycle de vie de réunion, où vous pouvez intégrer des onglets, des bots et des extensions de messagerie.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-113">It also includes different stages of a meeting lifecycle, where you can integrate tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="a8aa6-114">Avec les API d’extensibilité des réunions, vous pouvez identifier différents rôles de participants et types d’utilisateurs, obtenir des événements de réunion, générer des boîtes de dialogue en réunion, etc.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-114">With meetings extensibility APIs, you can identify different participant roles and user types, get meeting events, generate in-meeting dialogs, and so on.</span></span>

<span data-ttu-id="a8aa6-115">Pour personnaliser les Teams avec des applications pour les réunions, vous pouvez activer vos applications pour les réunions Teams en mettant à jour votre manifeste d’application et vous pouvez également configurer vos applications pour les scénarios de réunion.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-115">To customize Teams with apps for meetings, you can enable your apps for Teams meetings by updating your app manifest and you can also configure your apps for meeting scenarios.</span></span>

<span data-ttu-id="a8aa6-116">La nouvelle fonctionnalité mode Ensemble permet aux utilisateurs de collaborer à une réunion avec leur équipe au même endroit sans être séparés par des cases.</span><span class="sxs-lookup"><span data-stu-id="a8aa6-116">The new Together Mode feature enables users to collaborate in a meeting with their team in one place without being separated by boxes.</span></span>

## <a name="see-also"></a><span data-ttu-id="a8aa6-117">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a8aa6-117">See also</span></span>

* [<span data-ttu-id="a8aa6-118">Tab</span><span class="sxs-lookup"><span data-stu-id="a8aa6-118">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="a8aa6-119">Bot</span><span class="sxs-lookup"><span data-stu-id="a8aa6-119">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="a8aa6-120">Extension de la messagerie</span><span class="sxs-lookup"><span data-stu-id="a8aa6-120">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="a8aa6-121">Concevoir votre application</span><span class="sxs-lookup"><span data-stu-id="a8aa6-121">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="a8aa6-122">Conditions préalables et références d’API pour les applications Teams réunions</span><span class="sxs-lookup"><span data-stu-id="a8aa6-122">Prerequisites and API references for apps in Teams meetings</span></span>](create-apps-for-teams-meetings.md)
* [<span data-ttu-id="a8aa6-123">Mode Ensemble</span><span class="sxs-lookup"><span data-stu-id="a8aa6-123">Together Mode</span></span>](~/apps-in-teams-meetings/teams-together-mode.md)

## <a name="next-step"></a><span data-ttu-id="a8aa6-124">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="a8aa6-124">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a8aa6-125">Extensibilité des applications de réunion</span><span class="sxs-lookup"><span data-stu-id="a8aa6-125">Meeting app extensibility</span></span>](meeting-app-extensibility.md)
