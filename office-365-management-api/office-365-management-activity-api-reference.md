---
ms.TocTitle: Office 365 Management Activity API reference
title: Référence de l’API Activité de gestion Office 365
description: Cet article explique comment utiliser l’API Activité de gestion Office 365 pour récupérer des informations sur les actions et les événements des utilisateurs, des administrateurs, du système et des stratégies à partir des journaux d’activité Office 365 et Azure AD.
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 48065e1770e485ffa04778d662a170ae14916354
ms.sourcegitcommit: d55928a0d535090fa2dbe94f38c7316d0e52e9a9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2020
ms.locfileid: "44173140"
---
# <a name="office-365-management-activity-api-reference"></a><span data-ttu-id="e81c5-103">Référence de l’API Activité de gestion Office 365</span><span class="sxs-lookup"><span data-stu-id="e81c5-103">Office 365 Management Activity API reference</span></span>

<span data-ttu-id="e81c5-104">Cet article explique comment utiliser l’API Activité de gestion Office 365 pour récupérer des informations sur les actions et les événements des utilisateurs, des administrateurs, du système et des stratégies à partir des journaux d’activité Office 365 et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e81c5-104">Use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Office 365 and Azure AD activity logs.</span></span> 

<span data-ttu-id="e81c5-105">Vous pouvez utiliser les actions et les événements à partir des journaux d’audit et d’activité Office 365 et Microsoft Azure Active Directory pour créer des solutions de supervision, d’analyse et de visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="e81c5-105">You can use the actions and events from the Office 365 and Microsoft Azure Active Directory audit and activity logs to create solutions that provide monitoring, analysis, and data visualization.</span></span> <span data-ttu-id="e81c5-106">Ces solutions offrent aux organisations une meilleure visibilité sur les actions effectuées sur leur contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-106">These solutions give organizations greater visibility into actions taken on their content.</span></span> <span data-ttu-id="e81c5-107">Ces actions et ces événements sont également disponibles dans les rapports d’activité Office 365.</span><span class="sxs-lookup"><span data-stu-id="e81c5-107">These actions and events are also available in the Office 365 Activity Reports.</span></span> <span data-ttu-id="e81c5-108">Pour en savoir plus, reportez-vous à l’article [Effectuer des recherches dans le journal d’audit dans le Centre de sécurité et de conformité Office 365](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span><span class="sxs-lookup"><span data-stu-id="e81c5-108">For more information, see [Search the audit log in the Office 365 Security & Compliance Center](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span></span>

<span data-ttu-id="e81c5-109">L’API Activité de gestion Office 365 est un service web REST qui vous permet de développer des solutions à l’aide de n’importe quel langage et environnement d’hébergement qui prend en charge les certificats X.509 et HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e81c5-109">The Office 365 Management Activity API is a REST web service that you can use to develop solutions using any language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="e81c5-110">L’API s’appuie sur Azure AD et le protocole OAuth2 pour l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="e81c5-110">The API relies on Azure AD and the OAuth2 protocol for authentication and authorization.</span></span> <span data-ttu-id="e81c5-111">Pour accéder à l’API depuis votre application, inscrivez-la d’abord dans Azure AD et configurez-la avec les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="e81c5-111">To access the API from your application, you'll need to first register it in Azure AD and configure it with appropriate permissions.</span></span> <span data-ttu-id="e81c5-112">Ainsi, votre application pourra demander les jetons d’accès OAuth2 dont elle a besoin pour appeler l’API.</span><span class="sxs-lookup"><span data-stu-id="e81c5-112">This will enable your application to request the OAuth2 access tokens it needs to call the API.</span></span> <span data-ttu-id="e81c5-113">Pour en savoir plus, consultez l’article relatif à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="e81c5-113">For more information, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="e81c5-114">Pour obtenir des informations sur les données renvoyées par l’API Activité de gestion Office 365 ainsi que sur les problèmes connus et les modifications à venir risquant d’affecter votre implémentation, consultez l’article relatif au [schéma de l’API Activité de gestion Office 365](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e81c5-114">For information about the data that the Office 365 Management Activity API returns, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e81c5-115">Avant de pouvoir accéder aux données via l’API Activité de gestion Office 365, vous devez activer la journalisation d’audit unifié pour votre organisation Office 365.</span><span class="sxs-lookup"><span data-stu-id="e81c5-115">Before you can access data through the Office 365 Management Activity API, you must enable unified audit logging for your Office 365 organization.</span></span> <span data-ttu-id="e81c5-116">Pour ce faire, vous devez activer le journal d’audit d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="e81c5-116">You do this by turning on the Office 365 audit log.</span></span> <span data-ttu-id="e81c5-117">Pour obtenir des instructions, consultez la rubrique [Activer ou désactiver la recherche dans un journal d’audit Office 365](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span><span class="sxs-lookup"><span data-stu-id="e81c5-117">For instructions, see [Turn Office 365 audit log search on or off](https://docs.microsoft.com/office365/securitycompliance/turn-audit-log-search-on-or-off).</span></span>


## <a name="working-with-the-office-365-management-activity-api"></a><span data-ttu-id="e81c5-118">Utilisation de l’API Activité de gestion Office 365</span><span class="sxs-lookup"><span data-stu-id="e81c5-118">Working with the Office 365 Management Activity API</span></span>

<span data-ttu-id="e81c5-119">L’API Activité de gestion Office 365 agrège des actions et des événements dans des blobs de contenu propres au locataire, classés selon le type et la source du contenu qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="e81c5-119">The Office 365 Management Activity API aggregates actions and events into tenant-specific content blobs, which are classified by the type and source of the content they contain.</span></span> <span data-ttu-id="e81c5-120">Actuellement, les types de contenu suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="e81c5-120">Currently, these content types are supported:</span></span>

- <span data-ttu-id="e81c5-121">Audit.AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="e81c5-121">Audit.AzureActiveDirectory</span></span>
    
- <span data-ttu-id="e81c5-122">Audit.Exchange</span><span class="sxs-lookup"><span data-stu-id="e81c5-122">Audit.Exchange</span></span>
    
- <span data-ttu-id="e81c5-123">Audit.SharePoint</span><span class="sxs-lookup"><span data-stu-id="e81c5-123">Audit.SharePoint</span></span>
    
- <span data-ttu-id="e81c5-124">Audit.General (comprend toutes les autres charges de travail non incluses dans les types de contenu précédents)</span><span class="sxs-lookup"><span data-stu-id="e81c5-124">Audit.General (includes all other workloads not included in the previous content types)</span></span>

- <span data-ttu-id="e81c5-125">DLP.All (événements DLP liés à toutes les charges de travail)</span><span class="sxs-lookup"><span data-stu-id="e81c5-125">DLP.All (DLP events only for all workloads)</span></span>
    
