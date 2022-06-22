---
title: FAQ sur Live Share
description: Dans ce module, découvrez-en plus sur la FAQ Live Share.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.openlocfilehash: 0c51d88ba08dea50e23b0b8eb451f84557f1f867
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189295"
---
---

# <a name="live-share-sdk-faq"></a>FAQ sur le Kit de développement logiciel (SDK) de partage en direct

Obtenez des réponses aux questions courantes lors de l’utilisation de Live Share.<br>

<br>

<details>

<summary><b>Puis-je utiliser mon propre service Relais Azure Fluid ?</b></summary>

Oui. Lors de la construction de la classe `TeamsFluidClient`, vous pouvez définir votre propre `AzureConnectionConfig`. Live Share associe des conteneurs que vous créez à des réunions, mais vous devez créer votre propre Azure `ITokenProvider` pour signer des jetons pour vos conteneurs et des exigences régionales. Pour plus d'informations, voir la [Documentation Relais Azure Fluid](/azure/azure-fluid-relay/).

<br>

</details>

<details>

<summary><b>Combien de temps les données stockées dans le service hébergé de Live Share sont-elles accessibles ?</b></summary>

Toutes les données envoyées ou stockées via les conteneurs Fluid créés per le service Relais Azure Fluid de Live Share sont accessibles pendant 24 heures. Si vous souhaitez conserver les données au-delà de 24 heures, vous pouvez remplacer notre service Relais Azure Fluid hébergé par le vôtre. Vous pouvez également utiliser votre propre fournisseur de stockage en parallèle au service hébergé de Live Share.

<br>

</details>

<details>

<summary><b>Quels types de réunions prend Live Share en charge ?</b></summary>

Seules les réunions planifiées sont actuellement prises en charge et tous les participants doivent figurer dans le calendrier de la réunion. Les types de réunion tels que les appels en tête-à-tête, les appels de groupe et les réunions instantanées ne sont pas pris en charge.

<br>

</details>

<details>

<summary><b>Le package multimédia de Live Share fonctionne-t-il avec le contenu DRM ?</b></summary>

Non. Teams ne prend actuellement pas en charge les supports chiffrés pour les applications d’onglet.

<br>

</details>

<details>
<summary><b>Combien de personnes peuvent assister à une session Live Share ?</b></summary>

Actuellement, Live Share prend en charge un maximum de 100 participants par session.

<br>

</details>

## <a name="have-more-questions-or-feedback"></a>Vous avez d’autres questions ou commentaires ?

Soumettez des problèmes et des demandes de fonctionnalités au référentiel du Kit de développement logiciel (SDK) pour le [Kit de développement logiciel (SDK) Live Share](https://github.com/microsoft/live-share-sdk). Utilisez la balise `live-share` et `microsoft-teams` pour publier des questions de procédure sur le Kit de développement logiciel (SDK) sur [Stack Overflow](https://stackoverflow.com/questions/tagged/live-share+microsoft-teams).

## <a name="see-also"></a>Voir aussi

- [Référentiel GitHub](https://github.com/microsoft/live-share-sdk)
- [ Documents de référence du kit SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Documents de référence du Kit de développement logiciel (SDK) Live Share Media](/javascript/api/@microsoft/live-share-media/)
- [Applications Teams dans les réunions](teams-apps-in-meetings.md)
