---
title: Guide sur le processus d’approbation de l’application Microsoft teams
description: Décrit le processus d’approbation pour l’obtention de votre application publiée dans le magasin d’applications Microsoft teams
keywords: teams publier le magasin de publication Office AppSource
ms.openlocfilehash: 70f81f40ff424ab28e7129da7b947be0b1fcf469
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914545"
---
# <a name="submit-your-app-to-appsource"></a>Envoi de votre application à AppSource

## <a name="teams-app-submission"></a>Soumission d’applications teams

La publication de votre application dans [AppSource](https://appsource.microsoft.com) le rend disponible dans le catalogue d’applications de teams et sur le Web. À un niveau élevé, le processus d’envoi de votre application à AppSource est le suivant :

1. Développez votre application en suivant nos [instructions de conception](~/concepts/design/understand-use-cases.md). Les onglets doivent suivre [les instructions de conception d’onglet](~/tabs/design/tabs.md). Les robots doivent suivre les [instructions de conception de robot](~/bots/design/bots.md).
1. [Configurez un compte de développeur dans le](/office/dev/store/open-a-developer-account) [Centre de partenaires](https://support.microsoft.com/help/4499930/partner-center-overview).
1. Préparez votre application pour l’envoi en suivant notre [liste de vérification de soumission](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).
1. Consultez nos [conseils pour obtenir la soumission d’une application réussie](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md).
1. Envoyez votre package à [AppSource via le centre de partenaires](/office/dev/store/use-partner-center-to-submit-to-appsource).
1. Suivez le processus d’approbation de votre tableau de bord du centre partenaires. *Consultez la rubrique* [Présentation du centre partenaires](https://support.microsoft.com/help/4499930/partner-center-overview).
1. Post-soumission : consultez nos instructions pour [maintenir et prendre en charge votre application publiée](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).

>[!NOTE]
>
> * Si votre application teams contient un bot, vous devez vous conformer au [Code de conduite de](https://aka.ms/bf-conduct)l’infrastructure de développement de robots.
> * Si votre application contient un connecteur Office 365, des conditions supplémentaires peuvent s’appliquer. *Consultez* le [tableau de bord du développeur de connecteurs](https://aka.ms/connectorsdashboard) et des développeurs d' [applications](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm).

## <a name="faqs--teams-apps-and-partner-accounts"></a>FAQ — applications teams et comptes partenaires

## <a name="how-do-i-create-a-partner-center-account"></a>Comment puis-je créer un compte de centre partenaire ?

Il existe deux façons de créer un compte de centre partenaire :

* Si vous débutez avec le centre de partenaires et que vous n’avez pas de compte dans le réseau Microsoft, [créez un compte à l’aide de la page d’enregistrement du centre partenaires](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment).
* Si vous êtes déjà dans le réseau partenaire, [créez un compte directement dans le centre de partenaires à l’aide d’une inscriptions existante](/office/dev/store/).

## <a name="how-do-i-add-my-phone-number-to-the-contact-info-section"></a>Comment puis-je ajouter mon numéro de téléphone à la section informations sur le contact ?

Le numéro de téléphone comprend trois parties : indicatif du pays, indicatif régional et numéro de téléphone. Si aucune section n’est applicable, entrez le numéro `0`.

## <a name="why-do-i-get-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>Pourquoi est-ce que je reçois le message « ce compte n’est pas autorisé à publier » lorsque j’essaie d’envoyer mon complément via le centre de partenariat ?

Vous recevrez le message d’erreur ci-dessus lorsque l' [État de vérification](/partner-center/verification-responses) de votre compte est en attente. Vous pouvez vérifier l’état de la vérification de votre compte dans le [tableau de bord](https://partner.microsoft.com/dashboard) du centre partenaires en sélectionnant l’option **paramètres** (icône d’engrenage) dans le coin supérieur droit de l’environnement d’en-tête de page et en sélectionnant paramètres**du compte de** **compte**  => pour les **développeurs** => .

![Page Paramètres du compte du centre de partenaires](../../../assets/images/partner-center-accts-page.png)

![Statut de vérification du centre de partenaires](../../../assets/images/partner-center-verification-status.png)

Pendant le processus de vérification de compte, l’état de chaque étape requise (la propriété de l’e-mail, la vérification de l’emploi et la vérification de l’entreprise) s’affiche. Une fois le processus de vérification terminé, l’état de vérification de votre enregistrement sur la page de profil passe de « en attente » à « autorisé » et les étapes du processus ne s’affichent plus.

![Erreur de vérification du centre partenaire](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a>Comment puis-je obtenir une assistance supplémentaire pour les problèmes liés à mon compte ?

Visitez la [page aide et support partenaires](https://aka.ms/marketplacepublishersupport) et recherchez des solutions utiles pour obtenir une documentation relative à votre problème. Si les solutions ou les documents en libre-service fournis ne sont pas utiles pour résoudre votre problème, Veuillez classer un ticket de support en sélectionnant **fournir les détails du problème** dans la section **étape suivante** . Vous pouvez rechercher votre rubrique de problème dans la zone de recherche ou sélectionner **Parcourir les rubriques**, sous la zone de recherche, pour approfondir votre exploration.

> [!TIP]
> Si vous souhaitez obtenir de l’aide sur un problème de **vérification de compte** :
>
>1. Sous la **zone de recherche**, sélectionnez **Parcourir les rubriques**.
>1. Dans le menu déroulant **catégorie** , sélectionnez **tous les programmes** .
> 1. Sélectionnez **compte, intégration, accès** dans le menu déroulant **rubrique** .
>1. **Sélectionnez une option** dans le menu déroulant sous- **sujet** .
>1. Pour obtenir de l’aide. Sélectionnez **fournir les détails du problème** dans la section **étape suivante** .
>

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a>J’ai vérifié mes dossiers de courrier et je n’ai pas reçu le message électronique de vérification. Que dois-je faire maintenant ?

Procédez comme suit :

1. Vérifiez votre dossier de courrier indésirable.
1. Effacez le cache du navigateur, accédez à votre tableau de bord du compte centre partenaire, puis sélectionnez le lien **renvoyer le message électronique de vérification** pour renvoyer le message électronique de vérification à votre adresse de messagerie.
1. Essayez d’accéder au lien **renvoyer la messagerie de vérification** à partir d’un autre navigateur.
1. Collaborez avec votre service informatique pour vous assurer que les e-mails de vérification ne sont pas bloqués par le serveur de messagerie.
1. Réglez le filtre de courrier indésirable de votre serveur pour autoriser/autoriser tous les messages électroniques provenant d' **maccount@microsoft.<span> </span> com**.

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>Combien de temps dure le processus de vérification de l’emploi ?

Si tous les détails sont fournis correctement, la vérification de l’emploi se termine dans 1 à 2 heures.

## <a name="ive-already-reached-out-to-support-is-there-a-way-to-expedite-my-case"></a>J’ai déjà accédé à la prise en charge, est-il possible d’expédier mon dossier ?

Les tickets de support seront résolus au cours d’une semaine. Recherchez les mises à jour qui seront envoyées à l’e-mail fourni lorsque le ticket de support était généré.

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>J’ai créé un ticket d’assistance, il a été de 7 jours ouvrés et je n’ai pas reçu de mise à jour. Où puis-je obtenir de l’aide supplémentaire ?

Envoyez un courrier électronique **<teamsubm@microsoft.com>** avec les informations suivantes :

1. **Ligne d’objet**. *Problème de compte du centre partenaire pour <App_Name>* (spécifiez le nom de votre application).
2. **Corps du message :**
    * Numéro de ticket d’assistance :
    * Votre IDENTIFIant vendeur :
    * Une capture d’écran du problème.

> [!div class="nextstepaction"]
> [En savoir plus sur les stratégies de validation d’application pour Microsoft teams](https://docs.microsoft.com/legal/marketplace/certification-policies)
