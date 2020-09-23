---
title: Conception de cartes efficaces
description: Décrit les instructions de conception pour la création de cartes
keywords: instructions de conception teams fiches d’infrastructure de référence (cartes simplifiées)
ms.openlocfilehash: 4ec410820e0288d99dacb6944a8096f4f61b9d34
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209836"
---
# <a name="design-effective-cards"></a>Conception de cartes efficaces

Les cartes sont des extraits de code actionnables, que vous pouvez ajouter à une conversation via un bot, un connecteur ou une application. En utilisant du texte, des graphiques et des boutons, les cartes vous permettent de communiquer avec une audience.

Notre infrastructure de cartes élimine le fardeau de concevoir une expérience utilisateur entièrement fonctionnelle. Nous avons développé plusieurs types de cartes standard et chacun d’eux s’adapte à nos plateformes prises en charge. Cela signifie que la disposition est entièrement prise en charge, et vous n’avez pas besoin de développer des itérations de carte différentes sur les plateformes. Au lieu de cela, vous pouvez vous concentrer sur la numérotation dans votre contenu.

---

## <a name="guidelines"></a>Conseils

Considérez une carte comme une réponse à une question d’utilisateur ou à un paramètre. Une carte peut répondre à une question directe (par exemple, le nombre de bogues ouverts) ou à une condition (par exemple, « envoyer une liste de mes bogues ouverts à 9 am tous les jours »).

> [!TIP]
> En utilisant l’un de nos types de cartes standard, vous savez déjà que toutes vos réponses s’afficheront correctement sur chaque plateforme prise en charge.

Une carte peut inclure n’importe lequel des éléments suivants :<br />

[!include[Card anatomy](~/includes/design/card-image-anatomy.html)]

1. **Texte**de l’enveloppe : idéal pour les messages de conversation. Par exemple, si vous souhaitez qu’un bot indique : « Voici ce que j’ai trouvé ! » ou « heure de votre résumé d’informations 1:00 », ce message est mieux affiché dans le texte de l’enveloppe.

   Le texte d’enveloppe est un excellent moyen d’injecter un peu de personnalité dans votre service, n’oubliez pas de le conserver relativement rapidement.

2. **Titre**: votre titre sera toujours le plus grand texte de votre carte. Il sert également de « raccordement », donc essayez de conserver le titre Short, mémorable et facile à analyser.

3. **Sous-titre**: idéal pour les attributions, les slogans ou comme directive secondaire. Ce composant apparaît juste en dessous de votre titre.

4. **Image**: les images s’ajustent à leur conteneur. Les cartes héros ont une largeur maximale de 420px, les miniatures ont une largeur maximale de 100px et les affichages de liste uniquement pour des en mode Bureau.

5. **Text**: idéal pour le texte brut dans le corps de votre carte. Votre longueur maximale dépend du type de carte que vous avez sélectionné.

6. **Buttons**: idéal pour ouvrir des pages Web, des onglets ou du contenu de conversation supplémentaire. Veillez à laisser le texte du bouton court et jusqu’au point.

   Vous pouvez inclure jusqu’à 6 boutons par carte, mais nous vous recommandons de suivre une philosophie « moins de plus » ici.

7. **Appuyez sur région**: il s’agit de la région cliquable de votre carte. La plupart des utilisateurs veulent cliquer sur les images automatiquement, essayez de concevoir votre texte afin qu’ils sachent où ils doivent appuyer ou cliquer.

> [!TIP]
> Il n’est pas nécessaire d’inclure chaque élément dans chaque carte que vous créez. Laissez votre contenu dicter vos éléments.

---

## <a name="types-of-cards"></a>Types de cartes

### <a name="hero"></a>Hero

Notre plus grande carte. Idéal pour les articles, les descriptions longues ou les scénarios dans lesquels votre image indique la plus grande partie de l’histoire.

[!include[Card anatomy](~/includes/design/card-image-hero.html)]

### <a name="thumbnail"></a>Thumbnail

Short et doux. Ces cartes sont idéales pour des réponses courtes ou si vous souhaitez renvoyer plusieurs cartes en même temps afin que l’utilisateur puisse choisir parmi plusieurs options. Nous pensons qu’il s’agit d’un excellent moyen de créer un lien profond vers un autre onglet ou un service Web.

[!include[Card anatomy](~/includes/design/card-image-thumbnail.html)]

