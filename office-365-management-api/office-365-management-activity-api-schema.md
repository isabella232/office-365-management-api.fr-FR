---
ms.TocTitle: Office 365 Management Activity API schema
title: Schéma de l’API Activité de gestion Office 365
description: 'Le schéma de l’API Activité de gestion Office 365 est fourni en tant que service de données en deux couches : le schéma commun et le schéma propre au produit.'
ms.ContentId: 1c2bf08c-4f3b-26c0-e1b2-90b190f641f5
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 85e9a62a029a905204d0091d3f0d58824d3c1d9a
ms.sourcegitcommit: 0db48c00c956935a4a52aa2c2686f160a3efc8f3
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/22/2019
ms.locfileid: "37636283"
---
# <a name="office-365-management-activity-api-schema"></a>Schéma de l’API Activité de gestion Office 365
 
Le schéma de l’API Activité de gestion Office 365 est fourni en tant que service de données en deux couches :

- **Schéma commun**. L’interface permettant d’accéder aux principaux concepts d’audit d’Office 365, comme le type d’enregistrement, l’heure de création, le type d’utilisateur et l’action, ainsi que d’obtenir les dimensions principales (par exemple, l’ID utilisateur), les informations sur l’emplacement (par exemple, l’adresse IP du client) et les propriétés propres au produit (par exemple, l’ID d’objet). Elle présente des affichages uniformes et cohérents pour les utilisateurs afin d’extraire toutes les données d’audit d’Office 365 dans un nombre réduit d’affichages de niveau supérieur avec les paramètres appropriés. Elle fournit un schéma fixe pour toutes les sources de données, ce qui réduit considérablement le coût d’apprentissage. Le schéma commun est issu des données de produit appartenant à chaque équipe de produit, comme Exchange, SharePoint, Azure Active Directory, Yammer et OneDrive Entreprise. Le champ ID d’objet peut être étendu par les équipes de produit pour ajouter des propriétés propres au produit.
    
- **Schéma propre au produit**. Conçu en complément du schéma commun pour fournir un ensemble d’attributs spécifiques du produit. Par exemple : schéma Sway, schéma SharePoint, schéma OneDrive Entreprise et schéma d’administration Exchange.
    
**Quelle couche devez-vous utiliser dans votre scénario ?**
En général, si les données sont disponibles dans une couche supérieure, ne revenez pas à une couche inférieure. En d’autres termes, si l’exigence de données peut s’adapter au schéma propre au produit, vous n’avez pas besoin de revenir au schéma commun. 

## <a name="office-365-management-api-schemas"></a>Schémas de l’API de gestion d’Office 365

Cet article donne des détails sur le schéma commun, ainsi que sur tous les schémas propres aux produits. Le tableau suivant décrit les schémas disponibles. 

