---
ms.TocTitle: Office 365 Management Activity API reference
title: Référence de l’API Activité de gestion Office 365
description: Cet article explique comment utiliser l’API Activité de gestion Office 365 pour récupérer des informations sur les actions et les événements des utilisateurs, des administrateurs, du système et des stratégies à partir des journaux d’activité Office 365 et Azure AD.
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: 01/10/2018
ms.openlocfilehash: fc738a0974cf27ad2ad5e2d9795df220579751a3
ms.sourcegitcommit: 525c0d0e78cc44ea8cb6a4bdce1858cb4ef91d57
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2018
ms.locfileid: "25834839"
---
# <a name="office-365-management-activity-api-reference"></a>Référence de l’API Activité de gestion Office 365

Cet article explique comment utiliser l’API Activité de gestion Office 365 pour récupérer des informations sur les actions et les événements des utilisateurs, des administrateurs, du système et des stratégies à partir des journaux d’activité Office 365 et Azure AD. 

Vous pouvez utiliser les actions et les événements à partir des journaux d’audit et d’activité Office 365 et Microsoft Azure Active Directory pour créer des solutions de supervision, d’analyse et de visualisation des données. Ces solutions offrent aux organisations une meilleure visibilité sur les actions effectuées sur leur contenu. Ces actions et ces événements sont également disponibles dans les rapports d’activité Office 365. Pour en savoir plus, reportez-vous à l’article [Effectuer des recherches dans le journal d’audit dans le Centre de sécurité et de conformité Office 365](https://support.office.com/fr-FR/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).

L’API Activité de gestion Office 365 est un service web REST qui vous permet de développer des solutions à l’aide de n’importe quel langage et environnement d’hébergement qui prend en charge les certificats X.509 et HTTPS. L’API s’appuie sur Azure AD et le protocole OAuth2 pour l’authentification et l’autorisation. Pour accéder à l’API depuis votre application, inscrivez-la d’abord dans Azure AD et configurez-la avec les autorisations appropriées. Ainsi, votre application pourra demander les jetons d’accès OAuth2 dont elle a besoin pour appeler l’API. Pour en savoir plus, consultez l’article relatif à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).

> [!NOTE] 
> Pour obtenir des informations sur le schéma de données renvoyé par l’API Activité de gestion Office 365 ainsi que sur les problèmes connus et les modifications à venir risquant d’affecter votre implémentation, consultez l’article relatif au [schéma de l’API Activité de gestion Office 365](office-365-management-activity-api-schema.md).


## <a name="working-with-the-office-365-management-activity-api"></a>Utilisation de l’API Activité de gestion Office 365

L’API Activité de gestion Office 365 agrège des actions et des événements dans des blobs de contenu propres au locataire, classés selon le type et la source du contenu qu’ils contiennent. Actuellement, les types de contenu suivants sont pris en charge :

- Audit.AzureActiveDirectory
    
- Audit.Exchange
    
- Audit.SharePoint
    
- Audit.General (comprend toutes les autres charges de travail non incluses dans les types de contenu précédents)

- DLP.All (événements DLP liés à toutes les charges de travail)
    
Pour en savoir plus sur les événements et les propriétés associés à ces types de contenu, consultez l’article relatif au [schéma de l’API Activité de gestion Office 365](office-365-management-activity-api-schema.md).

Pour commencer à récupérer des blobs de contenu associés à un locataire, créez d’abord un abonnement aux types de contenu souhaités. Si vous récupérez des blobs de contenu associés à plusieurs locataires, créez un abonnement à chacun des types de contenu souhaités pour chaque client.

Une fois qu’un abonnement est créé, vous pouvez régulièrement l’interroger pour découvrir les nouveaux blobs de contenu disponibles au téléchargement. Sinon, vous pouvez inscrire un point de terminaison de webhook avec l’abonnement, auquel nous enverrons des notifications dès que de nouveaux blobs de contenu sont disponibles.


