---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Service Communications API reference
title: Référence de l’API Office 365 Service Communications
description: 'Utilisez cette API pour accéder aux données suivantes : Obtenir les services, Obtenir l’état actuel, Obtenir l’état de l’historique et Obtenir les messages.'
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 883c7026ea41794e290208bed73b8da4f8ce90861cd2a1f8193e731e5dd1a4ef
ms.sourcegitcommit: 88ef5f75a9e2a25760a2caa2cef1f51f9afba90c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/05/2021
ms.locfileid: "54274338"
---
# <a name="office-365-service-communications-api-reference"></a>Référence de l’API Office 365 Service Communications

> [!IMPORTANT]
> L’API sur l’Intégrité des services et des communications dans Microsoft Graph est désormais disponible. L’API Microsoft Graph remplace l’API Service Communications spécifié dans cet article. La version héritée de l’API Service Communications sera mise hors service à compter du 17 décembre 2021. Pour plus d’informations sur la nouvelle API Microsoft Graph, voir [Vue d’ensemble de l’accès à l’intégrité des services et aux communications dans Microsoft Graph](/graph/service-communications-concept-overview).

Vous pouvez utiliser l’API V2 Office 365 Service Communications pour accéder aux données suivantes :

- **Obtenir les services** : obtenez la liste des services abonnés.

- **Obtenir l’état actuel** : obtenez une vue en temps réel des incidents de service des événements en cours.

- **Obtenir l’état de l’historique** : obtenez une vue historique des incidents de service.

- **Obtenir les messages** : communications Rechercher un incident et Centre de messages.

Actuellement, l’API Office 365 Service Communications contient des données pour Office 365, Yammer, Dynamics CRM et les services Cloud de Microsoft Intune.

## <a name="the-fundamentals"></a>Les principes de base

L’URL racine de l’API inclut un identificateur client qui étend les opérations sur un seul client :

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

L’**API Office 365 Service Communications** est un service REST qui vous permet de développer des solutions à l’aide de n’importe quel langage web et environnement d’hébergement qui prend en charge les certificats X.509 et HTTPS. L’API se base sur **Microsoft Azure Active Directory** et le protocole **OAuth2** pour l’authentification et l’autorisation. Pour accéder à l’API depuis votre application, vous devez d’abord l’enregistrer dans Azure AD et la configurer avec les autorisations appropriées. Cela permettra à votre application de demander les jetons d’accès OAuth2 nécessaires pour appeler l’API. Vous trouverez plus d’informations sur l’enregistrement et la configuration d’une application dans Azure AD dans la rubrique relative à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).

Toutes les demandes API nécessitent un en-tête HTTP d’autorisation contenant un jeton d’accès JWT OAuth2 valide provenant d’Azure AD qui contient la revendication **ServiceHealth.Read** ; et l’identificateur client doit correspondre à l’identificateur client dans l’URL racine.

```json
Authorization: Bearer {OAuth2 token}
```

### <a name="request-headers"></a>En-têtes de demande

Voici les en-têtes de demande pris en charge pour toutes les opérations de l’API Office 365 Service Communications.

|En-tête|Description|
|:-----|:-----|
|**Accept (facultatif)**|Voici les représentations acceptables pour la réponse :<br/>**application/json;odata.metadata=full**<br/>**application/json;odata.metadata=minimal**<br/>[La valeur par défaut si l’en-tête n’est pas spécifié] **application/json;odata.metadata=none**|
|**Authorization (obligatoire)**|Jeton d’autorisation (jeton Azure AD JWT du porteur) de la demande.|

<br/>

### <a name="response-headers"></a>En-têtes de réponse

Voici les en-têtes de réponse renvoyés pour toutes les opérations de l’API Office 365 Service Communications :

|En-tête|Description|
|:-----|:-----|
|**Content-Length**|La longueur du corps de la réponse.|
|**Content-Type**|Représentation de la réponse :<br/>**application/json**<br/>**application/json;odata.metadata=full**<br/>**application/json;odata.metadata=minimal**<br/>**application/json;odata.metadata=none**<br/>**odata.streaming=true**|
|**Cache-Control**|Utilisé pour spécifier les directives que doivent respecter tous les mécanismes de mise en cache accompagnant la chaîne de demande/réponse.|
|**Pragma**|Comportements propres à l’implémentation.|
|**Date d’expiration**|Date d’expiration de la ressource définie par le client.|
|**X-Activity-Id**|ID d’activité généré par le serveur.|
|**OData-Version**|Version d’OData prise en charge (4.0).|
|**Date**|Date UTC d’envoi de la réponse à partir du serveur.|
|**X-Time-Taken**|Durée de génération de la réponse (ms).|
|**X-Instance-Name**|Identificateur de l’instance Azure utilisé pour générer la réponse (à des fins de débogage).|
|**Serveur**|Serveur utilisé pour générer la réponse (à des fins de débogage).|
|**X-ASPNET-Version**|Version d’ASP.Net utilisée par le serveur ayant généré la réponse (à des fins de débogage).|
|**X-Powered-By**|Technologies utilisées dans le serveur ayant généré la réponse (à des fins de débogage).|
|||

