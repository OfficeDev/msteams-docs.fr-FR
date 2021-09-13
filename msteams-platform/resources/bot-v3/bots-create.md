---
title: Créer un bot
description: Décrit comment créer des bots dans Microsoft Teams
ms.topic: how-to
keywords: création de bots teams
ms.localizationpriority: medium
ms.date: 12/07/2018
ms.openlocfilehash: d258f9e6713e6bb3d68aa19ef8a3b36d44dd3a07
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155870"
---
# <a name="create-a-bot"></a>Créer un bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Tous les bots créés à l Microsoft Bot Framework sont configurés et prêts à fonctionner dans Microsoft Teams.

Pour plus d’informations, voir [la documentation bot Framework pour](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) obtenir des informations générales sur les bots.

## <a name="create-a-bot-for-microsoft-teams"></a>Créer un bot dans Microsoft Teams

**Teams App Studio** est un outil qui peut vous aider à créer votre bot et un package d’application qui fait référence à votre bot. Elle contient également une bibliothèque de contrôle React et des exemples configurables pour les cartes. Pour plus d’informations, voir [Mise en Teams App Studio.](~/concepts/build-and-test/app-studio-overview.md) Les étapes qui suivent supposent que vous configurez manuellement votre bot et que vous n’utilisez **pas Teams App Studio**:

1. Créez le bot à l’aide de ce lien : https://dev.botframework.com/bots/new . **Veillez à ajouter Microsoft Teams sous la forme d’un canal à partir de la liste de chaînes proposées après avoir créé votre bot.** N’hésitez pas à réutiliser tout ID d’application Microsoft que vous avez généré si vous avez déjà créé votre package d’application/manifeste.

   ![Page d’inscription de Bot Framework](~/assets/images/bots/bfregister.png)

> [!NOTE]
> Si vous ne souhaitez pas créer  votre bot dans Azure, vous devez utiliser ce lien pour créer un bot https://dev.botframework.com/bots/new : Si vous cliquez sur Créer un **bot** dans le portail Bot Framework à la place, vous créerez votre bot dans [Microsoft Azure](#bots-and-microsoft-azure) à la place.

2. Créez le bot à l’aide du package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet, du [SDK Bot Framework](https://github.com/microsoft/botframework-sdk)ou de l’API [Bot Connector.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)

3. Testez le bot à [l’aide Bot Framework Emulator](/bot-framework/debug-bots-emulator).

4. Déployez le bot sur un service cloud, tel que [Microsoft Azure](https://azure.microsoft.com/). Vous pouvez également exécuter votre application localement et utiliser un service de tunneling tel [que ngrok](https://ngrok.com) pour exposer un point de terminaison https:// de votre bot, tel que `https://45az0eb1.ngrok.io/api/messages` .

> [!NOTE]
> ## <a name="bots-and-microsoft-azure"></a>Bots et Microsoft Azure
> Depuis décembre 2017, le portail Bot Framework est optimisé pour l’inscription des bots dans Microsoft Azure. Voici quelques opérations que vous pouvez prendre en compte :
>
> * Le canal Microsoft Teams pour les bots inscrits sur Azure est gratuit. Les messages envoyés par le Teams ne sont pas comptabilisés dans les messages consommés pour le bot.
> * Bien qu’il soit possible de créer un [bot Bot Framework](https://dev.botframework.com/bots/new) sans utiliser Azure, vous devez utiliser cette URL ( qui n’est plus exposée dans le portail Bot https://dev.botframework.com/bots/new) Framework.
> * Lorsque vous modifiez les propriétés d’un bot existant dans la liste de vos bots dans [Bot Framework,](https://dev.botframework.com/bots) par exemple son « point de terminaison de messagerie », ce qui est courant lors du premier développement d’un bot, en particulier si vous utilisez [ngrok,](https://ngrok.com)vous verrez la colonne « État de la migration » et un bouton bleu « Migrer » qui vous permettra d’entrer dans le portail Microsoft Azure. Ne cliquez pas sur le bouton « Migrer », sauf si c’est ce que vous voulez faire . Au lieu de cela, cliquez sur le nom du bot et vous pouvez modifier ses propriétés :</br>
   ![Modifier les propriétés du bot](~/assets/images/bots/bf-migrate-bot-to-azure.png)
> * Si vous inscrivez votre bot à l’Microsoft Azure, votre code de bot n’a pas besoin d’être *hébergé* sur Microsoft Azure.
> * Si vous inscrivez un bot à l’aide du Portail Microsoft Azure, vous devez disposer d’un compte Microsoft Azure. Vous pouvez [en créer un gratuitement](https://azure.microsoft.com/free/). Pour vérifier votre identité lorsque vous en créez une, vous devez fournir une carte de crédit, mais elle ne sera pas facturée . Il est toujours gratuit de créer et d’utiliser des bots avec Microsoft Teams.
> * Vous pouvez désormais utiliser App Studio pour enregistrer/mettre à jour des informations d’application et de bot directement dans Microsoft Teams. Vous devez uniquement utiliser le portail Microsoft Azure pour ajouter ou configurer d’autres canaux Bot Framework tels que Direct Line, Web Chat, Skype et Facebook Messenger.

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)