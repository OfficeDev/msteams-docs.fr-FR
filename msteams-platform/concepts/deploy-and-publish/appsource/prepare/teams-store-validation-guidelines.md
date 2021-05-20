---
title: Microsoft Teams de validation des magasins
description: Décrit les lignes directrices que chaque application soumise Teams store (AppSource) doit suivre.
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 4daa8b027d7525f0fb3223c2000eee301043398a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565136"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams de validation des magasins

Suivre ces lignes directrices augmente la probabilité que votre application passe le processus Microsoft Teams soumission en magasin. Ces Teams spécifiques complètent les politiques de [certification du marché commercial](/legal/marketplace/certification-policies) Microsoft et sont mises à jour fréquemment pour refléter les nouvelles fonctionnalités, les commentaires des utilisateurs et les modifications apportées aux règles métier.

> [!NOTE]
> Certaines lignes directrices peuvent ne pas s’appliquer à votre application. Par exemple, si votre application n’inclut pas de bot, vous pouvez ignorer les directives relatives aux bots.

## <a name="10-value-proposition"></a>1.0 Proposition de valeur

### <a name="11-app-name"></a>1.1 Nom de l’application

Le nom d’une application joue un rôle essentiel dans la façon dont les utilisateurs la découvrent dans le magasin. Rappelez-vous ce qui suit sur les noms d’applications:

* Le nom doit inclure des termes pertinents pour vos utilisateurs.
* Les noms des fonctionnalités de Teams de base&#8212;telles que **Chat,** **Contacts,** **Calendrier,** **Appels,** **Fichiers,** **Activité,** **Teams,** **Apps** et **Help**&#8212;ne doivent pas être inclus dans le nom de votre application.
* Les noms communs doivent être préfixés ou suffisés avec le nom du développeur (par exemple, **tâches contoso plutôt** que **tâches).**
* Ne doit pas **utiliser Teams ou** d’autres noms de produits Microsoft qui pourraient faussement indiquer la co-marque ou la co-vente. (Pour plus d’informations sur le référencement des logiciels, produits et services Microsoft, consultez les lignes directrices [microsoft sur les marques et les marques).](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)
* Si votre application fait partie d’un partenariat officiel avec Microsoft, le nom de votre application doit passer en premier (par **exemple, Connecteur Contoso pour Microsoft Teams).**
* Ne doit pas copier le nom d’une application répertoriée dans le magasin ou d’une autre offre sur le marché commercial.
* Ne doit pas contenir de termes profanes ou péjoratifs. Le nom ne doit pas non plus inclure un langage raciste ou culturellement insensible.
* Ça doit être unique. Par exemple, vous ne pouvez pas énumérer plusieurs applications pour différentes régions avec le même nom et les mêmes fonctionnalités.

### <a name="12-suitable-for-workplace-consumption"></a>1.2 Convient à la consommation en milieu de travail

