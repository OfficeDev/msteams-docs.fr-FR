---
title: Modèles d’applications Microsoft teams
description: Liens et descriptions des modèles d’application pour la plateforme Microsoft teams
keywords: Démonstration des exemples de modèles Microsoft teams
ms.openlocfilehash: 36f04727828b3bfa3be9b808cafcd33c11bf2c0d
ms.sourcegitcommit: 646a8224523be7db96f9686e22d420d62d55d4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/02/2020
ms.locfileid: "42365268"
---
# <a name="app-templates-for-microsoft-teams"></a>Modèles d’application pour Microsoft teams

Les modèles d’application sont des applications prêtes pour la production pour Microsoft Teams, basées sur la Communauté, la source ouverte et disponibles sur GitHub. Chacun d’eux contient des instructions détaillées pour le déploiement et l’installation de cette application pour votre organisation, en fournissant une application prête à l’emploi que vous pouvez installer et commencer à utiliser immédiatement. Le code source complet est également disponible, ce qui vous permet de l’Explorer en détail ou de le modifier pour répondre à vos besoins spécifiques.

## <a name="key-benefits-of-using-app-templates"></a>Principaux avantages de l’utilisation des modèles d’application

* **Expérience plug-and-Play :** Tous les modèles d’application incluent des scripts de déploiement qui vous permettront d’héberger tous les services nécessaires dans Microsoft Azure. Aucun codage n’est requis pour déployer les applications.
* **Code prêt pour la production :** Les modèles d’application sont conformes aux meilleures pratiques recommandées en matière de sécurité et d’infrastructure, et toutes les modifications apportées à celles-ci sont examinées afin de garantir une poursuite de la conformité.
* **Personnalisable et extensible :** Alors que tous les modèles d’application sont prêts à être déployés tels quels, nous fournissons la base de code et les scripts de déploiement complets afin que vous puissiez facilement les personnaliser ou les étendre afin de répondre à vos besoins spécifiques.
* **Documentation détaillée & la prise en charge :** Tous les modèles d’application sont accompagnés d’une documentation de bout en bout sur l’architecture de la solution, le déploiement et les étapes de configuration. Les référentiels étant également surveillés, veuillez signaler tous les problèmes que vous rencontrez en générant un problème sur GitHub.

## <a name="celebrations"></a>Célébrations

Celebrations est une application de teams qui permet aux membres de l’équipe de célébrer les anniversaires, les commémorations et autres événements périodiques. Il se souvient des occasions spéciales de tous les membres de l’équipe et envoie un message convivial dans toutes les équipes sélectionnées au moment de la création d’un événement, afin que les membres de l’équipe semblent particuliers le jour.

L’application fournit une interface simple permettant à tous les membres de l’équipe d’ajouter et d’afficher personnellement leurs événements et permet également à l’utilisateur de sélectionner les équipes dans lesquelles les événements sont partagés.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="company-communicator"></a>Communicateur d’entreprise

L’application Communicator de l’entreprise permet aux équipes de créer et d’envoyer des messages destinés à plusieurs équipes ou à un grand nombre d’employés via une conversation, ce qui permet aux organisations d’atteindre directement les employés où elles collaborent. Utilisez ce modèle pour plusieurs scénarios tels que les nouvelles annonces de l’initiative, l’intégration des employés, l’apprentissage et le développement modernes ou les diffusions à l’échelle de l’organisation.

L’application fournit une interface simple permettant aux utilisateurs désignés de créer, de prévisualiser, de collaborer et d’envoyer des messages.

Elle permet de créer des fonctionnalités de communication ciblées personnalisées, telles que la télémétrie personnalisée sur le nombre d’utilisateurs ayant reçu ou interagi avec un message.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![Forum aux questions et GIF](~/assets/images/CompanyCommunicatorCompose.png)

## <a name="faq-plus"></a>Forum aux questions

Q conversation&les robots sont un moyen simple de fournir des réponses aux questions fréquemment posées par les utilisateurs. Toutefois, la plupart des bots ne s’engagent pas correctement avec les utilisateurs, car il n’y a aucun humain dans la boucle lorsque le bot échoue. Le bot FAQ est un Q convivial&un bot qui amène un humain dans la boucle lorsqu’il n’est pas en mesure d’aider. Un peut poser une question au bot et le bot répond avec une réponse si elle est contenue dans la base de connaissances. Si ce n’est pas le cas, le bot permet à l’utilisateur de soumettre une requête qui est ensuite publiée dans une équipe d’experts préconfigurée qui aide à fournir une assistance en agissant sur les notifications à partir de son équipe.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-faqplusplus-app)

