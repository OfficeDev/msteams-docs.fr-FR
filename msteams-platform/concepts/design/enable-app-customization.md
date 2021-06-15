---
title: Activer la personnalisation de votre application
author: heath-hamilton
description: Comprendre comment Teams administrateurs peuvent personnaliser votre application pour leur organisation.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: bf1b43629c87dd4123520c634772e5dea14e0bb5
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915082"
---
# <a name="enable-your-microsoft-teams-app-to-be-customized"></a><span data-ttu-id="09fa7-103">Activer la personnalisation Microsoft Teams votre application</span><span class="sxs-lookup"><span data-stu-id="09fa7-103">Enable your Microsoft Teams app to be customized</span></span>

<span data-ttu-id="09fa7-104">Vous pouvez permettre aux clients de personnaliser certains aspects de votre application Microsoft Teams dans le centre d’administration Teams client.</span><span class="sxs-lookup"><span data-stu-id="09fa7-104">You can allow customers to customize some aspects of your Microsoft Teams app in the Teams admin center.</span></span> <span data-ttu-id="09fa7-105">Cette fonctionnalité est prise en charge uniquement pour les applications publiées dans Teams store.</span><span class="sxs-lookup"><span data-stu-id="09fa7-105">This feature is supported only for apps published to the Teams store.</span></span> <span data-ttu-id="09fa7-106">Les applications et les applications téléchargées de côté publiées pour une organisation ne peuvent pas être personnalisées.</span><span class="sxs-lookup"><span data-stu-id="09fa7-106">Sideloaded apps and apps published for an org can't be customized.</span></span>

<span data-ttu-id="09fa7-107">Voici quelques exemples possibles de cette fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="09fa7-107">Some possible examples of this feature include:</span></span>

* <span data-ttu-id="09fa7-108">Modification de la couleur d’accentuage de l’application pour qu’elle corresponde à la marque d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="09fa7-108">Changing the app's accent color to match an org's brand.</span></span>
* <span data-ttu-id="09fa7-109">Mise à jour du nom de l’application de *Contoso* vers *l’agent Contoso*, qui est le nom que les utilisateurs de l’organisation voient.</span><span class="sxs-lookup"><span data-stu-id="09fa7-109">Updating the app name from *Contoso* to *Contoso Agent*, which is the name users in the org will see.</span></span> <span data-ttu-id="09fa7-110">(Remarque : les utilisateurs qui ajoutent un connecteur à une conversation ou un canal voient toujours le nom de l’application d’origine, *Contoso.)*</span><span class="sxs-lookup"><span data-stu-id="09fa7-110">(Note: Users adding a connector to a chat or a channel will still see the original app name, *Contoso*.)</span></span>

<span data-ttu-id="09fa7-111">Vous pouvez activer cette fonctionnalité dans le Portail des développeurs [pour Teams](https://dev.teams.microsoft.com/home).</span><span class="sxs-lookup"><span data-stu-id="09fa7-111">You can enable this feature in the [Developer Portal for Teams](https://dev.teams.microsoft.com/home).</span></span> <span data-ttu-id="09fa7-112">Cette configuration, qui ne sont pas disponibles dans les versions antérieures à `configurableProperties` la version 1.10 du manifeste Teams’application.</span><span class="sxs-lookup"><span data-stu-id="09fa7-112">This configures `configurableProperties`, which aren't available in versions prior to 1.10 of the Teams app manifest.</span></span>

## <a name="test-your-app"></a><span data-ttu-id="09fa7-113">Tester votre application</span><span class="sxs-lookup"><span data-stu-id="09fa7-113">Test your app</span></span>

<span data-ttu-id="09fa7-114">Vous ne pouvez pas tester cette fonctionnalité pendant le développement.</span><span class="sxs-lookup"><span data-stu-id="09fa7-114">You cannot test this feature during development.</span></span> <span data-ttu-id="09fa7-115">La personnalisation d’application n’est pas prise en charge pour le chargement de version de version ou la publication dans le catalogue d’applications d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="09fa7-115">App customization is not supported for sideloading or publishing to an organization's app catalog.</span></span>

## <a name="user-considerations"></a><span data-ttu-id="09fa7-116">Considérations sur les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="09fa7-116">User considerations</span></span>

<span data-ttu-id="09fa7-117">En tant qu’éditeur d’application, fournissez les informations suivantes aux clients Teams administrateurs :</span><span class="sxs-lookup"><span data-stu-id="09fa7-117">As the app publisher, provide the following information to customers in Teams admins:</span></span>
* <span data-ttu-id="09fa7-118">Incluez une note recommandant de tester les modifications de personnalisation dans un client Teams test avant d’apporter des modifications dans son environnement de production.</span><span class="sxs-lookup"><span data-stu-id="09fa7-118">Include a note recommending to test customization changes in a Teams test tenant before making changes in their production environment.</span></span> 
* <span data-ttu-id="09fa7-119">Fournissez les meilleures pratiques pour personnaliser votre application.</span><span class="sxs-lookup"><span data-stu-id="09fa7-119">Provide best practices for how to customize your app.</span></span>

## <a name="see-also"></a><span data-ttu-id="09fa7-120">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="09fa7-120">See also</span></span>

* [<span data-ttu-id="09fa7-121">Personnaliser des applications dans le Centre d Teams’administration Windows</span><span class="sxs-lookup"><span data-stu-id="09fa7-121">Customize apps in the Teams admin center</span></span>](/MicrosoftTeams/customize-apps)
