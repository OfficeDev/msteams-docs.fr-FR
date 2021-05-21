---
title: Référence du schéma de manifeste d’aperçu du développeur
description: Décrit le schéma pris en charge par le manifeste pour Microsoft Teams
ms.topic: reference
keywords: Aperçu du schéma de manifeste teams pour les développeurs
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: b52d52f96312dc2978844b07a0f7ebb1d817166d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566704"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="db5cb-104">Schéma de manifeste de prévisualisation pour les développeurs Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="db5cb-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="db5cb-105">Pour plus [d’informations](~/resources/dev-preview/developer-preview-intro.md) sur le programme et la façon dont vous pouvez participer, voir Aperçu du développeur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="db5cb-106">Si vous n’utilisez pas la prévisualisation du développeur, vous ne devez pas utiliser cette version du manifeste.</span><span class="sxs-lookup"><span data-stu-id="db5cb-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="db5cb-107">Voir [la référence : schéma de manifeste Microsoft Teams](~/resources/schema/manifest-schema.md) pour la version publique du manifeste.</span><span class="sxs-lookup"><span data-stu-id="db5cb-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="db5cb-108">Le Microsoft Teams de l’application décrit comment l’application s’intègre au Microsoft Teams produit.</span><span class="sxs-lookup"><span data-stu-id="db5cb-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="db5cb-109">Votre manifeste doit être conforme au schéma hébergé sur [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="db5cb-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="db5cb-110">Pour plus d’informations sur les fonctionnalités disponibles, voir : [Fonctionnalités de](~/resources/dev-preview/developer-preview-features.md)la prévisualisation pour les développeurs publics Microsoft Teams .</span><span class="sxs-lookup"><span data-stu-id="db5cb-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="db5cb-111">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="db5cb-111">Sample full manifest</span></span>

```json
{
  "$schema": "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
  "manifestVersion": "devPreview",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "devicePermissions" : [ "geolocation", "media" ],
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "localizationInfo": {
    "defaultLanguageTag": "es-es",
    "additionalLanguages": [
      {
        "languageTag": "en-us",
        "file": "en-us.json"
      }
    ]
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters"
  },
  "description": {
    "short": "Short description of your app",
    "full": "Full description of your app"
  },
  "icons": {
    "outline": "%FILENAME-32x32px%",
    "color": "%FILENAME-192x192px"
  },
  "accentColor": "%HEX-COLOR%",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [ "team", "groupchat" ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "idForPage",
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content?host=msteams",
      "websiteUrl": "https://contoso.com/content",
      "scopes": [ "personal" ]
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "scopes": [ "team", "personal", "groupchat" ],
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [ "team", "groupchat" ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command N",
              "description": "Description of Command N"
            }
          ]
        },
        {
          "scopes": [ "personal", "groupchat" ],
          "commands": [
            {
              "title": "Personal command 1",
              "description": "Description of Personal command 1"
            },
            {
              "title": "Personal command N",
              "description": "Description of Personal command N"
            }
          ]
        }
      ]
    }
  ],
  "connectors": [
    {
      "connectorId": "GUID-FROM-CONNECTOR-DEV-PORTAL%",
      "configurationUrl": "https://contoso.com/teamsconnector/configure",
      "scopes": [ "team"]
    }
  ],
  "composeExtensions": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "type" : "search",
          "context" : ["compose", "commandBox"],
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "description": "Enter the keywords to search for"
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "type" : "action",
          "fetchTask" : true,
          "context" : ["message"],
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType" : "text"
            }
          ]
        },
        {
          "id": "exampleMessageHandler",
          "title": "Message Handler",
          "description": "Domains that will create a preview when pasted into the compose box",
          "messageHandlers": [
            {
              "type" : "link",
              "value" : {
                "domains" : [
                  "mysite.someplace.com",
                  "othersite.someplace.com"
                ]
              }
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers",
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ],
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "websiteUrl",
     "privacyUrl",
     "termsOfUseUrl"        
  ],
  "defaultInstallScope": "meetings",
  "defaultGroupCapability": {
    "meetings": "tab", 
    "team": "bot", 
    "groupchat": "bot"
  }
}
```

<span data-ttu-id="db5cb-112">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="db5cb-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="db5cb-113">$schema</span><span class="sxs-lookup"><span data-stu-id="db5cb-113">$schema</span></span>

<span data-ttu-id="db5cb-114">*Facultatif, mais recommandé* &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="db5cb-115">L https:// URL référente au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="db5cb-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="db5cb-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="db5cb-116">manifestVersion</span></span>

<span data-ttu-id="db5cb-117">**Obligatoire** &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-117">**Required** &ndash; String</span></span>

<span data-ttu-id="db5cb-118">Version du schéma de manifeste utilisé par ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="db5cb-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="db5cb-119">Il doit s’qu’il s’appelle « devPreview ».</span><span class="sxs-lookup"><span data-stu-id="db5cb-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="db5cb-120">version</span><span class="sxs-lookup"><span data-stu-id="db5cb-120">version</span></span>

<span data-ttu-id="db5cb-121">**Obligatoire** &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-121">**Required** &ndash; String</span></span>

