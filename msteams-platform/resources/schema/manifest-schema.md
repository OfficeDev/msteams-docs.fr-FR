---
title: Référence du schéma de manifeste
description: Décrit le schéma pris en charge par le manifeste pour Microsoft teams
keywords: schéma de manifeste teams
ms.openlocfilehash: d4a2864c18a5066673bafab42a46733a0ab5f116
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673814"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="07371-104">Référence : schéma de manifeste pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="07371-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="07371-105">Le manifeste Microsoft teams décrit la façon dont l’application s’intègre dans le produit Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="07371-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="07371-106">Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span><span class="sxs-lookup"><span data-stu-id="07371-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="07371-107">Les versions précédentes 1.0 à 1.4 sont également prises en charge (à l’aide de « v1. x » dans l’URL).</span><span class="sxs-lookup"><span data-stu-id="07371-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="07371-108">L’exemple de schéma suivant montre toutes les options d’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="07371-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="07371-109">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="07371-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
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
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
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
        }
      ],
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
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
     "contoso.com",
     "mysite.someplace.com",
     "othersite.someplace.com"
  ]
}
```

<span data-ttu-id="07371-110">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="07371-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="07371-111">$schema</span><span class="sxs-lookup"><span data-stu-id="07371-111">$schema</span></span>

<span data-ttu-id="07371-112">*Facultatif, mais chaîne recommandée* &ndash;</span><span class="sxs-lookup"><span data-stu-id="07371-112">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="07371-113">URL https://référençant le schéma JSON du manifeste.</span><span class="sxs-lookup"><span data-stu-id="07371-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="07371-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="07371-114">manifestVersion</span></span>

<span data-ttu-id="07371-115">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="07371-115">**Required** &ndash; String</span></span>

<span data-ttu-id="07371-116">Version du schéma de manifeste utilisé par ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="07371-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="07371-117">Il doit être « 1,5 ».</span><span class="sxs-lookup"><span data-stu-id="07371-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="07371-118">version</span><span class="sxs-lookup"><span data-stu-id="07371-118">version</span></span>

<span data-ttu-id="07371-119">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="07371-119">**Required** &ndash; String</span></span>

<span data-ttu-id="07371-120">Version de l’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="07371-120">The version of the specific app.</span></span> <span data-ttu-id="07371-121">Si vous mettez à jour un événement dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="07371-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="07371-122">Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="07371-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="07371-123">Si cette application a été envoyée au magasin, le nouveau manifeste doit être soumis à nouveau et revalidé.</span><span class="sxs-lookup"><span data-stu-id="07371-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="07371-124">Ensuite, les utilisateurs de cette application obtiendront automatiquement le nouveau manifeste mis à jour en quelques heures, une fois celui-ci approuvé.</span><span class="sxs-lookup"><span data-stu-id="07371-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="07371-125">Si l’application a demandé une modification des autorisations, les utilisateurs sont invités à effectuer une mise à niveau et à reconfigurer l’application.</span><span class="sxs-lookup"><span data-stu-id="07371-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="07371-126">Cette chaîne de version doit suivre la norme [semver](http://semver.org/) (major. Petites. CORRECTIF).</span><span class="sxs-lookup"><span data-stu-id="07371-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="07371-127">id</span><span class="sxs-lookup"><span data-stu-id="07371-127">id</span></span>

<span data-ttu-id="07371-128">ID d’application Microsoft **requis** &ndash;</span><span class="sxs-lookup"><span data-stu-id="07371-128">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="07371-129">Identificateur unique généré par Microsoft pour cette application.</span><span class="sxs-lookup"><span data-stu-id="07371-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="07371-130">Si vous avez inscrit un robot via Microsoft bot Framework ou si l’application Web de votre onglet se connecte déjà à Microsoft, vous devez déjà avoir un ID et l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="07371-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="07371-131">Dans le cas contraire, vous devez générer un nouvel ID dans le portail d’inscription des applications Microsoft ([mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous ajoutez un bot. Remarque : Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="07371-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="packagename"></a><span data-ttu-id="07371-132">packageName</span><span class="sxs-lookup"><span data-stu-id="07371-132">packageName</span></span>

<span data-ttu-id="07371-133">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="07371-133">**Required** &ndash; String</span></span>

<span data-ttu-id="07371-134">Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="07371-134">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="07371-135">developer</span><span class="sxs-lookup"><span data-stu-id="07371-135">developer</span></span>

<span data-ttu-id="07371-136">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="07371-136">**Required**</span></span>

<span data-ttu-id="07371-137">Spécifie les informations relatives à votre société.</span><span class="sxs-lookup"><span data-stu-id="07371-137">Specifies information about your company.</span></span> <span data-ttu-id="07371-138">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="07371-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="07371-139">Pour plus d’informations, consultez nos [instructions de publication](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) .</span><span class="sxs-lookup"><span data-stu-id="07371-139">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="07371-140">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-140">Name</span></span>| <span data-ttu-id="07371-141">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-141">Maximum size</span></span> | <span data-ttu-id="07371-142">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-142">Required</span></span> | <span data-ttu-id="07371-143">Description</span><span class="sxs-lookup"><span data-stu-id="07371-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="07371-144">32 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-144">32 characters</span></span>|<span data-ttu-id="07371-145">✔</span><span class="sxs-lookup"><span data-stu-id="07371-145">✔</span></span>|<span data-ttu-id="07371-146">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="07371-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="07371-147">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-147">2048 characters</span></span>|<span data-ttu-id="07371-148">✔</span><span class="sxs-lookup"><span data-stu-id="07371-148">✔</span></span>|<span data-ttu-id="07371-149">URL https://vers le site Web du développeur.</span><span class="sxs-lookup"><span data-stu-id="07371-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="07371-150">Ce lien doit prendre les utilisateurs à la page d’accueil de votre entreprise ou de votre propre produit.</span><span class="sxs-lookup"><span data-stu-id="07371-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="07371-151">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-151">2048 characters</span></span>|<span data-ttu-id="07371-152">✔</span><span class="sxs-lookup"><span data-stu-id="07371-152">✔</span></span>|<span data-ttu-id="07371-153">URL https://vers la stratégie de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="07371-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="07371-154">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-154">2048 characters</span></span>|<span data-ttu-id="07371-155">✔</span><span class="sxs-lookup"><span data-stu-id="07371-155">✔</span></span>|<span data-ttu-id="07371-156">L’URL https://vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="07371-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="07371-157">10 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-157">10 characters</span></span>| |<span data-ttu-id="07371-158">**Facultatif** ID réseau du partenaire Microsoft qui identifie l’organisation partenaire qui crée l’application.</span><span class="sxs-lookup"><span data-stu-id="07371-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="07371-159">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="07371-159">localizationInfo</span></span>

<span data-ttu-id="07371-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="07371-160">**Optional**</span></span>

<span data-ttu-id="07371-161">Permet de spécifier une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="07371-161">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="07371-162">Consultez la rubrique [Localization](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="07371-162">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="07371-163">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-163">Name</span></span>| <span data-ttu-id="07371-164">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-164">Maximum size</span></span> | <span data-ttu-id="07371-165">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-165">Required</span></span> | <span data-ttu-id="07371-166">Description</span><span class="sxs-lookup"><span data-stu-id="07371-166">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="07371-167">✔</span><span class="sxs-lookup"><span data-stu-id="07371-167">✔</span></span>|<span data-ttu-id="07371-168">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="07371-168">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="07371-169">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="07371-169">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="07371-170">Tableau d’objets spécifiant des traductions de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="07371-170">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="07371-171">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-171">Name</span></span>| <span data-ttu-id="07371-172">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-172">Maximum size</span></span> | <span data-ttu-id="07371-173">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-173">Required</span></span> | <span data-ttu-id="07371-174">Description</span><span class="sxs-lookup"><span data-stu-id="07371-174">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="07371-175">✔</span><span class="sxs-lookup"><span data-stu-id="07371-175">✔</span></span>|<span data-ttu-id="07371-176">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="07371-176">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="07371-177">✔</span><span class="sxs-lookup"><span data-stu-id="07371-177">✔</span></span>|<span data-ttu-id="07371-178">Chemin d’accès relatif à un fichier. JSON contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="07371-178">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="07371-179">nom</span><span class="sxs-lookup"><span data-stu-id="07371-179">name</span></span>

<span data-ttu-id="07371-180">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="07371-180">**Required**</span></span>

<span data-ttu-id="07371-181">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’expérience de teams.</span><span class="sxs-lookup"><span data-stu-id="07371-181">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="07371-182">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="07371-182">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="07371-183">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="07371-183">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="07371-184">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-184">Name</span></span>| <span data-ttu-id="07371-185">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-185">Maximum size</span></span> | <span data-ttu-id="07371-186">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-186">Required</span></span> | <span data-ttu-id="07371-187">Description</span><span class="sxs-lookup"><span data-stu-id="07371-187">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="07371-188">30 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-188">30 characters</span></span>|<span data-ttu-id="07371-189">✔</span><span class="sxs-lookup"><span data-stu-id="07371-189">✔</span></span>|<span data-ttu-id="07371-190">Nom complet court de l’application.</span><span class="sxs-lookup"><span data-stu-id="07371-190">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="07371-191">100 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-191">100 characters</span></span>||<span data-ttu-id="07371-192">Nom complet de l’application, utilisé si le nom complet de l’application dépasse les 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="07371-192">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="07371-193">description</span><span class="sxs-lookup"><span data-stu-id="07371-193">description</span></span>

<span data-ttu-id="07371-194">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="07371-194">**Required**</span></span>

<span data-ttu-id="07371-195">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="07371-195">Describes your app to users.</span></span> <span data-ttu-id="07371-196">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="07371-196">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="07371-197">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="07371-197">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="07371-198">Vous devez également noter, dans la description complète, si un compte externe est requis pour l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="07371-198">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="07371-199">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="07371-199">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="07371-200">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="07371-200">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="07371-201">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-201">Name</span></span>| <span data-ttu-id="07371-202">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-202">Maximum size</span></span> | <span data-ttu-id="07371-203">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-203">Required</span></span> | <span data-ttu-id="07371-204">Description</span><span class="sxs-lookup"><span data-stu-id="07371-204">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="07371-205">80 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-205">80 characters</span></span>|<span data-ttu-id="07371-206">✔</span><span class="sxs-lookup"><span data-stu-id="07371-206">✔</span></span>|<span data-ttu-id="07371-207">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="07371-207">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="07371-208">4000 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-208">4000 characters</span></span>|<span data-ttu-id="07371-209">✔</span><span class="sxs-lookup"><span data-stu-id="07371-209">✔</span></span>|<span data-ttu-id="07371-210">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="07371-210">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="07371-211">icons</span><span class="sxs-lookup"><span data-stu-id="07371-211">icons</span></span>

<span data-ttu-id="07371-212">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="07371-212">**Required**</span></span>

<span data-ttu-id="07371-213">Icônes utilisées dans l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="07371-213">Icons used within the Teams app.</span></span> <span data-ttu-id="07371-214">Les fichiers d’icône doivent être inclus dans le package de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="07371-214">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="07371-215">Pour plus d’informations, consultez la rubrique [Icons](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="07371-215">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="07371-216">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-216">Name</span></span>| <span data-ttu-id="07371-217">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-217">Maximum size</span></span> | <span data-ttu-id="07371-218">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-218">Required</span></span> | <span data-ttu-id="07371-219">Description</span><span class="sxs-lookup"><span data-stu-id="07371-219">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="07371-220">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-220">2048 characters</span></span>|<span data-ttu-id="07371-221">✔</span><span class="sxs-lookup"><span data-stu-id="07371-221">✔</span></span>|<span data-ttu-id="07371-222">Chemin d’accès relatif à une icône de contour PNG 32x32 transparent.</span><span class="sxs-lookup"><span data-stu-id="07371-222">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="07371-223">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-223">2048 characters</span></span>|<span data-ttu-id="07371-224">✔</span><span class="sxs-lookup"><span data-stu-id="07371-224">✔</span></span>|<span data-ttu-id="07371-225">Chemin d’accès relatif à une icône PNG 192x192 couleur complète.</span><span class="sxs-lookup"><span data-stu-id="07371-225">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="07371-226">accentColor</span><span class="sxs-lookup"><span data-stu-id="07371-226">accentColor</span></span>

<span data-ttu-id="07371-227">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="07371-227">**Required** &ndash; String</span></span>

<span data-ttu-id="07371-228">Couleur à utiliser en combinaison avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="07371-228">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="07371-229">La valeur doit être un code de couleur HTML valide commençant par « # », par `#4464ee`exemple.</span><span class="sxs-lookup"><span data-stu-id="07371-229">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="07371-230">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="07371-230">configurableTabs</span></span>

