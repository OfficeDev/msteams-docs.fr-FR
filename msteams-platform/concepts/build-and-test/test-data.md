---
title: Ajouter des données de test à votre client de test Microsoft 365
description: Configurer votre abonnement au programme pour les développeurs Office 365 pour tester les applications Microsoft Teams à l’aide d’extraits de code
ms.topic: how-to
ms.localizationpriority: high
keywords: test des équipes du programme développeur d’applications
ms.date: 11/01/2019
ms.openlocfilehash: eca2c87b92e6dfdcce869ac1fd207b2149055070
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111968"
---
# <a name="add-test-data-to-your-microsoft-365-test-tenant"></a>Ajouter des données de test à votre client de test Microsoft 365

Vous pouvez tester votre application Microsoft Teams avec des exemples de données avec un abonnement Microsoft 365 développeur.

## <a name="prerequisites"></a>Configuration requise

1. [Rejoignez le programme de développement Microsoft 365](/office/developer-program/office-365-developer-program), si vous n’avez pas de client de test.
2. [Configurez un abonnement Microsoft 365 Développeur](/office/developer-program/office-365-developer-program-get-started).
3. [Utilisez des exemples de packs de données avec votre abonnement de développeur Microsoft 365 pour installer le pack de contenu Utilisateurs](/office/developer-program/install-sample-packs).
4. [Installer le module Teams PowerShell](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2).
5. [Installez le module PowerShell Azure AD](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true).

> [!NOTE]
> Vous devez disposer d’autorisations d’administrateur général dans le client pour exécuter les scripts.

## <a name="allow-users-to-upload-apps"></a>Autoriser les utilisateurs à charger des applications

Par défaut, seuls les administrateurs généraux ou les administrateurs de service Teams peuvent charger (charger une version test) des applications dans un locataire. Vous pouvez également autoriser les utilisateurs à charger des applications personnalisées pour leur propre utilisation ou à des équipes à des fins de test. Pour plus d’informations, consultez [gérer les paramètres et les stratégies d’application personnalisés dans Teams](/microsoftteams/teams-custom-app-policies-and-settings).

## <a name="create-teams-and-channels-for-testing"></a>Créer des équipes et des canaux pour les tests

