---
title: Soumettre votre application à l’Partner Center
description: Découvrez comment créer un compte Espace partenaires et soumettre votre application pour validation dans le Store.
author: heath-hamilton
ms.author: lajanuar
ms.topic: how-to
ms.openlocfilehash: 732e283bffc253743e890b0c45dc7b0689108716
ms.sourcegitcommit: d9274ac2f32880e861b206ac6ce29467d631177f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/04/2021
ms.locfileid: "52760888"
---
# <a name="submit-your-microsoft-teams-app-to-partner-center"></a>Soumettre votre application Microsoft Teams à l’Partner Center

Après avoir préparé votre soumission au Store, vous pouvez officiellement soumettre votre application pour révision.

## <a name="create-a-partner-center-account"></a>Créer un compte d’Espace partenaires

Pour publier votre application sur le Teams store et AppSource, vous devez d’abord [configurer un compte de développeur.](https://docs.microsoft.com/office/dev/store/open-a-developer-account)

## <a name="submit-your-app"></a>Envoyer votre application

Pour soumettre votre application, suivez ces [instructions pas à](https://docs.microsoft.com/office/dev/store/add-in-submission-guide)pas de soumission dans le Store. Lors de la création d’une soumission, spécifiez que vous soumettez une Teams application.

### <a name="app-category-mapping"></a>Mappage des catégories d’application

Lors de la soumission, vous êtes invité à catégoriser votre application. Le tableau suivant ma Teams catégories de magasin aux catégories répertoriées dans l’Partner Center.

| Teams catégories       | Catégories de l’Centre partenaires  |
|:---------------------|:---------------|
| Analyse et bi | Analyse, visualisation des données et bi |
| Développeur et informatique | Outils de développement, administrateur informatique |
| Éducation | Éducation |
| Ressources humaines | Ressources humaines et recrutement |
| Productivité | Gestion de contenu, fichiers et documents, productivité, formation et didacticiels, et utilitaires |
| Gestion de projet | Communication, gestion Project, flux de travail et gestion de l’entreprise |
| Ventes et support | Gestion des clients et des contacts, support client, gestion financière, ventes et marketing |
| Social et fun | Galeries d’images et de vidéos, style de vie, actualités et météo, réseau social, voyage et navigation |

### <a name="3-fix-issues-with-your-submission"></a>3. Résoudre les problèmes de votre soumission

Si la soumission de votre application échoue, vous recevez un rapport d’échec pour savoir ce qu’il faut corriger et soumettre à nouveau. Microsoft fournit également un service de gant blanc pour vous aider à obtenir votre application répertoriée.

## <a name="faqs"></a>Foire aux questions

### <a name="how-do-i-create-a-partner-center-account"></a>Comment créer un compte Espace partenaires ?

Vous pouvez créer un compte Espace partenaires de l’une des manières suivantes :

- Si vous débutez avec l’Espace partenaires et que vous n’avez pas de compte dans le réseau Microsoft, créez un compte à l’aide de la page d’inscription de [l’Espace partenaires.](/office/dev/store/open-a-developer-account#create-an-account-using-the-partner-center-enrollment-page)
- Si vous êtes déjà inscrit au Réseau de partenaires, créez un compte directement dans l’Espace partenaires à l’aide d’une [page d’inscription existante.](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)

### <a name="what-if-i-cant-find-my-office-store-account-in-partner-center"></a>Que se passe-t-il si je ne trouve pas mon compte Office Store dans l’Partner Center ?

Ouvrez un [ticket de support de l’Espace](https://partner.microsoft.com/support/v2/?stage=1) partenaires et sélectionnez ce qui suit dans les menus listes :

| Menu | Option |
| -------   | -------  |
|Catégorie| Commercial Marketplace|
| Rubrique | Questions générales sur l’aide et les comments sur Marketplace |
| Subtopic| Complément Office |

### <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a>Où puis-je obtenir de l’aide pour les problèmes de compte de l’Partner Center ?

Visitez la [page de support des éditeurs](https://aka.ms/marketplacepublishersupport) pour rechercher votre sujet de problème et obtenir des conseils. Si les conseils fournis ne sont pas utiles, augmentez un [ticket de support de l’Centre partenaires.](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)

### <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a>Comment gérer mon compte Office Store dans l’Partner Center ?

Visitez le [compte Gérer votre Office Store via l’Partner Center](/office/dev/store/manage-account-settings-and-profile) pour obtenir des conseils.

### <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a>Comment ajouter mon numéro de téléphone à la section de contact de profil partenaire ?

Le numéro de téléphone est en trois parties : code pays, code de zone et numéro de téléphone. Si votre numéro de téléphone n’inclut pas de code de zone, laissez la deuxième zone vide et complétez la troisième zone.

### <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a>Comment gérer les paramètres de mon compte et mon profil de partenaire dans l’Partner Center ?

Consultez la page [Gérer les paramètres du compte et les](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) informations de profil pour obtenir des conseils sur la gestion de vos paramètres de compte De l’Partner Center.

### <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-app"></a>Pourquoi reçois-je le message « Ce compte n’est pas éligible pour la publication » lorsque j’essaie de soumettre mon application ?

Vous recevez le message d’erreur ci-dessus lorsque l’état [de vérification de](/partner-center/verification-responses) votre compte est en attente. Vérifiez l’état de vérification de votre compte dans le tableau de bord de l’Centre [partenaires.](https://partner.microsoft.com/dashboard) Sélectionnez **Paramètres**, l’icône d’engrenage dans le coin supérieur droit de l’en-tête de page. Choisissez **les paramètres du compte**  =>  **de**   =>  **paramètres du développeur.**

![Page paramètres du compte de l’Partner Center](../../../assets/images/partner-center-accts-page.png)

![État de vérification de l’Partner Center](../../../assets/images/partner-center-verification-status.png)

L’état de chaque étape requise, telle que la propriété de l’e-mail, la vérification de l’emploi et la vérification de l’entreprise, est affiché dans le processus de vérification du compte. Une fois le processus de vérification terminé, l’état de vérification de votre inscription sur la page de profil passe *d’en* attente *à autorisé.* Les étapes du processus ne sont plus affichées.

![Erreur de vérification de l’Centre partenaires](../../../assets/images/partner-center-acct-verification-error.png)

### <a name="what-is-verified-in-the-partner-center-account-verification-process-and-how-to-respond"></a>Qu’est-ce qui est vérifié dans le processus de vérification du compte de l’Partner Center et comment y répondre ?

Il existe trois zones de vérification, **la propriété de messagerie,** **l’emploi** et **l’entreprise.** Pour plus d’informations sur le processus de vérification, voir [Ce qui est vérifié et comment y répondre.](/partner-center/verification-responses#what-is-verified-and-how-to-respond)
Si vous êtes le contact principal, l’administrateur global ou l’administrateur de compte, go to your Partner Profile to monitor verification status and track the progress.

Une fois le processus de vérification terminé, l’état de vérification de votre inscription sur la page de profil passe *d’en* attente *à autorisé.* Après l’autorisation, les étapes du processus et leur état ne sont plus disponibles sur la page. Le contact principal reçoit un courrier électronique de Microsoft dans les jours ou suivants après la fin de la vérification.

### <a name="my-account-verification-status-hasnt-advanced-beyond-email-ownership-how-should-i-proceed"></a>L’état de vérification de mon compte n’a pas dépassé la propriété de l’e-mail. Comment dois-je continuer ?

Pendant le processus **de vérification de la** propriété de l’e-mail, un e-mail de vérification est envoyé à l’adresse de messagerie du contact principal. Vérifiez la boîte de réception de votre contact principal pour obtenir un e-mail **maccount@<span>microsoft</span>.com** avec l’action de ligne d’objet requise : Vérifiez votre compte de messagerie *auprès de Microsoft.* Terminez le processus de vérification du courrier électronique. L’e-mail de vérification est envoyé à l’adresse de messagerie répertoriée sur la page des paramètres de votre compte dans l’Partner Center.

> [!NOTE]
> * Le lien de vérification du courrier électronique n’est valide que pendant sept jours. 
> * Vous pouvez nous demander de renvoyer l’e-mail en visitant la page de votre profil de partenaire et en sélectionnant le lien renvoyer le courrier électronique de **vérification.**
> * Pour vous assurer que le courrier électronique est reçu, listez les messages électroniques provenant de microsoft.com comme domaine sécurisé et vérifiez vos dossiers de courrier indésirable.

### <a name="how-do-i-get-further-support-for-my-account-related-issues"></a>Comment obtenir une assistance supplémentaire pour les problèmes liés à mon compte ?

Consultez la page [Support pour le programme Commercial Marketplace](/azure/marketplace/partner-center-portal/support) dans l’Espace partenaires pour obtenir des conseils et des étapes pour créer un ticket de support.

### <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what-must-i-do-next"></a>J’ai vérifié mes dossiers de courrier et je n’ai pas reçu l’e-mail de vérification. Que dois-je faire ensuite ?

Procédez comme suit :
* Vérifiez votre dossier de courrier indésirable ou de courrier indésirable.
* Clear the browser cache, go to your Partner Center account dashboard, and select the **Resend verification email** link to have the verification email resent to your email address.
* Essayez d’accéder au **lien renvoyer le courrier** électronique de vérification à partir d’un autre navigateur.
* Contactez votre service informatique pour vous assurer que les e-mails de vérification ne sont pas bloqués par le serveur de messagerie.
* Ajustez le filtre de courrier indésirable de votre serveur pour autoriser ou lister en toute sécurité tous les messages électroniques provenant **maccount@microsoft. <span></span> com**.

### <a name="how-long-does-the-employment-verification-process-usually-take"></a>Combien de temps dure généralement le processus de vérification de l’emploi ?

Si tous les détails envoyés sont corrects, le processus de vérification de l’emploi prend environ deux heures.

### <a name="how-long-does-the-business-verification-process-usually-take"></a>Combien de temps le processus de vérification d’entreprise prend-il en général ?

Si tous les documents requis sont envoyés, la vérification de l’entreprise prend un à deux jours ou plus.

### <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a>Si je pars en direction de l’équipe de support technique, mon ticket sera-t-il accéléré ?

Les tickets de support sont résolus dans une semaine. Recherchez les mises à jour envoyées à l’ID de courrier électronique fourni lors de l’augmentation du ticket de support.

### <a name="my-issue-is-not-listed-here-are-there-other-pages-i-can-reference-for-partner-center-issues"></a>Mon problème n’est pas répertorié ici. Existe-t-il d’autres pages que je peux référencer pour les problèmes de l’Partner Center ?

Pour plus [d’aide, consultez](/azure/marketplace/) la documentation du marketplace commercial.

### <a name="ive-created-a-support-ticket-and-i-havent-received-an-update-in-7-business-days-where-can-i-get-help"></a>J’ai créé un ticket de support et je n’ai pas reçu de mise à jour depuis 7 jours ou moins. Où puis-je obtenir de l’aide ?

Envoyez un courrier **<teamsubm@microsoft.com>** électronique avec les détails suivants :

* **Ligne d’objet**: Problème de compte de l'<App_Name> (spécifiez le nom de votre application).
* **Corps de l’e-mail**:
    * Numéro de ticket de support
    * Votre ID vendeur
    * Capture d’écran du problème (si possible)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Maintenance et prise en charge de votre application](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
