---
title: Résoudre les problèmes de votre application
description: Résoudre les problèmes ou les erreurs lors de la création d’applications pour Microsoft Teams
keywords: Résolution des problèmes de développement d’applications Teams
localization_priority: Normal
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: ea6a452d3e3ace7c78e29f6829ac124eea8219d6
ms.sourcegitcommit: 6f1bd36b1071e256bdc14e6ccb31dfdda9ca6d6b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/13/2022
ms.locfileid: "66048961"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Résoudre les problèmes de votre application Microsoft Teams

## <a name="troubleshooting-tabs"></a>Onglets de résolution des problèmes

### <a name="accessing-the-devtools"></a>Accès aux DevTools

Vous pouvez ouvrir [DevTools dans le client Teams](~/tabs/how-to/developer-tools.md) pour une expérience similaire à celle d’appuyer sur F12 (sur Windows) ou Command-Option-I (sur MacOS) dans un navigateur.

### <a name="blank-tab-screen"></a>Écran d’onglet vide

Si vous ne voyez pas votre contenu dans l’affichage onglet, il peut s’agir des éléments suivants :

* votre contenu ne peut pas être affiché dans un `<iframe>`.
* le domaine de contenu ne figure pas dans la liste [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le manifeste.

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>Le bouton Enregistrer n’est pas activé dans la boîte de dialogue Paramètres

Veillez à appeler `microsoftTeams.settings.setValidityState(true)` une fois que l’utilisateur a saisi ou sélectionné toutes les données requises dans votre page de paramètres pour activer le bouton Enregistrer.

### <a name="the-tab-settings-cant-be-saved-on-selecting-save"></a>Les paramètres de l’onglet ne peuvent pas être enregistrés lors de la sélection de l’option Enregistrer

Lorsque vous ajoutez un onglet, si vous **sélectionnez Enregistrer** mais recevez un message d’erreur indiquant que les paramètres ne peuvent pas être enregistrés, le problème peut être l’une des deux classes de problèmes :

* **Le message de réussite de l’enregistrement n’a jamais été reçu** : si un gestionnaire d’enregistrement a été inscrit à l’aide `microsoftTeams.settings.registerOnSaveHandler(handler)`, le rappel doit appeler `saveEvent.notifySuccess()`.

  * Si le rappel n’appelle `saveEvent.notifySuccess()` pas dans les 30 secondes ou appelle `saveEvent.notifyFailure(reason)` à la place, cette erreur s’affiche.
  * Si aucun gestionnaire d’enregistrement n’a été inscrit, l’appel `saveEvent.notifySuccess()` est effectué automatiquement lorsque l’utilisateur sélectionne **Enregistrer**.

* **Les paramètres fournis n’étaient pas valides** : l’autre raison pour laquelle les paramètres ne peuvent pas être enregistrés est si l’appel à `microsoftTeams.setSettings(settings)` fourni un objet de paramètres non valide ou si l’appel n’a pas été effectué du tout. Consultez la section suivante, Problèmes courants avec l’objet settings.

### <a name="common-problems-with-the-settings-object"></a>Problèmes courants avec l’objet settings

* `settings.entityId` est manquant. Ce champ est obligatoire.
* `settings.contentUrl` est manquant. Ce champ est obligatoire.
* `settings.contentUrl` ou facultatifs `settings.removeUrl`, ou `settings.websiteUrl` sont fournis mais non valides. Les URL doivent utiliser HTTPS et doivent également être le même domaine que la page des paramètres ou spécifiées dans la liste du `validDomains` manifeste.

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>Impossible d’authentifier l’utilisateur ou d’afficher votre fournisseur d’authentification dans votre onglet

Sauf si vous effectuez une authentification silencieuse, vous devez suivre le processus d’authentification fourni par le [SDK client JavaScript Microsoft Teams](/javascript/api/overview/msteams-client).

> [!NOTE]
> Nous exigeons que tout le flux d’authentification démarre et se termine sur votre domaine, qui doit être répertorié dans l’objet `validDomains` dans votre manifeste.

Pour plus d’informations sur l’authentification, consultez [Authentifier un utilisateur](~/concepts/authentication/authentication.md).

### <a name="static-tabs-not-showing-up"></a>Les onglets statiques ne s’affichent pas

Il existe un problème connu où la mise à jour d’une application de bot existante avec un onglet statique nouveau ou mis à jour n’affiche pas ce changement d’onglet lors de l’accès à l’application à partir d’une conversation personnelle.  Pour voir la modification, vous devez tester sur un nouvel utilisateur ou une nouvelle instance de test, ou accéder au bot à partir du menu volant Applications.

## <a name="troubleshooting-bots"></a>Dépannage des bots

### <a name="cant-add-my-bot"></a>Impossible d’ajouter mon bot

Les applications doivent être activées par l’administrateur de locataire Office 365 pour qu’elles soient chargées par les utilisateurs finaux. Dans certains cas, le locataire Office 365 peut avoir plusieurs références SKU associées, et pour que les bots fonctionnent dans n’importe quel, ils doivent être activés dans toutes les références SKU. Pour plus d’informations, consultez [Préparer votre locataire Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

### <a name="cant-add-bot-as-a-member-of-a-team"></a>Impossible d’ajouter un bot en tant que membre d’une équipe

Les bots doivent d’abord être chargés dans une équipe avant d’être accessibles dans n’importe quel canal de cette équipe. Pour plus d’informations sur ce processus, consultez [Chargement de votre application dans une équipe](~/concepts/deploy-and-publish/apps-upload.md).

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>Mon bot n’obtient pas mon message dans un canal

Les bots dans les canaux reçoivent des messages uniquement lorsqu’ils sont explicitement @mentioned, même si vous répondez à un message de bot précédent. La seule exception où vous ne voyez peut-être pas le nom du bot dans un message est si le bot reçoit une `imBack` action à la suite d’une CardAction qu’il a envoyée à l’origine.

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>Mon bot ne comprend pas mes commandes dans un canal

Étant donné que les bots dans les canaux reçoivent uniquement des messages lorsqu’ils sont @mentioned, tous les messages que votre bot reçoit dans un canal incluent ce @mention dans le champ de texte. Il est recommandé de supprimer le nom du bot lui-même de tous les messages texte entrants avant de passer à votre logique d’analyse. Passez en [revue les mentions](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) pour obtenir des conseils sur la façon de gérer ce cas.

## <a name="issues-with-packaging-and-uploading"></a>Problèmes liés à l’empaquetage et au chargement

### <a name="error-while-reading-manifestjson"></a>Erreur lors de la lecture de manifest.json

La plupart des erreurs de manifeste indiquent quel champ spécifique est manquant ou non valide. Toutefois, si le fichier JSON ne peut pas être lu en tant que JSON, ce message d’erreur générique est utilisé.

Raisons courantes des erreurs de lecture de manifeste :

* JSON non valide. Utilisez un IDE tel que [Visual Studio Code](https://code.visualstudio.com) ou [Visual Studio](https://www.visualstudio.com/vs/) qui valide automatiquement la syntaxe JSON.
* Problèmes d’encodage. Utilisez UTF-8 pour le fichier *manifest.json* . D’autres encodages, en particulier avec la mémoire bom, peuvent ne pas être lisibles.
* Package de .zip mal formé. Le fichier *manifest.json* doit se trouver au niveau supérieur du fichier .zip. Notez que la compression de fichier Mac par défaut peut placer *le fichier manifest.json* dans un sous-répertoire, qui ne se charge pas correctement dans Microsoft Teams.

### <a name="another-extension-with-same-id-exists"></a>Il existe une autre extension avec le même ID

Si vous tentez de charger à nouveau un package mis à jour avec le même ID, choisissez l’icône **Remplacer** à la fin de la ligne du tableau de l’onglet plutôt que le bouton **Télécharger**.

Si vous ne retentez pas un package mis à jour, vérifiez que l’ID est unique.
