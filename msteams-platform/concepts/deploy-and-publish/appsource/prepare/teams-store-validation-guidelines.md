---
title: Microsoft Teams de validation du magasin d’informations
description: Décrit les instructions que chaque application envoyée au Teams store (AppSource) doit suivre.
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
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams de validation du magasin d’informations

Le fait de suivre ces instructions augmente la probabilité que votre application passe le Microsoft Teams soumission au Store. Ces Teams spécifiques complètent les stratégies de certification de Microsoft [Commercial Marketplace](/legal/marketplace/certification-policies) et sont fréquemment mises à jour pour refléter les nouvelles fonctionnalités, les commentaires des utilisateurs et les modifications apportées aux règles métiers.

> [!NOTE]
> Certaines recommandations peuvent ne pas être applicables à votre application. Par exemple, si votre application n’inclut pas de bot, vous pouvez ignorer les instructions liées au bot.

## <a name="10-value-proposition"></a>1.0 Proposition de valeur

### <a name="11-app-name"></a>1.1 Nom de l’application

Le nom d’une application joue un rôle essentiel dans la façon dont les utilisateurs la découvrent dans le Store. Souvenez-vous des informations suivantes sur les noms d’application :

* Le nom doit inclure des termes pertinents pour vos utilisateurs.
* Les noms des fonctionnalités Teams principales&#8212;telles que **chat,** **contacts,** **calendrier,** **appels,** **fichiers,** **activité, Teams,** applications et **&#8212;** d’aide ne doivent pas être inclus dans le nom de votre application.  
* Les noms communs doivent être précédés ou suffixes avec le nom du développeur (par exemple, **Tâches Contoso** plutôt que Tâches **).**
* Ne doit pas utiliser **Teams** ou d’autres noms de produits Microsoft qui pourraient indiquer à tort la co- branding ou la co-vente. (Pour plus d’informations sur le référencement des logiciels, des produits et des services Microsoft, voir les recommandations en matière de marque et de marque [Microsoft).](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)
* Si votre application fait partie d’un partenariat officiel avec Microsoft, le nom de votre application doit être donné en premier (par exemple, **Contoso Connector pour Microsoft Teams**).
* Ne doit pas copier le nom d’une application répertoriée dans le Store ou une autre offre sur le marketplace commercial.
* Ne doit pas contenir de termes désobligeants ou désobligeants. Le nom ne doit pas non plus inclure de langues ethniques ou culturelles non sensibles.
* Doit être unique. Par exemple, vous ne pouvez pas lister plusieurs applications pour différentes régions avec le même nom et les mêmes fonctionnalités.

### <a name="12-suitable-for-workplace-consumption"></a>1.2 Convient à la consommation de l’espace de travail

