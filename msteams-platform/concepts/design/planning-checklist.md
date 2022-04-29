---
title: Questions pour aider à planifier le développement de l'application Teams
author: heath-hamilton
description: "Questions à prendre en compte lors de la planification de votre application : comprendre l'utilisateur et ses besoins, comprendre les problèmes que votre application pourrait résoudre, planifier l'authentification de l'utilisateur et son expérience d'intégration."
ms.topic: conceptual
ms.localizationpriority: high
ms.author: surbhigupta
ms.openlocfilehash: 4620d1bc17332e40f79c429769090f1ce7b2210f
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104307"
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

| # | Facteurs |
| --- | --- |
| 1 | Les utilisateurs sont-ils principalement des employés de première ligne sur des clients mobiles ? |
| 2 | Vous attendez-vous à ce que de nombreux utilisateurs invités aient besoin d'accéder à votre application ? |
| 3 | Utilisent-ils des équipes et des canaux ou principalement des conversations de groupe ? |
| 4 | Quel est le niveau de sophistication technique de vos principaux utilisateurs ? |
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

| # | Facteurs|
|--- | --- |
| 1 | Les utilisateurs auront-ils accès à différentes affichages des données en fonction de leur rôle ? |
| 2 | Y a-t-il des informations d’identification personnelle impliquées ? |
| 3 | Les interactions seront-elles également basées sur les rôles des utilisateurs ? |
| 4 | Des utilisateurs externes auront-ils accès à l'application ? |

</details>
<br>
<details>
<summary>Planifier l’expérience d’intégration</summary>

| # | Facteurs |
| --- | --- |
| 1 | Que se passe-t-il lorsqu'un utilisateur configure pour la première fois votre onglet dans un canal ? |
| 2 | Si vous partagez des cartes avec une extension de messagerie, est-il judicieux d'ajouter un petit lien vers une page d'informations pour présenter aux utilisateurs les autres possibilités offertes par votre application ? |
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
| 1 | Les informations présentées par l’application, sous l’onglet ou via un bot, sont-elles pertinentes et utiles pour la plupart des membres d’une équipe ? Par exemple, l’application Scrum. |
| 2 | Le contexte de l'application pourrait-il changer en fonction de l'équipe dans laquelle elle est ajoutée ? Par exemple, les tâches du planificateur sont différentes selon les équipes. |
| 3 | Est-il possible que tous les membres d’un personnage qui ont besoin de collaborer font partie d’une seule équipe ? Par exemple, les agents travaillant sur un ticket. |

</details>
<br>
<details>
<summary>Choisir l’environnement de build</summary>

Suggestion : des options permettant de sélectionner l'environnement approprié en fonction des besoins de l'application.
</details>
<br>
<details>
<summary>Planifier le test de l’application</summary>

Suggestion : des options qui permettent de déterminer le meilleur environnement de test pour l’application.
</details>
<br>
<details>
<summary>Planifier la distribution des applications</summary>

Suggestion : des options qui permettent de déterminer le meilleur modèle de distribution.

</details>

## <a name="plan-for-hosting-your-teams-app"></a>Planifier l’hébergement de votre application Teams web

Teams n’héberge pas votre application. Lorsqu’un utilisateur installe votre application dans Teams, il installe un package d’application qui contient un seul fichier de configuration (également appelé manifeste d’application) et les icônes de votre application. La logique de l’application et le stockage des données sont hébergés ailleurs, par exemple sur localhost pendant le développement et sur Azure Web Services. Teams accède à ces ressources via HTTPS.

:::image type="content" source="../../assets/images/teams-app-host.png" alt-text="Illustration montrant l’hébergement d’applications pour Application Teams" border="true":::

## <a name="plan-beyond-app-building"></a>Planifier au-delà de la création d’applications

- **Décidez de ce qui va dans Teams** : Qu'il s'agisse d'une nouvelle application ou d'une application existante, vérifiez si vous souhaitez que l'application entière soit intégrée au client Teams. Si vous n'intégrez qu'une partie de l'application, concentrez-vous sur le partage, la collaboration, le lancement et le suivi des flux de travail.

- **Planifiez l'expérience d'intégration** : concevez votre expérience d'accueil en pensant à vos principaux utilisateurs. La façon dont vous présentez un robot de conversation installé dans un canal avec un millier de personne est différente lorsqu’il est installé dans une conversation individuelle.

- **Planifier l’avenir** : identifiez les nouvelles fonctionnalités que l’utilisateur préférera dans la solution actuelle. Toute nouvelle fonctionnalité peut avoir un impact sur la conception et l’architecture de l’application.
