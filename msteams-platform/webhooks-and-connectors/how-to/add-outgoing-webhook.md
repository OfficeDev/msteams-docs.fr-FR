---
title: Ajouter des bots personnalisés à Microsoft Teams avec des webhooks sortants
description: explique comment ajouter un webhook sortant
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: 'onglets teams : message actionnable de webhook sortant vérifiant le webhook'
ms.openlocfilehash: a5a0cdfc9080ac4567f438b6fb6fd0671df8c19f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566529"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>Ajouter des bots personnalisés à Teams avec des webhooks sortants

## <a name="outgoing-webhooks-in-teams"></a>Webhooks sortants dans Teams

Les webhooks sont un moyen Teams pour s’intégrer à des applications externes. Un webhook est essentiellement une requête POST envoyée à une URL de rappel. Les webhooks sortants permettent aux utilisateurs d’envoyer des messages à votre service web sans passer par le processus complet de création de bots via le [Microsoft Bot Framework](https://dev.botframework.com/).

Le webhook sortant envoie des données de Teams service choisi capable d’accepter une charge utile JSON. Après avoir ajouté les webhooks sortants à une équipe, il agit comme un bot et recherche des messages dans les canaux à l’aide de **\@ la mention**. Il envoie des notifications aux services web externes et répond par des messages enrichis, qui incluent des cartes et des images.

## <a name="outgoing-webhook-key-features"></a>Fonctionnalités de clé de webhook sortant

| Fonctionnalité | Description |
| ------- | ----------- |
| Configuration limitée| Les webhooks sont limitées au niveau de l’équipe. Vous devez passer par le processus de configuration de chaque équipe dans laquelle vous souhaitez ajouter votre webhook sortant. |
| Messagerie réactive| Les utilisateurs doivent utiliser @mention pour que le webhook reçoit des messages. Actuellement, les utilisateurs peuvent uniquement envoyer des messages à un webhook sortant dans les canaux publics et non dans l’étendue personnelle ou privée. |
|Échange de messages HTTP standard|Les réponses apparaissent dans la même chaîne que le message de demande d’origine et peuvent inclure n’importe quel contenu de message d’infrastructure de bot, par exemple du texte enrichi, des images, des cartes et des emojis. Bien que les webhooks sortants peuvent utiliser des cartes, ils ne peuvent pas utiliser d’actions de carte à l’exception de `openURL` .|
| Teams Prise en charge des méthodes d’API|Le webhook sortant envoie une demande HTTP POST à un service web et renvoie une réponse. Ils ne peuvent pas accéder à d’autres API telles que la récupération de la liste de la liste ou de la liste des canaux d’une équipe.|

## <a name="creating-actionable-messages"></a>Créations des messages intégrant des actions

Les cartes de connecteur incluent trois boutons visibles sur la carte. Chaque bouton est défini dans la propriété du message à `potentialAction` l’aide `ActionCard` d’actions. Chacune `ActionCard` contient un type d’entrée, un champ de texte, un s picker de date ou une liste à choix multiples. Chaque `ActionCard` action est associée à une action, par exemple. `HttpPOST`

Les cartes de connecteur prennent en charge trois types d’actions :

| Opération | Description |
| ------- | ----------- |
| `ActionCard` |Présente un ou plusieurs types d’entrée et actions associées.|
| `HttpPOST` | Envoie une demande POST à une URL. |
| `OpenUri` |  Ouvre un URI dans un navigateur ou une application distinct, cible éventuellement différentes URI en fonction des systèmes d’exploitation.|

L'action `ActionCard` prend en charge trois types d'entrée :

| Type d’entrée | Description |
| ------- | ----------- |
| `TextInput` | Champ de texte à ligne unique ou multiligne avec une limite de longueur facultative. |
| `DateInput` | Sélecteur de dates avec un sélecteur d’heure facultatif. |
| `MultichoiceInput` | Liste de choix spécifiée, offrant soit une sélection unique, soit plusieurs sélections.|

`MultichoiceInput` prend en `style` charge une propriété qui contrôle l’affichage d’une liste entièrement étendue. La valeur par défaut `style` dépend de la `isMultiSelect` valeur.

| `isMultiSelect` value  | `style` valeur par défaut  |
| --- | --- |
| `false` ou non spécifié | Le style par défaut est `compact`|
| `true` | Le style par défaut est `expanded` |

> [!NOTE]
> * Entrez les `"isMultiSelect": true` deux et, si vous souhaitez que la liste à sélections multiples soit affichée `"style": true` dans un style compact.
> * La sélection de la propriété dans Teams est la même que la sélection de la propriété `compact` `style` dans Microsoft `normal` `style` Outlook.
> * Les webhooks ne peuvent Office 365 les cartes de retour de message et les cartes adaptatives.

Pour plus d’informations sur les actions de carte de connecteur, voir **[Actions](/outlook/actionable-messages/card-reference#actions)** dans la référence de carte de message actionnable.

## <a name="adding-outgoing-webhooks-to-your-app"></a>Ajout de webhooks sortants à votre application

**Scénario**: envoyer des notifications d’état de modification sur Teams de base de données de canal vers votre application.  
**Exemple**: vous avez une application métier qui suit toutes les opérations CRUD réalisées sur les enregistrements des employés par Teams utilisateurs RH de canal au sein d’Office 365 clients.

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. Créez une URL sur le serveur de votre application pour accepter et traiter une demande POST avec une charge utile JSON

Votre service reçoit des messages dans un schéma de messagerie de service de bot Azure standard. Le connecteur d’infrastructure du bot est un service RESTful qui permet à votre service de traiter l’échange de messages au format JSON via des protocoles HTTPS, comme documenté dans [l’API Azure Bot Service.](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) Vous pouvez également suivre le [Microsoft Bot Framework SDK] pour traiter et passer des messages. Voir aussi [à propos d’Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).


Les webhooks sortants sont limitées au niveau et `team` sont visibles par tous les membres de l’équipe. Tout comme un bot, les utilisateurs doivent **\@ mentionner** le nom du webhook sortant pour l’appeler dans le canal.

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. Créer une méthode pour vérifier le jeton HMAC du webhook sortant

#### <a name="hmac-signature-for-testing-with-code-example"></a>Exemple de signature HMAC à tester avec du code

Utilisation d’un exemple de message entrant et d’ID : « contoso » de SigningKeyDictionary de {"contoso », « vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA= » }.

Utilisez la valeur « HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U= » dans l’autorisation de l’en-tête de demande.

Pour vous assurer que votre service ne reçoit des appels que de clients Teams réels, Teams fournit un code HMAC dans l’en-tête `hmac` HTTP. Toujours inclus le code dans votre protocole d’authentification.

Votre code doit toujours valider la signature HMAC incluse dans la demande :

* Générer le jeton HMAC à partir du corps de la demande du message. Il existe des bibliothèques standard pour le faire sur la plupart des plateformes (voir [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or see [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C \# ). Microsoft Teams utilise le chiffrement HMAC SHA256 standard. Vous devez convertir le corps en tableau d’byte en UTF8.
* Calculez le hachage à partir du  tableau d’Teams du jeton de sécurité lorsque vous avez inscrit le webhook sortant dans le client Teams]. Voir [Créer un webhook sortant.](#create-an-outgoing-webhook)
* Convertissez le hachage en chaîne à l’aide du codage UTF-8.
* Comparez la valeur de chaîne du hachage généré à la valeur fournie dans la requête HTTP.

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. Créer une méthode pour envoyer une réponse de réussite ou d’échec

Les réponses de vos webhooks sortants apparaissent dans la même chaîne de réponse que le message d’origine. Lorsque l’utilisateur effectue une requête, Microsoft Teams envoie une demande HTTP synchrone à votre service et votre code obtient cinq secondes pour répondre au message avant que la connexion n’arrive à terme et ne se termine.

### <a name="example-response"></a>Exemple de réponse

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>Créer un webhook sortant

1. Sélectionnez l’équipe appropriée et choisissez **Gérer** l’équipe dans le menu déroulant (&#8226;&#8226;&#8226;).
1. Choisissez **l’onglet Applications** dans la barre de navigation.
1. Dans le coin inférieur droit de la fenêtre, **sélectionnez Créer un webhook sortant.**
1. Dans la fenêtre popup qui en résulte, remplissez les champs requis :

>* **Nom**: titre du webhook et @mention’appuyer
>* **URL de rappel**: point de terminaison HTTPS qui accepte les charges utiles JSON et reçoit les demandes POST de Teams
>* **Description**: chaîne détaillée qui apparaît dans la carte de visite et le tableau de bord de l’application au niveau de l’équipe
>* **Image de profil**: icône d’application facultative pour votre webhook
>* Sélectionnez **le bouton** Créer dans le coin inférieur droit de la fenêtre pop-up et le webhook sortant est ajouté aux canaux de l’équipe actuelle.
>* La fenêtre de boîte de dialogue suivante affiche un jeton de sécurité [HMAC (Message Authentication Code)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) basé sur le hachage utilisé pour authentifier les appels entre Teams et le service externe désigné.
>* Le webhook sortant est disponible pour les utilisateurs de l’équipe, uniquement si l’URL est valide et que les jetons d’authentification du serveur et du client sont égaux, par exemple, une négociation HMAC.

## <a name="code-sample"></a>Exemple de code
|**Exemple de nom** | **Description** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| Webhooks sortants | Exemples de création **de bots personnalisés** à utiliser dans Microsoft Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

