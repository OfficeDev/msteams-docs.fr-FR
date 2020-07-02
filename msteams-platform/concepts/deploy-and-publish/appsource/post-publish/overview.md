---
title: Publication post
description: Ce qu’il faut faire après avoir publié votre application
keywords: teams post publier le certificat de mise à jour
ms.openlocfilehash: 887e18ac7e27cf12aa4319ac240e42f21f05fd75
ms.sourcegitcommit: e355f59d2d21a2d5ae36cc46acad5ed4765b42e0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2020
ms.locfileid: "45021572"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="2989d-104">Gérer et prendre en charge votre application publiée</span><span class="sxs-lookup"><span data-stu-id="2989d-104">Maintain and support your published app</span></span> 

<span data-ttu-id="2989d-105">Une fois que votre application est approuvée et inscrite dans le catalogue d’applications public, vous pouvez augmenter votre portée en terminant le programme de conformité des applications Microsoft 365 ou en ajoutant un bouton Télécharger sur votre site Web.</span><span class="sxs-lookup"><span data-stu-id="2989d-105">After your app is approved and listed in the public app catalog, you can increase your reach by completing the Microsoft 365 App Compliance Program or by adding a download button on your website.</span></span>

## <a name="m365-certified"></a><span data-ttu-id="2989d-106">Certification M365</span><span class="sxs-lookup"><span data-stu-id="2989d-106">M365 Certified</span></span>

<span data-ttu-id="2989d-107">Le [programme de conformité des applications Microsoft 365](./application-certification.md)est une approche à trois niveaux de la sécurité et de la conformité des applications.</span><span class="sxs-lookup"><span data-stu-id="2989d-107">The [Microsoft 365 App Compliance Program](./application-certification.md), is a three tier approach to app security and compliance.</span></span> <span data-ttu-id="2989d-108">Chaque niveau est basé sur le suivant : Offrez un programme en couches pour répondre aux besoins de vos clients.</span><span class="sxs-lookup"><span data-stu-id="2989d-108">Each tier builds upon the next – offering a layered program to meet your customer’s needs.</span></span> <span data-ttu-id="2989d-109">Pour en savoir plus sur la sécurité et la conformité des applications Teams, consultez la [page conformité](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span><span class="sxs-lookup"><span data-stu-id="2989d-109">You can learn more about the security and compliance posture of Teams apps by visiting the [compliance page](https://docs.microsoft.com/microsoft-365-app-certification/teams/teams-apps).</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="2989d-110">Ajouter un bouton de téléchargement à votre site de produit</span><span class="sxs-lookup"><span data-stu-id="2989d-110">Add a download button to your product site</span></span>

<span data-ttu-id="2989d-111">Si votre application se trouve dans le magasin Microsoft Teams, vous pouvez générer un lien vers votre site Web qui lance teams et affiche une boîte de dialogue de consentement et d’installation pour permettre aux utilisateurs d’ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2989d-111">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="2989d-112">Le format est : `https://teams.microsoft.com/l/app/<appId>` où AppID est le GUID qu’il déclare dans le manifeste soumis.</span><span class="sxs-lookup"><span data-stu-id="2989d-112">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="2989d-113">Exemple : `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` est le lien pour installer Trello.</span><span class="sxs-lookup"><span data-stu-id="2989d-113">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="2989d-114">Mise à jour de votre application teams existante</span><span class="sxs-lookup"><span data-stu-id="2989d-114">Updating your existing Teams app</span></span>

* <span data-ttu-id="2989d-115">N’utilisez pas le bouton *Ajouter une nouvelle application* pour renvoyer votre application.</span><span class="sxs-lookup"><span data-stu-id="2989d-115">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="2989d-116">Utilisez plutôt la mosaïque de votre application sous l’onglet vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="2989d-116">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="2989d-117">L’appId dans le manifeste mis à jour doit être le même que dans le manifeste actuel, avec un numéro de version incrémentiel.</span><span class="sxs-lookup"><span data-stu-id="2989d-117">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="2989d-118">Incrémentez votre numéro de version dans le manifeste si vous effectuez des modifications de manifeste dans votre envoi.</span><span class="sxs-lookup"><span data-stu-id="2989d-118">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="2989d-119">Les soumissions mises à jour doivent être soumises à un nouveau processus de révision et de validation.</span><span class="sxs-lookup"><span data-stu-id="2989d-119">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="2989d-120">Mises à jour de l’application et flux de consentement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="2989d-120">App updates and the user consent flow</span></span>

<span data-ttu-id="2989d-121">Lorsqu’un utilisateur installe votre application, il est autorisé à accorder à l’application l’autorisation d’accéder aux services et informations dont elle a besoin pour faire son travail.</span><span class="sxs-lookup"><span data-stu-id="2989d-121">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="2989d-122">Dans la plupart des cas, une fois que vous avez terminé une mise à jour de l’application, la nouvelle version s’affiche automatiquement pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="2989d-122">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="2989d-123">Toutefois, certaines mises à jour du manifeste de l' [application teams](../../../../resources/schema/manifest-schema.md) nécessitent l’acceptation de l’utilisateur et peuvent déclencher à nouveau ce comportement de consentement :</span><span class="sxs-lookup"><span data-stu-id="2989d-123">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="2989d-124">Un bot a été ajouté ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="2989d-124">A bot was added or removed.</span></span>
> * <span data-ttu-id="2989d-125">La valeur unique d’un bot existant `botId` a changé.</span><span class="sxs-lookup"><span data-stu-id="2989d-125">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="2989d-126">La valeur booléenne d’un bot existant `isNotificationOnly` a changé.</span><span class="sxs-lookup"><span data-stu-id="2989d-126">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="2989d-127">La valeur booléenne d’un bot existant `supportsFiles` a changé.</span><span class="sxs-lookup"><span data-stu-id="2989d-127">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="2989d-128">Une extension de messagerie ( `composeExtensions` ) a été ajoutée ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="2989d-128">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="2989d-129">Un nouveau connecteur a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="2989d-129">A new connector was added.</span></span>
> * <span data-ttu-id="2989d-130">Un nouvel onglet statique/personnel a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="2989d-130">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="2989d-131">Un nouvel onglet de groupe/canal configurable a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="2989d-131">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="2989d-132">Les `webApplicationInfo` valeurs ont changé.</span><span class="sxs-lookup"><span data-stu-id="2989d-132">The `webApplicationInfo` values changed.</span></span>
>
