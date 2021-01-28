---
title: Fonctionnalités de la prévisualisation pour les développeurs publics
description: Détails des fonctionnalités de la prévisualisation du développeur public Microsoft Teams
ms.topic: reference
keywords: Teams prévisualiser les fonctionnalités de développement
ms.openlocfilehash: 3275ef7ac0d4ba052f417f6e852f48e2fdf267f5
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014354"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="f7412-104">Fonctionnalités de la prévisualisation pour les développeurs publics pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f7412-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="f7412-105">La prévisualisation pour développeurs inclut les nouvelles fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="f7412-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="f7412-106">Onglets sign-on (SSO)</span><span class="sxs-lookup"><span data-stu-id="f7412-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="f7412-107">Vous pouvez désormais utiliser l’authentification unique [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) pour vous connecter et authentifier un utilisateur sur ordinateur de bureau et mobile à l’aide du SDK JavaScript Teams à partir d’une page de contenu web.</span><span class="sxs-lookup"><span data-stu-id="f7412-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="f7412-108">L’un des avantages est qu’un utilisateur n’a jamais à se connecter ; et une fois qu’ils ont accepté l’application à l’aide de leur profil : ils sont automatiquement inscrits à leur onglet (y compris mobile).</span><span class="sxs-lookup"><span data-stu-id="f7412-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="f7412-109">Notre version préliminaire pour développeurs est disponible dans les versions de manifeste 1.5 et ultérieures.</span><span class="sxs-lookup"><span data-stu-id="f7412-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="f7412-110">Notre implémentation actuelle ne peut obtenir qu’une quantité limitée d’API Graph, mais nous fournissons une solution de contournement pour obtenir des API Graph supplémentaires à l’aide de notre API d’authentification existante.</span><span class="sxs-lookup"><span data-stu-id="f7412-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="f7412-111">Appels et bots de réunion en ligne</span><span class="sxs-lookup"><span data-stu-id="f7412-111">Calls and online meeting bots</span></span>

<span data-ttu-id="f7412-112">Avec l’ajout d’API Microsoft Graph pour les appels et les réunions en ligne, les applications Microsoft Teams peuvent désormais interagir avec les [utilisateurs](/graph/api/resources/communications-api-overview?view=graph-rest-beta)de manière enrichie à l’aide de la voix et de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="f7412-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="f7412-113">Ces API vous permettent d’ajouter de nouvelles fonctionnalités d’application telles que la réponse vocale interactive (IVR), le contrôle d’appel et l’accès aux flux audio et/ou vidéo en temps réel pour les appels et les réunions, y compris le partage de bureau et d’application.</span><span class="sxs-lookup"><span data-stu-id="f7412-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="f7412-114">Nous avons ajouté une nouvelle section sur la création et le développement d’appels et de bots de réunions en ligne, en commençant par la [vue d’ensemble.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f7412-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="f7412-115">Prise en charge de l’agrandissement de l’image</span><span class="sxs-lookup"><span data-stu-id="f7412-115">Image enlarge support</span></span>

<span data-ttu-id="f7412-116">Il est désormais possible pour les bots d’indiquer les images partagées dans les cartes adaptatives dans Teams qui sont autorisées à être agrandies.</span><span class="sxs-lookup"><span data-stu-id="f7412-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="f7412-117">Cela est utile pour les scénarios tels que le partage de guides visuels détaillés pas à pas via des bots qui peuvent être difficiles à lire pour les utilisateurs dans le cas contraire.</span><span class="sxs-lookup"><span data-stu-id="f7412-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="f7412-118">Pour rendre une image ex expandable, marquez-la `allowExpand: true` simplement comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f7412-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="f7412-119">Ainsi, le client web/de bureau Teams restituera un élément sur l’image pour permettre à l’utilisateur de développer l’image.</span><span class="sxs-lookup"><span data-stu-id="f7412-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

