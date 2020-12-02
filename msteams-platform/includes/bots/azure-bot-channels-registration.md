1. Dans le [Portail Microsoft Azure](https://ms.portal.azure.com/#home), sous Services Azure, sélectionnez **Créer une ressource**.
1. Entrez « bot » dans la zone de recherche. Ensuite, dans la liste déroulante, sélectionnez **Inscription de chaînes de bot**.
1. Sélectionnez le bouton **Créer**.
1. Dans le panneau **Inscription de chaînes de bot**, fournissez les informations demandées relatives à votre bot.
1. Laissez la zone **Point de terminaison de la messagerie** vide pour le moment. Vous entrerez l’URL demandée après le déploiement du bot. L’image suivante présente un exemple de paramètres d’inscription :

    ![inscription de chaînes d’application de bot](../../assets/images/authentication/auth-bot-channels-registration.png)

1. Cliquez sur **ID d'application Microsoft et mot de passe**, puis sur **Créer nouveau**.

    ![Créer un ID d'application Microsoft](../../assets/images/authentication/CreateMicrosoftAppID.png) ![Créer un nouvel ID d'application Microsoft](../../assets/images/authentication/CreateNewMicrosoftAppID.png)    

1. Cliquez sur le lien **Créer l'ID d'application sur le portail d'inscription d'application**.

   ![Inscriptions d’applications](../../assets/images/authentication/AppRegistration.png)
   
1. Dans la fenêtre **Inscription d’application** affichée, cliquez sur l’onglet **Nouvelle inscription** dans le coin supérieur gauche.
1. Entrez le nom de l’application bot que vous inscrivez, nous avons utilisé *BotTeamsAuth* (vous devez sélectionner votre propre nom).
1. Pour les **Types de comptes pris en charge**, sélectionnez *Comptes dans un annuaire organisationnel (comptes Azure AD Directory multi-locataires) et les comptes personnels Microsoft (par ex. Skype, Xbox)*.
1. Cliquez sur le bouton **Inscrire**. Une fois terminé, Azure affiche la page *Aperçu* de l’application.
1. Copiez et enregistrez la valeur **ID du client d’application** dans un fichier.
1. Dans le panneau de gauche, cliquez sur **Certificat et clés secrètes**.
    1. Sous *Clés secrètes client*, cliquez sur **Nouvelle clé secrète client**.
    1. Ajoutez une description pour reconnaître la clé secrète des autres que vous devrez peut-être créer pour cette application.
    1. Configurez la *Date d’expiration* de votre sélection.
    1. Cliquez sur **Ajouter**.
    1. Copiez la clé secrète client et enregistrez-la dans un fichier.
1. Revenez à la fenêtre **Inscription de chaînes de bot** et copiez l’*ID d’application* et la *Clé secrète client* dans les zones **ID d’application Microsoft** et **Mot de passe** respectives.
1. Cliquez sur **OK**.
1. Pour finir, cliquez sur **Créer**.

Après la création par Azure de la ressource d’inscription, celle-ci sera incluse dans la liste du groupe de ressources.  

![groupe d’inscription de chaînes d’application de bot](~/assets/images/authentication/auth-bot-channels-registration-group.PNG)

Une fois l’inscription de chaînes de bot créée, vous devez activer le canal Teams.

1. Dans le [Portail Microsoft Azure](https://ms.portal.azure.com/#home), sous les Services Azure, sélectionnez l’**Inscription de chaînes de bot** que vous venez de créer.
1. Dans le panneau de gauche, cliquez sur **Chaînes**.
1. Cliquez sur l’icône Microsoft Teams, puis sélectionnez **Enregistrer**.
