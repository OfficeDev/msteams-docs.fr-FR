---
title: Questions pour aider à planifier le développement de l'application Teams
author: heath-hamilton
description: Apprenez à planifier votre application à l’aide de la liste de vérification pour vous assurer que votre plan couvre les détails importants du développement d’applications. Planifier le cycle de vie de l’application. Prévoyez d’héberger votre application Teams.
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: 932e8ea564a6cc47bb2b8dbe4e01256d0688cefa
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100713"
---
# <a name="teams-app-planning-checklist"></a>Liste de vérification de la planification d’applications Teams

Le cycle de vie d'une application s'étend de la planification de votre application à son déploiement éventuel, et bien au-delà. Pour planifier votre application, connaître votre utilisateur et vos besoins ne suffisent pas. En fonction des besoins de votre application, vous pouvez également envisager la planification de futures mises à jour.

Examinons de manière pratique la planification du cycle de vie d’une application.

## <a name="relevant-questions"></a>Questions pertinentes

Voici une liste de questions à prendre en compte lorsque vous planifiez votre application. Utilisez-la comme indication pour vous assurer que votre plan couvre les détails importants du développement d’applications.

<br>
<br>
<details>
<summary>Comprendre votre utilisateur</summary>

Comprendre l’utilisateur et ses préoccupations sont les premiers indicateurs de la façon dont une application Teams peut vous aider. Créez votre cas d’usage autour du problème, déterminez comment une application peut le résoudre et dessinez une solution. Pour plus d’informations, consultez [comprendre vos cas d’usage](understand-use-cases.md).

| # | Facteurs |
| --- | --- |
| 1 | Les utilisateurs sont-ils principalement des employés de première ligne sur des clients mobiles ? |
| 2 | Vous attendez-vous à ce que de nombreux utilisateurs externes aient besoin d'accéder à votre application ? |
| 3 | Utilisent-ils des équipes et des canaux ou principalement des conversations de groupe ? |
| 4 | Quel est le niveau d’avancé technique de vos principaux utilisateurs ? |
| 5 | Vous avez besoin d'une expérience d'intégration complète ou quelques conseils peuvent suffire ? |

</details>
<br>
<details>
<summary>Comprendre le problème</summary>

| # | Facteurs |
|--- | --- |
| 1 | Quels sont les avantages et les inconvénients du système d'état actuel utilisé par vos utilisateurs ? |
| 2 | Quels sont les problèmes auxquels sont confrontés vos utilisateurs et que vous souhaitez résoudre ? |
| 3 | Quelles sont les fonctionnalités ou les capacités que vos utilisateurs apprécient dans leur façon actuelle d'effectuer le processus ? |

</details>
<br>
<details>
<summary>Comprendre les limitations de l’application</summary>

| # | Facteurs |
| --- | --- |
| 1 | Quels sont les défis liés à l'intégration du back-end de l'application actuelle ? |
| 2 | Qui est propriétaire des données du back-end (internes ou tierces) ? |
| 3 | Y a-t-il des pare-feu qui ont un impact sur le fonctionnement de l'application ? |
| 4 | Existe-t-il des API pour accéder aux données dont vous avez besoin pour le fonctionnement de votre application ? |

</details>
<br>
<details>
<summary>Fournir l’authentification</summary>

L’authentification consiste à valider les utilisateurs d’application et à sécuriser les utilisateurs de l’application et de l’application contre un accès injustifié. Vous pouvez utiliser une méthode d’authentification adaptée à votre application pour valider les utilisateurs de l’application qui souhaitent utiliser l’application Teams. Pour plus d’informations, consultez [Authentifier les utilisateurs dans Microsoft Teams](../authentication/authentication.md).

| # | Facteurs|
|--- | --- |
| 1 | Les utilisateurs auront-ils accès à différentes affichages des données en fonction de leur rôle ? |
| 2 | Y a-t-il du contenu d’utilisateur impliqué ? |
| 3 | Les interactions seront-elles également basées sur les rôles des utilisateurs ? |
| 4 | Des utilisateurs externes auront-ils accès à l'application ? |

</details>
<br>
<details>
<summary>Planifier l’expérience d’intégration</summary>

La création d’une application Teams exceptionnelle consiste à trouver la bonne combinaison de fonctionnalités pour répondre aux besoins de votre utilisateur. Pour offrir à vos utilisateurs une expérience d’intégration transparente, vous pouvez créer un guide pas à pas expliquant comment et quoi faire avec votre application. Par exemple, consultez [créer un bot de conversation Teams](../../sbs-teams-conversation-bot.yml).

