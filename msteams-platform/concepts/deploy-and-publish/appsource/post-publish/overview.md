---
title: Publication post
description: Ce qu’il faut faire après avoir publié votre application
keywords: teams post publier le certificat de mise à jour
ms.openlocfilehash: 77b74d77546de0ae93b0ae39aec925d2e3dec2cf
ms.sourcegitcommit: fdc50183f3f4bec9e4b83bcfe5e016b591402f7c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/24/2020
ms.locfileid: "44867092"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="12fd8-104">Gérer et prendre en charge votre application publiée</span><span class="sxs-lookup"><span data-stu-id="12fd8-104">Maintain and support your published app</span></span> 

<span data-ttu-id="12fd8-105">Une fois que votre application est approuvée et inscrite dans le catalogue d’applications public, vous pouvez augmenter votre portée en obtenant la certification de l’application ou en ajoutant un bouton de téléchargement de votre site Web.</span><span class="sxs-lookup"><span data-stu-id="12fd8-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="12fd8-106">Certificat d’application</span><span class="sxs-lookup"><span data-stu-id="12fd8-106">Application Certificate</span></span>

<span data-ttu-id="12fd8-107">Microsoft fournit un [programme de certification d’application](./application-certification.md) qui compile vos informations d’application et les présente sur la [page de sécurité et de conformité des applications Microsoft teams](https://aka.ms/AppCertification).</span><span class="sxs-lookup"><span data-stu-id="12fd8-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="12fd8-108">Ces informations visent à aider les administrateurs à choisir les applications qui sont sûres pour leur organisation.</span><span class="sxs-lookup"><span data-stu-id="12fd8-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="12fd8-109">Ajouter un bouton de téléchargement à votre site de produit</span><span class="sxs-lookup"><span data-stu-id="12fd8-109">Add a download button to your product site</span></span>

<span data-ttu-id="12fd8-110">Si votre application se trouve dans le magasin Microsoft Teams, vous pouvez générer un lien vers votre site Web qui lance teams et affiche une boîte de dialogue de consentement et d’installation pour permettre aux utilisateurs d’ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="12fd8-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="12fd8-111">Le format est : `https://teams.microsoft.com/l/app/<appId>` où AppID est le GUID qu’il déclare dans le manifeste soumis.</span><span class="sxs-lookup"><span data-stu-id="12fd8-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="12fd8-112">Exemple : `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` est le lien pour installer Trello.</span><span class="sxs-lookup"><span data-stu-id="12fd8-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="12fd8-113">Mise à jour de votre application teams existante</span><span class="sxs-lookup"><span data-stu-id="12fd8-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="12fd8-114">N’utilisez pas le bouton *Ajouter une nouvelle application* pour renvoyer votre application.</span><span class="sxs-lookup"><span data-stu-id="12fd8-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="12fd8-115">Utilisez plutôt la mosaïque de votre application sous l’onglet vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="12fd8-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="12fd8-116">L’appId dans le manifeste mis à jour doit être le même que dans le manifeste actuel, avec un numéro de version incrémentiel.</span><span class="sxs-lookup"><span data-stu-id="12fd8-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="12fd8-117">Incrémentez votre numéro de version dans le manifeste si vous effectuez des modifications de manifeste dans votre envoi.</span><span class="sxs-lookup"><span data-stu-id="12fd8-117">Increment your version number in the manifest if you make any manifest changes to your submission.</span></span>
* <span data-ttu-id="12fd8-118">Les soumissions mises à jour doivent être soumises à un nouveau processus de révision et de validation.</span><span class="sxs-lookup"><span data-stu-id="12fd8-118">Updated submissions are required to undergo a new review and validation process.</span></span>

## <a name="app-updates-and-the-user-consent-flow"></a><span data-ttu-id="12fd8-119">Mises à jour de l’application et flux de consentement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="12fd8-119">App updates and the user consent flow</span></span>

<span data-ttu-id="12fd8-120">Lorsqu’un utilisateur installe votre application, il est autorisé à accorder à l’application l’autorisation d’accéder aux services et informations dont elle a besoin pour faire son travail.</span><span class="sxs-lookup"><span data-stu-id="12fd8-120">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="12fd8-121">Dans la plupart des cas, une fois que vous avez terminé une mise à jour de l’application, la nouvelle version s’affiche automatiquement pour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="12fd8-121">In most cases, after you complete an app update the new version will automatically appear for end users.</span></span> <span data-ttu-id="12fd8-122">Toutefois, certaines mises à jour du manifeste de l' [application teams](../../../../resources/schema/manifest-schema.md) nécessitent l’acceptation de l’utilisateur et peuvent déclencher à nouveau ce comportement de consentement :</span><span class="sxs-lookup"><span data-stu-id="12fd8-122">However, there are some updates to the [Teams app manifest](../../../../resources/schema/manifest-schema.md) that require user acceptance to complete and can re-trigger this consent behavior:</span></span>

 >[!div class="checklist"]
>
> * <span data-ttu-id="12fd8-123">Un bot a été ajouté ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="12fd8-123">A bot was added or removed.</span></span>
> * <span data-ttu-id="12fd8-124">La valeur unique d’un bot existant `botId` a changé.</span><span class="sxs-lookup"><span data-stu-id="12fd8-124">An existing bot's unique `botId` value changed.</span></span>
> * <span data-ttu-id="12fd8-125">La valeur booléenne d’un bot existant `isNotificationOnly` a changé.</span><span class="sxs-lookup"><span data-stu-id="12fd8-125">An existing bot's `isNotificationOnly` boolean value changed.</span></span>
> * <span data-ttu-id="12fd8-126">La valeur booléenne d’un bot existant `supportsFiles` a changé.</span><span class="sxs-lookup"><span data-stu-id="12fd8-126">An existing bot's `supportsFiles` boolean value changed.</span></span>
> * <span data-ttu-id="12fd8-127">Une extension de messagerie ( `composeExtensions` ) a été ajoutée ou supprimée.</span><span class="sxs-lookup"><span data-stu-id="12fd8-127">A messaging extension (`composeExtensions`) was added or removed.</span></span>
> * <span data-ttu-id="12fd8-128">Un nouveau connecteur a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="12fd8-128">A new connector was added.</span></span>
> * <span data-ttu-id="12fd8-129">Un nouvel onglet statique/personnel a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="12fd8-129">A new static/personal tab was added.</span></span>
> * <span data-ttu-id="12fd8-130">Un nouvel onglet de groupe/canal configurable a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="12fd8-130">A new configurable group/channel tab was added.</span></span>
> * <span data-ttu-id="12fd8-131">Les `webApplicationInfo` valeurs ont changé.</span><span class="sxs-lookup"><span data-stu-id="12fd8-131">The `webApplicationInfo` values changed.</span></span>
>