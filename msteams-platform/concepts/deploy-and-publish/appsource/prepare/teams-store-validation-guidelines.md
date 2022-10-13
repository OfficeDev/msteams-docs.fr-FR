---
title: Instructions de validation du magasin Microsoft Teams
description: Découvrez comment augmenter les chances que votre application réussisse le processus de soumission du Microsoft Teams Store. Comprendre les correctifs obligatoires et suggérés. Explorez les instructions de validation.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 0a0151c72820baf1b6bd39ee00539cacbd3fa38b
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560982"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Instructions de validation du magasin Microsoft Teams

Le respect de ces directives augmente les chances que votre application réussisse le processus de soumission du magasin Microsoft Teams. Les directives spécifiques aux équipes complètent les [politiques de certification du marché commercial](/legal/marketplace/certification-policies#1140-teams) Microsoft et sont mises à jour fréquemment pour refléter les nouvelles fonctionnalités, les commentaires des utilisateurs et les modifications des règles métier.

> [!NOTE]
>
> * Certaines instructions peuvent ne pas être applicables à votre application. Par exemple, si votre application n’inclut pas de bot, vous pouvez ignorer les instructions liées aux bots.
> * Nous avons recoupé ces directives avec les politiques de certification commerciale de Microsoft et ajouté les choses à faire et à ne pas faire avec des exemples de scénarios de réussite ou d'échec rencontrés dans notre processus de validation.
> * Certaines directives sont marquées comme *Correction obligatoire*. Si votre soumission d'application ne respecte pas ces directives obligatoires, vous recevrez un rapport d'échec de notre part avec des mesures pour atténuer. Votre soumission d'application ne passera la validation du Microsoft Teams Store qu'une fois que vous aurez résolu les problèmes.
> * Other guidelines are marked as *Suggested Fix*. For an ideal user experience, we suggest that you fix the issues, however, your app submission will not be blocked from publishing on the Teams store, if you choose not to fix the issues.

:::row:::
   :::column:::
      :::image type="icon" source="../../../../assets/icons/value-proposition.png" link="#value-proposition" border="false":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../../assets/icons/security.png" link="#security" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/function.png" link="#general-functionality-and-performance" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/package.png" link="#app-package-and-store-listing" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/saas-offer.PNG" link="#apps-linked-to-saas-offer" border="false":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/tab.png" link="#tabs" border="false":::
   :::column-end:::
   :::column:::
      :::image type="icon" source="../../../../assets/icons/bot.png" link="#bots-1" border="false":::
   :::column-end:::
   :::column span="":::
     :::image type="icon" source="../../../../assets/icons/messaging-extension.png" link="#message-extensions" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/task-module.png" link="#task-modules" border="false":::
   :::column-end:::
     :::column span="":::
      :::image type="icon" source="../../../../assets/icons/meeting.png" link="#meeting-extensions" border="false":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/notifications.png" link="#notifications" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/microsoft-365.png" link="#microsoft-365-app-compliance-program" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/advertising.png" link="#advertising" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/crypto-currency-based-apps-icon.png" link="#cryptocurrency-based-apps" border="false":::
   :::column-end:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/app-functionality-icon.png" link="#app-functionality" border="false":::
   :::column-end:::
:::row-end:::
:::row:::
   :::column span="":::
      :::image type="icon" source="../../../../assets/icons/mobile-experience-icon.png" link="#mobile-experience" border="false":::
   :::column-end:::
:::row-end:::

## <a name="value-proposition"></a>Proposition de valeur

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la stratégie de certification commerciale de [Microsoft, numéro 1140.1, ](/legal/marketplace/certification-policies#11401-value-proposition-and-offer-requirements)et fournit des conseils supplémentaires aux développeurs d'applications Microsoft Teams sur la proposition de valeur de leur offre.

### <a name="app-name"></a>Nom de l'application

[*Correction obligatoire*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la stratégie de certification commerciale de Microsoft[, numéro 1140.1.1](/legal/marketplace/certification-policies#114011-app-name), et fournit des conseils supplémentaires aux développeurs pour nommer leurs applications.
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Le nom d’une application joue un rôle essentiel dans la façon dont les utilisateurs la découvrent dans le magasin. Utilisez les instructions suivantes pour nommer une application :

* Le nom doit inclure des termes susceptibles d’intéresser vos utilisateurs.
* Préfixe ou suffixe des noms communs avec le nom du développeur. Par exemple, **Tâches Contoso** au lieu de **Tâches**.
* Ne doit pas utiliser **Teams** ou d’autres noms de produits Microsoft tels qu’Excel, PowerPoint, Word, OneDrive, SharePoint, OneNote, Azure, Surface et Xbox qui pourraient indiquer faussement la co-personnalisation ou la co-vente. Pour plus d'informations sur le référencement des produits et services logiciels Microsoft, consultez [Directives sur les marques et marques Microsoft](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general).
* Ne doit pas copier le nom d’une application répertoriée dans le magasin ou une autre offre sur la place de marché commerciale.
* Ne doit pas contenir de termes vulgaires ou désobligeants. Le nom ne doit pas non plus inclure un langage qui manque d’égard en matière de race ou de culture.
* Doit être unique. Si votre application (Contoso) est répertoriée dans le Microsoft Teams Store et Microsoft AppSource et que vous souhaitez répertorier une autre application spécifique à une zone géographique telle que Contoso Mexico, votre soumission doit répondre aux critères suivants :
  * Appelez la fonctionnalité spécifique à la région de l'application dans le titre, les métadonnées, l'expérience de l'application de première réponse et les sections d'aide. Par exemple, le titre doit être Contoso Mexico. Le titre de l'application doit clairement différencier une application existante du même développeur pour éviter toute confusion chez l'utilisateur final.
  * Lors du téléchargement du package d'application dans Partner Center, sélectionnez les bons **marchés** où l'application sera disponible dans la section **Disponibilité**.

* Le nom de l’application ne doit pas être dirigé avec une fonctionnalité Teams de base telle que la conversation, les contacts, le calendrier, les appels, les fichiers, l’activité, les équipes, les applications et l’aide. Le nom de l’application peut être abrégé en Conversation, Contacts, Calendrier, Appels, Fichiers, Activité, Teams, Applications et Aide lors de l’installation dans le volet de navigation gauche.

* If your app is part of an official partnership with Microsoft, the name of your app must come first. For example, **Contoso Connector for Microsoft Teams**.

* Le nom de l’application ne doit pas avoir de référence aux produits Microsoft ou Microsoft. N’utilisez pas **Teams**, **Microsoft** ou **App** dans le nom de l’application, sauf si votre application est en partenariat officiel avec Microsoft. Dans ce cas, le nom de l’application doit passer en premier avant toute référence à Microsoft. Par exemple, **connecteur Contoso pour Microsoft Teams**.

* N’utilisez pas de parenthèses pour nommer les produits Microsoft.

* Le nom du développeur doit être le même dans le manifeste et AppSource.

* Les manifestes d’application soumis doivent être des manifestes de production. Par conséquent, le nom de l’application ne doit pas indiquer que l’application est une application de préproduction. Par exemple, le nom de l’application ne doit pas contenir de mots tels que Beta, Dev, Preview et UAT.

 > [!TIP]
 > La personnalisation de votre application sur le Microsoft Teams Store et AppSource, y compris le nom de votre application, le nom du développeur, l’icône d’application, les captures d’écran AppSource, la vidéo, la description courte et le site web séparément ou pris ensemble, ne doit pas emprunter l’identité d’une offre Microsoft officielle, sauf si votre application est une offre Microsoft 1P officielle.

</details>

### <a name="suitable-for-workplace-consumption"></a>Convient à une utilisation dans l’espace de travail

[*Correction obligatoire*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la stratégie de certification commerciale de Microsoft [1140.1.2](/legal/marketplace/certification-policies#114012-workplace-appropriateness), [100.8](/legal/marketplace/certification-policies#1008-significant-value) et [100.10](/legal/marketplace/certification-policies#10010-inappropriate-content) et fournit des conseils supplémentaires aux développeurs sur la création d'applications adaptées au lieu de travail.
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Le contenu de l'application doit être adapté à la consommation générale sur le lieu de travail et respecter toutes les restrictions énumérées dans les politiques de certification du marché commercial. Le contenu lié à la religion, à la politique, aux jeux et aux divertissements prolongés est interdit.

Votre application doit permettre la collaboration de groupe, améliorer la productivité d'un individu, ou les deux. Les applications destinées à la socialisation et à l’esprit d’équipe doivent être collaboratives et conçues pour plusieurs participants. Les applications ne doivent pas nécessiter un investissement de temps substantiel de plus de 60 minutes par session ou affecter la productivité.

</details>

### <a name="similar-platforms-and-services"></a>Plateformes et services similaires

[*Correction obligatoire*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est en ligne avec [la stratégie de certification commerciale de Microsoft numéro 1140.1.3](/legal/marketplace/certification-policies#114013-other-platforms-and-services).

Les applications doivent se concentrer sur l'expérience Teams et ne pas inclure les noms, icônes ou images d'autres plates-formes ou services de collaboration similaires basés sur le chat dans le contenu de l'application ou dans les métadonnées de l'application, à moins que l'application ne fournisse une interopérabilité spécifique.

### <a name="feature-names"></a>Noms de fonctionnalité

Les noms des fonctionnalités d’application dans les boutons et tout autre texte de l’interface utilisateur ne doivent pas utiliser la terminologie réservée à Teams et à d’autres produits Microsoft. Par exemple, **démarrer une réunion**, **passer un appel** ou **démarrer une conversation** sont des noms de fonctionnalités utilisés par Microsoft dans Microsoft Teams. Si nécessaire, incluez le nom de votre application pour faire la distinction clairement, par exemple **démarrer la réunion Contoso**.

### <a name="authentication"></a>Authentification

[*Correction obligatoire*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est en ligne avec la stratégie de certification commerciale [Microsoft numéro 1140.1.4](/legal/marketplace/certification-policies#114014-access-to-services) et fournit des conseils aux développeurs sur l'authentification de leurs applications avec des services externes.

Pour plus d'informations sur la mise en œuvre de l'authentification des applications, consultez l'[authentification dans Teams](~/concepts/authentication/authentication.md).
<br></br>
<details><summary>Développer pour en savoir plus</summary>

#### <a name="authenticating-with-external-services"></a>Authentification avec des services externes

Si votre application authentifie les utilisateurs avec un service externe, suivez ces instructions :

* **Expériences d’inscription, de connexion et de déconnexion** :
  * Les applications qui dépendent de comptes ou de services externes doivent fournir une expérience de connexion, de déconnexion et d'inscription claire et simple.
  * Lorsque les utilisateurs se déconnectent, ils doivent se déconnecter uniquement de l'application et rester connectés à Teams.
  * Les applications qui dépendent de comptes ou de services externes doivent permettre aux nouveaux utilisateurs de s'inscrire ou de contacter l'éditeur de l'application pour en savoir plus sur les services et accéder aux services.
  La marche à suivre doit être disponible dans le manifeste de l'application, la description longue AppSource et l'expérience de première exécution de l'application (message de bienvenue du bot, configuration de l'onglet ou page de configuration).
  * Les applications qui nécessitent que l'administrateur du locataire effectue une configuration unique doivent appeler la dépendance à l'administrateur du locataire pour configurer l'application (avant qu'un autre utilisateur du locataire ne puisse installer et utiliser l'application).
  La dépendance doit être indiquée dans le manifeste de l'application, la description longue AppSource, tous les points de contact de la première exécution (message de bienvenue du bot, configuration de l'onglet ou page de configuration), le texte d'aide considéré comme nécessaire dans le cadre de la réponse du bot, de l'extension de composition ou du contenu de l'onglet statique.
  
* **Expériences de partage de contenu** : les applications qui nécessitent une authentification auprès d'un service externe pour partager du contenu dans les canaux Teams doivent indiquer clairement dans la documentation d'aide (ou des ressources similaires) comment déconnecter ou annuler le partage de contenu si cette fonctionnalité est prise en charge sur le service externe. Cela ne signifie pas que la possibilité d’annuler le partage de contenu doit être présente dans votre application Teams.

</details>

## <a name="security"></a>Sécurité

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la stratégie de certification commerciale de [Microsoft, numéro 1140.3](/legal/marketplace/certification-policies#11403-security).

### <a name="financial-information"></a>Informations financières

[*Correction obligatoire*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Cette section est incluse dans la stratégie de [certification commerciale Microsoft 1140.3.1](/legal/marketplace/certification-policies#114031-financial-transactions) et fournit des conseils sur la transmission d’informations financières dans l’interface Teams et informe les développeurs des scénarios de paiement restreint sur la version mobile (Android et iOS) de leur application Teams.
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Les applications ne doivent pas demander aux utilisateurs d'effectuer des paiements dans l'interface Teams et de transmettre des informations financières aux utilisateurs via une interface de bot.

:::image type="content" source="../../../../assets/images/submission/validation-financial-information-1.png" alt-text="validation-financial-info":::

Vous pouvez fournir un lien vers des services de paiement externes sécurisés uniquement si vous le divulguez dans vos conditions d'utilisation, votre politique de confidentialité, votre page de profil ou votre site Web avant que l'utilisateur n'accepte d'utiliser l'application.

Ne facilitez pas les paiements via une application pour des biens ou des services interdits par la [Police générale numéro 100.10 Contenu inapproprié](/legal/marketplace/certification-policies#10010-inappropriate-content).

Les applications qui s’exécutent sur la version iOS ou Android de Teams doivent respecter les instructions suivantes :

* Les applications ne doivent pas inclure d'achats intégrés, d'offres d'essai ou d'interface utilisateur visant à vendre aux utilisateurs des versions payantes ou des magasins en ligne pour acheter d'autres contenus, applications ou compléments.

    :::image type="content" source="../../../../assets/images/submission/validation-financial-information-in-app-purchase.png" alt-text="validation-financial-info-in-app-purchase":::

    :::image type="content" source="../../../../assets/images/submission/validation-financial-information-online-stores.png" alt-text="validation-online-store":::

* Si votre application nécessite un compte, les utilisateurs peuvent créer un compte gratuitement. L’utilisation du terme **compte gratuit** ou **gratuit** est interdite.
* You can determine whether an account is active indefinitely or for a limited time. When the account expires the app must not show UI, text, or links indicating the need to pay.
* La politique de confidentialité et les conditions d'utilisation de votre application doivent être exemptes d'interface utilisateur ou de liens liés au commerce.

</details>

### <a name="bots"></a>Bots

[*Correction obligatoire*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la stratégie 1140.3.2 du[ marché commercial de Microsoft](/legal/marketplace/certification-policies#114032-bots-and-messaging-extension).
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Pour les applications qui utilisent Microsoft Azure Bot Service (par exemple, les bots et les extensions de messagerie), vous devez respecter toutes les conditions définies dans les [Conditions d’utilisation des services en ligne Microsoft](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

Les robots doivent toujours demander la permission de télécharger un fichier et afficher un message de confirmation.

:::image type="content" source="../../../../assets/images/submission/validation-bot-confirmation-message.png" alt-text="validation-bot-confirmation":::

</details>

### <a name="external-domains"></a>Domaines externes

[*Correction obligatoire*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme [à la stratégie 1140.3.3](/legal/marketplace/certification-policies#114033-external-domains) du marché commercial de Microsoft et fournit des conseils aux développeurs sur l'utilisation des domaines restreints`validDomains` dans la propriété du manifeste.
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Don't include domains outside of your organization's control (including wildcards) and tunneling services in your app's domain configurations. The following exceptions include:

* Si votre application utilise le OAuthCard d’Azure Bot Service, vous devez inclure `token.botframework.com` en tant que domaine valide, sinon le bouton **Se connecter** ne fonctionne pas.
* Si votre application repose sur SharePoint, vous pouvez inclure le site racine SharePoint associé en tant que domaine valide à l’aide de la propriété de contexte `{teamSiteDomain}`.
* N’utilisez pas de domaines de niveau supérieur tels que **.com**, **.in** et **.org** comme domaine valide. [*Correction obligatoire*]

* N’utilisez pas **.onmicrosoft.com ou** en tant que domaine valide où **onmicrosoft** n’est pas sous votre contrôle. Toutefois, vous pouvez utiliser **yoursite.com** comme domaine valide où **votre site** est sous votre contrôle, même si le domaine inclut un caractère générique. [*Correction obligatoire*]

* Si votre application est une application PowerApp basée sur Microsoft Power Platform, vous devez inclure *apps.powerapps.com* comme domaine valide pour permettre à votre application d’être accessible et fonctionnelle dans Teams.

</details>

### <a name="sensitive-content"></a>Contenu sensible

[*Correction obligatoire*]

Votre application ne doit pas publier de données sensibles, telles que carte de crédit, détails de paiement, santé, recherche de contacts ou autres informations personnellement identifiables (PII) à un public qui n'a pas l'intention de voir le contenu.

L'application doit avertir les utilisateurs avant de télécharger des fichiers ou des exécutables (.exe) sur la machine ou l'environnement de l'utilisateur.

## <a name="general-functionality-and-performance"></a>Fonctionnalités et performances générales

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4 du marché commercial de Microsoft](/legal/marketplace/certification-policies#11404-functionality).

* Les instructions d’avenir sont obligatoires pour l’administrateur et les utilisateurs existants. Vous pouvez ajouter des conseils sur la voie à suivre en tant que liens hypertexte pour vous inscrire, commencer, nous contacter, obtenir des liens d’aide ou envoyer des e-mails.
* L’appel de dépendances ou de limitations de compte sous la fonctionnalité d’application n’est pas obligatoire, mais il est obligatoire de l’ajouter à la fois dans la description longue du manifeste et dans la description de l’application AppSource.
* Vous devez appeler toute dépendance vis-à-vis des administrateurs de locataires pour les nouveaux utilisateurs. S’il n’existe aucune dépendance, il est obligatoire de fournir une inscription, de nous contacter, de créer un lien ou d’envoyer un e-mail.

### <a name="launching-external-functionality"></a>Lancement des fonctionnalités externes

[*Correction obligatoire*]

Les applications ne doivent pas extraire les utilisateurs de Teams pour des scénarios utilisateur de base. Le contenu et les interactions de l'application doivent se produire dans les capacités de Teams, telles que les robots, les cartes adaptatives, les onglets et les modules de tâches.
<br>
</br>

<details><summary>Développer pour en savoir plus</summary>

* Liez les utilisateurs au sein de l'application Teams et non à un site ou une application externe. Pour les scénarios qui nécessitent une fonctionnalité externe, votre application doit obtenir une autorisation utilisateur explicite pour lancer la fonctionnalité.

* Le texte de l'interface utilisateur du bouton qui lance la fonctionnalité externe doit inclure du contenu pour indiquer que l'utilisateur est retiré de l'instance Teams. Par exemple, incluez du texte tel que **Par ici vers Contoso.com** ou **Afficher dans Contoso.com**.

* **Ajoutez une** icône contextuelle pour informer les utilisateurs qu’ils sont en cours de navigation en dehors de Teams. Vous pouvez utiliser l’icône :::image type="icon" source="../../../../assets/icons/pop-out-icon.png" ::: contextuelle à droite du lien.

* Si vous ne parvenez pas à **ajouter une icône** contextuelle, vous pouvez implémenter l’une des options suivantes pour informer l’utilisateur qu’il est en cours de navigation en dehors de Teams :
  * Ajoutez une note dans la carte adaptative qui indique que lorsque les utilisateurs sélectionnent **Obtenir de l’aide à l’aide de cette application**, l’utilisateur se trouve en dehors de Teams.
  * Ajouter des dialogues interstitiels.

</details>

### <a name="compatibility"></a>Compatibilité

[*Correction obligatoire*]

Les applications doivent être entièrement fonctionnelles sur les dernières versions des systèmes d'exploitation et des navigateurs suivants :

* Microsoft Windows
* macOS
* Microsoft Edge
* Google Chrome
* iOS
* Android

Votre application doit afficher un message d'échec normal sur les navigateurs et systèmes d'exploitation non pris en charge.

### <a name="response-time"></a>Temps de réponse

[*Correction obligatoire*]

Les applications Teams doivent répondre dans un délai raisonnable ou afficher un indicateur de chargement ou de saisie, un message ou un avertissement.

* Les onglets doivent répondre dans les deux secondes ou afficher un message de chargement ou un avertissement.
* Les bots doivent répondre aux commandes de l’utilisateur dans un délai de deux secondes ou afficher un indicateur de saisie.
* Les extensions de messagerie doivent répondre aux commandes de l'utilisateur dans les deux secondes.
* Les notifications doivent s'afficher dans les deux secondes suivant l'action de l'utilisateur.

## <a name="app-package-and-store-listing"></a>Package d’application et description dans le Store

[*Correction obligatoire*]

Les packages d’application doivent être correctement formatés et inclure toutes les informations et composants requis.

> [!TIP]
>
> * Vous devez vous assurer que les comptes de test ou l’environnement de test fournis sont valides à perpétuité, c’est-à-dire jusqu’à ce que l’application soit active sur la place de marché commerciale.
> * Vous devez inclure les instructions de test détaillées suivantes pour valider la soumission de votre application :
>
>   * **Étapes pour configurer les comptes de test d'application** au cas où l'application dépendrait de comptes externes pour l'authentification.
>   * Résumé du **comportement attendu de l'application** pour les workflows de base au sein des équipes.
>   * **Décrivez clairement les limitations**, conditions ou exceptions aux fonctionnalités, caractéristiques et livrables dans la description longue de l'application et les documents connexes.
>   * **Mettre l'accent sur toutes les considérations** pour les testeurs lors de la validation de la soumission de votre application.
>   * **Pré-remplir les comptes de test avec des données factices** pour faciliter les tests.
>   * Si vous fournissez vos comptes de test, veillez à activer l’intégration tierce. Désactivez également l’authentification à deux facteurs ou multifacteur.

### <a name="app-manifest"></a>Manifeste d'application

[*Correction obligatoire*]

Le manifeste de l'application Teams définit la configuration de votre application.

* Votre manifeste doit être conforme à un schéma de manifeste publié publiquement. Pour plus d'informations, consultez la [référence du manifeste](~/resources/schema/manifest-schema.md). Ne soumettez pas votre application à l'aide d'une version d'aperçu du manifeste.
* Si votre application inclut un bot ou une extension de messagerie, les détails du manifeste de l'application doivent être cohérents avec les métadonnées de Bot Framework, notamment le nom du bot, le logo, le lien vers la politique de confidentialité et le lien vers les conditions d'utilisation.
* Si votre application utilise Azure Active Directory pour l’authentification, incluez l’ID d’application (client) Microsoft Azure Active Directory (Azure AD) dans le manifeste. Pour plus d’informations, voir la [référence de manifeste](~/resources/schema/manifest-schema.md#webapplicationinfo).

### <a name="uses-of-latest-manifest-schema"></a>Utilisations du schéma de manifeste le plus récent

* Si votre application utilise l’authentification unique (SSO), vous devez déclarer Microsoft Azure Active Directory ID (Azure AD) dans le manifeste pour l’authentification utilisateur. [*Correction obligatoire*]

* Vous devez utiliser un schéma de manifeste publié publiquement. Vous pouvez mettre à jour votre package d’application pour utiliser une version publique du schéma de manifeste 1.10 ou version ultérieure. [*Correction obligatoire*]

* Lorsque vous envoyez une mise à jour d’application, augmentez uniquement le numéro de version de l’application. L’ID d’application de l’application mise à jour doit correspondre à l’ID d’application de l’application publiée. [*Correction obligatoire*]

* La présence de fichiers supplémentaires dans le package d’application n’est pas acceptable. [*Correction obligatoire*]

* Le numéro de version doit être le même dans le schéma de fichier manifeste et le schéma de manifeste des langues supplémentaires. [*Correction obligatoire*]

* Vous devez utiliser le schéma de manifeste Teams version 1.5 ou ultérieure pour localiser votre application. Pour utiliser le schéma d’application version 1.5 ou ultérieure dans votre fichier manifest.json, mettez à jour l’attribut vers la `$schema` version 1.5 ou ultérieure. Mettez à jour la propriété vers la `manifestVersion` `$schema` version (1.5 dans ce cas). [*Correction obligatoire*]

* Lorsque vous ajoutez, mettez à jour ou supprimez une fonctionnalité existante, ajoutez ou supprimez des métadonnées de manifeste ou d’Espace partenaires, vous devez augmenter le numéro de version de l’application et envoyer le nouveau manifeste d’application dans votre compte Espace partenaires pour validation.

* La chaîne de version doit suivre la norme DEM (Semantic Versioning Specification) (SemVer). MINEUR. PATCH). [*Correction obligatoire*]

* Si votre application exige que les administrateurs examinent les autorisations et accordent leur consentement dans le Centre d’administration Teams, vous devez déclarer `webapplicationinfo` dans le manifeste. S’il `webapplicationinfo` n’est pas déclaré dans le manifeste, la page **Autorisations** de votre application dans le Centre d’administration Teams s’affiche sous **la forme ...** [*Correctif obligatoire*]

* Dans le cadre de la certification des applications Teams, vous devez soumettre une version de production du manifeste de l’application. [*Correction obligatoire*]

* Nous vous recommandons de déclarer l’ID MPN (Microsoft Partner Network) dans le manifeste. L’ID MPN permet d’identifier l’organisation partenaire qui génère l’application. [*Correctif suggéré*]

### <a name="app-icons"></a>Icônes d’application

[*Correction obligatoire*]

Les icônes sont l’un des principaux éléments que les utilisateurs voient lors de la navigation dans le magasin Teams.
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Vos icônes doivent communiquer la marque et l'objectif de votre application tout en respectant les exigences suivantes :

* Votre package d’application doit inclure deux versions .png de votre icône d’application : une icône de couleur et une icône de contour.
* La version couleur de votre icône doit être de 192x192 pixels. Votre symbole d'icône peut être de n'importe quelle couleur, mais il doit être placé sur un fond carré uni ou entièrement transparent.
* La version simplifiée de votre icône s'affiche dans les scénarios suivants :
  * Lorsque votre application est utilisée et **hébergée** dans la barre d'applications sur le côté gauche de Teams.
  * Lorsqu’un utilisateur épingle l’extension de message de votre application.

* Le contour doit être de 32x32 pixels et peut être blanc avec un fond transparent ou transparent avec un fond blanc. L'icône ne doit pas avoir de rembourrage supplémentaire autour du symbole.

* Votre package d'application doit inclure des icônes correctement dimensionnées et formatées. Les icônes doivent correspondre aux informations contenues dans les métadonnées de la fiche Play Store.

Pour plus d'informations, consultez les [instructions relatives aux icônes](~/concepts/build-and-test/apps-package.md#app-icons).

</details>

### <a name="app-descriptions"></a>Descriptions de l’application

Vous devez avoir une description courte et longue pour votre application. Les descriptions de la configuration de votre application et de l’Espace partenaires doivent être identiques.

:::image type="content" source="../../../../assets/images/submission/validation-app-description-adequete-information.png" alt-text="Le graphique montre un exemple de description d’application appropriée dans l’application Teams.":::

:::image type="content" source="../../../../assets/images/submission/validation-app-description-inadequete.png" alt-text="Le graphique montre un scénario d’échec pour une description d’application inadéquate.":::

<br></br>
<details><summary>Développer pour en savoir plus</summary>

Les descriptions ne doivent pas directement ou par insinuation dénigrer une autre marque (détenue par Microsoft ou non). Assurez-vous que votre description n’inclut pas les revendications qui ne peuvent pas être corroborées. Par exemple, **Augmentation garantie de 200 % de l'efficacité**.

* La description de l’application ne doit pas contenir d’informations marketing comparatives. Par exemple, n’utilisez pas de logos ou de marques concurrents dans la liste des offres, y compris des étiquettes ou d’autres métadonnées qui référencent des offres ou des places de marché concurrentes. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-comparitive-marketing-fail.png" alt-text="Le graphique montre un exemple d’informations marketing comparatives dans la description de l’application.":::

* Détails du contact de lien hypertexte, prise en main, aide ou inscription dans la description de l’application.

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-contact-deatils-hyperlinked.png" alt-text="Le graphique montre un exemple de lien hypertexte des détails du contact dans les descriptions de l’application.":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-contact-deatils-not-hyperlinked.png" alt-text="Le graphique montre un exemple de détails de contact non liés par lien hypertexte dans les descriptions de l’application.":::

* La description de l’application doit identifier l’audience prévue, expliquer brièvement et clairement sa valeur unique et distincte, identifier les produits Microsoft pris en charge et d’autres logiciels, et inclure les conditions préalables ou les exigences pour son utilisation. Vous devez décrire clairement les limitations, conditions ou exceptions aux fonctionnalités, fonctionnalités et livrables, comme décrit dans la liste et les documents associés avant que le client n’acquiert votre offre. Les fonctionnalités que vous déclarez doivent être liées aux fonctions principales et à la description de votre offre. [*Correction obligatoire*]

* Si vous mettez à jour le nom de votre application, remplacez l’ancien nom de l’application par le nouveau nom de l’application dans les métadonnées de l’offre dans le manifeste, AppSource et, le cas échéant. [*Correction obligatoire*]

* Les limitations et les dépendances de compte doivent être indiquées dans le manifeste Description de l’application, AppSource et Espace partenaires. Par exemple :
  * Compte d’entreprise
  * Abonnement payant
  * Une autre licence ou un autre compte
  * Langue
  * Numérotation de réseau téléphonique commuté (RTC) publique
  * Dépendance régionale
  * Délai de réservation des traducteurs ou des agents en direct
  * Fonctionnalités basées sur les rôles
  * Dépendance vis-à-vis de l’application native

  :::image type="content" source="../../../../assets/images/submission/validation-app-description-limitations-calledout-pass.png" alt-text="Le graphique montre un exemple de limitations indiquées dans la description de l’application.":::
  
  :::image type="content" source="../../../../assets/images/submission/validation-app-description-limitations-not-calledout-fail.png" alt-text="Le graphique montre un exemple de limitations qui ne sont pas indiquées dans les descriptions d’application.":::

* Si votre application est prise en charge pour des régions ou des emplacements géographiques spécifiques, vous devez appeler cette dépendance de région spécifique dans la description de l’application dans le manifeste, l’Espace partenaires et AppSource pour cette offre.

* Si vous devez référencer Teams, écrivez la première référence dans la liste des applications en tant que Microsoft Teams. Les références ultérieures peuvent être raccourcies à Teams.

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-teams-reference-pass.png" alt-text="Le graphique montre un exemple de référence correcte à Teams dans la description de l’application.":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-teams-reference-fail.png" alt-text="Le graphique montre un exemple de référence incorrecte à Teams dans la description de l’application.":::

#### <a name="short-description"></a>Description courte

Une brève description est un résumé concis de votre application qui met en évidence sa proposition de valeur et s’adresse à votre public cible.

**À faire :**

* Votre description courte doit tenir sur une seule phrase.
* Mettez les informations les plus importantes en premier.
* Incluez des mots clés que les clients sont susceptibles de rechercher.
* Utilisez efficacement la limite de caractères disponible. Par exemple, ne répétez pas le nom de votre application.

**À ne pas faire :**

[*Correctif suggéré*]

Utilisez le mot **application** dans la description courte.

#### <a name="long-description"></a>Description longue

La description longue peut fournir un narratif attrayant qui met en évidence la proposition de valeur de votre application, le public principal et le secteur cible. Bien que cette description puisse contenir jusqu’à 4 000 caractères, la plupart des utilisateurs ne lisent qu’entre 300 et 500 mots.

**À faire :**

* Utilisez [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) pour mettre en forme votre description.

* Utilisez la voix active et parlez directement aux utilisateurs. Par exemple, **Vous pouvez...**.

* Répertoriez les fonctionnalités à l’aide de points à puces pour faciliter l’examen de la description.

* Décrivez clairement les limitations, caractéristiques, conditions ou exceptions à la fonctionnalité et les livrables dans la liste et les documents connexes avant que l'utilisateur n'installe votre application. Les capacités des équipes doivent être liées aux fonctions de base décrites dans la liste.

* Vérifiez que la description de l’application correspond aux fonctionnalités disponibles dans l’application Teams. Toute référence à des flux de travail en dehors de l'application Teams doit être limitée et distinctement appelée à partir de la fonctionnalité de l'application Teams.

* Incluez un lien d’aide ou de support.

* Faites référence à **Microsoft 365** au lieu d’**Office 365**.

* Utilisez le langage suivant pour décrire le fonctionnement de l’application avec Teams (ou Microsoft 365) :
  * **« ... fonctionne avec Microsoft Teams. »**
  * **« ... fonctionner avec Microsoft Teams. »**
  * **« ... dans Microsoft Teams. »**
  * **« ... pour Microsoft Teams. »**
  * **« ... intégré à Microsoft Teams. »**
  * **... conçu pour...**
  * **... développé pour...**
  * **« ... conçu pour... »**

**À ne pas faire**

[*Correction obligatoire*]

* Supérieure à 500 mots.
* Abrégez **Microsoft** en tant que **MS** ou **MSFT**.

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-microsoft-abbreviated.png" alt-text="Le graphique montre un exemple d’abréviation de Microsoft en tant que MS ou MSFT pour la première fois dans la description de l’application.":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-microsoft-not-abbreviated.png" alt-text="Le graphique montre un exemple de non-abréviation de Microsoft en tant que MS ou MSFT pour la première fois dans la description de l’application.":::

* Indiquez que l’application est une offre de Microsoft, y compris à l’aide de slogans ou d’accroches Microsoft.

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-offering-from-microsoft.png" alt-text="Le graphique montre un exemple montrant comment ne pas indiquer l’offre Microsoft dans la description de l’application.":::

   :::image type="content" source="../../../../assets/images/submission/validation-app-description-no-offering-indication-from-microsoft.png" alt-text="Graphique montrant un exemple d’écriture d’une description d’application sans utiliser de slogans et de slogans Microsoft.":::

* Utilisez la langue suivante, sauf si vous êtes un partenaire Microsoft certifié :
  * **« ... certifié pour ... »**
  * **« ... optimisé par ... »**
* Inclure les fautes de frappe, les erreurs grammaticales.
* Mettez inutilement en majuscule l'intégralité du manifeste, la description longue AppSource ou le contenu de l'application.

   :::image type="content" source="../../../../assets/images/submission/validation-long-description-typos-pass.png" alt-text="Le graphique montre un exemple de description longue de l’application sans erreurs.":::

   :::image type="content" source="../../../../assets/images/submission/validation-long-description-typos-fail.png" alt-text="Le graphique montre un exemple de description longue de l’application avec des fautes de frappe et des erreurs.":::

* Incluez des liens vers AppSource.

  :::image type="content" source="../../../../assets/images/submission/validation-app-description-link-to-appsource.png" alt-text="Le graphique montre un exemple de scénario d’échec avec des liens vers AppSource dans une description longue de l’application.":::

* Faire des réclamations non vérifiées. Par exemple, meilleur, premier et classé, à moins que cela ne vienne avec la source de la réclamation.
* Comparez votre offre avec d’autres offres du marché.

</details>

### <a name="screenshots"></a>Captures d’écran

Les captures d’écran fournissent un aperçu visuel évident de votre application pour compléter le nom, l’icône et les descriptions de votre application.
<br></br>
<details><summary>Développer pour en savoir plus</summary>

N'oubliez pas ce qui suit :

* Vous pouvez avoir jusqu’à cinq captures d’écran par référencement.
* Les types de fichiers pris en charge sont PNG, JPEG et GIF.
* Les dimensions doivent être de 1366x768 pixels.
* Taille maximale de 1 024 Ko.

**À faire :**

* Focus on your app's capabilities. For example, how people can communicate with your bot.
* Incluez du contenu qui représente précisément votre application.
* Utilisez le texte judicieusement.
* Cadrez les captures d'écran avec une couleur qui reflète votre marque et incluez du contenu marketing.
* Utilisez des captures d’écran haute résolution qui sont nettes et contiennent du texte lisible et lisible. [*Correction obligatoire*]
* Utilisez des maquettes qui décrivent avec précision l’interface utilisateur réelle de l’application pour le bénéfice des utilisateurs finaux. [*Correction obligatoire*]
* Fournissez au moins trois captures d’écran dans la liste de la Place de marché de votre application.
* Si votre application Teams est extensible à d’autres hubs Microsoft 365, les captures d’écran fournies doivent représenter les fonctionnalités de l’application dans d’autres hubs Microsoft 365.
* Au moins une capture d’écran doit représenter les fonctionnalités de votre application sur les appareils mobiles.
* Nous vous recommandons de fournir des légendes dans vos captures d’écran pour permettre à l’utilisateur de comprendre clairement la fonctionnalité de l’application.

**À ne pas faire**

* Incluez des maquettes qui reflètent de façon inexacte l’interface utilisateur réelle de votre application, comme l’affichage de votre application utilisée en dehors de Teams.

> [!TIP]
>
> * Une vidéo peut être le moyen le plus efficace de communiquer pourquoi les gens doivent utiliser votre application. Une vidéo est également la première chose que les utilisateurs voient dans votre annonce.
> * Si vous choisissez de fournir une vidéo dans votre liste d’applications, vous devez désactiver les publicités dans les paramètres YouTube ou Vimeo avant de soumettre le lien vidéo dans l’Espace partenaires. Les vidéos fournies dans la liste des applications ne doivent pas dépasser 90 secondes et doivent uniquement représenter les fonctionnalités et l’intégration de l’application à Microsoft Teams. Pour plus d’informations, voir [créer une vidéo pour votre référencement de magasin](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video).

</details>

### <a name="privacy-policy"></a>Déclaration de confidentialité

[*Correction obligatoire*]

La politique de confidentialité peut être spécifique à votre application Teams ou à une stratégie globale pour tous vos services.

* Si vous utilisez un modèle de politique de confidentialité générique, vous devez ajouter une référence aux **services**, **applications**, ou **plateformes dans le cadre de votre politique de confidentialité**. Vous n'avez pas besoin de spécifier votre application Teams dans la portée, si vous incluez une référence aux **services**, **applications** et **plateformes**. Le processus de validation de l'application interprétera ces références pour inclure votre application Teams avec vos autres services ou sites Web.
* Doit inclure la façon dont vous traitez le stockage, la rétention et la suppression des données utilisateur. Vous devez décrire les contrôles de sécurité pour la protection des données.
* Doit inclure vos informations de contact.
* Ne doit pas inclure d'URL cassées ou à des fins de bêta ou de transfert.
* Ne doit pas inclure de liens vers AppSource.
* Ne doit pas exiger d'authentification pour accéder à la politique de confidentialité.
* Ne doit pas inclure d'interface utilisateur de commerce ou de liens de magasin.

### <a name="terms-of-use"></a>Conditions d’utilisation

[*Correction obligatoire*]

Utilisez les directives suivantes pour rédiger les conditions d'utilisation :

* Doit être spécifique et applicable à votre offre.
* Doit être hébergé sur votre propre domaine.
* Doit avoir un lien sécurisé (HTTPS).
* L'accès aux Conditions d'utilisation ne doit pas nécessiter d'authentification.

### <a name="support-links"></a>Liens vers le support technique

[*Correction obligatoire*]

Les URL d'assistance de votre application ne doivent pas nécessiter d'authentification. Par exemple, les utilisateurs ne doivent pas se connecter pour vous contacter.
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Les URL d'assistance doivent inclure vos coordonnées ou une voie à suivre pour que les utilisateurs créent un ticket d'assistance. Par exemple, si votre URL d'assistance est hébergée sur GitHub, la page GitHub doit être votre propriété et doit inclure vos coordonnées ou une voie à suivre pour que les utilisateurs créent un ticket d'assistance.

:::image type="content" source="../../../../assets/images/submission/validation-supportlinks-authentication.png" alt-text="validation-support-links-auth":::

</details>

### <a name="localization"></a>Localisation

[*Correction obligatoire*]

* Si votre application prend en charge la localisation, votre package d’application doit inclure un fichier avec des traductions linguistiques qui s’affichent en fonction du paramètre de langue Teams. Le fichier doit être conforme au schéma de localisation Teams. Pour plus d'informations, consultez [Schéma de localisation Teams](~/concepts/build-and-test/apps-localization.md).

* Le contenu des métadonnées d’application doit être identique dans et dans `en-us` d’autres langages de localisation. [*Correction obligatoire*]

* Les langues prises en charge doivent être affichées dans la description de l’application AppSource. Par exemple, cette application est disponible en X (X= langue localisée). [*Correction obligatoire*]

* Si les paramètres client de l’utilisateur ne correspondent à aucune de vos langues supplémentaires, la langue par défaut est utilisée comme langue de secours finale. Mettez à jour la `localizationInfo` propriété avec la langue par défaut correcte prise en charge par votre application. [*Correction obligatoire*]

* Mettez à jour la `localizationInfo` propriété avec la langue par défaut correcte prise en charge par votre application ou ajoutez du contenu localisé pour le manifeste et la description longue et courte de l’Espace partenaires. [*Correction obligatoire*]

## <a name="apps-linked-to-saas-offer"></a>Applications liées à l'offre SaaS

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png"::: Cette section est conforme à la [Stratégie du marché commercial Microsoft numéro 1140.5](/legal/marketplace/certification-policies?branch=pr-en-us-5673). Si vous créez une application Teams liée à une offre SaaS, assurez-vous qu’elle respecte ces instructions.
<br></br>
<details><summary>Général</summary>

* Les ISV doivent prendre en charge la possibilité pour plusieurs utilisateurs (abonnés) d'un même locataire de gérer leur propre abonnement et d'attribuer des licences aux utilisateurs du locataire.
* L'offre doit répondre à toutes les [exigences techniques](/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/include-saas-offer) des applications Teams liées à une offre SaaS.
* Les applications Teams liées à l'offre SaaS doivent répondre à toutes les exigences définies dans [1000 Software as a Service (SaaS)](/legal/marketplace/certification-policies#1000-software-as-a-service-saas).
* `subscriptionOffer` détails mentionnés dans le fichier manifeste doivent être corrects. Dans le manifeste de votre application, ajoutez ou mettez à jour le nœud `subscriptionOffer` avec la valeur `publisherId.offerId`. Par exemple, si votre ID d'éditeur est `contoso1234` et que votre ID d'offre est `offer01`, la valeur que vous spécifiez dans le manifeste de votre application doit être `contoso1234.offer01`.
* L'offre SaaS liée à l'application Teams doit être en ligne dans AppSource et les offres d'aperçu ne sont pas acceptées pour l'approbation du magasin.

</details>

</br>
<details><summary>Métadonnées d’offre</summary>

* Les métadonnées de l'offre doivent correspondre dans le manifeste Teams, la liste des applications Teams dans AppSource et l'offre SaaS dans AppSource.
* L'application Teams et l'offre SaaS doivent provenir du même éditeur ou développeur. L'offre SaaS référencée dans le manifeste de l'application doit appartenir au même éditeur que l'application Teams est soumise à la place de marché commerciale.
* Étant donné que votre offre soumise est une application Teams liée à l'offre SaaS, vous devez sélectionner **Achats supplémentaires** sur **Oui, mon produit nécessite l'achat d'un service ou propose des achats intégrés supplémentaires** dans la section de configuration des produits du Centre des partenaires de votre liste d'offres.
* Les descriptions des forfaits et les détails des prix doivent fournir suffisamment d'informations pour que les utilisateurs comprennent clairement les listes d'offres.
* Toutes les limitations, dépendances vis-à-vis des services supplémentaires et exceptions aux fonctionnalités proposées doivent être clairement indiquées dans les descriptions des plans.
* Les applications Teams liées à l'offre SaaS sont conçues pour prendre en charge les licences attribuées sur une base nommée, par utilisateur. Parfois, l'offre SaaS est construite avec d'autres méthodes ou a des flux d'achat spécialisés. Vous devez clairement mentionner dans les métadonnées de l'application et les détails du plan d'abonnement sur la méthode et les flux d'achat.
* L'offre SaaS doit fournir des messages et des conseils à tous les utilisateurs dans tous les états applicables du flux d'achat.

</details>
</br>

<details><summary>Page d'accueil de l'offre SaaS et gestion des licences</summary>

* Fournir une introduction aux abonnés sur la façon d'utiliser le produit.
* Autoriser l'abonné à attribuer des licences.
* Fournissez différentes façons de prendre en charge les problèmes, tels que les questions fréquentes (FAQ), les base de connaissances et les e-mails.
* Validez les utilisateurs pour vous assurer qu'ils n'ont pas déjà une licence attribuée par un autre utilisateur.
* Notifier les utilisateurs après l'attribution de la licence.
* Guidez les utilisateurs sur la façon d’ajouter l’application à Teams et de bien démarrer par le biais d’un chat bot ou d’un e-mail Teams.

</details>
</br>

<details><summary>Convivialité et fonctionnalité</summary>

* Une fois l'achat et l'attribution des licences réussis, vous devez fournir les éléments suivants :
  * Accès aux utilisateurs pour les fonctionnalités du plan souscrit.
  * Valeur ajoutée et avantages significatifs du plan d'abonnement pour les utilisateurs.
  * À partir de votre application Teams, fournissez un lien vers la page d'accueil de l'application SaaS pour que les abonnés puissent gérer les licences à l'avenir.

</details>
</br>

<details><summary>Configurer et tester l'application SaaS</summary>

Si la configuration de votre application à des fins de test est complexe, fournissez un document fonctionnel de bout en bout, des étapes de configuration de l’offre SaaS liée et des instructions pour la gestion des licences et des utilisateurs dans le cadre de vos *notes de certification*.

> [!TIP]
> Vous pouvez ajouter une vidéo sur le fonctionnement de votre application et de la gestion des licences pour aider l'équipe à effectuer les tests.

</details>

## <a name="tabs"></a>Onglets

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4.2 du marché commercial de Microsoft](/legal/marketplace/certification-policies#114042-tabs).
Si votre application inclut un onglet, assurez-vous qu’elle respecte ces instructions.
> [!TIP]
> Pour plus d'informations sur la création d'une expérience d'application de haute qualité, consultez les [directives de conception de l'onglet Teams](~/tabs/design/tabs.md).

</br>
<details><summary>Configuration</summary>

* La configuration de l'onglet **ne doit pas s'arrêter** un nouvel utilisateur. Fournissez un message sur la façon d’effectuer l’action ou le flux de travail. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-new-user.png" alt-text="Le graphique montre un exemple de tabulation avec un point mort lors de l’installation.":::

* L’utilisateur ne doit pas laisser l’expérience de configuration de l’onglet dans Teams pour créer du contenu en dehors de Teams, puis revenir à Teams pour l’épingler. L'écran de configuration de l'onglet doit expliquer la valeur de la configuration et comment configurer. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-profile-name.png" alt-text="validation-tabs-set-up-profile-name":::

* Tab configuration screen must not embed an entire website. Keep your configuration experience focused. For example, if you're building a project management app that lets users configure a project in a channel, keep the tab configuration screen focused on allowing the user to select a project from your app to configure in the channel. [*Mandatory Fix*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-experience.png" alt-text="validation-tabs-setup-configuration-exp":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-screen.png" alt-text="validation-tabs-set-up-configuration-screen":::

* Les applications qui nécessitent que les utilisateurs entrent une URL lors de la configuration d’un onglet doivent :
  * Fournissez un guide de transfert approprié pour l’utilisateur afin d’acquérir ou de générer l’URL. [*Correction obligatoire*]
  * Recherchez l’URL appropriée ou appropriée aux fonctionnalités de l’application conformément à la description de l’application. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-tab-configuration-way-forward-url-pass.png" alt-text="Capture d’écran montrant un exemple de configuration d’onglet avec un moyen pour l’utilisateur de générer une URL.":::
  
    :::image type="content" source="../../../../assets/images/submission/validation-tab-configuration-way-forward-url-fail.png" alt-text="Capture d’écran montrant un exemple de configuration d’onglet sans chemin d’accès permettant à l’utilisateur de générer une URL.":::

* Créez un lien hypertexte entre les informations nous contactant dans l’écran de configuration au lieu d’un texte brut pour aider les utilisateurs à vous contacter pour les exigences de support. [*Correction obligatoire*]

* Pour une expérience utilisateur de première exécution transparente, nous vous recommandons de faire un lien hypertexte entre votre URL de support ou votre e-mail dans l’écran de configuration. [*Correctif suggéré*]

</details>
</br>

<details><summary>Affichages</summary>

* The sign in screen area must not use large logos. [*Mandatory Fix*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-applogin.png" alt-text="validation-views-app-login":::

* Le contenu peut être simplifié en le décomposant sur plusieurs onglets.

    :::image type="content" source="../../../../assets/images/submission/validation-views-multiple-tabs.png" alt-text="val-views-multiple-tabs":::

* Les onglets ne doivent pas avoir d'en-tête en double. Supprimez les logos dupliqués de l’image I, car l’infrastructure de tabulation affiche déjà l’icône et le nom de l’application. [*Correctif suggéré*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-no-duplicate-header-logo.png" alt-text="Le graphique montre un exemple d’onglet sans en-têtes et logos en double.":::

    :::image type="content" source="../../../../assets/images/submission/validation-views-duplicate-header-logo.png" alt-text="Le graphique montre un exemple d’onglet avec des en-têtes et des logos en double.":::

</details>
</br>

<details><summary>Navigation</summary>

Voici les directives de navigation :

* Les onglets ne doivent pas fournir de navigation en conflit avec la principale navigation de Teams. Si vous fournissez une navigation à gauche dans votre onglet, elle ne doit pas inclure uniquement des icônes ou des icônes avec du texte empilé. Il ne doit pas s'agir d'un rail pliable avec la possibilité de voir des icônes avec du texte empilé (imitant la barre de navigation Teams). Incluez des icônes avec du texte en ligne ou uniquement du texte ou utilisez des menus hamburger au lieu du rail gauche de l'onglet. [*Correction obligatoire*]

Concevez votre application avec des composants Fluent UI [de base](~/concepts/design/design-teams-app-basic-ui-components.md) et [avancés](~\concepts\design\design-teams-app-advanced-ui-components.md).

:::image type="content" source="../../../../assets/images/submission/validation-navigation-static-tab.png" alt-text="Le graphique montre un exemple de navigation dans un onglet qui n’entre pas en conflit avec la navigation Teams principale.":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-left-navigation.png" alt-text="Le graphique montre un exemple de rail de navigation gauche en conflit avec la navigation Teams principale.":::

* Les onglets avec barre d’outils dans le rail gauche doivent laisser un espacement de 20 pixels à partir de la navigation à gauche de Teams. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-spacing-between-toolbar.png" alt-text="validation-nav-spacing-between-toolbar":::

* Les pages secondaires et tertiaires d’un onglet doivent être ouvertes dans une vue de niveau 2 (L2) et de niveau 3 (L3) dans la zone de l’onglet principal, qui est parcourue via une barre de navigation ou une navigation à gauche. Vous pouvez également utiliser les composants suivants pour faciliter la navigation dans un onglet :
  * Boutons Retour
  * En-têtes de page
  * Menus d’hamburger

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-improper-navigation-leveles.png" alt-text="Capture d’écran montrant un exemple de boîte de dialogue en réunion avec plusieurs niveaux de navigation.":::

* Les liens profonds dans les onglets ne doivent pas être liés à une page Web externe mais au sein de Teams. Par exemple, les modules de tâche ou d’autres onglets. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-view-button-not-linked-static-tab.png" alt-text="validation-nav-view-button-not-linked-static-tab":::

* Les onglets ne doivent pas permettre aux utilisateurs de naviguer en dehors de Teams pour l'expérience de l'application principale. Les onglets peuvent rediriger en dehors des équipes pour les flux de travail non essentiels. Par exemple, pour créer un ticket d'assistance. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-within-configuration.png" alt-text="validation-nav-core-workflow-within-configuration":::

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-redirects-outside.png" alt-text="validation-nav-core-workflow-redirects-outside":::

* Le défilement horizontal ne doit pas être présent dans un onglet en réunion. [*Correctif obligatoire*]

* Les dialogues en réunion utilisés dans votre application ne doivent pas autoriser le défilement horizontal. Utilisez les dialogues en réunion avec parcimonie et pour les scénarios légers et orientés tâches. Vous pouvez spécifier la largeur de l’image I de la boîte de dialogue en réunion dans la plage de tailles prise en charge pour prendre en compte différents scénarios. [*Correction obligatoire*]
* Les modules de tâches utilisés dans votre application ne doivent pas autoriser le défilement horizontal. Les modules de tâche vous permettent de sélectionner différentes tailles pour rendre le contenu réactif sans avoir besoin de défilement horizontal. Si nécessaire, vous pouvez utiliser une vue d’étape (un composant d’interface utilisateur plein écran pour exposer votre contenu web) pour terminer le flux de travail sans défilement horizontal. [*Correction obligatoire*]

* Le défilement horizontal présent dans l’onglet d’une conversation personnelle, d’un canal et d’un onglet de détails en réunion dans n’importe quelle étendue n’est pas autorisé si l’intégralité du canevas d’onglet peut faire défiler, sauf si votre onglet utilise un canevas infini avec des éléments d’interface utilisateur fixes. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-allowed-scenarios.png" alt-text="Le graphique montre des exemples de tous les scénarios mobiles où le défilement horizontal est autorisé.":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-allowed-kanban.png" alt-text="Le graphique montre un exemple de défilement horizontal dans le tableau Kanban.":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-list-view-components.png" alt-text="Le graphique montre un exemple d’affichage de liste avec de nombreux composants.":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-fixed-board.png" alt-text="Le graphique montre un exemple de défilement horizontal dans un tableau blanc avec un canevas infini et un tableau fixe.":::

   :::image type="content" source="../../../../assets/images/submission/validation-horizontal-scroll-in-list-view.png" alt-text="Le graphique montre un exemple de défilement horizontal en mode liste.":::

* Le défilement horizontal dans les cartes adaptatives ne doit pas être présent dans Teams. [*Correction obligatoire*]

* Le rail inférieur utilisé pour la navigation dans les onglets ne doit pas entrer en conflit avec la navigation des applications mobiles natives Teams. [*Correction obligatoire*]

  :::image type="content" source="../../../../assets/images/submission/validation-tab-bottom-rail-conflicts-with-teams-mobile.png" alt-text="Le graphique montre un exemple d’onglet en conflit avec la navigation des applications mobiles natives Teams.":::

</details>
</br>

<details><summary>Facilité d’utilisation</summary>

* Les onglets doivent apporter une valeur au-delà de l'hébergement d'un site Web existant. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-provides-workflows.png" alt-text="Le graphique montre un exemple d’application avec un flux de travail précieux pour canaliser les membres au sein d’une équipe.":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-website-i-framed.png" alt-text="Le graphique montre un exemple d’application avec un site web entier dans un I-frame sans option back.":::

* Le contenu ne doit pas être tronqué ou se chevaucher dans l'onglet.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-content-truncation.png" alt-text="validation-usability-content-truncations":::

* Les utilisateurs doivent pouvoir annuler leur dernière action dans l’onglet.

* Les onglets dans un contexte personnel peuvent agréger le contenu des instances partagées de l’application. Par exemple, une application de gestion de projet avec un onglet configurable qui permet aux membres du canal de commenter le projet sur des cartes Kanban, doit agréger ce contenu et s'afficher dans l'application personnelle. [*Correctif suggéré*]

* Les onglets doivent répondre aux thèmes de Teams. Lorsqu’un utilisateur modifie le thème, le thème de l’application doit refléter la sélection.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-responsive-tabs.png" alt-text="Le graphique montre un exemple d’onglet réactif à un thème dans Teams.":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-unresponsive-tabs.png" alt-text="Le graphique montre un exemple de tabulation qui ne répond pas au thème dans Teams.":::

* Les onglets doivent utiliser des composants de style Teams tels que les polices Teams, les rampes de type, les palettes de couleurs, le système de grille, le mouvement, le ton de la voix, dans la mesure du possible. Pour plus d'informations, consultez les [instructions de conception des onglets](/microsoftteams/platform/tabs/design/tabs). [*Correctif suggéré*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-uses-diff-font.png" alt-text="Capture d’écran montrant un exemple d’onglet avec une police calibri au lieu de la police Teams native.":::

* Si la fonctionnalité de votre application nécessite des modifications des paramètres, incluez un onglet **Paramètres**. [*Correction suggérée*]
* Les onglets doivent suivre la conception de l’interaction Teams, par exemple, la navigation dans la page, la position et l’utilisation des dialogues, des hiérarchies d’informations. Pour plus d’informations, consultez le [kit d’interface utilisateur Fluent de Microsoft Teams](~/concepts/design/design-teams-app-basic-ui-components.md).

* Les expériences d'onglet doivent être entièrement réactives sur mobile (Android et iOS).

   > [!TIP]
   >
   > * Incluez un bot personnel avec un onglet personnel.
   > * Autorisez les utilisateurs à partager du contenu à partir de leur onglet personnel.

* L’onglet ne doit pas contenir d’éléments qui obstruent ou entravent complètement les flux de travail dans l’onglet. Par exemple, bot à l’intérieur d’un onglet qui ne peut pas être réduit.

   :::image type="content" source="../../../../assets/images/submission/validation-tab-elements-impede-workflow.png" alt-text="Le graphique montre un exemple d’onglet avec des éléments qui entravent les flux de travail dans l’onglet.":::

* L’onglet ne doit pas avoir de fonctionnalité interrompue. Votre offre doit être une solution logicielle utilisable et doit fournir les fonctionnalités, fonctionnalités et livrables, comme décrit dans votre liste et d’autres documents connexes. [*Correction obligatoire*]

* Si vos onglets contiennent un pied de page, veillez à supprimer du pied de page tous les liens non liés aux fonctionnalités de l’application.

</details>
</br>

<details><summary>Sélection de l’étendue</summary>

* Le contenu de la page de destination des onglets configurables ne doit pas être limité à une utilisation individuelle et ne doit pas inclure de contenu personnel tel que **Mes tâches** ou **Mon tableau de bord**.

   :::image type="content" source="../../../../assets/images/submission/validation-configurable-tab-content-personal-scope.png" alt-text="Le graphique montre un exemple de contenu dans un onglet configurable avec une étendue personnelle telle que Mes tâches ou Mon tableau de bord.":::

* Après l’expérience de configuration, la page d’accueil doit afficher une vue collaborative pour l’ensemble de l’équipe.

* Si votre application nécessite la fourniture d'une vue d'étendue personnelle pour que l'utilisateur améliore l'efficacité ou la productivité sur le lieu de travail, utilisez des vues filtrées, des liens profonds vers des applications personnelles ou accédez aux vues L2 ou L3 dans l'onglet configurable et gardez la page de destination contextuellement la même pour tous les utilisateurs.

* Le contenu de la page de destination des onglets configurables doit être contextuellement identique pour tous les membres de la chaîne.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-tab-personal-info.png" alt-text="Le graphique montre un exemple de contenu dans la page d’accueil des onglets configurables contextuelment différents pour tous les membres.":::

* Les onglets configurables doivent avoir des fonctionnalités ciblées.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-nested-tabs.png" alt-text="onglet validation-usability-configurable-nested-tab":::

</details>
<br/>

## <a name="bots"></a>Bots

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4.3 du marché commercial de Microsoft](/legal/marketplace/certification-policies#114043-bots).

Si votre application inclut un bot, assurez-vous qu’elle respecte ces instructions.

> [!TIP]
> Pour plus d'informations sur la création d'une expérience d'application de haute qualité, consultez les [directives de conception de bot Teams](~/bots/design/bots.md).

</br>
<details><summary> Lignes directrices pour la conception du Bot </summary>

* Votre application Teams doit suivre [les instructions de conception de bot Teams](../../../../bots/design/bots.md).

* Vous devez implémenter un module de tâche pour éviter la réponse multitour du bot lorsque le flux de travail implique l’utilisateur effectuant des tâches répétitives. Par exemple, utilisez un module de tâche pour capturer de façon répétitive le nom, le dob, l’emplacement et la désignation au lieu d’utiliser des conversations à plusieurs tours. [*Correction obligatoire*]

* Tous les liens, réponses ou flux de travail rompus dans votre application doivent être corrigés. [*Correction obligatoire*]

</details>

</br>
<details><summary>Commandes de bot</summary>

Analyzing user input and predicting user intent is difficult. Bot commands provide users a set of words or phrases for your bot to understand.

* Vous devez répertorier au moins une commande de bot prise en charge dans la `{commandList}` section du manifeste de votre application. Ces commandes s’affichent dans la zone de rédaction lorsqu’un utilisateur tente d’envoyer un message à votre bot.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-listed.png" alt-text="Le graphique montre un exemple de commandes de bot répertoriées dans le manifeste de l’application.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-not-listed.png" alt-text="Le graphique montre un exemple de commandes de bot non répertoriées dans le manifeste de l’application.":::

* Toutes les commandes prises en charge par votre bot doivent fonctionner correctement, y compris les commandes génériques telles que **Hi**, **Hello** et **Help**.
  
  :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-generic-response-pass.png" alt-text="Le graphique montre un exemple de bot répondant à des commandes génériques.":::

  :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-generic-no-response.png" alt-text="Le graphique montre un exemple de bot sans réponse aux commandes génériques.":::

* Les commandes de bot ne doivent pas conduire un utilisateur dans une impasse, les commandes doivent toujours fournir une voie à suivre.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-deadend.png" alt-text="validation-bot-commands-dead-end":::

* Vous devez répertorier au moins une commande de bot valide dans la `items.commands.title` section du manifeste et ajouter une description appropriée qui donne de la clarté à l’utilisateur sur la commande bot et son utilisation. Les commandes de bot répertoriées dans la `commandLists` section de l’aire de manifeste en tant que commandes préremplies dans le menu de commandes du bot fournissent un moyen d’avancer pour permettre au nouvel utilisateur d’interagir avec le bot. [*Correction obligatoire*]

* La réponse du bot ne doit pas contenir d’images ou d’avatars de produit Microsoft officiels. Utilisez vos propres ressources dans votre application. L’utilisation d’images de produit Microsoft dans votre application n’est pas autorisée. Vous ne pouvez copier, modifier, distribuer, afficher, concéder ou vendre des images de produit protégées par des droits d’auteur Microsoft que si vous disposez d’une autorisation explicite dans le cadre du contrat de licence End-User (CLUF), des termes du contrat de licence qui accompagnent le contenu, ou dans [les instructions de marque et de marque Microsoft](https://www.microsoft.com/legal/intellectualproperty/trademarks). [*Correction obligatoire*]

* Les bots doivent répondre aux commandes utilisateur sans afficher d’indicateur de chargement continu. [*Correction obligatoire*]

* La réponse de la commande d’aide du bot ne doit pas rediriger l’utilisateur en dehors de Teams. La réponse à la commande d’aide du bot peut rediriger l’utilisateur vers un canevas au sein de l’application Teams ou fournir une réponse de progression dans une carte adaptative. [*Correction obligatoire*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-redirects-user-outside-teams.png" alt-text="Le graphique montre un exemple de réponse de bot redirigeant l’utilisateur en dehors de Teams.":::

* Les bots doivent toujours fournir une réponse valide à une entrée utilisateur, même si l’entrée n’est pas pertinente ou incorrecte. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-valid-improper-input.png" alt-text="Le graphique montre un exemple de réponse valide pour une commande de bot incorrecte.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-improper-response-invalid-command.png" alt-text="Le graphique montre un exemple de réponse non valide pour une commande de bot incorrecte.":::

* Les caractères spéciaux tels que la barre oblique (**/**) ne doivent pas être préfixés pour les commandes du bot. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-special-characters.png" alt-text="Le graphique montre un exemple de scénario d’échec dans lequel des caractères spéciaux sont préfixés de commandes de bot.":::

* Les bots doivent fournir une réponse valide aux commandes utilisateur non valides. Les bots ne doivent pas arrêter l’utilisateur ou afficher une erreur si un utilisateur envoie une commande de bot non valide. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-way-forward-for-invalid-command.png" alt-text="Le graphique montre un exemple de bot fournissant un moyen d’avancer pour une commande non valide.":::

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-bot-dead-end-invalid-command.png" alt-text="Le graphique montre un exemple de scénario d’échec où un bot envoie une même réponse pour une commande valide et non valide.":::

* La fonctionnalité du bot doit être pertinente pour l’étendue dans laquelle le bot est installé et le bot doit fournir une valeur dans l’étendue installée. [*Correction obligatoire*]

* Les bots ne doivent pas contenir de commandes en double. [*Correction obligatoire*]

* Les bots ne doivent pas afficher d’indicateur de saisie après avoir répondu à la commande utilisateur, mais peuvent afficher un indicateur de saisie lors de la réponse à la commande utilisateur. [*Correction obligatoire*]

* Les bots doivent fournir une réponse valide à la commande **d’aide** tapée en minuscules ou en majuscules qui fournit à l’utilisateur un moyen d’avancer ou permet à l’utilisateur d’accéder au contenu d’aide lié à l’utilisation du bot. Les bots doivent fournir une réponse valide même si l’utilisateur n’a pas ouvert de session sur l’application. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-valid-response-lowercase.png" alt-text="Le graphique montre un exemple de bot qui ne fournit pas de réponse valide pour une commande en minuscules ou en majuscules.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-valid-response-logged-app.png" alt-text="Le graphique montre un exemple de bot sans réponse valide lorsque l’utilisateur ne s’est pas connecté à l’application.":::

* Les bots doivent fournir une réponse valide pour **la commande d’aide** .

   :::image type="content" source="../../../../assets/images/submission/validation-bot-help-command.png" alt-text="Le graphique montre un exemple de bot qui envoie une réponse valide à la commande d’aide.":::

* Les réponses de bot sur mobile doivent être réactives sans aucune troncation des données qui entrave l’utilisation du bot de l’utilisateur final pour terminer les workflows souhaités. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-no-truncate-mobile.png" alt-text="Le graphique montre un exemple de message de bot sans tronquer sur un appareil mobile.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-response-truncate-mobile.png" alt-text="Le graphique montre un exemple de tronquement d’un message de bot sur un appareil mobile.":::

* Tous les liens d’une carte adaptative de réponse de bot doivent être réactifs. Tout lien qui amène l’utilisateur en dehors de la plateforme Teams doit avoir un texte de redirection clair, tel que **« Afficher dans ».** ou **Cette façon de..**, une icône contextuelle dans le bouton d’action de réponse du bot, ou un texte de redirection approprié dans le corps du message de réponse du bot. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-action-button-redirect-warning.png" alt-text="Le graphique montre un exemple de bouton d’action de réponse de bot avec une redirection.":::

* Par défaut, si votre bot ne répond pas ou ne prend en charge aucune commande utilisateur et qu’il s’agit d’un bot unidirectionnel destiné uniquement à avertir les utilisateurs. Vous devez définir `isNotificationOnly` sur true dans le manifeste. [*Correction obligatoire*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-command-isnotification-only-true.png" alt-text="Le graphique montre un exemple de propriété notification uniquement définie sur true dans le manifeste de l’application.":::

  :::image type="content" source="../../../../assets/images/submission/validation-bot-command-isnotification-only-not-true.png" alt-text="Le graphique montre un exemple de bot de notification uniquement qui ne répond pas au message d’un utilisateur.":::

* L’expérience utilisateur du bot ne doit pas être interrompue sur les plateformes mobiles. Votre bot doit être entièrement réactif sur mobile. [*Correction obligatoire*]

> [!TIP]
> Pour les bots personnels, incluez un onglet **Aide** qui décrit davantage ce que votre bot peut faire.

</details>
</br>

<details><summary>Messages de bienvenue du bot</summary>

* Si l'application a un flux de configuration complexe (nécessite une licence d'entreprise ou manque d'un flux d'inscription intuitif), les robots de ces applications doivent toujours envoyer un message de bienvenue lors de la première exécution.

  Pour une expérience optimale, le message d’accueil doit inclure la valeur offerte par le bot aux utilisateurs, qui ont installé le bot dans le canal, comment configurer le bot et décrire brièvement toutes les commandes de bot prises en charge. Vous pouvez afficher le message de bienvenue à l'aide d'une carte adaptative avec des boutons pour une meilleure convivialité. Pour plus d’informations, voir [comment déclencher un message de bienvenue du bot](~/bots/how-to/conversations/send-proactive-messages.md). Pour les applications sans flux de configuration complexe, vous pouvez choisir de déclencher un message de bienvenue lors de la première exécution du bot. Cependant, si un message de bienvenue est déclenché, il doit suivre les instructions relatives aux messages de bienvenue.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message.png" alt-text="Le graphique montre un exemple de bot qui envoie un message de bienvenue lorsque le bot a un workflow de configuration complexe.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message.png" alt-text="Le graphique montre un exemple de bot qui n’envoie pas de message d’accueil lorsque le bot a un workflow de configuration complexe.":::

* Les messages d’accueil du bot dans les canaux et les conversations sont facultatifs lors de la première exécution, en particulier si le bot est disponible pour un usage personnel et effectue des actions similaires. Votre bot ne doit pas envoyer de messages de bienvenue aux utilisateurs individuellement (c'est considéré comme du [spam](#botmessagespamming)). Le message doit également mentionner la personne qui a ajouté le bot.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-not-triggered.png" alt-text="validation-bot-welcome-message-not-trigger":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-triggered.png" alt-text="validation-bot-wel-message-trigger":::

* Les bots de notification uniquement doivent envoyer un message de bienvenue qui précise que le bot est un bot de notification uniquement et que les utilisateurs ne pourront pas interagir avec le bot. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-notification-only-welcome-message-pass.png" alt-text="Le graphique montre un exemple de bot qui envoie un message de bienvenue indiquant qu’il s’agit d’un bot de notification uniquement.":::

* Le message d’accueil ne doit pas arrêter l’utilisateur. Le message de bienvenue doit inclure la valeur offerte par le bot aux utilisateurs qui ont installé le bot dans le canal, comment configurer le bot et décrire brièvement toutes les commandes de bot prises en charge. Vous pouvez afficher le message de bienvenue à l'aide d'une carte adaptative avec des boutons pour une meilleure convivialité. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-no-way-forward.png" alt-text="Le graphique montre un exemple de scénario d’échec dans lequel le bot n’a aucun moyen d’avancer pour l’utilisateur dans un message de bienvenue.":::

   :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-clear-way-forward.png" alt-text="Le graphique montre un exemple de message d’accueil du bot avec une voie claire pour que l’utilisateur termine la tâche.":::

* Le bot installé dans une étendue de conversation de canal ou de groupe ne doit pas envoyer de message de bienvenue proactif à tous les membres de l’équipe dans la conversation 1:1. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-send-proactive-message-to-all-members.png" alt-text="Le graphique montre un exemple de bot qui envoie un message de bienvenue proactif à tous les membres de l’équipe.":::

* Seul le bot de notification peut envoyer un message d’accueil proactif dans un canal uniquement si le message contient des informations importantes pour que tout utilisateur puisse terminer la configuration du bot ou précise les scénarios lorsque des notifications sont déclenchées. [*Correction obligatoire*]

* Le bot installé dans une étendue de conversation de canal ou de groupe ne doit pas envoyer de messages proactifs (pas seulement un message de bienvenue) qui ne sont pas pertinents pour tous les utilisateurs du canal ou de la conversation de groupe. Il doit plutôt envoyer des messages proactifs à l’utilisateur sur une conversation 1:1. [*Correction obligatoire*]

* Le bot installé dans un canal ou une étendue de conversation de groupe ne doit pas permettre aux utilisateurs de démarrer des flux de travail individuels. Les bots doivent effectuer des workflows individuels dans une conversation 1:1 avec l’utilisateur. [*Correction obligatoire*]

* Le message d’accueil du bot doit clairement faire ressortir les limitations liées à l’utilisation du bot dans l’étendue installée. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-messahe-with-app-limitation.png" alt-text="Le graphique montre un exemple de limitation d’application dans le message d’accueil du bot.":::

   :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-messahe-without-app-limitation.png" alt-text="Le graphique montre un exemple de bot sans limitation d’application dans un message de bienvenue.":::

* Le message d’accueil doit se déclencher automatiquement lors de l’installation de l’application dans une étendue personnelle. Si le bot n’envoie pas de message d’accueil dans une étendue personnelle, l’utilisateur est dirigé vers une impasse. Si l’application n’inclut pas de flux de travail de configuration complexe, il est facultatif pour le développeur de déclencher un message de bienvenue dans l’étendue du canal ou de la conversation de groupe. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message-in-personal-scope.png" alt-text="Le graphique montre un exemple de bot qui n’envoie pas automatiquement de message d’accueil dans l’étendue personnelle.":::

* Les messages d’accueil ne doivent se déclencher qu’une seule fois lors de l’installation du bot. Les messages d’accueil ne doivent pas se déclencher chaque fois que l’utilisateur appelle la commande d’aide. La réponse à la commande d’aide doit être ciblée pour inclure un moyen pour l’utilisateur d’accéder à l’aide relative au bot. [*Correction obligatoire*]

* Les messages d’accueil ne doivent pas se déclencher avec chaque commande de bot. Il s’agit d’un courrier indésirable. [*Correction obligatoire*]

  :::image type="content" source="../../../../assets/images/submission/validation-welcome-message-trigger-for-any-command.png" alt-text="Le graphique montre un exemple de bot déclenchant un message de bienvenue pour n’importe quelle commande.":::

* Le contenu du message de bienvenue doit être lié au flux de travail du bot mentionné dans la description longue de l’application et l’étendue de l’installation. Le message de bienvenue doit inclure la valeur offerte par le bot aux utilisateurs qui ont installé le bot dans le canal, comment configurer le bot et décrire brièvement toutes les commandes de bot prises en charge. [*Correction obligatoire*]

* Le bot ne doit pas envoyer plusieurs messages d’accueil lorsqu’il est déclenché lors de l’installation de l’application. [*Correction obligatoire*]

  :::image type="content" source="../../../../assets/images/submission/validation-bot-multiple-message-trigger-install.png" alt-text="Le graphique montre un exemple de bot déclenchant plusieurs messages d’accueil lors de l’installation de l’application.":::

* Le nom de l’application dans le message d’accueil doit correspondre au nom de l’application dans le manifeste. [*Correction obligatoire*]

  :::image type="content" source="../../../../assets/images/submission/validation-app-name-mismatch-manifeast-and-welcome-message.png" alt-text="Le graphique montre un exemple de nom d’application dans le message de bienvenue qui ne correspond pas au nom de l’application dans le manifeste de l’application.":::

* Le message d’accueil ne doit pas afficher les noms de plateforme collaborative basés sur les conversations concurrentes, sauf si l’application fournit une interopérabilité spécifique.

* Le message d’accueil ne doit pas rediriger l’utilisateur vers une autre application Teams, mais le message de bienvenue doit pousser l’utilisateur à effectuer sa première tâche et décrire brièvement toutes les commandes de bot prises en charge dans l’application. [*Correction obligatoire*]

* Le message d’accueil ne doit pas contenir de liens vers une place de marché d’application, y compris AppSource. [*Correction obligatoire*]

* Si votre application a un flux de travail de configuration complexe qui nécessite une installation dirigée par l’administrateur, n’a pas de flux d’inscription intuitif et facilement disponible, ou nécessite que les utilisateurs effectuent des étapes de configuration en dehors de l’expérience Teams et retournent, le bot doit envoyer un message de bienvenue proactif dans une étendue de conversation d’équipe ou de groupe après l’installation. [*Correction obligatoire*]

* Si votre bot envoie un message de bienvenue dans le canal, il ne doit pas l’envoyer aux utilisateurs individuellement (il est considéré comme du spam). Le message d’accueil doit également mentionner la personne qui a ajouté le bot. [*Correctif suggéré*]

> [!TIP]
> Dans les messages de bienvenue aux utilisateurs individuels, une visite guidée du carrousel peut fournir un aperçu efficace de votre bot et de toutes les autres fonctionnalités de l'application pour encourager les utilisateurs à essayer les commandes du bot. Par exemple, **Créer une tâche**.

</details>
</br>

<details><summary><a id="botmessagespamming">Message de bot indésirables</a></summary>

Les bots ne doivent pas spammer les utilisateurs en envoyant plusieurs messages de courte durée.

* **Messages de bot dans les canaux et les conversations** : ne pas envoyer de courrier indésirable aux utilisateurs en créant des publications distinctes. Créez un billet unique avec des réponses dans le même fil de discussion.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-message-spamming-one-message.png" alt-text="validation-bot-message-spam-one-message":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-message-spamming-multiple-messages.png" alt-text="validation-bot-message-spam-multiple-message":::

* **Messages de bot dans les applications personnelles** :
  * N’envoyez pas plusieurs messages rapidement.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-multiple-message-quick-succession.png" alt-text="Le graphique montre un exemple de bot qui envoie plusieurs messages en succession rapide.":::

  * Envoyez un message avec des informations complètes.
  * Évitez les conversations à plusieurs tours pour terminer un seul flux de travail répétitif.
  * Utilisez un formulaire (ou un module de tâches) pour collecter toutes les entrées d'un utilisateur en même temps.
  * Les chatbots conversationnels basés sur la PNL peuvent utiliser une conversation à plusieurs tours pour rendre la discussion plus engageante et compléter un flux de travail.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-task-module.png" alt-text="validation-bot-message-using-task-module":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-mutliple-conversation.png" alt-text="Le graphique montre un exemple de bot utilisant des messages multitours pour terminer une conversation unique.":::

* **Messages de bienvenue** : Ne répétez pas le même message de bienvenue à intervalles réguliers. Par exemple, lorsqu’un nouveau membre est ajouté à une équipe, n’envoyez pas de courrier indésirable aux autres membres avec un message de bienvenue. Envoyez un message personnel au nouveau membre.

   :::image type="icon" source="../../../../assets/images/submission/validation-bot-send-proactive-message-to-all-members.png" alt-text="Le graphique montre un exemple de bot qui spamme les utilisateurs avec le même message de bienvenue.":::

</details>
</br>

<details><summary>Notifications de bot</summary>

Les notifications de bot doivent inclure du contenu pertinent pour l’étendue que vous définissez pour le bot (équipe, conversation ou personnel).

:::image type="content" source="../../../../assets/images/submission/validation-bot-notifications-relevant.png" alt-text="validation-bot-notification-relevant":::

:::image type="content" source="../../../../assets/images/submission/validation-bot-notifications-not-relevant.png" alt-text="validation-bot-notification-not-relevant":::

</details>
</br>
<details><summary>Bots et cartes adaptatives</summary>

Les cartes adaptatives sont une façon vivement recommandée d’afficher des messages de bot. Les cartes doivent être légères et ne comporter que six actions maximum. Pour afficher plus de contenu, pensez à utiliser un module de tâche ou un onglet.

Pour plus d'informations sur les cartes, consultez :

* [Conception de cartes adaptatives](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Référence de cartes](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

L'expérience du bot doit être entièrement réactive sur mobile. Les réponses des bots doivent fournir une voie à suivre, le cas échéant. Le bot doit être réactif et échouer avec un message d'erreur gracieux pour les échecs. Les messages de bot envoyés dans la portée personnelle à la base de l'utilisateur sur des déclencheurs dans une portée collaborative doivent fournir des informations contextuelles (y compris l'origine du message).

</details>
</br>

<details><summary>Notification uniquement pour les bots</summary>

Les applications constituées de robots de notification uniquement fournissent une valeur utilisateur en déclenchant des notifications utilisateur en fonction de certains déclencheurs ou événements dans l'application principale ou le backend. Par exemple, un nouveau prospect ou un nouveau prospect est ajouté pour le suivi de l'équipe commerciale. Un bot de notification de haute qualité avertit les utilisateurs régulièrement sur certaines saisies semi-automatiques d’événements, telles que les saisies semi-automatiques de workflow ou les alertes.

Une notification fournit de la valeur dans Teams si :

1. La carte ou le texte affiché fournit des détails adéquats ne nécessitant aucune autre action de l'utilisateur.
1. La carte ou le texte publié fournit des informations d'aperçu adéquates pour qu'un utilisateur puisse prendre des mesures ou décider d'afficher plus de détails dans un lien s'ouvrant en dehors de Teams.

Applications qui fournissent uniquement des notifications avec du contenu, par exemple, **vous disposez d’une nouvelle notification**, **cliquez pour afficher** et demandez à l’utilisateur de naviguer en dehors de Teams pour tout le reste ne fournissent pas de valeur significative dans Teams.

   :::image type="content" source="../../../../assets/images/submission/validation-bot-notification-only-inadequete-info.png" alt-text="Capture d’écran montrant un exemple de notification avec des informations insuffisantes dans la préversion.":::

> [!TIP]
> Affichez un aperçu des informations et fournissez des actions utilisateur incluses de base dans la carte publiée afin que l’utilisateur ne soit pas obligé de naviguer en dehors de Teams pour toutes les actions (quelle que soit la complexité).

</details>
<br/>

<details><summary>Informations sur les métadonnées du bot</summary>

* Les informations du bot dans le manifeste de l’application (nom du bot, logo, lien de confidentialité et lien de conditions de service) doivent être cohérentes avec les métadonnées Bot Framework. [*Correction obligatoire*]

* L’ID de bot doit correspondre dans le manifeste de l’application et les métadonnées Bot Framework. [*Correction obligatoire*]

* Vérifiez que l’ID de bot dans le manifeste de l’application correspond à l’ID de bot dans la dernière version publiée du magasin de votre application. La modification des ID de bot dans une mise à jour d’application entraîne la perte permanente de tout l’historique des interactions utilisateur avec le bot pour les utilisateurs existants de votre application et démarre une nouvelle chaîne de conversation avec le nouvel ID de bot. [*Correction obligatoire*]

* Toute modification apportée au nom de l’application, aux métadonnées, au message de bienvenue du bot ou aux réponses du bot doit être mise à jour avec un nouveau nom. [*Correction obligatoire*]

* Le nom de l’application dans le message d’accueil du bot ou les réponses du bot doivent correspondre au nom de l’application dans le manifeste. [*Correction obligatoire*]

</details>
<br/>

<details><summary>Bot dans l’étendue collaborative</summary>

* L’installation du bot dans une étendue de conversation de canal ou de groupe pour obtenir la liste d’équipe pour l’envoi de notifications proactives pour les utilisateurs, car les conversations 1:1 pour des déclencheurs spécifiques à l’équipe ne sont pas autorisées. Par exemple, une application qui associe des personnes pour une réunion. [*Correction obligatoire*]

* Bot dans un canal ou une conversation de groupe utilisé uniquement pour obtenir les messages ou les publications dans canal ou conversation de groupe pour l’envoi de notifications proactives pour les utilisateurs, car les conversations 1:1 ne sont pas autorisées. [*Correction obligatoire*]

* Les bots installés dans une étendue collaborative doivent fournir une valeur utilisateur dans l’étendue collaborative. [*Correction obligatoire*]

</details>

## <a name="message-extensions"></a>Extensions de messages

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4.4 du marché commercial de Microsoft](/legal/marketplace/certification-policies#114044-messaging-extensions).

Si votre application inclut une extension de message, assurez-vous qu’elle respecte ces instructions.

> [!TIP]
> Pour plus d'informations sur la création d'une expérience d'application de haute qualité, consultez les [instructions de conception d'extension de messagerie Teams](~/messaging-extensions/design/messaging-extension-design.md).

<br/>

<details><summary>Instructions de conception des extensions de messagerie</summary>

* Si votre application Teams utilise la fonctionnalité d’extension de messagerie, votre application doit suivre les [instructions de conception de l’extension de messagerie](../../../../messaging-extensions/design/messaging-extension-design.md).

   :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-design-guidelines-fail.png" alt-text="Le graphique montre un exemple d’application qui ne répond pas aux instructions d’extension.":::

* Les extensions de messagerie sont des raccourcis permettant d’insérer du contenu d’application ou agir sur un message sans quitter la conversation. Simplifiez votre extension de messagerie et affichez uniquement les composants nécessaires pour effectuer efficacement l’action. Le site web complet ne doit pas être encadré dans l’extension de messagerie [*Correctif obligatoire*]

* Les images d’aperçu des cartes adaptatives dans les extensions de messagerie doivent se charger correctement. [*Correction obligatoire*]

  :::image type="content" source="../../../../assets/images/submission/validation-preview-image-adaptive-card-loading.png" alt-text="Le graphique montre un exemple de chargement d’image en préversion dans une carte adaptative.":::

  :::image type="content" source="../../../../assets/images/submission/validation-preview-image-adaptive-card-not-loading.png" alt-text="Le graphique montre un exemple d’image d’aperçu qui ne se charge pas dans la carte adaptative.":::

* La carte de réponse de l’extension de messagerie doit inclure l’icône d’application pour éviter toute confusion de l’utilisateur final. [*Correction obligatoire*]

* Votre application ne doit pas avoir de fonctionnalités rompues. L’application ne doit pas être bloquée ou empêcher l’utilisateur d’exécuter un flux de travail dans une extension de messagerie. [*Correction obligatoire*]

* Les extensions de messagerie doivent répondre ou fonctionner comme prévu dans les étendues de conversation de groupe et de canal. [*Correction obligatoire*]

* Vous devez inclure un moyen pour l’utilisateur de se connecter ou de se déconnecter à partir de l’extension de messagerie. [*Correction obligatoire*]

</details>
</br>

<details><summary>Commandes d’action pour les extensions de message basées sur l’action</summary>

Les extensions de messagerie basées sur les actions doivent effectuer les opérations suivantes :

* Autorisez les utilisateurs à déclencher des actions sur un message sans effectuer d'étapes intermédiaires, telles que la connexion.

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-no-intermediate-step.png" alt-text="validation-messaging-extension-no-intermediate-steps":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-intermediate-step-available.png" alt-text="validation-messaging-extension-intermediate-steps-available":::

* Passez le contexte du message à l’état de travail suivant. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-passes-message.png" alt-text="validation-messaging-extension-app-passes-messages":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-doesnot-pass-message.png" alt-text="validation-messaging-extension-app-doesnot-pass-messages":::

* Incorporez le nom de l'application hôte au lieu d'un verbe générique pour les commandes d'action déclenchées à partir d'un message de discussion, d'une publication de canal ou d'un appel à l'action dans les applications. Par exemple, utilisez **Démarrer une Réunion Skype** pour **démarrer la réunion**, charger le **fichier vers DocuSign** pour **le fichier de chargement**. [*Correctif suggéré*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-host-name.png" alt-text="Le graphique montre un exemple de nom d’application hôte pour une commande d’action.":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-verb.png" alt-text="Le graphique montre un exemple de verbe générique pour une commande d’action.":::

* L’appel d’une action de message doit permettre à l’utilisateur d’effectuer le flux de travail. Les erreurs, les réponses vides ou les indicateurs de chargement continu pour rendre l’action de message fonctionnelle comme prévu ne doivent pas être présentes. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-continous-loading-indicator-action-command.png" alt-text="Le graphique montre un exemple d’indicateur de chargement continu lorsqu’un bot appelle une commande d’action.":::

* Les commandes d’action en double ne doivent pas être présentes. [*Correction obligatoire*]

* Les actions de message doivent permettre à l’utilisateur d’effectuer le flux de travail comme prévu sans réponse non valide. [*Correction obligatoire*]

* Les applications avec uniquement une extension de messagerie basée sur des actions doivent avoir l’état final suivant :

  * Publiez une action pertinente en tant que notification dans le contexte où l’extension de message est appelée ou dans une conversation de bot 1:1 en fonction du scénario utilisateur. [*Correction obligatoire*]

  * Autoriser les utilisateurs à partager des cartes avec d’autres utilisateurs en fonction de l’action effectuée. Cela permet de s’assurer que les applications ne prennent pas d’actions silencieuses. Par exemple, un ticket est créé en fonction d’un message dans un canal, mais l’application n’envoie pas de notification ou ne fournit pas de moyen de demander à l’utilisateur de partager les détails du ticket une fois le ticket créé. [*Correction obligatoire*]

</details>
</br>

<details><summary>Liens d’aperçu (déploiement de liens)</summary>

[*Correction obligatoire*]

Les extensions de messagerie doivent prévisualiser les liens reconnus dans la zone de rédaction Teams. N'ajoutez pas de domaines hors de votre contrôle (qu'il s'agisse d'URL absolues ou de caractères génériques). Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` non valide. Les domaines de premier niveau sont également interdits. Par exemple : `*.com` ou `*.org`. [*Correction obligatoire*]

</details>
</br>

<details><summary>Commandes de recherche</summary>

* Les extensions de messagerie basées sur la recherche doivent fournir du texte qui aide les utilisateurs à rechercher efficacement. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-available.png" alt-text="Le graphique montre un exemple d’extension de message avec du texte d’aide permettant aux utilisateurs de rechercher efficacement.":::

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-not-available.png" alt-text="Le graphique montre un exemple d’extension de message sans texte d’aide permettant aux utilisateurs de rechercher efficacement.":::

* Les @mention exécutables doivent être claires, faciles à comprendre et lisibles.

    :::image type="content" source="../../../../assets/images/submission/validation-search-command-unclear-executable.png" alt-text="validation-search-commands-unclear-executable":::

</details>
</br>

<details><summary>Commandes d’action pour l’extension de message basée sur la recherche</summary>

[*Correction obligatoire*]

Les applications qui consistent en une extension de messagerie basée sur la recherche offrent une valeur utilisateur en partageant des cartes qui permettent des conversations contextuelles sans changement de contexte.

Pour réussir la validation d’une application d’extension de message basée sur la recherche uniquement, les éléments suivants sont requis comme base de référence pour garantir que l’expérience utilisateur n’est pas interrompue. Une carte partagée via une extension de messagerie apporte de la valeur dans Teams si :

1. La carte publiée fournit des détails adéquats ne nécessitant aucune autre action de l'utilisateur.
1. La carte publiée fournit des informations d'aperçu adéquates pour qu'un utilisateur puisse prendre des mesures ou décider d'afficher plus de détails dans un lien s'ouvrant en dehors de Teams.

    :::image type="content" source="../../../../assets/images/submission/validation-search-based-messaging-ext-adequete-info.png" alt-text="validation-search-base-messaging-ext-adequete-info":::

    :::image type="content" source="../../../../assets/images/submission/validation-search-based-messaging-ext-inadequete-info.png" alt-text="validation-search-base-messaging-ext-inadequete-info":::

Les applications de déploiement de liens uniquement n'apportent pas de valeur significative au sein des équipes. Envisagez de créer des workflows supplémentaires dans votre application, si votre application ne prend en charge que le déploiement de liens et n'a aucune autre fonctionnalité.

</details>

## <a name="task-modules"></a>Modules de tâche

[*Correction obligatoire*]

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4.5 du marché commercial de Microsoft](/legal/marketplace/certification-policies#114045-task-modules).
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Un module de tâche doit inclure une icône et le nom court de l’application avec laquelle il est associé. Les modules de tâches ne doivent pas intégrer une application entière et afficher uniquement les composants requis pour effectuer une action spécifique.

Pour plus d'informations, consultez [Instructions de conception du module de tâches Teams](~\task-modules-and-cards\task-modules\design-teams-task-modules.md).

:::image type="content" source="../../../../assets/images/submission/validation-task-module-displays-components.png" alt-text="validation-task-module-displays-component":::

:::image type="content" source="../../../../assets/images/submission/validation-task-module-embeds-app.png" alt-text="validation-task-module-embed-app":::

> [!TIP]
> Pour plus d'informations sur la création d'une expérience d'application de haute qualité, consultez les [Directives de conception du module de tâche des équipes](~/task-modules-and-cards/task-modules/design-teams-task-modules.md).

</details>

## <a name="meeting-extensions"></a>Extensions de réunion

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la stratégie[ 1140.4.6 du marché commercial de Microsoft](/legal/marketplace/certification-policies#114046-meeting-extensions).
> [!TIP]
> Pour plus d'informations sur la création d'une expérience d'application de haute qualité, consultez les [directives de conception d'extension de réunion Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).

</br>
<details><summary>Recommandations en matière de conception d’extension de réunion</summary>

* Vos applications Teams doivent suivre [les instructions de conception d’extension de réunion](../../../../apps-in-teams-meetings/design/designing-apps-in-meetings.md).

* Avec l’expérience de l’application en réunion, vous pouvez impliquer les participants pendant la réunion à l’aide des onglets de la réunion, de la boîte de dialogue et de la fonctionnalité de partage de réunion à étape. Si votre application prend en charge l’extension de réunion Teams, vous devez fournir une expérience de réunion réactive alignée sur l’expérience de réunion Teams. [*Correction obligatoire*]

* Avec l'expérience d'application de pré-réunion, les utilisateurs peuvent rechercher et ajouter des applications de réunion. Les utilisateurs peuvent également effectuer des tâches préalables à la réunion, telles que le développement d’un sondage pour interroger les participants à la réunion. Une application qui fournit une expérience de pré-réunion doit être pertinente pour le flux de travail de la réunion et offrir de la valeur à l’utilisateur. [*Correction obligatoire*]

* Avec l’expérience de l’application post-réunion, les utilisateurs peuvent afficher les résultats de la réunion, tels que les résultats de l’enquête de sondage ou les commentaires et d’autres contenus d’application. Une application qui fournit une expérience post-réunion doit être pertinente pour le flux de travail de la réunion et offrir de la valeur à l’utilisateur. [*Correction obligatoire*]

* Avec l'expérience de l'application en réunion, vous pouvez impliquer les participants à la réunion pendant la réunion et améliorer l'expérience de la réunion pour tous les participants. Les participants ne doivent pas être emmenés en dehors de la réunion Teams pour effectuer les flux de travail utilisateur principaux de l’application. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-outside-teams-core-workflows.png" alt-text="Le graphique montre un exemple d’expérience en réunion qui redirige l’utilisateur en dehors de Teams pour compléter les fonctionnalités principales de l’application.":::

* Votre application doit offrir de la valeur au-delà de la fourniture de scènes personnalisées en mode Ensemble dans Teams. [*Correction obligatoire*]

* Vous devez déclarer `groupChat` en tant que portée sous `configurableTabs` et `meetingDetailsTab`, `meetingChatTab`et `meetingSidePanel` en tant que propriété de contexte dans le manifeste pour activer votre application pour les réunions sur Teams mobile. [*Correction obligatoire*]

* Les canevas de réunion ne doivent pas arrêter un participant à la réunion. Les canevas de réunion doivent afficher un message d’échec approprié pour les limitations de l’application, telles que la dépendance spécifique à la région. [*Correction obligatoire*]

* L’en-tête du canevas de réunion doit afficher le nom d’application approprié pour éviter de confondre le participant à la réunion. [*Correction obligatoire*]

* Vous devez inclure une option permettant à l’utilisateur de se déconnecter ou de se déconnecter de l’extension de réunion. [*Correction obligatoire*]

* Les onglets de réunion sur les plateformes mobiles doivent inclure des flux de travail pertinents. Les pages vides ne doivent pas être présentes dans un onglet de réunion. [*Correctif obligatoire*]

* La phase de réunion est un canevas de participation axé, intuitif et collaboratif. La phase de réunion ne doit pas incorporer l’expérience complète du site web. [*Correction obligatoire*]

* L’application ne doit pas afficher l’écran de chargement continu, les erreurs ou les fonctionnalités interrompues qui bloquent l’exécution d’un flux de travail dans un scénario de réunion. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-app-shows-continous-loading-screen.png" alt-text="Le graphique montre un exemple d’écran de chargement continu dans une application.":::

* L’application ne doit pas ouvrir une nouvelle instance Teams au démarrage d’une réunion. Les canevas de réunion sont une extension des fonctionnalités teams qui favorisent la collaboration en temps réel et les nouvelles réunions doivent toujours s’ouvrir au sein de l’instance Teams actuellement active. [*Correction obligatoire*]

* Les applications de réunion doivent effectuer des workflows au sein de la plateforme Microsoft Teams sans rediriger vers les plateformes de conversation concurrentes. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-apps-redirecting-competitor-chat-platform.png" alt-text="Le graphique montre un exemple de redirection d’application vers une plateforme de conversation concurrente.":::

* Si votre application prend en charge les vues basées sur les rôles et que certains flux de travail ne sont pas disponibles pour tous les participants, nous vous recommandons d’implémenter une messagerie appropriée pour les participants dans l’onglet et le panneau latéral indiquant que l’application est actuellement destinée à l’affichage de l’organisateur et de fournir des détails sur la façon dont les participants recevront les notes de réunion, les éléments d’action et les agendas de mise à jour. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-way-forward-not-available-for-role-based-views.png" alt-text="Le graphique montre un exemple d’application sans chemin d’accès pour les participants dans une vue basée sur un rôle.":::

</details>
<br/>

<details><summary>Général</summary>

Utilisez les directives suivantes pour les extensions de réunion :

* Les applications d’extensibilité de réunion doivent offrir une expérience de réunion réactive alignée sur l’expérience de réunion Teams. L’expérience en réunion est obligatoire pour une application Teams qui prend en charge l’extensibilité des réunions, mais les expériences de pré et de post-réunion ne sont pas obligatoires.

  * Avec l'expérience d'application de pré-réunion, les utilisateurs peuvent rechercher et ajouter des applications de réunion. Les utilisateurs peuvent également effectuer des tâches préalables à la réunion, telles que le développement d’un sondage pour interroger les participants à la réunion. Si votre application offre une expérience de pré-réunion, elle doit être pertinente pour le flux de travail de la réunion.

  * Avec l’expérience d’application post-réunion, les utilisateurs peuvent afficher les résultats de la réunion, tels que les résultats de l’enquête de sondage ou les commentaires et d’autres contenus d’application. Si votre application offre une expérience post-réunion, elle doit être pertinente pour le flux de travail de la réunion.

  * Avec l'expérience de l'application en réunion, vous pouvez impliquer les participants à la réunion pendant la réunion et améliorer l'expérience de la réunion pour tous les participants. Les participants ne doivent pas être emmenés en dehors de la réunion Teams pour terminer les flux de travail utilisateur principaux de votre application.

* Votre application doit offrir une valeur au-delà de la fourniture de scènes de mode Together personnalisées dans Teams.

* La fonctionnalité d'étape de réunion partagée ne peut être lancée que via l'application de bureau Teams. Cependant, l'expérience de consommation de l'étape de réunion partagée doit être utilisable et non interrompue lorsqu'elle est visualisée sur des appareils mobiles.

> [!TIP]
> Vous devez déclarer `groupChat` en tant que portée sous `configurableTabs` et `meetingDetailsTab`, `meetingChatTab`et `meetingSidePanel` en tant que propriété de contexte dans le manifeste pour activer votre application pour les réunions sur Teams mobile.

</details>
</br>

<details><summary>Expérience avant et après la réunion</summary>

* Les écrans avant et après la réunion doivent respecter les directives générales de conception des onglets. Pour plus d'informations, consultez [Directives de conception Teams](~/tabs/design/tabs.md).
* Les onglets doivent avoir une disposition organisée lors de l'affichage de plusieurs éléments. Par exemple, plus de 10 sondages ou enquêtes, voir [exemple de mise en page](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* Votre application doit informer les utilisateurs lorsque les résultats d'une enquête ou d'un sondage sont exportés en indiquant, **Résultats téléchargés avec succès**.

   :::image type="content" source="../../../../assets/images/submission/validation-meeting-experience-tab-design-guidelines-fail.png" alt-text="Le graphique montre un exemple d’onglet qui ne suit pas les instructions de conception d’onglet.":::

</details>

</br>
<details><summary>Expérience en réunion</summary>

* Les applications doivent uniquement utiliser un thème foncé pendant les réunions. Pour plus d'informations, consultez [Directives de conception Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming).
* Une info-bulle doit afficher le nom de l'application lorsque vous survolez l'icône de l'application pendant les réunions.

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-display-app-name.png" alt-text="validation-in-meeting-exp-display-app-names":::

* Les extensions de messagerie doivent fonctionner de la même manière pendant les réunion qu’en dehors des réunions.

</details>

</br>
<details><summary>Onglets de réunion</summary>

* Doivent être réactifs.
* Doit maintenir le rembourrage et la taille des composants.
* Doit avoir un bouton de retour s'il y a plus d'une couche de navigation.

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button.png" alt-text="Le graphique montre un exemple de bouton Précédent présent.":::

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button-absent.png" alt-text="Le graphique montre un exemple de bouton Précédent non présent.":::

* Ne doit pas inclure plus d'un bouton de fermeture. Cela peut dérouter les utilisateurs car il existe déjà un bouton d'en-tête intégré pour fermer l'onglet.
* Ne doit pas avoir de défilement horizontal.

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-tab-vertical-scroll.png" alt-text="Le graphique montre un exemple d’onglet en réunion avec défilement vertical.":::

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-tab-horizontal-scroll.png" alt-text="Le graphique montre un exemple d’onglet in-meeting avec défilement horizontal.":::

</details>

</br>
<details><summary>Boîtes de dialogue en réunion</summary>

* Doit être utilisé avec parcimonie et pour des scénarios légers et axés sur les tâches.
* Doivent afficher le contenu dans une seule colonne et ne pas avoir plusieurs niveaux de navigation.

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-single-column-layout.png" alt-text="Le graphique montre un exemple de disposition d’une seule colonne pour la boîte de dialogue en réunion.":::

  :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-multiple-column-layout.png" alt-text="Le graphique montre un exemple de plusieurs dispositions de colonnes pour la boîte de dialogue en réunion.":::

* Ne doivent pas utiliser de modules de tâche.
* Doivent s’aligner sur le centre de la phase de réunion.

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-dialog-not-aligned.png" alt-text="Le graphique montre un exemple de boîte de dialogue en réunion qui ne s’aligne pas sur le centre de la phase de réunion.":::

* Doit être rejeté après qu'un utilisateur a sélectionné un bouton ou effectué une action.

* **Mode Ensemble** : assurez-vous de prendre en compte les meilleures pratiques suivantes pour une expérience de création de scène :
  * Toutes les images sont au format .png.
  * Le package final avec toutes les images rassemblées ne doit pas dépasser une résolution de 1920x1080. La résolution est un nombre pair. Cette résolution est une exigence pour que les scènes soient affichées avec succès.
  * La taille maximale de la scène est de 10 Mo.
  * La taille maximale de chaque image est de 5 Mo. Une scène est une collection de plusieurs images. La limite est pour chaque image individuelle.
  * Sélectionnez **Transparent** selon vos besoins. Cette case à cocher est disponible sur le panneau de droite lorsqu'une image est sélectionnée. Les images qui se chevauchent doivent être marquées comme transparentes pour indiquer qu'elles se chevauchent dans la scène.

</details>

## <a name="notifications"></a>Notifications

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4.7 du marché commercial de Microsoft](/legal/marketplace/certification-policies#114047-notification-apis).

Si votre application utilise les [API de flux d’activité fournies par Microsoft Graph](/graph/teams-send-activityfeednotifications), assurez-vous qu’elle respecte les instructions suivantes.

> [!TIP]
> Si vos applications prennent en charge les scénarios de notification où les notifications sont déclenchées après de longs intervalles, par exemple, après un jour ou un mois. Avant de soumettre une demande de révision, veillez à déclencher ces notifications en arrière-plan pour que nous puissions tester les notifications.

<br></br>

<details><summary>Instructions de conception des notifications</summary>

* Vos applications Teams doivent suivre [les instructions de conception des notifications de flux d’activité](/graph/teams-send-activityfeednotifications).

* Le flux de travail non pertinent, incorrect, non répondant ou rompu ne doit pas être présent après que l’utilisateur a sélectionné une notification dans le flux d’activité Teams. Les utilisateurs ne doivent pas être empêchés d’exécuter un flux de travail après avoir sélectionné une notification de flux d’activité. [*Correction obligatoire*]

* Incluez le nom de votre application dans la notification de flux d’activité pour que les utilisateurs finaux comprennent la source ou le déclencheur de la notification sans confusion. [*Correction obligatoire*]

* L’application doit déclencher des notifications pour tous les scénarios de notification mentionnés dans la description longue de l’application, l’expérience de première exécution de l’application et dans les scénarios déclarés sous `activityTypes` le manifeste. [*Correction obligatoire*]

* Les notifications doivent s’afficher dans les cinq secondes après l’action d’un utilisateur. [*Correction obligatoire*]

* Vous devez rappeler les limitations de notification (le cas échéant) dans la description longue de votre application ou dans l’expérience de première exécution de l’application. [*Correction obligatoire*]

</details>
<br/>

<details><summary>Général</summary>

* Tous les déclencheurs de notification spécifiés dans la configuration de votre application doivent fonctionner.
* Les notifications doivent être localisées selon les langues de prise en charge configurées pour votre application.
* Les notifications doivent s’afficher dans les cinq secondes après l’action d’un utilisateur.
* Les notifications doivent être localisées en fonction des langues prises en charge pour toutes les plateformes sur lesquelles votre application est compatible. [*Correction obligatoire*]

</details>
</br>

<details><summary>Avatars</summary>

* L'avatar de notification doit correspondre à l'icône de couleur de votre application.
* Les notifications déclenchées par un utilisateur doivent inclure l'avatar de l'utilisateur.

</details>
</br>
<details><summary>Envoi de courrier indésirable</summary>

* Les applications ne doivent pas envoyer plus de 10 notifications par minute à un utilisateur.
* Les bots et le flux d'activité ne doivent pas déclencher de notifications en double.
* Les notifications doivent fournir une valeur ajoutée aux utilisateurs et ne pas être utilisées pour des événements triviaux ou non pertinents.

</details>
</br>
<details><summary>Navigation et disposition</summary>

* Les notifications doivent respecter la disposition et l’expérience de flux d’activités Teams.
* Lors de la sélection d'une notification, l'utilisateur doit être dirigé vers le contenu pertinent dans Teams.

</details>

## <a name="microsoft-365-app-compliance-program"></a>Programme de conformité d’Application Microsoft 365

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la stratégie [1140.6 du marché commercial de Microsoft](/legal/marketplace/certification-policies#11406-publisher-attestation).
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Le Programme de conformité d’Application Microsoft 365 est destiné à aider les organisations à évaluer et à gérer les risques en évaluant les informations de sécurité et de conformité concernant votre application. Si vous publiez une application dans le magasin Teams, vous devez effectuer les niveaux suivants du programme :

* **Vérification de l’éditeur** : permet aux administrateurs et aux utilisateurs finaux de comprendre l’authenticité des développeurs d’applications procédant à une intégration avec la Plateforme d'identités Microsoft. Une fois terminé, un badge de **vérifié** bleu s’affiche dans la boîte de dialogue de consentement Azure Active Directory et sur d’autres écrans. Pour plus d'informations, voir [Marquer votre application comme vérifiée par l'éditeur](/azure/active-directory/develop/mark-app-as-publisher-verified).

    :::image type="content" source="../../../../assets/images/submission/validation-365-compliance-publisher-verification.png" alt-text="Le graphique montre un exemple de badge vérifié bleu dans la boîte de dialogue de consentement Azure Active Directory.":::

* **Attestation d’éditeur** : processus dans lequel vous partagez des informations générales, de gestion des données et de sécurité et de conformité pour permettre aux clients potentiels de prendre des décisions informées sur l’utilisation de votre application.

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Si vous soumettez une application qui n'a pas été répertoriée auparavant, vous ne pouvez pas compléter officiellement l'attestation d'éditeur tant que votre application n'est pas dans le Teams Store. Si vous êtes mettez à jour une application répertoriée, achevez l’attestation d’éditeur avant de soumettre la dernière version de l’application.

</details>

## <a name="advertising"></a>Publicité

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie du marché commercial de Microsoft, numéro 1140.7](/legal/marketplace/certification-policies#11407-advertising).

Les applications ne doivent pas afficher de publicité, y compris les publicités dynamiques, les bannières publicitaires et les publicités dans les messages.

:::image type="content" source="../../../../assets/images/submission/validation-advertising-banners.png" alt-text="Le graphique montre un exemple de scénario d’échec de la publicité dans Teams.":::

## <a name="cryptocurrency-based-apps"></a>Applications basées sur la crypto-monnaie

Vous devez démontrer la conformité à toutes les lois dans lesquelles votre application est distribuée, si votre application :

* Facilite les transactions ou les transmissions de chiffrement au sein de l’application.

* Promeut le contenu lié à la cryptomonnaie.

* Permet aux utilisateurs de stocker ou d’accéder à leur chiffrement stocké.

* Encourage ou permet aux utilisateurs d’effectuer une transaction ou une transmission basée sur la crypto-monnaie en dehors de la plateforme Teams.

* Encourage ou facilite l’exploration de jetons de chiffrement.

* Facilite la participation des utilisateurs aux offres de pièces initiales.

* Récompense ou encourage les utilisateurs à utiliser des jetons de chiffrement pour effectuer une tâche.

Après une révision interne de Microsoft, si la démonstration de conformité est satisfaisante, Microsoft peut poursuivre la certification de votre application. Si la démonstration de conformité n’est pas satisfaisante, Microsoft vous informera de la décision de ne pas poursuivre la certification de votre application.

## <a name="app-functionality"></a>Fonctionnalités de l’application

* Les flux de travail ou le contenu de l’application doivent être liés à l’étendue. [*Correction obligatoire*]
* Toutes les fonctionnalités de l’application doivent être fonctionnelles et fonctionner correctement, comme décrit dans la description longue d’AppSource ou de manifeste. [*Correction obligatoire*]
* Les applications doivent toujours être intimes à l’utilisateur avant de télécharger un fichier ou un exécutable sur l’environnement de l’utilisateur. Tout appel à l’action (CTA), basé sur du texte ou autre, qui indique clairement à l’utilisateur qu’un fichier ou un exécutable est téléchargé lors de l’action de l’utilisateur est autorisé dans l’application. [*Correction obligatoire*]

## <a name="mobile-experience"></a>Expérience mobile

* Les compléments mobiles doivent être gratuits. Il ne doit pas y avoir de contenu ou de liens dans l’application qui favorisent la vente à la vente, les magasins en ligne ou d’autres demandes de paiement. Les comptes requis pour les applications ne doivent pas être facturés pour une utilisation et, s’ils sont limités dans le temps, ne doivent pas inclure de contenu indiquant la nécessité de payer.

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-add-in-charges.png" alt-text="Le graphique montre un exemple de complément mobile demandant un paiement.":::

* L’utilisation du mot **FREE**, **FREE TRIAL** ou **TRY FREE** est autorisée sur l’expérience de bureau ou d’application web sans aucune limitation ou considération.

* L’utilisation du mot **FREE** comme texte brut dans le contexte d’une version d’évaluation ou d’une mise à niveau d’application est autorisée sur mobile.

* L’utilisation du mot **GRATUIT** dans le contexte d’une version d’évaluation ou d’une mise à niveau d’application avec un lien menant à une page d’accueil sans informations de paiement ou de tarification est autorisée sur mobile. Le texte brut pour signaler que l’application est **PAYANTe** est autorisé sur mobile.

* L’utilisation du mot **FREE** comme texte brut dans le contexte d’une version d’évaluation ou d’une mise à niveau d’application et associée à des détails tarifaires n’est pas autorisée sur les appareils mobiles.

* L’utilisation du mot **GRATUIT** dans le contexte d’une version d’évaluation ou d’une mise à niveau d’application et associée à un lien qui mène à une page d’accueil avec des informations de tarification ou des détails de paiement sur mobile n’est pas autorisée.

* Les détails de tarification sur les appareils mobiles dans n’importe quel format, par exemple, l’image, le texte ou le lien ne sont pas autorisés. L’authentification CTA, telle que **les plans d’affichage** sur les appareils mobiles, n’est pas autorisée. Les informations sur les plans sans détails tarifaires, mais avec un lien de contact ou un e-mail sur mobile ne sont pas autorisées. Tout texte avec des détails de contact liant ou faisant allusion à une mise à niveau payante n’est pas autorisé sur mobile. Paiements pour les biens physiques sont autorisés sur les appareils mobiles. Par exemple, votre application peut autoriser le paiement pour réserver un taxi.

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-exp-pricing-details-on-mobile-fail.png" alt-text="Le graphique montre un exemple de détails de tarification sur les appareils mobiles.":::

* Paiements pour les biens numériques dans l’application ne sont pas autorisés sur les appareils mobiles. [*Correction obligatoire*]

   :::image type="content" source="../../../../assets/images/submission/validation-mobile-exp-payments-digital-goods.png" alt-text="Le graphique montre un exemple de paiement de biens numériques sur les appareils mobiles.":::

* Les applications Teams doivent offrir une expérience mobile inter-appareils appropriée. [*Correction obligatoire*]

* Les fonctionnalités qui ne sont pas prises en charge sur les appareils mobiles ne doivent pas être sans fin pour un utilisateur et doivent fournir un message d’échec approprié, le cas échéant. [*Correction obligatoire*]

## <a name="next-step"></a>Étape suivante

> [!div class=*nextstepaction*]
> [Créer un compte d’Espace partenaires](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)

## <a name="see-also"></a>Voir aussi

* [Distribuer votre application.](~/concepts/deploy-and-publish/apps-publish-overview.md)
* [Préparer l'envoi de votre magasin](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [Tester et déboguer votre application](~/concepts/build-and-test/debug.md)
* [Créer un compte de développeur de l’Espace partenaires](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
