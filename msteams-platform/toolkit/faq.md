---
title: FAQ
author: MuyangAmigo
description: Dans ce module, consultez faq sur Teams Toolkit à l’aide de Visual Studio Code
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 88a1fba1213dce01ed48fccbc72ca02757859033
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617099"
---
# <a name="faq-for-teams-toolkit-using-visual-studio-code"></a>FAQ sur Teams Toolkit à l’aide de Visual Studio Code

Vous pouvez voir le FAQ pour toutes les sections du Kit de ressources Teams pour Visual Studio Code.

FAQ sur [l’approvisionnement de ressources cloud à l’aide du Kit de ressources Teams](provision.md)

<br>

<details>

<summary><b>Procédure de dépannage ?</b></summary>

Si vous obtenez des erreurs avec Teams Shared Computer Toolkit dans Visual Studio Code, vous pouvez sélectionner **Obtenir de l’aide** dans la notification d’erreur pour accéder au document associé. Si vous utilisez l’interface CLI TeamsFx, un lien hypertexte à la fin du message d’erreur pointe vers la documentation d’aide. Vous pouvez également consulter directement la [documentation d’aide sur l’approvisionnement](https://aka.ms/teamsfx-arm-help) .

<br>

</details>

<details>

<summary><b>Comment puis-je basculer vers un autre abonnement Azure lors de l’approvisionnement ?</b></summary>

1. Basculez l’abonnement dans le compte actuel ou déconnectez-vous et sélectionnez un nouvel abonnement.
2. Si vous avez déjà approvisionné l’environnement actuel, vous devez créer un environnement et effectuer l’approvisionnement, car ARM ne prend pas en charge le déplacement des ressources.
3. Si vous n’avez pas approvisionné l’environnement actuel, vous pouvez déclencher l’approvisionnement directement.

<br>

</details>

<details>

<summary><b>Comment puis-je modifier le groupe de ressources lors de l’approvisionnement ?</b></summary>

Avant l’approvisionnement, l’outil vous demande si vous souhaitez créer un groupe de ressources ou en utiliser un existant. Vous pouvez fournir un nouveau nom de groupe de ressources ou en choisir un existant dans cette étape.

<br>

</details>

<details>

<summary><b>Comment puis-je provisionner une application basée sur Sharepoint ?</b></summary>

Vous pouvez suivre [l’approvisionnement SharePoint application basée sur](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4).

> [!NOTE]
> Actuellement, la création Teams application avec sharepoint framework avec Teams Shared Computer Toolkit n’a pas d’intégration directe avec Azure. Le contenu de la documentation ne s’applique pas aux applications basées sur SPFx.

<br>

</details>
