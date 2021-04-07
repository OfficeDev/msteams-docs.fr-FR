---
title: Ajouter des données de test à votre client test Microsoft 365
description: Configurer votre abonnement au programme pour les développeurs Office 365 pour tester les applications Microsoft Teams
ms.topic: how-to
keywords: test des équipes de programme pour les développeurs d’applications
ms.date: 11/01/2019
ms.openlocfilehash: 863f1d9843bb3ebe968ca180ee70a5b6bfa6cd7a
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596188"
---
# <a name="add-test-data-to-your-microsoft-365-test-tenant"></a>Ajouter des données de test à votre client de test Microsoft 365

Avec un abonnement Microsoft 365 Développeur, vous pouvez utiliser votre application Microsoft Teams avec des équipes de test, des canaux et des utilisateurs.

## <a name="before-you-start"></a>Avant de commencer

Si vous n’avez pas encore de client de test, vous devrez rejoindre le programme pour les développeurs Office 365 et vous inscrire à un abonnement développeur. Vous devez également installer les modules PowerShell nécessaires. Quel que soit le client que vous utilisez, vous devez avoir des autorisations d’administrateur général pour exécuter les scripts.

1. [Rejoignez le programme développeur de Microsoft 365](/office/developer-program/office-365-developer-program)
2. [Configurer un abonnement Microsoft 365 Développeur](/office/developer-program/office-365-developer-program-get-started)
3. [Utiliser des packs d’exemples de données avec votre abonnement Microsoft 365 Développeur pour installer le pack de contenu Utilisateurs](/office/developer-program/install-sample-packs)
4. [Installer le module PowerShell Teams](https://www.powershellgallery.com/packages/MicrosoftTeams/1.0.2)
5. [Installer le module Azure AD PowerShell](/powershell/azure/active-directory/install-adv2?view=azureadps-2.0#installing-the-azure-ad-module&preserve-view=true)

## <a name="optional-enable-custom-app-sideloading"></a>(Facultatif) Activer le chargement d’une version d’application personnalisée

Par défaut, seuls les administrateurs globaux ou les administrateurs du service Teams peuvent télécharger des applications personnalisées dans le catalogue d’applications client. Vous pouvez également autoriser les utilisateurs à télécharger des applications personnalisées dans Teams. Pour plus d’informations, [gérez les stratégies de configuration d’application dans Teams.](/microsoftteams/teams-app-setup-policies)

## <a name="create-teams-and-channels"></a>Créer des équipes et des canaux

Enregistrez l’extrait de code suivant en tant que code XML (.xml) et notez l’endroit où vous l’avez enregistré.  Ce XML définit la structure des équipes et des canaux qui seront créés, ainsi que ses membres.

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

Enregistrez l’extrait de code suivant en tant que script PowerShell (.ps1) et notez l’endroit où vous l’avez enregistré.  Ce script exécute les étapes pour créer les équipes et les canaux et y ajouter des membres.

```powershell
Param(
    [Parameter(Mandatory = $true)]
    
    # This specifies the location of your configuration XML.
    
    [string] $teamsFilePath 
)
    
[xml]$XmlDocument = Get-Content -Path $teamsFilePath.ToString()

if ($XmlDocument.Teams.Team.Count -gt 0) {

    try {
        
        # 1. Login with the global administrator account for your O365 Developer Program tenant.  This script will then use these credentials to connect to the powershell modules for Azure Active Directory and Microsoft Teams
        
        $creds = Get-Credential

        # Connecting to AAD PowerShell
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

Ouvrez une session Windows PowerShell en mode Administrateur.  Exécutez le script que vous avez enregistré.  Vous serez invité à fournir les informations d’identification : utilisez les informations d’identification d’administrateur général que vous avez reçues lors de votre première inscription à votre abonnement développeur.

> [!Note]
> L’exécution du script prendra plusieurs minutes : ne fermez pas votre session PowerShell.  Si vous avez modifié les utilisateurs de votre abonnement à partir de ce qui est créé dans le pack de contenu par défaut, certains utilisateurs peuvent ne pas être ajoutés aux équipes.  À mesure que le script s’exécute, il produit des actions réussies ou échouées.

Une fois l’exécution du script terminée, vous pouvez vous connecter au client Teams avec l’un des comptes d’utilisateur et afficher les équipes nouvellement créées.
