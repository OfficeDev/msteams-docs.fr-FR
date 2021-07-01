---
title: Intégration de la fonctionnalité S sélectionneur de personnes
author: Rajeshwari-v
description: Comment utiliser le SDK Teams client JavaScript pour intégrer la fonctionnalité S picker de personnes
keywords: contrôle du s picker de personnes
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 8399eeb1a088e4b60c466d51c223b9405ebf1711
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211635"
---
# <a name="integrate-people-picker-capability"></a><span data-ttu-id="c2c05-104">Intégration de la fonctionnalité S sélectionneur de personnes</span><span class="sxs-lookup"><span data-stu-id="c2c05-104">Integrate People Picker capability</span></span> 

<span data-ttu-id="c2c05-105">Le sélecateur de personnes est un contrôle pour rechercher et sélectionner des personnes.</span><span class="sxs-lookup"><span data-stu-id="c2c05-105">People Picker is a control to search and select people.</span></span> <span data-ttu-id="c2c05-106">Il s’agit d’une fonctionnalité native disponible sur Teams plateforme.</span><span class="sxs-lookup"><span data-stu-id="c2c05-106">This is a native capability available in Teams platform.</span></span> <span data-ttu-id="c2c05-107">Vous pouvez intégrer Teams contrôle d’entrée natif du s picker de personnes à vos applications web.</span><span class="sxs-lookup"><span data-stu-id="c2c05-107">You can integrate Teams native People Picker input control with your web apps.</span></span> <span data-ttu-id="c2c05-108">Vous pouvez choisir entre une sélection unique ou multiple et des configurations, telles que la limitation de la recherche au sein d’une conversation, de canaux ou de l’ensemble de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="c2c05-108">You can select between single or multi selection, and configurations, such as limiting search within a chat, channels, or across the entire organization.</span></span>

<span data-ttu-id="c2c05-109">Vous pouvez utiliser [Microsoft Teams SDK client JavaScript,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)qui fournit l’API pour intégrer la fonctionnalité S picker de personnes `selectPeople` dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="c2c05-109">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides `selectPeople` API to integrate the People Picker capability within your web app.</span></span> 

## <a name="advantages-of-integrating-people-picker-capability"></a><span data-ttu-id="c2c05-110">Avantages de l’intégration de la fonctionnalité de s picker de personnes</span><span class="sxs-lookup"><span data-stu-id="c2c05-110">Advantages of integrating People Picker capability</span></span>

* <span data-ttu-id="c2c05-111">Le contrôle S picker de personnes fonctionne sur toutes les surfaces Teams, telles que le module de tâche, une conversation, un canal, un onglet de réunion et une application personnelle.</span><span class="sxs-lookup"><span data-stu-id="c2c05-111">The People Picker control works in all of Teams surfaces, such as task module, a chat, channel, meeting tab, and personal app.</span></span>
* <span data-ttu-id="c2c05-112">Ce contrôle vous permet de rechercher et de sélectionner des utilisateurs au sein d’une conversation, d’un canal ou de l’ensemble de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="c2c05-112">This control allows you to search for and select users within a chat, channel, or the entire organization.</span></span>
*  <span data-ttu-id="c2c05-113">La fonctionnalité Sélecteur de personnes facilite les scénarios impliquant l’affectation de tâches, le marquage et l’informer d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c2c05-113">The People Picker capability helps with scenarios involving task assignment, tagging, notifying a user.</span></span> 
* <span data-ttu-id="c2c05-114">Vous pouvez utiliser ce contrôle facilement disponible dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="c2c05-114">You can use this readily available control in your web app.</span></span> <span data-ttu-id="c2c05-115">Cela permet d’économiser considérablement l’effort et le temps nécessaires pour créer un tel contrôle vous-même.</span><span class="sxs-lookup"><span data-stu-id="c2c05-115">It saves the effort and time significantly to build such a control on your own.</span></span>

<span data-ttu-id="c2c05-116">Vous devez appeler l’API pour intégrer le contrôle S picker de personnes `selectPeople` dans votre application Teams utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c2c05-116">You must call the `selectPeople` API to integrate People Picker control in your Teams app.</span></span> <span data-ttu-id="c2c05-117">Pour une intégration efficace, vous devez comprendre l’extrait de [code](#code-snippet) pour appeler l’API.</span><span class="sxs-lookup"><span data-stu-id="c2c05-117">For effective integration, you must have an understanding of [code snippet](#code-snippet) for calling the API.</span></span> <span data-ttu-id="c2c05-118">Il est important de vous familiariser avec les erreurs de [réponse d’API](#error-handling) pour gérer les erreurs dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="c2c05-118">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your web app.</span></span>

