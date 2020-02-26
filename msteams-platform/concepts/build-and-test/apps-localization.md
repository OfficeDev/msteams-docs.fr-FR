---
title: Localisation des applications d’équipe
description: Décrit les problèmes liés à la localisation de votre application
keywords: teams publier le magasin Office publication AppSource langue de localisation
ms.date: 05/15/2018
ms.openlocfilehash: 0affa61ee1967a0e1bc19e423f05049bad750ce7
ms.sourcegitcommit: 67c021fa20eb5ea70c059fcc35be1c19c6c97c95
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/26/2020
ms.locfileid: "42279760"
---
# <a name="localization-for-microsoft-teams-apps"></a><span data-ttu-id="9b0b3-104">Localisation pour les applications Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="9b0b3-104">Localization for Microsoft Teams apps</span></span>

<span data-ttu-id="9b0b3-105">Lors de la localisation de votre application Microsoft Teams, vous devez prendre en compte trois éléments principaux.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-105">When localizing your Microsoft Teams app there are three major areas you need to consider.</span></span>

1. <span data-ttu-id="9b0b3-106">Votre AppSource Listing (si vous effectuez une publication sur le magasin d’applications).</span><span class="sxs-lookup"><span data-stu-id="9b0b3-106">Your AppSource listing (if you're publishing to the app store).</span></span>
1. <span data-ttu-id="9b0b3-107">L’utilisateur final a accès à des chaînes dans votre manifeste de l’application (par exemple, commandes de bot).</span><span class="sxs-lookup"><span data-stu-id="9b0b3-107">The end-user facing strings in your app manifest (for example bot commands).</span></span>
1. <span data-ttu-id="9b0b3-108">Réponse au texte localisé envoyé par vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-108">Responding to localized text submitted from your users.</span></span>

## <a name="localizing-your-appsource-listing"></a><span data-ttu-id="9b0b3-109">Localisation de votre liste AppSource</span><span class="sxs-lookup"><span data-stu-id="9b0b3-109">Localizing your AppSource listing</span></span>

<span data-ttu-id="9b0b3-110">Si vous effectuez une publication sur App Store, vous devez savoir que la localisation de votre liste AppSource n’est pas encore prise en charge.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-110">If you're publishing to the app store, you need to be aware that localizing your AppSource listing is not yet supported.</span></span> <span data-ttu-id="9b0b3-111">Toutefois, en vue de la prise en charge des listes localisées dans l’App Store, vous pouvez ajouter des langues supplémentaires à votre annonce.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-111">However, in preparation for support for localized listings in the app store you can add additional languages to your listing.</span></span> <span data-ttu-id="9b0b3-112">Actuellement, seules les informations de langue par défaut (anglais) que vous fournissez dans le [Centre des partenaires](/dev/store/use-partner-center-to-submit-to-appsource) pour votre liste apparaîtront dans la liste de [sites Web AppSource](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) de votre application.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-112">Currently only the default (English) language information you provide in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource) for your listing will appear in the [AppSource website](https://appsource.microsoft.com/marketplace/apps?product=office%3Bteams&page=1) listing for your app.</span></span>

<span data-ttu-id="9b0b3-113">Pour configurer une langue supplémentaire pour votre application, dans le [Centre de partenaires](/dev/store/use-partner-center-to-submit-to-appsource), sélectionnez anglais et la langue supplémentaire de l’application.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-113">To configure an additional language for your app, in [Partner Center](/dev/store/use-partner-center-to-submit-to-appsource), select both English and the additional language of the app.</span></span> <span data-ttu-id="9b0b3-114">Le français est utilisé dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-114">French is used in this example.</span></span>

1. <span data-ttu-id="9b0b3-115">Ajouter une langue anglaise</span><span class="sxs-lookup"><span data-stu-id="9b0b3-115">Add English language</span></span>
    * <span data-ttu-id="9b0b3-116">Renseignez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-116">Fill in the app name.</span></span>
    * <span data-ttu-id="9b0b3-117">Entrez une brève description de l’application en anglais.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-117">Fill in a short description of the app in English.</span></span>
    * <span data-ttu-id="9b0b3-118">Renseignez la description longue de l’application en anglais.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-118">Fill in the long description of the app in English.</span></span>
    * <span data-ttu-id="9b0b3-119">Dans la description longue, ajoutez également la ligne « cette application est disponible en français ».</span><span class="sxs-lookup"><span data-stu-id="9b0b3-119">In the long description, please also add the line “This app is available in “French”.</span></span>
    * <span data-ttu-id="9b0b3-120">Téléchargez les images de l’interface utilisateur de votre application (en anglais).</span><span class="sxs-lookup"><span data-stu-id="9b0b3-120">Upload the images of your app UI (in English).</span></span>
2. <span data-ttu-id="9b0b3-121">Ajouter la langue française</span><span class="sxs-lookup"><span data-stu-id="9b0b3-121">Add French language</span></span>
    * <span data-ttu-id="9b0b3-122">Renseignez le nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-122">Fill in the app name.</span></span>
    * <span data-ttu-id="9b0b3-123">Entrez une brève description de l’application en français.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-123">Fill in a short description of the app in French.</span></span>
    * <span data-ttu-id="9b0b3-124">Renseignez la description longue de l’application en français.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-124">Fill in the long description of the app in French.</span></span>
    * <span data-ttu-id="9b0b3-125">Téléchargez les images de l’interface utilisateur de votre application (en français).</span><span class="sxs-lookup"><span data-stu-id="9b0b3-125">Upload the images of your app UI (in French).</span></span>

<span data-ttu-id="9b0b3-126">Les images que vous chargez avec la langue anglaise seront celles utilisées dans AppSource.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-126">The images you upload with the English language will be the ones used in AppSource.</span></span>

## <a name="localizing-the-strings-in-your-app-manifest"></a><span data-ttu-id="9b0b3-127">Localisation des chaînes dans le manifeste de votre application</span><span class="sxs-lookup"><span data-stu-id="9b0b3-127">Localizing the strings in your app manifest</span></span>

<span data-ttu-id="9b0b3-128">Vous devez utiliser le schéma d’application Microsoft teams v 1.5 + pour localiser correctement votre application.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-128">You must use the Microsoft Teams app schema v1.5+ to properly localize your app.</span></span> <span data-ttu-id="9b0b3-129">Vous pouvez effectuer cette opération en définissant l' `$schema` attribut dans votre fichier manifest. JSONhttps://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.jsonsur' 'et en mettant à jour la propriété’manifestVersion’en' 1,5 '.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-129">You can do this by setting the `$schema` attribute in your manifest.json file to 'https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json' and updating the 'manifestVersion' property to '1.5'.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="9b0b3-130">Exemple de modification de manifest. JSON</span><span class="sxs-lookup"><span data-stu-id="9b0b3-130">Example manifest.json change</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  ...
}
```

<span data-ttu-id="9b0b3-131">Vous pouvez ensuite ajouter la propriété « localizationInfo » avec la langue par défaut prise en charge par votre application.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-131">You will then want to add the 'localizationInfo' property with the default language that your application supports.</span></span> <span data-ttu-id="9b0b3-132">La langue par défaut est utilisée comme langue de secours finale si les paramètres du client de l’utilisateur ne correspondent à aucune de vos langues supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-132">The default language is used as the final fallback language if the user's client settings do not match any of your additional languages.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="9b0b3-133">Exemple de modification de manifest. JSON</span><span class="sxs-lookup"><span data-stu-id="9b0b3-133">Example manifest.json change</span></span>

```json
{
  ...
  "localizationInfo": {
    "defaultLanguageTag": "en"
  }
  ...
}
```

<span data-ttu-id="9b0b3-134">Vous pouvez fournir des fichiers. JSON supplémentaires avec des traductions de toutes les chaînes accessibles par l’utilisateur dans votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-134">You can provide additional .json files with translations of all the user facing strings in your manifest.</span></span> <span data-ttu-id="9b0b3-135">Ces fichiers doivent adhérer au [schéma JSON fichier de localisation](../../resources/schema/localization-schema.md) et ils doivent être ajoutés à la propriété « localizationInfo » de votre manifeste.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-135">These files must adhere to the [Localization file JSON schema](../../resources/schema/localization-schema.md) and they must be added to the 'localizationInfo' property of your manifest.</span></span> <span data-ttu-id="9b0b3-136">Chaque fichier correspond à une balise de langue que le client teams utilise pour choisir les chaînes appropriées.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-136">Each file correlates to a language tag which the Teams client uses to choose the appropriate strings.</span></span> <span data-ttu-id="9b0b3-137">La balise de <language> - <region> langue prend la forme, mais il est recommandé d' <region> omettre la partie pour cibler toutes les régions qui prennent en charge la langue souhaitée.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-137">The language tag takes the form of <language>-<region> but it is recommended to omit the <region> portion to target all regions that support the desired language.</span></span>

<span data-ttu-id="9b0b3-138">Le client teams applique les chaînes dans l’ordre suivant : chaînes de langue par défaut-> langue de l’utilisateur uniquement chaînes-> langue de l’utilisateur + chaînes de région de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-138">The Teams client will apply the strings in this order: default language strings -> user's language only strings -> user's language + user's region strings.</span></span>

<span data-ttu-id="9b0b3-139">Par exemple, vous fournissez une langue par défaut de « fr » (français, toutes les régions) et des fichiers de langue supplémentaires pour « en » (anglais, toutes les régions) et « en-GB » (anglais, Grande-Bretagne).</span><span class="sxs-lookup"><span data-stu-id="9b0b3-139">For example, you provide a default language of 'fr' (French, all regions), and additional language files for 'en' (English, all regions) and 'en-gb' (English, Great Britain).</span></span> <span data-ttu-id="9b0b3-140">Si la langue de l’utilisateur est définie sur « en-GB » :</span><span class="sxs-lookup"><span data-stu-id="9b0b3-140">If the user's language is set to 'en-gb':</span></span>

1. <span data-ttu-id="9b0b3-141">Le client teams prendra les chaînes « fr » les remplacer par les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="9b0b3-141">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="9b0b3-142">Remplacez ceux-ci par les chaînes « en-GB ».</span><span class="sxs-lookup"><span data-stu-id="9b0b3-142">Overwrite those with the 'en-gb' strings.</span></span>

<span data-ttu-id="9b0b3-143">Si la langue de l’utilisateur est définie sur « en-ca » :</span><span class="sxs-lookup"><span data-stu-id="9b0b3-143">If the user's language is set to 'en-ca':</span></span> 

1. <span data-ttu-id="9b0b3-144">Le client teams prendra les chaînes « fr » les remplacer par les chaînes « en ».</span><span class="sxs-lookup"><span data-stu-id="9b0b3-144">The Teams client will take the 'fr' strings overwrite them with the 'en' strings.</span></span>
2. <span data-ttu-id="9b0b3-145">Étant donné qu’aucune localazation « en-ca » n’est fournie, les localisations « en » seront utilisées.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-145">Since no 'en-ca' localazation is supplied, the 'en' localizations will be used.</span></span>

<span data-ttu-id="9b0b3-146">Si la langue de l’utilisateur est définie sur « es-es », le client teams prend les chaînes « fr » et ne les remplace pas par l’un des fichiers de langue.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-146">If the user's language is set to 'es-es', the Teams client will take the 'fr' strings and will not override them with any of the language files.</span></span>

<span data-ttu-id="9b0b3-147">Par conséquent, il est vivement recommandé de fournir des traductions de niveau supérieur, de langue uniquement dans votre manifeste (« en » au lieu de « en-US ») et de fournir uniquement des substitutions au niveau de la région pour les quelques chaînes qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-147">Therefore, it is strongly recommended to provide top-level, language-only translations in your manifest ('en' instead of 'en-us') and only provide region-level overrides for the few strings that need them.</span></span>

### <a name="example-manifestjson-change"></a><span data-ttu-id="9b0b3-148">Exemple de modification de manifest. JSON</span><span class="sxs-lookup"><span data-stu-id="9b0b3-148">Example manifest.json change</span></span>

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

### <a name="example-localization-json-file"></a><span data-ttu-id="9b0b3-149">Exemple de fichier Localization. JSON</span><span class="sxs-lookup"><span data-stu-id="9b0b3-149">Example localization .json file</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.Localization.schema.json",
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

## <a name="handling-localized-text-submissions-from-your-users"></a><span data-ttu-id="9b0b3-150">Gestion des envois de texte localisés provenant de vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="9b0b3-150">Handling localized text submissions from your users</span></span>

<span data-ttu-id="9b0b3-151">Si vous fournissez des versions localisées de votre application, il est fort probable que vos utilisateurs y répondront dans la même langue.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-151">If your provide localized versions of your application it is very likely that your users will respond with the same language.</span></span> <span data-ttu-id="9b0b3-152">Teams ne reconvertit pas les soumissions de l’utilisateur vers la langue par défaut, de sorte que votre application doit gérer cela.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-152">Teams does not translate the user submissions back to the default language, so your app will need to handle that.</span></span> <span data-ttu-id="9b0b3-153">Par exemple, si vous fournissez une localisation `commandList`, les réponses à votre bot seront le texte localisé de la commande, pas la langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-153">For example, if you provide a localized `commandList`, the responses to your bot will be the localized text of the command, not the default language.</span></span> <span data-ttu-id="9b0b3-154">Votre application doit répondre de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="9b0b3-154">Your app will need to respond appropriately.</span></span>