> [!NOTE]
> La version 2020 de **FAQ plus, version 2** prend en charge des Q&s améliorées en permettant à l’équipe d’experts de réaliser les opérations suivantes :
>
> &#x2714; ajouter de nouvelles&Q directement à la base de connaissances à l’aide des extensions de message.
>
> &#x2714; modifier et supprimer Q&une paire ajoutée par un bot.
>
> &#x2714; effectuer le suivi de l’historique des révisions de Q&en tant que.
>
> &#x2714; configurer une réponse avec des détails supplémentaires à afficher sous forme de [carte adaptative](/task-modules-and-cards/cards/cards-reference#adaptive-card).
>
>[**L’obtenir sur GitHub**](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)
>
>

![Forum aux questions et GIF](~/assets/images/FAQPlusEndUser.gif)

## <a name="hr-support"></a>Prise en charge RH

HR support bot est un Q convivial&un bot qui fournit un spécialiste/expert du support technique de l’équipe RH dans la boucle lorsqu’il ne peut pas aider. Un peut poser une question au bot et le bot répond avec une réponse si elle est contenue dans la base de connaissances. Si ce n’est pas le cas, le bot permet à l’utilisateur de soumettre une requête qui est ensuite publiée dans une équipe d’experts préconfigurée qui aide à fournir une assistance en agissant sur les notifications à partir de son équipe. De plus, le bot propose des liens vers des questions/stratégies RH recommandées en recherchant des balises préconfigurées dans la question. Ces vignettes sont également disponibles dans l’onglet associé sous forme de référence rapide. La prise en charge des RH fonctionne bien pour les QnA de poids léger et pour fournir une assistance rapide lors du lancement de nouveaux projets/initiatives au sein de l’organisation.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![Prise en charge RH](~/assets/images/expert-user.png)

## <a name="list-search"></a>Recherche de liste

La collaboration dans Microsoft teams fait souvent référence à des informations contenues dans les éléments d’une liste SharePoint. Le simple collage d’un lien vers l’élément en question force tout le monde à basculer le contexte à l’extérieur de la conversation, à trouver les informations nécessaires, puis à revenir à teams pour poursuivre la conversation. Au fur et à mesure de la conversation, les personnes devront généralement revenir à l’élément de référence plusieurs fois pour vérifier les nouveaux commentaires et actualiser leurs souvenirs des informations contenues dans l’élément. Ce changement de contexte crée une barrière à des fins de collaboration et constitue une recette pour les choses qui passent par les fissures.

Pour vous aider à résoudre ce problème, nous vous offrons le modèle d’application de recherche de liste. Des millions d’utilisateurs utilisent SharePoint pour alimenter certains des flux de travail de base au sein de leur organisation. Toutefois, la collaboration sur les listes peut être particulièrement fastidieuse. À l’aide du modèle d’application de recherche de liste de Microsoft Teams, les utilisateurs peuvent insérer des informations à partir d’éléments de liste SharePoint directement au sein d’une conversation de conversation afin d’atténuer le changement de contexte provoqué lors de l’insertion d’un lien dans une conversation. Les informations sont insérées sous la forme d’une carte à format automatique facile à lire, permettant ainsi à vos utilisateurs de participer à la conversation.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![Application de recherche de liste](~/assets/images/list-search-template.png)

## <a name="custom-stickers"></a>Autocollants personnalisés

L’auto-expression est essentielle pour une culture d’équipe saine. Ce modèle d’application est une [extension de messagerie](~/messaging-extensions/what-are-messaging-extensions.md) qui permet à vos utilisateurs d’utiliser des autocollants et des images gif personnalisées dans Microsoft Teams. Ce modèle offre une expérience de configuration Web simple où un utilisateur disposant d’un accès à la configuration peut télécharger les images gif/autocollantes/images dont il veut que les utilisateurs finals disposent, ce qui permet à l’ensemble de votre équipe d’utiliser n’importe quel ensemble d’autocollants que vous avez choisis.

