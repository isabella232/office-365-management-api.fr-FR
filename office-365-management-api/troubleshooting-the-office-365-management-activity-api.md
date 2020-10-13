---
ms.technology: o365-service-communications
ms.TocTitle: Troubleshooting the Office 365 Management Activity API
title: Résolution des problèmes de l’API Activité de gestion Office 365
description: Cet article présente les questions les plus fréquemment posées au Support Microsoft concernant cette API.
ms.ContentId: 50822603-a1ec-a754-e7dc-67afe36bb1b0
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 218c0517697f1d71b1557f3b55a4c184fb52ec54
ms.sourcegitcommit: c9cb078e6c94bcf0bb28cb0fffef39302ec8c197
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/12/2020
ms.locfileid: "48425618"
---
# <a name="office-365-management-activity-api-faqs-and-troubleshooting"></a>FAQ sur l'API de l'activité de gestion d'Office 365 et résolution des problèmes

L'API de l'activité de gestion d'Office 365 (également connue sous le nom d'*API d'audit unifié*) fait partie des offres de sécurité et de conformité d'Office 365, qui :

- Elle autorise l’accès par programme à plusieurs charges de travail du pipeline d’audit (par exemple, SharePoint et Exchange).

- Elle est l’interface principale utilisée par un large éventail de produits tiers pour agréger et indexer les données d’audit.

L’API Activité de gestion ne doit pas être confondue avec l’API Communications de service Office 365. L’API Activité de gestion vous permet d’auditer les activités des utilisateurs finals dans différentes charges de travail. L’API Communications de service, quant à elle, sert à auditer l’état et les messages envoyés par les services disponibles dans Office 365 (par exemple, Dynamics CRM ou Identité du service).

## <a name="frequently-asked-questions-about-the-office-365-management-activity-api"></a>Questions fréquemment posées sur l'API de l'activité de gestion de l'Office 365

**Comment intégrer à l’API Activité de gestion ?**

Pour commencer à utiliser l’API Activité de gestion Office 365, reportez-vous à [Prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).

**Que se passe-t-il si je désactive l’audit pour mon organisation Office 365 ? Est-ce que je reçois encore des événements via l’API Activité de gestion ?**