<span data-ttu-id="db5cb-122">Version de l’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="db5cb-122">The version of the specific app.</span></span> <span data-ttu-id="db5cb-123">Si vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="db5cb-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="db5cb-124">Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="db5cb-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="db5cb-125">Si cette application a été soumise au Store, le nouveau manifeste devra être soumis à nouveau et validé à nouveau.</span><span class="sxs-lookup"><span data-stu-id="db5cb-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="db5cb-126">Ensuite, les utilisateurs de cette application obtiennent automatiquement le nouveau manifeste mis à jour dans quelques heures, une fois qu’il est approuvé.</span><span class="sxs-lookup"><span data-stu-id="db5cb-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="db5cb-127">Si l’application demande des autorisations, les utilisateurs sont invités à mettre à niveau et à consentir à l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="db5cb-128">Cette chaîne de version doit suivre la [norme de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="db5cb-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="db5cb-129">id</span><span class="sxs-lookup"><span data-stu-id="db5cb-129">id</span></span>

<span data-ttu-id="db5cb-130">**Obligatoire** &ndash; ID d’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="db5cb-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="db5cb-131">Identificateur unique généré par Microsoft pour cette application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="db5cb-132">Si vous avez inscrit un bot via le Microsoft Bot Framework ou si l’application web de votre onglet se signe déjà avec Microsoft, vous devez déjà avoir un ID et l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="db5cb-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="db5cb-133">Sinon, vous devez générer un nouvel ID sur le portail d’inscription des applications Microsoft[(Mes applications),](https://apps.dev.microsoft.com)entrez-le ici, puis réutilisez-le lorsque vous [ajoutez un bot.](~/bots/how-to/create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="db5cb-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="db5cb-134">packageName</span><span class="sxs-lookup"><span data-stu-id="db5cb-134">packageName</span></span>

<span data-ttu-id="db5cb-135">**Obligatoire** &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-135">**Required** &ndash; String</span></span>

<span data-ttu-id="db5cb-136">Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="db5cb-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="db5cb-137">developer</span><span class="sxs-lookup"><span data-stu-id="db5cb-137">developer</span></span>

<span data-ttu-id="db5cb-138">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="db5cb-138">**Required**</span></span>

<span data-ttu-id="db5cb-139">Spécifie des informations sur votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="db5cb-139">Specifies information about your company.</span></span> <span data-ttu-id="db5cb-140">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="db5cb-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="db5cb-141">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-141">Name</span></span>| <span data-ttu-id="db5cb-142">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-142">Maximum size</span></span> | <span data-ttu-id="db5cb-143">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-143">Required</span></span> | <span data-ttu-id="db5cb-144">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="db5cb-145">32 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-145">32 characters</span></span>|<span data-ttu-id="db5cb-146">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-146">✔</span></span>|<span data-ttu-id="db5cb-147">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="db5cb-148">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-148">2048 characters</span></span>|<span data-ttu-id="db5cb-149">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-149">✔</span></span>|<span data-ttu-id="db5cb-150">L https:// URL du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="db5cb-151">Ce lien doit permettre aux utilisateurs d’accès à votre entreprise ou à votre page d’accueil spécifique au produit.</span><span class="sxs-lookup"><span data-stu-id="db5cb-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="db5cb-152">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-152">2048 characters</span></span>|<span data-ttu-id="db5cb-153">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-153">✔</span></span>|<span data-ttu-id="db5cb-154">L https:// URL vers la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="db5cb-155">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-155">2048 characters</span></span>|<span data-ttu-id="db5cb-156">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-156">✔</span></span>|<span data-ttu-id="db5cb-157">L https:// URL vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="db5cb-158">10 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-158">10 characters</span></span>|<span data-ttu-id="db5cb-159">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-159">✔</span></span>|<span data-ttu-id="db5cb-160">**Facultatif** ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="db5cb-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="db5cb-161">localizationInfo</span></span>

<span data-ttu-id="db5cb-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="db5cb-162">**Optional**</span></span>

<span data-ttu-id="db5cb-163">Permet la spécification d’une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="db5cb-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="db5cb-164">Voir [localisation.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="db5cb-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="db5cb-165">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-165">Name</span></span>| <span data-ttu-id="db5cb-166">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-166">Maximum size</span></span> | <span data-ttu-id="db5cb-167">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-167">Required</span></span> | <span data-ttu-id="db5cb-168">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="db5cb-169">4 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-169">4 characters</span></span>|<span data-ttu-id="db5cb-170">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-170">✔</span></span>|<span data-ttu-id="db5cb-171">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="db5cb-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="db5cb-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="db5cb-173">Tableau d’objets spécifiant des traductions linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="db5cb-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="db5cb-174">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-174">Name</span></span>| <span data-ttu-id="db5cb-175">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-175">Maximum size</span></span> | <span data-ttu-id="db5cb-176">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-176">Required</span></span> | <span data-ttu-id="db5cb-177">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="db5cb-178">4 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-178">4 characters</span></span>|<span data-ttu-id="db5cb-179">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-179">✔</span></span>|<span data-ttu-id="db5cb-180">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="db5cb-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="db5cb-181">4 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-181">4 characters</span></span>|<span data-ttu-id="db5cb-182">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-182">✔</span></span>|<span data-ttu-id="db5cb-183">Chemin d’accès relatif au fichier .json contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="db5cb-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="db5cb-184">name</span><span class="sxs-lookup"><span data-stu-id="db5cb-184">name</span></span>

<span data-ttu-id="db5cb-185">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="db5cb-185">**Required**</span></span>

<span data-ttu-id="db5cb-186">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’Teams expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="db5cb-187">Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="db5cb-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="db5cb-188">Les valeurs `short` de et ne doivent pas être `full` identiques.</span><span class="sxs-lookup"><span data-stu-id="db5cb-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="db5cb-189">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-189">Name</span></span>| <span data-ttu-id="db5cb-190">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-190">Maximum size</span></span> | <span data-ttu-id="db5cb-191">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-191">Required</span></span> | <span data-ttu-id="db5cb-192">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="db5cb-193">30 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-193">30 characters</span></span>|<span data-ttu-id="db5cb-194">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-194">✔</span></span>|<span data-ttu-id="db5cb-195">Nom d’affichage court de l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="db5cb-196">100 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-196">100 characters</span></span>||<span data-ttu-id="db5cb-197">Nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="db5cb-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="db5cb-198">description</span><span class="sxs-lookup"><span data-stu-id="db5cb-198">description</span></span>

<span data-ttu-id="db5cb-199">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="db5cb-199">**Required**</span></span>

<span data-ttu-id="db5cb-200">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="db5cb-200">Describes your app to users.</span></span> <span data-ttu-id="db5cb-201">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="db5cb-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="db5cb-202">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="db5cb-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="db5cb-203">Notez également, dans la description complète, si un compte externe est requis pour être utilisé.</span><span class="sxs-lookup"><span data-stu-id="db5cb-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="db5cb-204">Les valeurs `short` de et ne doivent pas être `full` identiques.</span><span class="sxs-lookup"><span data-stu-id="db5cb-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="db5cb-205">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="db5cb-206">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-206">Name</span></span>| <span data-ttu-id="db5cb-207">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-207">Maximum size</span></span> | <span data-ttu-id="db5cb-208">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-208">Required</span></span> | <span data-ttu-id="db5cb-209">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="db5cb-210">80 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-210">80 characters</span></span>|<span data-ttu-id="db5cb-211">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-211">✔</span></span>|<span data-ttu-id="db5cb-212">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="db5cb-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="db5cb-213">4 000 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-213">4000 characters</span></span>|<span data-ttu-id="db5cb-214">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-214">✔</span></span>|<span data-ttu-id="db5cb-215">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="db5cb-216">icons</span><span class="sxs-lookup"><span data-stu-id="db5cb-216">icons</span></span>

<span data-ttu-id="db5cb-217">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="db5cb-217">**Required**</span></span>

<span data-ttu-id="db5cb-218">Icônes utilisées dans l’Teams app.</span><span class="sxs-lookup"><span data-stu-id="db5cb-218">Icons used within the Teams app.</span></span> <span data-ttu-id="db5cb-219">Les fichiers d’icône doivent être inclus dans le package de chargement.</span><span class="sxs-lookup"><span data-stu-id="db5cb-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="db5cb-220">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-220">Name</span></span>| <span data-ttu-id="db5cb-221">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-221">Maximum size</span></span> | <span data-ttu-id="db5cb-222">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-222">Required</span></span> | <span data-ttu-id="db5cb-223">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="db5cb-224">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-224">2048 characters</span></span>|<span data-ttu-id="db5cb-225">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-225">✔</span></span>|<span data-ttu-id="db5cb-226">Chemin d’accès relatif à un plan PNG transparent 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="db5cb-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="db5cb-227">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-227">2048 characters</span></span>|<span data-ttu-id="db5cb-228">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-228">✔</span></span>|<span data-ttu-id="db5cb-229">Chemin d’accès relatif à une icône PNG couleur 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="db5cb-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="db5cb-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="db5cb-230">accentColor</span></span>

<span data-ttu-id="db5cb-231">**Obligatoire** &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-231">**Required** &ndash; String</span></span>

<span data-ttu-id="db5cb-232">Couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="db5cb-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="db5cb-233">La valeur doit être un code de couleur HTML valide commençant par « # » par `#4464ee` exemple.</span><span class="sxs-lookup"><span data-stu-id="db5cb-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="db5cb-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="db5cb-234">configurableTabs</span></span>

<span data-ttu-id="db5cb-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="db5cb-235">**Optional**</span></span>

<span data-ttu-id="db5cb-236">Utilisé lorsque l’expérience de votre application possède une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="db5cb-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="db5cb-237">Les onglets configurables sont pris en charge uniquement dans l’étendue Teams, et actuellement, un seul onglet par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="db5cb-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="db5cb-238">L’objet est un tableau avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="db5cb-239">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet de canal configurable.</span><span class="sxs-lookup"><span data-stu-id="db5cb-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="db5cb-240">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-240">Name</span></span>| <span data-ttu-id="db5cb-241">Type</span><span class="sxs-lookup"><span data-stu-id="db5cb-241">Type</span></span>| <span data-ttu-id="db5cb-242">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-242">Maximum size</span></span> | <span data-ttu-id="db5cb-243">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-243">Required</span></span> | <span data-ttu-id="db5cb-244">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="db5cb-245">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-245">String</span></span>|<span data-ttu-id="db5cb-246">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-246">2048 characters</span></span>|<span data-ttu-id="db5cb-247">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-247">✔</span></span>|<span data-ttu-id="db5cb-248">Url https:// à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="db5cb-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="db5cb-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="db5cb-249">Boolean</span></span>|||<span data-ttu-id="db5cb-250">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="db5cb-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="db5cb-251">Valeur par défaut : `true`</span><span class="sxs-lookup"><span data-stu-id="db5cb-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="db5cb-252">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="db5cb-252">Array of enum</span></span>|<span data-ttu-id="db5cb-253">1</span><span class="sxs-lookup"><span data-stu-id="db5cb-253">1</span></span>|<span data-ttu-id="db5cb-254">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-254">✔</span></span>|<span data-ttu-id="db5cb-255">Actuellement, les onglets configurables ne peuvent que les `team` étendues et les `groupchat` étendues.</span><span class="sxs-lookup"><span data-stu-id="db5cb-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="db5cb-256">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-256">String</span></span>|<span data-ttu-id="db5cb-257">2048</span><span class="sxs-lookup"><span data-stu-id="db5cb-257">2048</span></span>||<span data-ttu-id="db5cb-258">Chemin d’accès relatif à une image d’aperçu d’onglet à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="db5cb-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="db5cb-259">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="db5cb-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="db5cb-260">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="db5cb-260">Array of enum</span></span>|<span data-ttu-id="db5cb-261">1</span><span class="sxs-lookup"><span data-stu-id="db5cb-261">1</span></span>||<span data-ttu-id="db5cb-262">Définit la façon dont votre onglet sera disponible dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="db5cb-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="db5cb-263">Les options sont `sharePointFullPage` et `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="db5cb-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="db5cb-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="db5cb-264">staticTabs</span></span>

<span data-ttu-id="db5cb-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="db5cb-265">**Optional**</span></span>

<span data-ttu-id="db5cb-266">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="db5cb-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="db5cb-267">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="db5cb-268">Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="db5cb-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="db5cb-269">L’objet est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="db5cb-270">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="db5cb-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="db5cb-271">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-271">Name</span></span>| <span data-ttu-id="db5cb-272">Type</span><span class="sxs-lookup"><span data-stu-id="db5cb-272">Type</span></span>| <span data-ttu-id="db5cb-273">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-273">Maximum size</span></span> | <span data-ttu-id="db5cb-274">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-274">Required</span></span> | <span data-ttu-id="db5cb-275">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="db5cb-276">String</span><span class="sxs-lookup"><span data-stu-id="db5cb-276">String</span></span>|<span data-ttu-id="db5cb-277">64 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-277">64 characters</span></span>|<span data-ttu-id="db5cb-278">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-278">✔</span></span>|<span data-ttu-id="db5cb-279">Identificateur unique de l’entité affichée par l’onglet.</span><span class="sxs-lookup"><span data-stu-id="db5cb-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="db5cb-280">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-280">String</span></span>|<span data-ttu-id="db5cb-281">128 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-281">128 characters</span></span>|<span data-ttu-id="db5cb-282">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-282">✔</span></span>|<span data-ttu-id="db5cb-283">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="db5cb-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="db5cb-284">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-284">String</span></span>|<span data-ttu-id="db5cb-285">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-285">2048 characters</span></span>|<span data-ttu-id="db5cb-286">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-286">✔</span></span>|<span data-ttu-id="db5cb-287">Url https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone Teams dessin.</span><span class="sxs-lookup"><span data-stu-id="db5cb-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="db5cb-288">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-288">String</span></span>|<span data-ttu-id="db5cb-289">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-289">2048 characters</span></span>||<span data-ttu-id="db5cb-290">L https:// URL pointant vers si un utilisateur choisit d’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="db5cb-291">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="db5cb-291">Array of enum</span></span>|<span data-ttu-id="db5cb-292">1</span><span class="sxs-lookup"><span data-stu-id="db5cb-292">1</span></span>|<span data-ttu-id="db5cb-293">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-293">✔</span></span>|<span data-ttu-id="db5cb-294">Actuellement, les onglets statiques ne peuvent prendre en charge que l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de `personal` l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="db5cb-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="db5cb-295">bots</span><span class="sxs-lookup"><span data-stu-id="db5cb-295">bots</span></span>

<span data-ttu-id="db5cb-296">**Optional**</span><span class="sxs-lookup"><span data-stu-id="db5cb-296">**Optional**</span></span>

<span data-ttu-id="db5cb-297">Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="db5cb-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="db5cb-298">L’objet est un tableau (jusqu’à un seul élément actuellement un seul bot est autorisé par application) avec tous les &mdash; éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="db5cb-299">Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.</span><span class="sxs-lookup"><span data-stu-id="db5cb-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="db5cb-300">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-300">Name</span></span>| <span data-ttu-id="db5cb-301">Type</span><span class="sxs-lookup"><span data-stu-id="db5cb-301">Type</span></span>| <span data-ttu-id="db5cb-302">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-302">Maximum size</span></span> | <span data-ttu-id="db5cb-303">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-303">Required</span></span> | <span data-ttu-id="db5cb-304">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="db5cb-305">String</span><span class="sxs-lookup"><span data-stu-id="db5cb-305">String</span></span>|<span data-ttu-id="db5cb-306">64 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-306">64 characters</span></span>|<span data-ttu-id="db5cb-307">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-307">✔</span></span>|<span data-ttu-id="db5cb-308">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="db5cb-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="db5cb-309">Cela peut être identique à [l’ID d’application global.](#id)</span><span class="sxs-lookup"><span data-stu-id="db5cb-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="db5cb-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="db5cb-310">Boolean</span></span>|||<span data-ttu-id="db5cb-311">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="db5cb-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="db5cb-312">Valeur par défaut : `false`</span><span class="sxs-lookup"><span data-stu-id="db5cb-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="db5cb-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="db5cb-313">Boolean</span></span>|||<span data-ttu-id="db5cb-314">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="db5cb-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="db5cb-315">Valeur par défaut : `false`</span><span class="sxs-lookup"><span data-stu-id="db5cb-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="db5cb-316">Boolean</span><span class="sxs-lookup"><span data-stu-id="db5cb-316">Boolean</span></span>|||<span data-ttu-id="db5cb-317">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="db5cb-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="db5cb-318">Valeur par défaut : `false`</span><span class="sxs-lookup"><span data-stu-id="db5cb-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="db5cb-319">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="db5cb-319">Array of enum</span></span>|<span data-ttu-id="db5cb-320">3</span><span class="sxs-lookup"><span data-stu-id="db5cb-320">3</span></span>|<span data-ttu-id="db5cb-321">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-321">✔</span></span>|<span data-ttu-id="db5cb-322">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="db5cb-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="db5cb-323">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="db5cb-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="db5cb-324">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="db5cb-324">bots.commandLists</span></span>

<span data-ttu-id="db5cb-325">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="db5cb-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="db5cb-326">L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type ; vous devez définir une liste de commandes distincte pour chaque étendue que `object` votre bot prend en charge.</span><span class="sxs-lookup"><span data-stu-id="db5cb-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="db5cb-327">Pour plus d’informations, voir [menus bot.](~/bots/how-to/create-a-bot-commands-menu.md)</span><span class="sxs-lookup"><span data-stu-id="db5cb-327">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="db5cb-328">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-328">Name</span></span>| <span data-ttu-id="db5cb-329">Type</span><span class="sxs-lookup"><span data-stu-id="db5cb-329">Type</span></span>| <span data-ttu-id="db5cb-330">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-330">Maximum size</span></span> | <span data-ttu-id="db5cb-331">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-331">Required</span></span> | <span data-ttu-id="db5cb-332">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="db5cb-333">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="db5cb-333">array of enum</span></span>|<span data-ttu-id="db5cb-334">3</span><span class="sxs-lookup"><span data-stu-id="db5cb-334">3</span></span>|<span data-ttu-id="db5cb-335">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-335">✔</span></span>|<span data-ttu-id="db5cb-336">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="db5cb-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="db5cb-337">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="db5cb-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="db5cb-338">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="db5cb-338">array of objects</span></span>|<span data-ttu-id="db5cb-339">10</span><span class="sxs-lookup"><span data-stu-id="db5cb-339">10</span></span>|<span data-ttu-id="db5cb-340">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-340">✔</span></span>|<span data-ttu-id="db5cb-341">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="db5cb-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="db5cb-342">`title`: nom de la commande du bot (chaîne, 32).</span><span class="sxs-lookup"><span data-stu-id="db5cb-342">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="db5cb-343">`description`: une description simple ou un exemple de la syntaxe de commande et de son argument (chaîne, 128).</span><span class="sxs-lookup"><span data-stu-id="db5cb-343">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="db5cb-344">connecteurs</span><span class="sxs-lookup"><span data-stu-id="db5cb-344">connectors</span></span>

<span data-ttu-id="db5cb-345">**Optional**</span><span class="sxs-lookup"><span data-stu-id="db5cb-345">**Optional**</span></span>

<span data-ttu-id="db5cb-346">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="db5cb-347">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="db5cb-348">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="db5cb-349">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-349">Name</span></span>| <span data-ttu-id="db5cb-350">Type</span><span class="sxs-lookup"><span data-stu-id="db5cb-350">Type</span></span>| <span data-ttu-id="db5cb-351">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-351">Maximum size</span></span> | <span data-ttu-id="db5cb-352">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-352">Required</span></span> | <span data-ttu-id="db5cb-353">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="db5cb-354">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-354">String</span></span>|<span data-ttu-id="db5cb-355">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-355">2048 characters</span></span>|<span data-ttu-id="db5cb-356">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-356">✔</span></span>|<span data-ttu-id="db5cb-357">Url https:// à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="db5cb-358">String</span><span class="sxs-lookup"><span data-stu-id="db5cb-358">String</span></span>|<span data-ttu-id="db5cb-359">64 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-359">64 characters</span></span>|<span data-ttu-id="db5cb-360">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-360">✔</span></span>|<span data-ttu-id="db5cb-361">Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="db5cb-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="db5cb-362">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="db5cb-362">Array of enum</span></span>|<span data-ttu-id="db5cb-363">1</span><span class="sxs-lookup"><span data-stu-id="db5cb-363">1</span></span>|<span data-ttu-id="db5cb-364">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-364">✔</span></span>|<span data-ttu-id="db5cb-365">Spécifie si le connecteur offre une expérience dans le contexte d’un canal dans un , ou une expérience limitée à un `team` utilisateur individuel seul ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="db5cb-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="db5cb-366">Actuellement, seule `team` l’étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="db5cb-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="db5cb-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="db5cb-367">composeExtensions</span></span>

<span data-ttu-id="db5cb-368">**Optional**</span><span class="sxs-lookup"><span data-stu-id="db5cb-368">**Optional**</span></span>

<span data-ttu-id="db5cb-369">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="db5cb-370">Le nom de la fonctionnalité a été modifié de « extension de composition » à « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même pour que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="db5cb-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="db5cb-371">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="db5cb-372">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="db5cb-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="db5cb-373">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-373">Name</span></span>| <span data-ttu-id="db5cb-374">Type</span><span class="sxs-lookup"><span data-stu-id="db5cb-374">Type</span></span> | <span data-ttu-id="db5cb-375">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-375">Maximum Size</span></span> | <span data-ttu-id="db5cb-376">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-376">Required</span></span> | <span data-ttu-id="db5cb-377">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="db5cb-378">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-378">String</span></span>|<span data-ttu-id="db5cb-379">64</span><span class="sxs-lookup"><span data-stu-id="db5cb-379">64</span></span>|<span data-ttu-id="db5cb-380">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-380">✔</span></span>|<span data-ttu-id="db5cb-381">ID d’application Microsoft unique pour le bot qui permet de récupérer l’extension de messagerie, tel qu’inscrit auprès de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="db5cb-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="db5cb-382">Cela peut être identique à [l’ID d’application global.](#id)</span><span class="sxs-lookup"><span data-stu-id="db5cb-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="db5cb-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="db5cb-383">Boolean</span></span>|||<span data-ttu-id="db5cb-384">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="db5cb-385">La valeur par défaut est `false`.</span><span class="sxs-lookup"><span data-stu-id="db5cb-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="db5cb-386">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="db5cb-386">Array of object</span></span>|<span data-ttu-id="db5cb-387">10</span><span class="sxs-lookup"><span data-stu-id="db5cb-387">10</span></span>|<span data-ttu-id="db5cb-388">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-388">✔</span></span>|<span data-ttu-id="db5cb-389">Tableau de commandes pris en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="db5cb-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="db5cb-390">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="db5cb-390">composeExtensions.commands</span></span>

<span data-ttu-id="db5cb-391">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="db5cb-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="db5cb-392">Chaque commande s’affiche Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="db5cb-393">Il existe un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="db5cb-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="db5cb-394">Chaque élément de commande est un objet avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="db5cb-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="db5cb-395">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-395">Name</span></span>| <span data-ttu-id="db5cb-396">Type</span><span class="sxs-lookup"><span data-stu-id="db5cb-396">Type</span></span>| <span data-ttu-id="db5cb-397">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-397">Maximum size</span></span> | <span data-ttu-id="db5cb-398">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-398">Required</span></span> | <span data-ttu-id="db5cb-399">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="db5cb-400">String</span><span class="sxs-lookup"><span data-stu-id="db5cb-400">String</span></span>|<span data-ttu-id="db5cb-401">64 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-401">64 characters</span></span>|<span data-ttu-id="db5cb-402">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-402">✔</span></span>|<span data-ttu-id="db5cb-403">ID de la commande.</span><span class="sxs-lookup"><span data-stu-id="db5cb-403">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="db5cb-404">String</span><span class="sxs-lookup"><span data-stu-id="db5cb-404">String</span></span>|<span data-ttu-id="db5cb-405">64 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-405">64 characters</span></span>||<span data-ttu-id="db5cb-406">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="db5cb-406">Type of the command.</span></span> <span data-ttu-id="db5cb-407">L’un `query` ou `action` l’autre .</span><span class="sxs-lookup"><span data-stu-id="db5cb-407">One of `query` or `action`.</span></span> <span data-ttu-id="db5cb-408">Valeur par défaut : `query`</span><span class="sxs-lookup"><span data-stu-id="db5cb-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="db5cb-409">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-409">String</span></span>|<span data-ttu-id="db5cb-410">32 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-410">32 characters</span></span>|<span data-ttu-id="db5cb-411">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-411">✔</span></span>|<span data-ttu-id="db5cb-412">Nom de la commande conviviale.</span><span class="sxs-lookup"><span data-stu-id="db5cb-412">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="db5cb-413">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-413">String</span></span>|<span data-ttu-id="db5cb-414">128 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-414">128 characters</span></span>||<span data-ttu-id="db5cb-415">Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.</span><span class="sxs-lookup"><span data-stu-id="db5cb-415">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="db5cb-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="db5cb-416">Boolean</span></span>|||<span data-ttu-id="db5cb-417">Valeur boolé américaine qui indique si la commande doit être exécuté initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="db5cb-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="db5cb-418">Valeur par défaut : `false`</span><span class="sxs-lookup"><span data-stu-id="db5cb-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="db5cb-419">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="db5cb-419">Array of Strings</span></span>|<span data-ttu-id="db5cb-420">3</span><span class="sxs-lookup"><span data-stu-id="db5cb-420">3</span></span>||<span data-ttu-id="db5cb-421">Définit l’endroit à partir de lequel l’extension de message peut être invoquée.</span><span class="sxs-lookup"><span data-stu-id="db5cb-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="db5cb-422">N’importe quelle `compose` combinaison de `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="db5cb-423">La valeur par défaut est `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="db5cb-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="db5cb-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="db5cb-424">Boolean</span></span>|||<span data-ttu-id="db5cb-425">Valeur booléle qui indique s’il doit extraire dynamiquement le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="db5cb-425">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="db5cb-426">Objet</span><span class="sxs-lookup"><span data-stu-id="db5cb-426">Object</span></span>|||<span data-ttu-id="db5cb-427">Spécifiez le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="db5cb-427">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="db5cb-428">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-428">String</span></span>|<span data-ttu-id="db5cb-429">64</span><span class="sxs-lookup"><span data-stu-id="db5cb-429">64</span></span>||<span data-ttu-id="db5cb-430">Titre de la boîte de dialogue initiale.</span><span class="sxs-lookup"><span data-stu-id="db5cb-430">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="db5cb-431">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-431">String</span></span>|||<span data-ttu-id="db5cb-432">Largeur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="db5cb-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="db5cb-433">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-433">String</span></span>|||<span data-ttu-id="db5cb-434">Hauteur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » ou « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="db5cb-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="db5cb-435">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-435">String</span></span>|||<span data-ttu-id="db5cb-436">URL webview initiale.</span><span class="sxs-lookup"><span data-stu-id="db5cb-436">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="db5cb-437">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="db5cb-437">Array of Objects</span></span>|<span data-ttu-id="db5cb-438">5 </span><span class="sxs-lookup"><span data-stu-id="db5cb-438">5</span></span>||<span data-ttu-id="db5cb-439">Liste des handlers qui permettent d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="db5cb-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="db5cb-440">Les domaines doivent également être répertoriés dans `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-440">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="db5cb-441">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-441">String</span></span>|||<span data-ttu-id="db5cb-442">Type de handler de messages.</span><span class="sxs-lookup"><span data-stu-id="db5cb-442">The type of message handler.</span></span> <span data-ttu-id="db5cb-443">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="db5cb-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="db5cb-444">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="db5cb-444">Array of Strings</span></span>|||<span data-ttu-id="db5cb-445">Tableau de domaines pour l’inscription du handler de message de lien.</span><span class="sxs-lookup"><span data-stu-id="db5cb-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="db5cb-446">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="db5cb-446">Array of object</span></span>|<span data-ttu-id="db5cb-447">5 </span><span class="sxs-lookup"><span data-stu-id="db5cb-447">5</span></span>|<span data-ttu-id="db5cb-448">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-448">✔</span></span>|<span data-ttu-id="db5cb-449">Liste des paramètres pris par la commande.</span><span class="sxs-lookup"><span data-stu-id="db5cb-449">The list of parameters the command takes.</span></span> <span data-ttu-id="db5cb-450">Minimum : 1 ; maximum : 5</span><span class="sxs-lookup"><span data-stu-id="db5cb-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="db5cb-451">String</span><span class="sxs-lookup"><span data-stu-id="db5cb-451">String</span></span>|<span data-ttu-id="db5cb-452">64 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-452">64 characters</span></span>|<span data-ttu-id="db5cb-453">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-453">✔</span></span>|<span data-ttu-id="db5cb-454">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="db5cb-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="db5cb-455">Ceci est inclus dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="db5cb-456">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-456">String</span></span>|<span data-ttu-id="db5cb-457">32 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-457">32 characters</span></span>|<span data-ttu-id="db5cb-458">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-458">✔</span></span>|<span data-ttu-id="db5cb-459">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="db5cb-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="db5cb-460">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-460">String</span></span>|<span data-ttu-id="db5cb-461">128 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-461">128 characters</span></span>||<span data-ttu-id="db5cb-462">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="db5cb-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="db5cb-463">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-463">String</span></span>|<span data-ttu-id="db5cb-464">128 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-464">128 characters</span></span>||<span data-ttu-id="db5cb-465">Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="db5cb-466">`text`L’un des , , , , , `textarea` `number` `date` `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="db5cb-467">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="db5cb-467">Array of Objects</span></span>|<span data-ttu-id="db5cb-468">10</span><span class="sxs-lookup"><span data-stu-id="db5cb-468">10</span></span>||<span data-ttu-id="db5cb-469">Options de choix pour `choiceset` le .</span><span class="sxs-lookup"><span data-stu-id="db5cb-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="db5cb-470">Utilisez uniquement lorsque `parameter.inputType` `choiceset` c’est le cas.</span><span class="sxs-lookup"><span data-stu-id="db5cb-470">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="db5cb-471">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-471">String</span></span>|<span data-ttu-id="db5cb-472">128</span><span class="sxs-lookup"><span data-stu-id="db5cb-472">128</span></span>||<span data-ttu-id="db5cb-473">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="db5cb-473">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="db5cb-474">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-474">String</span></span>|<span data-ttu-id="db5cb-475">512</span><span class="sxs-lookup"><span data-stu-id="db5cb-475">512</span></span>||<span data-ttu-id="db5cb-476">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="db5cb-476">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="db5cb-477">autorisations</span><span class="sxs-lookup"><span data-stu-id="db5cb-477">permissions</span></span>

<span data-ttu-id="db5cb-478">**Optional**</span><span class="sxs-lookup"><span data-stu-id="db5cb-478">**Optional**</span></span>

<span data-ttu-id="db5cb-479">Tableau qui spécifie les autorisations que l’application demande, ce qui permet aux utilisateurs finaux de savoir comment `string` l’extension va s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="db5cb-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="db5cb-480">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="db5cb-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="db5cb-481">`identity`&emsp;Nécessite des informations d’identité d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-481">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="db5cb-482">`messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="db5cb-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="db5cb-483">La modification de ces autorisations lors de la mise à jour de votre application entraîne la répétition du processus de consentement par vos utilisateurs la première fois qu’ils exécutent l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="db5cb-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="db5cb-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="db5cb-484">devicePermissions</span></span>

<span data-ttu-id="db5cb-485">**Facultatif** Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="db5cb-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="db5cb-486">Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application peut demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="db5cb-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="db5cb-487">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="db5cb-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="db5cb-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="db5cb-488">validDomains</span></span>

<span data-ttu-id="db5cb-489">**Facultatif,** sauf **obligatoire lorsqu’il** est indiqué</span><span class="sxs-lookup"><span data-stu-id="db5cb-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="db5cb-490">Liste des domaines valides à partir des lesquels l’application s’attend à charger du contenu.</span><span class="sxs-lookup"><span data-stu-id="db5cb-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="db5cb-491">Les listes de domaines peuvent inclure des caractères génériques, par `*.example.com` exemple.</span><span class="sxs-lookup"><span data-stu-id="db5cb-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="db5cb-492">Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="db5cb-493">Si votre interface utilisateur de contenu ou de configuration d’onglet doit accéder à un autre domaine en plus de celui utilisé pour la configuration de l’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="db5cb-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="db5cb-494">**Toutefois, il** n’est pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="db5cb-495">Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db5cb-496">N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="db5cb-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="db5cb-497">Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` non valide.</span><span class="sxs-lookup"><span data-stu-id="db5cb-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="db5cb-498">L’objet est un tableau avec tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="db5cb-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="db5cb-499">webApplicationInfo</span></span>

<span data-ttu-id="db5cb-500">**Optional**</span><span class="sxs-lookup"><span data-stu-id="db5cb-500">**Optional**</span></span>

<span data-ttu-id="db5cb-501">Spécifiez votre ID d’application AAD et Graph pour aider les utilisateurs à se connecter en toute transparence à votre application AAD.</span><span class="sxs-lookup"><span data-stu-id="db5cb-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="db5cb-502">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-502">Name</span></span>| <span data-ttu-id="db5cb-503">Type</span><span class="sxs-lookup"><span data-stu-id="db5cb-503">Type</span></span>| <span data-ttu-id="db5cb-504">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-504">Maximum size</span></span> | <span data-ttu-id="db5cb-505">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-505">Required</span></span> | <span data-ttu-id="db5cb-506">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="db5cb-507">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-507">String</span></span>|<span data-ttu-id="db5cb-508">36 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-508">36 characters</span></span>|<span data-ttu-id="db5cb-509">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-509">✔</span></span>|<span data-ttu-id="db5cb-510">ID d’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-510">AAD application id of the app.</span></span> <span data-ttu-id="db5cb-511">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="db5cb-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="db5cb-512">Chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-512">String</span></span>|<span data-ttu-id="db5cb-513">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="db5cb-513">2048 characters</span></span>|<span data-ttu-id="db5cb-514">✔</span><span class="sxs-lookup"><span data-stu-id="db5cb-514">✔</span></span>|<span data-ttu-id="db5cb-515">URL de ressource de l’application pour l’acquisition d’un jeton d’th pour l' sso.</span><span class="sxs-lookup"><span data-stu-id="db5cb-515">Resource url of app for acquiring auth token for SSO.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="db5cb-516">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="db5cb-516">configurableProperties</span></span>

<span data-ttu-id="db5cb-517">**Facultatif** - tableau</span><span class="sxs-lookup"><span data-stu-id="db5cb-517">**Optional** - array</span></span>

<span data-ttu-id="db5cb-518">Le `configurableProperties` bloc définit les propriétés d’application que Teams administrateur peut personnaliser.</span><span class="sxs-lookup"><span data-stu-id="db5cb-518">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="db5cb-519">Pour plus d’informations, voir [personnaliser les applications dans Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="db5cb-519">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="db5cb-520">Au moins une propriété doit être définie.</span><span class="sxs-lookup"><span data-stu-id="db5cb-520">A minimum of one property must be defined.</span></span> <span data-ttu-id="db5cb-521">Vous pouvez définir un maximum de neuf propriétés dans ce bloc.</span><span class="sxs-lookup"><span data-stu-id="db5cb-521">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="db5cb-522">En tant que meilleure pratique, vous devez fournir des instructions de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-522">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="db5cb-523">Vous pouvez définir l’une des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="db5cb-523">You can define any of the following properties:</span></span>
* <span data-ttu-id="db5cb-524">`name`: permet à l’administrateur de modifier le nom complet de l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-524">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="db5cb-525">`shortDescription`: permet à l’administrateur de modifier la description courte de l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-525">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="db5cb-526">`longDescription`: permet à l’administrateur de modifier la description détaillée de l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-526">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="db5cb-527">`smallImageUrl`: il s’agit `outline` de la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="db5cb-527">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="db5cb-528">`largeImageUrl`: il s’agit `color` de la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="db5cb-528">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="db5cb-529">`accentColor`: il s’agit de la couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="db5cb-529">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="db5cb-530">`websiteUrl`: il s’agit https:// URL du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-530">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="db5cb-531">`privacyUrl`: il s’agit https:// URL vers la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-531">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="db5cb-532">`termsOfUseUrl`: il s’agit de https:// URL des conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="db5cb-532">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="db5cb-533">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="db5cb-533">defaultInstallScope</span></span>

<span data-ttu-id="db5cb-534">**Facultatif** - chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-534">**Optional** - string</span></span>

<span data-ttu-id="db5cb-535">Spécifie l’étendue d’installation définie par défaut pour cette application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-535">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="db5cb-536">L’étendue définie est l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-536">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="db5cb-537">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="db5cb-537">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="db5cb-538">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="db5cb-538">defaultGroupCapability</span></span>

<span data-ttu-id="db5cb-539">**Facultatif** - objet</span><span class="sxs-lookup"><span data-stu-id="db5cb-539">**Optional** - object</span></span>

<span data-ttu-id="db5cb-540">Lorsqu’une étendue d’installation de groupe est sélectionnée, elle définit la fonctionnalité par défaut lorsque l’utilisateur installe l’application.</span><span class="sxs-lookup"><span data-stu-id="db5cb-540">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="db5cb-541">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="db5cb-541">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="db5cb-542">Nom</span><span class="sxs-lookup"><span data-stu-id="db5cb-542">Name</span></span>| <span data-ttu-id="db5cb-543">Type</span><span class="sxs-lookup"><span data-stu-id="db5cb-543">Type</span></span>| <span data-ttu-id="db5cb-544">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="db5cb-544">Maximum size</span></span> | <span data-ttu-id="db5cb-545">Requis</span><span class="sxs-lookup"><span data-stu-id="db5cb-545">Required</span></span> | <span data-ttu-id="db5cb-546">Description</span><span class="sxs-lookup"><span data-stu-id="db5cb-546">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="db5cb-547">string</span><span class="sxs-lookup"><span data-stu-id="db5cb-547">string</span></span>|||<span data-ttu-id="db5cb-548">Lorsque l’étendue d’installation sélectionnée `team` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="db5cb-548">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="db5cb-549">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-549">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="db5cb-550">chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-550">string</span></span>|||<span data-ttu-id="db5cb-551">Lorsque l’étendue d’installation sélectionnée `groupchat` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="db5cb-551">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="db5cb-552">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-552">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="db5cb-553">chaîne</span><span class="sxs-lookup"><span data-stu-id="db5cb-553">string</span></span>|||<span data-ttu-id="db5cb-554">Lorsque l’étendue d’installation sélectionnée `meetings` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="db5cb-554">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="db5cb-555">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="db5cb-555">Options: `tab`, `bot`, or `connector`.</span></span>|

