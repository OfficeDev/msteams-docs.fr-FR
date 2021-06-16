---
title: Scènes personnalisées en mode ensemble
description: Travailler avec des scènes personnalisées du mode Ensemble
ms.topic: conceptual
ms.openlocfilehash: b2a81d92724785acbcd198d6240eec7d8d510e1c
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949748"
---
# <a name="custom-together-mode-scenes-in-teams"></a><span data-ttu-id="78103-103">Scènes personnalisées en mode ensemble dans Teams</span><span class="sxs-lookup"><span data-stu-id="78103-103">Custom Together Mode scenes in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="78103-104">Cette fonctionnalité est actuellement disponible en prévisualisation [pour les](../resources/dev-preview/developer-preview-intro.md) développeurs publics uniquement.</span><span class="sxs-lookup"><span data-stu-id="78103-104">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="78103-105">Les scènes personnalisées en mode ensemble Microsoft Teams un environnement de réunion immersif et attrayant qui rassemble les personnes et les encourage à activer leur vidéo.</span><span class="sxs-lookup"><span data-stu-id="78103-105">Custom Together Mode scenes in Microsoft Teams provides an immersive and engaging meeting environment that brings people together and encourages them to turn on their video.</span></span> <span data-ttu-id="78103-106">Il combine numériquement les participants dans une scène virtuelle unique et place leurs flux vidéo dans des sièges pré-déterminés conçus et corrigés par le créateur de scène.</span><span class="sxs-lookup"><span data-stu-id="78103-106">It digitally combines participants into a single virtual scene and places their video streams in pre-determined seats designed and fixed by the scene creator.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/MGsNmYKgeTA]

<span data-ttu-id="78103-107">Une scène dans des scènes personnalisées en mode ensemble est un artefact créé par le développeur de scène à l’aide de Microsoft Scene studio.</span><span class="sxs-lookup"><span data-stu-id="78103-107">A scene in custom Together Mode scenes is an artifact created by the scene developer using the Microsoft Scene studio.</span></span> <span data-ttu-id="78103-108">Dans un paramètre de scène en cours, les participants ont des sièges désignés avec des flux vidéo restituer dans ces sièges.</span><span class="sxs-lookup"><span data-stu-id="78103-108">In a conceived scene setting, participants have designated seats with video streams rendered in those seats.</span></span>

> [!NOTE]
> <span data-ttu-id="78103-109">Les applications de scène uniquement sont recommandées, car l’expérience d’acquisition pour ces applications est plus transparente.</span><span class="sxs-lookup"><span data-stu-id="78103-109">Scene only apps are recommended as the acquisition experience for such apps is more seamless.</span></span>

<span data-ttu-id="78103-110">Le processus suivant donne une vue d’ensemble pour créer une application de scène uniquement :</span><span class="sxs-lookup"><span data-stu-id="78103-110">The following process gives an overview to create a scene only app:</span></span>

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="Créer une application de scène uniquement" border="false":::

> [!NOTE]
> * <span data-ttu-id="78103-112">Une application de scène uniquement est toujours une application dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="78103-112">A scene only app is still an app in Microsoft Teams.</span></span> <span data-ttu-id="78103-113">Le studio Scene gère la création du package d’application en arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="78103-113">The Scene studio handles the app package creation in the background.</span></span>
> * <span data-ttu-id="78103-114">Plusieurs scènes d’un même package d’application s’affichent sous la forme d’une liste plate de scènes pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="78103-114">Multiple scenes in a single app package appear as a flat list of scenes to users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78103-115">Conditions requises</span><span class="sxs-lookup"><span data-stu-id="78103-115">Prerequisites</span></span>

<span data-ttu-id="78103-116">Vous devez avoir une connaissance de base des éléments suivants pour utiliser des scènes personnalisées du mode Ensemble :</span><span class="sxs-lookup"><span data-stu-id="78103-116">You must have a basic understanding of the following to use custom Together Mode scenes:</span></span>

* <span data-ttu-id="78103-117">Définition de la scène et des sièges dans une scène.</span><span class="sxs-lookup"><span data-stu-id="78103-117">Definition of scene and seats in a scene.</span></span>
* <span data-ttu-id="78103-118">Vous avez un compte de développeur Microsoft et familiarisez-vous avec le portail Microsoft Teams [développeur et](../concepts/build-and-test/teams-developer-portal.md) App Studio.</span><span class="sxs-lookup"><span data-stu-id="78103-118">Have a Microsoft Developer account and be familiar with the Microsoft Teams [Developer Portal](../concepts/build-and-test/teams-developer-portal.md) and App Studio.</span></span>
* <span data-ttu-id="78103-119">[Concept de chargement de version d’application.](../concepts/deploy-and-publish/apps-upload.md)</span><span class="sxs-lookup"><span data-stu-id="78103-119">[Concept of app sideloading](../concepts/deploy-and-publish/apps-upload.md).</span></span>
* <span data-ttu-id="78103-120">Assurez-vous que l’administrateur a accordé l’autorisation **Télécharger une** application personnalisée et de sélectionner tous les filtres dans le cadre de la configuration de l’application et des stratégies de réunion, respectivement.</span><span class="sxs-lookup"><span data-stu-id="78103-120">Ensure that the Administrator has granted permission to **Upload a custom app** and to select all filters as part of App Setup and Meeting policies respectively.</span></span>

