---
title: Localisation de votre application
description: Décrit les considérations pour la recherche de votre application Microsoft Teams.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publient la langue de localisation d'AppSource de publication office dans le Store
ms.date: 05/15/2018
ms.openlocfilehash: 8490230ad0b268d402a9ad7deb5f8b1e3f420f9d
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020848"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="272bd-104">Localisation des applications Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="272bd-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="272bd-105">Lorsque vous localisez votre application Microsoft Teams, vous devez tenir compte de trois aspects importants.</span><span class="sxs-lookup"><span data-stu-id="272bd-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="272bd-106">Votre liste AppSource (si vous publiez dans l'App Store).</span><span class="sxs-lookup"><span data-stu-id="272bd-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="272bd-107">Chaînes orientées utilisateur final dans le manifeste de votre application (par exemple, commandes de bot).</span><span class="sxs-lookup"><span data-stu-id="272bd-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="272bd-108">Réponse au texte local envoyé par vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="272bd-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="272bd-109">Localisation de votre liste AppSource</span><span class="sxs-lookup"><span data-stu-id="272bd-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="272bd-110">Si vous publiez dans l'App Store, vous devez savoir que la recherche dans AppSource n'est pas encore prise en charge.</span><span class="sxs-lookup"><span data-stu-id="272bd-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="272bd-111">Toutefois, en vue de la prise en charge des listes localisées dans l'App Store, vous pouvez ajouter des langues supplémentaires à votre liste.</span><span class="sxs-lookup"><span data-stu-id="272bd-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="272bd-112">Actuellement, seules les informations de langue par défaut (anglais) que vous fournissez dans [l'Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) pour votre liste s'affichent dans la liste du site web [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) pour votre application.</span><span class="sxs-lookup"><span data-stu-id="272bd-112">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="272bd-113">Pour configurer une langue supplémentaire pour votre application, dans [l'Partner Center,](/office/dev/store/submit-to-appsource-via-partner-center)sélectionnez l'anglais et la langue supplémentaire de l'application.</span><span class="sxs-lookup"><span data-stu-id="272bd-113">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="272bd-114">Le français est utilisé dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="272bd-114">French is used in this example.</span></span>