<br/>

Voici les opérations de l’API Office 365 Service Communications.

## <a name="get-services"></a>Obtenir les services

Renvoie la liste des services abonnés.

|Informations|Service|Description|
|:-----|:-----|:-----|
|**Path**| `/Services`||
|**Query-option**|$select|Sélectionnez un sous-ensemble de propriétés.|
|**Response**|Liste des entités « Service »|L’entité « Service » contient « Id » (chaîne), « DisplayName » (chaîne) et « FeatureNames » (liste de chaînes).|
||||

### <a name="sample-request"></a>Exemple de demande

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

### <a name="sample-response"></a>Exemple de réponse

```json
{
    "value": [
        {
            "Id": "Exchange",
            "DisplayName": "Exchange Online",
            "FeatureNames": [
                "Sign-in",
                "E-Mail and calendar access",
                "E-Mail timely delivery",
                "Management and Provisioning",
                "Voice mail"
            ]
        },
        {
            "Id": "Lync",
            "DisplayName": "Lync Online",
            "FeatureNames": [
                "Audio and Video",
                "Federation",
                "Management and Provisioning",
                "Sign-In",
                "All Features",
                "Dial-In Conferencing",
                "Online Meetings",
                "Instant Messaging",
                "Presence",
                "Mobility"
            ]
        }
    ]
}
```

## <a name="get-current-status"></a>Obtenir l’état actuel

Renvoie l’état du service au cours des 24 heures précédentes.

> [!NOTE] 
> La réponse du service contient l’état et les éventuels incidents au cours des 24 heures précédentes. La valeur StatusDate ou StatusTime renvoyée sera exactement 24 heures dans le passé. Pour obtenir la dernière mise à jour d’un incident particulier, utilisez la fonctionnalité Obtenir les messages et lisez la valeur LastUpdatedTime de l’enregistrement de la réponse qui correspond à votre ID d’incident. <br/>

<br/>

|Informations|Service|Description|
|:-----|:-----|:-----|
|**Path**| `/CurrentStatus`||
|**Filter**|Charge de travail|Filtrez par charge de travail (chaîne, valeur par défaut : all).|
|**Query-option**|$select|Sélectionnez un sous-ensemble de propriétés.|
|**Response**|Liste des entités « WorkloadStatus ».|L’entité « WorkloadStatus » contient « Id » (chaîne), « Workload » (chaîne), « StatusTime »(DateTimeOffset), « WorkloadDisplayName » (chaîne), « Status » (chaîne), « IncidentIds » (liste de chaînes) et FeatureGroupStatusCollection (liste des « FeatureStatus »).<br/><br/>L’entité « FeatureStatus » contient « Feature » (chaîne), « FeatureGroupDisplayName » (chaîne) et « FeatureStatus » (chaîne).|
||||

### <a name="sample-request"></a>Exemple de demande

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a>Exemple de réponse

```json
{
    "value": [
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        },
        {
            "Id": "Lync",
            "Workload": "Lync",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Lync Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "AudioVideo",
                    "FeatureGroupDisplayName": "Audio and Video",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Federation",
                    "FeatureGroupDisplayName": "Federation",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "ManagementandProvisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Sign-In",
                    "FeatureGroupDisplayName": "Sign-In",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "All",
                    "FeatureGroupDisplayName": "All Features",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "DialInConferencing",
                    "FeatureGroupDisplayName": "Dial-In Conferencing",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "OnlineMeetings",
                    "FeatureGroupDisplayName": "Online Meetings",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "InstantMessaging",
                    "FeatureGroupDisplayName": "Instant Messaging",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Presence",
                    "FeatureGroupDisplayName": "Presence",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Mobility",
                    "FeatureGroupDisplayName": "Mobility",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        }
    ]
}
```

### <a name="status-definitions"></a>Définitions des états

Les définitions d’état englobent les valeurs suivantes :

- Investigating
- ServiceDegradation
- ServiceInterruption
- RestoringService
- ExtendedRecovery
- InvestigationSuspended
- ServiceRestored
- FalsePositive
- PostIncidentReportPublished
- ServiceOperational

