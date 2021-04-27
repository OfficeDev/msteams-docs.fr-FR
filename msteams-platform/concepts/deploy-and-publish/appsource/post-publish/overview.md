---
title: Maintenance et prise en charge de votre application publiée
description: Que faire une fois que vous avez publié votre application
ms.topic: how-to
localization_priority: Normal
keywords: teams publient le manifeste de mise à jour de l'application de certification des mises à jour
ms.openlocfilehash: 11c32ce61664f34a246905124b767e17d3c6f536
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020799"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="d3027-104">Maintenir et prendre en charge votre application publiée</span><span class="sxs-lookup"><span data-stu-id="d3027-104">Maintain and support your published app</span></span> 

<span data-ttu-id="d3027-105">Une fois votre application approuvée et répertoriée dans le catalogue d'applications publiques, vous pouvez augmenter votre portée en complétant le programme de conformité des applications Microsoft 365 ou en ajoutant un bouton de téléchargement sur votre site web.</span><span class="sxs-lookup"><span data-stu-id="d3027-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="d3027-106">Certification Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="d3027-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="d3027-107">Le programme de conformité des applications [Microsoft 365](./application-certification.md), est une approche à trois niveaux pour la sécurité et la conformité des applications.</span><span class="sxs-lookup"><span data-stu-id="d3027-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="d3027-108">Chaque niveau s'appuie sur le suivant , offrant un programme en couches pour répondre aux besoins de votre client.</span><span class="sxs-lookup"><span data-stu-id="d3027-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="d3027-109">Vous pouvez en savoir plus sur la posture de sécurité et de conformité des applications Teams en visitant la [page de conformité.](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)</span><span class="sxs-lookup"><span data-stu-id="d3027-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="d3027-110">Ajouter un bouton de téléchargement à votre site de produit</span><span class="sxs-lookup"><span data-stu-id="d3027-110">Add a download button to your product site</span></span>

<span data-ttu-id="d3027-111">Si votre application se trouve dans le magasin global Microsoft Teams, vous pouvez générer un lien pour votre site web qui lance Teams et affiche une boîte de dialogue de consentement et d'installation pour que les utilisateurs ajoutent l'application.</span><span class="sxs-lookup"><span data-stu-id="d3027-111">If your app is in the Microsoft Teams global store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="d3027-112">Le format est :  `https://teams.microsoft.com/l/app/<appId>` où appID est le GUID qu'il déclare dans le manifeste envoyé.</span><span class="sxs-lookup"><span data-stu-id="d3027-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="d3027-113">Exemple : `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` est le lien vers l'installation de Trello.</span><span class="sxs-lookup"><span data-stu-id="d3027-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="d3027-114">Mise à jour de votre application Teams existante</span><span class="sxs-lookup"><span data-stu-id="d3027-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="d3027-115">N'utilisez pas *le bouton Ajouter une nouvelle application* pour resoumettre votre application.</span><span class="sxs-lookup"><span data-stu-id="d3027-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="d3027-116">Utilisez plutôt la vignette de votre application sous l'onglet Vue d'ensemble.</span><span class="sxs-lookup"><span data-stu-id="d3027-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="d3027-117">L'appId dans le manifeste mis à jour doit être le même que dans le manifeste actuel, avec un numéro de version incrémenté.</span><span class="sxs-lookup"><span data-stu-id="d3027-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="d3027-118">Incrémentez votre numéro de version dans le manifeste si vous a apporté des modifications à votre soumission, y compris le nom de l'application ou des métadonnées dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="d3027-118">Increment your version number in the manifest if you make any changes to your submission including app name or any metadata in the manifest.</span></span>
* <span data-ttu-id="d3027-119">Les soumissions mises à jour sont requises pour faire l'objet d'un nouveau processus de révision et de validation.</span><span class="sxs-lookup"><span data-stu-id="d3027-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="d3027-120">Mises à jour de l'application et flux de consentement de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="d3027-120">App updates and the user consent flow</span></span>

