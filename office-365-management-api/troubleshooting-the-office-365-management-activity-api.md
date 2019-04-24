---
ms.TocTitle: Troubleshooting the Office 365 Management Activity API
title: Résolution des problèmes de l’API Activité de gestion Office 365
description: Cet article présente les questions les plus fréquemment posées au Support Microsoft concernant cette API.
ms.ContentId: 50822603-a1ec-a754-e7dc-67afe36bb1b0
ms.topic: reference (API)
ms.date: 09/05/2018
localization_priority: Priority
ms.openlocfilehash: ed84984dc3009d03e0bb7cacba16eafb687c93e0
ms.sourcegitcommit: 5b1eaeb7f262b7b9f7ab30ccb9f10878814153ac
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "32223951"
---
# <a name="troubleshooting-the-office-365-management-activity-api"></a>Résolution des problèmes de l’API Activité de gestion Office 365

L’API Activité de gestion Office 365 (également appelée *API Audit unifié*) n’est qu’une des solutions comprises dans les offres de sécurité et de conformité Office 365, mais elle suscite beaucoup d’intérêt pour plusieurs raisons :

- Elle autorise l’accès par programme à plusieurs charges de travail du pipeline d’audit (par exemple, SharePoint et Exchange).
- Elle est l’interface principale utilisée par un large éventail de produits tiers pour agréger et indexer les données d’audit.

L’API Activité de gestion ne doit pas être confondue avec l’API Communications de service Office 365. L’API Activité de gestion vous permet d’auditer les activités des utilisateurs finals dans différentes charges de travail.  L’API Communications de service, quant à elle, sert à auditer l’état et les messages envoyés par les services disponibles dans Office 365 (par exemple, Dynamics CRM ou Identité du service).

Même si elle comporte relativement peu d’opérations et une interface REST simple, les utilisateurs ne savent pas toujours très bien comment utiliser l’API Activité de gestion et comment les données sont récupérées.  Tout d’abord, les personnes qui utilisent pour la première fois l’API Activité de gestion doivent savoir que les charges de travail ne peuvent être interrogées en fonction des spécificités d’un événement (par exemple la date à laquelle l’événement s’est produit, la collection de sites à partir de laquelle l’événement a été déclenché ou le type d’événement).  En effet, vous devez créer des abonnements à des charges de travail spécifiques (par exemple, SharePoint ou Azure AD), chaque abonnement correspondant à un seul locataire.

Cet article présente les questions les plus fréquemment posées au Support Microsoft concernant cette API.  Nous allons vous proposer une sélection de scripts PowerShell simples pour vous aider à répondre aux questions les plus fréquemment posées par les clients ou à implémenter une solution personnalisée en montrant les principales opérations à réaliser.  Seules quelques opérations sont expliquées dans cet article. Vous pouvez toutes les retrouver dans la [référence de l’API Activité de gestion Office 365](office-365-management-activity-api-reference.md).

## <a name="questions-about-third-party-tools-and-clients"></a>Questions sur les clients et les outils tiers

Les questions les plus courantes auxquelles nous répondons sont posées par des clients qui utilisent des produits tiers pour télécharger et agréger des données d’audit. Selon le produit tiers, les clients peuvent éprouver des difficultés pendant la configuration ou rencontrer une interruption ou une incohérence dans les données figurant dans ces produits. En premier lieu, ces clients doivent contacter l’équipe de support de leur fournisseur. Parmi toutes les demandes de service reçues par le support, un seul incident était dû à un problème lié au service du locataire.

Néanmoins, certaines questions des clients peuvent être restées sans réponse. Peut-être que leur fournisseur a insisté sur le fait qu’il s’agit d’un problème lié au service, ou peut-être n’ont-ils pas voulu procéder à certaines vérifications avant de contacter leur fournisseur. 

## <a name="connecting-to-the-api"></a>Connexion à l’API

