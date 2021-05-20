---
title: Créer une page de suppression d’onglets
author: laujan
description: Comment créer une page de suppression d’onglets
keywords: équipes onglets canal de groupe configurable supprimer supprimer
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: e1a1f38a2bcb3b5bc4bc54f469c8727e44d8695e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566669"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>Modifier ou supprimer un onglet de groupe de canal

Vous pouvez étendre et améliorer l’expérience utilisateur en soutenant les options de suppression et de modification dans votre application. Teams permet aux utilisateurs de renommer ou de supprimer un onglet canal/groupe et vous pouvez permettre aux utilisateurs de reconfigurer votre onglet après l’installation. En outre, votre expérience de suppression d’onglet peut inclure la déstabilisation de ce qui arrive au contenu lorsque votre onglet est supprimé ou de donner aux utilisateurs des options post-suppression telles que la suppression ou l’archivage du contenu.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Activez la reconfiguration de votre onglet après l’installation

Votre **manifest.jsdéfinit** les fonctionnalités et les capacités de votre onglet. La propriété `canUpdateConfiguration` d’instance d’onglet prend une valeur Boolean qui indique si un utilisateur peut modifier ou reconfigurer l’onglet après sa création :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`canUpdateConfiguration`|Booléen|||Une valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après la création. faire défaut: `true`|

Lorsque votre onglet est téléchargé sur un canal ou un chat de groupe, Teams ajoutera un menu drop-down à clic droit pour votre onglet. Les options disponibles sont déterminées par le `canUpdateConfiguration` paramètre :

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Paramètres            |   √    |       |La `configurationUrl` page est rechargée dans un IFrame permettant à l’utilisateur de reconfigurer l’onglet.  |
|     Renommer              |   √    |   √   | L’utilisateur peut modifier le nom de l’onglet tel qu’il apparaît dans la barre d’onglet.          |
|     Supprimer              |   √    |   √   |  Si la  `removeURL` propriété et la valeur sont incluses dans la page de **configuration,** la **page de suppression** est chargée dans un IFrame et présentée à l’utilisateur. Si une page de suppression n’est pas incluse, l’utilisateur est présenté avec une boîte de dialogue de confirmation.          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>Créez une page de suppression d’onglets pour votre application

La page de suppression optionnelle est une page HTML que vous hébergez et s’affiche lorsque l’onglet est supprimé. L’URL de la page de suppression est désignée par `setSettings()` la méthode dans votre page de configuration. Comme pour toutes les pages de votre application, la page de suppression doit se conformer aux [exigences Teams’onglets](../../../tabs/how-to/tab-requirements.md).

### <a name="register-a-remove-handler"></a>Enregistrer un gestionnaire de suppression

En option, dans votre logique de page de suppression, vous pouvez invoquer `registerOnRemoveHandler((RemoveEvent) => {}` le gestionnaire d’événements lorsque l’utilisateur supprime une configuration d’onglet existante. La méthode prend dans [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) l’interface et exécute le code dans le gestionnaire quand un utilisateur tente de supprimer du contenu. Il est utilisé pour effectuer des opérations de nettoyage telles que la suppression de la ressource sous-jacente qui alimenter le contenu de l’onglet. Un seul gestionnaire de suppression peut être enregistré à la fois.

`RemoveEvent`L’interface décrit un objet avec deux méthodes :

* La `notifySuccess()` fonction est requise. Il indique que la suppression de la ressource sous-jacente a réussi et que son contenu peut être supprimé.

* La `notifyFailure(string)` fonction est facultative. Il indique que la suppression de la ressource sous-jacente a échoué et que son contenu ne peut pas être supprimé. Le paramètre de chaîne optionnel spécifie une raison de la défaillance. Si elle est fournie, cette chaîne s’affiche à l’utilisateur; sinon une erreur générique s’affiche.

#### <a name="use-the-getsettings-function"></a>Utiliser la `getSettings()` fonction

Vous pouvez utiliser `getSettings()` pour désigner le contenu de l’onglet à supprimer. La `getSettings((Settings) =>{})` fonction prend dans le et fournit les valeurs de propriété paramètres [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) valides qui peuvent être récupérés.

#### <a name="use-the-getcontext-function"></a>Utiliser la `getContext()` fonction

Vous pouvez utiliser pour `getContext()` récupérer le contexte actuel dans lequel le cadre est en cours d’exécution. La `getContext((Context) =>{})` fonction prend dans le et fournit des valeurs de propriété [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) `Context` valides que vous pouvez utiliser dans votre logique de page de suppression pour déterminer le contenu à afficher dans la page de suppression.

#### <a name="include-authentication"></a>Inclure l’authentification

Vous pourriez avoir besoin d’authentification avant de permettre à un utilisateur de supprimer le contenu de l’onglet. Les informations context contextiées peuvent être utilisées pour aider à construire des demandes d’authentification et des URL de page d’autorisation. Voir le [Microsoft Teams’authentification pour les onglets](~/tabs/how-to/authentication/auth-flow-tab.md). Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` `validDomains` tableau.

Voici un bloc de code de suppression d’onglets d’échantillon :

```html
<body>
  <button onclick="onClick()">Delete this tab and all underlying data?</button>
  <script>
    microsoftTeams.initialize();
    microsoftTeams.settings.registerOnRemoveHandler((removeEvent) => {
      // Here you can designate the tab content to be removed and/or archived.
        microsoftTeams.settings.getSettings((settings) => {
        settings.contentUrl = "..."
        });
        removeEvent.notifySuccess();
    });

    const onClick() => {
        microsoftTeams.settings.setValidityState(true);
    }
  </script>
</body>

```

Lorsqu’un utilisateur sélectionne **Supprimer du** menu de drop-down de l’onglet, Teams charge la page optionnelle (désignée dans votre page `removeUrl` de **configuration)** dans un IFrame. Ici, l’utilisateur est présenté avec un bouton chargé de la `onClick()` fonction qui appelle et permet le bouton `microsoftTeams.settings.setValidityState(true)` **Supprimer** situé près du bas de la page de suppression IFrame.

Après l’exécution du gestionnaire de suppression, `removeEvent.notifySuccess()` ou `removeEvent.notifyFailure()` avertit Teams résultat de suppression de contenu.

>[!NOTE]
> * Pour s’assurer que le contrôle d’un utilisateur autorisé sur un onglet n’est pas inhibé, Teams supprimera l’onglet dans les cas de succès et d’échec.\
> * Teams permet le **bouton Supprimer** après 5 secondes, même si votre onglet n’a pas appelé `setValidityState()` .\
> * Lorsque l’utilisateur sélectionne **Supprimer Teams** supprime l’onglet après 30 secondes, que vos actions aient été terminées ou non.
