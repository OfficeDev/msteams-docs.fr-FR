---
title: Résoudre les problèmes de votre application
description: Résoudre les problèmes ou les erreurs lors de la création d'applications pour Microsoft Teams
keywords: résolution des problèmes de développement d'applications teams
ms.topic: troubleshooting
ms.date: 07/09/2018
ms.openlocfilehash: a870a19eac9295f841b44b3b0364c46ffbc2d1d5
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696506"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a>Résoudre les problèmes de votre application Microsoft Teams

## <a name="troubleshooting-tabs"></a>Onglets de dépannage

### <a name="accessing-the-devtools"></a>Accès aux DevTools

Vous pouvez ouvrir [DevTools](~/tabs/how-to/developer-tools.md) dans le client Teams pour une expérience similaire à celle d'appuyer sur F12 (sur Windows) ou Command-Option-I (sur MacOS) dans un navigateur.

### <a name="blank-tab-screen"></a>Écran d'onglet vide

Si vous ne voyez pas votre contenu dans l'affichage Onglet, il peut s'agit des suivants :

* votre contenu ne peut pas être affiché dans un `<iframe>` .
* le domaine de contenu ne figure pas dans la [liste validDomains](~/resources/schema/manifest-schema.md#validdomains) du manifeste.

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a>Le bouton Enregistrer n'est pas activé dans la boîte de dialogue Paramètres

Assurez-vous d'appeler une fois que l'utilisateur a reçu une entrée ou sélectionné toutes les données requises sur votre page de paramètres pour `microsoftTeams.settings.setValidityState(true)` activer le bouton Enregistrer.

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a>Après avoir sélectionné le bouton Enregistrer, les paramètres de l'onglet ne peuvent pas être enregistrés.

Lorsque vous ajoutez un onglet, si vous cliquez sur les boutons d'enregistrer mais qu'un message d'erreur indiquant que les paramètres ne peuvent pas être enregistrés s'affiche, le problème peut être l'une des deux catégories de problèmes suivants :

* Le message de réussite de l'enregistrer n'a jamais été reçu. Si un handler d'enregistrement a été enregistré à `microsoftTeams.settings.registerOnSaveHandler(handler)` l'aide de , le rappel doit appeler `saveEvent.notifySuccess()` . Si le rappel ne l'appelle pas dans les 30 secondes ou s'il appelle à la place, cette `saveEvent.notifyFailure(reason)` erreur s'affiche.

* Si aucun handler d'enregistrement n'a été enregistré, l'appel est effectué automatiquement dès que l'utilisateur sélectionne `saveEvent.notifySuccess()` le bouton Enregistrer.

* Les paramètres fournis n'étaient pas valides. L'autre raison pour laquelle les paramètres peuvent ne pas être enregistrés est si l'appel pour fournir un objet paramètres non valide ou `microsoftTeams.setSettings(settings)` l'appel n'a pas été effectué du tout. Consultez la section suivante, Problèmes courants avec l'objet paramètres.

### <a name="common-problems-with-the-settings-object"></a>Problèmes courants avec l'objet settings

* `settings.entityId` est manquant. Ce champ est obligatoire.
* `settings.contentUrl` est manquant. Ce champ est obligatoire.
* `settings.contentUrl` ou `settings.removeUrl` facultatifs, ou `settings.websiteUrl` sont fournis mais non valides. Les URL doivent utiliser HTTPS et doivent également être le même domaine que la page de paramètres ou spécifiés dans la liste du `validDomains` manifeste.

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a>Ne peut pas authentifier l'utilisateur ou afficher votre fournisseur d'authentification dans votre onglet

Sauf si vous faites une authentification silencieuse, vous devez suivre le processus d'authentification fourni par le [SDK client JavaScript Microsoft Teams.](/javascript/api/overview/msteams-client.md)

> [!NOTE]
>Nous exigeons que tout le flux d'authentification démarre et se termine sur votre domaine, qui doit être répertorié dans `validDomains` l'objet dans votre manifeste.

Pour plus d'informations sur l'authentification, voir [Authentifier un utilisateur.](~/concepts/authentication/authentication.md)

### <a name="static-tabs-not-showing-up"></a>Onglets statiques non s'affichant

Il existe un problème connu où la mise à jour d'une application de bot existante avec un onglet statique nouveau ou mis à jour n'affichera pas ce changement d'onglet lors de l'accès à l'application à partir d'une conversation personnelle.  Pour voir la modification, vous devez tester sur un nouvel utilisateur ou une nouvelle instance de test, ou accéder au bot à partir du flyout Applications.

## <a name="troubleshooting-bots"></a>Résolution des problèmes de bots

### <a name="cant-add-my-bot"></a>Can't add my bot

Les applications doivent être activées par l'administrateur client Office 365 pour qu'elles soient chargées par les utilisateurs finaux. Notez que dans certains cas, le client Office 365 peut être associé à plusieurs S SKUs, et pour que les bots fonctionnent dans n'importe quelle, ils doivent être activés dans toutes les S SKUs. Pour plus d'informations, voir Préparer votre [client Office 365.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

### <a name="cant-add-bot-as-a-member-of-a-team"></a>Can't add bot as a member of a team

Les bots doivent d'abord être chargés dans une équipe avant d'être accessibles dans n'importe quel canal de cette équipe. Pour plus d'informations sur ce [processus, consultez](~/concepts/deploy-and-publish/apps-upload.md) le téléchargement de votre application dans une équipe.

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a>Mon bot ne reçoit pas mon message dans un canal

Les bots dans les canaux reçoivent des messages uniquement lorsqu'ils sont explicitement @mentioned, même si vous répondez à un message de bot précédent. La seule exception lorsque vous ne voyez pas le nom du bot dans un message est si le bot reçoit une action à la suite d'un CardAction qu'il a `imBack` envoyé à l'origine.

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a>Mon bot ne comprend pas mes commandes dans un canal

Étant donné que les bots dans les canaux reçoivent des messages uniquement lorsqu'ils sont @mentioned, tous les messages que votre bot reçoit dans un canal incluent ce @mention dans le champ de texte. Il est préférable d'inger le nom du bot lui-même de tous les messages texte entrants avant de passer à votre logique d'examen. Examinez [les mentions](../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) pour obtenir des conseils sur la façon de gérer ce cas.

## <a name="issues-with-packaging-and-uploading"></a>Problèmes d'empaquetage et de chargement

### <a name="error-while-reading-manifestjson"></a>Erreur lors de la lecture manifest.jssur

La plupart des erreurs de manifeste fournissent un conseil sur le champ spécifique manquant ou non valide. Toutefois, si le fichier JSON ne peut pas du tout être lu en tant que JSON, ce message d'erreur générique est utilisé.

Raisons courantes des erreurs de lecture de manifeste :

* JSON non valide. Utilisez un IDE tel que [Visual Studio Code ou](https://code.visualstudio.com) [Visual Studio](https://www.visualstudio.com/vs/) qui valide automatiquement la syntaxe JSON.
* Problèmes de codage. Utilisez UTF-8 pour le *fichiermanifest.jssur.* D'autres encodages, en particulier avec la boM, peuvent ne pas être lisibles.
* Package .zip malformé. Le *manifest.jssur* le fichier doit se trouver au niveau supérieur du fichier .zip. Notez que la compression de fichiers Mac par défaut peut placer le *manifest.js* dans un sous-dossier, qui ne sera pas chargé correctement dans Microsoft Teams.

### <a name="another-extension-with-same-id-exists"></a>Il existe une autre extension avec le même ID

Si vous tentez de re-télécharger un package mis à jour  avec le même ID, choisissez l'icône Remplacer à la fin de la ligne de tableau de l'onglet plutôt que le bouton **Télécharger.**

Si vous ne retentez pas un package mis à jour, assurez-vous que l'ID est unique.
