---
title: Créer un bot
description: Décrit comment créer des robots dans Microsoft teams
keywords: création de robots teams
ms.date: 12/07/2018
ms.openlocfilehash: cb2d0974baf1d36a4acf077c219eb12449a5721a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673586"
---
# <a name="create-a-bot"></a>Créer un bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Tous les robots créés à l’aide de Microsoft bot Framework sont configurés et prêts à fonctionner dans Microsoft Teams.

Consultez la [documentation](/azure/bot-service/?view=azure-bot-service-3.0) de la structure de bot pour obtenir des informations générales sur les robots.

## <a name="create-a-bot-for-microsoft-teams"></a>Créer un bot pour Microsoft teams

*Teams App Studio* est un outil qui peut vous aider à créer votre robot, ainsi qu’un package d’application qui fait référence à votre bot. Il contient également une bibliothèque de contrôle REACT et des exemples configurables pour cartes. Consultez la rubrique [prise en main de Team App Studio](~/concepts/build-and-test/app-studio-overview.md). Les étapes qui suivent supposent que vous configuriez votre robot et que vous n’utilisiez pas *Team App Studio*.

1. Créez le bot à l’aide de https://dev.botframework.com/bots/newce lien :. **N’oubliez pas d’ajouter Microsoft teams en tant que canal à partir de la liste des chaînes proposées après avoir créé votre bot.** N’hésitez pas à réutiliser un ID d’application Microsoft que vous avez généré si vous avez déjà créé votre package d’application/manifeste.

   ![Page d’inscription de l’infrastructure bot](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Si vous ne souhaitez pas créer de robot dans Azure, vous **devez** utiliser ce lien pour créer un nouveau robot : https://dev.botframework.com/bots/new. Si vous cliquez sur le bouton *créer un bot* dans le portail de l’infrastructure bot à la place, vous allez [créer votre robot dans Microsoft Azure](#bots-and-microsoft-azure) .

2. Générez le bot en utilisant le package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) , le package NPM [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) , ou l' [API du connecteur bot](https://docs.microsoft.com/bot-framework/rest-api/bot-framework-rest-connector-api-reference).

3. Testez le bot à l’aide de l’émulateur de l' [infrastructure bot](https://docs.microsoft.com/bot-framework/debug-bots-emulator).

4. Déployez le robot sur un service Cloud, tel que [Microsoft Azure](https://azure.microsoft.com/). Vous pouvez également exécuter votre application localement et utiliser un service de tunneling tel [ngrok](https://ngrok.com) pour exposer un point de terminaison HTTPS://pour votre bot `https://45az0eb1.ngrok.io/api/messages`, tel que.

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Robots et Microsoft Azure
> Depuis décembre 2017, le portail de l’infrastructure bot est optimisé pour l’enregistrement des robots dans Microsoft Azure. Voici quelques éléments à savoir :
>
> * Le canal Microsoft teams pour les robots enregistrés sur Azure est gratuit. Les messages envoyés via le canal Teams ne seront pas pris en compte dans les messages consommés pour le bot.
> * Bien qu’il soit possible de [créer un nouveau](https://dev.botframework.com/bots/new) robot d’infrastructure bot sans utiliser Azure, vous devez utiliser cettehttps://dev.botframework.com/bots/new)URL (, qui n’est plus exposée dans le portail de l’infrastructure bot.
> * Lorsque vous modifiez les propriétés d’un bot existant dans la [liste de vos robots dans l’infrastructure de robot](https://dev.botframework.com/bots) , telle que son « point de terminaison de messagerie », qui est courante lors du premier développement d’un robot, en particulier si vous utilisez [ngrok](https://ngrok.com), vous verrez la colonne « État de la migration » et un bouton « déplacer » bleu qui vous permettra d’accéder au portail Microsoft Azure. Ne cliquez pas sur le bouton « migrer », sauf si c’est ce que vous voulez faire ; au lieu de cela, cliquez sur le nom du bot et vous pouvez modifier ses propriétés :</br>
   ![Modifier les propriétés du bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Si vous enregistrez votre bot à l’aide de Microsoft Azure, votre code de robot n’a pas besoin d’être *hébergé* sur Microsoft Azure.
> * Si vous enregistrez un bot à l’aide du portail Microsoft Azure, vous devez disposer d’un compte Microsoft Azure. Vous pouvez en [créer une gratuitement](https://azure.microsoft.com/free/). Pour vérifier votre identité lors de sa création, vous devez fournir une carte de crédit, mais elle ne sera pas facturée ; Il est toujours gratuit de créer et d’utiliser des robots avec Microsoft Teams.
> * Vous pouvez désormais utiliser app Studio pour enregistrer/mettre à jour des informations sur les applications et les robots directement dans Microsoft Teams. Il vous suffit d’utiliser le portail Microsoft Azure pour ajouter/configurer d’autres canaux de l’infrastructure de robots, tels que la ligne directe, la conversation Web, Skype et Facebook Messenger.
