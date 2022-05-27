---
title: Obtenir un contexte Teams pour votre onglet
description: Décrit comment obtenir du contexte utilisateur dans vos onglets
ms.localizationpriority: medium
ms.topic: how-to
keywords: Contexte utilisateur sous l’onglet Équipes
ms.openlocfilehash: 04a0e751a8a532895b183690e00bc058c94d3346
ms.sourcegitcommit: d9025e959dcdd011ed4feca820dae7c5d1251b27
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/27/2022
ms.locfileid: "65755943"
---
# <a name="get-context-for-your-tab"></a>Obtenir un contexte Teams pour votre onglet

Votre onglet nécessite des informations contextuelles pour afficher le contenu pertinent :

* Informations de base sur l’utilisateur, l’équipe ou l’entreprise.
* Paramètres régionaux et informations de thème.
* Lisez le `entityId` ou `subEntityId` qui identifie ce qui se trouve dans cet onglet.

[!INCLUDE [sdk-include](~/includes/sdk-include.md)]

## <a name="user-context"></a>Contexte utilisateur

Le contexte de l’utilisateur, de l’équipe ou de l’entreprise peut être particulièrement utile quand :

* Vous créez ou associez des ressources dans votre application à l’utilisateur ou à l’équipe spécifié.
* Vous lancez un flux d’authentification à partir d’Microsoft Azure Active Directory (Azure AD) ou d’un autre fournisseur d’identité, et vous n’avez pas besoin que l’utilisateur entre à nouveau son nom d’utilisateur.

Pour plus d’informations, consultez [l’authentification d’un utilisateur dans votre Microsoft Teams](~/concepts/authentication/authentication.md).

> [!IMPORTANT]
> Bien que ces informations utilisateur puissent vous aider à fournir une expérience utilisateur fluide, vous ne devez pas les utiliser comme preuve d’identité.  Par exemple, un attaquant peut charger votre page dans un navigateur et afficher des informations ou des demandes dangereuses.

## <a name="access-context-information"></a>Accéder aux informations de contexte

Vous pouvez accéder aux informations de contexte de deux façons :

* Insérer des valeurs d’espace réservé d’URL.
* Utilisez le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client).

### <a name="get-context-by-inserting-url-placeholder-values"></a>Obtenir le contexte en insérant des valeurs d’espace réservé d’URL

Utilisez des espaces réservés dans vos URL de configuration ou de contenu. Microsoft Teams remplace les espaces réservés par les valeurs appropriées lorsqu’il détermine l’URL de configuration ou de contenu. Les espaces réservés disponibles incluent tous les champs de l’objet [de contexte](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-1.12.1&preserve-view=true) . Voici les scénarios les plus courants :

* {entityId} : ID que vous avez fourni pour l’élément dans cet onglet lors de la première [configuration de l’onglet](~/tabs/how-to/create-tab-pages/configuration-page.md).
* {subEntityId} : ID que vous avez fourni lors de la génération d’un [lien profond](~/concepts/build-and-test/deep-links.md) pour un élément spécifique dans cet onglet. Cela doit être utilisé pour restaurer à un état spécifique au sein d’une entité ; par exemple, le défilement vers ou l’activation d’un élément de contenu spécifique.
* {loginHint} : valeur appropriée comme indicateur de connexion pour Azure AD. Il s’agit généralement du nom de connexion de l’utilisateur actuel dans son locataire d’origine.
* {userPrincipalName} : nom d’utilisateur principal de l’utilisateur actuel dans le locataire actuel.
* {userObjectId} : ID d’objet Azure AD de l’utilisateur actuel dans le locataire actuel.
* {theme} : thème de l’interface utilisateur actuelle, tel que `default`, `dark`ou `contrast`.
* {groupId} : ID du groupe Office 365 dans lequel réside l’onglet.
* {tid}: ID de client Azure AD de l’utilisateur actuel.
* {locale} : paramètres régionaux actuels de l’utilisateur au format languageId-countryId(en-us).

> [!NOTE]
> L’espace réservé `{upn}`précédent est désormais supprimé. Pour des raisons de compatibilité ascendante, il s'agit actuellement d'un synonyme de `{loginHint}`.