> [!NOTE] 
> <span data-ttu-id="c2c05-119">Actuellement, Microsoft Teams prise en charge de la fonctionnalité S’il s’agit du s’il s’agit de personnes est disponible uniquement pour les clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="c2c05-119">Currently, Microsoft Teams support for People Picker capability is available for mobile clients only.</span></span>

## <a name="selectpeople-api"></a><span data-ttu-id="c2c05-120">`selectPeople` API</span><span class="sxs-lookup"><span data-stu-id="c2c05-120">`selectPeople` API</span></span> 

<span data-ttu-id="c2c05-121">`selectPeople`L’API vous permet d’ajouter des Teams `People Picker input control` natives à vos applications web.</span><span class="sxs-lookup"><span data-stu-id="c2c05-121">`selectPeople` API enables you to add Teams native `People Picker input control` to your web apps.</span></span>  
<span data-ttu-id="c2c05-122">La description de l’API est la suivante :</span><span class="sxs-lookup"><span data-stu-id="c2c05-122">The API description is as follows:</span></span>

| <span data-ttu-id="c2c05-123">API</span><span class="sxs-lookup"><span data-stu-id="c2c05-123">API</span></span>      | <span data-ttu-id="c2c05-124">Description</span><span class="sxs-lookup"><span data-stu-id="c2c05-124">Description</span></span>  |
| --- | --- |
|<span data-ttu-id="c2c05-125">**selectPeople**</span><span class="sxs-lookup"><span data-stu-id="c2c05-125">**selectPeople**</span></span>|<span data-ttu-id="c2c05-126">Lance un sélecateur de personnes et permet à l’utilisateur de rechercher et de sélectionner une ou plusieurs personnes dans la liste.</span><span class="sxs-lookup"><span data-stu-id="c2c05-126">Launches a People Picker and allows the user to search and select one or more people from the list.</span></span><br/><br/><span data-ttu-id="c2c05-127">Cette API renvoie l’ID, le nom et l’adresse e-mail des utilisateurs sélectionnés à l’application web d’appel.</span><span class="sxs-lookup"><span data-stu-id="c2c05-127">This API returns the ID, name and email address of selected users to the calling web app.</span></span><br/><br/><span data-ttu-id="c2c05-128">Dans le cas d’une application personnelle, le contrôle recherche dans l’organisation.</span><span class="sxs-lookup"><span data-stu-id="c2c05-128">In case of a personal app, the control searches across the organization.</span></span> <span data-ttu-id="c2c05-129">Si l’application est ajoutée à une conversation ou un canal, le contexte de recherche est configuré en fonction du scénario.</span><span class="sxs-lookup"><span data-stu-id="c2c05-129">If the app is added to a chat or channel, then the search context is configured depending on the scenario.</span></span> <span data-ttu-id="c2c05-130">La recherche est limitée au sein des membres de cette conversation, canal ou mis à disposition au sein de l’organisation.</span><span class="sxs-lookup"><span data-stu-id="c2c05-130">The search is restricted within the members of that chat, channel, or made available across the organization.</span></span>|

<span data-ttu-id="c2c05-131">`selectPeople`L’API est livré avec les configurations d’entrée suivantes :</span><span class="sxs-lookup"><span data-stu-id="c2c05-131">The `selectPeople` API comes along with following input configurations:</span></span>

