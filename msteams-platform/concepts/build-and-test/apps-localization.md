---
title: Localisation de votre application
description: Décrit les considérations à prendre en compte pour la Microsoft Teams application.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publish store office publishing AppSource localization language
ms.date: 05/15/2018
ms.openlocfilehash: 6dbdeb6d16c99aada23f8d74a92d958f9c29b69d
ms.sourcegitcommit: 118f7261d313feeac5b398fef56a44bd90104b2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2021
ms.locfileid: "52709627"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="f67df-104">Localisation pour les applications Microsoft Teams de recherche</span><span class="sxs-lookup"><span data-stu-id="f67df-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="f67df-105">Lorsque vous localisez votre Microsoft Teams, vous devez prendre en compte les considérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f67df-105">When localizing your Microsoft Teams app, you must consider the following:</span></span>

1. <span data-ttu-id="f67df-106">Votre Teams dans le Store (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="f67df-106">Your Teams store listing (if applicable).</span></span>
1. <span data-ttu-id="f67df-107">Chaînes orientées utilisateur final dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="f67df-107">The end-user facing strings in your app manifest.</span></span> <span data-ttu-id="f67df-108">Par exemple, commandes de bot.</span><span class="sxs-lookup"><span data-stu-id="f67df-108">For example bot commands.</span></span>
1. <span data-ttu-id="f67df-109">Réponse au texte local envoyé par vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f67df-109">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="f67df-110">Localisation de votre liste AppSource</span><span class="sxs-lookup"><span data-stu-id="f67df-110">Localizing your AppSource listing</span></span>

<span data-ttu-id="f67df-111">Si vous publiez dans le Store, sachez que la recherche dans AppSource n’est pas encore prise en charge.</span><span class="sxs-lookup"><span data-stu-id="f67df-111">If you're publishing to the store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="f67df-112">Toutefois, en vue de la prise en charge des listes localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre liste.</span><span class="sxs-lookup"><span data-stu-id="f67df-112">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="f67df-113">Actuellement, seules les informations de langue par défaut (anglais) que vous fournissez dans [l’Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) pour votre liste s’affichent dans la liste du site web [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) pour votre application.</span><span class="sxs-lookup"><span data-stu-id="f67df-113">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

### <a name="example-of-configuring-localization"></a><span data-ttu-id="f67df-114">Exemple de configuration de la localisation</span><span class="sxs-lookup"><span data-stu-id="f67df-114">Example of configuring localization</span></span>

<span data-ttu-id="f67df-115">Pour configurer une langue supplémentaire pour votre application, dans [l’Partner Center,](/office/dev/store/submit-to-appsource-via-partner-center)sélectionnez l’anglais et la langue supplémentaire de l’application.</span><span class="sxs-lookup"><span data-stu-id="f67df-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="f67df-116">Le français est utilisé dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="f67df-116">French is used in this example:</span></span>

1. <span data-ttu-id="f67df-117">Ajouter l’anglais</span><span class="sxs-lookup"><span data-stu-id="f67df-117">Add English language</span></span>
    * <span data-ttu-id="f67df-118">Remplissez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="f67df-118">Fill in the app name.</span></span>
    * <span data-ttu-id="f67df-119">Remplissez une brève description de l’application en anglais.</span><span class="sxs-lookup"><span data-stu-id="f67df-119">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="f67df-120">Remplissez la description longue de l’application en anglais.</span><span class="sxs-lookup"><span data-stu-id="f67df-120">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="f67df-121">Dans la description longue, ajoutez également la ligne « Cette application est disponible en français ».</span><span class="sxs-lookup"><span data-stu-id="f67df-121">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="f67df-122">Télécharger images de l’interface utilisateur de votre application (en anglais).</span><span class="sxs-lookup"><span data-stu-id="f67df-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="f67df-123">Ajouter le français</span><span class="sxs-lookup"><span data-stu-id="f67df-123">Add French language</span></span>
    * <span data-ttu-id="f67df-124">Remplissez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="f67df-124">Fill in the app name.</span></span>
    * <span data-ttu-id="f67df-125">Remplissez une brève description de l’application en français.</span><span class="sxs-lookup"><span data-stu-id="f67df-125">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="f67df-126">Remplissez la description longue de l’application en français.</span><span class="sxs-lookup"><span data-stu-id="f67df-126">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="f67df-127">Télécharger images de l’interface utilisateur de votre application (en français).</span><span class="sxs-lookup"><span data-stu-id="f67df-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="f67df-128">Les images que vous téléchargez avec l’anglais seront utilisées dans AppSource.</span><span class="sxs-lookup"><span data-stu-id="f67df-128">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="f67df-129">Localisation des chaînes dans le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="f67df-129">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="f67df-130">Vous devez utiliser le Microsoft Teams d’application v1.5+ pour localiser correctement votre application.</span><span class="sxs-lookup"><span data-stu-id="f67df-130">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="f67df-131">Pour ce faire, vous pouvez définir l’attribut de votre manifest.jssur « ' » et mettre à jour la propriété « manifestVersion » sur `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json « 1.7 ».</span><span class="sxs-lookup"><span data-stu-id="f67df-131">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="f67df-132">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="f67df-132">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="f67df-133">Vous souhaitez ensuite ajouter la propriété « localizationInfo » avec la langue par défaut que votre application prend en charge.</span><span class="sxs-lookup"><span data-stu-id="f67df-133">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="f67df-134">La langue par défaut est utilisée comme langue de base finale si les paramètres client de l’utilisateur ne correspondent à aucune de vos langues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f67df-134">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="f67df-135">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="f67df-135">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="f67df-136">Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de toutes les chaînes orientées utilisateur dans votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="f67df-136">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="f67df-137">Ces fichiers doivent adhérer au schéma [JSON](../../resources/schema/localization-schema.md) du fichier de localisation et ils doivent être ajoutés à la propriété « localizationInfo » de votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="f67df-137">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="f67df-138">Chaque fichier correspond à une balise de langue que le client Teams utilise pour choisir les chaînes appropriées.</span><span class="sxs-lookup"><span data-stu-id="f67df-138">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="f67df-139">La balise de langue prend la forme de, mais il est recommandé d’omettre la partie pour cibler toutes les régions qui prennent en charge <language> - <region> la <region> langue souhaitée.</span><span class="sxs-lookup"><span data-stu-id="f67df-139">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="f67df-140">Le client Teams appliquera les chaînes dans cet ordre : chaînes de langue par défaut -> chaînes de langue de l’utilisateur uniquement -> langue de l’utilisateur + chaînes de région de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f67df-140">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="f67df-141">Par exemple, vous fournissez une langue par défaut « fr » (français, toutes les régions) et des fichiers linguistiques supplémentaires pour « en » (anglais, toutes les régions) et « en-gb » (anglais, Grande-France).</span><span class="sxs-lookup"><span data-stu-id="f67df-141">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="f67df-142">Si la langue de l’utilisateur est définie sur « en-gb » :</span><span class="sxs-lookup"><span data-stu-id="f67df-142">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="f67df-143">Le Teams client prend les chaînes « fr » pour les réécrire par les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="f67df-143">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="f67df-144">Overwrite those with the 'en-gb' strings.</span><span class="sxs-lookup"><span data-stu-id="f67df-144">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="f67df-145">Si la langue de l’utilisateur est définie sur « en-ca » :</span><span class="sxs-lookup"><span data-stu-id="f67df-145">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="f67df-146">Le Teams client prend les chaînes « fr » pour les réécrire par les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="f67df-146">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="f67df-147">Étant donné qu’aucune localisation « en-ca » n’est fournie, les localisations « en » seront utilisées.</span><span class="sxs-lookup"><span data-stu-id="f67df-147">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="f67df-148">Si la langue de l’utilisateur est définie sur « es-es » (es-es), le client Teams prend les chaînes « fr » et ne les remplace par aucun des fichiers de langue.</span><span class="sxs-lookup"><span data-stu-id="f67df-148">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="f67df-149">Par conséquent, il est vivement recommandé de fournir des traductions linguistiques de niveau supérieur uniquement dans votre manifeste ('en' au lieu de « en-us » ) et de fournir uniquement des substitutions au niveau de la région pour les chaînes qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="f67df-149">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="f67df-150">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="f67df-150">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en",
    "additionalLanguages": [
      {
        "languageTag": "en-gb",
        "file": "en-gb.json"
      },
      {
        "languageTag": "fr",
        "file": "fr.json"
      },
      {
        "languageTag": "pl",
        "file": "pl.json"
      }
    ]
  }
  ...
}
```

### <a name="example-localization-json-file"></a><span data-ttu-id="f67df-151">Exemple de fichier .json de localisation</span><span class="sxs-lookup"><span data-stu-id="f67df-151">Example localization .json file</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "name.short": "Le App",
  "name.full": "App pour Microsoft Teams",
  "description.short": "Créez d'excellentes applications pour Microsoft Teams avec App.",
  "description.full": "Créez de nouvelles applications Microsoft Teams, concevez et prévisualisez des cartes bot, et explorez la documentation avec App.",
  "staticTabs[0].name": "Editeur de manifest",
  "staticTabs[1].name": "Editeur de cartes",
  "staticTabs[2].name": "Bibliothèque de contrôles",
  "bots[0].commandLists[0].commands[0].title": "chercher",
  "bots[0].commandLists[0].commands[0].description": "Rechercher la documentation Teams pertinente"
}
```

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="f67df-152">Gestion des envois de texte localisées de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f67df-152">Handling localized text submissions from your users</span></span>