Pour obtenir la description de ces définitions d’état, voir [Vérifier l’état du service Microsoft 365](/enterprise/view-service-health#status-definitions).

## <a name="get-historical-status"></a>Obtenir l’état de l’historique

Renvoie l’état historique du service, par jour, sur un intervalle de temps donné.

|Informations|Service|Description|
|:-----|:-----|:-----|
|**Path**| `/HistoricalStatus`||
|**Filters**|Charge de travail|Filtrez par charge de travail (chaîne, valeur par défaut : all).|
||StatusTime|Filtrez par jour supérieur à StatusTime (DateTimeOffset, valeur par défaut : ge CurrentTime - 7 jours).|
|**Query-option**|$select|Sélectionnez un sous-ensemble de propriétés.|
|**Response**|Liste des entités « WorkloadStatus ».|L’entité « WorkloadStatus » contient « Id » (chaîne), « Workload » (chaîne), « StatusTime »(DateTimeOffset), « WorkloadDisplayName » (chaîne), « Status » (chaîne), « IncidentIds » (liste de chaînes) et FeatureGroupStatusCollection (liste des « FeatureStatus »).<br/><br/>L’entité « FeatureStatus » contient « Feature » (chaîne), « FeatureGroupDisplayName » (chaîne) et « FeatureStatus » (chaîne).|
||||

### <a name="sample-request"></a>Exemple de demande

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a>Exemple de réponse

```json
{
    "value": [
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-11T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "ServiceOperational",
            "IncidentIds": [],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "ServiceOperational"
                }
            ]
        },
        {
            "Id": "Exchange",
            "Workload": "Exchange",
            "StatusDate": "2015-04-10T00:00:00Z",
            "WorkloadDisplayName": "Exchange Online",
            "Status": "InformationAvailable",
            "IncidentIds": [
                "EX20870"
            ],
            "FeatureGroupStatusCollection": [
                {
                    "Feature": "Signin",
                    "FeatureGroupDisplayName": "Sign-in",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Access",
                    "FeatureGroupDisplayName": "E-Mail and calendar access",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Delivery",
                    "FeatureGroupDisplayName": "E-Mail timely delivery",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "Provisioning",
                    "FeatureGroupDisplayName": "Management and Provisioning",
                    "FeatureStatus": "ServiceOperational"
                },
                {
                    "Feature": "UnifiedMessaging",
                    "FeatureGroupDisplayName": "Voice mail",
                    "FeatureStatus": "InformationAvailable"
                }
            ]
        }
    ]
}
```

## <a name="get-messages"></a>Obtenir les messages

Renvoie les messages sur le service sur un intervalle de temps donné. Utilisez le filtre de type pour filtrer les messages « Incident de service », « Maintenance planifiée » ou « Centre de messages ».

|Informations|Service|Description|
|:-----|:-----|:-----|
|**Path**| `/Messages`||
|**Filters**|Charge de travail|Filtrez par charge de travail (chaîne, valeur par défaut : all).|
||StartTime|Filtrez par Start Time (DateTimeOffset, valeur par défaut : ge CurrentTime - 7 jours).|
||EndTime|Filtrez par End Time (DateTimeOffset, valeur par défaut : le CurrentTime).|
||MessageType|Filtrez par MessageType (chaîne, valeur par défaut : all).|
||ID|Filtrez par ID (chaîne, valeur par défaut : all).|
|**Query-option**|$select|Sélectionnez un sous-ensemble de propriétés.|
||$top|Sélectionnez le nombre de résultats le plus élevé (valeur par défaut et max $top=100).|
||$skip|Ignorez le nombre de résultats (valeur par défaut : $skip = 0).|
|**Response**|Liste des entités « Message ».|L’entité « Message » contient « Id » (chaîne), « StartTime » (DateTimeOffset), « EndTime » (DateTimeOffset), « Status » (chaîne), « Messages » (liste des entités « MessageHistory »), « LastUpdatedTime » (DateTimeOffset), « Workload » (chaîne), « WorkloadDisplayName » (chaîne), « Feature » (chaîne), « FeatureDisplayName » (chaîne), « MessageType » (Enum, valeur par défaut : all).<br/><br/>L’entité « MessageHistory » contient « PublishedTime » (DateTimeOffset) et « MessageText » (chaîne).|
||||

### <a name="sample-request"></a>Exemple de demande

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a>Exemple de réponse

```json
{
    "value": [
        {
            "Id": "EX20119",
            "Name": "EX20119",
            "Title": null,
            "StartTime": "2015-04-01T22:25:00Z",
            "EndTime": "2015-04-07T21:48:00Z",
            "Status": "Service restored",
            "Messages": [
                {
                    "PublishedTime": "2015-04-01T22:34:28.76Z",
                    "MessageText": "Current Status: Engineers are investigating an issue in which some customers may be experiencing problems accessing or using Exchange Online services or features. This event is actively being investigated. More information will be provided shortly."
                },
                {
                    "PublishedTime": "2015-04-03T18:45:32.56Z",
                    "MessageText": "Current Status: Engineers are implementing a fix within the affected infrastructure to remediate Exchange Online archive access issues. \n\nUser Experience: Affected users are unable to access online archives when using Outlook Web App (OWA). As a workaround, users may be able to access online archives via the Outlook client.\n\nCustomer Impact: Customer impact appears to be limited at this time. This issue only affects hybrid customers.\n\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues.  \n\nNext Update by: Monday, April 6, 2015, at 9:00 PM UTC\n"
                },
                {
                    "PublishedTime": "2015-04-06T21:17:34.007Z",
                    "MessageText": "Current Status: Deployment of the fix is almost complete. Engineers are monitoring service health to ensure the issue has been remediated. \n\nUser Experience: Affected users are unable to access online archives when using Outlook Web App (OWA). As a workaround, users may be able to access online archives via the Outlook client. \n\nCustomer Impact: Customer impact appears to be limited at this time. This issue only affects hybrid customers.\n\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues. \n\nNext Update by: Tuesday, April 7, 2015, at 10:00 PM UTC "
                },
                {
                    "PublishedTime": "2015-04-08T21:54:49.06Z",
                    "MessageText": "Final Status: Engineers have implemented a fix which remediated end-user impact. \r\n\r\nUser Experience: Affected users were unable to access online archives when using Outlook Web App (OWA).\r\n\r\nCustomer Impact: Customer impact appears to have been limited. This issue only affected hybrid customers.\r\n\r\nIncident Start Time: Monday, March 30, 2015, at 9:28 AM UTC\r\n\r\nIncident End Time: Tuesday, April 7, 2015, at 8:00 PM UTC\r\n\r\nPreliminary Root Cause: As part of our ongoing work, an updated certificate was deployed to the infrastructure; however, a caching issue has caused the infrastructure to use an expired certificate which is causing archive access issues.  \r\n\r\nNext Steps: The following is a list of known action item(s) associated with this incident. As part of the Office 365 problem management process, additional engineering actions may be identified to improve the overall service.\r\n- Action: Review the monitoring infrastructure for improvements as this event was reported by customers before an alert prompted a high priority investigation. \r\n\r\nA post-incident report will be available on the Service Health Dashboard within five business days."
                }
            ],
            "LastUpdatedTime": "2015-04-08T21:54:49.55Z",
            "Workload": "Exchange Online",
            "WorkloadDisplayName": "Exchange",
            "Feature": "Access",
            "FeatureDisplayName": "E-Mail and calendar access"
        },
        {
            "Id": "EX20789",
            "Name": "EX20789",
            "Title": null,
            "StartTime": "2015-04-06T20:00:00Z",
            "EndTime": "2015-04-07T23:00:00Z",
            "Status": "Service restored",
            "Messages": [
                {
                    "PublishedTime": "2015-04-07T23:26:44.643Z",
                    "MessageText": "Final Status: Engineers have validated that the deployed fix has resolved the issue and that service is restored.\r\n\r\nUser Experience: Affected users were unable to send or receive email while using Exchange Web Services (EWS) on their mobile devices.\r\n\r\nCustomer Impact: Customer impact appeared to be limited during this event. This issue was only affecting customers that use third-party Mobile Device Management software from Good Technology. As a workaround to provide immediate relief from impact, engineers implemented a configuration change for customers who reported this issue to Microsoft Support.\r\n\r\nIncident Start Time: Wednesday, April 1, 2015, at 2:00 PM UTC\r\n\r\nIncident End Time: Tuesday, April 7, 2015, at 10:00 PM UTC\r\n\r\nPreliminary Root Cause: As part of our ongoing efforts to improve service resiliency, an update was deployed to the infrastructure that facilitates connections from multiple Exchange Online protocols to mailbox databases. The update, however, contained a code issue that caused connectivity issues in some scenarios. \r\n\r\nNext Steps: The following is a list of known action item(s) associated with this incident. As part of the Office 365 problem management process, additional engineering actions may be identified to improve the overall service.\r\n- Action: Review the infrastructure update process to prevent reoccurrences of this scenario.\r\n\r\nPlease consider this service notification the final update on the event."
                }
            ],
            "LastUpdatedTime": "2015-04-07T23:26:45.08Z",
            "Workload": "Exchange Online",
            "WorkloadDisplayName": "Exchange",
            "Feature": "Access",
            "FeatureDisplayName": "E-Mail and calendar access"
        }
    ]
}
```

## <a name="errors"></a>Errors

Lorsque le service rencontre une erreur, il signale le code de la réponse d’erreur à l’appelant à l’aide de la syntaxe de code d’erreur HTTP standard. Selon la [spécification OData V4](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), des informations supplémentaires sont incluses dans le corps de l’appel ayant échoué en tant qu’objet JSON unique. Voici un exemple de corps d’erreur JSON complet :


```json
{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}
```
