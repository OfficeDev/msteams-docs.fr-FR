---
title: Référence du schéma JSON du fichier de localisation
description: Décrit le schéma de localisation pris en charge par le fichier de localisation pour Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: Localisation du schéma de manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: 3e4207fb3e862eac18c80ffc49e7c5648ae05c28
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019705"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="f033f-104">Référence : schéma JSON du fichier de localisation</span><span class="sxs-lookup"><span data-stu-id="f033f-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="f033f-105">Le fichier de localisation de Microsoft Teams décrit les traductions linguistiques qui seront servies en fonction des paramètres de langue du client.</span><span class="sxs-lookup"><span data-stu-id="f033f-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="f033f-106">Votre fichier doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="f033f-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="f033f-107">Pour plus d'informations, [voir localisation d'application.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="f033f-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="f033f-108">Échantillon</span><span class="sxs-lookup"><span data-stu-id="f033f-108">Sample</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "name.short": "Le App Studio",
  "name.full": "App Studio pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App Studio.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App Studio.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

<span data-ttu-id="f033f-109">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="f033f-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="f033f-110">$schema</span><span class="sxs-lookup"><span data-stu-id="f033f-110">$schema</span></span>

<span data-ttu-id="f033f-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="f033f-111">**URI**</span></span>

<span data-ttu-id="f033f-112">L https:// URL référente au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="f033f-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="f033f-113">Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code : `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="f033f-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="f033f-114">name.short</span><span class="sxs-lookup"><span data-stu-id="f033f-114">name.short</span></span>

<span data-ttu-id="f033f-115">**Chaîne, longueur maximale 30**</span><span class="sxs-lookup"><span data-stu-id="f033f-115">**String, Max Length 30**</span></span>

<span data-ttu-id="f033f-116">Remplace la chaîne correspondante du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="f033f-117">name.full</span><span class="sxs-lookup"><span data-stu-id="f033f-117">name.full</span></span>

<span data-ttu-id="f033f-118">**Chaîne, longueur maximale 100**</span><span class="sxs-lookup"><span data-stu-id="f033f-118">**String, Max Length 100**</span></span>

<span data-ttu-id="f033f-119">Remplace la chaîne correspondante du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="f033f-120">description.short</span><span class="sxs-lookup"><span data-stu-id="f033f-120">description.short</span></span>

<span data-ttu-id="f033f-121">**Chaîne, longueur maximale 80**</span><span class="sxs-lookup"><span data-stu-id="f033f-121">**String, Max Length 80**</span></span>

<span data-ttu-id="f033f-122">Remplace la chaîne correspondante du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="f033f-123">description.full</span><span class="sxs-lookup"><span data-stu-id="f033f-123">description.full</span></span>

<span data-ttu-id="f033f-124">**Chaîne, longueur maximale 4000**</span><span class="sxs-lookup"><span data-stu-id="f033f-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="f033f-125">Remplace la chaîne correspondante du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="f033f-126">staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="f033f-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="f033f-127">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="f033f-127">**String, Max Length 128**</span></span>

<span data-ttu-id="f033f-128">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="f033f-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="f033f-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="f033f-130">**Chaîne, longueur maximale 32**</span><span class="sxs-lookup"><span data-stu-id="f033f-130">**String, Max Length 32**</span></span>

<span data-ttu-id="f033f-131">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="f033f-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="f033f-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="f033f-133">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="f033f-133">**String, Max Length 128**</span></span>

<span data-ttu-id="f033f-134">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="f033f-135">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="f033f-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="f033f-136">**Chaîne, longueur maximale 32**</span><span class="sxs-lookup"><span data-stu-id="f033f-136">**String, Max Length 32**</span></span>

<span data-ttu-id="f033f-137">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="f033f-138">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="f033f-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="f033f-139">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="f033f-139">**String, Max Length 128**</span></span>

<span data-ttu-id="f033f-140">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="f033f-141">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="f033f-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="f033f-142">**Chaîne, longueur maximale 32**</span><span class="sxs-lookup"><span data-stu-id="f033f-142">**String, Max Length 32**</span></span>

<span data-ttu-id="f033f-143">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="f033f-144">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="f033f-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="f033f-145">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="f033f-145">**String, Max Length 128**</span></span>

<span data-ttu-id="f033f-146">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="f033f-147">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value</span><span class="sxs-lookup"><span data-stu-id="f033f-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="f033f-148">**Chaîne, longueur maximale 512**</span><span class="sxs-lookup"><span data-stu-id="f033f-148">**String, Max Length 512**</span></span>

<span data-ttu-id="f033f-149">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="f033f-150">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="f033f-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="f033f-151">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="f033f-151">**String, Max Length 128**</span></span>

<span data-ttu-id="f033f-152">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="f033f-153">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="f033f-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="f033f-154">**Chaîne, longueur maximale 64**</span><span class="sxs-lookup"><span data-stu-id="f033f-154">**String, Max Length 64**</span></span>

<span data-ttu-id="f033f-155">Remplace la ou les chaînes correspondantes du manifeste de l'application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="f033f-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