## <a name="best-practices"></a><span data-ttu-id="78103-121">Meilleures pratiques</span><span class="sxs-lookup"><span data-stu-id="78103-121">Best practices</span></span>

<span data-ttu-id="78103-122">Avant de créer une scène, considérez ce qui suit pour une expérience de création de scène transparente :</span><span class="sxs-lookup"><span data-stu-id="78103-122">Prior to building a scene, consider the following to have a seamless scene building experience:</span></span>

* <span data-ttu-id="78103-123">Assurez-vous que toutes les images sont au format PNG.</span><span class="sxs-lookup"><span data-stu-id="78103-123">Ensure that all images are in PNG format.</span></span>
* <span data-ttu-id="78103-124">Assurez-vous que le package final avec toutes les images rassemblées ne doit pas dépasser la résolution 1920x1080.</span><span class="sxs-lookup"><span data-stu-id="78103-124">Ensure that the final package with all the images put together must not exceed 1920x1080 resolution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="78103-125">La résolution est un nombre even.</span><span class="sxs-lookup"><span data-stu-id="78103-125">The resolution is an even number.</span></span> <span data-ttu-id="78103-126">Il s’agit d’une condition requise pour que les scènes soient éclairées correctement.</span><span class="sxs-lookup"><span data-stu-id="78103-126">This is a requirement for scenes to be lit up successfully.</span></span>

* <span data-ttu-id="78103-127">Assurez-vous que la taille de scène maximale est de 10 Mo.</span><span class="sxs-lookup"><span data-stu-id="78103-127">Ensure that the maximum scene size is 10 MB.</span></span>
* <span data-ttu-id="78103-128">Assurez-vous que la taille maximale de chaque image est de 5 Mo.</span><span class="sxs-lookup"><span data-stu-id="78103-128">Ensure that the maximum size of each image is 5 MB.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="78103-129">Une scène est une collection de plusieurs images.</span><span class="sxs-lookup"><span data-stu-id="78103-129">A scene is a collection of multiple images.</span></span> <span data-ttu-id="78103-130">La limite est pour chaque image individuelle.</span><span class="sxs-lookup"><span data-stu-id="78103-130">The limit is for each individual image.</span></span>
    > * <span data-ttu-id="78103-131">La résolution d’image individuelle doit également être un nombre even.</span><span class="sxs-lookup"><span data-stu-id="78103-131">The individual image resolution must also be an even number.</span></span>
  
* <span data-ttu-id="78103-132">Assurez-vous que la **case à** cocher Transparente est sélectionnée si l’image est transparente.</span><span class="sxs-lookup"><span data-stu-id="78103-132">Ensure that the **Transparent** checkbox is selected if the image is transparent.</span></span> <span data-ttu-id="78103-133">Cette case à cocher est disponible dans le panneau droit lorsqu’une image est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="78103-133">This checkbox is available on the right panel when an image is selected.</span></span>

    > [!NOTE]
    > <span data-ttu-id="78103-134">Les images qui se chevauchent doivent être marquées comme **transparentes** pour indiquer qu’elles se chevauchent dans la scène.</span><span class="sxs-lookup"><span data-stu-id="78103-134">Overlapping images need to be marked as **Transparent** to indicate that they are overlapping images in the scene.</span></span>

## <a name="build-a-scene-using-the-scene-studio"></a><span data-ttu-id="78103-135">Créer une scène à l’aide de Scene studio</span><span class="sxs-lookup"><span data-stu-id="78103-135">Build a scene using the Scene studio</span></span>