> [!NOTE] 
> Quand un abonnement est créé, il faut attendre jusqu’à 12 heures avant que les premiers blobs de contenu associés à cet abonnement deviennent disponibles. Les blobs de contenu sont créés en collectant et en agrégeant des actions et des événements sur plusieurs serveurs et centres de données. À la suite de ce processus distribué, les actions et les événements contenus dans les blobs de contenu n’apparaissent pas nécessairement dans l’ordre dans lequel ils ont eu lieu. Un blob de contenu peut contenir des actions et des événements qui ont eu lieu avant les actions et les événements contenus dans un blob de contenu antérieur. Nous mettons tout en œuvre pour réduire la latence entre l’occurrence des actions et des événements et leur disponibilité au sein d’un blob de contenu, mais nous ne pouvons pas garantir qu’elles apparaissent de manière séquentielle.


> [!NOTE] 
> Les données sensibles régies par les stratégies de protection contre la perte de données (DLP) sont disponibles dans l’API Flux d’activités uniquement pour les utilisateurs auxquels les autorisations « Lire les données sensibles DLP » ont été accordées. Pour en savoir plus, reportez-vous à l’article [Vue d’ensemble des stratégies de protection contre la perte de données](https://support.office.com/fr-FR/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e).

## <a name="activity-api-operations"></a>Opérations de l’API Activité

Toutes les opérations de l’API sont limitées à un seul locataire et l’URL racine de l’API inclut un ID de locataire qui spécifie le contexte du locataire. L’ID de locataire est un GUID. Pour savoir comment obtenir le GUID, consultez l’article relatif à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).


```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

Étant donné que les notifications que nous envoyons à votre webhook incluent l’**ID de locataire**, vous pouvez utiliser le même webhook pour recevoir des notifications pour tous les locataires.

Toutes les opérations de l’API nécessitent un en-tête HTTP d’autorisation avec un jeton d’accès provenant d’Azure AD. L’ID de locataire présent dans le jeton d’accès doit correspondre à l’ID de locataire indiqué dans l’URL racine de l’API. De plus, le jeton d’accès doit contenir la revendication ActivityFeed.Read (qui correspond à l’autorisation [Lire les données d’activité d’une organisation] configurée pour votre application dans Azure AD).

```json
Authorization: Bearer eyJ0e...Qa6wg
```

L’API Activité prend en charge les opérations suivantes :

- **Démarrer un abonnement** pour commencer à recevoir des notifications et récupérer les données d’activité d’un locataire.
    
- **Arrêter un abonnement** pour ne plus récupérer les données d’un locataire.
    
- **Répertorier les abonnements actifs**
    
- **Répertorier le contenu disponible** et les URL de contenu correspondantes.
    
- **Recevoir des notifications** envoyées par un webhook dès que du nouveau contenu est disponible.
    
- **Récupérer du contenu** à l’aide de l’URL de contenu.
    
- **Répertorier les notifications** envoyées par un webhook.

- **Récupérer les noms conviviaux des ressources** pour les objets du flux de données identifiés par un GUID.
    

## <a name="start-a-subscription"></a>Démarrer un abonnement

Cette opération démarre l’abonnement souscrit pour le type de contenu spécifié. Si un abonnement pour le type de contenu spécifié existe déjà, cette opération sert à :

- mettre à jour les propriétés d’un webhook actif.
    
- activer un webhook qui a été désactivé en raison du nombre excessif de notifications d’échec envoyées.
    
- réactiver un webhook expiré en spécifiant une date d’expiration Null ou ultérieure.
    
- supprimer un webhook.
    
||Abonnement|Description|
|:-----|:-----|:-----|
|**Chemin**| `/subscriptions/start?contentType={ContentType}`||
|**Paramètres**|contentType|Doit être un type de contenu valide.|
||PublisherIdentifier|GUID de locataire de l’éditeur qui code l’API. Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code. Ce paramètre permet de limiter le taux de requêtes émises. Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié. Toutes les requêtes reçues sans ce paramètre auront le même quota.|
|**Corps**|webhook|Cet objet JSON facultatif comprend trois propriétés :<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>address</b> : point de terminaison HTTPS obligatoire qui peut recevoir des notifications.  Un message test est envoyé au webhook pour valider le webhook avant de créer l’abonnement.</p></li><li><p><b>authId</b> : chaîne facultative incluse comme en-tête WebHook-AuthID dans les notifications envoyées au webhook pour identifier et autoriser la source de la requête envoyée au webhook.</p></li><li><p><b>expiration</b> : date/heure (valeur facultative) après laquelle les notifications ne doivent plus être envoyées au webhook.</p></li></ul>|
|**Réponse**|contentType|Type de contenu spécifié dans l’appel.|
||statut|Statut de l’abonnement. Si un abonnement est désactivé, vous ne pouvez pas répertorier ou récupérer du contenu.|
||webhook|Propriétés du webhook spécifiées dans l’appel avec l’état du webhook. Si le webhook est désactivé, vous ne recevez pas de notification, mais vous pouvez toujours répertorier et récupérer du contenu, à condition que l’abonnement soit activé.|

#### <a name="sample-request"></a>Exemple de demande

```json
POST {root}/subscriptions/start?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Content-Type: application/json; utf-8
Authorization: Bearer eyJ0e...Qa6wg

