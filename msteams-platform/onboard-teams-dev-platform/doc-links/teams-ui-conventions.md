---
title: Détermination des contextes de vos applications teams
author: heath-hamilton
description: Lors de la planification de votre application Teams, vous devez décider si l’application sera utilisée dans des espaces de collaboration, des espaces personnels ou les deux.
ms.openlocfilehash: 05c92aa8b199cbdb58e477fb4a64467c150edbfd
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651953"
---
# <a name="getting-to-know-teams-ui-conventions"></a>Découverte des conventions de l’interface utilisateur de teams

Les applications présentent généralement une ou plusieurs conventions d’interface utilisateur de teams standard. L’élaboration des fonctionnalités de votre application à l’aide de ces conventions conduit à des expériences enrichies qui semblent natives pour les utilisateurs de teams.

## <a name="cards"></a>Cartes

Les [cartes](~/task-modules-and-cards/what-are-cards.md) sont des conteneurs d’interface utilisateur définis par schématisées JSON pouvant contenir plusieurs propriétés et pièces jointes. Ils peuvent contenir du texte mis en forme, des médias, des contrôles (tels que des zones déroulantes et des cases d’option) et des boutons qui déclenchent des actions de carte.

Les actions de carte peuvent envoyer des charges utiles vers l’API de votre application, ouvrir un lien, initier des flux d’authentification ou envoyer des messages vers les conversations. La plateforme teams prend en charge plusieurs types de cartes, notamment des cartes adaptatives, des cartes héros, des cartes miniatures, etc. Vous pouvez combiner des collections de cartes et les afficher dans une liste ou un carrousel.

## <a name="task-modules"></a>Modules de tâche

Les [modules de tâches](~/task-modules-and-cards/what-are-task-modules.md) fournissent des expériences contextuelles modales dans Teams. Elles sont particulièrement utiles pour lancer des flux de travail, collecter des entrées d’utilisateur ou afficher des informations enrichies, telles que des vidéos ou des tableaux de bord Power BI. Dans les modules de tâches, vous pouvez exécuter du code frontal personnalisé, afficher un `<iframe>` widget ou afficher une carte adaptative.

Lorsque vous envisagez de créer votre application, rappelez-vous que les modaux sont naturels pour que les utilisateurs entrent des informations ou exécutent des tâches par rapport à un onglet ou à une expérience de robot basée sur une conversation.

## <a name="deep-links"></a>Liens profonds

Votre application peut créer [des liens détaillés d’URL](~/concepts/build-and-test/deep-links.md) pour vous aider à parcourir votre utilisateur via votre application, ainsi que le client Teams. Vous pouvez créer un lien profond pour la plupart des entités au sein de Teams, et certaines (par exemples, une nouvelle demande de réunion) vous permettent de pré-peupler des informations à l’aide de chaînes de requête dans l’URL. 

Par exemple, votre bot de conversation peut envoyer un message vers un canal avec un lien profond à un module de tâche qui génère une carte envoyée comme message individuel à un utilisateur, qui à son tour contient un lien profond pour créer une réunion avec un utilisateur spécifique à une date et heure donnée. Utilisez des liens profonds pour vous connecter entre les différents points d’extension disponibles pour votre application, en gardant à tout moment votre utilisateur dans le contexte approprié.

## <a name="web-based-content"></a>Contenu Web

Le [contenu Web](~/tabs/how-to/create-tab-pages/content-page.md) est une page Web que vous hébergez et qui peut être incorporée dans un sous-onglet ou un module de tâches. Pour incorporer votre page Web dans le client Teams, procédez comme suit :

* Inclure `HTTPS` dans l’URL.
* Être incorporée dans un `<iframe>` .
* Incluez le kit de développement logiciel (SDK) JavaScript client Microsoft teams et appelez la méthode du kit de développement logiciel `initialize()` sur le chargement des pages.

## <a name="next-steps"></a>Étapes suivantes

* [Conception de votre application](../../tabs/design/tabs.md)
