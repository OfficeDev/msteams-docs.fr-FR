---
title: Référence du schéma de manifeste de l’aperçu développeur
description: Décrit le schéma pris en charge par le manifeste pour Microsoft teams
keywords: Aperçu des développeurs de schéma de manifeste teams
ms.date: 05/20/2019
ms.openlocfilehash: b99e1ae99b7fd1edd4c695f43f3ac25270f0c710
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673561"
---
# <a name="developer-preview-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="3683b-104">Schéma de manifeste de l’aperçu développeur pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="3683b-104">Developer preview manifest schema for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="3683b-105">Pour plus d’informations sur le programme et sur la procédure de participation, voir [developer preview](~/resources/dev-preview/developer-preview-intro.md) .</span><span class="sxs-lookup"><span data-stu-id="3683b-105">See [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) for information on the program and how you can join.</span></span>
> <span data-ttu-id="3683b-106">Si vous n’utilisez pas l’aperçu du développeur, vous ne devez pas utiliser cette version du manifeste.</span><span class="sxs-lookup"><span data-stu-id="3683b-106">If you are not using the developer preview you should not be using this version of the manifest.</span></span> <span data-ttu-id="3683b-107">Voir [référence : schéma de manifeste pour Microsoft teams](~/resources/schema/manifest-schema.md) pour la version publique du manifeste.</span><span class="sxs-lookup"><span data-stu-id="3683b-107">See [Reference: Manifest schema for Microsoft Teams](~/resources/schema/manifest-schema.md) for the public version of the manifest.</span></span>

