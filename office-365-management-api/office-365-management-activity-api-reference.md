---
ms.TocTitle: Office 365 Management Activity API reference
title: Référence de l’API Activité de gestion Office 365
description: Cet article explique comment utiliser l’API Activité de gestion Office 365 pour récupérer des informations sur les actions et les événements des utilisateurs, des administrateurs, du système et des stratégies à partir des journaux d’activité Office 365 et Azure AD.
ms.ContentId: 52749845-37f8-6076-7ea5-49d9a4055445
ms.topic: reference (API)
ms.date: 01/10/2018
localization_priority: Priority
ms.openlocfilehash: e6675628a384ab4b2dac3342875332b50586526f
ms.sourcegitcommit: 5b1eaeb7f262b7b9f7ab30ccb9f10878814153ac
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "32223979"
---
# <a name="office-365-management-activity-api-reference"></a><span data-ttu-id="a2c91-103">Référence de l’API Activité de gestion Office 365</span><span class="sxs-lookup"><span data-stu-id="a2c91-103">Office 365 Management Activity API reference</span></span>

<span data-ttu-id="a2c91-104">Cet article explique comment utiliser l’API Activité de gestion Office 365 pour récupérer des informations sur les actions et les événements des utilisateurs, des administrateurs, du système et des stratégies à partir des journaux d’activité Office 365 et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2c91-104">Use the Office 365 Management Activity API to retrieve information about user, admin, system, and policy actions and events from Office 365 and Azure AD activity logs.</span></span> 

<span data-ttu-id="a2c91-105">Vous pouvez utiliser les actions et les événements à partir des journaux d’audit et d’activité Office 365 et Microsoft Azure Active Directory pour créer des solutions de supervision, d’analyse et de visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="a2c91-105">You can use the actions and events from the Office 365 and Microsoft Azure Active Directory audit and activity logs to create solutions that provide monitoring, analysis, and data visualization.</span></span> <span data-ttu-id="a2c91-106">Ces solutions offrent aux organisations une meilleure visibilité sur les actions effectuées sur leur contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-106">These solutions give organizations greater visibility into actions taken on their content.</span></span> <span data-ttu-id="a2c91-107">Ces actions et ces événements sont également disponibles dans les rapports d’activité Office 365.</span><span class="sxs-lookup"><span data-stu-id="a2c91-107">These actions and events are also available in the Office 365 Activity Reports.</span></span> <span data-ttu-id="a2c91-108">Pour en savoir plus, reportez-vous à l’article [Effectuer des recherches dans le journal d’audit dans le Centre de sécurité et de conformité Office 365](https://support.office.com/fr-FR/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span><span class="sxs-lookup"><span data-stu-id="a2c91-108">For more information, see [Search the audit log in the Office 365 Security & Compliance Center](https://support.office.com/fr-FR/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c).</span></span>

<span data-ttu-id="a2c91-109">L’API Activité de gestion Office 365 est un service web REST qui vous permet de développer des solutions à l’aide de n’importe quel langage et environnement d’hébergement qui prend en charge les certificats X.509 et HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a2c91-109">The Office 365 Management Activity API is a REST web service that you can use to develop solutions using any language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="a2c91-110">L’API s’appuie sur Azure AD et le protocole OAuth2 pour l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="a2c91-110">The API relies on Azure AD and the OAuth2 protocol for authentication and authorization.</span></span> <span data-ttu-id="a2c91-111">Pour accéder à l’API depuis votre application, inscrivez-la d’abord dans Azure AD et configurez-la avec les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="a2c91-111">To access the API from your application, you'll need to first register it in Azure AD and configure it with appropriate permissions.</span></span> <span data-ttu-id="a2c91-112">Ainsi, votre application pourra demander les jetons d’accès OAuth2 dont elle a besoin pour appeler l’API.</span><span class="sxs-lookup"><span data-stu-id="a2c91-112">This will enable your application to request the OAuth2 access tokens it needs to call the API.</span></span> <span data-ttu-id="a2c91-113">Pour en savoir plus, consultez l’article relatif à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="a2c91-113">For more information, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="a2c91-114">Pour obtenir des informations sur le schéma de données renvoyé par l’API Activité de gestion Office 365 ainsi que sur les problèmes connus et les modifications à venir risquant d’affecter votre implémentation, consultez l’article relatif au [schéma de l’API Activité de gestion Office 365](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a2c91-114">For information about the schema of the data that the Office 365 Management Activity API returns, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>


## <a name="working-with-the-office-365-management-activity-api"></a><span data-ttu-id="a2c91-115">Utilisation de l’API Activité de gestion Office 365</span><span class="sxs-lookup"><span data-stu-id="a2c91-115">Working with the Office 365 Management Activity API</span></span>

<span data-ttu-id="a2c91-116">L’API Activité de gestion Office 365 agrège des actions et des événements dans des blobs de contenu propres au locataire, classés selon le type et la source du contenu qu’ils contiennent.</span><span class="sxs-lookup"><span data-stu-id="a2c91-116">The Office 365 Management Activity API aggregates actions and events into tenant-specific content blobs, which are classified by the type and source of the content they contain.</span></span> <span data-ttu-id="a2c91-117">Actuellement, les types de contenu suivants sont pris en charge :</span><span class="sxs-lookup"><span data-stu-id="a2c91-117">Currently, these content types are supported:</span></span>

- <span data-ttu-id="a2c91-118">Audit.AzureActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="a2c91-118">Audit.AzureActiveDirectory</span></span>
    
- <span data-ttu-id="a2c91-119">Audit.Exchange</span><span class="sxs-lookup"><span data-stu-id="a2c91-119">Audit.Exchange</span></span>
    
- <span data-ttu-id="a2c91-120">Audit.SharePoint</span><span class="sxs-lookup"><span data-stu-id="a2c91-120">Audit.SharePoint</span></span>
    
- <span data-ttu-id="a2c91-121">Audit.General (comprend toutes les autres charges de travail non incluses dans les types de contenu précédents)</span><span class="sxs-lookup"><span data-stu-id="a2c91-121">Audit.General (includes all other workloads not included in the previous content types)</span></span>

- <span data-ttu-id="a2c91-122">DLP.All (événements DLP liés à toutes les charges de travail)</span><span class="sxs-lookup"><span data-stu-id="a2c91-122">DLP.All (DLP events only for all workloads)</span></span>
    
<span data-ttu-id="a2c91-123">Pour en savoir plus sur les événements et les propriétés associés à ces types de contenu, consultez l’article relatif au [schéma de l’API Activité de gestion Office 365](office-365-management-activity-api-schema.md).</span><span class="sxs-lookup"><span data-stu-id="a2c91-123">For details about the events and properties associated with these content types, see [Office 365 Management Activity API schema](office-365-management-activity-api-schema.md).</span></span>

<span data-ttu-id="a2c91-124">Pour commencer à récupérer des blobs de contenu associés à un locataire, créez d’abord un abonnement aux types de contenu souhaités.</span><span class="sxs-lookup"><span data-stu-id="a2c91-124">To begin retrieving content blobs for a tenant, you first a create subscription to the desired content types.</span></span> <span data-ttu-id="a2c91-125">Si vous récupérez des blobs de contenu associés à plusieurs locataires, créez un abonnement à chacun des types de contenu souhaités pour chaque client.</span><span class="sxs-lookup"><span data-stu-id="a2c91-125">If you are retrieving content blobs for multiple tenants, you create multiple subscriptions to each of the desired content types, one for each tenant.</span></span>

<span data-ttu-id="a2c91-126">Une fois qu’un abonnement est créé, vous pouvez régulièrement l’interroger pour découvrir les nouveaux blobs de contenu disponibles au téléchargement. Sinon, vous pouvez inscrire un point de terminaison de webhook avec l’abonnement, auquel nous enverrons des notifications dès que de nouveaux blobs de contenu sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="a2c91-126">After you create a subscription, you can poll regularly to discover new content blobs that are available for download, or you can register a webhook endpoint with the subscription and we will send notifications to this endpoint as new content blobs are available.</span></span>


> [!NOTE] 
> <span data-ttu-id="a2c91-127">Quand un abonnement est créé, il faut attendre jusqu’à 12 heures avant que les premiers blobs de contenu associés à cet abonnement deviennent disponibles.</span><span class="sxs-lookup"><span data-stu-id="a2c91-127">When a subscription is created, it can take up to 12 hours for the first content blobs to become available for that subscription.</span></span> <span data-ttu-id="a2c91-128">Les blobs de contenu sont créés en collectant et en agrégeant des actions et des événements sur plusieurs serveurs et centres de données.</span><span class="sxs-lookup"><span data-stu-id="a2c91-128">The content blobs are created by collecting and aggregating actions and events across multiple servers and datacenters.</span></span> <span data-ttu-id="a2c91-129">À la suite de ce processus distribué, les actions et les événements contenus dans les blobs de contenu n’apparaissent pas nécessairement dans l’ordre dans lequel ils ont eu lieu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-129">As a result of this distributed process, the actions and events contained in the content blobs will not necessarily appear in the order in which they occurred.</span></span> <span data-ttu-id="a2c91-130">Un blob de contenu peut contenir des actions et des événements qui ont eu lieu avant les actions et les événements contenus dans un blob de contenu antérieur.</span><span class="sxs-lookup"><span data-stu-id="a2c91-130">One content blob can contain actions and events that occurred prior to the actions and events contained in an earlier content blob.</span></span> <span data-ttu-id="a2c91-131">Nous mettons tout en œuvre pour réduire la latence entre l’occurrence des actions et des événements et leur disponibilité au sein d’un blob de contenu, mais nous ne pouvons pas garantir qu’elles apparaissent de manière séquentielle.</span><span class="sxs-lookup"><span data-stu-id="a2c91-131">We are working to decrease the latency between the occurrence of actions and events and their availability within a content blob, but we can't guarantee that they appear sequentially.</span></span>