Le contenu de l’application doit être adapté à une utilisation générale de l’espace de travail et respecter toutes les restrictions répertoriées dans les stratégies de certification du marketplace commercial. Le contenu lié à l’animation, à la politique, aux jeux et aux divertissements prolongés est interdit. Pour plus d’informations, voir les [stratégies de certification du marketplace commercial.](/legal/marketplace/certification-policies#10010-inappropriate-content)

Votre application doit faciliter la collaboration de groupe, améliorer la productivité d’un individu, ou les deux. Les applications destinées à la liaison et à la socialisation d’équipe doivent être collaboratives et conçues pour plusieurs participants. Ces types d’applications ne doivent pas non plus nécessiter un investissement en temps considérable ou avoir un impact négatif sur la productivité.

### <a name="13-similar-platforms-and-services"></a>1.3 Plateformes et services similaires

Les applications doivent se concentrer sur l’expérience Teams et ne pas inclure les noms, les icônes ou les images d’autres plateformes ou services de collaboration basés sur la conversation similaires, sauf si votre application fournit une interopérabilité spécifique.

### <a name="14-feature-names"></a>1.4 Noms des fonctionnalités

Les noms des fonctionnalités d’application dans les boutons et tout autre texte d’interface utilisateur ne doivent pas être en conflit avec la terminologie réservée Teams et d’autres produits Microsoft. Par exemple, commencez **la réunion,** **appelez** ou **démarrez la conversation.** Incluez le nom de votre application si vous ne pouvez pas l’éviter complètement, par exemple, démarrer une réunion **Contoso** au lieu de **commencer la réunion.**

## <a name="20-security"></a>Sécurité 2.0

### <a name="21-microsoft-365-app-compliance-program"></a>2.1 Programme Microsoft 365 conformité des applications

Le [Microsoft 365 conformité](/microsoft-365-app-certification/overview) des applications est conçu pour aider les organisations à évaluer et à gérer les risques en évaluant les informations de sécurité et de conformité concernant votre application. Si vous publiez une application dans le Teams, vous devez effectuer les niveaux suivants du programme :

* [Publisher vérification :](/azure/active-directory/develop/publisher-verification-overview)permet aux administrateurs et aux utilisateurs finaux de comprendre l’authenticité de l’intégration des développeurs d’applications au Plateforme d’identités Microsoft. Une fois terminé, un badge bleu « vérifié » s’affiche sur la boîte de dialogue de consentement Azure Active Directory (Azure AD) et d’autres écrans. Pour plus d’informations, voir [les questions fréquemment posées,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)comment marquer votre application comme éditeur vérifié et résoudre les problèmes de vérification de [l’éditeur](/azure/active-directory/develop/troubleshoot-publisher-verification). [](/azure/active-directory/develop/mark-app-as-publisher-verified)
* [Publisher attestation](/microsoft-365-app-certification/docs/attestation): processus dans lequel vous partagez des informations générales, de gestion des données et de sécurité et de conformité pour aider les clients potentiels à prendre des décisions éclairées sur l’utilisation de votre application.

> [!NOTE]
> Si vous soumettez une application qui n’a pas été répertoriée précédemment, vous ne pouvez pas terminer officiellement l’attestation d’Publisher tant que votre application n’est pas dans le Teams store. Si vous êtes en train de mettre à jour une application répertoriée, Publisher attestation avant de soumettre la dernière version de l’application.

### <a name="22-bots"></a>2.2 Bots

Pour les applications qui utilisent le service Microsoft Azure Bot (par exemple, les bots et les extensions de messagerie), vous devez respecter toutes les conditions définies dans les conditions d’utilisation de Microsoft [Online Services.](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)

Les bots doivent toujours demander l’autorisation de télécharger un fichier et afficher un message de confirmation après le téléchargement du fichier.

### <a name="23-external-domains"></a>2.3 Domaines externes

Dans la plupart des cas, vous ne devez pas inclure de domaines en dehors du contrôle de votre organisation (y compris les caractères génériques) et des services de tunneling dans les configurations de domaine de votre application. Les exceptions suivantes sont les suivantes :

* Si votre application utilise le OAuthCard d’Azure Bot Service, vous devez inclure en tant que domaine valide, sinon le bouton Se connecter ne `token.botframework.com` fonctionne pas. 
* Si votre application s’appuie sur SharePoint, vous pouvez inclure le site SharePoint racine associé en tant que domaine valide à l’aide de la `{teamSiteDomain}` propriété de contexte.

### <a name="24-authentication"></a>2.4 Authentification

Pour plus d’informations sur l’implémenter l’authentification d’application, voir [l’authentification dans Teams](~/concepts/authentication/authentication.md).

#### <a name="241-authenticating-with-external-services"></a>2.4.1 Authentification avec des services externes

N’oubliez pas ce qui suit si votre application authentifier les utilisateurs avec un service externe.

* **Connectez-vous, connectez-vous et inscrivez-vous** aux expériences :
  * Les applications qui dépendent de comptes ou de services externes doivent fournir des expériences claires et simples de se connecter, de se signer et de s’inscrire.
  * Lorsqu’un utilisateur se connecte, il ne doit se sortir que de l’application et rester Teams.
* Expériences de partage de contenu : les applications qui nécessitent une authentification auprès d’un service externe pour partager du contenu dans des canaux Teams doivent clairement faire état dans la documentation d’aide (ou ressources similaires) de la manière de déconnecter ou de partager du contenu si cette fonctionnalité est prise en charge sur le service externe. Cela ne signifie pas que la possibilité de partager du contenu doit être présente dans votre application Teams partage.

#### <a name="242-government-community-cloud-listings"></a>2.4.2 listes Cloud de la communauté du secteur public listes

Pour distribuer votre application aux utilisateurs Cloud de la communauté du secteur public (Cloud de la communauté du secteur public) tout en évitant les doublons dans le magasin Teams, le processus d’authentification doit identifier et router les utilisateurs vers une URL spécifique ou attendue Cloud de la communauté du secteur public.

### <a name="25-sensitive-content"></a>2.5 Contenu sensible

Votre application ne doit pas publier de données sensibles, telles que des données de carte bancaire ou d’instrument de paiement financier. L’application ne doit pas non plus afficher l’état d’état, le suivi des contacts ou d’autres informations d’identification personnelle (PII) à une audience qui n’est pas destinée à afficher ce contenu.

Avertissez les utilisateurs avant que votre application télécharge des fichiers ou des fichiers exécutables (.exe) sur l’ordinateur ou l’environnement de l’utilisateur.

### <a name="26-financial-information"></a>2.6 Informations financières

Les applications ne doivent pas demander aux utilisateurs d’effectuer des paiements dans Teams interface utilisateur. Les détails de l’instrument financier ne doivent pas être transmis aux utilisateurs via une interface de bot.

Vous pouvez établir un lien vers des services de paiement externes sécurisés uniquement si vous avez effectué la divulgation appropriée dans vos conditions d’utilisation, politique de confidentialité ou toute page de profil ou site web avant que l’utilisateur n’accepte d’utiliser l’application.

Les applications qui s’exécutent sur la version iOS ou Android de Teams doivent respecter les instructions suivantes :

* Les applications ne doivent pas inclure d’achats dans l’application, d’offres d’essai ou d’interface utilisateur qui visent à promouvoir des versions payantes ou des liens vers des magasins en ligne où les utilisateurs peuvent acheter ou acquérir d’autres contenus, applications ou modules.
* Si votre application nécessite un compte, les utilisateurs doivent pouvoir s’inscrire à un compte gratuitement. L’utilisation du terme **compte libre** ou **gratuit** est interdite.
* Vous pouvez déterminer si un compte est actif indéfiniment ou pendant une durée limitée, mais si le compte expire, aucune interface utilisateur, texte ou liens indiquant la nécessité de payer ne s’affiche.
* Les pages de politique de confidentialité et de conditions d’utilisation de votre application ne doivent pas être liées à une interface utilisateur ou à des liens commerciaux.

## <a name="30-general-functionality-and-performance"></a>3.0 Fonctionnalités et performances générales

### <a name="31-launching-external-functionality"></a>3.1 Lancement des fonctionnalités externes

Les applications ne doivent pas sortir les utilisateurs de Teams pour les scénarios utilisateur principaux. Le contenu et les interactions de l’application peuvent se produire Teams fonctionnalités, telles que les bots, les cartes et les modules de tâche.

Vous devez lier les utilisateurs Teams et non à un site ou une application externe. Pour les scénarios qui nécessitent des fonctionnalités externes, votre application doit avoir une autorisation utilisateur explicite pour lancer cette fonctionnalité.

### <a name="32-compatibility"></a>3.2 Compatibilité

Les applications doivent être entièrement fonctionnelles sur les systèmes d’exploitation et navigateurs suivants :

* Microsoft Windows 7 et ultérieures
* macOS 10.10 et ultérieur
* Microsoft Edge 12 et versions ultérieures
* Mozilla Firefox 47.0 et version ultérieure
* Google Chrome 51.0 et ultérieur
* iOS 9.0 et ultérieur
* Android 4.4 et version ultérieure

### <a name="33-response-time"></a>3.3 Temps de réponse

Teams applications doivent répondre dans un délai raisonnable, qui varie en fonction de la fonctionnalité.

* Les onglets doivent répondre dans un délai de trois secondes ou afficher un message de chargement ou un avertissement.
* Les bots doivent répondre aux commandes de l’utilisateur dans un délai de deux secondes ou afficher un indicateur de saisie.
* Les extensions de messagerie doivent répondre aux commandes de l’utilisateur dans un délai de cinq secondes.
* Les notifications doivent s’afficher dans les cinq secondes après l’action de l’utilisateur.

## <a name="40-app-package-and-store-listing"></a>Package d’application 4.0 et liste du Store

Les packages d’application doivent être correctement formatés et inclure toutes les informations et composants requis.

### <a name="41-app-manifest"></a>4.1 Manifeste de l’application

Le Teams de l’application définit les configurations de votre application.

* Votre manifeste doit être conforme au schéma de manifeste le plus récent. Pour plus d’informations, voir la [référence de manifeste.](~/resources/schema/manifest-schema.md)
* Si votre application inclut une extension de bot ou de messagerie, votre manifeste doit être cohérent avec les métadonnées Bot Framework, y compris le nom du bot, le logo, le lien de la politique de confidentialité et le lien des conditions d’utilisation.
* Si votre application utilise Azure Active Directory (Azure AD) pour l’authentification, incluez l’ID de l’application Azure AD (client) dans le manifeste. Pour plus d’informations, voir la [référence de manifeste.](~/resources/schema/manifest-schema.md#webapplicationinfo)

### <a name="42-app-icons"></a>4.2 Icônes d’application

Les icônes sont l’un des principaux éléments que les utilisateurs voient lors de la navigation dans Teams store. Vos icônes doivent communiquer la marque et l’objectif de votre application tout en respectant les exigences suivantes :

* Votre package d’application doit inclure deux versions PNG de l’icône de votre application : une icône de couleur et une icône de plan.
* La version de couleur de votre icône s’affiche dans la plupart Teams scénarios et doit être de 192 x 192 pixels. Votre symbole d’icône (96 x 96 pixels) peut être n’importe quelle couleur ou couleur, mais il doit être sur un arrière-plan carré plein ou entièrement transparent.
* La version plan de votre icône s’affiche lorsque votre application est en cours d’utilisation et « hissée » dans la barre de l’application sur le côté gauche de Teams et lorsqu’un utilisateur épingle l’extension de messagerie de votre application. Elle doit être de 32 x 32 pixels et peut être blanche avec un arrière-plan transparent ou transparente avec un arrière-plan blanc (aucune autre couleur n’est autorisée). L’icône ne doit pas avoir d’espacement supplémentaire autour du symbole.
* Les icônes correctement formatées et de taille doivent être incluses dans votre package d’application. Les icônes doivent également correspondre à ce qui est envoyé avec les métadonnées de la liste du Store.

Pour plus d’informations, de meilleures pratiques et d’exemples, voir les recommandations [Teams’icône d’application.](~/concepts/build-and-test/apps-package.md#app-icons)

### <a name="43-app-descriptions"></a>4.3 Descriptions des applications

Vous devez avoir une description courte et longue de votre application. Les descriptions dans les configurations de votre application et dans l’Partner Center doivent être identiques.

Les descriptions ne doivent pas désapprouver directement ou par insinuation une autre marque (propriété de Microsoft ou autre). Assurez-vous que votre description n’inclut pas les revendications qui ne peuvent pas être garanties (par exemple, « Augmentation garantie de 200 % de l’efficacité »).

#### <a name="431-short-description"></a>4.3.1 Description courte

Une brève description est un résumé concis de votre application qui met en évidence sa proposition de valeur et s’adresse à votre public cible.

**À faire :**

* Conservez la description courte jusqu’à une phrase.
* Mettez les informations les plus importantes en premier.
* Incluez des mots clés que les clients sont susceptibles de rechercher.

**À ne pas faire :**

* Répétez le nom de votre application.
* Utilisez **l’application Word** dans la description courte.

#### <a name="432-long-description"></a>4.3.2 Description longue

La description longue peut fournir un narratif attrayant qui met en évidence la proposition de valeur de votre application, le public principal et le secteur cible. Bien que cette description puisse prendre jusqu’à 4 000 caractères, la plupart des utilisateurs ne lisent qu’entre 300 et 500 mots.

**À faire :**

* Utilisez [Markdown pour](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) mettre en forme votre description.
* Utilisez la voix active et parlez directement aux utilisateurs. Par exemple, *vous pouvez...*.
* List features with bullet points so it’s easier to scan the description.
* Décrivez clairement les limitations, conditions ou exceptions aux fonctionnalités, fonctionnalités et livrables décrites dans la description et les documents associés avant que l’utilisateur installe votre application. Les Teams que votre application prend en charge doivent être liées aux fonctions principales que votre description décrit.
* Inclure un lien d’aide ou de support.
* **Reportez-vous Microsoft 365** au lieu de **Office 365**.
* Si vous devez référencer **Teams**, écrivez la première référence en **tant que Microsoft Teams**. Les références suivantes peuvent être raccourcies **Teams**.
* Utilisez le langage suivant pour décrire le fonctionnement de l’application avec Teams (ou Microsoft 365) :
  * "... fonctionne avec Microsoft Teams. »
  * "... travailler avec Microsoft Teams. »
  * "... dans Microsoft Teams. »
  * "... pour Microsoft Teams. »

**À ne pas faire :**

* Dépassez 500 mots.
* Abréviation **de Microsoft** en tant que **MS** ou **MSFT**.
* Indiquez que l’application est une offre de Microsoft, y compris à l’aide de balises ou de balises microsoft.
* Utilisez des noms de marque protégés par des droits d’auteur que vous ne possédez pas.
* Inclure des fautes de frappe, des erreurs grammaticales et des majuscules inutiles (par **exemple,** Utilisateurs au lieu des **utilisateurs).**
* Inclure des liens vers AppSource.
* Utilisez la langue suivante, sauf si vous êtes un partenaire Microsoft certifié :
  * "... intégré à Microsoft Teams »
  * "... s’intègre avec ...
  * "... conçu pour ...
  * "... intégré à ...
  * "... s’exécute sur ...
  * "... activé par ...
  * "... certifié pour ...
  * "... développé pour ...
  * "... conçu pour ...

### <a name="44-screenshots"></a>4.4 Captures d’écran

Les captures d’écran fournissent un aperçu visuel de votre application pour compléter le nom, l’icône et les descriptions de votre application. Souvenez-vous des captures d’écran suivantes :

* Vous pouvez avoir jusqu’à cinq captures d’écran par liste.
* Les types de fichiers pris en charge sont PNG, JPEG et GIF.
* Les dimensions doivent être de 1 366 x 768 pixels.
* Taille maximale de 1 024 Ko.

**À faire :**

* Concentrez-vous sur les fonctionnalités de votre application (par exemple, comment les personnes peuvent communiquer avec votre bot).
* Incluez du contenu qui représente précisément votre application.
* Utilisez du texte judicieusement.
* Captures d’écran avec une couleur qui reflète votre marque et inclut du contenu marketing, similaire à l’exemple de listing [Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) (les exigences de dimension s’appliquent à l’image entière et pas seulement à la capture d’écran).

**À ne pas faire :**

* Afficher des appareils spécifiques, tels que des téléphones ou des ordinateurs portables.
* Afficher le chrome ou l’interface utilisateur qui ne se présente pas dans votre application.
* Capturez les Teams ou l’interface utilisateur du navigateur dans vos captures d’écran.
* Incluez des maquettes qui reflètent de manière incorrecte l’interface utilisateur réelle de votre application, comme l’affichage de votre application utilisée en dehors de Teams.

> [!TIP]
> Une vidéo peut être le moyen le plus efficace de communiquer pourquoi les personnes doivent utiliser votre application. Une vidéo est également la première chose que les utilisateurs voient dans votre liste (par défaut, une vidéo s’affiche avant les captures d’écran). Pour plus d’informations, [voir créer une vidéo pour votre listing dans le Store.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)

### <a name="45-privacy-policy"></a>4.5 Politique de confidentialité

La politique de confidentialité peut être spécifique à votre application Teams ou une stratégie globale pour tous vos services.

* Si vous utilisez un modèle de stratégie de confidentialité générique, vous devez référencer des **services,** **des applications** et des **plateformes** pour inclure votre application Teams et votre service ou site web.
* Doit inclure la façon dont vous traitez le stockage, la rétention et la suppression des données utilisateur. Vous devez également décrire les contrôles de sécurité que vous utilisez pour la protection des données.
* Doit inclure vos informations de contact.
* Ne doit pas contenir d’URL rompues ou à des fins bêta ou intermédiaire.
* Ne doit pas inclure de liens vers AppSource.

### <a name="46-terms-of-use"></a>4.6 Conditions d’utilisation

Vos conditions d’utilisation doivent être spécifiques et applicables à votre offre.

### <a name="47-support-links"></a>4.7 Liens de support

Les URL de support de votre application ne doivent pas nécessiter d’authentification. Par exemple, les utilisateurs ne doivent pas avoir à se connecter pour vous contacter.

### <a name="48-localization"></a>4.8 Localisation

Si votre application prend en charge la localisation, votre package d’application doit inclure un fichier avec des traductions linguistiques qui s’affichent en fonction du paramètre Teams langue. Le fichier doit être conforme au schéma Teams de localisation. Pour plus d’informations, [voir Teams schéma de localisation.](~/concepts/build-and-test/apps-localization.md)

## <a name="50-tabs"></a>5.0 Onglets

Si votre application inclut un onglet, assurez-vous qu’elle respecte ces recommandations.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les recommandations [Teams de conception d’onglets.](~/tabs/design/tabs.md)

### <a name="51-setup"></a>5.1 Installation

* La configuration de l’onglet ne doit pas arrêter un nouvel utilisateur. Fournissez un message sur la façon d’effectuer l’action ou le flux de travail.
* L’authentification doit avoir lieu pendant la configuration de l’onglet et non après.

### <a name="52-views"></a>5.2 Affichages

* La zone d’écran de la signature ne doit pas utiliser de grands logos ni afficher une page web entière.
* Le contenu peut être simplifié en le parsent sur plusieurs onglets.
* Les onglets ne doivent pas avoir d’en-tête en double. Supprimez le logo de l’iframe, car l’infrastructure d’onglet affiche déjà l’icône et le nom de l’application.

### <a name="53-navigation"></a>5.3 Navigation

* Les onglets ne doivent pas avoir plus de trois niveaux de navigation.
* Les onglets ne doivent pas fournir de navigation en conflit avec le Teams navigation principale.
* Les pages secondaires et troisièmes d’un onglet doivent être ouvertes dans un affichage de niveau 2 et 3 dans la zone d’onglet principale, qui est accessible via une navigation à gauche ou une navigation à gauche. Vous pouvez également inclure les composants suivants pour faciliter la navigation par onglets :
    * Boutons Arrière
    * En-têtes de page
    * Menus hamburger
* La tabulation ne doit pas avoir de défilement horizontal.
* Les liens profonds dans les onglets ne doivent pas être lié à une page web externe, mais quelque part dans Teams. Par exemple, les modules de tâche ou d’autres onglets.
* Les onglets ne doivent pas permettre aux utilisateurs de naviguer en dehors Teams pour l’expérience d’application principale.

### <a name="54-usability"></a>5.4 Utilisation

* Les onglets doivent fournir une valeur au-delà du simple hébergement d’un site web existant.
* Les utilisateurs doivent pouvoir annuler leur dernière action dans l’onglet.
* Les onglets dans un contexte personnel peuvent agréger le contenu des instances partagées de l’application.
* Les onglets doivent répondre Teams thèmes. Lorsqu’un utilisateur modifie le thème, le thème de l’application doit refléter la sélection.
* Les onglets doivent utiliser des composants de style Teams, tels que les polices Teams, les gammes de types, les palettes de couleurs, le système de grille, le mouvement, le ton de la voix, etc. dans la mesure du possible.
* Vous devez inclure un **onglet Paramètres’onglet.**
* Les onglets doivent suivre Teams conception de l’interaction, telle que la navigation dans la page, la position et l’utilisation des boîtes de dialogue, des hiérarchies d’informations, etc. dans la mesure du possible.
* Le contenu de l’onglet dans l’iframe ne doit pas inclure de fonctionnalités qui imitent Teams fonctionnalités principales. Par exemple, les bots, les extensions de messagerie, les appels, les réunions, etc.

> [!TIP]
>
> * Incluez un bot personnel avec un onglet personnel.
> * Autoriser les utilisateurs à partager du contenu à partir de leur onglet personnel.

## <a name="60-bots"></a>6.0 Bots

Si votre application inclut un bot, assurez-vous qu’elle respecte ces recommandations.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les recommandations [Teams conception de bot.](~/bots/design/bots.md)

### <a name="61-bot-commands"></a>6.1 Commandes de bot

L’analyse de l’entrée utilisateur et la prévision de l’intention de l’utilisateur sont difficiles. Les commandes de bot fournissent aux utilisateurs un ensemble de mots ou d’expressions que votre bot comprend afin qu’ils (et votre bot) n’ont pas à deviner.

* Il est vivement recommandé de répertorier les commandes de bot prise en charge dans les configurations de votre application. Ces commandes s’affichent dans la zone de composition lorsqu’un utilisateur tente d’envoyer un message à votre bot.
* Toutes les commandes que votre bot prend en charge doivent fonctionner correctement, y compris les commandes **Bonjour,** **Hello** et **Aide.**

> [!TIP]
> Pour les bots personnels, incluez un onglet **Aide** qui décrit plus en détail ce que votre bot peut faire.

### <a name="62-bot-welcome-messages"></a>6.2 Messages de bienvenue du bot

* Les bots doivent presque toujours envoyer un message de bienvenue lors de la première run. Pour une expérience de qualité, le message doit inclure la proposition de valeur de votre bot, la configuration du bot et décrire brièvement toutes les commandes de bot prise en charge. Vous pouvez afficher le message à l’aide d’une carte adaptative avec des boutons pour une meilleure utilisation. Pour plus d’informations, [voir comment déclencher un message de bienvenue du bot.](~/bots/how-to/conversations/send-proactive-messages.md)
* Les messages d’accueil du bot dans les canaux et les conversations sont facultatifs lors de la première utilisation, en particulier si le bot est disponible pour un usage personnel et effectue des actions similaires. Si votre bot envoie des messages de bienvenue, il ne doit pas les envoyer aux utilisateurs individuellement (ceci est considéré comme [du courrier indésirable).](#63-bot-message-spamming) Le message doit également mentionner la personne qui a ajouté le bot.
* Les bots de notification uniquement doivent envoyer un message de bienvenue qui leur communique qu’ils ne répondront pas aux messages des utilisateurs.

> [!TIP]
> Dans les messages de bienvenue à des utilisateurs individuels, une visite guidée en carrousel peut fournir une vue d’ensemble efficace de votre bot et de toutes les autres fonctionnalités de l’application. Il est vivement encouragé d’inclure des boutons pour que les utilisateurs essaient les commandes de bot. Par exemple, **créez une tâche.**

### <a name="63-bot-message-spamming"></a>6.3 Courrier indésirable de bot

Les bots ne doivent pas envoyer de courrier indésirable aux utilisateurs en envoyant plusieurs messages successivement.

* **Messages de bot dans les canaux et conversations**: ne pas envoyer de courrier indésirable aux utilisateurs en créant des publications distinctes. Créez un billet unique avec des réponses dans le même fil de discussion.
* **Messages de bot dans les applications personnelles**: n’envoyez pas plusieurs messages successivement. Envoyez un message avec des informations complètes. Évitez les conversations à plusieurs tour pour terminer un seul flux de travail. Envisagez plutôt d’utiliser un formulaire (ou un module de tâche) pour collecter toutes les entrées d’un utilisateur en même temps.
* **Messages de bienvenue**: répéter le même message de bienvenue à intervalles réguliers n’est pas autorisé et considéré comme du courrier indésirable. Par exemple, lorsqu’un nouveau membre est ajouté à une équipe, ne spam pas les autres membres avec un message de bienvenue. Message personnel du nouveau membre.

### <a name="64-bot-notifications"></a>6.4 Notifications de bot

Les notifications de bot doivent inclure du contenu pertinent pour l’étendue que vous définissez pour le bot (équipe, conversation ou personnel).

### <a name="65-bots-and-adaptive-cards"></a>6.5 Bots et cartes adaptatives

Les cartes adaptatives sont un moyen fortement recommandé d’afficher des messages de bot. Vos cartes doivent être légères et inclure uniquement 1 à 3 actions. Si vous avez besoin d’afficher davantage de contenu, envisagez d’utiliser un module de tâche ou un onglet.

Pour plus d'informations, consultez les ressources suivantes :

* [Conception de cartes adaptatives](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Référence de cartes](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="70-messaging-extensions"></a>7.0 Extensions de messagerie

Si votre application inclut une extension de messagerie, assurez-vous qu’elle respecte ces recommandations.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les instructions [Teams conception d’extension de messagerie.](~/messaging-extensions/design/messaging-extension-design.md)

### <a name="71-action-commands"></a>7.1 Commandes d’action

Les extensions de messagerie basées sur l’action doivent :

* Autoriser les utilisateurs à déclencher des actions sur un message sans effectuer d’étapes intermédiaires, telles que la signature.
* Passez le contexte du message à l’état de travail suivant.

### <a name="72-preview-links-link-unfurling"></a>7.2 Aperçu des liens (déploiement de lien)

Les extensions de messagerie doivent prévisualiser les liens reconnus dans la Teams de composition. N’ajoutez pas de domaines qui sont en dehors de votre contrôle (URL absolues ou caractères génériques). Par exemple, `yourapp.onmicrosoft.com` est valide, mais `*.onmicrosoft.com` n’est pas valide. Les domaines de niveau supérieur sont également interdits (par exemple, `*.com` ou `*.org` ).

### <a name="73-search-commands"></a>7.3 Commandes de recherche

* Les extensions de messagerie basées sur la recherche doivent fournir du texte qui aide les utilisateurs à effectuer des recherches efficacement.
* @mention exécutables doivent être clairs, faciles à comprendre et lisibles.

## <a name="80-task-modules"></a>Modules de tâche 8.0

Un module de tâche doit inclure une icône et le nom court de l’application à qui il est associé.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les instructions Teams de conception du [module de tâche.](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="90-meeting-extensions"></a>9.0 Extensions de réunion

Si votre application inclut une extension de réunion, assurez-vous qu’elle respecte ces recommandations.

> [!TIP]
> Pour plus d’informations sur la création d’une expérience d’application de haute qualité, voir les instructions Teams [conception d’extension de réunion.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)

### <a name="91-pre--and-post-meeting-experience"></a>9.1 Expérience avant et après la réunion

* Les écrans avant et après la réunion doivent respecter les recommandations générales en matière de conception d’onglets. Pour plus d’informations, voir les [recommandations Teams conception.](~/tabs/design/tabs.md)
* Les onglets ne doivent pas avoir un défilement horizontal.
* Les onglets doivent avoir une disposition organisée lors de l’affichage de plusieurs éléments. Par exemple, plus de 10 sondages ou enquêtes. Voir un [exemple de disposition.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting)
* Votre application doit informer les utilisateurs lorsque les résultats d’une enquête ou d’un sondage sont exportés en indiquant « Résultats téléchargés avec succès ».

### <a name="92-in-meeting-experience"></a>9.2 Expérience en réunion

* Les applications doivent uniquement utiliser un thème foncé pendant les réunions. Pour plus d’informations, voir les [recommandations Teams conception.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)
* Une boîte à outils doit afficher le nom de l’application lorsque vous placez le pointage sur l’icône de l’application pendant les réunions.
* Les extensions de messagerie doivent fonctionner de la même manière pendant les réunions qu’en dehors des réunions.

### <a name="93-in-meeting-tabs"></a>9.3 Onglets de réunion

* Doit être réactif. Veillez à maintenir la taille des remplissages et des composants.
* Doit avoir un bouton Retour s’il existe plusieurs couches de navigation.
* Ne doit pas inclure plusieurs boutons d’arrêt ou de fermeture. Cela peut dérouter les utilisateurs, car il existe déjà un bouton d’en-tête intégré pour faire disparaître l’onglet.
* Ne doit pas avoir de défilement horizontal.

### <a name="94-in-meeting-dialogs"></a>9.4 Boîtes de dialogue en réunion

* Doit être utilisé avec parcimonie et pour les scénarios légers et orientés vers les tâches.
* Doit afficher le contenu dans une seule colonne et ne pas avoir plusieurs niveaux de navigation.
* Ne doit pas utiliser de modules de tâche.
* Doit s’aligner sur le centre de la phase de réunion.
* Doit être rejeté lorsqu’un utilisateur sélectionne un bouton ou effectue une action.

## <a name="100-notifications"></a>10.0 Notifications

Si votre application utilise les API de flux d’activités fournies par [Microsoft Graph](/graph/teams-send-activityfeednotifications), assurez-vous qu’elle respecte les instructions suivantes.

### <a name="101-general"></a>10.1 Général

* Tous les déclencheurs de notification spécifiés dans les configurations de votre application doivent recevoir une notification dans l’application.
* Les notifications doivent être localisées selon les langues de prise en charge configurées pour votre application.
* Les notifications doivent s’afficher dans les cinq secondes après l’action de l’utilisateur.

### <a name="102-avatars"></a>10.2 Avatars

* L’avatar de notification doit correspondre à l’icône de couleur de votre application.
* Les notifications déclenchées par un utilisateur doivent inclure l’avatar de l’utilisateur.

### <a name="103-spamming"></a>10.3 Spamming

* Les applications ne doivent pas envoyer plus de 10 notifications par minute à un utilisateur.
* Les bots et le flux d’activités ne doivent pas déclencher de notifications en double.
* Les notifications doivent fournir une valeur ajoutée aux utilisateurs et ne pas être utilisées pour des événements trivials ou non pertinents.

### <a name="104-navigation-and-layout"></a>10.4 Navigation et disposition

* Les notifications doivent respecter la disposition et l’expérience Teams flux d’activités.
* Lors de la sélection d’une notification, l’utilisateur doit être dirigé vers du contenu pertinent au sein Teams et ne pas être retiré de l’expérience Teams’utilisateur.

## <a name="110-advertising"></a>11.0 Publicité

Les applications ne doivent pas afficher de publicités, y compris les publicités dynamiques, les bannières publicitaires et les publicités dans les messages.

## <a name="see-also"></a>Voir aussi

[Package d’application 4.0 et liste du Store](#40-app-package-and-store-listing)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Créer un compte d’Espace partenaires](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