{
    "webhook" : {
        "address": "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": ""
    }
}

```


#### <a name="sample-response"></a>Exemple de réponse

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
    "contentType": "Audit.SharePoint",
    "status": "enabled",
    "webhook": {
        "status": "enabled",
        "address":  "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": null
    }
}

```


## <a name="webhook-validation"></a>Validation du webhook

Quand l’opération /start est appelée et un webhook est spécifié, nous vous envoyons une notification de validation à l’adresse de webhook indiquée pour confirmer qu’un détecteur actif peut accepter et traiter les notifications. Si nous ne recevons pas une réponse HTTP 200 OK, l’abonnement n’est pas créé. Sinon, si l’opération /start est appelée pour ajouter un webhook à un abonnement existant et si nous ne recevons pas une réponse HTTP 200 OK, le webhook n’est pas ajouté et l’abonnement reste inchangé.

#### <a name="sample-request"></a>Exemple de demande

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId) if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a>Exemple de réponse

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a>Arrêter un abonnement

Cette opération arrête un abonnement souscrit pour le type de contenu spécifié. 

Quand un abonnement est arrêté, vous ne recevez plus de notifications et vous ne pouvez pas récupérer le contenu disponible. Si, plus tard, vous décidez de redémarrer l’abonnement, vous aurez accès au nouveau contenu disponible à partir de ce moment-là. Vous ne pourrez pas récupérer le contenu mis à disposition pendant la période où l’abonnement était arrêté.


||Abonnement|Description|
|:-----|:-----|:-----|
|**Chemin**| `/subscriptions/stop?contentType={ContentType}`||
|**Paramètres**|contentType|Doit être un type de contenu valide.|
||PublisherIdentifier|GUID de locataire de l’éditeur qui code l’API. Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code. Ce paramètre permet de limiter le taux de requêtes émises. Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié. Toutes les requêtes reçues sans ce paramètre auront le même quota.|
|**Corps**|(vide)||
|**Réponse**|(vide)|||

#### <a name="sample-request"></a>Exemple de demande

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Exemple de réponse

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a>Répertorier les abonnements actifs

Cette opération renvoie une collection d’abonnements actifs avec les webhooks associés.

||Abonnement|Description|
|:-----|:-----|:-----|
|**Chemin**| `/subscriptions/list`||
|**Paramètres**|PublisherIdentifier|GUID de locataire de l’éditeur qui code l’API. Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code. Ce paramètre permet de limiter le taux de requêtes émises. Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié. Toutes les requêtes reçues sans ce paramètre auront le même quota.|
|**Corps**|(vide)||
|**Réponse**|Tableau JSON|Chaque abonnement est représenté par un objet JSON comprenant trois propriétés :<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>contentType</b> : indique le type de contenu.</p></li><li><p><b>status</b> : indique le statut de l’abonnement.</p></li><li><p><b>webhook</b> : indique le webhook configuré avec l’état (activé, désactivé, expiré) du webhook.  Si un abonnement n’a pas de webhook, la propriété du webhook est indiquée avec une valeur Null.</p></li></ul>|


#### <a name="sample-request"></a>Exemple de demande

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Exemple de réponse

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType" : "Audit.SharePoint",
        "status": "enabled",
        "webhook": {
            "status": "enabled",
            "address": "https://webhook.myapp.com/o365/",
            "authId": "o365activityapinotification",
            "expiration": null
        }
    },

    ...

    {
        "contentType": "Audit.Exchange",
        "webhook": null
    }
]

