---
title: Publication post
description: Ce qu’il faut faire après avoir publié votre application
keywords: teams post publier le certificat de mise à jour
ms.openlocfilehash: 05e4ea47bbf81967ccf086230bf0ad8c633f6e0b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673633"
---
# <a name="maintain-and-support-your-published-app"></a><span data-ttu-id="2f906-104">Gérer et prendre en charge votre application publiée</span><span class="sxs-lookup"><span data-stu-id="2f906-104">Maintain and support your published app</span></span> 

<span data-ttu-id="2f906-105">Une fois que votre application est approuvée et inscrite dans le catalogue d’applications public, vous pouvez augmenter votre portée en obtenant la certification de l’application ou en ajoutant un bouton de téléchargement de votre site Web.</span><span class="sxs-lookup"><span data-stu-id="2f906-105">After your app is approved and listed in the public app catalog, you can increase your reach by achieving app certification, or adding a download button your website.</span></span>

## <a name="application-certificate"></a><span data-ttu-id="2f906-106">Certificat d’application</span><span class="sxs-lookup"><span data-stu-id="2f906-106">Application Certificate</span></span>

<span data-ttu-id="2f906-107">Microsoft fournit un [programme de certification d’application](./application-certification.md) qui compile vos informations d’application et les présente sur la [page de sécurité et de conformité des applications Microsoft teams](https://aka.ms/AppCertification).</span><span class="sxs-lookup"><span data-stu-id="2f906-107">Microsoft provides a [Application Certification program](./application-certification.md) that compiles your app information and presents it on [Microsoft Teams App Security and Compliance Page](https://aka.ms/AppCertification).</span></span> <span data-ttu-id="2f906-108">Ces informations visent à aider les administrateurs à choisir les applications qui sont sûres pour leur organisation.</span><span class="sxs-lookup"><span data-stu-id="2f906-108">This information is intended to help admins to choose apps that are safe for their organizations.</span></span>

## <a name="add-a-download-button-to-your-product-site"></a><span data-ttu-id="2f906-109">Ajouter un bouton de téléchargement à votre site de produit</span><span class="sxs-lookup"><span data-stu-id="2f906-109">Add a download button to your product site</span></span>

<span data-ttu-id="2f906-110">Si votre application se trouve dans le magasin Microsoft Teams, vous pouvez générer un lien vers votre site Web qui lance teams et affiche une boîte de dialogue de consentement et d’installation pour permettre aux utilisateurs d’ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="2f906-110">If your app is in the Microsoft Teams store, you can generate a link for your website that launches Teams and shows a consent and installation dialog for users to add the app.</span></span>
<span data-ttu-id="2f906-111">Le format est : `https://teams.microsoft.com/l/app/<appId>` où AppID est le GUID qu’il déclare dans le manifeste soumis.</span><span class="sxs-lookup"><span data-stu-id="2f906-111">The format is:  `https://teams.microsoft.com/l/app/<appId>` where appID is the GUID they declare in the submitted manifest.</span></span>
<span data-ttu-id="2f906-112">Exemple : `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` est le lien pour installer Trello.</span><span class="sxs-lookup"><span data-stu-id="2f906-112">Example: `https://teams.microsoft.com/l/app/49e6f432-d79c-49e8-94f7-89b94f3672fd` is the link to install Trello.</span></span>

## <a name="updating-your-existing-teams-app"></a><span data-ttu-id="2f906-113">Mise à jour de votre application teams existante</span><span class="sxs-lookup"><span data-stu-id="2f906-113">Updating your existing Teams app</span></span>

* <span data-ttu-id="2f906-114">N’utilisez pas le bouton *Ajouter une nouvelle application* pour renvoyer votre application.</span><span class="sxs-lookup"><span data-stu-id="2f906-114">Do not use the *Add a new app* button to resubmit your app.</span></span> <span data-ttu-id="2f906-115">Utilisez plutôt la mosaïque de votre application sous l’onglet vue d’ensemble.</span><span class="sxs-lookup"><span data-stu-id="2f906-115">Use the tile for your app on the Overview tab instead.</span></span>
* <span data-ttu-id="2f906-116">L’appId dans le manifeste mis à jour doit être le même que dans le manifeste actuel, avec un numéro de version incrémentiel.</span><span class="sxs-lookup"><span data-stu-id="2f906-116">The appId in the updated manifest should be the same as in the current manifest, with an incremented version number.</span></span>
* <span data-ttu-id="2f906-117">Incrémentez votre numéro de version dans votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="2f906-117">Increment your version number in your manifest.</span></span>

### <a name="when-does-updating-your-app-trigger-the-user-consent-flow"></a><span data-ttu-id="2f906-118">Quand la mise à jour de votre application déclenche-t-elle le flux de consentement de l’utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="2f906-118">When does updating your app trigger the user consent flow?</span></span>

<span data-ttu-id="2f906-119">Lorsqu’un utilisateur installe votre application, il est autorisé à accorder à l’application l’autorisation d’accéder aux services et informations dont elle a besoin pour faire son travail.</span><span class="sxs-lookup"><span data-stu-id="2f906-119">When a user installs your application one of the first things they do is consent to give the app permission to access the services and information that the app needs to do its job.</span></span> <span data-ttu-id="2f906-120">Lorsque vous mettez à jour votre application, vous pouvez réactiver ce comportement de consentement, en particulier si vous avez effectué une ou plusieurs des modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f906-120">When you update your app, that can re-trigger this consent behavior, particularly if you have made one or more of the following changes:</span></span>

* <span data-ttu-id="2f906-121">Ajout d’une nouvelle fonctionnalité à une application, telle que l’ajout d’un bot à une application de type onglet uniquement.</span><span class="sxs-lookup"><span data-stu-id="2f906-121">Adding a new capability to an app such as adding a bot to an tab only app.</span></span>
* <span data-ttu-id="2f906-122">Modification du tableau d’autorisations dans le manifeste.</span><span class="sxs-lookup"><span data-stu-id="2f906-122">Changing the permissions array in the manifest.</span></span>
* <span data-ttu-id="2f906-123">Incrémentez le numéro de version de votre application dans votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="2f906-123">Increment your app version number in your manifest.</span></span>
