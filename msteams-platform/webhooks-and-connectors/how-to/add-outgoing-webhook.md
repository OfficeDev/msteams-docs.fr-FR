---
title: Ajoutez des bots personnalisés à Microsoft Teams avec des coins web sortants
description: décrit comment ajouter un webhook sortant
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: les équipes onglets sortant webhook message actionnable vérifier webhook
ms.openlocfilehash: a5a0cdfc9080ac4567f438b6fb6fd0671df8c19f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566529"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>Ajoutez des bots personnalisés à Teams avec des webhooks sortants

## <a name="outgoing-webhooks-in-teams"></a>Webhooks sortants dans Teams

Webhooks sont un moyen éminent pour les Teams’intégrer avec des applications externes. Un webhook est essentiellement une demande POST envoyée à une URL de rappel. Les webhooks sortants permettent aux utilisateurs d’envoyer des messages à votre service Web sans passer par le processus complet de création de bots via [Microsoft Bot Framework](https://dev.botframework.com/).

Le webhook sortant envoie des données Teams à n’importe quel service choisi capable d’accepter une charge utile JSON. Après avoir ajouté les webhooks sortants à une équipe, il agit comme un bot et recherche des messages dans les canaux en utilisant la **\@ mention**. Il envoie des notifications aux services Web externes et répond par des messages riches, qui incluent des cartes et des images.

## <a name="outgoing-webhook-key-features"></a>Fonctionnalités clés du webhook sortant

| Fonctionnalité | Description |
| ------- | ----------- |
| Configuration étendue| Les webhooks sont portées au niveau de l’équipe. Vous devez passer par le processus de configuration pour chaque équipe où vous souhaitez ajouter votre webhook sortant. |
| Messagerie réactive| Les utilisateurs doivent utiliser @mention pour que le webhook reçoive des messages. Actuellement, les utilisateurs ne peuvent envoyer un message qu’à un internaute sortant sur les chaînes publiques et non dans le cadre personnel ou privé. |
|Échange de messages HTTP standard|Les réponses apparaissent dans la même chaîne que le message de demande d’origine et peuvent inclure n’importe quel contenu de message-cadre bot, par exemple, texte riche, images, cartes et emojis. Bien que les internautes sortants puissent utiliser des cartes, ils ne peuvent pas utiliser d’actions de carte à l’exception de `openURL` .|
| Teams Prise en charge de la méthode API|Le webhook sortant envoie un MESSAGE HTTP à un service Web et traite une réponse. Ils ne peuvent accéder à aucune autre API comme récupérer la liste ou la liste des canaux d’une équipe.|

## <a name="creating-actionable-messages"></a>Créations des messages intégrant des actions

Les cartes de connecteur incluent trois boutons visibles sur la carte. Chaque bouton est défini dans la `potentialAction` propriété du message en utilisant des `ActionCard` actions. Chacun `ActionCard` contient un type d’entrée; un champ de texte, un cueilleur de date ou une liste multi-choix. Chaque `ActionCard` action a une action associée, par exemple, `HttpPOST` .

Les cartes de connecteur prennent en charge trois types d’actions :

| Opération | Description |
| ------- | ----------- |
| `ActionCard` |Présente un ou plusieurs types d’entrées et actions associées.|
| `HttpPOST` | Envoie une demande POST à une URL. |
| `OpenUri` |  Ouvre un URI dans un navigateur ou une application distinct, cible en option différentes URL basées sur des systèmes d’exploitation.|

L'action `ActionCard` prend en charge trois types d'entrée :

| Type d’entrée | Description |
| ------- | ----------- |
| `TextInput` | Un champ de texte à ligne unique ou multilienne avec une limite de longueur optionnelle. |
| `DateInput` | Un sélecteur de date avec sélecteur de temps optionnel. |
| `MultichoiceInput` | Une liste spécifique de choix, offrant soit une sélection unique ou plusieurs sélections.|

`MultichoiceInput` prend en `style` charge une propriété qui contrôle l’affichage d’une liste entièrement élargie. La valeur par défaut `style` dépend de la `isMultiSelect` valeur.

| `isMultiSelect` valeur  | `style` valeur par défaut  |
| --- | --- |
| `false` ou non spécifié | Le style par défaut est `compact`|
| `true` | Le style par défaut est `expanded` |

> [!NOTE]
> * Entrez `"isMultiSelect": true` à la fois `"style": true` et, si vous voulez que la liste multi-sélection s’affiche dans un style compact.
> * La `compact` sélection de la propriété dans Teams est la même que la sélection pour la propriété dans `style` Microsoft `normal` `style` Outlook.
> * Webhooks ne supporte que Office 365 cartes de retour de message et les cartes adaptatives.

Pour tous les autres détails sur les actions de la carte connecteur, **[voir Actions](/outlook/actionable-messages/card-reference#actions)** dans la référence actionnable de la carte de message.

## <a name="adding-outgoing-webhooks-to-your-app"></a>Ajout de webhooks sortants à votre application

**Scénario**: Poussez les notifications d’état de modification sur Teams serveur de base de données de canal à votre application.  
**Exemple**: Vous avez une application de secteur d’activité qui suit toutes les opérations CRUD effectuées aux dossiers des employés par les utilisateurs rh du canal Teams à travers une Office 365 location.

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. Créez une URL sur le serveur de votre application pour accepter et traiter une demande POST avec une charge utile JSON

Votre service reçoit des messages dans un schéma de messagerie de bot Azure standard. Le connecteur-cadre bot est un service RESTful qui permet à votre service de traiter l’échange de messages formatés JSON via les protocoles HTTPS tels que documentés dans [l’API Azure Bot Service](/bot-framework/rest-api/bot-framework-rest-connector-api-reference). Vous pouvez également suivre le [Microsoft Bot Framework SDK] pour traiter et analysé les messages. Voir aussi [sur Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).


Les webhooks sortants sont portées au niveau `team` et sont visibles par tous les membres de l’équipe. Tout comme un bot, les utilisateurs doivent mentionner **\@ le** nom du webhook sortant pour l’invoquer dans le canal.

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. Créer une méthode pour vérifier le jeton sortant de l’HMAC webhook

#### <a name="hmac-signature-for-testing-with-code-example"></a>Signature HMAC pour les tests avec exemple de code

En utilisant l’exemple du message entrant et id: « contoso » de SigningKeyDictionary de {"contoso », « vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA= » }.

Utilisez la valeur « HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U= » dans l’autorisation de l’en-tête de demande.

Pour vous assurer que votre service ne reçoit des appels que de clients Teams, Teams fournit un code HMAC dans l’en-tête `hmac` HTTP. Toujours inclus le code dans votre protocole d’authentification.

Votre code doit toujours valider la signature HMAC incluse dans la demande :

* Générer le jeton HMAC à partir du corps de demande du message. Il existe des bibliothèques standard pour ce faire sur la plupart des plates-formes [(voir Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) pour Node.js ou [voir Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C \# ). Microsoft Teams utilise la cryptographie SHA256 HMAC standard. Vous devez convertir le corps en un tableau d’au-être dans UTF8.
* Calculez le hachage à partir du tableau d’au-Teams **de sécurité fourni par Teams** lorsque vous avez enregistré le webhook sortant dans le Teams client]. Voir [Créer un webhook sortant](#create-an-outgoing-webhook).
* Convertir le hachage en chaîne à l’aide de l’encodage UTF-8.
* Comparez la valeur de chaîne du hachage généré avec la valeur fournie dans la demande HTTP.

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. Créer une méthode pour envoyer une réponse de succès ou d’échec

Les réponses de vos webhooks sortants apparaissent dans la même chaîne de réponses que le message original. Lorsque l’utilisateur effectue une requête, Microsoft Teams émet une demande HTTP synchrone à votre service et votre code obtient cinq secondes pour répondre au message avant que la connexion ne s’arrête et se termine.

### <a name="example-response"></a>Exemple de réponse

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>Créer un webhook sortant

1. Sélectionnez l’équipe appropriée et **choisissez l’équipe** Manage dans le menu de drop-down (&#8226;&#8226;&#8226;).
1. Choisissez **l’onglet Apps** à partir de la barre de navigation.
1. À partir du coin inférieur droit de la fenêtre **sélectionnez Créer un webhook sortant.**
1. Dans la fenêtre contextup résultante, remplissez les champs requis :

>* **Nom**: Le titre webhook et @mention robinet
>* **URL de rappel**: Le point final HTTPS qui accepte les charges utiles JSON et reçoit les demandes POST de Teams
>* **Description**: Chaîne détaillée qui apparaît dans la carte de profil et le tableau de bord de l’application au niveau de l’équipe
>* **Photo de profil**: Une icône d’application optionnelle pour votre webhook
>* Sélectionnez le bouton **Créer** à partir du coin inférieur droit de la fenêtre contexturée et le webhook sortant est ajouté aux canaux de l’équipe actuelle.
>* La fenêtre de dialogue suivante affiche [un jeton de sécurité HMAC (Code d’authentification des](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) messages basé sur le hachage) qui est utilisé pour authentifier les appels entre Teams et le service extérieur désigné.
>* Le webhook sortant est disponible pour les utilisateurs de l’équipe, seulement si l’URL est valide et que les jetons d’authentification du serveur et du client sont égaux par exemple, une poignée de main HMAC.

## <a name="code-sample"></a>Exemple de code
|**Nom de l’échantillon** | **Description** | **.NET (en)** | **Node.js** |
|----------------|------------------|--------|----------------|
| Webhooks sortants | Échantillons pour créer **des bots personnalisés** à utiliser dans Microsoft Teams.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