```


## <a name="list-available-content"></a>Répertorier le contenu disponible

Cette opération répertorie le contenu actuellement disponible que vous pouvez récupérer pour le type de contenu spécifié. Le contenu est une agrégation des actions et des événements collectés sur plusieurs serveurs de plusieurs centres de données. Le contenu est répertorié dans l’ordre de mise à disposition des agrégations. En revanche, nous ne pouvons pas garantir que les événements et les actions des agrégations sont répertoriés de manière séquentielle. Une erreur est renvoyée si l’état de l’abonnement est désactivé.


||Abonnement|Description|
|:-----|:-----|:-----|
|**Chemin**| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|**Paramètres**|contentType|Doit être un type de contenu valide.|
||PublisherIdentifier|GUID de locataire de l’éditeur qui code l’API. Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code. Ce paramètre permet de limiter le taux de requêtes émises. Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié. Toutes les requêtes reçues sans ce paramètre auront le même quota.|
||startTimeendTime|Date/Heure (UTC) facultative indiquant l’intervalle de temps à prendre en compte pour renvoyer le contenu, selon le moment à partir duquel le contenu est devenu disponible. L’intervalle de temps est compris entre l’heure de début (startTime <= contentCreated) et l’heure de fin (contentCreated < endTime). Ainsi, les intervalles de temps sont incrémentés sans se chevaucher pour permettre de parcourir le contenu disponible.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>YYYY-MM-DD</p></li><li><p>YYYY-MM-DDTHH:MM</p></li><li><p>YYYY-MM-DDTHH:MM:SS</p></li></ul>L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours. Par défaut, si l’heure de début et l’heure de fin ne sont pas renseignées, le contenu disponible au cours des dernières 24 heures est renvoyé.<p>**REMARQUE** : même si l’heure de début et l’heure de fin peuvent être espacées de plus de 24 heures, nous vous déconseillons de le faire. Par ailleurs, si vous obtenez des résultats en réponse à une requête portant sur un intervalle de plus de 24 heures, ces résultats peuvent être partiels et ne doivent pas être pris en compte. L’intervalle de la requête émise entre l’heure de début et l’heure de fin doit couvrir une plage horaire de moins de 24 heures.</p>|
|**Réponse**|Tableau JSON|Le contenu disponible est représenté par des objets JSON comprenant les propriétés suivantes :<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>contentType</b> : indique le type de contenu.</p></li><li><p><b>contentId</b> : chaîne opaque qui identifie le contenu.</p></li><li><p><b>contentUri</b> : URL à utiliser pour récupérer le contenu.</p></li><li><p><b>contentCreated</b> : date/heure à laquelle le contenu est disponible.</p></li><li><p><b>contentExpiration</b> : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</p></li></ul>|


#### <a name="sample-request"></a>Exemple de demande

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Exemple de réponse

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z"
    },
    ...
]

```


### <a name="pagination"></a>Pagination

Quand vous répertoriez le contenu disponible au cours d’un intervalle de temps donné, le nombre de résultats renvoyés est limité pour éviter de dépasser le délai de réponse. Si d’autres résultats correspondent à l’intervalle de temps spécifié mais ne peuvent pas être renvoyés dans une seule réponse, les résultats sont tronqués et un en-tête est ajouté à la réponse indiquant l’URL à utiliser pour accéder à la page de résultats suivante. L’URL contient les mêmes paramètres _startTime_ et _endTime_ qui ont été spécifiés dans la requête d’origine, ainsi qu’un paramètre indiquant l’ID interne de la page suivante. Si les paramètres _startTime_ et _endTime_ ne sont pas spécifiés dans la requête d’origine, ils indiquent l’intervalle de 24 heures qui précède la requête d’origine.


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

Pour répertorier tout le contenu disponible dans un intervalle de temps spécifié, vous devrez peut-être récupérer plusieurs pages jusqu’à ce que vous receviez une réponse qui ne contient pas l’en-tête **NextPageUri**.


## <a name="receiving-notifications"></a>Réception des notifications

Les notifications sont envoyées au webhook configuré pour un abonnement au fur et à mesure que le nouveau contenu devient disponible. Étant donné que les notifications incluent l’ID de locataire, vous pouvez utiliser le même webhook pour recevoir des notifications pour tous les locataires auxquels vous êtes abonné.

