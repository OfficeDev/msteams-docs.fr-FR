---
title: Référence du schéma de manifeste
description: Décrit le schéma pris en charge par le manifeste pour Microsoft teams
keywords: schéma de manifeste teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: b67b23278a2d2bbb2b24c0e828f01cf1789c6191
ms.sourcegitcommit: bac0226d9048c363d96bbaf6f5395388c5f5c45a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2020
ms.locfileid: "45039285"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="58721-104">Référence : schéma de manifeste pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="58721-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="58721-105">Le manifeste Microsoft teams décrit la façon dont l’application s’intègre dans le produit Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="58721-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="58721-106">Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="58721-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="58721-107">Les versions précédentes 1.0 à 1.4 sont également prises en charge (à l’aide de « v1. x » dans l’URL).</span><span class="sxs-lookup"><span data-stu-id="58721-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="58721-108">L’exemple de schéma suivant montre toutes les options d’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="58721-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="58721-109">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="58721-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.7",
  "version": "1.0.0",
  "id": "%MICROSOFT-APP-ID%",
  "packageName": "com.example.myapp",
  "localizationInfo": {
    "defaultLanguageTag": "en-us",
    "additionalLanguages": [
      {
        "languageTag": "es-es",
        "file": "en-us.json"
      }
    ]
  },
  "developer": {
    "name": "Publisher Name",
    "websiteUrl": "https://website.com/",
    "privacyUrl": "https://website.com/privacy",
    "termsOfUseUrl": "https://website.com/app-tos",
    "mpnId": "1234567890"
  },
  "name": {
    "short": "Name of your app (<=30 chars)",
    "full": "Full name of app, if longer than 30 characters (<=100 chars)"
  },
  "description": {
    "short": "Short description of your app (<= 80 chars)",
    "full": "Full description of your app (<= 4000 chars)"
  },
  "icons": {
    "outline": "A relative path to a transparent .png icon — 32px X 32px",
    "color": "A relative path to a full color .png icon — 192px X 192px"
  },
  "accentColor": "A valid HTML color code.",
  "configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "scopes": [
        "team",
        "groupchat"
      ],
      "canUpdateConfiguration": true,
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": "Define how your tab wil be made available in SharePoint (full page or web part)"
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser"
    }
  ],
  "bots": [
    {
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "scopes": [
        "team",
        "personal",
        "groupchat"
      ],
      "needsChannelSelector": false,
      "isNotificationOnly": false,
      "supportsFiles": true,
      "commandLists": [
        {
          "scopes": [
            "team",
            "groupchat"
          ],
          "commands": [
            {
              "title": "Command 1",
              "description": "Description of Command 1"
            },
            {
              "title": "Command 2",
              "description": "Description of Command 2"
            }
          ]
        },
        {
          "scopes": [
            "personal",
            "groupchat"
          ],
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
      "scopes": [
        "team"
      ],
      "configurationUrl": "https://contoso.com/teamsconnector/configure"
    }
  ],
  "composeExtensions": [
    {
      "canUpdateConfiguration": true,
      "botId": "%MICROSOFT-APP-ID-REGISTERED-WITH-BOT-FRAMEWORK%",
      "commands": [
        {
          "id": "exampleCmd1",
          "title": "Example Command",
          "type": "query",
          "context": [
            "compose",
            "commandBox"
          ],
          "description": "Command Description; e.g., Search on the web",
          "initialRun": true,
          "fetchTask": false,
          "parameters": [
            {
              "name": "keyword",
              "title": "Search keywords",
              "inputType": "text",
              "description": "Enter the keywords to search for",
              "value": "Initial value for the parameter",
              "choices": [
                {
                  "title": "Title of the choice",
                  "value": "Value of the choice"
                }
              ]
            }
          ]
        },
        {
          "id": "exampleCmd2",
          "title": "Example Command 2",
          "type": "action",
          "context": [
            "message"
          ],
          "description": "Command Description; e.g., Search for a customer",
          "initialRun": true,
          "fetchTask": true,
          "parameters": [
            {
              "name": "custinfo",
              "title": "Customer name",
              "description": "Enter a customer name",
              "inputType": "text"
            }
          ]
        }
      ],
      "taskInfo": {
        "title": "Initial dialog title",
        "width": "Dialog width",
        "height": "Dialog height",
        "url": "Initial webview URL"
      },
      "messageHandlers": [
        {
          "type": "link",
          "value": {
            "domains": [
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
  "devicePermissions": [
    "geolocation",
    "media",
    "notifications",
    "midi",
    "openExternal"
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
  "showLoadingIndicator": false,
  "isFullScreen": false,
  "activities": {
    "activityTypes": [
      {
        "type": "taskCreated",
        "description": "Task created activity",
        "templateText": "<team member> created task <taskId> for you"
      },
      {
        "type": "userMention",
        "description": "Personal mention activity",
        "templateText": "<team member> mentioned you"
      }
    ]
  }
}
```

<span data-ttu-id="58721-110">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="58721-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="58721-111">$schema</span><span class="sxs-lookup"><span data-stu-id="58721-111">$schema</span></span>

<span data-ttu-id="58721-112">*Facultatif, mais recommandé* — String</span><span class="sxs-lookup"><span data-stu-id="58721-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="58721-113">URL https://référençant le schéma JSON du manifeste.</span><span class="sxs-lookup"><span data-stu-id="58721-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="58721-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="58721-114">manifestVersion</span></span>

<span data-ttu-id="58721-115">**Required** — String</span><span class="sxs-lookup"><span data-stu-id="58721-115">**Required** — string</span></span>

<span data-ttu-id="58721-116">Version du schéma de manifeste utilisé par ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="58721-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="58721-117">Il doit être « 1,5 ».</span><span class="sxs-lookup"><span data-stu-id="58721-117">It should be "1.5".</span></span>

## <a name="version"></a><span data-ttu-id="58721-118">version</span><span class="sxs-lookup"><span data-stu-id="58721-118">version</span></span>

<span data-ttu-id="58721-119">**Required** — String</span><span class="sxs-lookup"><span data-stu-id="58721-119">**Required** — string</span></span>

<span data-ttu-id="58721-120">Version de l’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="58721-120">The version of the specific app.</span></span> <span data-ttu-id="58721-121">Si vous mettez à jour un événement dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="58721-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="58721-122">Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="58721-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="58721-123">Si cette application a été envoyée au magasin, le nouveau manifeste doit être soumis à nouveau et revalidé.</span><span class="sxs-lookup"><span data-stu-id="58721-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="58721-124">Ensuite, les utilisateurs de cette application obtiendront automatiquement le nouveau manifeste mis à jour en quelques heures, une fois celui-ci approuvé.</span><span class="sxs-lookup"><span data-stu-id="58721-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="58721-125">Si l’application a demandé une modification des autorisations, les utilisateurs sont invités à effectuer une mise à niveau et à reconfigurer l’application.</span><span class="sxs-lookup"><span data-stu-id="58721-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="58721-126">Cette chaîne de version doit suivre la norme [semver](http://semver.org/) (major. Petites. CORRECTIF).</span><span class="sxs-lookup"><span data-stu-id="58721-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="58721-127">id</span><span class="sxs-lookup"><span data-stu-id="58721-127">id</span></span>

<span data-ttu-id="58721-128">**Obligatoire** — ID de l’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="58721-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="58721-129">Identificateur unique généré par Microsoft pour cette application.</span><span class="sxs-lookup"><span data-stu-id="58721-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="58721-130">Si vous avez inscrit un robot via Microsoft bot Framework ou si l’application Web de votre onglet se connecte déjà à Microsoft, vous devez déjà avoir un ID et l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="58721-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="58721-131">Dans le cas contraire, vous devez générer un nouvel ID dans le portail d’inscription des applications Microsoft ([mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous ajoutez un bot. Remarque : Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="58721-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="58721-132">developer</span><span class="sxs-lookup"><span data-stu-id="58721-132">developer</span></span>

<span data-ttu-id="58721-133">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="58721-133">**Required** — object</span></span>

<span data-ttu-id="58721-134">Spécifie les informations relatives à votre société.</span><span class="sxs-lookup"><span data-stu-id="58721-134">Specifies information about your company.</span></span> <span data-ttu-id="58721-135">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="58721-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="58721-136">Pour plus d’informations, consultez nos [instructions de publication](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) .</span><span class="sxs-lookup"><span data-stu-id="58721-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="58721-137">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-137">Name</span></span>| <span data-ttu-id="58721-138">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-138">Maximum size</span></span> | <span data-ttu-id="58721-139">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-139">Required</span></span> | <span data-ttu-id="58721-140">Description</span><span class="sxs-lookup"><span data-stu-id="58721-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="58721-141">32 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-141">32 characters</span></span>|<span data-ttu-id="58721-142">✔</span><span class="sxs-lookup"><span data-stu-id="58721-142">✔</span></span>|<span data-ttu-id="58721-143">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="58721-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="58721-144">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-144">2048 characters</span></span>|<span data-ttu-id="58721-145">✔</span><span class="sxs-lookup"><span data-stu-id="58721-145">✔</span></span>|<span data-ttu-id="58721-146">URL https://vers le site Web du développeur.</span><span class="sxs-lookup"><span data-stu-id="58721-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="58721-147">Ce lien doit prendre les utilisateurs à la page d’accueil de votre entreprise ou de votre propre produit.</span><span class="sxs-lookup"><span data-stu-id="58721-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="58721-148">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-148">2048 characters</span></span>|<span data-ttu-id="58721-149">✔</span><span class="sxs-lookup"><span data-stu-id="58721-149">✔</span></span>|<span data-ttu-id="58721-150">URL https://vers la stratégie de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="58721-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="58721-151">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-151">2048 characters</span></span>|<span data-ttu-id="58721-152">✔</span><span class="sxs-lookup"><span data-stu-id="58721-152">✔</span></span>|<span data-ttu-id="58721-153">L’URL https://vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="58721-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="58721-154">10 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-154">10 characters</span></span>| |<span data-ttu-id="58721-155">**Facultatif** ID réseau du partenaire Microsoft qui identifie l’organisation partenaire qui crée l’application.</span><span class="sxs-lookup"><span data-stu-id="58721-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="58721-156">name</span><span class="sxs-lookup"><span data-stu-id="58721-156">name</span></span>

<span data-ttu-id="58721-157">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="58721-157">**Required** — object</span></span>

<span data-ttu-id="58721-158">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’expérience de teams.</span><span class="sxs-lookup"><span data-stu-id="58721-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="58721-159">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="58721-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="58721-160">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="58721-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="58721-161">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-161">Name</span></span>| <span data-ttu-id="58721-162">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-162">Maximum size</span></span> | <span data-ttu-id="58721-163">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-163">Required</span></span> | <span data-ttu-id="58721-164">Description</span><span class="sxs-lookup"><span data-stu-id="58721-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="58721-165">30 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-165">30 characters</span></span>|<span data-ttu-id="58721-166">✔</span><span class="sxs-lookup"><span data-stu-id="58721-166">✔</span></span>|<span data-ttu-id="58721-167">Nom complet court de l’application.</span><span class="sxs-lookup"><span data-stu-id="58721-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="58721-168">100 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-168">100 characters</span></span>||<span data-ttu-id="58721-169">Nom complet de l’application, utilisé si le nom complet de l’application dépasse les 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="58721-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="58721-170">description</span><span class="sxs-lookup"><span data-stu-id="58721-170">description</span></span>

<span data-ttu-id="58721-171">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="58721-171">**Required** — object</span></span>

<span data-ttu-id="58721-172">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="58721-172">Describes your app to users.</span></span> <span data-ttu-id="58721-173">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="58721-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="58721-174">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="58721-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="58721-175">Vous devez également noter, dans la description complète, si un compte externe est requis pour l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="58721-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="58721-176">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="58721-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="58721-177">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="58721-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="58721-178">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-178">Name</span></span>| <span data-ttu-id="58721-179">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-179">Maximum size</span></span> | <span data-ttu-id="58721-180">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-180">Required</span></span> | <span data-ttu-id="58721-181">Description</span><span class="sxs-lookup"><span data-stu-id="58721-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="58721-182">80 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-182">80 characters</span></span>|<span data-ttu-id="58721-183">✔</span><span class="sxs-lookup"><span data-stu-id="58721-183">✔</span></span>|<span data-ttu-id="58721-184">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="58721-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="58721-185">4000 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-185">4000 characters</span></span>|<span data-ttu-id="58721-186">✔</span><span class="sxs-lookup"><span data-stu-id="58721-186">✔</span></span>|<span data-ttu-id="58721-187">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="58721-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="58721-188">packageName</span><span class="sxs-lookup"><span data-stu-id="58721-188">packageName</span></span>

<span data-ttu-id="58721-189">**Facultatif** — String</span><span class="sxs-lookup"><span data-stu-id="58721-189">**Optional** — string</span></span>

<span data-ttu-id="58721-190">Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="58721-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="58721-191">Longueur maximale : 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="58721-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="58721-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="58721-192">localizationInfo</span></span>

<span data-ttu-id="58721-193">**Facultatif** — Object</span><span class="sxs-lookup"><span data-stu-id="58721-193">**Optional** — object</span></span>

<span data-ttu-id="58721-194">Permet de spécifier une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="58721-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="58721-195">Consultez la rubrique [Localization](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="58721-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="58721-196">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-196">Name</span></span>| <span data-ttu-id="58721-197">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-197">Maximum size</span></span> | <span data-ttu-id="58721-198">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-198">Required</span></span> | <span data-ttu-id="58721-199">Description</span><span class="sxs-lookup"><span data-stu-id="58721-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="58721-200">✔</span><span class="sxs-lookup"><span data-stu-id="58721-200">✔</span></span>|<span data-ttu-id="58721-201">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="58721-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="58721-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="58721-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="58721-203">Tableau d’objets spécifiant des traductions de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="58721-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="58721-204">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-204">Name</span></span>| <span data-ttu-id="58721-205">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-205">Maximum size</span></span> | <span data-ttu-id="58721-206">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-206">Required</span></span> | <span data-ttu-id="58721-207">Description</span><span class="sxs-lookup"><span data-stu-id="58721-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="58721-208">✔</span><span class="sxs-lookup"><span data-stu-id="58721-208">✔</span></span>|<span data-ttu-id="58721-209">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="58721-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="58721-210">✔</span><span class="sxs-lookup"><span data-stu-id="58721-210">✔</span></span>|<span data-ttu-id="58721-211">Chemin d’accès relatif à un fichier. JSON contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="58721-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="58721-212">icons</span><span class="sxs-lookup"><span data-stu-id="58721-212">icons</span></span>

<span data-ttu-id="58721-213">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="58721-213">**Required** — object</span></span>

<span data-ttu-id="58721-214">Icônes utilisées dans l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="58721-214">Icons used within the Teams app.</span></span> <span data-ttu-id="58721-215">Les fichiers d’icône doivent être inclus dans le package de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="58721-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="58721-216">Pour plus d’informations, consultez la rubrique [Icons](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="58721-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="58721-217">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-217">Name</span></span>| <span data-ttu-id="58721-218">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-218">Maximum size</span></span> | <span data-ttu-id="58721-219">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-219">Required</span></span> | <span data-ttu-id="58721-220">Description</span><span class="sxs-lookup"><span data-stu-id="58721-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="58721-221">32 x 32 pixels</span><span class="sxs-lookup"><span data-stu-id="58721-221">32 x 32 pixels</span></span>|<span data-ttu-id="58721-222">✔</span><span class="sxs-lookup"><span data-stu-id="58721-222">✔</span></span>|<span data-ttu-id="58721-223">Chemin d’accès relatif à une icône de contour PNG 32x32 transparent.</span><span class="sxs-lookup"><span data-stu-id="58721-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="58721-224">192 x 192 pixels</span><span class="sxs-lookup"><span data-stu-id="58721-224">192 x 192 pixels</span></span>|<span data-ttu-id="58721-225">✔</span><span class="sxs-lookup"><span data-stu-id="58721-225">✔</span></span>|<span data-ttu-id="58721-226">Chemin d’accès relatif à une icône PNG 192x192 couleur complète.</span><span class="sxs-lookup"><span data-stu-id="58721-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="58721-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="58721-227">accentColor</span></span>

<span data-ttu-id="58721-228">**Facultatif** — code couleur hexadécimal html</span><span class="sxs-lookup"><span data-stu-id="58721-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="58721-229">Couleur à utiliser en combinaison avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="58721-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="58721-230">La valeur doit être un code de couleur HTML valide commençant par « # », par exemple `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="58721-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="58721-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="58721-231">configurableTabs</span></span>

<span data-ttu-id="58721-232">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="58721-232">**Optional** — array</span></span>

<span data-ttu-id="58721-233">Utilisé lorsque l’expérience de votre application dispose d’un onglet Channel Team qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="58721-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="58721-234">Les onglets configurables sont pris en charge uniquement dans l’étendue Teams (non personnel) et **un** seul onglet par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="58721-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="58721-235">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-235">Name</span></span>| <span data-ttu-id="58721-236">Type</span><span class="sxs-lookup"><span data-stu-id="58721-236">Type</span></span>| <span data-ttu-id="58721-237">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-237">Maximum size</span></span> | <span data-ttu-id="58721-238">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-238">Required</span></span> | <span data-ttu-id="58721-239">Description</span><span class="sxs-lookup"><span data-stu-id="58721-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="58721-240">string</span><span class="sxs-lookup"><span data-stu-id="58721-240">string</span></span>|<span data-ttu-id="58721-241">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-241">2048 characters</span></span>|<span data-ttu-id="58721-242">✔</span><span class="sxs-lookup"><span data-stu-id="58721-242">✔</span></span>|<span data-ttu-id="58721-243">URL https://à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="58721-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="58721-244">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="58721-244">array of enum</span></span>|<span data-ttu-id="58721-245">1 </span><span class="sxs-lookup"><span data-stu-id="58721-245">1</span></span>|<span data-ttu-id="58721-246">✔</span><span class="sxs-lookup"><span data-stu-id="58721-246">✔</span></span>|<span data-ttu-id="58721-247">Actuellement, les onglets configurables prennent en charge uniquement les `team` `groupchat` étendues et.</span><span class="sxs-lookup"><span data-stu-id="58721-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="58721-248">booléen</span><span class="sxs-lookup"><span data-stu-id="58721-248">boolean</span></span>|||<span data-ttu-id="58721-249">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="58721-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="58721-250">Valeur par défaut : **true**.</span><span class="sxs-lookup"><span data-stu-id="58721-250">Default: **true**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="58721-251">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-251">string</span></span>|<span data-ttu-id="58721-252">2048</span><span class="sxs-lookup"><span data-stu-id="58721-252">2048</span></span>||<span data-ttu-id="58721-253">Chemin d’accès relatif à une image d’aperçu de tabulation à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="58721-253">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="58721-254">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="58721-254">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="58721-255">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="58721-255">array of enum</span></span>|<span data-ttu-id="58721-256">1 </span><span class="sxs-lookup"><span data-stu-id="58721-256">1</span></span>||<span data-ttu-id="58721-257">Définit la manière dont votre onglet sera disponible dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="58721-257">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="58721-258">Les options sont `sharePointFullPage` et`sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="58721-258">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="58721-259">staticTabs</span><span class="sxs-lookup"><span data-stu-id="58721-259">staticTabs</span></span>

<span data-ttu-id="58721-260">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="58721-260">**Optional** — array</span></span>

<span data-ttu-id="58721-261">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur ne les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="58721-261">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="58721-262">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="58721-262">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="58721-263">Les onglets statiques déclarés dans l' `team` étendue ne sont pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="58721-263">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="58721-264">Cet élément est un tableau (au maximum 16 éléments) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="58721-264">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="58721-265">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="58721-265">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="58721-266">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-266">Name</span></span>| <span data-ttu-id="58721-267">Type</span><span class="sxs-lookup"><span data-stu-id="58721-267">Type</span></span>| <span data-ttu-id="58721-268">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-268">Maximum size</span></span> | <span data-ttu-id="58721-269">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-269">Required</span></span> | <span data-ttu-id="58721-270">Description</span><span class="sxs-lookup"><span data-stu-id="58721-270">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="58721-271">string</span><span class="sxs-lookup"><span data-stu-id="58721-271">string</span></span>|<span data-ttu-id="58721-272">64 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-272">64 characters</span></span>|<span data-ttu-id="58721-273">✔</span><span class="sxs-lookup"><span data-stu-id="58721-273">✔</span></span>|<span data-ttu-id="58721-274">Identificateur unique de l’entité que l’onglet affiche.</span><span class="sxs-lookup"><span data-stu-id="58721-274">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="58721-275">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-275">string</span></span>|<span data-ttu-id="58721-276">128 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-276">128 characters</span></span>|<span data-ttu-id="58721-277">✔</span><span class="sxs-lookup"><span data-stu-id="58721-277">✔</span></span>|<span data-ttu-id="58721-278">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="58721-278">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="58721-279">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-279">string</span></span>|<span data-ttu-id="58721-280">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-280">2048 characters</span></span>|<span data-ttu-id="58721-281">✔</span><span class="sxs-lookup"><span data-stu-id="58721-281">✔</span></span>|<span data-ttu-id="58721-282">URL https://qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de dessin de teams.</span><span class="sxs-lookup"><span data-stu-id="58721-282">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="58721-283">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-283">string</span></span>|<span data-ttu-id="58721-284">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-284">2048 characters</span></span>||<span data-ttu-id="58721-285">URL https://vers laquelle pointer si un utilisateur choisit de l’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="58721-285">The https:// URL to point at if a user opts to view in a browser.</span></span>|
|`scopes`|<span data-ttu-id="58721-286">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="58721-286">array of enum</span></span>|<span data-ttu-id="58721-287">1 </span><span class="sxs-lookup"><span data-stu-id="58721-287">1</span></span>|<span data-ttu-id="58721-288">✔</span><span class="sxs-lookup"><span data-stu-id="58721-288">✔</span></span>|<span data-ttu-id="58721-289">Actuellement, les onglets statiques prennent en charge uniquement l' `personal` étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="58721-289">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|

> [!NOTE]
> <span data-ttu-id="58721-290">Si vos onglets nécessitent des informations contextuelles pour afficher le contenu pertinent ou pour initier un flux d’authentification, *reportez-vous* à [la rubrique obtenir le contexte de votre onglet Microsoft teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="58721-290">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="58721-291">bots</span><span class="sxs-lookup"><span data-stu-id="58721-291">bots</span></span>

<span data-ttu-id="58721-292">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="58721-292">**Optional** — array</span></span>

<span data-ttu-id="58721-293">Définit une solution de robot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="58721-293">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="58721-294">L’élément est un tableau (un seul élément un seul d' &mdash; entre eux est actuellement autorisé par application) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="58721-294">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="58721-295">Ce bloc est requis uniquement pour les solutions qui fournissent une expérience de robot.</span><span class="sxs-lookup"><span data-stu-id="58721-295">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="58721-296">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-296">Name</span></span>| <span data-ttu-id="58721-297">Type</span><span class="sxs-lookup"><span data-stu-id="58721-297">Type</span></span>| <span data-ttu-id="58721-298">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-298">Maximum size</span></span> | <span data-ttu-id="58721-299">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-299">Required</span></span> | <span data-ttu-id="58721-300">Description</span><span class="sxs-lookup"><span data-stu-id="58721-300">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="58721-301">string</span><span class="sxs-lookup"><span data-stu-id="58721-301">string</span></span>|<span data-ttu-id="58721-302">64 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-302">64 characters</span></span>|<span data-ttu-id="58721-303">✔</span><span class="sxs-lookup"><span data-stu-id="58721-303">✔</span></span>|<span data-ttu-id="58721-304">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="58721-304">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="58721-305">Il peut s’agir de la même chose que l' [ID d’application](#id)global.</span><span class="sxs-lookup"><span data-stu-id="58721-305">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="58721-306">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="58721-306">array of enum</span></span>|<span data-ttu-id="58721-307">3 </span><span class="sxs-lookup"><span data-stu-id="58721-307">3</span></span>|<span data-ttu-id="58721-308">✔</span><span class="sxs-lookup"><span data-stu-id="58721-308">✔</span></span>|<span data-ttu-id="58721-309">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="58721-309">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="58721-310">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="58721-310">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="58721-311">booléen</span><span class="sxs-lookup"><span data-stu-id="58721-311">boolean</span></span>|||<span data-ttu-id="58721-312">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="58721-312">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="58721-313">Default**`false`**</span><span class="sxs-lookup"><span data-stu-id="58721-313">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="58721-314">booléen</span><span class="sxs-lookup"><span data-stu-id="58721-314">boolean</span></span>|||<span data-ttu-id="58721-315">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="58721-315">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="58721-316">Default`**false**`</span><span class="sxs-lookup"><span data-stu-id="58721-316">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="58721-317">booléen</span><span class="sxs-lookup"><span data-stu-id="58721-317">boolean</span></span>|||<span data-ttu-id="58721-318">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="58721-318">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="58721-319">Default**`false`**</span><span class="sxs-lookup"><span data-stu-id="58721-319">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="58721-320">bots. commandLists</span><span class="sxs-lookup"><span data-stu-id="58721-320">bots.commandLists</span></span>

<span data-ttu-id="58721-321">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="58721-321">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="58721-322">L’objet est un tableau (nombre maximal de 2 éléments) avec tous les éléments de type `object` ; vous devez définir une liste de commandes distincte pour chaque étendue prise en charge par votre bot.</span><span class="sxs-lookup"><span data-stu-id="58721-322">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="58721-323">Pour plus d’informations, voir [menus de bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="58721-323">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="58721-324">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-324">Name</span></span>| <span data-ttu-id="58721-325">Type</span><span class="sxs-lookup"><span data-stu-id="58721-325">Type</span></span>| <span data-ttu-id="58721-326">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-326">Maximum size</span></span> | <span data-ttu-id="58721-327">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-327">Required</span></span> | <span data-ttu-id="58721-328">Description</span><span class="sxs-lookup"><span data-stu-id="58721-328">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="58721-329">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="58721-329">array of enum</span></span>|<span data-ttu-id="58721-330">3 </span><span class="sxs-lookup"><span data-stu-id="58721-330">3</span></span>|<span data-ttu-id="58721-331">✔</span><span class="sxs-lookup"><span data-stu-id="58721-331">✔</span></span>|<span data-ttu-id="58721-332">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="58721-332">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="58721-333">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="58721-333">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="58721-334">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="58721-334">array of objects</span></span>|<span data-ttu-id="58721-335">10 </span><span class="sxs-lookup"><span data-stu-id="58721-335">10</span></span>|<span data-ttu-id="58721-336">✔</span><span class="sxs-lookup"><span data-stu-id="58721-336">✔</span></span>|<span data-ttu-id="58721-337">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="58721-337">An array of commands the bot supports:</span></span><br><span data-ttu-id="58721-338">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="58721-338">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="58721-339">`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)</span><span class="sxs-lookup"><span data-stu-id="58721-339">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="58721-340">bots. commandLists. Commands</span><span class="sxs-lookup"><span data-stu-id="58721-340">bots.commandLists.commands</span></span>

|<span data-ttu-id="58721-341">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-341">Name</span></span>| <span data-ttu-id="58721-342">Type</span><span class="sxs-lookup"><span data-stu-id="58721-342">Type</span></span>| <span data-ttu-id="58721-343">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-343">Maximum size</span></span> | <span data-ttu-id="58721-344">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-344">Required</span></span> | <span data-ttu-id="58721-345">Description</span><span class="sxs-lookup"><span data-stu-id="58721-345">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="58721-346">title</span><span class="sxs-lookup"><span data-stu-id="58721-346">title</span></span>|<span data-ttu-id="58721-347">string</span><span class="sxs-lookup"><span data-stu-id="58721-347">string</span></span>|<span data-ttu-id="58721-348">12 </span><span class="sxs-lookup"><span data-stu-id="58721-348">12</span></span>|<span data-ttu-id="58721-349">✔</span><span class="sxs-lookup"><span data-stu-id="58721-349">✔</span></span>|<span data-ttu-id="58721-350">Nom de la commande bot</span><span class="sxs-lookup"><span data-stu-id="58721-350">The bot command name</span></span>|
|<span data-ttu-id="58721-351">description</span><span class="sxs-lookup"><span data-stu-id="58721-351">description</span></span>|<span data-ttu-id="58721-352">string</span><span class="sxs-lookup"><span data-stu-id="58721-352">string</span></span>|<span data-ttu-id="58721-353">128 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-353">128 characters</span></span>|<span data-ttu-id="58721-354">✔</span><span class="sxs-lookup"><span data-stu-id="58721-354">✔</span></span>|<span data-ttu-id="58721-355">Une description de texte simple ou un exemple de syntaxe de commande et ses arguments.</span><span class="sxs-lookup"><span data-stu-id="58721-355">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="58721-356">ceux</span><span class="sxs-lookup"><span data-stu-id="58721-356">connectors</span></span>

<span data-ttu-id="58721-357">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="58721-357">**Optional** — array</span></span>

<span data-ttu-id="58721-358">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="58721-358">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="58721-359">L’objet est un tableau (un maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="58721-359">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="58721-360">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="58721-360">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="58721-361">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-361">Name</span></span>| <span data-ttu-id="58721-362">Type</span><span class="sxs-lookup"><span data-stu-id="58721-362">Type</span></span>| <span data-ttu-id="58721-363">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-363">Maximum size</span></span> | <span data-ttu-id="58721-364">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-364">Required</span></span> | <span data-ttu-id="58721-365">Description</span><span class="sxs-lookup"><span data-stu-id="58721-365">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="58721-366">string</span><span class="sxs-lookup"><span data-stu-id="58721-366">string</span></span>|<span data-ttu-id="58721-367">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-367">2048 characters</span></span>|<span data-ttu-id="58721-368">✔</span><span class="sxs-lookup"><span data-stu-id="58721-368">✔</span></span>|<span data-ttu-id="58721-369">URL https://à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="58721-369">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="58721-370">tableau de l’énum</span><span class="sxs-lookup"><span data-stu-id="58721-370">array of enum</span></span>|<span data-ttu-id="58721-371">1 </span><span class="sxs-lookup"><span data-stu-id="58721-371">1</span></span>|<span data-ttu-id="58721-372">✔</span><span class="sxs-lookup"><span data-stu-id="58721-372">✔</span></span>|<span data-ttu-id="58721-373">Indique si le connecteur offre une expérience dans le contexte d’un canal dans un `team` , ou une expérience étendue à un utilisateur individuel ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="58721-373">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="58721-374">Actuellement, seule l' `team` étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="58721-374">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="58721-375">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-375">string</span></span>|<span data-ttu-id="58721-376">64 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-376">64 characters</span></span>|<span data-ttu-id="58721-377">✔</span><span class="sxs-lookup"><span data-stu-id="58721-377">✔</span></span>|<span data-ttu-id="58721-378">Identificateur unique du connecteur correspondant à son ID dans le [tableau de bord du développeur de connecteurs](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="58721-378">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="58721-379">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="58721-379">composeExtensions</span></span>

<span data-ttu-id="58721-380">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="58721-380">**Optional** — array</span></span>

<span data-ttu-id="58721-381">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="58721-381">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="58721-382">Le nom de la fonctionnalité a été modifié de « extension de composition » en « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même afin que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="58721-382">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="58721-383">L’élément est un tableau (un maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="58721-383">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="58721-384">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="58721-384">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="58721-385">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-385">Name</span></span>| <span data-ttu-id="58721-386">Type</span><span class="sxs-lookup"><span data-stu-id="58721-386">Type</span></span> | <span data-ttu-id="58721-387">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-387">Maximum Size</span></span> | <span data-ttu-id="58721-388">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="58721-388">Required</span></span> | <span data-ttu-id="58721-389">Description</span><span class="sxs-lookup"><span data-stu-id="58721-389">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="58721-390">string</span><span class="sxs-lookup"><span data-stu-id="58721-390">string</span></span>|<span data-ttu-id="58721-391">64</span><span class="sxs-lookup"><span data-stu-id="58721-391">64</span></span>|<span data-ttu-id="58721-392">✔</span><span class="sxs-lookup"><span data-stu-id="58721-392">✔</span></span>|<span data-ttu-id="58721-393">ID d’application Microsoft unique pour le bot qui sauvegarde l’extension de messagerie, tel qu’inscrit auprès de l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="58721-393">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="58721-394">Il peut s’agir de la même chose que l’ID d’application global.</span><span class="sxs-lookup"><span data-stu-id="58721-394">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="58721-395">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="58721-395">array of objects</span></span>|<span data-ttu-id="58721-396">10 </span><span class="sxs-lookup"><span data-stu-id="58721-396">10</span></span>|<span data-ttu-id="58721-397">✔</span><span class="sxs-lookup"><span data-stu-id="58721-397">✔</span></span>|<span data-ttu-id="58721-398">Tableau de commandes prises en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="58721-398">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="58721-399">booléen</span><span class="sxs-lookup"><span data-stu-id="58721-399">boolean</span></span>|||<span data-ttu-id="58721-400">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58721-400">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="58721-401">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="58721-401">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="58721-402">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="58721-402">array of Objects</span></span>|<span data-ttu-id="58721-403">5 </span><span class="sxs-lookup"><span data-stu-id="58721-403">5</span></span>||<span data-ttu-id="58721-404">Liste de gestionnaires permettant d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="58721-404">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="58721-405">Les domaines doivent également être affichés dans`validDomains`</span><span class="sxs-lookup"><span data-stu-id="58721-405">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="58721-406">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-406">string</span></span>|||<span data-ttu-id="58721-407">Type de gestionnaire de messages.</span><span class="sxs-lookup"><span data-stu-id="58721-407">The type of message handler.</span></span> <span data-ttu-id="58721-408">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="58721-408">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="58721-409">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="58721-409">array of Strings</span></span>|||<span data-ttu-id="58721-410">Tableau de domaines pour lesquels le gestionnaire de messages de liaison peut s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="58721-410">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="58721-411">composeExtensions. Commands</span><span class="sxs-lookup"><span data-stu-id="58721-411">composeExtensions.commands</span></span>

<span data-ttu-id="58721-412">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="58721-412">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="58721-413">Chaque commande apparaît dans Microsoft teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58721-413">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="58721-414">Il y a un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="58721-414">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="58721-415">Chaque élément de commande est un objet de la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="58721-415">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="58721-416">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-416">Name</span></span>| <span data-ttu-id="58721-417">Type</span><span class="sxs-lookup"><span data-stu-id="58721-417">Type</span></span>| <span data-ttu-id="58721-418">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-418">Maximum size</span></span> | <span data-ttu-id="58721-419">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-419">Required</span></span> | <span data-ttu-id="58721-420">Description</span><span class="sxs-lookup"><span data-stu-id="58721-420">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="58721-421">string</span><span class="sxs-lookup"><span data-stu-id="58721-421">string</span></span>|<span data-ttu-id="58721-422">64 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-422">64 characters</span></span>|<span data-ttu-id="58721-423">✔</span><span class="sxs-lookup"><span data-stu-id="58721-423">✔</span></span>|<span data-ttu-id="58721-424">ID de la commande.</span><span class="sxs-lookup"><span data-stu-id="58721-424">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="58721-425">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-425">string</span></span>|<span data-ttu-id="58721-426">32 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-426">32 characters</span></span>|<span data-ttu-id="58721-427">✔</span><span class="sxs-lookup"><span data-stu-id="58721-427">✔</span></span>|<span data-ttu-id="58721-428">Nom de la commande conviviale.</span><span class="sxs-lookup"><span data-stu-id="58721-428">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="58721-429">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-429">string</span></span>|<span data-ttu-id="58721-430">64 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-430">64 characters</span></span>||<span data-ttu-id="58721-431">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="58721-431">Type of the command.</span></span> <span data-ttu-id="58721-432">L’une `query` ou l’autre `action` .</span><span class="sxs-lookup"><span data-stu-id="58721-432">One of `query` or `action`.</span></span> <span data-ttu-id="58721-433">Valeur par défaut : **requête**.</span><span class="sxs-lookup"><span data-stu-id="58721-433">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="58721-434">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-434">string</span></span>|<span data-ttu-id="58721-435">128 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-435">128 characters</span></span>||<span data-ttu-id="58721-436">Description qui apparaît pour les utilisateurs afin d’indiquer la finalité de cette commande.</span><span class="sxs-lookup"><span data-stu-id="58721-436">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="58721-437">booléen</span><span class="sxs-lookup"><span data-stu-id="58721-437">boolean</span></span>|||<span data-ttu-id="58721-438">Valeur booléenne indiquant si la commande doit être exécutée initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="58721-438">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="58721-439">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="58721-439">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="58721-440">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="58721-440">array of Strings</span></span>|<span data-ttu-id="58721-441">3 </span><span class="sxs-lookup"><span data-stu-id="58721-441">3</span></span>||<span data-ttu-id="58721-442">Définit l’emplacement à partir duquel l’extension de message peut être appelée.</span><span class="sxs-lookup"><span data-stu-id="58721-442">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="58721-443">Toute combinaison de `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="58721-443">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="58721-444">La valeur par défaut est `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="58721-444">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="58721-445">booléen</span><span class="sxs-lookup"><span data-stu-id="58721-445">boolean</span></span>|||<span data-ttu-id="58721-446">Valeur booléenne qui indique s’il doit extraire le module de tâches de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="58721-446">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="58721-447">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="58721-447">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="58721-448">objet</span><span class="sxs-lookup"><span data-stu-id="58721-448">object</span></span>|||<span data-ttu-id="58721-449">Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="58721-449">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="58721-450">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-450">string</span></span>|<span data-ttu-id="58721-451">64 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-451">64 characters</span></span>||<span data-ttu-id="58721-452">Titre de la boîte de dialogue initiale.</span><span class="sxs-lookup"><span data-stu-id="58721-452">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="58721-453">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-453">string</span></span>|||<span data-ttu-id="58721-454">Largeur de la boîte de dialogue-soit un nombre en pixels, soit une mise en page par défaut telle que « grande », « moyen » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="58721-454">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="58721-455">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-455">string</span></span>|||<span data-ttu-id="58721-456">Hauteur de la boîte de dialogue : nombre en pixels ou mise en page par défaut, par exemple, « grande », « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="58721-456">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="58721-457">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-457">string</span></span>|||<span data-ttu-id="58721-458">URL d’affichage WebView initiale.</span><span class="sxs-lookup"><span data-stu-id="58721-458">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="58721-459">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="58721-459">array of object</span></span>|<span data-ttu-id="58721-460">5 éléments</span><span class="sxs-lookup"><span data-stu-id="58721-460">5 items</span></span>|<span data-ttu-id="58721-461">✔</span><span class="sxs-lookup"><span data-stu-id="58721-461">✔</span></span>|<span data-ttu-id="58721-462">La liste des paramètres que la commande prend.</span><span class="sxs-lookup"><span data-stu-id="58721-462">The list of parameters the command takes.</span></span> <span data-ttu-id="58721-463">Minimum : 1 ; maximum : 5.</span><span class="sxs-lookup"><span data-stu-id="58721-463">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="58721-464">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-464">string</span></span>|<span data-ttu-id="58721-465">64 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-465">64 characters</span></span>|<span data-ttu-id="58721-466">✔</span><span class="sxs-lookup"><span data-stu-id="58721-466">✔</span></span>|<span data-ttu-id="58721-467">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="58721-467">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="58721-468">Elle est incluse dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58721-468">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="58721-469">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-469">string</span></span>|<span data-ttu-id="58721-470">32 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-470">32 characters</span></span>|<span data-ttu-id="58721-471">✔</span><span class="sxs-lookup"><span data-stu-id="58721-471">✔</span></span>|<span data-ttu-id="58721-472">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="58721-472">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="58721-473">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-473">string</span></span>|<span data-ttu-id="58721-474">128 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-474">128 characters</span></span>||<span data-ttu-id="58721-475">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="58721-475">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="58721-476">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-476">string</span></span>|<span data-ttu-id="58721-477">512 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-477">512 characters</span></span>||<span data-ttu-id="58721-478">Valeur initiale du paramètre.</span><span class="sxs-lookup"><span data-stu-id="58721-478">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="58721-479">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-479">string</span></span>|<span data-ttu-id="58721-480">128 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-480">128 characters</span></span>||<span data-ttu-id="58721-481">Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="58721-481">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="58721-482">L’une des `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="58721-482">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="58721-483">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="58721-483">array of objects</span></span>|<span data-ttu-id="58721-484">10 éléments</span><span class="sxs-lookup"><span data-stu-id="58721-484">10 items</span></span>||<span data-ttu-id="58721-485">Options de choix pour le `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="58721-485">The choice options for the`choiceset`.</span></span> <span data-ttu-id="58721-486">Utilisez uniquement lorsque `parameter.inputType` est `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="58721-486">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="58721-487">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-487">string</span></span>|<span data-ttu-id="58721-488">128 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-488">128 characters</span></span>|<span data-ttu-id="58721-489">✔</span><span class="sxs-lookup"><span data-stu-id="58721-489">✔</span></span>|<span data-ttu-id="58721-490">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="58721-490">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="58721-491">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-491">string</span></span>|<span data-ttu-id="58721-492">512 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-492">512 characters</span></span>|<span data-ttu-id="58721-493">✔</span><span class="sxs-lookup"><span data-stu-id="58721-493">✔</span></span>|<span data-ttu-id="58721-494">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="58721-494">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="58721-495">autorisations</span><span class="sxs-lookup"><span data-stu-id="58721-495">permissions</span></span>

<span data-ttu-id="58721-496">**Facultatif** — tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="58721-496">**Optional** — array of strings</span></span>

<span data-ttu-id="58721-497">Un tableau `string` qui spécifie les autorisations demandées par l’application, ce qui permet aux utilisateurs finaux de savoir comment effectuer l’extension.</span><span class="sxs-lookup"><span data-stu-id="58721-497">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="58721-498">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="58721-498">The following options are non-exclusive:</span></span>

* <span data-ttu-id="58721-499">`identity`&emsp;Nécessite des informations d’identité d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="58721-499">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="58721-500">`messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="58721-500">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="58721-501">Si vous modifiez ces autorisations lors de la mise à jour de votre application, vos utilisateurs répéteront le processus de consentement la première fois qu’ils exécuteront l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="58721-501">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="58721-502">Pour plus d’informations, consultez [la rubrique mise à jour de votre application](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="58721-502">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="58721-503">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="58721-503">devicePermissions</span></span>

<span data-ttu-id="58721-504">**Facultatif** — tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="58721-504">**Optional** — array of strings</span></span>

<span data-ttu-id="58721-505">Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur auquel votre application peut demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="58721-505">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="58721-506">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="58721-506">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="58721-507">validDomains</span><span class="sxs-lookup"><span data-stu-id="58721-507">validDomains</span></span>

<span data-ttu-id="58721-508">**Facultatif** **, sauf indication contraire**</span><span class="sxs-lookup"><span data-stu-id="58721-508">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="58721-509">Une liste des domaines valides pour les sites Web que l’application prévoit de charger dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="58721-509">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="58721-510">Les listes de domaine peuvent inclure des caractères génériques, par exemple `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="58721-510">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="58721-511">Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="58721-511">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="58721-512">Si la configuration de votre onglet ou de votre interface utilisateur de contenu doit accéder à un autre domaine en plus de celui utilisé pour la configuration d’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="58721-512">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="58721-513">Toutefois, il n’est **pas** nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="58721-513">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="58721-514">Par exemple, pour authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="58721-514">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="58721-515">Les applications teams qui requièrent leurs propres URL SharePoint pour fonctionner correctement, peuvent inclure « {teamsitedomain} » dans leur liste de domaines valide.</span><span class="sxs-lookup"><span data-stu-id="58721-515">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="58721-516">N’ajoutez pas de domaines qui se trouvent en dehors de votre contrôle, soit directement, soit via des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="58721-516">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="58721-517">Par exemple, `yourapp.onmicrosoft.com` est valide, mais n' `*.onmicrosoft.com` est pas valide.</span><span class="sxs-lookup"><span data-stu-id="58721-517">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="58721-518">L’objet est un tableau contenant tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="58721-518">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="58721-519">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="58721-519">webApplicationInfo</span></span>

<span data-ttu-id="58721-520">**Facultatif** — Object</span><span class="sxs-lookup"><span data-stu-id="58721-520">**Optional** — object</span></span>

<span data-ttu-id="58721-521">Spécifiez l’ID de votre application AAD et les informations graphiques pour aider les utilisateurs à se connecter à votre application AAD de manière transparente.</span><span class="sxs-lookup"><span data-stu-id="58721-521">Specify your AAD App ID and Graph information to help users seamlessly sign into your AAD app.</span></span>

|<span data-ttu-id="58721-522">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-522">Name</span></span>| <span data-ttu-id="58721-523">Type</span><span class="sxs-lookup"><span data-stu-id="58721-523">Type</span></span>| <span data-ttu-id="58721-524">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-524">Maximum size</span></span> | <span data-ttu-id="58721-525">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-525">Required</span></span> | <span data-ttu-id="58721-526">Description</span><span class="sxs-lookup"><span data-stu-id="58721-526">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="58721-527">string</span><span class="sxs-lookup"><span data-stu-id="58721-527">string</span></span>|<span data-ttu-id="58721-528">36 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-528">36 characters</span></span>|<span data-ttu-id="58721-529">✔</span><span class="sxs-lookup"><span data-stu-id="58721-529">✔</span></span>|<span data-ttu-id="58721-530">ID de l’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="58721-530">AAD application id of the app.</span></span> <span data-ttu-id="58721-531">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="58721-531">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="58721-532">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-532">string</span></span>|<span data-ttu-id="58721-533">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-533">2048 characters</span></span>||<span data-ttu-id="58721-534">URL de ressource de l’application pour l’acquisition du jeton d’authentification pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="58721-534">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="58721-535">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="58721-535">array of strings</span></span>|<span data-ttu-id="58721-536">128 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-536">128 characters</span></span>||<span data-ttu-id="58721-537">Spécifier le [consentement spécifique](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions) à une ressource granulaire</span><span class="sxs-lookup"><span data-stu-id="58721-537">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="58721-538">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="58721-538">showLoadingIndicator</span></span>

<span data-ttu-id="58721-539">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="58721-539">**Optional** — boolean</span></span>

<span data-ttu-id="58721-540">Indiquer où afficher ou non l’indicateur de chargement lors du chargement d’une application ou d’un onglet.</span><span class="sxs-lookup"><span data-stu-id="58721-540">Indicate where or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="58721-541">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="58721-541">Default: **false**.</span></span>

## <a name="isfullscreen"></a><span data-ttu-id="58721-542">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="58721-542">isFullScreen</span></span>

 <span data-ttu-id="58721-543">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="58721-543">**Optional** — boolean</span></span>

<span data-ttu-id="58721-544">Indiquer où une application personnelle est rendue avec ou sans barre d’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="58721-544">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="58721-545">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="58721-545">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="58721-546">activities</span><span class="sxs-lookup"><span data-stu-id="58721-546">activities</span></span>

<span data-ttu-id="58721-547">**Facultatif** — Object</span><span class="sxs-lookup"><span data-stu-id="58721-547">**Optional** — object</span></span>

<span data-ttu-id="58721-548">Définissez les propriétés que votre application utilisera pour publier dans un flux d’activités utilisateur.</span><span class="sxs-lookup"><span data-stu-id="58721-548">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="58721-549">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-549">Name</span></span>| <span data-ttu-id="58721-550">Type</span><span class="sxs-lookup"><span data-stu-id="58721-550">Type</span></span>| <span data-ttu-id="58721-551">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-551">Maximum size</span></span> | <span data-ttu-id="58721-552">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-552">Required</span></span> | <span data-ttu-id="58721-553">Description</span><span class="sxs-lookup"><span data-stu-id="58721-553">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="58721-554">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="58721-554">array of Objects</span></span>|<span data-ttu-id="58721-555">128 éléments</span><span class="sxs-lookup"><span data-stu-id="58721-555">128 items</span></span>| | <span data-ttu-id="58721-556">Spécifiez les types d’activités que votre application peut publier dans le flux d’activités des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="58721-556">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="58721-557">Activities. activityTypes</span><span class="sxs-lookup"><span data-stu-id="58721-557">activities.activityTypes</span></span>

|<span data-ttu-id="58721-558">Nom</span><span class="sxs-lookup"><span data-stu-id="58721-558">Name</span></span>| <span data-ttu-id="58721-559">Type</span><span class="sxs-lookup"><span data-stu-id="58721-559">Type</span></span>| <span data-ttu-id="58721-560">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="58721-560">Maximum size</span></span> | <span data-ttu-id="58721-561">Requis</span><span class="sxs-lookup"><span data-stu-id="58721-561">Required</span></span> | <span data-ttu-id="58721-562">Description</span><span class="sxs-lookup"><span data-stu-id="58721-562">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="58721-563">string</span><span class="sxs-lookup"><span data-stu-id="58721-563">string</span></span>|<span data-ttu-id="58721-564">32 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-564">32 characters</span></span>|<span data-ttu-id="58721-565">✔</span><span class="sxs-lookup"><span data-stu-id="58721-565">✔</span></span>|<span data-ttu-id="58721-566">Type de notification.</span><span class="sxs-lookup"><span data-stu-id="58721-566">The notification type.</span></span> <span data-ttu-id="58721-567">*Voir ci-dessous*.</span><span class="sxs-lookup"><span data-stu-id="58721-567">*See below*.</span></span>|
|`description`|<span data-ttu-id="58721-568">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-568">string</span></span>|<span data-ttu-id="58721-569">128 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-569">128 characters</span></span>|<span data-ttu-id="58721-570">✔</span><span class="sxs-lookup"><span data-stu-id="58721-570">✔</span></span>|<span data-ttu-id="58721-571">Brève description de la notification.</span><span class="sxs-lookup"><span data-stu-id="58721-571">A brief description of the notification.</span></span> <span data-ttu-id="58721-572">*Voir ci-dessous*.</span><span class="sxs-lookup"><span data-stu-id="58721-572">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="58721-573">chaîne</span><span class="sxs-lookup"><span data-stu-id="58721-573">string</span></span>|<span data-ttu-id="58721-574">128 caractères</span><span class="sxs-lookup"><span data-stu-id="58721-574">128 characters</span></span>|<span data-ttu-id="58721-575">✔</span><span class="sxs-lookup"><span data-stu-id="58721-575">✔</span></span>|<span data-ttu-id="58721-576">Ex : « tâche créée le {Actor} {taskId} »</span><span class="sxs-lookup"><span data-stu-id="58721-576">Ex: "{actor} created task {taskId} for you"</span></span>|

```json
{
   "activities":{
      "activityTypes":[
         {
            "type":"taskCreated",
            "description":"Task Created Activity",
            "templateText":"{actor} created task {taskId} for you"
         },
         {
            "type":"teamMention",
            "description":"Team Mention Activity",
            "templateText":"{actor} mentioned team"
         },
         {
            "type":"channelMention",
            "description":"Channel Mention Activity",
            "templateText":"{actor} mentioned channel"
         },
         {
            "type":"userMention",
            "description":"Personal Mention Activity",
            "templateText":"{actor} mentioned user"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"calendarForward",
            "description":"Forwarding a Calendar Event",
            "templateText":"{actor} sent user an invite on behalf of {eventOwner}"
         },
         {
            "type":"creatorTaskCreated",
            "description":"Created Task Created",
            "templateText":"The Creator created task {taskId} for you"
         }
      ]
   }
}
```

***
>
>
