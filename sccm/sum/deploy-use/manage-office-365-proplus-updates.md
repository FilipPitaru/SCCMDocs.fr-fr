---
title: "Gérer les mises à jour d’Office 365 ProPlus | Microsoft Docs"
description: "Configuration Manager synchronise les mises à jour du client Office 365 du catalogue WSUS vers le serveur de site de façon à rendre les mises à jour disponibles pour un déploiement sur les clients."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 03/24/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 016580dc6ee3c5268833db941d42416a976d201c
ms.contentlocale: fr-fr
ms.lasthandoff: 05/17/2017

---

# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gérer Office 365 ProPlus avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager synchronise les mises à jour du client Office 365 et les rend disponibles pour les déployer sur les clients où Office 365 est installé. À compter de Configuration Manager version 1610, vous pouvez consulter les informations sur le client Office 365 dans le tableau de bord Gestion des clients Office 365.

À compter de Configuration Manager version 1602, Configuration Manager permet de gérer les mises à jour du client Office 365 en utilisant le flux de travail de gestion des mises à jour logicielles. Lorsque Microsoft publie une nouvelle mise à jour du client Office 365 sur le réseau de distribution contenu (CDN) d’Office, Microsoft publie également un package de mise à jour sur Windows Server Update Services (WSUS). Après que Configuration Manager a synchronisé la mise à jour du client Office 365 du catalogue WSUS vers le serveur de site, la mise à jour est disponible pour un déploiement sur les clients.

Depuis la version 1702, vous pouvez démarrer le programme d’installation Office 365 depuis le tableau de bord Gestion des clients Office 365 pour faciliter l’installation initiale de l’application Office 365. L’Assistant vous permet de configurer les paramètres d’installation Office 365, de télécharger des fichiers à partir de réseaux de distribution de contenu Office et de créer et déployer une application de script avec le contenu.

## <a name="office-365-client-management-dashboard"></a>Tableau de bord Gestion des clients Office 365  
À partir de Configuration Manager version 1610, le tableau de bord de gestion des clients Office 365 est disponible dans la console Configuration Manager. Pour afficher le tableau de bord, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**.

Le tableau de bord affiche des graphiques pour les éléments suivants :

- Nombre de clients Office 365
- Versions du client Office 365
- Langues du client Office 365
- Canaux du client Office 365     
Pour plus d’informations, consultez [Présentation des canaux de mise à jour pour Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
<!--- - Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products). --->

<!---You can take the following actions on the dashboard:
- --->

En haut du tableau de bord, utilisez le paramètre de liste déroulante **Regroupement** pour filtrer les données de tableau de bord selon les membres d’un regroupement spécifique.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Afficher des données dans le tableau de bord Gestion des clients Office 365
Les données affichées dans le tableau de bord Gestion des clients Office 365 sont issues de l’inventaire matériel. Pour permettre l’affichage des données dans ce tableau de bord, vous devez activer l’inventaire matériel et sélectionner la classe d’inventaire matériel **Configurations Office 365 ProPlus**.
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Pour afficher des données dans le tableau de bord Gestion des clients Office 365
1. Activez l’inventaire matériel si vous ne l’avez pas encore fait. Pour plus d’informations, consultez [Configurer l’inventaire matériel](\sccm\core\clients\manage\configure-hardware-inventory).
2. Dans la console Configuration Manager, accédez à **Administration** > **Paramètres client** > **Paramètres client par défaut**.  
3. Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  
4. Dans la boîte de dialogue **Paramètres client par défaut** , cliquez sur **Inventaire matériel**.  
5. Dans la liste **Paramètres du périphérique** , cliquez sur **Définir des classes**.  
6. Dans la boîte de dialogue **Classes d’inventaire matériel**, sélectionnez **Configurations Office 365 ProPlus**.  
7.  Cliquez sur **OK** pour enregistrer vos modifications et fermer la boîte de dialogue **Classes d'inventaire matériel** .  
Le tableau de bord Gestion des clients Office 365 commence à afficher des données dès qu’un inventaire matériel est signalé.