Cette application permet également de partager facilement des images/des images/gif/autocollants entre les équipes sans avoir à accéder à des sites SharePoint ou à des canaux individuels comme mécanismes de stockage et de partage. Par exemple, les équipes de produits peuvent facilement partager des images de produits et des images gif sur des équipes de marketing, de marketing et de médias sociaux par programme. Il est également possible d’étendre cette application en déclenchant un flux de notification à des équipes ou des utilisateurs spécifiques lorsque de nouvelles images/gif sont mis à disposition.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![Application d’autocollants](~/assets/images/stickers.png)

## <a name="icebreaker"></a>Brise-glace

Il s’agit d’un [robot Microsoft teams](../bots/what-are-bots.md) qui permet à votre équipe de se rapprocher en appariant deux membres d’équipe aléatoires, chaque semaine, pour répondre à vos besoins. Le bot facilite la planification en suggérant automatiquement des temps libres qui fonctionnent pour les deux membres. Renforcer les connexions personnelles et créer une communauté étroitement à l’aide de cette application.

En plus d’encourager les connexions personnelles à l’ensemble de votre équipe, l’application brise-glace peut vous aider à cultiver des communautés d’intérêt au sein de votre organisation. Par exemple, vous pouvez utiliser cette application pour un groupe d’intérêt DevOps afin d’aider les idées et les meilleures pratiques dispersées dans votre organisation.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Application brise-glace](~/assets/images/icebreaker.png)

## <a name="scrum-status-bot"></a>Bot d’état de Scrum

Scrum Status bot est un robot Assistant de Scrum simple qui permettra aux utilisateurs d’exécuter des réunions de mise en attente asynchrones et de permettre aux utilisateurs de partager leurs mises à jour quotidiennes et facilement. Il est conçu pour fonctionner dans les conversations de groupe teams et tous les membres peuvent contribuer à Scrum. Une possibilité de démarrer et de terminer un Scrum et de consulter les mises à jour effectuées par d’autres personnes dans un Scrum en cours d’exécution.

[Git sur GitHub](https://github.com/OfficeDev/microsoft-teams-app-scrumstatus/)

![Bot d’état de Scrum](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="crowdsourcer-bot"></a>Robot Crowdsourcer

Crowdsourcer est un [robot Microsoft teams](../bots/what-are-bots.md) qui donne aux équipes des informations de la part des membres du groupe. Il s’agit d’un excellent moyen de répondre aux questions fréquemment posées, tout en permettant aux participants de s’engager activement et de contribuer à une ressource d’informations amusantes et utiles.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![Interaction de l’utilisateur final échangez](../assets/images/crowdsourcer.png)

## <a name="expert-finder-bot"></a>Robot de recherche d’expert

Le Finder expert est un [robot Microsoft teams](../bots/what-are-bots.md) qui identifie les membres spécifiques de l’organisation en fonction de leurs compétences, de leurs centres d’intérêt et de leurs attributs d’éducation. Les membres recherchent des experts au sein d’une organisation qui correspondent à une recherche par mot clé des profils utilisateur Azure Active Directory.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![Démonstration des résultats de recherche expert Finder](../assets/images/expert-finder.png)

## <a name="book-a-room-bot"></a>Livre-un bot de salle

Book-a-Room est un [robot Microsoft teams](../bots/what-are-bots.md) qui permet aux utilisateurs de trouver et de réserver rapidement une salle de réunion pour 30 (par défaut), 60 ou 90 minutes à compter de l’heure actuelle. Les étendues de bot livre-a-room aux conversations personnelles ou 1:1.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![Livre-démo de salle](../assets/images/book-a-room.png)

## <a name="attendance-app"></a>Application assiduité

L’application de participation est un onglet [d’applications puissantes](https://docs.microsoft.com/powerapps/maker/canvas-apps/embed-teams-appdesigned) qui peut être épinglé dans une équipe. Elle est conçue pour enregistrer la présence, généralement dans des paramètres tels que les environnements d’apprentissage et de formation. Les utilisateurs peuvent marquer ou modifier la participation pendant 30 jours au plus et afficher des rapports de présence résumés pour un groupe entier ou des participants individuels.

[L’obtenir sur GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![Démonstration de l’application assiduité](../assets/images/attendance-app.png)

Vous avez une idée pour un modèle d’application que vous aimeriez voir ? [Faites-nous part](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)de vos commentaires.