|<span data-ttu-id="c2c05-132">Paramètre de configuration</span><span class="sxs-lookup"><span data-stu-id="c2c05-132">Configuration parameter</span></span>|<span data-ttu-id="c2c05-133">Type</span><span class="sxs-lookup"><span data-stu-id="c2c05-133">Type</span></span>|<span data-ttu-id="c2c05-134">Description</span><span class="sxs-lookup"><span data-stu-id="c2c05-134">Description</span></span>| <span data-ttu-id="c2c05-135">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="c2c05-135">Default value</span></span>|
|-----|------|--------------|------|
|`title`| <span data-ttu-id="c2c05-136">String</span><span class="sxs-lookup"><span data-stu-id="c2c05-136">String</span></span>| <span data-ttu-id="c2c05-137">Il s’agit d’un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="c2c05-137">It is an optional parameter.</span></span> <span data-ttu-id="c2c05-138">Il définit le titre du contrôle S sélectionneur de personnes.</span><span class="sxs-lookup"><span data-stu-id="c2c05-138">It sets title for the People Picker control.</span></span> | <span data-ttu-id="c2c05-139">Sélectionner des personnes</span><span class="sxs-lookup"><span data-stu-id="c2c05-139">Select people</span></span>|
|`setSelected`|<span data-ttu-id="c2c05-140">String</span><span class="sxs-lookup"><span data-stu-id="c2c05-140">String</span></span>| <span data-ttu-id="c2c05-141">Il s’agit d’un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="c2c05-141">It is an optional parameter.</span></span> <span data-ttu-id="c2c05-142">Vous devez transmettre les ID AAD des personnes à pré-sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c2c05-142">You must pass AAD IDs of the people to be preselected.</span></span> <span data-ttu-id="c2c05-143">Ce paramètre présélectionne les personnes lors du lancement du contrôle Sélectionneur de personnes.</span><span class="sxs-lookup"><span data-stu-id="c2c05-143">This parameter preselects people while launching the People Picker control.</span></span> <span data-ttu-id="c2c05-144">En cas de sélection unique, seul le premier utilisateur valide est pré-préruplé en ignorant le reste.</span><span class="sxs-lookup"><span data-stu-id="c2c05-144">In case of single selection, only the first valid user is prepopulated ignoring the rest.</span></span> |<span data-ttu-id="c2c05-145">Null</span><span class="sxs-lookup"><span data-stu-id="c2c05-145">Null</span></span>| 
|`openOrgWideSearchInChatOrChannel`|<span data-ttu-id="c2c05-146">Boolean</span><span class="sxs-lookup"><span data-stu-id="c2c05-146">Boolean</span></span> | <span data-ttu-id="c2c05-147">Il s’agit d’un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="c2c05-147">It is an optional parameter.</span></span> <span data-ttu-id="c2c05-148">Lorsqu’elle est définie sur true, elle lance le sérial de personnes dans l’étendue de l’organisation, même si l’application est ajoutée à une conversation ou un canal.</span><span class="sxs-lookup"><span data-stu-id="c2c05-148">When it is set to true, it launches the People Picker in organization wide scope even if the app is added to a chat or channel.</span></span> |<span data-ttu-id="c2c05-149">Faux</span><span class="sxs-lookup"><span data-stu-id="c2c05-149">False</span></span>|
|`singleSelect`|<span data-ttu-id="c2c05-150">Boolean</span><span class="sxs-lookup"><span data-stu-id="c2c05-150">Boolean</span></span>|<span data-ttu-id="c2c05-151">Il s’agit d’un paramètre facultatif.</span><span class="sxs-lookup"><span data-stu-id="c2c05-151">It is an optional parameter.</span></span> <span data-ttu-id="c2c05-152">Lorsqu’elle est définie sur True, elle lance le s sélectionneur de personnes en limitant la sélection à un seul utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c2c05-152">When it is set to true, it launches the People Picker restricting the selection to one user only.</span></span> |<span data-ttu-id="c2c05-153">Faux</span><span class="sxs-lookup"><span data-stu-id="c2c05-153">False</span></span>|

<span data-ttu-id="c2c05-154">L’image suivante illustre l’expérience de la fonctionnalité S picker de personnes dans un exemple d’application web :</span><span class="sxs-lookup"><span data-stu-id="c2c05-154">The following image depicts the experience of People Picker capability in a sample web app:</span></span>

![Expérience d’application web de la fonctionnalité S picker de personnes](../../assets/images/tabs/people-picker-control-capability.png)

### <a name="code-snippet"></a><span data-ttu-id="c2c05-156">Extrait de code</span><span class="sxs-lookup"><span data-stu-id="c2c05-156">Code snippet</span></span>

<span data-ttu-id="c2c05-157">**Appel `selectPeople` API permettant** de sélectionner des personnes dans une liste :</span><span class="sxs-lookup"><span data-stu-id="c2c05-157">**Calling `selectPeople` API** to select people from a list:</span></span>