<span data-ttu-id="07371-231">**Optional**</span><span class="sxs-lookup"><span data-stu-id="07371-231">**Optional**</span></span>

<span data-ttu-id="07371-232">Utilisé lorsque l’expérience de votre application dispose d’un onglet Channel Team qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="07371-232">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="07371-233">Les onglets configurables sont pris en charge uniquement dans l’étendue teams et un seul onglet par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="07371-233">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="07371-234">L’objet est un tableau contenant tous les éléments du type `object`.</span><span class="sxs-lookup"><span data-stu-id="07371-234">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="07371-235">Ce bloc est requis uniquement pour les solutions qui fournissent une solution de sous-onglet canal configurable.</span><span class="sxs-lookup"><span data-stu-id="07371-235">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="07371-236">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-236">Name</span></span>| <span data-ttu-id="07371-237">Type</span><span class="sxs-lookup"><span data-stu-id="07371-237">Type</span></span>| <span data-ttu-id="07371-238">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-238">Maximum size</span></span> | <span data-ttu-id="07371-239">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-239">Required</span></span> | <span data-ttu-id="07371-240">Description</span><span class="sxs-lookup"><span data-stu-id="07371-240">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="07371-241">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-241">String</span></span>|<span data-ttu-id="07371-242">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-242">2048 characters</span></span>|<span data-ttu-id="07371-243">✔</span><span class="sxs-lookup"><span data-stu-id="07371-243">✔</span></span>|<span data-ttu-id="07371-244">URL https://à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="07371-244">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="07371-245">Boolean</span><span class="sxs-lookup"><span data-stu-id="07371-245">Boolean</span></span>|||<span data-ttu-id="07371-246">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="07371-246">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="07371-247">Default`true`</span><span class="sxs-lookup"><span data-stu-id="07371-247">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="07371-248">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="07371-248">Array of enum</span></span>|<span data-ttu-id="07371-249">1 </span><span class="sxs-lookup"><span data-stu-id="07371-249">1</span></span>|<span data-ttu-id="07371-250">✔</span><span class="sxs-lookup"><span data-stu-id="07371-250">✔</span></span>|<span data-ttu-id="07371-251">Actuellement, les onglets configurables prennent `team` en `groupchat` charge uniquement les étendues et.</span><span class="sxs-lookup"><span data-stu-id="07371-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="07371-252">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-252">String</span></span>|<span data-ttu-id="07371-253">2048</span><span class="sxs-lookup"><span data-stu-id="07371-253">2048</span></span>||<span data-ttu-id="07371-254">Chemin d’accès relatif à une image d’aperçu de tabulation à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="07371-254">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="07371-255">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="07371-255">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="07371-256">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="07371-256">Array of enum</span></span>|<span data-ttu-id="07371-257">1 </span><span class="sxs-lookup"><span data-stu-id="07371-257">1</span></span>||<span data-ttu-id="07371-258">Définit la manière dont votre onglet sera disponible dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="07371-258">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="07371-259">Les options `sharePointFullPage` sont et`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="07371-259">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="07371-260">staticTabs</span><span class="sxs-lookup"><span data-stu-id="07371-260">staticTabs</span></span>