<span data-ttu-id="e81c5-126">Pour en savoir plus sur les événements et les propriétés associés à ces types de contenu, consultez l’article relatif au [schéma de l’API Activité de gestion Office 365](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e81c5-126">For details about the events and properties associated with these content types, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

<span data-ttu-id="e81c5-127">Pour commencer à récupérer des blobs de contenu associés à un locataire, créez d’abord un abonnement aux types de contenu souhaités.</span><span class="sxs-lookup"><span data-stu-id="e81c5-127">To begin retrieving content blobs for a tenant, you first a create subscription to the desired content types.</span></span> <span data-ttu-id="e81c5-128">Si vous récupérez des blobs de contenu associés à plusieurs locataires, créez un abonnement à chacun des types de contenu souhaités pour chaque client.</span><span class="sxs-lookup"><span data-stu-id="e81c5-128">If you are retrieving content blobs for multiple tenants, you create multiple subscriptions to each of the desired content types, one for each tenant.</span></span>

<span data-ttu-id="e81c5-129">Une fois qu’un abonnement est créé, vous pouvez régulièrement l’interroger pour découvrir les nouveaux blobs de contenu disponibles au téléchargement. Sinon, vous pouvez inscrire un point de terminaison de webhook avec l’abonnement, auquel nous enverrons des notifications dès que de nouveaux blobs de contenu sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="e81c5-129">After you create a subscription, you can poll regularly to discover new content blobs that are available for download, or you can register a webhook endpoint with the subscription and we will send notifications to this endpoint as new content blobs are available.</span></span>


> [!NOTE] 
> <span data-ttu-id="e81c5-130">Quand un abonnement est créé, il faut attendre jusqu’à 12 heures avant que les premiers blobs de contenu associés à cet abonnement deviennent disponibles.</span><span class="sxs-lookup"><span data-stu-id="e81c5-130">When a subscription is created, it can take up to 12 hours for the first content blobs to become available for that subscription.</span></span> <span data-ttu-id="e81c5-131">Les blobs de contenu sont créés en collectant et en agrégeant des actions et des événements sur plusieurs serveurs et centres de données.</span><span class="sxs-lookup"><span data-stu-id="e81c5-131">The content blobs are created by collecting and aggregating actions and events across multiple servers and datacenters.</span></span> <span data-ttu-id="e81c5-132">À la suite de ce processus distribué, les actions et les événements contenus dans les blobs de contenu n’apparaissent pas nécessairement dans l’ordre dans lequel ils ont eu lieu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-132">As a result of this distributed process, the actions and events contained in the content blobs will not necessarily appear in the order in which they occurred.</span></span> <span data-ttu-id="e81c5-133">Un blob de contenu peut contenir des actions et des événements qui ont eu lieu avant les actions et les événements contenus dans un blob de contenu antérieur.</span><span class="sxs-lookup"><span data-stu-id="e81c5-133">One content blob can contain actions and events that occurred prior to the actions and events contained in an earlier content blob.</span></span> <span data-ttu-id="e81c5-134">Nous mettons tout en œuvre pour réduire la latence entre l’occurrence des actions et des événements et leur disponibilité au sein d’un blob de contenu, mais nous ne pouvons pas garantir qu’elles apparaissent de manière séquentielle.</span><span class="sxs-lookup"><span data-stu-id="e81c5-134">We are working to decrease the latency between the occurrence of actions and events and their availability within a content blob, but we can't guarantee that they appear sequentially.</span></span>


> [!NOTE] 
> <span data-ttu-id="e81c5-135">Les données sensibles régies par les stratégies de protection contre la perte de données (DLP) sont disponibles dans l’API Flux d’activités uniquement pour les utilisateurs auxquels les autorisations « Lire les données sensibles DLP » ont été accordées.</span><span class="sxs-lookup"><span data-stu-id="e81c5-135">DLP sensitive data is only available in the activity feed API to users that have been granted “Read DLP sensitive data” permissions.</span></span> <span data-ttu-id="e81c5-136">Pour en savoir plus, reportez-vous à l’article [Vue d’ensemble des stratégies de protection contre la perte de données](https://support.office.com/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e).</span><span class="sxs-lookup"><span data-stu-id="e81c5-136">For more on Data Loss Prevention (DLP) see [Overview of Data Loss Prevention Policies](https://support.office.com/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span></span>

## <a name="activity-api-operations"></a><span data-ttu-id="e81c5-137">Opérations de l’API Activité</span><span class="sxs-lookup"><span data-stu-id="e81c5-137">Activity API operations</span></span>

<span data-ttu-id="e81c5-138">Toutes les opérations de l’API sont limitées à un seul locataire et l’URL racine de l’API inclut un ID de locataire qui spécifie le contexte du locataire.</span><span class="sxs-lookup"><span data-stu-id="e81c5-138">All API operations are scoped to a single tenant and the root URL of the API includes a tenant ID that specifies the tenant context.</span></span> <span data-ttu-id="e81c5-139">L’ID de locataire est un GUID.</span><span class="sxs-lookup"><span data-stu-id="e81c5-139">The tenant ID is a GUID.</span></span> <span data-ttu-id="e81c5-140">Pour savoir comment obtenir le GUID, consultez l’article relatif à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="e81c5-140">For information about how to get the GUID, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span> 

<span data-ttu-id="e81c5-141">Étant donné que les notifications que nous envoyons à votre webhook incluent l’ID de locataire, vous pouvez utiliser le même webhook pour recevoir des notifications pour tous les locataires.</span><span class="sxs-lookup"><span data-stu-id="e81c5-141">Because the notifications we send to your webhook include the tenant ID, you can use the same webhook to receive notifications for all tenants.</span></span>

<span data-ttu-id="e81c5-142">L’URL du point de terminaison de l’API que vous utilisez est basée sur le type d’abonnement Microsoft 365 ou Office 365 pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="e81c5-142">The URL for the API endpoint that you use is based on the type of Microsoft 365 or Office 365 subscription plan for your organization.</span></span>

<span data-ttu-id="e81c5-143">**Plan entreprise et secteur public GCC**</span><span class="sxs-lookup"><span data-stu-id="e81c5-143">**Enterprise plan and GCC government plan**</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="e81c5-144">**Plan pour le secteur public GCC**</span><span class="sxs-lookup"><span data-stu-id="e81c5-144">**GCC High government plan**</span></span>

```http
https://manage.office365.us/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="e81c5-145">**Plan pour le secteur public DoD**</span><span class="sxs-lookup"><span data-stu-id="e81c5-145">**DoD government plan**</span></span>

```http
https://manage.protection.apps.mil/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="e81c5-146">Toutes les opérations de l’API nécessitent un en-tête HTTP d’autorisation avec un jeton d’accès provenant d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e81c5-146">All API operations require an Authorization HTTP header with an access token obtained from Azure AD.</span></span> <span data-ttu-id="e81c5-147">L’ID de locataire présent dans le jeton d’accès doit correspondre à l’ID de locataire indiqué dans l’URL racine de l’API. De plus, le jeton d’accès doit contenir la revendication ActivityFeed.Read (qui correspond à l’autorisation [Lire les données d’activité d’une organisation] configurée pour votre application dans Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e81c5-147">The tenant ID in the access token must match the tenant ID in the root URL of the API and the access token must contain the ActivityFeed.Read claim (this corresponds to the permission [Read activity data for an organization] that you configured for you application in Azure AD).</span></span>

```json
Authorization: Bearer eyJ0e...Qa6wg
```

<span data-ttu-id="e81c5-148">L’API Activité prend en charge les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e81c5-148">The Activity API supports the following operations:</span></span>

- <span data-ttu-id="e81c5-149">**Démarrer un abonnement** pour commencer à recevoir des notifications et récupérer les données d’activité d’un locataire.</span><span class="sxs-lookup"><span data-stu-id="e81c5-149">**Start a subscription** to begin receiving notifications and retrieving activity data for a tenant.</span></span>
    
- <span data-ttu-id="e81c5-150">**Arrêter un abonnement** pour ne plus récupérer les données d’un locataire.</span><span class="sxs-lookup"><span data-stu-id="e81c5-150">**Stop a subscription** to discontinue retrieving data for a tenant.</span></span>
    
- <span data-ttu-id="e81c5-151">**Répertorier les abonnements actifs**</span><span class="sxs-lookup"><span data-stu-id="e81c5-151">**List current subscriptions**</span></span>
    
- <span data-ttu-id="e81c5-152">**Répertorier le contenu disponible** et les URL de contenu correspondantes.</span><span class="sxs-lookup"><span data-stu-id="e81c5-152">**List available content** and the corresponding content URLs.</span></span>
    
- <span data-ttu-id="e81c5-153">**Recevoir des notifications** envoyées par un webhook dès que du nouveau contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-153">**Receiving notifications** sent by a webhook when new content is available.</span></span>
    
- <span data-ttu-id="e81c5-154">**Récupérer du contenu** à l’aide de l’URL de contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-154">**Retrieving content** by using the content URL.</span></span>
    
- <span data-ttu-id="e81c5-155">**Répertorier les notifications** envoyées par un webhook.</span><span class="sxs-lookup"><span data-stu-id="e81c5-155">**List notifications** sent by a webhook.</span></span>

- <span data-ttu-id="e81c5-156">**Récupérer les noms conviviaux des ressources** pour les objets du flux de données identifiés par un GUID.</span><span class="sxs-lookup"><span data-stu-id="e81c5-156">**Retrieve resource friendly names** for objects in the data feed identified by guids.</span></span>
    

## <a name="start-a-subscription"></a><span data-ttu-id="e81c5-157">Démarrer un abonnement</span><span class="sxs-lookup"><span data-stu-id="e81c5-157">Start a subscription</span></span>

<span data-ttu-id="e81c5-158">Cette opération démarre l’abonnement souscrit pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-158">This operation starts a subscription to the specified content type.</span></span> <span data-ttu-id="e81c5-159">Si un abonnement pour le type de contenu spécifié existe déjà, cette opération sert à :</span><span class="sxs-lookup"><span data-stu-id="e81c5-159">If a subscription to the specified content type already exists, this operation is used to:</span></span>

- <span data-ttu-id="e81c5-160">mettre à jour les propriétés d’un webhook actif.</span><span class="sxs-lookup"><span data-stu-id="e81c5-160">Update the properties of an active webhook.</span></span>
    
- <span data-ttu-id="e81c5-161">activer un webhook qui a été désactivé en raison du nombre excessif de notifications d’échec envoyées.</span><span class="sxs-lookup"><span data-stu-id="e81c5-161">Enable a webhook that was disabled because of excessive failed notifications.</span></span>
    
- <span data-ttu-id="e81c5-162">réactiver un webhook expiré en spécifiant une date d’expiration Null ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e81c5-162">Re-enable an expired webhook by specifying a later or null expiration date.</span></span>
    
- <span data-ttu-id="e81c5-163">supprimer un webhook.</span><span class="sxs-lookup"><span data-stu-id="e81c5-163">Remove a webhook.</span></span>
    
||<span data-ttu-id="e81c5-164">Abonnement</span><span class="sxs-lookup"><span data-stu-id="e81c5-164">Subscription</span></span>|<span data-ttu-id="e81c5-165">Description</span><span class="sxs-lookup"><span data-stu-id="e81c5-165">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="e81c5-166">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="e81c5-166">**Path**</span></span>| `/subscriptions/start?contentType={ContentType}`||
|<span data-ttu-id="e81c5-167">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="e81c5-167">**Parameters**</span></span>|<span data-ttu-id="e81c5-168">contentType</span><span class="sxs-lookup"><span data-stu-id="e81c5-168">contentType</span></span>|<span data-ttu-id="e81c5-169">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="e81c5-169">Must be a valid content type.</span></span>|
||<span data-ttu-id="e81c5-170">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="e81c5-170">PublisherIdentifier</span></span>|<span data-ttu-id="e81c5-171">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="e81c5-171">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="e81c5-172">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="e81c5-172">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="e81c5-173">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="e81c5-173">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="e81c5-174">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-174">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="e81c5-175">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="e81c5-175">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="e81c5-176">**Corps**</span><span class="sxs-lookup"><span data-stu-id="e81c5-176">**Body**</span></span>|<span data-ttu-id="e81c5-177">webhook</span><span class="sxs-lookup"><span data-stu-id="e81c5-177">webhook</span></span>|<span data-ttu-id="e81c5-178">Cet objet JSON facultatif comprend trois propriétés :</span><span class="sxs-lookup"><span data-stu-id="e81c5-178">Optional JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-179"><b>address</b> : point de terminaison HTTPS obligatoire qui peut recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="e81c5-179"><b>address</b>: Required HTTPS endpoint that can receive notifications.</span></span>  <span data-ttu-id="e81c5-180">Un message test est envoyé au webhook pour valider le webhook avant de créer l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="e81c5-180">A test message will be sent to the webhook to validate the webhook before creating the subscription.</span></span></p></li><li><p><span data-ttu-id="e81c5-181"><b>authId</b> : chaîne facultative incluse comme en-tête WebHook-AuthID dans les notifications envoyées au webhook pour identifier et autoriser la source de la requête envoyée au webhook.</span><span class="sxs-lookup"><span data-stu-id="e81c5-181"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span></span></p></li><li><p><span data-ttu-id="e81c5-182"><b>expiration</b> : date/heure (valeur facultative) après laquelle les notifications ne doivent plus être envoyées au webhook.</span><span class="sxs-lookup"><span data-stu-id="e81c5-182"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-183">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e81c5-183">**Response**</span></span>|<span data-ttu-id="e81c5-184">contentType</span><span class="sxs-lookup"><span data-stu-id="e81c5-184">contentType</span></span>|<span data-ttu-id="e81c5-185">Type de contenu spécifié dans l’appel.</span><span class="sxs-lookup"><span data-stu-id="e81c5-185">The content type specified in the call.</span></span>|
||<span data-ttu-id="e81c5-186">statut</span><span class="sxs-lookup"><span data-stu-id="e81c5-186">status</span></span>|<span data-ttu-id="e81c5-187">Statut de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="e81c5-187">The status of the subscription.</span></span> <span data-ttu-id="e81c5-188">Si un abonnement est désactivé, vous ne pouvez pas répertorier ou récupérer du contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-188">If a subscription is disabled, you will not be able to list or retrieve content.</span></span>|
||<span data-ttu-id="e81c5-189">webhook</span><span class="sxs-lookup"><span data-stu-id="e81c5-189">webhook</span></span>|<span data-ttu-id="e81c5-190">Propriétés du webhook spécifiées dans l’appel avec l’état du webhook.</span><span class="sxs-lookup"><span data-stu-id="e81c5-190">The webhook properties specified in the call together with the status of the webhook.</span></span> <span data-ttu-id="e81c5-191">Si le webhook est désactivé, vous ne recevez pas de notification, mais vous pouvez toujours répertorier et récupérer du contenu, à condition que l’abonnement soit activé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-191">If the webhook is disabled, you will not receive notification, but you will still be able to list and retrieve content, provided the subscription is enabled.</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="e81c5-192">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="e81c5-192">Sample request</span></span>

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


#### <a name="sample-response"></a><span data-ttu-id="e81c5-193">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="e81c5-193">Sample response</span></span>

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


## <a name="webhook-validation"></a><span data-ttu-id="e81c5-194">Validation du webhook</span><span class="sxs-lookup"><span data-stu-id="e81c5-194">Webhook validation</span></span>

<span data-ttu-id="e81c5-195">Quand l’opération /start est appelée et un webhook est spécifié, nous vous envoyons une notification de validation à l’adresse de webhook indiquée pour confirmer qu’un détecteur actif peut accepter et traiter les notifications.</span><span class="sxs-lookup"><span data-stu-id="e81c5-195">When the /start operation is called and a webhook is specified, we will send a validation notification to the specified webhook address to validate that an active listener can accept and process notifications.</span></span> <span data-ttu-id="e81c5-196">Si nous ne recevons pas une réponse HTTP 200 OK, l’abonnement n’est pas créé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-196">If we do not receive an HTTP 200 OK response, the subscription will not be created.</span></span> <span data-ttu-id="e81c5-197">Sinon, si l’opération /start est appelée pour ajouter un webhook à un abonnement existant et si nous ne recevons pas une réponse HTTP 200 OK, le webhook n’est pas ajouté et l’abonnement reste inchangé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-197">Or, if /start is being called to add a webhook to an existing subscription and a response of HTTP 200 OK is not received, the webhook will not be added and the subscription will remain unchanged.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="e81c5-198">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="e81c5-198">Sample request</span></span>

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId, if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a><span data-ttu-id="e81c5-199">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="e81c5-199">Sample response</span></span>

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a><span data-ttu-id="e81c5-200">Arrêter un abonnement</span><span class="sxs-lookup"><span data-stu-id="e81c5-200">Stop a subscription</span></span>

<span data-ttu-id="e81c5-201">Cette opération arrête un abonnement souscrit pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-201">This operation stops a subscription to the specified content type.</span></span> 

<span data-ttu-id="e81c5-202">Quand un abonnement est arrêté, vous ne recevez plus de notifications et vous ne pouvez pas récupérer le contenu disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-202">When a subscription is stopped, you will no longer receive notifications and you will not be able to retrieve available content.</span></span> <span data-ttu-id="e81c5-203">Si, plus tard, vous décidez de redémarrer l’abonnement, vous aurez accès au nouveau contenu disponible à partir de ce moment-là.</span><span class="sxs-lookup"><span data-stu-id="e81c5-203">If the subscription is later restarted, you will have access to new content from that point forward.</span></span> <span data-ttu-id="e81c5-204">Vous ne pourrez pas récupérer le contenu mis à disposition pendant la période où l’abonnement était arrêté.</span><span class="sxs-lookup"><span data-stu-id="e81c5-204">You will not be able to retrieve content that was available between the time the subscription was stopped and restarted.</span></span>


||<span data-ttu-id="e81c5-205">Abonnement</span><span class="sxs-lookup"><span data-stu-id="e81c5-205">Subscription</span></span>|<span data-ttu-id="e81c5-206">Description</span><span class="sxs-lookup"><span data-stu-id="e81c5-206">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="e81c5-207">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="e81c5-207">**Path**</span></span>| `/subscriptions/stop?contentType={ContentType}`||
|<span data-ttu-id="e81c5-208">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="e81c5-208">**Parameters**</span></span>|<span data-ttu-id="e81c5-209">contentType</span><span class="sxs-lookup"><span data-stu-id="e81c5-209">contentType</span></span>|<span data-ttu-id="e81c5-210">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="e81c5-210">Must be a valid content type.</span></span>|
||<span data-ttu-id="e81c5-211">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="e81c5-211">PublisherIdentifier</span></span>|<span data-ttu-id="e81c5-212">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="e81c5-212">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="e81c5-213">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="e81c5-213">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="e81c5-214">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="e81c5-214">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="e81c5-215">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-215">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="e81c5-216">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="e81c5-216">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="e81c5-217">**Corps**</span><span class="sxs-lookup"><span data-stu-id="e81c5-217">**Body**</span></span>|<span data-ttu-id="e81c5-218">(vide)</span><span class="sxs-lookup"><span data-stu-id="e81c5-218">(empty)</span></span>||
|<span data-ttu-id="e81c5-219">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e81c5-219">**Response**</span></span>|<span data-ttu-id="e81c5-220">(vide)</span><span class="sxs-lookup"><span data-stu-id="e81c5-220">(empty)</span></span>|||

#### <a name="sample-request"></a><span data-ttu-id="e81c5-221">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="e81c5-221">Sample request</span></span>

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="e81c5-222">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="e81c5-222">Sample response</span></span>

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a><span data-ttu-id="e81c5-223">Répertorier les abonnements actifs</span><span class="sxs-lookup"><span data-stu-id="e81c5-223">List current subscriptions</span></span>

<span data-ttu-id="e81c5-224">Cette opération renvoie une collection d’abonnements actifs avec les webhooks associés.</span><span class="sxs-lookup"><span data-stu-id="e81c5-224">This operation returns a collection of the current subscriptions together with the associated webhooks.</span></span>

||<span data-ttu-id="e81c5-225">Abonnement</span><span class="sxs-lookup"><span data-stu-id="e81c5-225">Subscription</span></span>|<span data-ttu-id="e81c5-226">Description</span><span class="sxs-lookup"><span data-stu-id="e81c5-226">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="e81c5-227">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="e81c5-227">**Path**</span></span>| `/subscriptions/list`||
|<span data-ttu-id="e81c5-228">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="e81c5-228">**Parameters**</span></span>|<span data-ttu-id="e81c5-229">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="e81c5-229">PublisherIdentifier</span></span>|<span data-ttu-id="e81c5-230">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="e81c5-230">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="e81c5-231">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="e81c5-231">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="e81c5-232">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="e81c5-232">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="e81c5-233">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-233">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="e81c5-234">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="e81c5-234">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="e81c5-235">**Corps**</span><span class="sxs-lookup"><span data-stu-id="e81c5-235">**Body**</span></span>|<span data-ttu-id="e81c5-236">(vide)</span><span class="sxs-lookup"><span data-stu-id="e81c5-236">(empty)</span></span>||
|<span data-ttu-id="e81c5-237">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e81c5-237">**Response**</span></span>|<span data-ttu-id="e81c5-238">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="e81c5-238">JSON array</span></span>|<span data-ttu-id="e81c5-239">Chaque abonnement est représenté par un objet JSON comprenant trois propriétés :</span><span class="sxs-lookup"><span data-stu-id="e81c5-239">Each subscription will be represented by a JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-240"><b>contentType</b> : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-240"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="e81c5-241"><b>status</b> : indique le statut de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="e81c5-241"><b>status</b>: Indicates the status of the subscription.</span></span></p></li><li><p><span data-ttu-id="e81c5-242"><b>webhook</b> : indique le webhook configuré avec l’état (activé, désactivé, expiré) du webhook.</span><span class="sxs-lookup"><span data-stu-id="e81c5-242"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.</span></span>  <span data-ttu-id="e81c5-243">Si un abonnement n’a pas de webhook, la propriété du webhook est indiquée avec une valeur Null.</span><span class="sxs-lookup"><span data-stu-id="e81c5-243">If a subscription does not have a webhook, the webhook property will be present but with null value.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="e81c5-244">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="e81c5-244">Sample request</span></span>

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="e81c5-245">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="e81c5-245">Sample response</span></span>

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


## <a name="list-available-content"></a><span data-ttu-id="e81c5-246">Répertorier le contenu disponible</span><span class="sxs-lookup"><span data-stu-id="e81c5-246">List available content</span></span>

<span data-ttu-id="e81c5-247">Cette opération répertorie le contenu actuellement disponible que vous pouvez récupérer pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-247">This operation lists the content currently available for retrieval for the specified content type.</span></span> <span data-ttu-id="e81c5-248">Le contenu est une agrégation des actions et des événements collectés sur plusieurs serveurs de plusieurs centres de données.</span><span class="sxs-lookup"><span data-stu-id="e81c5-248">The content is an aggregation of actions and events harvested from multiple servers across multiple datacenters.</span></span> <span data-ttu-id="e81c5-249">Le contenu est répertorié dans l’ordre de mise à disposition des agrégations. En revanche, nous ne pouvons pas garantir que les événements et les actions des agrégations sont répertoriés de manière séquentielle.</span><span class="sxs-lookup"><span data-stu-id="e81c5-249">The content will be listed in the order in which the aggregations become available, but the events and actions within the aggregations are not guaranteed to be sequential.</span></span> <span data-ttu-id="e81c5-250">Une erreur est renvoyée si l’état de l’abonnement est désactivé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-250">An error is returned if the subscription status is disabled.</span></span>


||<span data-ttu-id="e81c5-251">Abonnement</span><span class="sxs-lookup"><span data-stu-id="e81c5-251">Subscription</span></span>|<span data-ttu-id="e81c5-252">Description</span><span class="sxs-lookup"><span data-stu-id="e81c5-252">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="e81c5-253">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="e81c5-253">**Path**</span></span>| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="e81c5-254">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="e81c5-254">**Parameters**</span></span>|<span data-ttu-id="e81c5-255">contentType</span><span class="sxs-lookup"><span data-stu-id="e81c5-255">contentType</span></span>|<span data-ttu-id="e81c5-256">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="e81c5-256">Must be a valid content type.</span></span>|
||<span data-ttu-id="e81c5-257">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="e81c5-257">PublisherIdentifier</span></span>|<span data-ttu-id="e81c5-258">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="e81c5-258">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="e81c5-259">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="e81c5-259">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="e81c5-260">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="e81c5-260">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="e81c5-261">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-261">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="e81c5-262">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="e81c5-262">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="e81c5-263">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="e81c5-263">startTime endTime</span></span>|<span data-ttu-id="e81c5-264">Date/Heure (UTC) facultative indiquant l’intervalle de temps à prendre en compte pour renvoyer le contenu, selon le moment à partir duquel le contenu est devenu disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-264">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="e81c5-265">L’intervalle de temps est compris entre l’heure de début (startTime <= contentCreated) et l’heure de fin (contentCreated < endTime). Ainsi, les intervalles de temps sont incrémentés sans se chevaucher pour permettre de parcourir le contenu disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-265">The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-266">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="e81c5-266">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="e81c5-267">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="e81c5-267">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="e81c5-268">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="e81c5-268">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="e81c5-269">L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="e81c5-269">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="e81c5-270">Par défaut, si l’heure de début et l’heure de fin ne sont pas renseignées, le contenu disponible au cours des dernières 24 heures est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-270">By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span></span><p><span data-ttu-id="e81c5-271">**REMARQUE** : même si l’heure de début et l’heure de fin peuvent être espacées de plus de 24 heures, nous vous déconseillons de le faire.</span><span class="sxs-lookup"><span data-stu-id="e81c5-271">**NOTE**: Even though it is possible to specify a startTime and endTime more than 24 hours apart, this is not recommended.</span></span> <span data-ttu-id="e81c5-272">Par ailleurs, si vous obtenez des résultats en réponse à une requête portant sur un intervalle de plus de 24 heures, ces résultats peuvent être partiels et ne doivent pas être pris en compte.</span><span class="sxs-lookup"><span data-stu-id="e81c5-272">Furthermore, if you do get any results in response to a request for more than 24 hours, these could be partial results and should not be taken into account.</span></span> <span data-ttu-id="e81c5-273">L’intervalle de la requête émise entre l’heure de début et l’heure de fin doit couvrir une plage horaire de moins de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="e81c5-273">The request should be issued with an interval of no more than 24 hours between the startTime and endTime.</span></span></p>|
|<span data-ttu-id="e81c5-274">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e81c5-274">**Response**</span></span>|<span data-ttu-id="e81c5-275">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="e81c5-275">JSON array</span></span>|<span data-ttu-id="e81c5-276">Le contenu disponible est représenté par des objets JSON comprenant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="e81c5-276">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-277"><b>contentType</b> : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-277"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="e81c5-278"><b>contentId</b> : chaîne opaque qui identifie le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-278"><b>contentId</b>: An opaque string that uniquely identifies the content.</span></span></p></li><li><p><span data-ttu-id="e81c5-279"><b>contentUri</b> : URL à utiliser pour récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-279"><b>contentUri</b>: The URL to use when retrieving the content.</span></span></p></li><li><p><span data-ttu-id="e81c5-280"><b>contentCreated</b> : date/heure à laquelle le contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-280"><b>contentCreated</b>: The datetime when the content was made available.</span></span></p></li><li><p><span data-ttu-id="e81c5-281"><b>contentExpiration</b> : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-281"><b>contentExpiration</b>: The datetime after which the content will no longer be available for retrieval.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="e81c5-282">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="e81c5-282">Sample request</span></span>

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="e81c5-283">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="e81c5-283">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="e81c5-284">Pagination</span><span class="sxs-lookup"><span data-stu-id="e81c5-284">Pagination</span></span>

<span data-ttu-id="e81c5-285">Quand vous répertoriez le contenu disponible au cours d’un intervalle de temps donné, le nombre de résultats renvoyés est limité pour éviter de dépasser le délai de réponse.</span><span class="sxs-lookup"><span data-stu-id="e81c5-285">When listing available content for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="e81c5-286">Si d’autres résultats correspondent à l’intervalle de temps spécifié mais ne peuvent pas être renvoyés dans une seule réponse, les résultats sont tronqués et un en-tête est ajouté à la réponse indiquant l’URL à utiliser pour accéder à la page de résultats suivante.</span><span class="sxs-lookup"><span data-stu-id="e81c5-286">If there are more results in the specified time range than can be returned in single response, the results will be truncated and a header will be added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="e81c5-287">L’URL contient les mêmes paramètres _startTime_ et _endTime_ qui ont été spécifiés dans la requête d’origine, ainsi qu’un paramètre indiquant l’ID interne de la page suivante.</span><span class="sxs-lookup"><span data-stu-id="e81c5-287">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="e81c5-288">Si les paramètres _startTime_ et _endTime_ ne sont pas spécifiés dans la requête d’origine, ils indiquent l’intervalle de 24 heures qui précède la requête d’origine.</span><span class="sxs-lookup"><span data-stu-id="e81c5-288">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="e81c5-289">Pour répertorier tout le contenu disponible dans un intervalle de temps spécifié, vous devrez peut-être récupérer plusieurs pages jusqu’à ce que vous receviez une réponse qui ne contient pas l’en-tête **NextPageUri**.</span><span class="sxs-lookup"><span data-stu-id="e81c5-289">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>


## <a name="receiving-notifications"></a><span data-ttu-id="e81c5-290">Réception des notifications</span><span class="sxs-lookup"><span data-stu-id="e81c5-290">Receiving notifications</span></span>

<span data-ttu-id="e81c5-291">Les notifications sont envoyées au webhook configuré pour un abonnement au fur et à mesure que le nouveau contenu devient disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-291">Notifications are sent to the configured webhook for a subscription as new content becomes available.</span></span> <span data-ttu-id="e81c5-292">Étant donné que les notifications incluent l’ID de locataire, vous pouvez utiliser le même webhook pour recevoir des notifications pour tous les locataires auxquels vous êtes abonné.</span><span class="sxs-lookup"><span data-stu-id="e81c5-292">Because the notification includes the tenant identifier, you can use the same webhook to receive notifications for all tenants for which you have subscriptions.</span></span>

<span data-ttu-id="e81c5-293">La notification est envoyée sous la forme d’une requête HTTP POST sur TLS (TLS 1.0 et versions ultérieures) à l’adresse de webhook spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e81c5-293">The notification is made as an HTTP POST over TLS (TLS 1.0 and later versions) to the specified webhook address.</span></span> <span data-ttu-id="e81c5-294">Si la configuration du webhook inclut un ID d’authentification, nous l’envoyons comme en-tête HTTP : Webhook-AuthID.</span><span class="sxs-lookup"><span data-stu-id="e81c5-294">If the webhook configuration includes an auth ID, we will send it as an HTTP header: Webhook-AuthID.</span></span> <span data-ttu-id="e81c5-295">Les réponses qui n’incluent pas HTTP 200 OK seront considérées comme ayant échoué et la notification sera renvoyée.</span><span class="sxs-lookup"><span data-stu-id="e81c5-295">Any response other than HTTP 200 OK will be considered a failure and the notification will be retried.</span></span> <span data-ttu-id="e81c5-296">Vous pouvez également configurer votre webhook pour exiger une authentification basée sur les certificats clients ; nous nous authentifierons alors à l’aide du certificat manage.office.com.</span><span class="sxs-lookup"><span data-stu-id="e81c5-296">You can also configure your webhook to require client certificate-based authentication and we will authenticate using the manage.office.com certificate.</span></span>

<span data-ttu-id="e81c5-297">Le corps de la requête contiendra une matrice comprenant un ou plusieurs objets JSON qui représentent les blobs de contenu disponibles.</span><span class="sxs-lookup"><span data-stu-id="e81c5-297">The body of the request will contain an array of one or more JSON objects that represent the available content blobs.</span></span> <span data-ttu-id="e81c5-298">Le nombre de blobs de contenu compris dans chaque notification est limité pour réduire au maximum la taille de la notification.</span><span class="sxs-lookup"><span data-stu-id="e81c5-298">The number of content blobs in each notification is limited to keep the size of the notification relatively small.</span></span> <span data-ttu-id="e81c5-299">Dans la mesure où cette limite peut être modifiée, votre implémentation doit interroger la longueur de la matrice au lieu de prévoir une taille fixe.</span><span class="sxs-lookup"><span data-stu-id="e81c5-299">Because this limit might change, your implementation should query for the length of the array instead of expecting a fixed size.</span></span> <span data-ttu-id="e81c5-300">Chaque objet inclura les mêmes propriétés renvoyées par l’opération /content ainsi que le GUID du locataire auquel appartiennent les données et le GUID de l’application ayant créé les abonnements.</span><span class="sxs-lookup"><span data-stu-id="e81c5-300">Each object will include the same properties returned by the /content operation, together with the GUID of the tenant to which the data belongs and the GUID of your application that created the subscriptions.</span></span> <span data-ttu-id="e81c5-301">Ainsi, le webhook peut établir le contexte dans lequel il est utilisé avec plusieurs locataires et applications.</span><span class="sxs-lookup"><span data-stu-id="e81c5-301">This allows the webhook to establish context when it is being used with multiple tenants and applications.</span></span>

- <span data-ttu-id="e81c5-302">**tenantId** : GUID du locataire auquel appartient le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-302">**tenantId**: The GUID of the tenant to which the content belongs.</span></span>
    
- <span data-ttu-id="e81c5-303">**clientId** : GUID de votre application qui a créé l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="e81c5-303">**clientId**: The GUID of your application that created the subscription.</span></span>
    
- <span data-ttu-id="e81c5-304">**contentType** : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-304">**contentType**: Indicates the content type.</span></span>
    
- <span data-ttu-id="e81c5-305">**contentId** : chaîne opaque qui identifie le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-305">**contentId**: An opaque string that uniquely identifies the content.</span></span>
    
- <span data-ttu-id="e81c5-306">**contentUri** : URL à utiliser pour récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-306">**contentUri**: The URL to use when retrieving the content.</span></span>
    
- <span data-ttu-id="e81c5-307">**contentCreated** : date/heure à laquelle le contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-307">**contentCreated**: The datetime when the content was made available.</span></span>
    
- <span data-ttu-id="e81c5-308">**contentExpiration** : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-308">**contentExpiration**: The datetime after which the content will no longer be available for retrieval.</span></span>
    
<span data-ttu-id="e81c5-309">Vous trouverez ci-dessous un exemple de notification.</span><span class="sxs-lookup"><span data-stu-id="e81c5-309">The following is an example of a notification.</span></span>

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


## <a name="notification-failure-and-retry"></a><span data-ttu-id="e81c5-310">Échec de notification et nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="e81c5-310">Notification failure and retry</span></span>

<span data-ttu-id="e81c5-311">Le système de notification envoie des notifications dès que du nouveau contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-311">The notification system sends notifications as new content becomes available.</span></span> <span data-ttu-id="e81c5-312">Si l’envoi des notifications échoue à de multiples reprises, le délai d’attente entre chaque nouvelle tentative augmente.</span><span class="sxs-lookup"><span data-stu-id="e81c5-312">If we encounter excessive failures when sending notifications, our retry mechanism will exponentially increase the time between retries.</span></span> <span data-ttu-id="e81c5-313">Si l’envoi des notifications continue d’échouer, nous nous réservons le droit de désactiver le webhook et d’arrêter de lui envoyer des notifications.</span><span class="sxs-lookup"><span data-stu-id="e81c5-313">If we continue to encounter failures, we reserve the right to disable the webhook and stop sending notifications to it altogether.</span></span> <span data-ttu-id="e81c5-314">L’opération /start peut être utilisée pour réactiver un webhook désactivé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-314">The /start operation can be used to re-enable a disabled webhook.</span></span>


## <a name="retrieving-content"></a><span data-ttu-id="e81c5-315">Récupérer du contenu</span><span class="sxs-lookup"><span data-stu-id="e81c5-315">Retrieving content</span></span>

<span data-ttu-id="e81c5-316">Pour récupérer un blob de contenu, envoyez une requête GET à l’URI de contenu correspondante qui figure dans la liste du contenu disponible et dans les notifications envoyées au webhook.</span><span class="sxs-lookup"><span data-stu-id="e81c5-316">To retrieve a content blob, make a GET request against the corresponding content URI that is included in the list of available content and in the notifications sent to a webhook.</span></span> <span data-ttu-id="e81c5-317">Le contenu renvoyé correspondra à une collection d’un ou de plusieurs événements ou actions au format JSON.</span><span class="sxs-lookup"><span data-stu-id="e81c5-317">The returned content will be a collection of one more actions or events in JSON format.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="e81c5-318">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="e81c5-318">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a><span data-ttu-id="e81c5-319">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="e81c5-319">Sample response</span></span>

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


## <a name="list-notifications"></a><span data-ttu-id="e81c5-320">Répertorier les notifications</span><span class="sxs-lookup"><span data-stu-id="e81c5-320">List notifications</span></span>

<span data-ttu-id="e81c5-321">Cette opération répertorie toutes les tentatives de notification associées au type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-321">This operation lists all notification attempts for the specified content type.</span></span> <span data-ttu-id="e81c5-322">Si vous n’avez pas inclus un webhook au démarrage de l’abonnement souscrit pour le type de contenu, aucune notification ne pourra être récupérée.</span><span class="sxs-lookup"><span data-stu-id="e81c5-322">If you did not include a webhook when starting the subscription to the content type, there will be no notifications to retrieve.</span></span> <span data-ttu-id="e81c5-323">Dans la mesure où nous renvoyons les notifications en cas d’échec de l’envoi initial, cette opération peut renvoyer plusieurs notifications pour le même contenu. Par ailleurs, l’ordre dans lequel les notifications sont envoyées ne correspond pas nécessairement à l’ordre de parution du contenu (en particulier en cas d’échecs et de nouvelles tentatives).</span><span class="sxs-lookup"><span data-stu-id="e81c5-323">Because we retry notifications in the event of failure, this operation can return multiple notifications for the same content, and the order in which the notifications are sent will not necessarily match the order in which the content became available (especially when there are failures and retries).</span></span> 

<span data-ttu-id="e81c5-324">Vous pouvez utiliser cette opération pour vous aider à résoudre les problèmes liés aux webhooks et aux notifications, mais nous vous déconseillons de l’utiliser pour déterminer le contenu disponible que vous pouvez récupérer.</span><span class="sxs-lookup"><span data-stu-id="e81c5-324">You can use this operation to help investigate issues related to webhooks and notifications, but you should not use it to determine what content is currently available for retrieval.</span></span> <span data-ttu-id="e81c5-325">Pour cela, utilisez plutôt l’opération /content.</span><span class="sxs-lookup"><span data-stu-id="e81c5-325">Use the /content operation instead.</span></span> <span data-ttu-id="e81c5-326">Nous renvoyons une erreur si l’état de l’abonnement est désactivé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-326">We return an error if the subscription status is disabled.</span></span>


||<span data-ttu-id="e81c5-327">Abonnement</span><span class="sxs-lookup"><span data-stu-id="e81c5-327">Subscription</span></span>|<span data-ttu-id="e81c5-328">Description</span><span class="sxs-lookup"><span data-stu-id="e81c5-328">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="e81c5-329">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="e81c5-329">**Path**</span></span>| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="e81c5-330">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="e81c5-330">**Parameters**</span></span>|<span data-ttu-id="e81c5-331">contentType</span><span class="sxs-lookup"><span data-stu-id="e81c5-331">contentType</span></span>|<span data-ttu-id="e81c5-332">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="e81c5-332">Must be a valid content type.</span></span>|
||<span data-ttu-id="e81c5-333">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="e81c5-333">PublisherIdentifier</span></span>|<span data-ttu-id="e81c5-334">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="e81c5-334">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="e81c5-335">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="e81c5-335">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="e81c5-336">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="e81c5-336">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="e81c5-337">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-337">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="e81c5-338">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="e81c5-338">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="e81c5-339">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="e81c5-339">startTime endTime</span></span>|<span data-ttu-id="e81c5-340">Date/Heure (UTC) facultative indiquant l’intervalle de temps à prendre en compte pour renvoyer le contenu, selon le moment à partir duquel le contenu est devenu disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-340">Optional datetimes (UTC) that indicate the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="e81c5-341">L’intervalle de temps est délimité par les paramètres _startTime_ (_startTime_ <= contentCreated) et _endTime_ (_contentCreated_ < endTime). Ainsi, les intervalles de temps sont incrémentés sans se chevaucher pour permettre de parcourir le contenu disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-341">The time range is inclusive with respect to  _startTime_ ( _startTime_ <= contentCreated) and exclusive with respect to _endTime_ (_contentCreated_ < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-342">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="e81c5-342">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="e81c5-343">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="e81c5-343">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="e81c5-344">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="e81c5-344">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="e81c5-345">L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="e81c5-345">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="e81c5-346">Par défaut, si les paramètres _startTime_ et _endTime_ ne sont pas renseignés, le contenu disponible au cours des dernières 24 heures est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-346">By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span></span>|
|<span data-ttu-id="e81c5-347">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e81c5-347">**Response**</span></span>|<span data-ttu-id="e81c5-348">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="e81c5-348">JSON array</span></span>|<span data-ttu-id="e81c5-349">Les notifications sont représentées par des objets JSON comprenant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="e81c5-349">The notifications will be represented by JSON objects with the following properties:</span></span> <ul><li><span data-ttu-id="e81c5-350">**contentType** : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-350">**contentType**: indicates the content type.</span></span></li><li><span data-ttu-id="e81c5-351">**contentId** : chaîne opaque qui identifie le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-351">**contentId**: an opaque string that uniquely identifies the content.</span></span></li><li><span data-ttu-id="e81c5-352">**contentUri** : URL à utiliser pour récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-352">**contentUri**: the URL to use when retrieving the content.</span></span> </li><li><span data-ttu-id="e81c5-353">**contentCreated** : date/heure à laquelle le contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="e81c5-353">**contentCreated**: the datetime when the content was made available.</span></span></li><li><span data-ttu-id="e81c5-354">**contentExpiration** : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="e81c5-354">**contentExpiration**: the datetime after which the content will no longer be available for retrieval.</span></span></li><li><span data-ttu-id="e81c5-355">**notificationSent** : date/heure d’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="e81c5-355">**notificationSent**: the datetime when the notification was sent.</span></span></li><li><span data-ttu-id="e81c5-356">**notificationStatus** : indique la réussite ou l’échec de la tentative de notification.</span><span class="sxs-lookup"><span data-stu-id="e81c5-356">**notificationStatus**: indicates the success or failure of the notification attempt.</span></span></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="e81c5-357">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="e81c5-357">Sample request</span></span>

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="e81c5-358">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="e81c5-358">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="e81c5-359">Pagination</span><span class="sxs-lookup"><span data-stu-id="e81c5-359">Pagination</span></span>

<span data-ttu-id="e81c5-360">Quand vous répertoriez l’historique de notification au cours d’un intervalle de temps donné, le nombre de résultats renvoyés est limité pour éviter de dépasser le délai de réponse.</span><span class="sxs-lookup"><span data-stu-id="e81c5-360">When listing notification history for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="e81c5-361">Si d’autres résultats correspondent à l’intervalle de temps spécifié mais ne peuvent pas être renvoyés dans une seule réponse, les résultats sont tronqués et un en-tête est ajouté à la réponse indiquant l’URL à utiliser pour accéder à la page de résultats suivante.</span><span class="sxs-lookup"><span data-stu-id="e81c5-361">If there are more results in the specified time range than can be returned in a single response, the results are truncated and a header is added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="e81c5-362">L’URL contient les mêmes paramètres _startTime_ et _endTime_ qui ont été spécifiés dans la requête d’origine, ainsi qu’un paramètre indiquant l’ID interne de la page suivante.</span><span class="sxs-lookup"><span data-stu-id="e81c5-362">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="e81c5-363">Si les paramètres _startTime_ et _endTime_ ne sont pas spécifiés dans la requête d’origine, ils indiquent l’intervalle de 24 heures qui précède la requête d’origine.</span><span class="sxs-lookup"><span data-stu-id="e81c5-363">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="e81c5-364">Pour répertorier tout le contenu disponible dans un intervalle de temps spécifié, vous devrez peut-être récupérer plusieurs pages jusqu’à ce que vous receviez une réponse qui ne contient pas l’en-tête **NextPageUrl**.</span><span class="sxs-lookup"><span data-stu-id="e81c5-364">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUrl** header is received.</span></span>

## <a name="retrieve-resource-friendly-names"></a><span data-ttu-id="e81c5-365">Récupération des noms conviviaux des ressources</span><span class="sxs-lookup"><span data-stu-id="e81c5-365">Retrieve resource friendly names</span></span>

<span data-ttu-id="e81c5-366">Cette opération récupère les noms conviviaux des ressources pour les objets du flux de données identifiés par un GUID.</span><span class="sxs-lookup"><span data-stu-id="e81c5-366">This operation retrieves friendly names for objects in the data feed identified by guids.</span></span> <span data-ttu-id="e81c5-367">« DlpSensitiveType » est actuellement le seul objet pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e81c5-367">Currently "DlpSensitiveType" is the only supported object.</span></span> 


||<span data-ttu-id="e81c5-368">Abonnement</span><span class="sxs-lookup"><span data-stu-id="e81c5-368">Subscription</span></span>|<span data-ttu-id="e81c5-369">Description</span><span class="sxs-lookup"><span data-stu-id="e81c5-369">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="e81c5-370">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="e81c5-370">**Path**</span></span>| `/resources/dlpSensitiveTypes`||
|<span data-ttu-id="e81c5-371">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="e81c5-371">**Parameters**</span></span>|<span data-ttu-id="e81c5-372">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="e81c5-372">PublisherIdentifier</span></span>|<span data-ttu-id="e81c5-373">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="e81c5-373">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="e81c5-374">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="e81c5-374">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="e81c5-375">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="e81c5-375">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="e81c5-376">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-376">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="e81c5-377">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="e81c5-377">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="e81c5-378">**En-têtes**</span><span class="sxs-lookup"><span data-stu-id="e81c5-378">**Headers**</span></span>|<span data-ttu-id="e81c5-379">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="e81c5-379">Accept-Language</span></span>|<span data-ttu-id="e81c5-380">En-tête pour spécifier la langue dans laquelle les noms doivent être localisés.</span><span class="sxs-lookup"><span data-stu-id="e81c5-380">Header to specify the desired language for localized names.</span></span> <span data-ttu-id="e81c5-381">Par exemple, utilisez « en-US » pour l’anglais ou « es » pour l’espagnol.</span><span class="sxs-lookup"><span data-stu-id="e81c5-381">For example, use "en-US" for English or "es" for Spanish.</span></span> <span data-ttu-id="e81c5-382">La langue par défaut (en-US) est renvoyée si cet en-tête n’est pas présent.</span><span class="sxs-lookup"><span data-stu-id="e81c5-382">The default language (en-US) will be returned if this header is not present.</span></span>|
|<span data-ttu-id="e81c5-383">**Corps**</span><span class="sxs-lookup"><span data-stu-id="e81c5-383">**Body**</span></span>|<span data-ttu-id="e81c5-384">(vide)</span><span class="sxs-lookup"><span data-stu-id="e81c5-384">(empty)</span></span>||
|<span data-ttu-id="e81c5-385">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="e81c5-385">**Response**</span></span>|<span data-ttu-id="e81c5-386">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="e81c5-386">JSON array</span></span>|<span data-ttu-id="e81c5-387">Le contenu disponible est représenté par des objets JSON comprenant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="e81c5-387">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-388"><b>id</b> : indique le GUID du type d’informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="e81c5-388"><b>id</b>: Indicates the guid of the sensitive information type.</span></span></p></li><li><p><span data-ttu-id="e81c5-389"><b>name</b> : nom convivial du type d’informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="e81c5-389"><b>name</b>: The friendly name of the sensitive information type.</span></span></p></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="e81c5-390">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="e81c5-390">Sample request</span></span>

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a><span data-ttu-id="e81c5-391">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="e81c5-391">Sample response</span></span>

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

## <a name="api-throttling"></a><span data-ttu-id="e81c5-392">Limitation des requêtes de l’API</span><span class="sxs-lookup"><span data-stu-id="e81c5-392">API throttling</span></span>

<span data-ttu-id="e81c5-393">Les organisations accédant à des journaux d’audit via l’API Activité de gestion d’Office 365 étaient restreintes par des seuils de limitation au niveau de l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="e81c5-393">Organizations that access auditing logs through the Office 365 Management Activity API were restricted by throttling limits at the publisher level.</span></span> <span data-ttu-id="e81c5-394">Cela signifie que pour un éditeur faisant une extraction de données pour le compte de plusieurs clients, la limite était partagée par tous les clients.</span><span class="sxs-lookup"><span data-stu-id="e81c5-394">This means that for a publisher pulling data on behalf of multiple customers, the limit was shared by all those customers.</span></span>

<span data-ttu-id="e81c5-395">Nous allons passer d’une limite au niveau éditeur à une limite au niveau du client.</span><span class="sxs-lookup"><span data-stu-id="e81c5-395">We're moving from a publisher-level limit to a tenant-level limit.</span></span> <span data-ttu-id="e81c5-396">Chaque organisation obtient ainsi son propre quota de bande passante entièrement allouée pour accéder à leurs données d’audit.</span><span class="sxs-lookup"><span data-stu-id="e81c5-396">The result is that each organization will get their own fully allocated bandwidth quota to access their auditing data.</span></span> <span data-ttu-id="e81c5-397">Les organisations reçoivent une ligne de base de 2 000 demandes par minute.</span><span class="sxs-lookup"><span data-stu-id="e81c5-397">All organizations are initially allocated a baseline of 2,000 requests per minute.</span></span> <span data-ttu-id="e81c5-398">Il ne s’agit pas d’une limite statique prédéfinie, mais elle est modelée sur la combinaison de facteurs, tels que le nombre de sièges au sein de l’organisation, et les organisations Office 365 et Microsoft 365 E5 obtiennent une bande passante à peu près deux fois plus importante que les organisations non E5.</span><span class="sxs-lookup"><span data-stu-id="e81c5-398">This is not a static, predefined limit but is modeled on a combination of factors including the number of seats in the organization and that Office 365 and Microsoft 365 E5 organizations will get approximately twice as much bandwidth as non-E5 organizations.</span></span> <span data-ttu-id="e81c5-399">La bande passante aura également un plafond maximal pour protéger l’état d’intégrité du service.</span><span class="sxs-lookup"><span data-stu-id="e81c5-399">There will also be cap on the maximum bandwidth to protect the health of the service.</span></span>

<span data-ttu-id="e81c5-400">Pour plus d’informations, voir la section « Accès à large bande passante à l'API Activité de gestionOffice 365 » dans l'[Audit avancé de Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/advanced-audit#high-bandwidth-access-to-the-office-365-management-activity-api).</span><span class="sxs-lookup"><span data-stu-id="e81c5-400">For more information, see the "High-bandwidth access to the Office 365 Management Activity API" section in [Advanced audit in Microsoft 365](https://docs.microsoft.com/microsoft-365/compliance/advanced-audit#high-bandwidth-access-to-the-office-365-management-activity-api).</span></span>

> [!NOTE] 
> <span data-ttu-id="e81c5-401">Même si chaque client peut initialement envoyer 2 000 requêtes par minute, Microsoft ne peut garantir le taux de réponse.</span><span class="sxs-lookup"><span data-stu-id="e81c5-401">Even though each tenant can initially submit up to 2,000 requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="e81c5-402">Le taux de réponse dépend de différents facteurs, tels que les performances du système client, la capacité et la vitesse du réseau.</span><span class="sxs-lookup"><span data-stu-id="e81c5-402">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span> 

## <a name="errors"></a><span data-ttu-id="e81c5-403">Errors</span><span class="sxs-lookup"><span data-stu-id="e81c5-403">Errors</span></span>

<span data-ttu-id="e81c5-404">Quand le service rencontre une erreur, il signale le code de la réponse d’erreur à l’appelant en utilisant la syntaxe du code d’erreur HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="e81c5-404">When the service encounters an error, it will report the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="e81c5-405">.</span><span class="sxs-lookup"><span data-stu-id="e81c5-405">.</span></span> <span data-ttu-id="e81c5-406">Des informations complémentaires sont incluses dans le corps de l’appel ayant échoué en tant qu’objet JSON unique.</span><span class="sxs-lookup"><span data-stu-id="e81c5-406">Additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="e81c5-407">Voici un exemple du corps complet de l’erreur JSON :</span><span class="sxs-lookup"><span data-stu-id="e81c5-407">An example of a full JSON error body is shown below:</span></span> 

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
|<span data-ttu-id="e81c5-408">Code</span><span class="sxs-lookup"><span data-stu-id="e81c5-408">Code</span></span>|<span data-ttu-id="e81c5-409">Message</span><span class="sxs-lookup"><span data-stu-id="e81c5-409">Message</span></span>|
|<span data-ttu-id="e81c5-410">AF10001</span><span class="sxs-lookup"><span data-stu-id="e81c5-410">AF10001</span></span>|<span data-ttu-id="e81c5-411">Le jeu d’autorisations ({0}) envoyé dans la requête n’inclut pas l’autorisation **ActivityFeed.Read** attendue.</span><span class="sxs-lookup"><span data-stu-id="e81c5-411">The permission set ({0}) sent in the request did not include the expected permission **ActivityFeed.Read**.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-412">{0} = jeu d’autorisations défini dans le jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="e81c5-412">{0} = the permission set in the access token.</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-413">AF20001</span><span class="sxs-lookup"><span data-stu-id="e81c5-413">AF20001</span></span>|<span data-ttu-id="e81c5-414">Paramètre manquant : {0}.</span><span class="sxs-lookup"><span data-stu-id="e81c5-414">Missing parameter: {0}.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-415">{0} = nom du paramètre manquant.</span><span class="sxs-lookup"><span data-stu-id="e81c5-415">{0} = the name of the missing parameter.</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-416">AF20002</span><span class="sxs-lookup"><span data-stu-id="e81c5-416">AF20002</span></span>|<span data-ttu-id="e81c5-417">Type de paramètre non valide : {0}.</span><span class="sxs-lookup"><span data-stu-id="e81c5-417">Invalid parameter type: {0}.</span></span> <span data-ttu-id="e81c5-418">Type attendu : {1}.</span><span class="sxs-lookup"><span data-stu-id="e81c5-418">Expected type: {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-419">{0} = nom du paramètre non valide.</span><span class="sxs-lookup"><span data-stu-id="e81c5-419">{0} = the name of the invalid parameter.</span></span></p></li><li><p><span data-ttu-id="e81c5-420">{1} = type attendu (int, datetime, guid).</span><span class="sxs-lookup"><span data-stu-id="e81c5-420">{1} = the expected type (int, datetime, guid).</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-421">AF20003</span><span class="sxs-lookup"><span data-stu-id="e81c5-421">AF20003</span></span>|<span data-ttu-id="e81c5-422">L’expiration {0} fournie indique une date et une heure passées.</span><span class="sxs-lookup"><span data-stu-id="e81c5-422">Expiration {0} provided is set to past date and time.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-423">{0} = expiration transmise dans l’appel de l’API.</span><span class="sxs-lookup"><span data-stu-id="e81c5-423">{0} = the expiration passed in the API call.</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-424">AF20010</span><span class="sxs-lookup"><span data-stu-id="e81c5-424">AF20010</span></span>|<span data-ttu-id="e81c5-425">L’ID de locataire transmis dans l’URL ({0}) ne correspond pas à l’ID de locataire transmis dans le jeton d’accès ({1}).</span><span class="sxs-lookup"><span data-stu-id="e81c5-425">The tenant ID passed in the URL ({0}) does not match the tenant ID passed in the access token ({1}).</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-426">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="e81c5-426">{0} = tenant ID passed in the URL</span></span></p></li><li><p><span data-ttu-id="e81c5-427">{1} = ID de locataire transmis dans le jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="e81c5-427">{1} = tenant ID passed in the access token</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-428">AF20011</span><span class="sxs-lookup"><span data-stu-id="e81c5-428">AF20011</span></span>|<span data-ttu-id="e81c5-429">L’ID de locataire spécifié ({0}) n’existe pas dans le système ou a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-429">Specified tenant ID ({0}) does not exist in the system or has been deleted.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   <span data-ttu-id="e81c5-430">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="e81c5-430">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-431">AF20012</span><span class="sxs-lookup"><span data-stu-id="e81c5-431">AF20012</span></span>|<span data-ttu-id="e81c5-432">L’ID de locataire spécifié ({0}) est configuré de façon incorrecte dans le système.</span><span class="sxs-lookup"><span data-stu-id="e81c5-432">Specified tenant ID ({0}) is incorrectly configured in the system.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    <span data-ttu-id="e81c5-433">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="e81c5-433">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-434">AF20013</span><span class="sxs-lookup"><span data-stu-id="e81c5-434">AF20013</span></span>|<span data-ttu-id="e81c5-435">L’ID de locataire transmis dans l’URL ({0}) n’est pas un GUID valide.</span><span class="sxs-lookup"><span data-stu-id="e81c5-435">The tenant ID passed in the URL ({0}) is not a valid GUID.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> <span data-ttu-id="e81c5-436">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="e81c5-436">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-437">AF20020</span><span class="sxs-lookup"><span data-stu-id="e81c5-437">AF20020</span></span>|<span data-ttu-id="e81c5-438">Le type de contenu spécifié n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="e81c5-438">The specified content type is not valid.</span></span>|
|<span data-ttu-id="e81c5-439">AF20021</span><span class="sxs-lookup"><span data-stu-id="e81c5-439">AF20021</span></span>|<span data-ttu-id="e81c5-440">Le point de terminaison de webhook {{0}) n’a pas été validé.</span><span class="sxs-lookup"><span data-stu-id="e81c5-440">The webhook endpoint {{0}) could not be validated.</span></span> <span data-ttu-id="e81c5-441">{1}</span><span class="sxs-lookup"><span data-stu-id="e81c5-441">{1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-442">{0} = adresse de webhook.</span><span class="sxs-lookup"><span data-stu-id="e81c5-442">{0} = webhook address.</span></span></p></li><li><p><span data-ttu-id="e81c5-443">{1} = « Le point de terminaison n’a pas renvoyé HTTP 200. »</span><span class="sxs-lookup"><span data-stu-id="e81c5-443">{1} = "The endpoint did not return HTTP 200."</span></span> <span data-ttu-id="e81c5-444">ou « L’adresse doit commencer par HTTPS. ».</span><span class="sxs-lookup"><span data-stu-id="e81c5-444">or "The address must begin with HTTPS."</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-445">AF20022</span><span class="sxs-lookup"><span data-stu-id="e81c5-445">AF20022</span></span>|<span data-ttu-id="e81c5-446">Aucun abonnement trouvé pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="e81c5-446">No subscription found for the specified content type.</span></span>|
|<span data-ttu-id="e81c5-447">AF20023</span><span class="sxs-lookup"><span data-stu-id="e81c5-447">AF20023</span></span>|<span data-ttu-id="e81c5-448">L’abonnement a été désactivé par {0}.</span><span class="sxs-lookup"><span data-stu-id="e81c5-448">The subscription was disabled by {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-449">{0} = « un administrateur du locataire » ou « administrateur du service »</span><span class="sxs-lookup"><span data-stu-id="e81c5-449">{0} = "a tenant admin" or "a service admin"</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-450">AF20030</span><span class="sxs-lookup"><span data-stu-id="e81c5-450">AF20030</span></span>|<span data-ttu-id="e81c5-451">L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="e81c5-451">Start time and end time must both be specified (or both omitted) and must be less than or equal to 24 hours apart, with the start time no more than 7 days in the past.</span></span>|
|<span data-ttu-id="e81c5-452">AF20031</span><span class="sxs-lookup"><span data-stu-id="e81c5-452">AF20031</span></span>|<span data-ttu-id="e81c5-453">Saisie nextPage non valide : {0}.</span><span class="sxs-lookup"><span data-stu-id="e81c5-453">Invalid nextPage Input: {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-454">{0} = indicateur de la page suivante transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="e81c5-454">{0} = the next page indicator passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-455">AF20050</span><span class="sxs-lookup"><span data-stu-id="e81c5-455">AF20050</span></span>|<span data-ttu-id="e81c5-456">Le contenu spécifié ({0}) n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="e81c5-456">The specified content ({0}) does not exist.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-457">{0} = ID ou URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="e81c5-457">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-458">AF20051</span><span class="sxs-lookup"><span data-stu-id="e81c5-458">AF20051</span></span>|<span data-ttu-id="e81c5-459">Le contenu demandé avec la touche {0} a déjà expiré.</span><span class="sxs-lookup"><span data-stu-id="e81c5-459">Content requested with the key {0} has already expired.</span></span> <span data-ttu-id="e81c5-460">Le contenu datant de plus de 7 jours ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="e81c5-460">Content older than 7 days cannot be retrieved.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-461">•    {0} = ID ou URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="e81c5-461">•    {0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-462">AF20052</span><span class="sxs-lookup"><span data-stu-id="e81c5-462">AF20052</span></span>|<span data-ttu-id="e81c5-463">L’ID de contenu {0} dans l’URL n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="e81c5-463">Content ID {0} in the URL is invalid.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-464">{0} = ID ou URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="e81c5-464">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-465">AF20053</span><span class="sxs-lookup"><span data-stu-id="e81c5-465">AF20053</span></span>|<span data-ttu-id="e81c5-466">Une seule langue peut être indiquée dans l’en-tête Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="e81c5-466">Only one language may be present in the Accept-Language header.</span></span>|
|<span data-ttu-id="e81c5-467">AF20054</span><span class="sxs-lookup"><span data-stu-id="e81c5-467">AF20054</span></span>|<span data-ttu-id="e81c5-468">Syntaxe non valide dans l’en-tête Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="e81c5-468">Invalid syntax in Accept-Language header.</span></span>|
|<span data-ttu-id="e81c5-469">AF429</span><span class="sxs-lookup"><span data-stu-id="e81c5-469">AF429</span></span>|<span data-ttu-id="e81c5-470">Trop de demandes.</span><span class="sxs-lookup"><span data-stu-id="e81c5-470">Too many requests.</span></span> <span data-ttu-id="e81c5-471">Method={0}, PublisherId={1}</span><span class="sxs-lookup"><span data-stu-id="e81c5-471">Method={0}, PublisherId={1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="e81c5-472">{0} = méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="e81c5-472">{0} = HTTP Method</span></span></p></li><li><p><span data-ttu-id="e81c5-473">{1} = GUID de locataire utilisé en tant que PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="e81c5-473">{1} = Tenant GUID used as PublisherIdentifier</span></span></p></li></ul>|
|<span data-ttu-id="e81c5-474">AF50000</span><span class="sxs-lookup"><span data-stu-id="e81c5-474">AF50000</span></span>|<span data-ttu-id="e81c5-475">Une erreur interne s’est produite.</span><span class="sxs-lookup"><span data-stu-id="e81c5-475">An internal error occurred.</span></span> <span data-ttu-id="e81c5-476">Retentez la requête.</span><span class="sxs-lookup"><span data-stu-id="e81c5-476">Retry the request.</span></span>|