> [!NOTE] 
> <span data-ttu-id="a2c91-132">Les données sensibles régies par les stratégies de protection contre la perte de données (DLP) sont disponibles dans l’API Flux d’activités uniquement pour les utilisateurs auxquels les autorisations « Lire les données sensibles DLP » ont été accordées.</span><span class="sxs-lookup"><span data-stu-id="a2c91-132">DLP sensitive data is only available in the activity feed API to users that have been granted “Read DLP sensitive data” permissions.</span></span> <span data-ttu-id="a2c91-133">Pour en savoir plus, reportez-vous à l’article [Vue d’ensemble des stratégies de protection contre la perte de données](https://support.office.com/fr-FR/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e).</span><span class="sxs-lookup"><span data-stu-id="a2c91-133">For more on Data Loss Prevention (DLP) see [Overview of Data Loss Prevention Policies](https://support.office.com/fr-FR/article/Overview-of-data-loss-prevention-policies-1966b2a7-d1e2-4d92-ab61-42efbb137f5e)</span></span>

## <a name="activity-api-operations"></a><span data-ttu-id="a2c91-134">Opérations de l’API Activité</span><span class="sxs-lookup"><span data-stu-id="a2c91-134">Activity API operations</span></span>

<span data-ttu-id="a2c91-135">Toutes les opérations de l’API sont limitées à un seul locataire et l’URL racine de l’API inclut un ID de locataire qui spécifie le contexte du locataire.</span><span class="sxs-lookup"><span data-stu-id="a2c91-135">All API operations are scoped to a single tenant and the root URL of the API includes a tenant ID that specifies the tenant context.</span></span> <span data-ttu-id="a2c91-136">L’ID de locataire est un GUID.</span><span class="sxs-lookup"><span data-stu-id="a2c91-136">The tenant ID is a GUID.</span></span> <span data-ttu-id="a2c91-137">Pour savoir comment obtenir le GUID, consultez l’article relatif à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="a2c91-137">For information about how to get the GUID, see [Get started with Office 365 Management APIs](get-started-with-office-365-management-apis.md).</span></span>


```http
https://manage.office.com/api/v1.0/{tenant_id}/activity/feed/{operation}
```

<span data-ttu-id="a2c91-138">Étant donné que les notifications que nous envoyons à votre webhook incluent l’**ID de locataire**, vous pouvez utiliser le même webhook pour recevoir des notifications pour tous les locataires.</span><span class="sxs-lookup"><span data-stu-id="a2c91-138">Because the notifications we send to your webhook include the **tenant ID**, you can use the same webhook to receive notifications for all tenants.</span></span>

<span data-ttu-id="a2c91-139">Toutes les opérations de l’API nécessitent un en-tête HTTP d’autorisation avec un jeton d’accès provenant d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2c91-139">All API operations require an Authorization HTTP header with an access token obtained from Azure AD.</span></span> <span data-ttu-id="a2c91-140">L’ID de locataire présent dans le jeton d’accès doit correspondre à l’ID de locataire indiqué dans l’URL racine de l’API. De plus, le jeton d’accès doit contenir la revendication ActivityFeed.Read (qui correspond à l’autorisation [Lire les données d’activité d’une organisation] configurée pour votre application dans Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2c91-140">The tenant ID in the access token must match the tenant ID in the root URL of the API and the access token must contain the ActivityFeed.Read claim (this corresponds to the permission [Read activity data for an organization] that you configured for you application in Azure AD).</span></span>

```json
Authorization: Bearer eyJ0e...Qa6wg
```

<span data-ttu-id="a2c91-141">L’API Activité prend en charge les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2c91-141">The Activity API supports the following operations:</span></span>

- <span data-ttu-id="a2c91-142">**Démarrer un abonnement** pour commencer à recevoir des notifications et récupérer les données d’activité d’un locataire.</span><span class="sxs-lookup"><span data-stu-id="a2c91-142">**Start a subscription** to begin receiving notifications and retrieving activity data for a tenant.</span></span>
    
- <span data-ttu-id="a2c91-143">**Arrêter un abonnement** pour ne plus récupérer les données d’un locataire.</span><span class="sxs-lookup"><span data-stu-id="a2c91-143">**Stop a subscription** to discontinue retrieving data for a tenant.</span></span>
    
- <span data-ttu-id="a2c91-144">**Répertorier les abonnements actifs**</span><span class="sxs-lookup"><span data-stu-id="a2c91-144">**List current subscriptions**</span></span>
    
- <span data-ttu-id="a2c91-145">**Répertorier le contenu disponible** et les URL de contenu correspondantes.</span><span class="sxs-lookup"><span data-stu-id="a2c91-145">**List available content** and the corresponding content URLs.</span></span>
    
- <span data-ttu-id="a2c91-146">**Recevoir des notifications** envoyées par un webhook dès que du nouveau contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-146">**Receiving notifications** sent by a webhook when new content is available.</span></span>
    
- <span data-ttu-id="a2c91-147">**Récupérer du contenu** à l’aide de l’URL de contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-147">**Retrieving content** by using the content URL.</span></span>
    
- <span data-ttu-id="a2c91-148">**Répertorier les notifications** envoyées par un webhook.</span><span class="sxs-lookup"><span data-stu-id="a2c91-148">**List notifications** sent by a webhook.</span></span>

- <span data-ttu-id="a2c91-149">**Récupérer les noms conviviaux des ressources** pour les objets du flux de données identifiés par un GUID.</span><span class="sxs-lookup"><span data-stu-id="a2c91-149">**Retrieve resource friendly names** for objects in the data feed identified by guids.</span></span>
    

## <a name="start-a-subscription"></a><span data-ttu-id="a2c91-150">Démarrer un abonnement</span><span class="sxs-lookup"><span data-stu-id="a2c91-150">Start a subscription</span></span>

<span data-ttu-id="a2c91-151">Cette opération démarre l’abonnement souscrit pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-151">This operation starts a subscription to the specified content type.</span></span> <span data-ttu-id="a2c91-152">Si un abonnement pour le type de contenu spécifié existe déjà, cette opération sert à :</span><span class="sxs-lookup"><span data-stu-id="a2c91-152">If a subscription to the specified content type already exists, this operation is used to:</span></span>

- <span data-ttu-id="a2c91-153">mettre à jour les propriétés d’un webhook actif.</span><span class="sxs-lookup"><span data-stu-id="a2c91-153">Update the properties of an active webhook.</span></span>
    
- <span data-ttu-id="a2c91-154">activer un webhook qui a été désactivé en raison du nombre excessif de notifications d’échec envoyées.</span><span class="sxs-lookup"><span data-stu-id="a2c91-154">Enable a webhook that was disabled because of excessive failed notifications.</span></span>
    
- <span data-ttu-id="a2c91-155">réactiver un webhook expiré en spécifiant une date d’expiration Null ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a2c91-155">Re-enable an expired webhook by specifying a later or null expiration date.</span></span>
    
- <span data-ttu-id="a2c91-156">supprimer un webhook.</span><span class="sxs-lookup"><span data-stu-id="a2c91-156">Remove a webhook.</span></span>
    
||<span data-ttu-id="a2c91-157">Abonnement</span><span class="sxs-lookup"><span data-stu-id="a2c91-157">Subscription</span></span>|<span data-ttu-id="a2c91-158">Description</span><span class="sxs-lookup"><span data-stu-id="a2c91-158">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a2c91-159">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="a2c91-159">**Path**</span></span>| `/subscriptions/start?contentType={ContentType}`||
|<span data-ttu-id="a2c91-160">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="a2c91-160">**Parameters**</span></span>|<span data-ttu-id="a2c91-161">contentType</span><span class="sxs-lookup"><span data-stu-id="a2c91-161">contentType</span></span>|<span data-ttu-id="a2c91-162">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="a2c91-162">Must be a valid content type.</span></span>|
||<span data-ttu-id="a2c91-163">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="a2c91-163">PublisherIdentifier</span></span>|<span data-ttu-id="a2c91-164">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="a2c91-164">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="a2c91-165">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="a2c91-165">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="a2c91-166">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="a2c91-166">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="a2c91-167">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-167">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="a2c91-168">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="a2c91-168">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="a2c91-169">**Corps**</span><span class="sxs-lookup"><span data-stu-id="a2c91-169">**Body**</span></span>|<span data-ttu-id="a2c91-170">webhook</span><span class="sxs-lookup"><span data-stu-id="a2c91-170">webhook</span></span>|<span data-ttu-id="a2c91-171">Cet objet JSON facultatif comprend trois propriétés :</span><span class="sxs-lookup"><span data-stu-id="a2c91-171">Optional JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-172"><b>address</b> : point de terminaison HTTPS obligatoire qui peut recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="a2c91-172"><b>address</b>: Required HTTPS endpoint that can receive notifications.</span></span>  <span data-ttu-id="a2c91-173">Un message test est envoyé au webhook pour valider le webhook avant de créer l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2c91-173">A test message will be sent to the webhook to validate the webhook before creating the subscription.</span></span></p></li><li><p><span data-ttu-id="a2c91-174"><b>authId</b> : chaîne facultative incluse comme en-tête WebHook-AuthID dans les notifications envoyées au webhook pour identifier et autoriser la source de la requête envoyée au webhook.</span><span class="sxs-lookup"><span data-stu-id="a2c91-174"><b>authId</b>: Optional string that will be included as the WebHook-AuthID header in notifications sent to the webhook as a means of identifying and authorizing the source of the request to the webhook.</span></span></p></li><li><p><span data-ttu-id="a2c91-175"><b>expiration</b> : date/heure (valeur facultative) après laquelle les notifications ne doivent plus être envoyées au webhook.</span><span class="sxs-lookup"><span data-stu-id="a2c91-175"><b>expiration</b>: Optional datetime that indicates a datetime after which notifications should no longer be sent to the webhook.</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-176">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="a2c91-176">**Response**</span></span>|<span data-ttu-id="a2c91-177">contentType</span><span class="sxs-lookup"><span data-stu-id="a2c91-177">contentType</span></span>|<span data-ttu-id="a2c91-178">Type de contenu spécifié dans l’appel.</span><span class="sxs-lookup"><span data-stu-id="a2c91-178">The content type specified in the call.</span></span>|
||<span data-ttu-id="a2c91-179">statut</span><span class="sxs-lookup"><span data-stu-id="a2c91-179">status</span></span>|<span data-ttu-id="a2c91-180">Statut de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2c91-180">The status of the subscription.</span></span> <span data-ttu-id="a2c91-181">Si un abonnement est désactivé, vous ne pouvez pas répertorier ou récupérer du contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-181">If a subscription is disabled, you will not be able to list or retrieve content.</span></span>|
||<span data-ttu-id="a2c91-182">webhook</span><span class="sxs-lookup"><span data-stu-id="a2c91-182">webhook</span></span>|<span data-ttu-id="a2c91-183">Propriétés du webhook spécifiées dans l’appel avec l’état du webhook.</span><span class="sxs-lookup"><span data-stu-id="a2c91-183">The webhook properties specified in the call together with the status of the webhook.</span></span> <span data-ttu-id="a2c91-184">Si le webhook est désactivé, vous ne recevez pas de notification, mais vous pouvez toujours répertorier et récupérer du contenu, à condition que l’abonnement soit activé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-184">If the webhook is disabled, you will not receive notification, but you will still be able to list and retrieve content, provided the subscription is enabled.</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="a2c91-185">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a2c91-185">Sample request</span></span>

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


#### <a name="sample-response"></a><span data-ttu-id="a2c91-186">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a2c91-186">Sample response</span></span>

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


## <a name="webhook-validation"></a><span data-ttu-id="a2c91-187">Validation du webhook</span><span class="sxs-lookup"><span data-stu-id="a2c91-187">Webhook validation</span></span>

<span data-ttu-id="a2c91-188">Quand l’opération /start est appelée et un webhook est spécifié, nous vous envoyons une notification de validation à l’adresse de webhook indiquée pour confirmer qu’un détecteur actif peut accepter et traiter les notifications.</span><span class="sxs-lookup"><span data-stu-id="a2c91-188">When the /start operation is called and a webhook is specified, we will send a validation notification to the specified webhook address to validate that an active listener can accept and process notifications.</span></span> <span data-ttu-id="a2c91-189">Si nous ne recevons pas une réponse HTTP 200 OK, l’abonnement n’est pas créé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-189">If we do not receive an HTTP 200 OK response, the subscription will not be created.</span></span> <span data-ttu-id="a2c91-190">Sinon, si l’opération /start est appelée pour ajouter un webhook à un abonnement existant et si nous ne recevons pas une réponse HTTP 200 OK, le webhook n’est pas ajouté et l’abonnement reste inchangé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-190">Or, if /start is being called to add a webhook to an existing subscription and a response of HTTP 200 OK is not received, the webhook will not be added and the subscription will remain unchanged.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="a2c91-191">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a2c91-191">Sample request</span></span>

```json
POST {webhook address}
Content-Type: application/json; charset=utf-8
Webhook-AuthID: (webhook authId) if provided)
Webhook-ValidationCode: (random opaque string)

{
    "validationCode": (random opaque string, same as header)
}

```


#### <a name="sample-response"></a><span data-ttu-id="a2c91-192">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a2c91-192">Sample response</span></span>

```json

HTTP/1.1 200 OK

```


## <a name="stop-a-subscription"></a><span data-ttu-id="a2c91-193">Arrêter un abonnement</span><span class="sxs-lookup"><span data-stu-id="a2c91-193">Stop a subscription</span></span>

<span data-ttu-id="a2c91-194">Cette opération arrête un abonnement souscrit pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-194">This operation stops a subscription to the specified content type.</span></span> 

<span data-ttu-id="a2c91-195">Quand un abonnement est arrêté, vous ne recevez plus de notifications et vous ne pouvez pas récupérer le contenu disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-195">When a subscription is stopped, you will no longer receive notifications and you will not be able to retrieve available content.</span></span> <span data-ttu-id="a2c91-196">Si, plus tard, vous décidez de redémarrer l’abonnement, vous aurez accès au nouveau contenu disponible à partir de ce moment-là.</span><span class="sxs-lookup"><span data-stu-id="a2c91-196">If the subscription is later restarted, you will have access to new content from that point forward.</span></span> <span data-ttu-id="a2c91-197">Vous ne pourrez pas récupérer le contenu mis à disposition pendant la période où l’abonnement était arrêté.</span><span class="sxs-lookup"><span data-stu-id="a2c91-197">You will not be able to retrieve content that was available between the time the subscription was stopped and restarted.</span></span>


||<span data-ttu-id="a2c91-198">Abonnement</span><span class="sxs-lookup"><span data-stu-id="a2c91-198">Subscription</span></span>|<span data-ttu-id="a2c91-199">Description</span><span class="sxs-lookup"><span data-stu-id="a2c91-199">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a2c91-200">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="a2c91-200">**Path**</span></span>| `/subscriptions/stop?contentType={ContentType}`||
|<span data-ttu-id="a2c91-201">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="a2c91-201">**Parameters**</span></span>|<span data-ttu-id="a2c91-202">contentType</span><span class="sxs-lookup"><span data-stu-id="a2c91-202">contentType</span></span>|<span data-ttu-id="a2c91-203">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="a2c91-203">Must be a valid content type.</span></span>|
||<span data-ttu-id="a2c91-204">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="a2c91-204">PublisherIdentifier</span></span>|<span data-ttu-id="a2c91-205">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="a2c91-205">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="a2c91-206">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="a2c91-206">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="a2c91-207">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="a2c91-207">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="a2c91-208">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-208">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="a2c91-209">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="a2c91-209">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="a2c91-210">**Corps**</span><span class="sxs-lookup"><span data-stu-id="a2c91-210">**Body**</span></span>|<span data-ttu-id="a2c91-211">(vide)</span><span class="sxs-lookup"><span data-stu-id="a2c91-211">(empty)</span></span>||
|<span data-ttu-id="a2c91-212">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="a2c91-212">**Response**</span></span>|<span data-ttu-id="a2c91-213">(vide)</span><span class="sxs-lookup"><span data-stu-id="a2c91-213">(empty)</span></span>|||

#### <a name="sample-request"></a><span data-ttu-id="a2c91-214">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a2c91-214">Sample request</span></span>

```json
POST {root}/subscriptions/stop?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="a2c91-215">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a2c91-215">Sample response</span></span>

```json
HTTP/1.1 200 OK
```


## <a name="list-current-subscriptions"></a><span data-ttu-id="a2c91-216">Répertorier les abonnements actifs</span><span class="sxs-lookup"><span data-stu-id="a2c91-216">List current subscriptions</span></span>

<span data-ttu-id="a2c91-217">Cette opération renvoie une collection d’abonnements actifs avec les webhooks associés.</span><span class="sxs-lookup"><span data-stu-id="a2c91-217">This operation returns a collection of the current subscriptions together with the associated webhooks.</span></span>

||<span data-ttu-id="a2c91-218">Abonnement</span><span class="sxs-lookup"><span data-stu-id="a2c91-218">Subscription</span></span>|<span data-ttu-id="a2c91-219">Description</span><span class="sxs-lookup"><span data-stu-id="a2c91-219">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a2c91-220">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="a2c91-220">**Path**</span></span>| `/subscriptions/list`||
|<span data-ttu-id="a2c91-221">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="a2c91-221">**Parameters**</span></span>|<span data-ttu-id="a2c91-222">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="a2c91-222">PublisherIdentifier</span></span>|<span data-ttu-id="a2c91-223">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="a2c91-223">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="a2c91-224">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="a2c91-224">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="a2c91-225">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="a2c91-225">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="a2c91-226">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-226">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="a2c91-227">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="a2c91-227">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="a2c91-228">**Corps**</span><span class="sxs-lookup"><span data-stu-id="a2c91-228">**Body**</span></span>|<span data-ttu-id="a2c91-229">(vide)</span><span class="sxs-lookup"><span data-stu-id="a2c91-229">(empty)</span></span>||
|<span data-ttu-id="a2c91-230">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="a2c91-230">**Response**</span></span>|<span data-ttu-id="a2c91-231">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="a2c91-231">JSON array</span></span>|<span data-ttu-id="a2c91-232">Chaque abonnement est représenté par un objet JSON comprenant trois propriétés :</span><span class="sxs-lookup"><span data-stu-id="a2c91-232">Each subscription will be represented by a JSON object with three properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-233"><b>contentType</b> : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-233"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="a2c91-234"><b>status</b> : indique le statut de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2c91-234"><b>status</b>: Indicates the status of the subscription.</span></span></p></li><li><p><span data-ttu-id="a2c91-235"><b>webhook</b> : indique le webhook configuré avec l’état (activé, désactivé, expiré) du webhook.</span><span class="sxs-lookup"><span data-stu-id="a2c91-235"><b>webhook</b>: Indicates the configured webhook, together with the status (enabled, disabled, expired) of the webhook.</span></span>  <span data-ttu-id="a2c91-236">Si un abonnement n’a pas de webhook, la propriété du webhook est indiquée avec une valeur Null.</span><span class="sxs-lookup"><span data-stu-id="a2c91-236">If a subscription does not have a webhook, the webhook property will be present but with null value.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="a2c91-237">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a2c91-237">Sample request</span></span>

```json
GET {root}/subscriptions/list?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="a2c91-238">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a2c91-238">Sample response</span></span>

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


## <a name="list-available-content"></a><span data-ttu-id="a2c91-239">Répertorier le contenu disponible</span><span class="sxs-lookup"><span data-stu-id="a2c91-239">List available content</span></span>

<span data-ttu-id="a2c91-240">Cette opération répertorie le contenu actuellement disponible que vous pouvez récupérer pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-240">This operation lists the content currently available for retrieval for the specified content type.</span></span> <span data-ttu-id="a2c91-241">Le contenu est une agrégation des actions et des événements collectés sur plusieurs serveurs de plusieurs centres de données.</span><span class="sxs-lookup"><span data-stu-id="a2c91-241">The content is an aggregation of actions and events harvested from multiple servers across multiple datacenters.</span></span> <span data-ttu-id="a2c91-242">Le contenu est répertorié dans l’ordre de mise à disposition des agrégations. En revanche, nous ne pouvons pas garantir que les événements et les actions des agrégations sont répertoriés de manière séquentielle.</span><span class="sxs-lookup"><span data-stu-id="a2c91-242">The content will be listed in the order in which the aggregations become available, but the events and actions within the aggregations are not guaranteed to be sequential.</span></span> <span data-ttu-id="a2c91-243">Une erreur est renvoyée si l’état de l’abonnement est désactivé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-243">An error is returned if the subscription status is disabled.</span></span>


||<span data-ttu-id="a2c91-244">Abonnement</span><span class="sxs-lookup"><span data-stu-id="a2c91-244">Subscription</span></span>|<span data-ttu-id="a2c91-245">Description</span><span class="sxs-lookup"><span data-stu-id="a2c91-245">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a2c91-246">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="a2c91-246">**Path**</span></span>| `/subscriptions/content?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="a2c91-247">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="a2c91-247">**Parameters**</span></span>|<span data-ttu-id="a2c91-248">contentType</span><span class="sxs-lookup"><span data-stu-id="a2c91-248">contentType</span></span>|<span data-ttu-id="a2c91-249">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="a2c91-249">Must be a valid content type.</span></span>|
||<span data-ttu-id="a2c91-250">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="a2c91-250">PublisherIdentifier</span></span>|<span data-ttu-id="a2c91-251">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="a2c91-251">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="a2c91-252">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="a2c91-252">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="a2c91-253">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="a2c91-253">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="a2c91-254">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-254">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="a2c91-255">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="a2c91-255">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="a2c91-256">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="a2c91-256">startTime endTime</span></span>|<span data-ttu-id="a2c91-257">Date/Heure (UTC) facultative indiquant l’intervalle de temps à prendre en compte pour renvoyer le contenu, selon le moment à partir duquel le contenu est devenu disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-257">Optional datetimes (UTC) indicating the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="a2c91-258">L’intervalle de temps est compris entre l’heure de début (startTime <= contentCreated) et l’heure de fin (contentCreated < endTime). Ainsi, les intervalles de temps sont incrémentés sans se chevaucher pour permettre de parcourir le contenu disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-258">The time range is inclusive with respect to startTime (startTime <= contentCreated) and exclusive with respect to endTime (contentCreated < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-259">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="a2c91-259">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="a2c91-260">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="a2c91-260">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="a2c91-261">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="a2c91-261">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="a2c91-262">L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="a2c91-262">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="a2c91-263">Par défaut, si l’heure de début et l’heure de fin ne sont pas renseignées, le contenu disponible au cours des dernières 24 heures est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-263">By default, if startTime and endTime are omitted, then the content available in the last 24 hours is returned.</span></span><p><span data-ttu-id="a2c91-264">**REMARQUE** : même si l’heure de début et l’heure de fin peuvent être espacées de plus de 24 heures, nous vous déconseillons de le faire.</span><span class="sxs-lookup"><span data-stu-id="a2c91-264">**NOTE**: Even though it is possible to specify a startTime and endTime more than 24 hours apart, this is not recommended.</span></span> <span data-ttu-id="a2c91-265">Par ailleurs, si vous obtenez des résultats en réponse à une requête portant sur un intervalle de plus de 24 heures, ces résultats peuvent être partiels et ne doivent pas être pris en compte.</span><span class="sxs-lookup"><span data-stu-id="a2c91-265">Furthermore, if you do get any results in response to a request for more than 24 hours, these could be partial results and should not be taken into account.</span></span> <span data-ttu-id="a2c91-266">L’intervalle de la requête émise entre l’heure de début et l’heure de fin doit couvrir une plage horaire de moins de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="a2c91-266">The request should be issued with an interval of no more than 24 hours between the startTime and endTime.</span></span></p>|
|<span data-ttu-id="a2c91-267">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="a2c91-267">**Response**</span></span>|<span data-ttu-id="a2c91-268">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="a2c91-268">JSON array</span></span>|<span data-ttu-id="a2c91-269">Le contenu disponible est représenté par des objets JSON comprenant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2c91-269">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-270"><b>contentType</b> : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-270"><b>contentType</b>: Indicates the content type.</span></span></p></li><li><p><span data-ttu-id="a2c91-271"><b>contentId</b> : chaîne opaque qui identifie le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-271"><b>contentId</b>: An opaque string that uniquely identifies the content.</span></span></p></li><li><p><span data-ttu-id="a2c91-272"><b>contentUri</b> : URL à utiliser pour récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-272"><b>contentUri</b>: The URL to use when retrieving the content.</span></span></p></li><li><p><span data-ttu-id="a2c91-273"><b>contentCreated</b> : date/heure à laquelle le contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-273"><b>contentCreated</b>: The datetime when the content was made available.</span></span></p></li><li><p><span data-ttu-id="a2c91-274"><b>contentExpiration</b> : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-274"><b>contentExpiration</b>: The datetime after which the content will no longer be available for retrieval.</span></span></p></li></ul>|


#### <a name="sample-request"></a><span data-ttu-id="a2c91-275">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a2c91-275">Sample request</span></span>

```json
GET {root}/subscriptions/content?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="a2c91-276">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a2c91-276">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="a2c91-277">Pagination</span><span class="sxs-lookup"><span data-stu-id="a2c91-277">Pagination</span></span>

<span data-ttu-id="a2c91-278">Quand vous répertoriez le contenu disponible au cours d’un intervalle de temps donné, le nombre de résultats renvoyés est limité pour éviter de dépasser le délai de réponse.</span><span class="sxs-lookup"><span data-stu-id="a2c91-278">When listing available content for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="a2c91-279">Si d’autres résultats correspondent à l’intervalle de temps spécifié mais ne peuvent pas être renvoyés dans une seule réponse, les résultats sont tronqués et un en-tête est ajouté à la réponse indiquant l’URL à utiliser pour accéder à la page de résultats suivante.</span><span class="sxs-lookup"><span data-stu-id="a2c91-279">If there are more results in the specified time range than can be returned in single response, the results will be truncated and a header will be added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="a2c91-280">L’URL contient les mêmes paramètres _startTime_ et _endTime_ qui ont été spécifiés dans la requête d’origine, ainsi qu’un paramètre indiquant l’ID interne de la page suivante.</span><span class="sxs-lookup"><span data-stu-id="a2c91-280">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="a2c91-281">Si les paramètres _startTime_ et _endTime_ ne sont pas spécifiés dans la requête d’origine, ils indiquent l’intervalle de 24 heures qui précède la requête d’origine.</span><span class="sxs-lookup"><span data-stu-id="a2c91-281">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>


```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUri: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="a2c91-282">Pour répertorier tout le contenu disponible dans un intervalle de temps spécifié, vous devrez peut-être récupérer plusieurs pages jusqu’à ce que vous receviez une réponse qui ne contient pas l’en-tête **NextPageUri**.</span><span class="sxs-lookup"><span data-stu-id="a2c91-282">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUri** header is received.</span></span>


## <a name="receiving-notifications"></a><span data-ttu-id="a2c91-283">Réception des notifications</span><span class="sxs-lookup"><span data-stu-id="a2c91-283">Receiving notifications</span></span>

<span data-ttu-id="a2c91-284">Les notifications sont envoyées au webhook configuré pour un abonnement au fur et à mesure que le nouveau contenu devient disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-284">Notifications are sent to the configured webhook for a subscription as new content becomes available.</span></span> <span data-ttu-id="a2c91-285">Étant donné que les notifications incluent l’ID de locataire, vous pouvez utiliser le même webhook pour recevoir des notifications pour tous les locataires auxquels vous êtes abonné.</span><span class="sxs-lookup"><span data-stu-id="a2c91-285">Because the notification includes the tenant identifier, you can use the same webhook to receive notifications for all tenants for which you have subscriptions.</span></span>

<span data-ttu-id="a2c91-286">La notification est envoyée sous la forme d’une requête HTTP POST sur TLS (TLS 1.0 et versions ultérieures) à l’adresse de webhook spécifiée.</span><span class="sxs-lookup"><span data-stu-id="a2c91-286">The notification is made as an HTTP POST over TLS (TLS 1.0 and later versions) to the specified webhook address.</span></span> <span data-ttu-id="a2c91-287">Si la configuration du webhook inclut un ID d’authentification, nous l’envoyons comme en-tête HTTP : Webhook-AuthID.</span><span class="sxs-lookup"><span data-stu-id="a2c91-287">If the webhook configuration includes an auth ID, we will send it as an HTTP header: Webhook-AuthID.</span></span> <span data-ttu-id="a2c91-288">Les réponses qui n’incluent pas HTTP 200 OK seront considérées comme ayant échoué et la notification sera renvoyée.</span><span class="sxs-lookup"><span data-stu-id="a2c91-288">Any response other than HTTP 200 OK will be considered a failure and the notification will be retried.</span></span> <span data-ttu-id="a2c91-289">Vous pouvez également configurer votre webhook pour exiger une authentification basée sur les certificats clients ; nous nous authentifierons alors à l’aide du certificat manage.office.com.</span><span class="sxs-lookup"><span data-stu-id="a2c91-289">You can also configure your webhook to require client certificate-based authentication and we will authenticate using the manage.office.com certificate.</span></span>

<span data-ttu-id="a2c91-290">Le corps de la requête contiendra une matrice comprenant un ou plusieurs objets JSON qui représentent les blobs de contenu disponibles.</span><span class="sxs-lookup"><span data-stu-id="a2c91-290">The body of the request will contain an array of one or more JSON objects that represent the available content blobs.</span></span> <span data-ttu-id="a2c91-291">Le nombre de blobs de contenu compris dans chaque notification est limité pour réduire au maximum la taille de la notification.</span><span class="sxs-lookup"><span data-stu-id="a2c91-291">The number of content blobs in each notification is limited to keep the size of the notification relatively small.</span></span> <span data-ttu-id="a2c91-292">Dans la mesure où cette limite peut être modifiée, votre implémentation doit interroger la longueur de la matrice au lieu de prévoir une taille fixe.</span><span class="sxs-lookup"><span data-stu-id="a2c91-292">Because this limit might change, your implementation should query for the length of the array instead of expecting a fixed size.</span></span> <span data-ttu-id="a2c91-293">Chaque objet inclura les mêmes propriétés renvoyées par l’opération /content ainsi que le GUID du locataire auquel appartiennent les données et le GUID de l’application ayant créé les abonnements.</span><span class="sxs-lookup"><span data-stu-id="a2c91-293">Each object will include the same properties returned by the /content operation, together with the GUID of the tenant to which the data belongs and the GUID of your application that created the subscriptions.</span></span> <span data-ttu-id="a2c91-294">Ainsi, le webhook peut établir le contexte dans lequel il est utilisé avec plusieurs locataires et applications.</span><span class="sxs-lookup"><span data-stu-id="a2c91-294">This allows the webhook to establish context when it is being used with multiple tenants and applications.</span></span>

- <span data-ttu-id="a2c91-295">**tenantId** : GUID du locataire auquel appartient le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-295">**tenantId**: The GUID of the tenant to which the content belongs.</span></span>
    
- <span data-ttu-id="a2c91-296">**clientId** : GUID de votre application qui a créé l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2c91-296">**clientId**: The GUID of your application that created the subscription.</span></span>
    
- <span data-ttu-id="a2c91-297">**contentType** : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-297">**contentType**: Indicates the content type.</span></span>
    
- <span data-ttu-id="a2c91-298">**contentId** : chaîne opaque qui identifie le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-298">**contentId**: An opaque string that uniquely identifies the content.</span></span>
    
- <span data-ttu-id="a2c91-299">**contentUri** : URL à utiliser pour récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-299">**contentUri**: The URL to use when retrieving the content.</span></span>
    
- <span data-ttu-id="a2c91-300">**contentCreated** : date/heure à laquelle le contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-300">**contentCreated**: The datetime when the content was made available.</span></span>
    
- <span data-ttu-id="a2c91-301">**contentExpiration** : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-301">**contentExpiration**: The datetime after which the content will no longer be available for retrieval.</span></span>
    
<span data-ttu-id="a2c91-302">Vous trouverez ci-dessous un exemple de notification.</span><span class="sxs-lookup"><span data-stu-id="a2c91-302">The following is an example of a notification.</span></span>

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


## <a name="notification-failure-and-retry"></a><span data-ttu-id="a2c91-303">Échec de notification et nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="a2c91-303">Notification failure and retry</span></span>

<span data-ttu-id="a2c91-304">Le système de notification envoie des notifications dès que du nouveau contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-304">The notification system sends notifications as new content becomes available.</span></span> <span data-ttu-id="a2c91-305">Si l’envoi des notifications échoue à de multiples reprises, le délai d’attente entre chaque nouvelle tentative augmente.</span><span class="sxs-lookup"><span data-stu-id="a2c91-305">If we encounter excessive failures when sending notifications, our retry mechanism will exponentially increase the time between retries.</span></span> <span data-ttu-id="a2c91-306">Si l’envoi des notifications continue d’échouer, nous nous réservons le droit de désactiver le webhook et d’arrêter de lui envoyer des notifications.</span><span class="sxs-lookup"><span data-stu-id="a2c91-306">If we continue to encounter failures, we reserve the right to disable the webhook and stop sending notifications to it altogether.</span></span> <span data-ttu-id="a2c91-307">L’opération /start peut être utilisée pour réactiver un webhook désactivé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-307">The /start operation can be used to re-enable a disabled webhook.</span></span>


## <a name="retrieving-content"></a><span data-ttu-id="a2c91-308">Récupérer du contenu</span><span class="sxs-lookup"><span data-stu-id="a2c91-308">Retrieving content</span></span>

<span data-ttu-id="a2c91-309">Pour récupérer un blob de contenu, envoyez une requête GET à l’URI de contenu correspondante qui figure dans la liste du contenu disponible et dans les notifications envoyées au webhook.</span><span class="sxs-lookup"><span data-stu-id="a2c91-309">To retrieve a content blob, make a GET request against the corresponding content URI that is included in the list of available content and in the notifications sent to a webhook.</span></span> <span data-ttu-id="a2c91-310">Le contenu renvoyé correspondra à une collection d’un ou de plusieurs événements ou actions au format JSON.</span><span class="sxs-lookup"><span data-stu-id="a2c91-310">The returned content will be a collection of one more actions or events in JSON format.</span></span>

#### <a name="sample-request"></a><span data-ttu-id="a2c91-311">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a2c91-311">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/41463f53-8812-40f4-890f-865bf6e35190/activity/feed/audit/301299007231$301299007231$41463f53881240f4890f865bf6e35190aad2015062920$e1c2ab19858a469fb1f1fd097effffc9$04 HTTP/1.1
Authorization: Bearer eyJ0e...Qa6wg
```

#### <a name="sample-response"></a><span data-ttu-id="a2c91-312">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a2c91-312">Sample response</span></span>

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


## <a name="list-notifications"></a><span data-ttu-id="a2c91-313">Répertorier les notifications</span><span class="sxs-lookup"><span data-stu-id="a2c91-313">List notifications</span></span>

<span data-ttu-id="a2c91-314">Cette opération répertorie toutes les tentatives de notification associées au type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-314">This operation lists all notification attempts for the specified content type.</span></span> <span data-ttu-id="a2c91-315">Si vous n’avez pas inclus un webhook au démarrage de l’abonnement souscrit pour le type de contenu, aucune notification ne pourra être récupérée.</span><span class="sxs-lookup"><span data-stu-id="a2c91-315">If you did not include a webhook when starting the subscription to the content type, there will be no notifications to retrieve.</span></span> <span data-ttu-id="a2c91-316">Dans la mesure où nous renvoyons les notifications en cas d’échec de l’envoi initial, cette opération peut renvoyer plusieurs notifications pour le même contenu. Par ailleurs, l’ordre dans lequel les notifications sont envoyées ne correspond pas nécessairement à l’ordre de parution du contenu (en particulier en cas d’échecs et de nouvelles tentatives).</span><span class="sxs-lookup"><span data-stu-id="a2c91-316">Because we retry notifications in the event of failure, this operation can return multiple notifications for the same content, and the order in which the notifications are sent will not necessarily match the order in which the content became available (especially when there are failures and retries).</span></span> 

<span data-ttu-id="a2c91-317">Vous pouvez utiliser cette opération pour vous aider à résoudre les problèmes liés aux webhooks et aux notifications, mais nous vous déconseillons de l’utiliser pour déterminer le contenu disponible que vous pouvez récupérer.</span><span class="sxs-lookup"><span data-stu-id="a2c91-317">You can use this operation to help investigate issues related to webhooks and notifications, but you should not use it to determine what content is currently available for retrieval.</span></span> <span data-ttu-id="a2c91-318">Pour cela, utilisez plutôt l’opération /content.</span><span class="sxs-lookup"><span data-stu-id="a2c91-318">Use the /content operation instead.</span></span> <span data-ttu-id="a2c91-319">Nous renvoyons une erreur si l’état de l’abonnement est désactivé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-319">We return an error if the subscription status is disabled.</span></span>


||<span data-ttu-id="a2c91-320">Abonnement</span><span class="sxs-lookup"><span data-stu-id="a2c91-320">Subscription</span></span>|<span data-ttu-id="a2c91-321">Description</span><span class="sxs-lookup"><span data-stu-id="a2c91-321">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a2c91-322">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="a2c91-322">**Path**</span></span>| `/subscriptions/notifications?contentType={ContentType}&amp;startTime={0}&amp;endTime={1}`||
|<span data-ttu-id="a2c91-323">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="a2c91-323">**Parameters**</span></span>|<span data-ttu-id="a2c91-324">contentType</span><span class="sxs-lookup"><span data-stu-id="a2c91-324">contentType</span></span>|<span data-ttu-id="a2c91-325">Doit être un type de contenu valide.</span><span class="sxs-lookup"><span data-stu-id="a2c91-325">Must be a valid content type.</span></span>|
||<span data-ttu-id="a2c91-326">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="a2c91-326">PublisherIdentifier</span></span>|<span data-ttu-id="a2c91-327">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="a2c91-327">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="a2c91-328">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="a2c91-328">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="a2c91-329">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="a2c91-329">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="a2c91-330">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-330">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="a2c91-331">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="a2c91-331">All requests received without this parameter will share the same quota.</span></span>|
||<span data-ttu-id="a2c91-332">startTime endTime</span><span class="sxs-lookup"><span data-stu-id="a2c91-332">startTime endTime</span></span>|<span data-ttu-id="a2c91-333">Date/Heure (UTC) facultative indiquant l’intervalle de temps à prendre en compte pour renvoyer le contenu, selon le moment à partir duquel le contenu est devenu disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-333">Optional datetimes (UTC) that indicate the time range of content to return, based on when the content became available.</span></span> <span data-ttu-id="a2c91-334">L’intervalle de temps est délimité par les paramètres _startTime_ (_startTime_ <= contentCreated) et _endTime_ (_contentCreated_ < endTime). Ainsi, les intervalles de temps sont incrémentés sans se chevaucher pour permettre de parcourir le contenu disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-334">The time range is inclusive with respect to  _startTime_ ( _startTime_ <= contentCreated) and exclusive with respect to _endTime_ (_contentCreated_ < endTime), so that non-overlapping, incrementing time intervals can used to page through available content.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-335">YYYY-MM-DD</span><span class="sxs-lookup"><span data-stu-id="a2c91-335">YYYY-MM-DD</span></span></p></li><li><p><span data-ttu-id="a2c91-336">YYYY-MM-DDTHH:MM</span><span class="sxs-lookup"><span data-stu-id="a2c91-336">YYYY-MM-DDTHH:MM</span></span></p></li><li><p><span data-ttu-id="a2c91-337">YYYY-MM-DDTHH:MM:SS</span><span class="sxs-lookup"><span data-stu-id="a2c91-337">YYYY-MM-DDTHH:MM:SS</span></span></p></li></ul><span data-ttu-id="a2c91-338">L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="a2c91-338">Both must be specified (or both omitted) and they must be no more than 24 hours apart, with the start time no more than 7 days in the past.</span></span> <span data-ttu-id="a2c91-339">Par défaut, si les paramètres _startTime_ et _endTime_ ne sont pas renseignés, le contenu disponible au cours des dernières 24 heures est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-339">By default, if  _startTime_ and _endTime_ are omitted, the content available in the last 24 hours is returned.</span></span>|
|<span data-ttu-id="a2c91-340">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="a2c91-340">**Response**</span></span>|<span data-ttu-id="a2c91-341">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="a2c91-341">JSON array</span></span>|<span data-ttu-id="a2c91-342">Les notifications sont représentées par des objets JSON comprenant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2c91-342">The notifications will be represented by JSON objects with the following properties:</span></span> <ul><li><span data-ttu-id="a2c91-343">**contentType** : indique le type de contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-343">**contentType**: indicates the content type.</span></span></li><li><span data-ttu-id="a2c91-344">**contentId** : chaîne opaque qui identifie le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-344">**contentId**: an opaque string that uniquely identifies the content.</span></span></li><li><span data-ttu-id="a2c91-345">**contentUri** : URL à utiliser pour récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-345">**contentUri**: the URL to use when retrieving the content.</span></span> </li><li><span data-ttu-id="a2c91-346">**contentCreated** : date/heure à laquelle le contenu est disponible.</span><span class="sxs-lookup"><span data-stu-id="a2c91-346">**contentCreated**: the datetime when the content was made available.</span></span></li><li><span data-ttu-id="a2c91-347">**contentExpiration** : date/heure après laquelle vous ne pouvez plus récupérer le contenu.</span><span class="sxs-lookup"><span data-stu-id="a2c91-347">**contentExpiration**: the datetime after which the content will no longer be available for retrieval.</span></span></li><li><span data-ttu-id="a2c91-348">**notificationSent** : date/heure d’envoi de la notification.</span><span class="sxs-lookup"><span data-stu-id="a2c91-348">**notificationSent**: the datetime when the notification was sent.</span></span></li><li><span data-ttu-id="a2c91-349">**notificationStatus** : indique la réussite ou l’échec de la tentative de notification.</span><span class="sxs-lookup"><span data-stu-id="a2c91-349">**notificationStatus**: indicates the success or failure of the notification attempt.</span></span></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="a2c91-350">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a2c91-350">Sample request</span></span>

```json
GET {root}/subscriptions/notifications?contentType=Audit.SharePoint&PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg

```

#### <a name="sample-response"></a><span data-ttu-id="a2c91-351">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a2c91-351">Sample response</span></span>

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


### <a name="pagination"></a><span data-ttu-id="a2c91-352">Pagination</span><span class="sxs-lookup"><span data-stu-id="a2c91-352">Pagination</span></span>

<span data-ttu-id="a2c91-353">Quand vous répertoriez l’historique de notification au cours d’un intervalle de temps donné, le nombre de résultats renvoyés est limité pour éviter de dépasser le délai de réponse.</span><span class="sxs-lookup"><span data-stu-id="a2c91-353">When listing notification history for a time range, the number of results returned is limited to prevent response timeouts.</span></span> <span data-ttu-id="a2c91-354">Si d’autres résultats correspondent à l’intervalle de temps spécifié mais ne peuvent pas être renvoyés dans une seule réponse, les résultats sont tronqués et un en-tête est ajouté à la réponse indiquant l’URL à utiliser pour accéder à la page de résultats suivante.</span><span class="sxs-lookup"><span data-stu-id="a2c91-354">If there are more results in the specified time range than can be returned in a single response, the results are truncated and a header is added to the response indicating the URL to use to retrieve the next page of results.</span></span> <span data-ttu-id="a2c91-355">L’URL contient les mêmes paramètres _startTime_ et _endTime_ qui ont été spécifiés dans la requête d’origine, ainsi qu’un paramètre indiquant l’ID interne de la page suivante.</span><span class="sxs-lookup"><span data-stu-id="a2c91-355">The URL will contain the same  _startTime_ and _endTime_ parameters that were specified in the original request, together with a parameter indicating the internal ID of the next page.</span></span> <span data-ttu-id="a2c91-356">Si les paramètres _startTime_ et _endTime_ ne sont pas spécifiés dans la requête d’origine, ils indiquent l’intervalle de 24 heures qui précède la requête d’origine.</span><span class="sxs-lookup"><span data-stu-id="a2c91-356">If _startTime_ and _endTime_ were not specified in the original request, they will be set to reflect the 24-hour interval that preceded the original request.</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
NextPageUrl: https://manage.office.com/api/v1/{tenant_id}/activity/feed/subscriptions/content?contentType=Audit.SharePoint&amp;startTime=2015-10-01&amp;endTime=2015-10-02&amp;nextPage=2015101900R022885001761

```

<span data-ttu-id="a2c91-357">Pour répertorier tout le contenu disponible dans un intervalle de temps spécifié, vous devrez peut-être récupérer plusieurs pages jusqu’à ce que vous receviez une réponse qui ne contient pas l’en-tête **NextPageUrl**.</span><span class="sxs-lookup"><span data-stu-id="a2c91-357">To list all available content for a specified time range, you might need to retrieve multiple pages until a response without the **NextPageUrl** header is received.</span></span>

## <a name="retrieve-resource-friendly-names"></a><span data-ttu-id="a2c91-358">Récupération des noms conviviaux des ressources</span><span class="sxs-lookup"><span data-stu-id="a2c91-358">Retrieve resource friendly names</span></span>

<span data-ttu-id="a2c91-359">Cette opération récupère les noms conviviaux des ressources pour les objets du flux de données identifiés par un GUID.</span><span class="sxs-lookup"><span data-stu-id="a2c91-359">This operation retrieves friendly names for objects in the data feed identified by guids.</span></span> <span data-ttu-id="a2c91-360">« DlpSensitiveType » est actuellement le seul objet pris en charge.</span><span class="sxs-lookup"><span data-stu-id="a2c91-360">Currently "DlpSensitiveType" is the only supported object.</span></span> 


||<span data-ttu-id="a2c91-361">Abonnement</span><span class="sxs-lookup"><span data-stu-id="a2c91-361">Subscription</span></span>|<span data-ttu-id="a2c91-362">Description</span><span class="sxs-lookup"><span data-stu-id="a2c91-362">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a2c91-363">**Chemin**</span><span class="sxs-lookup"><span data-stu-id="a2c91-363">**Path**</span></span>| `/resources/dlpSensitiveTypes`||
|<span data-ttu-id="a2c91-364">**Paramètres**</span><span class="sxs-lookup"><span data-stu-id="a2c91-364">**Parameters**</span></span>|<span data-ttu-id="a2c91-365">PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="a2c91-365">PublisherIdentifier</span></span>|<span data-ttu-id="a2c91-366">GUID de locataire de l’éditeur qui code l’API.</span><span class="sxs-lookup"><span data-stu-id="a2c91-366">The tenant GUID of the vendor coding against the API.</span></span> <span data-ttu-id="a2c91-367">Il ne s’agit **pas** du GUID de l’application ou du GUID du client qui utilise l’application, mais bien du GUID de l’entreprise qui écrit le code.</span><span class="sxs-lookup"><span data-stu-id="a2c91-367">This is **not** the application GUID or the GUID of the customer using the application, but the GUID of the company writing the code.</span></span> <span data-ttu-id="a2c91-368">Ce paramètre permet de limiter le taux de requêtes émises.</span><span class="sxs-lookup"><span data-stu-id="a2c91-368">This parameter is used for throttling the request rate.</span></span> <span data-ttu-id="a2c91-369">Vérifiez que ce paramètre est spécifié dans toutes les requêtes émises pour obtenir un quota dédié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-369">Make sure this parameter is specified in all issued requests to get a dedicated quota.</span></span> <span data-ttu-id="a2c91-370">Toutes les requêtes reçues sans ce paramètre auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="a2c91-370">All requests received without this parameter will share the same quota.</span></span>|
|<span data-ttu-id="a2c91-371">**En-têtes**</span><span class="sxs-lookup"><span data-stu-id="a2c91-371">**Headers**</span></span>|<span data-ttu-id="a2c91-372">Accept-Language</span><span class="sxs-lookup"><span data-stu-id="a2c91-372">Accept-Language</span></span>|<span data-ttu-id="a2c91-373">En-tête pour spécifier la langue dans laquelle les noms doivent être localisés.</span><span class="sxs-lookup"><span data-stu-id="a2c91-373">Header to specify the desired language for localized names.</span></span> <span data-ttu-id="a2c91-374">Par exemple, utilisez « en-US » pour l’anglais ou « es » pour l’espagnol.</span><span class="sxs-lookup"><span data-stu-id="a2c91-374">For example, use "en-US" for English or "es" for Spanish.</span></span> <span data-ttu-id="a2c91-375">La langue par défaut (en-US) est renvoyée si cet en-tête n’est pas présent.</span><span class="sxs-lookup"><span data-stu-id="a2c91-375">The default language (en-US) will be returned if this header is not present.</span></span>|
|<span data-ttu-id="a2c91-376">**Corps**</span><span class="sxs-lookup"><span data-stu-id="a2c91-376">**Body**</span></span>|<span data-ttu-id="a2c91-377">(vide)</span><span class="sxs-lookup"><span data-stu-id="a2c91-377">(empty)</span></span>||
|<span data-ttu-id="a2c91-378">**Réponse**</span><span class="sxs-lookup"><span data-stu-id="a2c91-378">**Response**</span></span>|<span data-ttu-id="a2c91-379">Tableau JSON</span><span class="sxs-lookup"><span data-stu-id="a2c91-379">JSON array</span></span>|<span data-ttu-id="a2c91-380">Le contenu disponible est représenté par des objets JSON comprenant les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="a2c91-380">The available content will be represented by JSON objects with the following properties:</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-381"><b>id</b> : indique le GUID du type d’informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="a2c91-381"><b>id</b>: Indicates the guid of the sensitive information type.</span></span></p></li><li><p><span data-ttu-id="a2c91-382"><b>name</b> : nom convivial du type d’informations sensibles.</span><span class="sxs-lookup"><span data-stu-id="a2c91-382"><b>name</b>: The friendly name of the sensitive information type.</span></span></p></li></ul>|

#### <a name="sample-request"></a><span data-ttu-id="a2c91-383">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a2c91-383">Sample request</span></span>

```json
GET {root}/resources/dlpSensitiveTypes?PublisherIdentifier=46b472a7-c68e-4adf-8ade-3db49497518e
Authorization: Bearer eyJ0e...Qa6wg
Accept-Language: {language code} 

```

#### <a name="sample-response"></a><span data-ttu-id="a2c91-384">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a2c91-384">Sample response</span></span>

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

## <a name="api-throttling"></a><span data-ttu-id="a2c91-385">Limitation des requêtes de l’API</span><span class="sxs-lookup"><span data-stu-id="a2c91-385">API throttling</span></span>

<span data-ttu-id="a2c91-386">Chaque éditeur qui code l’API reçoit un quota dédié qui limite le nombre de requêtes envoyées à 60 000 requêtes par minute.</span><span class="sxs-lookup"><span data-stu-id="a2c91-386">Each vendor coding against the API has a dedicated quota for request throttling at 60K per minute.</span></span> <span data-ttu-id="a2c91-387">Pour obtenir le quota dédié, renseignez le paramètre PublisherIdentifier dans toutes vos requêtes.</span><span class="sxs-lookup"><span data-stu-id="a2c91-387">To get the dedicated quota, specify the parameter PublisherIdentifier in all your requests.</span></span> <span data-ttu-id="a2c91-388">Les requêtes contenant le même PublisherIdentifier auront le même quota.</span><span class="sxs-lookup"><span data-stu-id="a2c91-388">Requests with the same PublisherIdentifier will share the same quota.</span></span> <span data-ttu-id="a2c91-389">Toutes les requêtes ne contenant aucun PublisherIdentifier auront le même quota que le GUID 00000000-0000-0000-0000-000000000000.</span><span class="sxs-lookup"><span data-stu-id="a2c91-389">All requests without the PublisherIdentifier specified will share the same quota as GUID 00000000-0000-0000-0000-000000000000.</span></span>

<span data-ttu-id="a2c91-390">Si Office 365 doit vous contacter pour vous faire part d’un problème, vérifiez que l’abonnement du locataire dont le GUID sert de PublisherIdentifier contient des informations exactes et à jour sur le contact.</span><span class="sxs-lookup"><span data-stu-id="a2c91-390">If Office 365 needs to reverse escalate to you in certain issues, make sure the subscription for the tenant whose GUID is used as your PublisherIdentifier is current and updated with the correct contact information.</span></span> <span data-ttu-id="a2c91-391">Aucun abonnement ne doit être souscrit pour ce locataire.</span><span class="sxs-lookup"><span data-stu-id="a2c91-391">There is no subscription requirement for this tenant.</span></span>

<span data-ttu-id="a2c91-392">Pour les clients qui développent leurs solutions à l’aide de cette API, nous leur recommandons d’utiliser leur propre GUID de locataire pour éviter toute concurrence due à un quota partagé limité.</span><span class="sxs-lookup"><span data-stu-id="a2c91-392">For customers who are developing their own solutions using this API, we recommend using your own tenant GUID to avoid competition caused by a limited shared quota.</span></span>

> [!NOTE] 
> <span data-ttu-id="a2c91-393">Même si chaque éditeur peut envoyer 60 000 requêtes par minute, Microsoft ne peut garantir le taux de réponse.</span><span class="sxs-lookup"><span data-stu-id="a2c91-393">Even though each publisher can submit up to 60K requests per minute, Microsoft cannot guarantee a response rate.</span></span> <span data-ttu-id="a2c91-394">Le taux de réponse dépend de différents facteurs, tels que les performances du système client, la capacité réseau et la vitesse du réseau.</span><span class="sxs-lookup"><span data-stu-id="a2c91-394">The response rate depends on various factors, such as client system performance, network capacity, and network speed.</span></span>  <span data-ttu-id="a2c91-395">Un éditeur peut soumettre 60 000 requêtes par minute, mais ne vous attendez pas à recevoir des réponses pour les 60 000 requêtes au cours de cette minute.</span><span class="sxs-lookup"><span data-stu-id="a2c91-395">A publisher can submit up to 60K requests per minute, but should not expect to receive responses for all 60K requests within that same minute.</span></span> <span data-ttu-id="a2c91-396">Si un éditeur souhaite effectuer un test d’évaluation sur une application cliente, il doit le faire dans tous les environnements dans lesquels il prévoit d’exécuter l’application cliente, car les résultats peuvent varier d’un environnement à l’autre.</span><span class="sxs-lookup"><span data-stu-id="a2c91-396">If anything, should a publisher want to benchmark a client application, they should do so in each different environment that they are planning on running the client application in because results will vary from environment to environment.</span></span>

## <a name="errors"></a><span data-ttu-id="a2c91-397">Erreurs</span><span class="sxs-lookup"><span data-stu-id="a2c91-397">Errors</span></span>

<span data-ttu-id="a2c91-398">Quand le service rencontre une erreur, il signale le code de la réponse d’erreur à l’appelant en utilisant la syntaxe du code d’erreur HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="a2c91-398">When the service encounters an error, it will report the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="a2c91-399">.</span><span class="sxs-lookup"><span data-stu-id="a2c91-399">.</span></span> <span data-ttu-id="a2c91-400">Des informations complémentaires sont incluses dans le corps de l’appel ayant échoué en tant qu’objet JSON unique.</span><span class="sxs-lookup"><span data-stu-id="a2c91-400">Additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="a2c91-401">Voici un exemple du corps complet de l’erreur JSON :</span><span class="sxs-lookup"><span data-stu-id="a2c91-401">An example of a full JSON error body is shown below:</span></span> 

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
|<span data-ttu-id="a2c91-402">Code</span><span class="sxs-lookup"><span data-stu-id="a2c91-402">Code</span></span>|<span data-ttu-id="a2c91-403">Message</span><span class="sxs-lookup"><span data-stu-id="a2c91-403">Message</span></span>|
|<span data-ttu-id="a2c91-404">AF10001</span><span class="sxs-lookup"><span data-stu-id="a2c91-404">AF10001</span></span>|<span data-ttu-id="a2c91-405">Le jeu d’autorisations ({0}) envoyé dans la requête n’inclut pas l’autorisation **ActivityFeed.Read** attendue.</span><span class="sxs-lookup"><span data-stu-id="a2c91-405">The permission set ({0}) sent in the request did not include the expected permission **ActivityFeed.Read**.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-406">{0} = jeu d’autorisations défini dans le jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="a2c91-406">{0} = the permission set in the access token.</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-407">AF20001</span><span class="sxs-lookup"><span data-stu-id="a2c91-407">AF20001</span></span>|<span data-ttu-id="a2c91-408">Paramètre manquant : {0}.</span><span class="sxs-lookup"><span data-stu-id="a2c91-408">Missing parameter: {0}.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-409">{0} = nom du paramètre manquant.</span><span class="sxs-lookup"><span data-stu-id="a2c91-409">{0} = the name of the missing parameter.</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-410">AF20002</span><span class="sxs-lookup"><span data-stu-id="a2c91-410">AF20002</span></span>|<span data-ttu-id="a2c91-411">Type de paramètre non valide : {0}.</span><span class="sxs-lookup"><span data-stu-id="a2c91-411">Invalid parameter type: {0}.</span></span> <span data-ttu-id="a2c91-412">Type attendu : {1}.</span><span class="sxs-lookup"><span data-stu-id="a2c91-412">Expected type: {1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-413">{0} = nom du paramètre non valide.</span><span class="sxs-lookup"><span data-stu-id="a2c91-413">{0} = the name of the invalid parameter.</span></span></p></li><li><p><span data-ttu-id="a2c91-414">{1} = type attendu (int, datetime, guid).</span><span class="sxs-lookup"><span data-stu-id="a2c91-414">{1} = the expected type (int, datetime, guid).</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-415">AF20003</span><span class="sxs-lookup"><span data-stu-id="a2c91-415">AF20003</span></span>|<span data-ttu-id="a2c91-416">L’expiration {0} fournie indique une date et une heure passées.</span><span class="sxs-lookup"><span data-stu-id="a2c91-416">Expiration {0} provided is set to past date and time.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-417">{0} = expiration transmise dans l’appel de l’API.</span><span class="sxs-lookup"><span data-stu-id="a2c91-417">{0} = the expiration passed in the API call.</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-418">AF20010</span><span class="sxs-lookup"><span data-stu-id="a2c91-418">AF20010</span></span>|<span data-ttu-id="a2c91-419">L’ID de locataire transmis dans l’URL ({0}) ne correspond pas à l’ID de locataire transmis dans le jeton d’accès ({1}).</span><span class="sxs-lookup"><span data-stu-id="a2c91-419">The tenant ID passed in the URL ({0}) does not match the tenant ID passed in the access token ({1}).</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-420">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="a2c91-420">{0} = tenant ID passed in the URL</span></span></p></li><li><p><span data-ttu-id="a2c91-421">{1} = ID de locataire transmis dans le jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="a2c91-421">{1} = tenant ID passed in the access token</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-422">AF20011</span><span class="sxs-lookup"><span data-stu-id="a2c91-422">AF20011</span></span>|<span data-ttu-id="a2c91-423">L’ID de locataire spécifié ({0}) n’existe pas dans le système ou a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-423">Specified tenant ID ({0}) does not exist in the system or has been deleted.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>   <span data-ttu-id="a2c91-424">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="a2c91-424">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-425">AF20012</span><span class="sxs-lookup"><span data-stu-id="a2c91-425">AF20012</span></span>|<span data-ttu-id="a2c91-426">L’ID de locataire spécifié ({0}) est configuré de façon incorrecte dans le système.</span><span class="sxs-lookup"><span data-stu-id="a2c91-426">Specified tenant ID ({0}) is incorrectly configured in the system.</span></span> <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>    <span data-ttu-id="a2c91-427">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="a2c91-427">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-428">AF20013</span><span class="sxs-lookup"><span data-stu-id="a2c91-428">AF20013</span></span>|<span data-ttu-id="a2c91-429">L’ID de locataire transmis dans l’URL ({0}) n’est pas un GUID valide.</span><span class="sxs-lookup"><span data-stu-id="a2c91-429">The tenant ID passed in the URL ({0}) is not a valid GUID.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p> <span data-ttu-id="a2c91-430">{0} = ID de locataire transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="a2c91-430">{0} = tenant ID passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-431">AF20020</span><span class="sxs-lookup"><span data-stu-id="a2c91-431">AF20020</span></span>|<span data-ttu-id="a2c91-432">Le type de contenu spécifié n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="a2c91-432">The specified content type is not valid.</span></span>|
|<span data-ttu-id="a2c91-433">AF20021</span><span class="sxs-lookup"><span data-stu-id="a2c91-433">AF20021</span></span>|<span data-ttu-id="a2c91-434">Le point de terminaison de webhook {{0}) n’a pas été validé.</span><span class="sxs-lookup"><span data-stu-id="a2c91-434">The webhook endpoint {{0}) could not be validated.</span></span> <span data-ttu-id="a2c91-435">{1}</span><span class="sxs-lookup"><span data-stu-id="a2c91-435">{1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-436">{0} = adresse de webhook.</span><span class="sxs-lookup"><span data-stu-id="a2c91-436">{0} = webhook address.</span></span></p></li><li><p><span data-ttu-id="a2c91-437">{1} = « Le point de terminaison n’a pas renvoyé HTTP 200. »</span><span class="sxs-lookup"><span data-stu-id="a2c91-437">{1} = "The endpoint did not return HTTP 200."</span></span> <span data-ttu-id="a2c91-438">ou « L’adresse doit commencer par HTTPS. ».</span><span class="sxs-lookup"><span data-stu-id="a2c91-438">or "The address must begin with HTTPS."</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-439">AF20022</span><span class="sxs-lookup"><span data-stu-id="a2c91-439">AF20022</span></span>|<span data-ttu-id="a2c91-440">Aucun abonnement trouvé pour le type de contenu spécifié.</span><span class="sxs-lookup"><span data-stu-id="a2c91-440">No subscription found for the specified content type.</span></span>|
|<span data-ttu-id="a2c91-441">AF20023</span><span class="sxs-lookup"><span data-stu-id="a2c91-441">AF20023</span></span>|<span data-ttu-id="a2c91-442">L’abonnement a été désactivé par {0}.</span><span class="sxs-lookup"><span data-stu-id="a2c91-442">The subscription was disabled by {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-443">{0} = « un administrateur du locataire » ou « administrateur du service »</span><span class="sxs-lookup"><span data-stu-id="a2c91-443">{0} = "a tenant admin" or "a service admin"</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-444">AF20030</span><span class="sxs-lookup"><span data-stu-id="a2c91-444">AF20030</span></span>|<span data-ttu-id="a2c91-445">L’heure de début et l’heure de fin doivent être toutes les deux renseignées (ou omises), doivent être espacées d’un intervalle de moins de 24 heures, et l’heure de début ne doit pas dater de plus de 7 jours.</span><span class="sxs-lookup"><span data-stu-id="a2c91-445">Start time and end time must both be specified (or both omitted) and must be less than or equal to 24 hours apart, with the start time no more than 7 days in the past.</span></span>|
|<span data-ttu-id="a2c91-446">AF20031</span><span class="sxs-lookup"><span data-stu-id="a2c91-446">AF20031</span></span>|<span data-ttu-id="a2c91-447">Saisie nextPage non valide : {0}.</span><span class="sxs-lookup"><span data-stu-id="a2c91-447">Invalid nextPage Input: {0}.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-448">{0} = indicateur de la page suivante transmis dans l’URL</span><span class="sxs-lookup"><span data-stu-id="a2c91-448">{0} = the next page indicator passed in the URL</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-449">AF20050</span><span class="sxs-lookup"><span data-stu-id="a2c91-449">AF20050</span></span>|<span data-ttu-id="a2c91-450">Le contenu spécifié ({0}) n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="a2c91-450">The specified content ({0}) does not exist.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-451">{0} = ID ou URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="a2c91-451">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-452">AF20051</span><span class="sxs-lookup"><span data-stu-id="a2c91-452">AF20051</span></span>|<span data-ttu-id="a2c91-453">Le contenu demandé avec la touche {0} a déjà expiré.</span><span class="sxs-lookup"><span data-stu-id="a2c91-453">Content requested with the key {0} has already expired.</span></span> <span data-ttu-id="a2c91-454">Le contenu datant de plus de 7 jours ne peut pas être récupéré.</span><span class="sxs-lookup"><span data-stu-id="a2c91-454">Content older than 7 days cannot be retrieved.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-455">•    {0} = ID ou URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="a2c91-455">•    {0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-456">AF20052</span><span class="sxs-lookup"><span data-stu-id="a2c91-456">AF20052</span></span>|<span data-ttu-id="a2c91-457">L’ID de contenu {0} dans l’URL n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="a2c91-457">Content ID {0} in the URL is invalid.</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-458">{0} = ID ou URL de la ressource</span><span class="sxs-lookup"><span data-stu-id="a2c91-458">{0} = resource id or resource URL</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-459">AF20053</span><span class="sxs-lookup"><span data-stu-id="a2c91-459">AF20053</span></span>|<span data-ttu-id="a2c91-460">Une seule langue peut être indiquée dans l’en-tête Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="a2c91-460">Only one language may be present in the Accept-Language header.</span></span>|
|<span data-ttu-id="a2c91-461">AF20054</span><span class="sxs-lookup"><span data-stu-id="a2c91-461">AF20054</span></span>|<span data-ttu-id="a2c91-462">Syntaxe non valide dans l’en-tête Accept-Language.</span><span class="sxs-lookup"><span data-stu-id="a2c91-462">Invalid syntax in Accept-Language header.</span></span>|
|<span data-ttu-id="a2c91-463">AF429</span><span class="sxs-lookup"><span data-stu-id="a2c91-463">AF429</span></span>|<span data-ttu-id="a2c91-464">Trop de demandes.</span><span class="sxs-lookup"><span data-stu-id="a2c91-464">Too many requests.</span></span> <span data-ttu-id="a2c91-465">Method={0}, PublisherId={1}</span><span class="sxs-lookup"><span data-stu-id="a2c91-465">Method={0}, PublisherId={1}</span></span><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><span data-ttu-id="a2c91-466">{0} = méthode HTTP</span><span class="sxs-lookup"><span data-stu-id="a2c91-466">{0} = HTTP Method</span></span></p></li><li><p><span data-ttu-id="a2c91-467">{1} = GUID de locataire utilisé en tant que PublisherIdentifier</span><span class="sxs-lookup"><span data-stu-id="a2c91-467">{1} = Tenant GUID used as PublisherIdentifier</span></span></p></li></ul>|
|<span data-ttu-id="a2c91-468">AF50000</span><span class="sxs-lookup"><span data-stu-id="a2c91-468">AF50000</span></span>|<span data-ttu-id="a2c91-469">Une erreur interne s’est produite.</span><span class="sxs-lookup"><span data-stu-id="a2c91-469">An internal error occurred.</span></span> <span data-ttu-id="a2c91-470">Retentez la requête.</span><span class="sxs-lookup"><span data-stu-id="a2c91-470">Retry the request.</span></span>|
