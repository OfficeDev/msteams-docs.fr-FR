---
title: Référence du schéma de manifeste
description: Décrit le schéma pris en charge par le manifeste pour Microsoft teams
keywords: schéma de manifeste teams
ms.openlocfilehash: 1a1a690e6e382dcad3ceb200ec02286e8c9171f8
ms.sourcegitcommit: 060b486c38b72a3e6b63b4d617b759174082a508
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2020
ms.locfileid: "41953487"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="280b2-104">Référence : schéma de manifeste pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="280b2-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="280b2-105">Le manifeste Microsoft teams décrit la façon dont l’application s’intègre dans le produit Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="280b2-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="280b2-106">Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span><span class="sxs-lookup"><span data-stu-id="280b2-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="280b2-107">Les versions précédentes 1.0 à 1.4 sont également prises en charge (à l’aide de « v1. x » dans l’URL).</span><span class="sxs-lookup"><span data-stu-id="280b2-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="280b2-108">L’exemple de schéma suivant montre toutes les options d’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="280b2-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="280b2-109">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="280b2-109">Sample full manifest</span></span>

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

<span data-ttu-id="280b2-110">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="280b2-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="280b2-111">$schema</span><span class="sxs-lookup"><span data-stu-id="280b2-111">$schema</span></span>

<span data-ttu-id="280b2-112">*Facultatif, mais chaîne recommandée* &ndash;</span><span class="sxs-lookup"><span data-stu-id="280b2-112">*Optional, but recommended* &ndash; String</span></span>

<span data-ttu-id="280b2-113">URL https://référençant le schéma JSON du manifeste.</span><span class="sxs-lookup"><span data-stu-id="280b2-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="280b2-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="280b2-114">manifestVersion</span></span>

<span data-ttu-id="280b2-115">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="280b2-115">**Required** &ndash; String</span></span>

<span data-ttu-id="280b2-116">Version du schéma de manifeste utilisé par ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="280b2-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="280b2-117">Il doit être « 1,5 ».</span><span class="sxs-lookup"><span data-stu-id="280b2-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="280b2-118">version</span><span class="sxs-lookup"><span data-stu-id="280b2-118">version</span></span>

<span data-ttu-id="280b2-119">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="280b2-119">**Required** &ndash; String</span></span>

<span data-ttu-id="280b2-120">Version de l’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="280b2-120">The version of the specific app.</span></span> <span data-ttu-id="280b2-121">Si vous mettez à jour un événement dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="280b2-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="280b2-122">Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="280b2-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="280b2-123">Si cette application a été envoyée au magasin, le nouveau manifeste doit être soumis à nouveau et revalidé.</span><span class="sxs-lookup"><span data-stu-id="280b2-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="280b2-124">Ensuite, les utilisateurs de cette application obtiendront automatiquement le nouveau manifeste mis à jour en quelques heures, une fois celui-ci approuvé.</span><span class="sxs-lookup"><span data-stu-id="280b2-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="280b2-125">Si l’application a demandé une modification des autorisations, les utilisateurs sont invités à effectuer une mise à niveau et à reconfigurer l’application.</span><span class="sxs-lookup"><span data-stu-id="280b2-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="280b2-126">Cette chaîne de version doit suivre la norme [semver](http://semver.org/) (major. Petites. CORRECTIF).</span><span class="sxs-lookup"><span data-stu-id="280b2-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="280b2-127">id</span><span class="sxs-lookup"><span data-stu-id="280b2-127">id</span></span>

<span data-ttu-id="280b2-128">ID d’application Microsoft **requis** &ndash;</span><span class="sxs-lookup"><span data-stu-id="280b2-128">**Required** &ndash; Microsoft app ID</span></span>