La notification est envoyée sous la forme d’une requête HTTP POST sur TLS (TLS 1.0 et versions ultérieures) à l’adresse de webhook spécifiée. Si la configuration du webhook inclut un ID d’authentification, nous l’envoyons comme en-tête HTTP : Webhook-AuthID. Les réponses qui n’incluent pas HTTP 200 OK seront considérées comme ayant échoué et la notification sera renvoyée. Vous pouvez également configurer votre webhook pour exiger une authentification basée sur les certificats clients ; nous nous authentifierons alors à l’aide du certificat manage.office.com.

Le corps de la requête contiendra une matrice comprenant un ou plusieurs objets JSON qui représentent les blobs de contenu disponibles. Le nombre de blobs de contenu compris dans chaque notification est limité pour réduire au maximum la taille de la notification. Dans la mesure où cette limite peut être modifiée, votre implémentation doit interroger la longueur de la matrice au lieu de prévoir une taille fixe. Chaque objet inclura les mêmes propriétés renvoyées par l’opération /content ainsi que le GUID du locataire auquel appartiennent les données et le GUID de l’application ayant créé les abonnements. Ainsi, le webhook peut établir le contexte dans lequel il est utilisé avec plusieurs locataires et applications.

- **tenantId** : GUID du locataire auquel appartient le contenu.
    
- **clientId** : GUID de votre application qui a créé l’abonnement.
    
- **contentType** : indique le type de contenu.
    
- **contentId** : chaîne opaque qui identifie le contenu.
    
- **contentUri** : URL à utiliser pour récupérer le contenu.
    
- **contentCreated** : date/heure à laquelle le contenu est disponible.
    
- **contentExpiration** : date/heure après laquelle vous ne pouvez plus récupérer le contenu.
    
Vous trouverez ci-dessous un exemple de notification.

```json
POST https://webhook.myapp.com/o365/ 
Content-Type: application/json; utf-8
Webhook-AuthID: o365activityapinotification

[
    {
        "tenantId": "{GUID}"
        "clientId": "{GUID}"
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z"
    },
    ...
]

```


## <a name="notification-failure-and-retry"></a>Échec de notification et nouvelle tentative

Le système de notification envoie des notifications dès que du nouveau contenu est disponible. Si l’envoi des notifications échoue à de multiples reprises, le délai d’attente entre chaque nouvelle tentative augmente. Si l’envoi des notifications continue d’échouer, nous nous réservons le droit de désactiver le webhook et d’arrêter de lui envoyer des notifications. L’opération /start peut être utilisée pour réactiver un webhook désactivé.


## <a name="retrieving-content"></a>Récupérer du contenu

Pour récupérer un blob de contenu, envoyez une requête GET à l’URI de contenu correspondante qui figure dans la liste du contenu disponible et dans les notifications envoyées au webhook. Le contenu renvoyé correspondra à une collection d’un ou de plusieurs événements ou actions au format JSON.

