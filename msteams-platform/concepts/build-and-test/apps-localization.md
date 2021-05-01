---
title: Localisation de votre application
description: Décrit les considérations à prendre en compte pour la Microsoft Teams application.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publient la langue de localisation d'AppSource de publication office dans le Store
ms.date: 05/15/2018
ms.openlocfilehash: 9a939b1990d1b09410af344f79dd39b8b02c404b
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101708"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="78e62-104">Localisation pour les applications Microsoft Teams de recherche</span><span class="sxs-lookup"><span data-stu-id="78e62-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="78e62-105">Lorsque vous localisez votre Microsoft Teams, vous devez prendre en compte les considérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="78e62-105">When localizing your Microsoft Teams app, you must consider the following:</span></span>

1. <span data-ttu-id="78e62-106">Votre Teams dans le Store (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="78e62-106">Your Teams store listing (if applicable).</span></span>
1. <span data-ttu-id="78e62-107">Chaînes orientées utilisateur final dans le manifeste de votre application (par exemple, commandes de bot).</span><span class="sxs-lookup"><span data-stu-id="78e62-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="78e62-108">Réponse au texte local envoyé par vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="78e62-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="78e62-109">Localisation de votre liste AppSource</span><span class="sxs-lookup"><span data-stu-id="78e62-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="78e62-110">Si vous publiez dans le Store, sachez que la recherche dans AppSource n'est pas encore prise en charge.</span><span class="sxs-lookup"><span data-stu-id="78e62-110">If you're publishing to the store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="78e62-111">Toutefois, en vue de la prise en charge des listes localisées dans l'App Store, vous pouvez ajouter des langues supplémentaires à votre liste.</span><span class="sxs-lookup"><span data-stu-id="78e62-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="78e62-112">Actuellement, seules les informations de langue par défaut (anglais) que vous fournissez dans [l'Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) pour votre liste s'affichent dans la liste du site web [AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) pour votre application.</span><span class="sxs-lookup"><span data-stu-id="78e62-112">Currently only the default (English) language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

### <a name="example-of-configuring-localization"></a><span data-ttu-id="78e62-113">Exemple de configuration de la localisation</span><span class="sxs-lookup"><span data-stu-id="78e62-113">Example of configuring localization</span></span>

<span data-ttu-id="78e62-114">Pour configurer une langue supplémentaire pour votre application, dans [l'Partner Center,](/office/dev/store/submit-to-appsource-via-partner-center)sélectionnez l'anglais et la langue supplémentaire de l'application.</span><span class="sxs-lookup"><span data-stu-id="78e62-114">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="78e62-115">Le français est utilisé dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="78e62-115">French is used in this example.</span></span>

1. <span data-ttu-id="78e62-116">Ajouter l'anglais</span><span class="sxs-lookup"><span data-stu-id="78e62-116">Add English language</span></span>
    * <span data-ttu-id="78e62-117">Remplissez le nom de l'application.</span><span class="sxs-lookup"><span data-stu-id="78e62-117">Fill in the app name.</span></span>
    * <span data-ttu-id="78e62-118">Remplissez une brève description de l'application en anglais.</span><span class="sxs-lookup"><span data-stu-id="78e62-118">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="78e62-119">Remplissez la description longue de l'application en anglais.</span><span class="sxs-lookup"><span data-stu-id="78e62-119">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="78e62-120">Dans la description longue, ajoutez également la ligne « Cette application est disponible en français ».</span><span class="sxs-lookup"><span data-stu-id="78e62-120">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="78e62-121">Télécharger images de l'interface utilisateur de votre application (en anglais).</span><span class="sxs-lookup"><span data-stu-id="78e62-121">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="78e62-122">Ajouter le français</span><span class="sxs-lookup"><span data-stu-id="78e62-122">Add French language</span></span>
    * <span data-ttu-id="78e62-123">Remplissez le nom de l'application.</span><span class="sxs-lookup"><span data-stu-id="78e62-123">Fill in the app name.</span></span>
    * <span data-ttu-id="78e62-124">Remplissez une brève description de l'application en français.</span><span class="sxs-lookup"><span data-stu-id="78e62-124">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="78e62-125">Remplissez la description longue de l'application en français.</span><span class="sxs-lookup"><span data-stu-id="78e62-125">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="78e62-126">Télécharger images de l'interface utilisateur de votre application (en français).</span><span class="sxs-lookup"><span data-stu-id="78e62-126">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="78e62-127">Les images que vous téléchargez avec l'anglais seront utilisées dans AppSource.</span><span class="sxs-lookup"><span data-stu-id="78e62-127">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="78e62-128">Localisation des chaînes dans le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="78e62-128">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="78e62-129">Vous devez utiliser le Microsoft Teams d'application v1.5+ pour localiser correctement votre application.</span><span class="sxs-lookup"><span data-stu-id="78e62-129">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="78e62-130">Pour ce faire, vous pouvez définir l'attribut de votre manifest.jssur « ' » et mettre à jour la propriété « manifestVersion » sur `$schema` https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json « 1.7 ».</span><span class="sxs-lookup"><span data-stu-id="78e62-130">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json' and updating the 'manifestVersion' property to '1.7'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="78e62-131">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="78e62-131">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.8/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="78e62-132">Vous souhaitez ensuite ajouter la propriété « localizationInfo » avec la langue par défaut que votre application prend en charge.</span><span class="sxs-lookup"><span data-stu-id="78e62-132">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="78e62-133">La langue par défaut est utilisée comme langue de base finale si les paramètres client de l'utilisateur ne correspondent à aucune de vos autres langues.</span><span class="sxs-lookup"><span data-stu-id="78e62-133">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="78e62-134">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="78e62-134">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="78e62-135">Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de toutes les chaînes orientées utilisateur dans votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="78e62-135">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="78e62-136">Ces fichiers doivent adhérer au schéma [JSON](../../resources/schema/localization-schema.md) du fichier de localisation et ils doivent être ajoutés à la propriété « localizationInfo » de votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="78e62-136">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="78e62-137">Chaque fichier correspond à une balise de langue que le client Teams utilise pour choisir les chaînes appropriées.</span><span class="sxs-lookup"><span data-stu-id="78e62-137">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="78e62-138">La balise de langue prend la forme de, mais il est recommandé d'omettre la partie pour cibler toutes les régions qui prennent en charge <language> - <region> la <region> langue souhaitée.</span><span class="sxs-lookup"><span data-stu-id="78e62-138">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="78e62-139">Le client Teams appliquera les chaînes dans cet ordre : chaînes de langue par défaut -> chaînes de langue de l'utilisateur uniquement -> langue de l'utilisateur + chaînes de région de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="78e62-139">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="78e62-140">Par exemple, vous fournissez une langue par défaut « fr » (français, toutes les régions) et des fichiers linguistiques supplémentaires pour « en » (anglais, toutes les régions) et « en-gb » (anglais, Grande-France).</span><span class="sxs-lookup"><span data-stu-id="78e62-140">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="78e62-141">Si la langue de l'utilisateur est définie sur « en-gb » :</span><span class="sxs-lookup"><span data-stu-id="78e62-141">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="78e62-142">Le Teams client prend les chaînes « fr » pour les réécrire par les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="78e62-142">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="78e62-143">Overwrite those with the 'en-gb' strings.</span><span class="sxs-lookup"><span data-stu-id="78e62-143">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="78e62-144">Si la langue de l'utilisateur est définie sur « en-ca » :</span><span class="sxs-lookup"><span data-stu-id="78e62-144">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="78e62-145">Le Teams client prend les chaînes « fr » pour les réécrire par les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="78e62-145">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="78e62-146">Étant donné qu'aucune localisation « en-ca » n'est fournie, les localisations « en » seront utilisées.</span><span class="sxs-lookup"><span data-stu-id="78e62-146">Since no 'en-ca' localization is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="78e62-147">Si la langue de l'utilisateur est définie sur « es-es » (es-es), le client Teams prend les chaînes « fr » et ne les remplace par aucun des fichiers de langue.</span><span class="sxs-lookup"><span data-stu-id="78e62-147">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="78e62-148">Par conséquent, il est vivement recommandé de fournir des traductions linguistiques de niveau supérieur uniquement dans votre manifeste ('en' au lieu de « en-us » ) et de fournir uniquement des substitutions au niveau de la région pour les chaînes qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="78e62-148">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="78e62-149">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="78e62-149">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="78e62-150">Exemple de fichier .json de localisation</span><span class="sxs-lookup"><span data-stu-id="78e62-150">Example localization .json file</span></span>

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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="78e62-151">Gestion des envois de texte localisées de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="78e62-151">Handling localized text submissions from your users</span></span>

<span data-ttu-id="78e62-152">Si vous fournissez des versions localisées de votre application, il est très probable que vos utilisateurs répondent avec la même langue.</span><span class="sxs-lookup"><span data-stu-id="78e62-152">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="78e62-153">Teams ne traduit pas les soumissions de l'utilisateur dans la langue par défaut, votre application devra donc gérer cela.</span><span class="sxs-lookup"><span data-stu-id="78e62-153">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="78e62-154">Par exemple, si vous fournissez une valeur localisée, les réponses à votre bot seront le texte localisée de la commande, et non `commandList` la langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="78e62-154">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="78e62-155">Votre application devra répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="78e62-155">Your app will need to respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="78e62-156">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="78e62-156">Code sample</span></span>

| <span data-ttu-id="78e62-157">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="78e62-157">Sample name</span></span> | <span data-ttu-id="78e62-158">Description</span><span class="sxs-lookup"><span data-stu-id="78e62-158">Description</span></span> | <span data-ttu-id="78e62-159">.NET</span><span class="sxs-lookup"><span data-stu-id="78e62-159">.NET</span></span> |
|-------------|-------------|------|
| <span data-ttu-id="78e62-160">Localisation d'application</span><span class="sxs-lookup"><span data-stu-id="78e62-160">App Localization</span></span> | <span data-ttu-id="78e62-161">Microsoft Teams'application à l'aide du bot et de l'onglet.</span><span class="sxs-lookup"><span data-stu-id="78e62-161">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="78e62-162">View</span><span class="sxs-lookup"><span data-stu-id="78e62-162">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |


