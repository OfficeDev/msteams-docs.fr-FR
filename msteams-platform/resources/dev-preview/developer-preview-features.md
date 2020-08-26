---
title: Fonctionnalités de l’aperçu public pour les développeurs
description: Détails des fonctionnalités de Microsoft teams public developer preview
keywords: fonctionnalités de développeur d’aperçu teams
ms.openlocfilehash: 773e0334bddf45b7b86d31329b99607f3b70c534
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874841"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="1f448-104">Fonctionnalités de l’aperçu public pour les développeurs pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="1f448-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="1f448-105">L’aperçu des développeurs inclut les nouvelles fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="1f448-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="1f448-106">Authentification unique (SSO) des onglets</span><span class="sxs-lookup"><span data-stu-id="1f448-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="1f448-107">Vous pouvez désormais utiliser l’authentification [unique (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) pour vous connecter et authentifier un utilisateur sur un ordinateur de bureau et un appareil mobile à l’aide du kit de développement logiciel (SDK) JavaScript teams à partir d’une page de contenu Web.</span><span class="sxs-lookup"><span data-stu-id="1f448-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="1f448-108">L’un des avantages est qu’un utilisateur n’a jamais à se connecter ; et une fois qu’ils ont accepté l’application à l’aide de leur profil : ils sont automatiquement connectés à leur onglet (y compris mobile).</span><span class="sxs-lookup"><span data-stu-id="1f448-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="1f448-109">Notre Aperçu pour les développeurs est disponible dans les versions de manifeste 1,5 et ultérieure.</span><span class="sxs-lookup"><span data-stu-id="1f448-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="1f448-110">Notre implémentation actuelle peut uniquement obtenir une quantité limitée d’API Graph, mais nous fournissons une solution de contournement pour obtenir des API Graph supplémentaires à l’aide de notre API d’authentification existante.</span><span class="sxs-lookup"><span data-stu-id="1f448-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="1f448-111">Appels et robots de réunion en ligne</span><span class="sxs-lookup"><span data-stu-id="1f448-111">Calls and online meeting bots</span></span>

<span data-ttu-id="1f448-112">Avec l’ajout d' [API Microsoft Graph pour les appels et les réunions en ligne](/graph/api/resources/communications-api-overview?view=graph-rest-beta), les applications Microsoft teams peuvent désormais interagir avec les utilisateurs de façon enrichie à l’aide de la voix et de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="1f448-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="1f448-113">Ces API vous permettent d’ajouter de nouvelles fonctionnalités d’application, telles que la réponse vocale interactive (IVR), le contrôle d’appel et l’accès à des flux audio et/ou vidéo en temps réel pour les appels et les réunions, y compris le partage de bureau et d’application.</span><span class="sxs-lookup"><span data-stu-id="1f448-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="1f448-114">Nous avons ajouté une nouvelle section sur la façon de créer et de développer des appels et des robots de réunions en ligne, en commençant par la [vue d’ensemble](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f448-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="1f448-115">Prise en charge de l’image</span><span class="sxs-lookup"><span data-stu-id="1f448-115">Image enlarge support</span></span>

<span data-ttu-id="1f448-116">Il est désormais possible pour les robots d’indiquer les images partagées dans les cartes adaptatives de teams qui peuvent être agrandies.</span><span class="sxs-lookup"><span data-stu-id="1f448-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="1f448-117">Cela est utile pour des scénarios tels que le partage de guides détaillés pas à pas via des robots qui pourraient être difficiles à lire pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1f448-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="1f448-118">Pour qu’une image soit extensible, il vous suffit de la marquer `allowExpand: true` comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1f448-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="1f448-119">Cela entraînera le rendu par le client teams Web/de bureau d’un élément sur l’image pour permettre à l’utilisateur de développer l’image.</span><span class="sxs-lookup"><span data-stu-id="1f448-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

