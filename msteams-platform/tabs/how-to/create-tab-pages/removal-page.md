---
title: Créer une page de suppression d’onglets
author: laujan
description: Comment créer une page de suppression d’onglets
keywords: suppression des onglets teams du canal de groupe configurable
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 49e2df47095999e9f9eea76ea341a44215bfacb3
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797882"
---
# <a name="modify-or-remove-a-channel-group-tab"></a>Modifier ou supprimer un onglet de groupe de canaux

Vous pouvez étendre et améliorer l’expérience utilisateur en prendre en charge les options de suppression et de modification dans votre application. Teams permet aux utilisateurs de renommer ou de supprimer un onglet canal/groupe et vous pouvez permettre aux utilisateurs de reconfigurer votre onglet après l’installation. En outre, votre expérience de suppression d’onglets peut inclure la désignation de ce qu’il advient du contenu lorsque votre onglet est supprimé ou l’offre d’options post-suppression aux utilisateurs, telles que la suppression ou l’archivage du contenu.

## <a name="enable-your-tab-to-be-reconfigured-after-installation"></a>Activer la reconfiguration de votre onglet après l’installation

Votre **manifest.jsdéfinit** les fonctionnalités et fonctionnalités de votre onglet. La propriété d’instance d’onglet prend une valeur boolé générale qui indique si un utilisateur peut modifier ou reconfigurer l’onglet `canUpdateConfiguration` après sa création :

|Nom| Type| Taille maximale | Requis | Description|
|---|---|---|---|---|
|`canUpdateConfiguration`|Boolean|||Valeur indiquant si une instance de la configuration de l’onglet peut être mise à jour par l’utilisateur après sa création. Valeur par défaut : `true`|

Lorsque votre onglet est téléchargé vers un canal ou une conversation de groupe, Teams ajoute un menu déroulant de clic droit pour votre onglet. Les options disponibles sont déterminées par le `canUpdateConfiguration` paramètre :

| `canUpdateConfiguration`| true   | false | description |
| ----------------------- | :----: | ----- | ----------- |
|     Paramètres            |   √    |       |La page est rechargée dans un IFrame, ce qui permet à l’utilisateur de `configurationUrl` reconfigurer l’onglet.  |
|     Renommer              |   √    |   √   | L’utilisateur peut modifier le nom de l’onglet tel qu’il apparaît dans la barre d’onglets.          |
|     Supprimer              |   √    |   √   |  Si la propriété et la valeur sont incluses dans la page de configuration, la page de suppression est chargée dans un IFrame et présentée `removeURL` à l’utilisateur.   Si une page de suppression n’est pas incluse, une boîte de dialogue de confirmation s’est présentée à l’utilisateur.          |
|||||

## <a name="create-a-tab-removal-page-for-your-application"></a>Créer une page de suppression d’onglets pour votre application

La page de suppression facultative est une page HTML que vous hébergez et qui s’affiche lorsque l’onglet est supprimé. L’URL de la page de suppression est désignée par la `setSettings()` méthode dans votre page de configuration. Comme pour toutes les pages de votre application, la page de suppression doit respecter les exigences de [l’onglet Teams.](../../../tabs/how-to/tab-requirements.md)

### <a name="register-a-remove-handler"></a>Inscrire un remove handler

Si vous le souhaitez, dans votre logique de page de suppression, vous pouvez appeler le handler d’événements lorsque l’utilisateur supprime une `registerOnRemoveHandler((RemoveEvent) => {}` configuration d’onglet existante. La méthode prend l’interface et exécute le code dans le handler lorsqu’un utilisateur tente [`RemoveEvent`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.removeevent?view=msteams-client-js-latest&preserve-view=true) de supprimer du contenu. Il est utilisé pour effectuer des opérations de nettoyage telles que la suppression de la ressource sous-jacente qui alimentera le contenu de l’onglet. Un seul de ces derniers peut être inscrit à la fois.

`RemoveEvent`L’interface décrit un objet avec deux méthodes :

* La `notifySuccess()` fonction est obligatoire. Il indique que la suppression de la ressource sous-jacente a réussi et que son contenu peut être supprimé.

* La `notifyFailure(string)` fonction est facultative. Il indique que la suppression de la ressource sous-jacente a échoué et que son contenu ne peut pas être supprimé. Le paramètre de chaîne facultatif spécifie la raison de l’échec. Si elle est fournie, cette chaîne s’affiche pour l’utilisateur ; Sinon, une erreur générique s’affiche.

#### <a name="use-the-getsettings-function"></a>Utiliser la `getSettings()` fonction

Vous pouvez `getSettings()` l’utiliser pour désigner le contenu de l’onglet à supprimer. La fonction prend dans et fournit les valeurs de propriété `getSettings((Settings) =>{})` de [`Settings interface`](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true) paramètres valides qui peuvent être récupérées.

#### <a name="use-the-getcontext-function"></a>Utiliser la `getContext()` fonction

Vous pouvez `getContext()` l’utiliser pour récupérer le contexte actuel dans lequel l’image est en cours d’exécution. La fonction prend en compte les valeurs de propriété valides que vous pouvez utiliser dans votre logique de page de suppression pour déterminer le contenu à afficher `getContext((Context) =>{})` dans la page de [`Context interface`](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) `Context` suppression.

#### <a name="include-authentication"></a>Inclure l’authentification

Vous pouvez exiger une authentification avant d’autoriser un utilisateur à supprimer le contenu de l’onglet. Les informations de contexte peuvent être utilisées pour créer des demandes d’authentification et des URL de page d’autorisation. Voir [flux d’authentification Microsoft Teams pour les onglets.](~/tabs/how-to/authentication/auth-flow-tab.md) Assurez-vous que tous les domaines utilisés dans vos pages d’onglets sont répertoriés dans le `manifest.json` `validDomains` tableau.

Voici un exemple de bloc de code de suppression d’onglet :

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

Lorsqu’un utilisateur  sélectionne Supprimer du menu déroulant de l’onglet, Teams charge la page facultative (désignée dans votre page de `removeUrl` **configuration)** dans un IFrame. Ici, un bouton chargé avec la fonction qui appelle et active le bouton Supprimer se trouve en bas de l’IFrame de `onClick()` la page de `microsoftTeams.settings.setValidityState(true)` suppression. 

Après l’exécution du handler de suppression, ou `removeEvent.notifySuccess()` `removeEvent.notifyFailure()` avertit Teams du résultat de la suppression de contenu.

>[!NOTE]
>Pour vous assurer que le contrôle d’un utilisateur autorisé sur un onglet n’est pas inhibé, Teams supprime l’onglet dans les cas de réussite et d’échec.\
>Teams active le bouton **Supprimer** après 5 secondes, même si votre onglet n’a pas appelé `setValidityState()` .\
>Lorsque l’utilisateur sélectionne **Supprimer** Teams, l’onglet est supprimé après 30 secondes, que vos actions soient terminées ou non.
