---
title: Recommandations sur le processus de soumission d’approbation d’application Microsoft Teams
description: Décrit le processus d’approbation de soumission pour la publication de votre application dans le Magasin d’applications Microsoft Teams
keywords: teams publish store office publishing publish AppSource partner center account verification apps account not publish eligible
ms.openlocfilehash: 6268d408cc4c44633b9b3629c902044815639176
ms.sourcegitcommit: db19fee033b41152267bb524d67aee5b7f64b04a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797481"
---
# <a name="submit-your-app-to-appsource"></a>Soumettre votre application à AppSource

## <a name="teams-app-submission"></a>Soumission d’applications Teams

La publication de votre application [dans AppSource](https://appsource.microsoft.com) la rend disponible dans le catalogue d’applications Teams et sur le web. À un niveau élevé, le processus de soumission de votre application à AppSource est le suivant :

1. Développez votre application en suivant les instructions [de conception.](~/concepts/design/understand-use-cases.md) Les onglets doivent respecter les instructions de conception des onglets pour les ordinateurs de [bureau et web](~/tabs/design/tabs.md) et [mobiles.](~/tabs/design/tabs-mobile.md) Les bots doivent respecter les instructions [de conception du bot.](~/bots/design/bots.md)
1. Assurez-vous que votre application répond aux stratégies [de validation d’application](/legal/marketplace/certification-policies) pour Microsoft Teams. 
1. Testez vous-même votre application à l’aide [de l’outil de validation de manifeste.](prepare/submission-checklist.md#teams-app-validation-tool)
1. [Configurer un compte de développeur dans](/office/dev/store/open-a-developer-account) [l’Partner Center](https://support.microsoft.com/help/4499930/partner-center-overview). *Voir aussi* [Comment créer un compte Espace](#how-do-i-create-a-partner-center-account) partenaires dans la section FAQ ci-dessous.
1. Préparez votre application pour la soumission en suivant notre liste [de vérification de soumission.](prepare/submission-checklist.md)
1. Examinez les [cas de test les plus échoués pour obtenir une approbation plus rapide de la qualité de l’application.](prepare/frequently-failed-cases.md)
1. Envoyez votre package à [AppSource via l’Partner Center.](/office/dev/store/use-partner-center-to-submit-to-appsource)
1. Suivez le processus d’approbation sur votre tableau de bord de l’Centre partenaires. *Voir la* [vue d’ensemble de l’Centre partenaires.](https://support.microsoft.com/help/4499930/partner-center-overview)
1. Post-soumission : tenez compte de nos conseils [pour la maintenance et la prise en charge de votre application publiée.](post-publish/overview.md)

>[!NOTE]
>
>- Votre application Teams doit être [](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) mobile réactive et se conformer à aucune exigence de vente sur le système d’exploitation mobile (iOS et Android). 
>- Si votre application Teams contient un bot, vous devez vous conformer au [code](https://aka.ms/bf-conduct)de conduite de Bot Developer Framework.
>- Si votre application contient un connecteur Office 365, des conditions supplémentaires peuvent s’appliquer. *Voir Tableau* [de bord du développeur connecteurs](https://aka.ms/connectorsdashboard) et [Contrat du développeur d’applications.](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)
>- Pour rendre votre application disponible pour les utilisateurs GCC et éviter les listes d’applications en double dans le Store, le processus/flux d’th doit identifier et router l’utilisateur vers l’URL de contenu spécifiée/attendue pour les utilisateurs GCC.

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a>FAQ : processus de vérification des applications Teams et des comptes partenaires dans l’Centre partenaires

## <a name="how-do-i-create-a-partner-center-account"></a>Comment créer un compte Espace partenaires ?

Il existe deux façons de créer un compte Espace partenaires :

- Si vous débutez avec l’Espace partenaires et que vous n’avez pas de compte dans le réseau Microsoft, créez un compte à l’aide de la page d’inscription de [l’Espace partenaires.](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)
- Si vous êtes déjà inscrit au Réseau de partenaires, créez un compte directement dans l’Espace partenaires à l’aide [d’une inscription existante.](/office/dev/store/)

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a>Que se passe-t-il si je ne trouve pas mon compte Office Store dans l’Partner Center ?

Ouvrez un [ticket de support de l’Espace](https://partner.microsoft.com/support/v2/?stage=1) partenaires et sélectionnez les informations suivantes dans les menus listes :

| Menu | Option |
| -------   | -------  |
|Catégorie| Commercial Marketplace|
| Rubrique | Questions générales sur l’aide et les comments sur Marketplace |
| Subtopic| Complément Office |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>Où puis-je obtenir de l’aide pour les problèmes de compte de l’Partner Center ?

Visitez notre [page de support des éditeurs](https://aka.ms/marketplacepublishersupport) pour rechercher votre sujet de problème et trouver des conseils. Si les conseils fournis ne sont pas utiles, ouvrez un ticket de support de [l’Espace partenaires.](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>Comment gérer mon compte Office Store dans l’Partner Center ?

Consultez notre  [compte Gérer votre Office Store dans l’Partner Center](/office/dev/store/manage-account-settings-and-profile) pour obtenir des conseils sur la gestion de votre compte Office Store via l’Partner Center.

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>Comment ajouter mon numéro de téléphone à la section de contact de profil partenaire ?

Le numéro de téléphone est en trois parties : code pays, code de zone et numéro de téléphone. Si votre numéro de téléphone n’inclut pas de code de zone, laissez la deuxième zone vide et complétez la troisième zone.

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>Comment gérer les paramètres de mon compte et mon profil de partenaire dans l’Partner Center ?

Visitez notre page [Gérer les paramètres du compte](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) et les informations de profil pour obtenir des conseils sur la gestion de vos paramètres de compte De l’Partner Center.

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a>Pourquoi reçois-je le message « Ce compte n’est pas éligible pour la publication » lorsque j’essaie d’envoyer mon add-in par le biais de l’Partner Center ?

Vous recevrez le message d’erreur ci-dessus lorsque l’état [de vérification de](/partner-center/verification-responses) votre compte est en attente. Vous pouvez vérifier l’état de [](https://partner.microsoft.com/dashboard) vérification de votre compte dans le tableau de bord de l’Centre partenaires en sélectionnant l’option **Paramètres** (icône d’engrenage) dans le coin supérieur droit de l’en-tête de page et en choisissant paramètres du compte de compte des **paramètres** du  =>     =>  **développeur.**

![Page paramètres du compte de l’Partner Center](../../../assets/images/partner-center-accts-page.png)

![État de vérification de l’Partner Center](../../../assets/images/partner-center-verification-status.png)

Au cours du processus de vérification du compte, l’état de chaque étape requise (propriété de l’e-mail, vérification d’emploi et vérification de l’entreprise) s’affiche. Une fois le processus de vérification terminé, l’état de vérification de votre inscription sur la page de profil passe de « en attente » à « autorisé » et les étapes du processus ne sont plus affichées.

![Erreur de vérification de l’Partner Center](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-partner-center-account-verification-process-and-how-to-respond"></a>Qu’est-ce qui est vérifié dans le processus de vérification du compte de l’Partner Center et comment y répondre ?
Il existe trois domaines de vérification : propriété du courrier électronique, Emploi et Entreprise. Veuillez consulter les [](/partner-center/verification-responses#what-is-verified-and-how-to-respond) détails de ce qui est vérifié et comment répondre Si vous êtes le contact principal (administrateur global ou administrateur de compte), nous vous recommandons d’aller à votre profil de partenaire pour surveiller l’état de vérification et suivre l’avancement.

Une fois le processus de vérification terminé, l’état de  vérification  de votre inscription sur la page de profil passe d’en attente à autorisé et les étapes du processus avec l’état, affichées sur cette page, disparaissent. Le contact principal reçoit un courrier électronique de Microsoft dans les jours ou suivants après la fin de la vérification.

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-partner-center-how-should-i-proceed"></a>L’état de vérification de mon compte n’a pas été avancé au-delà de la propriété de l’e-mail dans l’Partner Center. Comment dois-je continuer ?

Pendant le processus **de vérification de la** propriété de l’e-mail, un message électronique de vérification est envoyé à l’adresse de messagerie du contact principal. Veuillez vérifier la boîte de réception de votre contact principal pour obtenir un e-mail de **maccount@<span>microsoft</span>.com** avec l’action de ligne d’objet requise : Vérifiez votre compte de messagerie auprès de *Microsoft,* en demandant que vous complétiez le processus de vérification du courrier électronique. L’e-mail de vérification est envoyé à l’adresse de messagerie répertoriée dans la page des paramètres de votre compte dans l’Partner Center.

> [!NOTE]
 >Le lien de vérification du courrier électronique n’est valide que pendant 7 jours. Vous pouvez demander que nous vous renvoyions l’e-mail en visitant la page de votre profil de partenaire et en sélectionnant le lien renvoyer l’e-mail de **vérification.** Pour vous assurer que le courrier électronique est reçu, microsoft.com listes sécurisées en tant que domaine sécurisé et vérifiez vos dossiers de courrier indésirable.

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a>Comment obtenir une assistance supplémentaire pour les problèmes liés à mon compte ?

Visitez notre [support pour le programme Commercial Marketplace](/azure/marketplace/partner-center-portal/support) dans la page Espace partenaires pour obtenir des instructions et des étapes pour créer un ticket de support.

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a>J’ai vérifié mes dossiers de courrier et je n’ai pas reçu l’e-mail de vérification. Que dois-je faire ensuite ?

Essayez ce qui suit :

1. Vérifiez votre dossier courrier indésirable.
1. Clear the browser cache, go to your Partner Center account dashboard, and select the **Resend verification email** link to have the verification email resent to your email address.
1. Essayez d’accéder au  **lien renvoyer le courrier** électronique de vérification à partir d’un autre navigateur.
1. Contactez votre service informatique pour vous assurer que les e-mails de vérification ne sont pas bloqués par le serveur de messagerie.
1. Ajustez le filtre de courrier indésirable de votre serveur pour autoriser/mettre en liste sécurisée tous les messages **maccount@microsoft. <span></span> com**.

## <a name="how-long-does-the-employment-verification-process-usually-take"></a>Combien de temps dure généralement le processus de vérification de l’emploi ?

Si tous les détails envoyés sont corrects, la vérification de l’emploi se termine dans 1 à 2 heures.

## <a name="how-long-does-the-business-verification-process-usually-take"></a>Combien de temps prend généralement le processus « Vérification d’entreprise » ?

La vérification d’entreprise prend entre 1 et 2 jours ou jours, à condition que tous les documents requis ont été envoyés.

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>Si j’arrive à l’équipe de support technique, mon ticket sera-t-il accéléré ?

Les tickets de support seront résolus dans un délai d’une semaine. Veuillez rechercher les mises à jour qui seront envoyées à l’e-mail fourni lorsque le ticket de support a été lancé.

## <a name="my-issue-is-not-listed-here--are-there-other-pages-i-can-reference-for-partner-center-issues"></a>Mon problème n’est pas répertorié ici.  Existe-t-il d’autres pages que je peux référencer pour les problèmes de l’Partner Center ?

Pour plus d’aide, [reportez-vous](/azure/marketplace/) à notre documentation commerciale marketplace.

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a>J’ai créé un ticket de support, cela fait 7 jours ou moins et je n’ai pas reçu de mise à jour. Où puis-je obtenir de l’aide supplémentaire ?

Envoyez un courrier électronique **<teamsubm@microsoft.com>** avec les détails suivants :

1. **Ligne d’objet**. *Problème de compte de l'<App_Name>* (spécifiez le nom de votre application).
1. **Corps de l’e-mail :**
    * Numéro de ticket de support :
    * Votre ID vendeur :
    * Capture d’écran du problème (si possible) :
    
## <a name="app-category-mapping"></a>Mappage des catégories d’application

| Catégorie Teams       | Catégories de PC  |
|:---------------------|:---------------|
| Analyse et bi | Analyse, visualisation des données et bi |
| Développeur et informatique | Outils de développement, administrateur informatique |
| Éducation | Éducation |
| Ressources humaines | Ressources humaines et recrutement |
| Productivité | Gestion de contenu, fichiers et documents, productivité, formation et didacticiels, et utilitaires |
| Gestion de projets | Communication, gestion de projet, flux de travail et gestion de l’entreprise |
| Ventes et support | Gestion des clients et des contacts, support client, gestion financière, ventes et marketing |
| Social et fun | Galeries d’images et de vidéos, style de vie, actualités et météo, réseau social, voyage et navigation |

>
> [!div class="nextstepaction"]
> [En savoir plus sur les stratégies de validation d’application pour Microsoft Teams](/legal/marketplace/certification-policies)
