---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Management Activity API reference
title: Référence de l’API Activité de gestion Office 365
description: Cet article explique comment utiliser l’API Activité de gestion Office 365 pour récupérer des informations sur les actions et les événements des utilisateurs, des administrateurs, du système et des stratégies à partir des journaux d’activité Office 365 et Azure AD.
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: c8eb59433b49c9735ddfefea0d1e6804e8937439
ms.sourcegitcommit: f08ff7cfd17aedd9d2ca85b5df0666ca986c9aed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/15/2021
ms.locfileid: "53447897"
---
# <a name="office-365-management-activity-api-reference"></a><span data-ttu-id="36d63-103">Référence de l’API Activité de gestion Office 365</span><span class="sxs-lookup"><span data-stu-id="36d63-103">Office 365 Management Activity API reference</span></span>

<span data-ttu-id="36d63-104">Cet article explique comment utiliser l’API Activité de gestion Office 365 pour récupérer des informations sur les actions et les événements des utilisateurs, des administrateurs, du système et des stratégies à partir des journaux d’activité Office 365 et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="36d63-104">Use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Office 365 and Azure AD activity logs.</span></span> 

<span data-ttu-id="36d63-105">Vous pouvez utiliser les actions et les événements à partir des journaux d’audit et d’activité Office 365 et Microsoft Azure Active Directory pour créer des solutions de supervision, d’analyse et de visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="36d63-105">You can use the actions and events from the Office 365 and Microsoft Azure Active Directory audit and activity logs to create solutions that provide monitoring, analysis, and data visualization.</span></span> <span data-ttu-id="36d63-106">Ces solutions offrent aux organisations une meilleure visibilité sur les actions effectuées sur leur contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-106">These solutions give organizations greater visibility into actions taken on their content.</span></span> <span data-ttu-id="36d63-107">Ces actions et ces événements sont également disponibles dans les rapports d’activité Office 365.</span><span class="sxs-lookup"><span data-stu-id="36d63-107">These actions and events are also available in the Office 365 Activity Reports.</span></span> <span data-ttu-id="36d63-108">Pour en savoir plus, reportez-vous à l’article [Effectuer des recherches dans le journal d’audit dans le Centre de sécurité et de conformité Office 365](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span><span class="sxs-lookup"><span data-stu-id="36d63-108">For more information, see [Search the audit log in the Office 365 Security & Compliance Center](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span></span>

<span data-ttu-id="36d63-109">L’API Activité de gestion Office 365 est un service web REST qui vous permet de développer des solutions à l’aide de n’importe quel langage et environnement d’hébergement qui prend en charge les certificats X.509 et HTTPS.</span><span class="sxs-lookup"><span data-stu-id="36d63-109">The Office 365 Management Activity API is a REST web service that you can use to develop solutions using any language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="36d63-110">L’API s’appuie sur Azure AD et le protocole OAuth2 pour l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="36d63-110">The API relies on Azure AD and the OAuth2 protocol for authentication and authorization.</span></span> <span data-ttu-id="36d63-111">Pour accéder à l’API depuis votre application, inscrivez-la d’abord dans Azure AD et configurez-la avec les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="36d63-111">To access the API from your application, you'll need to first register it in Azure AD and configure it with appropriate permissions.</span></span> <span data-ttu-id="36d63-112">Ainsi, votre application pourra demander les jetons d’accès OAuth2 dont elle a besoin pour appeler l’API.</span><span class="sxs-lookup"><span data-stu-id="36d63-112">This will enable your application to request the OAuth2 access tokens it needs to call the API.</span></span> <span data-ttu-id="36d63-113">Pour en savoir plus, consultez l’article relatif à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="36d63-113">For more information, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="36d63-114">Pour obtenir des informations sur les données renvoyées par l’API Activité de gestion Office 365 ainsi que sur les problèmes connus et les modifications à venir risquant d’affecter votre implémentation, consultez l’article relatif au [schéma de l’API Activité de gestion Office 365](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="36d63-114">For information about the data that the Office 365 Management Activity API returns, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36d63-115">Avant de pouvoir accéder aux données via l’API Activité de gestion Office 365, vous devez activer la journalisation d’audit unifié pour votre organisation Office 365.</span><span class="sxs-lookup"><span data-stu-id="36d63-115">Before you can access data through the Office 365 Management Activity API, you must enable unified audit logging for your Office 365 organization.</span></span> <span data-ttu-id="36d63-116">Pour ce faire, vous devez activer le journal d’audit d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="36d63-116">You do this by turning on the Office 365 audit log.</span></span> <span data-ttu-id="36d63-117">Pour obtenir des instructions, consultez la rubrique [Activer ou désactiver la recherche dans un journal d’audit Office 365](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span><span class="sxs-lookup"><span data-stu-id="36d63-117">For instructions, see [Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span></span>


## <a name="working-with-the-office-365-management-activity-api"></a><span data-ttu-id="36d63-118">Utilisation de l’API Activité de gestion Office 365</span><span class="sxs-lookup"><span data-stu-id="36d63-118">Working with the Office 365 Management Activity API</span></span>

<span data-ttu-id="36d63-p104">L’API Activité de gestion Office 365 agrège des actions et des événements dans des blobs de contenu propres au locataire, classés selon le type et la source du contenu qu’ils contiennent. Actuellement, les types de contenu suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="36d63-p104">The Office 365 Management Activity API aggregates actions and events into tenant-specific content blobs, which are classified by the type and source of the content they contain. Currently, these content types are supported:</span></span>

- <span data-ttu-id="36d63-121">Audit.AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="36d63-121">Audit.AzureActiveDirectory</span></span>
    
- <span data-ttu-id="36d63-122">Audit.Exchange</span><span class="sxs-lookup"><span data-stu-id="36d63-122">Audit.Exchange</span></span>
    
- <span data-ttu-id="36d63-123">Audit.SharePoint</span><span class="sxs-lookup"><span data-stu-id="36d63-123">Audit.SharePoint</span></span>
    
- <span data-ttu-id="36d63-124">Audit.General (comprend toutes les autres charges de travail non incluses dans les types de contenu précédents)</span><span class="sxs-lookup"><span data-stu-id="36d63-124">Audit.General (includes all other workloads not included in the previous content types)</span></span>

- <span data-ttu-id="36d63-125">DLP.All (événements DLP liés à toutes les charges de travail)</span><span class="sxs-lookup"><span data-stu-id="36d63-125">DLP.All (DLP events only for all workloads)</span></span>
    