<span data-ttu-id="3683b-108">Le manifeste Microsoft teams décrit la façon dont l’application s’intègre dans le produit Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="3683b-108">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="3683b-109">Votre manifeste doit être conforme au schéma hébergé sur [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span><span class="sxs-lookup"><span data-stu-id="3683b-109">Your manifest must conform to the schema hosted at [`https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json`](https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json).</span></span>

<span data-ttu-id="3683b-110">Pour plus d’informations sur les fonctionnalités disponibles, voir : [Features in the public developer preview for Microsoft teams](~/resources/dev-preview/developer-preview-features.md).</span><span class="sxs-lookup"><span data-stu-id="3683b-110">For more information on the features available see: [Features in the Public Developer Preview for Microsoft Teams](~/resources/dev-preview/developer-preview-features.md).</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="3683b-111">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="3683b-111">Sample full manifest</span></span>

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
  ]
}
```

<span data-ttu-id="3683b-112">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="3683b-112">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="3683b-113">$schema</span><span class="sxs-lookup"><span data-stu-id="3683b-113">$schema</span></span>

<span data-ttu-id="3683b-114">*Facultatif, mais chaîne recommandée* &ndash;</span><span class="sxs-lookup"><span data-stu-id="3683b-114">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="3683b-115">URL https://référençant le schéma JSON du manifeste.</span><span class="sxs-lookup"><span data-stu-id="3683b-115">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="3683b-116">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="3683b-116">manifestVersion</span></span>

<span data-ttu-id="3683b-117">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="3683b-117">**Required** &ndash; String</span></span>

<span data-ttu-id="3683b-118">Version du schéma de manifeste utilisé par ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="3683b-118">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="3683b-119">Il doit être « devPreview ».</span><span class="sxs-lookup"><span data-stu-id="3683b-119">It should be "devPreview".</span></span>

## <a name="version"></a><span data-ttu-id="3683b-120">version</span><span class="sxs-lookup"><span data-stu-id="3683b-120">version</span></span>

<span data-ttu-id="3683b-121">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="3683b-121">**Required** &ndash; String</span></span>

<span data-ttu-id="3683b-122">Version de l’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="3683b-122">The version of the specific app.</span></span> <span data-ttu-id="3683b-123">Si vous mettez à jour un événement dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="3683b-123">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="3683b-124">Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3683b-124">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="3683b-125">Si cette application a été envoyée au magasin, le nouveau manifeste doit être soumis à nouveau et revalidé.</span><span class="sxs-lookup"><span data-stu-id="3683b-125">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="3683b-126">Ensuite, les utilisateurs de cette application obtiendront automatiquement le nouveau manifeste mis à jour en quelques heures, une fois celui-ci approuvé.</span><span class="sxs-lookup"><span data-stu-id="3683b-126">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="3683b-127">Si l’application a demandé une modification des autorisations, les utilisateurs sont invités à effectuer une mise à niveau et à reconfigurer l’application.</span><span class="sxs-lookup"><span data-stu-id="3683b-127">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="3683b-128">Cette chaîne de version doit suivre la norme [semver](http://semver.org/) (major. Petites. CORRECTIF).</span><span class="sxs-lookup"><span data-stu-id="3683b-128">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="3683b-129">id</span><span class="sxs-lookup"><span data-stu-id="3683b-129">id</span></span>

<span data-ttu-id="3683b-130">ID d’application Microsoft **requis** &ndash;</span><span class="sxs-lookup"><span data-stu-id="3683b-130">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="3683b-131">Identificateur unique généré par Microsoft pour cette application.</span><span class="sxs-lookup"><span data-stu-id="3683b-131">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="3683b-132">Si vous avez inscrit un robot via Microsoft bot Framework ou si l’application Web de votre onglet se connecte déjà à Microsoft, vous devez déjà avoir un ID et l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="3683b-132">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="3683b-133">Dans le cas contraire, vous devez générer un nouvel ID dans le portail d’inscription des applications Microsoft ([mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous [Ajoutez un bot](~/bots/how-to/create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="3683b-133">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you [add a bot](~/bots/how-to/create-a-bot-for-teams.md).</span></span>

## <a name="packagename"></a><span data-ttu-id="3683b-134">packageName</span><span class="sxs-lookup"><span data-stu-id="3683b-134">packageName</span></span>

<span data-ttu-id="3683b-135">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="3683b-135">**Required** &ndash; String</span></span>

<span data-ttu-id="3683b-136">Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="3683b-136">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="3683b-137">developer</span><span class="sxs-lookup"><span data-stu-id="3683b-137">developer</span></span>

<span data-ttu-id="3683b-138">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="3683b-138">**Required**</span></span>

<span data-ttu-id="3683b-139">Spécifie les informations relatives à votre société.</span><span class="sxs-lookup"><span data-stu-id="3683b-139">Specifies information about your company.</span></span> <span data-ttu-id="3683b-140">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="3683b-140">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span>

|<span data-ttu-id="3683b-141">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-141">Name</span></span>| <span data-ttu-id="3683b-142">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-142">Maximum size</span></span> | <span data-ttu-id="3683b-143">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-143">Required</span></span> | <span data-ttu-id="3683b-144">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-144">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="3683b-145">32 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-145">32 characters</span></span>|<span data-ttu-id="3683b-146">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-146">✔</span></span>|<span data-ttu-id="3683b-147">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="3683b-147">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="3683b-148">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-148">2048 characters</span></span>|<span data-ttu-id="3683b-149">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-149">✔</span></span>|<span data-ttu-id="3683b-150">URL https://vers le site Web du développeur.</span><span class="sxs-lookup"><span data-stu-id="3683b-150">The https:// URL to the developer's website.</span></span> <span data-ttu-id="3683b-151">Ce lien doit prendre les utilisateurs à la page d’accueil de votre entreprise ou de votre propre produit.</span><span class="sxs-lookup"><span data-stu-id="3683b-151">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="3683b-152">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-152">2048 characters</span></span>|<span data-ttu-id="3683b-153">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-153">✔</span></span>|<span data-ttu-id="3683b-154">URL https://vers la stratégie de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="3683b-154">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="3683b-155">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-155">2048 characters</span></span>|<span data-ttu-id="3683b-156">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-156">✔</span></span>|<span data-ttu-id="3683b-157">L’URL https://vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="3683b-157">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="3683b-158">10 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-158">10 characters</span></span>|<span data-ttu-id="3683b-159">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-159">✔</span></span>|<span data-ttu-id="3683b-160">**Facultatif** ID réseau du partenaire Microsoft qui identifie l’organisation partenaire qui crée l’application.</span><span class="sxs-lookup"><span data-stu-id="3683b-160">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="3683b-161">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="3683b-161">localizationInfo</span></span>

<span data-ttu-id="3683b-162">**Optional**</span><span class="sxs-lookup"><span data-stu-id="3683b-162">**Optional**</span></span>

<span data-ttu-id="3683b-163">Permet de spécifier une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3683b-163">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="3683b-164">Consultez la rubrique [Localization](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="3683b-164">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="3683b-165">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-165">Name</span></span>| <span data-ttu-id="3683b-166">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-166">Maximum size</span></span> | <span data-ttu-id="3683b-167">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-167">Required</span></span> | <span data-ttu-id="3683b-168">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-168">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`|<span data-ttu-id="3683b-169">4 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-169">4 characters</span></span>|<span data-ttu-id="3683b-170">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-170">✔</span></span>|<span data-ttu-id="3683b-171">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="3683b-171">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="3683b-172">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="3683b-172">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="3683b-173">Tableau d’objets spécifiant des traductions de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3683b-173">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="3683b-174">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-174">Name</span></span>| <span data-ttu-id="3683b-175">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-175">Maximum size</span></span> | <span data-ttu-id="3683b-176">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-176">Required</span></span> | <span data-ttu-id="3683b-177">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-177">Description</span></span>|
|---|---|---|---|
|`languageTag`|<span data-ttu-id="3683b-178">4 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-178">4 characters</span></span>|<span data-ttu-id="3683b-179">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-179">✔</span></span>|<span data-ttu-id="3683b-180">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="3683b-180">The language tag of the strings in the provided file.</span></span>|
|`file`|<span data-ttu-id="3683b-181">4 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-181">4 characters</span></span>|<span data-ttu-id="3683b-182">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-182">✔</span></span>|<span data-ttu-id="3683b-183">Chemin d’accès relatif à un fichier. JSON contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="3683b-183">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="3683b-184">nom</span><span class="sxs-lookup"><span data-stu-id="3683b-184">name</span></span>

<span data-ttu-id="3683b-185">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="3683b-185">**Required**</span></span>

<span data-ttu-id="3683b-186">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’expérience de teams.</span><span class="sxs-lookup"><span data-stu-id="3683b-186">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="3683b-187">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="3683b-187">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="3683b-188">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="3683b-188">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="3683b-189">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-189">Name</span></span>| <span data-ttu-id="3683b-190">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-190">Maximum size</span></span> | <span data-ttu-id="3683b-191">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-191">Required</span></span> | <span data-ttu-id="3683b-192">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-192">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="3683b-193">30 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-193">30 characters</span></span>|<span data-ttu-id="3683b-194">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-194">✔</span></span>|<span data-ttu-id="3683b-195">Nom complet court de l’application.</span><span class="sxs-lookup"><span data-stu-id="3683b-195">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="3683b-196">100 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-196">100 characters</span></span>||<span data-ttu-id="3683b-197">Nom complet de l’application, utilisé si le nom complet de l’application dépasse les 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="3683b-197">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="3683b-198">description</span><span class="sxs-lookup"><span data-stu-id="3683b-198">description</span></span>