#### <a name="sample-request"></a>Exemple de demande

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a>Exemple de réponse

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "CreationTime": "2015-06-29T20:03:19",
        "Id": "80c76bd2-9d81-4c57-a97a-accfc3443dca",
        "Operation": "PasswordLogonInitialAuthUsingPassword",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 9,
        "ResultStatus": "failed",
        "UserKey": "1153977025279851686@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ClientIP": "134.170.188.221",
        "ObjectId": "admin@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "ExtendedProperties": [
            {
                "Name": "LoginError",
                "Value": "-2147217390;PP_E_BAD_PASSWORD;The entered and stored passwords do not match."
            }
        ],
        "Client": "Exchange",
        "LoginStatus": -2147217390,
        "UserDomain": "contoso.onmicrosoft.com"
    },
    {
        "CreationTime": "2015-06-29T20:03:34",
        "Id": "4e655d3f-35fa-42e0-b050-264b2d255c7a",
        "Operation": "PasswordLogonInitialAuthUsingPassword",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 9,
        "ResultStatus": "success",
        "UserKey": "1153977025279851686@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ClientIP": "134.170.188.221",
        "ObjectId": "admin@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "Client": "Exchange",
        "LoginStatus": 0,
        "UserDomain": "contoso.onmicrosoft.com"
    },
    {
        "CreationTime": "2015-06-29T20:04:55",
        "Id": "b567caf0-088e-4c1c-a4ea-633a1e3d66c8",
        "Operation": "Add User.",
        "OrganizationId": "41463f53-8812-40f4-890f-865bf6e35190",
        "RecordType": 8,
        "ResultStatus": "success",
        "UserKey": "1003BFFD8EC47CA6@contoso.onmicrosoft.com",
        "UserType": 0,
        "Workload": "AzureActiveDirectory",
        "ObjectId": "user001@contoso.onmicrosoft.com",
        "UserId": "admin@contoso.onmicrosoft.com",
        "AzureActiveDirectoryEventType": 0,
        "Actor": [
            {
                "ID": "1cef1fdb-ff52-48c4-8e4e-dfb5ea83d357",
                "Type": 2
            },
            {
                "ID": "admin@contoso.onmicrosoft.com",
                "Type": 5
            },
            {
                "ID": "1003BFFD8EC47CA6",
                "Type": 3
            }
        ],
        "ActorContextId": "41463f53-8812-40f4-890f-865bf6e35190",
        "InterSystemsId": "c2ced078-ad57-4079-a743-5c37f5284790",
        "IntraSystemId": "d1497f7e-15b4-49aa-83ad-11a17ca4a2f4",
        "Target": [
            {
                "ID": "user001@contoso.onmicrosoft.com",
                "Type": 5
            },
            {
                "ID": "10037FFE91510806",
                "Type": 3
            }
        ],
        "TargetContextId": "41463f53-8812-40f4-890f-865bf6e35190"
    }
]

```


## <a name="list-notifications"></a>Répertorier les notifications

Cette opération répertorie toutes les tentatives de notification associées au type de contenu spécifié. Si vous n’avez pas inclus un webhook au démarrage de l’abonnement souscrit pour le type de contenu, aucune notification ne pourra être récupérée. Dans la mesure où nous renvoyons les notifications en cas d’échec de l’envoi initial, cette opération peut renvoyer plusieurs notifications pour le même contenu. Par ailleurs, l’ordre dans lequel les notifications sont envoyées ne correspond pas nécessairement à l’ordre de parution du contenu (en particulier en cas d’échecs et de nouvelles tentatives). 

Vous pouvez utiliser cette opération pour vous aider à résoudre les problèmes liés aux webhooks et aux notifications, mais nous vous déconseillons de l’utiliser pour déterminer le contenu disponible que vous pouvez récupérer. Pour cela, utilisez plutôt l’opération /content. Nous renvoyons une erreur si l’état de l’abonnement est désactivé.


||Abonnement|Description|
|:-----|:-----|:-----|
|**Chemin**| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|**Paramètres**|contentType|Doit être un type de contenu valide.|
||PublisherIdentifier|GUID de locataire de l’éditeur qui code l’API. Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code. Ce paramètre permet de limiter le taux de requêtes émises. Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié. Toutes les requêtes reçues sans ce paramètre auront le même quota.|
||startTimeendTime|Date/Heure (UTC) facultative indiquant l’intervalle de temps à prendre en compte pour renvoyer le contenu, selon le moment à partir duquel le contenu est devenu disponible. L’intervalle de temps est délimité par les paramètres _startTime_ (_startTime_ <= contentCreated) et _endTime_ (_contentCreated_ < endTime). Ainsi, les intervalles de temps sont incrémentés sans se chevaucher pour permettre de parcourir le contenu disponible.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>YYYY-MM-DD</p></li><li><p>YYYY-MM-DDTHH:MM</p></li><li><p>YYYY-MM-DDTHH:MM:SS</p></li></ul>L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours. Par défaut, si les paramètres _startTime_ et _endTime_ ne sont pas renseignés, le contenu disponible au cours des dernières 24 heures est renvoyé.|
|**Réponse**|Tableau JSON|Les notifications sont représentées par des objets JSON comprenant les propriétés suivantes : <ul><li>**contentType** : indique le type de contenu.</li><li>**contentId** : chaîne opaque qui identifie le contenu.</li><li>**contentUri** : URL à utiliser pour récupérer le contenu. </li><li>**contentCreated** : date/heure à laquelle le contenu est disponible.</li><li>**contentExpiration** : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</li><li>**notificationSent** : date/heure d’envoi de la notification.</li><li>**notificationStatus** : indique la réussite ou l’échec de la tentative de notification.</li></ul>|

#### <a name="sample-request"></a>Exemple de demande

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a>Exemple de réponse

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

[
    {
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z",
        "notificationSent": "2015-05-23T17:36:00.000Z",
        "notificationStatus": "success"

    },
    ...
]

```