<span data-ttu-id="f67df-153">Si vous fournissez des versions localisées de votre application, il est très probable que vos utilisateurs répondent avec la même langue.</span><span class="sxs-lookup"><span data-stu-id="f67df-153">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="f67df-154">Teams ne traduit pas les soumissions de l’utilisateur dans la langue par défaut, votre application devra donc gérer cela.</span><span class="sxs-lookup"><span data-stu-id="f67df-154">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="f67df-155">Par exemple, si vous fournissez une valeur localisée, les réponses à votre bot seront le texte localisée de la commande, et non `commandList` la langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="f67df-155">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="f67df-156">Votre application devra répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="f67df-156">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="f67df-157">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="f67df-157">Code sample</span></span>

| <span data-ttu-id="f67df-158">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="f67df-158">Sample name</span></span> | <span data-ttu-id="f67df-159">Description</span><span class="sxs-lookup"><span data-stu-id="f67df-159">Description</span></span> | <span data-ttu-id="f67df-160">.NET</span><span class="sxs-lookup"><span data-stu-id="f67df-160">.NET</span></span> | <span data-ttu-id="f67df-161">Node.js</span><span class="sxs-lookup"><span data-stu-id="f67df-161">Node.js</span></span> |
|-------------|-------------|------|------|
| <span data-ttu-id="f67df-162">Localisation d’application</span><span class="sxs-lookup"><span data-stu-id="f67df-162">App Localization</span></span> | <span data-ttu-id="f67df-163">Microsoft Teams’application à l’aide du bot et de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="f67df-163">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="f67df-164">View</span><span class="sxs-lookup"><span data-stu-id="f67df-164">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[<span data-ttu-id="f67df-165">View</span><span class="sxs-lookup"><span data-stu-id="f67df-165">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |


