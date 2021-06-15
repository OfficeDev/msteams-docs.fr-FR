---
title: Référence du schéma de manifeste d’aperçu du développeur
description: Décrit le schéma pris en charge par le manifeste pour Microsoft Teams
ms.topic: reference
keywords: Aperçu du schéma de manifeste teams pour les développeurs
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: c2009038341a22664b0f055fa9756a9d1eba87b9
ms.sourcegitcommit: 64c1cf2a268ef101a519bc31d171618d0f6cd12a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/13/2021
ms.locfileid: "52915089"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="34165-104">Schéma de manifeste de prévisualisation pour les développeurs Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="34165-104">Developer preview manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="34165-105">Pour plus d’informations sur la façon d’activer la prévisualisation pour les développeurs, voir la prévisualisation pour [les développeurs Microsoft Teams](~/resources/dev-preview/developer-preview-intro.md).</span><span class="sxs-lookup"><span data-stu-id="34165-105">For information on how to enable developer preview, see [public developer preview for Microsoft Teams](~/resources/dev-preview/developer-preview-intro.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="34165-106">Si vous n’utilisez pas les fonctionnalités de prévisualisation pour les développeurs, utilisez plutôt le manifeste de l’application pour les [fonctionnalités ga.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="34165-106">If you aren't using developer preview features, use the [app manifest for GA features](~/resources/schema/manifest-schema.md) instead.</span></span>

<span data-ttu-id="34165-107">Le Microsoft Teams de l’application décrit comment l’application s’intègre au Microsoft Teams produit.</span><span class="sxs-lookup"><span data-stu-id="34165-107">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="34165-108">Votre manifeste doit être conforme au schéma hébergé sur [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="34165-108">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="34165-109">Pour plus d’informations sur les fonctionnalités disponibles, voir : [Fonctionnalités de](~/resources/dev-preview/developer-preview-features.md)la prévisualisation pour les développeurs publics Microsoft Teams .</span><span class="sxs-lookup"><span data-stu-id="34165-109">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="34165-110">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="34165-110">Sample full manifest</span></span>

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
      "contentBotId": "Specifies to the app that tab is an Adaptive Card Tab. You can either provide the contentBotId or contentUrl.",
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
  "webApplicationInfo": {
    "id": "AAD App ID",
    "resource": "Resource URL for acquiring auth token for SSO",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelSettings.Read.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "ChannelMessage.Read.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group",
      "Member.ReadWrite.Group",
      "Owner.ReadWrite.Group"
    ],
  },
   "configurableProperties": [
     "name",
     "shortDescription",
     "longDescription",
     "smallImageUrl", 
     "largeImageUrl", 
     "accentColor",
     "developerUrl",
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

<span data-ttu-id="34165-111">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="34165-111">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="34165-112">$schema</span><span class="sxs-lookup"><span data-stu-id="34165-112">$schema</span></span>

<span data-ttu-id="34165-113">*Facultatif, mais recommandé* &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="34165-113">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="34165-114">L https:// URL référente au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="34165-114">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="34165-115">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="34165-115">manifestVersion</span></span>

<span data-ttu-id="34165-116">**Obligatoire** &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="34165-116">**Required** &ndash; String</span></span>

<span data-ttu-id="34165-117">Version du schéma de manifeste utilisé par ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="34165-117">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="34165-118">Il doit s’appelle « devPreview ».</span><span class="sxs-lookup"><span data-stu-id="34165-118">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="34165-119">version</span><span class="sxs-lookup"><span data-stu-id="34165-119">version</span></span>

<span data-ttu-id="34165-120">**Obligatoire** &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="34165-120">**Required** &ndash; String</span></span>

<span data-ttu-id="34165-121">Version de l’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="34165-121">The version of the specific app.</span></span> <span data-ttu-id="34165-122">Si vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="34165-122">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="34165-123">Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="34165-123">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="34165-124">Si cette application a été soumise au Store, le nouveau manifeste devra être soumis à nouveau et validé à nouveau.</span><span class="sxs-lookup"><span data-stu-id="34165-124">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="34165-125">Ensuite, les utilisateurs de cette application obtiennent automatiquement le nouveau manifeste mis à jour dans quelques heures, après son approbation.</span><span class="sxs-lookup"><span data-stu-id="34165-125">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="34165-126">Si l’application demande des autorisations, les utilisateurs sont invités à mettre à niveau et à consentir à l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-126">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="34165-127">Cette chaîne de version doit suivre la [norme de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="34165-127">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="34165-128">id</span><span class="sxs-lookup"><span data-stu-id="34165-128">id</span></span>

<span data-ttu-id="34165-129">**Obligatoire** &ndash; ID d’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="34165-129">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="34165-130">Identificateur unique généré par Microsoft pour cette application.</span><span class="sxs-lookup"><span data-stu-id="34165-130">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="34165-131">Si vous avez inscrit un bot via le Microsoft Bot Framework ou si l’application web de votre onglet se signe déjà avec Microsoft, vous devez déjà avoir un ID et l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="34165-131">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="34165-132">Sinon, vous devez générer un nouvel ID sur le portail d’inscription des applications Microsoft[(Mes applications),](https://apps.dev.microsoft.com)entrez-le ici, puis réutilisez-le lorsque vous [ajoutez un bot.](~/bots/how-to/create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="34165-132">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="34165-133">packageName</span><span class="sxs-lookup"><span data-stu-id="34165-133">packageName</span></span>

<span data-ttu-id="34165-134">**Obligatoire** &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="34165-134">**Required** &ndash; String</span></span>

<span data-ttu-id="34165-135">Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="34165-135">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="34165-136">developer</span><span class="sxs-lookup"><span data-stu-id="34165-136">developer</span></span>

<span data-ttu-id="34165-137">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="34165-137">**Required**</span></span>

<span data-ttu-id="34165-138">Spécifie des informations sur votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="34165-138">Specifies information about your company.</span></span> <span data-ttu-id="34165-139">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="34165-139">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="34165-140">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-140">Name</span></span>| <span data-ttu-id="34165-141">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-141">Maximum size</span></span> | <span data-ttu-id="34165-142">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-142">Required</span></span> | <span data-ttu-id="34165-143">Description</span><span class="sxs-lookup"><span data-stu-id="34165-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="34165-144">32 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-144">32 characters</span></span>|<span data-ttu-id="34165-145">✔</span><span class="sxs-lookup"><span data-stu-id="34165-145">✔</span></span>|<span data-ttu-id="34165-146">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="34165-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="34165-147">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-147">2048 characters</span></span>|<span data-ttu-id="34165-148">✔</span><span class="sxs-lookup"><span data-stu-id="34165-148">✔</span></span>|<span data-ttu-id="34165-149">L https:// URL du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="34165-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="34165-150">Ce lien doit permettre aux utilisateurs d’accès à votre entreprise ou à votre page d’accueil spécifique au produit.</span><span class="sxs-lookup"><span data-stu-id="34165-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="34165-151">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-151">2048 characters</span></span>|<span data-ttu-id="34165-152">✔</span><span class="sxs-lookup"><span data-stu-id="34165-152">✔</span></span>|<span data-ttu-id="34165-153">L https:// URL vers la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="34165-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="34165-154">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-154">2048 characters</span></span>|<span data-ttu-id="34165-155">✔</span><span class="sxs-lookup"><span data-stu-id="34165-155">✔</span></span>|<span data-ttu-id="34165-156">L https:// URL vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="34165-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="34165-157">10 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-157">10 characters</span></span>|<span data-ttu-id="34165-158">✔</span><span class="sxs-lookup"><span data-stu-id="34165-158">✔</span></span>|<span data-ttu-id="34165-159">**Facultatif** ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-159">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="34165-160">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="34165-160">localizationInfo</span></span>

<span data-ttu-id="34165-161">**Optional**</span><span class="sxs-lookup"><span data-stu-id="34165-161">**Optional**</span></span>

<span data-ttu-id="34165-162">Autorise la spécification d’une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="34165-162">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="34165-163">Voir [localisation.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="34165-163">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="34165-164">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-164">Name</span></span>| <span data-ttu-id="34165-165">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-165">Maximum size</span></span> | <span data-ttu-id="34165-166">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-166">Required</span></span> | <span data-ttu-id="34165-167">Description</span><span class="sxs-lookup"><span data-stu-id="34165-167">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="34165-168">4 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-168">4 characters</span></span>|<span data-ttu-id="34165-169">✔</span><span class="sxs-lookup"><span data-stu-id="34165-169">✔</span></span>|<span data-ttu-id="34165-170">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="34165-170">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="34165-171">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="34165-171">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="34165-172">Tableau d’objets spécifiant des traductions linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="34165-172">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="34165-173">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-173">Name</span></span>| <span data-ttu-id="34165-174">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-174">Maximum size</span></span> | <span data-ttu-id="34165-175">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-175">Required</span></span> | <span data-ttu-id="34165-176">Description</span><span class="sxs-lookup"><span data-stu-id="34165-176">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="34165-177">4 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-177">4 characters</span></span>|<span data-ttu-id="34165-178">✔</span><span class="sxs-lookup"><span data-stu-id="34165-178">✔</span></span>|<span data-ttu-id="34165-179">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="34165-179">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="34165-180">4 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-180">4 characters</span></span>|<span data-ttu-id="34165-181">✔</span><span class="sxs-lookup"><span data-stu-id="34165-181">✔</span></span>|<span data-ttu-id="34165-182">Chemin d’accès relatif au fichier .json contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="34165-182">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="34165-183">name</span><span class="sxs-lookup"><span data-stu-id="34165-183">name</span></span>

<span data-ttu-id="34165-184">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="34165-184">**Required**</span></span>

<span data-ttu-id="34165-185">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’Teams expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="34165-185">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="34165-186">Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="34165-186">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="34165-187">Les valeurs `short` de et ne doivent pas être `full` identiques.</span><span class="sxs-lookup"><span data-stu-id="34165-187">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="34165-188">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-188">Name</span></span>| <span data-ttu-id="34165-189">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-189">Maximum size</span></span> | <span data-ttu-id="34165-190">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-190">Required</span></span> | <span data-ttu-id="34165-191">Description</span><span class="sxs-lookup"><span data-stu-id="34165-191">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="34165-192">30 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-192">30 characters</span></span>|<span data-ttu-id="34165-193">✔</span><span class="sxs-lookup"><span data-stu-id="34165-193">✔</span></span>|<span data-ttu-id="34165-194">Nom d’affichage court de l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-194">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="34165-195">100 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-195">100 characters</span></span>||<span data-ttu-id="34165-196">Nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="34165-196">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="34165-197">description</span><span class="sxs-lookup"><span data-stu-id="34165-197">description</span></span>

<span data-ttu-id="34165-198">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="34165-198">**Required**</span></span>

<span data-ttu-id="34165-199">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="34165-199">Describes your app to users.</span></span> <span data-ttu-id="34165-200">Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="34165-200">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="34165-201">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="34165-201">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="34165-202">Notez également, dans la description complète, si un compte externe est requis pour être utilisé.</span><span class="sxs-lookup"><span data-stu-id="34165-202">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="34165-203">Les valeurs `short` de et ne doivent pas être `full` identiques.</span><span class="sxs-lookup"><span data-stu-id="34165-203">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="34165-204">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="34165-204">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="34165-205">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-205">Name</span></span>| <span data-ttu-id="34165-206">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-206">Maximum size</span></span> | <span data-ttu-id="34165-207">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-207">Required</span></span> | <span data-ttu-id="34165-208">Description</span><span class="sxs-lookup"><span data-stu-id="34165-208">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="34165-209">80 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-209">80 characters</span></span>|<span data-ttu-id="34165-210">✔</span><span class="sxs-lookup"><span data-stu-id="34165-210">✔</span></span>|<span data-ttu-id="34165-211">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="34165-211">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="34165-212">4 000 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-212">4000 characters</span></span>|<span data-ttu-id="34165-213">✔</span><span class="sxs-lookup"><span data-stu-id="34165-213">✔</span></span>|<span data-ttu-id="34165-214">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="34165-214">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="34165-215">icons</span><span class="sxs-lookup"><span data-stu-id="34165-215">icons</span></span>

<span data-ttu-id="34165-216">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="34165-216">**Required**</span></span>

<span data-ttu-id="34165-217">Icônes utilisées dans l’Teams app.</span><span class="sxs-lookup"><span data-stu-id="34165-217">Icons used within the Teams app.</span></span> <span data-ttu-id="34165-218">Les fichiers d’icône doivent être inclus dans le package de chargement.</span><span class="sxs-lookup"><span data-stu-id="34165-218">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="34165-219">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-219">Name</span></span>| <span data-ttu-id="34165-220">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-220">Maximum size</span></span> | <span data-ttu-id="34165-221">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-221">Required</span></span> | <span data-ttu-id="34165-222">Description</span><span class="sxs-lookup"><span data-stu-id="34165-222">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="34165-223">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-223">2048 characters</span></span>|<span data-ttu-id="34165-224">✔</span><span class="sxs-lookup"><span data-stu-id="34165-224">✔</span></span>|<span data-ttu-id="34165-225">Chemin d’accès relatif à un plan PNG transparent 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="34165-225">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="34165-226">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-226">2048 characters</span></span>|<span data-ttu-id="34165-227">✔</span><span class="sxs-lookup"><span data-stu-id="34165-227">✔</span></span>|<span data-ttu-id="34165-228">Chemin d’accès relatif à une icône PNG couleur 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="34165-228">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="34165-229">accentColor</span><span class="sxs-lookup"><span data-stu-id="34165-229">accentColor</span></span>

<span data-ttu-id="34165-230">**Obligatoire** &ndash; Chaîne</span><span class="sxs-lookup"><span data-stu-id="34165-230">**Required** &ndash; String</span></span>

<span data-ttu-id="34165-231">Couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="34165-231">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="34165-232">La valeur doit être un code de couleur HTML valide commençant par « # » par `#4464ee` exemple.</span><span class="sxs-lookup"><span data-stu-id="34165-232">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="34165-233">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="34165-233">configurableTabs</span></span>

<span data-ttu-id="34165-234">**Optional**</span><span class="sxs-lookup"><span data-stu-id="34165-234">**Optional**</span></span>

<span data-ttu-id="34165-235">Utilisé lorsque l’expérience de votre application possède une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="34165-235">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="34165-236">Les onglets configurables sont pris en charge uniquement dans l’étendue Teams, et actuellement, un seul onglet par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="34165-236">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="34165-237">L’objet est un tableau avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="34165-237">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="34165-238">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet de canal configurable.</span><span class="sxs-lookup"><span data-stu-id="34165-238">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="34165-239">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-239">Name</span></span>| <span data-ttu-id="34165-240">Type</span><span class="sxs-lookup"><span data-stu-id="34165-240">Type</span></span>| <span data-ttu-id="34165-241">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-241">Maximum size</span></span> | <span data-ttu-id="34165-242">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-242">Required</span></span> | <span data-ttu-id="34165-243">Description</span><span class="sxs-lookup"><span data-stu-id="34165-243">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="34165-244">String</span><span class="sxs-lookup"><span data-stu-id="34165-244">String</span></span>|<span data-ttu-id="34165-245">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-245">2048 characters</span></span>|<span data-ttu-id="34165-246">✔</span><span class="sxs-lookup"><span data-stu-id="34165-246">✔</span></span>|<span data-ttu-id="34165-247">Url https:// à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="34165-247">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="34165-248">Boolean</span><span class="sxs-lookup"><span data-stu-id="34165-248">Boolean</span></span>|||<span data-ttu-id="34165-249">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="34165-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="34165-250">Valeur par défaut : `true`</span><span class="sxs-lookup"><span data-stu-id="34165-250">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="34165-251">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="34165-251">Array of enum</span></span>|<span data-ttu-id="34165-252">1</span><span class="sxs-lookup"><span data-stu-id="34165-252">1</span></span>|<span data-ttu-id="34165-253">✔</span><span class="sxs-lookup"><span data-stu-id="34165-253">✔</span></span>|<span data-ttu-id="34165-254">Actuellement, les onglets configurables ne peuvent que les `team` étendues et les `groupchat` étendues.</span><span class="sxs-lookup"><span data-stu-id="34165-254">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="34165-255">String</span><span class="sxs-lookup"><span data-stu-id="34165-255">String</span></span>|<span data-ttu-id="34165-256">2048</span><span class="sxs-lookup"><span data-stu-id="34165-256">2048</span></span>||<span data-ttu-id="34165-257">Chemin d’accès relatif à une image d’aperçu d’onglet à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="34165-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="34165-258">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="34165-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="34165-259">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="34165-259">Array of enum</span></span>|<span data-ttu-id="34165-260">1</span><span class="sxs-lookup"><span data-stu-id="34165-260">1</span></span>||<span data-ttu-id="34165-261">Définit la façon dont votre onglet sera disponible dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="34165-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="34165-262">Les options sont `sharePointFullPage` et `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="34165-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="34165-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="34165-263">staticTabs</span></span>

<span data-ttu-id="34165-264">**Optional**</span><span class="sxs-lookup"><span data-stu-id="34165-264">**Optional**</span></span>

<span data-ttu-id="34165-265">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="34165-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="34165-266">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="34165-267">Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="34165-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="34165-268">Restituer les onglets avec des cartes adaptatives en spécifiant plutôt que `contentBotId` `contentUrl` dans le bloc **staticTabs.**</span><span class="sxs-lookup"><span data-stu-id="34165-268">Render tabs with Adaptive Cards by specifying `contentBotId` instead of `contentUrl` in the **staticTabs** block.</span></span>

<span data-ttu-id="34165-269">L’objet est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="34165-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="34165-270">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="34165-270">This block is required only for solutions that provide a static tab solution.</span></span>


|<span data-ttu-id="34165-271">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-271">Name</span></span>| <span data-ttu-id="34165-272">Type</span><span class="sxs-lookup"><span data-stu-id="34165-272">Type</span></span>| <span data-ttu-id="34165-273">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-273">Maximum size</span></span> | <span data-ttu-id="34165-274">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-274">Required</span></span> | <span data-ttu-id="34165-275">Description</span><span class="sxs-lookup"><span data-stu-id="34165-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="34165-276">String</span><span class="sxs-lookup"><span data-stu-id="34165-276">String</span></span>|<span data-ttu-id="34165-277">64 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-277">64 characters</span></span>|<span data-ttu-id="34165-278">✔</span><span class="sxs-lookup"><span data-stu-id="34165-278">✔</span></span>|<span data-ttu-id="34165-279">Identificateur unique de l’entité affichée par l’onglet.</span><span class="sxs-lookup"><span data-stu-id="34165-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="34165-280">String</span><span class="sxs-lookup"><span data-stu-id="34165-280">String</span></span>|<span data-ttu-id="34165-281">128 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-281">128 characters</span></span>|<span data-ttu-id="34165-282">✔</span><span class="sxs-lookup"><span data-stu-id="34165-282">✔</span></span>|<span data-ttu-id="34165-283">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="34165-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="34165-284">String</span><span class="sxs-lookup"><span data-stu-id="34165-284">String</span></span>|<span data-ttu-id="34165-285">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-285">2048 characters</span></span>|<span data-ttu-id="34165-286">✔</span><span class="sxs-lookup"><span data-stu-id="34165-286">✔</span></span>|<span data-ttu-id="34165-287">Url https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone Teams dessin.</span><span class="sxs-lookup"><span data-stu-id="34165-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`contentBotId`|   | | | <span data-ttu-id="34165-288">L Microsoft Teams’ID d’application spécifié pour le bot dans le portail Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="34165-288">The Microsoft Teams app ID specified for the bot in the Bot Framework portal.</span></span> |
|`websiteUrl`|<span data-ttu-id="34165-289">String</span><span class="sxs-lookup"><span data-stu-id="34165-289">String</span></span>|<span data-ttu-id="34165-290">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-290">2048 characters</span></span>||<span data-ttu-id="34165-291">L https:// URL pointant vers si un utilisateur choisit d’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="34165-291">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="34165-292">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="34165-292">Array of enum</span></span>|<span data-ttu-id="34165-293">1</span><span class="sxs-lookup"><span data-stu-id="34165-293">1</span></span>|<span data-ttu-id="34165-294">✔</span><span class="sxs-lookup"><span data-stu-id="34165-294">✔</span></span>|<span data-ttu-id="34165-295">Actuellement, les onglets statiques ne prendre en charge que l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de `personal` l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="34165-295">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="34165-296">bots</span><span class="sxs-lookup"><span data-stu-id="34165-296">bots</span></span>

<span data-ttu-id="34165-297">**Optional**</span><span class="sxs-lookup"><span data-stu-id="34165-297">**Optional**</span></span>

<span data-ttu-id="34165-298">Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="34165-298">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="34165-299">L’objet est un tableau (jusqu’à un seul élément actuellement un seul bot est autorisé par application) avec tous les &mdash; éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="34165-299">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="34165-300">Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.</span><span class="sxs-lookup"><span data-stu-id="34165-300">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="34165-301">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-301">Name</span></span>| <span data-ttu-id="34165-302">Type</span><span class="sxs-lookup"><span data-stu-id="34165-302">Type</span></span>| <span data-ttu-id="34165-303">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-303">Maximum size</span></span> | <span data-ttu-id="34165-304">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-304">Required</span></span> | <span data-ttu-id="34165-305">Description</span><span class="sxs-lookup"><span data-stu-id="34165-305">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="34165-306">String</span><span class="sxs-lookup"><span data-stu-id="34165-306">String</span></span>|<span data-ttu-id="34165-307">64 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-307">64 characters</span></span>|<span data-ttu-id="34165-308">✔</span><span class="sxs-lookup"><span data-stu-id="34165-308">✔</span></span>|<span data-ttu-id="34165-309">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="34165-309">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="34165-310">Cela peut être identique à [l’ID d’application global.](#id)</span><span class="sxs-lookup"><span data-stu-id="34165-310">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="34165-311">Boolean</span><span class="sxs-lookup"><span data-stu-id="34165-311">Boolean</span></span>|||<span data-ttu-id="34165-312">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="34165-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="34165-313">Valeur par défaut : `false`</span><span class="sxs-lookup"><span data-stu-id="34165-313">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="34165-314">Boolean</span><span class="sxs-lookup"><span data-stu-id="34165-314">Boolean</span></span>|||<span data-ttu-id="34165-315">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="34165-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="34165-316">Valeur par défaut : `false`</span><span class="sxs-lookup"><span data-stu-id="34165-316">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="34165-317">Boolean</span><span class="sxs-lookup"><span data-stu-id="34165-317">Boolean</span></span>|||<span data-ttu-id="34165-318">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="34165-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="34165-319">Valeur par défaut : `false`</span><span class="sxs-lookup"><span data-stu-id="34165-319">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="34165-320">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="34165-320">Array of enum</span></span>|<span data-ttu-id="34165-321">3</span><span class="sxs-lookup"><span data-stu-id="34165-321">3</span></span>|<span data-ttu-id="34165-322">✔</span><span class="sxs-lookup"><span data-stu-id="34165-322">✔</span></span>|<span data-ttu-id="34165-323">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="34165-323">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="34165-324">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="34165-324">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="34165-325">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="34165-325">bots.commandLists</span></span>

<span data-ttu-id="34165-326">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="34165-326">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="34165-327">L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type ; vous devez définir une liste de commandes distincte pour chaque étendue que `object` votre bot prend en charge.</span><span class="sxs-lookup"><span data-stu-id="34165-327">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="34165-328">Pour plus d’informations, voir [menus bot.](~/bots/how-to/create-a-bot-commands-menu.md)</span><span class="sxs-lookup"><span data-stu-id="34165-328">For more information, see [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md).</span></span>

|<span data-ttu-id="34165-329">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-329">Name</span></span>| <span data-ttu-id="34165-330">Type</span><span class="sxs-lookup"><span data-stu-id="34165-330">Type</span></span>| <span data-ttu-id="34165-331">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-331">Maximum size</span></span> | <span data-ttu-id="34165-332">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-332">Required</span></span> | <span data-ttu-id="34165-333">Description</span><span class="sxs-lookup"><span data-stu-id="34165-333">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="34165-334">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="34165-334">array of enum</span></span>|<span data-ttu-id="34165-335">3</span><span class="sxs-lookup"><span data-stu-id="34165-335">3</span></span>|<span data-ttu-id="34165-336">✔</span><span class="sxs-lookup"><span data-stu-id="34165-336">✔</span></span>|<span data-ttu-id="34165-337">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="34165-337">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="34165-338">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="34165-338">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="34165-339">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="34165-339">array of objects</span></span>|<span data-ttu-id="34165-340">10</span><span class="sxs-lookup"><span data-stu-id="34165-340">10</span></span>|<span data-ttu-id="34165-341">✔</span><span class="sxs-lookup"><span data-stu-id="34165-341">✔</span></span>|<span data-ttu-id="34165-342">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="34165-342">An array of commands the bot supports:</span></span><br><span data-ttu-id="34165-343">`title`: nom de la commande du bot (chaîne, 32).</span><span class="sxs-lookup"><span data-stu-id="34165-343">`title`: the bot command name (string, 32).</span></span><br><span data-ttu-id="34165-344">`description`: une description simple ou un exemple de la syntaxe de commande et de son argument (chaîne, 128).</span><span class="sxs-lookup"><span data-stu-id="34165-344">`description`: a simple description or example of the command syntax and its argument (string, 128).</span></span>|

## <a name="connectors"></a><span data-ttu-id="34165-345">connecteurs</span><span class="sxs-lookup"><span data-stu-id="34165-345">connectors</span></span>

<span data-ttu-id="34165-346">**Optional**</span><span class="sxs-lookup"><span data-stu-id="34165-346">**Optional**</span></span>

<span data-ttu-id="34165-347">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-347">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="34165-348">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="34165-348">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="34165-349">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="34165-349">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="34165-350">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-350">Name</span></span>| <span data-ttu-id="34165-351">Type</span><span class="sxs-lookup"><span data-stu-id="34165-351">Type</span></span>| <span data-ttu-id="34165-352">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-352">Maximum size</span></span> | <span data-ttu-id="34165-353">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-353">Required</span></span> | <span data-ttu-id="34165-354">Description</span><span class="sxs-lookup"><span data-stu-id="34165-354">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="34165-355">String</span><span class="sxs-lookup"><span data-stu-id="34165-355">String</span></span>|<span data-ttu-id="34165-356">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-356">2048 characters</span></span>|<span data-ttu-id="34165-357">✔</span><span class="sxs-lookup"><span data-stu-id="34165-357">✔</span></span>|<span data-ttu-id="34165-358">Url https:// à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="34165-358">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="34165-359">String</span><span class="sxs-lookup"><span data-stu-id="34165-359">String</span></span>|<span data-ttu-id="34165-360">64 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-360">64 characters</span></span>|<span data-ttu-id="34165-361">✔</span><span class="sxs-lookup"><span data-stu-id="34165-361">✔</span></span>|<span data-ttu-id="34165-362">Identificateur unique du connecteur qui correspond à son ID dans le [tableau de bord du développeur de connecteurs.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="34165-362">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="34165-363">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="34165-363">Array of enum</span></span>|<span data-ttu-id="34165-364">1</span><span class="sxs-lookup"><span data-stu-id="34165-364">1</span></span>|<span data-ttu-id="34165-365">✔</span><span class="sxs-lookup"><span data-stu-id="34165-365">✔</span></span>|<span data-ttu-id="34165-366">Spécifie si le connecteur offre une expérience dans le contexte d’un canal dans un , ou une expérience limitée à un `team` utilisateur individuel seul ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="34165-366">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="34165-367">Actuellement, seule `team` l’étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="34165-367">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="34165-368">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="34165-368">composeExtensions</span></span>

<span data-ttu-id="34165-369">**Optional**</span><span class="sxs-lookup"><span data-stu-id="34165-369">**Optional**</span></span>

<span data-ttu-id="34165-370">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-370">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="34165-371">Le nom de la fonctionnalité a été modifié de « extension de composition » à « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même pour que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="34165-371">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="34165-372">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="34165-372">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="34165-373">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="34165-373">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="34165-374">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-374">Name</span></span>| <span data-ttu-id="34165-375">Type</span><span class="sxs-lookup"><span data-stu-id="34165-375">Type</span></span> | <span data-ttu-id="34165-376">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-376">Maximum Size</span></span> | <span data-ttu-id="34165-377">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="34165-377">Required</span></span> | <span data-ttu-id="34165-378">Description</span><span class="sxs-lookup"><span data-stu-id="34165-378">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="34165-379">String</span><span class="sxs-lookup"><span data-stu-id="34165-379">String</span></span>|<span data-ttu-id="34165-380">64</span><span class="sxs-lookup"><span data-stu-id="34165-380">64</span></span>|<span data-ttu-id="34165-381">✔</span><span class="sxs-lookup"><span data-stu-id="34165-381">✔</span></span>|<span data-ttu-id="34165-382">ID d’application Microsoft unique pour le bot qui permet de récupérer l’extension de messagerie, tel qu’inscrit auprès de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="34165-382">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="34165-383">Cela peut être identique à [l’ID d’application global.](#id)</span><span class="sxs-lookup"><span data-stu-id="34165-383">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="34165-384">Boolean</span><span class="sxs-lookup"><span data-stu-id="34165-384">Boolean</span></span>|||<span data-ttu-id="34165-385">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="34165-385">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="34165-386">La valeur par défaut est `false`.</span><span class="sxs-lookup"><span data-stu-id="34165-386">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="34165-387">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="34165-387">Array of object</span></span>|<span data-ttu-id="34165-388">10</span><span class="sxs-lookup"><span data-stu-id="34165-388">10</span></span>|<span data-ttu-id="34165-389">✔</span><span class="sxs-lookup"><span data-stu-id="34165-389">✔</span></span>|<span data-ttu-id="34165-390">Tableau de commandes pris en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="34165-390">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="34165-391">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="34165-391">composeExtensions.commands</span></span>

<span data-ttu-id="34165-392">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="34165-392">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="34165-393">Chaque commande s’affiche Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="34165-393">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="34165-394">Il existe un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="34165-394">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="34165-395">Chaque élément de commande est un objet avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="34165-395">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="34165-396">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-396">Name</span></span>| <span data-ttu-id="34165-397">Type</span><span class="sxs-lookup"><span data-stu-id="34165-397">Type</span></span>| <span data-ttu-id="34165-398">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-398">Maximum size</span></span> | <span data-ttu-id="34165-399">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-399">Required</span></span> | <span data-ttu-id="34165-400">Description</span><span class="sxs-lookup"><span data-stu-id="34165-400">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="34165-401">String</span><span class="sxs-lookup"><span data-stu-id="34165-401">String</span></span>|<span data-ttu-id="34165-402">64 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-402">64 characters</span></span>|<span data-ttu-id="34165-403">✔</span><span class="sxs-lookup"><span data-stu-id="34165-403">✔</span></span>|<span data-ttu-id="34165-404">ID de la commande.</span><span class="sxs-lookup"><span data-stu-id="34165-404">The ID for the command.</span></span>|
|`type`|<span data-ttu-id="34165-405">String</span><span class="sxs-lookup"><span data-stu-id="34165-405">String</span></span>|<span data-ttu-id="34165-406">64 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-406">64 characters</span></span>||<span data-ttu-id="34165-407">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="34165-407">Type of the command.</span></span> <span data-ttu-id="34165-408">L’un `query` ou `action` l’autre .</span><span class="sxs-lookup"><span data-stu-id="34165-408">One of `query` or `action`.</span></span> <span data-ttu-id="34165-409">Valeur par défaut : `query`</span><span class="sxs-lookup"><span data-stu-id="34165-409">Default: `query`</span></span>|
|`title`|<span data-ttu-id="34165-410">String</span><span class="sxs-lookup"><span data-stu-id="34165-410">String</span></span>|<span data-ttu-id="34165-411">32 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-411">32 characters</span></span>|<span data-ttu-id="34165-412">✔</span><span class="sxs-lookup"><span data-stu-id="34165-412">✔</span></span>|<span data-ttu-id="34165-413">Nom de la commande conviviale.</span><span class="sxs-lookup"><span data-stu-id="34165-413">The user-friendly command name.</span></span>|
|`description`|<span data-ttu-id="34165-414">String</span><span class="sxs-lookup"><span data-stu-id="34165-414">String</span></span>|<span data-ttu-id="34165-415">128 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-415">128 characters</span></span>||<span data-ttu-id="34165-416">Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.</span><span class="sxs-lookup"><span data-stu-id="34165-416">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="34165-417">Boolean</span><span class="sxs-lookup"><span data-stu-id="34165-417">Boolean</span></span>|||<span data-ttu-id="34165-418">Valeur boolé américaine qui indique si la commande doit être exécuté initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="34165-418">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="34165-419">Valeur par défaut : `false`</span><span class="sxs-lookup"><span data-stu-id="34165-419">Default: `false`</span></span>|
|`context`|<span data-ttu-id="34165-420">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="34165-420">Array of Strings</span></span>|<span data-ttu-id="34165-421">3</span><span class="sxs-lookup"><span data-stu-id="34165-421">3</span></span>||<span data-ttu-id="34165-422">Définit l’endroit à partir de lequel l’extension de message peut être invoquée.</span><span class="sxs-lookup"><span data-stu-id="34165-422">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="34165-423">N’importe quelle `compose` combinaison de `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="34165-423">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="34165-424">La valeur par défaut est `["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="34165-424">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="34165-425">Boolean</span><span class="sxs-lookup"><span data-stu-id="34165-425">Boolean</span></span>|||<span data-ttu-id="34165-426">Valeur booléle qui indique s’il doit extraire dynamiquement le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="34165-426">A boolean value that indicates if it should fetch the task module dynamically.</span></span>|
|`taskInfo`|<span data-ttu-id="34165-427">Objet</span><span class="sxs-lookup"><span data-stu-id="34165-427">Object</span></span>|||<span data-ttu-id="34165-428">Spécifiez le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="34165-428">Specify the task module to preload when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="34165-429">String</span><span class="sxs-lookup"><span data-stu-id="34165-429">String</span></span>|<span data-ttu-id="34165-430">64</span><span class="sxs-lookup"><span data-stu-id="34165-430">64</span></span>||<span data-ttu-id="34165-431">Titre de la boîte de dialogue initiale.</span><span class="sxs-lookup"><span data-stu-id="34165-431">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="34165-432">String</span><span class="sxs-lookup"><span data-stu-id="34165-432">String</span></span>|||<span data-ttu-id="34165-433">Largeur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="34165-433">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="34165-434">String</span><span class="sxs-lookup"><span data-stu-id="34165-434">String</span></span>|||<span data-ttu-id="34165-435">Hauteur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="34165-435">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="34165-436">String</span><span class="sxs-lookup"><span data-stu-id="34165-436">String</span></span>|||<span data-ttu-id="34165-437">URL webview initiale.</span><span class="sxs-lookup"><span data-stu-id="34165-437">Initial webview URL.</span></span>|
|`messageHandlers`|<span data-ttu-id="34165-438">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="34165-438">Array of Objects</span></span>|<span data-ttu-id="34165-439">5 </span><span class="sxs-lookup"><span data-stu-id="34165-439">5</span></span>||<span data-ttu-id="34165-440">Liste des handlers qui permettent d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="34165-440">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="34165-441">Les domaines doivent également être répertoriés dans `validDomains` .</span><span class="sxs-lookup"><span data-stu-id="34165-441">Domains must also be listed in `validDomains`.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="34165-442">String</span><span class="sxs-lookup"><span data-stu-id="34165-442">String</span></span>|||<span data-ttu-id="34165-443">Type de handler de messages.</span><span class="sxs-lookup"><span data-stu-id="34165-443">The type of message handler.</span></span> <span data-ttu-id="34165-444">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="34165-444">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="34165-445">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="34165-445">Array of Strings</span></span>|||<span data-ttu-id="34165-446">Tableau de domaines pour l’inscription du handler de message de lien.</span><span class="sxs-lookup"><span data-stu-id="34165-446">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="34165-447">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="34165-447">Array of object</span></span>|<span data-ttu-id="34165-448">5 </span><span class="sxs-lookup"><span data-stu-id="34165-448">5</span></span>|<span data-ttu-id="34165-449">✔</span><span class="sxs-lookup"><span data-stu-id="34165-449">✔</span></span>|<span data-ttu-id="34165-450">Liste des paramètres pris par la commande.</span><span class="sxs-lookup"><span data-stu-id="34165-450">The list of parameters the command takes.</span></span> <span data-ttu-id="34165-451">Minimum : 1 ; maximum : 5</span><span class="sxs-lookup"><span data-stu-id="34165-451">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="34165-452">String</span><span class="sxs-lookup"><span data-stu-id="34165-452">String</span></span>|<span data-ttu-id="34165-453">64 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-453">64 characters</span></span>|<span data-ttu-id="34165-454">✔</span><span class="sxs-lookup"><span data-stu-id="34165-454">✔</span></span>|<span data-ttu-id="34165-455">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="34165-455">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="34165-456">Ceci est inclus dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="34165-456">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="34165-457">String</span><span class="sxs-lookup"><span data-stu-id="34165-457">String</span></span>|<span data-ttu-id="34165-458">32 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-458">32 characters</span></span>|<span data-ttu-id="34165-459">✔</span><span class="sxs-lookup"><span data-stu-id="34165-459">✔</span></span>|<span data-ttu-id="34165-460">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="34165-460">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="34165-461">String</span><span class="sxs-lookup"><span data-stu-id="34165-461">String</span></span>|<span data-ttu-id="34165-462">128 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-462">128 characters</span></span>||<span data-ttu-id="34165-463">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="34165-463">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="34165-464">String</span><span class="sxs-lookup"><span data-stu-id="34165-464">String</span></span>|<span data-ttu-id="34165-465">128 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-465">128 characters</span></span>||<span data-ttu-id="34165-466">Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="34165-466">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="34165-467">`text`L’un des , , , , , `textarea` `number` `date` `time` `toggle` `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="34165-467">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`.</span></span>|
|`parameter.choices`|<span data-ttu-id="34165-468">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="34165-468">Array of Objects</span></span>|<span data-ttu-id="34165-469">10</span><span class="sxs-lookup"><span data-stu-id="34165-469">10</span></span>||<span data-ttu-id="34165-470">Options de choix pour `choiceset` le .</span><span class="sxs-lookup"><span data-stu-id="34165-470">The choice options for the `choiceset`.</span></span> <span data-ttu-id="34165-471">Utilisez uniquement lorsque `parameter.inputType` `choiceset` c’est le cas.</span><span class="sxs-lookup"><span data-stu-id="34165-471">Use only when `parameter.inputType` is `choiceset`.</span></span>|
|`parameter.choices.title`|<span data-ttu-id="34165-472">String</span><span class="sxs-lookup"><span data-stu-id="34165-472">String</span></span>|<span data-ttu-id="34165-473">128</span><span class="sxs-lookup"><span data-stu-id="34165-473">128</span></span>||<span data-ttu-id="34165-474">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="34165-474">Title of the choice.</span></span>|
|`parameter.choices.value`|<span data-ttu-id="34165-475">String</span><span class="sxs-lookup"><span data-stu-id="34165-475">String</span></span>|<span data-ttu-id="34165-476">512</span><span class="sxs-lookup"><span data-stu-id="34165-476">512</span></span>||<span data-ttu-id="34165-477">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="34165-477">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="34165-478">autorisations</span><span class="sxs-lookup"><span data-stu-id="34165-478">permissions</span></span>

<span data-ttu-id="34165-479">**Optional**</span><span class="sxs-lookup"><span data-stu-id="34165-479">**Optional**</span></span>

<span data-ttu-id="34165-480">Tableau qui spécifie les autorisations que l’application demande, ce qui permet aux utilisateurs finaux de savoir comment `string` l’extension va s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="34165-480">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="34165-481">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="34165-481">The following options are non-exclusive:</span></span>

* <span data-ttu-id="34165-482">`identity`&emsp;Nécessite des informations d’identité d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="34165-482">`identity` &emsp; Requires user identity information.</span></span>
* <span data-ttu-id="34165-483">`messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="34165-483">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members.</span></span>

<span data-ttu-id="34165-484">La modification de ces autorisations lors de la mise à jour de votre application entraîne la répétition du processus de consentement par vos utilisateurs la première fois qu’ils exécutent l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="34165-484">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="34165-485">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="34165-485">devicePermissions</span></span>

<span data-ttu-id="34165-486">**Facultatif** Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="34165-486">**Optional** Array of Strings</span></span>

<span data-ttu-id="34165-487">Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application peut demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="34165-487">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="34165-488">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="34165-488">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="34165-489">validDomains</span><span class="sxs-lookup"><span data-stu-id="34165-489">validDomains</span></span>

<span data-ttu-id="34165-490">**Facultatif,** sauf **obligatoire lorsqu’il** est indiqué</span><span class="sxs-lookup"><span data-stu-id="34165-490">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="34165-491">Liste des domaines valides à partir des lesquels l’application s’attend à charger du contenu.</span><span class="sxs-lookup"><span data-stu-id="34165-491">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="34165-492">Les listes de domaines peuvent inclure des caractères génériques, par `*.example.com` exemple.</span><span class="sxs-lookup"><span data-stu-id="34165-492">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="34165-493">Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="34165-493">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="34165-494">Si votre interface utilisateur de contenu ou de configuration d’onglet doit accéder à un autre domaine en plus de celui utilisé pour la configuration de l’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="34165-494">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="34165-495">**Toutefois, il** n’est pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="34165-495">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="34165-496">Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="34165-496">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34165-497">N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="34165-497">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="34165-498">Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="34165-498">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="34165-499">L’objet est un tableau avec tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="34165-499">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="34165-500">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="34165-500">webApplicationInfo</span></span>

<span data-ttu-id="34165-501">**Optional**</span><span class="sxs-lookup"><span data-stu-id="34165-501">**Optional**</span></span>

<span data-ttu-id="34165-502">Spécifiez votre ID d’application AAD et Graph informations pour aider les utilisateurs à se connecter en toute transparence à votre application AAD.</span><span class="sxs-lookup"><span data-stu-id="34165-502">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="34165-503">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-503">Name</span></span>| <span data-ttu-id="34165-504">Type</span><span class="sxs-lookup"><span data-stu-id="34165-504">Type</span></span>| <span data-ttu-id="34165-505">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-505">Maximum size</span></span> | <span data-ttu-id="34165-506">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-506">Required</span></span> | <span data-ttu-id="34165-507">Description</span><span class="sxs-lookup"><span data-stu-id="34165-507">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="34165-508">String</span><span class="sxs-lookup"><span data-stu-id="34165-508">String</span></span>|<span data-ttu-id="34165-509">36 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-509">36 characters</span></span>|<span data-ttu-id="34165-510">✔</span><span class="sxs-lookup"><span data-stu-id="34165-510">✔</span></span>|<span data-ttu-id="34165-511">ID d’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-511">AAD application id of the app.</span></span> <span data-ttu-id="34165-512">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="34165-512">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="34165-513">String</span><span class="sxs-lookup"><span data-stu-id="34165-513">String</span></span>|<span data-ttu-id="34165-514">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="34165-514">2048 characters</span></span>|<span data-ttu-id="34165-515">✔</span><span class="sxs-lookup"><span data-stu-id="34165-515">✔</span></span>|<span data-ttu-id="34165-516">URL de ressource de l’application pour l’acquisition d’un jeton d’th pour l' sso.</span><span class="sxs-lookup"><span data-stu-id="34165-516">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="34165-517">Tableau</span><span class="sxs-lookup"><span data-stu-id="34165-517">Array</span></span>|<span data-ttu-id="34165-518">Maximum 100 éléments</span><span class="sxs-lookup"><span data-stu-id="34165-518">Maximum 100 items</span></span>|<span data-ttu-id="34165-519">✔</span><span class="sxs-lookup"><span data-stu-id="34165-519">✔</span></span>|<span data-ttu-id="34165-520">Autorisations de ressources pour l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-520">Resource permissions for application.</span></span>|

## <a name="configurableproperties"></a><span data-ttu-id="34165-521">configurableProperties</span><span class="sxs-lookup"><span data-stu-id="34165-521">configurableProperties</span></span>

<span data-ttu-id="34165-522">**Facultatif** - tableau</span><span class="sxs-lookup"><span data-stu-id="34165-522">**Optional** - array</span></span>

<span data-ttu-id="34165-523">Le `configurableProperties` bloc définit les propriétés d’application que les administrateurs Teams personnaliser.</span><span class="sxs-lookup"><span data-stu-id="34165-523">The `configurableProperties` block defines the app properties that Teams admins can customize.</span></span> <span data-ttu-id="34165-524">Pour plus d’informations, voir [activer la personnalisation de l’application.](~/concepts/design/enable-app-customization.md)</span><span class="sxs-lookup"><span data-stu-id="34165-524">For more information, see [enable app customization](~/concepts/design/enable-app-customization.md).</span></span>

> [!NOTE]
> <span data-ttu-id="34165-525">Au moins une propriété doit être définie.</span><span class="sxs-lookup"><span data-stu-id="34165-525">A minimum of one property must be defined.</span></span> <span data-ttu-id="34165-526">Vous pouvez définir un maximum de neuf propriétés dans ce bloc.</span><span class="sxs-lookup"><span data-stu-id="34165-526">You can define a maximum of nine properties in this block.</span></span>

<span data-ttu-id="34165-527">Vous pouvez définir l’une des propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="34165-527">You can define any of the following properties:</span></span>

* <span data-ttu-id="34165-528">`name`: nom d’affichage de l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-528">`name`: The app's display name.</span></span>
* <span data-ttu-id="34165-529">`shortDescription`: Description courte de l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-529">`shortDescription`: The app's short description.</span></span>
* <span data-ttu-id="34165-530">`longDescription`: Description détaillée de l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-530">`longDescription`: The app's detailed description.</span></span>
* <span data-ttu-id="34165-531">`smallImageUrl`: Icône de plan de l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-531">`smallImageUrl`: The app's outline icon.</span></span>
* <span data-ttu-id="34165-532">`largeImageUrl`: Icône de couleur de l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-532">`largeImageUrl`: The app's color icon.</span></span>
* <span data-ttu-id="34165-533">`accentColor`: couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="34165-533">`accentColor`: The color to use in conjunction with and as a background for your outline icons.</span></span>
* <span data-ttu-id="34165-534">`developerUrl`: URL HTTPS du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="34165-534">`developerUrl`: The HTTPS URL of the developer's website.</span></span>
* <span data-ttu-id="34165-535">`privacyUrl`: URL HTTPS de la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="34165-535">`privacyUrl`: The HTTPS URL of the developer's privacy policy.</span></span>
* <span data-ttu-id="34165-536">`termsOfUseUrl`: URL HTTPS des conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="34165-536">`termsOfUseUrl`: The HTTPS URL of the developer's terms of use.</span></span>

## <a name="defaultinstallscope"></a><span data-ttu-id="34165-537">defaultInstallScope</span><span class="sxs-lookup"><span data-stu-id="34165-537">defaultInstallScope</span></span>

<span data-ttu-id="34165-538">**Facultatif** - chaîne</span><span class="sxs-lookup"><span data-stu-id="34165-538">**Optional** - string</span></span>

<span data-ttu-id="34165-539">Spécifie l’étendue d’installation définie par défaut pour cette application.</span><span class="sxs-lookup"><span data-stu-id="34165-539">Specifies the install scope defined for this app by default.</span></span> <span data-ttu-id="34165-540">L’étendue définie est l’option affichée sur le bouton lorsqu’un utilisateur tente d’ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-540">The defined scope will be the option displayed on the button when a user tries to add the app.</span></span> <span data-ttu-id="34165-541">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="34165-541">Options are:</span></span>
* `personal`
* `team`
* `groupchat`
* `meetings`

## <a name="defaultgroupcapability"></a><span data-ttu-id="34165-542">defaultGroupCapability</span><span class="sxs-lookup"><span data-stu-id="34165-542">defaultGroupCapability</span></span>

<span data-ttu-id="34165-543">**Facultatif** - objet</span><span class="sxs-lookup"><span data-stu-id="34165-543">**Optional** - object</span></span>

<span data-ttu-id="34165-544">Lorsqu’une étendue d’installation de groupe est sélectionnée, elle définit la fonctionnalité par défaut lorsque l’utilisateur installe l’application.</span><span class="sxs-lookup"><span data-stu-id="34165-544">When a group install scope is selected, it will define the default capability when the user installs the app.</span></span> <span data-ttu-id="34165-545">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="34165-545">Options are:</span></span>
* `team`
* `groupchat`
* `meetings`
 
|<span data-ttu-id="34165-546">Nom</span><span class="sxs-lookup"><span data-stu-id="34165-546">Name</span></span>| <span data-ttu-id="34165-547">Type</span><span class="sxs-lookup"><span data-stu-id="34165-547">Type</span></span>| <span data-ttu-id="34165-548">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="34165-548">Maximum size</span></span> | <span data-ttu-id="34165-549">Requis</span><span class="sxs-lookup"><span data-stu-id="34165-549">Required</span></span> | <span data-ttu-id="34165-550">Description</span><span class="sxs-lookup"><span data-stu-id="34165-550">Description</span></span>|
|---|---|---|---|---|
|`team`|<span data-ttu-id="34165-551">string</span><span class="sxs-lookup"><span data-stu-id="34165-551">string</span></span>|||<span data-ttu-id="34165-552">Lorsque l’étendue d’installation sélectionnée `team` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="34165-552">When the install scope selected is `team`, this field specifies the default capability available.</span></span> <span data-ttu-id="34165-553">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="34165-553">Options: `tab`, `bot`, or `connector`.</span></span>|
|`groupchat`|<span data-ttu-id="34165-554">string</span><span class="sxs-lookup"><span data-stu-id="34165-554">string</span></span>|||<span data-ttu-id="34165-555">Lorsque l’étendue d’installation sélectionnée `groupchat` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="34165-555">When the install scope selected is `groupchat`, this field specifies the default capability available.</span></span> <span data-ttu-id="34165-556">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="34165-556">Options: `tab`, `bot`, or `connector`.</span></span>|
|`meetings`|<span data-ttu-id="34165-557">string</span><span class="sxs-lookup"><span data-stu-id="34165-557">string</span></span>|||<span data-ttu-id="34165-558">Lorsque l’étendue d’installation sélectionnée `meetings` est , ce champ spécifie la fonctionnalité par défaut disponible.</span><span class="sxs-lookup"><span data-stu-id="34165-558">When the install scope selected is `meetings`, this field specifies the default capability available.</span></span> <span data-ttu-id="34165-559">Options : `tab` , `bot` ou `connector` .</span><span class="sxs-lookup"><span data-stu-id="34165-559">Options: `tab`, `bot`, or `connector`.</span></span>|