1. Enregistrez l’extrait de code suivant en tant que fichier **.xml** et notez le chemin d’accès au fichier. Ce code XML définit la structure de l’équipe et du canal créés avec ses membres :

    ```xml
    <?xml version="1.0"?>
    <Teams>
      <Team Name="Store Portal" ID="storeportal" Description="" Type="Private" Creator="admin">
        <Members>
          <Member UserName="AlexW" IsOwner="false"/>
          <Member UserName="PattiF" IsOwner="false"/>
          <Member UserName="PradeepG" IsOwner="false"/>
          <Member UserName="JoniS" IsOwner="false"/>
          <Member UserName="JohannaL" IsOwner="false"/>
          <Member UserName="NestorW" IsOwner="false"/>
          <Member UserName="IsaiahL" IsOwner="false"/>
          <Member UserName="AdeleV" IsOwner="false"/>
          <Member UserName="LeeG" IsOwner="false"/>
          <Member UserName="MeganB" IsOwner="true"/>
          <Member UserName="LynneR" IsOwner="false"/>
          <Member UserName="GradyA" IsOwner="false"/>
          <Member UserName="LidiaH" IsOwner="false"/>
          <Member UserName="DiegoS" IsOwner="false"/>
          <Member UserName="MiriamG" IsOwner="true"/>
        </Members>
        <Channels>
          <Channel Name="Sales" ID="sales" Description="" Creator="Admin" />
          <Channel Name="Inventory" ID="inventory" Description="" Creator="Admin" />
          <Channel Name="Los Angeles Store 239" ID="losangelesstore239" Description="" Creator="Admin" />
          <Channel Name="Seattle Store 121" ID="seattlestore121" Description="" Creator="Admin" />
          <Channel Name="Online" ID="online" Description="" Creator="Admin" />
          <Channel Name="Store Layout" ID="storelayout" Description="" Creator="Admin" />
          <Channel Name="Promotions" ID="promotions" Description="" Creator="Admin" />
        </Channels>
      </Team>
      <Team Name="Mark 8 Project Team" ID="Mark8ProjectTeam" Description="Welcome to the team that we've assembled to create the Mark 8." Type="Private" Creator="admin">
        <Members>
          <Member UserName="meganb" IsOwner="true" />
          <Member UserName="alexw" IsOwner="false" />
          <Member UserName="lynner" IsOwner="false" />
          <Member UserName="isaiahl" IsOwner="false" />
          <Member UserName="leeg" IsOwner="false" />
          <Member UserName="pradeepg" IsOwner="false" />
          <Member UserName="lidiah" IsOwner="false" />
          <Member UserName="diegos" IsOwner="false" />
          <Member UserName="johannal" IsOwner="false" />
          <Member UserName="miriamg" IsOwner="false" />
          <Member UserName="adelev" IsOwner="false" />
          <Member UserName="jonis" IsOwner="false" />
          <Member UserName="nestorw" IsOwner="false" />
          <Member UserName="gradya" IsOwner="false" />
          <Member UserName="pattif" IsOwner="false" />
        </Members>
        <Channels>
          <Channel Name="Research and Development" ID="researchanddevelopment" Description="Channel for Research and Development!" Creator="meganb" />
          <Channel Name="Design" ID="design" Description="Discuss design projects." Creator="meganb" />
          <Channel Name="Digital Assets Web" ID="digitalassetsweb" Description="Discuss digital assets." Creator="meganb" />
          <Channel Name="Go to Market Plan" ID="gotomarketplan" Description="Our go-to-market plan!" Creator="meganb" />
        </Channels>
      </Team>
      <Team Name="District 9 Road Safety Audit" ID="district9roadsafetyaudit" Description="" Type="Private" Creator="admin">
        <Members>
          <Member UserName="meganb" IsOwner="true" />
          <Member UserName="alexw" IsOwner="false" />
          <Member UserName="lynner" IsOwner="false" />
          <Member UserName="isaiahl" IsOwner="false" />
          <Member UserName="leeg" IsOwner="false" />
          <Member UserName="pradeepg" IsOwner="false" />
          <Member UserName="lidiah" IsOwner="false" />
          <Member UserName="diegos" IsOwner="false" />
          <Member UserName="johannal" IsOwner="false" />
          <Member UserName="miriamg" IsOwner="false" />
          <Member UserName="adelev" IsOwner="false" />
          <Member UserName="jonis" IsOwner="false" />
          <Member UserName="nestorw" IsOwner="false" />
          <Member UserName="gradya" IsOwner="false" />
          <Member UserName="pattif" IsOwner="false" />
        </Members>
        <Channels>
          <Channel Name="Audit Planning" ID="auditplanning" Description="" Creator="Admin" />
          <Channel Name="Delivery" ID="delivery" Description="" Creator="Admin" />
          <Channel Name="Findings" ID="findings" Description="" Creator="Admin" />
          <Channel Name="Recommended Actions" ID="recommendedactions" Description="" Creator="Admin" />
          <Channel Name="Survey" ID="survey" Description="" Creator="Admin" />
        </Channels>
      </Team>
      <Team Name="ACC-1000 Product Team" ID="acc1000productteam" Description="" Type="Private" Creator="admin" >
        <Members>
          <Member UserName="meganb" IsOwner="true" />
          <Member UserName="alexw" IsOwner="false" />
          <Member UserName="lynner" IsOwner="false" />
          <Member UserName="isaiahl" IsOwner="false" />
          <Member UserName="leeg" IsOwner="false" />
          <Member UserName="pradeepg" IsOwner="false" />
          <Member UserName="lidiah" IsOwner="false" />
          <Member UserName="diegos" IsOwner="false" />
          <Member UserName="johannal" IsOwner="false" />
          <Member UserName="miriamg" IsOwner="false" />
          <Member UserName="adelev" IsOwner="false" />
          <Member UserName="jonis" IsOwner="false" />
          <Member UserName="nestorw" IsOwner="false" />
          <Member UserName="gradya" IsOwner="false" />
          <Member UserName="pattif" IsOwner="false" />
        </Members>
        <Channels>
          <Channel Name="Corporate Communication" ID="corporatecommunication" Description="" Creator="Admin" />
          <Channel Name="Lean Process Improvement" ID="corporatecommunication" Description="" Creator="Admin" />
          <Channel Name="Training and Certification" ID="trainingandcertification" Description="" Creator="Admin" />
          <Channel Name="Production" ID="production" Description="" Creator="Admin" />
          <Channel Name="Research and Development" ID="researchanddevelopment" Description="" Creator="Admin" />
          <Channel Name="Supplier Collaboration" ID="suppliercollaboration" Description="" Creator="Admin" />
        </Channels>
      </Team>
    </Teams>
    ```

