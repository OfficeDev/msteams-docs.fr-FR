---
title: Ajouter des robots personnalisés à Microsoft teams avec des webhooks sortants
author: laujan
description: ''
keywords: onglet teams webhook sortant *
ms.topic: conceptual
ms.author: laujan
ms.openlocfilehash: 4570e597484494f05f4e18b4d29746da96c73661
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673728"
---
# <a name="add-custom-bots-to-microsoft-teams-with-outgoing-webhooks"></a>Ajouter des robots personnalisés à Microsoft teams avec des webhooks sortants

## <a name="what-are-outgoing-webhooks-in-teams"></a>Qu’est-ce qu’un webhooks sortants dans teams ?

Les webhooks sont un excellent moyen pour les équipes de s’intégrer aux applications externes. Un webhook est essentiellement une requête POST envoyée à une URL de rappel. Dans Teams, les webhooks sortants offrent un moyen simple pour permettre aux utilisateurs d’envoyer des messages à votre service Web sans avoir à passer par le processus complet de création de robots via [Microsoft bot Framework](https://dev.botframework.com/). Webhooks sortants publiez des données à partir de teams vers tout service choisi capable d’accepter une charge utile JSON. Une fois qu’un webhook sortant est ajouté à une équipe, il se comporte comme du robot, à l’écoute de canaux pour les messages utilisant une ** \@mention**, à l’envoi de notifications à des services Web externes et à la réponse avec des messages enrichis pouvant inclure des cartes et des images.

## <a name="outgoing-webhook-key-features"></a>Fonctionnalités clés de webhook sortantes

| Fonctionnalité | Description |
| ------- | ----------- |
| Configuration étendue| Les webhooks sont étendus au niveau de l’équipe. Vous devez passer par le processus de configuration pour chaque équipe à laquelle vous souhaitez ajouter votre webhook sortant. |
| Messagerie réactive| Les utilisateurs doivent utiliser @mention pour le webhook pour recevoir des messages. Actuellement, les utilisateurs peuvent uniquement envoyer un webhook sortant dans des canaux publics et non dans l’étendue personnelle ou privée. |
|Échange de messages HTTP standard|Les réponses apparaîtront dans la même chaîne que le message de requête d’origine et peuvent inclure tout contenu de message de la structure bot (texte enrichi, images, cartes et Emoji). **Remarque**: bien que les webhooks sortants puissent utiliser les cartes, ils ne peuvent pas `openURL`utiliser les actions de carte à l’exception de.|
| Prise en charge des méthodes de l’API teams|Dans Teams, les webhooks sortants envoient un billet HTTP à un service Web et traitent une réponse. Ils ne peuvent pas accéder à d’autres API, par exemple, récupérer la liste ou la liste des canaux d’une équipe.|

## <a name="adding-outgoing-webhook-processing-to-your-app"></a>Ajout du traitement webhook sortant à votre application

**Scénario**: notifications d’état de modification de transmission sur un serveur de base de données de canal teams vers votre application.  
**Exemple**: vous disposez d’une application métier qui effectue le suivi de toutes les opérations CRUD effectuées pour les enregistrements d’employés par les utilisateurs de Channels teams dans le client Office 365.

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. créer une URL sur le serveur de votre application pour accepter et traiter une requête POST avec une charge utile JSON

Votre service recevra les messages dans le schéma de messagerie du service Azure bot standard. Le connecteur de robot est un service RESTful qui permet à votre service de traiter l’échange de messages au format JSON via les protocoles HTTPs, comme indiqué dans l' [API du service Azure bot](/bot-framework/rest-api/bot-framework-rest-connector-api-reference). Vous pouvez également suivre le kit de développement logiciel (SDK) de Microsoft bot Framework pour traiter et analyser les messages. *Voir aussi*  [à propos du service de robots Azure](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0).

Les webhooks sortants sont inclus dans `team` le niveau et sont visibles par tous les membres de l’équipe. Tout comme un bot, les utilisateurs AE doivent ** \@mentionner** le nom du webhook sortant pour l’appeler dans le canal.

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. créer une méthode pour vérifier le jeton HMAC de webhook sortant

Pour vous assurer que votre service reçoit des appels uniquement à partir de clients teams réels, teams fournit un `hmac` code HMAC dans l’en-tête HTTP qui doit toujours être inclus dans votre protocole d’authentification.

Votre code doit toujours valider la signature HMAC incluse dans la demande :

* *Générez* le jeton HMAC à partir du corps de la demande du message. Il existe des bibliothèques standard pour effectuer cette opération sur la plupart des plateformes (*reportez-vous* à [crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node. js ou *voir* [Team webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) pour C\#). Microsoft teams utilise le chiffrement HMAC standard SHA256. Vous devrez convertir le corps en un tableau d’octets en UTF8.
* *Calculer* le hachage à partir du tableau d’octets du jeton de sécurité **fourni par teams** lorsque vous avez enregistré le webhook sortant dans le client teams]. *Voir* [créer un webhook sortant](#create-an-outgoing-webhook), ci-dessous.
* *Convertissez* le hachage en une chaîne à l’aide de l’encodage UTF-8.
* *Comparez* la valeur de chaîne du hachage généré à la valeur fournie dans la demande http.

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. créer une méthode pour envoyer une réponse de réussite ou d’échec

Les réponses de votre webhook sortant apparaîtront dans la même chaîne de réponse que le message d’origine. Lorsque l’utilisateur effectue une requête, Microsoft teams émet une demande HTTP synchrone à votre service et votre code disposera de 5 secondes pour répondre au message avant que la connexion expire et ne se termine.

### <a name="example-response"></a>Exemple de réponse

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>Créer un webhook sortant

1. Sélectionnez l’équipe appropriée et sélectionnez **gérer une équipe** dans le menu déroulant (&#8226;&#8226;&#8226;).
1. Sélectionnez l’onglet **applications** dans la barre de navigation.
1. Dans le coin inférieur droit de la fenêtre, sélectionnez **créer un webhook sortant**.
1. Dans la fenêtre contextuelle résultante, renseignez les champs obligatoires :

>* **Nom** : le titre du webhook et le @mention TAP.
>* **URL de rappel** : le point de terminaison HTTPS qui accepte les charges utiles JSON et reçoit les requêtes post de teams.
>* **Description** : une chaîne détaillée qui apparaîtra sur la carte de visite et le tableau de bord de l’application au niveau de l’équipe.
>* **Image de profil** (facultatif) icône de l’application pour votre webhook.
>* Sélectionnez le bouton **créer** dans le coin inférieur droit de la fenêtre contextuelle et le webhook sortant sera ajouté aux canaux de l’équipe active.
>* La fenêtre de boîte de dialogue suivante affiche un jeton de sécurité [HMAC (Hash-based Message Authentication Code)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) qui sera utilisé pour authentifier les appels entre teams et le service externe désigné.
>* Si l’URL est valide et si les jetons d’authentification du serveur et du client sont égaux (par exemple, une négociation HMAC), le webhook sortant sera disponible pour les utilisateurs de l’équipe.

## <a name="code-samples"></a>Exemples de code

Vous pouvez afficher les exemples de code webhook sortants sur GitHub :

### <a name="nodejs"></a>Node.js

[OfficeDev/msteams-Samples-sortante-webhook-NodeJS](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a>C\#

[OfficeDev/Microsoft-teams-Sample-sortante-webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