### <a name="pagination"></a>Pagination

Quand vous répertoriez l’historique de notification au cours d’un intervalle de temps donné, le nombre de résultats renvoyés est limité pour éviter de dépasser le délai de réponse. Si d’autres résultats correspondent à l’intervalle de temps spécifié mais ne peuvent pas être renvoyés dans une seule réponse, les résultats sont tronqués et un en-tête est ajouté à la réponse indiquant l’URL à utiliser pour accéder à la page de résultats suivante. L’URL contient les mêmes paramètres _startTime_ et _endTime_ qui ont été spécifiés dans la requête d’origine, ainsi qu’un paramètre indiquant l’ID interne de la page suivante. Si les paramètres _startTime_ et _endTime_ ne sont pas spécifiés dans la requête d’origine, ils indiquent l’intervalle de 24 heures qui précède la requête d’origine.

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

Pour répertorier tout le contenu disponible dans un intervalle de temps spécifié, vous devrez peut-être récupérer plusieurs pages jusqu’à ce que vous receviez une réponse qui ne contient pas l’en-tête **NextPageUrl**.

## <a name="retrieve-resource-friendly-names"></a>Récupération des noms conviviaux des ressources

Cette opération récupère les noms conviviaux des ressources pour les objets du flux de données identifiés par un GUID. « DlpSensitiveType » est actuellement le seul objet pris en charge. 


||Abonnement|Description|
|:-----|:-----|:-----|
|**Chemin**| `/resources/dlpSensitiveTypes`||
|**Paramètres**|PublisherIdentifier|GUID de locataire de l’éditeur qui code l’API. Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code. Ce paramètre permet de limiter le taux de requêtes émises. Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié. Toutes les requêtes reçues sans ce paramètre auront le même quota.|
|**En-têtes**|Accept-Language|En-tête pour spécifier la langue dans laquelle les noms doivent être localisés. Par exemple, utilisez « en-US » pour l’anglais ou « es » pour l’espagnol. La langue par défaut (en-US) est renvoyée si cet en-tête n’est pas présent.|
|**Corps**|(vide)||
|**Réponse**|Tableau JSON|Le contenu disponible est représenté par des objets JSON comprenant les propriétés suivantes :<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><b>id</b> : indique le GUID du type d’informations sensibles.</p></li><li><p><b>name</b> : nom convivial du type d’informations sensibles.</p></li></ul>|

#### <a name="sample-request"></a>Exemple de demande

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a>Exemple de réponse

```json
HTTP/1.1 200 OK

[
    {
        "id": "50842eb7-edc8-4019-85dd-5a5c1f2bb085",
        "name": "CreditCardNumber"
    }, 
    {
        "id": "0e9b3178-9678-47dd-a509-37222ca96b42",
        "name": "EUDebitCardNumber"
    }, 
    ...
    {
    }
]

```

## <a name="api-throttling"></a>Limitation des requêtes de l’API

Chaque éditeur qui code l’API reçoit un quota dédié qui limite le nombre de requêtes envoyées à 60 000 requêtes par minute. Pour obtenir le quota dédié, renseignez le paramètre PublisherIdentifier dans toutes vos requêtes. Les requêtes contenant le même PublisherIdentifier auront le même quota. Toutes les requêtes ne contenant aucun PublisherIdentifier auront le même quota que le GUID 00000000-0000-0000-0000-000000000000.

Si Office 365 doit vous contacter pour vous faire part d’un problème, vérifiez que l’abonnement du locataire dont le GUID sert de PublisherIdentifier contient des informations exactes et à jour sur le contact. Aucun abonnement ne doit être souscrit pour ce locataire.

Pour les clients qui développent leurs solutions à l’aide de cette API, nous leur recommandons d’utiliser leur propre GUID de locataire pour éviter toute concurrence due à un quota partagé limité.