<span data-ttu-id="07371-261">**Optional**</span><span class="sxs-lookup"><span data-stu-id="07371-261">**Optional**</span></span>

<span data-ttu-id="07371-262">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur ne les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="07371-262">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="07371-263">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="07371-263">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="07371-264">Les onglets statiques `team` déclarés dans l’étendue ne sont pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="07371-264">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="07371-265">L’objet est un tableau (au maximum 16 éléments) avec tous les éléments du type `object`.</span><span class="sxs-lookup"><span data-stu-id="07371-265">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="07371-266">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="07371-266">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="07371-267">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-267">Name</span></span>| <span data-ttu-id="07371-268">Type</span><span class="sxs-lookup"><span data-stu-id="07371-268">Type</span></span>| <span data-ttu-id="07371-269">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-269">Maximum size</span></span> | <span data-ttu-id="07371-270">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-270">Required</span></span> | <span data-ttu-id="07371-271">Description</span><span class="sxs-lookup"><span data-stu-id="07371-271">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="07371-272">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-272">String</span></span>|<span data-ttu-id="07371-273">64 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-273">64 characters</span></span>|<span data-ttu-id="07371-274">✔</span><span class="sxs-lookup"><span data-stu-id="07371-274">✔</span></span>|<span data-ttu-id="07371-275">Identificateur unique de l’entité que l’onglet affiche.</span><span class="sxs-lookup"><span data-stu-id="07371-275">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="07371-276">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-276">String</span></span>|<span data-ttu-id="07371-277">128 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-277">128 characters</span></span>|<span data-ttu-id="07371-278">✔</span><span class="sxs-lookup"><span data-stu-id="07371-278">✔</span></span>|<span data-ttu-id="07371-279">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="07371-279">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="07371-280">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-280">String</span></span>|<span data-ttu-id="07371-281">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-281">2048 characters</span></span>|<span data-ttu-id="07371-282">✔</span><span class="sxs-lookup"><span data-stu-id="07371-282">✔</span></span>|<span data-ttu-id="07371-283">URL https://qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de dessin de teams.</span><span class="sxs-lookup"><span data-stu-id="07371-283">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="07371-284">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-284">String</span></span>|<span data-ttu-id="07371-285">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-285">2048 characters</span></span>||<span data-ttu-id="07371-286">URL https://vers laquelle pointer si un utilisateur choisit de l’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="07371-286">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="07371-287">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="07371-287">Array of enum</span></span>|<span data-ttu-id="07371-288">1 </span><span class="sxs-lookup"><span data-stu-id="07371-288">1</span></span>|<span data-ttu-id="07371-289">✔</span><span class="sxs-lookup"><span data-stu-id="07371-289">✔</span></span>|<span data-ttu-id="07371-290">Actuellement, les onglets statiques `personal` prennent en charge uniquement l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="07371-290">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

