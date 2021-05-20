---
title: Localisation de votre application
description: Décrit les considérations pour la localisation de votre Microsoft Teams appe.
ms.topic: conceptual
localization_priority: Normal
keywords: les équipes publient le langage de localisation AppSource d’édition de bureau de magasin
ms.date: 05/15/2018
ms.openlocfilehash: a55b8af97e5306843858e5844a017dd402ab3516
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566046"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="a3d34-104">Localisation des applications Microsoft Teams vidéo</span><span class="sxs-lookup"><span data-stu-id="a3d34-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="a3d34-105">Lors de la Microsoft Teams votre application, vous devez tenir compte des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a3d34-105">When localizing your Microsoft Teams app, you must consider the following:</span></span>

1. <span data-ttu-id="a3d34-106">Votre Teams magasin (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="a3d34-106">Your Teams store listing (if applicable).</span></span>
1. <span data-ttu-id="a3d34-107">L’utilisateur final faisant face à des chaînes dans votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="a3d34-107">The end-user facing strings in your app manifest.</span></span> <span data-ttu-id="a3d34-108">Par exemple, les commandes bot.</span><span class="sxs-lookup"><span data-stu-id="a3d34-108">For example bot commands.</span></span>
1. <span data-ttu-id="a3d34-109">Répondre au texte localisé soumis par vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a3d34-109">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="a3d34-110">Localisation de votre annonce AppSource</span><span class="sxs-lookup"><span data-stu-id="a3d34-110">Localizing your AppSource listing</span></span>

<span data-ttu-id="a3d34-111">Si vous publiez dans le magasin, vous devez être conscient que la localisation de votre annonce AppSource n’est pas encore prise en charge.</span><span class="sxs-lookup"><span data-stu-id="a3d34-111">If you're publishing to the store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="a3d34-112">Toutefois, en vue de la prise en charge des annonces localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre annonce.</span><span class="sxs-lookup"><span data-stu-id="a3d34-112">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="a3d34-113">Actuellement, seules les informations par défaut (en anglais) que vous fournissez [dans Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) pour votre annonce apparaîtront dans la liste du site Web [d’AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) pour votre application.</span><span class="sxs-lookup"><span data-stu-id="a3d34-113">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

### <a name="example-of-configuring-localization"></a><span data-ttu-id="a3d34-114">Exemple de localisation configurante</span><span class="sxs-lookup"><span data-stu-id="a3d34-114">Example of configuring localization</span></span>

<span data-ttu-id="a3d34-115">Pour configurer une langue supplémentaire pour votre application, dans [Partner Center, sélectionnez](/office/dev/store/submit-to-appsource-via-partner-center)à la fois l’anglais et la langue supplémentaire de l’application.</span><span class="sxs-lookup"><span data-stu-id="a3d34-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="a3d34-116">Français est utilisé dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="a3d34-116">French is used in this example:</span></span>

1. <span data-ttu-id="a3d34-117">Ajouter la langue anglaise</span><span class="sxs-lookup"><span data-stu-id="a3d34-117">Add English language</span></span>
    * <span data-ttu-id="a3d34-118">Remplissez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="a3d34-118">Fill in the app name.</span></span>
    * <span data-ttu-id="a3d34-119">Remplissez une courte description de l’application en anglais.</span><span class="sxs-lookup"><span data-stu-id="a3d34-119">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="a3d34-120">Remplissez la longue description de l’application en anglais.</span><span class="sxs-lookup"><span data-stu-id="a3d34-120">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="a3d34-121">Dans la longue description, s’il vous plaît également ajouter la ligne « Cette application est disponible en « Français ».</span><span class="sxs-lookup"><span data-stu-id="a3d34-121">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="a3d34-122">Télécharger les images de votre interface utilisateur (en anglais).</span><span class="sxs-lookup"><span data-stu-id="a3d34-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="a3d34-123">Ajouter Français langue</span><span class="sxs-lookup"><span data-stu-id="a3d34-123">Add French language</span></span>
    * <span data-ttu-id="a3d34-124">Remplissez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="a3d34-124">Fill in the app name.</span></span>
    * <span data-ttu-id="a3d34-125">Remplissez une courte description de l’application dans Français.</span><span class="sxs-lookup"><span data-stu-id="a3d34-125">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="a3d34-126">Remplissez la longue description de l’application dans Français.</span><span class="sxs-lookup"><span data-stu-id="a3d34-126">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="a3d34-127">Télécharger les images de l’interface utilisateur de votre application (en Français).</span><span class="sxs-lookup"><span data-stu-id="a3d34-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="a3d34-128">Les images que vous téléchargez avec la langue anglaise seront ceux utilisés dans AppSource.</span><span class="sxs-lookup"><span data-stu-id="a3d34-128">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="a3d34-129">Localisation des chaînes dans le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="a3d34-129">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="a3d34-130">Vous devez utiliser le schéma Microsoft Teams’application v1.5+ pour bien localisér votre application.</span><span class="sxs-lookup"><span data-stu-id="a3d34-130">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="a3d34-131">Vous pouvez le faire en fixant `$schema` l’attribut dans votre manifest.jsdans le fichier https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json à « » et en mettant à jour la propriété « manifestVersion » à « 1,7 ».</span><span class="sxs-lookup"><span data-stu-id="a3d34-131">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="a3d34-132">Exemple manifest.jssur le changement</span><span class="sxs-lookup"><span data-stu-id="a3d34-132">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="a3d34-133">Vous souhaitez ensuite ajouter la propriété 'localizationInfo' avec le langage par défaut que votre application prend en charge.</span><span class="sxs-lookup"><span data-stu-id="a3d34-133">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="a3d34-134">Le langage par défaut est utilisé comme langue de récupération finale si les paramètres clients de l’utilisateur ne correspondent à aucune de vos langues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a3d34-134">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="a3d34-135">Exemple manifest.jssur le changement</span><span class="sxs-lookup"><span data-stu-id="a3d34-135">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="a3d34-136">Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de tous les utilisateurs faisant face à des chaînes dans votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="a3d34-136">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="a3d34-137">Ces fichiers doivent adhérer au schéma [JSON du fichier de localisation et](../../resources/schema/localization-schema.md) ils doivent être ajoutés à la propriété 'localisationInfo' de votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="a3d34-137">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="a3d34-138">Chaque fichier est corrélé à une balise de langue que Teams client utilise pour choisir les chaînes appropriées.</span><span class="sxs-lookup"><span data-stu-id="a3d34-138">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="a3d34-139">L’étiquette linguistique prend la forme <language> - <region> de, mais il est recommandé d’omettre <region> la partie pour cibler toutes les régions qui soutiennent la langue désirée.</span><span class="sxs-lookup"><span data-stu-id="a3d34-139">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="a3d34-140">Le Teams client appliquera les chaînes dans cet ordre : chaînes de langage par défaut -> la langue de l’utilisateur ne fait que des chaînes -> langue de l’utilisateur + chaînes de région de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a3d34-140">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="a3d34-141">Par exemple, vous fournissez une langue par défaut de « fr » (Français, toutes les régions), et des fichiers linguistiques supplémentaires pour « fr » (anglais, toutes les régions) et « en-gb » (anglais, Grande-Bretagne).</span><span class="sxs-lookup"><span data-stu-id="a3d34-141">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="a3d34-142">Si la langue de l’utilisateur est définie sur 'en-gb':</span><span class="sxs-lookup"><span data-stu-id="a3d34-142">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="a3d34-143">Le Teams client prendra les cordes 'fr' les écraser avec les cordes 'en'.</span><span class="sxs-lookup"><span data-stu-id="a3d34-143">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="a3d34-144">Écraser ceux qui ont les cordes 'en-gb'.</span><span class="sxs-lookup"><span data-stu-id="a3d34-144">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="a3d34-145">Si la langue de l’utilisateur est définie sur « en-ca » :</span><span class="sxs-lookup"><span data-stu-id="a3d34-145">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="a3d34-146">Le Teams client prendra les cordes 'fr' les écraser avec les cordes 'en'.</span><span class="sxs-lookup"><span data-stu-id="a3d34-146">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="a3d34-147">Comme aucune localisation « en-ca » n’est fournie, les localisations « en » seront utilisées.</span><span class="sxs-lookup"><span data-stu-id="a3d34-147">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="a3d34-148">Si la langue de l’utilisateur est définie sur « es-es », le client Teams prendra les chaînes « fr » et ne les remplacera pas avec l’un des fichiers linguistiques.</span><span class="sxs-lookup"><span data-stu-id="a3d34-148">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="a3d34-149">Par conséquent, il est fortement recommandé de fournir des traductions de haut niveau, uniquement en langue dans votre manifeste (« fr » au lieu de « en-us ») et de ne fournir des dérogations au niveau régional pour les quelques chaînes qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="a3d34-149">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="a3d34-150">Exemple manifest.jssur le changement</span><span class="sxs-lookup"><span data-stu-id="a3d34-150">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="a3d34-151">Exemple de localisation .json fichier</span><span class="sxs-lookup"><span data-stu-id="a3d34-151">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="a3d34-152">Traitement des soumissions de texte localisées de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="a3d34-152">Handling localized text submissions from your users</span></span>

<span data-ttu-id="a3d34-153">Si vous fournissez des versions localisées de votre application, il est très probable que vos utilisateurs répondront avec la même langue.</span><span class="sxs-lookup"><span data-stu-id="a3d34-153">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="a3d34-154">Teams ne traduit pas les soumissions de l’utilisateur dans la langue par défaut, de sorte que votre application devra gérer cela.</span><span class="sxs-lookup"><span data-stu-id="a3d34-154">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="a3d34-155">Par exemple, si vous fournissez une `commandList` localisée, les réponses à votre bot seront le texte localisé de la commande, pas la langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="a3d34-155">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="a3d34-156">Votre application devra répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="a3d34-156">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="a3d34-157">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="a3d34-157">Code sample</span></span>

| <span data-ttu-id="a3d34-158">Nom de l’échantillon</span><span class="sxs-lookup"><span data-stu-id="a3d34-158">Sample name</span></span> | <span data-ttu-id="a3d34-159">Description</span><span class="sxs-lookup"><span data-stu-id="a3d34-159">Description</span></span> | <span data-ttu-id="a3d34-160">.NET</span><span class="sxs-lookup"><span data-stu-id="a3d34-160">.NET</span></span> |
|-------------|-------------|------|
| <span data-ttu-id="a3d34-161">Localisation des applications</span><span class="sxs-lookup"><span data-stu-id="a3d34-161">App Localization</span></span> | <span data-ttu-id="a3d34-162">Microsoft Teams localisation de l’application à l’aide de bot et onglet.</span><span class="sxs-lookup"><span data-stu-id="a3d34-162">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="a3d34-163">View</span><span class="sxs-lookup"><span data-stu-id="a3d34-163">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


