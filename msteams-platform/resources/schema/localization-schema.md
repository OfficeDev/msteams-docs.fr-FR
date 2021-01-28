---
title: Référence du schéma JSON du fichier de localisation
description: Décrit le schéma de localisation pris en charge par le fichier de localisation pour Microsoft Teams
ms.topic: reference
keywords: Localisation du schéma de manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: 696a65de70a63e767f8fcdb040364fe90cde8716
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014599"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="9e7e3-104">Référence : schéma JSON du fichier de localisation</span><span class="sxs-lookup"><span data-stu-id="9e7e3-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="9e7e3-105">Le fichier de localisation de Microsoft Teams décrit les traductions linguistiques qui seront servies en fonction des paramètres de langue du client.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="9e7e3-106">Votre fichier doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="9e7e3-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="9e7e3-107">Pour plus d’informations, [voir localisation d’application.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="9e7e3-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="9e7e3-108">Échantillon</span><span class="sxs-lookup"><span data-stu-id="9e7e3-108">Sample</span></span>

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

<span data-ttu-id="9e7e3-109">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="9e7e3-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="9e7e3-110">$schema</span><span class="sxs-lookup"><span data-stu-id="9e7e3-110">$schema</span></span>

<span data-ttu-id="9e7e3-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-111">**URI**</span></span>

<span data-ttu-id="9e7e3-112">L https:// URL référente au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="9e7e3-113">Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code : `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="9e7e3-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="9e7e3-114">name.short</span><span class="sxs-lookup"><span data-stu-id="9e7e3-114">name.short</span></span>

<span data-ttu-id="9e7e3-115">**Chaîne, longueur maximale 30**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-115">**String, Max Length 30**</span></span>

<span data-ttu-id="9e7e3-116">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="9e7e3-117">name.full</span><span class="sxs-lookup"><span data-stu-id="9e7e3-117">name.full</span></span>

<span data-ttu-id="9e7e3-118">**Chaîne, longueur maximale 100**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-118">**String, Max Length 100**</span></span>

<span data-ttu-id="9e7e3-119">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="9e7e3-120">description.short</span><span class="sxs-lookup"><span data-stu-id="9e7e3-120">description.short</span></span>

<span data-ttu-id="9e7e3-121">**Chaîne, longueur maximale 80**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-121">**String, Max Length 80**</span></span>

<span data-ttu-id="9e7e3-122">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="9e7e3-123">description.full</span><span class="sxs-lookup"><span data-stu-id="9e7e3-123">description.full</span></span>

<span data-ttu-id="9e7e3-124">**Chaîne, longueur maximale 4000**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="9e7e3-125">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="9e7e3-126">staticTabs \\ [([0-9]|1[0-5]) \\ ] \\ .name</span><span class="sxs-lookup"><span data-stu-id="9e7e3-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="9e7e3-127">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-127">**String, Max Length 128**</span></span>

<span data-ttu-id="9e7e3-128">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="9e7e3-129">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="9e7e3-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="9e7e3-130">**Chaîne, longueur maximale 32**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-130">**String, Max Length 32**</span></span>

<span data-ttu-id="9e7e3-131">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="9e7e3-132">bots \\ [0 \\ ] \\ .commandLists \\ [[0-2] \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="9e7e3-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="9e7e3-133">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-133">**String, Max Length 128**</span></span>

<span data-ttu-id="9e7e3-134">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="9e7e3-135">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="9e7e3-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="9e7e3-136">**Chaîne, longueur maximale 32**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-136">**String, Max Length 32**</span></span>

<span data-ttu-id="9e7e3-137">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="9e7e3-138">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="9e7e3-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="9e7e3-139">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-139">**String, Max Length 128**</span></span>

<span data-ttu-id="9e7e3-140">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="9e7e3-141">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="9e7e3-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="9e7e3-142">**Chaîne, longueur maximale 32**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-142">**String, Max Length 32**</span></span>

<span data-ttu-id="9e7e3-143">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="9e7e3-144">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .description</span><span class="sxs-lookup"><span data-stu-id="9e7e3-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="9e7e3-145">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-145">**String, Max Length 128**</span></span>

<span data-ttu-id="9e7e3-146">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="9e7e3-147">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .value</span><span class="sxs-lookup"><span data-stu-id="9e7e3-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="9e7e3-148">**Chaîne, longueur maximale 512**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-148">**String, Max Length 512**</span></span>

<span data-ttu-id="9e7e3-149">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="9e7e3-150">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .parameters \\ [[0-4] \\ ] \\ .choices \\ [[0-9] \\ ] \\ .title</span><span class="sxs-lookup"><span data-stu-id="9e7e3-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="9e7e3-151">**Chaîne, longueur maximale 128**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-151">**String, Max Length 128**</span></span>

<span data-ttu-id="9e7e3-152">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="9e7e3-153">composeExtensions \\ [0 \\ ] \\ .commands \\ [[0-9] \\ ] \\ .taskInfo \\ .title</span><span class="sxs-lookup"><span data-stu-id="9e7e3-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="9e7e3-154">**Chaîne, longueur maximale 64**</span><span class="sxs-lookup"><span data-stu-id="9e7e3-154">**String, Max Length 64**</span></span>

<span data-ttu-id="9e7e3-155">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="9e7e3-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