<span data-ttu-id="3683b-199">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="3683b-199">**Required**</span></span>

<span data-ttu-id="3683b-200">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3683b-200">Describes your app to users.</span></span> <span data-ttu-id="3683b-201">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="3683b-201">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="3683b-202">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="3683b-202">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="3683b-203">Vous devez également noter, dans la description complète, si un compte externe est requis pour l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3683b-203">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="3683b-204">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="3683b-204">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="3683b-205">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="3683b-205">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="3683b-206">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-206">Name</span></span>| <span data-ttu-id="3683b-207">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-207">Maximum size</span></span> | <span data-ttu-id="3683b-208">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-208">Required</span></span> | <span data-ttu-id="3683b-209">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-209">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="3683b-210">80 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-210">80 characters</span></span>|<span data-ttu-id="3683b-211">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-211">✔</span></span>|<span data-ttu-id="3683b-212">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="3683b-212">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="3683b-213">4000 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-213">4000 characters</span></span>|<span data-ttu-id="3683b-214">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-214">✔</span></span>|<span data-ttu-id="3683b-215">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="3683b-215">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="3683b-216">icons</span><span class="sxs-lookup"><span data-stu-id="3683b-216">icons</span></span>

<span data-ttu-id="3683b-217">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="3683b-217">**Required**</span></span>

<span data-ttu-id="3683b-218">Icônes utilisées dans l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="3683b-218">Icons used within the Teams app.</span></span> <span data-ttu-id="3683b-219">Les fichiers d’icône doivent être inclus dans le package de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="3683b-219">The icon files must be included as part of the upload package.</span></span>

|<span data-ttu-id="3683b-220">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-220">Name</span></span>| <span data-ttu-id="3683b-221">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-221">Maximum size</span></span> | <span data-ttu-id="3683b-222">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-222">Required</span></span> | <span data-ttu-id="3683b-223">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-223">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="3683b-224">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-224">2048 characters</span></span>|<span data-ttu-id="3683b-225">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-225">✔</span></span>|<span data-ttu-id="3683b-226">Chemin d’accès relatif à une icône de contour PNG 32x32 transparent.</span><span class="sxs-lookup"><span data-stu-id="3683b-226">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="3683b-227">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-227">2048 characters</span></span>|<span data-ttu-id="3683b-228">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-228">✔</span></span>|<span data-ttu-id="3683b-229">Chemin d’accès relatif à une icône PNG 192x192 couleur complète.</span><span class="sxs-lookup"><span data-stu-id="3683b-229">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="3683b-230">accentColor</span><span class="sxs-lookup"><span data-stu-id="3683b-230">accentColor</span></span>

<span data-ttu-id="3683b-231">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="3683b-231">**Required** &ndash; String</span></span>

<span data-ttu-id="3683b-232">Couleur à utiliser en combinaison avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="3683b-232">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="3683b-233">La valeur doit être un code de couleur HTML valide commençant par « # », par `#4464ee`exemple.</span><span class="sxs-lookup"><span data-stu-id="3683b-233">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="3683b-234">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="3683b-234">configurableTabs</span></span>

<span data-ttu-id="3683b-235">**Optional**</span><span class="sxs-lookup"><span data-stu-id="3683b-235">**Optional**</span></span>

<span data-ttu-id="3683b-236">Utilisé lorsque l’expérience de votre application dispose d’un onglet Channel Team qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="3683b-236">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="3683b-237">Les onglets configurables sont pris en charge uniquement dans l’étendue teams et un seul onglet par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3683b-237">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="3683b-238">L’objet est un tableau contenant tous les éléments du type `object`.</span><span class="sxs-lookup"><span data-stu-id="3683b-238">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="3683b-239">Ce bloc est requis uniquement pour les solutions qui fournissent une solution de sous-onglet canal configurable.</span><span class="sxs-lookup"><span data-stu-id="3683b-239">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="3683b-240">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-240">Name</span></span>| <span data-ttu-id="3683b-241">Type</span><span class="sxs-lookup"><span data-stu-id="3683b-241">Type</span></span>| <span data-ttu-id="3683b-242">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-242">Maximum size</span></span> | <span data-ttu-id="3683b-243">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-243">Required</span></span> | <span data-ttu-id="3683b-244">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-244">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="3683b-245">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-245">String</span></span>|<span data-ttu-id="3683b-246">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-246">2048 characters</span></span>|<span data-ttu-id="3683b-247">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-247">✔</span></span>|<span data-ttu-id="3683b-248">URL https://à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="3683b-248">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="3683b-249">Boolean</span><span class="sxs-lookup"><span data-stu-id="3683b-249">Boolean</span></span>|||<span data-ttu-id="3683b-250">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="3683b-250">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="3683b-251">Default`true`</span><span class="sxs-lookup"><span data-stu-id="3683b-251">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="3683b-252">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="3683b-252">Array of enum</span></span>|<span data-ttu-id="3683b-253">1 </span><span class="sxs-lookup"><span data-stu-id="3683b-253">1</span></span>|<span data-ttu-id="3683b-254">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-254">✔</span></span>|<span data-ttu-id="3683b-255">Actuellement, les onglets configurables prennent `team` en `groupchat` charge uniquement les étendues et.</span><span class="sxs-lookup"><span data-stu-id="3683b-255">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="3683b-256">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-256">String</span></span>|<span data-ttu-id="3683b-257">2048</span><span class="sxs-lookup"><span data-stu-id="3683b-257">2048</span></span>||<span data-ttu-id="3683b-258">Chemin d’accès relatif à une image d’aperçu de tabulation à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3683b-258">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="3683b-259">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="3683b-259">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="3683b-260">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="3683b-260">Array of enum</span></span>|<span data-ttu-id="3683b-261">1 </span><span class="sxs-lookup"><span data-stu-id="3683b-261">1</span></span>||<span data-ttu-id="3683b-262">Définit la manière dont votre onglet sera disponible dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3683b-262">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="3683b-263">Les options `sharePointFullPage` sont et`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="3683b-263">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="3683b-264">staticTabs</span><span class="sxs-lookup"><span data-stu-id="3683b-264">staticTabs</span></span>