<span data-ttu-id="36d63-126">Pour en savoir plus sur les événements et les propriétés associés à ces types de contenu, consultez l’article relatif au [schéma de l’API Activité de gestion Office 365](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="36d63-126">For details about the events and properties associated with these content types, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

<span data-ttu-id="36d63-127">Pour commencer à récupérer des blobs de contenu associés à un locataire, créez d’abord un abonnement aux types de contenu souhaités.</span><span class="sxs-lookup"><span data-stu-id="36d63-127">To begin retrieving content blobs for a tenant, you first a create subscription to the desired content types.</span></span> <span data-ttu-id="36d63-128">Si vous récupérez des blobs de contenu associés à plusieurs locataires, créez un abonnement à chacun des types de contenu souhaités pour chaque client.</span><span class="sxs-lookup"><span data-stu-id="36d63-128">If you are retrieving content blobs for multiple tenants, you create multiple subscriptions to each of the desired content types, one for each tenant.</span></span>

<span data-ttu-id="36d63-129">Une fois qu’un abonnement est créé, vous pouvez régulièrement l’interroger pour découvrir les nouveaux blobs de contenu disponibles au téléchargement. Sinon, vous pouvez inscrire un point de terminaison de webhook avec l’abonnement, auquel nous enverrons des notifications dès que de nouveaux blobs de contenu sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="36d63-129">After you create a subscription, you can poll regularly to discover new content blobs that are available for download, or you can register a webhook endpoint with the subscription and we will send notifications to this endpoint as new content blobs are available.</span></span>


> [!NOTE] 
> <span data-ttu-id="36d63-130">Quand un abonnement est créé, il faut attendre jusqu’à 12 heures avant que les premiers blobs de contenu associés à cet abonnement deviennent disponibles.</span><span class="sxs-lookup"><span data-stu-id="36d63-130">When a subscription is created, it can take up to 12 hours for the first content blobs to become available for that subscription.</span></span> <span data-ttu-id="36d63-131">Les blobs de contenu sont créés en collectant et en agrégeant des actions et des événements sur plusieurs serveurs et centres de données.</span><span class="sxs-lookup"><span data-stu-id="36d63-131">The content blobs are created by collecting and aggregating actions and events across multiple servers and datacenters.</span></span> <span data-ttu-id="36d63-132">À la suite de ce processus distribué, les actions et les événements contenus dans les blobs de contenu n’apparaissent pas nécessairement dans l’ordre dans lequel ils ont eu lieu.</span><span class="sxs-lookup"><span data-stu-id="36d63-132">As a result of this distributed process, the actions and events contained in the content blobs will not necessarily appear in the order in which they occurred.</span></span> <span data-ttu-id="36d63-133">Un blob de contenu peut contenir des actions et des événements qui ont eu lieu avant les actions et les événements contenus dans un blob de contenu antérieur.</span><span class="sxs-lookup"><span data-stu-id="36d63-133">One content blob can contain actions and events that occurred prior to the actions and events contained in an earlier content blob.</span></span> <span data-ttu-id="36d63-134">Nous mettons tout en œuvre pour réduire la latence entre l’occurrence des actions et des événements et leur disponibilité au sein d’un blob de contenu, mais nous ne pouvons pas garantir qu’elles apparaissent de manière séquentielle.</span><span class="sxs-lookup"><span data-stu-id="36d63-134">We are working to decrease the latency between the occurrence of actions and events and their availability within a content blob, but we can't guarantee that they appear sequentially.</span></span>


> [!NOTE] 
> <span data-ttu-id="36d63-135">Les données sensibles régies par les stratégies de protection contre la perte de données (DLP) sont disponibles dans l’API Flux d’activités uniquement pour les utilisateurs auxquels les autorisations « Lire les données sensibles DLP » ont été accordées.</span><span class="sxs-lookup"><span data-stu-id="36d63-135">DLP sensitive data is only available in the activity feed API to users that have been granted “Read DLP sensitive data” permissions.</span></span> <span data-ttu-id="36d63-136">Pour en savoir plus, reportez-vous à l’article [Vue d’ensemble des stratégies de protection contre la perte de données](https://support.office.com/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e).</span><span class="sxs-lookup"><span data-stu-id="36d63-136">For more on Data Loss Prevention (DLP) see [Overview of Data Loss Prevention Policies](https://support.office.com/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span></span>

## <a name="activity-api-operations"></a><span data-ttu-id="36d63-137">Opérations de l’API Activité</span><span class="sxs-lookup"><span data-stu-id="36d63-137">Activity API operations</span></span>

<span data-ttu-id="36d63-138">Toutes les opérations de l’API sont limitées à un seul locataire et l’URL racine de l’API inclut un ID de locataire qui spécifie le contexte du locataire.</span><span class="sxs-lookup"><span data-stu-id="36d63-138">All API operations are scoped to a single tenant and the root URL of the API includes a tenant ID that specifies the tenant context.</span></span> <span data-ttu-id="36d63-139">L’ID de locataire est un GUID.</span><span class="sxs-lookup"><span data-stu-id="36d63-139">The tenant ID is a GUID.</span></span> <span data-ttu-id="36d63-140">Pour savoir comment obtenir le GUID, consultez l’article relatif à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="36d63-140">For information about how to get the GUID, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span> 

<span data-ttu-id="36d63-141">Étant donné que les notifications que nous envoyons à votre webhook incluent l’ID de locataire, vous pouvez utiliser le même webhook pour recevoir des notifications pour tous les locataires.</span><span class="sxs-lookup"><span data-stu-id="36d63-141">Because the notifications we send to your webhook include the tenant ID, you can use the same webhook to receive notifications for all tenants.</span></span>

<span data-ttu-id="36d63-142">L’URL du point de terminaison de l’API que vous utilisez est basée sur le type d’abonnement Microsoft 365 ou Office 365 pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="36d63-142">The URL for the API endpoint that you use is based on the type of Microsoft 365 or Office 365 subscription plan for your organization.</span></span>

<span data-ttu-id="36d63-143">**Plan Entreprise**</span><span class="sxs-lookup"><span data-stu-id="36d63-143">**Enterprise plan**</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="36d63-144">**Plan pour le secteur public GCC**</span><span class="sxs-lookup"><span data-stu-id="36d63-144">**GCC government plan**</span></span>

```http
https://manage-gcc.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="36d63-145">**Plan pour le secteur public GCC**</span><span class="sxs-lookup"><span data-stu-id="36d63-145">**GCC High government plan**</span></span>

```http
https://manage.office365.us/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="36d63-146">**Plan pour le secteur public DoD**</span><span class="sxs-lookup"><span data-stu-id="36d63-146">**DoD government plan**</span></span>

```http
https://manage.protection.apps.mil/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="36d63-p109">Toutes les opérations de l’API nécessitent un en-tête HTTP d’autorisation avec un jeton d’accès provenant d’Azure AD. L’ID de locataire présent dans le jeton d’accès doit correspondre à l’ID de locataire indiqué dans l’URL racine de l’API. De plus, le jeton d’accès doit contenir la revendication ActivityFeed.Read (qui correspond à l’autorisation [Lire les données d’activité d’une organisation] configurée pour votre application dans Azure AD).</span><span class="sxs-lookup"><span data-stu-id="36d63-p109">All API operations require an Authorization HTTP header with an access token obtained from Azure AD. The tenant ID in the access token must match the tenant ID in the root URL of the API and the access token must contain the ActivityFeed.Read claim (this corresponds to the permission [Read activity data for an organization] that you configured for you application in Azure AD).</span></span>

```json
Authorization: Bearer eyJ0e...Qa6wg
```

<span data-ttu-id="36d63-149">L’API Activité prend en charge les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="36d63-149">The Activity API supports the following operations:</span></span>

- <span data-ttu-id="36d63-150">**Démarrer un abonnement** pour commencer à recevoir des notifications et récupérer les données d’activité d’un locataire.</span><span class="sxs-lookup"><span data-stu-id="36d63-150">**Start a subscription** to begin receiving notifications and retrieving activity data for a tenant.</span></span>
    
- <span data-ttu-id="36d63-151">**Arrêter un abonnement** pour ne plus récupérer les données d’un locataire.</span><span class="sxs-lookup"><span data-stu-id="36d63-151">**Stop a subscription** to discontinue retrieving data for a tenant.</span></span>
    
- <span data-ttu-id="36d63-152">**Répertorier les abonnements actifs**</span><span class="sxs-lookup"><span data-stu-id="36d63-152">**List current subscriptions**</span></span>
    
- <span data-ttu-id="36d63-153">**Répertorier le contenu disponible** et les URL de contenu correspondantes.</span><span class="sxs-lookup"><span data-stu-id="36d63-153">**List available content** and the corresponding content URLs.</span></span>
    
- <span data-ttu-id="36d63-154">**Recevoir des notifications** envoyées par un webhook dès que du nouveau contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-154">**Receiving notifications** sent by a webhook when new content is available.</span></span>
    
- <span data-ttu-id="36d63-155">**Récupérer du contenu** à l’aide de l’URL de contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-155">**Retrieving content** by using the content URL.</span></span>
    
- <span data-ttu-id="36d63-156">**Répertorier les notifications** envoyées par un webhook.</span><span class="sxs-lookup"><span data-stu-id="36d63-156">**List notifications** sent by a webhook.</span></span>

- <span data-ttu-id="36d63-157">**Récupérer les noms conviviaux des ressources** pour les objets du flux de données identifiés par un GUID.</span><span class="sxs-lookup"><span data-stu-id="36d63-157">**Retrieve resource friendly names** for objects in the data feed identified by guids.</span></span>
    

## <a name="start-a-subscription"></a><span data-ttu-id="36d63-158">Démarrer un abonnement</span><span class="sxs-lookup"><span data-stu-id="36d63-158">Start a subscription</span></span>

<span data-ttu-id="36d63-159">Cette opération démarre l’abonnement souscrit pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="36d63-159">This operation starts a subscription to the specified content type.</span></span> <span data-ttu-id="36d63-160">Si un abonnement pour le type de contenu spécifié existe déjà, cette opération sert à :</span><span class="sxs-lookup"><span data-stu-id="36d63-160">If a subscription to the specified content type already exists, this operation is used to:</span></span>

- <span data-ttu-id="36d63-161">mettre à jour les propriétés d’un webhook actif.</span><span class="sxs-lookup"><span data-stu-id="36d63-161">Update the properties of an active webhook.</span></span>
    
- <span data-ttu-id="36d63-162">activer un webhook qui a été désactivé en raison du nombre excessif de notifications d’échec envoyées.</span><span class="sxs-lookup"><span data-stu-id="36d63-162">Enable a webhook that was disabled because of excessive failed notifications.</span></span>
    
- <span data-ttu-id="36d63-163">réactiver un webhook expiré en spécifiant une date d’expiration Null ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="36d63-163">Re-enable an expired webhook by specifying a later or null expiration date.</span></span>
    
- <span data-ttu-id="36d63-164">supprimer un webhook.</span><span class="sxs-lookup"><span data-stu-id="36d63-164">Remove a webhook.</span></span>
    
||<span data-ttu-id="36d63-165">Abonnement</span><span class="sxs-lookup"><span data-stu-id="36d63-165">Subscription</span></span>|<span data-ttu-id="36d63-166">Description</span><span class="sxs-lookup"><span data-stu-id="36d63-166">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="36d63-167">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="36d63-167">**Path**</span></span>| `/subscriptions/start?contentType={ContentType}`||
|<span data-ttu-id="36d63-168">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="36d63-168">**Parameters**</span></span>|<span data-ttu-id="36d63-169">contentType</span><span class="sxs-lookup"><span data-stu-id="36d63-169">contentType</span></span>|<span data-ttu-id="36d63-170">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="36d63-170">Must be a valid content type.</span></span>|
||<span data-ttu-id="36d63-171">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="36d63-171">PublisherIdentifier</span></span>|<span data-ttu-id="36d63-172">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="36d63-172">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="36d63-173">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="36d63-173">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="36d63-174">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="36d63-174">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="36d63-175">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="36d63-175">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="36d63-176">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="36d63-176">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="36d63-177">**Corps**</span><span class="sxs-lookup"><span data-stu-id="36d63-177">**Body**</span></span>|<span data-ttu-id="36d63-178">webhook</span><span class="sxs-lookup"><span data-stu-id="36d63-178">webhook</span></span>|<span data-ttu-id="36d63-179">Cet objet JSON facultatif comprend trois propriétés :</span><span class="sxs-lookup"><span data-stu-id="36d63-179">Optional JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-180"><b>address</b> : point de terminaison HTTPS obligatoire qui peut recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="36d63-180"><b>address</b>: Required HTTPS endpoint that can receive notifications.</span></span>  <span data-ttu-id="36d63-181">Un message test est envoyé au webhook pour valider le webhook avant de créer l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="36d63-181">A test message will be sent to the webhook to validate the webhook before creating the subscription.</span></span></p></li><li><p><span data-ttu-id="36d63-182"><b>authId</b> : chaîne facultative incluse comme en-tête WebHook-AuthID dans les notifications envoyées au webhook pour identifier et autoriser la source de la requête envoyée au webhook.</span><span class="sxs-lookup"><span data-stu-id="36d63-182"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span></span></p></li><li><p><span data-ttu-id="36d63-183"><b>expiration</b> : date/heure (valeur facultative) après laquelle les notifications ne doivent plus être envoyées au webhook.</span><span class="sxs-lookup"><span data-stu-id="36d63-183"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span></span></p></li></ul>|
|<span data-ttu-id="36d63-184">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="36d63-184">**Response**</span></span>|<span data-ttu-id="36d63-185">contentType</span><span class="sxs-lookup"><span data-stu-id="36d63-185">contentType</span></span>|<span data-ttu-id="36d63-186">Type de contenu spécifié dans l’appel.</span><span class="sxs-lookup"><span data-stu-id="36d63-186">The content type specified in the call.</span></span>|
||<span data-ttu-id="36d63-187">statut</span><span class="sxs-lookup"><span data-stu-id="36d63-187">status</span></span>|<span data-ttu-id="36d63-p113">État de l’abonnement. Si un abonnement est désactivé, vous ne pourrez pas répertorier ou récupérer du contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-p113">The status of the subscription. If a subscription is disabled, you will not be able to list or retrieve content.</span></span>|
||<span data-ttu-id="36d63-190">webhook</span><span class="sxs-lookup"><span data-stu-id="36d63-190">webhook</span></span>|<span data-ttu-id="36d63-191">Propriétés du webhook spécifiées dans l’appel avec l’état du webhook.</span><span class="sxs-lookup"><span data-stu-id="36d63-191">The webhook properties specified in the call together with the status of the webhook.</span></span> <span data-ttu-id="36d63-192">Si le webhook est désactivé, vous ne recevez pas de notification, mais vous pouvez toujours répertorier et récupérer du contenu, à condition que l’abonnement soit activé.</span><span class="sxs-lookup"><span data-stu-id="36d63-192">If the webhook is disabled, you will not receive notification, but you will still be able to list and retrieve content, provided the subscription is enabled.</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="36d63-193">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="36d63-193">Sample request</span></span>

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


#### <a name="sample-response"></a><span data-ttu-id="36d63-194">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="36d63-194">Sample response</span></span>

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


## <a name="webhook-validation"></a><span data-ttu-id="36d63-195">Validation du webhook</span><span class="sxs-lookup"><span data-stu-id="36d63-195">Webhook validation</span></span>

<span data-ttu-id="36d63-196">Quand l’opération /start est appelée et un webhook est spécifié, nous vous envoyons une notification de validation à l’adresse de webhook indiquée pour confirmer qu’un détecteur actif peut accepter et traiter les notifications.</span><span class="sxs-lookup"><span data-stu-id="36d63-196">When the /start operation is called and a webhook is specified, we will send a validation notification to the specified webhook address to validate that an active listener can accept and process notifications.</span></span> <span data-ttu-id="36d63-197">Si nous ne recevons pas une réponse HTTP 200 OK, l’abonnement n’est pas créé.</span><span class="sxs-lookup"><span data-stu-id="36d63-197">If we do not receive an HTTP 200 OK response, the subscription will not be created.</span></span> <span data-ttu-id="36d63-198">Sinon, si l’opération /start est appelée pour ajouter un webhook à un abonnement existant et si nous ne recevons pas une réponse HTTP 200 OK, le webhook n’est pas ajouté et l’abonnement reste inchangé.</span><span class="sxs-lookup"><span data-stu-id="36d63-198">Or, if /start is being called to add a webhook to an existing subscription and a response of HTTP 200 OK is not received, the webhook will not be added and the subscription will remain unchanged.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="36d63-199">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="36d63-199">Sample request</span></span>

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId, if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a><span data-ttu-id="36d63-200">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="36d63-200">Sample response</span></span>

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a><span data-ttu-id="36d63-201">Arrêter un abonnement</span><span class="sxs-lookup"><span data-stu-id="36d63-201">Stop a subscription</span></span>

<span data-ttu-id="36d63-202">Cette opération arrête un abonnement souscrit pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="36d63-202">This operation stops a subscription to the specified content type.</span></span> 

<span data-ttu-id="36d63-203">Quand un abonnement est arrêté, vous ne recevez plus de notifications et vous ne pouvez pas récupérer le contenu disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-203">When a subscription is stopped, you will no longer receive notifications and you will not be able to retrieve available content.</span></span> <span data-ttu-id="36d63-204">Si, plus tard, vous décidez de redémarrer l’abonnement, vous aurez accès au nouveau contenu disponible à partir de ce moment-là.</span><span class="sxs-lookup"><span data-stu-id="36d63-204">If the subscription is later restarted, you will have access to new content from that point forward.</span></span> <span data-ttu-id="36d63-205">Vous ne pourrez pas récupérer le contenu mis à disposition pendant la période où l’abonnement était arrêté.</span><span class="sxs-lookup"><span data-stu-id="36d63-205">You will not be able to retrieve content that was available between the time the subscription was stopped and restarted.</span></span>


||<span data-ttu-id="36d63-206">Abonnement</span><span class="sxs-lookup"><span data-stu-id="36d63-206">Subscription</span></span>|<span data-ttu-id="36d63-207">Description</span><span class="sxs-lookup"><span data-stu-id="36d63-207">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="36d63-208">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="36d63-208">**Path**</span></span>| `/subscriptions/stop?contentType={ContentType}`||
|<span data-ttu-id="36d63-209">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="36d63-209">**Parameters**</span></span>|<span data-ttu-id="36d63-210">contentType</span><span class="sxs-lookup"><span data-stu-id="36d63-210">contentType</span></span>|<span data-ttu-id="36d63-211">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="36d63-211">Must be a valid content type.</span></span>|
||<span data-ttu-id="36d63-212">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="36d63-212">PublisherIdentifier</span></span>|<span data-ttu-id="36d63-213">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="36d63-213">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="36d63-214">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="36d63-214">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="36d63-215">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="36d63-215">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="36d63-216">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="36d63-216">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="36d63-217">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="36d63-217">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="36d63-218">**Corps**</span><span class="sxs-lookup"><span data-stu-id="36d63-218">**Body**</span></span>|<span data-ttu-id="36d63-219">(vide)</span><span class="sxs-lookup"><span data-stu-id="36d63-219">(empty)</span></span>||
|<span data-ttu-id="36d63-220">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="36d63-220">**Response**</span></span>|<span data-ttu-id="36d63-221">(vide)</span><span class="sxs-lookup"><span data-stu-id="36d63-221">(empty)</span></span>|||

#### <a name="sample-request"></a><span data-ttu-id="36d63-222">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="36d63-222">Sample request</span></span>

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="36d63-223">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="36d63-223">Sample response</span></span>

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a><span data-ttu-id="36d63-224">Répertorier les abonnements actifs</span><span class="sxs-lookup"><span data-stu-id="36d63-224">List current subscriptions</span></span>

<span data-ttu-id="36d63-225">Cette opération renvoie une collection d’abonnements actifs avec les webhooks associés.</span><span class="sxs-lookup"><span data-stu-id="36d63-225">This operation returns a collection of the current subscriptions together with the associated webhooks.</span></span>

||<span data-ttu-id="36d63-226">Abonnement</span><span class="sxs-lookup"><span data-stu-id="36d63-226">Subscription</span></span>|<span data-ttu-id="36d63-227">Description</span><span class="sxs-lookup"><span data-stu-id="36d63-227">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="36d63-228">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="36d63-228">**Path**</span></span>| `/subscriptions/list`||
|<span data-ttu-id="36d63-229">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="36d63-229">**Parameters**</span></span>|<span data-ttu-id="36d63-230">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="36d63-230">PublisherIdentifier</span></span>|<span data-ttu-id="36d63-231">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="36d63-231">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="36d63-232">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="36d63-232">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="36d63-233">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="36d63-233">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="36d63-234">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="36d63-234">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="36d63-235">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="36d63-235">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="36d63-236">**Corps**</span><span class="sxs-lookup"><span data-stu-id="36d63-236">**Body**</span></span>|<span data-ttu-id="36d63-237">(vide)</span><span class="sxs-lookup"><span data-stu-id="36d63-237">(empty)</span></span>||
|<span data-ttu-id="36d63-238">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="36d63-238">**Response**</span></span>|<span data-ttu-id="36d63-239">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="36d63-239">JSON array</span></span>|<span data-ttu-id="36d63-240">Chaque abonnement est représenté par un objet JSON comprenant trois propriétés :</span><span class="sxs-lookup"><span data-stu-id="36d63-240">Each subscription will be represented by a JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-241"><b>contentType</b> : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-241"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="36d63-242"><b>status</b> : indique le statut de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="36d63-242"><b>status</b>: Indicates the status of the subscription.</span></span></p></li><li><p><span data-ttu-id="36d63-243"><b>webhook</b> : indique le webhook configuré avec l’état (activé, désactivé, expiré) du webhook.</span><span class="sxs-lookup"><span data-stu-id="36d63-243"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.</span></span>  <span data-ttu-id="36d63-244">Si un abonnement n’a pas de webhook, la propriété du webhook est indiquée avec une valeur Null.</span><span class="sxs-lookup"><span data-stu-id="36d63-244">If a subscription does not have a webhook, the webhook property will be present but with null value.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="36d63-245">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="36d63-245">Sample request</span></span>

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="36d63-246">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="36d63-246">Sample response</span></span>

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


## <a name="list-available-content"></a><span data-ttu-id="36d63-247">Répertorier le contenu disponible</span><span class="sxs-lookup"><span data-stu-id="36d63-247">List available content</span></span>

<span data-ttu-id="36d63-248">Cette opération répertorie le contenu actuellement disponible que vous pouvez récupérer pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="36d63-248">This operation lists the content currently available for retrieval for the specified content type.</span></span> <span data-ttu-id="36d63-249">Le contenu est une agrégation des actions et des événements collectés sur plusieurs serveurs de plusieurs centres de données.</span><span class="sxs-lookup"><span data-stu-id="36d63-249">The content is an aggregation of actions and events harvested from multiple servers across multiple datacenters.</span></span> <span data-ttu-id="36d63-250">Le contenu est répertorié dans l’ordre de mise à disposition des agrégations. En revanche, nous ne pouvons pas garantir que les événements et les actions des agrégations sont répertoriés de manière séquentielle.</span><span class="sxs-lookup"><span data-stu-id="36d63-250">The content will be listed in the order in which the aggregations become available, but the events and actions within the aggregations are not guaranteed to be sequential.</span></span> <span data-ttu-id="36d63-251">Une erreur est renvoyée si l’état de l’abonnement est désactivé.</span><span class="sxs-lookup"><span data-stu-id="36d63-251">An error is returned if the subscription status is disabled.</span></span>


||<span data-ttu-id="36d63-252">Abonnement</span><span class="sxs-lookup"><span data-stu-id="36d63-252">Subscription</span></span>|<span data-ttu-id="36d63-253">Description</span><span class="sxs-lookup"><span data-stu-id="36d63-253">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="36d63-254">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="36d63-254">**Path**</span></span>| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="36d63-255">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="36d63-255">**Parameters**</span></span>|<span data-ttu-id="36d63-256">contentType</span><span class="sxs-lookup"><span data-stu-id="36d63-256">contentType</span></span>|<span data-ttu-id="36d63-257">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="36d63-257">Must be a valid content type.</span></span>|
||<span data-ttu-id="36d63-258">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="36d63-258">PublisherIdentifier</span></span>|<span data-ttu-id="36d63-259">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="36d63-259">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="36d63-260">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="36d63-260">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="36d63-261">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="36d63-261">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="36d63-262">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="36d63-262">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="36d63-263">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="36d63-263">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="36d63-264">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="36d63-264">startTime endTime</span></span>|<span data-ttu-id="36d63-265">Date/Heure (UTC) facultative indiquant l’intervalle de temps à prendre en compte pour renvoyer le contenu, selon le moment à partir duquel le contenu est devenu disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-265">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="36d63-266">L’intervalle de temps est compris entre l’heure de début (startTime <= contentCreated) et l’heure de fin (contentCreated < endTime). Ainsi, les intervalles de temps sont incrémentés sans se chevaucher pour permettre de parcourir le contenu disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-266">The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-267">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="36d63-267">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="36d63-268">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="36d63-268">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="36d63-269">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="36d63-269">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="36d63-270">L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="36d63-270">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="36d63-271">Par défaut, si l’heure de début et l’heure de fin ne sont pas renseignées, le contenu disponible au cours des dernières 24 heures est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="36d63-271">By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span></span><p><span data-ttu-id="36d63-272">**REMARQUE** : même si l’heure de début et l’heure de fin peuvent être espacées de plus de 24 heures, nous vous déconseillons de le faire.</span><span class="sxs-lookup"><span data-stu-id="36d63-272">**NOTE**: Even though it is possible to specify a startTime and endTime more than 24 hours apart, this is not recommended.</span></span> <span data-ttu-id="36d63-273">Par ailleurs, si vous obtenez des résultats en réponse à une requête portant sur un intervalle de plus de 24 heures, ces résultats peuvent être partiels et ne doivent pas être pris en compte.</span><span class="sxs-lookup"><span data-stu-id="36d63-273">Furthermore, if you do get any results in response to a request for more than 24 hours, these could be partial results and should not be taken into account.</span></span> <span data-ttu-id="36d63-274">L’intervalle de la requête émise entre l’heure de début et l’heure de fin doit couvrir une plage horaire de moins de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="36d63-274">The request should be issued with an interval of no more than 24 hours between the startTime and endTime.</span></span></p>|
|<span data-ttu-id="36d63-275">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="36d63-275">**Response**</span></span>|<span data-ttu-id="36d63-276">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="36d63-276">JSON array</span></span>|<span data-ttu-id="36d63-277">Le contenu disponible est représenté par des objets JSON comprenant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="36d63-277">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-278"><b>contentType</b> : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-278"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="36d63-279"><b>contentId</b> : chaîne opaque qui identifie le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-279"><b>contentId</b>: An opaque string that uniquely identifies the content.</span></span></p></li><li><p><span data-ttu-id="36d63-280"><b>contentUri</b> : URL à utiliser pour récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-280"><b>contentUri</b>: The URL to use when retrieving the content.</span></span></p></li><li><p><span data-ttu-id="36d63-281"><b>contentCreated</b> : date/heure à laquelle le contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-281"><b>contentCreated</b>: The datetime when the content was made available.</span></span></p></li><li><p><span data-ttu-id="36d63-282"><b>contentExpiration</b> : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-282"><b>contentExpiration</b>: The datetime after which the content will no longer be available for retrieval.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="36d63-283">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="36d63-283">Sample request</span></span>

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="36d63-284">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="36d63-284">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="36d63-285">Pagination</span><span class="sxs-lookup"><span data-stu-id="36d63-285">Pagination</span></span>

<span data-ttu-id="36d63-286">Quand vous répertoriez le contenu disponible au cours d’un intervalle de temps donné, le nombre de résultats renvoyés est limité pour éviter de dépasser le délai de réponse.</span><span class="sxs-lookup"><span data-stu-id="36d63-286">When listing available content for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="36d63-287">Si d’autres résultats correspondent à l’intervalle de temps spécifié mais ne peuvent pas être renvoyés dans une seule réponse, les résultats sont tronqués et un en-tête est ajouté à la réponse indiquant l’URL à utiliser pour accéder à la page de résultats suivante.</span><span class="sxs-lookup"><span data-stu-id="36d63-287">If there are more results in the specified time range than can be returned in single response, the results will be truncated and a header will be added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="36d63-288">L’URL contient les mêmes paramètres _startTime_ et _endTime_ qui ont été spécifiés dans la requête d’origine, ainsi qu’un paramètre indiquant l’ID interne de la page suivante.</span><span class="sxs-lookup"><span data-stu-id="36d63-288">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="36d63-289">Si les paramètres _startTime_ et _endTime_ ne sont pas spécifiés dans la requête d’origine, ils indiquent l’intervalle de 24 heures qui précède la requête d’origine.</span><span class="sxs-lookup"><span data-stu-id="36d63-289">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="36d63-290">Pour répertorier tout le contenu disponible dans un intervalle de temps spécifié, vous devrez peut-être récupérer plusieurs pages jusqu’à ce que vous receviez une réponse qui ne contient pas l’en-tête **NextPageUri**.</span><span class="sxs-lookup"><span data-stu-id="36d63-290">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>


## <a name="receiving-notifications"></a><span data-ttu-id="36d63-291">Réception des notifications</span><span class="sxs-lookup"><span data-stu-id="36d63-291">Receiving notifications</span></span>

<span data-ttu-id="36d63-292">Les notifications sont envoyées au webhook configuré pour un abonnement au fur et à mesure que le nouveau contenu devient disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-292">Notifications are sent to the configured webhook for a subscription as new content becomes available.</span></span> <span data-ttu-id="36d63-293">Étant donné que les notifications incluent l’ID de locataire, vous pouvez utiliser le même webhook pour recevoir des notifications pour tous les locataires auxquels vous êtes abonné.</span><span class="sxs-lookup"><span data-stu-id="36d63-293">Because the notification includes the tenant identifier, you can use the same webhook to receive notifications for all tenants for which you have subscriptions.</span></span>

<span data-ttu-id="36d63-294">La notification est envoyée sous la forme d’une requête HTTP POST sur TLS (TLS 1.0 et versions ultérieures) à l’adresse de webhook spécifiée.</span><span class="sxs-lookup"><span data-stu-id="36d63-294">The notification is made as an HTTP POST over TLS (TLS 1.0 and later versions) to the specified webhook address.</span></span> <span data-ttu-id="36d63-295">Si la configuration du webhook inclut un ID d’authentification, nous l’envoyons comme en-tête HTTP : Webhook-AuthID.</span><span class="sxs-lookup"><span data-stu-id="36d63-295">If the webhook configuration includes an auth ID, we will send it as an HTTP header: Webhook-AuthID.</span></span> <span data-ttu-id="36d63-296">Les réponses qui n’incluent pas HTTP 200 OK seront considérées comme ayant échoué et la notification sera renvoyée.</span><span class="sxs-lookup"><span data-stu-id="36d63-296">Any response other than HTTP 200 OK will be considered a failure and the notification will be retried.</span></span> <span data-ttu-id="36d63-297">Vous pouvez également configurer votre webhook pour exiger une authentification basée sur les certificats clients ; nous nous authentifierons alors à l’aide du certificat manage.office.com.</span><span class="sxs-lookup"><span data-stu-id="36d63-297">You can also configure your webhook to require client certificate-based authentication and we will authenticate using the manage.office.com certificate.</span></span>

<span data-ttu-id="36d63-298">Le corps de la requête contiendra une matrice comprenant un ou plusieurs objets JSON qui représentent les blobs de contenu disponibles.</span><span class="sxs-lookup"><span data-stu-id="36d63-298">The body of the request will contain an array of one or more JSON objects that represent the available content blobs.</span></span> <span data-ttu-id="36d63-299">Le nombre de blobs de contenu compris dans chaque notification est limité pour réduire au maximum la taille de la notification.</span><span class="sxs-lookup"><span data-stu-id="36d63-299">The number of content blobs in each notification is limited to keep the size of the notification relatively small.</span></span> <span data-ttu-id="36d63-300">Dans la mesure où cette limite peut être modifiée, votre implémentation doit interroger la longueur de la matrice au lieu de prévoir une taille fixe.</span><span class="sxs-lookup"><span data-stu-id="36d63-300">Because this limit might change, your implementation should query for the length of the array instead of expecting a fixed size.</span></span> <span data-ttu-id="36d63-301">Chaque objet inclura les mêmes propriétés renvoyées par l’opération /content ainsi que le GUID du locataire auquel appartiennent les données et le GUID de l’application ayant créé les abonnements.</span><span class="sxs-lookup"><span data-stu-id="36d63-301">Each object will include the same properties returned by the /content operation, together with the GUID of the tenant to which the data belongs and the GUID of your application that created the subscriptions.</span></span> <span data-ttu-id="36d63-302">Ainsi, le webhook peut établir le contexte dans lequel il est utilisé avec plusieurs locataires et applications.</span><span class="sxs-lookup"><span data-stu-id="36d63-302">This allows the webhook to establish context when it is being used with multiple tenants and applications.</span></span>

- <span data-ttu-id="36d63-303">**tenantId** : GUID du locataire auquel appartient le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-303">**tenantId**: The GUID of the tenant to which the content belongs.</span></span>
    
- <span data-ttu-id="36d63-304">**clientId** : GUID de votre application qui a créé l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="36d63-304">**clientId**: The GUID of your application that created the subscription.</span></span>
    
- <span data-ttu-id="36d63-305">**contentType** : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-305">**contentType**: Indicates the content type.</span></span>
    
- <span data-ttu-id="36d63-306">**contentId** : chaîne opaque qui identifie le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-306">**contentId**: An opaque string that uniquely identifies the content.</span></span>
    
- <span data-ttu-id="36d63-307">**contentUri** : URL à utiliser pour récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-307">**contentUri**: The URL to use when retrieving the content.</span></span>
    
- <span data-ttu-id="36d63-308">**contentCreated** : date/heure à laquelle le contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-308">**contentCreated**: The datetime when the content was made available.</span></span>
    
- <span data-ttu-id="36d63-309">**contentExpiration** : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-309">**contentExpiration**: The datetime after which the content will no longer be available for retrieval.</span></span>
    
<span data-ttu-id="36d63-310">Vous trouverez ci-dessous un exemple de notification.</span><span class="sxs-lookup"><span data-stu-id="36d63-310">The following is an example of a notification.</span></span>

```json
POST https://webhook.myapp.com/o365/ 
Content-Type: application/json; utf-8
Webhook-AuthID: o365activityapinotification

[
    {
        "tenantId": "{GUID}",
        "clientId": "{GUID}",
        "contentType": "Audit.SharePoint",
        "contentId": "492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentUri": "https://manage.office.com/api/v1.0/f28ab78a-d401-4060-8012-736e373933eb/activity/feed/audit/492638008028$492638008028$f28ab78ad40140608012736e373933ebspo2015043022$4a81a7c326fc4aed89c62e6039ab833b$04",
        "contentCreated": "2015-05-23T17:35:00.000Z",
        "contentExpiration": "2015-05-30T17:35:00.000Z"
    },
    ...
]

```


## <a name="notification-failure-and-retry"></a><span data-ttu-id="36d63-311">Échec de notification et nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="36d63-311">Notification failure and retry</span></span>

<span data-ttu-id="36d63-312">Le système de notification envoie des notifications dès que du nouveau contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-312">The notification system sends notifications as new content becomes available.</span></span> <span data-ttu-id="36d63-313">Si l’envoi des notifications échoue à de multiples reprises, le délai d’attente entre chaque nouvelle tentative augmente.</span><span class="sxs-lookup"><span data-stu-id="36d63-313">If we encounter excessive failures when sending notifications, our retry mechanism will exponentially increase the time between retries.</span></span> <span data-ttu-id="36d63-314">Si l’envoi des notifications continue d’échouer, nous nous réservons le droit de désactiver le webhook et d’arrêter de lui envoyer des notifications.</span><span class="sxs-lookup"><span data-stu-id="36d63-314">If we continue to encounter failures, we reserve the right to disable the webhook and stop sending notifications to it altogether.</span></span> <span data-ttu-id="36d63-315">L’opération /start peut être utilisée pour réactiver un webhook désactivé.</span><span class="sxs-lookup"><span data-stu-id="36d63-315">The /start operation can be used to re-enable a disabled webhook.</span></span>


## <a name="retrieving-content"></a><span data-ttu-id="36d63-316">Récupérer du contenu</span><span class="sxs-lookup"><span data-stu-id="36d63-316">Retrieving content</span></span>

<span data-ttu-id="36d63-317">Pour récupérer un blob de contenu, envoyez une requête GET à l’URI de contenu correspondante qui figure dans la liste du contenu disponible et dans les notifications envoyées au webhook.</span><span class="sxs-lookup"><span data-stu-id="36d63-317">To retrieve a content blob, make a GET request against the corresponding content URI that is included in the list of available content and in the notifications sent to a webhook.</span></span> <span data-ttu-id="36d63-318">Le contenu renvoyé correspondra à une collection d’un ou de plusieurs événements ou actions au format JSON.</span><span class="sxs-lookup"><span data-stu-id="36d63-318">The returned content will be a collection of one more actions or events in JSON format.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="36d63-319">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="36d63-319">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a><span data-ttu-id="36d63-320">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="36d63-320">Sample response</span></span>

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


## <a name="list-notifications"></a><span data-ttu-id="36d63-321">Répertorier les notifications</span><span class="sxs-lookup"><span data-stu-id="36d63-321">List notifications</span></span>

<span data-ttu-id="36d63-322">Cette opération répertorie toutes les tentatives de notification associées au type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="36d63-322">This operation lists all notification attempts for the specified content type.</span></span> <span data-ttu-id="36d63-323">Si vous n’avez pas inclus un webhook au démarrage de l’abonnement souscrit pour le type de contenu, aucune notification ne pourra être récupérée.</span><span class="sxs-lookup"><span data-stu-id="36d63-323">If you did not include a webhook when starting the subscription to the content type, there will be no notifications to retrieve.</span></span> <span data-ttu-id="36d63-324">Dans la mesure où nous renvoyons les notifications en cas d’échec de l’envoi initial, cette opération peut renvoyer plusieurs notifications pour le même contenu. Par ailleurs, l’ordre dans lequel les notifications sont envoyées ne correspond pas nécessairement à l’ordre de parution du contenu (en particulier en cas d’échecs et de nouvelles tentatives).</span><span class="sxs-lookup"><span data-stu-id="36d63-324">Because we retry notifications in the event of failure, this operation can return multiple notifications for the same content, and the order in which the notifications are sent will not necessarily match the order in which the content became available (especially when there are failures and retries).</span></span> 

<span data-ttu-id="36d63-325">Vous pouvez utiliser cette opération pour vous aider à résoudre les problèmes liés aux webhooks et aux notifications, mais nous vous déconseillons de l’utiliser pour déterminer le contenu disponible que vous pouvez récupérer.</span><span class="sxs-lookup"><span data-stu-id="36d63-325">You can use this operation to help investigate issues related to webhooks and notifications, but you should not use it to determine what content is currently available for retrieval.</span></span> <span data-ttu-id="36d63-326">Pour cela, utilisez plutôt l’opération /content.</span><span class="sxs-lookup"><span data-stu-id="36d63-326">Use the /content operation instead.</span></span> <span data-ttu-id="36d63-327">Nous renvoyons une erreur si l’état de l’abonnement est désactivé.</span><span class="sxs-lookup"><span data-stu-id="36d63-327">We return an error if the subscription status is disabled.</span></span>


||<span data-ttu-id="36d63-328">Abonnement</span><span class="sxs-lookup"><span data-stu-id="36d63-328">Subscription</span></span>|<span data-ttu-id="36d63-329">Description</span><span class="sxs-lookup"><span data-stu-id="36d63-329">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="36d63-330">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="36d63-330">**Path**</span></span>| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="36d63-331">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="36d63-331">**Parameters**</span></span>|<span data-ttu-id="36d63-332">contentType</span><span class="sxs-lookup"><span data-stu-id="36d63-332">contentType</span></span>|<span data-ttu-id="36d63-333">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="36d63-333">Must be a valid content type.</span></span>|
||<span data-ttu-id="36d63-334">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="36d63-334">PublisherIdentifier</span></span>|<span data-ttu-id="36d63-335">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="36d63-335">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="36d63-336">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="36d63-336">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="36d63-337">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="36d63-337">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="36d63-338">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="36d63-338">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="36d63-339">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="36d63-339">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="36d63-340">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="36d63-340">startTime endTime</span></span>|<span data-ttu-id="36d63-341">Date/Heure (UTC) facultative indiquant l’intervalle de temps à prendre en compte pour renvoyer le contenu, selon le moment à partir duquel le contenu est devenu disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-341">Optional datetimes (UTC) that indicate the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="36d63-342">L’intervalle de temps est délimité par les paramètres _startTime_ (_startTime_ <= contentCreated) et _endTime_ (_contentCreated_ < endTime). Ainsi, les intervalles de temps sont incrémentés sans se chevaucher pour permettre de parcourir le contenu disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-342">The time range is inclusive with respect to  _startTime_ ( _startTime_ <= contentCreated) and exclusive with respect to _endTime_ (_contentCreated_ < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-343">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="36d63-343">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="36d63-344">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="36d63-344">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="36d63-345">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="36d63-345">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="36d63-346">L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="36d63-346">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="36d63-347">Par défaut, si les paramètres _startTime_ et _endTime_ ne sont pas renseignés, le contenu disponible au cours des dernières 24 heures est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="36d63-347">By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span></span>|
|<span data-ttu-id="36d63-348">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="36d63-348">**Response**</span></span>|<span data-ttu-id="36d63-349">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="36d63-349">JSON array</span></span>|<span data-ttu-id="36d63-350">Les notifications sont représentées par des objets JSON comprenant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="36d63-350">The notifications will be represented by JSON objects with the following properties:</span></span> <ul><li><span data-ttu-id="36d63-351">**contentType** : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-351">**contentType**: indicates the content type.</span></span></li><li><span data-ttu-id="36d63-352">**contentId** : chaîne opaque qui identifie le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-352">**contentId**: an opaque string that uniquely identifies the content.</span></span></li><li><span data-ttu-id="36d63-353">**contentUri** : URL à utiliser pour récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-353">**contentUri**: the URL to use when retrieving the content.</span></span> </li><li><span data-ttu-id="36d63-354">**contentCreated** : date/heure à laquelle le contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="36d63-354">**contentCreated**: the datetime when the content was made available.</span></span></li><li><span data-ttu-id="36d63-355">**contentExpiration** : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="36d63-355">**contentExpiration**: the datetime after which the content will no longer be available for retrieval.</span></span></li><li><span data-ttu-id="36d63-356">**notificationSent** : date/heure d’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="36d63-356">**notificationSent**: the datetime when the notification was sent.</span></span></li><li><span data-ttu-id="36d63-357">**notificationStatus** : indique la réussite ou l’échec de la tentative de notification.</span><span class="sxs-lookup"><span data-stu-id="36d63-357">**notificationStatus**: indicates the success or failure of the notification attempt.</span></span></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="36d63-358">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="36d63-358">Sample request</span></span>

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="36d63-359">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="36d63-359">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="36d63-360">Pagination</span><span class="sxs-lookup"><span data-stu-id="36d63-360">Pagination</span></span>

<span data-ttu-id="36d63-361">Quand vous répertoriez l’historique de notification au cours d’un intervalle de temps donné, le nombre de résultats renvoyés est limité pour éviter de dépasser le délai de réponse.</span><span class="sxs-lookup"><span data-stu-id="36d63-361">When listing notification history for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="36d63-362">Si d’autres résultats correspondent à l’intervalle de temps spécifié mais ne peuvent pas être renvoyés dans une seule réponse, les résultats sont tronqués et un en-tête est ajouté à la réponse indiquant l’URL à utiliser pour accéder à la page de résultats suivante.</span><span class="sxs-lookup"><span data-stu-id="36d63-362">If there are more results in the specified time range than can be returned in a single response, the results are truncated and a header is added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="36d63-363">L’URL contient les mêmes paramètres _startTime_ et _endTime_ qui ont été spécifiés dans la requête d’origine, ainsi qu’un paramètre indiquant l’ID interne de la page suivante.</span><span class="sxs-lookup"><span data-stu-id="36d63-363">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="36d63-364">Si les paramètres _startTime_ et _endTime_ ne sont pas spécifiés dans la requête d’origine, ils indiquent l’intervalle de 24 heures qui précède la requête d’origine.</span><span class="sxs-lookup"><span data-stu-id="36d63-364">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="36d63-365">Pour répertorier tout le contenu disponible dans un intervalle de temps spécifié, vous devrez peut-être récupérer plusieurs pages jusqu’à ce que vous receviez une réponse qui ne contient pas l’en-tête **NextPageUri**.</span><span class="sxs-lookup"><span data-stu-id="36d63-365">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>

## <a name="retrieve-resource-friendly-names"></a><span data-ttu-id="36d63-366">Récupération des noms conviviaux des ressources</span><span class="sxs-lookup"><span data-stu-id="36d63-366">Retrieve resource friendly names</span></span>

<span data-ttu-id="36d63-367">Cette opération récupère les noms conviviaux des ressources pour les objets du flux de données identifiés par un GUID.</span><span class="sxs-lookup"><span data-stu-id="36d63-367">This operation retrieves friendly names for objects in the data feed identified by guids.</span></span> <span data-ttu-id="36d63-368">« DlpSensitiveType » est actuellement le seul objet pris en charge.</span><span class="sxs-lookup"><span data-stu-id="36d63-368">Currently "DlpSensitiveType" is the only supported object.</span></span> 


||<span data-ttu-id="36d63-369">Abonnement</span><span class="sxs-lookup"><span data-stu-id="36d63-369">Subscription</span></span>|<span data-ttu-id="36d63-370">Description</span><span class="sxs-lookup"><span data-stu-id="36d63-370">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="36d63-371">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="36d63-371">**Path**</span></span>| `/resources/dlpSensitiveTypes`||
|<span data-ttu-id="36d63-372">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="36d63-372">**Parameters**</span></span>|<span data-ttu-id="36d63-373">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="36d63-373">PublisherIdentifier</span></span>|<span data-ttu-id="36d63-374">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="36d63-374">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="36d63-375">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="36d63-375">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="36d63-376">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="36d63-376">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="36d63-377">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="36d63-377">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="36d63-378">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="36d63-378">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="36d63-379">**En-têtes**</span><span class="sxs-lookup"><span data-stu-id="36d63-379">**Headers**</span></span>|<span data-ttu-id="36d63-380">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="36d63-380">Accept-Language</span></span>|<span data-ttu-id="36d63-381">En-tête pour spécifier la langue dans laquelle les noms doivent être localisés.</span><span class="sxs-lookup"><span data-stu-id="36d63-381">Header to specify the desired language for localized names.</span></span> <span data-ttu-id="36d63-382">Par exemple, utilisez « en-US » pour l’anglais ou « es » pour l’espagnol.</span><span class="sxs-lookup"><span data-stu-id="36d63-382">For example, use "en-US" for English or "es" for Spanish.</span></span> <span data-ttu-id="36d63-383">La langue par défaut (en-US) est renvoyée si cet en-tête n’est pas présent.</span><span class="sxs-lookup"><span data-stu-id="36d63-383">The default language (en-US) will be returned if this header is not present.</span></span>|
|<span data-ttu-id="36d63-384">**Corps**</span><span class="sxs-lookup"><span data-stu-id="36d63-384">**Body**</span></span>|<span data-ttu-id="36d63-385">(vide)</span><span class="sxs-lookup"><span data-stu-id="36d63-385">(empty)</span></span>||
|<span data-ttu-id="36d63-386">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="36d63-386">**Response**</span></span>|<span data-ttu-id="36d63-387">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="36d63-387">JSON array</span></span>|<span data-ttu-id="36d63-388">Le contenu disponible est représenté par des objets JSON comprenant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="36d63-388">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-389"><b>id</b> : indique le GUID du type d’informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="36d63-389"><b>id</b>: Indicates the guid of the sensitive information type.</span></span></p></li><li><p><span data-ttu-id="36d63-390"><b>name</b> : nom convivial du type d’informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="36d63-390"><b>name</b>: The friendly name of the sensitive information type.</span></span></p></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="36d63-391">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="36d63-391">Sample request</span></span>

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a><span data-ttu-id="36d63-392">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="36d63-392">Sample response</span></span>

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

## <a name="api-throttling"></a><span data-ttu-id="36d63-393">Limitation des requêtes de l’API</span><span class="sxs-lookup"><span data-stu-id="36d63-393">API throttling</span></span>

<span data-ttu-id="36d63-394">Les organisations accédant à des journaux d’audit via l’API Activité de gestion d’Office 365 étaient restreintes par des seuils de limitation au niveau de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="36d63-394">Organizations that access auditing logs through the Office 365 Management Activity API were restricted by throttling limits at the publisher level.</span></span> <span data-ttu-id="36d63-395">Cela signifie que pour un éditeur faisant une extraction de données pour le compte de plusieurs clients, la limite était partagée par tous les clients.</span><span class="sxs-lookup"><span data-stu-id="36d63-395">This means that for a publisher pulling data on behalf of multiple customers, the limit was shared by all those customers.</span></span>

<span data-ttu-id="36d63-396">Nous allons passer d’une limite au niveau éditeur à une limite au niveau du client.</span><span class="sxs-lookup"><span data-stu-id="36d63-396">We're moving from a publisher-level limit to a tenant-level limit.</span></span> <span data-ttu-id="36d63-397">Chaque organisation obtient ainsi son propre quota de bande passante entièrement allouée pour accéder à leurs données d’audit.</span><span class="sxs-lookup"><span data-stu-id="36d63-397">The result is that each organization will get their own fully allocated bandwidth quota to access their auditing data.</span></span> <span data-ttu-id="36d63-398">Les organisations reçoivent une ligne de base de 2 000 demandes par minute.</span><span class="sxs-lookup"><span data-stu-id="36d63-398">All organizations are initially allocated a baseline of 2,000 requests per minute.</span></span> <span data-ttu-id="36d63-399">Il ne s’agit pas d’une limite statique prédéfinie, mais elle est modelée sur la combinaison de facteurs, tels que le nombre de sièges au sein de l’organisation, et les organisations Office 365 et Microsoft 365 E5 obtiennent une bande passante à peu près deux fois plus importante que les organisations non E5.</span><span class="sxs-lookup"><span data-stu-id="36d63-399">This is not a static, predefined limit but is modeled on a combination of factors including the number of seats in the organization and that Office 365 and Microsoft 365 E5 organizations will get approximately twice as much bandwidth as non-E5 organizations.</span></span> <span data-ttu-id="36d63-400">La bande passante aura également un plafond maximal pour protéger l’état d’intégrité du service.</span><span class="sxs-lookup"><span data-stu-id="36d63-400">There will also be cap on the maximum bandwidth to protect the health of the service.</span></span>

<span data-ttu-id="36d63-401">Pour plus d’informations, voir la section « Accès à large bande passante à l'API Activité de gestionOffice 365 » dans l'[Audit avancé de Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/advanced-audit#high-bandwidth-access-to-the-office-365-management-activity-api).</span><span class="sxs-lookup"><span data-stu-id="36d63-401">For more information, see the "High-bandwidth access to the Office 365 Management Activity API" section in [Advanced audit in Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/advanced-audit#high-bandwidth-access-to-the-office-365-management-activity-api).</span></span>

> [!NOTE] 
> <span data-ttu-id="36d63-402">Même si chaque client peut initialement envoyer 2 000 requêtes par minute, Microsoft ne peut garantir le taux de réponse.</span><span class="sxs-lookup"><span data-stu-id="36d63-402">Even though each tenant can initially submit up to 2,000 requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="36d63-403">Le taux de réponse dépend de différents facteurs, tels que les performances du système client, la capacité et la vitesse du réseau.</span><span class="sxs-lookup"><span data-stu-id="36d63-403">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span> 

## <a name="errors"></a><span data-ttu-id="36d63-404">Errors</span><span class="sxs-lookup"><span data-stu-id="36d63-404">Errors</span></span>

<span data-ttu-id="36d63-405">Quand le service rencontre une erreur, il signale le code de la réponse d’erreur à l’appelant en utilisant la syntaxe du code d’erreur HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="36d63-405">When the service encounters an error, it will report the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="36d63-406">.</span><span class="sxs-lookup"><span data-stu-id="36d63-406">.</span></span> <span data-ttu-id="36d63-407">Des informations complémentaires sont incluses dans le corps de l’appel ayant échoué en tant qu’objet JSON unique.</span><span class="sxs-lookup"><span data-stu-id="36d63-407">Additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="36d63-408">Voici un exemple du corps complet de l’erreur JSON :</span><span class="sxs-lookup"><span data-stu-id="36d63-408">An example of a full JSON error body is shown below:</span></span> 

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
|<span data-ttu-id="36d63-409">Code</span><span class="sxs-lookup"><span data-stu-id="36d63-409">Code</span></span>|<span data-ttu-id="36d63-410">Message</span><span class="sxs-lookup"><span data-stu-id="36d63-410">Message</span></span>|
|<span data-ttu-id="36d63-411">AF10001</span><span class="sxs-lookup"><span data-stu-id="36d63-411">AF10001</span></span>|<span data-ttu-id="36d63-412">Le jeu d’autorisations ({0}) envoyé dans la requête n’inclut pas l’autorisation **ActivityFeed.Read** attendue.</span><span class="sxs-lookup"><span data-stu-id="36d63-412">The permission set ({0}) sent in the request did not include the expected permission **ActivityFeed.Read**.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-413">{0} = jeu d’autorisations défini dans le jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="36d63-413">{0} = the permission set in the access token.</span></span></p></li></ul>|
|<span data-ttu-id="36d63-414">AF20001</span><span class="sxs-lookup"><span data-stu-id="36d63-414">AF20001</span></span>|<span data-ttu-id="36d63-415">Paramètre manquant : {0}.</span><span class="sxs-lookup"><span data-stu-id="36d63-415">Missing parameter: {0}.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-416">{0} = nom du paramètre manquant.</span><span class="sxs-lookup"><span data-stu-id="36d63-416">{0} = the name of the missing parameter.</span></span></p></li></ul>|
|<span data-ttu-id="36d63-417">AF20002</span><span class="sxs-lookup"><span data-stu-id="36d63-417">AF20002</span></span>|<span data-ttu-id="36d63-418">Type de paramètre non valide : {0}.</span><span class="sxs-lookup"><span data-stu-id="36d63-418">Invalid parameter type: {0}.</span></span> <span data-ttu-id="36d63-419">Type attendu : {1}.</span><span class="sxs-lookup"><span data-stu-id="36d63-419">Expected type: {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-420">{0} = nom du paramètre non valide.</span><span class="sxs-lookup"><span data-stu-id="36d63-420">{0} = the name of the invalid parameter.</span></span></p></li><li><p><span data-ttu-id="36d63-421">{1} = type attendu (int, datetime, guid).</span><span class="sxs-lookup"><span data-stu-id="36d63-421">{1} = the expected type (int, datetime, guid).</span></span></p></li></ul>|
|<span data-ttu-id="36d63-422">AF20003</span><span class="sxs-lookup"><span data-stu-id="36d63-422">AF20003</span></span>|<span data-ttu-id="36d63-423">L’expiration {0} fournie indique une date et une heure passées.</span><span class="sxs-lookup"><span data-stu-id="36d63-423">Expiration {0} provided is set to past date and time.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-424">{0} = expiration transmise dans l’appel de l’API.</span><span class="sxs-lookup"><span data-stu-id="36d63-424">{0} = the expiration passed in the API call.</span></span></p></li></ul>|
|<span data-ttu-id="36d63-425">AF20010</span><span class="sxs-lookup"><span data-stu-id="36d63-425">AF20010</span></span>|<span data-ttu-id="36d63-426">L’ID de locataire transmis dans l’URL ({0}) ne correspond pas à l’ID de locataire transmis dans le jeton d’accès ({1}).</span><span class="sxs-lookup"><span data-stu-id="36d63-426">The tenant ID passed in the URL ({0}) does not match the tenant ID passed in the access token ({1}).</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-427">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="36d63-427">{0} = tenant ID passed in the URL</span></span></p></li><li><p><span data-ttu-id="36d63-428">{1} = ID de locataire transmis dans le jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="36d63-428">{1} = tenant ID passed in the access token</span></span></p></li></ul>|
|<span data-ttu-id="36d63-429">AF20011</span><span class="sxs-lookup"><span data-stu-id="36d63-429">AF20011</span></span>|<span data-ttu-id="36d63-430">L’ID de locataire spécifié ({0}) n’existe pas dans le système ou a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="36d63-430">Specified tenant ID ({0}) does not exist in the system or has been deleted.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   <span data-ttu-id="36d63-431">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="36d63-431">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="36d63-432">AF20012</span><span class="sxs-lookup"><span data-stu-id="36d63-432">AF20012</span></span>|<span data-ttu-id="36d63-433">L’ID de locataire spécifié ({0}) est configuré de façon incorrecte dans le système.</span><span class="sxs-lookup"><span data-stu-id="36d63-433">Specified tenant ID ({0}) is incorrectly configured in the system.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    <span data-ttu-id="36d63-434">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="36d63-434">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="36d63-435">AF20013</span><span class="sxs-lookup"><span data-stu-id="36d63-435">AF20013</span></span>|<span data-ttu-id="36d63-436">L’ID de locataire transmis dans l’URL ({0}) n’est pas un GUID valide.</span><span class="sxs-lookup"><span data-stu-id="36d63-436">The tenant ID passed in the URL ({0}) is not a valid GUID.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> <span data-ttu-id="36d63-437">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="36d63-437">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="36d63-438">AF20020</span><span class="sxs-lookup"><span data-stu-id="36d63-438">AF20020</span></span>|<span data-ttu-id="36d63-439">Le type de contenu spécifié n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="36d63-439">The specified content type is not valid.</span></span>|
|<span data-ttu-id="36d63-440">AF20021</span><span class="sxs-lookup"><span data-stu-id="36d63-440">AF20021</span></span>|<span data-ttu-id="36d63-p145">Le point de terminaison de webhook {{0}) n’a pas été validé. {1}</span><span class="sxs-lookup"><span data-stu-id="36d63-p145">The webhook endpoint {{0}) could not be validated. {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-443">{0} = adresse de webhook.</span><span class="sxs-lookup"><span data-stu-id="36d63-443">{0} = webhook address.</span></span></p></li><li><p><span data-ttu-id="36d63-444">{1} = « Le point de terminaison n’a pas renvoyé HTTP 200. »</span><span class="sxs-lookup"><span data-stu-id="36d63-444">{1} = "The endpoint did not return HTTP 200."</span></span> <span data-ttu-id="36d63-445">ou « L’adresse doit commencer par HTTPS. ».</span><span class="sxs-lookup"><span data-stu-id="36d63-445">or "The address must begin with HTTPS."</span></span></p></li></ul>|
|<span data-ttu-id="36d63-446">AF20022</span><span class="sxs-lookup"><span data-stu-id="36d63-446">AF20022</span></span>|<span data-ttu-id="36d63-447">Aucun abonnement trouvé pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="36d63-447">No subscription found for the specified content type.</span></span>|
|<span data-ttu-id="36d63-448">AF20023</span><span class="sxs-lookup"><span data-stu-id="36d63-448">AF20023</span></span>|<span data-ttu-id="36d63-449">L’abonnement a été désactivé par {0}.</span><span class="sxs-lookup"><span data-stu-id="36d63-449">The subscription was disabled by {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-450">{0} = « un administrateur du locataire » ou « administrateur du service »</span><span class="sxs-lookup"><span data-stu-id="36d63-450">{0} = "a tenant admin" or "a service admin"</span></span></p></li></ul>|
|<span data-ttu-id="36d63-451">AF20030</span><span class="sxs-lookup"><span data-stu-id="36d63-451">AF20030</span></span>|<span data-ttu-id="36d63-452">L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="36d63-452">Start time and end time must both be specified (or both omitted) and must be less than or equal to 24 hours apart, with the start time no more than 7 days in the past.</span></span>|
|<span data-ttu-id="36d63-453">AF20031</span><span class="sxs-lookup"><span data-stu-id="36d63-453">AF20031</span></span>|<span data-ttu-id="36d63-454">Saisie nextPage non valide : {0}.</span><span class="sxs-lookup"><span data-stu-id="36d63-454">Invalid nextPage Input: {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-455">{0} = indicateur de la page suivante transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="36d63-455">{0} = the next page indicator passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="36d63-456">AF20050</span><span class="sxs-lookup"><span data-stu-id="36d63-456">AF20050</span></span>|<span data-ttu-id="36d63-457">Le contenu spécifié ({0}) n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="36d63-457">The specified content ({0}) does not exist.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-458">{0} = ID ou URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="36d63-458">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="36d63-459">AF20051</span><span class="sxs-lookup"><span data-stu-id="36d63-459">AF20051</span></span>|<span data-ttu-id="36d63-460">Le contenu demandé avec la touche {0} a déjà expiré.</span><span class="sxs-lookup"><span data-stu-id="36d63-460">Content requested with the key {0} has already expired.</span></span> <span data-ttu-id="36d63-461">Le contenu datant de plus de 7 jours ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="36d63-461">Content older than 7 days cannot be retrieved.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-462">•    {0} = ID ou URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="36d63-462">•    {0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="36d63-463">AF20052</span><span class="sxs-lookup"><span data-stu-id="36d63-463">AF20052</span></span>|<span data-ttu-id="36d63-464">L’ID de contenu {0} dans l’URL n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="36d63-464">Content ID {0} in the URL is invalid.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-465">{0} = ID ou URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="36d63-465">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="36d63-466">AF20053</span><span class="sxs-lookup"><span data-stu-id="36d63-466">AF20053</span></span>|<span data-ttu-id="36d63-467">Une seule langue peut être indiquée dans l’en-tête Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="36d63-467">Only one language may be present in the Accept-Language header.</span></span>|
|<span data-ttu-id="36d63-468">AF20054</span><span class="sxs-lookup"><span data-stu-id="36d63-468">AF20054</span></span>|<span data-ttu-id="36d63-469">Syntaxe non valide dans l’en-tête Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="36d63-469">Invalid syntax in Accept-Language header.</span></span>|
|<span data-ttu-id="36d63-470">AF429</span><span class="sxs-lookup"><span data-stu-id="36d63-470">AF429</span></span>|<span data-ttu-id="36d63-471">Trop de demandes.</span><span class="sxs-lookup"><span data-stu-id="36d63-471">Too many requests.</span></span> <span data-ttu-id="36d63-472">Method={0}, PublisherId={1}</span><span class="sxs-lookup"><span data-stu-id="36d63-472">Method={0}, PublisherId={1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="36d63-473">{0} = méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="36d63-473">{0} = HTTP Method</span></span></p></li><li><p><span data-ttu-id="36d63-474">{1} = GUID de locataire utilisé en tant que PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="36d63-474">{1} = Tenant GUID used as PublisherIdentifier</span></span></p></li></ul>|
|<span data-ttu-id="36d63-475">AF50000</span><span class="sxs-lookup"><span data-stu-id="36d63-475">AF50000</span></span>|<span data-ttu-id="36d63-476">Une erreur interne s’est produite.</span><span class="sxs-lookup"><span data-stu-id="36d63-476">An internal error occurred.</span></span> <span data-ttu-id="36d63-477">Retentez la requête.</span><span class="sxs-lookup"><span data-stu-id="36d63-477">Retry the request.</span></span>|
