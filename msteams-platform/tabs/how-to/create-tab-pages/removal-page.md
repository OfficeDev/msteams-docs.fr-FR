---
title: Créer une page de suppression d’onglets
author: laujan
description: Procédure de création d’une page de suppression d’onglets
keywords: onglets teams groupe canal configurable supprimer supprimer
ms.topic: conceptual
ms.author: ''
ms.openlocfilehash: 576a3bc88d8776a193b48868d37df204c3112fd8
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673542"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>Modifier ou supprimer un onglet de groupe de canaux

Vous pouvez étendre et améliorer l’expérience utilisateur en prenant en charge les options de suppression et de modification dans votre application. Teams permet aux utilisateurs de renommer ou de supprimer un onglet de canal/groupe et de permettre aux utilisateurs de reconfigurer votre onglet après l’installation. En outre, l’expérience de suppression de votre onglet peut inclure la désignation de ce qui se passe sur le contenu lorsque votre onglet est supprimé ou en fournissant aux utilisateurs des options de post-suppression telles que la suppression ou l’archivage du contenu.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Activer la reconfiguration de votre onglet après l’installation

Votre **fichier manifest. JSON** définit les fonctionnalités et fonctionnalités de votre onglet. La propriété d' `canUpdateConfiguration` instance d’onglet prend une valeur de type Boolean qui indique si un utilisateur peut modifier ou reconfigurer l’onglet après sa création :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. Default`true`|

Lorsque votre onglet est chargé dans un canal ou une conversation de groupe, teams ajoute un menu déroulant de clic droit pour votre onglet. Les options disponibles sont déterminées `canUpdateConfiguration` par le paramètre :

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Paramètres            |   √    |       |La `configurationUrl` page est rechargée dans un IFRAME, ce qui permet à l’utilisateur de reconfigurer l’onglet.  |
|     Renommer              |   √    |   √   | L’utilisateur peut modifier le nom de l’onglet tel qu’il apparaît dans la barre d’onglets.          |
|     Supprimer              |   √    |   √   |  Si la `removeURL` propriété et la valeur sont incluses dans la **page de configuration**, la page de **suppression** est chargée dans un IFRAME et présentée à l’utilisateur. Si une page de suppression n’est pas incluse, l’utilisateur voit s’afficher une boîte de dialogue de confirmation.          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>Créer une page de suppression d’onglets pour votre application

La page de suppression facultative est une page HTML que vous hébergez et qui s’affiche lorsque l’onglet est supprimé. L’URL de la page de suppression est `setSettings()` désignée par la méthode dans votre page de configuration. Comme avec toutes les pages de votre application, la page de suppression doit respecter les [exigences des onglets teams](~/tabs/how-to/add-tab.md).

### <a name="register-a-remove-handler"></a>Inscrire un gestionnaire de suppression

Éventuellement, dans la logique de votre page de suppression, vous pouvez `registerOnRemoveHandler((RemoveEvent) => {}` appeler le gestionnaire d’événements lorsque l’utilisateur supprime une configuration d’onglet existante. La méthode prend l' [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest) interface et exécute le code dans le gestionnaire lorsqu’un utilisateur tente de supprimer du contenu. Il est utilisé pour effectuer des opérations de nettoyage, telles que la suppression de la ressource sous-jacente qui alimente le contenu de l’onglet. Un seul gestionnaire de suppression peut être inscrit à la fois.

L' `RemoveEvent` interface décrit un objet avec deux méthodes :

* La `notifySuccess()` fonction est requise. Il indique que la suppression de la ressource sous-jacente a réussi et que son contenu peut être supprimé.

* La `notifyFailure(string)` fonction est facultative. Cela indique que la suppression de la ressource sous-jacente a échoué et que son contenu ne peut pas être supprimé. Le paramètre facultatif String spécifie la raison de l’échec. S’il est fourni, cette chaîne est affichée à l’utilisateur ; Sinon, une erreur générique s’affiche.

#### <a name="use-the-getsettings-function"></a>Utiliser la `getSettings()` fonction

Vous pouvez utiliser `getSettings()`pour désigner le contenu des onglets à supprimer. La `getSettings((Settings) =>{})` fonction prend le [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) et fournit les valeurs de propriété de paramètres valides qui peuvent être récupérées.

#### <a name="use-the-getcontext-function"></a>Utiliser la `getContext()` fonction

Vous pouvez utiliser `getContext()` pour extraire le contexte actuel dans lequel le cadre est en cours d’exécution. La `getContext((Context) =>{})` fonction prend en [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) et fournit des valeurs `Context` de propriété valides que vous pouvez utiliser dans la logique de votre page de suppression pour déterminer le contenu à afficher dans la page de suppression.

#### <a name="include-authentication"></a>Inclure l’authentification

Vous pouvez exiger l’authentification avant d’autoriser un utilisateur à supprimer le contenu de l’onglet. Les informations de contexte peuvent être utilisées pour vous aider à créer des demandes d’authentification et des URL de page d’autorisation. Consultez la rubrique [flux d’authentification Microsoft teams pour les onglets](~/tabs/how-to/authentication/auth-flow-tab.md). Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` `validDomains` tableau.

Vous trouverez ci-dessous un exemple de bloc de code de suppression d’onglet :

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

Lorsqu’un utilisateur sélectionne **supprimer** dans le menu déroulant de l’onglet, teams charge la page `removeUrl` facultative (désignée dans votre **page de configuration**) dans un IFRAME. Ici, l’utilisateur voit s’afficher un bouton chargé avec la `onClick()` fonction qui appelle `microsoftTeams.settings.setValidityState(true)` et active le bouton **supprimer** situé dans la partie inférieure du cadre de la page de suppression.

Après l’exécution du gestionnaire de suppression, `removeEvent.notifySuccess()` ou `removeEvent.notifyFailure()` avertir les équipes du résultat de la suppression de contenu.

>[!NOTE]
>Pour vous assurer que le contrôle d’un utilisateur autorisé sur un onglet n’est pas inhibé, teams supprime l’onglet dans les cas de réussite et d’échec. \
>Teams active le bouton **supprimer** au bout de 5 secondes, même si votre `setValidityState()`onglet n’a pas été appelé. \
>Lorsque l’utilisateur sélectionne **supprimer** teams supprime l’onglet après 30 secondes, que vos actions soient terminées ou non.