<span data-ttu-id="d3027-121">Lorsqu'un utilisateur installe votre application, l'une des premières choses qu'il fait est de donner à l'application l'autorisation d'accéder aux services et aux informations dont l'application a besoin pour faire son travail.</span><span class="sxs-lookup"><span data-stu-id="d3027-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="d3027-122">Dans la plupart des cas, une fois que vous avez terminé la mise à jour d'une application, la nouvelle version s'affiche automatiquement pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="d3027-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="d3027-123">Toutefois, certaines mises à jour du manifeste de l'application [Teams](../../../../resources/schema/manifest-schema.md) nécessitent l'acceptation de l'utilisateur et peuvent déclencher de nouvelles fois ce comportement de consentement :</span><span class="sxs-lookup"><span data-stu-id="d3027-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="d3027-124">Un bot est ajouté ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="d3027-124">A bot is added or removed.</span></span>
> * <span data-ttu-id="d3027-125">La valeur unique d'un bot `botId` existant est modifiée.</span><span class="sxs-lookup"><span data-stu-id="d3027-125">An existing bot's unique `botId` value is changed.</span></span>
> * <span data-ttu-id="d3027-126">La valeur booléle d'un bot `isNotificationOnly` existant est modifiée.</span><span class="sxs-lookup"><span data-stu-id="d3027-126">An existing bot's `isNotificationOnly` boolean value is changed.</span></span>
> * <span data-ttu-id="d3027-127">La valeur d'un bot `supportsFiles` ou d'un `supportsCalling` booléen existant est modifiée.</span><span class="sxs-lookup"><span data-stu-id="d3027-127">An existing bot's `supportsFiles` or `supportsCalling` boolean value is changed.</span></span>
> * <span data-ttu-id="d3027-128">Une extension de `composeExtensions` messagerie est ajoutée ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="d3027-128">A messaging extension `composeExtensions` is added or removed.</span></span>
> * <span data-ttu-id="d3027-129">Un nouveau connecteur est ajouté.</span><span class="sxs-lookup"><span data-stu-id="d3027-129">A new connector is added.</span></span>
> * <span data-ttu-id="d3027-130">Un nouvel onglet statique ou personnel est ajouté.</span><span class="sxs-lookup"><span data-stu-id="d3027-130">A new static or personal tab is added.</span></span>
> * <span data-ttu-id="d3027-131">Un nouvel onglet de groupe ou de canal configurable est ajouté.</span><span class="sxs-lookup"><span data-stu-id="d3027-131">A new configurable group or channel tab is added.</span></span>
> * <span data-ttu-id="d3027-132">Les propriétés à `webApplicationInfo` l'intérieur sont modifiées.</span><span class="sxs-lookup"><span data-stu-id="d3027-132">The properties inside `webApplicationInfo` are changed.</span></span> <span data-ttu-id="d3027-133">Pour les modifications `webApplicationInfo` apportées à , le consentement est uniquement requis dans l'étendue Teams.</span><span class="sxs-lookup"><span data-stu-id="d3027-133">For changes to `webApplicationInfo`, consent is only required in the Teams scope.</span></span>

### <a name="images-of-user-consent-flow"></a><span data-ttu-id="d3027-134">Images du flux de consentement de l'utilisateur :</span><span class="sxs-lookup"><span data-stu-id="d3027-134">Images of user consent flow:</span></span>

<span data-ttu-id="d3027-135">**Configurer un connecteur : cet** écran s'affiche uniquement pour les utilisateurs de Teams.</span><span class="sxs-lookup"><span data-stu-id="d3027-135">**Set up a connector** —  This screen will appear only for Teams users.</span></span>

![Configuration du flux de consentement d'un diagramme de connecteur](../../../../assets/images/connector-teams-consentflow.png)

<span data-ttu-id="d3027-137">**Flux de consentement utilisateur** : cet écran est courant pour les étendues personnelle et de groupe.</span><span class="sxs-lookup"><span data-stu-id="d3027-137">**User consent flow** - This screen is common for both personal and group scope.</span></span> <span data-ttu-id="d3027-138">Ici, sélectionnez la case **à cocher Consentement** au nom de votre organisation et choisissez **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="d3027-138">Here, select the **Consent on behalf of your organization** checkbox and choose **Accept**.</span></span>

![Diagramme des autorisations](../../../../assets/images/user-consent-flow.png)