La plupart des applications se connectent à l’API à l’aide d’un simple flux OAuth2 d’informations d’identification du client. Par conséquent, la première étape consiste à créer une application Azure AD ayant les autorisations nécessaires pour accéder aux données de l’API Activité de gestion. Nous ne pouvons pas vous expliquer dans cet article comment créer une inscription d’application Azure AD. Pour en savoir plus, consultez l’article relatif à l’[inscription d’une application avec le locataire Azure Active Directory](https://docs.microsoft.com/fr-FR/azure/active-directory/develop/active-directory-integrating-applications).

### <a name="azure-application-permissions"></a>Autorisations de l’application Azure

Les trois autorisations actuellement utilisées pour l’API Activité de gestion Office 365 sont les suivantes :
1. Lire les données d’activité de votre organisation
2. Lire les informations d’état du service de votre organisation
3. Lire les événements de la politique Protection contre la perte de données (DLP), y compris les informations sensibles détectées 

> [!NOTE] 
> Nous vous recommandons d’activer les Autorisations d’application et les Autorisations déléguées au moins pour les deux premiers jeux d’autorisations ci-dessus. L’autorisation Lire les événements de la stratégie DLP vous sera utile uniquement si vous êtes intéressé par les charges de travail DLP.

### <a name="getting-an-access-token"></a>Obtention d’un jeton d’accès

Le script PowerShell suivant utilise l’ID de l’application et une clé secrète client pour obtenir le jeton OAuth2 auprès du point de terminaison d’authentification de l’API Activité de gestion. Il place ensuite le jeton d’accès dans la variable `$headerParams` de la matrice, que vous joindrez à votre requête HTTP : 

```powershell
# Create app of type Web app / API in Azure AD, generate a Client Secret, and update the client id and client secret here
$ClientID = "<YOUR_APPLICATION_ID"
$ClientSecret = "<YOUR_CLIENT_SECRET>"
$loginURL = "https://login.microsoftonline.com/"
$tenantdomain = "<YOUR_DOMAIN>.onmicrosoft.com"
# Get the tenant GUID from Properties | Directory ID under the Azure Active Directory section
$TenantGUID = "<YOUR_TENANT_GUID>"
$resource = "https://manage.office.com"
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

## <a name="checking-your-subscriptions"></a>Vérification de vos abonnements

Quand on constate une interruption du flux de données à destination d’une solution ou d’un client de l’API Activité de gestion existant, il est normal de se demander si l’abonnement est impacté. Pour vérifier vos abonnements actifs, ajoutez ce qui suit au script précédent :

```powershell
Invoke-WebRequest -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/list" 
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

## <a name="creating-a-new-subscription"></a>Création d’un abonnement

Pour créer un abonnement, utilisez l’opération /start :

```powershell
Invoke-WebRequest -Method Post -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/start?contentType=Audit.AzureActiveDirectory"
```

> [!NOTE] 
> N’oubliez pas que la variable `$headerParams` a été remplie dans la première partie du script présentée à la section [Connexion à l’API](#connecting-to-the-api) de cet article.

Le code précédent crée un abonnement au type de contenu Audit.AzureActiveDirectory, avec un webhook null. Vous pouvez ensuite vérifier vos abonnements en utilisant le code indiqué dans la section [Vérification de vos abonnements](#checking-your-subscriptions) de cet article.

## <a name="checking-content-availability"></a>Vérification de la disponibilité du contenu

Pour vérifier les blobs de contenu qui ont été créés à une période donnée, vous pouvez ajouter la ligne suivante au script de la section « Connexion à l’API » :

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint"
```

L’exemple précédent reçoit les notifications de contenu mis à disposition aujourd’hui, entre 12:00 AM UTC et l’heure actuelle. Si vous voulez indiquer une période différente (en gardant à l’esprit que vous ne pouvez pas interroger l’API sur des périodes supérieures à 24 heures), ajoutez les paramètres *starttime* et *endtime* à l’URI. Par exemple :

```powershell
Invoke-WebRequest -Method GET -Headers $headerParams -Uri "https://manage.office.com/api/v1.0/$tenantGUID/activity/feed/subscriptions/content?contentType=Audit.SharePoint&startTime=2017-10-13T00:00&endTime=2017-10-13T11:59"
```

> [!NOTE] 
> Les paramètres *starttime* et *endtime* peuvent être utilisés uniquement ensemble.

La requête précédente renvoie un objet JSON avec une collection de notifications devenues disponibles pendant la période spécifiée. La réponse ressemble à ceci :

```json
[{      "contentUri" : "https://manage.office.com/api/v1.0/<<your_tenant_guid>>/activity/feed/audit/20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentId" : "20171014180051748005825$20171014180051748005825$audit_sharepoint$Audit_SharePoint",
        "contentType" : "Audit.SharePoint",
        "contentCreated" : "2017-10-13T18:00:51.748Z",
        "contentExpiration" : "2017-10-20T18:00:51.748Z",
}]
```

> [!IMPORTANT] 
> - La propriété *contentUri* est l’URI qui vous permet de récupérer le blob de contenu. Le blob contient les détails des événements, et ce pour 1 – N événements. Alors que la collection peut contenir 30 objets JSON, il peut y avoir davantage de détails d’événements dans ces 30 URI de contenu.
> - La propriété *contentCreated* ne correspond pas à la date à laquelle l’événement notifié a été créé. Il s’agit de la date à laquelle la notification a été créée. Les événements détaillés dans ce blob ont peut-être été créés bien avant le blob de contenu. Par conséquent, vous ne pouvez jamais interroger directement l’API sur les événements survenus pendant une période donnée.

### <a name="paging-contents-for-busy-tenants"></a>Pagination du contenu pour les locataires occupés

Dans de nombreux locataires Office 365 plus importants, des milliers d’événements peuvent être générés en une heure. Si c’est le cas dans votre organisation, et si vous essayez d’exécuter une requête pour une période de 24 heures comme dans l’exemple ci-dessus, il peut être utile de récupérer davantage de notifications pouvant être renvoyées dans une seule réponse. Dans ce cas, nous vous recommandons d’implémenter une boucle logique qui vérifie si les en-têtes de réponse contiennent la valeur **NextPageUrl:**. Pour en savoir plus, consultez la section [Pagination](office-365-management-activity-api-reference.md#pagination) dans la référence de l’API Activité de gestion Office 365. 

La logique de cette boucle devrait ressembler à ceci :

```powershell
IF the NextPageUrl header is present in the response... 

THEN issue a new request substituting the Uri parameter in the above Invoke-WebRequest example for the value of the NextPageUrl header...
 
ELSE exit the loop
```

Il sera difficile de tester ce code en boucle, sauf si votre locataire est très actif. Dans notre test, nous avons essayé d’exécuter des milliers d’opérations de mise à jour dans un script. Le nombre de notifications généré était insuffisant pour exiger l’envoi de l’en-tête **NextPageUrl**.

## <a name="using-webhooks"></a>Utilisation des webhooks

Deux approches vous permettent de recevoir une notification créée par les blobs de contenu. L’approche *push* est implémentée avec un point de terminaison de webhook, qui correspond à une application web que vous créez et hébergez vous-même ou sur une plateforme cloud. Inscrivez le webhook quand vous créez un abonnement à un type de contenu audité. Vous pouvez également ajouter une inscription de webhook à un abonnement existant à l’aide de l’approche illustrée ci-dessous. L’approche *pull* nécessite que vous interrogiez l’API sur un certain intervalle de temps (inférieur à 24 heures) à l’aide de l’[opération /content](office-365-management-activity-api-reference.md#list-available-content). La réponse vous indique les blobs de contenu qui ont été créés pendant la période spécifiée.

Avant d’ajouter un webhook, vous devez connaître les aspects suivants :

1. Les webhooks ne sont plus mis en avant par Microsoft en raison des difficultés rencontrées pour les déboguer et les dépanner. En règle générale, il faut héberger un point de terminaison WebApi qui répond à des requêtes entrantes. De nombreux clients utilisent soit des environnements d’hébergement (qu’ils ne contrôlent pas totalement), soit des environnements locaux (qui ont des difficultés à autoriser les requêtes HTTP entrantes). L’équipe de support a reçu de nombreuses questions liées à des problèmes où les requêtes entrantes provenant du pipeline d’audit Office 365 étaient bloquées par un pare-feu ou un routeur. Dans ce cas, l’API implémente un algorithme d’interruption qui peut être source de confusion et entraîner la désactivation du webhook dans l’abonnement.

2. Le webhook doit être prêt à répondre immédiatement à une requête de validation quand l’opération /start est exécutée. S’il y a un bogue dans l’application webhook, la validation échoue et le webhook n’est pas activé. Pour en savoir plus sur le schéma de requête de validation, consultez la section relative à la [validation du webhook](office-365-management-activity-api-reference.md#webhook-validation) dans la référence de l’API Activité de gestion Office 365. Nous vous conseillons d’envisager sérieusement les difficultés que vous pourriez rencontrer en produisant un webhook prêt pour la production pour répondre aux notifications de l’API Activité de gestion.

Si vous décidez d’implémenter un webhook, il doit être testé pour vérifier que le point de terminaison est prêt à envoyer une réponse HTTP 200 à la requête de validation et aux demandes de notification normales avant le premier appel d’une opération /start indiquant un point de terminaison de webhook. En règle générale, il est préférable d’envoyer une requête factice à partir de l’API pour tester la préparation du webhook. Lisez attentivement les sections relatives à la [validation du webhook](office-365-management-activity-api-reference.md#webhook-validation) et à la [récupération du contenu](office-365-management-activity-api-reference.md#retrieving-content) dans la référence de l’API Activité de gestion Office 365 pour comprendre le schéma de ces deux types de requêtes.

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

Immédiatement après cet appel, une requête de validation est envoyée à l’URI `https://webhook.myapp.com/o365/ …`. Un détecteur doit être prêt à répondre conformément à la description présente dans la section relative à la [validation du webhook](office-365-management-activity-api-reference.md#webhook-validation) de la référence de l’API Activité de gestion Office 365. Votre détecteur doit envoyer une réponse HTTP 200. Si vous exécutez immédiatement l’opération /list à ce stade, le webhook affichera null jusqu’à ce que la validation soit renvoyée.

### <a name="checking-notifications-to-webhooks"></a>Vérification des notifications envoyées aux webhooks

Il est important de faire la distinction entre l’opération /notifications et l’opération /content. Il est utile de vérifier les notifications uniquement si vous vous êtes abonné auprès d’un point de terminaison de webhook. Cette opération vous permettra de savoir si les tentatives d’envoi des notifications à votre webhook ont réussi. Cette opération ne doit pas être utilisée pour lister le contenu disponible. Pour vérifier la disponibilité du contenu par rapport à ce que vous avez peut-être déjà reçu dans votre webhook, utilisez l’opération /content. Avant toute chose, vérifiez si vous avez reçu des notifications d’échec en utilisant l’[opération /notifications](office-365-management-activity-api-reference.md#list-notifications).

## <a name="requesting-content-blobs-and-throttling"></a>Requête de blobs de contenu et limitation de requêtes

Dès que vous avez obtenu la liste des URI de contenu, demandez les blobs spécifiés par les URI. Voici un exemple de demande d’un blob de contenu à l’aide de PowerShell. Cet exemple part du principe que vous avez déjà utilisé l’exemple précédent de la section [Obtention d’un jeton d’accès](#getting-an-access-token) de cet article pour obtenir un jeton d’accès et remplir la variable `$headerParams` comme il se doit.

```powershell
# Get a content blob
$uri = 'https://manage.office.com/api/v1.0/<<your-tenant-guid>>/activity/feed/audit/<<ContentID>$audit_sharepoint$Audit_SharePoint'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

Quelques remarques concernant la variable *$uri* utilisée dans l’exemple précédent :

- Nous avons utilisé des guillemets simples pour que les symboles *$* ne soient pas interprétées comme des variables dans PowerShell.
- L’URI entière est renvoyée dans la propriété *contentUri* de la réponse à l’appel précédent passé au point de terminaison /content. Les jetons d’espace réservé affichés sont fournis à titre d’exemple uniquement.

Quand ils tentent de récupérer les blobs de contenu disponibles, de nombreux clients (utilisant principalement des locataires occupés) rencontrent des erreurs semblables à celles-ci :

```json
Response Code 403: {'error':{'code':'AF429','message':'Too many requests. Method=GetBlob, PublisherId=00000000-0000-0000-0000-000000000000'}}
```

Cette erreur est probablement due à la limitation des requêtes. Notez que la valeur du paramètre PublisherId indique probablement que le client n’a pas spécifié *PublisherIdentifier* dans la requête. Par ailleurs, n’oubliez pas que le nom correct du paramètre est *PublisherIdentifier* même si *PublisherId* est répertorié dans les réponses de l’erreur 403.

> [!NOTE] 
> Dans la référence de l’API, le paramètre *PublisherIdentifier* figure dans chaque opération de l’API, mais il doit également être inclus dans la requête GET envoyée à l’URL contentUri pendant la récupération du blob de contenu.

Si vous effectuez des appels d’API simples pour résoudre des problèmes (par exemple, pour vérifier si un abonnement est actif), vous pouvez ignorer sereinement le paramètre *PublisherIdentifier*. En revanche, tout code destiné à la production doit inclure le paramètre *PublisherIdentifier* dans chaque appel.

Si vous implémentez un client pour le locataire de votre entreprise, le paramètre *PublisherIdentifier* est le GUID client. Si vous créez une application ou un complément tiers pour plusieurs clients, le paramètre *PublisherIdentifier* doit être le GUID client de l’éditeur de logiciels indépendant, et non le GUID client de l’entreprise de l’utilisateur final.

Si vous incluez le paramètre *PublisherIdentifier* valide, votre application sera dans un pool qui reçoit 60 000 requêtes par minute par locataire. Il s’agit d’un nombre incroyablement élevé de requêtes. Toutefois, si vous n’incluez pas le paramètre *PublisherIdentifier*, votre application sera dans le pool général qui reçoit 60 000 requêtes par minute pour tous les locataires. Dans ce cas, vous trouverez certainement que vos appels sont limités. Pour éviter cela, voici comment vous pouvez demander un blob de contenu à l’aide du paramètre *PublisherIdentifier* :

```powershell
$contentUri = ($response.Content | ConvertFrom-Json).contentUri[0]
$uri = $contentUri + '?PublisherIdentifier=82b24b6d-0591-4604-827b-705d55d0992f'
$contents = Invoke-WebRequest -Method GET -Headers $headerParams -Uri $uri
```

L’exemple précédent part du principe que la variable *$response* a été remplie avec la réponse d’une requête envoyée au point de terminaison /content et que la variable *$headerParams* inclut un jeton d’accès valide. Le script prend le premier élément de la matrice des URI de contenu dans la réponse, puis invoque la méthode GET pour télécharger ce blob et le placer dans la variable *$contents*. Votre code va probablement exécuter des boucles dans la collection contentUri, en émettant la méthode GET pour chaque *contentUri*.

## <a name="frequently-asked-questions-about-the-office-365-management-api"></a>Questions fréquemment posées sur l’API Gestion Office 365.

#### <a name="what-is-the-maximum-time-i-will-have-to-wait-before-a-notification-is-sent-about-a-given-office-365-event"></a>Combien de temps maximum faut-il attendre avant qu’une notification soit envoyée sur un événement Office 365 ?

Nous ne pouvons pas garantir le délai maximal avant la remise de la notification. (Il ne peut être garanti par un contrat SLA.) D’après les observations faites par le Support Microsoft, la plupart des notifications sont envoyées dans l’heure qui suit l’événement. Bien souvent, ce délai est plus court, mais il arrive aussi qu’il soit plus long. Il varie légèrement d’une charge de travail à l’autre, mais, en règle générale, la plupart des notifications sont remises dans les 24 heures suivant l’événement d’origine.

#### <a name="arent-webhook-notifications-more-immediate-after-all-arent-they-are-event-driven"></a>Les notifications webhook ne sont-elles pas plus immédiates ? Après tout, ne sont-elles pas fondées sur les événements ?

Non. Les notifications webhook ne sont pas fondées sur les événements au sens où l’événement déclencherait la notification. Le blob de contenu doit quand même être créé. Par ailleurs, la création du blob de contenu déclenche l’envoi de la notification. Récemment, les délais des notifications étaient plus longs avec un webhook qu’en interrogeant directement l’API à l’aide de l’opération /content. Par conséquent, l’API Activité de gestion ne doit pas être considérée comme un système d’alerte de sécurité en temps réel. Microsoft propose d’autres produits pour cela. Concernant la sécurité, les notifications d’événements de l’API Activité de gestion peuvent être utilisées de façon plus appropriée pour déterminer les modes d’utilisation sur des périodes prolongées. 

#### <a name="can-i-query-the-management-activity-api-for-a-particular-event-id-or-recordtype-or-other-properties-in-the-content-blob"></a>Peut-on interroger l’API Activité de gestion sur l’ID d’un événement spécifique ou sur la propriété RecordType ou d’autres propriétés présentes dans le blob de contenu ?

Non. Les données disponibles via l’API Activité de gestion ne représentent pas un « journal » au sens traditionnel du terme. Considérez-les plutôt comme une image mémoire des détails de l’événement. C’est à vous de réunir tous les détails de l’événement, de les stocker et de les indexer localement, puis d’implémenter votre propre logique de requête, en utilisant une application personnalisée ou un outil tiers.

#### <a name="how-do-i-know-the-data-coming-from-my-existing-auditing-solution-which-collects-data-from-the-management-activity-api-is-accurate-and-complete"></a>Comment savoir si les données provenant de ma solution d’audit existante, qui collecte des données auprès de l’API Activité de gestion, sont précises et complètes ?

En bref, Microsoft ne fournit aucun type de journal qui vous permet de vérifier une application donnée ou une application tierce (ISV). D’autres produits de sécurité Microsoft extraient leurs données du même pipeline, mais ces produits ne peuvent être énumérés dans cet article et ne peuvent pas être utilisés pour vérifier directement l’API Activité de gestion. Si vous vous préoccupez des différences pouvant exister entre ce que votre solution vous fournit et ce dont vous en attendez, nous vous recommandons d’implémenter les opérations illustrées ci-dessus. Cette démarche peut être difficile à réaliser selon la méthode employée par votre outil ou votre solution pour lister et indexer les données. Si, dans votre solution, les données sont triées uniquement selon l’heure de création de l’événement, vous ne pouvez pas interroger l’API selon l’heure de création de l’événement pour comparer les jeux de résultats. Dans ce cas, nous vous conseillons de collecter les blobs de contenu notifiés pendant plusieurs jours, de les indexer ou de les trier manuellement, puis d’effectuer une rapide comparaison.

#### <a name="how-long-will-the-content-blobs-remain-available"></a>Combien de temps les blobs de contenu sont-ils disponibles ?

Les blobs de contenu sont disponibles pendant 7 jours après l’envoi de la notification de disponibilité du blob de contenu. Autrement dit, si la création du blob de contenu est retardée de façon significative, le blob reste disponible plus longtemps (délai plus 7 jours) après la date de création réelle de l’événement.

#### <a name="if-there-is-a-24-hour-delay-in-getting-a-notification-doesnt-that-mean-i-will-have-only-6-days-to-retrieve-the-content-blob"></a>Si l’envoi de la notification est retardé de 24 heures, me restera-t-il seulement 6 jours pour récupérer le blob de contenu ?

Non. Même si la notification est retardée pendant un certain temps (par exemple, dans le cas d’une interruption de service), il vous reste 7 jours après la date d’envoi initial de la notification pour télécharger le blob de contenu lié à l’événement d’origine.