<span data-ttu-id="3683b-265">**Optional**</span><span class="sxs-lookup"><span data-stu-id="3683b-265">**Optional**</span></span>

<span data-ttu-id="3683b-266">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur ne les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="3683b-266">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="3683b-267">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="3683b-267">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="3683b-268">Les onglets statiques `team` déclarés dans l’étendue ne sont pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="3683b-268">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="3683b-269">L’objet est un tableau (au maximum 16 éléments) avec tous les éléments du type `object`.</span><span class="sxs-lookup"><span data-stu-id="3683b-269">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="3683b-270">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="3683b-270">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="3683b-271">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-271">Name</span></span>| <span data-ttu-id="3683b-272">Type</span><span class="sxs-lookup"><span data-stu-id="3683b-272">Type</span></span>| <span data-ttu-id="3683b-273">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-273">Maximum size</span></span> | <span data-ttu-id="3683b-274">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-274">Required</span></span> | <span data-ttu-id="3683b-275">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-275">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="3683b-276">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-276">String</span></span>|<span data-ttu-id="3683b-277">64 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-277">64 characters</span></span>|<span data-ttu-id="3683b-278">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-278">✔</span></span>|<span data-ttu-id="3683b-279">Identificateur unique de l’entité que l’onglet affiche.</span><span class="sxs-lookup"><span data-stu-id="3683b-279">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="3683b-280">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-280">String</span></span>|<span data-ttu-id="3683b-281">128 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-281">128 characters</span></span>|<span data-ttu-id="3683b-282">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-282">✔</span></span>|<span data-ttu-id="3683b-283">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="3683b-283">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="3683b-284">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-284">String</span></span>|<span data-ttu-id="3683b-285">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-285">2048 characters</span></span>|<span data-ttu-id="3683b-286">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-286">✔</span></span>|<span data-ttu-id="3683b-287">URL https://qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de dessin de teams.</span><span class="sxs-lookup"><span data-stu-id="3683b-287">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="3683b-288">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-288">String</span></span>|<span data-ttu-id="3683b-289">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-289">2048 characters</span></span>||<span data-ttu-id="3683b-290">URL https://vers laquelle pointer si un utilisateur choisit de l’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="3683b-290">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="3683b-291">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="3683b-291">Array of enum</span></span>|<span data-ttu-id="3683b-292">1 </span><span class="sxs-lookup"><span data-stu-id="3683b-292">1</span></span>|<span data-ttu-id="3683b-293">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-293">✔</span></span>|<span data-ttu-id="3683b-294">Actuellement, les onglets statiques `personal` prennent en charge uniquement l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="3683b-294">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="3683b-295">bots</span><span class="sxs-lookup"><span data-stu-id="3683b-295">bots</span></span>

<span data-ttu-id="3683b-296">**Optional**</span><span class="sxs-lookup"><span data-stu-id="3683b-296">**Optional**</span></span>

<span data-ttu-id="3683b-297">Définit une solution de robot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="3683b-297">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="3683b-298">L’objet est un tableau (maximum d’un seul élément&mdash;, actuellement un seul bot est autorisé par application) à tous les éléments du `object`type.</span><span class="sxs-lookup"><span data-stu-id="3683b-298">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="3683b-299">Ce bloc est requis uniquement pour les solutions qui fournissent une expérience de robot.</span><span class="sxs-lookup"><span data-stu-id="3683b-299">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="3683b-300">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-300">Name</span></span>| <span data-ttu-id="3683b-301">Type</span><span class="sxs-lookup"><span data-stu-id="3683b-301">Type</span></span>| <span data-ttu-id="3683b-302">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-302">Maximum size</span></span> | <span data-ttu-id="3683b-303">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-303">Required</span></span> | <span data-ttu-id="3683b-304">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-304">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="3683b-305">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-305">String</span></span>|<span data-ttu-id="3683b-306">64 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-306">64 characters</span></span>|<span data-ttu-id="3683b-307">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-307">✔</span></span>|<span data-ttu-id="3683b-308">ID d’application Microsoft unique pour le bot enregistré avec l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="3683b-308">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="3683b-309">Il peut s’agir de la même chose que l' [ID d’application](#id)global.</span><span class="sxs-lookup"><span data-stu-id="3683b-309">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="3683b-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="3683b-310">Boolean</span></span>|||<span data-ttu-id="3683b-311">Indique si le bot utilise un Conseil de l’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="3683b-311">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="3683b-312">Default`false`</span><span class="sxs-lookup"><span data-stu-id="3683b-312">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="3683b-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="3683b-313">Boolean</span></span>|||<span data-ttu-id="3683b-314">Indique si un bot est un robot à sens unique, par opposition à un bot de conversation.</span><span class="sxs-lookup"><span data-stu-id="3683b-314">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="3683b-315">Default`false`</span><span class="sxs-lookup"><span data-stu-id="3683b-315">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="3683b-316">Boolean</span><span class="sxs-lookup"><span data-stu-id="3683b-316">Boolean</span></span>|||<span data-ttu-id="3683b-317">Indique si le bot prend en charge la possibilité de télécharger ou de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="3683b-317">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="3683b-318">Default`false`</span><span class="sxs-lookup"><span data-stu-id="3683b-318">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="3683b-319">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="3683b-319">Array of enum</span></span>|<span data-ttu-id="3683b-320">3 </span><span class="sxs-lookup"><span data-stu-id="3683b-320">3</span></span>|<span data-ttu-id="3683b-321">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-321">✔</span></span>|<span data-ttu-id="3683b-322">Indique si le bot offre une expérience dans le contexte d’un canal dans un `team`, dans une conversation de groupe`groupchat`() ou dans une expérience étendue à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="3683b-322">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="3683b-323">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="3683b-323">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="3683b-324">bots. commandLists</span><span class="sxs-lookup"><span data-stu-id="3683b-324">bots.commandLists</span></span>

