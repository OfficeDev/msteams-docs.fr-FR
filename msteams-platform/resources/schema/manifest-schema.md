---
title: Référence du schéma de manifeste
description: Décrit le schéma de manifeste de Microsoft teams
keywords: schéma de manifeste teams
author: laujan
ms.author: lajanuar
ms.openlocfilehash: 26c6ca0ed6edceb9b34c84c28a43a63f65a348de
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552555"
---
# <a name="reference-manifest-schema-for-microsoft-teams"></a><span data-ttu-id="b3433-104">Référence : schéma de manifeste pour Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="b3433-104">Reference: Manifest schema for Microsoft Teams</span></span>

<span data-ttu-id="b3433-105">Le manifeste Microsoft teams décrit la façon dont l’application s’intègre dans le produit Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="b3433-105">The Microsoft Teams manifest describes how the app integrates into the Microsoft Teams product.</span></span> <span data-ttu-id="b3433-106">Votre manifeste doit être conforme au schéma hébergé sur [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json) .</span><span class="sxs-lookup"><span data-stu-id="b3433-106">Your manifest must conform to the schema hosted at [`https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json`]( https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json).</span></span> <span data-ttu-id="b3433-107">Les versions précédentes 1.0 à 1.4 sont également prises en charge (à l’aide de « v1. x » dans l’URL).</span><span class="sxs-lookup"><span data-stu-id="b3433-107">Previous versions 1.0-1.4 are also supported (using "v1.x" in the URL).</span></span>

<span data-ttu-id="b3433-108">L’exemple de schéma suivant montre toutes les options d’extensibilité.</span><span class="sxs-lookup"><span data-stu-id="b3433-108">The following schema sample shows all extensibility options.</span></span>

## <a name="sample-full-manifest"></a><span data-ttu-id="b3433-109">Exemple de manifeste complet</span><span class="sxs-lookup"><span data-stu-id="b3433-109">Sample full manifest</span></span>

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

<span data-ttu-id="b3433-110">Le schéma définit les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3433-110">The schema defines the following properties:</span></span>

## <a name="schema"></a><span data-ttu-id="b3433-111">$schema</span><span class="sxs-lookup"><span data-stu-id="b3433-111">$schema</span></span>

<span data-ttu-id="b3433-112">*Facultatif, mais recommandé* — String</span><span class="sxs-lookup"><span data-stu-id="b3433-112">*Optional, but recommended* — string</span></span>

<span data-ttu-id="b3433-113">URL https://référençant le schéma JSON du manifeste.</span><span class="sxs-lookup"><span data-stu-id="b3433-113">The https:// URL referencing the JSON Schema for the manifest.</span></span>

## <a name="manifestversion"></a><span data-ttu-id="b3433-114">manifestVersion</span><span class="sxs-lookup"><span data-stu-id="b3433-114">manifestVersion</span></span>

<span data-ttu-id="b3433-115">**Required** — String</span><span class="sxs-lookup"><span data-stu-id="b3433-115">**Required** — string</span></span>

<span data-ttu-id="b3433-116">Version du schéma de manifeste utilisé par ce manifeste.</span><span class="sxs-lookup"><span data-stu-id="b3433-116">The version of the manifest schema this manifest is using.</span></span> <span data-ttu-id="b3433-117">Il doit être « 1,7 ».</span><span class="sxs-lookup"><span data-stu-id="b3433-117">It should be "1.7".</span></span>

## <a name="version"></a><span data-ttu-id="b3433-118">version</span><span class="sxs-lookup"><span data-stu-id="b3433-118">version</span></span>

<span data-ttu-id="b3433-119">**Required** — String</span><span class="sxs-lookup"><span data-stu-id="b3433-119">**Required** — string</span></span>

<span data-ttu-id="b3433-120">Version de l’application spécifique.</span><span class="sxs-lookup"><span data-stu-id="b3433-120">The version of the specific app.</span></span> <span data-ttu-id="b3433-121">Si vous mettez à jour un événement dans votre manifeste, la version doit également être incrémentée.</span><span class="sxs-lookup"><span data-stu-id="b3433-121">If you update something in your manifest, the version must be incremented as well.</span></span> <span data-ttu-id="b3433-122">Ainsi, lorsque le nouveau manifeste est installé, il remplace celui existant et l’utilisateur a accès aux nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="b3433-122">This way, when the new manifest is installed, it will overwrite the existing one and the user will get the new functionality.</span></span> <span data-ttu-id="b3433-123">Si cette application a été envoyée au magasin, le nouveau manifeste doit être soumis à nouveau et revalidé.</span><span class="sxs-lookup"><span data-stu-id="b3433-123">If this app was submitted to the store, the new manifest will have to be re-submitted and re-validated.</span></span> <span data-ttu-id="b3433-124">Ensuite, les utilisateurs de cette application obtiendront automatiquement le nouveau manifeste mis à jour en quelques heures, une fois celui-ci approuvé.</span><span class="sxs-lookup"><span data-stu-id="b3433-124">Then, users of this app will get the new updated manifest automatically in a few hours, after it is approved.</span></span>

<span data-ttu-id="b3433-125">Si l’application a demandé une modification des autorisations, les utilisateurs sont invités à effectuer une mise à niveau et à reconfigurer l’application.</span><span class="sxs-lookup"><span data-stu-id="b3433-125">If the app requested permissions change, users will be prompted to upgrade and re-consent to the app.</span></span>

