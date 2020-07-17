---
title: Référence du schéma JSON du fichier de localisation
description: Décrit le schéma de localisation pris en charge par le fichier de localisation pour Microsoft teams
keywords: Localisation de schéma de manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: 061729ecb5110c99d8f85f144796f1a78b266c3d
ms.sourcegitcommit: bac0226d9048c363d96bbaf6f5395388c5f5c45a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2020
ms.locfileid: "45039278"
---
# <a name="reference-localization-file-json-schema"></a><span data-ttu-id="a13ec-104">Référence : schéma JSON du fichier de localisation</span><span class="sxs-lookup"><span data-stu-id="a13ec-104">Reference: Localization file JSON schema</span></span>

<span data-ttu-id="a13ec-105">Le fichier de localisation Microsoft teams décrit les traductions de langue qui seront fournies en fonction des paramètres de langue du client.</span><span class="sxs-lookup"><span data-stu-id="a13ec-105">The Microsoft Teams localization file describes language translations that will be served based on the client language settings.</span></span> <span data-ttu-id="a13ec-106">Votre fichier doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="a13ec-106">Your file must conform to the schema hosted at [`https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json`](https://developer.microsoft.com/en-us/json-schemas/teams/v1.7/MicrosoftTeams.Localization.schema.json).</span></span> <span data-ttu-id="a13ec-107">Pour plus d’informations, consultez la rubrique [Localization App](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="a13ec-107">For additional information see [app localization](~/concepts/build-and-test/apps-localization.md).</span></span>

## <a name="sample"></a><span data-ttu-id="a13ec-108">Exemple</span><span class="sxs-lookup"><span data-stu-id="a13ec-108">Sample</span></span>

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

<span data-ttu-id="a13ec-109">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a13ec-109">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="a13ec-110">$schema</span><span class="sxs-lookup"><span data-stu-id="a13ec-110">$schema</span></span>

<span data-ttu-id="a13ec-111">**URI**</span><span class="sxs-lookup"><span data-stu-id="a13ec-111">**URI**</span></span>

<span data-ttu-id="a13ec-112">URL https://référençant le schéma JSON du manifeste.</span><span class="sxs-lookup"><span data-stu-id="a13ec-112">The https:// URL referencing the JSON Schema for the manifest.</span></span>

> [!TIP]
> <span data-ttu-id="a13ec-113">Spécifiez le schéma au début de votre manifeste pour activer IntelliSense ou une prise en charge similaire à partir de votre éditeur de code :`"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span><span class="sxs-lookup"><span data-stu-id="a13ec-113">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor: `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`</span></span>

## <a name="nameshort"></a><span data-ttu-id="a13ec-114">Name. Short</span><span class="sxs-lookup"><span data-stu-id="a13ec-114">name.short</span></span>

<span data-ttu-id="a13ec-115">**Chaîne, longueur maximale 30**</span><span class="sxs-lookup"><span data-stu-id="a13ec-115">**String, Max Length 30**</span></span>

<span data-ttu-id="a13ec-116">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-116">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="namefull"></a><span data-ttu-id="a13ec-117">Name. Full</span><span class="sxs-lookup"><span data-stu-id="a13ec-117">name.full</span></span>

<span data-ttu-id="a13ec-118">**Chaîne, longueur maxi 100**</span><span class="sxs-lookup"><span data-stu-id="a13ec-118">**String, Max Length 100**</span></span>

<span data-ttu-id="a13ec-119">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-119">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionshort"></a><span data-ttu-id="a13ec-120">Description. Short</span><span class="sxs-lookup"><span data-stu-id="a13ec-120">description.short</span></span>

<span data-ttu-id="a13ec-121">**Chaîne, longueur maxi 80**</span><span class="sxs-lookup"><span data-stu-id="a13ec-121">**String, Max Length 80**</span></span>

<span data-ttu-id="a13ec-122">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-122">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="descriptionfull"></a><span data-ttu-id="a13ec-123">Description. Full</span><span class="sxs-lookup"><span data-stu-id="a13ec-123">description.full</span></span>

<span data-ttu-id="a13ec-124">**Chaîne, longueur maxi 4000**</span><span class="sxs-lookup"><span data-stu-id="a13ec-124">**String, Max Length 4000**</span></span>

<span data-ttu-id="a13ec-125">Remplace la chaîne correspondante du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-125">Replaces the corresponding string from the app manifest with the value provided here.</span></span>

## <a name="statictabs0-910-5name"></a><span data-ttu-id="a13ec-126">staticTabs \\ [([0-9] | 1 [0-5]) \\ ] \\ . nom</span><span class="sxs-lookup"><span data-stu-id="a13ec-126">staticTabs\\[([0-9]|1[0-5])\\]\\.name</span></span>

<span data-ttu-id="a13ec-127">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="a13ec-127">**String, Max Length 128**</span></span>

<span data-ttu-id="a13ec-128">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-128">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9title"></a><span data-ttu-id="a13ec-129">robots \\ [0 \\ ] \\ . commandLists \\ [[0-2] \\ ] \\ . Commands \\ [[0-9] \\ ] \\ . title</span><span class="sxs-lookup"><span data-stu-id="a13ec-129">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="a13ec-130">**Chaîne, longueur maxi 32**</span><span class="sxs-lookup"><span data-stu-id="a13ec-130">**String, Max Length 32**</span></span>

<span data-ttu-id="a13ec-131">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-131">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="bots0commandlists0-2commands0-9description"></a><span data-ttu-id="a13ec-132">robots \\ [0 \\ ] \\ . commandLists \\ [[0-2] \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Description</span><span class="sxs-lookup"><span data-stu-id="a13ec-132">bots\\[0\\]\\.commandLists\\[[0-2]\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="a13ec-133">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="a13ec-133">**String, Max Length 128**</span></span>

<span data-ttu-id="a13ec-134">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-134">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9title"></a><span data-ttu-id="a13ec-135">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . title</span><span class="sxs-lookup"><span data-stu-id="a13ec-135">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="a13ec-136">**Chaîne, longueur maxi 32**</span><span class="sxs-lookup"><span data-stu-id="a13ec-136">**String, Max Length 32**</span></span>

<span data-ttu-id="a13ec-137">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-137">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9description"></a><span data-ttu-id="a13ec-138">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Description</span><span class="sxs-lookup"><span data-stu-id="a13ec-138">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.description</span></span>

<span data-ttu-id="a13ec-139">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="a13ec-139">**String, Max Length 128**</span></span>

<span data-ttu-id="a13ec-140">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-140">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4title"></a><span data-ttu-id="a13ec-141">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . title</span><span class="sxs-lookup"><span data-stu-id="a13ec-141">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.title</span></span>

<span data-ttu-id="a13ec-142">**Chaîne, longueur maxi 32**</span><span class="sxs-lookup"><span data-stu-id="a13ec-142">**String, Max Length 32**</span></span>

<span data-ttu-id="a13ec-143">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-143">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4description"></a><span data-ttu-id="a13ec-144">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . Description</span><span class="sxs-lookup"><span data-stu-id="a13ec-144">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.description</span></span>

<span data-ttu-id="a13ec-145">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="a13ec-145">**String, Max Length 128**</span></span>

<span data-ttu-id="a13ec-146">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-146">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4value"></a><span data-ttu-id="a13ec-147">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . Value</span><span class="sxs-lookup"><span data-stu-id="a13ec-147">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.value</span></span>

<span data-ttu-id="a13ec-148">**Chaîne, longueur maxi 512**</span><span class="sxs-lookup"><span data-stu-id="a13ec-148">**String, Max Length 512**</span></span>

<span data-ttu-id="a13ec-149">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-149">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9parameters0-4choices0-9title"></a><span data-ttu-id="a13ec-150">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . Parameters \\ [[0-4] \\ ] \\ . Choices [ \\ [0-9] \\ ] \\ . title</span><span class="sxs-lookup"><span data-stu-id="a13ec-150">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.parameters\\[[0-4]\\]\\.choices\\[[0-9]\\]\\.title</span></span>

<span data-ttu-id="a13ec-151">**Chaîne, longueur maxi 128**</span><span class="sxs-lookup"><span data-stu-id="a13ec-151">**String, Max Length 128**</span></span>

<span data-ttu-id="a13ec-152">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-152">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>

## <a name="composeextensions0commands0-9taskinfotitle"></a><span data-ttu-id="a13ec-153">composeExtensions \\ [0 \\ ] \\ . commandes \\ [[0-9] \\ ] \\ . TaskInfo \\ . title</span><span class="sxs-lookup"><span data-stu-id="a13ec-153">composeExtensions\\[0\\]\\.commands\\[[0-9]\\]\\.taskInfo\\.title</span></span>

<span data-ttu-id="a13ec-154">**Chaîne, longueur maxi 64**</span><span class="sxs-lookup"><span data-stu-id="a13ec-154">**String, Max Length 64**</span></span>

<span data-ttu-id="a13ec-155">Remplace la ou les chaînes correspondantes du manifeste de l’application par la valeur fournie ici.</span><span class="sxs-lookup"><span data-stu-id="a13ec-155">Replaces the corresponding string(s) from the app manifest with the value provided here.</span></span>