Par exemple, dans le manifeste de votre onglet sur lequel vous définissez l’attribut `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, l’utilisateur connecté a les attributs suivants :

* Leur nom d’utilisateur est **user@example.com**.
* Leur ID de locataire d’entreprise est **e2653c-etc**.
* Ils sont membres du groupe Office 365 avec l’ID **00209384-etc**.
* L’utilisateur a défini son thème Teams sur **sombre**.

Quand ils configurent l’onglet, Teams appelle l’URL suivante :

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a>Obtenir le contexte à l’aide de la bibliothèque JavaScript Microsoft Teams

Vous pouvez également récupérer les informations répertoriées ci-dessus à l’aide du [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client) en appelant la `app.getContext()` fonction. Pour plus d’informations, consultez les propriétés de [l’interface contextuel](/javascript/api/@microsoft/teams-js/app.context?view=msteams-client-js-latest&preserve-view=true).

## <a name="retrieve-context-in-private-channels"></a>Récupérer le contexte dans des canaux privés

Lorsque votre page de contenu est chargée dans un canal privé, les données que vous recevez de l’appel `getContext` sont masquées pour protéger la confidentialité du canal.

Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal privé :

* `groupId`: Non défini pour les canaux privés
* `teamId`: défini sur le threadId du canal privé
* `teamName`: définir sur le nom du canal privé
* `teamSiteUrl`: défini sur l’URL d’un site SharePoint distinct et unique pour le canal privé
* `teamSitePath`: définir le chemin d’accès d’un site SharePoint distinct et unique pour le canal privé
* `teamSiteDomain`: défini sur le domaine d’un domaine de site SharePoint distinct et unique pour le canal privé

Si votre page utilise l’une de ces valeurs, la valeur du `channelType` champ doit être `Private` de déterminer si votre page est chargée dans un canal privé et peut répondre de manière appropriée.

## <a name="retrieve-context-in-microsoft-teams-connect-shared-channels"></a>Récupérer le contexte dans Microsoft Teams Connect canaux partagés

> [!NOTE]
> Actuellement, Microsoft Teams Connect canaux partagés sont en [préversion](../../resources/dev-preview/developer-preview-intro.md) développeur uniquement.

Lorsque votre page de contenu est chargée dans un canal partagé Microsoft Teams Connect, les données que vous recevez de l’appel `getContext` sont modifiées en raison de la liste unique d’utilisateurs dans les canaux partagés.

Les champs suivants sont modifiés lorsque votre page de contenu se trouve dans un canal partagé :

* `groupId`: non défini pour les canaux partagés.
* `teamId`: défini sur l’équipe `threadId` , le canal est partagé pour l’utilisateur actuel. Si l’utilisateur a accès à plusieurs équipes, il `teamId` est défini sur l’équipe qui héberge (crée) le canal partagé.
* `teamName`: défini sur le nom de l’équipe, le canal est partagé pour l’utilisateur actuel. Si l’utilisateur a accès à plusieurs équipes, il `teamName` est défini sur l’équipe qui héberge (crée) le canal partagé.
* `teamSiteUrl`: défini sur l’URL d’un site SharePoint distinct et unique pour le canal partagé.
* `teamSitePath`: défini sur le chemin d’accès d’un site SharePoint distinct et unique pour le canal partagé.
* `teamSiteDomain`: défini sur le domaine d’un domaine de site SharePoint distinct et unique pour le canal partagé.

En plus de ces modifications de champ, deux nouveaux champs sont disponibles pour les canaux partagés :

* `hostTeamGroupId`: affectez la `groupId` valeur associée à l’équipe d’hébergement ou à l’équipe qui a créé le canal partagé. La propriété peut permettre à Microsoft API Graph appels de récupérer l’appartenance au canal partagé.
* `hostTeamTenantId`: affectez la `tenantId` valeur associée à l’équipe d’hébergement ou à l’équipe qui a créé le canal partagé. La propriété peut être référencée de manière croisée avec l’ID de locataire de l’utilisateur actuel trouvé dans le `tid` champ de `getContext` déterminer si l’utilisateur est interne ou externe au locataire de l’équipe d’hébergement.

Si votre page utilise l’une de ces valeurs, la valeur du `channelType` champ doit être `Shared` de déterminer si votre page est chargée dans un canal partagé et peut répondre de manière appropriée.

> [!NOTE]
> Chaque fois qu’un utilisateur redémarre ou recharge le Teams client de bureau ou web, un nouvel ID de session est créé, suivi par Teams session, tandis qu’un utilisateur quitte les applications Teams et le recharge dans Teams plateforme, un nouvel ID de session d’application est créé, suivi par session d’application.

## <a name="handle-theme-change"></a>Gérer la modification du thème

Vous pouvez inscrire votre application pour être informé si le thème change en appelant `app.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.

L’argument `theme` dans la fonction est une chaîne avec la valeur `default`, `dark`ou `contrast`.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer des onglets avec les Cartes adaptatives](~/tabs/how-to/build-adaptive-card-tabs.md)

## <a name="see-also"></a>Articles associés

* [Instructions de conception de tabulation](../../tabs/design/tabs.md)
* [Onglets Teams](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
* [Utiliser des modules de tâche dans les onglets](~/task-modules-and-cards/task-modules/task-modules-tabs.md)
