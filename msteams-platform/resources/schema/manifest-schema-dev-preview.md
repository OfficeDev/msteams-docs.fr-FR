---
title: Développeur Preview Manifeste schema référence
description: Décrit le schéma soutenu par le manifeste pour Microsoft Teams
ms.topic: reference
keywords: équipes manifestent schéma Developer Preview
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: b52d52f96312dc2978844b07a0f7ebb1d817166d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566704"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="a32fc-104">Schéma manifeste de manifeste d’aperçu de développeur pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a32fc-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="a32fc-105">Consultez [l’aperçu des](~/resources/dev-preview/developer-preview-intro.md) développeurs pour plus d’informations sur le programme et comment vous pouvez vous inscrire.</span><span class="sxs-lookup"><span data-stu-id="a32fc-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="a32fc-106">Si vous n’utilisez pas l’aperçu du développeur, vous ne devez pas utiliser cette version du manifeste.</span><span class="sxs-lookup"><span data-stu-id="a32fc-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="a32fc-107">Voir [Référence : Schéma manifeste pour Microsoft Teams](~/resources/schema/manifest-schema.md) pour la version publique du manifeste.</span><span class="sxs-lookup"><span data-stu-id="a32fc-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="a32fc-108">Le Microsoft Teams décrit comment l’application s’intègre dans le Microsoft Teams produit.</span><span class="sxs-lookup"><span data-stu-id="a32fc-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="a32fc-109">Votre manifeste doit se conformer au schéma hébergé à [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="a32fc-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="a32fc-110">Pour plus d’informations sur les fonctionnalités disponibles voir: [Fonctionnalités dans l’aperçu des développeurs publics pour Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span><span class="sxs-lookup"><span data-stu-id="a32fc-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="a32fc-111">Exemple manifeste complet</span><span class="sxs-lookup"><span data-stu-id="a32fc-111">Sample full manifest</span></span>

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

<span data-ttu-id="a32fc-112">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a32fc-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="a32fc-113">$schema</span><span class="sxs-lookup"><span data-stu-id="a32fc-113">$schema</span></span>

<span data-ttu-id="a32fc-114">*Facultatif, mais recommandé* &ndash; corde</span><span class="sxs-lookup"><span data-stu-id="a32fc-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="a32fc-115">L https:// URL faisant référence au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="a32fc-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="a32fc-116">manifesteVersion</span><span class="sxs-lookup"><span data-stu-id="a32fc-116">manifestVersion</span></span>

<span data-ttu-id="a32fc-117">**Requis** &ndash; corde</span><span class="sxs-lookup"><span data-stu-id="a32fc-117">**Required** &ndash; String</span></span>

<span data-ttu-id="a32fc-118">La version du schéma manifeste que ce manifeste utilise.</span><span class="sxs-lookup"><span data-stu-id="a32fc-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="a32fc-119">Il devrait être « devPreview ».</span><span class="sxs-lookup"><span data-stu-id="a32fc-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="a32fc-120">version</span><span class="sxs-lookup"><span data-stu-id="a32fc-120">version</span></span>

<span data-ttu-id="a32fc-121">**Requis** &ndash; corde</span><span class="sxs-lookup"><span data-stu-id="a32fc-121">**Required** &ndash; String</span></span>

<span data-ttu-id="a32fc-122">La version de l’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="a32fc-122">The version of the specific app.</span></span> <span data-ttu-id="a32fc-123">Si vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="a32fc-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="a32fc-124">Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="a32fc-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="a32fc-125">Si cette application a été soumise au magasin, le nouveau manifeste devra être soumis à nouveau et re-validé.</span><span class="sxs-lookup"><span data-stu-id="a32fc-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="a32fc-126">Ensuite, les utilisateurs de cette application recevront automatiquement le nouveau manifeste mis à jour dans quelques heures, après son approbation.</span><span class="sxs-lookup"><span data-stu-id="a32fc-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="a32fc-127">Si l’application a demandé que les autorisations changent, les utilisateurs seront invités à mettre à niveau et à consentir à nouveau à l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="a32fc-128">Cette chaîne de version doit suivre la [norme semver](http://semver.org/) (MAJOR. mineur. PATCH).</span><span class="sxs-lookup"><span data-stu-id="a32fc-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="a32fc-129">id</span><span class="sxs-lookup"><span data-stu-id="a32fc-129">id</span></span>

<span data-ttu-id="a32fc-130">**Requis** &ndash; ID de l’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="a32fc-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="a32fc-131">L’identifiant unique généré par Microsoft pour cette application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="a32fc-132">Si vous avez enregistré un bot via le Microsoft Bot Framework, ou si l’application Web de votre onglet se signe déjà avec Microsoft, vous devez déjà avoir un IDENTIFIANT et l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="a32fc-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="a32fc-133">Sinon, vous devez générer un nouvel ID sur le portail d’enregistrement des applications Microsoft ([Mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous ajoutez [un bot](~/bots/how-to/create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="a32fc-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="a32fc-134">packageName PackageName PackageName packageName</span><span class="sxs-lookup"><span data-stu-id="a32fc-134">packageName</span></span>

<span data-ttu-id="a32fc-135">**Requis** &ndash; corde</span><span class="sxs-lookup"><span data-stu-id="a32fc-135">**Required** &ndash; String</span></span>

<span data-ttu-id="a32fc-136">Un identificateur unique pour cette application dans la notation de domaine inverse; par exemple, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="a32fc-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="a32fc-137">developer</span><span class="sxs-lookup"><span data-stu-id="a32fc-137">developer</span></span>

<span data-ttu-id="a32fc-138">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="a32fc-138">**Required**</span></span>

<span data-ttu-id="a32fc-139">Spécifie les informations sur votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="a32fc-139">Specifies information about your company.</span></span> <span data-ttu-id="a32fc-140">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="a32fc-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="a32fc-141">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-141">Name</span></span>| <span data-ttu-id="a32fc-142">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-142">Maximum size</span></span> | <span data-ttu-id="a32fc-143">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-143">Required</span></span> | <span data-ttu-id="a32fc-144">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="a32fc-145">32 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-145">32 characters</span></span>|<span data-ttu-id="a32fc-146">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-146">✔</span></span>|<span data-ttu-id="a32fc-147">Le nom d’affichage du développeur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="a32fc-148">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-148">2048 characters</span></span>|<span data-ttu-id="a32fc-149">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-149">✔</span></span>|<span data-ttu-id="a32fc-150">L https:// URL du site Web du développeur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="a32fc-151">Ce lien doit emmener les utilisateurs vers votre entreprise ou votre page de destination spécifique au produit.</span><span class="sxs-lookup"><span data-stu-id="a32fc-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="a32fc-152">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-152">2048 characters</span></span>|<span data-ttu-id="a32fc-153">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-153">✔</span></span>|<span data-ttu-id="a32fc-154">Le https:// URL de la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="a32fc-155">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-155">2048 characters</span></span>|<span data-ttu-id="a32fc-156">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-156">✔</span></span>|<span data-ttu-id="a32fc-157">Le https:// URL aux conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="a32fc-158">10 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-158">10 characters</span></span>|<span data-ttu-id="a32fc-159">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-159">✔</span></span>|<span data-ttu-id="a32fc-160">**Facultatif** L’ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="a32fc-161">localisationInfo</span><span class="sxs-lookup"><span data-stu-id="a32fc-161">localizationInfo</span></span>

<span data-ttu-id="a32fc-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a32fc-162">**Optional**</span></span>

<span data-ttu-id="a32fc-163">Permet la spécification d’une langue par défaut, ainsi que des pointeurs à des fichiers linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a32fc-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="a32fc-164">Voir [localisation](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="a32fc-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="a32fc-165">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-165">Name</span></span>| <span data-ttu-id="a32fc-166">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-166">Maximum size</span></span> | <span data-ttu-id="a32fc-167">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-167">Required</span></span> | <span data-ttu-id="a32fc-168">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="a32fc-169">4 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-169">4 characters</span></span>|<span data-ttu-id="a32fc-170">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-170">✔</span></span>|<span data-ttu-id="a32fc-171">L’étiquette de langue des chaînes dans ce fichier manifeste de haut niveau.</span><span class="sxs-lookup"><span data-stu-id="a32fc-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="a32fc-172">localisationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="a32fc-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="a32fc-173">Un éventail d’objets spécifier des traductions linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a32fc-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="a32fc-174">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-174">Name</span></span>| <span data-ttu-id="a32fc-175">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-175">Maximum size</span></span> | <span data-ttu-id="a32fc-176">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-176">Required</span></span> | <span data-ttu-id="a32fc-177">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="a32fc-178">4 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-178">4 characters</span></span>|<span data-ttu-id="a32fc-179">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-179">✔</span></span>|<span data-ttu-id="a32fc-180">L’étiquette linguistique des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="a32fc-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="a32fc-181">4 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-181">4 characters</span></span>|<span data-ttu-id="a32fc-182">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-182">✔</span></span>|<span data-ttu-id="a32fc-183">Un chemin de fichier relatif vers un fichier .json contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="a32fc-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="a32fc-184">name</span><span class="sxs-lookup"><span data-stu-id="a32fc-184">name</span></span>

<span data-ttu-id="a32fc-185">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="a32fc-185">**Required**</span></span>

<span data-ttu-id="a32fc-186">Le nom de votre expérience d’application, affiché aux utilisateurs dans l’expérience Teams’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="a32fc-187">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="a32fc-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="a32fc-188">Les valeurs de `short` et ne devraient pas être les `full` mêmes.</span><span class="sxs-lookup"><span data-stu-id="a32fc-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="a32fc-189">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-189">Name</span></span>| <span data-ttu-id="a32fc-190">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-190">Maximum size</span></span> | <span data-ttu-id="a32fc-191">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-191">Required</span></span> | <span data-ttu-id="a32fc-192">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a32fc-193">30 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-193">30 characters</span></span>|<span data-ttu-id="a32fc-194">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-194">✔</span></span>|<span data-ttu-id="a32fc-195">Le nom d’affichage court de l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="a32fc-196">100 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-196">100 characters</span></span>||<span data-ttu-id="a32fc-197">Le nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="a32fc-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="a32fc-198">description</span><span class="sxs-lookup"><span data-stu-id="a32fc-198">description</span></span>

<span data-ttu-id="a32fc-199">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="a32fc-199">**Required**</span></span>

<span data-ttu-id="a32fc-200">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a32fc-200">Describes your app to users.</span></span> <span data-ttu-id="a32fc-201">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="a32fc-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="a32fc-202">Assurez-vous que votre description décrit avec précision votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="a32fc-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="a32fc-203">Vous devez également noter, dans la description complète, si un compte externe est nécessaire pour une utilisation.</span><span class="sxs-lookup"><span data-stu-id="a32fc-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="a32fc-204">Les valeurs de `short` et ne devraient pas être les `full` mêmes.</span><span class="sxs-lookup"><span data-stu-id="a32fc-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="a32fc-205">Votre courte description ne doit pas être répétée dans la longue description et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="a32fc-206">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-206">Name</span></span>| <span data-ttu-id="a32fc-207">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-207">Maximum size</span></span> | <span data-ttu-id="a32fc-208">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-208">Required</span></span> | <span data-ttu-id="a32fc-209">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="a32fc-210">80 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-210">80 characters</span></span>|<span data-ttu-id="a32fc-211">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-211">✔</span></span>|<span data-ttu-id="a32fc-212">Une courte description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="a32fc-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="a32fc-213">4000 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-213">4000 characters</span></span>|<span data-ttu-id="a32fc-214">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-214">✔</span></span>|<span data-ttu-id="a32fc-215">La description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="a32fc-216">icons</span><span class="sxs-lookup"><span data-stu-id="a32fc-216">icons</span></span>

<span data-ttu-id="a32fc-217">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="a32fc-217">**Required**</span></span>

<span data-ttu-id="a32fc-218">Icônes utilisées dans l’application Teams’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-218">Icons used within the Teams app.</span></span> <span data-ttu-id="a32fc-219">Les fichiers icônes doivent être inclus dans le paquet de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="a32fc-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="a32fc-220">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-220">Name</span></span>| <span data-ttu-id="a32fc-221">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-221">Maximum size</span></span> | <span data-ttu-id="a32fc-222">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-222">Required</span></span> | <span data-ttu-id="a32fc-223">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="a32fc-224">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-224">2048 characters</span></span>|<span data-ttu-id="a32fc-225">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-225">✔</span></span>|<span data-ttu-id="a32fc-226">Un chemin de fichier relatif vers une icône transparente de contour PNG 32x32.</span><span class="sxs-lookup"><span data-stu-id="a32fc-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="a32fc-227">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-227">2048 characters</span></span>|<span data-ttu-id="a32fc-228">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-228">✔</span></span>|<span data-ttu-id="a32fc-229">Un chemin de fichier relatif vers une icône PNG 192x192 en couleur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="a32fc-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="a32fc-230">accentColor</span></span>

<span data-ttu-id="a32fc-231">**Requis** &ndash; corde</span><span class="sxs-lookup"><span data-stu-id="a32fc-231">**Required** &ndash; String</span></span>

<span data-ttu-id="a32fc-232">Une couleur à utiliser en conjonction avec et comme arrière-plan pour vos icônes de contour.</span><span class="sxs-lookup"><span data-stu-id="a32fc-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="a32fc-233">La valeur doit être un code couleur HTML valide commençant par '#', par exemple `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="a32fc-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="a32fc-234">configurableTabs</span></span>

<span data-ttu-id="a32fc-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a32fc-235">**Optional**</span></span>

<span data-ttu-id="a32fc-236">Utilisé lorsque votre expérience d’application dispose d’une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="a32fc-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="a32fc-237">Les onglets configurables ne sont pris en charge que dans la portée des équipes, et actuellement un seul onglet par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a32fc-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="a32fc-238">L’objet est un tableau avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="a32fc-239">Ce bloc n’est nécessaire que pour les solutions qui fournissent une solution d’onglet de canal configurable.</span><span class="sxs-lookup"><span data-stu-id="a32fc-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="a32fc-240">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-240">Name</span></span>| <span data-ttu-id="a32fc-241">Type</span><span class="sxs-lookup"><span data-stu-id="a32fc-241">Type</span></span>| <span data-ttu-id="a32fc-242">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-242">Maximum size</span></span> | <span data-ttu-id="a32fc-243">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-243">Required</span></span> | <span data-ttu-id="a32fc-244">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a32fc-245">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-245">String</span></span>|<span data-ttu-id="a32fc-246">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-246">2048 characters</span></span>|<span data-ttu-id="a32fc-247">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-247">✔</span></span>|<span data-ttu-id="a32fc-248">L https:// URL à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="a32fc-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="a32fc-249">Valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="a32fc-249">Boolean</span></span>|||<span data-ttu-id="a32fc-250">Une valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après la création.</span><span class="sxs-lookup"><span data-stu-id="a32fc-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="a32fc-251">faire défaut: `true`</span><span class="sxs-lookup"><span data-stu-id="a32fc-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="a32fc-252">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="a32fc-252">Array of enum</span></span>|<span data-ttu-id="a32fc-253">1</span><span class="sxs-lookup"><span data-stu-id="a32fc-253">1</span></span>|<span data-ttu-id="a32fc-254">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-254">✔</span></span>|<span data-ttu-id="a32fc-255">Actuellement, les onglets configurables ne supportent que `team` les `groupchat` étendues et les étendues.</span><span class="sxs-lookup"><span data-stu-id="a32fc-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="a32fc-256">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-256">String</span></span>|<span data-ttu-id="a32fc-257">2048</span><span class="sxs-lookup"><span data-stu-id="a32fc-257">2048</span></span>||<span data-ttu-id="a32fc-258">Un chemin de fichier relatif vers une image d’aperçu d’onglet pour une utilisation SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a32fc-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="a32fc-259">Taille 1024x768.</span><span class="sxs-lookup"><span data-stu-id="a32fc-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="a32fc-260">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="a32fc-260">Array of enum</span></span>|<span data-ttu-id="a32fc-261">1</span><span class="sxs-lookup"><span data-stu-id="a32fc-261">1</span></span>||<span data-ttu-id="a32fc-262">Définit comment votre onglet sera disponible en SharePoint.</span><span class="sxs-lookup"><span data-stu-id="a32fc-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="a32fc-263">Les options sont `sharePointFullPage` et `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="a32fc-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="a32fc-264">staticTabs StaticTabs StaticTabs staticTab</span><span class="sxs-lookup"><span data-stu-id="a32fc-264">staticTabs</span></span>

<span data-ttu-id="a32fc-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a32fc-265">**Optional**</span></span>

<span data-ttu-id="a32fc-266">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="a32fc-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="a32fc-267">Les onglets statiques déclarés `personal` dans la portée sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="a32fc-268">Les onglets statiques déclarés dans la `team` portée ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a32fc-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="a32fc-269">L’objet est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="a32fc-270">Ce bloc n’est nécessaire que pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="a32fc-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="a32fc-271">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-271">Name</span></span>| <span data-ttu-id="a32fc-272">Type</span><span class="sxs-lookup"><span data-stu-id="a32fc-272">Type</span></span>| <span data-ttu-id="a32fc-273">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-273">Maximum size</span></span> | <span data-ttu-id="a32fc-274">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-274">Required</span></span> | <span data-ttu-id="a32fc-275">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="a32fc-276">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-276">String</span></span>|<span data-ttu-id="a32fc-277">64 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-277">64 characters</span></span>|<span data-ttu-id="a32fc-278">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-278">✔</span></span>|<span data-ttu-id="a32fc-279">Un identificateur unique pour l’entité que l’onglet affiche.</span><span class="sxs-lookup"><span data-stu-id="a32fc-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="a32fc-280">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-280">String</span></span>|<span data-ttu-id="a32fc-281">128 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-281">128 characters</span></span>|<span data-ttu-id="a32fc-282">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-282">✔</span></span>|<span data-ttu-id="a32fc-283">Le nom d’affichage de l’onglet dans l’interface du canal.</span><span class="sxs-lookup"><span data-stu-id="a32fc-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="a32fc-284">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-284">String</span></span>|<span data-ttu-id="a32fc-285">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-285">2048 characters</span></span>|<span data-ttu-id="a32fc-286">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-286">✔</span></span>|<span data-ttu-id="a32fc-287">L https:// URL qui indique l’interface utilisateur de l’entité à afficher dans la Teams externe.</span><span class="sxs-lookup"><span data-stu-id="a32fc-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="a32fc-288">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-288">String</span></span>|<span data-ttu-id="a32fc-289">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-289">2048 characters</span></span>||<span data-ttu-id="a32fc-290">L https:// URL à pointer si un utilisateur choisit de voir dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="a32fc-291">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="a32fc-291">Array of enum</span></span>|<span data-ttu-id="a32fc-292">1</span><span class="sxs-lookup"><span data-stu-id="a32fc-292">1</span></span>|<span data-ttu-id="a32fc-293">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-293">✔</span></span>|<span data-ttu-id="a32fc-294">Actuellement, les onglets statiques ne supportent que `personal` la portée, ce qui signifie qu’il ne peut être provisionné que dans le cadre de l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="a32fc-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="a32fc-295">Bots</span><span class="sxs-lookup"><span data-stu-id="a32fc-295">bots</span></span>

<span data-ttu-id="a32fc-296">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a32fc-296">**Optional**</span></span>

<span data-ttu-id="a32fc-297">Définit une solution bot, ainsi que des informations optionnelles telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="a32fc-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="a32fc-298">L’objet est un tableau (maximum de seulement 1 élément &mdash; actuellement un seul bot est autorisé par application) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="a32fc-299">Ce bloc n’est nécessaire que pour les solutions qui fournissent une expérience bot.</span><span class="sxs-lookup"><span data-stu-id="a32fc-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="a32fc-300">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-300">Name</span></span>| <span data-ttu-id="a32fc-301">Type</span><span class="sxs-lookup"><span data-stu-id="a32fc-301">Type</span></span>| <span data-ttu-id="a32fc-302">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-302">Maximum size</span></span> | <span data-ttu-id="a32fc-303">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-303">Required</span></span> | <span data-ttu-id="a32fc-304">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a32fc-305">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-305">String</span></span>|<span data-ttu-id="a32fc-306">64 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-306">64 characters</span></span>|<span data-ttu-id="a32fc-307">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-307">✔</span></span>|<span data-ttu-id="a32fc-308">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="a32fc-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="a32fc-309">Cela peut bien être le même que l’ID de [l’application globale](#id).</span><span class="sxs-lookup"><span data-stu-id="a32fc-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="a32fc-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="a32fc-310">Boolean</span></span>|||<span data-ttu-id="a32fc-311">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="a32fc-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="a32fc-312">faire défaut: `false`</span><span class="sxs-lookup"><span data-stu-id="a32fc-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="a32fc-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="a32fc-313">Boolean</span></span>|||<span data-ttu-id="a32fc-314">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="a32fc-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="a32fc-315">faire défaut: `false`</span><span class="sxs-lookup"><span data-stu-id="a32fc-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="a32fc-316">Boolean</span><span class="sxs-lookup"><span data-stu-id="a32fc-316">Boolean</span></span>|||<span data-ttu-id="a32fc-317">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="a32fc-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="a32fc-318">faire défaut: `false`</span><span class="sxs-lookup"><span data-stu-id="a32fc-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="a32fc-319">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="a32fc-319">Array of enum</span></span>|<span data-ttu-id="a32fc-320">3</span><span class="sxs-lookup"><span data-stu-id="a32fc-320">3</span></span>|<span data-ttu-id="a32fc-321">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-321">✔</span></span>|<span data-ttu-id="a32fc-322">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="a32fc-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a32fc-323">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="a32fc-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="a32fc-324">bots.commandLists (en)</span><span class="sxs-lookup"><span data-stu-id="a32fc-324">bots.commandLists</span></span>

<span data-ttu-id="a32fc-325">Une liste optionnelle de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="a32fc-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="a32fc-326">L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type `object` ; vous devez définir une liste de commande distincte pour chaque champ d’application que votre bot prend en charge.</span><span class="sxs-lookup"><span data-stu-id="a32fc-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="a32fc-327">Pour plus d’informations, voir [menus Bot](~/bots/how-to/create-a-bot-commands-menu.md).</span><span class="sxs-lookup"><span data-stu-id="a32fc-327">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="a32fc-328">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-328">Name</span></span>| <span data-ttu-id="a32fc-329">Type</span><span class="sxs-lookup"><span data-stu-id="a32fc-329">Type</span></span>| <span data-ttu-id="a32fc-330">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-330">Maximum size</span></span> | <span data-ttu-id="a32fc-331">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-331">Required</span></span> | <span data-ttu-id="a32fc-332">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="a32fc-333">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="a32fc-333">array of enum</span></span>|<span data-ttu-id="a32fc-334">3</span><span class="sxs-lookup"><span data-stu-id="a32fc-334">3</span></span>|<span data-ttu-id="a32fc-335">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-335">✔</span></span>|<span data-ttu-id="a32fc-336">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="a32fc-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="a32fc-337">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="a32fc-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="a32fc-338">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="a32fc-338">array of objects</span></span>|<span data-ttu-id="a32fc-339">10</span><span class="sxs-lookup"><span data-stu-id="a32fc-339">10</span></span>|<span data-ttu-id="a32fc-340">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-340">✔</span></span>|<span data-ttu-id="a32fc-341">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="a32fc-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="a32fc-342">`title`: le nom de commande bot (chaîne, 32).</span><span class="sxs-lookup"><span data-stu-id="a32fc-342">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="a32fc-343">`description`: une description simple ou un exemple de la syntaxe de commande et de son argument (chaîne, 128).</span><span class="sxs-lookup"><span data-stu-id="a32fc-343">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="a32fc-344">Connecteurs</span><span class="sxs-lookup"><span data-stu-id="a32fc-344">connectors</span></span>

<span data-ttu-id="a32fc-345">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a32fc-345">**Optional**</span></span>

<span data-ttu-id="a32fc-346">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="a32fc-347">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a32fc-348">Ce bloc n’est nécessaire que pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="a32fc-349">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-349">Name</span></span>| <span data-ttu-id="a32fc-350">Type</span><span class="sxs-lookup"><span data-stu-id="a32fc-350">Type</span></span>| <span data-ttu-id="a32fc-351">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-351">Maximum size</span></span> | <span data-ttu-id="a32fc-352">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-352">Required</span></span> | <span data-ttu-id="a32fc-353">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="a32fc-354">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-354">String</span></span>|<span data-ttu-id="a32fc-355">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-355">2048 characters</span></span>|<span data-ttu-id="a32fc-356">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-356">✔</span></span>|<span data-ttu-id="a32fc-357">L https:// URL à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="a32fc-358">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-358">String</span></span>|<span data-ttu-id="a32fc-359">64 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-359">64 characters</span></span>|<span data-ttu-id="a32fc-360">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-360">✔</span></span>|<span data-ttu-id="a32fc-361">Un identificateur unique pour le connecteur qui correspond à son ID dans le tableau de [bord des développeurs de connecteurs](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="a32fc-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="a32fc-362">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="a32fc-362">Array of enum</span></span>|<span data-ttu-id="a32fc-363">1</span><span class="sxs-lookup"><span data-stu-id="a32fc-363">1</span></span>|<span data-ttu-id="a32fc-364">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-364">✔</span></span>|<span data-ttu-id="a32fc-365">Précise si le connecteur offre une expérience dans le contexte d’un canal dans un `team` , ou une expérience étendue à un utilisateur individuel seul ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="a32fc-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="a32fc-366">Actuellement, seule la portée `team` est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="a32fc-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="a32fc-367">composerExtensions</span><span class="sxs-lookup"><span data-stu-id="a32fc-367">composeExtensions</span></span>

<span data-ttu-id="a32fc-368">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a32fc-368">**Optional**</span></span>

<span data-ttu-id="a32fc-369">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="a32fc-370">Le nom de la fonctionnalité a été changé de « composer extension » à « extension de messagerie » en Novembre 2017, mais le nom manifeste reste le même de sorte que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="a32fc-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="a32fc-371">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="a32fc-372">Ce bloc n’est nécessaire que pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="a32fc-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="a32fc-373">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-373">Name</span></span>| <span data-ttu-id="a32fc-374">Type</span><span class="sxs-lookup"><span data-stu-id="a32fc-374">Type</span></span> | <span data-ttu-id="a32fc-375">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-375">Maximum Size</span></span> | <span data-ttu-id="a32fc-376">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="a32fc-376">Required</span></span> | <span data-ttu-id="a32fc-377">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="a32fc-378">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-378">String</span></span>|<span data-ttu-id="a32fc-379">64</span><span class="sxs-lookup"><span data-stu-id="a32fc-379">64</span></span>|<span data-ttu-id="a32fc-380">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-380">✔</span></span>|<span data-ttu-id="a32fc-381">L’iD unique de l’application Microsoft pour le bot qui prend en arrière l’extension de messagerie, tel qu’enregistré avec le Cadre Bot.</span><span class="sxs-lookup"><span data-stu-id="a32fc-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="a32fc-382">Cela peut bien être le même que l’ID de [l’application globale](#id).</span><span class="sxs-lookup"><span data-stu-id="a32fc-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="a32fc-383">Valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="a32fc-383">Boolean</span></span>|||<span data-ttu-id="a32fc-384">Une valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="a32fc-385">La valeur par défaut est `false`.</span><span class="sxs-lookup"><span data-stu-id="a32fc-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="a32fc-386">Tableau d’objet</span><span class="sxs-lookup"><span data-stu-id="a32fc-386">Array of object</span></span>|<span data-ttu-id="a32fc-387">10</span><span class="sxs-lookup"><span data-stu-id="a32fc-387">10</span></span>|<span data-ttu-id="a32fc-388">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-388">✔</span></span>|<span data-ttu-id="a32fc-389">Tableau de commandes que l’extension de messagerie prend en charge</span><span class="sxs-lookup"><span data-stu-id="a32fc-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="a32fc-390">composerExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="a32fc-390">composeExtensions.commands</span></span>

<span data-ttu-id="a32fc-391">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="a32fc-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="a32fc-392">Chaque commande apparaît dans Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="a32fc-393">Il y a un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="a32fc-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="a32fc-394">Chaque élément de commande est un objet avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="a32fc-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="a32fc-395">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-395">Name</span></span>| <span data-ttu-id="a32fc-396">Type</span><span class="sxs-lookup"><span data-stu-id="a32fc-396">Type</span></span>| <span data-ttu-id="a32fc-397">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-397">Maximum size</span></span> | <span data-ttu-id="a32fc-398">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-398">Required</span></span> | <span data-ttu-id="a32fc-399">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a32fc-400">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-400">String</span></span>|<span data-ttu-id="a32fc-401">64 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-401">64 characters</span></span>|<span data-ttu-id="a32fc-402">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-402">✔</span></span>|<span data-ttu-id="a32fc-403">L’identification de la commande.</span><span class="sxs-lookup"><span data-stu-id="a32fc-403">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="a32fc-404">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-404">String</span></span>|<span data-ttu-id="a32fc-405">64 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-405">64 characters</span></span>||<span data-ttu-id="a32fc-406">Type de commande.</span><span class="sxs-lookup"><span data-stu-id="a32fc-406">Type of the command.</span></span> <span data-ttu-id="a32fc-407">L’un `query` ou `action` l’autre de ou .</span><span class="sxs-lookup"><span data-stu-id="a32fc-407">One of `query` or `action`.</span></span> <span data-ttu-id="a32fc-408">faire défaut: `query`</span><span class="sxs-lookup"><span data-stu-id="a32fc-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="a32fc-409">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-409">String</span></span>|<span data-ttu-id="a32fc-410">32 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-410">32 characters</span></span>|<span data-ttu-id="a32fc-411">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-411">✔</span></span>|<span data-ttu-id="a32fc-412">Le nom de commande convivial.</span><span class="sxs-lookup"><span data-stu-id="a32fc-412">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="a32fc-413">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-413">String</span></span>|<span data-ttu-id="a32fc-414">128 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-414">128 characters</span></span>||<span data-ttu-id="a32fc-415">La description qui apparaît aux utilisateurs pour indiquer le but de cette commande.</span><span class="sxs-lookup"><span data-stu-id="a32fc-415">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="a32fc-416">Valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="a32fc-416">Boolean</span></span>|||<span data-ttu-id="a32fc-417">Une valeur Boolean qui indique si la commande doit être exécuté initialement sans paramètres.</span><span class="sxs-lookup"><span data-stu-id="a32fc-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="a32fc-418">faire défaut: `false`</span><span class="sxs-lookup"><span data-stu-id="a32fc-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="a32fc-419">Tableau des cordes</span><span class="sxs-lookup"><span data-stu-id="a32fc-419">Array of Strings</span></span>|<span data-ttu-id="a32fc-420">3</span><span class="sxs-lookup"><span data-stu-id="a32fc-420">3</span></span>||<span data-ttu-id="a32fc-421">Définit d’où l’extension de message peut être invoquée.</span><span class="sxs-lookup"><span data-stu-id="a32fc-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="a32fc-422">Toute combinaison de `compose` , `commandBox` . `message`</span><span class="sxs-lookup"><span data-stu-id="a32fc-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="a32fc-423">Par défaut est `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="a32fc-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="a32fc-424">Valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="a32fc-424">Boolean</span></span>|||<span data-ttu-id="a32fc-425">Une valeur boolean qui indique si elle doit aller chercher le module de tâche dynamiquement.</span><span class="sxs-lookup"><span data-stu-id="a32fc-425">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="a32fc-426">Objet</span><span class="sxs-lookup"><span data-stu-id="a32fc-426">Object</span></span>|||<span data-ttu-id="a32fc-427">Spécifiez le module de tâches à précharger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="a32fc-427">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="a32fc-428">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-428">String</span></span>|<span data-ttu-id="a32fc-429">64</span><span class="sxs-lookup"><span data-stu-id="a32fc-429">64</span></span>||<span data-ttu-id="a32fc-430">Titre de dialogue initial.</span><span class="sxs-lookup"><span data-stu-id="a32fc-430">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="a32fc-431">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-431">String</span></span>|||<span data-ttu-id="a32fc-432">Largeur de dialogue - soit un nombre en pixels ou mise en page par défaut comme « grand », « moyen » ou « petit ».</span><span class="sxs-lookup"><span data-stu-id="a32fc-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="a32fc-433">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-433">String</span></span>|||<span data-ttu-id="a32fc-434">Hauteur de dialogue - soit un nombre en pixels ou mise en page par défaut comme « grand », « moyen » ou « petit ».</span><span class="sxs-lookup"><span data-stu-id="a32fc-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="a32fc-435">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-435">String</span></span>|||<span data-ttu-id="a32fc-436">URL webview initiale.</span><span class="sxs-lookup"><span data-stu-id="a32fc-436">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="a32fc-437">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="a32fc-437">Array of Objects</span></span>|<span data-ttu-id="a32fc-438">5 </span><span class="sxs-lookup"><span data-stu-id="a32fc-438">5</span></span>||<span data-ttu-id="a32fc-439">Une liste de gestionnaires qui permettent d’invoquer les applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="a32fc-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="a32fc-440">Les domaines doivent également être répertoriés dans `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-440">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="a32fc-441">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-441">String</span></span>|||<span data-ttu-id="a32fc-442">Le type de gestionnaire de messages.</span><span class="sxs-lookup"><span data-stu-id="a32fc-442">The type of message handler.</span></span> <span data-ttu-id="a32fc-443">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="a32fc-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="a32fc-444">Tableau des cordes</span><span class="sxs-lookup"><span data-stu-id="a32fc-444">Array of Strings</span></span>|||<span data-ttu-id="a32fc-445">Tableau des domaines pour qui le gestionnaire de message de lien peut s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="a32fc-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="a32fc-446">Tableau d’objet</span><span class="sxs-lookup"><span data-stu-id="a32fc-446">Array of object</span></span>|<span data-ttu-id="a32fc-447">5 </span><span class="sxs-lookup"><span data-stu-id="a32fc-447">5</span></span>|<span data-ttu-id="a32fc-448">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-448">✔</span></span>|<span data-ttu-id="a32fc-449">La liste des paramètres de la commande prend.</span><span class="sxs-lookup"><span data-stu-id="a32fc-449">The list of parameters the command takes.</span></span> <span data-ttu-id="a32fc-450">Minimum: 1; maximum: 5</span><span class="sxs-lookup"><span data-stu-id="a32fc-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="a32fc-451">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-451">String</span></span>|<span data-ttu-id="a32fc-452">64 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-452">64 characters</span></span>|<span data-ttu-id="a32fc-453">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-453">✔</span></span>|<span data-ttu-id="a32fc-454">Le nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="a32fc-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="a32fc-455">Ceci est inclus dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="a32fc-456">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-456">String</span></span>|<span data-ttu-id="a32fc-457">32 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-457">32 characters</span></span>|<span data-ttu-id="a32fc-458">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-458">✔</span></span>|<span data-ttu-id="a32fc-459">Titre convivial pour le paramètre.</span><span class="sxs-lookup"><span data-stu-id="a32fc-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="a32fc-460">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-460">String</span></span>|<span data-ttu-id="a32fc-461">128 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-461">128 characters</span></span>||<span data-ttu-id="a32fc-462">Chaîne conviviale qui décrit le but de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="a32fc-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="a32fc-463">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-463">String</span></span>|<span data-ttu-id="a32fc-464">128 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-464">128 characters</span></span>||<span data-ttu-id="a32fc-465">Définit le type de contrôle affiché sur un module de tâches pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="a32fc-466">L’un `text` `textarea` `number` d’eux, `date` , , , , `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="a32fc-467">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="a32fc-467">Array of Objects</span></span>|<span data-ttu-id="a32fc-468">10</span><span class="sxs-lookup"><span data-stu-id="a32fc-468">10</span></span>||<span data-ttu-id="a32fc-469">Les options de choix pour le `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="a32fc-470">Utilisez seulement quand `parameter.inputType` est `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-470">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="a32fc-471">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-471">String</span></span>|<span data-ttu-id="a32fc-472">128</span><span class="sxs-lookup"><span data-stu-id="a32fc-472">128</span></span>||<span data-ttu-id="a32fc-473">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="a32fc-473">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="a32fc-474">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-474">String</span></span>|<span data-ttu-id="a32fc-475">512</span><span class="sxs-lookup"><span data-stu-id="a32fc-475">512</span></span>||<span data-ttu-id="a32fc-476">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="a32fc-476">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="a32fc-477">autorisations</span><span class="sxs-lookup"><span data-stu-id="a32fc-477">permissions</span></span>

<span data-ttu-id="a32fc-478">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a32fc-478">**Optional**</span></span>

<span data-ttu-id="a32fc-479">Un tableau de `string` ce qui spécifie les autorisations que l’application demande, ce qui permet aux utilisateurs finaux de savoir comment l’extension se produira.</span><span class="sxs-lookup"><span data-stu-id="a32fc-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="a32fc-480">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="a32fc-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="a32fc-481">`identity`&emsp;Nécessite des informations d’identité utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-481">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="a32fc-482">`messageTeamMembers`&emsp;Nécessite la permission d’envoyer des messages directs aux membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="a32fc-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="a32fc-483">La modification de ces autorisations lors de la mise à jour de votre application fera répéter le processus de consentement à vos utilisateurs la première fois qu’ils exécutent l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="a32fc-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="a32fc-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="a32fc-484">devicePermissions</span></span>

<span data-ttu-id="a32fc-485">**Facultatif** Tableau des cordes</span><span class="sxs-lookup"><span data-stu-id="a32fc-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="a32fc-486">Spécifie les fonctionnalités natives de l’appareil d’un utilisateur à qui votre application peut demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="a32fc-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="a32fc-487">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="a32fc-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="a32fc-488">validDomains (en)</span><span class="sxs-lookup"><span data-stu-id="a32fc-488">validDomains</span></span>

<span data-ttu-id="a32fc-489">**Facultatif,** sauf requis **lorsqu’il** est noté</span><span class="sxs-lookup"><span data-stu-id="a32fc-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="a32fc-490">Une liste de domaines valides à partir de laquelle l’application s’attend à charger n’importe quel contenu.</span><span class="sxs-lookup"><span data-stu-id="a32fc-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="a32fc-491">Les annonces de domaine peuvent inclure des wildcards, par exemple `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="a32fc-492">Cela correspond exactement à un segment du domaine; si vous avez besoin de `a.b.example.com` correspondre, puis utiliser `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="a32fc-493">Si votre configuration d’onglet ou interface utilisateur de contenu doit naviguer vers n’importe quel autre domaine en dehors de l’une des utilisations pour la configuration de l’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="a32fc-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="a32fc-494">Il **n’est** toutefois pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="a32fc-495">Par exemple, pour authentifier à l’aide d’un identifiant Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a32fc-496">N’ajoutez pas de domaines qui sont hors de votre contrôle, que ce soit directement ou via des wildcards.</span><span class="sxs-lookup"><span data-stu-id="a32fc-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="a32fc-497">Par exemple, est `yourapp.onmicrosoft.com` valide, mais `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="a32fc-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="a32fc-498">L’objet est un tableau avec tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="a32fc-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="a32fc-499">webApplicationInfo</span></span>

<span data-ttu-id="a32fc-500">**Optional**</span><span class="sxs-lookup"><span data-stu-id="a32fc-500">**Optional**</span></span>

<span data-ttu-id="a32fc-501">Spécifiez votre identifiant d’application AAD Graph informations supplémentaires pour aider les utilisateurs à se connecter de manière transparente à votre application AAD.</span><span class="sxs-lookup"><span data-stu-id="a32fc-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="a32fc-502">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-502">Name</span></span>| <span data-ttu-id="a32fc-503">Type</span><span class="sxs-lookup"><span data-stu-id="a32fc-503">Type</span></span>| <span data-ttu-id="a32fc-504">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-504">Maximum size</span></span> | <span data-ttu-id="a32fc-505">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-505">Required</span></span> | <span data-ttu-id="a32fc-506">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="a32fc-507">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-507">String</span></span>|<span data-ttu-id="a32fc-508">36 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-508">36 characters</span></span>|<span data-ttu-id="a32fc-509">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-509">✔</span></span>|<span data-ttu-id="a32fc-510">Id d’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-510">AAD application id of the app.</span></span> <span data-ttu-id="a32fc-511">Cet id doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="a32fc-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="a32fc-512">String</span><span class="sxs-lookup"><span data-stu-id="a32fc-512">String</span></span>|<span data-ttu-id="a32fc-513">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="a32fc-513">2048 characters</span></span>|<span data-ttu-id="a32fc-514">✔</span><span class="sxs-lookup"><span data-stu-id="a32fc-514">✔</span></span>|<span data-ttu-id="a32fc-515">Url de ressources de l’application pour l’acquisition de jetons auth pour SSO.</span><span class="sxs-lookup"><span data-stu-id="a32fc-515">Resource url of app for acquiring auth token for SSO.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="a32fc-516">configurablesProperties</span><span class="sxs-lookup"><span data-stu-id="a32fc-516">configurableProperties</span></span>

<span data-ttu-id="a32fc-517">**Facultatif** - tableau</span><span class="sxs-lookup"><span data-stu-id="a32fc-517">**Optional** - array</span></span>

<span data-ttu-id="a32fc-518">Le `configurableProperties` bloc définit les propriétés de l’application Teams’administrateur peut personnaliser.</span><span class="sxs-lookup"><span data-stu-id="a32fc-518">The `configurableProperties` block defines the app properties that Teams admin can customize.</span></span> <span data-ttu-id="a32fc-519">Pour plus d’informations, [consultez les applications personnalisées dans Microsoft Teams](/MicrosoftTeams/customize-apps).</span><span class="sxs-lookup"><span data-stu-id="a32fc-519">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="a32fc-520">Un minimum d’une propriété doit être défini.</span><span class="sxs-lookup"><span data-stu-id="a32fc-520">A minimum of one property must be defined.</span></span> <span data-ttu-id="a32fc-521">Vous pouvez définir un maximum de neuf propriétés dans ce bloc.</span><span class="sxs-lookup"><span data-stu-id="a32fc-521">You can define a maximum of nine properties in this block.</span></span>
> <span data-ttu-id="a32fc-522">En tant que meilleure pratique, vous devez fournir des directives de personnalisation que les utilisateurs et les clients de l’application doivent suivre lors de la personnalisation de votre application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-522">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> 

<span data-ttu-id="a32fc-523">Vous pouvez définir l’une des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a32fc-523">You can define any of the following properties:</span></span>
* <span data-ttu-id="a32fc-524">`name`: Permet à l’administrateur de modifier le nom d’affichage de l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-524">`name`: Allows admin to change the app's display name.</span></span>
* <span data-ttu-id="a32fc-525">`shortDescription`: Permet à l’administrateur de modifier la courte description de l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-525">`shortDescription`: Allows admin to change the app's short description.</span></span>
* <span data-ttu-id="a32fc-526">`longDescription`: Permet à l’administrateur de modifier la description détaillée de l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-526">`longDescription`: Allows admin to change the app's detailed description.</span></span>
* <span data-ttu-id="a32fc-527">`smallImageUrl`: C’est `outline` la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="a32fc-527">`smallImageUrl`: It is the `outline` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="a32fc-528">`largeImageUrl`: C’est `color` la propriété dans le bloc du `icons` manifeste.</span><span class="sxs-lookup"><span data-stu-id="a32fc-528">`largeImageUrl`: It is the `color` property in the `icons` block of the manifest.</span></span>
* <span data-ttu-id="a32fc-529">`accentColor`: C’est la couleur à utiliser en conjonction avec et comme arrière-plan pour vos icônes de contour.</span><span class="sxs-lookup"><span data-stu-id="a32fc-529">`accentColor`: It is the color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="a32fc-530">`websiteUrl`: Il s’agit https://'URL du site Web du développeur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-530">`websiteUrl`: It is the https:// URL to the developer's website.</span></span>
* <span data-ttu-id="a32fc-531">`privacyUrl`: Il s’agit https://'URL de la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-531">`privacyUrl`: It is the https:// URL to the developer's privacy policy.</span></span>
* <span data-ttu-id="a32fc-532">`termsOfUseUrl`: C’est https:// URL aux conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="a32fc-532">`termsOfUseUrl`: It is the https:// URL to the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="a32fc-533">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="a32fc-533">defaultInstallScope</span></span>

<span data-ttu-id="a32fc-534">**Facultatif** - chaîne</span><span class="sxs-lookup"><span data-stu-id="a32fc-534">**Optional** - string</span></span>

<span data-ttu-id="a32fc-535">Spécifie la portée d’installation définie pour cette application par défaut.</span><span class="sxs-lookup"><span data-stu-id="a32fc-535">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="a32fc-536">La portée définie sera l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-536">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="a32fc-537">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="a32fc-537">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="a32fc-538">defaultGroupCapability (en)</span><span class="sxs-lookup"><span data-stu-id="a32fc-538">defaultGroupCapability</span></span>

<span data-ttu-id="a32fc-539">**Facultatif** - objet</span><span class="sxs-lookup"><span data-stu-id="a32fc-539">**Optional** - object</span></span>

<span data-ttu-id="a32fc-540">Lorsqu’une étendue d’installation de groupe est sélectionnée, elle définit la capacité par défaut lorsque l’utilisateur installe l’application.</span><span class="sxs-lookup"><span data-stu-id="a32fc-540">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="a32fc-541">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="a32fc-541">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="a32fc-542">Nom</span><span class="sxs-lookup"><span data-stu-id="a32fc-542">Name</span></span>| <span data-ttu-id="a32fc-543">Type</span><span class="sxs-lookup"><span data-stu-id="a32fc-543">Type</span></span>| <span data-ttu-id="a32fc-544">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="a32fc-544">Maximum size</span></span> | <span data-ttu-id="a32fc-545">Requis</span><span class="sxs-lookup"><span data-stu-id="a32fc-545">Required</span></span> | <span data-ttu-id="a32fc-546">Description</span><span class="sxs-lookup"><span data-stu-id="a32fc-546">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="a32fc-547">string</span><span class="sxs-lookup"><span data-stu-id="a32fc-547">string</span></span>|||<span data-ttu-id="a32fc-548">Lorsque la portée d’installation sélectionnée `team` est , ce champ spécifie la capacité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="a32fc-548">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="a32fc-549">Options: `tab` , , ou `bot` `connector` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-549">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="a32fc-550">string</span><span class="sxs-lookup"><span data-stu-id="a32fc-550">string</span></span>|||<span data-ttu-id="a32fc-551">Lorsque la portée d’installation sélectionnée `groupchat` est , ce champ spécifie la capacité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="a32fc-551">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="a32fc-552">Options: `tab` , , ou `bot` `connector` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-552">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="a32fc-553">string</span><span class="sxs-lookup"><span data-stu-id="a32fc-553">string</span></span>|||<span data-ttu-id="a32fc-554">Lorsque la portée d’installation sélectionnée `meetings` est , ce champ spécifie la capacité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="a32fc-554">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="a32fc-555">Options: `tab` , , ou `bot` `connector` .</span><span class="sxs-lookup"><span data-stu-id="a32fc-555">Options: `tab`, `bot`, or `connector`.</span></span>|

