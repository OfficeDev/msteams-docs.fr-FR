## <a name="add-a-messaging-extension-to-your-app"></a>Ajouter une extension de messagerie à votre application

Une extension de messagerie est un service hébergé dans le cloud qui écoute les demandes des utilisateurs et répond avec des données structurées, telles qu’une [carte.](~/task-modules-and-cards/what-are-cards.md) Vous intégrez votre service Microsoft Teams via des objets Bot `Activity` Framework. Nos extensions .NET et Node.js pour le Bot Builder SDK peuvent vous aider à ajouter des fonctionnalités d’extension de messagerie à votre application.

![Diagramme du flux de messages pour les extensions de messagerie](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>Inscrivez-vous dans le cadre bot

Si vous ne l’avez pas déjà fait, vous devez d’abord enregistrer un bot auprès de la Microsoft Bot Framework. L’id de l’application Microsoft et les paramètres de rappel de votre bot, tels qu’ils y sont définis, seront utilisés dans votre extension de messagerie pour recevoir et répondre aux demandes des utilisateurs. N’oubliez pas d’activer Microsoft Teams canal de recherche pour votre bot.

Enregistrez votre identifiant d’application bot et mot de passe d’application, vous devrez fournir l’iD de l’application dans votre manifeste d’application.

### <a name="update-your-app-manifest"></a>Mettez à jour le manifeste de votre application

Comme pour les bots et les onglets, vous mettez à jour le [manifeste de](~/resources/schema/manifest-schema.md#composeextensions) votre application pour inclure les propriétés d’extension de messagerie. Ces propriétés régissent la façon dont votre extension de messagerie apparaît et se comporte dans Microsoft Teams client. Les extensions de messagerie sont prises en charge en commençant par v1.0 du manifeste.

#### <a name="declare-your-messaging-extension"></a>Déclarez votre extension de messagerie

Pour ajouter une extension de messagerie, incluez une nouvelle structure JSON de haut niveau dans votre manifeste avec la `composeExtensions` propriété. Actuellement, vous vous limitez à créer une extension de messagerie unique pour votre application.

> [!NOTE]
> Le manifeste se réfère à des extensions de messagerie comme `composeExtensions` . Il s’agit de maintenir la compatibilité vers l’arrière.

La définition d’extension est un objet qui a la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? |
|---|---|---|
| `botId` | ID d’application Microsoft unique pour le bot inscrit dans le Bot Framework. Cela devrait généralement être le même que l’ID pour votre application Teams globale. | Oui |
| `scopes` | Tableau déclarant si cette extension peut être ajoutée ou `personal` `team` étendues (ou les deux). | Oui |
| `canUpdateConfiguration` | Permet **Paramètres élément** de menu. | Non |
| `commands` | Tableau de commandes que prend en charge cette extension de messagerie. Vous êtes limité à 10 commandes. | Oui |

#### <a name="define-commands"></a>Définir les commandes

Votre extension de messagerie doit déclarer une commande, qui apparaît lorsque l’utilisateur sélectionne votre application à partir **du bouton Plus d’options** **(&#8943;)** dans la boîte de composition.

![Capture d’écran de la liste des extensions de messagerie dans Teams](~/assets/images/compose-extensions/compose-extension-list.png)

Dans le manifeste de l’application, votre élément de commande est un objet avec la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? | Version manifeste minimale |
|---|---|---|---|
| `id` | ID unique que vous attribuez à cette commande. La demande de l’utilisateur inclura cet ID. | Oui | 1.0 |
| `title` | Nom de commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `description` | Aide texte indiquant ce que cette commande fait. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Définissez le type de commande. Les valeurs possibles sont `query` et `action`. Si elle n’est pas présente, la valeur par défaut est définie sur `query` . | Non | 1.4 |
| `initialRun` | Paramètre optionnel, utilisé avec `query` des commandes. Si elle est **définie pour** vrai , indique que cette commande doit être exécutée dès que l’utilisateur choisit cette commande dans l’interface utilisateur. | Non | 1.0 |
| `fetchTask` | Paramètre optionnel, utilisé avec `action` des commandes. Réglez à **vrai** pour aller chercher la carte adaptative ou url Web à afficher dans le [module de tâche](~/task-modules-and-cards/what-are-task-modules.md). Ceci est utilisé lorsque les entrées de la `action` commande sont dynamiques par opposition à un ensemble statique de paramètres. Notez que le s’il est défini **pour vrai** la liste de paramètres statiques pour la commande est ignorée. | Non | 1.4 |
| `parameters` | Liste statique des paramètres de la commande. | Oui | 1.0 |
| `parameter.name` | Le nom du paramètre. Ceci est envoyé à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Décrit les objectifs de ce paramètre ou l’exemple de la valeur qui devrait être fournie. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Titre ou étiquette de paramètre s’il vous est convivial. | Oui | 1.0 |
| `parameter.inputType` | Définissez le type d’entrée requis. Les valeurs possibles `text` incluent , , , , , `textarea` `number` `date` `time` `toggle` . Par défaut est défini sur `text` . | Non | 1.4 |
| `context` | Tableau facultatif de valeurs qui définit le contexte dans lequel l’action du message est disponible. Les valeurs possibles `message` sont `compose` , ou `commandBox` . La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |
