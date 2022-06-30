---
title: Créer une clé secrète client
description: Décrit la création d’une clé secrète client
ms.topic: how-to
ms.localizationpriority: medium
keywords: onglets d’authentification teams Microsoft Azure Active Directory (Azure AD) API Graph
ms.openlocfilehash: 77d1c4e43c9bdfb9d2cb9e3e97ee3a26b8b0fa01
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558848"
---
# <a name="create-client-secret"></a>Créer une clé secrète client

Une clé secrète client est une chaîne que l’application utilise pour prouver son identité lors de la demande d’un jeton.

1. Sélectionnez **Gérer** > **les certificats & secrets**.

2. Sélectionnez **+ Nouvelle clé secrète client**.

    :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="Page de clé secrète client":::

   La page **Ajouter une clé secrète client** s’affiche.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-secret.png" alt-text="Ajouter une page de clé secrète client":::

3. Entrez la description.
4. Sélectionnez la durée de validité du secret.
5. Sélectionnez **Ajouter**.

   Un message s’affiche sur le navigateur indiquant que la clé secrète client a été mise à jour, et la clé secrète client s’affiche sur la page.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-secret-added.png" alt-text="Clé secrète client ajoutée":::

6. Sélectionnez le bouton Copier en regard de la **valeur** de la clé secrète client.
7. Enregistrez la valeur que vous avez copiée pour une utilisation ultérieure.

   > [!NOTE]
   > Veillez à copier la valeur de la clé secrète client juste après sa création. La valeur n’est visible qu’au moment de la création de la clé secrète client et ne peut pas être affichée après cela.
