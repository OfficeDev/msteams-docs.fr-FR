---
title: Télécharger votre application personnalisée
description: Découvrez comment recharger une version de version de votre application dans Microsoft Teams. Le chargement de version test est courant lors du test et du débogage d’une application pendant le développement.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 39e94317ceb615ecd7d5481276ffafed5afe5cde
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565192"
---
# <a name="upload-your-app-in-microsoft-teams"></a><span data-ttu-id="281b2-104">Télécharger votre application dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="281b2-104">Upload your app in Microsoft Teams</span></span>

<span data-ttu-id="281b2-105">Vous pouvez télécharger une version Microsoft Teams applications sans avoir à publier dans votre organisation ou le Teams store.</span><span class="sxs-lookup"><span data-stu-id="281b2-105">You can sideload Microsoft Teams apps without having to publish to your organization or the Teams store.</span></span> <span data-ttu-id="281b2-106">Cela est logique dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="281b2-106">This makes sense in the following scenarios:</span></span>

* <span data-ttu-id="281b2-107">Vous souhaitez tester et déboguer une application localement vous-même ou avec d’autres développeurs.</span><span class="sxs-lookup"><span data-stu-id="281b2-107">You want to test and debug an app locally yourself or with other developers.</span></span>
* <span data-ttu-id="281b2-108">Vous avez créé une application uniquement pour vous-même.</span><span class="sxs-lookup"><span data-stu-id="281b2-108">You built an app just for yourself.</span></span> <span data-ttu-id="281b2-109">Par exemple, pour automatiser un flux de travail.</span><span class="sxs-lookup"><span data-stu-id="281b2-109">For example, to automate a workflow.</span></span>
* <span data-ttu-id="281b2-110">Vous avez créé une application pour un petit groupe d’utilisateurs, par exemple, votre groupe de travail.</span><span class="sxs-lookup"><span data-stu-id="281b2-110">You built an app for a small set of users, such as, your work group.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="281b2-111">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="281b2-111">Prerequisites</span></span>