<span data-ttu-id="3683b-325">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3683b-325">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="3683b-326">L’objet est un tableau (nombre maximal de 2 éléments) avec tous les éléments `object`de type ; vous devez définir une liste de commandes distincte pour chaque étendue prise en charge par votre bot.</span><span class="sxs-lookup"><span data-stu-id="3683b-326">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="3683b-327">Pour plus d’informations, voir [menus de bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="3683b-327">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="3683b-328">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-328">Name</span></span>| <span data-ttu-id="3683b-329">Type</span><span class="sxs-lookup"><span data-stu-id="3683b-329">Type</span></span>| <span data-ttu-id="3683b-330">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-330">Maximum size</span></span> | <span data-ttu-id="3683b-331">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-331">Required</span></span> | <span data-ttu-id="3683b-332">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-332">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="3683b-333">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="3683b-333">array of enum</span></span>|<span data-ttu-id="3683b-334">3 </span><span class="sxs-lookup"><span data-stu-id="3683b-334">3</span></span>|<span data-ttu-id="3683b-335">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-335">✔</span></span>|<span data-ttu-id="3683b-336">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="3683b-336">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="3683b-337">Les options `team`sont `personal`, et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="3683b-337">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="3683b-338">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="3683b-338">array of objects</span></span>|<span data-ttu-id="3683b-339">10 </span><span class="sxs-lookup"><span data-stu-id="3683b-339">10</span></span>|<span data-ttu-id="3683b-340">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-340">✔</span></span>|<span data-ttu-id="3683b-341">Tableau de commandes pris en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="3683b-341">An array of commands the bot supports:</span></span><br><span data-ttu-id="3683b-342">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="3683b-342">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="3683b-343">`description`: description simple ou exemple de la syntaxe de commande et de son argument (String, 128)</span><span class="sxs-lookup"><span data-stu-id="3683b-343">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="3683b-344">ceux</span><span class="sxs-lookup"><span data-stu-id="3683b-344">connectors</span></span>

<span data-ttu-id="3683b-345">**Optional**</span><span class="sxs-lookup"><span data-stu-id="3683b-345">**Optional**</span></span>