```javascript
 microsoftTeams.people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
 {
    if (error) 
    {
        if (error.message) 
           {
             alert(" ErrorCode: " + error.errorCode + error.message);
           }
            else 
            {
              alert(" ErrorCode: " + error.errorCode);
            }
      }
    if (people)
     {
            output(" People length: " + people.length + " " + JSON.stringify(people));
      }
  });
```

## <a name="error-handling"></a><span data-ttu-id="c2c05-158">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="c2c05-158">Error handling</span></span>

<span data-ttu-id="c2c05-159">Vous devez veiller à gérer correctement les erreurs dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="c2c05-159">You must ensure to handle the errors appropriately in your web app.</span></span> <span data-ttu-id="c2c05-160">Le tableau suivant répertorie les codes d’erreur et les conditions dans lesquelles les erreurs sont générées :</span><span class="sxs-lookup"><span data-stu-id="c2c05-160">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="c2c05-161">Code d’erreur</span><span class="sxs-lookup"><span data-stu-id="c2c05-161">Error code</span></span> |  <span data-ttu-id="c2c05-162">Nom de l’erreur</span><span class="sxs-lookup"><span data-stu-id="c2c05-162">Error name</span></span>     | <span data-ttu-id="c2c05-163">Condition</span><span class="sxs-lookup"><span data-stu-id="c2c05-163">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="c2c05-164">**100**</span><span class="sxs-lookup"><span data-stu-id="c2c05-164">**100**</span></span> | <span data-ttu-id="c2c05-165">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="c2c05-165">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="c2c05-166">L’API n’est pas prise en charge sur la plateforme actuelle.</span><span class="sxs-lookup"><span data-stu-id="c2c05-166">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="c2c05-167">**500**</span><span class="sxs-lookup"><span data-stu-id="c2c05-167">**500**</span></span> | <span data-ttu-id="c2c05-168">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="c2c05-168">INTERNAL_ERROR</span></span> | <span data-ttu-id="c2c05-169">Une erreur interne s’est produite lors du lancement du s picker de personnes.</span><span class="sxs-lookup"><span data-stu-id="c2c05-169">Internal error is encountered while launching People Picker.</span></span>|
| <span data-ttu-id="c2c05-170">**4000**</span><span class="sxs-lookup"><span data-stu-id="c2c05-170">**4000**</span></span> | <span data-ttu-id="c2c05-171">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="c2c05-171">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="c2c05-172">L’API est invoquée avec des arguments obligatoires erronés ou insuffisants.</span><span class="sxs-lookup"><span data-stu-id="c2c05-172">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="c2c05-173">**8000**</span><span class="sxs-lookup"><span data-stu-id="c2c05-173">**8000**</span></span> | <span data-ttu-id="c2c05-174">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="c2c05-174">USER_ABORT</span></span> |<span data-ttu-id="c2c05-175">L’utilisateur a annulé l’opération.</span><span class="sxs-lookup"><span data-stu-id="c2c05-175">User cancelled the operation.</span></span>|
| <span data-ttu-id="c2c05-176">**9000**</span><span class="sxs-lookup"><span data-stu-id="c2c05-176">**9000**</span></span> | <span data-ttu-id="c2c05-177">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="c2c05-177">OLD_PLATFORM</span></span> | <span data-ttu-id="c2c05-178">L’utilisateur se trouve sur une ancienne build de plateforme où l’implémentation de l’API n’est pas présente.</span><span class="sxs-lookup"><span data-stu-id="c2c05-178">User is on old platform build where implementation of the API is not present.</span></span>  <span data-ttu-id="c2c05-179">La mise à niveau de la build résout le problème.</span><span class="sxs-lookup"><span data-stu-id="c2c05-179">Upgrading the build resolves the issue.</span></span>|

## <a name="see-also"></a><span data-ttu-id="c2c05-180">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="c2c05-180">See also</span></span>

* [<span data-ttu-id="c2c05-181">Intégrer des fonctionnalités multimédias dans Teams</span><span class="sxs-lookup"><span data-stu-id="c2c05-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="c2c05-182">Intégrer le code QR ou la fonctionnalité de scanneur de code-barres dans Teams</span><span class="sxs-lookup"><span data-stu-id="c2c05-182">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="c2c05-183">Intégrer des fonctionnalités d’emplacement dans Teams</span><span class="sxs-lookup"><span data-stu-id="c2c05-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
