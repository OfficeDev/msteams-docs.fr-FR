---
title: Déploiement du lien des onglets et vue des étapes
author: Rajeshwari-v
description: Découvrez comment déployer un lien, ouvrir l’affichage de la scène et épingler un onglet avec Microsoft Teams application.
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: f465530dcc53ff3b0174f5b78ebf2240665a7d9e
ms.sourcegitcommit: 2c4c77dc8344f2fab8ed7a3f7155f15f0dd6a5ce
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/13/2021
ms.locfileid: "58345275"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Déploiement du lien des onglets et vue des étapes

> [!NOTE]
> Cette fonctionnalité est disponible uniquement en [prévisualisation pour les développeurs](../resources/dev-preview/developer-preview-intro.md) publics.

Stage View est un nouveau composant d’interface utilisateur qui vous permet d’afficher le contenu ouvert en plein écran en Teams et épinglé sous forme d’onglet.
 
> [!NOTE]
> Actuellement, Teams clients mobiles ne sont pas en charge le déploiement des liens d’onglets et l’affichage de la phase. Les clients mobiles utilisent l’attribut fourni par le développeur pour ouvrir la page dans le `websiteUrl` navigateur web de l’appareil.

## <a name="stage-view"></a>Vue d’étape

L’affichage d’étape est un composant d’interface utilisateur en plein écran que vous pouvez appeler pour faire surface à votre contenu web. Le service de déploiement de lien existant est mis à jour de sorte qu’il soit utilisé pour transformer les URL en onglet à l’aide d’une carte adaptative et des services de conversation. Lorsqu’un utilisateur envoie une URL dans une conversation ou un canal, l’URL est déployée vers une carte adaptative. L’utilisateur peut sélectionner **Afficher** dans la carte et épingler le contenu en tant qu’onglet directement à partir de l’affichage de l’étape.

## <a name="advantage-of-stage-view"></a>Avantage de l’affichage de l’étape

L’affichage de l’étape permet d’offrir une expérience plus transparente de l’affichage du contenu Teams. Les utilisateurs peuvent ouvrir et afficher le contenu fourni par votre application sans quitter le contexte, et ils peuvent épingler le contenu à la conversation ou au canal pour un accès rapide futur. Cela entraîne un plus grand engagement de l’utilisateur avec votre application.

## <a name="stage-view-vs-task-module"></a>Affichage de l’étape et module de tâche

|Vue d’étape|Module de tâche|
|:-----------|:-----------|
|L’affichage d’étape est utile lorsque vous avez du contenu enrichi à afficher aux utilisateurs, comme une page, un tableau de bord, un fichier, etc. Il fournit des fonctionnalités enrichies qui permettent d’restituer votre contenu dans le canevas plein écran.|[Le module de](../task-modules-and-cards/task-modules/task-modules-tabs.md) tâche est particulièrement utile pour afficher les messages qui nécessitent l’attention de l’utilisateur ou collecter les informations requises pour passer à l’étape suivante.|
  
## <a name="invoke-stage-view"></a>Appeler l’affichage de l’étape

Vous pouvez appeler l’affichage de l’étape des manières suivantes :

* [Appeler l’affichage de l’étape à partir d’une carte adaptative](#invoke-stage-view-from-adaptive-card)
* [Appeler l’affichage de l’étape par le biais d’un lien profond](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Appeler l’affichage de l’étape à partir d’une carte adaptative

Lorsque l’utilisateur entre une URL sur le client de bureau Teams, [](../task-modules-and-cards/cards/cards-actions.md) le bot est appelé et renvoie une carte adaptative avec la possibilité d’ouvrir l’URL dans une étape. Une fois qu’une étape est lancée et que l’étape est fournie, vous pouvez ajouter la possibilité d’épingler l’étape `tabInfo` sous la mesure d’un onglet.  

Les images suivantes affichent une étape ouverte à partir d’une carte adaptative :

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card1.png" alt="Open a stage from Adaptive Card" width="700"/>

<img src="~/assets/images/tab-images/open-stage-from-adaptive-card2.png" alt="Open a stage" width="700"/>

### <a name="example"></a>Exemple

Voici le code pour ouvrir une étape à partir d’une carte adaptative :

```json
{
    type: "Action.Submit",
    name: "View",
    data: {
          msteams: {
            type: "invoke",
            value: {
                type: "tab/tabInfoAction",
                tabInfo: {
                    contentUrl: contentUrl,
                    websiteUrl: websiteUrl,
                    name: "Tasks",
                    entityId: "entityId"
                 }
                }
            }
        }
} 
```

Le `invoke` type de requête doit être `composeExtension/queryLink` .

> [!NOTE]
> * `invoke` est similaire au flux de travail `appLinking` actuel. 
> * Pour conserver la cohérence, il est recommandé de nommer `Action.Submit` comme `View` .
> * `websiteUrl` est une propriété obligatoire à passer dans `TabInfo` l’objet.

Voici le processus d’appel de l’affichage de l’étape :

* Lorsque l’utilisateur sélectionne **Affichage,** le bot reçoit une `invoke` demande. Le type de requête `composeExtension/queryLink` est .
* `invoke` La réponse du bot contient une carte adaptative avec son `tab/tabInfoAction` type.
* Le bot répond par un `200` code.

> [!NOTE]
> Actuellement, Teams clients mobiles ne la prise en charge de la fonctionnalité Vue d’étape. Lorsqu’un utilisateur sélectionne **Afficher** sur un client mobile, l’utilisateur est conduit vers le navigateur de l’appareil. Le navigateur ouvre l’URL spécifiée dans le `websiteUrl` paramètre de `TabInfo` l’objet.

## <a name="invoke-stage-view-through-deep-link"></a>Appeler l’affichage de l’étape par le biais d’un lien profond

Pour appeler l’affichage de l’étape via un lien profond à partir de votre onglet, vous devez encapsuler l’URL du lien profond dans `microsoftTeams.executeDeeplink(url)` l’API. Le lien profond peut également être transmis via une `OpenURL` action dans la carte.

L’image suivante affiche une vue d’étape invoquée via un lien profond :

<img src="~/assets/images/tab-images/invoke-stage-view-through-deep-link.png" alt="Invoke a Stage View through a deep link" width="400"/>

### <a name="syntax"></a>Syntaxe

Voici la syntaxe du lien profond :  
 
https://teams.microsoft.com/l/stage/{appId}/0?context={« contentUrl »:"[contentUrl] »,"websiteUrl »:"[websiteUrl] »,"name »:"[name]"}

### <a name="examples"></a>Exemples

Lorsqu’un utilisateur entre une URL, elle est déployée dans une carte adaptative.

Voici les exemples de liens profonds pour appeler l’affichage de l’étape :

**Exemple 1**

https://teams.microsoft.com/l/stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={« contentUrl »:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx »,"websiteUrl »:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx »,"name »:"Contoso"}

**Exemple 2**

https://teams.microsoft.com/l/Meeting_Stage/2a527703-1f6f-4559-a332-d8a7d288cd88/0?context={« contentUrl »:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx »,"websiteUrl »:"https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FLokisSandbox%2FSitePages%2FSandbox-Page.aspx »,"name »:"Contoso"}

> [!NOTE]
> * Le `name` lien profond est facultatif. S’il n’est pas inclus, le nom de l’application le remplace.
> * Le lien profond peut également être transmis via une `OpenURL` action.
> * Actuellement, Teams clients mobiles ne la prise en charge de la fonctionnalité Vue d’étape. Lorsque les utilisateurs sélectionnent un lien profond vers une vue d’étape, ils sont conduits vers le navigateur web de leur appareil. Le navigateur web ouvre l’URL spécifiée dans le `websiteUrl` paramètre du lien profond.
> * Lorsque vous lancez une étape à partir d’un certain contexte, assurez-vous que votre application fonctionne dans ce contexte. Par exemple, si votre vue d’étape est lancée à partir d’une application personnelle, vous devez vous assurer que votre application a une étendue personnelle.

## <a name="tab-information-property"></a>Propriété d’informations sur l’onglet

| Nom de la propriété | Type | Nombre de caractères | Description |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | Cette propriété est un identificateur unique de l’entité affichée par l’onglet. Ce champ est obligatoire.|
| `name` | String
 | 128 | Cette propriété est le nom complet de l’onglet dans l’interface de canal. Ce champ est facultatif.|
| `contentUrl` | String
 | 2048 | Cette propriété est l’URL https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans Teams dessin. Ce champ est obligatoire.|
| `websiteUrl?` | String
 | 2048 | Cette propriété est l’URL https:// pointer vers, si un utilisateur choisit d’afficher dans un navigateur. Ce champ est obligatoire.|
| `removeUrl?` | String
 | 2048 | Cette propriété est l’URL https:// qui pointe vers l’interface utilisateur à afficher lorsque l’utilisateur supprime l’onglet. Il s’agit d’un champ facultatif.|

## <a name="see-also"></a>Voir aussi

* [Déploiement des liens des extensions de messagerie](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md)
