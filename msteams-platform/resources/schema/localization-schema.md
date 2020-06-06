---
title: Référence du schéma JSON du fichier de localisation
description: Décrit le schéma de localisation pris en charge par le fichier de localisation pour Microsoft teams
keywords: Localisation de schéma de manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: 14e08c582f065d1b09ff0f4906ca6788037460f1
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2020
ms.locfileid: "44590864"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="23ab4-104">Référence : schéma JSON du fichier de localisation</span><span class="sxs-lookup"><span data-stu-id="23ab4-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="23ab4-105">Le fichier de localisation Microsoft teams décrit les traductions de langue qui seront fournies en fonction des paramètres de langue du client.</span><span class="sxs-lookup"><span data-stu-id="23ab4-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="23ab4-106">Votre fichier doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="23ab4-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="23ab4-107">Pour plus d’informations, consultez la rubrique [Localization App](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="23ab4-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="23ab4-108">Exemple</span><span class="sxs-lookup"><span data-stu-id="23ab4-108">Sample</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
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

<span data-ttu-id="23ab4-109">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="23ab4-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="23ab4-110">$schema</span><span class="sxs-lookup"><span data-stu-id="23ab4-110">$schema</span></span>

<span data-ttu-id="23ab4-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="23ab4-111">**URI**</span></span>

<span data-ttu-id="23ab4-112">URL https://référençant le schéma JSON du manifeste.</span><span class="sxs-lookup"><span data-stu-id="23ab4-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="23ab4-113">Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code :`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="23ab4-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="23ab4-114">Name. Short</span><span class="sxs-lookup"><span data-stu-id="23ab4-114">name.short</span></span>

<span data-ttu-id="23ab4-115">**Chaîne, longueur maximale 30**</span><span class="sxs-lookup"><span data-stu-id="23ab4-115">**String, Max Length 30**</span></span>

<span data-ttu-id="23ab4-116">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="23ab4-117">Name. Full</span><span class="sxs-lookup"><span data-stu-id="23ab4-117">name.full</span></span>

<span data-ttu-id="23ab4-118">**Chaîne, longueur maxi 100**</span><span class="sxs-lookup"><span data-stu-id="23ab4-118">**String, Max Length 100**</span></span>

<span data-ttu-id="23ab4-119">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="23ab4-120">Description. Short</span><span class="sxs-lookup"><span data-stu-id="23ab4-120">description.short</span></span>

<span data-ttu-id="23ab4-121">**Chaîne, longueur maxi 80**</span><span class="sxs-lookup"><span data-stu-id="23ab4-121">**String, Max Length 80**</span></span>

<span data-ttu-id="23ab4-122">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="23ab4-123">Description. Full</span><span class="sxs-lookup"><span data-stu-id="23ab4-123">description.full</span></span>

<span data-ttu-id="23ab4-124">**Chaîne, longueur maxi 4000**</span><span class="sxs-lookup"><span data-stu-id="23ab4-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="23ab4-125">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="23ab4-126">staticTabs \\ [([0-9] | 1 [0-5]) \\ ] \\ . nom</span><span class="sxs-lookup"><span data-stu-id="23ab4-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="23ab4-127">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="23ab4-127">**String, Max Length 128**</span></span>

<span data-ttu-id="23ab4-128">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="23ab4-129">robots \\ [0 \\ ] \\ . commandLists \\ [[0-2] \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . title</span><span class="sxs-lookup"><span data-stu-id="23ab4-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="23ab4-130">**Chaîne, longueur maxi 32**</span><span class="sxs-lookup"><span data-stu-id="23ab4-130">**String, Max Length 32**</span></span>

<span data-ttu-id="23ab4-131">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="23ab4-132">robots \\ [0 \\ ] \\ . commandLists \\ [[0-2] \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Description</span><span class="sxs-lookup"><span data-stu-id="23ab4-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="23ab4-133">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="23ab4-133">**String, Max Length 128**</span></span>

<span data-ttu-id="23ab4-134">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="23ab4-135">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . title</span><span class="sxs-lookup"><span data-stu-id="23ab4-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="23ab4-136">**Chaîne, longueur maxi 32**</span><span class="sxs-lookup"><span data-stu-id="23ab4-136">**String, Max Length 32**</span></span>

<span data-ttu-id="23ab4-137">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="23ab4-138">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Description</span><span class="sxs-lookup"><span data-stu-id="23ab4-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="23ab4-139">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="23ab4-139">**String, Max Length 128**</span></span>

<span data-ttu-id="23ab4-140">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="23ab4-141">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . title</span><span class="sxs-lookup"><span data-stu-id="23ab4-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="23ab4-142">**Chaîne, longueur maxi 32**</span><span class="sxs-lookup"><span data-stu-id="23ab4-142">**String, Max Length 32**</span></span>

<span data-ttu-id="23ab4-143">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="23ab4-144">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . Description</span><span class="sxs-lookup"><span data-stu-id="23ab4-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="23ab4-145">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="23ab4-145">**String, Max Length 128**</span></span>

<span data-ttu-id="23ab4-146">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="23ab4-147">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . Value</span><span class="sxs-lookup"><span data-stu-id="23ab4-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="23ab4-148">**Chaîne, longueur maxi 512**</span><span class="sxs-lookup"><span data-stu-id="23ab4-148">**String, Max Length 512**</span></span>

<span data-ttu-id="23ab4-149">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="23ab4-150">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . Choices [ \\ [0-9] \\ ] \\ . title</span><span class="sxs-lookup"><span data-stu-id="23ab4-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="23ab4-151">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="23ab4-151">**String, Max Length 128**</span></span>

<span data-ttu-id="23ab4-152">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="23ab4-153">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . TaskInfo \\ . title</span><span class="sxs-lookup"><span data-stu-id="23ab4-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="23ab4-154">**Chaîne, longueur maxi 64**</span><span class="sxs-lookup"><span data-stu-id="23ab4-154">**String, Max Length 64**</span></span>

<span data-ttu-id="23ab4-155">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="23ab4-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>