|Nom du schéma|Description|
|:-----|:-----|
|[Schéma commun](#common-schema)|Vue permettant d’extraire le type d’enregistrement, l’ID utilisateur, l’adresse IP du client, le type d’utilisateur et l’action, ainsi que les dimensions principales telles que les propriétés utilisateur (comme UserID), les propriétés d’emplacement (comme l’adresse IP du client) et les propriétés propres au produit (comme l’ID d’objet).|
|[Schéma de base SharePoint](#sharepoint-base-schema)|Étend le schéma commun avec les propriétés spécifiques de toutes les données d’audit de SharePoint.|
|[Opérations sur les fichiers SharePoint](#sharepoint-file-operations)|Étend le schéma de base SharePoint avec les propriétés spécifiques de la manipulation et de l’accès aux fichiers dans SharePoint.|
|[Schéma de partage SharePoint](#sharepoint-sharing-schema)|Étend le schéma de base de SharePoint avec les propriétés spécifiques du partage de fichier.|
|[Schéma SharePoint](#sharepoint-schema)|Étend le schéma de base de SharePoint avec les propriétés spécifiques de SharePoint, mais non liées à la manipulation ou à l’accès aux fichiers.|
|[Schéma Project](#project-schema)|Étend le schéma de base SharePoint avec les propriétés spécifiques de Project.|
|[Schéma d’administration Exchange](#exchange-admin-schema)|Étend le schéma commun avec les propriétés spécifiques de toutes les données d’audit d’administration Exchange.|
|[Schéma de boîte aux lettres Exchange](#exchange-mailbox-schema)|Étend le schéma de base avec les propriétés spécifiques de toutes les données d’audit de boîte aux lettres Exchange.|
|[Schéma de base Azure Active Directory](#azure-active-directory-base-schema)|Étend le schéma commun avec les propriétés spécifiques de toutes les données d’audit Azure Active Directory.|
|[Schéma de connexion au compte Azure Active Directory](#azure-active-directory-account-logon-schema)|Étend le schéma de base Azure Active Directory avec les propriétés spécifiques de tous les événements de connexion Azure Active Directory.|
|[Schéma de connexion Secure STS Azure Active Directory](#azure-active-directory-secure-token-service-sts-logon-schema)|Étend le schéma de base Azure Active Directory avec les propriétés spécifiques de tous les événements de connexion STS (Secure Token Service) d’Azure Active Directory.|
|[Schéma Azure Active Directory](#azure-active-directory-schema)|Étend le schéma commun avec les propriétés spécifiques de toutes les données d’audit Azure Active Directory.|
|[Schéma DLP](#dlp-schema)|Étend le schéma commun avec les propriétés spécifiques des événements de protection contre la perte de données (DLP).|
|[Schéma du Centre de sécurité et conformité](#security-and-compliance-center-schema)|Étend le schéma commun avec les propriétés spécifiques de tous les événements du Centre de sécurité et conformité.|
|[Schéma d’alertes de sécurité et conformité](#security-and-compliance-alerts-schema)|Étend le schéma commun avec les propriétés spécifiques de toutes les alertes de sécurité et conformité d’Office 365.|
|[Schéma Yammer](#yammer-schema)|Étend le schéma commun avec les propriétés spécifiques de tous les événements Yammer.|
|[Schéma Sway](#sway-schema)|Étend le schéma commun avec les propriétés spécifiques de tous les événements Sway.|
|[Schéma de base de sécurité du centre de données](#data-center-security-base-schema)|Étend le Schéma commun avec les propriétés spécifiques de toutes les données d’audit de sécurité du centre de données.|
|[Schéma de cmdlet de sécurité du centre de données](#data-center-security-cmdlet-schema)|Étend le schéma de base de sécurité du centre de données avec les propriétés spécifiques de toutes les données d’audit de cmdlet de sécurité du centre de données.|
|[Schéma Microsoft Teams](#microsoft-teams-schema)|Étend le schéma commun avec les propriétés spécifiques de tous les événements Microsoft Teams.|
|[Schéma Office 365 - Protection avancée contre les menaces et Threat Investigation and Response](#office-365-advanced-threat-protection-and-threat-investigation-and-response-schema)|Étend le schéma commun avec les propriétés spécifiques des données relatives à Office 365 - Protection avancée contre les menaces et Threat Investigation and Response.|
|[Schéma Power BI](#power-bi-schema)|Étend le Schéma commun avec les propriétés spécifiques à tous les événements Power BI.|
|[Analyse du temps de travail](#workplace-analytics-schema)|Étend le schéma commun avec les propriétés spécifiques de tous les événements Analyse du temps de travail Microsoft.|
|||

## <a name="common-schema"></a>Schéma commun

**Nom EntityType** : AuditRecord

|Paramètre|Type|Obligatoire ?|Description|
|:-----|:-----|:-----|:-----|
|ID|Combinaison GUIDEdm.Guid|Oui|Identificateur unique d’un enregistrement d’audit.|
|RecordType|Self.[AuditLogRecordType](#auditlogrecordtype)|Oui|Type d’opération indiqué par l’enregistrement. Reportez-vous au tableau [AuditLogRecordType](#auditlogrecordtype) pour obtenir plus d’informations sur les types d’enregistrements du journal d’audit.|
|CreationTime|Edm.Date|Oui|Date et heure à l’heure UTC (temps universel coordonné) au moment où l’utilisateur a effectué l’activité.|
|Opération|Edm.String|Oui|Nom de l’activité de l’utilisateur ou de l’administrateur. Pour consulter la description des opérations/activités les plus courantes, reportez-vous à l’article relatif à la [recherche dans le journal d’audit dans le Centre de sécurité et conformité d’Office 365](http://go.microsoft.com/fwlink/p/?LinkId=708432). Pour une activité d’administration Exchange, cette propriété identifie le nom de la cmdlet qui a été exécutée. Pour les événements DLP, les valeurs possibles, définies sous « Schéma DLP » ci-dessous, sont les suivantes : « DlpRuleMatch », « DlpRuleUndo » ou « DlpInfo ».|
|OrganizationId|Edm.Guid|Oui|GUID pour le client Office 365 de votre organisation. Cette valeur sera toujours identique pour votre organisation, quel que soit le service Office 365 concerné.|
|UserType|Self.[UserType](#user-type)|Oui|Type d’utilisateur ayant effectué l’opération. Reportez-vous au tableau [UserType](#user-type) pour obtenir plus d’informations sur les types d’utilisateur.|
|UserKey|Edm.String|Oui|Autre ID pour l’utilisateur identifié dans la propriété UserId. Par exemple, cette propriété est renseignée avec l’ID unique Passport (PUID) pour les événements exécutés par des utilisateurs dans SharePoint, OneDrive Entreprise et Exchange. Cette propriété peut également spécifier la même valeur que la propriété UserID pour les événements se produisant dans d’autres services et les événements exécutés par des comptes système.|
|Charge de travail|Edm.String|Non|Service Office 365 dans lequel l’activité s’est produite. 
|ResultStatus|Edm.String|Non|Indique si l’action (indiquée dans la propriété Operation) a réussi ou non. Valeurs possibles : **Succeeded**, **PartiallySucceded** ou **Failed**. Pour une activité d’administration Exchange, la valeur peut être **True** ou **False**.<br/><br/>**Important** : plusieurs charges de travail peuvent remplacer la valeur de la propriété ResultStatus. Par exemple, pour les événements d’ouverture de session STS d’Azure Active Directory, la valeur **Succedded** pour ResultStatus indique uniquement que l’opération HTTP a réussi. Cela ne signifie pas que la connexion a réussi. Pour déterminer si l’ouverture de session elle-même a réussi ou non, examinez la propriété LogonError dans le [schéma de connexion STS Azure Active Directory](#azure-active-directory-secure-token-service-sts-logon-schema). Si la connexion a échoué, la valeur de cette propriété indique la raison de l’échec de la tentative de connexion. |
|ObjectId|Edm.string|Non|Pour l’activité SharePoint et OneDrive Entreprise, il s’agit du nom du chemin d’accès complet au fichier ou au dossier consulté par l’utilisateur. Pour la journalisation d’audit d’administration Exchange, il s’agit du nom de l’objet modifié par la cmdlet.|
|UserId|Edm.string|Oui|L’UPN (nom d’utilisateur principal) de l’utilisateur ayant effectué l’action (indiquée dans la propriété Operation) qui a entraîné la journalisation de l’enregistrement. Par exemple, `my_name@my_domain_name`. L’enregistrement d’une activité exécutée par un compte système (comme SHAREPOINT\system ou NT AUTHORITY\SYSTEM) est également inclus.|
|ClientIP|Edm.String|Oui|Adresse IP du périphérique utilisé lors de la journalisation de l’activité. L’adresse IP apparaît au format d’adresse IPv4 ou IPv6.<br/><br/>Pour certains services, la valeur affichée dans cette propriété peut être l'adresse IP d'une application sécurisée (par exemple, Office sur les applications Web) qui appelle le service au nom d'un utilisateur et non l'adresse IP de l'appareil utilisé par la personne ayant effectué l'activité. <br/><br/>Aussi, pour les événements relatifs à Azure Active Directory, l’adresse IP n’est pas enregistrée et la valeur de la propriété ClientIP est `null`.|
|Portée|Self.[AuditLogScope](#auditlogscope)|Non|Cet événement a-t-il été créé par un service Office 365 hébergé ou un serveur local ? Valeurs possibles : **online** et **onprem**. SharePoint est la seule charge de travail qui envoie actuellement des événements d’un serveur local à Office 365.|
|||||

### <a name="enum-auditlogrecordtype---type-edmint32"></a>Énumération : AuditLogRecordType - Type : Edm.Int32

#### <a name="auditlogrecordtype"></a>AuditLogRecordType

|Valeur|Nom du membre|Description|
|:-----|:-----|:-----|
|1|ExchangeAdmin|Événements du journal d’audit de d’administration Exchange.|
|2|ExchangeItem|Événements d’un enregistrement d’audit de boîte aux lettres Exchange pour les actions effectuées sur un seul élément, comme la création ou la réception d’un message électronique.|
|3|ExchangeItemGroup|Événements d’un événement d’audit de boîte aux lettres Exchange pour les actions qui peuvent être effectuées sur plusieurs éléments, comme le déplacement ou la suppression d’un ou de plusieurs messages électroniques.|
|4|SharePoint|Événements SharePoint.|
|6|SharePointFileOperation|Événements d’opération de fichier SharePoint.|
|8|AzureActiveDirectory|Événements Azure Active Directory.|
|9|AzureActiveDirectoryAccountLogon|Événements de connexion OrgId Azure Active Directory (arrêt de la prise en charge).|
|10|DataCenterSecurityCmdlet|Événements de cmdlet de sécurité du centre de données.|
|11|ComplianceDLPSharePoint|Événements de protection contre la perte de données (DLP) dans SharePoint et OneDrive Entreprise.|
|12|Sway|Événements à partir des clients et du service Sway.|
|13|ComplianceDLPExchange|Événements de protection contre la perte de données (DLP) dans Exchange lorsqu’ils sont configurés via une stratégie DLP unifiée. Les événements DLP basés sur les règles de transport Exchange ne sont pas pris en charge.|
|14|SharePointSharingOperation|Événements de partage SharePoint.|
|15|AzureActiveDirectoryStsLogon|Événements de connexion STS (Secure Token Service) dans Azure Active Directory.|
|18|SecurityComplianceCenterEOPCmdlet|Actions d’administration à partir du Centre de sécurité et conformité.|
|20|PowerBIAudit|Événements Power BI.|
|21|CRM|Événements Microsoft CRM.|
|22|Yammer|Événements Yammer.|
|23|SkypeForBusinessCmdlets|Événements Skype Entreprise.|
|24|Discovery|Événements pour les activités eDiscovery effectuées en exécutant des recherches de contenu et en gérant les cas d’eDiscovery dans le Centre de sécurité et conformité.|
|25|MicrosoftTeams|Événements de Microsoft Teams.|
|28|ThreatIntelligence|Événements d’hameçonnage et de programmes malveillants depuis Exchange Online Protection et Office 365 Advanced Threat Protection.|
|30|MicrosoftFlow|Événements Microsoft Flow.|
|31|AeD|Événements eDiscovery (découverte électronique) avancée.|
|32|MicrosoftStream|Événements Microsoft Stream.|
|35|Project|Événements Microsoft Project.|
|36|SharepointListOperation|Événements de liste SharePoint.|
|38|DataGovernance|Événements liés aux stratégies de rétention et étiquettes rétention dans le centre de sécurité et conformité|
|40|SecurityComplianceAlerts|Signaux d’alerte de sécurité et conformité.|
|41|ThreatIntelligenceUrl|Événements de liens approuvés de bloc horaire et bloc de remplacement à partir d’Office 365 Advanced Threat Protection.|
|44|WorkplaceAnalytics|Événements Workplace Analytics.|
|45|PowerAppsApp|Événements application PowerApps.|
|47|ThreatIntelligenceAtpContent|Événements d’hameçonnage et programmes malveillants pour les fichiers dans SharePoint, OneDrive Entreprise et Microsoft Teams dans Office 365 Advanced Threat Protection .|
|54|SharePointListItemOperation|Événements de liste SharePoint.|
|55|SharePointContentTypeOperation|Événements de type de contenu de liste SharePoint.|
||||

### <a name="enum-user-type---type-edmint32"></a>Énumération : User Type - Type : Edm.Int32

#### <a name="user-type"></a>Type d’utilisateur

|Valeur|Nom du membre|Description|
|:-----|:-----|:-----|
|0|Regular|Utilisateur standard.|
|1|Reserved|Utilisateur réservé.|
|2|Admin|Administrateur.|
|3|DcAdmin|Opérateur du centre de données Microsoft.|
|4|System|Compte système.|
|5|Application|Application.|
|6|ServicePrincipal|Principal de service.|
||||

> [!NOTE] 
> Seules les opérations Exchange incluent un type d’utilisateur. Les opérations SharePoint ne spécifient pas de type d’utilisateur. 

### <a name="enum-auditlogscope---type-edmint32"></a>Énumération : AuditLogScope - Type : Edm.Int32

#### <a name="auditlogscope"></a>AuditLogScope

|Valeur|Nom du membre|Description|
|:-----|:-----|:-----|
|0|Online|Cet événement a été créé par un service Office 365 hébergé.|
|1|Onprem|Cet événement a été créé par un serveur local.|
||||


## <a name="sharepoint-base-schema"></a>Schéma de base SharePoint

|**Paramètre**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Site|Edm.Guid|Non|GUID du site où se trouve le fichier ou le dossier consulté par l’utilisateur.|
|ItemType|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[ItemType](#itemtype)"|Non|Type d’objet consulté ou modifié. Reportez-vous au tableau [ItemType](#itemtype) pour obtenir plus d’informations sur les types d’objets.|
|EventSource|Edm.String String="Microsoft.Office.Audit.Schema.SharePoint.[EventSource](#eventsource)"|Non|Identifie qu’un événement s’est produit dans SharePoint. Valeurs possibles : **SharePoint** ou **ObjectModel**.|
|SourceName|Edm.String|Non|Entité qui a déclenché l’opération auditée. Valeurs possibles : SharePoint ou **ObjectModel**.|
|UserAgent|Edm.String|Non|Informations sur le navigateur ou le client de l’utilisateur. Ces informations sont fournies par le navigateur ou le client.|
|MachineDomainInfo|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|Non|Informations sur les opérations de synchronisation de périphérique. Ces informations sont signalées uniquement si elles figurent dans la demande.|
|MachineId|Edm.String Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"|Non|Informations sur les opérations de synchronisation de périphérique. Ces informations sont signalées uniquement si elles figurent dans la demande.|
|||||

### <a name="enum-itemtype---type-edmint32"></a>Énumération : ItemType - Type : Edm.Int32

#### <a name="itemtype"></a>ItemType

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|Invalid|L’élément n’est d’aucun des autres types d’éléments (qui sont répertoriés dans ce tableau).|
|1|File|L’élément est un fichier.|
|5|Folder|L’élément est un dossier.|
|6|Web|L’élément est de type web.|
|7|Site|L’élément est un site.|
|8|Tenant|L’élément est un client.|
|9|DocumentLibrary|L’élément est une bibliothèque de documents.|
|11|Page|L’élément est une page.|
||||

### <a name="enum-eventsource---type-edmint32"></a>Énumération : EventSource - Type : Edm.Int32

#### <a name="eventsource"></a>EventSource

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|SharePoint|La source de l’événement est SharePoint.|
|1|ObjectModel|La source de l’événement est ObjectModel.|
||||


### <a name="enum-sharepointauditoperation---type-edmint32"></a>Énumération : SharePointAuditOperation - Type : Edm.Int32

|**Nom du membre**|**Description**|
|:-----|:-----|
|AccessInvitationAccepted*|Le destinataire d’une invitation à afficher ou à modifier un fichier (ou dossier) partagé a accédé au fichier partagé en cliquant sur le lien dans l’invitation.|
|AccessInvitationCreated*|L’utilisateur envoie une invitation à une autre personne (interne ou externe à son organisation) pour afficher ou modifier un fichier ou dossier partagé sur un site SharePoint ou OneDrive Entreprise. Les détails de l’entrée d’événement identifient le nom du fichier qui a été partagé, l’utilisateur auquel l’invitation a été envoyée et le type d’autorisation de partage sélectionnée par la personne qui a envoyé l’invitation.|
|AccessInvitationExpired*|Une invitation envoyée à un utilisateur externe expire. Par défaut, une invitation envoyée à un utilisateur extérieur à votre organisation expire au bout de 7 jours si elle n’est pas acceptée.|
|AccessInvitationRevoked*|L’administrateur de site ou le propriétaire d’un site ou d’un document dans SharePoint ou OneDrive Entreprise retire une invitation qui a été envoyée à un utilisateur en dehors de votre organisation. Une invitation peut être retirée uniquement avant d’être acceptée.|
|AccessInvitationUpdated*|L’utilisateur qui a créé et envoyé une invitation à une autre personne pour afficher ou modifier un fichier (ou dossier) partagé sur un site SharePoint ou OneDrive Entreprise renvoie l’invitation.|
|AccessRequestApproved|L’administrateur ou le propriétaire d’un site ou d’un document dans SharePoint ou OneDrive Entreprise approuve la demande d’accès au site ou au document.|
|AccessRequestCreated|L’utilisateur demande l’accès à un site ou à un document dans SharePoint ou OneDrive Entreprise auquel ils n’est pas autorisé à accéder. |
|AccessRequestRejected*|L’administrateur de site ou le propriétaire d’un site ou d’un document dans SharePoint refuse la demande d’un utilisateur à accéder au site ou au document.|
|ActivationEnabled*|Les utilisateurs peuvent activer les modèles de formulaires pour le navigateur qui ne contiennent pas de code de formulaire, qui nécessitent une autorisation totale, qui activent le rendu sur un appareil mobile ou qui utilisent une connexion de données gérée par un administrateur de serveurs.|
|AdministratorAddedToTermStore*|Ajout d’un administrateur de magasin de termes.|
|AdministratorDeletedFromTermStore*|Suppression d’un administrateur de magasin de termes.|
|AllowGroupCreationSet*|Le propriétaire ou l’administrateur de site ajoute un niveau d’autorisation à un site SharePoint ou OneDrive Entreprise qui permet aux utilisateurs auxquels cette autorisation est affectée de créer un groupe pour ce site.|
|AppCatalogCreated*|Création d’un catalogue d’applications pour mettre à disposition des applications d’entreprise personnalisées pour votre environnement SharePoint.|
|AuditPolicyRemoved*|Stratégie de cycle de vie de document supprimée pour une collection de sites.|
|AuditPolicyUpdate*|Stratégie de cycle de vie de document mise à jour pour une collection de sites.|
|AzureStreamingEnabledSet*|Le propriétaire d’un portail vidéo a autorisé la diffusion en continu de vidéos à partir d’Azure.|
|CollaborationTypeModified*|Le type de collaboration autorisé sur les sites (par exemple, intranet, extranet ou public) a été modifié.|
|ConnectedSiteSettingModified|L’utilisateur a créé, modifié ou supprimé le lien entre un projet et un site de projets, ou il a modifié le paramètre de synchronisation sur le lien dans Project Web App.|
|CreateSSOApplication*|Application cible créée dans le service Banque d’informations sécurisé.|
|CustomFieldOrLookupTableCreated|L’utilisateur a créé un champ personnalisé, ou un élément ou une table de choix dans Project Web App.|
|CustomFieldOrLookupTableDeleted|L’utilisateur a supprimé un champ personnalisé, ou un élément ou une table de choix dans Project Web App.|
|CustomFieldOrLookupTableModified|L’utilisateur a modifié un champ personnalisé, ou un élément ou une table de choix dans Project Web App.|
|CustomizeExemptUsers*|L’administrateur général a personnalisé la liste des agents utilisateurs exemptés dans le Centre d’administration SharePoint. Vous pouvez spécifier les agents utilisateurs à exempter de la réception d’une page web entière à indexer. Cela signifie que lorsqu’un agent utilisateur que vous avez spécifié comme exempté rencontre un formulaire InfoPath, le formulaire est renvoyé sous la forme d’un fichier XML au lieu d’une page web entière. Cela permet d’accélérer l’indexation des formulaires InfoPath.|
|DefaultLanguageChangedInTermStore*|Paramètre de langue modifié dans le magasin de termes.|
|DelegateModified|Un utilisateur a créé ou modifié un délégué de sécurité dans Project Web App.|
|DelegateRemoved|Un utilisateur a supprimé un délégué de sécurité dans Project Web App.|
|DeleteSSOApplication*|Une application SSO a été supprimée.|
|eDiscoveryHoldApplied*|Une conservation inaltérable a été placée sur une source de contenu. Les conservations inaltérables sont gérées à l’aide d’une collection de sites eDiscovery (par exemple, le centre eDiscovery) dans SharePoint.|
|eDiscoveryHoldRemoved*|Une conservation inaltérable a été supprimée d’une source de contenu. Les conservations inaltérables sont gérées à l’aide d’une collection de sites eDiscovery (par exemple, le centre eDiscovery) dans SharePoint.|
|eDiscoverySearchPerformed*|Une recherche eDiscovery a été effectuée à l’aide d’une collection de sites eDiscovery dans SharePoint.|
|EngagementAccepted|Un utilisateur accepte un engagement de ressources dans Project Web App.|
|EngagementModified|Un utilisateur modifie un engagement de ressources dans Project Web App.|
|EngagementRejected|Un utilisateur rejette un engagement de ressources dans Project Web App.|
|EnterpriseCalendarModified|Un utilisateur copie, modifie ou supprime un calendrier d’entreprise dans Project Web App.|
|EntityDeleted|Un utilisateur supprime une feuille de temps dans Project Web App.|
|EntityForceCheckedIn|Un utilisateur force l’archivage d’un calendrier, d’un champ personnalisé ou d’une table de choix dans Project Web App.|
|ExemptUserAgentSet*|L’administrateur général ajoute un agent utilisateur à la liste des agents utilisateurs exemptés dans le Centre d’administration SharePoint.|
|FileAccessed|Un compte d’utilisateur ou système accède à un fichier sur un site SharePoint ou OneDrive Entreprise. Les comptes système peuvent également générer des événements FileAccessed.|
|FileCheckOutDiscarded*|Un utilisateur ignore (ou annule) un fichier extrait. Les modifications qu’il a apportées au fichier le temps de son extraction sont ignorées et ne sont pas enregistrées dans la version du document dans la bibliothèque de documents.|
|FileCheckedIn*|Un utilisateur archive un document qu’il a extrait à partir d’une bibliothèque de documents SharePoint ou OneDrive Entreprise.|
|FileCheckedOut*|Un utilisateur extrait un document situé dans une bibliothèque de documents SharePoint ou OneDrive Entreprise. Les utilisateurs peuvent extraire et apporter des modifications aux documents partagés avec eux.|
|FileCopied|Un utilisateur copie un document à partir d’un site SharePoint ou OneDrive Entreprise. Le fichier copié peut être enregistré dans un autre dossier sur le site.|
|FileDeleted|Un utilisateur supprime un document à partir d’un site SharePoint ou OneDrive Entreprise.|
|FileDeletedFirstStageRecycleBin|Un utilisateur supprime un fichier à partir de la corbeille sur un site SharePoint ou OneDrive Entreprise.|
|FileDeletedSecondStageRecycleBin|Un utilisateur supprime un fichier dans la corbeille secondaire sur un site SharePoint ou OneDrive Entreprise.|
|FileDownloaded|Un utilisateur télécharge un document à partir d’un site SharePoint ou OneDrive Entreprise.|
|FileFetched|Cet événement a été remplacé par l’événement FileAccessed et a été déconseillé.|
|FileModified|Un compte d’utilisateur ou système modifie le contenu ou les propriétés d’un document situé sur un site SharePoint ou OneDrive Entreprise.|
|FileMoved|Un utilisateur déplace un document de son emplacement actuel sur un site SharePoint ou OneDrive Entreprise vers un nouvel emplacement.|
|FilePreviewed|Un utilisateur affiche l’aperçu d’un document sur un site SharePoint ou OneDrive Entreprise.|
|FileRenamed|Un utilisateur renomme un document sur un site SharePoint ou OneDrive Entreprise.|
|FileRestored|Un utilisateur restaure un document à partir de la corbeille d’un site SharePoint ou OneDrive Entreprise. |
|FileSyncDownloadedFull|Un utilisateur établit une relation de synchronisation et télécharge des fichiers pour la première fois sur son ordinateur à partir d’une bibliothèque de documents SharePoint ou OneDrive Entreprise.|
|FileSyncDownloadedPartial|Un utilisateur télécharge les modifications apportées aux fichiers à partir d’une bibliothèque de documents SharePoint ou OneDrive Entreprise. Cet événement indique que les modifications qui ont été apportées aux fichiers dans la bibliothèque de documents ont été téléchargées sur l’ordinateur de l’utilisateur. Seules les modifications ont été téléchargées, car la bibliothèque de documents a été téléchargée précédemment par l’utilisateur (comme indiqué par l’événement FileSyncDownloadedFull).|
|FileSyncUploadedFull*|Un utilisateur établit une relation de synchronisation et charge des fichiers pour la première fois de son ordinateur dans une bibliothèque de documents SharePoint ou OneDrive Entreprise.|
|FileSyncUploadedPartial*|Un utilisateur charge les modifications apportées aux fichiers dans une bibliothèque de documents SharePoint ou OneDrive Entreprise. Cet événement indique que les modifications apportées à la version locale d’un fichier dans une bibliothèque de documents sont correctement chargées dans la bibliothèque de documents. Seules les modifications sont chargées, car ces fichiers ont été précédemment chargés par l’utilisateur (comme indiqué par l’événement FileSyncUploadedFull).|
|FileUploaded|Un utilisateur charge un document dans un dossier sur un site SharePoint ou OneDrive Entreprise. |
|FileViewed|Cet événement a été remplacé par l’événement FileAccessed et a été déconseillé.|
|FolderCopied|Un utilisateur copie un dossier à partir d’un site SharePoint ou OneDrive Entreprise vers un autre emplacement dans SharePoint ou OneDrive Entreprise.|
|FolderCreated|Un utilisateur crée un dossier sur un site SharePoint ou OneDrive Entreprise.|
|FolderDeleted|Un utilisateur supprime un dossier sur un site SharePoint ou OneDrive Entreprise.|
|FolderDeletedFirstStageRecycleBin|Un utilisateur supprime un dossier à partir de la corbeille sur un site SharePoint ou OneDrive Entreprise.|
|FolderDeletedSecondStageRecycleBin|Un utilisateur supprime un dossier dans la corbeille secondaire sur un site SharePoint ou OneDrive Entreprise.|
|FolderModified|Un utilisateur modifie un dossier sur un site SharePoint ou OneDrive Entreprise. Cet événement inclut les modifications de métadonnées de dossier, telles que les balises et les propriétés.|
|FolderMoved|Un utilisateur déplace un dossier à partir d’un site SharePoint ou OneDrive Entreprise.|
|FolderRenamed|Un utilisateur renomme un dossier sur un site SharePoint ou OneDrive Entreprise.|
|FolderRestored|Un utilisateur restaure un dossier à partir de la corbeille sur un site SharePoint ou OneDrive Entreprise.|
|GroupAdded*|Le propriétaire ou l’administrateur de site crée un groupe pour un site SharePoint ou OneDrive Entreprise, ou effectue une tâche qui entraîne la création d’un groupe. Par exemple, la première fois qu’un utilisateur crée un lien pour partager un fichier, un groupe système est ajouté au site OneDrive Entreprise de l’utilisateur. Cet événement peut également être le résultat de la création d’un lien par un utilisateur avec autorisation de modification sur un fichier partagé.|
|GroupRemoved*|Un utilisateur supprime un groupe d’un site SharePoint ou OneDrive Entreprise. |
|GroupUpdated*|Le propriétaire ou l’administrateur de site modifie les paramètres d’un groupe pour un site SharePoint ou OneDrive Entreprise. Cela peut inclure la modification du nom du groupe, qui peut consulter ou modifier l’appartenance au groupe et la gestion des demandes d’appartenance.|
|LanguageAddedToTermStore*|Langue ajoutée au magasin de termes.|
|LanguageRemovedFromTermStore*|Langue supprimée du magasin de termes.|
|LegacyWorkflowEnabledSet*|Le propriétaire ou l’administrateur du site ajoute le type de contenu de tâche de flux de travail SharePoint au site. Les administrateurs généraux peuvent également activer les workflows pour l’ensemble de l’organisation dans le Centre d’administration SharePoint.|
|LookAndFeelModified|Un utilisateur modifie un menu de lancement rapide, les formats de diagramme de Gantt ou les formats de groupe. Ou l’utilisateur crée, modifie ou supprime un affichage dans Project Web App.|
|ManagedSyncClientAllowed|Un utilisateur a établi une relation de synchronisation avec un site SharePoint ou OneDrive Entreprise. La relation de synchronisation est établie, car l’ordinateur de l’utilisateur est membre d’un domaine qui a été ajouté à la liste de domaines (« liste des destinataires approuvés ») qui peuvent accéder aux bibliothèques de documents de votre organisation. Pour plus d’informations sur cette fonctionnalité, reportez-vous à l’article [Utilisation des cmdlet Windows PowerShell pour activer la synchronisation de OneDrive pour les domaines figurant dans la liste des destinataires approuvés](http://go.microsoft.com/fwlink/p/?LinkID=534609).|
|MaxQuotaModified*|Le quota maximal pour un site a été modifié.|
|MaxResourceUsageModified*|L’utilisation de ressources maximale autorisée pour un site a été modifiée.|
|MySitePublicEnabledSet*|L’indicateur permettant aux utilisateurs de rendre public un site Mon site a été défini par l’administrateur SharePoint.|
|NewsFeedEnabledSet*|Le propriétaire ou l’administrateur de site active les flux RSS pour un site SharePoint ou OneDrive Entreprise. Les administrateurs généraux peuvent activer les flux RSS pour l’ensemble de l’organisation dans le Centre d’administration SharePoint.|
|ODBNextUXSettings*|Une nouvelle interface utilisateur pour OneDrive Entreprise a été activée.|
|OfficeOnDemandSet*|L’administrateur de site active Office à la demande, qui permet aux utilisateurs d’accéder à la dernière version des applications de bureau Office. « Office à la demande » est activé dans le Centre d’administration SharePoint et nécessite un abonnement Office 365 qui inclut l’installation de l’ensemble des applications Office.|
|PageViewed|Un utilisateur consulte une page sur un site SharePoint ou OneDrive Entreprise. Ceci n’inclut pas l’affichage des fichiers de bibliothèque de documents à partir d’un site SharePoint ou OneDrive Entreprise sur un navigateur.|
|PeopleResultsScopeSet*|L’administrateur de site crée ou modifie l’origine des résultats pour les recherches de personnes pour un site SharePoint.|
|PermissionSyncSettingModified|Un utilisateur modifie les paramètres de synchronisation d’autorisation de projet dans Project Web App.|
|PermissionTemplateModified|Un utilisateur crée, modifie ou supprime un modèle d’autorisation dans Project Web App.|
|PortfolioDataAccessed|Un utilisateur accède au contenu du portefeuille (bibliothèque de pilotes, classement par ordre de priorité des pilotes, analyses de portefeuille) dans Project Web App.|
|PortfolioDataModified|Un utilisateur crée, modifie ou supprime des données de portefeuille (bibliothèque de pilotes, classement par ordre de priorité des pilotes, analyses de portefeuille) dans Project Web App.|
|PreviewModeEnabledSet*|L’administrateur de site active l’aperçu de document pour un site SharePoint.|
|ProjectAccessed|Un utilisateur accède au contenu d’un projet dans Project Web App.|
|ProjectCheckedIn|Un utilisateur archive un projet qu’il a extrait de Project Web App.|
|ProjectCheckedOut|Un utilisateur extrait un projet situé dans Project Web App. Les utilisateurs peuvent extraire les projets qu’ils sont autorisés à ouvrir et y apporter des modifications .|
|ProjectCreated|Un utilisateur crée un projet dans Project Web App.|
|ProjectDeleted|Un utilisateur supprime un projet dans Project Web App.|
|ProjectForceCheckedIn|Un utilisateur force l’archivage d’un projet dans Project Web App.|
|ProjectModified|Un utilisateur modifie un projet dans Project Web App.|
|ProjectPublished|Un utilisateur publie un projet dans Project Web App.|
|ProjectWorkflowRestarted|Un utilisateur redémarre un flux de travail dans Project Web App.|
|PWASettingsAccessed|Un utilisateur accède aux paramètres de Project Web App via le modèle CSOM.|
|PWASettingsModified|Un utilisateur modifie une configuration de Project Web App.|
|QueueJobStateModified|Un utilisateur annule ou redémarre un travail de file d’attente dans Project Web App.|
|QuotaWarningEnabledModified*|Avertissement de quota de stockage modifié.|
|RenderingEnabled*|Les modèles de formulaires compatibles avec les navigateurs web seront rendus par les services des formulaires InfoPath.|
|ReportingAccessed|Un utilisateur a accédé au point de terminaison de génération de rapports dans Project Web App.|
|ReportingSettingModified|Un utilisateur modifie la configuration de la génération de rapports dans Project Web App.|
|ResourceAccessed|Un utilisateur accède au contenu d’une ressource d’entreprise dans Project Web App.|
|ResourceCheckedIn|Un utilisateur archive une ressource d’entreprise qu’il a extrait de Project Web App.|
|ResourceCheckedOut|Un utilisateur extrait une ressource d’entreprise située dans Project Web App.|
|ResourceCreated|Un utilisateur crée une ressource d’entreprise dans Project Web App.|
|ResourceDeleted|Un utilisateur supprime une ressource d’entreprise dans Project Web App.|
|ResourceForceCheckedIn|Un utilisateur force l’archivage d’une ressource d’entreprise dans Project Web App.|
|ResourceModified|Un utilisateur modifie une ressource d’entreprise dans Project Web App.|
|ResourcePlanCheckedInOrOut|Un utilisateur archive ou extrait un plan des ressources dans Project Web App.|
|ResourcePlanModified|Un utilisateur modifie un plan des ressources dans Project Web App.|
|ResourcePlanPublished|Un utilisateur publie un plan des ressources dans Project Web App.|
|ResourceRedacted|Un utilisateur rédige une ressource d’entreprise supprimant toutes les informations personnelles dans Project Web App.|
|ResourceWarningEnabledModified*|Avertissement de quota de ressource modifié.|
|SSOGroupCredentialsSet*|Informations d’identification de groupe définies dans le service Banque d’informations sécurisé.|
|SSOUserCredentialsSet*|Informations d’identification utilisateur définies dans le service Banque d’informations sécurisé.|
|SearchCenterUrlSet*|URL du Centre de recherche définie.|
|SecondaryMySiteOwnerSet*|Un utilisateur a ajouté un propriétaire secondaire à son site Mon site.|
|SecurityCategoryModified|Un utilisateur crée, modifie ou supprime une catégorie de sécurité dans Project Web App.|
|SecurityGroupModified|Un utilisateur crée, modifie ou supprime un groupe de sécurité dans Project Web App.|
|SendToConnectionAdded*|L’administrateur général crée une nouvelle connexion Envoyer à sur la page de gestion des enregistrements dans le Centre d’administration SharePoint. Une connexion Envoyer à spécifie les paramètres pour un référentiel de documents ou un centre des enregistrements. Lorsque vous créez une connexion Envoyer à, un organisateur de contenu peut soumettre des documents à l’emplacement spécifié.|
|SendToConnectionRemoved*|L’administrateur général supprime une connexion Envoyer à sur la page de gestion des enregistrements dans le Centre d’administration SharePoint.|
|SharedLinkCreated|Un utilisateur crée un lien vers un fichier partagé sur un site SharePoint ou OneDrive Entreprise. Ce lien peut être envoyé à d’autres personnes pour leur donner accès au fichier. Un utilisateur peut créer deux types de liens : un lien qui permet à la personne d’afficher et de modifier le fichier partagé, ou un lien qui permet à la personne d’afficher le fichier uniquement.|
|SharedLinkDisabled*|Un utilisateur désactive (définitivement) un lien qui a été créé pour partager un fichier.|
|SharingInvitationAccepted *|Un utilisateur accepte une invitation à partager un fichier ou un dossier. Cet événement est enregistré lorsqu’un utilisateur partage un fichier avec d’autres utilisateurs.|
|SharingRevoked*|L’utilisateur annule le partage d’un fichier ou d’un dossier qui a été précédemment partagé avec d’autres utilisateurs. Cet événement est enregistré lorsqu’un utilisateur arrête le partage d’un fichier avec d’autres utilisateurs.|
|SharingSet|Un utilisateur partage un fichier ou un dossier situé dans SharePoint ou OneDrive Entreprise avec un autre utilisateur au sein de son organisation.|
|SiteAdminChangeRequest*|Un utilisateur demande à être ajouté en tant qu’administrateur de collection de sites pour une collection de sites SharePoint. Les administrateurs de collection de sites disposent du niveau d’autorisation Contrôle total sur la collection de sites et tous les sous-sites.|
|SiteCollectionAdminAdded*|Le propriétaire ou l’administrateur de collection de sites ajoute une personne en tant qu’administrateur de collection de sites pour un site SharePoint ou OneDrive Entreprise. Les administrateurs de collection de sites disposent du niveau d’autorisation Contrôle total sur la collection de sites et tous les sous-sites.|
|SiteCollectionCreated*| L’administrateur général crée une nouvelle collection de sites dans votre organisation SharePoint.|
|SiteRenamed*|Le propriétaire ou l’administrateur de site renomme un site SharePoint ou OneDrive Entreprise.|
|StatusReportModified|Un utilisateur crée, modifie ou supprime un rapport d’état dans Project Web App.|
|SyncGetChanges*|Un utilisateur clique sur **Sync** dans la barre d’état d’action dans SharePoint ou OneDrive Entreprise pour synchroniser les modifications éventuelles à classer dans une bibliothèque de documents sur son ordinateur.|
|TaskStatusAccessed|Un utilisateur accède à l’état d’une ou de plusieurs tâches dans Project Web App.|
|TaskStatusApproved|Un utilisateur approuve une mise à jour de l’état d’une ou de plusieurs tâches dans Project Web App.|
|TaskStatusRejected|Un utilisateur rejette une mise à jour de l’état d’une ou de plusieurs tâches dans Project Web App.|
|TaskStatusSaved|Un utilisateur enregistre une mise à jour de l’état d’une ou de plusieurs tâches dans Project Web App.|
|TaskStatusSubmitted|Un utilisateur soumet une mise à jour de l’état d’une ou de plusieurs tâches dans Project Web App.|
|TimesheetAccessed|Un utilisateur accède à une feuille de temps dans Project Web App.|
|TimesheetApproved|Un utilisateur approuve une feuille de temps dans Project Web App.|
|TimesheetRejected|Un utilisateur rejette une feuille de temps dans Project Web App.|
|TimesheetSaved|Un utilisateur enregistre une feuille de temps dans Project Web App.|
|TimesheetSubmitted|Un utilisateur soumet une feuille de temps de l’état dans Project Web App.|
|UnmanagedSyncClientBlocked|Un utilisateur tente d’établir une relation de synchronisation avec un site SharePoint ou OneDrive Entreprise sur un ordinateur qui n’est pas membre du domaine de votre organisation ou qui est membre d’un domaine qui n’a pas été ajouté à la liste des domaines (appelée liste des destinataires approuvés) pouvant accéder aux bibliothèques de documents dans votre organisation. La relation de synchronisation n’est pas autorisée et l’ordinateur de l’utilisateur est bloqué en matière de synchronisation, de téléchargement ou de chargement de fichiers dans une bibliothèque de documents. Pour plus d’informations sur cette fonctionnalité, reportez-vous à l’article [Utilisation des cmdlet Windows PowerShell pour activer la synchronisation de OneDrive pour les domaines figurant dans la liste des destinataires approuvés](https://docs.microsoft.com/en-us/powershell/module/sharepoint-online/index?view=sharepoint-ps).|
|UpdateSSOApplication*|Application cible mise à jour dans le service Banque d’informations sécurisé.|
|UserAddedToGroup*|Le propriétaire ou l’administrateur de site ajoute une personne à un groupe sur un site SharePoint ou OneDrive Entreprise. Ajouter une personne à un groupe accorde à l’utilisateur les autorisations qui ont été affectées au groupe. |
|UserRemovedFromGroup*|Le propriétaire ou l’administrateur de site supprime une personne d’un groupe sur un site SharePoint ou OneDrive Entreprise. Une fois que la personne est supprimée, elle ne dispose plus des autorisations qui ont été affectées au groupe. |
|WorkflowModified|Un utilisateur crée, modifie ou supprime un type de projet d’entreprise, ou des étapes ou phases de flux de travail dans Project Web App.|
|||||


> [!NOTE] 
> *Cette opération est en version d’évaluation.



## <a name="sharepoint-file-operations"></a>Opérations de fichier SharePoint

Les événements SharePoint relatifs aux fichiers répertoriés dans la section « Activités de fichiers et de dossiers » dans l’article relatif à la [recherche dans le journal d’audit dans le Centre de sécurité et conformité d’Office 365](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&amp;rs=en-US&amp;ad=US) utilisent ce schéma.



|**Paramètre**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|SiteUrl|Edm.String|Oui|URL du site où se trouve le fichier ou le dossier consulté par l’utilisateur.|
|SourceRelativeUrl|Edm.String|Non|URL du dossier contenant le fichier consulté par l’utilisateur. La combinaison des valeurs pour les paramètres _SiteURL_, _SourceRelativeURL_ et _SourceFileName_ est identique à la valeur de la propriété **ObjectID**, qui est le nom du chemin d’accès complet au fichier consulté par l’utilisateur.|
|SourceFileName|Edm.String|Oui|Nom du fichier ou du dossier consulté par l’utilisateur.|
|SourceFileExtension|Edm.String|Non|Extension du fichier consulté par l’utilisateur. Cette propriété est vide si l’objet consulté est un dossier.|
|DestinationRelativeUrl|Edm.String|Non|URL du dossier de destination dans lequel un fichier est copié ou déplacé. La combinaison des valeurs pour les paramètres _SiteURL_, _DestinationRelativeURL_ et _DestinationFileName_ est identique à la valeur de la propriété **ObjectID**, qui est le nom du chemin d’accès complet au fichier qui a été copié. Cette propriété s’affiche uniquement pour les événements FileCopied et FileMoved.|
|DestinationFileName|Edm.String|Non|Nom du fichier qui est copié ou déplacé. Cette propriété s’affiche uniquement pour les événements FileCopied et FileMoved.|
|DestinationFileExtension|Edm.String|Non|Extension du fichier qui est copié ou déplacé. Cette propriété s’affiche uniquement pour les événements FileCopied et FileMoved.|
|UserSharedWith|Edm.String|Non|Utilisateur avec lequel une ressource a été partagée.|
|SharingType|Edm.String|Non|Type des autorisations de partage qui ont été affectées à l’utilisateur avec lequel la ressource a été partagée. Cet utilisateur est identifié par le paramètre _UserSharedWith_.|
|||||


## <a name="sharepoint-sharing-schema"></a>Schéma de partage SharePoint

 Événements SharePoint relatifs au partage de fichier. Il s’agit de différents événements relatifs aux fichiers et aux dossiers dans lesquels un utilisateur effectue une action qui a certains effets sur un autre utilisateur. Pour plus d’informations sur le schéma de partage SharePoint, reportez-vous à l’article relatif à l’[utilisation du partage de l’audit dans le journal d’audit Office 365](https://support.office.com/en-us/article/Use-sharing-auditing-in-the-Office-365-audit-log-50bbf89f-7870-4c2a-ae14-42635e0cfc01?ui=en-US&amp;rs=en-US&amp;ad=US).



|**Paramètre**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|TargetUserOrGroupName |Edm.String|Non|Stocke le nom d’utilisateur principal (UPN), ou le nom du groupe ou de l’utilisateur cible avec lequel une ressource a été partagée.|
|TargetUserOrGroupType|Edm.String|Non|Détermine si le groupe ou l’utilisateur cible est un membre, un invité, un groupe ou un partenaire. |
|EventData|Code XML|Non|Indique les informations de suivi concernant l’action de partage qui s’est produite. Par exemple, l’ajout d’un utilisateur à un groupe ou l’octroi d’autorisations de modification.|
|||||


## <a name="sharepoint-schema"></a>Schéma SharePoint

Les événements SharePoint répertoriés dans l’article relatif à la [recherche dans le journal d’audit dans le Centre de sécurité et conformité d’Office 365](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&amp;rs=en-US&amp;ad=US) (sans compter les événements de fichiers et de dossiers) utilisent ce schéma.


|**Paramètre**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|CustomEvent|Edm.String|Non|Chaîne facultative pour les événements personnalisés.|
|EventData|Edm.String|Non|Charge utile facultative pour les événements personnalisés.|
|ModifiedProperties|Collection(ModifiedProperty)|Non|La propriété est incluse pour les événements d’administration, par exemple l’ajout d’un utilisateur en tant que membre d’un site ou d’un groupe d’administration d’une collection de sites. La propriété inclut le nom de la propriété modifiée (par exemple, le groupe d’administrateurs du site), la nouvelle valeur de la propriété modifiée (comme l’utilisateur qui a été ajouté en tant qu’administrateur du site) et la valeur précédente de l’objet modifié.|
|||||

## <a name="project-schema"></a>Schéma Project

|**Paramètre**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Entity|Edm.String|Oui| [ProjectEntity](#project-entity) pour laquelle l’audit a été effectué.|
|Action|Edm.String|Oui|[ProjectAction](#project-action) qui a été effectuée.|
|OnBehalfOfResId|Edm.Guid|Non|ID de ressource au nom duquel l’action a été effectuée.|
|||||

### <a name="enum-project-action---type-edmint32"></a>Énumération : Project Action - Type : Edm.Int32

#### <a name="project-action"></a>Action de projet

|**Nom du membre**|**Description**|
|:-----|:-----|
|Accepted|L’utilisateur a accepté un événement ou un flux de travail.|
|Accessed|L’utilisateur a accédé à une entité.|
|Activated|L’utilisateur a activé une entité, un événement ou un flux de travail.|
|Cancelled|L’utilisateur a annulé un événement ou un flux de travail.|
|CheckedIn|L’utilisateur a archivé une entité.|
|CheckedOut|L’utilisateur a extrait une entité.|
|Copied|L’utilisateur a copié une entité.|
|Created|L’utilisateur a créé une entité.|
|Deactivated|L’utilisateur a désactivé une entité.|
|Deleted|L’utilisateur a supprimé une entité.|
|Exported|L’utilisateur a exporté une entité.|
|ForceCheckedIn|L’utilisateur a forcé l’archivage d’une entité.|
|Modified|L’utilisateur a modifié une entité.|
|Published|L’utilisateur a publié une entité.|
|Redacted|L’utilisateur a rédigé une entité.|
|Rejected|L’utilisateur a rejeté une entité.|
|Restarted|L’utilisateur a redémarré un événement ou un flux de travail.|
|Saved|L’utilisateur a enregistré une entité.|
|Sent|L’utilisateur a envoyé une entité.|
|Submitted|L’utilisateur a soumis une entité pour révision ou un flux de travail.|
|||||

### <a name="enum-project-entity---type-edmint32"></a>Énumération : Project Entity - Type : Edm.Int32

#### <a name="project-entity"></a>Entité de projet

|**Nom du membre**|**Description**|
|:-----|:-----|
|CustomField|Représente un champ personnalisé d’entreprise.|
|Driver|Représente un pilote de portefeuille.|
|DriverPrioritization|Représente une définition de priorités de portefeuille.|
|Engagement|Représente un engagement de ressources.|
|EnterpriseCalendar|Représente un calendrier des ressources d’entreprise.|
|EnterpriseProjectType|Représente un type de projet d’entreprise.|
|FiscalPeriod|Représente une période fiscale.|
|GanttChartFormat|Représente un format de diagramme de Gantt.|
|GroupingFormat|Représente un format de regroupement d’affichage.|
|LineClassification|Représente une classification de ligne de feuille de temps.|
|LookupTable|Représente une table de choix d’entreprise.|
|PermissionTemplate|Représente un modèle d’autorisation de sécurité.|
|PortfolioAnalysis|Représente une analyse de portefeuille.|
|Project|Représente un projet.|
|QueueJob|Représente un travail de file d’attente.|
|QuickLaunch|Représente un élément de lancement rapide.|
|Reporting|Représente le point de terminaison de génération de rapports.|
|Resource|Représente une ressource d’entreprise.|
|ResourcePlan|Représente un plan des ressources associé à un projet.|
|SecurityCategory|Représente une catégorie de sécurité.|
|SecurityGroup|Représente un groupe de sécurité.|
|Setting|Représente un paramètre Project Web App.|
|Statusing|Représente une mise à jour de l’état de tâche.|
|StatusReport|Représente un rapport d’état.|
|TimeReportingPeriod|Représente une période pour une feuille de temps.|
|Timesheet|Représente une entité de feuille de temps.|
|TimesheetAuditLog|Représente un journal d’audit de feuille de temps.|
|TimesheetManager|Représente le gestionnaire d’une feuille de temps.|
|UserDelegate|Représente une délégation d’utilisateur pour un autre utilisateur.|
|View|Représente une définition de l’affichage.|
|WorkflowPhase|Représente une phase dans un flux de travail.|
|WorkflowStage|Représente une étape dans un flux de travail.|
|||||

## <a name="exchange-admin-schema"></a>Schéma d’administration Exchange


|**Paramètres**|**Type**|**Obligatoire**|**Description**|
|:-----|:-----|:-----|:-----|
|ModifiedObjectResolvedName|Edm.String|Non|Il s’agit du nom convivial de l’objet modifié par la cmdlet. Ce paramètre est enregistré uniquement si la cmdlet modifie l’objet.|
|Paramètres|Collection(Common.NameValuePair)|Non|Nom et valeur de tous les paramètres utilisés avec la cmdlet identifiée dans la propriété Operations.|
|ModifiedProperties|Collection(Common.ModifiedProperty)|Non|Propriété incluse pour les événements d’administration. La propriété inclut le nom de la propriété modifiée, la nouvelle valeur de la propriété modifiée et la valeur précédente de l’objet modifié.|
|ExternalAccess|Edm.Boolean|Oui|Spécifie si la cmdlet a été exécutée par un utilisateur dans votre organisation, par le personnel du centre de données Microsoft ou par un compte de service du centre de données, ou par un administrateur délégué. La valeur **False** indique que la cmdlet a été exécutée par un membre de votre organisation. La valeur **True** indique que la cmdlet a été exécutée par le personnel du centre de données, un compte de service du centre de données ou un administrateur délégué.|
|OriginatingServer|Edm.String|Non|Nom du serveur à partir duquel la cmdlet a été exécutée.|
|OrganizationName|Edm.String|Non|Nom du client.|
|||||

## <a name="exchange-mailbox-schema"></a>Schéma de boîte aux lettres Exchange


|**Paramètres**|**Type**|**Obligatoire**|**Description**|
|:-----|:-----|:-----|:-----|
|LogonType|Self.[LogonType](#logontype)|Non| Indique le type d’utilisateur ayant accédé à la boîte aux lettres et effectué l’opération qui a été enregistrée.|
|InternalLogonType|Self.[LogonType](#logontype)|Non|Réservé à une utilisation interne.|
|MailboxGuid|Edm.String|Non|GUID Exchange de la boîte aux lettres consultée.|
|MailboxOwnerUPN|Edm.String|Non|Adresse de messagerie du propriétaire de la boîte aux lettres consultée.|
|MailboxOwnerSid|Edm.String|Non|SID du propriétaire de la boîte aux lettres.|
|MailboxOwnerMasterAccountSid|Edm.String|Non|SID du compte principal du compte du propriétaire de la boîte aux lettres.|
|LogonUserSid|Edm.String|Non|SID de l’utilisateur ayant effectué l’opération.|
|LogonUserDisplayName|Edm.String|Non|Nom convivial de l’utilisateur ayant effectué l’opération.|
|ExternalAccess|Edm.Boolean|Oui|La valeur est True si le domaine de l’utilisateur de connexion est différent du domaine du propriétaire de la boîte aux lettres.|
|OriginatingServer |Edm.String|Non|Il s’agit de l’emplacement où l’opération a été lancée.|
|OrganizationName|Edm.String|Non|Nom du client.|
|ClientInfoString|Edm.String|Non|Informations sur le client de messagerie que vous avez utilisé pour effectuer l’opération, comme la version d’un navigateur, la version d’Outlook et les informations d’appareil mobile.|
|ClientIPAddress|Edm.String|Non|Adresse IP du périphérique utilisé lors de la journalisation de l’opération. L’adresse IP apparaît au format IPv4 ou IPv6.|
|ClientMachineName|Edm.String|Non|Nom de l’ordinateur qui héberge le client Outlook.|
|ClientProcessName|Edm.String|Non|Client de messagerie que vous avez utilisé pour accéder à la boîte aux lettres. |
|ClientVersion|Edm.String|Non|Version du client de messagerie.|
|||||

### <a name="enum-logontype---type-edmint32"></a>Énumération : LogonType - Type : Edm.Int32

#### <a name="logontype"></a>LogonType


|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|Owner|Propriétaire de la boîte aux lettres.|
|1|Admin|Personne disposant des privilèges d’administration pour la boîte aux lettres d’un utilisateur.|
|2|Delegated|Personne disposant des privilèges de délégué pour la boîte aux lettres d’un utilisateur.|
|3|Transport|Service de transport dans le centre de données Microsoft.|
|4|SystemService|Compte de service dans le centre de données Microsoft|
|5|BestAccess|Réservé à une utilisation interne.|
|6|DelegatedAdmin|Administrateur délégué.|
|||||

### <a name="exchangemailboxauditgrouprecord-schema"></a>Schéma ExchangeMailboxAuditGroupRecord


|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Folder|Self.[ExchangeFolder](#exchangefolder-complex-type)|Non|Dossier où se trouve un groupe d’éléments.|
|CrossMailboxOperations|Edm.Boolean|Non|Indique si l’opération a impliqué plusieurs boîtes aux lettres.|
|DestMailboxId|Edm.Guid|Non|Défini uniquement si le paramètre CrossMailboxOperations est **True**. Indique le GUID de la boîte aux lettres cible.|
|DestMailboxOwnerUPN|Edm.String|Non|Défini uniquement si le paramètre CrossMailboxOperations est **True**. Indique l’UPN du propriétaire de la boîte aux lettres cible.|
|DestMailboxOwnerSid|Edm.String|Non|Défini uniquement si le paramètre CrossMailboxOperations est **True**. Indique le SID de la boîte aux lettres cible.|
|DestMailboxOwnerMasterAccountSid|Edm.String|Non|Défini uniquement si le paramètre CrossMailboxOperations est **True**. Spécifie le SID du compte principal du propriétaire de la boîte aux lettres cible.|
|DestFolder|Self.[ExchangeFolder](#exchangefolder-complex-type)|Non|Dossier de destination pour les opérations telles qu’un déplacement.|
|Folders|Collection(Self.[ExchangeFolder](#exchangefolder-complex-type))|Non|Informations sur les dossiers source impliqués dans une opération. Par exemple, si les dossiers sont sélectionnés, puis supprimés.|
|AffectedItems|Collection(Self.[ExchangeItem](#exchangeitem-complex-type))|Non|Informations sur chaque élément dans le groupe.|
|||||


### <a name="exchangemailboxauditrecord-schema"></a>Schéma ExchangeMailboxAuditRecord


|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Item|Self.[ExchangeItem](#exchangeitem-complex-type)|Non|Représente l’élément sur lequel l’opération a été effectuée.|
|ModifiedProperties|Collection(Edm.String)|Non|À déterminer|
|SendAsUserSmtp|Edm.String|Non|Adresse SMTP de l’utilisateur qui est empruntée.|
|SendAsUserMailboxGuid|Edm.Guid|Non|GUID Exchange de la boîte aux lettres consultée pour envoyer un message électronique.|
|SendOnBehalfOfUserSmtp|Edm.String|Non|Adresse SMTP de l’utilisateur au nom duquel le message électronique est envoyé.|
|SendOnBehalfOfUserMailboxGuid|Edm.Guid|Non|GUID Exchange de la boîte aux lettres consultée pour le compte duquel envoyer un message électronique.|
|||||

### <a name="exchangeitem-complex-type"></a>Type complexe ExchangeItem


|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|ID|Edm.String|Oui|ID de magasin.|
|Subject|Edm.String|Non|Ligne d’objet du message qui a été consulté.|
|ParentFolder|Edm.ExchangeFolder|Non|Nom du dossier dans lequel se trouve l’élément.|
|Attachments|Edm.String|Non|Liste des noms et taille du fichier de tous les éléments joints au message.|
|||||

### <a name="exchangefolder-complex-type"></a>Type complexe ExchangeFolder


|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|ID|Edm.String|Oui|ID de magasin de l’objet du dossier.|
|Path|Edm.String|Non|Nom de dossier de la boîte aux lettres dans laquelle se trouve le message consulté.|
|||||


## <a name="azure-active-directory-base-schema"></a>Schéma de base Azure Active Directory


|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|AzureActiveDirectoryEventType|Self.[AzureActiveDirectoryEventType](#azureactivedirectoryeventtype)|Oui|Type d’événement Azure AD. |
|ExtendedProperties|Collection(Common.NameValuePair)|Non|Propriétés étendues de l’événement Azure AD.|
|ModifiedProperties|Collection(Common.ModifiedProperty)|Non|Cette propriété est incluse pour les événements d’administration. La propriété inclut le nom de la propriété modifiée, la nouvelle valeur de la propriété modifiée et la valeur précédente de la propriété modifiée.|
|||||

### <a name="enum-azureactivedirectoryeventtype---type--edmint32"></a>Énumération : AzureActiveDirectoryEventType - Type : Edm.Int32

#### <a name="azureactivedirectoryeventtype"></a>AzureActiveDirectoryEventType

|**Nom du membre**|**Description**|
|:-----|:-----|
|AccountLogon|Événement de connexion au compte.|
|AzureApplicationAuditEvent|Événement de sécurité de l’application Azure.|
|||||

## <a name="azure-active-directory-account-logon-schema"></a>Schéma de connexion au compte Azure Active Directory


|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Application|Edm.String|Non|Application qui déclenche l’événement de connexion au compte. Par exemple, Office 15.|
|Client|Edm.String|Non|Détails sur le périphérique client, le système d’exploitation du périphérique et le navigateur du périphérique qui ont été utilisés pour l’événement de connexion au compte.|
|LoginStatus|Edm.Int32|Oui|Cette propriété provient directement de l’élément OrgIdLogon.LoginStatus. Le mappage de différents échecs de connexion intéressants peut être effectué à l’aide d’algorithmes d’alerte.|
|UserDomain|Edm.String|Oui|Informations sur l’identité du client (TII).|
|||||


### <a name="enum-credentialtype---type-edmint32"></a>Énumération : CredentialType - Type : Edm.Int32


|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|-1|Other|Autre authentification.|
|0|Password|Les informations d’identification utilisateur sont le nom d’utilisateur et le mot de passe.|
|1|MobilePhone|Les informations d’identification utilisateur correspondent à un téléphone mobile.|
|2|SecretQuestion|Les informations d’identification utilisateur correspondent à une question secrète.|
|3|SecurePin|Les informations d’identification utilisateur correspondent à un code confidentiel sécurisé.|
|4|SecurePinReset|Les informations d’identification utilisateur correspondent à une réinitialisation du code confidentiel sécurisé.|
|11|EasyID|Les informations d’identification utilisateur correspondent à EasyID.|
|14|PasswordIndexCredentialType|Les informations d’identification utilisateur correspondent à PasswordIndexCredentialType.|
|16|Device|Les informations d’identification utilisateur correspondent à un périphérique.|
|17|ForeignRealmIndex|Les informations d’identification utilisateur correspondent à ForeignRealmIndex.|
|||||

### <a name="enum-logintype---type-edmint32"></a>Énumération : LoginType - Type : Edm.Int32


|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|-1|Other|Autre type i.|
|1|InitialAuth|Connexion avec l’authentification initiale|
|2|CookieCopy|Connectez-vous avec le cookie.|
|3|SilentReAuth|Connectez-vous avec une authentification multiple en mode silencieux.|
|||||

### <a name="enum-authenticationmethod---type-edmint32"></a>Énumération : AuthenticationMethod - Type : Edm.Int32


|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|Min|La méthode d’authentification est Min.|
|1|Password|La méthode d’authentification est un mot de passe.|
|2|Digest|La méthode d’authentification est Digest.|
|3|ProxyAuth|La méthode d’authentification ProxyAuth.|
|4|InfoCard|La méthode d’authentification est InfoCard.|
|5|DAToken|La méthode d’authentification est DAToken.|
|6|Sha1RememberMyPassword|La méthode d’authentification est Sha1RememberMyPassword.|
|7|LMPasswordHash|La méthode d’authentification est LMPasswordHash.|
|8|ADFSFederatedToken|La méthode d’authentification est ADFSFederatedToken.|
|9|EID|La méthode d’authentification est EID.|
|10|DeviceID|La méthode d’authentification est DeviceID. |
|11|MD5|La méthode d’authentification est MD5.|
|12|EncProxyPasswordHash|La méthode d’authentification est EncProxyPasswordHash.|
|13|LWAFederation|La méthode d’authentification est LWAFederation.|
|14|Sha1HashedPassword|La méthode d’authentification est Sha1HashedPassword.|
|15|SecurePin|La méthode d’authentification est un code confidentiel sécurisé.|
|16|SecurePinReset|La méthode d’authentification est une réinitialisation de code confidentiel sécurisé.|
|17|SAML20PostSimpleSign|La méthode d’authentification est SAML20PostSimpleSign.|
|18|SAML20Post|La méthode d’authentification est SAML20Post.|
|19|OneTimeCode|La méthode d’authentification est un code à usage unique.|
|||||


## <a name="azure-active-directory-schema"></a>Schéma Azure Active Directory


|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Actor|Collection(Self.[IdentityTypeValuePair](#complex-type-identitytypevaluepair))|Non|Utilisateur ou principal de service ayant exécuté l’action.|
|ActorContextId|Edm.String|Non|GUID de l’organisation à laquelle appartient l’acteur.|
|ActorIpAddress|Edm.String|Non|Adresse IP de l’acteur au format d’adresse IPV4 ou IPV6.|
|InterSystemsId|Edm.String|Non|GUID effectuant le suivi des actions au sein des composants dans le service Office 365.|
|IntraSystemsId|Edm.String|Non|GUID généré par Azure Active Directory pour effectuer le suivi de l’action.|
|SupportTicketId|Edm.String|Non|ID de ticket de prise en charge de client pour l’action dans les situations « agir au nom d’un autre utilisateur ».|
|Target|Collection(Self.[IdentityTypeValuePair](#complex-type-identitytypevaluepair))|Non|Utilisateur sur lequel a été effectuée l’action (identifiée par la propriété Operation).|
|TargetContextId|Edm.String|Non|GUID de l’organisation à laquelle appartient l’utilisateur ciblé.|
|||||

### <a name="complex-type-identitytypevaluepair"></a>Type complexe IdentityTypeValuePair


|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|ID|Edm.String|Oui|Valeur de l’identité en fonction du type.|
|Type|Self.IdentityType|Oui|Type de l’identité.|
|||||

### <a name="enum-identitytype---type-edmint32"></a>Énumération : IdentityType - Type : Edm.Int32

#### <a name="identitytype"></a>IdentityType

|**Nom du membre**|**Description**|
|:-----|:-----|
|Claim|L’identité est une revendication à des fins d’autorisation.|
|Name|Nom d’affichage de l’identité cible ou de l’acteur de l’action d’audit.|
|Other|L’identité de l’acteur est d’un autre type. Par exemple, ObjectId dans le GUID généré par le service Office 365.|
|PUID|ID unique Passport (PUID) cible ou ID de l’acteur de l’action d’audit.|
|SPN|Identité d’un principal de service si l’action est effectuée par le service Office 365.|
|UPN|Nom d’utilisateur principal.|
|||||


## <a name="azure-active-directory-secure-token-service-sts-logon-schema"></a>Schéma de connexion STS (Secure Token Service) dans Azure Active Directory.

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|ApplicationId|Edm.String|Non|GUID représentant l’application qui demande la connexion. Le nom d’affichage peut être recherché via l’API Graph Azure Active Directory.|
|Client|Edm.String|Non|Informations sur le périphérique client, fournies par le navigateur exécutant la connexion.|
|LogonError|Edm.String|Non|En cas d’échec de connexion, la raison de l’échec est indiquée dans ce paramètre. Pour obtenir une description complète des erreurs LogonError, voir la liste des [codes d’erreur d’authentification et d’autorisation](https://docs.microsoft.com/fr-FR/azure/active-directory/develop/reference-aadsts-error-codes#aadsts-error-codes).
|||||

## <a name="dlp-schema"></a>Schéma DLP

Les événements DLP sont disponibles pour Exchange Online, SharePoint Online et OneDrive Entreprise. Les événements DLP dans Exchange sont disponibles uniquement pour les événements reposant sur la stratégie DLP unifiée (par exemple, configuration via le Centre de sécurité et de conformité). Les événements DLP reposant sur les règles de transport Exchange ne sont pas pris en charge.

Les événements DLP (prévention contre la perte de données) ont toujours UserKey="DlpAgent" dans le schéma commun. Il existe trois types d’événements DLP qui sont stockés en tant que valeur de la propriété Operation du schéma commun :

- DlpRuleMatch : indique qu’une règle a été satisfaite. Ces événements existent dans Exchange, SharePoint Online et OneDrive Entreprise. Pour Exchange, cela inclut les informations de remplacement et sur les faux positifs. Pour SharePoint Online et OneDrive Entreprise, les faux positifs et les remplacements génèrent des événements distincts.

- DlpRuleUndo : ces événements existent uniquement dans SharePoint Online et OneDrive Entreprise. Ils indiquent qu’une action de stratégie précédemment appliquée a été « annulée » en raison de la désignation d’un faux positif/remplacement par l’utilisateur, ou car le document n’est plus soumis à la stratégie (en raison d’une modification de la stratégie ou du contenu d’un document).

- DlpInfo : ces événements existent uniquement dans SharePoint Online et OneDrive Entreprise. Ils indiquent la désignation d’un faux positif, mais aucune action n’a été « annulée ».

|**Paramètres**|**Type**|**Obligatoire**|**Description**|
|:-----|:-----|:-----|:-----|
|SharePointMetaData|Self.[SharePointMetadata](#sharepointmetadata-complex-type)|Non|Décrit les métadonnées relatives au document dans SharePoint ou OneDrive Entreprise contenant les informations sensibles.|
|ExchangeMetaData|Self.[ExchangeMetadata](#exchangemetadata-complex-type)|Non|Décrit les métadonnées relatives au message électronique contenant des informations sensibles.|
|ExceptionInfo|Edm.String|Non|Identifie les raisons pour lesquelles une stratégie ne s’applique plus et/ou les informations relatives aux faux positifs et/ou remplacements indiqués par l’utilisateur final.|
|PolicyDetails|Collection(Self.[PolicyDetails](#policydetails-complex-type))|Oui|Informations concernant au moins une stratégie ayant déclenché l’événement DLP.|
|SensitiveInfoDetectionIsIncluded|Boolean|Oui|Indique si l’événement contient la valeur du type de données sensibles et le contexte environnant à partir du contenu source. L’accès aux données sensibles nécessite l’autorisation d’accès en lecture aux événements de stratégie DLP incluant des informations sensibles dans Azure Active Directory.|
|||||

### <a name="sharepointmetadata-complex-type"></a>Type complexe SharePointMetadata

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|From|Edm.String|Oui|Utilisateur ayant déclenché l’événement. Valeurs possibles : FileOwner, LastModifier ou LastSharer.|
|itemCreationTime|Edm.Date|Oui|Datetimestamp à l’heure UTC du moment de la journalisation de l’événement.|
|SiteCollectionGuid|Edm.Guid|Oui|GUID de la collection de sites.|
|SiteCollectionUrl|Edm.String|Oui|Nom du site SharePoint.|
|FileName|Edm.String|Oui|Nom du chemin d’accès.|
|FileOwner|Edm.String|Oui|Propriétaire du document.|
|FilePathUrl|Edm.String|Oui|URL du document.|
|DocumentLastModifier|Edm.String|Oui|Identité de l’utilisateur qui a modifié le document en dernier.|
|DocumentSharer|Edm.String|Oui|Identité de l’utilisateur qui a modifié le partage en dernier.|
|UniqueID|Edm.String|Oui|GUID qui identifie un fichier.|
|LastModifiedTime|Edm.DateTime|Oui|Horodatage à l’heure UTC du moment de la dernière modification du document.|
|||||


### <a name="exchangemetadata-complex-type"></a>Type complexe ExchangeMetadata

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|MessageID|Edm.String|Oui|ID du message électronique ayant déclenché l’événement.|
|From|Edm.String|Oui|L’utilisateur qui a envoyé le message électronique.|
|À|Collection(Edm.String)|Non|Collection d’adresses de messagerie qui se trouvaient sur la ligne À du message.|
|Cc|Collection(Edm.String)|Non|Collection d’adresses de messagerie qui se trouvaient sur la ligne Cc du message.|
|Cci|Collection(Edm.String)|Non|Collection d’adresses de messagerie qui se trouvaient sur la ligne Cci du message.|
|Subject|Edm.String|Oui|Objet du message électronique.|
|Sent|Edm.DateTime|Oui|Heure UTC de l’envoi du message électronique.|
|RecipientCount|Edm.Int32|Oui|Nombre total de tous les destinataires sur les lignes À, Cc et Cci du message.|
|||||

### <a name="policydetails-complex-type"></a>Type complexe PolicyDetails

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|PolicyId|Edm.Guid|Oui|GUID de la stratégie DLP pour cet événement.|
|PolicyName|Edm.String|Oui|Nom convivial de la stratégie DLP pour cet événement.|
|Rules|Collection(Self.[Rules](#rules-complex-type))|Oui|Informations sur les règles dans la stratégie qui ont été satisfaites pour cet événement.|
|||||

### <a name="rules-complex-type"></a>Type complexe Rules

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|RuleId|Edm.Guid|Oui|GUID de la règle DLP pour cet événement.|
|RuleName|Edm.String|Oui|Nom convivial de la règle DLP pour cet événement.|
|Actions|Collection(Edm.String)|Non|Liste des actions entreprises suite à un événement DLP RuleMatch.|
|OverriddenActions|Collection(Edm.String)|Non|Liste des actions entreprises précédemment qui ont été annulées suite à un événement DLPRuleUndo. |
|Severity|Edm.String|Non|Gravité (élevée, moyenne et faible) de la correspondance de règle.|
|RuleMode|Edm.String|Oui|Indiquez si la règle DLP a été définie sur Appliquer, Audit avec notification ou Audit uniquement.|
|ConditionsMatched|Self.[ConditionsMatched](#conditionsmatched-complex-type)|Non|Informations sur les conditions de la règle qui ont été satisfaites pour cet événement.|
|||||

### <a name="conditionsmatched-complex-type"></a>Type complexe ConditionsMatched

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|SensitiveInformation|Collection(Self.[SensitiveInformation](#sensitiveinformation-complex-type))|Non|Informations sur le type d’informations sensibles détecté.|
|DocumentProperties|Collection(NameValuePair)|Non|Informations sur les propriétés du document qui a déclenché une correspondance de règle.|
|OtherConditions|Collection(NameValuePair)|Non|Liste des paires clé/valeur décrivant les autres conditions qui ont été satisfaites.|
|||||

### <a name="sensitiveinformation-complex-type"></a>Type complexe SensitiveInformation

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Confidence|Edm.Int|Oui|Probabilité de modèle qui correspond à la détection.|
|Count|Edm.Int|Oui|Nombre d’instances sensibles détecté.|
|SensitiveType|Edm.Guid|Oui|GUID qui identifie le type de données sensibles détecté.|
|SensitiveInformationDetections|Self.SensitiveInformationDetections|Non|Tableau d’objets contenant des informations sensibles avec les détails suivants : valeur de correspondance et contexte de la valeur de correspondance.|
|||||

### <a name="sensitiveinformationdetections-complex-type"></a>Type complexe SensitiveInformationDetections 
Les données sensibles DLP sont disponibles uniquement dans l’API de flux d’activité pour les utilisateurs qui ont reçu l’autorisation d’accès en lecture aux données sensibles DLP. 

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Detections|Collection(Self.Detections)|Oui|Tableau d’informations sensibles détecté. Les informations contiennent des paires clé/valeur où la valeur = valeur de correspondance (ex. valeur de la carte de crédit de SSN) et où le contexte = un extrait de contenu source qui contient la valeur de correspondance. |
|ResultsTruncated|Edm.Boolean|Oui|Indique si les journaux ont été tronqués en raison du nombre élevé de résultats. |
|||||

### <a name="exceptioninfo-complex-type"></a>Type complexe ExceptionInfo

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Reason|Edm.String|Non|Pour un événement DLPRuleUndo, ce paramètre indique pourquoi la règle ne plus s’applique plus, ce qui peut être l’une de ces 3 raisons : remplacement, modification du document ou modification de la stratégie.|
|FalsePositive|Edm.Boolean|Non|Indique si l’utilisateur a désigné cet événement comme un faux positif.|
|Justification|Edm.String|Non|Si l’utilisateur a choisi de remplacer la stratégie, toute justification spécifiée par l’utilisateur est capturée ici.|
|Rules|Collection(Edm.Guid)|Non|Ensemble de GUID pour chaque règle désignée comme un faux positif ou un remplacement, ou pour laquelle une action a été annulée.|
|||||

## <a name="security-and-compliance-center-schema"></a>Schéma du Centre de sécurité et conformité

|**Paramètres**|**Type**|**Obligatoire**|**Description**|
|:-----|:-----|:-----|:-----|
|StartTime|Edm.Date|Non|Date et heure auxquelles la cmdlet a été exécutée.|
|ClientRequestId|Edm.String|Non|GUID pouvant être utilisé pour corréler cette cmdlet avec les opérations d’expérience utilisateur du Centre de sécurité et conformité. Ces informations sont utilisées uniquement par le support technique Microsoft.|
|CmdletVersion|Edm.String|Non|Version de build de la cmdlet lorsqu’elle a été exécutée.|
|EffectiveOrganization|Edm.String|Non|GUID de l’organisation affecté par la cmdlet. (Déconseillé : ce paramètre cessera d’apparaître à l’avenir.)|
|UserServicePlan|Edm.String|Non|Plan de service Exchange Online Protection affecté à l’utilisateur qui a exécuté la cmdlet.|
|ClientApplication|Edm.String|Non|Si la cmdlet a été exécutée par une application, contrairement à Powershell à distance, ce champ contient le nom de cette application.|
|Parameters|Edm.String|Non|Nom et valeur des paramètres qui ont été utilisés avec la cmdlet qui n’incluent pas d’informations d’identification personnelle.|
|NonPiiParameters|Edm.String|Non|Nom et valeur des paramètres qui ont été utilisés avec la cmdlet qui incluent des informations d’identification personnelle. (Déconseillé : ce champ cessera d’apparaître à l’avenir et son contenu sera fusionné avec le champ Paramètres.)|
|||||

## <a name="security-and-compliance-alerts-schema"></a>Schéma d’alertes de sécurité et conformité

Les signaux d’alerte sont les suivants :

- toutes les alertes générées en fonction des [stratégies d’alerte dans le Centre de sécurité et de conformité](https://docs.microsoft.com/office365/securitycompliance/alert-policies#default-alert-policies) ;
- les alertes liées à Office 365 générées dans [Sécurité des applications cloud Office 365](https://docs.microsoft.com/office365/securitycompliance/office-365-cas-overview) et [Microsoft Cloud App Security](https://docs.microsoft.com/fr-FR/cloud-app-security/what-is-cloud-app-security).

Les paramètres UserId et UserKey de ces événements sont toujours des alertes SecurityComplianceAlerts. Il existe deux types de signaux d’alerte stockés en tant que valeurs de la propriété Operation du schéma commun :

- AlertTriggered : une nouvelle alerte est générée en raison d’une correspondance de stratégie.

- AlertEntityGenerated : une nouvelle entité est ajoutée à une alerte. Cet événement s’applique uniquement aux alertes générées en fonction des stratégies d’alerte dans le Centre de sécurité et conformité Office 365. Chaque alerte générée peut être associée à un ou à plusieurs de ces événements. Par exemple, une stratégie d’alerte est définie pour déclencher une alerte si un utilisateur supprime plus de 100 fichiers en 5 minutes. Si deux utilisateurs dépassent le seuil au même moment, il existera deux événements AlertEntityGenerated, mais un seul événement AlertTriggered.

|**Paramètres**|**Type**|**Obligatoire**|**Description**|
|:-----|:-----|:-----|:-----|
|AlertId|Edm.Guid|Oui|GUID de l’alerte.|
|AlertType|Self.String|Oui|Type de l’alerte. Les types d’alertes sont les suivants : <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Système</p></li><li><p>Personnalisé</p></li>|
|Name|Edm.String|Oui|Nom de l’alerte.|
|PolicyId|Edm.Guid|Non|GUID de la stratégie qui a déclenché l’alerte.|
|Status|Edm.String|Non|Statut de l’alerte. Les statuts sont les suivants : <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Actif</p></li><li><p>Examen en cours</p></li><li><p>Résolu</p></li><li><p>Fermé</p></li></ul>|
|Severity|Edm.String|Non|Gravité de l’alerte. Les niveaux de gravité sont les suivants : <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Faible</p></li><li><p>Moyen</p></li><li><p>Élevé</p></li></ul>|
|Catégorie|Edm.String|Non|Catégorie de l’alerte. Les catégories sont les suivantes : <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>DataLossPrevention</p></li><li><p>ThreatManagement</p></li><li><p>DataGovernance</p></li><li><p>AccessGovernance</p></li><li><p>MailFlow</p></li><li><p>Other</p></li></ul>|
|Source|Edm.String|Non|Source de l’alerte. Les sources sont les suivantes : <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Conformité et sécurité dans Office 365</p></li><li><p>Cloud App Security</p></li></ul>|
|Comments|Edm.String|Non|Commentaires laissés par les utilisateurs qui ont vu l’alerte. Il s’agit d’une « nouvelle alerte » par défaut.|
|Data|Edm.String|Non|BLOB des données de détail de l’alerte ou de l’entité de l’alerte.|
|AlertEntityId|Edm.String|Non|Identificateur pour l’entité de l’alerte. Ce paramètre s’applique uniquement aux événements AlertEntityGenerated.|
|EntityType|Edm.String|Non|Type de l’alerte ou de l’entité de l’alerte. Les types d’entités sont les suivants : <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Utilisateur</p></li><li><p>Destinataires</p></li><li><p>Expéditeur</p></li><li><p>MalwareFamily</p></li></ul>Ce paramètre s’applique uniquement aux événements AlertEntityGenerated.|
|||||

## <a name="yammer-schema"></a>Schéma Yammer

Les événements Yammer répertoriés dans l’article relatif à la [recherche dans le journal d’audit dans le Centre de sécurité et conformité](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#yammer-activities) utilisent ce schéma.

|**Paramètres**|**Type**|**Obligatoire**|**Description**|
|:-----|:-----|:-----|:-----|
|ActorUserId|Edm.String|Non|Adresse électronique de l’utilisateur ayant effectué l’opération.|
|ActorYammerUserId|Edm.Int64|Non|ID de l’utilisateur ayant effectué l’opération.|
|DataExportType|Edm.String|Non|Renvoie « data » si l’exportation de données inclut des messages, des notes, des fichiers, des rubriques, des utilisateurs et des groupes. Renvoie « user » si exportation de données inclut uniquement des utilisateurs.|
|FileId|Edm.Int64|Non|ID du fichier dans l’opération. |
|FileName|Edm.String|Non|Nom du fichier dans l’opération. Ce paramètre s’affiche comme un champ vide s’il n’est pas pertinent pour l’opération.|
|GroupName|Edm.String|Non|Nom du groupe dans l’opération. Ce paramètre s’affiche comme un champ vide s’il n’est pas pertinent pour l’opération.|
|IsSoftDelete|Edm.Boolean|Non|Renvoie « true » si la stratégie de rétention des données du réseau est définie sur Suppression réversible. Renvoie « false » si la stratégie de rétention des données du réseau est définie sur Suppression définitive.|
|MessageId|Edm.Int64|Non|ID du message dans l’opération.|
|YammerNetworkId|Edm.Int64|Non|ID réseau de l’utilisateur ayant effectué l’opération.|
|TargetUserId|Edm.String|Non|Adresse électronique de l’utilisateur cible dans l’opération. Ce paramètre s’affiche comme un champ vide s’il n’est pas pertinent pour l’opération.|
|TargetYammerUserId|Edm.Int64|Non|ID de l’utilisateur cible dans l’opération.|
|VersionId|Edm.Int64|Non|ID de version du fichier dans l’opération.|
|||||

## <a name="sway-schema"></a>Schéma Sway

Les événements Sway répertoriés dans l’article relatif à la [recherche dans le journal d’audit dans le Centre de sécurité et conformité d’Office 365](https://support.office.com/en-us/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=en-US&amp;rs=en-US&amp;ad=US) (sans compter les événements de fichiers et de dossiers) utilisent ce schéma.

|**Paramètre**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|ObjectType|Self.[ObjectType](#objecttype)|Non|Point d’accès de l’événement déclenché. Les points d’accès incluent ce qui suit : <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Une instance Sway</p></li><li><p>Une instance Sway incorporée à un hôte</p></li><li><p>Les paramètres Sway dans le portail d’administration Office 365</p></li></ul>|
|Endpoint|Self.[Endpoint](#endpoint)|Non|Point de terminaison du client Sway pour l’événement déclenché. Le point de terminaison du client Sway peut être web, iOS, Windows ou Android. |
|BrowserName|Edm.String|Non|Navigateur utilisé pour accéder à Sway pour l’événement déclenché. |
|DeviceType|Self.[DeviceType](#devicetype)|Non|Type de périphérique utilisé pour accéder à Sway pour l’événement déclenché. Le type de périphérique peut être un ordinateur de bureau, un ordinateur portable ou une tablette.|
|SwayLookupId|Edm.String|Non|ID Sway. |
|SiteUrl|Edm.String|Non|URL pour Sway.|
|OperationResult|Self.[OperationResult](#operationresult)|Non|Réussite ou échec.|
|||||


### <a name="enum-objecttype---type-edmint32"></a>Énumération : ObjectType - Type : Edm.Int32

#### <a name="objecttype"></a>ObjectType

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|Sway|L’événement a été déclenché à partir d’une instance Sway.|
|1|SwayEmbedded|L’événement a été déclenché à partir d’une instance Sway incorporée dans un hôte.|
|2|SwayAdminPortal|L’événement a été déclenché à partir des paramètres de service Sway dans le portail d’administration Office 365.|
|||||


### <a name="enum-operationresult---type-edmint32"></a>Énumération : OperationResult - Type : Edm.Int32

#### <a name="operationresult"></a>OperationResult

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|Succeeded|L’événement a réussi.|
|1|Failed|Échec de l’événement.|
|||||


### <a name="enum-endpoint---type-edmint32"></a>Énumération : Endpoint - Type : Edm.Int32

#### <a name="endpoint"></a>Endpoint

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|SwayWeb|L’événement a été déclenché à l’aide du client web de Sway.|
|1|SwayIOS|L’événement a été déclenché à l’aide du client iOS de Sway.|
|2|SwayWindows|L’événement a été déclenché à l’aide du client Windows de Sway.|
|3|SwayAndroid|L’événement a été déclenché à l’aide du client Android de Sway.|
|||||


### <a name="enum-devicetype---type-edmint32"></a>Énumération : DeviceType - Type : Edm.Int32

#### <a name="devicetype"></a>DeviceType

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|Desktop|L’événement a été déclenché à partir d’un ordinateur de bureau.|
|1|Mobile|L’événement a été déclenché à partir d’un appareil mobile.|
|2|Tablet|L’événement a été déclenché à partir d’une tablette.|
|||||



### <a name="enum-swayauditoperation---type-edmint32"></a>Énumération : SwayAuditOperation - Type : Edm.Int32

#### <a name="swayauditoperation"></a>SwayAuditOperation

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|1|Create|L’utilisateur crée une instance Sway.|
|2|Delete|L’utilisateur supprime une instance Sway.|
|3|View|L’utilisateur affiche une instance Sway.|
|4|Edit|L’utilisateur modifie une instance Sway.|
|5|Duplicate|L’utilisateur duplique une instance Sway.|
|7|Share|L’utilisateur établit le partage d’une instance Sway. Cet événement capture l’action utilisateur consistant à cliquer sur une destination de partage spécifique dans le menu de partage Sway. L’événement n’indique pas si l’utilisateur effectue réellement l’action de partage et la termine.|
|8|ChangeShareLevel|L’utilisateur modifie le niveau de partage d’une instance Sway. Cet événement capture la modification par l’utilisateur de l’étendue du partage associé à une instance Sway. Par exemple, niveaux public ou interne à l’organisation.|
|9|RevokeShare|L’utilisateur cesse de partager une instance Sway en révoquant l’accès. Révoquer l’accès modifie les liens associés à une instance Sway.|
|10|EnableDuplication|L’utilisateur active la duplication d’une instance Sway (activée par défaut).|
|11|DisableDuplication|L’utilisateur désactive la duplication d’une instance Sway (désactivée par défaut).|
|12|ServiceOn|L’utilisateur active Sway pour l’ensemble de l’organisation via le centre d’administration Office 365 (activé par défaut).|
|13|ServiceOff|L’utilisateur désactive Sway pour l’ensemble de l’organisation via le centre d’administration Office 365 (désactivé par défaut).|
|14|ExternalSharingOn|L’utilisateur active le partage externe pour l’ensemble de l’organisation via le centre d’administration Office 365.|
|15|ExternalSharingOff|L’utilisateur désactive le partage externe pour l’ensemble de l’organisation via le centre d’administration Office 365.|
|||||

## <a name="data-center-security-base-schema"></a>Schéma de base de sécurité du centre de données

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|DataCenterSecurityEventType|Self.[DataCenterSecurityEventType ](#datacentersecurityeventtype)|Oui|Type d’événement de cmdlet dans la zone de verrouillage.|
|||||

### <a name="enum-datacentersecurityeventtype---type-edmint32"></a>Énumération : DataCenterSecurityEventType - Type : Edm.Int32

#### <a name="datacentersecurityeventtype"></a>DataCenterSecurityEventType


|**Nom du membre**|**Description**|
|:-----|:-----|
|DataCenterSecurityCmdletAuditEvent|Il s’agit de la valeur enum pour l’événement de type d’audit de la cmdlet.|
|||


## <a name="data-center-security-cmdlet-schema"></a>Schéma de cmdlet de sécurité du centre de données

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|StartTime|Edm.Date|Oui|Heure de début de l’exécution de la cmdlet.|
|EffectiveOrganization|Edm.String|Oui|Nom du client sur lequel l’élévation/la cmdlet a été ciblée.|
|ElevationTime|Edm.Date|Oui|Heure de début de l’élévation.|
|ElevationApprover|Edm.String|Oui|Nom d’un responsable Microsoft.|
|ElevationApprovedTime|Edm.Date|Non|Horodatage du moment où l’élévation a été approuvée.|
|ElevationRequestId|Edm.Guid|Oui|Identificateur unique pour la demande d’élévation.|
|ElevationRole|Edm.String|Non|Rôle pour lequel l’élévation a été demandée.|
|ElevationDuration|Edm.Int32|Oui|Durée pendant laquelle l’élévation était active.|
|GenericInfo|Edm.String|Non|Utilisé pour les commentaires et d’autres informations génériques.|
|||||


## <a name="microsoft-teams-schema"></a>Schéma Microsoft Teams

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|MessageId|Edm.String|Non|Identificateur pour un message de conversation ou de canal.|
|Members|Collection(Self.[MicrosoftTeamsMember](#microsoftteamsmember-complex-type))|Non|Liste des utilisateurs dans une équipe.|
|TeamName|Edm.String|Non|Nom de l’équipe auditée.|
|TeamGuid|Edm.Guid|Non|Identificateur unique de l’équipe auditée.|
|ChannelType|Edm.String|Non|Type de canal audité (standard/privé).|
|ChannelName|Edm.String|Non|Nom du canal audité.|
|ChannelGuid|Edm.Guid|Non|Identificateur unique pour le canal audité.|
|ExtraProperties|Collection(Self.[KeyValuePair](#keyvaluepair-complex-type))|Non|Liste de propriétés supplémentaires.|
|AddOnType|Self.[AddOnType](#addontype)|Non|Type de complément ayant généré cet événement.|
|AddonName|Edm.String|Non|Nom du complément ayant généré l’événement.|
|AddOnGuid|Edm.Guid|Non|Identificateur unique du complément ayant généré l’événement.|
|TabType|Edm.String|Non|Uniquement présent pour les événements de tabulation. Type de l’onglet ayant généré l’événement.|
|Nom|Edm.String|Non|Uniquement présent pour les événements de paramètres. Nom du paramètre modifié.|
|OldValue|Edm.String|Non|Uniquement présent pour les événements de paramètres. Ancienne valeur du paramètre.|
|NewValue|Edm.String|Non|Uniquement présent pour les événements de paramètres. Nouvelle valeur du paramètre.|
||||


### <a name="microsoftteamsmember-complex-type"></a>Type complexe MicrosoftTeamsMember

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|UPN|Edm.String|Non|Nom d’utilisateur principal (UPN) de l’utilisateur.|
|Role|Self.[MemberRoleType](#memberroletype)|Non|Rôle de l’utilisateur au sein de l’équipe.|
|DisplayName|Edm.String|Non|Nom d’affichage de l’utilisateur.|
|||||

### <a name="enum-memberroletype---type-edmint32"></a>Énumération : MemberRoleType - Type : Edm.Int32

#### <a name="memberroletype"></a>MemberRoleType

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|Member|Utilisateur membre de l’équipe.|
|1|Owner|Utilisateur propriétaire de l’équipe.|
|2|Guest|Utilisateur qui n’est pas membre de l’équipe.|
||||

### <a name="keyvaluepair-complex-type"></a>Type complexe KeyValuePair

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|Clé|Edm.String|Non|Clé de la paire clé/valeur.|
|Valeur|Edm.String|Non|Valeur de la paire clé-valeur.|
|||||


### <a name="enum-addontype---type-edmint32"></a>Énumération : AddOnType - Type : Edm.Int32

#### <a name="addontype"></a>AddOnType

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|1|Bot|Bot Microsoft Teams.|
|2|Connector|Connecteur Microsoft Teams.|
|3|Tab|Onglet Microsoft Teams.|
||||

## <a name="office-365-advanced-threat-protection-and-threat-investigation-and-response-schema"></a>Schéma Office 365 – Protection avancée contre les menaces et Threat Investigation and Response

Les événements [Office 365 – Protection avancée contre les menaces](https://docs.microsoft.com/office365/securitycompliance/office-365-atp) (ATP) et Threat Investigation and Response sont disponibles pour les clients Office 365 qui disposent d’un plan 1 ou d’un plan 2 du service Office 365 – Protection avancée contre les menaces, ou d’un abonnement E5. Chaque événement dans le flux Office 365 ATP correspond aux éléments suivants dans lesquels une menace a été détectée :

- Un message électronique envoyé ou reçu par un utilisateur dans l’organisation avec détections sur des messages au moment de la remise et à partir de la [purge automatique heure zéro](https://support.office.com/fr-FR/article/Zero-hour-auto-purge-protection-against-spam-and-malware-96deb75f-64e8-4c10-b570-84c99c674e15). 

- Les URL sur lesquelles un utilisateur a cliqué dans l’organisation qui ont été détectées comme malveillantes au moment du clic conformément à la protection liée aux [liens fiables dans ATP Office 365 ATP](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links).  

- Un fichier dans SharePoint Online, OneDrive Entreprise ou Microsoft Teams qui a été détecté comme étant malveillant par le système de protection [ATP d’Office 365](https://docs.microsoft.com/fr-FR/office365/securitycompliance/atp-for-spo-odb-and-teams).

- Alerte déclenchée qui a lancé une [investigation automatisée](https://docs.microsoft.com/office365/securitycompliance/automated-investigation-response-office).

> [!NOTE]
> Les fonctionnalités du service Office 365 – Protection avancée contre les menaces et Office 365 Threat Investigation and Response (anciennement Office 365 Threat Intelligence) font désormais partie du plan 2 du service Office 365 – Protection avancée contre les menaces, avec des fonctionnalités de protection contre les menaces supplémentaires. Pour obtenir plus d’informations, consultez les articles relatifs aux [plans Office 365 ATP et à la tarification](https://products.office.com/exchange/advance-threat-protection) et à la [description du service Office 365 ATP](https://docs.microsoft.com/office365/servicedescriptions/office-365-advanced-threat-protection-service-description).

### <a name="email-message-events"></a>Événements de message électronique

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|AttachmentData|Collection(Self.[AttachmentData](#attachmentdata))|Non|Données sur les pièces jointes dans le message électronique ayant déclenché l’événement.|
|DetectionType|Edm.String|Oui|Le type de détection (par exemple, **En ligne** | détection au moment de la remise ; **Différée** | détection après remise ; **ZAP** | messages supprimés par [purge automatique heure Zero](https://support.office.com/fr-FR/article/Zero-hour-auto-purge-protection-against-spam-and-malware-96deb75f-64e8-4c10-b570-84c99c674e15)). Les événements avec le type de détection ZAP sont généralement précédés d’un message avec le type de détection **Différé**.|
|DetectionMethod|Edm.String|Oui|Méthode ou technologie utilisée par ATP Office 365 pour la détection.|
|InternetMessageId|Edm.String|Oui|ID de message Internet.|
|NetworkMessageId|Edm.String|Oui|ID de message réseau Exchange Online.|
|P1Sender|Edm.String|Oui|Chemin de retour de l’expéditeur du message électronique.|
|P2Sender|Edm.String|Oui|Expéditeur du message électronique.|
|Stratégie|Self.[Policy](#policy-type-and-action-type)|Oui|Type de stratégie de filtrage (par exemple, **anti-courrier indésirable** ou **anti-hameçonnage**) et type d'action associé (par exemple,** courrier indésirable à niveau de confiance élevé**, **courrier indésirable** ou**hameçonnage**) pertinents pour le message électronique.|
|Stratégie|Self.[PolicyAction](#policy-action)|Oui|L’action configurée dans la stratégie de filtrage (par exemple, **Déplacer vers le dossier courrier indésirable** ou **Mise en quarantaine**) pertinente pour le message électronique.|
|P2Sender|Edm.String|Oui|L’expéditeur **De :** du message électronique.|
|Recipients|Collection(Edm.String)|Oui|Tableau des destinataires du message électronique.|
|SenderIp|Edm.String|Oui|Adresse IP ayant envoyé le message électronique d’Office 365. L’adresse IP apparaît au format IPv4 ou IPv6.|
|Subject|Edm.String|Oui|Ligne d’objet du message.|
|Verdict|Edm.String|Oui|Verdict du message.|
|MessageTime|Edm.Date|Oui|Date et l’heure en temps universel coordonné (UTC) de réception ou d’envoi du courrier électronique.|
|EventDeepLink|Edm.String|Oui|Lien profond vers l’événement de courrier électronique dans l’Explorateur ou rapports en temps réel dans le centre de conformité et sécurité Office 365.|
|||||

### <a name="attachmentdata-complex-type"></a>Type complexe AttachmentData

#### <a name="attachmentdata"></a>AttachmentData

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|FileName|Edm.String|Oui|Nom de fichier de la pièce jointe.|
|FileType|Edm.String|Oui|Type de fichier de la pièce jointe.|
|FileVerdict|Self.[FileVerdict](#fileverdict)|Oui|Verdict de programme malveillant dans le fichier.|
|MalwareFamily|Edm.String|Non|Famille de programme malveillant de fichier.|
|SHA256|Edm.String|Oui|Hachage SHA256 du fichier.|
|||||

### <a name="enum-fileverdict---type-edmint32"></a>Énumération : FileVerdict - Type : Edm.Int32

#### <a name="fileverdict"></a>FileVerdict

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|Good|Aucune menace détectée.|
|1|Bad|Programme malveillant détecté dans la pièce jointe.|
|-1|Error|Erreur d’analyse.|
|-2|Timeout|Expiration de l’analyse.|
|-3|Pending|Analyse non terminée.|
|||||

### <a name="enum-policy---type-edmint32"></a>Énumération : Stratégie – Type : Edm.Int32

#### <a name="policy-type-and-action-type"></a>Type de stratégie et type d’action

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|1|Anti-courrier indésirable, HSPM|Action contre le courrier indésirable à niveau de confiance élevé (HSPM) dans la stratégie anti-courrier indésirable.|
|2|Anti-courrier indésirable, SPM|Action contre le courrier indésirable (SPM) dans la stratégie anti-courrier indésirable.|
|3|Anti-courrier indésirable, Bloc|Action en bloc dans la stratégie anti-courrier indésirable.|
|4|Anti-courrier indésirable, PHSH|Action contre l’hameçonnage dans la stratégie anti-courrier indésirable.|
|5|Anti-hameçonnage, DIMP|Action contre l’emprunt d’identité de domaine (DIMP) dans la stratégie anti-hameçonnage.|
|6|Anti-hameçonnage, UIMP|Action contre l’emprunt d’identité de l’utilisateur (UIMP) dans la stratégie anti-hameçonnage.|
|7|Anti-hameçonnage, SPOOF|Action contre l’usurpation dans la stratégie anti-hameçonnage.|


### <a name="enum-policyaction---type-edmint32"></a>Énumération : PolicyAction – Type : Edm.Int32

#### <a name="policy-action"></a>Action de stratégie

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|0|MoveToJMF|L’action de stratégie consiste à déplacer vers le dossier courrier indésirable.|
|1|AddXHeader|L’action de stratégie consiste à ajouter un en-tête X au message électronique.|
|2|ModifySubject|L’action de stratégie consiste à modifier l’objet du message électronique avec les informations spécifiées par la stratégie de filtrage.|
|3|Rediriger|L’action de stratégie consiste à rediriger le courrier électronique vers une adresse de messagerie spécifique de la stratégie de filtrage.|
|4|Supprimer|L’action de stratégie consiste à supprimer (abandonner) le message électronique.|
|5|Quarantaine|L’action de stratégie consiste à mettre en quarantaine le message électronique.|
|6|NoAction| La stratégie est configurée de manière à ne prendre aucune mesure sur le message électronique.|
|7|BccMessage|L’action de stratégie consiste à mettre le message électronique en copie carbone invisible à l'adresse électronique spécifiée par la politique de filtrage.|


### <a name="url-time-of-click-events"></a>Événements d’heure de clic d’URL

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|UserId|Edm.String|Oui|Identificateur (par exemple, une adresse électronique) de l’utilisateur qui a cliqué sur l’URL.|
|AppName|Edm.String|Oui|Service Office 365 à partir duquel un utilisateur a cliqué sur l’URL (par exemple, Courrier Outlook).|
|URLClickAction|Self.[URLClickAction](#urlclickaction)|Oui|Cliquez sur action pour l’URL en fonction des stratégies de l’organisation pour [liens fiables Office 365 la fonctionnalité](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links).|
|SourceId|Edm.String|Oui|Identificateur du service Office 365 à partir duquel un utilisateur a cliqué sur l’URL (par exemple, pour la messagerie, il s’agit de l’ID de message réseau Exchange Online).|
|TimeOfClick|Edm.Date|Oui|Date et heure à l’heure UTC (temps universel coordonné) au moment où l’utilisateur a cliqué sur l’URL.|
|URL|Edm.String|Oui|URL sur laquelle l’utilisateur a cliqué.|
|UserIp|Edm.String|Oui|Adresse IP de l’utilisateur qui a cliqué sur l’URL. L’adresse IP apparaît au format d’adresse IPv4 ou IPv6.|
|||||

### <a name="enum-urlclickaction---type-edmint32"></a>Enum : URLClickAction ; Type : Edm.Int32

#### <a name="urlclickaction"></a>URLClickAction

|**Valeur**|**Nom du membre**|**Description**|
|:-----|:-----|:-----|
|2|Blockpage|Utilisateur est bloqué et ne peut pas accéder à l’URL par [Liens fiables ATP Office 365](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links).|
|3|PendingDetonationPage|La page de détonation en attente est affichée pour l’utilisateur par [Liens fiables ATP Office 365](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links).|
|4|BlockPageOverride|L’utilisateur est bloqué et ne peut pas accéder à l’URL par [Liens fiables ATP Office 365](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links); cependant, l'utilisateur a ignoré le blocage pour accéder à l’URL.|
|5|PendingDetonationPageOverride|La page détonation a été affichée pour l’utilisateur par [Liens fiables ATP Office 365](https://docs.microsoft.com/office365/securitycompliance/atp-safe-links) ; cependant, l'utilisateur a ignoré le blocage pour accéder à l’URL.|
|||||


### <a name="file-events"></a>Événements de fichier

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|FileData|Self.[FileData](#filedata)|Oui|Données sur le fichier ayant déclenché l’événement.|
|SourceWorkload|Self.[SourceWorkload](#sourceworkload)|Oui|Charge de travail ou service dans lequel le fichier a été trouvé (par exemple, SharePoint Online, OneDrive Entreprise ou Microsoft Teams)
|DetectionMethod|Edm.String|Oui|Méthode ou technologie utilisée par ATP Office 365 pour la détection.|
|LastModifiedDate|Edm.Date|Oui|Date et heure à l’heure UTC (temps universel coordonné) e création ou de dernière modification du fichier.|
|LastModifiedBy|Edm.String|Oui|Identificateur (par exemple, une adresse de messagerie) de l’utilisateur qui a créé ou modifié en dernier le fichier.|
|EventDeepLink|Edm.String|Oui|Lien profond vers l’événement de ficher dans l’Explorateur ou rapports en temps réel dans le centre de conformité et sécurité.|
|||||

### <a name="filedata-complex-type"></a>Type complexe FileData

#### <a name="filedata"></a>FileData

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
|DocumentId|Edm.String|Oui|Identificateur unique pour le fichier dans SharePoint, OneDrive ou Microsoft Teams.|
|FileName|Edm.String|Oui|Nom du fichier ayant déclenché l’événement.|
|FilePath|Edm.String|Oui|Chemin (emplacement) pour le fichier dans SharePoint, OneDrive ou Microsoft Teams.|
|FileVerdict|Self.[FileVerdict](#fileverdict)|Oui|Verdict de programme malveillant dans le fichier.|
|MalwareFamily|Edm.String|Non|Famille de programme malveillant de fichier.|
|SHA256|Edm.String|Oui|Hachage SHA256 du fichier.|
|FileSize|Edm.String|Oui|Taille du fichier, en octets.|
|||||

### <a name="enum-sourceworkload---type-edmint32"></a>Enum : SourceWorkload ; Type : Edm.Int32

#### <a name="sourceworkload"></a>SourceWorkload

|**Valeur**|**Nom du membre**|
|:-----|:-----|
|0|SharePoint Online|
|1|OneDrive Entreprise|
|2|Microsoft Teams|
|||||

### <a name="automated-investigation-and-response-events"></a>Événements d’investigation et de réponse automatisés

Les événements [Office 365 Automated investigation and Response (AIR)](https://docs.microsoft.com/office365/securitycompliance/automated-investigation-response-office) sont disponibles pour les clients Office 365 disposant d’un abonnement incluant Office 365 – Protection avancée contre les menaces (plan 2) ou Office 365 E5. Les événements d’investigation sont enregistrés sur la base d’un changement d’état d’investigation. Par exemple, lorsqu’un administrateur effectue une action qui fait passer l’état d’une investigation d’Actions en attente à Terminé, un événement est consigné. 

Pour l’instant, seules les investigations automatiques sont enregistrées. (Les événements pour les investigations générées manuellement seront disponibles prochainement). Les valeurs de statut suivantes sont consignées : 
- Une investigation a été créée
- Aucune menace détectée 
- Interrompu par le système 
- Action en attente 
- Menace détectée 
- Corrigé 
- Échec 
- Interrompu par une limitation 
- Interrompu par l’utilisateur 

#### <a name="main-investigation-schema"></a>Schéma d’investigation principal 

|Nom   |Type   |Description  |
|----|----|----|
|InvestigationId    |Edm.String |ID d’investigation/GUID |
|InvestigationName  |Edm.String |Nom de l’investigation |
|InvestigationType  |Edm.String |Type d’investigation. Peut prendre l’une des valeurs suivantes :<br/>- Messages signalés par l’utilisateur<br/>- Programme malveillant purgé<br/>- Hameçonnage purgé<br/>- Modification du verdict concernant l’URL<p>(Les investigations manuelles, actuellement indisponibles, le seront bientôt.) |
|LastUpdateTimeUtc  |Edm.Date   |Heure UTC de la dernière mise à jour pour une investigation |
|StartTimeUtc   |Edm.Date   |Heure de début d’une investigation |
|État     |Edm.String     |État d’investigation, d’exécution, d’actions en attente, etc. |
|DeeplinkURL    |Edm.String |URL de lien profond vers un examen dans le Centre de sécurité et conformité Office 365 |
|Actions |Collection (Edm.String)   |Ensemble d’actions recommandées par une investigation |
|Données   |Edm.String |Chaîne de données qui contient des détails supplémentaires sur les entités d’investigation, ainsi que des informations sur les alertes relatives à l’investigation. Les entités sont disponibles dans un nœud séparé dans l’objet BLOB. |

#### <a name="actions"></a>Actions

|Champ  |Type   |Description |
|----|----|----|
|ID     |Edm.String |ID d’action|
|ActionType |Edm.String |Type de l’action (par exemple, mise à jour de courrier électronique) |
|ActionStatus   |Edm.String |Les valeurs sont les suivantes : <br/>– En attente<br/>– En cours d’exécution<br/>- En attente de ressources<br/>– Terminé<br/>– Échec |
|ApprovedBy |Edm.String |Null si approuvée automatiquement; sinon, nom d’utilisateur/ID (prochainement disponible) |
|TimestampUtc   |Edm.DateTime   |Horodatage de la modification de l’état de l’action |
|ActionId   |Edm.String |Identificateur unique de l’action |
|InvestigationId    |Edm.String |Identificateur unique de l’examen |
|RelatedAlertIds    |Collection(Edm.String) |Alertes liées à une investigation |
|StartTimeUtc   |Edm.DateTime   |Horodatage de la création d’action |
|EndTimeUtc |Edm.DateTime   |Horodatage de la mise à jour de l’état final de l’action |
|Identificateurs de ressources   |Edm.String  |Correspond à l'identifiant du client Azure Active Directory.|
|Entités   |Collection(Edm.String) |Liste d’une ou plusieurs entités affectées par action |
|Identifiants d’alerte associée  |Edm.String |Alerte liée à une investigation |

#### <a name="entities"></a>Entités

##### <a name="mailmessage-email"></a>MailMessage (e-mail) 

|Champ  |Type   |Description  |
|----|----|----|
|Type   |Edm.String |"mail-message"  |
|Fichiers  |Collection (self. file) |Détails sur les fichiers des pièces jointes de ce message |
|Destinataire  |Edm.String |Le destinataire de ce message électronique |
|URL   |Collection (self. URL) |Les URL contenues dans ce message électronique  |
|Expéditeur |Edm.String |Adresse e-mail de l’expéditeur  |
|SenderIP   |Edm.String |Adresse IP de l’expéditeur  |
|ReceivedDate   |Edm.DateTime   |Date de réception de ce message  |
|NetworkMessageId   |Edm.Guid   |ID de message réseau de ce message électronique  |
|InternetMessageId  |Edm.String  |ID de message internet de ce message électronique |
|Subject    |Edm.String |L’objet de ce message électronique  |

#### <a name="ip"></a>IP

|Champ  |Type   |Description  |
|----|----|----|
|Type   |Edm.String |"IP" |
|Adresse    |Edm.String |Adresse IP sous la forme d’une chaîne, par exemple `127.0.0.1`

#### <a name="url"></a>URL

|Champ  |Type   |Description  |
|----|----|----|
|Type   |Edm.String |« URL » |
|Url    |Edm.String |URL complète vers laquelle pointe une entité  |

#### <a name="mailbox-also-equivalent-to-the-user"></a>Boîte aux lettres (également équivalente à l’utilisateur) 

|Champ  |Type   |Description |
|----|----|----|
|Type   |Edm.String |« boîte aux lettres »  |
|MailboxPrimaryAddress  |Edm.String |Adresse principale de la boîte aux lettres  |
|DisplayName    |Edm.String |Nom d’affichage de la boite aux lettres |
|UPN    |Edm.String |L’UPN de la boîte aux lettres  |

#### <a name="file"></a>File

|Champ  |Type   |Description  |
|----|----|----|
|Type   |Edm.String |« fichier » |
|Nom   |Edm.String |Nom de fichier sans chemin d’accès |
FileHashes |Collection (Edm.String) |Fichiers à hacher associés au fichier |

#### <a name="filehash"></a>FileHash

|Champ  |Type   |Description |
|----|----|----|
|Type   |Edm.String |« filehash » |
|Algorithme  |Edm.String |Le type d’algorithme de hachage, qui peut être l’une des valeurs suivantes :<br/>– Inconnu<br/>– MD5<br/>– SHA1<br/>- SHA256<br/>- SHA256AC
|Valeur  |Edm.String |Valeur de hachage  |

#### <a name="mailcluster"></a>MailCluster

|Champ  |Type   |Description   |
|----|----|----|
|Type   |Edm.String |"MailCluster" <br/>Détermine le type d’entité examinée |
|NetworkMessageIds  |Collection (Edm.String)    |Liste des ID de courrier qui font partie du cluster de courriers |
|CountByDeliveryStatus  |Collections (Edm.String)   |Nombre de messages électroniques par DeliveryStatus, représentation sous forme de chaîne |
|CountByThreatType  |Collections (Edm.String) |Nombre de messages électroniques par ThreatType, représentation sous forme de chaîne |
|Menaces    |Collections (Edm.String)   |Les menaces relatives aux messages électroniques qui font partie du cluster de courriers. Les menaces incluent des valeurs telles que le hameçonnage et les programmes malveillants. |
|Requête  |Edm.String |Requête utilisée pour identifier les messages du cluster de courriers  |
|QueryTime  |Edm.DateTime   |Heure de la requête  |
|MailCount  |Edm.int    |Nombre de messages électroniques qui font partie du cluster de courriers.  |
|Source |String |Source du cluster de courriers ; valeur de la source de cluster. |

## <a name="power-bi-schema"></a>Schéma Power BI

Les événements Power BI répertoriés dans l’article relatif à la [Recherche dans le journal d’audit dans le Centre de sécurité d’Office 365](/power-bi/service-admin-auditing#activities-audited-by-power-bi) utilisent ce schéma.

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
| AppName               | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Non  | Nom de l’application dans laquelle l’événement s’est produit. |
| DashboardName         | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Non  | Le nom du tableau de bord dans lequel l’événement s’est produit. |
| DataClassification    | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Non  | La [classification des données](/power-bi/service-data-classification), le cas échéant, pour le tableau de bord dans lequel l’événement s’est produit. |
| DatasetName           | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Non  | Le nom du tableau de l’ensemble de données dans lequel l’événement s’est produit. |
| MembershipInformation | Collection([MembershipInformationType](#membershipinformationtype-complex-type))   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Non  | Informations d’appartenance au groupe. |
| OrgAppPermission      | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Non  | Liste des autorisations pour une application d’organisation (organisation entière, utilisateurs spécifiques ou groupes spécifiques). |
| ReportName            | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Non  | Le nom du tableau du rapport dans lequel l’événement s’est produit. |
| SharingInformation    | Collection([SharingInformationType](#sharinginformationtype-complex-type))   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"    |  Non  | Informations sur la personne à laquelle est envoyée une invitation de partage. |
| SwitchState           | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Non  | Informations sur l’état des différents commutateurs au niveau client. |
| WorkSpaceName         | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true"                            |  Non  | Le nom du tableau de l’espace de travail dans lequel l’événement s’est produit. |
|||||

### <a name="membershipinformationtype-complex-type"></a>Type complexe MembershipInformationType

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
| MemberEmail | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Non  | Adresse de messagerie du groupe. |
| Statut      | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Non  | Actuellement non rempli. |
|||||

### <a name="sharinginformationtype-complex-type"></a>Type complexe SharingInformationType

|**Paramètres**|**Type**|**Obligatoire ?**|**Description**|
|:-----|:-----|:-----|:-----|
| RecipientEmail    | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Non  | Adresse de messagerie du destinataire de l’invitation de partage. |
| RecipientName    | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Non  | Nom du destinataire de l’invitation de partage. |
| ResharePermission | Edm.String   Term="Microsoft.Office.Audit.Schema.PIIFlag" Bool="true" |  Non  | L’autorisation accordée au destinataire. |
|||||

## <a name="workplace-analytics-schema"></a>Schéma Analyse du temps de travail

Les événements Analyse du temps de travail répertoriés dans l’article relatif à la [recherche dans le journal d’audit dans le Centre de sécurité et conformité Office 365](https://docs.microsoft.com/office365/securitycompliance/search-the-audit-log-in-security-and-compliance#microsoft-workplace-analytics-activities) utilisent ce schéma.

| **Paramètres**     | **Type**            | **Obligatoire ?** | **Description**|
|:------------------ | :------------------ | :--------------|:--------------|
| WpaUserRole        | Edm.String | Non     | Rôle Analyse du temps de travail de l’utilisateur ayant exécuté l’action.                                                                                            |
| ModifiedProperties | Collection (Common.ModifiedProperty) | Non | Cette propriété inclut le nom de la propriété modifiée, la nouvelle valeur de la propriété modifiée et la valeur précédente de la propriété modifiée.|
| OperationDetails   | Collection (Common.NameValuePair)    | Non | Liste des propriétés étendues pour le paramètre ayant été modifié. Chaque propriété a un **nom** et une **valeur**.|
||||
