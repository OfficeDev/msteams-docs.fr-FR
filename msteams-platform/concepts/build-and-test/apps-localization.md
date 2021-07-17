---
title: Localiser votre application
description: Décrit les considérations à prendre en compte pour la Microsoft Teams application.
ms.topic: conceptual
localization_priority: Normal
keywords: teams publient la langue de localisation d’AppSource de publication office dans le Store
ms.date: 05/15/2018
ms.openlocfilehash: 5410d6f829c3fec9b5d631452e459bd276df472e
ms.sourcegitcommit: c145d52b2d4daa7655e6c3ddfa739fa1beeb8d6a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/16/2021
ms.locfileid: "53455212"
---
# <a name="localize-your-app"></a><span data-ttu-id="8aa96-104">Localiser votre application</span><span class="sxs-lookup"><span data-stu-id="8aa96-104">Localize your app</span></span>

<span data-ttu-id="8aa96-105">Vous devez prendre en compte les facteurs suivants pour trouver votre application Microsoft Teams suivante :</span><span class="sxs-lookup"><span data-stu-id="8aa96-105">You must consider the following factors to localize your Microsoft Teams app:</span></span>

1. <span data-ttu-id="8aa96-106">[Localisez votre liste AppSource.](#localize-your-appsource-listing)</span><span class="sxs-lookup"><span data-stu-id="8aa96-106">[Localize your AppSource listing](#localize-your-appsource-listing).</span></span>
1. <span data-ttu-id="8aa96-107">[Localisez les chaînes dans le manifeste de votre application.](#localize-strings-in-your-app-manifest)</span><span class="sxs-lookup"><span data-stu-id="8aa96-107">[Localize strings in your app manifest](#localize-strings-in-your-app-manifest).</span></span> 
1. <span data-ttu-id="8aa96-108">[Gérer les envois de texte localisées de vos utilisateurs.](#handle-localized-text-submissions-from-your-users)</span><span class="sxs-lookup"><span data-stu-id="8aa96-108">[Handle localized text submissions from your users](#handle-localized-text-submissions-from-your-users).</span></span>

## <a name="localize-your-appsource-listing"></a><span data-ttu-id="8aa96-109">Localisez votre liste AppSource</span><span class="sxs-lookup"><span data-stu-id="8aa96-109">Localize your AppSource listing</span></span>

<span data-ttu-id="8aa96-110">Si vous publiez l’application dans le Store, vous devez savoir que la recherche dans AppSource n’est pas encore prise en charge.</span><span class="sxs-lookup"><span data-stu-id="8aa96-110">If you are publishing the app to the store, you must be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="8aa96-111">Pour prendre en charge les listes localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre liste.</span><span class="sxs-lookup"><span data-stu-id="8aa96-111">To support localized listings in the app store, you can add additional languages to your listing.</span></span> <span data-ttu-id="8aa96-112">Les informations de langue par défaut que vous fournissez dans [l’Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) pour votre liste apparaissent dans la liste du site [web AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource est un endroit pour tous les besoins de votre équipe. regroupez tous les outils, y compris les conversations, les réunions, les appels, les fichiers et les outils, pour permettre un travail d’équipe plus productif.") de votre application.</span><span class="sxs-lookup"><span data-stu-id="8aa96-112">The default language information you provide in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center) for your listing appears in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1 "AppSource is one place for all your team needs. bring everything together including chats, meetings, calls, files, and tools to enable more productive teamwork.") listing for your app.</span></span> <span data-ttu-id="8aa96-113">Actuellement, la langue par défaut est l’anglais.</span><span class="sxs-lookup"><span data-stu-id="8aa96-113">Currently, the default language is English.</span></span>

### <a name="configure-localization"></a><span data-ttu-id="8aa96-114">Configurer la localisation</span><span class="sxs-lookup"><span data-stu-id="8aa96-114">Configure localization</span></span>

<span data-ttu-id="8aa96-115">Pour configurer une langue supplémentaire pour votre application, dans [l’Partner Center,](/office/dev/store/submit-to-appsource-via-partner-center)sélectionnez l’anglais et la langue supplémentaire de l’application.</span><span class="sxs-lookup"><span data-stu-id="8aa96-115">To configure an additional language for your app, in [Partner Center](/office/dev/store/submit-to-appsource-via-partner-center), select both English and the additional language of the app.</span></span> <span data-ttu-id="8aa96-116">Le français est utilisé comme langue supplémentaire dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8aa96-116">French is used as an additional language in the following example:</span></span>

1. <span data-ttu-id="8aa96-117">Ajouter l’anglais</span><span class="sxs-lookup"><span data-stu-id="8aa96-117">Add English language</span></span>
    * <span data-ttu-id="8aa96-118">Entrez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="8aa96-118">Enter the app name.</span></span>
    * <span data-ttu-id="8aa96-119">Entrez une brève description de l’application en anglais.</span><span class="sxs-lookup"><span data-stu-id="8aa96-119">Enter a short description of the app in English.</span></span>
    * <span data-ttu-id="8aa96-120">Entrez la description longue de l’application en anglais.</span><span class="sxs-lookup"><span data-stu-id="8aa96-120">Enter the long description of the app in English.</span></span>
    * <span data-ttu-id="8aa96-121">Dans la description longue, entrez : **Cette application est disponible en français.**</span><span class="sxs-lookup"><span data-stu-id="8aa96-121">In the long description, enter: **This app is available in French**.</span></span>
    * <span data-ttu-id="8aa96-122">Télécharger images de l’interface utilisateur de votre application (en anglais).</span><span class="sxs-lookup"><span data-stu-id="8aa96-122">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="8aa96-123">Ajouter le français</span><span class="sxs-lookup"><span data-stu-id="8aa96-123">Add French language</span></span>
    * <span data-ttu-id="8aa96-124">Entrez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="8aa96-124">Enter the app name.</span></span>
    * <span data-ttu-id="8aa96-125">Entrez une brève description de l’application en français.</span><span class="sxs-lookup"><span data-stu-id="8aa96-125">Enter a short description of the app in French.</span></span>
    * <span data-ttu-id="8aa96-126">Entrez la description longue de l’application en français.</span><span class="sxs-lookup"><span data-stu-id="8aa96-126">Enter the long description of the app in French.</span></span>
    * <span data-ttu-id="8aa96-127">Télécharger images de l’interface utilisateur de votre application (en français).</span><span class="sxs-lookup"><span data-stu-id="8aa96-127">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="8aa96-128">Les images que vous téléchargez avec l’anglais sont utilisées dans AppSource.</span><span class="sxs-lookup"><span data-stu-id="8aa96-128">The images that you upload with the English language are used in AppSource.</span></span>

## <a name="localize-strings-in-your-app-manifest"></a><span data-ttu-id="8aa96-129">Localiser les chaînes dans le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="8aa96-129">Localize strings in your app manifest</span></span>

<span data-ttu-id="8aa96-130">Vous devez utiliser le schéma Microsoft Teams’application et `v1.5` ultérieurement pour le localiser.</span><span class="sxs-lookup"><span data-stu-id="8aa96-130">You must use the Microsoft Teams app schema `v1.5` and later to localize your app.</span></span> <span data-ttu-id="8aa96-131">Pour ce faire, vous pouvez définir l’attribut de votre manifest.jssur le fichier ou une version supérieure et mettre à jour la propriété en `$schema` **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** version `manifestVersion` `$schema` `1.5` (dans ce cas).</span><span class="sxs-lookup"><span data-stu-id="8aa96-131">You can do this by setting the `$schema` attribute in your manifest.json file to **https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json** or higher and updating the `manifestVersion` property to `$schema` version (`1.5` in this case).</span></span> 

<span data-ttu-id="8aa96-132">Vous devez ajouter la `localizationInfo` propriété avec la langue par défaut que votre application prend en charge.</span><span class="sxs-lookup"><span data-stu-id="8aa96-132">You must add the `localizationInfo` property with the default language that your application supports.</span></span> <span data-ttu-id="8aa96-133">La langue par défaut est utilisée comme langue de base finale si les paramètres du client de l’utilisateur ne correspondent à aucune de vos langues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8aa96-133">The default language is used as the final fallback language if the user's client settings do not match with any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="8aa96-134">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="8aa96-134">Example manifest.json change</span></span>

<span data-ttu-id="8aa96-135">L'manifest.jssuivante permet d’ajouter la propriété avec la langue par défaut que votre application prend en charge `localizationInfo` avec `additionalLanguages` :</span><span class="sxs-lookup"><span data-stu-id="8aa96-135">The following manifest.json helps to add the `localizationInfo` property with the default language that your application supports along with `additionalLanguages`:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "localizationInfo": {
        "defaultLanguageTag": "en",
        "additionalLanguages": [
            {
                "languageTag": "es-mx",
                "file": "es-mx.json"
            }
        ]
    }
  ...
}
```

### <a name="example-localization-json-change"></a><span data-ttu-id="8aa96-136">Exemple de modification .json de localisation</span><span class="sxs-lookup"><span data-stu-id="8aa96-136">Example localization .json change</span></span>

<span data-ttu-id="8aa96-137">Voici un exemple de localisation .json :</span><span class="sxs-lookup"><span data-stu-id="8aa96-137">Following is an example for localization .json:</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
  "manifestVersion": "1.5",
  "name.short": "Localización",
  "name.full": "Aplicación de localización",
  ...
}
```


<span data-ttu-id="8aa96-138">Vous pouvez fournir des fichiers .json supplémentaires avec des traductions de toutes les chaînes orientées utilisateur dans votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="8aa96-138">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="8aa96-139">Ces fichiers doivent respecter le schéma [JSON](../../resources/schema/localization-schema.md) du fichier de localisation et ils doivent être ajoutés à la propriété `localizationInfo` de votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="8aa96-139">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the `localizationInfo` property of your manifest.</span></span> <span data-ttu-id="8aa96-140">Chaque fichier est en corrélation avec une balise de langue, que le client Teams utilise pour sélectionner les chaînes appropriées.</span><span class="sxs-lookup"><span data-stu-id="8aa96-140">Each file correlates to a language tag, which the Teams client uses to select the appropriate strings.</span></span> <span data-ttu-id="8aa96-141">La balise de langue prend la forme de, mais vous pouvez omettre la partie pour cibler toutes les régions qui prennent en charge `<language>-<region>` `<region>` la langue souhaitée.</span><span class="sxs-lookup"><span data-stu-id="8aa96-141">The language tag takes the form of `<language>-<region>` but you can omit the `<region>` portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="8aa96-142">Le client Teams applique les chaînes dans l’ordre suivant : chaînes de langue par défaut -> chaînes de langue de l’utilisateur uniquement -> langue de l’utilisateur + chaînes de région de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="8aa96-142">The Teams client applies the strings in the following order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="8aa96-143">Par exemple, vous fournissez une langue par défaut « fr » (français, toutes les régions) et des fichiers linguistiques supplémentaires pour « en » (anglais, toutes les régions) et « en-gb » (anglais, Grande-France), la langue de l’utilisateur est définie sur « en-gb ».</span><span class="sxs-lookup"><span data-stu-id="8aa96-143">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain), the user's language is set to 'en-gb'.</span></span> <span data-ttu-id="8aa96-144">Les modifications suivantes sont apportées en fonction de la sélection de la langue :</span><span class="sxs-lookup"><span data-stu-id="8aa96-144">The following changes take place based on the language selection:</span></span>

1. <span data-ttu-id="8aa96-145">Le Teams client prend les chaînes « fr » et les overwrite avec les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="8aa96-145">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="8aa96-146">Overwrite the 'en' strings with the 'en-gb' strings.</span><span class="sxs-lookup"><span data-stu-id="8aa96-146">Overwrite the 'en' strings with the 'en-gb' strings.</span></span>

<span data-ttu-id="8aa96-147">Si la langue de l’utilisateur est définie sur « en-ca », les modifications suivantes ont lieu en fonction de la sélection de la langue :</span><span class="sxs-lookup"><span data-stu-id="8aa96-147">If the user's language is set to 'en-ca', the following changes take place based on the language selection:</span></span> 

1. <span data-ttu-id="8aa96-148">Le Teams client prend les chaînes « fr » et les overwrite avec les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="8aa96-148">The Teams client takes the 'fr' strings and overwrite them with the 'en' strings.</span></span>
1. <span data-ttu-id="8aa96-149">Étant donné qu’aucune localisation « en-ca » n’est fournie, les localisations « en » sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="8aa96-149">Since no 'en-ca' localization is supplied, the 'en\` localizations are used.</span></span>

<span data-ttu-id="8aa96-150">Si la langue de l’utilisateur est définie sur es-es, le client Teams prend les chaînes « fr ».</span><span class="sxs-lookup"><span data-stu-id="8aa96-150">If the user's language is set to 'es-es', the Teams client takes the 'fr' strings.</span></span> <span data-ttu-id="8aa96-151">Le client Teams ne remplace pas les chaînes par les fichiers de langue car aucune traduction « es » ou « es-es » n’est fournie.</span><span class="sxs-lookup"><span data-stu-id="8aa96-151">The Teams client does not override the strings with any of the language files as no 'es' or 'es-es' translation is provided.</span></span>

<span data-ttu-id="8aa96-152">Par conséquent, vous devez fournir des traductions linguistiques de niveau supérieur uniquement dans votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="8aa96-152">Therefore, you must provide top level, language only translations in your manifest.</span></span> <span data-ttu-id="8aa96-153">Par exemple, « en » au lieu de « en-us ».</span><span class="sxs-lookup"><span data-stu-id="8aa96-153">For example, 'en' instead of 'en-us'.</span></span> <span data-ttu-id="8aa96-154">Vous devez fournir des substitutions au niveau de la région uniquement pour les chaînes qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="8aa96-154">You must provide region level overrides only for the few strings that need them.</span></span> 

### <a name="example-manifestjson-change"></a><span data-ttu-id="8aa96-155">Exemple manifest.jsmodification</span><span class="sxs-lookup"><span data-stu-id="8aa96-155">Example manifest.json change</span></span>

<span data-ttu-id="8aa96-156">Le manifest.jssur la modification est illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8aa96-156">The manifest.json change is shown in the following example:</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="8aa96-157">Exemple de fichier .json de localisation</span><span class="sxs-lookup"><span data-stu-id="8aa96-157">Example localization .json file</span></span>

 <span data-ttu-id="8aa96-158">Le localization.jssur la modification est illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="8aa96-158">The localization.json change is shown in the following example:</span></span>

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

## <a name="handle-localized-text-submissions-from-your-users"></a><span data-ttu-id="8aa96-159">Gérer les envois de texte localisées de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="8aa96-159">Handle localized text submissions from your users</span></span>

<span data-ttu-id="8aa96-160">Si vous fournissez des versions localisées de votre application, les utilisateurs répondent avec la même langue.</span><span class="sxs-lookup"><span data-stu-id="8aa96-160">If your provide localized versions of your application, the users respond with the same language.</span></span> <span data-ttu-id="8aa96-161">Comme Teams ne traduit pas les envois de l’utilisateur dans la langue par défaut, votre application doit gérer les réponses linguistiques localisées.</span><span class="sxs-lookup"><span data-stu-id="8aa96-161">As Teams does not translate the user submissions back to the default language, your app must handle the localized language responses.</span></span> <span data-ttu-id="8aa96-162">Par exemple, si vous fournissez une langue localisée, les réponses à votre bot sont le texte localisée de la commande, et non `commandList` la langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="8aa96-162">For example, if you provide a localized `commandList`, the responses to your bot are the localized text of the command, not the default language.</span></span> <span data-ttu-id="8aa96-163">Votre application doit répondre correctement.</span><span class="sxs-lookup"><span data-stu-id="8aa96-163">Your app must respond appropriately.</span></span>

## <a name="code-sample"></a><span data-ttu-id="8aa96-164">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="8aa96-164">Code sample</span></span>

| <span data-ttu-id="8aa96-165">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="8aa96-165">Sample name</span></span> | <span data-ttu-id="8aa96-166">Description</span><span class="sxs-lookup"><span data-stu-id="8aa96-166">Description</span></span> | <span data-ttu-id="8aa96-167">.NET</span><span class="sxs-lookup"><span data-stu-id="8aa96-167">.NET</span></span> | <span data-ttu-id="8aa96-168">Node.js</span><span class="sxs-lookup"><span data-stu-id="8aa96-168">Node.js</span></span> |
|-------------|-------------|------|------|
| <span data-ttu-id="8aa96-169">Localisation d’application</span><span class="sxs-lookup"><span data-stu-id="8aa96-169">App Localization</span></span> | <span data-ttu-id="8aa96-170">Microsoft Teams’application à l’aide du bot et de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="8aa96-170">Microsoft Teams app localization using bot and tab.</span></span> | [<span data-ttu-id="8aa96-171">View</span><span class="sxs-lookup"><span data-stu-id="8aa96-171">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |[<span data-ttu-id="8aa96-172">View</span><span class="sxs-lookup"><span data-stu-id="8aa96-172">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) |