<span data-ttu-id="280b2-129">Identificateur unique généré par Microsoft pour cette application.</span><span class="sxs-lookup"><span data-stu-id="280b2-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="280b2-130">Si vous avez inscrit un robot via Microsoft bot Framework ou si l’application Web de votre onglet se connecte déjà à Microsoft, vous devez déjà avoir un ID et l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="280b2-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="280b2-131">Dans le cas contraire, vous devez générer un nouvel ID dans le portail d’inscription des applications Microsoft ([mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous ajoutez un bot. Remarque : Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="280b2-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="packagename"></a><span data-ttu-id="280b2-132">packageName</span><span class="sxs-lookup"><span data-stu-id="280b2-132">packageName</span></span>

<span data-ttu-id="280b2-133">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="280b2-133">**Required** &ndash; String</span></span>

<span data-ttu-id="280b2-134">Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="280b2-134">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span>

## <a name="developer"></a><span data-ttu-id="280b2-135">developer</span><span class="sxs-lookup"><span data-stu-id="280b2-135">developer</span></span>

<span data-ttu-id="280b2-136">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="280b2-136">**Required**</span></span>

<span data-ttu-id="280b2-137">Spécifie les informations relatives à votre société.</span><span class="sxs-lookup"><span data-stu-id="280b2-137">Specifies information about your company.</span></span> <span data-ttu-id="280b2-138">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="280b2-138">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="280b2-139">Pour plus d’informations, consultez nos [instructions de publication](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) .</span><span class="sxs-lookup"><span data-stu-id="280b2-139">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="280b2-140">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-140">Name</span></span>| <span data-ttu-id="280b2-141">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-141">Maximum size</span></span> | <span data-ttu-id="280b2-142">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-142">Required</span></span> | <span data-ttu-id="280b2-143">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-143">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="280b2-144">32 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-144">32 characters</span></span>|<span data-ttu-id="280b2-145">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-145">✔</span></span>|<span data-ttu-id="280b2-146">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="280b2-146">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="280b2-147">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-147">2048 characters</span></span>|<span data-ttu-id="280b2-148">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-148">✔</span></span>|<span data-ttu-id="280b2-149">URL https://vers le site Web du développeur.</span><span class="sxs-lookup"><span data-stu-id="280b2-149">The https:// URL to the developer's website.</span></span> <span data-ttu-id="280b2-150">Ce lien doit prendre les utilisateurs à la page d’accueil de votre entreprise ou de votre propre produit.</span><span class="sxs-lookup"><span data-stu-id="280b2-150">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="280b2-151">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-151">2048 characters</span></span>|<span data-ttu-id="280b2-152">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-152">✔</span></span>|<span data-ttu-id="280b2-153">URL https://vers la stratégie de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="280b2-153">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="280b2-154">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-154">2048 characters</span></span>|<span data-ttu-id="280b2-155">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-155">✔</span></span>|<span data-ttu-id="280b2-156">L’URL https://vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="280b2-156">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="280b2-157">10 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-157">10 characters</span></span>| |<span data-ttu-id="280b2-158">**Facultatif** ID réseau du partenaire Microsoft qui identifie l’organisation partenaire qui crée l’application.</span><span class="sxs-lookup"><span data-stu-id="280b2-158">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="localizationinfo"></a><span data-ttu-id="280b2-159">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="280b2-159">localizationInfo</span></span>

<span data-ttu-id="280b2-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="280b2-160">**Optional**</span></span>

<span data-ttu-id="280b2-161">Permet de spécifier une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="280b2-161">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="280b2-162">Consultez la rubrique [Localization](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="280b2-162">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="280b2-163">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-163">Name</span></span>| <span data-ttu-id="280b2-164">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-164">Maximum size</span></span> | <span data-ttu-id="280b2-165">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-165">Required</span></span> | <span data-ttu-id="280b2-166">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-166">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="280b2-167">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-167">✔</span></span>|<span data-ttu-id="280b2-168">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="280b2-168">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="280b2-169">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="280b2-169">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="280b2-170">Tableau d’objets spécifiant des traductions de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="280b2-170">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="280b2-171">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-171">Name</span></span>| <span data-ttu-id="280b2-172">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-172">Maximum size</span></span> | <span data-ttu-id="280b2-173">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-173">Required</span></span> | <span data-ttu-id="280b2-174">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-174">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="280b2-175">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-175">✔</span></span>|<span data-ttu-id="280b2-176">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="280b2-176">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="280b2-177">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-177">✔</span></span>|<span data-ttu-id="280b2-178">Chemin d’accès relatif à un fichier. JSON contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="280b2-178">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="name"></a><span data-ttu-id="280b2-179">nom</span><span class="sxs-lookup"><span data-stu-id="280b2-179">name</span></span>

<span data-ttu-id="280b2-180">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="280b2-180">**Required**</span></span>

<span data-ttu-id="280b2-181">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’expérience de teams.</span><span class="sxs-lookup"><span data-stu-id="280b2-181">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="280b2-182">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="280b2-182">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="280b2-183">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="280b2-183">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="280b2-184">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-184">Name</span></span>| <span data-ttu-id="280b2-185">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-185">Maximum size</span></span> | <span data-ttu-id="280b2-186">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-186">Required</span></span> | <span data-ttu-id="280b2-187">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-187">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="280b2-188">30 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-188">30 characters</span></span>|<span data-ttu-id="280b2-189">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-189">✔</span></span>|<span data-ttu-id="280b2-190">Nom complet court de l’application.</span><span class="sxs-lookup"><span data-stu-id="280b2-190">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="280b2-191">100 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-191">100 characters</span></span>||<span data-ttu-id="280b2-192">Nom complet de l’application, utilisé si le nom complet de l’application dépasse les 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="280b2-192">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="280b2-193">description</span><span class="sxs-lookup"><span data-stu-id="280b2-193">description</span></span>

<span data-ttu-id="280b2-194">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="280b2-194">**Required**</span></span>

<span data-ttu-id="280b2-195">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="280b2-195">Describes your app to users.</span></span> <span data-ttu-id="280b2-196">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="280b2-196">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="280b2-197">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="280b2-197">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="280b2-198">Vous devez également noter, dans la description complète, si un compte externe est requis pour l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="280b2-198">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="280b2-199">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="280b2-199">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="280b2-200">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="280b2-200">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="280b2-201">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-201">Name</span></span>| <span data-ttu-id="280b2-202">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-202">Maximum size</span></span> | <span data-ttu-id="280b2-203">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-203">Required</span></span> | <span data-ttu-id="280b2-204">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-204">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="280b2-205">80 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-205">80 characters</span></span>|<span data-ttu-id="280b2-206">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-206">✔</span></span>|<span data-ttu-id="280b2-207">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="280b2-207">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="280b2-208">4000 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-208">4000 characters</span></span>|<span data-ttu-id="280b2-209">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-209">✔</span></span>|<span data-ttu-id="280b2-210">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="280b2-210">The full description of your app.</span></span>|

## <a name="icons"></a><span data-ttu-id="280b2-211">icons</span><span class="sxs-lookup"><span data-stu-id="280b2-211">icons</span></span>

<span data-ttu-id="280b2-212">**Obligatoire**</span><span class="sxs-lookup"><span data-stu-id="280b2-212">**Required**</span></span>

<span data-ttu-id="280b2-213">Icônes utilisées dans l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="280b2-213">Icons used within the Teams app.</span></span> <span data-ttu-id="280b2-214">Les fichiers d’icône doivent être inclus dans le package de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="280b2-214">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="280b2-215">Pour plus d’informations, consultez la rubrique [Icons](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="280b2-215">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="280b2-216">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-216">Name</span></span>| <span data-ttu-id="280b2-217">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-217">Maximum size</span></span> | <span data-ttu-id="280b2-218">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-218">Required</span></span> | <span data-ttu-id="280b2-219">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-219">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="280b2-220">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-220">2048 characters</span></span>|<span data-ttu-id="280b2-221">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-221">✔</span></span>|<span data-ttu-id="280b2-222">Chemin d’accès relatif à une icône de contour PNG 32x32 transparent.</span><span class="sxs-lookup"><span data-stu-id="280b2-222">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="280b2-223">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-223">2048 characters</span></span>|<span data-ttu-id="280b2-224">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-224">✔</span></span>|<span data-ttu-id="280b2-225">Chemin d’accès relatif à une icône PNG 192x192 couleur complète.</span><span class="sxs-lookup"><span data-stu-id="280b2-225">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="280b2-226">accentColor</span><span class="sxs-lookup"><span data-stu-id="280b2-226">accentColor</span></span>

<span data-ttu-id="280b2-227">Chaîne **obligatoire** &ndash;</span><span class="sxs-lookup"><span data-stu-id="280b2-227">**Required** &ndash; String</span></span>

<span data-ttu-id="280b2-228">Couleur à utiliser en combinaison avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="280b2-228">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="280b2-229">La valeur doit être un code de couleur HTML valide commençant par « # », par `#4464ee`exemple.</span><span class="sxs-lookup"><span data-stu-id="280b2-229">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="280b2-230">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="280b2-230">configurableTabs</span></span>

<span data-ttu-id="280b2-231">**Optional**</span><span class="sxs-lookup"><span data-stu-id="280b2-231">**Optional**</span></span>

<span data-ttu-id="280b2-232">Utilisé lorsque l’expérience de votre application dispose d’un onglet Channel Team qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="280b2-232">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="280b2-233">Les onglets configurables sont pris en charge uniquement dans l’étendue teams et un seul onglet par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="280b2-233">Configurable tabs are supported only in the teams scope, and currently only one tab per app is supported.</span></span>

<span data-ttu-id="280b2-234">L’objet est un tableau contenant tous les éléments du type `object`.</span><span class="sxs-lookup"><span data-stu-id="280b2-234">The object is an array with all elements of the type `object`.</span></span> <span data-ttu-id="280b2-235">Ce bloc est requis uniquement pour les solutions qui fournissent une solution de sous-onglet canal configurable.</span><span class="sxs-lookup"><span data-stu-id="280b2-235">This block is required only for solutions that provide a configurable channel tab solution.</span></span>

|<span data-ttu-id="280b2-236">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-236">Name</span></span>| <span data-ttu-id="280b2-237">Type</span><span class="sxs-lookup"><span data-stu-id="280b2-237">Type</span></span>| <span data-ttu-id="280b2-238">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-238">Maximum size</span></span> | <span data-ttu-id="280b2-239">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-239">Required</span></span> | <span data-ttu-id="280b2-240">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-240">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="280b2-241">String</span><span class="sxs-lookup"><span data-stu-id="280b2-241">String</span></span>|<span data-ttu-id="280b2-242">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-242">2048 characters</span></span>|<span data-ttu-id="280b2-243">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-243">✔</span></span>|<span data-ttu-id="280b2-244">URL https://à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="280b2-244">The https:// URL to use when configuring the tab.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="280b2-245">Boolean</span><span class="sxs-lookup"><span data-stu-id="280b2-245">Boolean</span></span>|||<span data-ttu-id="280b2-246">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="280b2-246">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="280b2-247">Default`true`</span><span class="sxs-lookup"><span data-stu-id="280b2-247">Default: `true`</span></span>|
|`scopes`|<span data-ttu-id="280b2-248">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="280b2-248">Array of enum</span></span>|<span data-ttu-id="280b2-249">1 </span><span class="sxs-lookup"><span data-stu-id="280b2-249">1</span></span>|<span data-ttu-id="280b2-250">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-250">✔</span></span>|<span data-ttu-id="280b2-251">Actuellement, les onglets configurables prennent `team` en `groupchat` charge uniquement les étendues et.</span><span class="sxs-lookup"><span data-stu-id="280b2-251">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`sharePointPreviewImage`|<span data-ttu-id="280b2-252">String</span><span class="sxs-lookup"><span data-stu-id="280b2-252">String</span></span>|<span data-ttu-id="280b2-253">2048</span><span class="sxs-lookup"><span data-stu-id="280b2-253">2048</span></span>||<span data-ttu-id="280b2-254">Chemin d’accès relatif à une image d’aperçu de tabulation à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="280b2-254">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="280b2-255">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="280b2-255">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="280b2-256">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="280b2-256">Array of enum</span></span>|<span data-ttu-id="280b2-257">1 </span><span class="sxs-lookup"><span data-stu-id="280b2-257">1</span></span>||<span data-ttu-id="280b2-258">Définit la manière dont votre onglet sera disponible dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="280b2-258">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="280b2-259">Les options `sharePointFullPage` sont et`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="280b2-259">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="280b2-260">staticTabs</span><span class="sxs-lookup"><span data-stu-id="280b2-260">staticTabs</span></span>

<span data-ttu-id="280b2-261">**Optional**</span><span class="sxs-lookup"><span data-stu-id="280b2-261">**Optional**</span></span>

<span data-ttu-id="280b2-262">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur ne les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="280b2-262">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="280b2-263">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="280b2-263">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="280b2-264">Les onglets statiques `team` déclarés dans l’étendue ne sont pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="280b2-264">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="280b2-265">L’objet est un tableau (au maximum 16 éléments) avec tous les éléments du type `object`.</span><span class="sxs-lookup"><span data-stu-id="280b2-265">The object is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="280b2-266">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="280b2-266">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="280b2-267">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-267">Name</span></span>| <span data-ttu-id="280b2-268">Type</span><span class="sxs-lookup"><span data-stu-id="280b2-268">Type</span></span>| <span data-ttu-id="280b2-269">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-269">Maximum size</span></span> | <span data-ttu-id="280b2-270">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-270">Required</span></span> | <span data-ttu-id="280b2-271">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-271">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="280b2-272">String</span><span class="sxs-lookup"><span data-stu-id="280b2-272">String</span></span>|<span data-ttu-id="280b2-273">64 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-273">64 characters</span></span>|<span data-ttu-id="280b2-274">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-274">✔</span></span>|<span data-ttu-id="280b2-275">Identificateur unique de l’entité que l’onglet affiche.</span><span class="sxs-lookup"><span data-stu-id="280b2-275">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="280b2-276">String</span><span class="sxs-lookup"><span data-stu-id="280b2-276">String</span></span>|<span data-ttu-id="280b2-277">128 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-277">128 characters</span></span>|<span data-ttu-id="280b2-278">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-278">✔</span></span>|<span data-ttu-id="280b2-279">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="280b2-279">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="280b2-280">String</span><span class="sxs-lookup"><span data-stu-id="280b2-280">String</span></span>|<span data-ttu-id="280b2-281">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-281">2048 characters</span></span>|<span data-ttu-id="280b2-282">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-282">✔</span></span>|<span data-ttu-id="280b2-283">URL https://qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de dessin de teams.</span><span class="sxs-lookup"><span data-stu-id="280b2-283">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="280b2-284">String</span><span class="sxs-lookup"><span data-stu-id="280b2-284">String</span></span>|<span data-ttu-id="280b2-285">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-285">2048 characters</span></span>||<span data-ttu-id="280b2-286">URL https://vers laquelle pointer si un utilisateur choisit de l’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="280b2-286">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="280b2-287">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="280b2-287">Array of enum</span></span>|<span data-ttu-id="280b2-288">1 </span><span class="sxs-lookup"><span data-stu-id="280b2-288">1</span></span>|<span data-ttu-id="280b2-289">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-289">✔</span></span>|<span data-ttu-id="280b2-290">Actuellement, les onglets statiques `personal` prennent en charge uniquement l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="280b2-290">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="280b2-291">Si vos onglets nécessitent des informations contextuelles pour afficher le contenu pertinent ou pour initier un flux d’authentification, *reportez-vous* à [la rubrique obtenir le contexte de votre onglet Microsoft teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="280b2-291">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="280b2-292">bots</span><span class="sxs-lookup"><span data-stu-id="280b2-292">bots</span></span>

<span data-ttu-id="280b2-293">**Optional**</span><span class="sxs-lookup"><span data-stu-id="280b2-293">**Optional**</span></span>

<span data-ttu-id="280b2-294">Définit une solution de robot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="280b2-294">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="280b2-295">L’objet est un tableau (maximum d’un seul élément&mdash;, actuellement un seul bot est autorisé par application) à tous les éléments du `object`type.</span><span class="sxs-lookup"><span data-stu-id="280b2-295">The object is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="280b2-296">Ce bloc est requis uniquement pour les solutions qui fournissent une expérience de robot.</span><span class="sxs-lookup"><span data-stu-id="280b2-296">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="280b2-297">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-297">Name</span></span>| <span data-ttu-id="280b2-298">Type</span><span class="sxs-lookup"><span data-stu-id="280b2-298">Type</span></span>| <span data-ttu-id="280b2-299">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-299">Maximum size</span></span> | <span data-ttu-id="280b2-300">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-300">Required</span></span> | <span data-ttu-id="280b2-301">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-301">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="280b2-302">String</span><span class="sxs-lookup"><span data-stu-id="280b2-302">String</span></span>|<span data-ttu-id="280b2-303">64 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-303">64 characters</span></span>|<span data-ttu-id="280b2-304">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-304">✔</span></span>|<span data-ttu-id="280b2-305">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="280b2-305">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="280b2-306">Il peut s’agir de la même chose que l' [ID d’application](#id)global.</span><span class="sxs-lookup"><span data-stu-id="280b2-306">This may well be the same as the overall [app ID](#id).</span></span>|
|`needsChannelSelector`|<span data-ttu-id="280b2-307">Boolean</span><span class="sxs-lookup"><span data-stu-id="280b2-307">Boolean</span></span>|||<span data-ttu-id="280b2-308">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="280b2-308">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="280b2-309">Default`false`</span><span class="sxs-lookup"><span data-stu-id="280b2-309">Default: `false`</span></span>|
|`isNotificationOnly`|<span data-ttu-id="280b2-310">Boolean</span><span class="sxs-lookup"><span data-stu-id="280b2-310">Boolean</span></span>|||<span data-ttu-id="280b2-311">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="280b2-311">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="280b2-312">Default`false`</span><span class="sxs-lookup"><span data-stu-id="280b2-312">Default: `false`</span></span>|
|`supportsFiles`|<span data-ttu-id="280b2-313">Boolean</span><span class="sxs-lookup"><span data-stu-id="280b2-313">Boolean</span></span>|||<span data-ttu-id="280b2-314">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="280b2-314">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="280b2-315">Default`false`</span><span class="sxs-lookup"><span data-stu-id="280b2-315">Default: `false`</span></span>|
|`scopes`|<span data-ttu-id="280b2-316">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="280b2-316">Array of enum</span></span>|<span data-ttu-id="280b2-317">3 </span><span class="sxs-lookup"><span data-stu-id="280b2-317">3</span></span>|<span data-ttu-id="280b2-318">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-318">✔</span></span>|<span data-ttu-id="280b2-319">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="280b2-319">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="280b2-320">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="280b2-320">These options are non-exclusive.</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="280b2-321">bots. commandLists</span><span class="sxs-lookup"><span data-stu-id="280b2-321">bots.commandLists</span></span>

<span data-ttu-id="280b2-322">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="280b2-322">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="280b2-323">L’objet est un tableau (nombre maximal de 2 éléments) avec tous les éléments `object`de type ; vous devez définir une liste de commandes distincte pour chaque étendue prise en charge par votre bot.</span><span class="sxs-lookup"><span data-stu-id="280b2-323">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="280b2-324">Pour plus d’informations, voir [menus de bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="280b2-324">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="280b2-325">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-325">Name</span></span>| <span data-ttu-id="280b2-326">Type</span><span class="sxs-lookup"><span data-stu-id="280b2-326">Type</span></span>| <span data-ttu-id="280b2-327">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-327">Maximum size</span></span> | <span data-ttu-id="280b2-328">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-328">Required</span></span> | <span data-ttu-id="280b2-329">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-329">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="280b2-330">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="280b2-330">array of enum</span></span>|<span data-ttu-id="280b2-331">3 </span><span class="sxs-lookup"><span data-stu-id="280b2-331">3</span></span>|<span data-ttu-id="280b2-332">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-332">✔</span></span>|<span data-ttu-id="280b2-333">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="280b2-333">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="280b2-334">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="280b2-334">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="280b2-335">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="280b2-335">array of objects</span></span>|<span data-ttu-id="280b2-336">10 </span><span class="sxs-lookup"><span data-stu-id="280b2-336">10</span></span>|<span data-ttu-id="280b2-337">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-337">✔</span></span>|<span data-ttu-id="280b2-338">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="280b2-338">An array of commands the bot supports:</span></span><br><span data-ttu-id="280b2-339">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="280b2-339">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="280b2-340">`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)</span><span class="sxs-lookup"><span data-stu-id="280b2-340">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

## <a name="connectors"></a><span data-ttu-id="280b2-341">ceux</span><span class="sxs-lookup"><span data-stu-id="280b2-341">connectors</span></span>

<span data-ttu-id="280b2-342">**Optional**</span><span class="sxs-lookup"><span data-stu-id="280b2-342">**Optional**</span></span>

<span data-ttu-id="280b2-343">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="280b2-343">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="280b2-344">L’objet est un tableau (un maximum de 1 élément) avec tous les éléments `object`de type.</span><span class="sxs-lookup"><span data-stu-id="280b2-344">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="280b2-345">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="280b2-345">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="280b2-346">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-346">Name</span></span>| <span data-ttu-id="280b2-347">Type</span><span class="sxs-lookup"><span data-stu-id="280b2-347">Type</span></span>| <span data-ttu-id="280b2-348">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-348">Maximum size</span></span> | <span data-ttu-id="280b2-349">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-349">Required</span></span> | <span data-ttu-id="280b2-350">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-350">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="280b2-351">String</span><span class="sxs-lookup"><span data-stu-id="280b2-351">String</span></span>|<span data-ttu-id="280b2-352">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-352">2048 characters</span></span>|<span data-ttu-id="280b2-353">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-353">✔</span></span>|<span data-ttu-id="280b2-354">URL https://à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="280b2-354">The https:// URL to use when configuring the connector.</span></span>|
|`connectorId`|<span data-ttu-id="280b2-355">String</span><span class="sxs-lookup"><span data-stu-id="280b2-355">String</span></span>|<span data-ttu-id="280b2-356">64 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-356">64 characters</span></span>|<span data-ttu-id="280b2-357">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-357">✔</span></span>|<span data-ttu-id="280b2-358">Identificateur unique du connecteur correspondant à son ID dans le [tableau de bord du développeur de connecteurs](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="280b2-358">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|
|`scopes`|<span data-ttu-id="280b2-359">Tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="280b2-359">Array of enum</span></span>|<span data-ttu-id="280b2-360">1 </span><span class="sxs-lookup"><span data-stu-id="280b2-360">1</span></span>|<span data-ttu-id="280b2-361">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-361">✔</span></span>|<span data-ttu-id="280b2-362">Indique si le connecteur offre une expérience dans le contexte d’un canal dans un `team`, ou une expérience étendue à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="280b2-362">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="280b2-363">Actuellement, seule l' `team` étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="280b2-363">Currently, only the `team` scope is supported.</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="280b2-364">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="280b2-364">composeExtensions</span></span>

<span data-ttu-id="280b2-365">**Optional**</span><span class="sxs-lookup"><span data-stu-id="280b2-365">**Optional**</span></span>

<span data-ttu-id="280b2-366">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="280b2-366">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="280b2-367">Le nom de la fonctionnalité a été modifié de « extension de composition » en « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même afin que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="280b2-367">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="280b2-368">L’objet est un tableau (un maximum de 1 élément) avec tous les éléments `object`de type.</span><span class="sxs-lookup"><span data-stu-id="280b2-368">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="280b2-369">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="280b2-369">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="280b2-370">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-370">Name</span></span>| <span data-ttu-id="280b2-371">Type</span><span class="sxs-lookup"><span data-stu-id="280b2-371">Type</span></span> | <span data-ttu-id="280b2-372">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-372">Maximum Size</span></span> | <span data-ttu-id="280b2-373">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="280b2-373">Required</span></span> | <span data-ttu-id="280b2-374">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-374">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="280b2-375">String</span><span class="sxs-lookup"><span data-stu-id="280b2-375">String</span></span>|<span data-ttu-id="280b2-376">64</span><span class="sxs-lookup"><span data-stu-id="280b2-376">64</span></span>|<span data-ttu-id="280b2-377">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-377">✔</span></span>|<span data-ttu-id="280b2-378">ID d’application Microsoft unique pour le bot qui sauvegarde l’extension de messagerie, tel qu’inscrit auprès de l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="280b2-378">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="280b2-379">Il peut s’agir de la même chose que l’ID d’application global.</span><span class="sxs-lookup"><span data-stu-id="280b2-379">This may well be the same as the overall App ID.</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="280b2-380">Boolean</span><span class="sxs-lookup"><span data-stu-id="280b2-380">Boolean</span></span>|||<span data-ttu-id="280b2-381">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="280b2-381">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="280b2-382">La valeur par `false`défaut est.</span><span class="sxs-lookup"><span data-stu-id="280b2-382">The default is `false`.</span></span>|
|`commands`|<span data-ttu-id="280b2-383">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="280b2-383">Array of object</span></span>|<span data-ttu-id="280b2-384">10 </span><span class="sxs-lookup"><span data-stu-id="280b2-384">10</span></span>|<span data-ttu-id="280b2-385">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-385">✔</span></span>|<span data-ttu-id="280b2-386">Tableau de commandes prises en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="280b2-386">Array of commands the messaging extension supports</span></span>|
|`messageHandlers`|<span data-ttu-id="280b2-387">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="280b2-387">Array of Objects</span></span>|<span data-ttu-id="280b2-388">5 </span><span class="sxs-lookup"><span data-stu-id="280b2-388">5</span></span>||<span data-ttu-id="280b2-389">Liste de gestionnaires permettant d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="280b2-389">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="280b2-390">Les domaines doivent également être affichés dans`validDomains`</span><span class="sxs-lookup"><span data-stu-id="280b2-390">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="280b2-391">String</span><span class="sxs-lookup"><span data-stu-id="280b2-391">String</span></span>|||<span data-ttu-id="280b2-392">Type de gestionnaire de messages.</span><span class="sxs-lookup"><span data-stu-id="280b2-392">The type of message handler.</span></span> <span data-ttu-id="280b2-393">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="280b2-393">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="280b2-394">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="280b2-394">Array of Strings</span></span>|||<span data-ttu-id="280b2-395">Tableau de domaines pour lesquels le gestionnaire de messages de liaison peut s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="280b2-395">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="280b2-396">composeExtensions. Commands</span><span class="sxs-lookup"><span data-stu-id="280b2-396">composeExtensions.commands</span></span>

<span data-ttu-id="280b2-397">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="280b2-397">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="280b2-398">Chaque commande apparaît dans Microsoft teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="280b2-398">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="280b2-399">Il y a un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="280b2-399">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="280b2-400">Chaque élément de commande est un objet de la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="280b2-400">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="280b2-401">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-401">Name</span></span>| <span data-ttu-id="280b2-402">Type</span><span class="sxs-lookup"><span data-stu-id="280b2-402">Type</span></span>| <span data-ttu-id="280b2-403">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-403">Maximum size</span></span> | <span data-ttu-id="280b2-404">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-404">Required</span></span> | <span data-ttu-id="280b2-405">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-405">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="280b2-406">String</span><span class="sxs-lookup"><span data-stu-id="280b2-406">String</span></span>|<span data-ttu-id="280b2-407">64 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-407">64 characters</span></span>|<span data-ttu-id="280b2-408">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-408">✔</span></span>|<span data-ttu-id="280b2-409">ID de la commande</span><span class="sxs-lookup"><span data-stu-id="280b2-409">The ID for the command</span></span>|
|`type`|<span data-ttu-id="280b2-410">String</span><span class="sxs-lookup"><span data-stu-id="280b2-410">String</span></span>|<span data-ttu-id="280b2-411">64 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-411">64 characters</span></span>||<span data-ttu-id="280b2-412">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="280b2-412">Type of the command.</span></span> <span data-ttu-id="280b2-413">L’une `query` ou `action`l’autre.</span><span class="sxs-lookup"><span data-stu-id="280b2-413">One of `query` or `action`.</span></span> <span data-ttu-id="280b2-414">Default`query`</span><span class="sxs-lookup"><span data-stu-id="280b2-414">Default: `query`</span></span>|
|`title`|<span data-ttu-id="280b2-415">String</span><span class="sxs-lookup"><span data-stu-id="280b2-415">String</span></span>|<span data-ttu-id="280b2-416">32 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-416">32 characters</span></span>|<span data-ttu-id="280b2-417">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-417">✔</span></span>|<span data-ttu-id="280b2-418">Nom de commande convivial</span><span class="sxs-lookup"><span data-stu-id="280b2-418">The user-friendly command name</span></span>|
|`description`|<span data-ttu-id="280b2-419">String</span><span class="sxs-lookup"><span data-stu-id="280b2-419">String</span></span>|<span data-ttu-id="280b2-420">128 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-420">128 characters</span></span>||<span data-ttu-id="280b2-421">La description qui s’affiche pour les utilisateurs afin d’indiquer la finalité de cette commande.</span><span class="sxs-lookup"><span data-stu-id="280b2-421">The description that appears to users to indicate the purpose of this command</span></span>|
|`initialRun`|<span data-ttu-id="280b2-422">Boolean</span><span class="sxs-lookup"><span data-stu-id="280b2-422">Boolean</span></span>|||<span data-ttu-id="280b2-423">Valeur booléenne indiquant si la commande doit être exécutée initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="280b2-423">A Boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="280b2-424">Default`false`</span><span class="sxs-lookup"><span data-stu-id="280b2-424">Default: `false`</span></span>|
|`context`|<span data-ttu-id="280b2-425">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="280b2-425">Array of Strings</span></span>|<span data-ttu-id="280b2-426">3 </span><span class="sxs-lookup"><span data-stu-id="280b2-426">3</span></span>||<span data-ttu-id="280b2-427">Définit l’emplacement à partir duquel l’extension de message peut être appelée.</span><span class="sxs-lookup"><span data-stu-id="280b2-427">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="280b2-428">Toute combinaison de `compose`, `commandBox`, `message`.</span><span class="sxs-lookup"><span data-stu-id="280b2-428">Any combination of `compose`, `commandBox`, `message`.</span></span> <span data-ttu-id="280b2-429">Valeur par défaut est`["compose", "commandBox"]`</span><span class="sxs-lookup"><span data-stu-id="280b2-429">Default is `["compose", "commandBox"]`</span></span>|
|`fetchTask`|<span data-ttu-id="280b2-430">Boolean</span><span class="sxs-lookup"><span data-stu-id="280b2-430">Boolean</span></span>|||<span data-ttu-id="280b2-431">Une valeur booléenne qui indique s’il doit extraire le module de tâches de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="280b2-431">A boolean value that indicates if it should fetch the task module dynamically</span></span>|
|`taskInfo`|<span data-ttu-id="280b2-432">Objet</span><span class="sxs-lookup"><span data-stu-id="280b2-432">Object</span></span>|||<span data-ttu-id="280b2-433">Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="280b2-433">Specify the task module to preload when using a messaging extension command</span></span>|
|`taskInfo.title`|<span data-ttu-id="280b2-434">String</span><span class="sxs-lookup"><span data-stu-id="280b2-434">String</span></span>|<span data-ttu-id="280b2-435">64</span><span class="sxs-lookup"><span data-stu-id="280b2-435">64</span></span>||<span data-ttu-id="280b2-436">Titre de la boîte de dialogue initiale</span><span class="sxs-lookup"><span data-stu-id="280b2-436">Initial dialog title</span></span>|
|`taskInfo.width`|<span data-ttu-id="280b2-437">String</span><span class="sxs-lookup"><span data-stu-id="280b2-437">String</span></span>|||<span data-ttu-id="280b2-438">Largeur de la boîte de dialogue-soit un nombre en pixels, soit une mise en page par défaut telle que « grande », « moyen » ou « petite »</span><span class="sxs-lookup"><span data-stu-id="280b2-438">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.height`|<span data-ttu-id="280b2-439">String</span><span class="sxs-lookup"><span data-stu-id="280b2-439">String</span></span>|||<span data-ttu-id="280b2-440">Hauteur de la boîte de dialogue : nombre en pixels ou mise en page par défaut, par exemple, « grande », « moyen » ou « petite »</span><span class="sxs-lookup"><span data-stu-id="280b2-440">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|
|`taskInfo.url`|<span data-ttu-id="280b2-441">String</span><span class="sxs-lookup"><span data-stu-id="280b2-441">String</span></span>|||<span data-ttu-id="280b2-442">URL d’affichage WebView initiale</span><span class="sxs-lookup"><span data-stu-id="280b2-442">Initial webview URL</span></span>|
|`parameters`|<span data-ttu-id="280b2-443">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="280b2-443">Array of object</span></span>|<span data-ttu-id="280b2-444">5 </span><span class="sxs-lookup"><span data-stu-id="280b2-444">5</span></span>|<span data-ttu-id="280b2-445">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-445">✔</span></span>|<span data-ttu-id="280b2-446">La liste des paramètres que la commande prend.</span><span class="sxs-lookup"><span data-stu-id="280b2-446">The list of parameters the command takes.</span></span> <span data-ttu-id="280b2-447">Minimum : 1 ; maximum : 5</span><span class="sxs-lookup"><span data-stu-id="280b2-447">Minimum: 1; maximum: 5</span></span>|
|`parameter.name`|<span data-ttu-id="280b2-448">String</span><span class="sxs-lookup"><span data-stu-id="280b2-448">String</span></span>|<span data-ttu-id="280b2-449">64 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-449">64 characters</span></span>|<span data-ttu-id="280b2-450">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-450">✔</span></span>|<span data-ttu-id="280b2-451">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="280b2-451">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="280b2-452">Elle est incluse dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="280b2-452">This is included in the user request.</span></span>|
|`parameter.title`|<span data-ttu-id="280b2-453">String</span><span class="sxs-lookup"><span data-stu-id="280b2-453">String</span></span>|<span data-ttu-id="280b2-454">32 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-454">32 characters</span></span>|<span data-ttu-id="280b2-455">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-455">✔</span></span>|<span data-ttu-id="280b2-456">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="280b2-456">User-friendly title for the parameter.</span></span>|
|`parameter.description`|<span data-ttu-id="280b2-457">String</span><span class="sxs-lookup"><span data-stu-id="280b2-457">String</span></span>|<span data-ttu-id="280b2-458">128 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-458">128 characters</span></span>||<span data-ttu-id="280b2-459">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="280b2-459">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameter.inputType`|<span data-ttu-id="280b2-460">String</span><span class="sxs-lookup"><span data-stu-id="280b2-460">String</span></span>|<span data-ttu-id="280b2-461">128 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-461">128 characters</span></span>||<span data-ttu-id="280b2-462">Définit le type de contrôle affiché sur un module de tâche `fetchTask: true`pour.</span><span class="sxs-lookup"><span data-stu-id="280b2-462">Defines the type of control displayed on a task module for `fetchTask: true`.</span></span> <span data-ttu-id="280b2-463">`text` `textarea` `number`, `date`,, `time` `toggle``choiceset`</span><span class="sxs-lookup"><span data-stu-id="280b2-463">One of `text`, `textarea`, `number`, `date`, `time`, `toggle`, `choiceset`</span></span>|
|`parameter.choices`|<span data-ttu-id="280b2-464">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="280b2-464">Array of Objects</span></span>|<span data-ttu-id="280b2-465">10 </span><span class="sxs-lookup"><span data-stu-id="280b2-465">10</span></span>||<span data-ttu-id="280b2-466">Options de choix pour le `choiceset`.</span><span class="sxs-lookup"><span data-stu-id="280b2-466">The choice options for the `choiceset`.</span></span> <span data-ttu-id="280b2-467">À utiliser uniquement `parameter.inputType` lorsque est`choiceset`</span><span class="sxs-lookup"><span data-stu-id="280b2-467">Use only when `parameter.inputType` is `choiceset`</span></span>|
|`parameter.choices.title`|<span data-ttu-id="280b2-468">String</span><span class="sxs-lookup"><span data-stu-id="280b2-468">String</span></span>|<span data-ttu-id="280b2-469">128</span><span class="sxs-lookup"><span data-stu-id="280b2-469">128</span></span>||<span data-ttu-id="280b2-470">Titre du choix</span><span class="sxs-lookup"><span data-stu-id="280b2-470">Title of the choice</span></span>|
|`parameter.choices.value`|<span data-ttu-id="280b2-471">String</span><span class="sxs-lookup"><span data-stu-id="280b2-471">String</span></span>|<span data-ttu-id="280b2-472">512</span><span class="sxs-lookup"><span data-stu-id="280b2-472">512</span></span>||<span data-ttu-id="280b2-473">Valeur du choix</span><span class="sxs-lookup"><span data-stu-id="280b2-473">Value of the choice</span></span>|

## <a name="permissions"></a><span data-ttu-id="280b2-474">autorisations</span><span class="sxs-lookup"><span data-stu-id="280b2-474">permissions</span></span>

<span data-ttu-id="280b2-475">**Optional**</span><span class="sxs-lookup"><span data-stu-id="280b2-475">**Optional**</span></span>

<span data-ttu-id="280b2-476">Un tableau `string` qui spécifie les autorisations demandées par l’application, ce qui permet aux utilisateurs finaux de savoir comment effectuer l’extension.</span><span class="sxs-lookup"><span data-stu-id="280b2-476">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="280b2-477">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="280b2-477">The following options are non-exclusive:</span></span>

* <span data-ttu-id="280b2-478">`identity`&emsp; Nécessite des informations d’identité d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="280b2-478">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="280b2-479">`messageTeamMembers`&emsp; Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="280b2-479">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="280b2-480">Si vous modifiez ces autorisations lors de la mise à jour de votre application, vos utilisateurs répéteront le processus de consentement la première fois qu’ils exécuteront l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="280b2-480">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="280b2-481">Pour plus d’informations, consultez [la rubrique mise à jour de votre application](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="280b2-481">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="280b2-482">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="280b2-482">devicePermissions</span></span>

<span data-ttu-id="280b2-483">**Facultatif** Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="280b2-483">**Optional** Array of Strings</span></span>

<span data-ttu-id="280b2-484">Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur auquel votre application peut demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="280b2-484">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="280b2-485">Les options sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="280b2-485">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="280b2-486">validDomains</span><span class="sxs-lookup"><span data-stu-id="280b2-486">validDomains</span></span>

<span data-ttu-id="280b2-487">**Facultatif** **, sauf indication contraire**</span><span class="sxs-lookup"><span data-stu-id="280b2-487">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="280b2-488">Une liste des domaines valides pour les sites Web que l’application prévoit de charger dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="280b2-488">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="280b2-489">Les listes de domaine peuvent inclure des caractères génériques `*.example.com`, par exemple.</span><span class="sxs-lookup"><span data-stu-id="280b2-489">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="280b2-490">Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com`.</span><span class="sxs-lookup"><span data-stu-id="280b2-490">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="280b2-491">Si la configuration de votre onglet ou de votre interface utilisateur de contenu doit accéder à un autre domaine en plus de celui utilisé pour la configuration d’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="280b2-491">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="280b2-492">Toutefois, il n’est **pas** nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="280b2-492">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="280b2-493">Par exemple, pour authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne `validDomains[]`devez pas inclure Accounts.google.com dans.</span><span class="sxs-lookup"><span data-stu-id="280b2-493">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="280b2-494">Les applications teams qui requièrent leurs propres URL SharePoint pour fonctionner correctement, peuvent inclure « {teamsitedomain} » dans leur liste de domaines valide.</span><span class="sxs-lookup"><span data-stu-id="280b2-494">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="280b2-495">N’ajoutez pas de domaines qui se trouvent en dehors de votre contrôle, soit directement, soit via des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="280b2-495">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="280b2-496">Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="280b2-496">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="280b2-497">L’objet est un tableau contenant tous les éléments du type `string`.</span><span class="sxs-lookup"><span data-stu-id="280b2-497">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="280b2-498">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="280b2-498">webApplicationInfo</span></span>

<span data-ttu-id="280b2-499">**Optional**</span><span class="sxs-lookup"><span data-stu-id="280b2-499">**Optional**</span></span>

<span data-ttu-id="280b2-500">Spécifiez l’ID de votre application AAD et les informations graphiques pour aider les utilisateurs à se connecter à votre application AAD de manière transparente.</span><span class="sxs-lookup"><span data-stu-id="280b2-500">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="280b2-501">Nom</span><span class="sxs-lookup"><span data-stu-id="280b2-501">Name</span></span>| <span data-ttu-id="280b2-502">Type</span><span class="sxs-lookup"><span data-stu-id="280b2-502">Type</span></span>| <span data-ttu-id="280b2-503">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="280b2-503">Maximum size</span></span> | <span data-ttu-id="280b2-504">Requis</span><span class="sxs-lookup"><span data-stu-id="280b2-504">Required</span></span> | <span data-ttu-id="280b2-505">Description</span><span class="sxs-lookup"><span data-stu-id="280b2-505">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="280b2-506">String</span><span class="sxs-lookup"><span data-stu-id="280b2-506">String</span></span>|<span data-ttu-id="280b2-507">36 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-507">36 characters</span></span>|<span data-ttu-id="280b2-508">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-508">✔</span></span>|<span data-ttu-id="280b2-509">ID de l’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="280b2-509">AAD application id of the app.</span></span> <span data-ttu-id="280b2-510">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="280b2-510">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="280b2-511">String</span><span class="sxs-lookup"><span data-stu-id="280b2-511">String</span></span>|<span data-ttu-id="280b2-512">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="280b2-512">2048 characters</span></span>|<span data-ttu-id="280b2-513">✔</span><span class="sxs-lookup"><span data-stu-id="280b2-513">✔</span></span>|<span data-ttu-id="280b2-514">URL de ressource de l’application pour l’acquisition du jeton d’authentification pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="280b2-514">Resource url of app for acquiring auth token for SSO.</span></span>|