> [!NOTE] 
> Même si chaque éditeur peut envoyer 60 000 requêtes par minute, Microsoft ne peut garantir le taux de réponse. Le taux de réponse dépend de différents facteurs, tels que les performances du système client, la capacité réseau et la vitesse du réseau.  Un éditeur peut soumettre 60 000 requêtes par minute, mais ne vous attendez pas à recevoir des réponses pour les 60 000 requêtes au cours de cette minute. Si un éditeur souhaite effectuer un test d’évaluation sur une application cliente, il doit le faire dans tous les environnements dans lesquels il prévoit d’exécuter l’application cliente, car les résultats peuvent varier d’un environnement à l’autre.

## <a name="errors"></a>Erreurs

Quand le service rencontre une erreur, il signale le code de la réponse d’erreur à l’appelant en utilisant la syntaxe du code d’erreur HTTP standard. . Des informations complémentaires sont incluses dans le corps de l’appel ayant échoué en tant qu’objet JSON unique. Voici un exemple du corps complet de l’erreur JSON : 

```json

{ 
    "error":{ 
        "code":"AF50000",
        "message": "An internal server error occurred. Retry the request."
    } 
}

```


|||
|:-----|:-----|
|Code|Message|
|AF10001|Le jeu d’autorisations ({0}) envoyé dans la requête n’inclut pas l’autorisation **ActivityFeed.Read** attendue.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = jeu d’autorisations défini dans le jeton d’accès.</p></li></ul>|
|AF20001|Paramètre manquant : {0}. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = nom du paramètre manquant.</p></li></ul>|
|AF20002|Type de paramètre non valide : {0}. Type attendu : {1}.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = nom du paramètre non valide.</p></li><li><p>{1} = type attendu (int, datetime, guid).</p></li></ul>|
|AF20003|L’expiration {0} fournie indique une date et une heure passées.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = expiration transmise dans l’appel de l’API.</p></li></ul>|
|AF20010|L’ID de locataire transmis dans l’URL ({0}) ne correspond pas à l’ID de locataire transmis dans le jeton d’accès ({1}).<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = ID de locataire transmis dans l’URL</p></li><li><p>{1} = ID de locataire transmis dans le jeton d’accès</p></li></ul>|
|AF20011|L’ID de locataire spécifié ({0}) n’existe pas dans le système ou a été supprimé. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   {0} = ID de locataire transmis dans l’URL</p></li></ul>|
|AF20012|L’ID de locataire spécifié ({0}) est configuré de façon incorrecte dans le système. <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    {0} = ID de locataire transmis dans l’URL</p></li></ul>|
|AF20013|L’ID de locataire transmis dans l’URL ({0}) n’est pas un GUID valide.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> {0} = ID de locataire transmis dans l’URL</p></li></ul>|
|AF20020|Le type de contenu spécifié n’est pas valide.|
|AF20021|Le point de terminaison de webhook {{0}) n’a pas été validé. {1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = adresse de webhook.</p></li><li><p>{1} = « Le point de terminaison n’a pas renvoyé HTTP 200. » ou « L’adresse doit commencer par HTTPS. ».</p></li></ul>|
|AF20022|Aucun abonnement trouvé pour le type de contenu spécifié.|
|AF20023|L’abonnement a été désactivé par {0}.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = « un administrateur du locataire » ou « administrateur du service »</p></li></ul>|
|AF20030|L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.|
|AF20031|Saisie nextPage non valide : {0}.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = indicateur de la page suivante transmis dans l’URL</p></li></ul>|
|AF20050|Le contenu spécifié ({0}) n’existe pas.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = ID ou URL de la ressource</p></li></ul>|
|AF20051|Le contenu demandé avec la touche {0} a déjà expiré. Le contenu datant de plus de 7 jours ne peut pas être récupéré.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>•    {0} = ID ou URL de la ressource</p></li></ul>|
|AF20052|L’ID de contenu {0} dans l’URL n’est pas valide.<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = ID ou URL de la ressource</p></li></ul>|
|AF20053|Une seule langue peut être indiquée dans l’en-tête Accept-Language.|
|AF20054|Syntaxe non valide dans l’en-tête Accept-Language.|
|AF429|Trop de demandes. Method={0}, PublisherId={1}<ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>{0} = méthode HTTP</p></li><li><p>{1} = GUID de locataire utilisé en tant que PublisherIdentifier</p></li></ul>|
|AF50000|Une erreur interne s’est produite. Retentez la requête.|
