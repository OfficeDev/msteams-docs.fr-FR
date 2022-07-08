---
title: Instructions de validation du magasin Microsoft Teams
description: Dans cet article, vous trouverez les instructions que chaque application soumise au Store Teams (AppSource) doit suivre.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 0c92ce5acee19a1c83bf5fc83e0b09ab6a6dfc4f
ms.sourcegitcommit: 07f41abbeb1572a306a789485953c5588d65051e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/06/2022
ms.locfileid: "66659038"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Instructions de validation du magasin Microsoft Teams

Le respect de ces directives augmente les chances que votre application réussisse le processus de soumission du magasin Microsoft Teams. Les directives spécifiques aux équipes complètent les [politiques de certification du marché commercial](/legal/marketplace/certification-policies#1140-teams) Microsoft et sont mises à jour fréquemment pour refléter les nouvelles fonctionnalités, les commentaires des utilisateurs et les modifications des règles métier.

> [!NOTE]
>
> * Certaines instructions peuvent ne pas être applicables à votre application. Par exemple, si votre application n’inclut pas de bot, vous pouvez ignorer les instructions liées aux bots.
> * Nous avons recoupé ces directives avec les politiques de certification commerciale de Microsoft et ajouté les choses à faire et à ne pas faire avec des exemples de scénarios de réussite ou d'échec rencontrés dans notre processus de validation.
> * Certaines directives sont marquées comme *Correction obligatoire*. Si votre soumission d'application ne respecte pas ces directives obligatoires, vous recevrez un rapport d'échec de notre part avec des mesures pour atténuer. Votre soumission d'application ne passera la validation du Microsoft Teams Store qu'une fois que vous aurez résolu les problèmes.
> * D’autres instructions sont marquées comme *suggestions de correction*. Pour une expérience utilisateur idéale, nous vous suggérons de résoudre les problèmes. Toutefois, la publication de votre soumission d’application ne sera pas bloquée sur le magasin Teams, si vous choisissez de ne pas résoudre les problèmes.

:::row:::
   :::column:::
      :::image type="content" source="../../../../assets/icons/value-proposition.png" alt-text="value-proposition-teams" link="#value-proposition":::
   :::column-end:::
   :::column span="":::
     :::image type="content" source="../../../../assets/icons/security.png" alt-text="security-store" link="#security":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/function.png" alt-text="fonctionnalité" link="#general-functionality-and-performance":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/package.png" alt-text="package d’application" link="#app-package-and-store-listing":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/saas-offer.PNG" alt-text="SaaS" link="#apps-linked-to-saas-offer":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/tab.png" alt-text="tab-teams" link="#tabs":::
   :::column-end:::
   :::column:::
      :::image type="content" source="../../../../assets/icons/bot.png" alt-text="bot-teams" link="#bots-1":::
   :::column-end:::
   :::column span="":::
     :::image type="content" source="../../../../assets/icons/messaging-extension.png" alt-text="messagerie" link="#message-extensions":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/task-module.png" alt-text="task-module-teams" link="#task-modules":::
   :::column-end:::
     :::column span="":::
      :::image type="content" source="../../../../assets/icons/meeting.png" alt-text="meeting-extension" link="#meeting-extensions":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/empty.png" alt-text="empty-2":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/notifications.png" alt-text="teams-notification" link="#notifications":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/microsoft-365.png" alt-text="microsoft" link="#microsoft-365-app-compliance-program":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/advertising.png" alt-text="advertising-teams" link="#advertising":::
   :::column-end:::
   :::column span="":::
      :::image type="content" source="../../../../assets/icons/empty.png" alt-text="empty-1":::
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
* Les noms des fonctionnalités principales de Teams ne doivent pas être inclus dans le nom de votre application, tels que :  
  * **Conversation**
  * **Contacts**
  * **Calendar**
  * **Appels**
  * **Files**
  * **Activité**
  * **Applications**
  * **Help**
* Préfixe ou suffixe des noms communs avec le nom du développeur. Par exemple, **Tâches Contoso** au lieu de **Tâches**.
* Ne doit pas utiliser **Teams** ou d'autres noms de produits Microsoft tels qu'Excel, PowerPoint, Word, OneDrive, SharePoint, OneNote, Azure, Surface, Xbox, etc. qui pourraient faussement indiquer le co-branding ou la co-vente. Pour plus d'informations sur le référencement des produits et services logiciels Microsoft, consultez [Directives sur les marques et marques Microsoft](https://www.microsoft.com/legal/intellectualproperty/trademarks/usage/general).
* Si votre application fait partie d'un partenariat officiel avec Microsoft, le nom de votre application doit apparaître en premier. Par exemple, **Connecteur Contoso pour Microsoft Teams**.
* Ne doit pas copier le nom d’une application répertoriée dans le magasin ou une autre offre sur la place de marché commerciale.
* Ne doit pas contenir de termes vulgaires ou désobligeants. Le nom ne doit pas non plus inclure un langage qui manque d’égard en matière de race ou de culture.
* Doit être unique. Si votre application (Contoso) est répertoriée dans le Microsoft Teams Store et Microsoft AppSource et que vous souhaitez répertorier une autre application spécifique à une zone géographique, telle que Contoso Mexico, votre soumission doit répondre aux critères suivants :
  * Appelez la fonctionnalité spécifique à la région de l'application dans le titre, les métadonnées, l'expérience de l'application de première réponse et les sections d'aide. Par exemple, le titre doit être Contoso Mexico. Le titre de l'application doit clairement différencier une application existante du même développeur pour éviter toute confusion chez l'utilisateur final.
  * Lors du téléchargement du package d'application dans Partner Center, sélectionnez les bons **marchés** où l'application sera disponible dans la section **Disponibilité**.

 > [!TIP]  
 > La marque de votre application sur le magasin Microsoft Teams et Microsoft AppSource, y compris le nom de votre application, le nom du développeur, l'icône de l'application, les captures d'écran Microsoft AppSource, la vidéo, la brève description et le site Web, séparément ou pris ensemble, ne doivent pas usurper l'identité d'une offre officielle de Microsoft, sauf si votre application est officielle Offre Microsoft 1P.

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

Les noms de fonctionnalités d'application dans les boutons et autres textes de l'interface utilisateur ne doivent pas être dupliqués avec la terminologie réservée aux équipes et aux autres produits Microsoft. Par exemple, **Commencer la réunion**, **Passer des appels** ou **Démarrer une conversation**. Si nécessaire, incluez le nom de votre application, par exemple **Démarrer une réunion Contoso**.

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

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme au numéro 1140.3.1[ de la stratégie de certification commerciale de Microsoft](/legal/marketplace/certification-policies#114031-financial-transactions). Elle fournit des conseils sur la transmission d'informations financières dans l'interface Teams et informe les développeurs des scénarios de paiement restreints sur la version mobile (Android et iOS) de leur application Teams.
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
* Vous pouvez déterminer si un compte est actif indéfiniment ou pendant une durée limitée. Lorsque le compte expire, l’application ne doit pas afficher l’interface utilisateur, le texte ou les liens indiquant la nécessité de payer.
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

N’incluez pas les domaines en dehors du contrôle de votre organisation (y compris les caractères génériques) et les services de tunneling dans les configurations de domaine de votre application. Les exceptions suivantes sont les suivantes :

* Si votre application utilise le OAuthCard d’Azure Bot Service, vous devez inclure `token.botframework.com` en tant que domaine valide, sinon le bouton **Se connecter** ne fonctionne pas.
* Si votre application repose sur SharePoint, vous pouvez inclure le site racine SharePoint associé en tant que domaine valide à l’aide de la propriété de contexte `{teamSiteDomain}`.

#### <a name="government-community-cloud-listings"></a>Référencements Cloud de la communauté du secteur public

Pour distribuer votre application aux utilisateurs de Government Community Cloud (GCC), le processus d'authentification doit identifier et acheminer les utilisateurs vers une URL spécifique à GCC ou attendue tout en évitant les listes en double dans le magasin Teams.

</details>

### <a name="sensitive-content"></a>Contenu sensible

[*Correction obligatoire*]

Votre application ne doit pas publier de données sensibles, telles que carte de crédit, détails de paiement, santé, recherche de contacts ou autres informations personnellement identifiables (PII) à un public qui n'a pas l'intention de voir le contenu.

L'application doit avertir les utilisateurs avant de télécharger des fichiers ou des exécutables (.exe) sur la machine ou l'environnement de l'utilisateur.

## <a name="general-functionality-and-performance"></a>Fonctionnalités et performances générales

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4 du marché commercial de Microsoft](/legal/marketplace/certification-policies#11404-functionality).

### <a name="launching-external-functionality"></a>Lancement des fonctionnalités externes

[*Correction obligatoire*]

Les applications ne doivent pas extraire les utilisateurs de Teams pour des scénarios utilisateur de base. Le contenu et les interactions de l'application doivent se produire dans les capacités de Teams, telles que les robots, les cartes adaptatives, les onglets et les modules de tâches.
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Liez les utilisateurs au sein de l'application Teams et non à un site ou une application externe. Pour les scénarios qui nécessitent une fonctionnalité externe, votre application doit obtenir une autorisation utilisateur explicite pour lancer la fonctionnalité.

Le texte de l'interface utilisateur du bouton qui lance la fonctionnalité externe doit inclure du contenu pour indiquer que l'utilisateur est retiré de l'instance Teams. Par exemple, incluez du texte tel que **Par ici vers Contoso.com** ou **Afficher dans Contoso.com**.

</details>

### <a name="compatibility"></a>Compatibilité

[*Correction obligatoire*]

Les applications doivent être entièrement fonctionnelles sur les dernières versions des systèmes d'exploitation et des navigateurs suivants :

* Microsoft Windows
* macOS
* Microsoft Edge&nbsp;
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
> Vous devez inclure les instructions de test détaillées suivantes pour valider la soumission de votre application :
>
> * **Étapes pour configurer les comptes de test d'application** au cas où l'application dépendrait de comptes externes pour l'authentification.
> * Résumé du **comportement attendu de l'application** pour les workflows de base au sein des équipes.
> * **Décrivez clairement les limitations**, conditions ou exceptions aux fonctionnalités, caractéristiques et livrables dans la description longue de l'application et les documents connexes.
> * **Mettre l'accent sur toutes les considérations** pour les testeurs lors de la validation de la soumission de votre application.  
> * **Pré-remplir les comptes de test avec des données factices** pour faciliter les tests.

### <a name="app-manifest"></a>Manifeste d'application

[*Correction obligatoire*]

Le manifeste de l'application Teams définit la configuration de votre application.

* Votre manifeste doit être conforme à un schéma de manifeste publié publiquement. Pour plus d'informations, consultez la [référence du manifeste](~/resources/schema/manifest-schema.md). Ne soumettez pas votre application à l'aide d'une version d'aperçu du manifeste.
* Si votre application inclut un bot ou une extension de messagerie, les détails du manifeste de l'application doivent être cohérents avec les métadonnées de Bot Framework, notamment le nom du bot, le logo, le lien vers la politique de confidentialité et le lien vers les conditions d'utilisation.
* Si votre application utilise Azure Active Directory pour l’authentification, incluez l’ID d’application (client) Microsoft Azure Active Directory (Azure AD) dans le manifeste. Pour plus d’informations, voir la [référence de manifeste](~/resources/schema/manifest-schema.md#webapplicationinfo).

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

Vous devez avoir une description courte et longue de votre application. Les descriptions dans les configurations de votre application et dans l’Espace partenaires doivent être identiques.
<br></br>
<details><summary>Développer pour en savoir plus</summary>

Les descriptions ne doivent pas directement ou par insinuation dénigrer une autre marque (détenue par Microsoft ou non). Assurez-vous que votre description n'inclut pas d'affirmations qui ne peuvent être justifiées. Par exemple, **Augmentation garantie de 200 % de l'efficacité**.

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
* Si vous devez référencer **Teams**, écrivez la première référence en tant que **Microsoft Teams**. Les références ultérieures peuvent être raccourcies à **Teams**.
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
* Indiquez que l’application est une offre de Microsoft, y compris à l’aide de slogans ou d’accroches Microsoft.
* Utilisez des noms de marque protégés par le droit d'auteur que vous ne possédez pas.
* Utilisez la langue suivante, sauf si vous êtes un partenaire Microsoft certifié :
  * **« ... certifié pour ... »**
  * **« ... optimisé par ... »**
* Inclure les fautes de frappe, les erreurs grammaticales.
* Mettez inutilement en majuscule l'intégralité du manifeste, la description longue AppSource ou le contenu de l'application.
* Incluez des liens vers AppSource.
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

* Concentrez-vous sur les capacités de votre application. Par exemple, comment les gens peuvent communiquer avec votre bot.
* Incluez du contenu qui représente précisément votre application.
* Utilisez le texte judicieusement.
* Cadrez les captures d'écran avec une couleur qui reflète votre marque et incluez du contenu marketing.

**À ne pas faire**

[*Correctif suggéré*]

* Afficher des appareils spécifiques, tels que des téléphones ou des ordinateurs portables.
* Afficher Chrome ou l’interface utilisateur qui ne se présente pas dans votre application.
* Capturez l’interface Teams ou l’interface utilisateur du navigateur dans vos captures d’écran.
* Incluez des maquettes qui reflètent de manière incorrecte l’interface utilisateur réelle de votre application, comme l’affichage de votre application utilisée en dehors de Teams.

> [!TIP]  
> Une vidéo peut être le moyen le plus efficace de communiquer pourquoi les gens doivent utiliser votre application. Une vidéo est également la première chose que les utilisateurs voient dans votre annonce. Pour plus d’informations, voir [créer une vidéo pour votre référencement de magasin](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video).

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

Si votre application prend en charge la localisation, votre package d’application doit inclure un fichier avec des traductions linguistiques qui s’affichent en fonction du paramètre de langue Teams. Le fichier doit être conforme au schéma de localisation Teams. Pour plus d'informations, consultez [Schéma de localisation Teams](~/concepts/build-and-test/apps-localization.md).

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
* Proposez différents moyens d'entrer en contact avec le service d'assistance en cas de problème, tels que la FAQ, la base de connaissances et l'adresse électronique.
* Validez les utilisateurs pour vous assurer qu'ils n'ont pas déjà une licence attribuée par un autre utilisateur.
* Notifier les utilisateurs après l'attribution de la licence.
* Guidez les utilisateurs à travers le bot de discussion Teams ou par e-mail, sur la façon d'ajouter l'application à Teams et de commencer.

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

Si la configuration de votre application à des fins de test est complexe, fournissez un document fonctionnel de bout en bout, les étapes de configuration de l'offre SaaS liée et des instructions pour la gestion des licences et des utilisateurs dans le cadre de vos « Notes de certification ».

> [!TIP]  
> Vous pouvez ajouter une vidéo sur le fonctionnement de votre application et de la gestion des licences pour aider l'équipe à effectuer les tests.

</details>

## <a name="tabs"></a>Onglets

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4.2 du marché commercial de Microsoft](/legal/marketplace/certification-policies#114042-tabs).
Si votre application comprend un onglet, assurez-vous qu'il respecte ces directives.
> [!TIP]
> Pour plus d'informations sur la création d'une expérience d'application de haute qualité, consultez les [directives de conception de l'onglet Teams](~/tabs/design/tabs.md).

</br>
<details><summary>Configuration</summary>

* La configuration de l'onglet **ne doit pas s'arrêter** un nouvel utilisateur. Fournissez un message sur la façon d’effectuer l’action ou le flux de travail. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-create-new-account.png" alt-text="validation-tabs-setup-create-new-acc":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-missing-forward-guidance.png" alt-text="validation-tabs-missing-fwd-guidance":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-new-user.png" alt-text="validation-tabs-set-up-new-user":::

* Pour la meilleure expérience de première exécution, authentifiez vos utilisateurs pendant la configuration de l'onglet et non après. L'authentification peut se produire en dehors de la fenêtre de configuration de l'onglet. [*Correctif suggéré*]

* L'utilisateur ne doit pas quitter l'expérience de configuration des onglets dans Teams pour créer du contenu en dehors de Teams, puis revenir à Teams pour l'épingler. L'écran de configuration de l'onglet doit expliquer la valeur de la configuration et comment configurer. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-profile-name.png" alt-text="validation-tabs-set-up-profile-name":::

* L’écran de configuration de l’onglet ne doit pas incorporer un site web entier. Concentrez-vous sur votre expérience de configuration. Par exemple, si vous créez une application de gestion de projet qui permet aux utilisateurs de configurer un projet dans un canal, gardez l’écran de configuration de l’onglet axé sur l’autorisation de l’utilisateur à sélectionner un projet à partir de votre application à configurer dans le canal. [*correctif obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-experience.png" alt-text="validation-tabs-setup-configuration-exp":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configuration-screen.png" alt-text="validation-tabs-set-up-configuration-screen":::

* L'écran de configuration de l'onglet ne doit pas demander aux utilisateurs d'intégrer une URL. Demander aux utilisateurs de configurer une URL lors de la configuration de l'onglet est une UX cassée, l'utilisateur quitte l'écran de configuration de l'onglet, acquiert l'URL, revient à l'écran de configuration et saisit l'URL. Une fonctionnalité Teams préexistante permet déjà aux utilisateurs d'épingler un lien vers un site Web dans le canal. Si votre application demande à l'utilisateur d'intégrer une URL de site Web lors de la configuration de l'onglet et que l'application est limitée à afficher l'intégralité du contenu du site Web dans l'onglet de chaîne, votre application n'offre pas de valeur significative à l'utilisateur. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configured-url.png" alt-text="validation-tabs-set-up-configured-url":::

    :::image type="content" source="../../../../assets/images/submission/validation-tabs-setup-configured-url-two.png" alt-text="validation-tabs-set-up-configured-url-two":::

</details>
</br>

<details><summary>Affichages</summary>

* La zone d’écran de connexion ne doit pas utiliser de grands logos. [*correctif obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-applogin.png" alt-text="validation-views-app-login":::

* Le contenu peut être simplifié en le décomposant sur plusieurs onglets. [*Correctif suggéré*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-multiple-tabs.png" alt-text="val-views-multiple-tabs":::

* Les onglets ne doivent pas avoir d’en-tête en double. Supprimez le logo dupliqué de l’iframe, car l’infrastructure d’onglet affiche déjà l’icône et le nom de l’application. [*correction suggérée*]

    :::image type="content" source="../../../../assets/images/submission/validation-views-duplicate-header-logo.png" alt-text="validation-views-duplicate-head-logo":::

</details>
</br>

<details><summary>Navigation</summary>

Voici les directives de navigation :

* Les onglets ne doivent pas fournir de navigation en conflit avec la principale navigation de Teams. Si vous fournissez une navigation à gauche dans votre onglet, elle ne doit pas inclure uniquement des icônes ou des icônes avec du texte empilé. Il ne doit pas s'agir d'un rail pliable avec la possibilité de voir des icônes avec du texte empilé (imitant la barre de navigation Teams). Incluez des icônes avec du texte en ligne ou uniquement du texte ou utilisez des menus hamburger au lieu du rail gauche de l'onglet. [*Correction obligatoire*]

Concevez votre application avec des composants Fluent UI [de base](~/concepts/design/design-teams-app-basic-ui-components.md) et [avancés](~\concepts\design\design-teams-app-advanced-ui-components.md).

:::image type="content" source="../../../../assets/images/submission/validation-navigation-static-tab.png" alt-text="validation-nav-static-tab":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-horizontal-rail.png" alt-text="validation-nav-horizontal-rail":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-left-navigation.png" alt-text="validation-navigation-left-nav":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-icon-text.png" alt-text="validation-nav-icon-text":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-collapsable-left-rail.png" alt-text="validation-nav-collapsable-left-rail":::

* Les onglets avec barre d'outils dans le rail gauche doivent laisser un espacement de 20 pixels à partir de la navigation gauche de Teams. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-spacing-between-toolbar.png" alt-text="validation-nav-spacing-between-toolbar":::

* Les pages secondaire et troisième d’un onglet doivent être ouvertes dans une vue de niveau deux (L2) et de niveau 3 (L3) dans la zone d’onglet principale, qui est parcourue via des barres de navigation ou une navigation à gauche. Vous pouvez également inclure les composants suivants pour faciliter la navigation dans les onglets : [*Correctif obligatoire*]
  * Boutons Retour
  * En-têtes de page
  * Menus d’hamburger
* L’onglet ne doit pas comporter de défilement horizontal. Les applications de tableau blanc et d’autres applications qui nécessitent un canevas plus grand pour permettre aux utilisateurs de collaborer sans expérience d’application rompue, peuvent utiliser le défilement horizontal en fonction de leurs besoins métier. [*correction suggérée*]

* Les liens profonds dans les onglets ne doivent pas être liés à une page web externe, mais dans Teams. Par exemple, les modules de tâches ou d’autres onglets. [*correctif obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-view-button-not-linked-static-tab.png" alt-text="validation-nav-view-button-not-linked-static-tab":::

* Les onglets ne doivent pas permettre aux utilisateurs de naviguer en dehors de Teams pour l'expérience de l'application principale. Les onglets peuvent rediriger en dehors des équipes pour les flux de travail non essentiels. Par exemple, pour créer un ticket d'assistance. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-within-configuration.png" alt-text="validation-nav-core-workflow-within-configuration":::

    :::image type="content" source="../../../../assets/images/submission/validation-navigation-core-workflow-redirects-outside.png" alt-text="validation-nav-core-workflow-redirects-outside":::

</details>
</br>

<details><summary>Facilité d’utilisation</summary>

* Les onglets doivent apporter une valeur au-delà de l'hébergement d'un site Web existant. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-provides-workflows.png" alt-text="validation-usability-app-provides-work-flows":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-website-i-framed.png" alt-text="validation-usability-website-i-frame":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-teams-app-identical-website.png" alt-text="validation-usability-teams-app-identical-websites":::

* Le contenu ne doit pas être tronqué ou se chevaucher dans l'onglet.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-content-truncation.png" alt-text="validation-usability-content-truncations":::

* Les utilisateurs doivent pouvoir annuler leur dernière action dans l’onglet.

* Les onglets dans un contexte personnel peuvent agréger le contenu des instances partagées de l’application. Par exemple, une application de gestion de projet avec un onglet configurable qui permet aux membres du canal de commenter le projet sur des cartes Kanban, doit agréger ce contenu et s'afficher dans l'application personnelle. [*Correctif suggéré*]

* Les onglets doivent répondre aux thèmes de Teams. Lorsqu’un utilisateur modifie le thème, le thème de l’application doit refléter la sélection.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-responsive-tabs.png" alt-text="onglet validation-usability-responsive-tab":::

    :::image type="content" source="../../../../assets/images/submission/validation-usability-unresponsive-tabs.png" alt-text="validation-usability-unresponsive-tab":::

* Les onglets doivent utiliser des composants de style Teams, tels que les polices Teams, les palettes de types, les palettes de couleurs, le système de grille, le mouvement, le ton de la voix, etc. dans la mesure du possible. Pour plus d’informations, consultez [instructions de conception de l’onglet](/microsoftteams/platform/tabs/design/tabs). [*correction suggérée*]

    :::image type="content" source="../../../../assets/images/submission/validation-usability-app-uses-diff-font.png" alt-text="validation-usability-app-uses-font":::

* Si la fonctionnalité de votre application nécessite des modifications des paramètres, incluez un onglet **Paramètres**. [*Correction suggérée*]
* Les onglets doivent suivre la conception de l’interaction Teams, par exemple, la navigation dans la page, la position et l’utilisation des dialogues, des hiérarchies d’informations, etc. Pour plus d’informations, consultez le[kit d’interface utilisateur Fluent de Microsoft Teams](~/concepts/design/design-teams-app-basic-ui-components.md)

* Le contenu de l’onglet dans l’IFrame ne doit pas inclure de fonctionnalités qui imitent les fonctionnalités principales de Teams. Par exemple, les bots, les extensions de messagerie, les appels, les réunions, etc.

* Le contenu de la page de destination des onglets configurables doit être contextuellement identique pour tous les membres de la chaîne.

* Le contenu de la page de destination des onglets configurables ne doit pas être limité à une utilisation individuelle et ne doit pas inclure de contenu personnel tel que **Mes tâches** ou **Mon tableau de bord**.

* Si votre application nécessite la fourniture d'une vue d'étendue personnelle pour que l'utilisateur améliore l'efficacité ou la productivité sur le lieu de travail, utilisez des vues filtrées, des liens profonds vers des applications personnelles ou accédez aux vues L2 ou L3 dans l'onglet configurable et gardez la page de destination contextuellement la même pour tous les utilisateurs.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-tab-personal-info.png" alt-text="validation-usability-configurable-tab-pers-info":::

* Les onglets configurables doivent avoir des fonctionnalités ciblées.

    :::image type="content" source="../../../../assets/images/submission/validation-usability-configurable-nested-tabs.png" alt-text="onglet validation-usability-configurable-nested-tab":::

* Les expériences d'onglet doivent être entièrement réactives sur mobile (Android et iOS).

> [!TIP]
>
> * Incluez un bot personnel avec un onglet personnel.
> * Autorisez les utilisateurs à partager du contenu à partir de leur onglet personnel.

</details>

## <a name="bots"></a>Bots

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4.3 du marché commercial de Microsoft](/legal/marketplace/certification-policies#114043-bots).

Si votre application inclut un bot, assurez-vous qu'il respecte ces directives.

> [!TIP]
> Pour plus d'informations sur la création d'une expérience d'application de haute qualité, consultez les [directives de conception de bot Teams](~/bots/design/bots.md).

</br>
<details><summary>Commandes de bot</summary>

L’analyse des entrées utilisateur et la prédiction de l’intention de l’utilisateur sont difficiles. Les commandes bot fournissent aux utilisateurs un ensemble de mots ou d’expressions que votre bot peut comprendre.

* Il est vivement recommandé de répertorier les commandes de bot prises en charge dans les configurations de votre application. Ces commandes s’affichent dans la zone de rédaction lorsqu’un utilisateur tente d’envoyer un message à votre bot.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-listed.png" alt-text="validation-bot-commands-list":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-not-listed.png" alt-text="validation-bot-commands-not-list":::

* Toutes les commandes prises en charge par votre bot doivent fonctionner correctement, y compris les commandes génériques telles que **Hi**, **Hello** et **Help**.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-help-command.png" alt-text="validation-bots-help-command":::

* Les commandes de bot ne doivent pas conduire un utilisateur dans une impasse, les commandes doivent toujours fournir une voie à suivre.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-commands-deadend.png" alt-text="validation-bot-commands-dead-end":::

> [!TIP]
> Pour les bots personnels, incluez un onglet **Aide** qui décrit davantage ce que votre bot peut faire.

</details>
</br>

<details><summary>Messages de bienvenue du bot</summary>

* Si l'application a un flux de configuration complexe (nécessite une licence d'entreprise ou manque d'un flux d'inscription intuitif), les robots de ces applications doivent toujours envoyer un message de bienvenue lors de la première exécution.

Pour une meilleure expérience, le message de bienvenue doit inclure la valeur offerte par le bot aux utilisateurs, qui ont installé le bot dans le canal, comment configurer le bot et décrire brièvement toutes les commandes de bot prises en charge. Vous pouvez afficher le message de bienvenue à l'aide d'une carte adaptative avec des boutons pour une meilleure convivialité. Pour plus d’informations, voir [comment déclencher un message de bienvenue du bot](~/bots/how-to/conversations/send-proactive-messages.md). Pour les applications sans flux de configuration complexe, vous pouvez choisir de déclencher un message de bienvenue lors de la première exécution du bot. Cependant, si un message de bienvenue est déclenché, il doit suivre les instructions relatives aux messages de bienvenue.

:::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message.png" alt-text="validation-bot-welcom-message":::

:::image type="content" source="../../../../assets/images/submission/validation-bot-no-welcome-message.png" alt-text="validation-bot-no-wel-come-message":::

* Les messages d’accueil du bot dans les canaux et les conversations sont facultatifs lors de la première exécution, en particulier si le bot est disponible pour un usage personnel et effectue des actions similaires. Votre bot ne doit pas envoyer de messages de bienvenue aux utilisateurs individuellement (c'est considéré comme du [spam](#botmessagespamming)). Le message doit également mentionner la personne qui a ajouté le bot.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-not-triggered.png" alt-text="validation-bot-welcome-message-not-trigger":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-welcome-message-triggered.png" alt-text="validation-bot-wel-message-trigger":::

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
  * N'envoyez pas plusieurs messages en une courte durée.
  * Envoyez un message avec des informations complètes.
  * Évitez les conversations à plusieurs tours pour terminer un seul flux de travail répétitif.
  * Utilisez un formulaire (ou un module de tâches) pour collecter toutes les entrées d'un utilisateur en même temps.
  * Les chatbots conversationnels basés sur la PNL peuvent utiliser une conversation à plusieurs tours pour rendre la discussion plus engageante et compléter un flux de travail.

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-task-module.png" alt-text="validation-bot-message-using-task-module":::

    :::image type="content" source="../../../../assets/images/submission/validation-bot-messages-using-mutliple-conversation.png" alt-text="validation-bot-messages-using-mutliple-conversations":::

* **Messages de bienvenue** : Ne répétez pas le même message de bienvenue à intervalles réguliers. Par exemple, lorsqu’un nouveau membre est ajouté à une équipe, n’envoyez pas de courrier indésirable aux autres membres avec un message de bienvenue. Envoyez un message personnel au nouveau membre.

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

Les applications qui fournissent uniquement des notifications avec du contenu tel que **Vous avez une nouvelle notification, cliquez pour afficher** et obligent l'utilisateur à naviguer en dehors de Teams pour tout le reste n'apportent pas de valeur significative dans Teams.

:::image type="content" source="../../../../assets/images/submission/validation-navigation-static-tab.png" alt-text="validation-nav-static-tab":::

:::image type="content" source="../../../../assets/images/submission/validation-navigation-horizontal-rail.png" alt-text="validation-nav-horizontal-rail":::

:::image type="content" source="../../../../assets/images/submission/validation-bot-notification-only-inadequete-info.png" alt-text="validation-bot-notifications-only-inadequete-info":::

> [!TIP]
> Prévisualisez les informations et fournissez des actions utilisateur de base en ligne dans la carte publiée afin que l'utilisateur n'ait pas à naviguer en dehors des équipes pour toutes les actions (quelle que soit la complexité).

</details>

## <a name="message-extensions"></a>Extensions de messages

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie 1140.4.4 du marché commercial de Microsoft](/legal/marketplace/certification-policies#114044-messaging-extensions).

Si votre application comprend une extension de messagerie, assurez-vous qu'elle respecte ces consignes.

> [!TIP]
> Pour plus d'informations sur la création d'une expérience d'application de haute qualité, consultez les [instructions de conception d'extension de messagerie Teams](~/messaging-extensions/design/messaging-extension-design.md).

</br>
<details><summary>Commandes d'action</summary>

Les extensions de messagerie basées sur les actions doivent effectuer les opérations suivantes :

* Autorisez les utilisateurs à déclencher des actions sur un message sans effectuer d'étapes intermédiaires, telles que la connexion.

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-no-intermediate-step.png" alt-text="validation-messaging-extension-no-intermediate-steps":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-intermediate-step-available.png" alt-text="validation-messaging-extension-intermediate-steps-available":::

* Passez le contexte du message à l’état de travail suivant. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-passes-message.png" alt-text="validation-messaging-extension-app-passes-messages":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-app-doesnot-pass-message.png" alt-text="validation-messaging-extension-app-doesnot-pass-messages":::

* Incorporez le nom de l'application hôte au lieu d'un verbe générique pour les commandes d'action déclenchées à partir d'un message de discussion, d'une publication de canal ou d'un appel à l'action dans les applications. Par exemple, utilisez **Démarrer une Réunion Skype** pour **Démarrer la réunion**, **Télécharger fichier à DocuSign** pour **Télécharger fichier**, etc. [*Correctif suggéré*]

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-host-name.png" alt-text="validation-messaging-extension-action-command-host-names":::

    :::image type="content" source="../../../../assets/images/submission/validation-messaging-extension-action-command-verb.png" alt-text="validation-messaging-extension-action-commands-verb":::

</details>
</br>

<details><summary>Liens d’aperçu (déploiement de liens)</summary>

[*Correction obligatoire*]

Les extensions de messagerie doivent prévisualiser les liens reconnus dans la zone de rédaction Teams. N'ajoutez pas de domaines hors de votre contrôle (qu'il s'agisse d'URL absolues ou de caractères génériques). Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` non valide. Les domaines de premier niveau sont également interdits. Par exemple : `*.com` ou `*.org`. [*Correction obligatoire*]

</details>
</br>

<details><summary>Commandes de recherche</summary>

* Les extensions de messagerie basées sur la recherche doivent fournir du texte qui aide les utilisateurs à rechercher efficacement. [*Correction obligatoire*]

    :::image type="content" source="../../../../assets/images/submission/validation-search-commands-text-available.png" alt-text="validation-search-command-text-available":::

* Les @mention exécutables doivent être claires, faciles à comprendre et lisibles.

    :::image type="content" source="../../../../assets/images/submission/validation-search-command-unclear-executable.png" alt-text="validation-search-commands-unclear-executable":::

</details>
</br>

<details><summary>Commandes d'action</summary>Extensions de messagerie basées sur la recherche uniquement pour les applications

[*Correction obligatoire*]

Les applications qui consistent en une extension de messagerie basée sur la recherche offrent une valeur utilisateur en partageant des cartes qui permettent des conversations contextuelles sans changement de contexte.

Pour réussir la validation d'une application d'extension de message uniquement basée sur la recherche, les éléments suivants sont requis comme référence pour garantir que l'expérience utilisateur n'est pas interrompue. Une carte partagée via une extension de messagerie apporte de la valeur dans Teams si :

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
<details><summary>Général</summary>

Utilisez les directives suivantes pour les extensions de réunion :

* Les applications d'extensibilité de réunion doivent offrir une expérience de réunion réactive et alignée sur l'expérience de réunion Teams. L'expérience en réunion est obligatoire, les expériences avant et après la réunion ne sont pas obligatoires.

  * Avec l'expérience d'application de pré-réunion, les utilisateurs peuvent rechercher et ajouter des applications de réunion. Les utilisateurs peuvent également effectuer des tâches préalables à la réunion, telles que l'élaboration d'un sondage pour sonder les participants à la réunion. Si votre application offre une expérience de pré-réunion, elle doit être pertinente pour le flux de travail de la réunion.

  * Avec l'expérience de l'application après la réunion, les utilisateurs peuvent afficher les résultats de la réunion, tels que les résultats d'un sondage ou des commentaires, ainsi que d'autres contenus d'application. Si votre application offre une expérience post-réunion, elle doit être pertinente pour le flux de travail de la réunion.

  * Avec l'expérience de l'application en réunion, vous pouvez impliquer les participants à la réunion pendant la réunion et améliorer l'expérience de la réunion pour tous les participants. Les participants ne doivent pas être emmenés en dehors de la réunion Teams pour terminer les flux de travail des utilisateurs principaux de votre application.

* Votre application doit offrir une valeur au-delà de la fourniture de scènes de mode Together personnalisées dans Teams.

* La fonctionnalité d'étape de réunion partagée ne peut être lancée que via l'application de bureau Teams. Cependant, l'expérience de consommation de l'étape de réunion partagée doit être utilisable et non interrompue lorsqu'elle est visualisée sur des appareils mobiles.

> [!TIP]
> Vous devez déclarer `groupchat` en tant qu'étendue sous `configurableTabs` et `meetingDetailsTab`, ou `meetingChatTab` et `meetingSidePanel` en tant que propriété de contexte dans le manifeste pour activer votre application pour les réunions sur Teams mobile.

</details>

</br>
<details><summary>Expérience avant et après la réunion</summary>

* Les écrans avant et après la réunion doivent respecter les directives générales de conception des onglets. Pour plus d'informations, consultez [Directives de conception Teams](~/tabs/design/tabs.md).
* Les onglets ne doivent pas avoir de défilement horizontal.
* Les onglets doivent avoir une disposition organisée lors de l'affichage de plusieurs éléments. Par exemple, plus de 10 sondages ou enquêtes, voir [exemple de mise en page](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* Votre application doit informer les utilisateurs lorsque les résultats d'une enquête ou d'un sondage sont exportés en indiquant, **Résultats téléchargés avec succès**.

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

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button.png" alt-text="validation-in-meeting-exp-back-buttons":::

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-exp-back-button-absent.png" alt-text="validation-in-meeting-exp-back-buttons-absent":::

* Ne doit pas inclure plus d'un bouton de fermeture. Cela peut dérouter les utilisateurs car il existe déjà un bouton d'en-tête intégré pour fermer l'onglet.
* Ne doit pas avoir de défilement horizontal.

</details>

</br>
<details><summary>Boîtes de dialogue en réunion</summary>

* Doit être utilisé avec parcimonie et pour des scénarios légers et axés sur les tâches.
* Doivent afficher le contenu dans une seule colonne et ne pas avoir plusieurs niveaux de navigation.
* Ne doivent pas utiliser de modules de tâche.
* Doivent s’aligner sur le centre de la phase de réunion.

    :::image type="content" source="../../../../assets/images/submission/validation-in-meeting-dialog-not-aligned.png" alt-text="validation-in-meeting-dialog-not-align":::

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

Si votre application utilise les [API de flux d'activité fournies par Microsoft Graph](/graph/teams-send-activityfeednotifications), assurez-vous qu'elle respecte les directives suivantes.
<br></br>
<details><summary>Général</summary>

* Tous les déclencheurs de notification spécifiés dans la configuration de votre application doivent fonctionner.
* Les notifications doivent être localisées selon les langues de prise en charge configurées pour votre application.
* Les notifications doivent s’afficher dans les cinq secondes après l’action d’un utilisateur.

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

    :::image type="content" source="../../../../assets/images/submission/validation-365-compliance-publisher-verification.png" alt-text="validation-365-compliance-publisher-verifications":::

* **Attestation d’éditeur** : processus dans lequel vous partagez des informations générales, de gestion des données et de sécurité et de conformité pour permettre aux clients potentiels de prendre des décisions informées sur l’utilisation de votre application.

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Si vous soumettez une application qui n'a pas été répertoriée auparavant, vous ne pouvez pas compléter officiellement l'attestation d'éditeur tant que votre application n'est pas dans le Teams Store. Si vous êtes mettez à jour une application répertoriée, achevez l’attestation d’éditeur avant de soumettre la dernière version de l’application.

</details>

## <a name="advertising"></a>Publicité

:::image type="icon" source="../../../../assets/icons/certificate-icon-16.png":::Cette section est conforme à la [stratégie du marché commercial de Microsoft, numéro 1140.7](/legal/marketplace/certification-policies#11407-advertising).

Les applications ne doivent pas afficher de publicité, y compris les publicités dynamiques, les bannières publicitaires et les publicités dans les messages.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un compte d’Espace partenaires](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)

## <a name="see-also"></a>Voir aussi

* [Distribuer votre application.](~/concepts/deploy-and-publish/apps-publish-overview.md)
* [Préparer l'envoi de votre magasin](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [Tester et déboguer votre application](~/concepts/build-and-test/debug.md)
* [Créer un compte de développeur de l’Espace partenaires](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