### <a name="sign-in"></a>Connexion

Certains services exigent que les utilisateurs se connectent indépendamment de notre authentification. Dans ce cas, vous devez présenter une carte de connexion avant que l’utilisateur ne puisse se connecter à votre service.

[!include[Card anatomy](~/includes/design/card-image-signin.html)]

> [!TIP]
> Limitez les occurrences d’une carte de connexion supplémentaire, car elles constituent une forte vitesse de ralentissement pour les nouveaux utilisateurs.

---

## <a name="card-collections"></a>Collections de cartes

Nous disposons également de types de cartes standard qui conviennent mieux lorsque vous souhaitez présenter plusieurs éléments de contenu en une seule fois ou en succession rapide. À cet effet, nous disposons d’un carrousel, d’un résumé, d’une liste et de ce que nous appelons « fusion de bulles ».

### <a name="carousel"></a>Carrousel

Idéal pour les articles, les achats et la navigation à l’aide de cartes.

[!include[Card anatomy](~/includes/design/card-image-carousel.html)]

> [!TIP]
> Le Carrousel sera la hauteur maximale de votre carte principale. Nous vous recommandons d’utiliser le même type de carte et les mêmes champs de contenu dans.

### <a name="digest"></a>Digest

Idéal pour les actualités, les résumés et chaque fois que vous souhaitez que l’utilisateur affiche plusieurs cartes à la fois. Nous vous recommandons d’utiliser des cartes miniatures pour les résumés.

[!include[Card anatomy](~/includes/design/card-image-digest.html)]

### <a name="lists"></a>Listes

Les listes sont un excellent moyen de présenter un ensemble d’objets balayables dans un scénario de sélection. Les listes sont recommandées pour les éléments qui n’ont pas besoin d’une grande quantité d’explications.

[!include[Card anatomy](~/includes/design/card-image-list.html)]

### <a name="bubble-merge"></a>Fusion de bulles

Certains effets intéressants peuvent être atteints en envoyant rapidement un héros et plusieurs miniatures. Nous vous recommandons d’utiliser cette approche lorsque vous souhaitez traiter un résultat principal, mais seulement quelques éléments connexes.

[!include[Card anatomy](~/includes/design/card-image-bubble-merge.html)]

---

## <a name="best-practices"></a>Meilleures pratiques

### <a name="keep-the-noise-down"></a>Maintenir le bruit inactif

Il est facile d’envoyer plusieurs cartes dans une conversation, mais une fois que les cartes sortent de l’affichage, elles deviennent moins utiles. Essayez de vous limiter aux notions fondamentales. Cela est particulièrement vrai dans un canal où les utilisateurs ont moins de tolérance pour ce qu’ils perçoivent comme « bruit ».

### <a name="test-on-mobile"></a>Test sur mobile

Les environnements mobiles sont limités en espace et en bande passante, donc soyez vigilant lorsque vous incluez des images surdimensionnées et des ensembles de données volumineux dans des listes et des carrousels. En outre, les largeurs de titre et les longueurs de texte seront tronquées sur mobile, ce qui est une autre chose de garder un oeil.

### <a name="check-your-graphics"></a>Vérifier vos graphismes

Les graphiques sont redimensionnés, donc veillez à les afficher sur toutes les plateformes.

### <a name="avoid-including-text-in-a-graphic"></a>Éviter d’inclure du texte dans un graphisme

Tout ce qui doit être lu par un utilisateur doit être inclus dans un champ de texte. Une fois qu’une image est redimensionnée dynamiquement, le texte que vous ajoutez à un graphique peut devenir inintelligible.

### <a name="use-mentions-if-you-want-the-attention-of-specific-users"></a>Utiliser des mentions pour attirer l’attention des utilisateurs spécifiques

> [!NOTE]
> Mentionner la prise en charge des cartes est actuellement prise en charge en version préliminaire pour les [développeurs](~/resources/dev-preview/developer-preview-intro.md) .

Les mentions sont un excellent moyen d’avertir des utilisateurs spécifiques dans une conversation d’équipe ou de groupe. Vous pouvez inclure une mention dans la carte dans des scénarios, comme une tâche qui est affectée à un utilisateur ou la fourniture d’un Félicitations à un coéquipier. Découvrez comment inclure des mentions dans les cartes dans la [page de mise en forme](~/task-modules-and-cards/cards/cards-format.md)de la carte. 