<span data-ttu-id="3683b-346">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="3683b-346">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="3683b-347">L’objet est un tableau (un maximum de 1 élément) avec tous les éléments `object`de type.</span><span class="sxs-lookup"><span data-stu-id="3683b-347">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="3683b-348">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="3683b-348">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="3683b-349">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-349">Name</span></span>| <span data-ttu-id="3683b-350">Type</span><span class="sxs-lookup"><span data-stu-id="3683b-350">Type</span></span>| <span data-ttu-id="3683b-351">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-351">Maximum size</span></span> | <span data-ttu-id="3683b-352">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-352">Required</span></span> | <span data-ttu-id="3683b-353">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-353">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="3683b-354">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-354">String</span></span>|<span data-ttu-id="3683b-355">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-355">2048 characters</span></span>|<span data-ttu-id="3683b-356">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-356">✔</span></span>|<span data-ttu-id="3683b-357">URL https://à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="3683b-357">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="3683b-358">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-358">String</span></span>|<span data-ttu-id="3683b-359">64 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-359">64 characters</span></span>|<span data-ttu-id="3683b-360">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-360">✔</span></span>|<span data-ttu-id="3683b-361">Identificateur unique du connecteur correspondant à son ID dans le [tableau de bord du développeur de connecteurs](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="3683b-361">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="3683b-362">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="3683b-362">Array of enum</span></span>|<span data-ttu-id="3683b-363">1 </span><span class="sxs-lookup"><span data-stu-id="3683b-363">1</span></span>|<span data-ttu-id="3683b-364">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-364">✔</span></span>|<span data-ttu-id="3683b-365">Indique si le connecteur offre une expérience dans le contexte d’un canal dans un `team`, ou une expérience étendue à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="3683b-365">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="3683b-366">Actuellement, seule l' `team` étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="3683b-366">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="3683b-367">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="3683b-367">composeExtensions</span></span>

<span data-ttu-id="3683b-368">**Optional**</span><span class="sxs-lookup"><span data-stu-id="3683b-368">**Optional**</span></span>

<span data-ttu-id="3683b-369">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="3683b-369">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="3683b-370">Le nom de la fonctionnalité a été modifié de « extension de composition » en « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même afin que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="3683b-370">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="3683b-371">L’objet est un tableau (un maximum de 1 élément) avec tous les éléments `object`de type.</span><span class="sxs-lookup"><span data-stu-id="3683b-371">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="3683b-372">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="3683b-372">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="3683b-373">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-373">Name</span></span>| <span data-ttu-id="3683b-374">Type</span><span class="sxs-lookup"><span data-stu-id="3683b-374">Type</span></span> | <span data-ttu-id="3683b-375">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-375">Maximum Size</span></span> | <span data-ttu-id="3683b-376">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-376">Required</span></span> | <span data-ttu-id="3683b-377">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-377">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="3683b-378">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-378">String</span></span>|<span data-ttu-id="3683b-379">64</span><span class="sxs-lookup"><span data-stu-id="3683b-379">64</span></span>|<span data-ttu-id="3683b-380">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-380">✔</span></span>|<span data-ttu-id="3683b-381">ID d’application Microsoft unique pour le bot qui sauvegarde l’extension de messagerie, tel qu’inscrit auprès de l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="3683b-381">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="3683b-382">Il peut s’agir de la même chose que l' [ID d’application](#id)global.</span><span class="sxs-lookup"><span data-stu-id="3683b-382">This may well be the same as the overall [app ID](#id).</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="3683b-383">Boolean</span><span class="sxs-lookup"><span data-stu-id="3683b-383">Boolean</span></span>|||<span data-ttu-id="3683b-384">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3683b-384">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="3683b-385">La valeur par `false`défaut est.</span><span class="sxs-lookup"><span data-stu-id="3683b-385">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="3683b-386">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="3683b-386">Array of object</span></span>|<span data-ttu-id="3683b-387">10 </span><span class="sxs-lookup"><span data-stu-id="3683b-387">10</span></span>|<span data-ttu-id="3683b-388">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-388">✔</span></span>|<span data-ttu-id="3683b-389">Tableau de commandes prises en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="3683b-389">Array of commands the messaging extension supports</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="3683b-390">composeExtensions. Commands</span><span class="sxs-lookup"><span data-stu-id="3683b-390">composeExtensions.commands</span></span>

<span data-ttu-id="3683b-391">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="3683b-391">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="3683b-392">Chaque commande apparaît dans Microsoft teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3683b-392">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="3683b-393">Il y a un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="3683b-393">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="3683b-394">Chaque élément de commande est un objet de la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="3683b-394">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="3683b-395">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-395">Name</span></span>| <span data-ttu-id="3683b-396">Type</span><span class="sxs-lookup"><span data-stu-id="3683b-396">Type</span></span>| <span data-ttu-id="3683b-397">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-397">Maximum size</span></span> | <span data-ttu-id="3683b-398">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-398">Required</span></span> | <span data-ttu-id="3683b-399">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-399">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="3683b-400">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-400">String</span></span>|<span data-ttu-id="3683b-401">64 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-401">64 characters</span></span>|<span data-ttu-id="3683b-402">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-402">✔</span></span>|<span data-ttu-id="3683b-403">ID de la commande</span><span class="sxs-lookup"><span data-stu-id="3683b-403">The ID for the command</span></span>|
|`type`|<span data-ttu-id="3683b-404">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-404">String</span></span>|<span data-ttu-id="3683b-405">64 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-405">64 characters</span></span>||<span data-ttu-id="3683b-406">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="3683b-406">Type of the command.</span></span> <span data-ttu-id="3683b-407">L’une `query` ou `action`l’autre.</span><span class="sxs-lookup"><span data-stu-id="3683b-407">One of `query` or `action`.</span></span> <span data-ttu-id="3683b-408">Default`query`</span><span class="sxs-lookup"><span data-stu-id="3683b-408">Default: `query`</span></span>|
|`title`|<span data-ttu-id="3683b-409">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-409">String</span></span>|<span data-ttu-id="3683b-410">32 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-410">32 characters</span></span>|<span data-ttu-id="3683b-411">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-411">✔</span></span>|<span data-ttu-id="3683b-412">Nom de commande convivial</span><span class="sxs-lookup"><span data-stu-id="3683b-412">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="3683b-413">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-413">String</span></span>|<span data-ttu-id="3683b-414">128 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-414">128 characters</span></span>||<span data-ttu-id="3683b-415">La description qui s’affiche pour les utilisateurs afin d’indiquer la finalité de cette commande.</span><span class="sxs-lookup"><span data-stu-id="3683b-415">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="3683b-416">Boolean</span><span class="sxs-lookup"><span data-stu-id="3683b-416">Boolean</span></span>|||<span data-ttu-id="3683b-417">Valeur booléenne indiquant si la commande doit être exécutée initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="3683b-417">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="3683b-418">Default`false`</span><span class="sxs-lookup"><span data-stu-id="3683b-418">Default: `false`</span></span>|
|`context`|<span data-ttu-id="3683b-419">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="3683b-419">Array of Strings</span></span>|<span data-ttu-id="3683b-420">3 </span><span class="sxs-lookup"><span data-stu-id="3683b-420">3</span></span>||<span data-ttu-id="3683b-421">Définit l’emplacement à partir duquel l’extension de message peut être appelée.</span><span class="sxs-lookup"><span data-stu-id="3683b-421">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="3683b-422">Toute combinaison de `compose`, `commandBox`, `message`.</span><span class="sxs-lookup"><span data-stu-id="3683b-422">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="3683b-423">Valeur par défaut est`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="3683b-423">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="3683b-424">Boolean</span><span class="sxs-lookup"><span data-stu-id="3683b-424">Boolean</span></span>|||<span data-ttu-id="3683b-425">Une valeur booléenne qui indique s’il doit extraire le module de tâches de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="3683b-425">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="3683b-426">Objet</span><span class="sxs-lookup"><span data-stu-id="3683b-426">Object</span></span>|||<span data-ttu-id="3683b-427">Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="3683b-427">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="3683b-428">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-428">String</span></span>|<span data-ttu-id="3683b-429">64</span><span class="sxs-lookup"><span data-stu-id="3683b-429">64</span></span>||<span data-ttu-id="3683b-430">Titre de la boîte de dialogue initiale</span><span class="sxs-lookup"><span data-stu-id="3683b-430">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="3683b-431">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-431">String</span></span>|||<span data-ttu-id="3683b-432">Largeur de la boîte de dialogue-soit un nombre en pixels, soit une mise en page par défaut telle que « grande », « moyen » ou « petite »</span><span class="sxs-lookup"><span data-stu-id="3683b-432">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="3683b-433">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-433">String</span></span>|||<span data-ttu-id="3683b-434">Hauteur de la boîte de dialogue : nombre en pixels ou mise en page par défaut, par exemple, « grande », « moyen » ou « petite »</span><span class="sxs-lookup"><span data-stu-id="3683b-434">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="3683b-435">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-435">String</span></span>|||<span data-ttu-id="3683b-436">URL d’affichage WebView initiale</span><span class="sxs-lookup"><span data-stu-id="3683b-436">Initial webview URL</span></span>|
|`messageHandlers`|<span data-ttu-id="3683b-437">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="3683b-437">Array of Objects</span></span>|<span data-ttu-id="3683b-438">5 </span><span class="sxs-lookup"><span data-stu-id="3683b-438">5</span></span>||<span data-ttu-id="3683b-439">Liste de gestionnaires permettant d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="3683b-439">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="3683b-440">Les domaines doivent également être affichés dans`validDomains`</span><span class="sxs-lookup"><span data-stu-id="3683b-440">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="3683b-441">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-441">String</span></span>|||<span data-ttu-id="3683b-442">Type de gestionnaire de messages.</span><span class="sxs-lookup"><span data-stu-id="3683b-442">The type of message handler.</span></span> <span data-ttu-id="3683b-443">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="3683b-443">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="3683b-444">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="3683b-444">Array of Strings</span></span>|||<span data-ttu-id="3683b-445">Tableau de domaines pour lesquels le gestionnaire de messages de liaison peut s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="3683b-445">Array of domains that the link message handler can register for.</span></span>|
|`parameters`|<span data-ttu-id="3683b-446">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="3683b-446">Array of object</span></span>|<span data-ttu-id="3683b-447">5 </span><span class="sxs-lookup"><span data-stu-id="3683b-447">5</span></span>|<span data-ttu-id="3683b-448">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-448">✔</span></span>|<span data-ttu-id="3683b-449">La liste des paramètres que la commande prend.</span><span class="sxs-lookup"><span data-stu-id="3683b-449">The list of parameters the command takes.</span></span> <span data-ttu-id="3683b-450">Minimum : 1 ; maximum : 5</span><span class="sxs-lookup"><span data-stu-id="3683b-450">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="3683b-451">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-451">String</span></span>|<span data-ttu-id="3683b-452">64 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-452">64 characters</span></span>|<span data-ttu-id="3683b-453">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-453">✔</span></span>|<span data-ttu-id="3683b-454">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="3683b-454">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="3683b-455">Elle est incluse dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3683b-455">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="3683b-456">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-456">String</span></span>|<span data-ttu-id="3683b-457">32 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-457">32 characters</span></span>|<span data-ttu-id="3683b-458">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-458">✔</span></span>|<span data-ttu-id="3683b-459">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="3683b-459">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="3683b-460">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-460">String</span></span>|<span data-ttu-id="3683b-461">128 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-461">128 characters</span></span>||<span data-ttu-id="3683b-462">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="3683b-462">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="3683b-463">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-463">String</span></span>|<span data-ttu-id="3683b-464">128 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-464">128 characters</span></span>||<span data-ttu-id="3683b-465">Définit le type de contrôle affiché sur un module de tâche `fetchTask: true`pour.</span><span class="sxs-lookup"><span data-stu-id="3683b-465">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="3683b-466">`text` `textarea` `number`, `date`,, `time` `toggle``choiceset`</span><span class="sxs-lookup"><span data-stu-id="3683b-466">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="3683b-467">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="3683b-467">Array of Objects</span></span>|<span data-ttu-id="3683b-468">10 </span><span class="sxs-lookup"><span data-stu-id="3683b-468">10</span></span>||<span data-ttu-id="3683b-469">Options de choix pour le `choiceset`.</span><span class="sxs-lookup"><span data-stu-id="3683b-469">The choice options for the `choiceset`.</span></span> <span data-ttu-id="3683b-470">À utiliser uniquement `parameter.inputType` lorsque est`choiceset`</span><span class="sxs-lookup"><span data-stu-id="3683b-470">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="3683b-471">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-471">String</span></span>|<span data-ttu-id="3683b-472">128</span><span class="sxs-lookup"><span data-stu-id="3683b-472">128</span></span>||<span data-ttu-id="3683b-473">Titre du choix</span><span class="sxs-lookup"><span data-stu-id="3683b-473">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="3683b-474">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-474">String</span></span>|<span data-ttu-id="3683b-475">512</span><span class="sxs-lookup"><span data-stu-id="3683b-475">512</span></span>||<span data-ttu-id="3683b-476">Valeur du choix</span><span class="sxs-lookup"><span data-stu-id="3683b-476">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="3683b-477">autorisations</span><span class="sxs-lookup"><span data-stu-id="3683b-477">permissions</span></span>

<span data-ttu-id="3683b-478">**Optional**</span><span class="sxs-lookup"><span data-stu-id="3683b-478">**Optional**</span></span>

<span data-ttu-id="3683b-479">Un tableau `string` qui spécifie les autorisations demandées par l’application, ce qui permet aux utilisateurs finaux de savoir comment effectuer l’extension.</span><span class="sxs-lookup"><span data-stu-id="3683b-479">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="3683b-480">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="3683b-480">The following options are non-exclusive:</span></span>

* <span data-ttu-id="3683b-481">`identity`&emsp; Nécessite des informations d’identité d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="3683b-481">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="3683b-482">`messageTeamMembers`&emsp; Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="3683b-482">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="3683b-483">Si vous modifiez ces autorisations lors de la mise à jour de votre application, vos utilisateurs répéteront le processus de consentement la première fois qu’ils exécuteront l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="3683b-483">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="3683b-484">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="3683b-484">devicePermissions</span></span>

<span data-ttu-id="3683b-485">**Facultatif** Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="3683b-485">**Optional** Array of Strings</span></span>

<span data-ttu-id="3683b-486">Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur auquel votre application peut demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="3683b-486">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="3683b-487">Les options sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3683b-487">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="3683b-488">validDomains</span><span class="sxs-lookup"><span data-stu-id="3683b-488">validDomains</span></span>

<span data-ttu-id="3683b-489">**Facultatif** **, sauf indication contraire**</span><span class="sxs-lookup"><span data-stu-id="3683b-489">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="3683b-490">Une liste des domaines valides à partir desquels l’application prévoit de charger tout contenu.</span><span class="sxs-lookup"><span data-stu-id="3683b-490">A list of valid domains from which the app expects to load any content.</span></span> <span data-ttu-id="3683b-491">Les listes de domaine peuvent inclure des caractères génériques `*.example.com`, par exemple.</span><span class="sxs-lookup"><span data-stu-id="3683b-491">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="3683b-492">Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com`.</span><span class="sxs-lookup"><span data-stu-id="3683b-492">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="3683b-493">Si la configuration de votre onglet ou de votre interface utilisateur de contenu doit accéder à un autre domaine en plus de celui utilisé pour la configuration d’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="3683b-493">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="3683b-494">Toutefois, il n’est **pas** nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3683b-494">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="3683b-495">Par exemple, pour authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne `validDomains[]`devez pas inclure Accounts.google.com dans.</span><span class="sxs-lookup"><span data-stu-id="3683b-495">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3683b-496">N’ajoutez pas de domaines qui se trouvent en dehors de votre contrôle, soit directement, soit via des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="3683b-496">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="3683b-497">Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="3683b-497">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="3683b-498">L’objet est un tableau contenant tous les éléments du type `string`.</span><span class="sxs-lookup"><span data-stu-id="3683b-498">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="3683b-499">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="3683b-499">webApplicationInfo</span></span>

<span data-ttu-id="3683b-500">**Optional**</span><span class="sxs-lookup"><span data-stu-id="3683b-500">**Optional**</span></span>

<span data-ttu-id="3683b-501">Spécifiez l’ID de votre application AAD et les informations graphiques pour aider les utilisateurs à se connecter à votre application AAD de manière transparente.</span><span class="sxs-lookup"><span data-stu-id="3683b-501">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="3683b-502">Nom</span><span class="sxs-lookup"><span data-stu-id="3683b-502">Name</span></span>| <span data-ttu-id="3683b-503">Type</span><span class="sxs-lookup"><span data-stu-id="3683b-503">Type</span></span>| <span data-ttu-id="3683b-504">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="3683b-504">Maximum size</span></span> | <span data-ttu-id="3683b-505">Requis</span><span class="sxs-lookup"><span data-stu-id="3683b-505">Required</span></span> | <span data-ttu-id="3683b-506">Description</span><span class="sxs-lookup"><span data-stu-id="3683b-506">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="3683b-507">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-507">String</span></span>|<span data-ttu-id="3683b-508">36 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-508">36 characters</span></span>|<span data-ttu-id="3683b-509">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-509">✔</span></span>|<span data-ttu-id="3683b-510">ID de l’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="3683b-510">AAD application id of the app.</span></span> <span data-ttu-id="3683b-511">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="3683b-511">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="3683b-512">Chaîne</span><span class="sxs-lookup"><span data-stu-id="3683b-512">String</span></span>|<span data-ttu-id="3683b-513">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="3683b-513">2048 characters</span></span>|<span data-ttu-id="3683b-514">✔</span><span class="sxs-lookup"><span data-stu-id="3683b-514">✔</span></span>|<span data-ttu-id="3683b-515">URL de ressource de l’application pour l’acquisition du jeton d’authentification pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="3683b-515">Resource url of app for acquiring auth token for SSO.</span></span>|