* <span data-ttu-id="281b2-112">Créez votre [package d’application](~/concepts/build-and-test/apps-package.md) [et validez-le pour les](https://dev.teams.microsoft.com/appvalidation.html) erreurs.</span><span class="sxs-lookup"><span data-stu-id="281b2-112">Create your [app package](~/concepts/build-and-test/apps-package.md) and [validate it](https://dev.teams.microsoft.com/appvalidation.html) for errors.</span></span>
* <span data-ttu-id="281b2-113">[Activez le chargement d’applications personnalisées](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) dans Teams.</span><span class="sxs-lookup"><span data-stu-id="281b2-113">[Enable custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) in Teams.</span></span>
* <span data-ttu-id="281b2-114">Assurez-vous que votre application est en cours d’exécution et accessible via HTTPs.</span><span class="sxs-lookup"><span data-stu-id="281b2-114">Make sure that your app is running and accessible via HTTPs.</span></span>

## <a name="upload-your-app"></a><span data-ttu-id="281b2-115">Télécharger votre application</span><span class="sxs-lookup"><span data-stu-id="281b2-115">Upload your app</span></span>

<span data-ttu-id="281b2-116">Vous pouvez charger une version de votre application vers une équipe, une conversation, une réunion ou pour une utilisation personnelle en fonction de la façon dont vous avez configuré l’étendue de votre application.</span><span class="sxs-lookup"><span data-stu-id="281b2-116">You can sideload your app to a team, chat, meeting, or for personal use depending on how you configured your app's scope.</span></span>

1. <span data-ttu-id="281b2-117">Connectez-vous au client Teams avec [votre compte Microsoft 365 développement.](~/build-your-first-app/build-and-run.md#prerequisites)</span><span class="sxs-lookup"><span data-stu-id="281b2-117">Log in to the Teams client with your [Microsoft 365 development account](~/build-your-first-app/build-and-run.md#prerequisites).</span></span>
1. <span data-ttu-id="281b2-118">Sélectionnez **applications** et choisissez **Télécharger une application personnalisée.**</span><span class="sxs-lookup"><span data-stu-id="281b2-118">Select **Apps** and choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="281b2-119">Sélectionnez votre package d'.zip fichier.</span><span class="sxs-lookup"><span data-stu-id="281b2-119">Select your app package .zip file.</span></span> <span data-ttu-id="281b2-120">Une boîte de dialogue d’installation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="281b2-120">An install dialog displays.</span></span>
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Screenshot showing an example of a Teams app install dialog.":::
1. <span data-ttu-id="281b2-122">Ajoutez votre application à Teams.</span><span class="sxs-lookup"><span data-stu-id="281b2-122">Add your app to Teams.</span></span>

## <a name="troubleshoot-upload-issues"></a><span data-ttu-id="281b2-123">Résoudre les problèmes de téléchargement</span><span class="sxs-lookup"><span data-stu-id="281b2-123">Troubleshoot upload issues</span></span>

<span data-ttu-id="281b2-124">Si le chargement de version de votre application échoue, faites les choses suivantes jusqu’à ce que le problème soit résolu :</span><span class="sxs-lookup"><span data-stu-id="281b2-124">If your app fails to sideload, do the following until the issue resolves:</span></span>

1. <span data-ttu-id="281b2-125">Revenir en arrière dans les instructions de [création de votre package d’application.](../../concepts/build-and-test/apps-package.md)</span><span class="sxs-lookup"><span data-stu-id="281b2-125">Go back through the instructions for [creating your app package](../../concepts/build-and-test/apps-package.md).</span></span>
1. <span data-ttu-id="281b2-126">[Validez à nouveau votre package d’application.](https://dev.teams.microsoft.com/appvalidation.html)</span><span class="sxs-lookup"><span data-stu-id="281b2-126">[Validate your app package](https://dev.teams.microsoft.com/appvalidation.html) again.</span></span>
1. <span data-ttu-id="281b2-127">Assurez-vous que le manifeste de votre application correspond au [schéma le plus récent.](../../resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="281b2-127">Make sure your app manifest matches the latest [schema](../../resources/schema/manifest-schema.md).</span></span>

## <a name="access-your-app"></a><span data-ttu-id="281b2-128">Accéder à votre application</span><span class="sxs-lookup"><span data-stu-id="281b2-128">Access your app</span></span>

<span data-ttu-id="281b2-129">Teams propose plusieurs façons d’ouvrir des applications.</span><span class="sxs-lookup"><span data-stu-id="281b2-129">Teams provides several ways to open apps.</span></span> <span data-ttu-id="281b2-130">Pour plus d’informations, [voir accéder à vos applications dans Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span><span class="sxs-lookup"><span data-stu-id="281b2-130">For more information, see [access your apps in Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).</span></span>

## <a name="update-your-app"></a><span data-ttu-id="281b2-131">Mettre à jour votre application</span><span class="sxs-lookup"><span data-stu-id="281b2-131">Update your app</span></span>

<span data-ttu-id="281b2-132">Vous n’avez pas besoin de recharger une version de votre application si vous a apporté des modifications de code (celles-ci sont reflétées dans Teams en temps réel).</span><span class="sxs-lookup"><span data-stu-id="281b2-132">You don't have to sideload your app again if you make code changes (these are reflected in Teams in real-time).</span></span> <span data-ttu-id="281b2-133">Toutefois, vous devez réinstaller si vous modifiez des configurations d’application.</span><span class="sxs-lookup"><span data-stu-id="281b2-133">However, you must reinstall if you change any app configurations.</span></span>

## <a name="remove-your-app"></a><span data-ttu-id="281b2-134">Supprimer votre application</span><span class="sxs-lookup"><span data-stu-id="281b2-134">Remove your app</span></span>

<span data-ttu-id="281b2-135">Pour supprimer votre application, cliquez avec le bouton droit sur l’icône de l’Teams puis **sélectionnez Désinstaller.**</span><span class="sxs-lookup"><span data-stu-id="281b2-135">To remove your app, right click the app icon in Teams and select **Uninstall**.</span></span>

> [!NOTE]
> <span data-ttu-id="281b2-136">Vous ne pouvez pas supprimer entièrement l’activité du bot personnel.</span><span class="sxs-lookup"><span data-stu-id="281b2-136">You can't remove personal bot activity entirely.</span></span> <span data-ttu-id="281b2-137">Si vous supprimez l’application et l’ajoutez à nouveau, une nouvelle communication avec le bot s’ajoute à la conversation précédente avec elle.</span><span class="sxs-lookup"><span data-stu-id="281b2-137">If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.</span></span>

## <a name="next-step"></a><span data-ttu-id="281b2-138">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="281b2-138">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="281b2-139">Utiliser votre application Teams de messagerie</span><span class="sxs-lookup"><span data-stu-id="281b2-139">Use your Teams app</span></span>](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