| # | Facteurs |
| --- | --- |
| 1 | Que se passe-t-il lorsqu'un utilisateur configure pour la première fois votre onglet dans un canal ? |
| 2 | Si vous partagez des cartes avec une extension de messagerie, est-il judicieux d'ajouter un petit lien vers une page d'informations pour présenter aux utilisateurs les autres possibilités offertes par votre application ? |
| 3 | Vous attendez-vous à ce que la plupart des gens aient déjà une idée de ce à quoi sert votre application, ou qu'ils aient déjà utilisé vos services dans un autre contexte ? |
| 4 | Viennent-ils sur votre application sans aucune connaissance préalable ? |

</details>
<br>
<details>
<summary>Applications d’étendue personnelle</summary>

| # | Facteurs |
| --- | --- |
| 1 | Des interactions individuelles avec l'application sont-elles nécessaires pour des raisons de confidentialité ou autres ? Par exemple, la vérification du solde des congés ou d'autres informations privées. |
| 2 | Y aura-t-il une collaboration entre des utilisateurs qui n'ont peut-être pas d'équipes communes ? Par exemple, trouver les événements à venir au sein d'une entreprise. |
| 3 | Y a-t-il des notifications ou des messages personnalisés qui devront être envoyés à un utilisateur tout au long de l'expérience de l'application Teams ? |

</details>
<br>
<details>
<summary>Applications d’étendue partagée</summary>

| # | Facteurs |
| --- | --- |
| 1 | Is the information presented by the app, either in tab or through a bot, relevant and useful for most of the members in a Team? For example, Scrum app. |
| 2 | Le contexte de l'application peut-il changer en fonction de l'équipe dans laquelle elle est ajoutée ? Par exemple, les tâches du planificateur sont différentes selon les équipes. |
| 3 | Is it possible that all members in a persona who need to collaborate are a part of a single team? For example, agents working on a ticket. |

</details>
<br>
<details>
<summary>Choisir l’environnement de build</summary>

Avec Teams, vous pouvez choisir l’environnement de génération qui correspond le mieux aux besoins de votre application. Utilisez le Kit de ressources Teams ou d’autres Kits de développement logiciel (SDK), tels que C#, Blazor, Node.js, etc. pour commencer. Pour plus d’informations, consultez [Planifier votre application avec des fonctionnalités Teams](../app-fundamentals-overview.md).

Suggestion : des options permettant de sélectionner l'environnement approprié en fonction des besoins de l'application.
</details>
<br>
<details>
<summary>Planifier le test de l’application</summary>

Après avoir intégré votre application à Microsoft Teams, vous devez tester votre application avant de la publier. L’objectif final est d'obtenir un maximum d'utilisateurs pour votre application. Veillez donc à tester l'application sur plusieurs appareils que les utilisateurs pourraient utiliser. Pour plus d’informations, afficher [Mise à jour de votre application](../build-and-test/test-app-overview.md).

Suggestion : des options qui permettent de déterminer le meilleur environnement de test pour l’application.
</details>
<br>
<details>
<summary>Planifier la distribution des applications</summary>

Vous pouvez fournir votre application Microsoft Teams à une personne, une équipe, une organisation ou toute personne qui souhaite l’utiliser. La façon dont vous distribuez dépend de plusieurs facteurs, notamment les besoins des utilisateurs, l’activité, les exigences techniques et vos objectifs pour l’application. Pour plus d’informations, consultez [distribuer votre application Microsoft Teams](../deploy-and-publish/apps-publish-overview.md).

Suggestion : des options qui permettent de déterminer le meilleur modèle de distribution.

</details>

## <a name="plan-for-hosting-your-teams-app"></a>Planifier l’hébergement de votre application Teams web

Teams n’héberge pas votre application. Lorsqu’un utilisateur installe votre application dans Teams, il installe un package d’application qui contient un seul fichier de configuration (également appelé manifeste d’application) et les icônes de votre application. La logique de l’application et le stockage des données sont hébergés ailleurs, par exemple sur localhost pendant le développement et sur Azure Web Services. Teams accède à ces ressources via HTTPS.

:::image type="content" source="../../assets/images/teams-app-host.png" alt-text="Illustration montrant l’hébergement d’applications pour Application Teams":::

## <a name="plan-beyond-app-building"></a>Planifier au-delà de la création d’applications

- **Décidez de ce qui va dans Teams** : Qu'il s'agisse d'une nouvelle application ou d'une application existante, vérifiez si vous souhaitez que l'application entière soit intégrée au client Teams. Si vous n'intégrez qu'une partie de l'application, concentrez-vous sur le partage, la collaboration, le lancement et le suivi des flux de travail.

- **Planifiez l'expérience d'intégration** : concevez votre expérience d'accueil en pensant à vos principaux utilisateurs. La façon dont vous présentez un robot de conversation installé dans un canal avec un millier de personne est différente lorsqu’il est installé dans une conversation individuelle.

- **Planifier l’avenir** : identifiez les nouvelles fonctionnalités que l’utilisateur préférera dans la solution actuelle. Toute nouvelle fonctionnalité peut avoir un impact sur la conception et l’architecture de l’application.
