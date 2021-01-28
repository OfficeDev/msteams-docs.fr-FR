---
title: Maintenance et prise en charge de votre application publiée
description: Que faire une fois que vous avez publié votre application
ms.topic: how-to
keywords: teams publient le manifeste de mise à jour de l’application de certification des mises à jour
ms.openlocfilehash: ce63b840307f7e12a5cd05a1c67aed017cf6199b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014326"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="2720c-104">Maintenir et prendre en charge votre application publiée</span><span class="sxs-lookup"><span data-stu-id="2720c-104">Maintain and support your published app</span></span> 

<span data-ttu-id="2720c-105">Une fois votre application approuvée et répertoriée dans le catalogue d’applications publiques, vous pouvez augmenter votre portée en complétant le programme de conformité des applications Microsoft 365 ou en ajoutant un bouton de téléchargement sur votre site web.</span><span class="sxs-lookup"><span data-stu-id="2720c-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="microsoft-365-certified"></a><span data-ttu-id="2720c-106">Certification Microsoft 365</span><span class="sxs-lookup"><span data-stu-id="2720c-106">Microsoft 365 Certified</span></span>

<span data-ttu-id="2720c-107">Le programme de conformité des applications [Microsoft 365](./application-certification.md), est une approche à trois niveaux pour la sécurité et la conformité des applications.</span><span class="sxs-lookup"><span data-stu-id="2720c-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="2720c-108">Chaque niveau s’appuie sur le suivant , offrant un programme en couches pour répondre aux besoins de votre client.</span><span class="sxs-lookup"><span data-stu-id="2720c-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="2720c-109">Vous pouvez en savoir plus sur la posture de sécurité et de conformité des applications Teams en visitant la [page de conformité.](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps)</span><span class="sxs-lookup"><span data-stu-id="2720c-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="2720c-110">Ajouter un bouton de téléchargement à votre site de produit</span><span class="sxs-lookup"><span data-stu-id="2720c-110">Add a download button to your product site</span></span>

<span data-ttu-id="2720c-111">Si votre application se trouve dans le magasin global Microsoft Teams, vous pouvez générer un lien pour votre site web qui lance Teams et affiche une boîte de dialogue de consentement et d’installation pour que les utilisateurs ajoutent l’application.</span><span class="sxs-lookup"><span data-stu-id="2720c-111">If your app is in the Microsoft Teams global store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="2720c-112">Le format est :  `https://teams.microsoft.com/l/app/<appId>` où appID est le GUID qu’il déclare dans le manifeste envoyé.</span><span class="sxs-lookup"><span data-stu-id="2720c-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="2720c-113">Exemple : `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` est le lien vers l’installation de Trello.</span><span class="sxs-lookup"><span data-stu-id="2720c-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="2720c-114">Mise à jour de votre application Teams existante</span><span class="sxs-lookup"><span data-stu-id="2720c-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="2720c-115">N’utilisez pas *le bouton Ajouter une nouvelle application* pour resoumettre votre application.</span><span class="sxs-lookup"><span data-stu-id="2720c-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="2720c-116">Utilisez plutôt la vignette de votre application sous l’onglet Vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="2720c-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="2720c-117">L’appId dans le manifeste mis à jour doit être le même que dans le manifeste actuel, avec un numéro de version incrémenté.</span><span class="sxs-lookup"><span data-stu-id="2720c-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="2720c-118">Incrémentez votre numéro de version dans le manifeste si vous a apporté des modifications à votre soumission, y compris le nom de l’application ou des métadonnées dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="2720c-118">Increment your version number in the manifest if you make any changes to your submission including app name or any metadata in the manifest.</span></span>
* <span data-ttu-id="2720c-119">Les soumissions mises à jour sont requises pour faire l’objet d’un nouveau processus de révision et de validation.</span><span class="sxs-lookup"><span data-stu-id="2720c-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="2720c-120">Mises à jour de l’application et flux de consentement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2720c-120">App updates and the user consent flow</span></span>

<span data-ttu-id="2720c-121">Lorsqu’un utilisateur installe votre application, l’une des premières choses qu’il fait est de donner à l’application l’autorisation d’accéder aux services et aux informations dont l’application a besoin pour faire son travail.</span><span class="sxs-lookup"><span data-stu-id="2720c-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="2720c-122">Dans la plupart des cas, une fois que vous avez terminé la mise à jour d’une application, la nouvelle version s’affiche automatiquement pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="2720c-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="2720c-123">Toutefois, certaines mises à jour du manifeste de l’application [Teams](../../../../resources/schema/manifest-schema.md) nécessitent l’acceptation de l’utilisateur et peuvent déclencher ce comportement de consentement :</span><span class="sxs-lookup"><span data-stu-id="2720c-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="2720c-124">Un bot a été ajouté ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="2720c-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="2720c-125">La valeur unique d’un bot existant a `botId` changé.</span><span class="sxs-lookup"><span data-stu-id="2720c-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="2720c-126">La valeur booléle d’un bot `isNotificationOnly` existant a changé.</span><span class="sxs-lookup"><span data-stu-id="2720c-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="2720c-127">La valeur booléle d’un bot `supportsFiles` existant a changé.</span><span class="sxs-lookup"><span data-stu-id="2720c-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="2720c-128">Une extension de messagerie ( `composeExtensions` ) a été ajoutée ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="2720c-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="2720c-129">Un nouveau connecteur a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="2720c-129">A new connector was added.</span></span>
> * <span data-ttu-id="2720c-130">Un nouvel onglet statique/personnel a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="2720c-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="2720c-131">Un nouvel onglet groupe/canal configurable a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="2720c-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="2720c-132">Les `webApplicationInfo` valeurs ont changé.</span><span class="sxs-lookup"><span data-stu-id="2720c-132">The `webApplicationInfo` values changed.</span></span>
>

### <a name="images-of-user-consent-flow"></a><span data-ttu-id="2720c-133">Images du flux de consentement de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="2720c-133">Images of user consent flow:</span></span>

<span data-ttu-id="2720c-134">**Configurer un connecteur : cet** écran s’affiche uniquement pour les utilisateurs de Teams.</span><span class="sxs-lookup"><span data-stu-id="2720c-134">**Set up a connector** —  This screen will appear only for Teams users.</span></span>

![Configuration du flux de consentement d’un diagramme de connecteur](../../../../assets/images/connector-teams-consentflow.png)

<span data-ttu-id="2720c-136">**Flux de consentement utilisateur** : cet écran est courant pour les étendues personnelle et de groupe.</span><span class="sxs-lookup"><span data-stu-id="2720c-136">**User consent flow** - This screen is common for both personal and group scope.</span></span> <span data-ttu-id="2720c-137">Ici, sélectionnez la case **à cocher Consentement** au nom de votre organisation et choisissez **Accepter**.</span><span class="sxs-lookup"><span data-stu-id="2720c-137">Here, select the **Consent on behalf of your organization** checkbox and choose **Accept**.</span></span>

![Diagramme des autorisations](../../../../assets/images/user-consent-flow.png)