Le contenu des applications doit être adapté à la consommation générale en milieu de travail et respecter toutes les restrictions énumérées dans les politiques de certification du marché commercial. Le contenu lié à la religion, à la politique, au jeu et au divertissement prolongé est interdit. Pour plus d’informations, consultez les politiques [de certification du marché commercial](/legal/marketplace/certification-policies#10010-inappropriate-content).

Votre application doit faciliter la collaboration de groupe, améliorer la productivité d’une personne, ou les deux. Les applications destinées à la liaison d’équipe et à la socialisation doivent être collaboratives et conçues pour plusieurs participants. Ces types d’applications ne devraient pas non plus nécessiter un investissement de temps substantiel ou avoir un impact perspicace sur la productivité.

### <a name="13-similar-platforms-and-services"></a>1.3 Plates-formes et services similaires

Les applications doivent se concentrer sur l’expérience Teams et ne pas inclure les noms, icônes ou images d’autres plateformes ou services de collaboration similaires basés sur le chat, à moins que votre application ne fournisse une interopérabilité spécifique.

### <a name="14-feature-names"></a>1.4 Noms de fonctionnalités

Les noms de fonctionnalités d’application dans les boutons et autres textes d’interface utilisateur ne doivent pas entrer en conflit avec la terminologie réservée Teams et autres produits Microsoft. Par exemple, **Commencez la réunion,** **appelez,** ou commencez **à discuter**. Incluez le nom de votre application si vous ne pouvez pas l’éviter complètement, comme **la réunion Start Contoso au** lieu de la réunion **Démarrer**.

## <a name="20-security"></a>2.0 Sécurité

### <a name="21-microsoft-365-app-compliance-program"></a>2.1 Programme de conformité Microsoft 365 appr$

Le programme [Microsoft 365 conformité des applications est destiné à](/microsoft-365-app-certification/overview) aider les organisations à évaluer et à gérer les risques en évaluant les informations de sécurité et de conformité sur votre application. Si vous publiez une application sur le Teams magasin, vous devez remplir les niveaux suivants du programme :

* [Publisher : Aide](/azure/active-directory/develop/publisher-verification-overview)les administrateurs et les utilisateurs finaux à comprendre l’authenticité des développeurs d’applications qui s’intègrent Plateforme d’identités Microsoft. Une fois terminé, un badge bleu « vérifié » s’affiche sur le dialogue de consentement Azure Active Directory (Azure AD) et d’autres écrans. Pour plus d’informations, [consultez les questions fréquemment posées,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)comment marquer votre application comme éditeur [vérifié, et](/azure/active-directory/develop/mark-app-as-publisher-verified)la vérification de [l’éditeur de dépannage](/azure/active-directory/develop/troubleshoot-publisher-verification).
* [Publisher attestation : Processus](/microsoft-365-app-certification/docs/attestation)dans lequel vous partagez des informations générales, de traitement des données et de sécurité et de conformité pour aider les clients potentiels à prendre des décisions éclairées sur l’utilisation de votre application.

> [!NOTE]
> Si vous soumettez une application qui n’a pas été répertoriée précédemment, vous ne pouvez pas remplir officiellement l’attestation Publisher tant que votre application n’est pas dans le magasin Teams’argent. Si vous mettez à jour une application répertoriée, remplissez Publisher attestation avant de soumettre la dernière version de l’application.

### <a name="22-bots"></a>2.2 Bots

Pour les applications qui utilisent le Microsoft Azure Bot Service (tels que les bots et les extensions de messagerie), vous devez suivre toutes les exigences définies dans les conditions [des services en ligne Microsoft](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).

Les bots doivent toujours demander la permission de télécharger un fichier et d’afficher un message de confirmation après les téléchargements de fichiers.

### <a name="23-external-domains"></a>2.3 Domaines externes

Dans la plupart des cas, vous ne devez pas inclure de domaines hors du contrôle de votre organisation (y compris les wildcards) et des services de tunneling dans les configurations de domaine de votre application. Les exceptions suivantes comprennent :

* Si votre application utilise la Carte OAuthcard d’Azure Bot Service, vous devez inclure `token.botframework.com` comme domaine valide ou le bouton Connect **in** ne fonctionnera pas.
* Si votre application s’appuie sur SharePoint, vous pouvez inclure le site root SharePoint comme un domaine valide en utilisant la propriété `{teamSiteDomain}` context.

### <a name="24-authentication"></a>2.4 Authentification

Pour plus d’informations sur la façon d’implémenter l’authentification des applications, [voir l’authentification Teams](~/concepts/authentication/authentication.md).

#### <a name="241-authenticating-with-external-services"></a>2.4.1 Authentification avec des services externes

N’oubliez pas ce qui suit si votre application authentifie les utilisateurs avec un service externe.

* **Connectez-vous, dédez-vous et inscrivez-vous à des expériences**:
  * Les applications qui dépendent de comptes ou de services externes doivent fournir des expériences claires et simples de se connecter, de se dé connecter et de s’inscrire.
  * Lorsqu’un utilisateur se connecte, il ne doit se dédant qu’à partir de l’application et rester connecté Teams.
* **Expériences de partage de contenu**: Les applications qui nécessitent une authentification avec un service externe pour partager du contenu dans les canaux Teams doivent indiquer clairement dans la documentation d’aide (ou des ressources similaires) comment déconnecter ou déconnecter le contenu si cette fonctionnalité est prise en charge sur le service externe. Cela ne signifie pas que la possibilité de dé partager du contenu doit être présente dans votre Teams appe.

#### <a name="242-government-community-cloud-listings"></a>2.4.2 Annonces Cloud de la communauté du secteur public annonces

Pour distribuer votre application aux utilisateurs de Cloud de la communauté du secteur public (Cloud de la communauté du secteur public) tout en évitant les annonces en double dans le magasin Teams, le processus d’authentification doit identifier et acheminer les utilisateurs vers une URL spécifique ou attendue à Cloud de la communauté du secteur public.

### <a name="25-sensitive-content"></a>2.5 Contenu sensible

Votre application ne doit pas publier de données sensibles, telles que les données de carte de crédit ou d’instruments de paiement financier. L’application ne doit pas non plus afficher la santé, le traçage des contacts ou d’autres informations personnellement identifiables (IIP) à un public qui n’a pas l’intention de voir ce contenu.

Avertissez les utilisateurs avant que votre application ne télécharge des fichiers ou des exécutables (.exe) dans la machine ou l’environnement de l’utilisateur.

### <a name="26-financial-information"></a>2.6 Informations financières

Les applications ne doivent pas demander aux utilisateurs d’effectuer des paiements dans Teams interface. Les détails des instruments financiers ne doivent pas être transmis aux utilisateurs via une interface bot.

Vous ne pouvez établir un lien vers des services de paiement externes sécurisés que si vous avez fait la divulgation appropriée dans vos conditions d’utilisation, votre politique de confidentialité ou toute page de profil ou site Web avant que l’utilisateur accepte d’utiliser l’application.

Les applications fonctionnant sur la version iOS ou Android de Teams doivent respecter les lignes directrices suivantes :

* Les applications ne doivent pas inclure les achats intégrés, les offres d’essai ou l’interface utilisateur qui vise à vendre des versions payantes ou des liens vers des magasins en ligne où les utilisateurs peuvent acheter ou acquérir d’autres contenus, applications ou modules supplémentaires.
* Si votre application nécessite un compte, les utilisateurs doivent pouvoir s’inscrire gratuitement à un compte. L’utilisation du terme **compte** gratuit **ou gratuit** est interdite.
* Vous pouvez déterminer si un compte est actif indéfiniment ou pour une durée limitée, mais si le compte expire, aucune interface utilisateur, texte ou lien indiquant la nécessité de payer ne peut être affiché.
* La politique de confidentialité et les pages de conditions d’utilisation de votre application doivent être exemptes de toute interface utilisateur ou lien lié au commerce.

## <a name="30-general-functionality-and-performance"></a>3.0 Fonctionnalité générale et performance

### <a name="31-launching-external-functionality"></a>3.1 Lancement de fonctionnalités externes

Les applications ne doivent pas sortir les utilisateurs de Teams pour les scénarios utilisateur de base. Le contenu et les interactions des applications peuvent se Teams capacités spécifiques, telles que les bots, les cartes et les modules de tâches.

Vous devez lier les utilisateurs quelque part Teams et non à un site ou une application externe. Pour les scénarios qui nécessitent des fonctionnalités externes, votre application doit avoir l’autorisation explicite de l’utilisateur de lancer cette fonctionnalité.

### <a name="32-compatibility"></a>3.2 Compatibilité

Les applications doivent être entièrement fonctionnelles sur les systèmes d’exploitation et navigateurs suivants :

* Microsoft Windows 7 et plus tard
* macOS 10.10 et plus tard
* Microsoft Edge 12 et versions ultérieures
* Mozilla Firefox 47.0 et plus tard
* Google Chrome 51.0 et plus tard
* iOS 9.0 et plus tard
* Android 4.4 et plus tard

### <a name="33-response-time"></a>3.3 Temps de réponse

Teams applications doivent répondre dans un délai raisonnable, ce qui varie en fonction de la capacité.

* Les onglets doivent répondre dans les trois secondes ou afficher un message de chargement ou un avertissement.
* Les bots doivent répondre aux commandes de l’utilisateur dans les deux secondes ou afficher un indicateur de frappe.
* Les extensions de messagerie doivent répondre aux commandes de l’utilisateur dans les cinq secondes.
* Les notifications doivent s’afficher dans les cinq secondes qui ont après l’action de l’utilisateur.

## <a name="40-app-package-and-store-listing"></a>4.0 Paquet d’application et liste de magasin

Les paquets d’applications doivent être correctement formatés et inclure toutes les informations et composants requis.

### <a name="41-app-manifest"></a>4.1 Manifeste d’application

Le Teams’application définit les configurations de votre application.

* Votre manifeste doit se conformer au dernier schéma manifeste. Pour plus d’informations, voir [la référence manifeste](~/resources/schema/manifest-schema.md).
* Si votre application inclut une extension de bot ou de messagerie, votre manifeste doit être compatible avec les métadonnées bot framework, y compris le nom du bot, le logo, le lien de politique de confidentialité et le lien sur les conditions de service.
* Si votre application utilise Azure Active Directory (Azure AD) pour l’authentification, incluez l’iD azure ad (client) dans le manifeste. Pour plus d’informations, voir [la référence manifeste](~/resources/schema/manifest-schema.md#webapplicationinfo).

### <a name="42-app-icons"></a>4.2 Icônes d’application

Les icônes sont l’un des principaux éléments que les gens voient lors de la navigation Teams magasin. Vos icônes doivent communiquer la marque et le but de votre application tout en respectant les exigences suivantes :

* Votre package d’application doit inclure deux versions PNG de votre icône d’application : une icône couleur et une icône de contour.
* La version couleur de votre icône s’affiche dans la plupart Teams scénarios et doit être de 192x192 pixels. Votre symbole d’icône (pixels 96x96) peut être n’importe quelle couleur ou couleur, mais il doit s’asseoir sur un fond carré solide ou entièrement transparent.
* La version d’aperçu de votre icône s’affiche lorsque votre application est en cours d’utilisation et « hissée » sur la barre d’application sur le côté gauche de Teams et lorsqu’un utilisateur épingle l’extension de messagerie de votre application. Il doit être de 32x32 pixels et peut être blanc avec un fond transparent ou transparent avec un fond blanc (aucune autre couleur n’est autorisée). L’icône ne doit pas avoir de rembourrage supplémentaire autour du symbole.
* Les icônes correctement dimensionnées et formatées doivent être incluses dans votre package d’application. Les icônes doivent également correspondre à ce qui est soumis avec les métadonnées de liste de magasin.

Pour plus d’informations, les meilleures pratiques et les exemples, consultez les lignes directrices sur [Teams’icône de l’application](~/concepts/build-and-test/apps-package.md#app-icons).

### <a name="43-app-descriptions"></a>4.3 Descriptions d’applications

Vous devez avoir une description courte et longue de votre application. Les descriptions dans les configurations de votre application et partner center doivent être les mêmes.

Les descriptions ne devraient pas dénigrer directement ou par insinuation une autre marque (propriété de Microsoft ou autre). Assurez-vous que votre description n’inclut pas les allégations qui ne peuvent pas être corroborées (par exemple, « Augmentation garantie de 200 % de l’efficacité »).

#### <a name="431-short-description"></a>4.3.1 Description courte

Une courte description est un résumé concis de votre application qui met en évidence sa proposition de valeur et s’adresse à votre public cible.

**À faire :**

* Gardez la courte description à une phrase.
* Mettez les informations les plus importantes en premier.
* Incluez les mots clés que les clients sont susceptibles de rechercher.

**À ne pas faire :**

* Répétez le nom de votre application.
* Utilisez le mot **application** dans la courte description.

#### <a name="432-long-description"></a>4.3.2 Longue description

La longue description peut fournir un récit engageant qui met en évidence la proposition de valeur de votre application, l’audience primaire et l’industrie cible. Bien que cette description puisse aller jusqu’à 4 000 caractères, la plupart des utilisateurs ne liront qu’entre 300 et 500 mots.

**À faire :**

* Utilisez [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) pour formater votre description.
* Utilisez la voix active et parlez directement aux utilisateurs. Par exemple, *Vous pouvez ...*.
* Liste des fonctionnalités avec des points de balle de sorte qu’il est plus facile de scanner la description.
* Décrivez clairement les limitations, les conditions ou les exceptions aux fonctionnalités, fonctionnalités et livrables décrites dans la liste et les documents connexes avant que l’utilisateur n’installe votre application. Les Teams de votre application doivent se rapporter aux fonctions de base que votre annonce décrit.
* Incluez un lien d’aide ou de soutien.
* Se référer **à Microsoft 365** au lieu **de Office 365**.
* Si vous avez besoin de **référencer Teams**, écrivez la première référence **comme Microsoft Teams**. Les références ultérieures peuvent être raccourcies **Teams**.
* Utilisez la langue suivante pour décrire le fonctionnement de l’application avec Teams (ou Microsoft 365) :
  * "... travaille avec Microsoft Teams.
  * "... travailler avec Microsoft Teams.
  * "... dans Microsoft Teams.
  * "... pour Microsoft Teams.

**À ne pas faire :**

* Dépassez les 500 mots.
* Abréviation **Microsoft** comme **MS** ou **MSFT**.
* Indiquez que l’application est une offre de Microsoft, y compris en utilisant des slogans ou des slogans Microsoft.
* Utilisez des marques protégées par le droit d’auteur que vous ne possédez pas.
* Inclure des fautes de frappe, des erreurs grammaticales et des capitalisations inutiles (par exemple, les **utilisateurs au** lieu des **utilisateurs).**
* Incluez des liens vers AppSource.
* Utilisez la langue suivante à moins d’être un partenaire Microsoft certifié :
  * "... intégré à Microsoft Teams »
  * "... s’intègre à ... »
  * "... construit pour ... »
  * "... construit sur ... »
  * "... fonctionne sur ... »
  * "... activé par ... »
  * "... certifié pour ... »
  * "... développé pour ... »
  * "... conçu pour ... »

### <a name="44-screenshots"></a>4.4 Captures d’écran

Les captures d’écran fournissent un aperçu visuel important de votre application pour compléter le nom, l’icône et les descriptions de votre application. Rappelez-vous ce qui suit sur les captures d’écran:

* Vous pouvez avoir jusqu’à cinq captures d’écran par annonce.
* Les types de fichiers pris en charge incluent PNG, JPEG et GIF.
* Les dimensions doivent être de 1366x768 pixels.
* Taille maximale de 1 024 KB.

**À faire :**

* Concentrez-vous sur les capacités de votre application (par exemple, comment les gens peuvent communiquer avec votre bot).
* Incluez du contenu qui représente avec précision votre application.
* Utilisez le texte judicieusement.
* Cadrez des captures d’écran avec une couleur qui reflète votre marque et incluez du contenu marketing, similaire à [l’exemple de liste Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) (les exigences de dimension s’appliquent à l’ensemble de l’image et pas seulement à la capture d’écran).

**À ne pas faire :**

* Affichez des appareils spécifiques, tels que des téléphones ou des ordinateurs portables.
* Affichez chrome ou interface utilisateur qui n’est pas dans votre application.
* Capturez n’importe Teams ou interface utilisateur du navigateur dans vos captures d’écran.
* Incluez des maquettes qui reflètent inexactement l’interface utilisateur réelle de votre application, par exemple en montrant que votre application est utilisée en dehors de Teams.

> [!TIP]
> Une vidéo peut être le moyen le plus efficace de communiquer pourquoi les gens devraient utiliser votre application. Une vidéo est également la première chose que les utilisateurs voient dans votre annonce (par défaut, une vidéo s’affiche avant les captures d’écran). Pour plus d’informations, [voir créer une vidéo pour votre annonce de magasin](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video).

### <a name="45-privacy-policy"></a>4.5 Politique de confidentialité

La politique de confidentialité peut être spécifique à votre Teams ou à une politique globale pour tous vos services.

* Si vous utilisez un modèle générique de politique de confidentialité, vous devez faire référence **à des services,** **des applications** et des **plateformes** pour inclure votre application Teams et votre service ou site Web.
* Doit inclure la façon dont vous gérez le stockage, la conservation et la suppression des données des utilisateurs. Vous devez également décrire les contrôles de sécurité que vous utilisez pour la protection des données.
* Doit inclure vos coordonnées.
* Ne doit pas contenir d’URL cassées ou à des fins bêta ou de mise en scène.
* Ne doit pas inclure de liens vers AppSource.

### <a name="46-terms-of-use"></a>4.6 Conditions d’utilisation

Vos conditions d’utilisation doivent être spécifiques et applicables à votre offre.

### <a name="47-support-links"></a>4.7 Liens de soutien

Les URL de support de votre application ne doivent pas nécessiter d’authentification. Par exemple, les utilisateurs ne devraient pas avoir à se connecter pour vous contacter.

### <a name="48-localization"></a>4.8 Localisation

Si votre application prend en charge la localisation, votre package d’application doit inclure un fichier avec des traductions linguistiques qui s’affichent en fonction de l’Teams paramètre linguistique. Le fichier doit se conformer au schéma Teams localisation de la communauté. Pour plus d’informations, [consultez le schéma Teams localisation de la ville.](~/concepts/build-and-test/apps-localization.md)

## <a name="50-tabs"></a>5.0 Onglets

Si votre application inclut un onglet, assurez-vous qu’elle respecte ces lignes directrices.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, [consultez les lignes directrices Teams conception d’onglets.](~/tabs/design/tabs.md)

### <a name="51-setup"></a>5.1 Configuration

* La configuration de l’onglet ne doit pas mettre fin à un nouvel utilisateur. Fournissez un message sur la façon de compléter l’action ou le flux de travail.
* L’authentification doit se produire pendant la configuration de l’onglet et non après.

### <a name="52-views"></a>5.2 Vues

* La zone de l’écran de dédage ne doit pas utiliser de grands logos ou afficher une page Web entière.
* Le contenu peut être simplifié en le dé-dédant sur plusieurs onglets.
* Les onglets ne doivent pas avoir d’en-tête en double. Supprimez le logo de l’iframe puisque le cadre de l’onglet affiche déjà l’icône et le nom de l’application.

### <a name="53-navigation"></a>5.3 Navigation

* Les onglets ne doivent pas avoir plus de trois niveaux de navigation.
* Les onglets ne doivent pas fournir une navigation qui entre en conflit avec la Teams navigation.
* Les pages secondaires et tertiaires d’un onglet doivent être ouvertes dans une vue de niveau deux et de niveau 3 dans la zone de l’onglet principal, qui est naviguée par la chapelure ou la navigation à gauche. Vous pouvez également inclure les composants suivants pour faciliter la navigation par onglets :
    * Boutons arrière
    * En-têtes de page
    * Menus hamburger
* L’onglet ne doit pas avoir de parchemin horizontal.
* Les liens profonds dans les onglets ne doivent pas être lier à une page Web externe, mais quelque part dans Teams. Par exemple, modules de tâches ou autres onglets.
* Les onglets ne doivent pas permettre aux utilisateurs de naviguer en dehors Teams l’expérience de base de l’application.

### <a name="54-usability"></a>5.4 Facilité d’utilisation

* Les onglets doivent fournir une valeur au-delà de l’hébergement d’un site Web existant.
* Les utilisateurs doivent être en mesure de défaire leur dernière action dans l’onglet.
* Les onglets dans un contexte personnel peuvent regrouper le contenu des instances partagées de l’application.
* Les onglets doivent être sensibles aux Teams thèmes. Lorsqu’un utilisateur modifie le thème, le thème de l’application doit refléter la sélection.
* Les onglets doivent utiliser des composants de style Teams, tels que les polices Teams, les rampes de type, les palettes de couleurs, le système de grille, le mouvement, le ton de la voix, et ainsi de suite dans la mesure du possible.
* Vous devez inclure un **onglet Paramètres..**
* Les onglets doivent suivre Teams conception de l’interaction, comme la navigation en page, la position et l’utilisation des dialogues, des hiérarchies d’informations, et ainsi de suite dans la mesure du possible.
* Le contenu de l’onglet dans l’iframe ne doit pas inclure de fonctionnalités qui imitent Teams capacités de base. Par exemple, les bots, les extensions de messagerie, les appels, les réunions, et ainsi de suite.

> [!TIP]
>
> * Incluez un bot personnel à côté d’un onglet personnel.
> * Permettre aux utilisateurs de partager du contenu à partir de leur onglet personnel.

## <a name="60-bots"></a>6.0 Bots

Si votre application inclut un bot, assurez-vous qu’elle respecte ces directives.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, [consultez les Teams de conception de bots.](~/bots/design/bots.md)

### <a name="61-bot-commands"></a>6.1 Commandes bot

Il est difficile d’analyser l’entrée de l’utilisateur et de prédire l’intention de l’utilisateur. Les commandes Bot fournissent aux utilisateurs un ensemble de mots ou de phrases que votre bot comprend afin qu’ils (et votre bot) n’aient pas à deviner.

* L’inscription des commandes de bot prises en charge dans les configurations de votre application est fortement recommandée. Ces commandes s’affichent dans la boîte de composition lorsqu’un utilisateur tente de messager votre bot.
* Toutes les commandes que votre bot prend en charge doivent fonctionner correctement, y compris la **commande Salut,** **Bonjour** **et** Aide.

> [!TIP]
> Pour les bots personnels, incluez **un onglet** Aide qui décrit davantage ce que votre bot peut faire.

### <a name="62-bot-welcome-messages"></a>6.2 Bot messages de bienvenue

* Les bots doivent presque toujours envoyer un message de bienvenue lors de la première manche. Pour la meilleure expérience, le message doit inclure la proposition de valeur de votre bot, comment configurer le bot, et décrire brièvement toutes les commandes de bot prises en charge. Vous pouvez afficher le message à l’aide d’une carte adaptative avec des boutons pour une meilleure facilité d’utilisation. Pour plus d’informations, [voir comment déclencher un message de bienvenue bot](~/bots/how-to/conversations/send-proactive-messages.md).
* Bot messages de bienvenue dans les canaux et les chats sont facultatifs au cours de la première course, surtout si le bot est disponible pour un usage personnel et effectue des actions similaires. Si votre bot envoie des messages de bienvenue, il ne doit pas les envoyer aux utilisateurs individuellement (ceci est considéré [comme spamming).](#63-bot-message-spamming) Le message doit également mentionner la personne qui a ajouté le bot.
* Les bots de notification uniquement doivent envoyer un message de bienvenue qui le transmet ne répondra pas aux messages des utilisateurs.

> [!TIP]
> Dans les messages de bienvenue aux utilisateurs individuels, une visite carrousel peut fournir une vue d’ensemble efficace de votre bot et toutes les autres fonctionnalités de l’application. Y compris les boutons la permettent aux utilisateurs d’essayer les commandes bot est encouragé. Par exemple, **Créez une tâche**.

### <a name="63-bot-message-spamming"></a>6.3 Bot message spamming

Les bots ne doivent pas spammer les utilisateurs en envoyant plusieurs messages en succession courte.

* **Messages bot dans les canaux et les chats**: Ne spammez pas les utilisateurs en créant des publications distinctes. Créez un seul message avec des réponses dans le même thread.
* **Messages bot dans les applications personnelles**: N’envoyez pas plusieurs messages en succession rapide. Envoyez un message avec des informations complètes. Évitez les conversations multi-virages pour compléter un seul flux de travail. Au lieu de cela, envisagez d’utiliser un formulaire (ou un module de tâche) pour recueillir toutes les entrées d’un utilisateur en même temps.
* **Messages de bienvenue**: Répéter le même message de bienvenue à intervalles réguliers n’est pas autorisé et considéré comme un spamming. Par exemple, lorsqu’un nouveau membre est ajouté à une équipe, ne spammez pas les autres membres avec un message de bienvenue. Message le nouveau membre personnellement à la place.

### <a name="64-bot-notifications"></a>6.4 Notifications bot

Les notifications bot doivent inclure du contenu pertinent pour la portée que vous définissez pour le bot (équipe, chat ou personnel).

### <a name="65-bots-and-adaptive-cards"></a>6.5 Bots et cartes adaptatives

Cartes adaptatives sont un moyen fortement recommandé d’afficher des messages bot. Vos cartes doivent être légères et ne comprennent que 1-3 actions. Si vous avez besoin d’afficher plus de contenu, envisagez d’utiliser un module de tâches ou un onglet.

Pour plus d'informations, consultez les ressources suivantes :

* [Conception de cartes adaptatives](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Référence de cartes](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="70-messaging-extensions"></a>7.0 Extensions de messagerie

Si votre application inclut une extension de messagerie, assurez-vous qu’elle respecte ces directives.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, [consultez les lignes directrices Teams de conception d’extension de messagerie.](~/messaging-extensions/design/messaging-extension-design.md)

### <a name="71-action-commands"></a>7.1 Commandes d’action

Les extensions de messagerie basées sur l’action devraient faire ce qui suit :

* Permettre aux utilisateurs de déclencher des actions sur un message sans effectuer d’étapes intermédiaires, telles que la dédicace.
* Transmets le contexte du message à l’état de travail suivant.

### <a name="72-preview-links-link-unfurling"></a>7.2 Liens d’aperçu (lien se déployant)

Les extensions de messagerie doivent prévisualiser les liens reconnus dans Teams la boîte de composition. N’ajoutez pas de domaines qui sont hors de votre contrôle (urls absolues ou wildcards). Par exemple, est `yourapp.onmicrosoft.com` valide, mais `*.onmicrosoft.com` n’est pas valide. Les domaines de haut niveau sont également interdits (par exemple, `*.com` ou `*.org` ).

### <a name="73-search-commands"></a>7.3 Commandes de recherche

* Les extensions de messagerie basées sur la recherche doivent fournir du texte qui aide les utilisateurs à rechercher efficacement.
* @mention exécutables doivent être clairs, faciles à comprendre et lisibles.

## <a name="80-task-modules"></a>8.0 Modules de tâches

Un module de tâches doit inclure une icône et le nom court de l’application à qui il est associé.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, [consultez les lignes directrices Teams de conception de modules de tâches.](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="90-meeting-extensions"></a>9.0 Prolongations de réunion

Si votre application inclut une extension de réunion, assurez-vous qu’elle respecte ces directives.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, [consultez les lignes directrices Teams de conception d’extensions de réunion.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)

### <a name="91-pre--and-post-meeting-experience"></a>9.1 Expérience avant et après la réunion

* Les écrans avant et après la réunion doivent respecter les lignes directrices générales sur la conception des onglets. Pour plus d’informations, consultez les [lignes directrices Teams conception des données.](~/tabs/design/tabs.md)
* Les onglets ne doivent pas avoir de défilement horizontal.
* Les onglets doivent avoir une mise en page organisée lors de l’affichage de plusieurs éléments. Par exemple, plus de 10 sondages ou sondages. Voir une mise [en page d’exemple](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* Votre application doit informer les utilisateurs lorsque les résultats d’un sondage ou d’un sondage sont exportés en indiquant : « Résultats téléchargés avec succès ».

### <a name="92-in-meeting-experience"></a>9.2 Expérience en réunion

* Les applications ne doivent utiliser un thème sombre que pendant les réunions. Pour plus d’informations, consultez les [lignes directrices Teams conception des données.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)
* Un tooltip doit afficher le nom de l’application lorsque vous passez au-dessus de l’icône de l’application pendant les réunions.
* Les extensions de messagerie doivent fonctionner de la même manière pendant les réunions qu’en dehors des réunions.

### <a name="93-in-meeting-tabs"></a>9.3 Onglets en réunion

* Doit être réactif. Assurez-vous de maintenir le rembourrage et la taille des composants.
* Doit avoir un bouton arrière s’il y a plus d’une couche de navigation.
* Ne doit pas inclure plus d’un bouton de rejet ou de fermeture. Cela peut confondre les utilisateurs car il ya déjà un bouton en-tête intégré pour rejeter l’onglet.
* Ne doit pas avoir de défilement horizontal.

### <a name="94-in-meeting-dialogs"></a>9.4 Dialogues en réunion

* Doit être utilisé avec parcimonie et pour des scénarios qui sont légers et axés sur les tâches.
* Doit afficher le contenu dans une seule colonne et ne pas avoir plusieurs niveaux de navigation.
* Ne doit pas utiliser de modules de tâches.
* Doit s’aligner avec le centre de l’étape de réunion.
* Doit être rejeté une fois qu’un utilisateur sélectionne un bouton ou effectue une action.

## <a name="100-notifications"></a>10.0 Notifications

Si votre application utilise les [API de flux d’activité fournies par Microsoft Graph](/graph/teams-send-activityfeednotifications), assurez-vous qu’elle respecte les lignes directrices suivantes.

### <a name="101-general"></a>10.1 Général

* Tous les déclencheurs de notification spécifiés dans les configurations de votre application doivent recevoir une notification dans l’application.
* Les notifications doivent être localisées par les langues prises en charge configurées pour votre application.
* Les notifications doivent s’afficher dans les cinq secondes qui ont après l’action de l’utilisateur.

### <a name="102-avatars"></a>10.2 Avatars

* L’avatar de notification doit correspondre à l’icône couleur de votre application.
* Les notifications déclenchées par un utilisateur doivent inclure l’avatar de l’utilisateur.

### <a name="103-spamming"></a>10.3 Spamming

* Les applications ne doivent pas envoyer plus de 10 notifications par minute à un utilisateur.
* Les bots et le flux d’activité ne doivent pas déclencher de notifications en double.
* Les notifications doivent fournir une certaine valeur aux utilisateurs et ne pas être utilisées pour des événements insignifiants ou non pertinents.

### <a name="104-navigation-and-layout"></a>10.4 Navigation et mise en page

* Les notifications doivent respecter la disposition et l’expérience Teams’alimentation d’activité.
* Lors de la sélection d’une notification, l’utilisateur doit être dirigé vers le contenu pertinent dans Teams et non retiré de l’expérience Teams’utilisateur.

## <a name="110-advertising"></a>11.0 Publicité

Les applications ne doivent pas afficher de publicité, y compris des annonces dynamiques, des bannières publicitaires et des annonces dans les messages.

## <a name="see-also"></a>Voir aussi

[4.0 Paquet d’application et liste de magasin](#40-app-package-and-store-listing)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un compte d’Espace partenaires](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