2. Enregistrez l’extrait de code suivant en tant que script PowerShell (.ps1) et notez où vous l’avez enregistré. Ce script exécute les étapes permettant de créer l’équipe et le canal, et d’y ajouter des membres :

    ```powershell
    Param(
        [Parameter(Mandatory = $true)]

        # This specifies the location of your configuration XML.

        [string] $teamsFilePath 
    )

    [xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

    if ($XmlDocument.Teams.Team.Count -gt 0) {

        try {

            # 1. Login with the global administrator account for your Office 365 Developer Program tenant. This script uses these credentials to connect to the PowerShell modules for Azure Active Directory and Microsoft Teams

            $creds = Get-Credential

            # Connecting to Azure AD PowerShell
            Connect-AzureAD -Credential $creds | Out-Null

            # Connect to Microsoft Teams PowerShell
            Connect-MicrosoftTeams -Credential $creds | Out-Null

            Write-Host "Connected to Microsoft 365 and configuring your organization with test teams and channels"

            # 2. Create the teams as specified in the XML.

            foreach ($team in $XmlDocument.Teams.Team ) {
                try {
                    $group = New-Team -DisplayName $team.Name -Description $teams.description -visibility public 
                    Write-Host "Successfully created team: " $group.DisplayName
                }
                catch {
                    Write-Host "Unable to create team: $_"
                }

                # 3. Add users to the newly created teams.
                foreach ($user in $team.Members.Member) {
                    try {
                        $newUserPrincipalName = (Get-AzureADUser -SearchString $user.UserName).UserPrincipalName

                        if($user.IsOwner -eq $true){
                            Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName -Role Owner | Out-Null
                        }else{
                            Add-TeamUser -GroupId $group.GroupId -User $newUserPrincipalName | Out-Null
                        }

                        Write-Host "Successfully added user : " $user.UserName
                    }
                    catch {
                        Write-Host "Unable to add team user: $_"
                    }

                }

                # 4. Add a set of channels to each newly created team
                foreach ($channel in $team.Channels.Channel) {
                    try {
                        # Adding each team channel
                        New-TeamChannel -GroupId $group.GroupId -DisplayName $channel.Name -Description $channel.Description | Out-Null
                        Write-Host "Successfully created channel: " $channel.Name
                    }
                    catch {
                        Write-Host "Unable to add new Team Channel: $_"
                    }   
                }

                Clear-Variable -Name group
            }

            Clear-Variable -Name creds

            # 5. Disconnect from all PowerShell sessions

            Write-Host "Completed execution and disconnecting from Microsoft 365 PowerShell sessions."
            Disconnect-MicrosoftTeams
            Disconnect-AzureAD
        }
        catch {
            Write-Host "Unable to complete the operation: $_"
        }
    }
    else {
        Write-Host "Content file has invalid data."
    }
    ```

3. Ouvrez une session Windows PowerShell en mode Administrateur et exécutez le script que vous venez d’enregistrer.
4. Lorsque vous êtes invité à fournir les informations d’identification, entrez les informations d’identification d’administrateur général que vous avez reçues lors de votre première inscription à votre abonnement développeur.

    > [!Note]
    > Ne fermez pas votre session PowerShell, car l’exécution du script prend plusieurs minutes. Si vous avez modifié les utilisateurs de votre abonnement à partir de ce qui est créé dans le pack de contenu par défaut, certains utilisateurs peuvent ne pas être ajoutés à Teams. Lorsque le script s’exécute, il affiche les actions réussies ou ayant échoué.

5. Une fois l’exécution du script terminée, vous pouvez vous connecter au client Teams avec l’un des comptes d’utilisateur et afficher les équipes nouvellement créées.

## <a name="see-also"></a>Voir aussi

* [Déboguer votre onglet](~/tabs/how-to/developer-tools.md)
* [Déboguer vos bots](~/bots/how-to/debug/locally-with-an-ide.md)
* [Tester les autorisations RSC](~/graph-api/rsc/test-resource-specific-consent.md)