<span data-ttu-id="78103-136">Microsoft dispose d’un studio de scène qui vous permet de créer des scènes.</span><span class="sxs-lookup"><span data-stu-id="78103-136">Microsoft has a Scene studio that allows you to build scenes.</span></span> <span data-ttu-id="78103-137">Il est disponible dans [l’Éditeur de](https://dev.teams.microsoft.com/scenes)scènes - Teams portail du développeur.</span><span class="sxs-lookup"><span data-stu-id="78103-137">It is available on [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).</span></span>

> [!NOTE]
> <span data-ttu-id="78103-138">Ce document fait référence à Scene studio dans le portail Microsoft Teams développeur.</span><span class="sxs-lookup"><span data-stu-id="78103-138">This document is referring to Scene studio in the Microsoft Teams Developer Portal.</span></span> <span data-ttu-id="78103-139">L’interface et les fonctionnalités sont identiques dans Le Concepteur de scène App Studio.</span><span class="sxs-lookup"><span data-stu-id="78103-139">The interface and functionalities are all the same in App Studio Scene Designer.</span></span>

<span data-ttu-id="78103-140">Une scène dans le contexte du studio de scène est un artefact qui contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="78103-140">A scene in the context of the Scene studio is an artifact that contains the following:</span></span>

* <span data-ttu-id="78103-141">Sièges réservés aux organisateurs et présentateurs de réunion.</span><span class="sxs-lookup"><span data-stu-id="78103-141">Seats reserved for meeting organizer and meeting presenters.</span></span>

    > [!NOTE]
    > <span data-ttu-id="78103-142">Le présentateur ne fait pas référence à l’utilisateur qui partage activement.</span><span class="sxs-lookup"><span data-stu-id="78103-142">Presenter does not refer to the user who is actively sharing.</span></span> <span data-ttu-id="78103-143">Il fait référence au rôle [de réunion.](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="78103-143">It refers to the [meeting role](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

* <span data-ttu-id="78103-144">Siège et image pour chaque participant avec une largeur et une hauteur réglables.</span><span class="sxs-lookup"><span data-stu-id="78103-144">Seat and image for each participant with an adjustable width and height.</span></span>

    > [!NOTE]
    > <span data-ttu-id="78103-145">PNG est le seul format pris en charge.</span><span class="sxs-lookup"><span data-stu-id="78103-145">PNG is the only supported format.</span></span>

* <span data-ttu-id="78103-146">Coordonnées XYZ de tous les sièges et images.</span><span class="sxs-lookup"><span data-stu-id="78103-146">XYZ coordinates of all the seats and images.</span></span>
* <span data-ttu-id="78103-147">Collection d’images qui sont en tant qu’une seule image.</span><span class="sxs-lookup"><span data-stu-id="78103-147">Collection of images that are camouflaged as one image.</span></span>

<span data-ttu-id="78103-148">Les dimensions des sièges deviennent le canevas pour le rendu du flux vidéo du participant.</span><span class="sxs-lookup"><span data-stu-id="78103-148">The seat dimensions become the canvas for rendering the participant video stream.</span></span> <span data-ttu-id="78103-149">L’image suivante montre chaque siège représenté en tant qu’avatar pour les scènes de construction :</span><span class="sxs-lookup"><span data-stu-id="78103-149">The following image shows each seat represented as an avatar for building scenes:</span></span>

![Studio de scène](../assets/images/apps-in-meetings/scene-design-studio.png)

<span data-ttu-id="78103-151">**Pour créer une scène à l’aide de Scene studio**</span><span class="sxs-lookup"><span data-stu-id="78103-151">**To build a scene using the Scene studio**</span></span>

1. <span data-ttu-id="78103-152">Go to [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).</span><span class="sxs-lookup"><span data-stu-id="78103-152">Go to [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).</span></span>

    >[!NOTE]
    > * <span data-ttu-id="78103-153">Pour ouvrir Scene studio, vous pouvez accéder à la page d’accueil du [portail Teams développeur](https://dev.teams.microsoft.com/home) et sélectionner Créer des scènes **personnalisées pour les réunions.**</span><span class="sxs-lookup"><span data-stu-id="78103-153">To open Scene studio, you can navigate to the home page of [Teams Developer Portal](https://dev.teams.microsoft.com/home) and select **Create custom scenes for meetings**.</span></span>
    > * <span data-ttu-id="78103-154">Pour ouvrir Scene studio, vous pouvez accéder à la page  d’accueil du portail de développement [Teams,](https://dev.teams.microsoft.com/home)sélectionner Outils dans la section de gauche et sélectionner **Scene studio** dans la section **Outils.**</span><span class="sxs-lookup"><span data-stu-id="78103-154">To open Scene studio, you can navigate to the home page of [Teams Developer Portal](https://dev.teams.microsoft.com/home), select **Tools** from the left hand section, and select **Scene studio** from the **Tools** section.</span></span>

1. <span data-ttu-id="78103-155">Dans la page **Éditeur de** scènes, **sélectionnez Créer une nouvelle scène.**</span><span class="sxs-lookup"><span data-stu-id="78103-155">In the **Scenes Editor** page, select **Create a new scene**.</span></span>

1. <span data-ttu-id="78103-156">Dans la **zone Scène,** entrez un nom pour la scène.</span><span class="sxs-lookup"><span data-stu-id="78103-156">In the **Scene** box, enter a name for the scene.</span></span>

    >[!NOTE]
    > * <span data-ttu-id="78103-157">Vous pouvez sélectionner **Fermer** pour faire bascule entre la fermeture ou la réouverture du volet droit.</span><span class="sxs-lookup"><span data-stu-id="78103-157">You can select **Close** to toggle between closing or reopening the right pane.</span></span>
    > * <span data-ttu-id="78103-158">Vous pouvez effectuer un zoom avant ou arrière de la scène à l’aide de la barre de zoom pour une meilleure vue de la scène.</span><span class="sxs-lookup"><span data-stu-id="78103-158">You can zoom in or zoom out of the scene using the zoom bar for a better view of the scene.</span></span>

1. <span data-ttu-id="78103-159">Faites glisser et déposez l’image dans l’environnement tel qu’il est affiché dans l’image suivante :</span><span class="sxs-lookup"><span data-stu-id="78103-159">Drag and drop the image into the environment as displayed in the following image:</span></span>

    >[!NOTE]
    > * <span data-ttu-id="78103-160">Vous pouvez télécharger les [ fichiersSampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) et [SampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) avec les images.</span><span class="sxs-lookup"><span data-stu-id="78103-160">You can download the [SampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) and [SampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) files with the images.</span></span>
    > * <span data-ttu-id="78103-161">Vous pouvez également ajouter des images d’arrière-plan à la scène à l’aide **d’ajouter des images.**</span><span class="sxs-lookup"><span data-stu-id="78103-161">Alternately, you can add background images to the scene using **Add images**.</span></span>

    ![Glisser-glisser dans la scène](../assets/images/apps-in-meetings/drag-and-drop-scene.png)

1. <span data-ttu-id="78103-163">Sélectionnez l’image que vous avez placée.</span><span class="sxs-lookup"><span data-stu-id="78103-163">Select the image that you have placed.</span></span>

1. <span data-ttu-id="78103-164">Dans le volet droit, sélectionnez un alignement pour l’image ou utilisez le curseur **Resize** pour ajuster la taille de l’image.</span><span class="sxs-lookup"><span data-stu-id="78103-164">From the right pane, select an alignment for the image or use the **Resize** slider to adjust the image size.</span></span>

    ![Alignement des images](../assets/images/apps-in-meetings/image-alignment.png)

1. <span data-ttu-id="78103-166">Sélectionnez une zone en dehors de l’image.</span><span class="sxs-lookup"><span data-stu-id="78103-166">Select an area outside of the image.</span></span>

1. <span data-ttu-id="78103-167">Dans le coin supérieur droit, sélectionnez **Participants** sous **Calques.**</span><span class="sxs-lookup"><span data-stu-id="78103-167">In the upper-right corner, select **Participants** under **Layers**.</span></span>

1. <span data-ttu-id="78103-168">Sélectionnez le nombre de participants pour la scène dans la zone Nombre **de participants,** puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="78103-168">Select the number of participants for the scene from the **Number of participants** box, and select **Add**.</span></span>

    >[!NOTE]
    > * <span data-ttu-id="78103-169">Une fois la scène livrée, les emplacements d’avatar sont remplacés par les flux vidéo du participant réel.</span><span class="sxs-lookup"><span data-stu-id="78103-169">After the scene is shipped, the avatar placements are replaced with actual participant's video streams.</span></span>
    > * <span data-ttu-id="78103-170">Vous pouvez faire glisser les images des participants autour de la scène et les placer à la position requise et les resizer à l’aide de la flèche de re resize.</span><span class="sxs-lookup"><span data-stu-id="78103-170">You can drag the participant images around the scene and place them in the required position and resize them using the resize arrow.</span></span>

1. <span data-ttu-id="78103-171">Sélectionnez n’importe quelle image de participant, puis **activez** la case à cocher Affecter un spot pour affecter la place au participant.</span><span class="sxs-lookup"><span data-stu-id="78103-171">Select any participant image, and choose the **Assign Spot** check box to assign the spot to the participant.</span></span>

1. <span data-ttu-id="78103-172">Sélectionnez **le rôle Organisateur** de réunion ou **Présentateur** pour le participant.</span><span class="sxs-lookup"><span data-stu-id="78103-172">Select **Meeting Organizer** or **Presenter** role for the participant.</span></span>

    >[!NOTE]
    > <span data-ttu-id="78103-173">Au cours d’une réunion, un participant doit avoir le rôle d’organisateur de la réunion.</span><span class="sxs-lookup"><span data-stu-id="78103-173">In a meeting, one participant must be assigned the role of a meeting organizer.</span></span>

    ![Affecter un emplacement](../assets/images/apps-in-meetings/assign-spot.png)

1. <span data-ttu-id="78103-175">Sélectionnez **Enregistrer** et **sélectionner Afficher dans Teams** pour tester rapidement votre scène dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="78103-175">Select **Save** and select **View in Teams** to quickly test your scene in Microsoft Teams.</span></span>

    >[!NOTE]
    > <span data-ttu-id="78103-176">Pour supprimer une scène que vous avez créée, **sélectionnez Supprimer la scène** dans la barre supérieure.</span><span class="sxs-lookup"><span data-stu-id="78103-176">To delete a scene you created, select **Delete scene** on the top bar.</span></span>

1. <span data-ttu-id="78103-177">Dans la **boîte de dialogue Affichage Teams,** sélectionnez Aperçu dans **Teams**.</span><span class="sxs-lookup"><span data-stu-id="78103-177">In the **View in Teams** dialog box, select **Preview in Teams**.</span></span>
1. <span data-ttu-id="78103-178">Dans la boîte de dialogue qui s’affiche, sélectionnez **Ajouter.**</span><span class="sxs-lookup"><span data-stu-id="78103-178">In the dialog box that appears, select **Add**.</span></span>

    <span data-ttu-id="78103-179">La scène peut être testée ou accessible en créant une réunion de test et en lançant des scènes personnalisées du mode Ensemble.</span><span class="sxs-lookup"><span data-stu-id="78103-179">The scene can be tested or accessed by creating a test meeting and launching custom Together Mode scenes.</span></span> <span data-ttu-id="78103-180">Pour plus d’informations, voir [activer des scènes personnalisées du mode Ensemble.](#activate-custom-together-mode-scenes)</span><span class="sxs-lookup"><span data-stu-id="78103-180">For more information, see [activate custom Together Mode scenes](#activate-custom-together-mode-scenes).</span></span>

    ![Lancer des scènes personnalisées du mode Ensemble](../assets/images/apps-in-meetings/launchtogethermode.png)

    >[!NOTE]
    > * <span data-ttu-id="78103-182">La sélection **de l’aperçu** crée automatiquement une Microsoft Teams qui peut être vue dans la **page** Applications du portail Teams développeur.</span><span class="sxs-lookup"><span data-stu-id="78103-182">Selecting **Preview** automatically creates a Microsoft Teams app that can be viewed in the **Apps** page in the Teams Developer Portal.</span></span>
    > * <span data-ttu-id="78103-183">La sélection **de l’aperçu** crée automatiquement un package d’application appmanifest.jssur la scène.</span><span class="sxs-lookup"><span data-stu-id="78103-183">Selecting **Preview** automatically creates an app package that is appmanifest.json behind the scene.</span></span> <span data-ttu-id="78103-184">Comme indiqué précédemment, cela est abstrait, mais vous pouvez accéder au package d’application créé automatiquement en accédant à **Applications** à partir du menu.</span><span class="sxs-lookup"><span data-stu-id="78103-184">As stated earlier, this is abstracted, but you can access the automatically created app package by navigating to **Apps** from the menu.</span></span>
    > * <span data-ttu-id="78103-185">La scène peut ensuite être vue dans la galerie personnalisée des scènes du mode Ensemble.</span><span class="sxs-lookup"><span data-stu-id="78103-185">The scene can then be viewed in the custom Together Mode scenes gallery.</span></span>

1. <span data-ttu-id="78103-186">Si vous le souhaitez,  vous pouvez sélectionner **Partager** dans le menu déroulant Enregistrer pour créer un lien partageable afin de distribuer facilement vos scènes à d’autres personnes.</span><span class="sxs-lookup"><span data-stu-id="78103-186">Optionally, you can select **Share** from the **Save** drop-down menu to create a shareable link to easily distribute your scenes for others to use.</span></span> <span data-ttu-id="78103-187">L’ouverture de ce lien installe la scène pour l’utilisateur et il peut commencer à l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="78103-187">Opening this link installs the scene for the user and they can start using it.</span></span>

1. <span data-ttu-id="78103-188">Après la prévisualisation, la scène peut être livrée en tant qu’application Teams en suivant les étapes de soumission de l’application.</span><span class="sxs-lookup"><span data-stu-id="78103-188">After preview, the scene can be shipped as an app to Teams by following the steps for app submission.</span></span>

    >[!NOTE]
    > <span data-ttu-id="78103-189">Cette étape nécessite le package d’application différent du package de scène, pour la scène qui a été conçue.</span><span class="sxs-lookup"><span data-stu-id="78103-189">This step requires the app package that is different from the scene package, for the scene that was designed.</span></span> <span data-ttu-id="78103-190">Le package d’application créé automatiquement se trouve dans la section **Applications** du Teams développeur.</span><span class="sxs-lookup"><span data-stu-id="78103-190">The app package created automatically can be found in the **Apps** section in the Teams Developer Center.</span></span>

1. <span data-ttu-id="78103-191">Éventuellement, le package de scène peut être  récupéré en sélectionnant **Exporter** dans le menu déroulant Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="78103-191">Optionally, the scene package can be retrieved by selecting **Export** from the **Save** drop-down menu.</span></span> <span data-ttu-id="78103-192">Un .zip de scène, c’est-à-dire le package de scène, est téléchargé.</span><span class="sxs-lookup"><span data-stu-id="78103-192">A .zip file, that is the scene package, is downloaded.</span></span>

    ![Exporter une scène](../assets/images/apps-in-meetings/build-a-scene.png)

    >[!NOTE]
    > <span data-ttu-id="78103-194">Le package de scène comprend une scene.jssur et les ressources PNG utilisées pour créer une scène.</span><span class="sxs-lookup"><span data-stu-id="78103-194">Scene package comprises of a scene.json and the PNG assets used to build a scene.</span></span> <span data-ttu-id="78103-195">Le package de scène peut être examiné pour incorporer d’autres modifications, comme décrit dans l’exemple scene.jssection de ce document.</span><span class="sxs-lookup"><span data-stu-id="78103-195">The scene package can be reviewed for incorporating other changes as described in the Sample scene.json section of this document.</span></span>

<span data-ttu-id="78103-196">Une scène plus complexe qui tire parti de l’axe Z est illustré dans l’exemple de mise en marche pas à pas.</span><span class="sxs-lookup"><span data-stu-id="78103-196">A more complex scene that leverages the Z-axis is demonstrated in the step-by-step getting started sample.</span></span>

## <a name="sample-scenejson"></a><span data-ttu-id="78103-197">Exemple scene.jssur</span><span class="sxs-lookup"><span data-stu-id="78103-197">Sample scene.json</span></span>

<span data-ttu-id="78103-198">Scene.jssur les images indiquent la position exacte des sièges.</span><span class="sxs-lookup"><span data-stu-id="78103-198">Scene.json along with the images indicate the exact position of the seats.</span></span> <span data-ttu-id="78103-199">Une scène se compose d’images bitmap, de sprites et de rectangles dans lequel placer les vidéos des participants.</span><span class="sxs-lookup"><span data-stu-id="78103-199">A scene consists of bitmap images, sprites, and rectangles to put participant videos in.</span></span> <span data-ttu-id="78103-200">Ces sprites et zones de participant sont définis dans un système de coordonnées du monde avec l’axe X pointant vers la droite et l’axe Y pointant vers le bas.</span><span class="sxs-lookup"><span data-stu-id="78103-200">These sprites and participant boxes are defined in a world coordinate system with the X-axis pointing to the right and the Y-axis pointing downwards.</span></span> <span data-ttu-id="78103-201">Les scènes personnalisées en mode ensemble prend en charge le zoom avant sur les participants actuels.</span><span class="sxs-lookup"><span data-stu-id="78103-201">Custom Together Mode scenes supports zooming in on the current participants.</span></span> <span data-ttu-id="78103-202">Cela est utile pour les petites réunions dans une grande scène.</span><span class="sxs-lookup"><span data-stu-id="78103-202">This is helpful for small meetings in a large scene.</span></span> <span data-ttu-id="78103-203">Un sprite est une image bitmap statique positionnée dans le monde.</span><span class="sxs-lookup"><span data-stu-id="78103-203">A sprite is a static bitmap image positioned in the world.</span></span> <span data-ttu-id="78103-204">La valeur Z du sprite détermine la position du sprite.</span><span class="sxs-lookup"><span data-stu-id="78103-204">The Z value of the sprite determines the position of the sprite.</span></span> <span data-ttu-id="78103-205">Le rendu commence par le sprite avec la valeur Z la plus faible, donc une valeur Z plus élevée signifie qu’il est plus proche de la caméra.</span><span class="sxs-lookup"><span data-stu-id="78103-205">Rendering starts with the sprite with lowest Z value, so higher Z value means it is closer to the camera.</span></span> <span data-ttu-id="78103-206">Chaque participant possède son propre flux vidéo, qui est segmenté afin que seul le premier plan soit rendu.</span><span class="sxs-lookup"><span data-stu-id="78103-206">Each participant has its own video feed, which is segmented so that only the foreground is rendered.</span></span>

<span data-ttu-id="78103-207">Voici les scene.jssur l’exemple :</span><span class="sxs-lookup"><span data-stu-id="78103-207">Following is the scene.json sample:</span></span>

```json
{
   "protocolVersion": "1.0",
   "id": "A",
   "autoZoom": true,
   "mirrorParticipants ": true,
   "extent":{
      "left":0.0,
      "top":0.0,
      "width":16.0,
      "height":9.0
   },
   "sprites":[
      {
         "filename":"background.png",
         "cx":8.0,
         "cy":4.5,
         "width":16.0,
         "height":9.0,
         "zOrder":0.0,
   "isAlpha":false
      },
      {
         "filename":"table.png",
         "cx":8.0,
         "cy":7.0,
         "width":12.0,
         "height":4.0,
         "zOrder":3.0,
   "isAlpha":true
      },
      {
         "filename":"row0.png",
         "cx":12.0,
         "cy":15.0,
         "width":8.0,
         "height":4.0,
         "zOrder":2.0,
   "isAlpha":true
      }

   ],
   "participants":[
      {
         "cx":5.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":0
      },
      {
         "cx":11.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":1
      }
   ]
}
```

<span data-ttu-id="78103-208">Chaque scène possède un ID et un nom uniques.</span><span class="sxs-lookup"><span data-stu-id="78103-208">Each scene has a unique ID and name.</span></span> <span data-ttu-id="78103-209">Le JSON de scène contient également des informations sur toutes les ressources utilisées pour la scène.</span><span class="sxs-lookup"><span data-stu-id="78103-209">The scene JSON also contains information on all the assets used for the scene.</span></span> <span data-ttu-id="78103-210">Chaque bien contient un nom de fichier, une largeur, une hauteur et une position sur les axes X et Y.</span><span class="sxs-lookup"><span data-stu-id="78103-210">Each asset contains a filename, width, height, and position on the X and Y-axis.</span></span> <span data-ttu-id="78103-211">De même, chaque siège contient un ID de siège, sa largeur, sa hauteur et sa position sur les axes X et Y.</span><span class="sxs-lookup"><span data-stu-id="78103-211">Similarly, each seat contains a seat ID, width, height, and position on the X and Y-axis.</span></span> <span data-ttu-id="78103-212">L’ordre d’altération est généré automatiquement et peut être modifié selon les préférences.</span><span class="sxs-lookup"><span data-stu-id="78103-212">The seating order is generated automatically and can be altered as per preference.</span></span>

> [!NOTE]
> <span data-ttu-id="78103-213">Le numéro d’ordre de l’ordre de l’ordre des personnes qui rejoignent l’appel.</span><span class="sxs-lookup"><span data-stu-id="78103-213">Seating order number corresponds to the order of people joining the call.</span></span>

<span data-ttu-id="78103-214">L’axe zOrder représente l’ordre de placement des images et des sièges le long de l’axe Z.</span><span class="sxs-lookup"><span data-stu-id="78103-214">The zOrder represents the order of placing images and seats along the Z-axis.</span></span> <span data-ttu-id="78103-215">Dans de nombreux cas, elle donne une idée de la profondeur ou de la partition si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="78103-215">In many cases, it gives a sense of depth or partition if required.</span></span> <span data-ttu-id="78103-216">Pour plus d’informations, voir l’exemple de mise en marche pas à pas.</span><span class="sxs-lookup"><span data-stu-id="78103-216">For more information, see the step-by-step getting started sample.</span></span> <span data-ttu-id="78103-217">L’exemple tire parti de zOrder.</span><span class="sxs-lookup"><span data-stu-id="78103-217">The sample leverages the zOrder.</span></span>

<span data-ttu-id="78103-218">Maintenant que vous avez passé en scene.jsl’exemple, vous pouvez activer les scènes personnalisées du mode Ensemble pour vous engager dans des scènes.</span><span class="sxs-lookup"><span data-stu-id="78103-218">Now that you have gone through the sample scene.json, you can activate the custom Together Mode scenes to engage in scenes.</span></span>

## <a name="activate-custom-together-mode-scenes"></a><span data-ttu-id="78103-219">Activer des scènes personnalisées en mode ensemble</span><span class="sxs-lookup"><span data-stu-id="78103-219">Activate custom Together Mode scenes</span></span>

<span data-ttu-id="78103-220">Obtenez des informations de bout en bout sur la façon dont un utilisateur final s’engage avec des scènes dans des scènes personnalisées en mode ensemble.</span><span class="sxs-lookup"><span data-stu-id="78103-220">Get end-to-end information of how an end user engages with scenes in custom Together Mode scenes.</span></span>

<span data-ttu-id="78103-221">**Pour choisir des scènes et activer des scènes personnalisées en mode Ensemble**</span><span class="sxs-lookup"><span data-stu-id="78103-221">**To choose scenes and activate custom Together Mode scenes**</span></span>

1. <span data-ttu-id="78103-222">Créez une réunion de test.</span><span class="sxs-lookup"><span data-stu-id="78103-222">Create a new test meeting.</span></span>

    >[!NOTE]
    > <span data-ttu-id="78103-223">Lors de la sélection **de l’aperçu** dans Le studio de scène, la scène est installée en tant qu’application dans Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="78103-223">On selecting **Preview** in the Scene studio, the scene is installed as an app in Microsoft Teams.</span></span> <span data-ttu-id="78103-224">Il s’agit du modèle pour qu’un développeur teste et teste des scènes à partir du studio Scene studio.</span><span class="sxs-lookup"><span data-stu-id="78103-224">This is the model for a developer to test and try out scenes from the Scene studio.</span></span> <span data-ttu-id="78103-225">Une fois qu’une scène est livrée en tant qu’application, les utilisateurs voient ces scènes dans la galerie de scène.</span><span class="sxs-lookup"><span data-stu-id="78103-225">After a scene is shipped as an app, users see these scenes in the scene gallery.</span></span>

1. <span data-ttu-id="78103-226">Dans la **page de la** galerie dans le coin supérieur gauche, sélectionnez Mode **Ensemble.**</span><span class="sxs-lookup"><span data-stu-id="78103-226">From the **Gallery** drop-down in the upper-left corner, select **Together Mode**.</span></span> <span data-ttu-id="78103-227">La **boîte de dialogue s’affiche** et la scène ajoutée est disponible.</span><span class="sxs-lookup"><span data-stu-id="78103-227">The **Picker** dialog box appears and the scene that is added is available.</span></span>

1. <span data-ttu-id="78103-228">Sélectionnez **Modifier la scène** pour modifier la scène par défaut.</span><span class="sxs-lookup"><span data-stu-id="78103-228">Select **Change scene** to change the default scene.</span></span>

1. <span data-ttu-id="78103-229">Dans la **galerie de scène,** sélectionnez la scène que vous souhaitez utiliser pour votre réunion.</span><span class="sxs-lookup"><span data-stu-id="78103-229">From the **Scene Gallery**, select the scene you want to use for your meeting.</span></span>

1. <span data-ttu-id="78103-230">L’organisateur et le présentateur de la réunion peuvent éventuellement modifier **la scène pour tous** les participants à la réunion.</span><span class="sxs-lookup"><span data-stu-id="78103-230">Optionally, the meeting organizer and presenter can **Change scene for all participants** in the meeting.</span></span>

    >[!NOTE]
    > <span data-ttu-id="78103-231">À tout moment, une seule scène peut être utilisée de manière homogène pour la réunion.</span><span class="sxs-lookup"><span data-stu-id="78103-231">At any point in time, only one scene can be used homogeneously for the meeting.</span></span> <span data-ttu-id="78103-232">Si un présentateur ou un organisateur modifie une scène, elle change pour tout.</span><span class="sxs-lookup"><span data-stu-id="78103-232">If a presenter or organizer changes a scene, it  changes for all.</span></span> <span data-ttu-id="78103-233">Le basculement dans ou hors des scènes personnalisées du mode Ensemble est la responsabilité des participants individuels, mais dans les scènes personnalisées du mode Ensemble, tous les participants ont la même scène.</span><span class="sxs-lookup"><span data-stu-id="78103-233">Switching in or out of custom Together Mode scenes is up to individual participants, but while in custom Together Mode scenes, all participants have the same scene.</span></span>

1. <span data-ttu-id="78103-234">Sélectionnez **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="78103-234">Select **Apply**.</span></span> <span data-ttu-id="78103-235">Teams installe l’application pour l’utilisateur et applique la scène.</span><span class="sxs-lookup"><span data-stu-id="78103-235">Teams installs the app for the user and applies the scene.</span></span>

## <a name="open-a-custom-together-mode-scenes-scene-package"></a><span data-ttu-id="78103-236">Ouvrir un package de scène de scène en mode ensemble personnalisé</span><span class="sxs-lookup"><span data-stu-id="78103-236">Open a custom Together Mode scenes Scene Package</span></span>

<span data-ttu-id="78103-237">Vous pouvez partager le package de scène qui est un fichier .zip extrait du studio scene studio à d’autres créateurs pour améliorer davantage la scène.</span><span class="sxs-lookup"><span data-stu-id="78103-237">You can share the Scene Package that is a .zip file retrieved from the Scene studio to other creators to further enhance the scene.</span></span> <span data-ttu-id="78103-238">La **fonctionnalité Importer une** scène peut être mise à profit.</span><span class="sxs-lookup"><span data-stu-id="78103-238">The **Import a Scene** functionality can be leveraged.</span></span> <span data-ttu-id="78103-239">Cet outil permet de déballer un package de scène pour laisser le créateur continuer à créer la scène.</span><span class="sxs-lookup"><span data-stu-id="78103-239">This tool helps unwrap a scene package to let the creator continue building the scene.</span></span>

![Fichier zip de scène](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a><span data-ttu-id="78103-241">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="78103-241">See also</span></span>

[<span data-ttu-id="78103-242">Applications pour Teams réunions</span><span class="sxs-lookup"><span data-stu-id="78103-242">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)
