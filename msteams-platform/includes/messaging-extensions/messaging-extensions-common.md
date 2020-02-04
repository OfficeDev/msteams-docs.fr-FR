## <a name="add-a-messaging-extension-to-your-app"></a>Ajouter une extension de messagerie à votre application

Une extension de messagerie est un service hébergé sur le Cloud qui écoute les demandes des utilisateurs et répond avec des données structurées, telles qu’une [carte](~/task-modules-and-cards/what-are-cards.md). Vous intégrez votre service à Microsoft teams via `Activity` les objets de l’infrastructure bot. Nos extensions .NET et node. js pour le kit de développement logiciel (SDK) du générateur de robots peuvent vous aider à ajouter la fonctionnalité d’extension de messagerie à votre application.

![Diagramme du flux de messages pour les extensions de messagerie](~/assets/images/compose-extensions/ceflow.png)

### <a name="register-in-the-bot-framework"></a>Inscription dans l’infrastructure de robot

Si vous ne l’avez pas déjà fait, vous devez tout d’abord inscrire un bot auprès de Microsoft bot Framework. L’ID de l’application Microsoft et les points de terminaison de rappel de votre robot, tels qu’ils sont définis, seront utilisés dans votre extension de messagerie pour recevoir et répondre aux demandes des utilisateurs. N’oubliez pas d’activer le canal Microsoft teams pour votre robot.

Enregistrer l’ID de votre application bot et le mot de passe de l’application, vous devez fournir l’ID de l’application dans le manifeste de votre application.

### <a name="update-your-app-manifest"></a>Mettre à jour le manifeste de votre application

Comme avec les robots et les onglets, vous mettez à jour le [manifeste](~/resources/schema/manifest-schema.md#composeextensions) de votre application pour inclure les propriétés d’extension de messagerie. Ces propriétés déterminent la façon dont votre extension de messagerie apparaît et se comporte dans le client Microsoft Teams. Les extensions de messagerie sont prises en charge à partir de la version 1.0 du manifeste.

#### <a name="declare-your-messaging-extension"></a>Déclarer votre extension de messagerie

Pour ajouter une extension de messagerie, incluez une nouvelle structure JSON de niveau supérieur dans votre manifeste `composeExtensions` avec la propriété. Actuellement, vous êtes limité à la création d’une extension de messagerie unique pour votre application.

> [!NOTE]
> Le manifeste fait référence aux extensions de `composeExtensions`messagerie en tant que. Cela permet de conserver une compatibilité descendante.

La définition d’extension est un objet de la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? |
|---|---|---|
| `botId` | ID d’application Microsoft unique pour le bot enregistré avec l’infrastructure bot. Il doit en principe être identique à l’ID de votre application globale de teams. | Oui |
| `scopes` | Tableau déclarant si cette extension peut être ajoutée à `personal` ou `team` des étendues (ou les deux). | Oui |
| `canUpdateConfiguration` | Active l’élément de menu **paramètres** . | Non |
| `commands` | Tableau de commandes pris en charge par cette extension de messagerie. Vous êtes limité à 10 commandes. | Oui |

#### <a name="define-commands"></a>Définir des commandes

Votre extension de messagerie doit déclarer une commande, qui apparaît lorsque l’utilisateur sélectionne votre application dans le bouton **autres options** (**&#8943;**) de la zone de composition.

![Capture d’écran de la liste des extensions de messagerie dans teams](~/assets/images/compose-extensions/compose-extension-list.png)

Dans le manifeste de l’application, votre élément de commande est un objet de la structure suivante :

| Nom de la propriété | Objectif | Obligatoire ? | Version de manifeste minimale |
|---|---|---|---|
| `id` | ID unique que vous affectez à cette commande. La demande de l’utilisateur contiendra cet ID. | Oui | 1.0 |
| `title` | Nom de la commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `description` | Texte d’aide indiquant la signification de cette commande. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `type` | Définir le type de commande. Les valeurs possibles sont `query` et `action`. Si elle n’est pas présente, la valeur par défaut est définie sur`query` | Non | 1.4 |
| `initialRun` | Paramètre facultatif, utilisé avec `query` les commandes. Si la valeur est définie sur **true**, cette commande doit être exécutée dès que l’utilisateur choisit cette commande dans l’interface utilisateur. | Non | 1.0 |
| `fetchTask` | Paramètre facultatif, utilisé avec `action` les commandes. Affectez à cet argument la valeur **true** pour extraire la carte adaptative ou l’URL Web à afficher dans le [module de tâches](~/task-modules-and-cards/what-are-task-modules.md). Elle est utilisée lorsque les entrées de la `action` commande sont dynamiques par opposition à un ensemble statique de paramètres. Notez que si la liste de paramètres statiques de la commande est définie sur **true** , elle est ignorée. | Non | 1.4 |
| `parameters` | Liste statique des paramètres de la commande. | Oui | 1.0 |
| `parameter.name` | Le nom du paramètre. Cette adresse est envoyée à votre service dans la demande de l’utilisateur. | Oui | 1.0 |
| `parameter.description` | Décrit ce paramètre ou un exemple de la valeur qui doit être fournie. Cette valeur apparaît dans l’interface utilisateur. | Oui | 1.0 |
| `parameter.title` | Titre de paramètre court convivial ou étiquette. | Oui | 1.0 |
| `parameter.inputType` | Défini sur le type d’entrée requis. Les valeurs possibles `text`sont `textarea`, `number`, `date`, `time`, `toggle`et. La valeur par défaut est définie sur`text` | Non | 1.4 |
| `context` | Tableau facultatif de valeurs qui définit le contexte dans lequel l’action de message est disponible. Les valeurs possibles `message`sont `compose`, ou `commandBox`. La valeur par défaut est `["compose", "commandBox"]`. | Non | 1,5 |
