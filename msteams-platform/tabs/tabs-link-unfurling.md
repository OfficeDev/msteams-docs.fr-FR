---
title: Déploiement du lien des onglets et vue des étapes
author: Rajeshwari-v
description: Découvrez comment déployer un lien, ouvrir la vue d’étape et épingler un onglet avec Microsoft Teams’application. Découvrez l’affichage de la scène et son appel à l’aide d’une carte adaptative à l’aide d’exemples et d’exemples de code.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: none
ms.openlocfilehash: 3119e444c8dd2b654f26b2fad5638f7c831619ac
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518253"
---
# <a name="tabs-link-unfurling-and-stage-view"></a>Déploiement du lien des onglets et vue des étapes

Stage View est un nouveau composant d’interface utilisateur qui vous permet d’afficher le contenu ouvert en plein écran en Teams et épinglé sous forme d’onglet.
 
## <a name="stage-view"></a>Vue d’étape

L’affichage d’étape est un composant d’interface utilisateur en plein écran que vous pouvez appeler pour faire surface à votre contenu web. Le service de déploiement de lien existant est mis à jour de sorte qu’il soit utilisé pour transformer les URL en onglet à l’aide d’une carte adaptative et des services de conversation. Lorsqu’un utilisateur envoie une URL dans une conversation ou un canal, l’URL est déployée vers une carte adaptative. L’utilisateur peut sélectionner **Afficher** dans la carte et épingler le contenu en tant qu’onglet directement à partir de l’affichage de l’étape.

## <a name="advantage-of-stage-view"></a>Avantage de l’affichage de l’étape

L’affichage de l’étape permet d’offrir une expérience plus transparente de l’affichage du contenu Teams. Les utilisateurs peuvent ouvrir et afficher le contenu fourni par votre application sans quitter le contexte, et ils peuvent épingler le contenu à la conversation ou au canal pour un accès rapide futur, ce qui a pour effet d’augmenter l’implication des utilisateurs avec votre application.

## <a name="stage-view-vs-task-module"></a>Affichage de l’étape et module de tâche

|Vue d’étape|Module de tâche|
|:-----------|:-----------|
|L’affichage d’étape est utile lorsque vous avez du contenu enrichi à afficher aux utilisateurs, comme une page, un tableau de bord, un fichier, etc. Il fournit des fonctionnalités enrichies qui permettent d’restituer votre contenu dans le canevas plein écran.|[Le module de](../task-modules-and-cards/task-modules/task-modules-tabs.md) tâche est particulièrement utile pour afficher les messages qui nécessitent l’attention de l’utilisateur ou collecter les informations requises pour passer à l’étape suivante.|
  
## <a name="invoke-stage-view"></a>Appeler l’affichage de l’étape

Vous pouvez appeler l’affichage de l’étape des manières suivantes :

