---
title: Instructions de validation du magasin Microsoft Teams
description: Décrit les instructions que chaque application soumise au magasin Teams (AppSource) doit suivre.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.localizationpriority: high
ms.openlocfilehash: 96bcb97fbb6189a657c9ac2aea167aaaa7f74592
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720224"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Instructions de validation du magasin Microsoft Teams

Le fait de suivre ces instructions augmente la probabilité que votre application réussisse le processus d’intégration au magasin Microsoft Teams. Ces instructions spécifiques à Teams complètent les [stratégies de certification de la place de marché commerciale](/legal/marketplace/certification-policies) Microsoft et sont fréquemment mises à jour pour refléter les nouvelles fonctionnalités, les commentaires des utilisateurs et les modifications apportées aux règles d’entreprise.

> [!NOTE]
> Certaines instructions peuvent ne pas être applicables à votre application. Par exemple, si votre application n’inclut pas de bot, vous pouvez ignorer les instructions liées aux bots.

## <a name="value-proposition"></a>Proposition de valeur

### <a name="app-name"></a>Nom de l'application

Le nom d’une application joue un rôle essentiel dans la façon dont les utilisateurs la découvrent dans le magasin. N’oubliez ce qui suit concernant les noms d’application :

* Le nom doit inclure des termes susceptibles d’intéresser vos utilisateurs.
* Les noms des principales fonctionnalités Teams&#8212;telles que **Conversation**, **Contacts**, **Calendrier**, **Appels**, **Fichiers**, **Activité**, **Équipes**, **Applications** et **Aide**&#8212; ne doivent pas être inclus dans le nom de votre application.
* Les noms communs doivent être précédés ou suivis du nom du développeur (par exemple, **Tâches Contoso** plutôt que **Tâches**).
* Ne doit pas utiliser **Teams** ou d’autres noms de produits Microsoft qui pourraient indiquer à tort une association de marque ou de vente. (Pour plus d’informations sur le référencement des logiciels, des produits et des services Microsoft, voir les [Recommandations en matière d’image de marque et de marque déposée Microsoft](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)).
* Si votre application fait partie d’un partenariat officiel avec Microsoft, le nom de votre application doit être donné en premier (par exemple, **Connecteur Contoso pour Microsoft Teams**).
* Ne doit pas copier le nom d’une application répertoriée dans le magasin ou une autre offre sur la place de marché commerciale.
* Ne doit pas contenir de termes vulgaires ou désobligeants. Le nom ne doit pas non plus inclure un langage qui manque d’égard en matière de race ou de culture.
* Doit être unique. Par exemple, vous ne pouvez pas lister plusieurs applications pour différentes régions avec le même nom et la même fonctionnalité.

### <a name="suitable-for-workplace-consumption"></a>Convient à une utilisation dans l’espace de travail