<span data-ttu-id="b3433-126">Cette chaîne de version doit suivre la norme [semver](http://semver.org/) (major. Petites. CORRECTIF).</span><span class="sxs-lookup"><span data-stu-id="b3433-126">This version string must follow the [semver](http://semver.org/) standard (MAJOR.MINOR.PATCH).</span></span>

## <a name="id"></a><span data-ttu-id="b3433-127">id</span><span class="sxs-lookup"><span data-stu-id="b3433-127">id</span></span>

<span data-ttu-id="b3433-128">**Obligatoire** — ID de l’application Microsoft</span><span class="sxs-lookup"><span data-stu-id="b3433-128">**Required** — Microsoft app ID</span></span>

<span data-ttu-id="b3433-129">Identificateur unique généré par Microsoft pour cette application.</span><span class="sxs-lookup"><span data-stu-id="b3433-129">The unique Microsoft-generated identifier for this app.</span></span> <span data-ttu-id="b3433-130">Si vous avez inscrit un robot via Microsoft bot Framework ou si l’application Web de votre onglet se connecte déjà à Microsoft, vous devez déjà avoir un ID et l’entrer ici.</span><span class="sxs-lookup"><span data-stu-id="b3433-130">If you have registered a bot via the Microsoft Bot Framework, or your tab's web app already signs in with Microsoft, you should already have an ID and should enter it here.</span></span> <span data-ttu-id="b3433-131">Dans le cas contraire, vous devez générer un nouvel ID dans le portail d’inscription des applications Microsoft ([mes applications](https://apps.dev.microsoft.com)), l’entrer ici, puis le réutiliser lorsque vous ajoutez un bot. Remarque : Si vous envoyez une mise à jour à votre application existante dans AppSource, l’ID de votre manifeste ne doit pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="b3433-131">Otherwise, you should generate a new ID at the Microsoft Application Registration Portal ([My Applications](https://apps.dev.microsoft.com)), enter it here, and then reuse it when you add a bot.Note: If you are submitting an update to your existing app in AppSource, the ID in your manifest must not be modified.</span></span>

## <a name="developer"></a><span data-ttu-id="b3433-132">developer</span><span class="sxs-lookup"><span data-stu-id="b3433-132">developer</span></span>

<span data-ttu-id="b3433-133">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="b3433-133">**Required** — object</span></span>

<span data-ttu-id="b3433-134">Spécifie les informations relatives à votre société.</span><span class="sxs-lookup"><span data-stu-id="b3433-134">Specifies information about your company.</span></span> <span data-ttu-id="b3433-135">Pour les applications soumises à AppSource (anciennement Office Store), ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="b3433-135">For apps submitted to AppSource (formerly Office Store), these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="b3433-136">Pour plus d’informations, consultez nos [instructions de publication](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) .</span><span class="sxs-lookup"><span data-stu-id="b3433-136">See our [publishing guidelines](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md) for additional information.</span></span>

|<span data-ttu-id="b3433-137">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-137">Name</span></span>| <span data-ttu-id="b3433-138">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-138">Maximum size</span></span> | <span data-ttu-id="b3433-139">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-139">Required</span></span> | <span data-ttu-id="b3433-140">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-140">Description</span></span>|
|---|---|---|---|
|`name`|<span data-ttu-id="b3433-141">32 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-141">32 characters</span></span>|<span data-ttu-id="b3433-142">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-142">✔</span></span>|<span data-ttu-id="b3433-143">Nom complet du développeur.</span><span class="sxs-lookup"><span data-stu-id="b3433-143">The display name for the developer.</span></span>|
|`websiteUrl`|<span data-ttu-id="b3433-144">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-144">2048 characters</span></span>|<span data-ttu-id="b3433-145">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-145">✔</span></span>|<span data-ttu-id="b3433-146">URL https://vers le site Web du développeur.</span><span class="sxs-lookup"><span data-stu-id="b3433-146">The https:// URL to the developer's website.</span></span> <span data-ttu-id="b3433-147">Ce lien doit prendre les utilisateurs à la page d’accueil de votre entreprise ou de votre propre produit.</span><span class="sxs-lookup"><span data-stu-id="b3433-147">This link should take users to your company or product-specific landing page.</span></span>|
|`privacyUrl`|<span data-ttu-id="b3433-148">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-148">2048 characters</span></span>|<span data-ttu-id="b3433-149">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-149">✔</span></span>|<span data-ttu-id="b3433-150">URL https://vers la stratégie de confidentialité du développeur.</span><span class="sxs-lookup"><span data-stu-id="b3433-150">The https:// URL to the developer's privacy policy.</span></span>|
|`termsOfUseUrl`|<span data-ttu-id="b3433-151">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-151">2048 characters</span></span>|<span data-ttu-id="b3433-152">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-152">✔</span></span>|<span data-ttu-id="b3433-153">L’URL https://vers les conditions d’utilisation du développeur.</span><span class="sxs-lookup"><span data-stu-id="b3433-153">The https:// URL to the developer's terms of use.</span></span>|
|`mpnId`|<span data-ttu-id="b3433-154">10 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-154">10 characters</span></span>| |<span data-ttu-id="b3433-155">**Facultatif** ID réseau du partenaire Microsoft qui identifie l’organisation partenaire qui crée l’application.</span><span class="sxs-lookup"><span data-stu-id="b3433-155">**Optional** The Microsoft Partner Network ID that identifies the partner organization building the app.</span></span>|

## <a name="name"></a><span data-ttu-id="b3433-156">name</span><span class="sxs-lookup"><span data-stu-id="b3433-156">name</span></span>

<span data-ttu-id="b3433-157">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="b3433-157">**Required** — object</span></span>

<span data-ttu-id="b3433-158">Nom de l’expérience de votre application, affiché aux utilisateurs dans l’expérience de teams.</span><span class="sxs-lookup"><span data-stu-id="b3433-158">The name of your app experience, displayed to users in the Teams experience.</span></span> <span data-ttu-id="b3433-159">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="b3433-159">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span> <span data-ttu-id="b3433-160">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="b3433-160">The values of `short` and `full` should not be the same.</span></span>

|<span data-ttu-id="b3433-161">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-161">Name</span></span>| <span data-ttu-id="b3433-162">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-162">Maximum size</span></span> | <span data-ttu-id="b3433-163">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-163">Required</span></span> | <span data-ttu-id="b3433-164">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-164">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="b3433-165">30 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-165">30 characters</span></span>|<span data-ttu-id="b3433-166">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-166">✔</span></span>|<span data-ttu-id="b3433-167">Nom complet court de l’application.</span><span class="sxs-lookup"><span data-stu-id="b3433-167">The short display name for the app.</span></span>|
|`full`|<span data-ttu-id="b3433-168">100 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-168">100 characters</span></span>||<span data-ttu-id="b3433-169">Nom complet de l’application, utilisé si le nom complet de l’application dépasse les 30 caractères.</span><span class="sxs-lookup"><span data-stu-id="b3433-169">The full name of the app, used if the full app name exceeds 30 characters.</span></span>|

## <a name="description"></a><span data-ttu-id="b3433-170">description</span><span class="sxs-lookup"><span data-stu-id="b3433-170">description</span></span>

<span data-ttu-id="b3433-171">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="b3433-171">**Required** — object</span></span>

<span data-ttu-id="b3433-172">Décrit votre application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b3433-172">Describes your app to users.</span></span> <span data-ttu-id="b3433-173">Pour les applications soumises à AppSource, ces valeurs doivent correspondre aux informations contenues dans votre entrée AppSource.</span><span class="sxs-lookup"><span data-stu-id="b3433-173">For apps submitted to AppSource, these values must match the information in your AppSource entry.</span></span>

<span data-ttu-id="b3433-174">Assurez-vous que votre description décrit précisément votre expérience et fournit des informations pour aider les clients potentiels à comprendre ce que fait votre expérience.</span><span class="sxs-lookup"><span data-stu-id="b3433-174">Ensure that your description accurately describes your experience and provides information to help potential customers understand what your experience does.</span></span> <span data-ttu-id="b3433-175">Vous devez également noter, dans la description complète, si un compte externe est requis pour l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="b3433-175">You should also note, in the full description, if an external account is required for use.</span></span> <span data-ttu-id="b3433-176">Les valeurs `short` et `full` ne doivent pas être identiques.</span><span class="sxs-lookup"><span data-stu-id="b3433-176">The values of `short` and `full` should not be the same.</span></span>  <span data-ttu-id="b3433-177">Votre description courte ne doit pas être répétée dans la description longue et ne doit pas inclure d’autre nom d’application.</span><span class="sxs-lookup"><span data-stu-id="b3433-177">Your short description must not be repeated within the long description and must not include any other app name.</span></span>

|<span data-ttu-id="b3433-178">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-178">Name</span></span>| <span data-ttu-id="b3433-179">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-179">Maximum size</span></span> | <span data-ttu-id="b3433-180">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-180">Required</span></span> | <span data-ttu-id="b3433-181">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-181">Description</span></span>|
|---|---|---|---|
|`short`|<span data-ttu-id="b3433-182">80 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-182">80 characters</span></span>|<span data-ttu-id="b3433-183">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-183">✔</span></span>|<span data-ttu-id="b3433-184">Brève description de l’expérience de votre application, utilisée lorsque l’espace est limité.</span><span class="sxs-lookup"><span data-stu-id="b3433-184">A short description of your app experience, used when space is limited.</span></span>|
|`full`|<span data-ttu-id="b3433-185">4000 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-185">4000 characters</span></span>|<span data-ttu-id="b3433-186">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-186">✔</span></span>|<span data-ttu-id="b3433-187">Description complète de votre application.</span><span class="sxs-lookup"><span data-stu-id="b3433-187">The full description of your app.</span></span>|

## <a name="packagename"></a><span data-ttu-id="b3433-188">packageName</span><span class="sxs-lookup"><span data-stu-id="b3433-188">packageName</span></span>

<span data-ttu-id="b3433-189">**Facultatif** — String</span><span class="sxs-lookup"><span data-stu-id="b3433-189">**Optional** — string</span></span>

<span data-ttu-id="b3433-190">Un identificateur unique pour cette application dans la notation de domaine inverse ; par exemple, com. example. MyApp.</span><span class="sxs-lookup"><span data-stu-id="b3433-190">A unique identifier for this app in reverse domain notation; for example, com.example.myapp.</span></span> <span data-ttu-id="b3433-191">Longueur maximale : 64 caractères.</span><span class="sxs-lookup"><span data-stu-id="b3433-191">Maximum length: 64 characters.</span></span>

## <a name="localizationinfo"></a><span data-ttu-id="b3433-192">localizationInfo</span><span class="sxs-lookup"><span data-stu-id="b3433-192">localizationInfo</span></span>

<span data-ttu-id="b3433-193">**Facultatif** — Object</span><span class="sxs-lookup"><span data-stu-id="b3433-193">**Optional** — object</span></span>

<span data-ttu-id="b3433-194">Permet de spécifier une langue par défaut, ainsi que des pointeurs vers des fichiers de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b3433-194">Allows the specification of a default language, as well as pointers to additional language files.</span></span> <span data-ttu-id="b3433-195">Consultez la rubrique [Localization](~/concepts/build-and-test/apps-localization.md).</span><span class="sxs-lookup"><span data-stu-id="b3433-195">See [localization](~/concepts/build-and-test/apps-localization.md).</span></span>

|<span data-ttu-id="b3433-196">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-196">Name</span></span>| <span data-ttu-id="b3433-197">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-197">Maximum size</span></span> | <span data-ttu-id="b3433-198">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-198">Required</span></span> | <span data-ttu-id="b3433-199">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-199">Description</span></span>|
|---|---|---|---|
|`defaultLanguageTag`||<span data-ttu-id="b3433-200">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-200">✔</span></span>|<span data-ttu-id="b3433-201">Balise de langue des chaînes dans ce fichier manifeste de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="b3433-201">The language tag of the strings in this top level manifest file.</span></span>|

### <a name="localizationinfoadditionallanguages"></a><span data-ttu-id="b3433-202">localizationInfo.additionalLanguages</span><span class="sxs-lookup"><span data-stu-id="b3433-202">localizationInfo.additionalLanguages</span></span>

<span data-ttu-id="b3433-203">Tableau d’objets spécifiant des traductions de langue supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="b3433-203">An array of objects specifying additional language translations.</span></span>

|<span data-ttu-id="b3433-204">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-204">Name</span></span>| <span data-ttu-id="b3433-205">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-205">Maximum size</span></span> | <span data-ttu-id="b3433-206">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-206">Required</span></span> | <span data-ttu-id="b3433-207">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-207">Description</span></span>|
|---|---|---|---|
|`languageTag`||<span data-ttu-id="b3433-208">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-208">✔</span></span>|<span data-ttu-id="b3433-209">Balise de langue des chaînes dans le fichier fourni.</span><span class="sxs-lookup"><span data-stu-id="b3433-209">The language tag of the strings in the provided file.</span></span>|
|`file`||<span data-ttu-id="b3433-210">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-210">✔</span></span>|<span data-ttu-id="b3433-211">Chemin d’accès relatif à un fichier. JSON contenant les chaînes traduites.</span><span class="sxs-lookup"><span data-stu-id="b3433-211">A relative file path to a the .json file containing the translated strings.</span></span>|

## <a name="icons"></a><span data-ttu-id="b3433-212">icons</span><span class="sxs-lookup"><span data-stu-id="b3433-212">icons</span></span>

<span data-ttu-id="b3433-213">**Obligatoire** — objet</span><span class="sxs-lookup"><span data-stu-id="b3433-213">**Required** — object</span></span>

<span data-ttu-id="b3433-214">Icônes utilisées dans l’application Teams.</span><span class="sxs-lookup"><span data-stu-id="b3433-214">Icons used within the Teams app.</span></span> <span data-ttu-id="b3433-215">Les fichiers d’icône doivent être inclus dans le package de téléchargement.</span><span class="sxs-lookup"><span data-stu-id="b3433-215">The icon files must be included as part of the upload package.</span></span> <span data-ttu-id="b3433-216">Pour plus d’informations, consultez la rubrique [Icons](~/concepts/build-and-test/apps-package.md#icons) .</span><span class="sxs-lookup"><span data-stu-id="b3433-216">See [Icons](~/concepts/build-and-test/apps-package.md#icons) for more information.</span></span>

|<span data-ttu-id="b3433-217">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-217">Name</span></span>| <span data-ttu-id="b3433-218">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-218">Maximum size</span></span> | <span data-ttu-id="b3433-219">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-219">Required</span></span> | <span data-ttu-id="b3433-220">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-220">Description</span></span>|
|---|---|---|---|
|`outline`|<span data-ttu-id="b3433-221">32 x 32 pixels</span><span class="sxs-lookup"><span data-stu-id="b3433-221">32 x 32 pixels</span></span>|<span data-ttu-id="b3433-222">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-222">✔</span></span>|<span data-ttu-id="b3433-223">Chemin d’accès relatif à une icône de contour PNG 32x32 transparent.</span><span class="sxs-lookup"><span data-stu-id="b3433-223">A relative file path to a transparent 32x32 PNG outline icon.</span></span>|
|`color`|<span data-ttu-id="b3433-224">192 x 192 pixels</span><span class="sxs-lookup"><span data-stu-id="b3433-224">192 x 192 pixels</span></span>|<span data-ttu-id="b3433-225">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-225">✔</span></span>|<span data-ttu-id="b3433-226">Chemin d’accès relatif à une icône PNG 192x192 couleur complète.</span><span class="sxs-lookup"><span data-stu-id="b3433-226">A relative file path to a full color 192x192 PNG icon.</span></span>|

## <a name="accentcolor"></a><span data-ttu-id="b3433-227">accentColor</span><span class="sxs-lookup"><span data-stu-id="b3433-227">accentColor</span></span>

<span data-ttu-id="b3433-228">**Facultatif** — code couleur hexadécimal html</span><span class="sxs-lookup"><span data-stu-id="b3433-228">**Optional** — HTML Hex color code</span></span>

<span data-ttu-id="b3433-229">Couleur à utiliser en combinaison avec et en arrière-plan pour vos icônes de plan.</span><span class="sxs-lookup"><span data-stu-id="b3433-229">A color to use in conjunction with and as a background for your outline icons.</span></span>

<span data-ttu-id="b3433-230">La valeur doit être un code de couleur HTML valide commençant par « # », par exemple `#4464ee` .</span><span class="sxs-lookup"><span data-stu-id="b3433-230">The value must be a valid HTML color code starting with '#', for example `#4464ee`.</span></span>

## <a name="configurabletabs"></a><span data-ttu-id="b3433-231">configurableTabs</span><span class="sxs-lookup"><span data-stu-id="b3433-231">configurableTabs</span></span>

<span data-ttu-id="b3433-232">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="b3433-232">**Optional** — array</span></span>

<span data-ttu-id="b3433-233">Utilisé lorsque l’expérience de votre application dispose d’un onglet Channel Team qui nécessite une configuration supplémentaire avant d’être ajoutée.</span><span class="sxs-lookup"><span data-stu-id="b3433-233">Used when your app experience has a team channel tab experience that requires extra configuration before it is added.</span></span> <span data-ttu-id="b3433-234">Les onglets configurables sont pris en charge uniquement dans l’étendue Teams (non personnel) et **un** seul onglet par application est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b3433-234">Configurable tabs are supported only in the teams scope (not personal), and currently only **one** tab per app is supported.</span></span>

|<span data-ttu-id="b3433-235">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-235">Name</span></span>| <span data-ttu-id="b3433-236">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-236">Type</span></span>| <span data-ttu-id="b3433-237">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-237">Maximum size</span></span> | <span data-ttu-id="b3433-238">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-238">Required</span></span> | <span data-ttu-id="b3433-239">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-239">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="b3433-240">string</span><span class="sxs-lookup"><span data-stu-id="b3433-240">string</span></span>|<span data-ttu-id="b3433-241">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-241">2048 characters</span></span>|<span data-ttu-id="b3433-242">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-242">✔</span></span>|<span data-ttu-id="b3433-243">URL https://à utiliser lors de la configuration de l’onglet.</span><span class="sxs-lookup"><span data-stu-id="b3433-243">The https:// URL to use when configuring the tab.</span></span>|
|`scopes`|<span data-ttu-id="b3433-244">Tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b3433-244">array of enums</span></span>|<span data-ttu-id="b3433-245">1 </span><span class="sxs-lookup"><span data-stu-id="b3433-245">1</span></span>|<span data-ttu-id="b3433-246">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-246">✔</span></span>|<span data-ttu-id="b3433-247">Actuellement, les onglets configurables prennent en charge uniquement les `team` `groupchat` étendues et.</span><span class="sxs-lookup"><span data-stu-id="b3433-247">Currently, configurable tabs support only the `team` and `groupchat` scopes.</span></span> |
|`canUpdateConfiguration`|<span data-ttu-id="b3433-248">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b3433-248">boolean</span></span>|||<span data-ttu-id="b3433-249">Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création.</span><span class="sxs-lookup"><span data-stu-id="b3433-249">A value indicating whether an instance of the tab's configuration can be updated by the user after creation.</span></span> <span data-ttu-id="b3433-250">Valeur par défaut : **true**.</span><span class="sxs-lookup"><span data-stu-id="b3433-250">Default: **true**.</span></span>|
|`context` |<span data-ttu-id="b3433-251">Tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b3433-251">array of enums</span></span>|<span data-ttu-id="b3433-252">6 </span><span class="sxs-lookup"><span data-stu-id="b3433-252">6</span></span>||<span data-ttu-id="b3433-253">Ensemble des `contextItem` étendues dans lesquelles un onglet est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b3433-253">The set of `contextItem` scopes where a tab is supported.</span></span> <span data-ttu-id="b3433-254">Valeur par défaut : **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span><span class="sxs-lookup"><span data-stu-id="b3433-254">Default: **[channelTab, privateChatTab, meetingChatTab, meetingDetailsTab]**.</span></span>|
|`sharePointPreviewImage`|<span data-ttu-id="b3433-255">string</span><span class="sxs-lookup"><span data-stu-id="b3433-255">string</span></span>|<span data-ttu-id="b3433-256">2048</span><span class="sxs-lookup"><span data-stu-id="b3433-256">2048</span></span>||<span data-ttu-id="b3433-257">Chemin d’accès relatif à une image d’aperçu de tabulation à utiliser dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b3433-257">A relative file path to a tab preview image for use in SharePoint.</span></span> <span data-ttu-id="b3433-258">Taille 1024 x 768.</span><span class="sxs-lookup"><span data-stu-id="b3433-258">Size 1024x768.</span></span> |
|`supportedSharePointHosts`|<span data-ttu-id="b3433-259">Tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b3433-259">array of enums</span></span>|<span data-ttu-id="b3433-260">1 </span><span class="sxs-lookup"><span data-stu-id="b3433-260">1</span></span>||<span data-ttu-id="b3433-261">Définit la manière dont votre onglet sera disponible dans SharePoint.</span><span class="sxs-lookup"><span data-stu-id="b3433-261">Defines how your tab will be made available in SharePoint.</span></span> <span data-ttu-id="b3433-262">Les options sont `sharePointFullPage` et `sharePointWebPart`</span><span class="sxs-lookup"><span data-stu-id="b3433-262">Options are `sharePointFullPage` and `sharePointWebPart`</span></span> |

## <a name="statictabs"></a><span data-ttu-id="b3433-263">staticTabs</span><span class="sxs-lookup"><span data-stu-id="b3433-263">staticTabs</span></span>

<span data-ttu-id="b3433-264">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="b3433-264">**Optional** — array</span></span>

<span data-ttu-id="b3433-265">Définit un ensemble d’onglets qui peuvent être « épinglés » par défaut, sans que l’utilisateur ne les ajoute manuellement.</span><span class="sxs-lookup"><span data-stu-id="b3433-265">Defines a set of tabs that can be "pinned" by default, without the user adding them manually.</span></span> <span data-ttu-id="b3433-266">Les onglets statiques déclarés dans `personal` l’étendue sont toujours épinglés à l’expérience personnelle de l’application.</span><span class="sxs-lookup"><span data-stu-id="b3433-266">Static tabs declared in `personal` scope are always pinned to the app's personal experience.</span></span> <span data-ttu-id="b3433-267">Les onglets statiques déclarés dans l' `team` étendue ne sont pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="b3433-267">Static tabs declared in the `team` scope are currently not supported.</span></span>

<span data-ttu-id="b3433-268">Cet élément est un tableau (au maximum 16 éléments) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="b3433-268">This item is an array (maximum of 16 elements) with all elements of the type `object`.</span></span> <span data-ttu-id="b3433-269">Ce bloc est requis uniquement pour les solutions qui fournissent une solution d’onglet statique.</span><span class="sxs-lookup"><span data-stu-id="b3433-269">This block is required only for solutions that provide a static tab solution.</span></span>

|<span data-ttu-id="b3433-270">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-270">Name</span></span>| <span data-ttu-id="b3433-271">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-271">Type</span></span>| <span data-ttu-id="b3433-272">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-272">Maximum size</span></span> | <span data-ttu-id="b3433-273">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-273">Required</span></span> | <span data-ttu-id="b3433-274">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-274">Description</span></span>|
|---|---|---|---|---|
|`entityId`|<span data-ttu-id="b3433-275">string</span><span class="sxs-lookup"><span data-stu-id="b3433-275">string</span></span>|<span data-ttu-id="b3433-276">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-276">64 characters</span></span>|<span data-ttu-id="b3433-277">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-277">✔</span></span>|<span data-ttu-id="b3433-278">Identificateur unique de l’entité que l’onglet affiche.</span><span class="sxs-lookup"><span data-stu-id="b3433-278">A unique identifier for the entity that the tab displays.</span></span>|
|`name`|<span data-ttu-id="b3433-279">string</span><span class="sxs-lookup"><span data-stu-id="b3433-279">string</span></span>|<span data-ttu-id="b3433-280">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-280">128 characters</span></span>|<span data-ttu-id="b3433-281">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-281">✔</span></span>|<span data-ttu-id="b3433-282">Nom d’affichage de l’onglet dans l’interface de canal.</span><span class="sxs-lookup"><span data-stu-id="b3433-282">The display name of the tab in the channel interface.</span></span>|
|`contentUrl`|<span data-ttu-id="b3433-283">string</span><span class="sxs-lookup"><span data-stu-id="b3433-283">string</span></span>||<span data-ttu-id="b3433-284">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-284">✔</span></span>|<span data-ttu-id="b3433-285">URL https://qui pointe vers l’interface utilisateur de l’entité à afficher dans la zone de dessin de teams.</span><span class="sxs-lookup"><span data-stu-id="b3433-285">The https:// URL that points to the entity UI to be displayed in the Teams canvas.</span></span>|
|`websiteUrl`|<span data-ttu-id="b3433-286">string</span><span class="sxs-lookup"><span data-stu-id="b3433-286">string</span></span>|||<span data-ttu-id="b3433-287">URL https://pointant vers un utilisateur si celui-ci choisit de l’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="b3433-287">The https:// URL to point to if a user opts to view in a browser.</span></span>|
|`searchUrl`|<span data-ttu-id="b3433-288">string</span><span class="sxs-lookup"><span data-stu-id="b3433-288">string</span></span>|||<span data-ttu-id="b3433-289">URL https://vers laquelle pointe les requêtes de recherche d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b3433-289">The https:// URL to point to for a user's search queries.</span></span>|
|`scopes`|<span data-ttu-id="b3433-290">Tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b3433-290">array of enums</span></span>|<span data-ttu-id="b3433-291">1 </span><span class="sxs-lookup"><span data-stu-id="b3433-291">1</span></span>|<span data-ttu-id="b3433-292">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-292">✔</span></span>|<span data-ttu-id="b3433-293">Actuellement, les onglets statiques prennent en charge uniquement l' `personal` étendue, ce qui signifie qu’elle peut être mise en service uniquement dans le cadre de l’expérience personnelle.</span><span class="sxs-lookup"><span data-stu-id="b3433-293">Currently, static tabs support only the `personal` scope, which means it can be provisioned only as part of the personal experience.</span></span>|
|`context` | <span data-ttu-id="b3433-294">Tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b3433-294">array of enums</span></span>| <span data-ttu-id="b3433-295">2 </span><span class="sxs-lookup"><span data-stu-id="b3433-295">2</span></span>|| <span data-ttu-id="b3433-296">Ensemble des `contextItem` étendues dans lesquelles un onglet est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b3433-296">The set of `contextItem` scopes where a tab is supported.</span></span>|

> [!NOTE]
> <span data-ttu-id="b3433-297">Si vos onglets nécessitent des informations contextuelles pour afficher le contenu pertinent ou pour initier un flux d’authentification, *reportez-vous* à [la rubrique obtenir le contexte de votre onglet Microsoft teams](../../tabs/how-to/access-teams-context.md).</span><span class="sxs-lookup"><span data-stu-id="b3433-297">If your tabs require context-dependent information to display relevant content or for initiating an authentication flow, *see* [Get context for your Microsoft Teams tab](../../tabs/how-to/access-teams-context.md).</span></span>

## <a name="bots"></a><span data-ttu-id="b3433-298">bots</span><span class="sxs-lookup"><span data-stu-id="b3433-298">bots</span></span>

<span data-ttu-id="b3433-299">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="b3433-299">**Optional** — array</span></span>

<span data-ttu-id="b3433-300">Définit une solution de robot, ainsi que des informations facultatives telles que les propriétés de commande par défaut.</span><span class="sxs-lookup"><span data-stu-id="b3433-300">Defines a bot solution, along with optional information such as default command properties.</span></span>

<span data-ttu-id="b3433-301">L’élément est un tableau (un seul élément un seul d' &mdash; entre eux est actuellement autorisé par application) avec tous les éléments du type `object` .</span><span class="sxs-lookup"><span data-stu-id="b3433-301">The item is an array (maximum of only 1 element&mdash;currently only one bot is allowed per app) with all elements of the type `object`.</span></span> <span data-ttu-id="b3433-302">Ce bloc est requis uniquement pour les solutions qui fournissent une expérience de robot.</span><span class="sxs-lookup"><span data-stu-id="b3433-302">This block is required only for solutions that provide a bot experience.</span></span>

|<span data-ttu-id="b3433-303">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-303">Name</span></span>| <span data-ttu-id="b3433-304">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-304">Type</span></span>| <span data-ttu-id="b3433-305">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-305">Maximum size</span></span> | <span data-ttu-id="b3433-306">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-306">Required</span></span> | <span data-ttu-id="b3433-307">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-307">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="b3433-308">string</span><span class="sxs-lookup"><span data-stu-id="b3433-308">string</span></span>|<span data-ttu-id="b3433-309">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-309">64 characters</span></span>|<span data-ttu-id="b3433-310">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-310">✔</span></span>|<span data-ttu-id="b3433-311">ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="b3433-311">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="b3433-312">Il peut s’agir de la même chose que l' [ID d’application](#id)global.</span><span class="sxs-lookup"><span data-stu-id="b3433-312">This may well be the same as the overall [app ID](#id).</span></span>|
|`scopes`|<span data-ttu-id="b3433-313">Tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b3433-313">array of enums</span></span>|<span data-ttu-id="b3433-314">3 </span><span class="sxs-lookup"><span data-stu-id="b3433-314">3</span></span>|<span data-ttu-id="b3433-315">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-315">✔</span></span>|<span data-ttu-id="b3433-316">Indique si le bot offre une expérience dans le contexte d’un canal dans une `team`, dans une conversation de groupe (`groupchat`) ou dans une expérience limitée à un utilisateur individuel (`personal`).</span><span class="sxs-lookup"><span data-stu-id="b3433-316">Specifies whether the bot offers an experience in the context of a channel in a `team`, in a group chat (`groupchat`), or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="b3433-317">Ces options ne sont pas exclusives.</span><span class="sxs-lookup"><span data-stu-id="b3433-317">These options are non-exclusive.</span></span>|
|`needsChannelSelector`|<span data-ttu-id="b3433-318">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b3433-318">boolean</span></span>|||<span data-ttu-id="b3433-319">Indique si le bot utilise ou non un indicateur d’utilisateur pour ajouter le bot à un canal spécifique.</span><span class="sxs-lookup"><span data-stu-id="b3433-319">Describes whether or not the bot utilizes a user hint to add the bot to a specific channel.</span></span> <span data-ttu-id="b3433-320">Default **`false`**</span><span class="sxs-lookup"><span data-stu-id="b3433-320">Default: **`false`**</span></span>|
|`isNotificationOnly`|<span data-ttu-id="b3433-321">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b3433-321">boolean</span></span>|||<span data-ttu-id="b3433-322">Indique si un bot est unidirectionnel, de notification uniquement, par opposition à un bot conversationnel.</span><span class="sxs-lookup"><span data-stu-id="b3433-322">Indicates whether a bot is a one-way, notification-only bot, as opposed to a conversational bot.</span></span> <span data-ttu-id="b3433-323">Default `**false**`</span><span class="sxs-lookup"><span data-stu-id="b3433-323">Default: `**false**`</span></span>|
|`supportsFiles`|<span data-ttu-id="b3433-324">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b3433-324">boolean</span></span>|||<span data-ttu-id="b3433-325">Indique si le bot prend en charge la possibilité de télécharger des fichiers dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="b3433-325">Indicates whether the bot supports the ability to upload/download files in personal chat.</span></span> <span data-ttu-id="b3433-326">Default **`false`**</span><span class="sxs-lookup"><span data-stu-id="b3433-326">Default: **`false`**</span></span>|
|`supportsCalling`|<span data-ttu-id="b3433-327">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b3433-327">boolean</span></span>|||<span data-ttu-id="b3433-328">Valeur indiquant où un bot prend en charge les appels audio.</span><span class="sxs-lookup"><span data-stu-id="b3433-328">A value indicating where a bot supports audio calling.</span></span> <span data-ttu-id="b3433-329">**Important**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="b3433-329">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="b3433-330">Les propriétés expérimentales ne sont peut-être pas complètes et peuvent être sujettes à des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="b3433-330">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="b3433-331">Il est fourni à des fins de test et d’exploration uniquement et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="b3433-331">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="b3433-332">Default **`false`**</span><span class="sxs-lookup"><span data-stu-id="b3433-332">Default: **`false`**</span></span>|
|`supportsVideo`|<span data-ttu-id="b3433-333">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b3433-333">boolean</span></span>|||<span data-ttu-id="b3433-334">Valeur indiquant où un bot prend en charge les appels vidéo.</span><span class="sxs-lookup"><span data-stu-id="b3433-334">A value indicating where a bot supports video calling.</span></span> <span data-ttu-id="b3433-335">**Important**: cette propriété est actuellement expérimentale.</span><span class="sxs-lookup"><span data-stu-id="b3433-335">**IMPORTANT**: This property is currently experimental.</span></span> <span data-ttu-id="b3433-336">Les propriétés expérimentales ne sont peut-être pas complètes et peuvent être sujettes à des modifications avant de devenir entièrement disponibles.</span><span class="sxs-lookup"><span data-stu-id="b3433-336">Experimental properties may not be complete, and may undergo changes before becoming fully available.</span></span>  <span data-ttu-id="b3433-337">Il est fourni à des fins de test et d’exploration uniquement et ne doit pas être utilisé dans les applications de production.</span><span class="sxs-lookup"><span data-stu-id="b3433-337">It is provided for testing and exploration purposes only and should not be used in production applications.</span></span> <span data-ttu-id="b3433-338">Default **`false`**</span><span class="sxs-lookup"><span data-stu-id="b3433-338">Default: **`false`**</span></span>|

### <a name="botscommandlists"></a><span data-ttu-id="b3433-339">bots. commandLists</span><span class="sxs-lookup"><span data-stu-id="b3433-339">bots.commandLists</span></span>

<span data-ttu-id="b3433-340">Liste facultative de commandes que votre bot peut recommander aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b3433-340">An optional list of commands that your bot can recommend to users.</span></span> <span data-ttu-id="b3433-341">L’objet est un tableau (nombre maximal de 2 éléments) avec tous les éléments de type `object` ; vous devez définir une liste de commandes distincte pour chaque étendue prise en charge par votre bot.</span><span class="sxs-lookup"><span data-stu-id="b3433-341">The object is an array (maximum of 2 elements) with all elements of type `object`; you must define a separate command list for each scope that your bot supports.</span></span> <span data-ttu-id="b3433-342">Pour plus d’informations, voir [menus de bot](~/bots/how-to/create-a-bot-commands-menu.md) .</span><span class="sxs-lookup"><span data-stu-id="b3433-342">See [Bot menus](~/bots/how-to/create-a-bot-commands-menu.md) for more information.</span></span>

|<span data-ttu-id="b3433-343">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-343">Name</span></span>| <span data-ttu-id="b3433-344">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-344">Type</span></span>| <span data-ttu-id="b3433-345">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-345">Maximum size</span></span> | <span data-ttu-id="b3433-346">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-346">Required</span></span> | <span data-ttu-id="b3433-347">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-347">Description</span></span>|
|---|---|---|---|---|
|`items.scopes`|<span data-ttu-id="b3433-348">Tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b3433-348">array of enums</span></span>|<span data-ttu-id="b3433-349">3 </span><span class="sxs-lookup"><span data-stu-id="b3433-349">3</span></span>|<span data-ttu-id="b3433-350">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-350">✔</span></span>|<span data-ttu-id="b3433-351">Spécifie l’étendue pour laquelle la liste de commandes est valide.</span><span class="sxs-lookup"><span data-stu-id="b3433-351">Specifies the scope for which the command list is valid.</span></span> <span data-ttu-id="b3433-352">Les options sont `team`, `personal` et `groupchat`.</span><span class="sxs-lookup"><span data-stu-id="b3433-352">Options are `team`, `personal`, and `groupchat`.</span></span>|
|`items.commands`|<span data-ttu-id="b3433-353">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b3433-353">array of objects</span></span>|<span data-ttu-id="b3433-354">10 </span><span class="sxs-lookup"><span data-stu-id="b3433-354">10</span></span>|<span data-ttu-id="b3433-355">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-355">✔</span></span>|<span data-ttu-id="b3433-356">Ensemble de commandes prises en charge par le bot :</span><span class="sxs-lookup"><span data-stu-id="b3433-356">An array of commands the bot supports:</span></span><br><span data-ttu-id="b3433-357">`title`: nom de la commande bot (chaîne, 32)</span><span class="sxs-lookup"><span data-stu-id="b3433-357">`title`: the bot command name (string, 32)</span></span><br><span data-ttu-id="b3433-358">`description` : description simple ou exemple de la syntaxe de commande et de son argument (chaîne, 128)</span><span class="sxs-lookup"><span data-stu-id="b3433-358">`description`: a simple description or example of the command syntax and its argument (string, 128)</span></span>|

### <a name="botscommandlistscommands"></a><span data-ttu-id="b3433-359">bots. commandLists. Commands</span><span class="sxs-lookup"><span data-stu-id="b3433-359">bots.commandLists.commands</span></span>

|<span data-ttu-id="b3433-360">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-360">Name</span></span>| <span data-ttu-id="b3433-361">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-361">Type</span></span>| <span data-ttu-id="b3433-362">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-362">Maximum size</span></span> | <span data-ttu-id="b3433-363">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-363">Required</span></span> | <span data-ttu-id="b3433-364">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-364">Description</span></span>|
|---|---|---|---|---|
|<span data-ttu-id="b3433-365">title</span><span class="sxs-lookup"><span data-stu-id="b3433-365">title</span></span>|<span data-ttu-id="b3433-366">string</span><span class="sxs-lookup"><span data-stu-id="b3433-366">string</span></span>|<span data-ttu-id="b3433-367">12 </span><span class="sxs-lookup"><span data-stu-id="b3433-367">12</span></span>|<span data-ttu-id="b3433-368">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-368">✔</span></span>|<span data-ttu-id="b3433-369">Nom de la commande bot</span><span class="sxs-lookup"><span data-stu-id="b3433-369">The bot command name</span></span>|
|<span data-ttu-id="b3433-370">description</span><span class="sxs-lookup"><span data-stu-id="b3433-370">description</span></span>|<span data-ttu-id="b3433-371">string</span><span class="sxs-lookup"><span data-stu-id="b3433-371">string</span></span>|<span data-ttu-id="b3433-372">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-372">128 characters</span></span>|<span data-ttu-id="b3433-373">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-373">✔</span></span>|<span data-ttu-id="b3433-374">Une description de texte simple ou un exemple de syntaxe de commande et ses arguments.</span><span class="sxs-lookup"><span data-stu-id="b3433-374">A simple text description or an example of the command syntax and its arguments.</span></span>|

## <a name="connectors"></a><span data-ttu-id="b3433-375">ceux</span><span class="sxs-lookup"><span data-stu-id="b3433-375">connectors</span></span>

<span data-ttu-id="b3433-376">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="b3433-376">**Optional** — array</span></span>

<span data-ttu-id="b3433-377">Le `connectors` bloc définit un connecteur Office 365 pour l’application.</span><span class="sxs-lookup"><span data-stu-id="b3433-377">The `connectors` block defines an Office 365 Connector for the app.</span></span>

<span data-ttu-id="b3433-378">L’objet est un tableau (un maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="b3433-378">The object is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="b3433-379">Ce bloc est requis uniquement pour les solutions qui fournissent un connecteur.</span><span class="sxs-lookup"><span data-stu-id="b3433-379">This block is required only for solutions that provide a Connector.</span></span>

|<span data-ttu-id="b3433-380">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-380">Name</span></span>| <span data-ttu-id="b3433-381">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-381">Type</span></span>| <span data-ttu-id="b3433-382">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-382">Maximum size</span></span> | <span data-ttu-id="b3433-383">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-383">Required</span></span> | <span data-ttu-id="b3433-384">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-384">Description</span></span>|
|---|---|---|---|---|
|`configurationUrl`|<span data-ttu-id="b3433-385">string</span><span class="sxs-lookup"><span data-stu-id="b3433-385">string</span></span>|<span data-ttu-id="b3433-386">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-386">2048 characters</span></span>|<span data-ttu-id="b3433-387">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-387">✔</span></span>|<span data-ttu-id="b3433-388">URL https://à utiliser lors de la configuration du connecteur.</span><span class="sxs-lookup"><span data-stu-id="b3433-388">The https:// URL to use when configuring the connector.</span></span>|
|`scopes`|<span data-ttu-id="b3433-389">Tableau d’énumérations</span><span class="sxs-lookup"><span data-stu-id="b3433-389">array of enums</span></span>|<span data-ttu-id="b3433-390">1 </span><span class="sxs-lookup"><span data-stu-id="b3433-390">1</span></span>|<span data-ttu-id="b3433-391">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-391">✔</span></span>|<span data-ttu-id="b3433-392">Indique si le connecteur offre une expérience dans le contexte d’un canal dans un `team` , ou une expérience étendue à un utilisateur individuel ( `personal` ).</span><span class="sxs-lookup"><span data-stu-id="b3433-392">Specifies whether the Connector offers an experience in the context of a channel in a `team`, or an experience scoped to an individual user alone (`personal`).</span></span> <span data-ttu-id="b3433-393">Actuellement, seule l' `team` étendue est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="b3433-393">Currently, only the `team` scope is supported.</span></span>|
|`connectorId`|<span data-ttu-id="b3433-394">string</span><span class="sxs-lookup"><span data-stu-id="b3433-394">string</span></span>|<span data-ttu-id="b3433-395">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-395">64 characters</span></span>|<span data-ttu-id="b3433-396">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-396">✔</span></span>|<span data-ttu-id="b3433-397">Identificateur unique du connecteur correspondant à son ID dans le [tableau de bord du développeur de connecteurs](https://aka.ms/connectorsdashboard).</span><span class="sxs-lookup"><span data-stu-id="b3433-397">A unique identifier for the Connector that matches its ID in the [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard).</span></span>|

## <a name="composeextensions"></a><span data-ttu-id="b3433-398">composeExtensions</span><span class="sxs-lookup"><span data-stu-id="b3433-398">composeExtensions</span></span>

<span data-ttu-id="b3433-399">**Facultatif** — Array</span><span class="sxs-lookup"><span data-stu-id="b3433-399">**Optional** — array</span></span>

<span data-ttu-id="b3433-400">Définit une extension de messagerie pour l’application.</span><span class="sxs-lookup"><span data-stu-id="b3433-400">Defines a messaging extension for the app.</span></span>

> [!NOTE]
> <span data-ttu-id="b3433-401">Le nom de la fonctionnalité a été modifié de « extension de composition » en « extension de messagerie » en novembre 2017, mais le nom de manifeste reste le même afin que les extensions existantes continuent de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="b3433-401">The name of the feature was changed from "compose extension" to "messaging extension" in November, 2017, but the manifest name remains the same so that existing extensions continue to function.</span></span>

<span data-ttu-id="b3433-402">L’élément est un tableau (un maximum de 1 élément) avec tous les éléments de type `object` .</span><span class="sxs-lookup"><span data-stu-id="b3433-402">The item is an array (maximum of 1 element) with all elements of type `object`.</span></span> <span data-ttu-id="b3433-403">Ce bloc est requis uniquement pour les solutions qui fournissent une extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="b3433-403">This block is required only for solutions that provide a messaging extension.</span></span>

|<span data-ttu-id="b3433-404">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-404">Name</span></span>| <span data-ttu-id="b3433-405">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-405">Type</span></span> | <span data-ttu-id="b3433-406">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-406">Maximum Size</span></span> | <span data-ttu-id="b3433-407">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="b3433-407">Required</span></span> | <span data-ttu-id="b3433-408">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-408">Description</span></span>|
|---|---|---|---|---|
|`botId`|<span data-ttu-id="b3433-409">string</span><span class="sxs-lookup"><span data-stu-id="b3433-409">string</span></span>|<span data-ttu-id="b3433-410">64</span><span class="sxs-lookup"><span data-stu-id="b3433-410">64</span></span>|<span data-ttu-id="b3433-411">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-411">✔</span></span>|<span data-ttu-id="b3433-412">ID d’application Microsoft unique pour le bot qui sauvegarde l’extension de messagerie, tel qu’inscrit auprès de l’infrastructure bot.</span><span class="sxs-lookup"><span data-stu-id="b3433-412">The unique Microsoft app ID for the bot that backs the messaging extension, as registered with the Bot Framework.</span></span> <span data-ttu-id="b3433-413">Il peut s’agir de la même chose que l’ID d’application global.</span><span class="sxs-lookup"><span data-stu-id="b3433-413">This may well be the same as the overall App ID.</span></span>|
|`commands`|<span data-ttu-id="b3433-414">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b3433-414">array of objects</span></span>|<span data-ttu-id="b3433-415">10 </span><span class="sxs-lookup"><span data-stu-id="b3433-415">10</span></span>|<span data-ttu-id="b3433-416">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-416">✔</span></span>|<span data-ttu-id="b3433-417">Tableau de commandes prises en charge par l’extension de messagerie</span><span class="sxs-lookup"><span data-stu-id="b3433-417">array of commands the messaging extension supports</span></span>|
|`canUpdateConfiguration`|<span data-ttu-id="b3433-418">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b3433-418">boolean</span></span>|||<span data-ttu-id="b3433-419">Valeur indiquant si la configuration d’une extension de messagerie peut être mise à jour par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b3433-419">A value indicating whether the configuration of a messaging extension can be updated by the user.</span></span> <span data-ttu-id="b3433-420">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="b3433-420">Default: **false**.</span></span>|
|`messageHandlers`|<span data-ttu-id="b3433-421">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b3433-421">array of Objects</span></span>|<span data-ttu-id="b3433-422">5 </span><span class="sxs-lookup"><span data-stu-id="b3433-422">5</span></span>||<span data-ttu-id="b3433-423">Liste de gestionnaires permettant d’appeler des applications lorsque certaines conditions sont remplies.</span><span class="sxs-lookup"><span data-stu-id="b3433-423">A list of handlers that allow apps to be invoked when certain conditions are met.</span></span> <span data-ttu-id="b3433-424">Les domaines doivent également être affichés dans `validDomains`</span><span class="sxs-lookup"><span data-stu-id="b3433-424">Domains must also be listed in `validDomains`</span></span>|
|`messageHandlers.type`|<span data-ttu-id="b3433-425">string</span><span class="sxs-lookup"><span data-stu-id="b3433-425">string</span></span>|||<span data-ttu-id="b3433-426">Type de gestionnaire de messages.</span><span class="sxs-lookup"><span data-stu-id="b3433-426">The type of message handler.</span></span> <span data-ttu-id="b3433-427">Doit être `"link"`.</span><span class="sxs-lookup"><span data-stu-id="b3433-427">Must be `"link"`.</span></span>|
|`messageHandlers.value.domains`|<span data-ttu-id="b3433-428">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="b3433-428">array of Strings</span></span>|||<span data-ttu-id="b3433-429">Tableau de domaines pour lesquels le gestionnaire de messages de liaison peut s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="b3433-429">array of domains that the link message handler can register for.</span></span>|

### <a name="composeextensionscommands"></a><span data-ttu-id="b3433-430">composeExtensions. Commands</span><span class="sxs-lookup"><span data-stu-id="b3433-430">composeExtensions.commands</span></span>

<span data-ttu-id="b3433-431">Votre extension de messagerie doit déclarer une ou plusieurs commandes.</span><span class="sxs-lookup"><span data-stu-id="b3433-431">Your messaging extension should declare one or more commands.</span></span> <span data-ttu-id="b3433-432">Chaque commande apparaît dans Microsoft teams comme une interaction potentielle à partir du point d’entrée basé sur l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b3433-432">Each command appears in Microsoft Teams as a potential interaction from the UI-based entry point.</span></span> <span data-ttu-id="b3433-433">Il y a un maximum de 10 commandes.</span><span class="sxs-lookup"><span data-stu-id="b3433-433">There is a maximum of 10 commands.</span></span>

<span data-ttu-id="b3433-434">Chaque élément de commande est un objet de la structure suivante :</span><span class="sxs-lookup"><span data-stu-id="b3433-434">Each command item is an object with the following structure:</span></span>

|<span data-ttu-id="b3433-435">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-435">Name</span></span>| <span data-ttu-id="b3433-436">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-436">Type</span></span>| <span data-ttu-id="b3433-437">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-437">Maximum size</span></span> | <span data-ttu-id="b3433-438">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-438">Required</span></span> | <span data-ttu-id="b3433-439">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-439">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="b3433-440">string</span><span class="sxs-lookup"><span data-stu-id="b3433-440">string</span></span>|<span data-ttu-id="b3433-441">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-441">64 characters</span></span>|<span data-ttu-id="b3433-442">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-442">✔</span></span>|<span data-ttu-id="b3433-443">ID de la commande.</span><span class="sxs-lookup"><span data-stu-id="b3433-443">The ID for the command.</span></span>|
|`title`|<span data-ttu-id="b3433-444">string</span><span class="sxs-lookup"><span data-stu-id="b3433-444">string</span></span>|<span data-ttu-id="b3433-445">32 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-445">32 characters</span></span>|<span data-ttu-id="b3433-446">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-446">✔</span></span>|<span data-ttu-id="b3433-447">Nom de la commande conviviale.</span><span class="sxs-lookup"><span data-stu-id="b3433-447">The user-friendly command name.</span></span>|
|`type`|<span data-ttu-id="b3433-448">string</span><span class="sxs-lookup"><span data-stu-id="b3433-448">string</span></span>|<span data-ttu-id="b3433-449">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-449">64 characters</span></span>||<span data-ttu-id="b3433-450">Type de la commande.</span><span class="sxs-lookup"><span data-stu-id="b3433-450">Type of the command.</span></span> <span data-ttu-id="b3433-451">L’une `query` ou l’autre `action` .</span><span class="sxs-lookup"><span data-stu-id="b3433-451">One of `query` or `action`.</span></span> <span data-ttu-id="b3433-452">Valeur par défaut : **requête**.</span><span class="sxs-lookup"><span data-stu-id="b3433-452">Default: **query**.</span></span>|
|`description`|<span data-ttu-id="b3433-453">string</span><span class="sxs-lookup"><span data-stu-id="b3433-453">string</span></span>|<span data-ttu-id="b3433-454">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-454">128 characters</span></span>||<span data-ttu-id="b3433-455">Description qui apparaît pour les utilisateurs afin d’indiquer la finalité de cette commande.</span><span class="sxs-lookup"><span data-stu-id="b3433-455">The description that appears to users to indicate the purpose of this command.</span></span>|
|`initialRun`|<span data-ttu-id="b3433-456">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b3433-456">boolean</span></span>|||<span data-ttu-id="b3433-457">Valeur booléenne indiquant si la commande doit être exécutée initialement sans paramètre.</span><span class="sxs-lookup"><span data-stu-id="b3433-457">A boolean value that indicates whether the command should be run initially with no parameters.</span></span> <span data-ttu-id="b3433-458">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="b3433-458">Default: **false**.</span></span>|
|`context`|<span data-ttu-id="b3433-459">Tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="b3433-459">array of Strings</span></span>|<span data-ttu-id="b3433-460">3 </span><span class="sxs-lookup"><span data-stu-id="b3433-460">3</span></span>||<span data-ttu-id="b3433-461">Définit l’emplacement à partir duquel l’extension de message peut être appelée.</span><span class="sxs-lookup"><span data-stu-id="b3433-461">Defines where the message extension can be invoked from.</span></span> <span data-ttu-id="b3433-462">Toute combinaison de `compose` , `commandBox` , `message` .</span><span class="sxs-lookup"><span data-stu-id="b3433-462">Any combination of`compose`,`commandBox`,`message` .</span></span> <span data-ttu-id="b3433-463">La valeur par défaut est `["compose","commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="b3433-463">Default is `["compose","commandBox"]`.</span></span>|
|`fetchTask`|<span data-ttu-id="b3433-464">valeur booléenne</span><span class="sxs-lookup"><span data-stu-id="b3433-464">boolean</span></span>|||<span data-ttu-id="b3433-465">Valeur booléenne qui indique s’il doit extraire le module de tâches de façon dynamique.</span><span class="sxs-lookup"><span data-stu-id="b3433-465">A boolean value that indicates if it should fetch the task module dynamically.</span></span> <span data-ttu-id="b3433-466">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="b3433-466">Default: **false**.</span></span>|
|`taskInfo`|<span data-ttu-id="b3433-467">objet</span><span class="sxs-lookup"><span data-stu-id="b3433-467">object</span></span>|||<span data-ttu-id="b3433-468">Spécifier le module de tâche à précharger lors de l’utilisation d’une commande d’extension de messagerie.</span><span class="sxs-lookup"><span data-stu-id="b3433-468">Specify the task module to pre-load when using a messaging extension command.</span></span>|
|`taskInfo.title`|<span data-ttu-id="b3433-469">string</span><span class="sxs-lookup"><span data-stu-id="b3433-469">string</span></span>|<span data-ttu-id="b3433-470">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-470">64 characters</span></span>||<span data-ttu-id="b3433-471">Titre de la boîte de dialogue initiale.</span><span class="sxs-lookup"><span data-stu-id="b3433-471">Initial dialog title.</span></span>|
|`taskInfo.width`|<span data-ttu-id="b3433-472">string</span><span class="sxs-lookup"><span data-stu-id="b3433-472">string</span></span>|||<span data-ttu-id="b3433-473">Largeur de la boîte de dialogue-soit un nombre en pixels, soit une mise en page par défaut telle que « grande », « moyen » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="b3433-473">Dialog width - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.height`|<span data-ttu-id="b3433-474">string</span><span class="sxs-lookup"><span data-stu-id="b3433-474">string</span></span>|||<span data-ttu-id="b3433-475">Hauteur de la boîte de dialogue : nombre en pixels ou mise en page par défaut, par exemple, « grande », « moyenne » ou « petite ».</span><span class="sxs-lookup"><span data-stu-id="b3433-475">Dialog height - either a number in pixels or default layout such as 'large', 'medium', or 'small'.</span></span>|
|`taskInfo.url`|<span data-ttu-id="b3433-476">string</span><span class="sxs-lookup"><span data-stu-id="b3433-476">string</span></span>|||<span data-ttu-id="b3433-477">URL d’affichage WebView initiale.</span><span class="sxs-lookup"><span data-stu-id="b3433-477">Initial webview URL.</span></span>|
|`parameters`|<span data-ttu-id="b3433-478">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b3433-478">array of object</span></span>|<span data-ttu-id="b3433-479">5 éléments</span><span class="sxs-lookup"><span data-stu-id="b3433-479">5 items</span></span>|<span data-ttu-id="b3433-480">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-480">✔</span></span>|<span data-ttu-id="b3433-481">La liste des paramètres que la commande prend.</span><span class="sxs-lookup"><span data-stu-id="b3433-481">The list of parameters the command takes.</span></span> <span data-ttu-id="b3433-482">Minimum : 1 ; maximum : 5.</span><span class="sxs-lookup"><span data-stu-id="b3433-482">Minimum: 1; maximum: 5.</span></span>|
|`parameters.name`|<span data-ttu-id="b3433-483">string</span><span class="sxs-lookup"><span data-stu-id="b3433-483">string</span></span>|<span data-ttu-id="b3433-484">64 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-484">64 characters</span></span>|<span data-ttu-id="b3433-485">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-485">✔</span></span>|<span data-ttu-id="b3433-486">Nom du paramètre tel qu’il apparaît dans le client.</span><span class="sxs-lookup"><span data-stu-id="b3433-486">The name of the parameter as it appears in the client.</span></span> <span data-ttu-id="b3433-487">Elle est incluse dans la demande de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b3433-487">This is included in the user request.</span></span>|
|`parameters.title`|<span data-ttu-id="b3433-488">string</span><span class="sxs-lookup"><span data-stu-id="b3433-488">string</span></span>|<span data-ttu-id="b3433-489">32 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-489">32 characters</span></span>|<span data-ttu-id="b3433-490">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-490">✔</span></span>|<span data-ttu-id="b3433-491">Titre convivial du paramètre.</span><span class="sxs-lookup"><span data-stu-id="b3433-491">User-friendly title for the parameter.</span></span>|
|`parameters.description`|<span data-ttu-id="b3433-492">string</span><span class="sxs-lookup"><span data-stu-id="b3433-492">string</span></span>|<span data-ttu-id="b3433-493">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-493">128 characters</span></span>||<span data-ttu-id="b3433-494">Chaîne conviviale qui décrit l’objectif de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="b3433-494">User-friendly string that describes this parameter’s purpose.</span></span>|
|`parameters.value`|<span data-ttu-id="b3433-495">string</span><span class="sxs-lookup"><span data-stu-id="b3433-495">string</span></span>|<span data-ttu-id="b3433-496">512 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-496">512 characters</span></span>||<span data-ttu-id="b3433-497">Valeur initiale du paramètre.</span><span class="sxs-lookup"><span data-stu-id="b3433-497">Initial value for the parameter.</span></span>|
|`parameters.inputType`|<span data-ttu-id="b3433-498">string</span><span class="sxs-lookup"><span data-stu-id="b3433-498">string</span></span>|<span data-ttu-id="b3433-499">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-499">128 characters</span></span>||<span data-ttu-id="b3433-500">Définit le type de contrôle affiché sur un module de tâche pour `fetchTask: true` .</span><span class="sxs-lookup"><span data-stu-id="b3433-500">Defines the type of control displayed on a task module for`fetchTask: true` .</span></span> <span data-ttu-id="b3433-501">L’une des `text, textarea, number, date, time, toggle, choiceset` .</span><span class="sxs-lookup"><span data-stu-id="b3433-501">One of `text, textarea, number, date, time, toggle, choiceset` .</span></span>|
|`parameters.choices`|<span data-ttu-id="b3433-502">tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b3433-502">array of objects</span></span>|<span data-ttu-id="b3433-503">10 éléments</span><span class="sxs-lookup"><span data-stu-id="b3433-503">10 items</span></span>||<span data-ttu-id="b3433-504">Options de choix pour le `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="b3433-504">The choice options for the`choiceset`.</span></span> <span data-ttu-id="b3433-505">Utilisez uniquement lorsque `parameter.inputType` est `choiceset` .</span><span class="sxs-lookup"><span data-stu-id="b3433-505">Use only when`parameter.inputType` is `choiceset`.</span></span>|
|`parameters.choices.title`|<span data-ttu-id="b3433-506">string</span><span class="sxs-lookup"><span data-stu-id="b3433-506">string</span></span>|<span data-ttu-id="b3433-507">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-507">128 characters</span></span>|<span data-ttu-id="b3433-508">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-508">✔</span></span>|<span data-ttu-id="b3433-509">Titre du choix.</span><span class="sxs-lookup"><span data-stu-id="b3433-509">Title of the choice.</span></span>|
|`parameters.choices.value`|<span data-ttu-id="b3433-510">string</span><span class="sxs-lookup"><span data-stu-id="b3433-510">string</span></span>|<span data-ttu-id="b3433-511">512 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-511">512 characters</span></span>|<span data-ttu-id="b3433-512">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-512">✔</span></span>|<span data-ttu-id="b3433-513">Valeur du choix.</span><span class="sxs-lookup"><span data-stu-id="b3433-513">Value of the choice.</span></span>|

## <a name="permissions"></a><span data-ttu-id="b3433-514">autorisations</span><span class="sxs-lookup"><span data-stu-id="b3433-514">permissions</span></span>

<span data-ttu-id="b3433-515">**Facultatif** — tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="b3433-515">**Optional** — array of strings</span></span>

<span data-ttu-id="b3433-516">Un tableau `string` qui spécifie les autorisations demandées par l’application, ce qui permet aux utilisateurs finaux de savoir comment effectuer l’extension.</span><span class="sxs-lookup"><span data-stu-id="b3433-516">An array of `string` which specifies which permissions the app requests, which lets end users know how the extension will perform.</span></span> <span data-ttu-id="b3433-517">Les options suivantes ne sont pas exclusives :</span><span class="sxs-lookup"><span data-stu-id="b3433-517">The following options are non-exclusive:</span></span>

* <span data-ttu-id="b3433-518">`identity`&emsp;Nécessite des informations d’identité d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="b3433-518">`identity` &emsp; Requires user identity information</span></span>
* <span data-ttu-id="b3433-519">`messageTeamMembers`&emsp;Nécessite l’autorisation d’envoyer des messages directs aux membres de l’équipe</span><span class="sxs-lookup"><span data-stu-id="b3433-519">`messageTeamMembers` &emsp; Requires permission to send direct messages to team members</span></span>

<span data-ttu-id="b3433-520">Si vous modifiez ces autorisations lors de la mise à jour de votre application, vos utilisateurs répéteront le processus de consentement la première fois qu’ils exécuteront l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="b3433-520">Changing these permissions when updating your app will cause your users to repeat the consent process the first time they run the updated app.</span></span> <span data-ttu-id="b3433-521">Pour plus d’informations, consultez [la rubrique mise à jour de votre application](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) .</span><span class="sxs-lookup"><span data-stu-id="b3433-521">See [Updating your app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md) for more information.</span></span>

## <a name="devicepermissions"></a><span data-ttu-id="b3433-522">devicePermissions</span><span class="sxs-lookup"><span data-stu-id="b3433-522">devicePermissions</span></span>

<span data-ttu-id="b3433-523">**Facultatif** — tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="b3433-523">**Optional** — array of strings</span></span>

<span data-ttu-id="b3433-524">Spécifie les fonctionnalités natives sur l’appareil d’un utilisateur auquel votre application peut demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="b3433-524">Specifies the native features on a user's device that your app may request access to.</span></span> <span data-ttu-id="b3433-525">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="b3433-525">Options are:</span></span>

* `geolocation`
* `media`
* `notifications`
* `midi`
* `openExternal`

## <a name="validdomains"></a><span data-ttu-id="b3433-526">validDomains</span><span class="sxs-lookup"><span data-stu-id="b3433-526">validDomains</span></span>

<span data-ttu-id="b3433-527">**Facultatif** **, sauf indication contraire**</span><span class="sxs-lookup"><span data-stu-id="b3433-527">**Optional**, except **Required** where noted</span></span>

<span data-ttu-id="b3433-528">Une liste des domaines valides pour les sites Web que l’application prévoit de charger dans le client Teams.</span><span class="sxs-lookup"><span data-stu-id="b3433-528">A list of valid domains for websites the app expects to load within the Teams client.</span></span> <span data-ttu-id="b3433-529">Les listes de domaine peuvent inclure des caractères génériques, par exemple `*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="b3433-529">Domain listings can include wildcards, for example `*.example.com`.</span></span> <span data-ttu-id="b3433-530">Cela correspond exactement à un segment du domaine ; Si vous devez faire correspondre `a.b.example.com` , utilisez `*.*.example.com` .</span><span class="sxs-lookup"><span data-stu-id="b3433-530">This matches exactly one segment of the domain; if you need to match `a.b.example.com` then use `*.*.example.com`.</span></span> <span data-ttu-id="b3433-531">Si la configuration de votre onglet ou de votre interface utilisateur de contenu doit accéder à un autre domaine en plus de celui utilisé pour la configuration d’onglet, ce domaine doit être spécifié ici.</span><span class="sxs-lookup"><span data-stu-id="b3433-531">If your tab configuration or content UI needs to navigate to any other domain besides the one use for tab configuration, that domain must be specified here.</span></span>

<span data-ttu-id="b3433-532">Toutefois, il n’est **pas** nécessaire d’inclure les domaines des fournisseurs d’identité que vous souhaitez prendre en charge dans votre application.</span><span class="sxs-lookup"><span data-stu-id="b3433-532">It is **not** necessary to include the domains of identity providers you want to support in your app, however.</span></span> <span data-ttu-id="b3433-533">Par exemple, pour authentifier à l’aide d’un ID Google, il est nécessaire de rediriger vers accounts.google.com, mais vous ne devez pas inclure accounts.google.com dans `validDomains[]` .</span><span class="sxs-lookup"><span data-stu-id="b3433-533">For example, to authenticate using a Google ID, it's necessary to redirect to accounts.google.com, but you should not include accounts.google.com in `validDomains[]`.</span></span>

<span data-ttu-id="b3433-534">Les applications teams qui requièrent leurs propres URL SharePoint pour fonctionner correctement, peuvent inclure « {teamsitedomain} » dans leur liste de domaines valide.</span><span class="sxs-lookup"><span data-stu-id="b3433-534">Teams apps that require their own sharepoint URLs to function well, may include "{teamsitedomain}" in their valid domain list.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3433-535">N’ajoutez pas de domaines qui se trouvent en dehors de votre contrôle, soit directement, soit via des caractères génériques.</span><span class="sxs-lookup"><span data-stu-id="b3433-535">Do not add domains that are outside your control, either directly or via wildcards.</span></span> <span data-ttu-id="b3433-536">Par exemple, `yourapp.onmicrosoft.com` est valide, mais n' `*.onmicrosoft.com` est pas valide.</span><span class="sxs-lookup"><span data-stu-id="b3433-536">For example, `yourapp.onmicrosoft.com` is valid, but `*.onmicrosoft.com` is not valid.</span></span>

<span data-ttu-id="b3433-537">L’objet est un tableau contenant tous les éléments du type `string` .</span><span class="sxs-lookup"><span data-stu-id="b3433-537">The object is an array with all elements of the type `string`.</span></span>

## <a name="webapplicationinfo"></a><span data-ttu-id="b3433-538">webApplicationInfo</span><span class="sxs-lookup"><span data-stu-id="b3433-538">webApplicationInfo</span></span>

<span data-ttu-id="b3433-539">**Facultatif** — Object</span><span class="sxs-lookup"><span data-stu-id="b3433-539">**Optional** — object</span></span>

<span data-ttu-id="b3433-540">Spécifiez votre ID d’application Azure Active Directory (Azure AD) et les informations Microsoft Graph pour aider les utilisateurs à se connecter en toute transparence à votre application.</span><span class="sxs-lookup"><span data-stu-id="b3433-540">Specify your Azure Active Directory (Azure AD) App ID and Microsoft Graph information to help users seamlessly sign into your app.</span></span> <span data-ttu-id="b3433-541">Si votre application est inscrite dans Azure AD, vous devez fournir l’ID de l’application, afin que les administrateurs puissent consulter facilement les autorisations et accorder le consentement dans le centre d’administration Teams.</span><span class="sxs-lookup"><span data-stu-id="b3433-541">If your app is registered in Azure AD, you must provide the App ID, so that administrators can easily review permissions and grant consent in Teams admin center.</span></span>

|<span data-ttu-id="b3433-542">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-542">Name</span></span>| <span data-ttu-id="b3433-543">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-543">Type</span></span>| <span data-ttu-id="b3433-544">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-544">Maximum size</span></span> | <span data-ttu-id="b3433-545">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-545">Required</span></span> | <span data-ttu-id="b3433-546">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-546">Description</span></span>|
|---|---|---|---|---|
|`id`|<span data-ttu-id="b3433-547">string</span><span class="sxs-lookup"><span data-stu-id="b3433-547">string</span></span>|<span data-ttu-id="b3433-548">36 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-548">36 characters</span></span>|<span data-ttu-id="b3433-549">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-549">✔</span></span>|<span data-ttu-id="b3433-550">ID de l’application AAD de l’application.</span><span class="sxs-lookup"><span data-stu-id="b3433-550">AAD application id of the app.</span></span> <span data-ttu-id="b3433-551">Cet ID doit être un GUID.</span><span class="sxs-lookup"><span data-stu-id="b3433-551">This id must be a GUID.</span></span>|
|`resource`|<span data-ttu-id="b3433-552">string</span><span class="sxs-lookup"><span data-stu-id="b3433-552">string</span></span>|<span data-ttu-id="b3433-553">2 048 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-553">2048 characters</span></span>|<span data-ttu-id="b3433-554">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-554">✔</span></span>|<span data-ttu-id="b3433-555">URL de ressource de l’application pour l’acquisition du jeton d’authentification pour l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b3433-555">Resource url of app for acquiring auth token for SSO.</span></span>|
|`applicationPermissions`|<span data-ttu-id="b3433-556">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="b3433-556">array of strings</span></span>|<span data-ttu-id="b3433-557">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-557">128 characters</span></span>||<span data-ttu-id="b3433-558">Spécifier le [consentement spécifique](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions) à une ressource granulaire</span><span class="sxs-lookup"><span data-stu-id="b3433-558">Specify granular [resource specific consent](../../graph-api/rsc/resource-specific-consent.md#resource-specific-permissions)</span></span>|

## <a name="showloadingindicator"></a><span data-ttu-id="b3433-559">showLoadingIndicator</span><span class="sxs-lookup"><span data-stu-id="b3433-559">showLoadingIndicator</span></span>

<span data-ttu-id="b3433-560">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="b3433-560">**Optional** — boolean</span></span>

<span data-ttu-id="b3433-561">Indique si l’indicateur de chargement est affiché ou non lors du chargement d’une application ou d’un onglet.</span><span class="sxs-lookup"><span data-stu-id="b3433-561">Indicate whether or not to show the loading indicator when an app/tab is loading.</span></span> <span data-ttu-id="b3433-562">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="b3433-562">Default: **false**.</span></span>
>[!NOTE]
><span data-ttu-id="b3433-563">Si vous définissez « showLoadingIndicator : true » dans votre manifeste d’application, pour que la page se charge correctement, vous devez modifier les pages de contenu de vos onglets et modules de tâches conformément au protocole décrit dans [Show a Native Loading Indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span><span class="sxs-lookup"><span data-stu-id="b3433-563">If you set "showLoadingIndicator : true" in your app manifest, then for the page to load correctly, you must modify the content pages of your tabs and task modules as per the protocol described in [Show a native loading indicator](../../tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator) document.</span></span>


## <a name="isfullscreen"></a><span data-ttu-id="b3433-564">isFullScreen</span><span class="sxs-lookup"><span data-stu-id="b3433-564">isFullScreen</span></span>

 <span data-ttu-id="b3433-565">**Facultatif** — booléen</span><span class="sxs-lookup"><span data-stu-id="b3433-565">**Optional** — boolean</span></span>

<span data-ttu-id="b3433-566">Indiquer où une application personnelle est rendue avec ou sans barre d’en-tête d’onglet.</span><span class="sxs-lookup"><span data-stu-id="b3433-566">Indicate where a personal app is rendered with or without a tab-header bar.</span></span> <span data-ttu-id="b3433-567">Par défaut : **false**.</span><span class="sxs-lookup"><span data-stu-id="b3433-567">Default: **false**.</span></span>

## <a name="activities"></a><span data-ttu-id="b3433-568">activities</span><span class="sxs-lookup"><span data-stu-id="b3433-568">activities</span></span>

<span data-ttu-id="b3433-569">**Facultatif** — Object</span><span class="sxs-lookup"><span data-stu-id="b3433-569">**Optional** — object</span></span>

<span data-ttu-id="b3433-570">Définissez les propriétés que votre application utilisera pour publier dans un flux d’activités utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b3433-570">Define the properties your app will use to post to a user activity feed.</span></span>

|<span data-ttu-id="b3433-571">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-571">Name</span></span>| <span data-ttu-id="b3433-572">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-572">Type</span></span>| <span data-ttu-id="b3433-573">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-573">Maximum size</span></span> | <span data-ttu-id="b3433-574">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-574">Required</span></span> | <span data-ttu-id="b3433-575">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-575">Description</span></span>|
|---|---|---|---|---|
|`activityTypes`|<span data-ttu-id="b3433-576">Tableau d’objets</span><span class="sxs-lookup"><span data-stu-id="b3433-576">array of Objects</span></span>|<span data-ttu-id="b3433-577">128 éléments</span><span class="sxs-lookup"><span data-stu-id="b3433-577">128 items</span></span>| | <span data-ttu-id="b3433-578">Spécifiez les types d’activités que votre application peut publier dans le flux d’activités des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b3433-578">Specify the types of activities that your app can post to a users activity feed.</span></span>|

### <a name="activitiesactivitytypes"></a><span data-ttu-id="b3433-579">Activities. activityTypes</span><span class="sxs-lookup"><span data-stu-id="b3433-579">activities.activityTypes</span></span>

|<span data-ttu-id="b3433-580">Nom</span><span class="sxs-lookup"><span data-stu-id="b3433-580">Name</span></span>| <span data-ttu-id="b3433-581">Type</span><span class="sxs-lookup"><span data-stu-id="b3433-581">Type</span></span>| <span data-ttu-id="b3433-582">Taille maximale</span><span class="sxs-lookup"><span data-stu-id="b3433-582">Maximum size</span></span> | <span data-ttu-id="b3433-583">Requis</span><span class="sxs-lookup"><span data-stu-id="b3433-583">Required</span></span> | <span data-ttu-id="b3433-584">Description</span><span class="sxs-lookup"><span data-stu-id="b3433-584">Description</span></span>|
|---|---|---|---|---|
|`type`|<span data-ttu-id="b3433-585">string</span><span class="sxs-lookup"><span data-stu-id="b3433-585">string</span></span>|<span data-ttu-id="b3433-586">32 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-586">32 characters</span></span>|<span data-ttu-id="b3433-587">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-587">✔</span></span>|<span data-ttu-id="b3433-588">Type de notification.</span><span class="sxs-lookup"><span data-stu-id="b3433-588">The notification type.</span></span> <span data-ttu-id="b3433-589">*Voir ci-dessous*.</span><span class="sxs-lookup"><span data-stu-id="b3433-589">*See below*.</span></span>|
|`description`|<span data-ttu-id="b3433-590">string</span><span class="sxs-lookup"><span data-stu-id="b3433-590">string</span></span>|<span data-ttu-id="b3433-591">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-591">128 characters</span></span>|<span data-ttu-id="b3433-592">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-592">✔</span></span>|<span data-ttu-id="b3433-593">Brève description de la notification.</span><span class="sxs-lookup"><span data-stu-id="b3433-593">A brief description of the notification.</span></span> <span data-ttu-id="b3433-594">*Voir ci-dessous*.</span><span class="sxs-lookup"><span data-stu-id="b3433-594">*See below*.</span></span>|
|`templateText`|<span data-ttu-id="b3433-595">string</span><span class="sxs-lookup"><span data-stu-id="b3433-595">string</span></span>|<span data-ttu-id="b3433-596">128 caractères</span><span class="sxs-lookup"><span data-stu-id="b3433-596">128 characters</span></span>|<span data-ttu-id="b3433-597">✔</span><span class="sxs-lookup"><span data-stu-id="b3433-597">✔</span></span>|<span data-ttu-id="b3433-598">Ex : « tâche créée le {Actor} {taskId} »</span><span class="sxs-lookup"><span data-stu-id="b3433-598">Ex: "{actor} created task {taskId} for you"</span></span>|

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