## <a name="bots"></a><span data-ttu-id="07371-291">bots</span><span class="sxs-lookup"><span data-stu-id="07371-291">bots</span></span>

<span data-ttu-id="07371-292">**Optional**</span><span class="sxs-lookup"><span data-stu-id="07371-292">**Optional**</span></span>

<span data-ttu-id="07371-293">Définit une solution de robot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="07371-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="07371-294">L’objet est un tableau (maximum d’un seul élément&mdash;, actuellement un seul bot est autorisé par application) à tous les éléments du `object`type.</span><span class="sxs-lookup"><span data-stu-id="07371-294">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="07371-295">Ce bloc est requis uniquement pour les solutions qui fournissent une expérience de robot.</span><span class="sxs-lookup"><span data-stu-id="07371-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="07371-296">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-296">Name</span></span>| <span data-ttu-id="07371-297">Type</span><span class="sxs-lookup"><span data-stu-id="07371-297">Type</span></span>| <span data-ttu-id="07371-298">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-298">Maximum size</span></span> | <span data-ttu-id="07371-299">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-299">Required</span></span> | <span data-ttu-id="07371-300">Description</span><span class="sxs-lookup"><span data-stu-id="07371-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="07371-301">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-301">String</span></span>|<span data-ttu-id="07371-302">64 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-302">64 characters</span></span>|<span data-ttu-id="07371-303">✔</span><span class="sxs-lookup"><span data-stu-id="07371-303">✔</span></span>|<span data-ttu-id="07371-304">ID d’application Microsoft unique pour le bot enregistré avec l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="07371-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="07371-305">Il peut s’agir de la même chose que l' [ID d’application](#id)global.</span><span class="sxs-lookup"><span data-stu-id="07371-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="07371-306">Boolean</span><span class="sxs-lookup"><span data-stu-id="07371-306">Boolean</span></span>|||<span data-ttu-id="07371-307">Indique si le bot utilise un Conseil de l’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="07371-307">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="07371-308">Default`false`</span><span class="sxs-lookup"><span data-stu-id="07371-308">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="07371-309">Boolean</span><span class="sxs-lookup"><span data-stu-id="07371-309">Boolean</span></span>|||<span data-ttu-id="07371-310">Indique si un bot est un robot à sens unique, par opposition à un bot de conversation.</span><span class="sxs-lookup"><span data-stu-id="07371-310">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="07371-311">Default`false`</span><span class="sxs-lookup"><span data-stu-id="07371-311">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="07371-312">Boolean</span><span class="sxs-lookup"><span data-stu-id="07371-312">Boolean</span></span>|||<span data-ttu-id="07371-313">Indique si le bot prend en charge la possibilité de télécharger ou de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="07371-313">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="07371-314">Default`false`</span><span class="sxs-lookup"><span data-stu-id="07371-314">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="07371-315">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="07371-315">Array of enum</span></span>|<span data-ttu-id="07371-316">3 </span><span class="sxs-lookup"><span data-stu-id="07371-316">3</span></span>|<span data-ttu-id="07371-317">✔</span><span class="sxs-lookup"><span data-stu-id="07371-317">✔</span></span>|<span data-ttu-id="07371-318">Indique si le bot offre une expérience dans le contexte d’un canal dans un `team`, dans une conversation de groupe`groupchat`() ou dans une expérience étendue à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="07371-318">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="07371-319">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="07371-319">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="07371-320">bots. commandLists</span><span class="sxs-lookup"><span data-stu-id="07371-320">bots.commandLists</span></span>

