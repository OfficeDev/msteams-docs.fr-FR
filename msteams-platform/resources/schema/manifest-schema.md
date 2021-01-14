---
title: Référence du schéma de manifeste
description: Décrit le schéma de manifeste pour Microsoft Teams
keywords: schéma de manifeste teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: cf80251abd22f0c89388cbe5a6287a02dedce1fb
ms.sourcegitcommit: bf61ae5ad2afa4efdb0311158184d0cbb9c40174
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2021
ms.locfileid: "49845629"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="85bc6-104">Référence : schéma de manifeste pour Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="85bc6-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="85bc6-105">Le manifeste De Microsoft Teams décrit comment l’application s’intègre au produit Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="85bc6-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="85bc6-106">Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="85bc6-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="85bc6-107">Les versions précédentes 1.0-1.4 sont également pris en charge (à l’aide de « v1.x » dans l’URL).</span><span class="sxs-lookup"><span data-stu-id="85bc6-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="85bc6-108">L’exemple de schéma suivant montre toutes les options d’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="85bc6-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="85bc6-109">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="85bc6-109">Sample full manifest</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.8",
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
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
      ],
      "sharePointPreviewImage": "Relative path to a tab preview image for use in SharePoint — 1024px X 768",
      "supportedSharePointHosts": [
         "sharePointFullPage",
         "sharePointWebPart"
      ]
    }
  ],
  "staticTabs": [
    {
      "entityId": "unique Id for the page entity",
      "scopes": [
        "personal"
      ],
      "context":[
        "personalTab",
        "channelTab"
        ],
      "name": "Display name of tab",
      "contentUrl": "https://contoso.com/content (displayed in Teams canvas)",
      "websiteUrl": "https://contoso.com/content (displayed in web browser)",
       "searchUrl":  "https://contoso.com/content (displayed in web browser)"
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
      "supportsCalling": false,
      "supportsVideo": true,
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

<span data-ttu-id="85bc6-110">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="85bc6-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="85bc6-111">$schema</span><span class="sxs-lookup"><span data-stu-id="85bc6-111">$schema</span></span>

<span data-ttu-id="85bc6-112">*Chaîne facultative, mais recommandée*</span><span class="sxs-lookup"><span data-stu-id="85bc6-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="85bc6-113">L https:// URL référente au schéma JSON pour le manifeste.</span><span class="sxs-lookup"><span data-stu-id="85bc6-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="85bc6-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="85bc6-114">manifestVersion</span></span>

<span data-ttu-id="85bc6-115">**Obligatoire —** chaîne</span><span class="sxs-lookup"><span data-stu-id="85bc6-115">**Required** — string</span></span>

<span data-ttu-id="85bc6-116">Version du schéma de manifeste utilisé par ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="85bc6-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="85bc6-117">Elle doit être « 1.7 ».</span><span class="sxs-lookup"><span data-stu-id="85bc6-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="85bc6-118">version</span><span class="sxs-lookup"><span data-stu-id="85bc6-118">version</span></span>

<span data-ttu-id="85bc6-119">**Obligatoire —** chaîne</span><span class="sxs-lookup"><span data-stu-id="85bc6-119">**Required** — string</span></span>

<span data-ttu-id="85bc6-120">Version de l’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="85bc6-120">The version of the specific app.</span></span> <span data-ttu-id="85bc6-121">Si vous mettez à jour quelque chose dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="85bc6-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="85bc6-122">Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="85bc6-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="85bc6-123">Si cette application a été soumise au Store, le nouveau manifeste devra être soumis à nouveau et validé à nouveau.</span><span class="sxs-lookup"><span data-stu-id="85bc6-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="85bc6-124">Ensuite, les utilisateurs de cette application obtiennent automatiquement le nouveau manifeste mis à jour dans quelques heures, après son approbation.</span><span class="sxs-lookup"><span data-stu-id="85bc6-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="85bc6-125">Si l’application demande des autorisations, les utilisateurs sont invités à mettre à niveau et à consentir à l’application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="85bc6-126">Cette chaîne de version doit suivre la [norme de semver](http://semver.org/) (MAJOR. MINOR. PATCH).</span><span class="sxs-lookup"><span data-stu-id="85bc6-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="85bc6-127">id</span><span class="sxs-lookup"><span data-stu-id="85bc6-127">id</span></span>

<span data-ttu-id="85bc6-128">**Obligatoire** — ID d’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="85bc6-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="85bc6-129">Identificateur unique généré par Microsoft pour cette application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="85bc6-130">Si vous avez inscrit un bot via Microsoft Bot Framework ou si l’application web de votre onglet se signe déjà avec Microsoft, vous devez déjà avoir un ID et l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="85bc6-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="85bc6-131">Sinon, vous devez générer un nouvel ID sur le portail d’inscription des applications Microsoft[(Mes applications),](https://apps.dev.microsoft.com)entrez-le ici, puis réutilisez-le lorsque vous ajoutez un bot. Remarque : si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="85bc6-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="85bc6-132">developer</span><span class="sxs-lookup"><span data-stu-id="85bc6-132">developer</span></span>

<span data-ttu-id="85bc6-133">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="85bc6-133">**Required** — object</span></span>

<span data-ttu-id="85bc6-134">Spécifie des informations sur votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="85bc6-134">Specifies information about your company.</span></span> <span data-ttu-id="85bc6-135">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="85bc6-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="85bc6-136">Pour plus [d’informations, voir](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) nos recommandations en matière de publication.</span><span class="sxs-lookup"><span data-stu-id="85bc6-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="85bc6-137">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-137">Name</span></span>| <span data-ttu-id="85bc6-138">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-138">Maximum size</span></span> | <span data-ttu-id="85bc6-139">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-139">Required</span></span> | <span data-ttu-id="85bc6-140">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="85bc6-141">32 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-141">32 characters</span></span>|<span data-ttu-id="85bc6-142">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-142">✔</span></span>|<span data-ttu-id="85bc6-143">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="85bc6-144">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-144">2048 characters</span></span>|<span data-ttu-id="85bc6-145">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-145">✔</span></span>|<span data-ttu-id="85bc6-146">L https:// URL du site web du développeur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="85bc6-147">Ce lien doit permettre aux utilisateurs d’accès à votre entreprise ou à votre page d’accueil spécifique au produit.</span><span class="sxs-lookup"><span data-stu-id="85bc6-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="85bc6-148">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-148">2048 characters</span></span>|<span data-ttu-id="85bc6-149">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-149">✔</span></span>|<span data-ttu-id="85bc6-150">L https:// URL vers la politique de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="85bc6-151">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-151">2048 characters</span></span>|<span data-ttu-id="85bc6-152">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-152">✔</span></span>|<span data-ttu-id="85bc6-153">L https:// URL vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="85bc6-154">10 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-154">10 characters</span></span>| |<span data-ttu-id="85bc6-155">**Facultatif** ID Microsoft Partner Network qui identifie l’organisation partenaire qui construit l’application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="85bc6-156">name</span><span class="sxs-lookup"><span data-stu-id="85bc6-156">name</span></span>

<span data-ttu-id="85bc6-157">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="85bc6-157">**Required** — object</span></span>

<span data-ttu-id="85bc6-158">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’expérience Teams.</span><span class="sxs-lookup"><span data-stu-id="85bc6-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="85bc6-159">Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="85bc6-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="85bc6-160">Les valeurs `short` de et ne doivent pas être `full` identiques.</span><span class="sxs-lookup"><span data-stu-id="85bc6-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="85bc6-161">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-161">Name</span></span>| <span data-ttu-id="85bc6-162">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-162">Maximum size</span></span> | <span data-ttu-id="85bc6-163">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-163">Required</span></span> | <span data-ttu-id="85bc6-164">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="85bc6-165">30 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-165">30 characters</span></span>|<span data-ttu-id="85bc6-166">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-166">✔</span></span>|<span data-ttu-id="85bc6-167">Nom d’affichage court de l’application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="85bc6-168">100 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-168">100 characters</span></span>||<span data-ttu-id="85bc6-169">Nom complet de l’application, utilisé si le nom complet de l’application dépasse 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="85bc6-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="85bc6-170">description</span><span class="sxs-lookup"><span data-stu-id="85bc6-170">description</span></span>

<span data-ttu-id="85bc6-171">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="85bc6-171">**Required** — object</span></span>

<span data-ttu-id="85bc6-172">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="85bc6-172">Describes your app to users.</span></span> <span data-ttu-id="85bc6-173">Pour les applications envoyées à AppSource, ces valeurs doivent correspondre aux informations de votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="85bc6-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="85bc6-174">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="85bc6-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="85bc6-175">Notez également, dans la description complète, si un compte externe est requis pour être utilisé.</span><span class="sxs-lookup"><span data-stu-id="85bc6-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="85bc6-176">Les valeurs `short` de et ne doivent pas être `full` identiques.</span><span class="sxs-lookup"><span data-stu-id="85bc6-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="85bc6-177">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="85bc6-178">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-178">Name</span></span>| <span data-ttu-id="85bc6-179">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-179">Maximum size</span></span> | <span data-ttu-id="85bc6-180">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-180">Required</span></span> | <span data-ttu-id="85bc6-181">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="85bc6-182">80 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-182">80 characters</span></span>|<span data-ttu-id="85bc6-183">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-183">✔</span></span>|<span data-ttu-id="85bc6-184">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="85bc6-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="85bc6-185">4 000 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-185">4000 characters</span></span>|<span data-ttu-id="85bc6-186">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-186">✔</span></span>|<span data-ttu-id="85bc6-187">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="85bc6-188">packageName</span><span class="sxs-lookup"><span data-stu-id="85bc6-188">packageName</span></span>

<span data-ttu-id="85bc6-189">**Facultatif —** chaîne</span><span class="sxs-lookup"><span data-stu-id="85bc6-189">**Optional** — string</span></span>

<span data-ttu-id="85bc6-190">Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com.example.myapp.</span><span class="sxs-lookup"><span data-stu-id="85bc6-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="85bc6-191">Longueur maximale : 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="85bc6-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="85bc6-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="85bc6-192">localizationInfo</span></span>

<span data-ttu-id="85bc6-193">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="85bc6-193">**Optional** — object</span></span>

<span data-ttu-id="85bc6-194">Autorise la spécification d’une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="85bc6-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="85bc6-195">Voir [localisation.](~/concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="85bc6-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="85bc6-196">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-196">Name</span></span>| <span data-ttu-id="85bc6-197">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-197">Maximum size</span></span> | <span data-ttu-id="85bc6-198">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-198">Required</span></span> | <span data-ttu-id="85bc6-199">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="85bc6-200">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-200">✔</span></span>|<span data-ttu-id="85bc6-201">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="85bc6-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="85bc6-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="85bc6-203">Tableau d’objets spécifiant des traductions linguistiques supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="85bc6-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="85bc6-204">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-204">Name</span></span>| <span data-ttu-id="85bc6-205">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-205">Maximum size</span></span> | <span data-ttu-id="85bc6-206">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-206">Required</span></span> | <span data-ttu-id="85bc6-207">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="85bc6-208">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-208">✔</span></span>|<span data-ttu-id="85bc6-209">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="85bc6-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="85bc6-210">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-210">✔</span></span>|<span data-ttu-id="85bc6-211">Chemin d’accès relatif au fichier .json contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="85bc6-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="85bc6-212">icons</span><span class="sxs-lookup"><span data-stu-id="85bc6-212">icons</span></span>

<span data-ttu-id="85bc6-213">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="85bc6-213">**Required** — object</span></span>

<span data-ttu-id="85bc6-214">Icônes utilisées dans l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="85bc6-214">Icons used within the Teams app.</span></span> <span data-ttu-id="85bc6-215">Les fichiers d’icône doivent être inclus dans le package de chargement.</span><span class="sxs-lookup"><span data-stu-id="85bc6-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="85bc6-216">Pour plus [d’informations,](../../concepts/build-and-test/apps-package.md#app-icons) voir Icônes.</span><span class="sxs-lookup"><span data-stu-id="85bc6-216">See [Icons](../../concepts/build-and-test/apps-package.md#app-icons) for more information.</span></span>

|<span data-ttu-id="85bc6-217">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-217">Name</span></span>| <span data-ttu-id="85bc6-218">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-218">Maximum size</span></span> | <span data-ttu-id="85bc6-219">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-219">Required</span></span> | <span data-ttu-id="85bc6-220">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="85bc6-221">32 x 32 pixels</span><span class="sxs-lookup"><span data-stu-id="85bc6-221">32 x 32 pixels</span></span>|<span data-ttu-id="85bc6-222">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-222">✔</span></span>|<span data-ttu-id="85bc6-223">Chemin d’accès relatif à un plan PNG transparent 32 x 32.</span><span class="sxs-lookup"><span data-stu-id="85bc6-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="85bc6-224">192 x 192 pixels</span><span class="sxs-lookup"><span data-stu-id="85bc6-224">192 x 192 pixels</span></span>|<span data-ttu-id="85bc6-225">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-225">✔</span></span>|<span data-ttu-id="85bc6-226">Chemin d’accès relatif à une icône PNG couleur 192 x 192.</span><span class="sxs-lookup"><span data-stu-id="85bc6-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="85bc6-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="85bc6-227">accentColor</span></span>

<span data-ttu-id="85bc6-228">**Facultatif** — Code de couleur HTML Hex</span><span class="sxs-lookup"><span data-stu-id="85bc6-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="85bc6-229">Couleur à utiliser conjointement avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="85bc6-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="85bc6-230">La valeur doit être un code de couleur HTML valide commençant par « # » par `#4464ee` exemple.</span><span class="sxs-lookup"><span data-stu-id="85bc6-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="85bc6-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="85bc6-231">configurableTabs</span></span>

<span data-ttu-id="85bc6-232">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="85bc6-232">**Optional** — array</span></span>

<span data-ttu-id="85bc6-233">Utilisé lorsque l’expérience de votre application possède une expérience d’onglet de canal d’équipe qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="85bc6-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="85bc6-234">Les onglets configurables sont pris en charge uniquement dans l’étendue Teams (et non personnelle), et actuellement, un seul **onglet** par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="85bc6-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="85bc6-235">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-235">Name</span></span>| <span data-ttu-id="85bc6-236">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-236">Type</span></span>| <span data-ttu-id="85bc6-237">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-237">Maximum size</span></span> | <span data-ttu-id="85bc6-238">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-238">Required</span></span> | <span data-ttu-id="85bc6-239">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="85bc6-240">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-240">string</span></span>|<span data-ttu-id="85bc6-241">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-241">2048 characters</span></span>|<span data-ttu-id="85bc6-242">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-242">✔</span></span>|<span data-ttu-id="85bc6-243">Url https:// à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="85bc6-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="85bc6-244">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="85bc6-244">array of enums</span></span>|<span data-ttu-id="85bc6-245">1 </span><span class="sxs-lookup"><span data-stu-id="85bc6-245">1</span></span>|<span data-ttu-id="85bc6-246">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-246">✔</span></span>|<span data-ttu-id="85bc6-247">Actuellement, les onglets configurables ne peuvent que les `team` étendues et les `groupchat` étendues.</span><span class="sxs-lookup"><span data-stu-id="85bc6-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="85bc6-248">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="85bc6-248">boolean</span></span>|||<span data-ttu-id="85bc6-249">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="85bc6-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="85bc6-250">Valeur par défaut **: true**.</span><span class="sxs-lookup"><span data-stu-id="85bc6-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="85bc6-251">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="85bc6-251">array of enums</span></span>|<span data-ttu-id="85bc6-252">6 </span><span class="sxs-lookup"><span data-stu-id="85bc6-252">6</span></span>||<span data-ttu-id="85bc6-253">Ensemble `contextItem` d’étendues où un onglet est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="85bc6-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="85bc6-254">Par défaut **: [channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="85bc6-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="85bc6-255">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-255">string</span></span>|<span data-ttu-id="85bc6-256">2048</span><span class="sxs-lookup"><span data-stu-id="85bc6-256">2048</span></span>||<span data-ttu-id="85bc6-257">Chemin d’accès relatif à une image d’aperçu d’onglet à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85bc6-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="85bc6-258">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="85bc6-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="85bc6-259">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="85bc6-259">array of enums</span></span>|<span data-ttu-id="85bc6-260">1 </span><span class="sxs-lookup"><span data-stu-id="85bc6-260">1</span></span>||<span data-ttu-id="85bc6-261">Définit la façon dont votre onglet sera disponible dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="85bc6-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="85bc6-262">Les options sont `sharePointFullPage` et `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="85bc6-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="85bc6-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="85bc6-263">staticTabs</span></span>

<span data-ttu-id="85bc6-264">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="85bc6-264">**Optional** — array</span></span>

<span data-ttu-id="85bc6-265">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="85bc6-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="85bc6-266">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="85bc6-267">Les onglets statiques déclarés dans `team` l’étendue ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="85bc6-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="85bc6-268">Cet élément est un tableau (maximum de 16 éléments) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="85bc6-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="85bc6-269">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="85bc6-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="85bc6-270">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-270">Name</span></span>| <span data-ttu-id="85bc6-271">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-271">Type</span></span>| <span data-ttu-id="85bc6-272">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-272">Maximum size</span></span> | <span data-ttu-id="85bc6-273">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-273">Required</span></span> | <span data-ttu-id="85bc6-274">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="85bc6-275">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-275">string</span></span>|<span data-ttu-id="85bc6-276">64 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-276">64 characters</span></span>|<span data-ttu-id="85bc6-277">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-277">✔</span></span>|<span data-ttu-id="85bc6-278">Identificateur unique de l’entité affichée par l’onglet.</span><span class="sxs-lookup"><span data-stu-id="85bc6-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="85bc6-279">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-279">string</span></span>|<span data-ttu-id="85bc6-280">128 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-280">128 characters</span></span>|<span data-ttu-id="85bc6-281">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-281">✔</span></span>|<span data-ttu-id="85bc6-282">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="85bc6-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="85bc6-283">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-283">string</span></span>||<span data-ttu-id="85bc6-284">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-284">✔</span></span>|<span data-ttu-id="85bc6-285">Url https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans le canevas Teams.</span><span class="sxs-lookup"><span data-stu-id="85bc6-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="85bc6-286">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-286">string</span></span>|||<span data-ttu-id="85bc6-287">L https:// URL pointant vers si un utilisateur choisit d’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="85bc6-288">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-288">string</span></span>|||<span data-ttu-id="85bc6-289">L https:// URL pointant vers les requêtes de recherche d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="85bc6-290">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="85bc6-290">array of enums</span></span>|<span data-ttu-id="85bc6-291">1 </span><span class="sxs-lookup"><span data-stu-id="85bc6-291">1</span></span>|<span data-ttu-id="85bc6-292">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-292">✔</span></span>|<span data-ttu-id="85bc6-293">Actuellement, les onglets statiques ne prendre en charge que l’étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de `personal` l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="85bc6-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="85bc6-294">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="85bc6-294">array of enums</span></span>| <span data-ttu-id="85bc6-295">2 </span><span class="sxs-lookup"><span data-stu-id="85bc6-295">2</span></span>|| <span data-ttu-id="85bc6-296">Ensemble `contextItem` d’étendues où un onglet est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="85bc6-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="85bc6-297">Si vos onglets nécessitent des informations contextielles pour afficher  du contenu pertinent ou pour lancer un flux d’authentification, voir Obtenir le contexte de votre [onglet Microsoft Teams.](../../tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="85bc6-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="85bc6-298">bots</span><span class="sxs-lookup"><span data-stu-id="85bc6-298">bots</span></span>

<span data-ttu-id="85bc6-299">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="85bc6-299">**Optional** — array</span></span>

<span data-ttu-id="85bc6-300">Définit une solution bot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="85bc6-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="85bc6-301">L’élément est un tableau (maximum de 1 élément actuellement un seul bot est autorisé par application) avec tous les éléments &mdash; du type `object` .</span><span class="sxs-lookup"><span data-stu-id="85bc6-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="85bc6-302">Ce bloc est requis uniquement pour les solutions qui offrent une expérience de bot.</span><span class="sxs-lookup"><span data-stu-id="85bc6-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="85bc6-303">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-303">Name</span></span>| <span data-ttu-id="85bc6-304">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-304">Type</span></span>| <span data-ttu-id="85bc6-305">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-305">Maximum size</span></span> | <span data-ttu-id="85bc6-306">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-306">Required</span></span> | <span data-ttu-id="85bc6-307">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="85bc6-308">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-308">string</span></span>|<span data-ttu-id="85bc6-309">64 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-309">64 characters</span></span>|<span data-ttu-id="85bc6-310">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-310">✔</span></span>|<span data-ttu-id="85bc6-311">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="85bc6-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="85bc6-312">Cela peut être identique à [l’ID d’application global.](#id)</span><span class="sxs-lookup"><span data-stu-id="85bc6-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="85bc6-313">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="85bc6-313">array of enums</span></span>|<span data-ttu-id="85bc6-314">3 </span><span class="sxs-lookup"><span data-stu-id="85bc6-314">3</span></span>|<span data-ttu-id="85bc6-315">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-315">✔</span></span>|<span data-ttu-id="85bc6-316">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="85bc6-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="85bc6-317">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="85bc6-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="85bc6-318">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="85bc6-318">boolean</span></span>|||<span data-ttu-id="85bc6-319">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="85bc6-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="85bc6-320">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="85bc6-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="85bc6-321">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="85bc6-321">boolean</span></span>|||<span data-ttu-id="85bc6-322">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="85bc6-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="85bc6-323">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="85bc6-323">Default: **`false`**</span></span>|
|`supportsFiles`|<span data-ttu-id="85bc6-324">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="85bc6-324">boolean</span></span>|||<span data-ttu-id="85bc6-325">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="85bc6-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="85bc6-326">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="85bc6-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="85bc6-327">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="85bc6-327">boolean</span></span>|||<span data-ttu-id="85bc6-328">Valeur indiquant où un bot prend en charge les appels audio.</span><span class="sxs-lookup"><span data-stu-id="85bc6-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="85bc6-329">**IMPORTANT**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="85bc6-329">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="85bc6-330">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="85bc6-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="85bc6-331">Il est fourni uniquement à des fins de test et d’exploration et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="85bc6-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="85bc6-332">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="85bc6-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="85bc6-333">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="85bc6-333">boolean</span></span>|||<span data-ttu-id="85bc6-334">Valeur indiquant où un bot prend en charge les appels vidéo.</span><span class="sxs-lookup"><span data-stu-id="85bc6-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="85bc6-335">**IMPORTANT**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="85bc6-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="85bc6-336">Les propriétés expérimentales peuvent ne pas être complètes et peuvent subir des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="85bc6-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="85bc6-337">Il est fourni uniquement à des fins de test et d’exploration et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="85bc6-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="85bc6-338">Valeur par défaut : **`false`**</span><span class="sxs-lookup"><span data-stu-id="85bc6-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="85bc6-339">bots.commandLists</span><span class="sxs-lookup"><span data-stu-id="85bc6-339">bots.commandLists</span></span>

<span data-ttu-id="85bc6-340">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="85bc6-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="85bc6-341">L’objet est un tableau (maximum de 2 éléments) avec tous les éléments de type ; vous devez définir une liste de commandes distincte pour chaque étendue que votre `object` bot prend en charge.</span><span class="sxs-lookup"><span data-stu-id="85bc6-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="85bc6-342">Pour plus [d’informations,](~/bots/how-to/create-a-bot-commands-menu.md) voir les menus du bot.</span><span class="sxs-lookup"><span data-stu-id="85bc6-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="85bc6-343">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-343">Name</span></span>| <span data-ttu-id="85bc6-344">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-344">Type</span></span>| <span data-ttu-id="85bc6-345">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-345">Maximum size</span></span> | <span data-ttu-id="85bc6-346">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-346">Required</span></span> | <span data-ttu-id="85bc6-347">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="85bc6-348">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="85bc6-348">array of enums</span></span>|<span data-ttu-id="85bc6-349">3 </span><span class="sxs-lookup"><span data-stu-id="85bc6-349">3</span></span>|<span data-ttu-id="85bc6-350">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-350">✔</span></span>|<span data-ttu-id="85bc6-351">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="85bc6-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="85bc6-352">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="85bc6-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="85bc6-353">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="85bc6-353">array of objects</span></span>|<span data-ttu-id="85bc6-354">10 </span><span class="sxs-lookup"><span data-stu-id="85bc6-354">10</span></span>|<span data-ttu-id="85bc6-355">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-355">✔</span></span>|<span data-ttu-id="85bc6-356">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="85bc6-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="85bc6-357">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="85bc6-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="85bc6-358">`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)</span><span class="sxs-lookup"><span data-stu-id="85bc6-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="85bc6-359">bots.commandLists.commands</span><span class="sxs-lookup"><span data-stu-id="85bc6-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="85bc6-360">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-360">Name</span></span>| <span data-ttu-id="85bc6-361">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-361">Type</span></span>| <span data-ttu-id="85bc6-362">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-362">Maximum size</span></span> | <span data-ttu-id="85bc6-363">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-363">Required</span></span> | <span data-ttu-id="85bc6-364">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="85bc6-365">title</span><span class="sxs-lookup"><span data-stu-id="85bc6-365">title</span></span>|<span data-ttu-id="85bc6-366">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-366">string</span></span>|<span data-ttu-id="85bc6-367">12 </span><span class="sxs-lookup"><span data-stu-id="85bc6-367">12</span></span>|<span data-ttu-id="85bc6-368">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-368">✔</span></span>|<span data-ttu-id="85bc6-369">Nom de la commande du bot</span><span class="sxs-lookup"><span data-stu-id="85bc6-369">The bot command name</span></span>|
|<span data-ttu-id="85bc6-370">description</span><span class="sxs-lookup"><span data-stu-id="85bc6-370">description</span></span>|<span data-ttu-id="85bc6-371">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-371">string</span></span>|<span data-ttu-id="85bc6-372">128 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-372">128 characters</span></span>|<span data-ttu-id="85bc6-373">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-373">✔</span></span>|<span data-ttu-id="85bc6-374">Description de texte simple ou exemple de syntaxe de commande et de ses arguments.</span><span class="sxs-lookup"><span data-stu-id="85bc6-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="85bc6-375">connecteurs</span><span class="sxs-lookup"><span data-stu-id="85bc6-375">connectors</span></span>

<span data-ttu-id="85bc6-376">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="85bc6-376">**Optional** — array</span></span>

<span data-ttu-id="85bc6-377">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="85bc6-378">L’objet est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="85bc6-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="85bc6-379">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="85bc6-380">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-380">Name</span></span>| <span data-ttu-id="85bc6-381">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-381">Type</span></span>| <span data-ttu-id="85bc6-382">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-382">Maximum size</span></span> | <span data-ttu-id="85bc6-383">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-383">Required</span></span> | <span data-ttu-id="85bc6-384">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="85bc6-385">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-385">string</span></span>|<span data-ttu-id="85bc6-386">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-386">2048 characters</span></span>|<span data-ttu-id="85bc6-387">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-387">✔</span></span>|<span data-ttu-id="85bc6-388">Url https:// à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="85bc6-389">tableau d’enums</span><span class="sxs-lookup"><span data-stu-id="85bc6-389">array of enums</span></span>|<span data-ttu-id="85bc6-390">1 </span><span class="sxs-lookup"><span data-stu-id="85bc6-390">1</span></span>|<span data-ttu-id="85bc6-391">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-391">✔</span></span>|<span data-ttu-id="85bc6-392">Spécifie si le connecteur offre une expérience dans le contexte d’un canal dans un , ou une expérience limitée à un `team` utilisateur individuel seul ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="85bc6-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="85bc6-393">Actuellement, seule `team` l’étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="85bc6-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="85bc6-394">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-394">string</span></span>|<span data-ttu-id="85bc6-395">64 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-395">64 characters</span></span>|<span data-ttu-id="85bc6-396">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-396">✔</span></span>|<span data-ttu-id="85bc6-397">Identificateur unique du connecteur qui correspond à son ID dans le tableau de bord du [développeur de connecteurs.](https://aka.ms/connectorsdashboard)</span><span class="sxs-lookup"><span data-stu-id="85bc6-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="85bc6-398">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="85bc6-398">composeExtensions</span></span>

<span data-ttu-id="85bc6-399">**Facultatif** — tableau</span><span class="sxs-lookup"><span data-stu-id="85bc6-399">**Optional** — array</span></span>

<span data-ttu-id="85bc6-400">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="85bc6-401">Le nom de la fonctionnalité a été modifié de « extension de composition » à « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même pour que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="85bc6-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="85bc6-402">L’élément est un tableau (maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="85bc6-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="85bc6-403">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="85bc6-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="85bc6-404">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-404">Name</span></span>| <span data-ttu-id="85bc6-405">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-405">Type</span></span> | <span data-ttu-id="85bc6-406">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-406">Maximum Size</span></span> | <span data-ttu-id="85bc6-407">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="85bc6-407">Required</span></span> | <span data-ttu-id="85bc6-408">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="85bc6-409">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-409">string</span></span>|<span data-ttu-id="85bc6-410">64</span><span class="sxs-lookup"><span data-stu-id="85bc6-410">64</span></span>|<span data-ttu-id="85bc6-411">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-411">✔</span></span>|<span data-ttu-id="85bc6-412">ID d’application Microsoft unique pour le bot qui permet de récupérer l’extension de messagerie, tel qu’inscrit auprès de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="85bc6-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="85bc6-413">Cela peut être identique à l’ID d’application global.</span><span class="sxs-lookup"><span data-stu-id="85bc6-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="85bc6-414">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="85bc6-414">array of objects</span></span>|<span data-ttu-id="85bc6-415">10 </span><span class="sxs-lookup"><span data-stu-id="85bc6-415">10</span></span>|<span data-ttu-id="85bc6-416">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-416">✔</span></span>|<span data-ttu-id="85bc6-417">Tableau de commandes pris en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="85bc6-417">Array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="85bc6-418">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="85bc6-418">boolean</span></span>|||<span data-ttu-id="85bc6-419">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="85bc6-420">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="85bc6-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="85bc6-421">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="85bc6-421">array of Objects</span></span>|<span data-ttu-id="85bc6-422">5 </span><span class="sxs-lookup"><span data-stu-id="85bc6-422">5</span></span>||<span data-ttu-id="85bc6-423">Liste des handlers qui permettent d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="85bc6-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span>|
|`messageHandlers.type`|<span data-ttu-id="85bc6-424">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-424">string</span></span>|||<span data-ttu-id="85bc6-425">Type de handler de messages.</span><span class="sxs-lookup"><span data-stu-id="85bc6-425">The type of message handler.</span></span> <span data-ttu-id="85bc6-426">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="85bc6-426">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="85bc6-427">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="85bc6-427">array of Strings</span></span>|||<span data-ttu-id="85bc6-428">Tableau de domaines pour l’inscription du handler de message de lien.</span><span class="sxs-lookup"><span data-stu-id="85bc6-428">Array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="85bc6-429">composeExtensions.commands</span><span class="sxs-lookup"><span data-stu-id="85bc6-429">composeExtensions.commands</span></span>

<span data-ttu-id="85bc6-430">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="85bc6-430">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="85bc6-431">Chaque commande apparaît dans Microsoft Teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-431">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="85bc6-432">Il existe un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="85bc6-432">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="85bc6-433">Chaque élément de commande est un objet avec la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="85bc6-433">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="85bc6-434">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-434">Name</span></span>| <span data-ttu-id="85bc6-435">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-435">Type</span></span>| <span data-ttu-id="85bc6-436">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-436">Maximum size</span></span> | <span data-ttu-id="85bc6-437">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-437">Required</span></span> | <span data-ttu-id="85bc6-438">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-438">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="85bc6-439">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-439">string</span></span>|<span data-ttu-id="85bc6-440">64 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-440">64 characters</span></span>|<span data-ttu-id="85bc6-441">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-441">✔</span></span>|<span data-ttu-id="85bc6-442">ID de la commande.</span><span class="sxs-lookup"><span data-stu-id="85bc6-442">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="85bc6-443">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-443">string</span></span>|<span data-ttu-id="85bc6-444">32 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-444">32 characters</span></span>|<span data-ttu-id="85bc6-445">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-445">✔</span></span>|<span data-ttu-id="85bc6-446">Nom de la commande conviviale.</span><span class="sxs-lookup"><span data-stu-id="85bc6-446">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="85bc6-447">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-447">string</span></span>|<span data-ttu-id="85bc6-448">64 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-448">64 characters</span></span>||<span data-ttu-id="85bc6-449">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="85bc6-449">Type of the command.</span></span> <span data-ttu-id="85bc6-450">L’un `query` ou `action` l’autre .</span><span class="sxs-lookup"><span data-stu-id="85bc6-450">One of `query` or `action`.</span></span> <span data-ttu-id="85bc6-451">Par défaut : **requête**.</span><span class="sxs-lookup"><span data-stu-id="85bc6-451">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="85bc6-452">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-452">string</span></span>|<span data-ttu-id="85bc6-453">128 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-453">128 characters</span></span>||<span data-ttu-id="85bc6-454">Description qui apparaît aux utilisateurs pour indiquer l’objectif de cette commande.</span><span class="sxs-lookup"><span data-stu-id="85bc6-454">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="85bc6-455">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="85bc6-455">boolean</span></span>|||<span data-ttu-id="85bc6-456">Valeur booléle qui indique si la commande doit être exécuté initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="85bc6-456">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="85bc6-457">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="85bc6-457">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="85bc6-458">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="85bc6-458">array of Strings</span></span>|<span data-ttu-id="85bc6-459">3 </span><span class="sxs-lookup"><span data-stu-id="85bc6-459">3</span></span>||<span data-ttu-id="85bc6-460">Définit l’endroit à partir de lequel l’extension de message peut être invoquée.</span><span class="sxs-lookup"><span data-stu-id="85bc6-460">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="85bc6-461">N’importe quelle `compose` combinaison de `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="85bc6-461">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="85bc6-462">La valeur par défaut est `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="85bc6-462">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="85bc6-463">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="85bc6-463">boolean</span></span>|||<span data-ttu-id="85bc6-464">Valeur booléle qui indique s’il doit extraire dynamiquement le module de tâche.</span><span class="sxs-lookup"><span data-stu-id="85bc6-464">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="85bc6-465">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="85bc6-465">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="85bc6-466">objet</span><span class="sxs-lookup"><span data-stu-id="85bc6-466">object</span></span>|||<span data-ttu-id="85bc6-467">Spécifiez le module de tâche à pré-charger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="85bc6-467">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="85bc6-468">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-468">string</span></span>|<span data-ttu-id="85bc6-469">64 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-469">64 characters</span></span>||<span data-ttu-id="85bc6-470">Titre de la boîte de dialogue initiale.</span><span class="sxs-lookup"><span data-stu-id="85bc6-470">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="85bc6-471">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-471">string</span></span>|||<span data-ttu-id="85bc6-472">Largeur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="85bc6-472">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="85bc6-473">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-473">string</span></span>|||<span data-ttu-id="85bc6-474">Hauteur de la boîte de dialogue : nombre en pixels ou disposition par défaut telle que « grande » , « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="85bc6-474">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="85bc6-475">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-475">string</span></span>|||<span data-ttu-id="85bc6-476">URL webview initiale.</span><span class="sxs-lookup"><span data-stu-id="85bc6-476">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="85bc6-477">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="85bc6-477">array of object</span></span>|<span data-ttu-id="85bc6-478">5 éléments</span><span class="sxs-lookup"><span data-stu-id="85bc6-478">5 items</span></span>|<span data-ttu-id="85bc6-479">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-479">✔</span></span>|<span data-ttu-id="85bc6-480">Liste des paramètres pris par la commande.</span><span class="sxs-lookup"><span data-stu-id="85bc6-480">The list of parameters the command takes.</span></span> <span data-ttu-id="85bc6-481">Minimum : 1 ; maximum : 5.</span><span class="sxs-lookup"><span data-stu-id="85bc6-481">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="85bc6-482">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-482">string</span></span>|<span data-ttu-id="85bc6-483">64 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-483">64 characters</span></span>|<span data-ttu-id="85bc6-484">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-484">✔</span></span>|<span data-ttu-id="85bc6-485">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="85bc6-485">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="85bc6-486">Ceci est inclus dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-486">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="85bc6-487">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-487">string</span></span>|<span data-ttu-id="85bc6-488">32 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-488">32 characters</span></span>|<span data-ttu-id="85bc6-489">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-489">✔</span></span>|<span data-ttu-id="85bc6-490">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="85bc6-490">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="85bc6-491">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-491">string</span></span>|<span data-ttu-id="85bc6-492">128 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-492">128 characters</span></span>||<span data-ttu-id="85bc6-493">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="85bc6-493">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="85bc6-494">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-494">string</span></span>|<span data-ttu-id="85bc6-495">512 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-495">512 characters</span></span>||<span data-ttu-id="85bc6-496">Valeur initiale du paramètre.</span><span class="sxs-lookup"><span data-stu-id="85bc6-496">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="85bc6-497">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-497">string</span></span>|<span data-ttu-id="85bc6-498">128 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-498">128 characters</span></span>||<span data-ttu-id="85bc6-499">Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="85bc6-499">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="85bc6-500">L’une `text, textarea, number, date, time, toggle, choiceset` des .</span><span class="sxs-lookup"><span data-stu-id="85bc6-500">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="85bc6-501">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="85bc6-501">array of objects</span></span>|<span data-ttu-id="85bc6-502">10 éléments</span><span class="sxs-lookup"><span data-stu-id="85bc6-502">10 items</span></span>||<span data-ttu-id="85bc6-503">Options de choix pour `choiceset` le .</span><span class="sxs-lookup"><span data-stu-id="85bc6-503">The choice options for the`choiceset`.</span></span> <span data-ttu-id="85bc6-504">Utilisez uniquement lorsque `parameter.inputType` `choiceset` c’est le cas.</span><span class="sxs-lookup"><span data-stu-id="85bc6-504">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="85bc6-505">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-505">string</span></span>|<span data-ttu-id="85bc6-506">128 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-506">128 characters</span></span>|<span data-ttu-id="85bc6-507">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-507">✔</span></span>|<span data-ttu-id="85bc6-508">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="85bc6-508">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="85bc6-509">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-509">string</span></span>|<span data-ttu-id="85bc6-510">512 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-510">512 characters</span></span>|<span data-ttu-id="85bc6-511">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-511">✔</span></span>|<span data-ttu-id="85bc6-512">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="85bc6-512">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="85bc6-513">autorisations</span><span class="sxs-lookup"><span data-stu-id="85bc6-513">permissions</span></span>

<span data-ttu-id="85bc6-514">**Facultatif** : tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="85bc6-514">**Optional** — array of strings</span></span>

<span data-ttu-id="85bc6-515">Tableau qui spécifie les autorisations que l’application demande, ce qui permet aux utilisateurs finaux de savoir comment `string` l’extension va s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="85bc6-515">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="85bc6-516">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="85bc6-516">The following options are non-exclusive:</span></span>

* <span data-ttu-id="85bc6-517">`identity`&emsp;Nécessite des informations d’identité d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="85bc6-517">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="85bc6-518">`messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="85bc6-518">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="85bc6-519">La modification de ces autorisations lors de la mise à jour de votre application entraîne la répétition du processus de consentement par vos utilisateurs la première fois qu’ils exécutent l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="85bc6-519">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="85bc6-520">Pour plus [d’informations, voir](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) Mise à jour de votre application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-520">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="85bc6-521">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="85bc6-521">devicePermissions</span></span>

<span data-ttu-id="85bc6-522">**Facultatif** : tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="85bc6-522">**Optional** — array of strings</span></span>

<span data-ttu-id="85bc6-523">Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur à qui votre application peut demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="85bc6-523">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="85bc6-524">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="85bc6-524">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="85bc6-525">validDomains</span><span class="sxs-lookup"><span data-stu-id="85bc6-525">validDomains</span></span>

<span data-ttu-id="85bc6-526">**Facultatif,** sauf **obligatoire lorsqu’il** est indiqué</span><span class="sxs-lookup"><span data-stu-id="85bc6-526">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="85bc6-527">Liste des domaines valides pour les sites web que l’application s’attend à charger dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="85bc6-527">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="85bc6-528">Les listes de domaines peuvent inclure des caractères génériques, par `*.example.com` exemple.</span><span class="sxs-lookup"><span data-stu-id="85bc6-528">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="85bc6-529">Cela correspond exactement à un segment du domaine ; si vous avez besoin d’une `a.b.example.com` correspondance, utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="85bc6-529">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="85bc6-530">Si votre interface utilisateur de contenu ou de configuration d’onglet doit accéder à un autre domaine en plus de celui utilisé pour la configuration de l’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="85bc6-530">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="85bc6-531">**Toutefois, il** n’est pas nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-531">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="85bc6-532">Par exemple, pour vous authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="85bc6-532">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="85bc6-533">Les applications Teams qui nécessitent leurs propres URL sharepoint pour fonctionner bien peuvent inclure « {teamsitedomain} » dans leur liste de domaines valide.</span><span class="sxs-lookup"><span data-stu-id="85bc6-533">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="85bc6-534">N’ajoutez pas de domaines qui sont en dehors de votre contrôle, directement ou par le biais de caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="85bc6-534">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="85bc6-535">Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="85bc6-535">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="85bc6-536">L’objet est un tableau avec tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="85bc6-536">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="85bc6-537">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="85bc6-537">webApplicationInfo</span></span>

<span data-ttu-id="85bc6-538">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="85bc6-538">**Optional** — object</span></span>

<span data-ttu-id="85bc6-539">Spécifiez votre ID d’application Azure Active Directory (Azure AD) et les informations De Microsoft Graph pour aider les utilisateurs à se connecter en toute transparence à votre application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-539">Specify your Azure Active Directory (Azure AD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="85bc6-540">Si votre application est inscrite dans Azure AD, vous devez fournir l’ID de l’application, afin que les administrateurs peuvent facilement passer en revue les autorisations et accorder leur consentement dans le Centre d’administration Teams.</span><span class="sxs-lookup"><span data-stu-id="85bc6-540">If your app is registered in Azure AD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="85bc6-541">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-541">Name</span></span>| <span data-ttu-id="85bc6-542">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-542">Type</span></span>| <span data-ttu-id="85bc6-543">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-543">Maximum size</span></span> | <span data-ttu-id="85bc6-544">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-544">Required</span></span> | <span data-ttu-id="85bc6-545">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-545">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="85bc6-546">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-546">string</span></span>|<span data-ttu-id="85bc6-547">36 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-547">36 characters</span></span>|<span data-ttu-id="85bc6-548">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-548">✔</span></span>|<span data-ttu-id="85bc6-549">ID d’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="85bc6-549">AAD application id of the app.</span></span> <span data-ttu-id="85bc6-550">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="85bc6-550">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="85bc6-551">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-551">string</span></span>|<span data-ttu-id="85bc6-552">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-552">2048 characters</span></span>|<span data-ttu-id="85bc6-553">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-553">✔</span></span>|<span data-ttu-id="85bc6-554">URL de ressource de l’application pour l’acquisition d’un jeton d’th pour l' sso.</span><span class="sxs-lookup"><span data-stu-id="85bc6-554">Resource URL of app for acquiring auth token for SSO.</span></span> </br> <span data-ttu-id="85bc6-555">**REMARQUE :** Si vous n’utilisez pas l’oD SSO, veillez à entrer une valeur de chaîne factice dans ce champ dans le manifeste de votre application, par exemple, pour éviter une réponse https://notapplicable d’erreur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-555">**NOTE:** If you are not using SSO, ensure that you enter a dummy string value in this field to your app manifest, for example, https://notapplicable to avoid an error response.</span></span> |
|`applicationPermissions`|<span data-ttu-id="85bc6-556">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="85bc6-556">array of strings</span></span>|<span data-ttu-id="85bc6-557">128 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-557">128 characters</span></span>||<span data-ttu-id="85bc6-558">Spécifiez le consentement précis [spécifique à une ressource.](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span><span class="sxs-lookup"><span data-stu-id="85bc6-558">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions).</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="85bc6-559">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="85bc6-559">showLoadingIndicator</span></span>

<span data-ttu-id="85bc6-560">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="85bc6-560">**Optional** — boolean</span></span>

<span data-ttu-id="85bc6-561">Indiquez si l’indicateur de chargement s’affiche ou non lorsqu’une application/un onglet est en cours de chargement.</span><span class="sxs-lookup"><span data-stu-id="85bc6-561">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="85bc6-562">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="85bc6-562">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="85bc6-563">Si vous définissez « showLoadingIndicator : true » dans le manifeste de votre application, pour que la page se charge correctement, vous devez modifier les pages de contenu de vos onglets et modules de tâche selon le protocole décrit dans Afficher un [document](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) d’indicateur de chargement natif.</span><span class="sxs-lookup"><span data-stu-id="85bc6-563">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="85bc6-564">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="85bc6-564">isFullScreen</span></span>

 <span data-ttu-id="85bc6-565">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="85bc6-565">**Optional** — boolean</span></span>

<span data-ttu-id="85bc6-566">Indiquez l’endroit où une application personnelle est rendue avec ou sans barre d’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="85bc6-566">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="85bc6-567">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="85bc6-567">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="85bc6-568">activités</span><span class="sxs-lookup"><span data-stu-id="85bc6-568">activities</span></span>

<span data-ttu-id="85bc6-569">**Facultatif** — objet</span><span class="sxs-lookup"><span data-stu-id="85bc6-569">**Optional** — object</span></span>

<span data-ttu-id="85bc6-570">Définissez les propriétés que votre application utilisera pour publier dans un flux d’activités utilisateur.</span><span class="sxs-lookup"><span data-stu-id="85bc6-570">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="85bc6-571">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-571">Name</span></span>| <span data-ttu-id="85bc6-572">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-572">Type</span></span>| <span data-ttu-id="85bc6-573">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-573">Maximum size</span></span> | <span data-ttu-id="85bc6-574">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-574">Required</span></span> | <span data-ttu-id="85bc6-575">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-575">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="85bc6-576">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="85bc6-576">array of Objects</span></span>|<span data-ttu-id="85bc6-577">128 éléments</span><span class="sxs-lookup"><span data-stu-id="85bc6-577">128 items</span></span>| | <span data-ttu-id="85bc6-578">Spécifiez les types d’activités que votre application peut publier dans un flux d’activités des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="85bc6-578">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="85bc6-579">activities.activityTypes</span><span class="sxs-lookup"><span data-stu-id="85bc6-579">activities.activityTypes</span></span>

|<span data-ttu-id="85bc6-580">Nom</span><span class="sxs-lookup"><span data-stu-id="85bc6-580">Name</span></span>| <span data-ttu-id="85bc6-581">Type</span><span class="sxs-lookup"><span data-stu-id="85bc6-581">Type</span></span>| <span data-ttu-id="85bc6-582">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="85bc6-582">Maximum size</span></span> | <span data-ttu-id="85bc6-583">Requis</span><span class="sxs-lookup"><span data-stu-id="85bc6-583">Required</span></span> | <span data-ttu-id="85bc6-584">Description</span><span class="sxs-lookup"><span data-stu-id="85bc6-584">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="85bc6-585">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-585">string</span></span>|<span data-ttu-id="85bc6-586">32 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-586">32 characters</span></span>|<span data-ttu-id="85bc6-587">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-587">✔</span></span>|<span data-ttu-id="85bc6-588">Type de notification.</span><span class="sxs-lookup"><span data-stu-id="85bc6-588">The notification type.</span></span> <span data-ttu-id="85bc6-589">*Voir ci-dessous.*</span><span class="sxs-lookup"><span data-stu-id="85bc6-589">*See below*.</span></span>|
|`description`|<span data-ttu-id="85bc6-590">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-590">string</span></span>|<span data-ttu-id="85bc6-591">128 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-591">128 characters</span></span>|<span data-ttu-id="85bc6-592">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-592">✔</span></span>|<span data-ttu-id="85bc6-593">Brève description de la notification.</span><span class="sxs-lookup"><span data-stu-id="85bc6-593">A brief description of the notification.</span></span> <span data-ttu-id="85bc6-594">*Voir ci-dessous.*</span><span class="sxs-lookup"><span data-stu-id="85bc6-594">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="85bc6-595">string</span><span class="sxs-lookup"><span data-stu-id="85bc6-595">string</span></span>|<span data-ttu-id="85bc6-596">128 caractères</span><span class="sxs-lookup"><span data-stu-id="85bc6-596">128 characters</span></span>|<span data-ttu-id="85bc6-597">✔</span><span class="sxs-lookup"><span data-stu-id="85bc6-597">✔</span></span>|<span data-ttu-id="85bc6-598">Ex: « {actor} created task {taskId} for you »</span><span class="sxs-lookup"><span data-stu-id="85bc6-598">Ex: "{actor} created task {taskId} for you"</span></span>|

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