1. <span data-ttu-id="272bd-115">Ajouter l'anglais</span><span class="sxs-lookup"><span data-stu-id="272bd-115">Add English language</span></span>
    * <span data-ttu-id="272bd-116">Remplissez le nom de l'application.</span><span class="sxs-lookup"><span data-stu-id="272bd-116">Fill in the app name.</span></span>
    * <span data-ttu-id="272bd-117">Remplissez une brève description de l'application en anglais.</span><span class="sxs-lookup"><span data-stu-id="272bd-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="272bd-118">Remplissez la description longue de l'application en anglais.</span><span class="sxs-lookup"><span data-stu-id="272bd-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="272bd-119">Dans la description longue, ajoutez également la ligne « Cette application est disponible en français ».</span><span class="sxs-lookup"><span data-stu-id="272bd-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="272bd-120">Téléchargez les images de l'interface utilisateur de votre application (en anglais).</span><span class="sxs-lookup"><span data-stu-id="272bd-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="272bd-121">Ajouter le français</span><span class="sxs-lookup"><span data-stu-id="272bd-121">Add French language</span></span>
    * <span data-ttu-id="272bd-122">Remplissez le nom de l'application.</span><span class="sxs-lookup"><span data-stu-id="272bd-122">Fill in the app name.</span></span>
    * <span data-ttu-id="272bd-123">Remplissez une brève description de l'application en français.</span><span class="sxs-lookup"><span data-stu-id="272bd-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="272bd-124">Remplissez la description longue de l'application en français.</span><span class="sxs-lookup"><span data-stu-id="272bd-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="272bd-125">Téléchargez les images de l'interface utilisateur de votre application (en français).</span><span class="sxs-lookup"><span data-stu-id="272bd-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="272bd-126">Les images que vous téléchargez avec l'anglais seront utilisées dans AppSource.</span><span class="sxs-lookup"><span data-stu-id="272bd-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="272bd-127">Localisation des chaînes dans le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="272bd-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="272bd-128">Vous devez utiliser le schéma d'application Microsoft Teams v1.5+ pour localiser correctement votre application.</span><span class="sxs-lookup"><span data-stu-id="272bd-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="272bd-129">Pour ce faire, vous pouvez définir l'attribut de votre manifest.jssur « ' » et mettre à jour la propriété « manifestVersion » sur `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json « 1.7 ».</span><span class="sxs-lookup"><span data-stu-id="272bd-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="272bd-130">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="272bd-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="272bd-131">Vous souhaitez ensuite ajouter la propriété « localizationInfo » avec la langue par défaut que votre application prend en charge.</span><span class="sxs-lookup"><span data-stu-id="272bd-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="272bd-132">La langue par défaut est utilisée comme langue de base finale si les paramètres client de l'utilisateur ne correspondent à aucune de vos langues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="272bd-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="272bd-133">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="272bd-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="272bd-134">Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de toutes les chaînes orientées utilisateur dans votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="272bd-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="272bd-135">Ces fichiers doivent adhérer au schéma [JSON](../../resources/schema/localization-schema.md) du fichier de localisation et ils doivent être ajoutés à la propriété « localizationInfo » de votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="272bd-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="272bd-136">Chaque fichier correspond à une balise de langue que le client Teams utilise pour choisir les chaînes appropriées.</span><span class="sxs-lookup"><span data-stu-id="272bd-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="272bd-137">La balise de langue prend la forme de, mais il est recommandé d'omettre la partie pour cibler toutes les régions qui prennent en charge <language> - <region> la <region> langue souhaitée.</span><span class="sxs-lookup"><span data-stu-id="272bd-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="272bd-138">Le client Teams applique les chaînes dans cet ordre : chaînes de langue par défaut -> chaînes de langue de l'utilisateur uniquement -> langue de l'utilisateur + chaînes de région de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="272bd-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="272bd-139">Par exemple, vous fournissez une langue par défaut « fr » (français, toutes les régions) et des fichiers linguistiques supplémentaires pour « en » (anglais, toutes les régions) et « en-gb » (anglais, Grande-France).</span><span class="sxs-lookup"><span data-stu-id="272bd-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="272bd-140">Si la langue de l'utilisateur est définie sur « en-gb » :</span><span class="sxs-lookup"><span data-stu-id="272bd-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="272bd-141">Le client Teams prend les chaînes « fr » pour les réécrire avec les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="272bd-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="272bd-142">Overwrite those with the 'en-gb' strings.</span><span class="sxs-lookup"><span data-stu-id="272bd-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="272bd-143">Si la langue de l'utilisateur est définie sur « en-ca » :</span><span class="sxs-lookup"><span data-stu-id="272bd-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="272bd-144">Le client Teams prend les chaînes « fr » pour les réécrire avec les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="272bd-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="272bd-145">Étant donné qu'aucune localisation « en-ca » n'est fournie, les localisations « en » seront utilisées.</span><span class="sxs-lookup"><span data-stu-id="272bd-145">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="272bd-146">Si la langue de l'utilisateur est définie sur « es-es » (es-es), le client Teams prend les chaînes « fr » et ne les remplace pas par les fichiers de langue.</span><span class="sxs-lookup"><span data-stu-id="272bd-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="272bd-147">Par conséquent, il est vivement recommandé de fournir des traductions linguistiques de niveau supérieur uniquement dans votre manifeste ('en' au lieu de « en-us » ) et de fournir uniquement des substitutions au niveau de la région pour les chaînes qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="272bd-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="272bd-148">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="272bd-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="272bd-149">Exemple de fichier .json de localisation</span><span class="sxs-lookup"><span data-stu-id="272bd-149">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="272bd-150">Gestion des envois de texte localisées de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="272bd-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="272bd-151">Si vous fournissez des versions localisées de votre application, il est très probable que vos utilisateurs répondent avec la même langue.</span><span class="sxs-lookup"><span data-stu-id="272bd-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="272bd-152">Teams ne traduit pas les soumissions des utilisateurs dans la langue par défaut. Votre application devra donc gérer cela.</span><span class="sxs-lookup"><span data-stu-id="272bd-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="272bd-153">Par exemple, si vous fournissez une valeur localisée, les réponses à votre bot seront le texte localisée de la commande, et non `commandList` la langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="272bd-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="272bd-154">Votre application devra répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="272bd-154">Your app will need to respond appropriately.</span></span>