<span data-ttu-id="07371-321">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="07371-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="07371-322">L’objet est un tableau (nombre maximal de 2 éléments) avec tous les éléments `object`de type ; vous devez définir une liste de commandes distincte pour chaque étendue prise en charge par votre bot.</span><span class="sxs-lookup"><span data-stu-id="07371-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="07371-323">Pour plus d’informations, voir [menus de bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="07371-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="07371-324">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-324">Name</span></span>| <span data-ttu-id="07371-325">Type</span><span class="sxs-lookup"><span data-stu-id="07371-325">Type</span></span>| <span data-ttu-id="07371-326">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-326">Maximum size</span></span> | <span data-ttu-id="07371-327">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-327">Required</span></span> | <span data-ttu-id="07371-328">Description</span><span class="sxs-lookup"><span data-stu-id="07371-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="07371-329">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="07371-329">array of enum</span></span>|<span data-ttu-id="07371-330">3 </span><span class="sxs-lookup"><span data-stu-id="07371-330">3</span></span>|<span data-ttu-id="07371-331">✔</span><span class="sxs-lookup"><span data-stu-id="07371-331">✔</span></span>|<span data-ttu-id="07371-332">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="07371-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="07371-333">Les options `team`sont `personal`, et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="07371-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="07371-334">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="07371-334">array of objects</span></span>|<span data-ttu-id="07371-335">10 </span><span class="sxs-lookup"><span data-stu-id="07371-335">10</span></span>|<span data-ttu-id="07371-336">✔</span><span class="sxs-lookup"><span data-stu-id="07371-336">✔</span></span>|<span data-ttu-id="07371-337">Tableau de commandes pris en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="07371-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="07371-338">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="07371-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="07371-339">`description`: description simple ou exemple de la syntaxe de commande et de son argument (String, 128)</span><span class="sxs-lookup"><span data-stu-id="07371-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="07371-340">ceux</span><span class="sxs-lookup"><span data-stu-id="07371-340">connectors</span></span>

<span data-ttu-id="07371-341">**Optional**</span><span class="sxs-lookup"><span data-stu-id="07371-341">**Optional**</span></span>

<span data-ttu-id="07371-342">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="07371-342">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="07371-343">L’objet est un tableau (un maximum de 1 élément) avec tous les éléments `object`de type.</span><span class="sxs-lookup"><span data-stu-id="07371-343">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="07371-344">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="07371-344">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="07371-345">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-345">Name</span></span>| <span data-ttu-id="07371-346">Type</span><span class="sxs-lookup"><span data-stu-id="07371-346">Type</span></span>| <span data-ttu-id="07371-347">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-347">Maximum size</span></span> | <span data-ttu-id="07371-348">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-348">Required</span></span> | <span data-ttu-id="07371-349">Description</span><span class="sxs-lookup"><span data-stu-id="07371-349">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="07371-350">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-350">String</span></span>|<span data-ttu-id="07371-351">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-351">2048 characters</span></span>|<span data-ttu-id="07371-352">✔</span><span class="sxs-lookup"><span data-stu-id="07371-352">✔</span></span>|<span data-ttu-id="07371-353">URL https://à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="07371-353">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="07371-354">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-354">String</span></span>|<span data-ttu-id="07371-355">64 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-355">64 characters</span></span>|<span data-ttu-id="07371-356">✔</span><span class="sxs-lookup"><span data-stu-id="07371-356">✔</span></span>|<span data-ttu-id="07371-357">Identificateur unique du connecteur correspondant à son ID dans le [tableau de bord du développeur de connecteurs](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="07371-357">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="07371-358">Tableau d’énumération</span><span class="sxs-lookup"><span data-stu-id="07371-358">Array of enum</span></span>|<span data-ttu-id="07371-359">1 </span><span class="sxs-lookup"><span data-stu-id="07371-359">1</span></span>|<span data-ttu-id="07371-360">✔</span><span class="sxs-lookup"><span data-stu-id="07371-360">✔</span></span>|<span data-ttu-id="07371-361">Indique si le connecteur offre une expérience dans le contexte d’un canal dans un `team`, ou une expérience étendue à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="07371-361">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="07371-362">Actuellement, seule l' `team` étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="07371-362">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="07371-363">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="07371-363">composeExtensions</span></span>

<span data-ttu-id="07371-364">**Optional**</span><span class="sxs-lookup"><span data-stu-id="07371-364">**Optional**</span></span>

<span data-ttu-id="07371-365">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="07371-365">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="07371-366">Le nom de la fonctionnalité a été modifié de « extension de composition » en « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même afin que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="07371-366">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="07371-367">L’objet est un tableau (un maximum de 1 élément) avec tous les éléments `object`de type.</span><span class="sxs-lookup"><span data-stu-id="07371-367">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="07371-368">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="07371-368">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="07371-369">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-369">Name</span></span>| <span data-ttu-id="07371-370">Type</span><span class="sxs-lookup"><span data-stu-id="07371-370">Type</span></span> | <span data-ttu-id="07371-371">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-371">Maximum Size</span></span> | <span data-ttu-id="07371-372">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-372">Required</span></span> | <span data-ttu-id="07371-373">Description</span><span class="sxs-lookup"><span data-stu-id="07371-373">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="07371-374">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-374">String</span></span>|<span data-ttu-id="07371-375">64</span><span class="sxs-lookup"><span data-stu-id="07371-375">64</span></span>|<span data-ttu-id="07371-376">✔</span><span class="sxs-lookup"><span data-stu-id="07371-376">✔</span></span>|<span data-ttu-id="07371-377">ID d’application Microsoft unique pour le bot qui sauvegarde l’extension de messagerie, tel qu’inscrit auprès de l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="07371-377">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="07371-378">Il peut s’agir de la même chose que l’ID d’application global.</span><span class="sxs-lookup"><span data-stu-id="07371-378">This may well be the same as the overall App ID.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="07371-379">Boolean</span><span class="sxs-lookup"><span data-stu-id="07371-379">Boolean</span></span>|||<span data-ttu-id="07371-380">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="07371-380">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="07371-381">La valeur par `false`défaut est.</span><span class="sxs-lookup"><span data-stu-id="07371-381">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="07371-382">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="07371-382">Array of object</span></span>|<span data-ttu-id="07371-383">10 </span><span class="sxs-lookup"><span data-stu-id="07371-383">10</span></span>|<span data-ttu-id="07371-384">✔</span><span class="sxs-lookup"><span data-stu-id="07371-384">✔</span></span>|<span data-ttu-id="07371-385">Tableau de commandes prises en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="07371-385">Array of commands the messaging extension supports</span></span>|
|`messageHandlers`|<span data-ttu-id="07371-386">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="07371-386">Array of Objects</span></span>|<span data-ttu-id="07371-387">5 </span><span class="sxs-lookup"><span data-stu-id="07371-387">5</span></span>||<span data-ttu-id="07371-388">Liste de gestionnaires permettant d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="07371-388">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="07371-389">Les domaines doivent également être affichés dans`validDomains`</span><span class="sxs-lookup"><span data-stu-id="07371-389">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="07371-390">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-390">String</span></span>|||<span data-ttu-id="07371-391">Type de gestionnaire de messages.</span><span class="sxs-lookup"><span data-stu-id="07371-391">The type of message handler.</span></span> <span data-ttu-id="07371-392">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="07371-392">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="07371-393">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="07371-393">Array of Strings</span></span>|||<span data-ttu-id="07371-394">Tableau de domaines pour lesquels le gestionnaire de messages de liaison peut s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="07371-394">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="07371-395">composeExtensions. Commands</span><span class="sxs-lookup"><span data-stu-id="07371-395">composeExtensions.commands</span></span>

<span data-ttu-id="07371-396">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="07371-396">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="07371-397">Chaque commande apparaît dans Microsoft teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="07371-397">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="07371-398">Il y a un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="07371-398">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="07371-399">Chaque élément de commande est un objet de la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="07371-399">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="07371-400">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-400">Name</span></span>| <span data-ttu-id="07371-401">Type</span><span class="sxs-lookup"><span data-stu-id="07371-401">Type</span></span>| <span data-ttu-id="07371-402">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-402">Maximum size</span></span> | <span data-ttu-id="07371-403">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-403">Required</span></span> | <span data-ttu-id="07371-404">Description</span><span class="sxs-lookup"><span data-stu-id="07371-404">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="07371-405">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-405">String</span></span>|<span data-ttu-id="07371-406">64 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-406">64 characters</span></span>|<span data-ttu-id="07371-407">✔</span><span class="sxs-lookup"><span data-stu-id="07371-407">✔</span></span>|<span data-ttu-id="07371-408">ID de la commande</span><span class="sxs-lookup"><span data-stu-id="07371-408">The ID for the command</span></span>|
|`type`|<span data-ttu-id="07371-409">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-409">String</span></span>|<span data-ttu-id="07371-410">64 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-410">64 characters</span></span>||<span data-ttu-id="07371-411">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="07371-411">Type of the command.</span></span> <span data-ttu-id="07371-412">L’une `query` ou `action`l’autre.</span><span class="sxs-lookup"><span data-stu-id="07371-412">One of `query` or `action`.</span></span> <span data-ttu-id="07371-413">Default`query`</span><span class="sxs-lookup"><span data-stu-id="07371-413">Default: `query`</span></span>|
|`title`|<span data-ttu-id="07371-414">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-414">String</span></span>|<span data-ttu-id="07371-415">32 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-415">32 characters</span></span>|<span data-ttu-id="07371-416">✔</span><span class="sxs-lookup"><span data-stu-id="07371-416">✔</span></span>|<span data-ttu-id="07371-417">Nom de commande convivial</span><span class="sxs-lookup"><span data-stu-id="07371-417">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="07371-418">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-418">String</span></span>|<span data-ttu-id="07371-419">128 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-419">128 characters</span></span>||<span data-ttu-id="07371-420">La description qui s’affiche pour les utilisateurs afin d’indiquer la finalité de cette commande.</span><span class="sxs-lookup"><span data-stu-id="07371-420">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="07371-421">Boolean</span><span class="sxs-lookup"><span data-stu-id="07371-421">Boolean</span></span>|||<span data-ttu-id="07371-422">Valeur booléenne indiquant si la commande doit être exécutée initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="07371-422">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="07371-423">Default`false`</span><span class="sxs-lookup"><span data-stu-id="07371-423">Default: `false`</span></span>|
|`context`|<span data-ttu-id="07371-424">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="07371-424">Array of Strings</span></span>|<span data-ttu-id="07371-425">3 </span><span class="sxs-lookup"><span data-stu-id="07371-425">3</span></span>||<span data-ttu-id="07371-426">Définit l’emplacement à partir duquel l’extension de message peut être appelée.</span><span class="sxs-lookup"><span data-stu-id="07371-426">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="07371-427">Toute combinaison de `compose`, `commandBox`, `message`.</span><span class="sxs-lookup"><span data-stu-id="07371-427">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="07371-428">Valeur par défaut est`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="07371-428">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="07371-429">Boolean</span><span class="sxs-lookup"><span data-stu-id="07371-429">Boolean</span></span>|||<span data-ttu-id="07371-430">Une valeur booléenne qui indique s’il doit extraire le module de tâches de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="07371-430">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="07371-431">Objet</span><span class="sxs-lookup"><span data-stu-id="07371-431">Object</span></span>|||<span data-ttu-id="07371-432">Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="07371-432">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="07371-433">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-433">String</span></span>|<span data-ttu-id="07371-434">64</span><span class="sxs-lookup"><span data-stu-id="07371-434">64</span></span>||<span data-ttu-id="07371-435">Titre de la boîte de dialogue initiale</span><span class="sxs-lookup"><span data-stu-id="07371-435">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="07371-436">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-436">String</span></span>|||<span data-ttu-id="07371-437">Largeur de la boîte de dialogue-soit un nombre en pixels, soit une mise en page par défaut telle que « grande », « moyen » ou « petite »</span><span class="sxs-lookup"><span data-stu-id="07371-437">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="07371-438">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-438">String</span></span>|||<span data-ttu-id="07371-439">Hauteur de la boîte de dialogue : nombre en pixels ou mise en page par défaut, par exemple, « grande », « moyen » ou « petite »</span><span class="sxs-lookup"><span data-stu-id="07371-439">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="07371-440">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-440">String</span></span>|||<span data-ttu-id="07371-441">URL d’affichage WebView initiale</span><span class="sxs-lookup"><span data-stu-id="07371-441">Initial webview URL</span></span>|
|`parameters`|<span data-ttu-id="07371-442">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="07371-442">Array of object</span></span>|<span data-ttu-id="07371-443">5 </span><span class="sxs-lookup"><span data-stu-id="07371-443">5</span></span>|<span data-ttu-id="07371-444">✔</span><span class="sxs-lookup"><span data-stu-id="07371-444">✔</span></span>|<span data-ttu-id="07371-445">La liste des paramètres que la commande prend.</span><span class="sxs-lookup"><span data-stu-id="07371-445">The list of parameters the command takes.</span></span> <span data-ttu-id="07371-446">Minimum : 1 ; maximum : 5</span><span class="sxs-lookup"><span data-stu-id="07371-446">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="07371-447">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-447">String</span></span>|<span data-ttu-id="07371-448">64 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-448">64 characters</span></span>|<span data-ttu-id="07371-449">✔</span><span class="sxs-lookup"><span data-stu-id="07371-449">✔</span></span>|<span data-ttu-id="07371-450">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="07371-450">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="07371-451">Elle est incluse dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="07371-451">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="07371-452">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-452">String</span></span>|<span data-ttu-id="07371-453">32 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-453">32 characters</span></span>|<span data-ttu-id="07371-454">✔</span><span class="sxs-lookup"><span data-stu-id="07371-454">✔</span></span>|<span data-ttu-id="07371-455">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="07371-455">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="07371-456">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-456">String</span></span>|<span data-ttu-id="07371-457">128 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-457">128 characters</span></span>||<span data-ttu-id="07371-458">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="07371-458">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="07371-459">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-459">String</span></span>|<span data-ttu-id="07371-460">128 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-460">128 characters</span></span>||<span data-ttu-id="07371-461">Définit le type de contrôle affiché sur un module de tâche `fetchTask: true`pour.</span><span class="sxs-lookup"><span data-stu-id="07371-461">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="07371-462">`text` `textarea` `number`, `date`,, `time` `toggle``choiceset`</span><span class="sxs-lookup"><span data-stu-id="07371-462">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="07371-463">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="07371-463">Array of Objects</span></span>|<span data-ttu-id="07371-464">10 </span><span class="sxs-lookup"><span data-stu-id="07371-464">10</span></span>||<span data-ttu-id="07371-465">Options de choix pour le `choiceset`.</span><span class="sxs-lookup"><span data-stu-id="07371-465">The choice options for the `choiceset`.</span></span> <span data-ttu-id="07371-466">À utiliser uniquement `parameter.inputType` lorsque est`choiceset`</span><span class="sxs-lookup"><span data-stu-id="07371-466">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="07371-467">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-467">String</span></span>|<span data-ttu-id="07371-468">128</span><span class="sxs-lookup"><span data-stu-id="07371-468">128</span></span>||<span data-ttu-id="07371-469">Titre du choix</span><span class="sxs-lookup"><span data-stu-id="07371-469">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="07371-470">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-470">String</span></span>|<span data-ttu-id="07371-471">512</span><span class="sxs-lookup"><span data-stu-id="07371-471">512</span></span>||<span data-ttu-id="07371-472">Valeur du choix</span><span class="sxs-lookup"><span data-stu-id="07371-472">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="07371-473">autorisations</span><span class="sxs-lookup"><span data-stu-id="07371-473">permissions</span></span>

<span data-ttu-id="07371-474">**Optional**</span><span class="sxs-lookup"><span data-stu-id="07371-474">**Optional**</span></span>

<span data-ttu-id="07371-475">Un tableau `string` qui spécifie les autorisations demandées par l’application, ce qui permet aux utilisateurs finaux de savoir comment effectuer l’extension.</span><span class="sxs-lookup"><span data-stu-id="07371-475">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="07371-476">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="07371-476">The following options are non-exclusive:</span></span>

* <span data-ttu-id="07371-477">`identity`&emsp; Nécessite des informations d’identité d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="07371-477">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="07371-478">`messageTeamMembers`&emsp; Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="07371-478">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="07371-479">Si vous modifiez ces autorisations lors de la mise à jour de votre application, vos utilisateurs répéteront le processus de consentement la première fois qu’ils exécuteront l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="07371-479">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="07371-480">Pour plus d’informations, consultez [la rubrique mise à jour de votre application](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="07371-480">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="07371-481">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="07371-481">devicePermissions</span></span>

<span data-ttu-id="07371-482">**Facultatif** Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="07371-482">**Optional** Array of Strings</span></span>

<span data-ttu-id="07371-483">Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur auquel votre application peut demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="07371-483">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="07371-484">Les options sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="07371-484">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="07371-485">validDomains</span><span class="sxs-lookup"><span data-stu-id="07371-485">validDomains</span></span>

<span data-ttu-id="07371-486">**Facultatif** **, sauf indication contraire**</span><span class="sxs-lookup"><span data-stu-id="07371-486">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="07371-487">Une liste des domaines valides pour les sites Web que l’application prévoit de charger dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="07371-487">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="07371-488">Les listes de domaine peuvent inclure des caractères génériques `*.example.com`, par exemple.</span><span class="sxs-lookup"><span data-stu-id="07371-488">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="07371-489">Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com`.</span><span class="sxs-lookup"><span data-stu-id="07371-489">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="07371-490">Si la configuration de votre onglet ou de votre interface utilisateur de contenu doit accéder à un autre domaine en plus de celui utilisé pour la configuration d’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="07371-490">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="07371-491">Toutefois, il n’est **pas** nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="07371-491">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="07371-492">Par exemple, pour authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne `validDomains[]`devez pas inclure Accounts.google.com dans.</span><span class="sxs-lookup"><span data-stu-id="07371-492">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="07371-493">Les applications teams qui requièrent leurs propres URL SharePoint pour fonctionner correctement, peuvent inclure « {teamsitedomain} » dans leur liste de domaines valide.</span><span class="sxs-lookup"><span data-stu-id="07371-493">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07371-494">N’ajoutez pas de domaines qui se trouvent en dehors de votre contrôle, soit directement, soit via des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="07371-494">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="07371-495">Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="07371-495">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="07371-496">L’objet est un tableau contenant tous les éléments du type `string`.</span><span class="sxs-lookup"><span data-stu-id="07371-496">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="07371-497">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="07371-497">webApplicationInfo</span></span>

<span data-ttu-id="07371-498">**Optional**</span><span class="sxs-lookup"><span data-stu-id="07371-498">**Optional**</span></span>

<span data-ttu-id="07371-499">Spécifiez l’ID de votre application AAD et les informations graphiques pour aider les utilisateurs à se connecter à votre application AAD de manière transparente.</span><span class="sxs-lookup"><span data-stu-id="07371-499">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="07371-500">Nom</span><span class="sxs-lookup"><span data-stu-id="07371-500">Name</span></span>| <span data-ttu-id="07371-501">Type</span><span class="sxs-lookup"><span data-stu-id="07371-501">Type</span></span>| <span data-ttu-id="07371-502">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="07371-502">Maximum size</span></span> | <span data-ttu-id="07371-503">Requis</span><span class="sxs-lookup"><span data-stu-id="07371-503">Required</span></span> | <span data-ttu-id="07371-504">Description</span><span class="sxs-lookup"><span data-stu-id="07371-504">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="07371-505">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-505">String</span></span>|<span data-ttu-id="07371-506">36 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-506">36 characters</span></span>|<span data-ttu-id="07371-507">✔</span><span class="sxs-lookup"><span data-stu-id="07371-507">✔</span></span>|<span data-ttu-id="07371-508">ID de l’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="07371-508">AAD application id of the app.</span></span> <span data-ttu-id="07371-509">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="07371-509">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="07371-510">Chaîne</span><span class="sxs-lookup"><span data-stu-id="07371-510">String</span></span>|<span data-ttu-id="07371-511">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="07371-511">2048 characters</span></span>|<span data-ttu-id="07371-512">✔</span><span class="sxs-lookup"><span data-stu-id="07371-512">✔</span></span>|<span data-ttu-id="07371-513">URL de ressource de l’application pour l’acquisition du jeton d’authentification pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="07371-513">Resource url of app for acquiring auth token for SSO.</span></span>|