Non.L’audit unifié d’Office 365 doit être activé pour votre organisation pour que les enregistrements puissent être collectés via l’API Activité de gestion. Pour obtenir des instructions, voir [Activer ou désactiver la recherche dans le journal d'audit](https://docs.microsoft.com/microsoft-365/compliance/turn-audit-log-search-on-or-off).

**Quels événements sont audités pour un service Office 365 spécifique ?**

La documentation du schéma de l’API Activité de gestion Office 365 comprend la liste complète des événements. Pour plus d’informations, voir le Schéma de l’API Activité de gestion Office 365. Consultez également la section « Activités auditées » dans [Effectuer des recherches dans le journal d’audit dans le Centre de sécurité et conformité](https://docs.microsoft.com/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance#audited-activities) pour obtenir la liste des événements de la plupart des services Office 365 audités.

**Existe-t-il des différences entre les enregistrements récupérés par l’API Activité de gestion et les enregistrements renvoyés à l’aide de l’outil de recherche de journal d’audit dans le Centre de sécurité et conformité Microsoft 365 ?**

Les données renvoyées par les deux méthodes sont identiques. La seule différence réside dans le fait que, avec l’API, vous pouvez obtenir des données pour les 7 derniers jours uniquement (plus de détails dans les questions ci-dessous). Lors de la recherche du journal d’audit dans le Centre de sécurité et conformité (ou à l’aide de la cmdlet **Search-UnifiedAuditLog** correspondante dans Exchange Online PowerShell), vous pouvez obtenir les données de la période de rétention en vigueur lorsque les données sont générées (par exemple, 90 jours ou un an).

**Quel est le délai maximum d'attente avant l'envoi d'une notification concernant un événement donné d'Office 365 ?**

Il n'y a pas de délai maximal garanti pour la livraison des notifications (en d'autres termes, pas de contrat de niveau de service). En règle générale, la plupart des notifications sont envoyées dans l’heure suivant l’événement. Le délai est souvent beaucoup plus court, mais il peut être plus long, car il peut varier en fonction de la charge de travail.

**Les notifications webhook ne sont-elles pas plus immédiates ?**

Non. Dernièrement, les délais des notifications sont plus longs avec un webhook qu’en interrogeant directement l’API à l’aide de l’opération `/content`.

**Pendant combien de temps le contenu restera-t-il disponible pour récupération via l’API ?**

Le contenu est disponible pour récupération via l’API pendant 7 jours après l’envoi de la notification de disponibilité. Même si la notification est retardée pendant un certain temps (par exemple, dans le cas d’une interruption de service), il vous reste 7 jours après la date d’envoi initial de la notification pour télécharger le blob de contenu lié à l’événement d’origine.

**Puis-je interroger l'API d'activité de gestion pour un ID d'événement ou un RecordType particulier ou d'autres propriétés dans le blob de contenu ?**

Non. L’API de gestion des activités fournit tous les détails de l’événement pour un journal particulier. Elle peut être utilisée pour télécharger les détails complets, puis vous pouvez implémenter votre propre logique de requête sur les données téléchargées. Par exemple, à l’aide d’une application personnalisée ou d’un outil tiers.

**Comment savoir si les données provenant de ma solution d’audit existante, qui collecte des données auprès de l’API Activité de gestion, sont précises et complètes ?**

En bref, Microsoft ne fournit aucun type de journal qui vous permet de vérifier une application donnée ou tierce (ISV). Il existe d'autres produits de sécurité Microsoft qui obtiennent leurs données à partir du même pipeline, mais ils n'entrent pas dans le cadre de cette discussion et ne peuvent pas être utilisés pour recouper directement l'API Activité de gestion. Si vous vous préoccupez des différences pouvant exister entre ce que votre solution vous fournit et ce dont vous en attendez, nous vous recommandons d’implémenter les opérations illustrées ci-dessus. Cette démarche peut être difficile à réaliser selon la méthode employée par votre outil ou votre solution pour lister et indexer les données. Si votre solution existante ne présente que des données triées par heure de création de l'événement, il n'y a aucun moyen d'interroger l'API par heure de création de l'événement afin de comparer les ensembles de résultats. Dans ce cas, il faudrait collecter les blobs de contenu notifiés pendant plusieurs jours, les indexer ou les trier manuellement, puis faire une comparaison manuelle.

**Quel est le seuil de limitation pour l’API Activité de gestion ?**

Les organisations reçoivent une ligne de base de 2 000 demandes par minute. La limite de limitation est ensuite ajustée sur la base d’une combinaison de facteurs, notamment le nombre de sièges au sein de l’organisation. En outre, les organisations Office 365 E5 et Microsoft 365 E5 disposeront d’environ deux fois plus de bande passante que les organisations autres que E5. La bande passante aura également un plafond maximal pour protéger l’état d’intégrité du service.

> [!NOTE]
> Même si chaque client peut initialement envoyer 2 000 requêtes par minute, Microsoft ne peut garantir le taux de réponse. Le taux de réponse dépend de différents facteurs, tels que les performances du système client, la capacité et la vitesse du réseau.

**Je rencontre une erreur de limitation dans l’API Activité de gestion. Que dois-je faire ?**

Ouvrez un ticket avec le Support Microsoft et demandez un nouveau seuil de limitation et incluez une justification professionnelle pour augmenter la limite. Nous évaluerons la demande et si nous l’acceptons, nous augmenterons le seuil de limitation.

**Pourquoi les propriétés TargetUpdatedProperties n’apparaissent plus dans ExtendedProperties dans les journaux d’audit associés aux activités d’Azure Active Directory ?**

Les propriétés TargetUpdatedProperties figuraient dans ExtendedProperties. Toutefois, elles ont été supprimées de ExtendedProperties et apparaissent désormais dans ModifiedProperties.

## <a name="troubleshooting-the-office-365-management-activity-api"></a>Résolution des problèmes de l’API Activité de gestion Office 365

Tout d’abord, les personnes qui utilisent pour la première fois l’API Activité de gestion Office 365 doivent savoir que les charges de travail ne peuvent être interrogées en fonction des spécificités d’un événement (par exemple la date à laquelle l’événement s’est produit, la collection de sites à partir de laquelle l’événement a été déclenché ou le type d’événement). En effet, vous devez créer des abonnements à des charges de travail spécifiques (par exemple, SharePoint ou Azure AD), chaque abonnement correspondant à un seul locataire.

Les sections suivantes résument les questions les plus fréquentes que les clients se posent lors de l’utilisation de l’API d’activité de gestion d’Office 365 :

- [Questions sur les clients et les outils tiers](#questions-about-third-party-tools-and-clients)

- [Activation du journal d’audit unifié dans Office 365](#enabling-unified-audit-logging-in-office-365)

- [Connexion à l’API](#connecting-to-the-api)

- [Vérification de vos abonnements](#checking-your-subscriptions)

- [Création d’un nouvel abonnement](#creating-a-new-subscription)

- [Utilisation des webhooks](#using-webhooks)

- [Requête de blobs de contenu et limitation de requêtes](#requesting-content-blobs-and-throttling)

Nous allons vous proposer une sélection de scripts PowerShell simples pour vous aider à répondre aux questions les plus fréquemment posées par les clients ou à implémenter une solution personnalisée en montrant les principales opérations à réaliser. Toutes les opérations ne sont pas expliquées dans ces sections, mais elles sont toutes répertoriées dans la référence API de l'activité de gestion d'Office 365. 

### <a name="questions-about-third-party-tools-and-clients"></a>Questions sur les clients et les outils tiers

Les questions les plus courantes auxquelles nous répondons sont posées par des clients qui utilisent des produits tiers pour télécharger et agréger des données d’audit. Selon le produit tiers, les clients peuvent éprouver des difficultés pendant la configuration ou rencontrer une interruption ou une incohérence dans les données figurant dans ces produits. En premier lieu, ces clients doivent contacter l’équipe de support de leur fournisseur. Généralement, un problème de configuration ou de service d'un fournisseur spécifique au locataire est la cause des plaintes des clients.

### <a name="enabling-unified-audit-logging-in-office-365"></a>Activation de la journalisation d’audit unifié dans Office 365

Si vous venez de configurer une application qui tente sans succès d’utiliser l’API d’activités de gestion, vérifiez que vous avez activé la journalisation d’audit unifié pour votre organisation Office 365. Pour ce faire, vous devez activer le journal d’audit d’Office 365. Pour obtenir des instructions, consultez la rubrique [Activer ou désactiver la recherche dans un journal d’audit Office 365](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).

Si l’audit unifié n’est pas activé, un message d’erreur contenant la chaîne suivante s’affiche généralement : `Microsoft.Office.Compliance.Audit``.DataServiceException: Tenant <tenantID> does not exist.`

### <a name="connecting-to-the-api"></a>Connexion à l’API

La plupart des applications se connectent à l’API à l’aide d’un simple flux OAuth2 d’informations d’identification du client. Par conséquent, la première étape consiste à créer une application Azure AD ayant les autorisations nécessaires pour accéder aux données de l’API Activité de gestion. Nous ne pouvons pas vous expliquer dans cet article comment créer une inscription d’application Azure AD. Pour en savoir plus, consultez l’article relatif à l’[inscription d’une application avec le locataire Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).

#### <a name="azure-application-permissions"></a>Autorisations de l’application Azure

Les trois autorisations actuellement utilisées pour l’API Activité de gestion Office 365 sont les suivantes :

1. Lire les données d’activité de votre organisation

2. Lire les informations d’état du service de votre organisation

3. Lire les événements de la politique Protection contre la perte de données (DLP), y compris les informations sensibles détectées

> [!NOTE]
> Nous vous recommandons d’activer les Autorisations d’application et les Autorisations déléguées au moins pour les deux premiers jeux d’autorisations ci-dessus. L’autorisation Lire les événements de la stratégie DLP vous sera utile uniquement si vous êtes intéressé par les charges de travail DLP.

#### <a name="getting-an-access-token"></a>Obtention d’un jeton d’accès

Le script PowerShell suivant utilise l’ID de l’application et une clé secrète client pour obtenir le jeton OAuth2 auprès du point de terminaison d’authentification de l’API Activité de gestion. Il place ensuite le jeton d'accès dans la `$headerParams` variable de tableau, que vous joindrez à votre requête HTTP. Pour la valeur du point de terminaison de l’API (dans la variable $resource), utilisez l’une des valeurs suivantes, selon l’offre d’abonnement Microsoft 365 ou Office 365 de votre organisation :

- Offre pour le secteur privé : `manage.office.com`

- Offre pour le secteur public (Cloud de la communauté du secteur public) : `manage-gcc.office.com`

- Offre pour le secteur public (Cloud de la communauté du secteur public à haute disponibilité, ou « GCC High  ») : `manage.office365.us`

- Offre pour le secteur public (Département de la Défense) : `manage.protection.apps.mil`

```powershell
# Create app of type Web app / API in Azure AD, generate a Client Secret, and update the client id and client secret here
$ClientID = "<YOUR_APPLICATION_ID"
$ClientSecret = "<YOUR_CLIENT_SECRET>"
$loginURL = "https://login.microsoftonline.com/"
$tenantdomain = "<YOUR_DOMAIN>.onmicrosoft.com"
# Get the tenant GUID from Properties | Directory ID under the Azure Active Directory section. For $resource, use one of these endpoint values based on your subscription plan: Enterprise - manage.office.com; GCC - manage-gcc.office.com; GCC High: manage.office365.us; DoD: manage.protection.apps.mil
$TenantGUID = "<YOUR_TENANT_GUID>"
$resource = "https://<YOUR_API_ENDPOINT>"
# auth
$body = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
$headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"} 
```

La variable `$oauth` contient l’objet de réponse, qui comporte plusieurs propriétés dont le jeton d’accès. Voici un exemple de réponse :

```json
token_type     : Bearer
expires_in     : 3599
ext_expires_in : 0
expires_on     : 1508285860
not_before     : 1508281960
resource       : https://manage.office.com
access_token   : eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyIsImtpZCI6IjJLVmN1enFBaWRPTHFXU2FvbDd3Z0ZSR0NZbyJ9.eyJhdWQiOiJodHRwczov…
```

### <a name="checking-your-subscriptions"></a>Vérification de vos abonnements

Quand on constate une interruption du flux de données à destination d’une solution ou d’un client de l’API Activité de gestion existant, il est normal de se demander si quelque chose est arrivé à l’abonnement. Pour vérifier vos abonnements actifs, ajoutez ce qui suit au script précédent :

```powershell
Invoke-WebRequest -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/list" 
```

#### <a name="sample-response"></a>Exemple de réponse

```json
StatusCode        : 200
Status Description : OK
Content           : [{"contentType":"Audit.Exchange","status":"enabled","webhook":null},{"contentType":"Audit.SharePoint","status":"enabled","webhook":{"authId":"","address":"https://mvcwebapiwebhookreceiver.azurewebsite...
RawContent        : HTTP/1.1 200 OK
                    Pragma: no-cache
                    Content-Length: 266
                    Cache-Control: no-cache
                    Content-Type: application/json; charset=utf-8
                    Expires: -1
                    Server: Microsoft-IIS/8.5,Microsoft-IIS/8.5
                    X-AspNet-Versi...
Forms             : {}
Headers           : {[Pragma, no-cache], [Content-Length, 266], [Cache-Control, no-cache], [Content-Type, application/json; charset=utf-8]...}
Images            : {}
InputFields       : {}
Links             : {}
ParsedHtml        : mshtml.HTMLDocumentClass
RawContentLength  : 266
```

Cette réponse indique que les abonnements Audit.Exchange et Audit.SharePoint sont activés dans le locataire. Aucun webhook n’est activé (null) dans l’abonnement Exchange. Dans l’abonnement SharePoint, un webhook est activé et l’adresse du point de terminaison inscrit est affichée.

### <a name="creating-a-new-subscription"></a>Création d’un abonnement

Pour créer un abonnement, utilisez l’opération /start. Pour le point de terminaison de l’API, utilisez l’une de ces valeurs selon votre type d’abonnement :

- Offre pour le secteur privé : `manage.office.com`

- Offre pour le secteur public (Cloud de la communauté du secteur public) : `manage-gcc.office.com`

- Offre pour le secteur public (Cloud de la communauté du secteur public à haute disponibilité, ou « GCC High  ») : `manage.office365.us`

- Plan pour le secteur public DoD : `manage.protection.apps.mil`

```powershell
Invoke-WebRequest -Method Post -Headers $headerParams -Uri "https://<YOUR_API_ENDPOINT>/api/v1.0/$tenantGUID/activity/feed/subscriptions/start?contentType=Audit.AzureActiveDirectory"

> [!NOTE]
> Remember that `$headerParams` was populated in the first part of the script listed in the [Connecting to the API](#connecting-to-the-api) section in this article.

The previous code will create a new subscription to the Audit.AzureActiveDirectory content type, with a webhook that is null. You can then check your subscriptions using the code in the [Checking your subscriptions](#checking-your-subscriptions) section in this article.

## Checking content availability

To check what content blobs were created during a certain period, you can add the following line to the script in the “Connecting to the API” section.

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint"
```

L’exemple précédent reçoit les notifications de contenu mis à disposition aujourd’hui, entre 12:00 AM UTC et l’heure actuelle. Si vous voulez indiquer une période différente (en gardant à l’esprit que vous ne pouvez pas interroger l’API sur des périodes supérieures à 24 heures), ajoutez les paramètres *starttime* et *endtime* à l’URI. Par exemple :

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "$resource/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint&startTime=2017-10-13T00:00&endTime=2017-10-13T11:59"
```

> [!NOTE]
> Les paramètres *starttime* et *endtime* peuvent être utilisés uniquement ensemble.

```json
[{      "contentUri" : "https://<your_API_endpoint>/api/v1.0/<your_tenant_guid>/activity/feed/audit/20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentId" : "20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentType" : "Audit.SharePoint",
        "contentCreated" : "2017-10-13T18:00:51.748Z",
        "contentExpiration" : "2017-10-20T18:00:51.748Z",
}]
```

> [!IMPORTANT]
>
> - La propriété *contentUri* est l’URI qui vous permet de récupérer le blob de contenu. Le blob contient les détails des événements, et ce pour 1 – N événements. Alors que la collection peut contenir 30 objets JSON, il peut y avoir davantage de détails d’événements dans ces 30 URI de contenu.
>
> - La propriété *contentCreated* ne correspond pas à la date à laquelle l’événement notifié a été créé. Il s’agit de la date à laquelle la notification a été créée. Les événements détaillés dans ce blob ont peut-être été créés bien avant le blob de contenu. Par conséquent, vous ne pouvez jamais interroger directement l’API sur les événements survenus pendant une période donnée.

#### <a name="paging-contents-for-busy-tenants"></a>Pagination du contenu pour les locataires occupés

Dans de nombreux locataires Office 365 plus importants, des milliers d’événements peuvent être générés en une heure. Si c’est le cas dans votre organisation, et si vous essayez d’exécuter une requête pour une période de 24 heures comme dans l’exemple ci-dessus, il peut être utile de récupérer davantage de notifications pouvant être renvoyées dans une seule réponse. Dans ce cas, nous vous recommandons d’implémenter une boucle logique qui vérifie si les en-têtes de réponse contiennent la valeur **NextPageUrl:**. Voir la section Pagination dans la référence API de l'activité de gestion Office 365 pour plus de détails.

```powershell
IF the NextPageUrl header is present in the response... 

THEN issue a new request substituting the Uri parameter in the above Invoke-WebRequest example for the value of the NextPageUrl header...
 
ELSE exit the loop
```

Il sera difficile de tester ce code en boucle, sauf si votre locataire est très actif. Dans notre test, nous avons essayé d’exécuter des milliers d’opérations de mise à jour dans un script. Le nombre de notifications généré était insuffisant pour exiger l’envoi de l’en-tête **NextPageUrl**.

### <a name="using-webhooks"></a>Utilisation des webhooks

Deux approches vous permettent de recevoir une notification créée par les blobs de contenu. L’approche *push* est implémentée avec un point de terminaison de webhook, qui correspond à une application web que vous créez et hébergez vous-même ou sur une plateforme cloud. Inscrivez le webhook quand vous créez un abonnement à un type de contenu audité. Vous pouvez également ajouter une inscription de webhook à un abonnement existant à l’aide de l’approche illustrée ci-dessous. L’approche *pull*vous oblige à interroger pour une période particulière (pas plus de 24 heures) en utilisant l’opération /contenu. La réponse vous indique les blobs de contenu qui ont été créés pendant la période spécifiée.

Avant d’ajouter un webhook, vous devez connaître les aspects suivants :

1. Les webhooks ne sont plus mis en avant par Microsoft en raison des difficultés rencontrées pour les déboguer et les dépanner. En règle générale, il faut héberger un point de terminaison WebApi qui répond à des requêtes entrantes. De nombreux clients utilisent soit des environnements d’hébergement (qu’ils ne contrôlent pas totalement), soit des environnements locaux (qui ont des difficultés à autoriser les requêtes HTTP entrantes). L’équipe de support a reçu de nombreuses questions liées à des problèmes où les requêtes entrantes provenant du pipeline d’audit Office 365 étaient bloquées par un pare-feu ou un routeur. Dans ce cas, l’API implémente un algorithme d’interruption qui peut être source de confusion et entraîner la désactivation du webhook dans l’abonnement.

2. Le webhook doit être prêt à répondre immédiatement à une requête de validation quand l’opération /start est exécutée. S’il y a un bogue dans l’application webhook, la validation échoue et le webhook n’est pas activé. Pour en savoir plus sur le schéma de requête de validation, consultez la section relative à la validation du webhook dans la référence de l’API Activité de gestion Office 365. Nous vous conseillons d’envisager sérieusement les difficultés que vous pourriez rencontrer en produisant un webhook prêt pour la production pour répondre aux notifications de l’API Activité de gestion.

Si vous décidez d’implémenter un webhook, il doit être testé pour vérifier que le point de terminaison est prêt à envoyer une réponse HTTP 200 à la requête de validation et aux demandes de notification normales avant le premier appel d’une opération /start indiquant un point de terminaison de webhook. En règle générale, il est préférable d’envoyer une requête factice à partir de l’API pour tester la préparation du webhook. Lisez attentivement les sections relatives à la validation du webhook et à la récupération du contenu dans la référence de l’API Activité de gestion Office 365 pour comprendre le schéma de ces deux types de requêtes.

Pour ajouter un abonnement associé à un point de terminaison de webhook, ajoutez un paramètre BODY à la méthode POST du point de terminaison /start. Par exemple :

```json
$body = '{
    "webhook" : {
        "address": "https://webhook.myapp.com/o365/",
        "authId": "o365activityapinotification",
        "expiration": ""
    }}'
$uri = "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed//subscriptions/start?contentType=Audit.SharePoint"
Invoke-RestMethod -Method Post -uri $uri -Headers $headerParams -Body $body
```

Immédiatement après cet appel, une requête de validation est envoyée à l’URI `https://webhook.myapp.com/o365/ …`. Un détecteur doit être prêt à répondre conformément à la description présente dans la section relative à la validation du webhook de la référence de l’API Activité de gestion Office 365. Votre détecteur doit envoyer une réponse HTTP 200. Si vous exécutez immédiatement l’opération /list à ce stade, le webhook affichera null jusqu’à ce que la validation soit renvoyée.

#### <a name="checking-notifications-to-webhooks"></a>Vérification des notifications envoyées aux webhooks

Il est important de faire la distinction entre l'opération /notifications et l'opération /contenu. Il est utile de vérifier les notifications uniquement si vous vous êtes abonné auprès d’un point de terminaison de webhook. Cette opération vous permettra de savoir si les tentatives d’envoi des notifications à votre webhook ont réussi. Cette opération ne doit pas être utilisée pour lister le contenu disponible. Pour vérifier la disponibilité du contenu par rapport à ce que vous avez peut-être déjà reçu dans votre webhook, utilisez l’opération /content. Avant toute chose, vérifiez si vous avez reçu des notifications d’échec en utilisant l’opération /notifications.

### <a name="requesting-content-blobs-and-throttling"></a>Requête de blobs de contenu et limitation de requêtes

Dès que vous avez obtenu la liste des URI de contenu, demandez les blobs spécifiés par les URI. Voici un exemple de requête d’un blob de contenu (en utilisant le point de terminaison de l’API manage.office.com pour les organisations d’entreprise) avec PowerShell. Cet exemple part du principe que vous avez déjà utilisé l’exemple précédent de la section [Obtention d’un jeton d’accès](#getting-an-access-token) de cet article pour obtenir un jeton d’accès et remplir la variable `$headerParams` comme il se doit.

```powershell
# Get a content blob
$uri = 'https://manage.office.com/api/v1.0/<<your-tenant-guid>>/activity/feed/audit/<<ContentID>$audit_sharepoint$Audit_SharePoint'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

Quelques remarques concernant la variable *$uri* utilisée dans l’exemple précédent :

- Nous avons utilisé des guillemets simples pour *$* éviter toute interprétation des symboles en tant que variables dans PowerShell

- L’URI entière est renvoyée dans la propriété *contentUri* de la réponse à l’appel précédent passé au point de terminaison /content. Les jetons d’espace réservé affichés sont fournis à titre d’exemple uniquement.

Quand ils tentent de récupérer les blobs de contenu disponibles, de nombreux clients (utilisant principalement des locataires occupés) rencontrent des erreurs semblables à celles-ci :

```json
Response Code 403: {'error':{'code':'AF429','message':'Too many requests. Method=GetBlob, PublisherId=00000000-0000-0000-0000-000000000000'}}
```

Cette erreur est probablement due à la limitation des requêtes. Notez que la valeur du paramètre PublisherId indique probablement que le client n’a pas spécifié *PublisherIdentifier* dans la requête. Par ailleurs, n’oubliez pas que le nom correct du paramètre est *PublisherIdentifier* même si *PublisherId* est répertorié dans les réponses de l’erreur 403.

> [!NOTE]
> Dans la référence de l’API, le paramètre *PublisherIdentifier* figure dans chaque opération de l’API, mais il doit également être inclus dans la requête GET envoyée à l’URL contentUri pendant la récupération du blob de contenu.

Si vous effectuez des appels d’API simples pour résoudre des problèmes (par exemple, pour vérifier si un abonnement est actif), vous pouvez ignorer sereinement le paramètre *PublisherIdentifier*. En revanche, tout code destiné à la production doit inclure le paramètre *PublisherIdentifier* dans chaque appel.

Si vous mettez en place un client pour le locataire de votre entreprise, le paramètre *PublisherIdentifier* est le GUID du locataire. Si vous créez une application ISV ou un complément tiers pour plusieurs clients, le paramètre *PublisherIdentifier* devrait être le GUID du locataire de l'ISV, et non le GUID du locataire de l'entreprise de l'utilisateur final.

Si vous incluez le paramètre *PublisherIdentifier* valide, votre application sera dans un pool qui reçoit 60 000 requêtes par minute par locataire. Il s’agit d’un nombre incroyablement élevé de requêtes. Toutefois, si vous n’incluez pas le paramètre *PublisherIdentifier*, votre application sera dans le pool général qui reçoit 60 000 requêtes par minute pour tous les locataires. Dans ce cas, vous trouverez certainement que vos appels sont limités. Pour éviter cela, voici comment vous pouvez demander un blob de contenu à l’aide du paramètre *PublisherIdentifier* :

```json
$contentUri = ($response.Content | ConvertFrom-Json).contentUri[0]
$uri = $contentUri + '?PublisherIdentifier=82b24b6d-0591-4604-827b-705d55d0992f'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

L’exemple précédent part du principe que la variable *$response* a été remplie avec la réponse d’une requête envoyée au point de terminaison /content et que la variable *$headerParams* inclut un jeton d’accès valide. Le script prend le premier élément de la matrice des URI de contenu dans la réponse, puis invoque la méthode GET pour télécharger ce blob et le placer dans la variable *$contents*. Votre code va probablement exécuter des boucles dans la collection contentUri, en émettant la méthode GET pour chaque *contentUri*.