Le contenu de l’application doit être adapté à une utilisation générale dans l’espace de travail et respecter toutes les restrictions répertoriées dans les stratégies de certification de la place de marché commerciale. Le contenu lié à la religion, à la politique, aux jeux et aux divertissements prolongés est interdit. Pour plus d’informations, voir les [stratégies de certification de la place de marché commerciale](/legal/marketplace/certification-policies#10010-inappropriate-content).

Votre application doit faciliter la collaboration de groupe, améliorer la productivité d’un individu, ou les deux. Les applications destinées à la socialisation et à l’esprit d’équipe doivent être collaboratives et conçues pour plusieurs participants. Ces types d’applications ne doivent pas non plus nécessiter un investissement en temps considérable ou avoir un impact négatif sur la productivité.

### <a name="similar-platforms-and-services"></a>Plateformes et services similaires

Les applications doivent se concentrer sur l’expérience Teams et ne pas inclure de noms, d’icônes ou d’images provenant d’autres services ou plateformes similaires de collaboration basée sur la conversation, à moins que votre application propose une interopérabilité spécifique.

### <a name="feature-names"></a>Noms de fonctionnalité

Le nom des fonctionnalités d’application dans les boutons et tout autre texte d’interface utilisateur ne doivent pas être en conflit avec la terminologie réservée à Teams et à d’autres produits Microsoft. Par exemple, **Commencer la réunion**, **Passer des appels** ou **Démarrer une conversation**. Incluez le nom de votre application si vous ne pouvez pas l’éviter complètement, par exemple, **Commencer une réunion Contoso** au lieu de **Commencer la réunion**.

## <a name="security"></a>Sécurité

### <a name="microsoft-365-app-compliance-program"></a>Programme de conformité d’Application Microsoft 365

Le [Programme de conformité d’Application Microsoft 365](/microsoft-365-app-certification/overview) est destiné à aider les organisations à évaluer et à gérer les risques en évaluant les informations de sécurité et de conformité concernant votre application. Si vous publiez une application dans le magasin Teams, vous devez effectuer les niveaux suivants du programme :

* [Vérification de l’éditeur](/azure/active-directory/develop/publisher-verification-overview) : permet aux administrateurs et aux utilisateurs finaux de comprendre l’authenticité des développeurs d’applications procédant à une intégration avec la Plateforme d'identités Microsoft. Une fois terminé, un badge bleu « vérifié » s’affiche sur la boîte de dialogue de consentement Azure Active Directory (Azure AD) et d’autres écrans. Pour plus d’informations, voir [forum aux questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [comment marquer votre application comme éditeur vérifié](/azure/active-directory/develop/mark-app-as-publisher-verified) et [résoudre les problèmes de vérification de l’éditeur](/azure/active-directory/develop/troubleshoot-publisher-verification).
* [Attestation d’éditeur](/microsoft-365-app-certification/docs/attestation) : processus dans lequel vous partagez des informations générales, de gestion des données et de sécurité et de conformité pour permettre aux clients potentiels de prendre des décisions informées sur l’utilisation de votre application.

> [!NOTE]
> Si vous soumettez une application qui n’a pas été répertoriée précédemment, vous ne pouvez pas officiellement terminer l’attestation d’éditeur tant que votre application n’est pas dans le magasin Teams. Si vous êtes mettez à jour une application répertoriée, achevez l’attestation d’éditeur avant de soumettre la dernière version de l’application.

### <a name="bots"></a>Bots

Pour les applications qui utilisent Microsoft Azure Bot Service (par exemple, les bots et les extensions de messagerie), vous devez respecter toutes les conditions définies dans les [Conditions d’utilisation des services en ligne Microsoft](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

Les bots doivent toujours demander l’autorisation de télécharger un fichier et afficher un message de confirmation après le téléchargement du fichier.

### <a name="external-domains"></a>Domaines externes

Dans la plupart des cas, vous ne devez pas inclure de domaines qui ne sont pas contrôlables par votre organisation (y compris les caractères génériques) et des services de tunneling dans les configurations de domaine de votre application. Les exceptions suivantes incluent :

* Si votre application utilise le OAuthCard d’Azure Bot Service, vous devez inclure `token.botframework.com` en tant que domaine valide, sinon le bouton **Se connecter** ne fonctionne pas.
* Si votre application repose sur SharePoint, vous pouvez inclure le site racine SharePoint associé en tant que domaine valide à l’aide de la propriété de contexte `{teamSiteDomain}`.

### <a name="authentication"></a>Authentification

Pour plus d’informations sur l’implémentation de l’authentification d’application, voir [l’authentification dans Teams](~/concepts/authentication/authentication.md).

#### <a name="authenticating-with-external-services"></a>Authentification avec des services externes

N’oubliez pas ce qui suit si votre application authentifie les utilisateurs avec un service externe.

* **Expériences d’inscription, de connexion et de déconnexion** :
  * Les applications qui dépendent de comptes ou de services externes doivent fournir des expériences claires et simples d’inscription, de connexion et de déconnexion.
  * Lorsqu’un utilisateur se déconnecte, il doit se déconnecter uniquement de l’application et rester connecté à Teams.
* **Expériences de partage de contenu**: les applications qui nécessitent une authentification auprès d’un service externe pour partager du contenu dans les canaux Teams doivent indiquer clairement dans la documentation d’aide (ou des ressources similaires) comment déconnecter ou annuler le partage de contenu si cette fonctionnalité est prise en charge sur le service externe. Cela ne signifie pas que la possibilité d’annuler le partage de contenu doit être présente dans votre application Teams.

#### <a name="government-community-cloud-listings"></a>Référencements Cloud de la communauté du secteur public

Pour distribuer votre application aux utilisateurs Cloud de la communauté du secteur public (Cloud de la communauté du secteur public) tout en évitant les référencements en double dans le magasin Teams, le processus d’authentification doit identifier et rediriger les utilisateurs vers une URL prévue ou spécifique au Cloud de la communauté du secteur public.

### <a name="sensitive-content"></a>Contenu sensible

Votre application ne doit pas publier de données sensibles, telles que des données de carte bancaire ou d’instrument de paiement financier. L’application ne doit pas non plus afficher l’intégrité, le suivi des contacts ou d’autres informations d’identification personnelle (PII) à une audience non destinée à afficher ce contenu.

Avertissez les utilisateurs avant que votre application télécharge des fichiers ou des exécutables (.exe) sur l’ordinateur ou l’environnement de l’utilisateur.

### <a name="financial-information"></a>Informations financières

Les applications ne doivent pas demander aux utilisateurs d’effectuer des paiements dans l’interface Teams. Les détails de l’instrument financier ne doivent pas être transmis aux utilisateurs via une interface de bot.

Vous pouvez établir un lien vers des services de paiement externes et sécurisés uniquement si vous avez effectué la divulgation appropriée dans vos conditions d’utilisation, déclaration de confidentialité ou toute page de profil ou site web avant que l’utilisateur n’accepte d’utiliser l’application.

Les applications qui s’exécutent sur la version iOS ou Android de Teams doivent respecter les instructions suivantes :

* Les applications ne doivent pas comporter d’achats dans l’application, d’offres d’essai ou d’interface utilisateur destinée à inciter à la vente de versions payantes, ni de liens vers des magasins en ligne où les utilisateurs peuvent acheter ou acquérir d’autres contenus, applications ou compléments.
* Si votre application nécessite un compte, les utilisateurs doivent pouvoir ouvrir un compte gratuitement. L’utilisation du terme **compte gratuit** ou **gratuit** est interdite.
* Vous pouvez déterminer si un compte est actif indéfiniment ou pendant une durée limitée, mais si le compte expire, aucune interface utilisateur, aucun texte ou lien indiquant la nécessité de payer ne peut s’afficher.
* Les pages des conditions d’utilisation et de la déclaration de confidentialité de votre application ne doivent pas être liées à une interface utilisateur ou à des liens commerciaux payants.

> [!NOTE]
> Les descriptions du Windows Store Teams peuvent inclure des plans d’abonnement d’application ou des licences à acheter. Pour plus d’informations, consultez [inclure une offre SaaS avec votre application](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md).

## <a name="general-functionality-and-performance"></a>Fonctionnalités et performances générales

### <a name="launching-external-functionality"></a>Lancement des fonctionnalités externes

Les applications ne doivent pas extraire les utilisateurs de Teams pour des scénarios utilisateur de base. Le contenu et les interactions de l’application peuvent se produire au sein des fonctionnalités Teams, telles que les bots, les cartes et les modules de tâche.

Vous devez lier les utilisateurs à Teams et non à un site ou à une application externe. Pour les scénarios qui nécessitent des fonctionnalités externes, votre application doit avoir une autorisation utilisateur explicite pour lancer cette fonctionnalité.

### <a name="compatibility"></a>Compatibilité

Les applications doivent être entièrement opérationnelles sur les systèmes d’exploitation et navigateurs suivants :

* Microsoft Windows 7 et versions ultérieures
* macOS 10.10 et versions ultérieures
* Microsoft Edge 12 et versions ultérieures
* Mozilla Firefox 47.0 et versions ultérieures
* Google Chrome 51.0 et versions ultérieures
* iOS/iPadOS 9.0 et versions ultérieures
* Android 4.4 et versions ultérieures

### <a name="response-time"></a>Temps de réponse

Les applications Teams doivent répondre dans un délai raisonnable, ce qui varie selon la fonctionnalité.

* Les onglets doivent répondre dans un délai de trois secondes ou afficher un message de chargement ou un avertissement.
* Les bots doivent répondre aux commandes de l’utilisateur dans un délai de deux secondes ou afficher un indicateur de saisie.
* Les extensions de messagerie doivent répondre aux commandes de l’utilisateur dans un délai de cinq secondes.
* Les notifications doivent s’afficher dans un délai de cinq secondes après l’action de l’utilisateur.

## <a name="app-package-and-store-listing"></a>Package d’application et description dans le Store

Les packages d’application doivent être correctement formatés et inclure toutes les informations et composants requis.

### <a name="app-manifest"></a>Manifeste d'application

L’application Teams définit les configurations de votre application.

* Votre manifeste doit se conformer au dernier schéma de manifeste. Pour plus d’informations, voir la [référence de manifeste](~/resources/schema/manifest-schema.md).
* Si votre application inclut une extension de bot ou de messagerie, votre manifeste doit être cohérent avec les métadonnées Bot Framework, notamment le nom du bot, le logo, le lien de stratégie de confidentialité et le lien des conditions d’utilisation.
* Si votre application utilise Azure Active Directory (Azure AD) pour l’authentification, incluez l’ID d’application Azure AD (client) dans le manifeste. Pour plus d’informations, consultez la [référence de manifeste](~/resources/schema/manifest-schema.md#webapplicationinfo).

### <a name="app-icons"></a>Icônes d’application

Les icônes sont l’un des principaux éléments que les utilisateurs voient lors de la navigation dans le magasin Teams. Vos icônes doivent communiquer la marque et l’objectif de votre application tout en se conformant aux exigences suivantes :

* Votre package d’application doit inclure deux versions PNG de l’icône de votre application : une icône de couleur et une icône de plan.
* La version de couleur de votre icône s’affiche dans la plupart des scénarios Teams et doit être de 192x192 pixels. Votre symbole d’icône (96x96 pixels) peut être de n’importe quelle couleur ou couleurs, mais il doit être sur un arrière-plan carré plein ou entièrement transparent.
* La version de plan de votre icône s’affiche lorsque votre application est en cours d’utilisation et « soulevée » dans la barre de l’application sur le côté gauche de Teams et lorsqu’un utilisateur épingle l’extension de messagerie de votre application. Elle doit être de 32x32 pixels et peut être blanche avec un arrière-plan transparent ou transparente avec un arrière-plan blanc (aucune autre couleur n’est autorisée). L’icône ne doit pas avoir de remplissage supplémentaire autour du symbole.
* Les icônes correctement dimensionnées et formatées doivent être incluses dans votre package d’application. Les icônes doivent également correspondre à ce qui est envoyé avec les métadonnées du référencement au magasin.

Pour plus d’informations, les meilleures pratiques et des exemples, voir les [recommandations d’icône](~/concepts/build-and-test/apps-package.md#app-icons) de l’application Teams.

### <a name="app-descriptions"></a>Descriptions de l’application

Vous devez avoir une description courte et longue de votre application. Les descriptions dans les configurations de votre application et dans l’Espace partenaires doivent être identiques.

Les descriptions ne doivent pas désapprouver directement ou par insinuation une autre marque (propriété de Microsoft ou autre). Assurez-vous que votre description n’inclut pas des revendications qui ne peuvent pas être garanties (par exemple, « Augmentation garantie de 200 % en efficacité »).

#### <a name="short-description"></a>Description courte

Une brève description est un résumé concis de votre application qui met en évidence sa proposition de valeur et s’adresse à votre public cible.

**À faire :**

* Votre description courte doit tenir sur une seule phrase.
* Mettez les informations les plus importantes en premier.
* Incluez des mots clés que les clients sont susceptibles de rechercher.

**À ne pas faire :**

* Répétez le nom de votre application.
* Utilisez le mot **application** dans la description courte.

#### <a name="long-description"></a>Description longue

La description longue peut fournir un narratif attrayant qui met en évidence la proposition de valeur de votre application, le public principal et le secteur cible. Bien que cette description puisse contenir jusqu’à 4 000 caractères, la plupart des utilisateurs ne lisent qu’entre 300 et 500 mots.

**À faire :**

* Utilisez Markdown pour mettre en forme votre description.
* Utilisez la voix active et parlez directement aux utilisateurs. Par exemple, *Vous pouvez...*.
* Répertoriez les fonctionnalités à l’aide de points à puces pour faciliter l’examen de la description.
* Décrivez clairement les limitations, conditions ou exceptions de la fonctionnalité, des fonctions et livrables décrits dans le référencement et les documents associés avant que l’utilisateur installe votre application. Les fonctionnalités Teams que votre application prend en charge doivent être liées aux fonctions principales décrites dans votre référencement.
* Vérifiez que la description de l’application correspond aux fonctionnalités disponibles dans l’application Teams. Toute référence à des flux de travail en dehors de l’application Teams doit être limitée et distinctement appelée à partir des fonctionnalités de l’application Teams.
* Incluez un lien d’aide ou de support.
* Faites référence à **Microsoft 365** au lieu d’**Office 365**.
* Si vous devez référencer **Teams**, écrivez la première référence en tant que **Microsoft Teams**. Les références suivantes peuvent être raccourcies en **Teams**.
* Utilisez le langage suivant pour décrire le fonctionnement de l’application avec Teams (ou Microsoft 365) :
  * « ... fonctionne avec Microsoft Teams. »
  * « ... fonctionner avec Microsoft Teams. »
  * « ... dans Microsoft Teams. »
  * « ... pour Microsoft Teams. »
  * « ... intégré à Microsoft Teams. »
  * « ... créé pour... »
  * « ... développé pour... »
  * « ... conçu pour... »


**À ne pas faire :**

* Supérieure à 500 mots.
* Abrégez **Microsoft** en tant que **MS** ou **MSFT**.
* Indiquez que l’application est une offre de Microsoft, y compris à l’aide de slogans ou d’accroches Microsoft.
* Utilisez des noms de marque protégés par des droits d’auteur que vous ne possédez pas.
 * Utilisez le langage suivant, sauf si vous êtes un partenaire Microsoft certifié :
  * « ... certifié pour ... »
  * « ... optimisé par ... »
* Inclut les fautes de frappe, les erreurs grammaticales et les majuscules inutiles, telles que **Utilisateurs** au lieu de **utilisateurs**.
* Incluez des liens vers AppSource.
* Effectuez des revendications non vérifiées (par exemple : meilleure, supérieure, classée), sauf si elles sont accompagnées de la source de la revendication.
* Comparez votre offre avec d’autres offres du marché.



### <a name="screenshots"></a>Captures d’écran

Les captures d’écran fournissent un aperçu visuel évident de votre application pour compléter le nom, l’icône et les descriptions de votre application. N’oubliez pas de qui suit en ce qui concerne les captures d’écran :

* Vous pouvez avoir jusqu’à cinq captures d’écran par référencement.
* Les types de fichiers pris en charge sont PNG, JPEG et GIF.
* Les dimensions doivent être de 1 366 x 768 pixels.
* Taille maximale de 1 024 Ko.

**À faire :**

* Concentrez-vous sur les fonctionnalités de votre application (par exemple, comment les personnes peuvent communiquer avec votre bot).
* Incluez du contenu qui représente précisément votre application.
* Utilisez le texte judicieusement.
* Captures d’écran avec une couleur qui reflète votre marque et inclut du contenu marketing, similaire à l’exemple [Référencement Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) (les exigences de dimensions s’appliquent à l’image entière et pas seulement à la capture d’écran).

**À ne pas faire :**

* Afficher des appareils spécifiques, tels que des téléphones ou des ordinateurs portables.
* Afficher Chrome ou l’interface utilisateur qui ne se présente pas dans votre application.
* Capturez l’interface Teams ou l’interface utilisateur du navigateur dans vos captures d’écran.
* Incluez des maquettes qui reflètent de manière incorrecte l’interface utilisateur réelle de votre application, comme l’affichage de votre application utilisée en dehors de Teams.

> [!TIP]
> Une vidéo peut être le moyen le plus efficace pour expliquer pourquoi les personnes doivent utiliser votre application. Une vidéo est également la première chose que les utilisateurs voient dans votre référencement (par défaut, une vidéo s’affiche avant les captures d’écran). Pour plus d’informations, voir [créer une vidéo pour votre référencement de magasin](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video).

### <a name="privacy-policy"></a>Déclaration de confidentialité

La politique de confidentialité peut être spécifique à votre application Teams ou à une stratégie globale pour tous vos services.

* Si vous utilisez un modèle de déclaration de confidentialité générique, vous devez référencer des **services**, des **applications** et des **plateformes** pour inclure votre application Teams et votre service ou site web.
* Doit inclure la façon dont vous traitez le stockage, la rétention et la suppression des données utilisateur. Vous devez également décrire les contrôles de sécurité que vous utilisez pour la protection des données.
* Doit inclure vos informations de contact.
* Ne doit pas contenir d’URL rompues ou à des fins bêta ou intermédiaire.
* Ne doit pas inclure de liens vers AppSource.

### <a name="terms-of-use"></a>Conditions d’utilisation

Vos conditions d’utilisation doivent être spécifiques et applicables à votre offre.

### <a name="support-links"></a>Liens vers le support technique

Les URL vers le support technique de votre application ne doivent pas nécessiter d’authentification. Par exemple, les utilisateurs ne doivent pas avoir à se connecter pour vous contacter.

### <a name="localization"></a>Localisation

Si votre application prend en charge la localisation, votre package d’application doit inclure un fichier avec des traductions linguistiques qui s’affichent en fonction du paramètre de langue Teams. Le fichier doit être conforme au schéma de localisation Teams. Pour plus d’informations, voir le [Schéma de localisation Teams](~/concepts/build-and-test/apps-localization.md).

## <a name="tabs"></a>Onglets

Si votre application inclut un onglet, assurez-vous qu’il respecte ces recommandations.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les [recommandations Teams de conception d’onglets](~/tabs/design/tabs.md).

### <a name="setup"></a>Configuration

* La configuration de l’onglet ne doit pas être une impasse pour un nouvel utilisateur. Fournissez un message sur la façon d’effectuer l’action ou le flux de travail.
* L’authentification doit avoir lieu pendant la configuration de l’onglet et non après.

### <a name="views"></a>Affichages

* La zone d’écran de connexion ne doit pas utiliser de grands logos ni afficher une page web entière.
* Le contenu peut être simplifié en le divisant sur plusieurs onglets.
* Les onglets ne doivent pas avoir d’en-tête en double. Supprimez le logo de l’IFrame, car l’infrastructure d’onglet affiche déjà l’icône et le nom de l’application.

### <a name="navigation"></a>Navigation

* Les onglets ne doivent pas avoir plus de trois niveaux de navigation.
* Les onglets ne doivent pas fournir de navigation en conflit avec la principale navigation de Teams.
* Les pages secondaires et tertiaires d’un onglet doivent être ouvertes dans un affichage de niveau 2 et 3 dans la zone d’onglet principale, qui est accessible via des barres de navigation ou le volet de navigation gauche. Vous pouvez également inclure les composants suivants pour faciliter la navigation par onglets :
    * Boutons Retour
    * En-têtes de page
    * Menus d’hamburger
* La tabulation ne doit pas avoir de défilement horizontal.
* Les liens profonds dans les onglets ne doivent pas être liés à une page web externe, mais à un autre emplacement dans Teams. Par exemple, les modules de tâches ou d’autres onglets.
* Les onglets ne doivent pas permettre aux utilisateurs de naviguer en dehors de Teams pour l’expérience d’application principale.

### <a name="usability"></a>Facilité d’utilisation

* Les onglets doivent fournir une valeur au-delà du simple hébergement d’un site web existant.
* Les utilisateurs doivent pouvoir annuler leur dernière action dans l’onglet.
* Les onglets dans un contexte personnel peuvent agréger le contenu des instances partagées de l’application.
* Les onglets doivent répondre aux thèmes de Teams. Lorsqu’un utilisateur modifie le thème, le thème de l’application doit refléter la sélection.
* Les onglets doivent utiliser, dans la mesure du possible, des composants de style Teams, tels que les polices Teams, les rampes de types, les palettes de couleurs, le système de grille, le mouvement, le ton de la voix, etc.
* Si les fonctionnalités de votre application nécessitent des modifications dans les paramètres, incluez un onglet **Paramètres**.
* Les onglets doivent suivre, dans la mesure du possible, la conception de l’interaction Teams, telle que la navigation dans la page, la position et l’utilisation des boîtes de dialogue, des hiérarchies d’informations, etc.
* Le contenu de l’onglet dans l’IFrame ne doit pas inclure de fonctionnalités qui imitent les fonctionnalités principales de Teams. Par exemple, les bots, les extensions de messagerie, les appels, les réunions, etc.

> [!TIP]
>
> * Incluez un bot personnel avec un onglet personnel.
> * Autorisez les utilisateurs à partager du contenu à partir de leur onglet personnel.

## <a name="bots"></a>Bots

Si votre application inclut un bot, assurez-vous qu’il respecte ces recommandations.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les [recommandations Teams de conception de bot](~/bots/design/bots.md).

### <a name="bot-commands"></a>Commandes de bot

Il est difficile d’analyser des entrées utilisateur et de prédire l’intention de l’utilisateur. Les commandes de bot fournissent aux utilisateurs un ensemble de mots ou d’expressions que votre bot comprend afin qu’ils (et votre bot) n’aient pas à deviner.

* Il est vivement recommandé de répertorier les commandes de bot prises en charge dans les configurations de votre application. Ces commandes s’affichent dans la zone de rédaction lorsqu’un utilisateur tente d’envoyer un message à votre bot.
* Toutes les commandes que votre bot prend en charge doivent fonctionner correctement, y compris les commandes **Bonjour**, **Hello** et **Aide**.

> [!TIP]
> Pour les bots personnels, incluez un onglet **Aide** qui décrit davantage ce que votre bot peut faire.

### <a name="bot-welcome-messages"></a>Messages de bienvenue du bot

* Les bots doivent presque toujours envoyer un message de bienvenue lors de la première exécution. Pour une expérience de qualité, le message doit inclure la proposition de valeur de votre bot, la configuration du bot et décrire brièvement toutes les commandes de bot prises en charge. Vous pouvez afficher le message à l’aide d’une carte adaptative avec des boutons pour une meilleure utilisation. Pour plus d’informations, voir [comment déclencher un message de bienvenue du bot](~/bots/how-to/conversations/send-proactive-messages.md).
* Les messages d’accueil du bot dans les canaux et les conversations sont facultatifs lors de la première exécution, en particulier si le bot est disponible pour un usage personnel et effectue des actions similaires. Si votre bot envoie des messages de bienvenue, il ne doit pas les envoyer aux utilisateurs individuellement (ceci est considéré comme [du courrier indésirable](#bot-message-spamming)). Le message doit également mentionner la personne qui a ajouté le bot.
* Les bots de notification uniquement doivent envoyer un message de bienvenue informant qu’il ne répondra pas aux messages des utilisateurs.

> [!TIP]
> Dans les messages de bienvenue destinés à des utilisateurs individuels, une visite guidée en carrousel peut fournir une vue d’ensemble efficace de votre bot et de toutes les autres fonctionnalités de l’application. Il est recommandé d’inclure des boutons permettant aux utilisateurs d’essayer des commandes de bot. Par exemple, **Créer une tâche**.

### <a name="bot-message-spamming"></a>Message de bot indésirables

Les bots ne doivent pas envoyer de courrier indésirable aux utilisateurs en envoyant plusieurs messages en une courte succession.

* **Messages de bot dans les canaux et les conversations** : ne pas envoyer de courrier indésirable aux utilisateurs en créant des publications distinctes. Créez un billet unique avec des réponses dans le même fil de discussion.
* **Messages de bot dans les applications personnelles** : n’envoyez pas plusieurs messages successivement. Envoyez un message avec des informations complètes. Évitez les conversations à plusieurs tours pour terminer un seul flux de travail. Envisagez plutôt d’utiliser un formulaire (ou un module de tâche) pour collecter toutes les entrées d’un utilisateur en une fois.
* **Messages de bienvenue** : répéter le même message de bienvenue à intervalles réguliers n’est pas autorisé et considéré comme du courrier indésirable. Par exemple, lorsqu’un nouveau membre est ajouté à une équipe, n’envoyez pas de courrier indésirable aux autres membres avec un message de bienvenue. Envoyez un message personnel au nouveau membre à la place.

### <a name="bot-notifications"></a>Notifications de bot

Les notifications de bot doivent inclure du contenu pertinent pour l’étendue que vous définissez pour le bot (équipe, conversation ou personnel).

### <a name="bots-and-adaptive-cards"></a>Bots et cartes adaptatives

Les cartes adaptatives sont une façon vivement recommandée d’afficher des messages de bot. Vos cartes doivent être légères et inclure uniquement 1 à 3 actions. Si vous avez besoin d’afficher davantage de contenu, envisagez d’utiliser un module de tâche ou un onglet.

Pour plus d'informations, consultez les ressources suivantes :

* [Conception de cartes adaptatives](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Référence de cartes](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="messaging-extensions"></a>Extensions de messagerie

Si votre application inclut une extension de messagerie, assurez-vous qu’elle respecte ces recommandations.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les [instructions Teams de conception d’extension de messagerie](~/messaging-extensions/design/messaging-extension-design.md).

### <a name="action-commands"></a>Commandes d'action

Les extensions de messagerie basées sur l’action doivent effectuer ce qui suit :

* Autoriser les utilisateurs à déclencher des actions sur un message sans effectuer d’étapes intermédiaires, telles que la connexion.
* Passez le contexte du message à l’état de travail suivant.

### <a name="preview-links-link-unfurling"></a>Liens d’aperçu (déploiement de liens)

Les extensions de messagerie doivent afficher un aperçu des liens reconnus dans la zone de rédaction Teams. N’ajoutez pas de domaines qui sont en dehors de votre contrôle (des URL absolues ou des caractères génériques). Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide. Les domaines de niveau supérieur sont également interdits (par exemple, `*.com` ou `*.org`).

### <a name="search-commands"></a>Commandes de recherche

* Les extensions de messagerie basées sur la recherche doivent fournir du texte qui aide les utilisateurs à effectuer des recherches de manière efficace.
* Les @mention exécutables doivent être claires, faciles à comprendre et lisibles.

## <a name="task-modules"></a>Modules de tâche

Un module de tâche doit inclure une icône et le nom court de l’application avec laquelle il est associé.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les [instructions Teams de conception du module de tâche Teams](~/task-modules-and-cards/task-modules/design-teams-task-modules.md).

## <a name="meeting-extensions"></a>Extensions de réunion

Si votre application inclut une extension de réunion, assurez-vous qu’elle respecte ces recommandations.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les [instructions Teams de conception d’extension de réunion](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md).

### <a name="pre--and-post-meeting-experience"></a>Expérience avant et après la réunion

* Les écrans avant et après la réunion doivent respecter les recommandations générales en matière de conception d’onglets. Pour plus d’informations, voir les [recommandations de conception Teams](~/tabs/design/tabs.md).
* Les onglets ne doivent pas avoir de défilement horizontal.
* Les onglets doivent avoir une disposition organisée lors de l’affichage de plusieurs éléments. Par exemple, plus de 10 sondages ou enquêtes. Voir un [exemple de disposition](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* Votre application doit informer les utilisateurs lorsque les résultats d’une enquête ou d’un sondage sont exportés en indiquant « Résultats téléchargés avec succès ».

### <a name="in-meeting-experience"></a>Expérience en réunion

* Les applications doivent uniquement utiliser un thème foncé pendant les réunions. Pour plus d’informations, voir les [recommandations de conception Teams](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming).
* Une info-bulle doit afficher le nom de l’application lorsque vous placez le pointage sur l’icône de l’application pendant les réunions.
* Les extensions de messagerie doivent fonctionner de la même manière pendant les réunions comme en dehors des réunions.

### <a name="in-meeting-tabs"></a>Onglets de réunion

* Doit être réactif. Veillez à maintenir le remplissage et les tailles de composants.
* Doit avoir un bouton Retour s’il existe plusieurs couches de navigation.
* Ne doit pas inclure plusieurs boutons d’arrêt ou de fermeture. Cela peut dérouter les utilisateurs, car il existe déjà un bouton d’en-tête intégré pour faire disparaître l’onglet.
* Ne doit pas avoir de défilement horizontal.

### <a name="in-meeting-dialogs"></a>Boîtes de dialogue en réunion

* Doivent être utilisées avec parcimonie et pour des scénarios légers et orientés vers les tâches.
* Doivent afficher le contenu dans une seule colonne et ne pas avoir plusieurs niveaux de navigation.
* Ne doivent pas utiliser de modules de tâche.
* Doivent s’aligner sur le centre de la phase de réunion.
* Doivent être rejetées lorsqu’un utilisateur sélectionne un bouton ou effectue une action.

## <a name="notifications"></a>Notifications

Si votre application utilise les [API de flux d’activités fournies par Microsoft Graph](/graph/teams-send-activityfeednotifications), assurez-vous qu’elles respectent les instructions suivantes.

### <a name="general"></a>Général

* Tous les déclencheurs de notification spécifiés dans les configurations de votre application doivent recevoir une notification dans l’application.
* Les notifications doivent être localisées selon les langues de prise en charge configurées pour votre application.
* Les notifications doivent s’afficher dans les cinq secondes après l’action d’un utilisateur.

### <a name="avatars"></a>Avatars

* L’avatar de notification doit correspondre à l’icône de couleur de votre application.
* Les notifications déclenchées par un utilisateur doivent inclure l’avatar de l’utilisateur.

### <a name="spamming"></a>Envoi de courrier indésirable

* Les applications ne doivent pas envoyer plus de 10 notifications par minute à un utilisateur.
* Les bots et le flux d’activités ne doivent pas déclencher de notifications en double.
* Les notifications doivent fournir une valeur ajoutée aux utilisateurs et ne pas être utilisées pour des événements triviaux ou non pertinents.

### <a name="navigation-and-layout"></a>Navigation et disposition

* Les notifications doivent respecter la disposition et l’expérience de flux d’activités Teams.
* Lors de la sélection d’une notification, l’utilisateur doit être dirigé vers du contenu pertinent au sein Team des et ne pas être retiré de l’expérience utilisateur Teams.

## <a name="advertising"></a>Publicité

Les applications ne doivent pas afficher de publicités, y compris les publicités dynamiques, les bannières publicitaires et les publicités dans les messages.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un compte d’Espace partenaires](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