## <a name="deploy-office-365-updates-with-configuration-manager"></a>Déployer les mises à jour d’Office 365 avec Configuration Manager
Procédez comme suit pour déployer les mises à jour d’Office 365 avec le Gestionnaire de Configuration :

1.  [Vérifiez la configuration requise](https://technet.microsoft.com/library/mt628083.aspx) pour utiliser Configuration Manager en vue de gérer les mises à jour du client Office 365 dans la section **Configuration requise pour utiliser Configuration Manager afin de gérer les mises à jour du client Office 365** de la rubrique.  

2.  [Configurez les points de mise à jour logicielle](../get-started/configure-classifications-and-products.md) pour synchroniser les mises à jour du client Office 365. Définissez **Mises à jour** en guise de classification et sélectionnez **Office 365 Client** en guise de produit. Vous pouvez être amené à synchroniser les mises à jour logicielles au moins une fois avant que le produit Office 365 Client puisse être sélectionné. Vous devez synchroniser les mises à jour logicielles après avoir configuré les points de mise à jour logicielle pour utiliser la classification **Mises à jour**.
3.  Habilitez les clients Office 365 à recevoir des mises à jour de Configuration Manager. Pour cela, vous pouvez utiliser les paramètres du client Configuration Manager ou la stratégie de groupe. Employez l’une des méthodes suivantes pour activer le client :  
    - Méthode 1 : à compter de Configuration Manager version 1606, vous pouvez utiliser le paramètre du client Configuration Manager pour gérer l’agent Office 365 Client. Après avoir configuré ce paramètre et déployé les mises à jour d’Office 365, l’agent client Configuration Manager communique avec l’agent Office 365 Client de façon à télécharger les mises à jour d’Office 365 à partir d’un point de distribution et ensuite à les installer. Configuration Manager dresse l’inventaire des paramètres du client Office 365 ProPlus.
      1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Vue d’ensemble** > **Paramètres client**.  

      2.  Ouvrez les paramètres d’appareil appropriés pour activer l’agent client. Pour plus d’informations sur les paramètres par défaut et personnalisés du client, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Cliquez sur **Mises à jour logicielles** et sélectionnez **Oui** pour le paramètre **Activer la gestion de l’agent Office 365 Client**.  

    - Méthode 2 : [Habilitez les clients Office 365 à recevoir les mises à jour](https://technet.microsoft.com/library/mt628083.aspx#BKMK_EnableClient) de Configuration Manager via l’outil Déploiement d’Office ou la stratégie de groupe.  

4. [Déployez les mises à jour d’Office 365](deploy-software-updates.md) sur les clients.   

> [!Important]
> Si vous disposez d’un client Office 365 avec plusieurs langues et téléchargez les mises à jour pour moins de langues, les mises à jour ne pourront pas s’installer. Par exemple, supposons que vous disposiez d’un client Office 365 avec les langues en-us et fr-fr. Sur le serveur de site, vous téléchargez et déployez uniquement le contenu en-us pour une mise à jour Office 365 applicable. Lorsque l’utilisateur commence l’installation de cette mise à jour depuis le Centre logiciel, la mise à jour se bloque pendant le téléchargement du contenu. Vous devez télécharger et déployer les mises à jour dans les mêmes langues que les clients Office 365.  


## <a name="add-other-languages-for-office-365-update-downloads"></a>Télécharger des mises à jour Office 365 dans des langues supplémentaires
À compter de la version 1610, vous pouvez configurer Configuration Manager pour qu’il télécharge des mises à jour dans toutes les langues prises en charge par Office 365, que celles-ci soient prises en charge ou non par Configuration Manager.
> [!IMPORTANT]  
> La configuration de langues supplémentaires pour les mises à jour Office 365 est un paramètre qui s’étend au niveau du site. Une fois les langues ajoutées à l’aide de la procédure suivante, toutes les mises à jour Office 365 sont téléchargées dans ces langues, ainsi que dans celles sélectionnées dans la page Sélection de la langue de l’Assistant Téléchargement des mises à jour logicielles ou de l’Assistant Déploiement des mises à jour logicielles.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Pour télécharger des mises à jour dans des langues supplémentaires
Utilisez la procédure suivante sur le site d’administration centrale ou sur le site principal autonome sur lequel le rôle de système de site du point de mise à jour logicielle est installé.
1. À partir d’une invite de commande, tapez *wbemtest* avec des droits d’administration pour ouvrir le testeur WMI.
2. Cliquez sur **Connexion**, puis tapez *root\sms\site_&lt;siteCode&gt;*.
3. Cliquez sur **Requête**, puis exécutez la requête suivante : *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Requête WMI](..\media\1-wmiquery.png)
4. Dans le volet des résultats, double-cliquez sur l’objet avec le code de site pour le site d’administration centrale ou le site principal autonome.
5. Sélectionnez la propriété **Props**, cliquez sur **Modifier la propriété**, puis cliquez sur **Vue incorporée**.
![Éditeur de propriétés](..\media\2-propeditor.png)
6. En commençant par le premier résultat de la requête, ouvrez chaque objet jusqu’à ce que vous trouviez celui dont la propriété **PropertyName** a la valeur **AdditionalUpdateLanguagesForO365**.
7. Sélectionnez **Value2**, puis cliquez sur **Modifier la propriété**.  
![Modifier la propriété Value2](..\media\3-queryresult.png)
8. Ajoutez des langues supplémentaires à la propriété **Value2**, puis cliquez sur **Enregistrer la propriété**.  
Par exemple : pt-pt (Portugais - Portugal), af-za (Afrikaans - Afrique du Sud), nn-no (Norvégien [Nynorsk] - Norvège), etc.  
![Ajouter des langues dans l’Éditeur de propriétés](..\media\4-props.png)  
9. Cliquez sur **Fermer**, sur **Fermer**, sur **Enregistrer la propriété**, puis sur **Enregistrer l’objet** (si vous cliquez sur **Fermer** ici, les valeurs sont ignorées). Cliquez ensuite sur **Fermer**, puis sur **Quitter** pour quitter le testeur WMI.
10. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365** > **Mises à jour Office 365**.
11. Désormais, quand vous téléchargez des mises à jour Office 365, celles-ci sont téléchargées dans la langue sélectionnée dans l’Assistant et dans celles configurées durant cette procédure. Pour vérifier que les mises à jour ont été téléchargées dans ces langues, accédez à la source du package de la mise à jour et recherchez les fichiers dont le nom comprend le code de langue.  
![Noms de fichiers avec des langues supplémentaires](..\media\5-verification.png)


## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Modifier le canal de mise à jour une fois les clients Office 365 habilités à recevoir des mises à jour de Configuration Manager
Pour modifier le canal de mise à jour une fois que les clients Office 365 sont habilités à recevoir des mises à jour de Configuration Manager, vous pouvez utiliser une stratégie de groupe pour distribuer un changement de valeur de clé de Registre aux clients Office 365. Modifiez la clé de Registre **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** pour qu’elle utilise l’une des valeurs suivantes :

- Canal actuel :  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canal différé :  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Groupe First Release pour le canal actuel :  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Groupe First Release pour le canal différé :  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf

## <a name="deploy-office-365-apps"></a>Déployer des applications Office 365  
Depuis la version 1702, vous pouvez démarrer le programme d’installation Office 365 depuis le tableau de bord Gestion des clients Office 365 pour faciliter l’installation initiale de l’application Office 365. L’Assistant vous permet de configurer les paramètres d’installation Office 365, de télécharger des fichiers à partir de réseaux de distribution de contenu Office et de créer et déployer une application de script pour les fichiers.

Ceci est particulièrement utile car les mises à jour Office 365 ne sont pas applicables pour les clients où Office 365 n’est pas installé. Avant la version 1702, pour installer des applications Office 365 pour la première fois sur les clients, vous deviez télécharger manuellement l’outil de déploiement Office 365 (ODT) et les fichiers source d’installation Office 365, y compris tous les modules linguistiques nécessaires, puis générer le fichier Configuration.xml qui spécifie la version appropriée d’Office et le canal. Ensuite, vous deviez créer et déployer un package hérité ou une application de script pour les clients afin d’installer les applications Office 365.

> [!NOTE]
> - L’ordinateur qui exécute le programme d’installation de Office 365 doit avoir accès à Internet.  
> - L’utilisateur qui exécute le programme d’installation d’Office 365 doit avoir accès **en lecture** et en **écriture** au partage d’emplacement du contenu fourni dans l’Assistant.
> - Si vous recevez une erreur de téléchargement 404, copiez les fichiers suivants dans le dossier utilisateur %temp% :
>    - [releasehistory.xml](http://officecdn.microsoft.com.edgesuite.net/wsus/releasehistory.cab)
>    - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  
> - Après avoir créé et déployé des applications Office 365 à l’aide du programme d’installation Office 365, Configuration Manager ne gère pas les mises à jour Office par défaut. Pour permettre aux clients Office 365 de recevoir les mises à jour de Configuration Manager, consultez [Déployer les mises à jour d’Office 365 avec Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

### <a name="to-deploy-office-365-apps-to-clients-from-the-office-365-client-management-dashboard"></a>Pour déployer des applications Office 365 sur des clients depuis le tableau de bord Gestion des clients Office 365
1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**.
2. Cliquez sur **Office 365 Installer** (Programme d’installation d’Office 365) dans le volet supérieur droit. L’Assistant Installation d’Office 365 Client s’ouvre.
3. Dans la page **Application Settings** (Paramètres de l’application), indiquez le nom et une description de l’application, entrez l’emplacement de téléchargement pour les fichiers, puis cliquez sur **Suivant**. Notez que l’emplacement doit être spécifié sous la forme &#92;&#92;*serveur*&#92;*partage*.
4. Dans la page **Import Client Settings** (Importer les paramètres client), choisissez s’il convient d’importer les paramètres client Office 365 à partir d’un fichier de configuration XML existant ou de spécifier manuellement les paramètres, puis de cliquer sur **Suivant**.  

    Quand vous avez un fichier de configuration, entrez l’emplacement du fichier et passez à l’étape 7. Notez que l’emplacement doit être spécifié sous la forme &#92;&#92;*serveur*&#92;*partage*&#92;*nom_fichier*.XML.
5. Dans la page **Client Products** (Produits clients), sélectionnez la suite Office 365 que vous utilisez, les applications à inclure, les produits Office supplémentaires qui doivent être ajoutés, puis cliquez sur **Suivant**.
6. Dans la page **Paramètres client**, choisissez les paramètres à inclure, puis cliquez sur **Suivant**.
7. Dans la page **Déploiement**, choisissez de déployer ou non l’application, puis cliquez sur **Suivant**.  
Si vous choisissez de ne pas déployer le package dans l’Assistant, passez à l’étape 9.
8. Configurez le reste des pages de l’Assistant comme vous le feriez pour un déploiement d’application standard. Pour plus d’informations, consultez [Créer et déployer une application](/sccm/apps/get-started/create-and-deploy-an-application).
9. Effectuez toutes les étapes de l'Assistant.
10. Vous pouvez déployer ou modifier l’application de la même façon que toute autre application dans Configuration Manager à partir de **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des applications** > **Applications**.   

> [!IMPORTANT]
> L’application Office 365 que vous créez et déployez à l’aide de l'Assistant Création d'une application Office 365 dans Configuration Manager n’est pas automatiquement gérée par Configuration Manager tant que vous n’avez pas activé le paramètre de l’agent client des mises à jour logicielles **Enable management of the Office 365 Client Again**. Pour plus d’informations, consultez [À propos des paramètres du client](/sccm/core/clients/deploy/about-client-settings).

>[!NOTE]
>Après avoir déployé des applications Office 365, vous pouvez créer des règles de déploiement automatique pour mettre à jour les applications. Pour créer une règle de déploiement automatique pour les applications Office 365, cliquez sur **Créer une ADR** dans le tableau de bord Gestion des clients Office 365, sélectionnez **Client Office 365** lorsque vous choisissez le produit. Pour plus d’informations, consultez [Déployer automatiquement des mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates).

<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->

