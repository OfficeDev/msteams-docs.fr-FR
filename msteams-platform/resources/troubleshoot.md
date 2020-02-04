---
title: Résoudre les problèmes de votre application
description: Résoudre des problèmes ou des erreurs lors de la création d’applications pour Microsoft teams
keywords: résolution des problèmes de développement des applications teams
ms.date: 07/09/2018
ms.openlocfilehash: f7fe42e7c1f3ff2c4d8d1cbe81ed8f71e6c04384
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673560"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Résolution des problèmes liés à votre application Microsoft teams

## <a name="troubleshooting-tabs"></a>Onglets de dépannage

### <a name="accessing-the-devtools"></a>Accès au DevTools

Vous pouvez ouvrir [devtools dans le client teams](~/tabs/how-to/developer-tools.md) pour une expérience similaire en appuyant sur F12 (sous Windows) ou commande-option-I (sur MacOS) dans un navigateur.

### <a name="blank-tab-screen"></a>Onglet vide

Si vous ne voyez pas votre contenu dans l’affichage de l’onglet, il peut s’agir des éléments suivants :

* votre contenu ne peut pas être affiché `<iframe>`dans un.
* le domaine de contenu n’est pas dans la liste [validDomains](~/resources/schema/manifest-schema.md#validdomains) dans le manifeste.

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>Le bouton enregistrer n’est pas activé dans la boîte de dialogue Paramètres.

Veillez à appeler `microsoftTeams.settings.setValidityState(true)` une fois que l’utilisateur a entré ou sélectionné toutes les données requises sur la page des paramètres pour activer le bouton enregistrer.

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>Après avoir sélectionné le bouton enregistrer, les paramètres de tabulation ne peuvent pas être enregistrés.

Lors de l’ajout d’un onglet, si vous cliquez sur les boutons enregistrer mais que vous voyez s’afficher un message d’erreur indiquant que les paramètres ne peuvent pas être enregistrés, le problème peut être l’une des deux catégories de problèmes :

* Le message de réussite de l’enregistrement n’a jamais été reçu. Si un gestionnaire d’enregistrement a été `microsoftTeams.settings.registerOnSaveHandler(handler)`inscrit à l’aide de `saveEvent.notifySuccess()`, le rappel doit appeler. Si le rappel ne l’appelle pas dans un délai de `saveEvent.notifyFailure(reason)` 30 secondes ou appelle à la place, cette erreur est affichée.

* Si aucun gestionnaire d’enregistrement n’a été `saveEvent.notifySuccess()` enregistré, l’appel est automatiquement effectué dès que l’utilisateur sélectionne le bouton enregistrer.

* Les paramètres fournis n’étaient pas valides. L’autre raison pour laquelle les paramètres ne sont pas enregistrés est le fait `microsoftTeams.setSettings(settings)` que l’appel à fourni un objet de paramètres non valide ou l’appel n’a pas été effectué. Consultez la section suivante, problèmes courants liés à l’objet Settings.

### <a name="common-problems-with-the-settings-object"></a>Problèmes courants avec l’objet Settings

* `settings.entityId`est manquant. Ce champ est obligatoire.
* `settings.contentUrl`est manquant. Ce champ est obligatoire.
* `settings.contentUrl`ou facultatif `settings.removeUrl`, ou `settings.websiteUrl` sont fournis mais ne sont pas valides. Les URL doivent utiliser le protocole HTTPs et doivent également être le même domaine que la page de paramètres ou spécifié dans la `validDomains` liste du manifeste.

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>Impossible d’authentifier l’utilisateur ou d’afficher votre fournisseur d’authentification dans votre onglet

Sauf si vous effectuez une authentification sans assistance, vous devez suivre le processus d’authentification fourni par le [Kit de développement logiciel (SDK) JavaScript client Microsoft teams](/javascript/api/overview/msteams-client.md).

> [!NOTE]
>Tout le flux d’authentification doit être démarré et se terminer sur votre domaine, qui doit être mentionné `validDomains` dans l’objet de votre manifeste.

Pour plus d’informations sur l’authentification, consultez [la rubrique authentifier un utilisateur](~/concepts/authentication/authentication.md).

### <a name="static-tabs-not-showing-up"></a>Les onglets statiques ne sont pas affichés

Il existe un problème connu où la mise à jour d’une application de robot existante avec un onglet statique nouveau ou mis à jour n’affiche pas cette modification d’onglet lors de l’accès à l’application à partir d’une conversation de conversation personnelle.  Pour voir la modification, vous devez tester sur une nouvelle instance d’utilisateur ou de test, ou accéder au bot à partir du lanceur d’applications.

## <a name="troubleshooting-bots"></a>Dépannage des robots

### <a name="cant-add-my-bot"></a>Impossible d’ajouter mon bot

Les applications doivent être activées par l’administrateur client Office 365 pour être chargées par les utilisateurs finaux. Notez que, dans certains cas, le client Office 365 peut avoir plusieurs UGS associées et que les robots doivent être activés dans toutes les UGS. Pour plus d’informations, reportez-vous à [la rubrique prepare Your Office 365 client](~/concepts/build-and-test/prepare-your-o365-tenant.md) .

### <a name="cant-add-bot-as-a-member-of-a-team"></a>Impossible d’ajouter un bot en tant que membre d’une équipe

Les robots doivent d’abord être téléchargés dans une équipe pour être accessibles dans n’importe quel canal de cette équipe. Pour plus d’informations sur ce processus, consultez [la partie chargement de votre application dans une équipe](~/concepts/deploy-and-publish/apps-upload.md) .

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>Mon bot n’obtient pas mon message dans un canal

Les robots des canaux reçoivent des messages uniquement lorsqu’ils sont explicitement @mentioneds, même si vous répondez à un message de robot précédent. La seule exception où le nom du bot peut ne pas s’afficher dans un message est si le bot `imBack` reçoit une action à la suite d’un CardAction qu’il a envoyé à l’origine.

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>Mon bot ne comprends pas mes commandes dans un canal

Étant donné que les robots des canaux reçoivent uniquement les messages lorsqu’ils sont @mentioned, tous les messages que votre bot reçoit dans un canal incluent ce @mention dans le champ de texte. Il est recommandé de supprimer le nom du robot lui-même de tous les messages texte entrants avant de passer à votre logique d’analyse. Consultez les [mentions](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions) pour obtenir des conseils sur la façon de gérer ce cas.

## <a name="issues-with-packaging-and-uploading"></a>Problèmes liés à l’empaquetage et au chargement

### <a name="error-while-reading-manifestjson"></a>Erreur lors de la lecture de manifest. JSON

La plupart des erreurs de manifeste indiquent quel champ spécifique est manquant ou non valide. Toutefois, si le fichier JSON ne peut pas être lu en tant que JSON, ce message d’erreur générique est utilisé.

Causes courantes des erreurs de lecture de manifeste :

* JSON non valide. Utilisez une interface IDE telle que [Visual Studio code](https://code.visualstudio.com) ou [Visual Studio](https://www.visualstudio.com/vs/) qui valide automatiquement la syntaxe JSON.
* Problèmes d’encodage. Utilisez UTF-8 pour le fichier *Manifest. JSON* . Les autres codages, en particulier avec la nomenclature, peuvent ne pas être lisibles.
* Package. zip malformé. Le fichier *Manifest. JSON* doit se trouver au niveau supérieur du fichier. zip. Notez que la compression de fichiers Mac par défaut peut placer le fichier *Manifest. JSON* dans un sous-répertoire, qui ne se charge pas correctement dans Microsoft Teams.

### <a name="another-extension-with-same-id-exists"></a>Une autre extension portant le même ID existe

Si vous essayez de télécharger à nouveau un package mis à jour avec le même ID, cliquez sur l’icône **remplacer** à la fin de la ligne de tableau de l’onglet plutôt que sur le bouton de **Téléchargement** .

Si vous ne rechargez pas un package mis à jour, vérifiez que l’ID est unique.