* [Appeler l’affichage de l’étape à partir d’une carte adaptative](#invoke-stage-view-from-adaptive-card)
* [Appeler l’affichage de l’étape par le biais d’un lien profond](#invoke-stage-view-through-deep-link)

## <a name="invoke-stage-view-from-adaptive-card"></a>Appeler l’affichage de l’étape à partir d’une carte adaptative

Lorsque l’utilisateur entre une URL sur le client de bureau Teams, le bot est appelé et renvoie une carte adaptative avec la possibilité d’ouvrir l’URL dans une étape.[](../task-modules-and-cards/cards/cards-actions.md) Une fois qu’une étape est lancée `tabInfo` et que l’étape est fournie, vous pouvez ajouter la possibilité d’épingler l’étape sous la mesure d’un onglet.  

Les images suivantes affichent une étape ouverte à partir d’une carte adaptative :

[![Ouvrir une étape à partir de la carte adaptative](~/assets/images/tab-images/open-stage-from-adaptive-card1.png)](~/assets/images/tab-images/open-stage-from-adaptive-card1.png#lightbox)

[![Ouvrir une étape](~/assets/images/tab-images/open-stage-from-adaptive-card2.png)](~/assets/images/tab-images/open-stage-from-adaptive-card2.png#lightbox) 

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

Le `invoke` type de requête doit être `composeExtension/queryLink`.

> [!NOTE]
> * `invoke` est similaire au flux de travail `appLinking` actuel. 
> * Pour conserver la cohérence, il est recommandé de nommer `Action.Submit` comme `View`.
> * `websiteUrl` est une propriété obligatoire à passer dans l’objet `TabInfo` .

Voici le processus d’appel de l’affichage de l’étape :

* Lorsque l’utilisateur sélectionne **Affichage**, le bot reçoit une `invoke` demande. Le type de requête est `composeExtension/queryLink`.
* `invoke` La réponse du bot contient une carte adaptative avec son type `tab/tabInfoAction` .
* Le bot répond par un `200` code.

> [!NOTE]
> Sur Teams clients mobiles, l’utilisation de l’affichage de phase pour les applications distribuées via le magasin [Teams](/platform/concepts/deploy-and-publish/apps-publish-overview.md) sans expérience optimisée pour moblie ouvre le navigateur web par défaut de l’appareil. Le navigateur ouvre l’URL spécifiée dans le paramètre `websiteUrl` de l’objet `TabInfo` .

## <a name="invoke-stage-view-through-deep-link"></a>Appeler l’affichage de l’étape par le biais d’un lien profond

Pour appeler l’affichage de l’étape via un lien profond à partir de votre onglet, vous devez encapsuler l’URL du lien profond dans l’API `microsoftTeams.executeDeeplink(url)` . Le lien profond peut également être transmis via une `OpenURL` action dans la carte.

### <a name="syntax"></a>Syntaxe

Voici la syntaxe du lien profond : 

https://teams.microsoft.com/l/stage/{appId}/0?context={« contentUrl »:"contentUrl »,"websiteUrl »:"websiteUrl »,"name »:"Contoso"}
 
### <a name="examples"></a>Exemples

Lorsqu’un utilisateur entre une URL, elle est déployée dans une carte adaptative.

Voici les exemples de liens profonds pour appeler l’affichage de l’étape :

**Exemple 1 : URL avec threadId**

URL non codée :
 
https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context={« contentUrl »:" »https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191,"websiteUrl »:""https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true"title »:"Quotes:Miscellaneous »,"threadId »:"19:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.contrôle2"}

URL codée :

https://teams.microsoft.com/l/stage/be411542-2bd5-46fb-8deb-a3d5f85156f6/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%2C%22threadId%22%3A%2219:9UryYW9rjwnq-vwmBcexGjN1zQSNX0Y4oEAgtUC7WI81@thread.tacv2%22%7D


**Exemple 2 : URL sans threadId**

URL non codée :

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context={« contentUrl »:"https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191 »,"websiteUrl »:" »https://teams-alb.wakelet.com/teams/collection/e4173826-5dae-4de0-b77d-bfabafd6f191?standalone=true,"title »:"Quotes:Miscellaneous"}

Codé

https://teams.microsoft.com/l/stage/43f56af0-8615-49e6-9635-7bea3b5802c2/0?context=%7B%22contentUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%22%2C%22websiteUrl%22%3A%22https%3A%2F%2Fteams-alb.wakelet.com%2Fteams%2Fcollection%2Fe4173826-5dae-4de0-b77d-bfabafd6f191%3Fstandalone%3Dtrue%22%2C%22title%22%3A%22Quotes%3A%20Miscellaneous%22%7D


> [!NOTE]
> Tous les liens profonds doivent être encodés avant de pouvoir l’encoder. Nous ne  prise en charge pas les URL non codées.
> * Le `name` lien profond est facultatif. S’il n’est pas inclus, le nom de l’application le remplace.
> * Le lien profond peut également être transmis via une `OpenURL` action.
> * Lorsque vous lancez une étape à partir d’un certain contexte, assurez-vous que votre application fonctionne dans ce contexte. Par exemple, si votre vue d’étape est lancée à partir d’une application personnelle, vous devez vous assurer que votre application a une étendue personnelle.

## <a name="tab-information-property"></a>Propriété d’informations sur l’onglet

| Nom de la propriété | Type | Nombre de caractères | Description |
|:-----------|:---------|:------------|:-----------------------|
| `entityId` | String | 64 | Cette propriété est un identificateur unique de l’entité affichée par l’onglet. Ce champ est obligatoire.|
| `name` | String | 128 | Cette propriété est le nom complet de l’onglet dans l’interface de canal. Ce champ est facultatif.|
| `contentUrl` | String | 2048 | Cette propriété est l’URL https:// qui pointe vers l’interface utilisateur de l’entité à afficher dans Teams dessin. Ce champ est obligatoire.|
| `websiteUrl?` | Chaîne | 2048 | Cette propriété est l’URL https:// pointer vers, si un utilisateur choisit d’afficher dans un navigateur. Ce champ est obligatoire.|
| `removeUrl?` | String | 2048 | Cette propriété est l’URL https:// qui pointe vers l’interface utilisateur à afficher lorsque l’utilisateur supprime l’onglet. Il s’agit d’un champ facultatif.|

## <a name="code-sample"></a>Exemple de code

| Exemple de nom | Description | C# |Node.js|
|-------------|-------------|------|----|
|Onglet en vue de l’étape |Microsoft Teams exemple d’application d’onglet pour montrer l’onglet en vue de la phase.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-stage-view/nodejs)|
    

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer des onglets de conversation](~/tabs/how-to/conversational-tabs.md)

## <a name="see-also"></a>Voir aussi

* [Déploiement des liens des extensions de messagerie](~/messaging-extensions/how-to/link-unfurling.md)
* [Teams onglets](~/tabs/what-are-tabs.md)
* [Créer un onglet personnel](~/tabs/how-to/create-personal-tab.md)
* [Créer un onglet de canal ou de groupe](~/tabs/how-to/create-channel-group-tab.md)
