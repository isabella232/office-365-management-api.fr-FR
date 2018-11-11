---
ms.TocTitle: Office 365 Service Communications API reference (preview)
title: Référence de l’API Office 365 Service Communications (préversion)
description: 'Utilisez cette API pour accéder aux données suivantes : Obtenir les services, Obtenir l’état actuel, Obtenir l’état de l’historique et Obtenir les messages.'
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: 09/05/2018
ms.openlocfilehash: cde34da7377c5d4820d6ca62dd3affe806eda229
ms.sourcegitcommit: 525c0d0e78cc44ea8cb6a4bdce1858cb4ef91d57
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2018
ms.locfileid: "25834825"
---
# <a name="office-365-service-communications-api-reference-preview"></a><span data-ttu-id="a9b1d-103">Référence de l’API Office 365 Service Communications (préversion)</span><span class="sxs-lookup"><span data-stu-id="a9b1d-103">For operations reference, see Office 365 Service Communications API reference (preview).</span></span>

> [!NOTE] 
> <span data-ttu-id="a9b1d-104">Cette documentation décrit les fonctionnalités qui sont actuellement en préversion.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-104">This documentation covers features that are currently in preview.</span></span>

<span data-ttu-id="a9b1d-105">Vous pouvez utiliser l’API V2 Office 365 Service Communications pour accéder aux données suivantes :</span><span class="sxs-lookup"><span data-stu-id="a9b1d-105">You can use the Office 365 Service Communications API V2 to access the following data:</span></span>

- <span data-ttu-id="a9b1d-106">**Obtenir les services** : obtenez la liste des services abonnés.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-106">**Get Services**: Get the list of subscribed services.</span></span>
    
- <span data-ttu-id="a9b1d-107">**Obtenir l’état actuel** : obtenez une vue en temps réel des incidents de service des événements de maintenance en cours.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-107">**Get Current Status**: Get a real-time view of current and ongoing service incidents and maintenance events</span></span>
    
- <span data-ttu-id="a9b1d-108">**Obtenir l’état de l’historique**: obtenez une vue historique de l’état du service, y compris les incidents de service et les événements de maintenance.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-108">**Get Historical Status**: Get a historical view of service health, including service incidents and maintenance events.</span></span>
    
- <span data-ttu-id="a9b1d-109">**Obtenir les messages** : communications Rechercher un incident, Maintenance planifiée et Centre de messages.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-109">**Get Messages**: Find Incident, Planned Maintenance, and Message Center communications.</span></span>
    
<span data-ttu-id="a9b1d-110">Pour l’instant, l’API Office 365 Service Communications contient des données pour les services suivants : Dynamics CRM, Dynamics Marketing, Exchange Online, Exchange Online Protection, Service d’identité, Gestion des périphériques mobiles, Centre d’administration des partenaires Office 365, OneDrive Entreprise, Parature, OneDrive Entreprise, Power BI pour Office 365, Service Gestion des droits, SharePoint Online, Administration de SHD, Skype Entreprise, Social Engagement, et Yammer Entreprise.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-110">Currently, the Office 365 Service Communications API contains data for the following services: Dynamics CRM, Dynamics Marketing, Exchange Online, Exchange Online Protection, Identity Service, Mobile Device Management, Office 365 Partner Admin Center, OneDrive for Business, Parature, OneDrive for Business, Power BI for Office 365, Rights Management Service, SharePoint Online, SHD Admin, Skype for Business, Social Engagement, and Yammer Enterprise.</span></span>

## <a name="the-fundamentals"></a><span data-ttu-id="a9b1d-111">Les principes de base</span><span class="sxs-lookup"><span data-stu-id="a9b1d-111">The fundamentals</span></span>

<span data-ttu-id="a9b1d-112">L’URL racine de l’API inclut un identificateur client qui étend les opérations sur un seul client :</span><span class="sxs-lookup"><span data-stu-id="a9b1d-112">The root URL of the API includes a tenant identifier that scopes the operations to a single tenant:</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

<span data-ttu-id="a9b1d-113">L’**API Office 365 Service Communications** est un service REST qui vous permet de développer des solutions à l’aide de n’importe quel langage web et environnement d’hébergement qui prend en charge les certificats X.509 et HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-113">The **Office 365 Service Communications API** is a REST service that allows you to develop solutions using any web language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="a9b1d-114">L’API se base sur **Microsoft Azure Active Directory** et le protocole **OAuth2** pour l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-114">The API relies on **Microsoft Azure Active Directory** and the **OAuth2** protocol for authentication and authorization.</span></span> <span data-ttu-id="a9b1d-115">Pour accéder à l’API depuis votre application, vous devez d’abord l’enregistrer dans Azure AD et la configurer avec les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-115">To access the Video API from your application, you'll need to register it in Azure AD with permissions at the appropriate scope.</span></span> <span data-ttu-id="a9b1d-116">Cela permettra à votre application de demander les jetons d’accès OAuth2 nécessaires pour appeler l’API.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-116">This will enable your application to request OAuth2 access tokens necessary for calling the API.</span></span> <span data-ttu-id="a9b1d-117">Vous trouverez plus d’informations sur l’enregistrement et la configuration d’une application dans Azure AD dans la rubrique relative à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-117">You can find more information about registering and configuring an application in Azure AD at [Office 365 Management APIs getting started](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="a9b1d-118">Toutes les demandes API nécessitent un en-tête HTTP d’autorisation contenant un jeton d’accès JWT OAuth2 valide provenant d’Azure AD qui contient la revendication **ServiceHealth.Read** ; et l’identificateur client doit correspondre à l’identificateur client dans l’URL racine.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-118">All API requests require an Authorization HTTP header that has a valid OAuth2 JWT access token obtained from Azure AD that contains the **ServiceHealth.Read** claim; and the tenant identifier must match the tenant identifier in the root URL.</span></span>

```json
Authorization: Bearer {OAuth2 token}
```

<span data-ttu-id="a9b1d-119">**En-têtes de demande**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-119">**Request headers**</span></span>

<span data-ttu-id="a9b1d-120">Voici les en-têtes de demande pris en charge pour toutes les opérations de l’API Office 365 Service Communications.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-120">These are the supported request headers for all Office 365 Service Communications API operations.</span></span>

|<span data-ttu-id="a9b1d-121">En-tête</span><span class="sxs-lookup"><span data-stu-id="a9b1d-121">Header</span></span>|<span data-ttu-id="a9b1d-122">Description</span><span class="sxs-lookup"><span data-stu-id="a9b1d-122">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="a9b1d-123">**Accept (facultatif)**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-123">**Accept (Optional)**</span></span>|<span data-ttu-id="a9b1d-124">Voici les représentations acceptables pour la réponse :</span><span class="sxs-lookup"><span data-stu-id="a9b1d-124">The following are acceptable representations for the response:</span></span><br/><span data-ttu-id="a9b1d-125">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-125">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="a9b1d-126">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-126">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="a9b1d-127">[La valeur par défaut si l’en-tête n’est pas spécifié] **application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-127">[The default if header not specified] **application/json;odata.metadata=none**</span></span>|
|<span data-ttu-id="a9b1d-128">**Authorization (obligatoire)**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-128">**Authorization (Required)**</span></span>|<span data-ttu-id="a9b1d-129">Jeton d’autorisation (jeton Azure AD JWT du porteur) de la demande.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-129">Authorization token (Bearer JWT Azure AD Token) for the request.</span></span>|


<br/>

<span data-ttu-id="a9b1d-130">**En-têtes de réponse**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-130">**Response headers**</span></span>

<span data-ttu-id="a9b1d-131">Voici les en-têtes de réponse renvoyés pour toutes les opérations de l’API Office 365 Service Communications :</span><span class="sxs-lookup"><span data-stu-id="a9b1d-131">These are the response headers returned for all Office 365 Service Communications API operations:</span></span>

|<span data-ttu-id="a9b1d-132">En-tête</span><span class="sxs-lookup"><span data-stu-id="a9b1d-132">Header</span></span>|<span data-ttu-id="a9b1d-133">Description</span><span class="sxs-lookup"><span data-stu-id="a9b1d-133">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="a9b1d-134">**Content-Length**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-134">**Content-Length**</span></span>|<span data-ttu-id="a9b1d-135">La longueur du corps de la réponse.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-135">The length of the response body.</span></span>|
|<span data-ttu-id="a9b1d-136">**Content-Type**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-136">**Content-Type**</span></span>|<span data-ttu-id="a9b1d-137">Représentation de la réponse :</span><span class="sxs-lookup"><span data-stu-id="a9b1d-137">Representation of the response:</span></span><br/><span data-ttu-id="a9b1d-138">**application/json**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-138">**application/json**</span></span><br/><span data-ttu-id="a9b1d-139">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-139">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="a9b1d-140">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-140">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="a9b1d-141">**application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-141">**application/json;odata.metadata=none**</span></span><br/><span data-ttu-id="a9b1d-142">**odata.streaming=true**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-142">**odata.streaming=true**</span></span>|
|<span data-ttu-id="a9b1d-143">**Cache-Control**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-143">**Cache-Control**</span></span>|<span data-ttu-id="a9b1d-144">Utilisé pour spécifier les directives que doivent respecter tous les mécanismes de mise en cache accompagnant la chaîne de demande/réponse.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-144">Used to specify directives that all caching mechanisms along the request/response chain must obey.</span></span>|
|<span data-ttu-id="a9b1d-145">**Pragma**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-145">**Pragma**</span></span>|<span data-ttu-id="a9b1d-146">Comportements propres à l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-146">Implementation-specific behaviors.</span></span>|
|<span data-ttu-id="a9b1d-147">**Date d’expiration**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-147">**Expires**</span></span>|<span data-ttu-id="a9b1d-148">Date d’expiration de la ressource définie par le client.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-148">When the client should make the resource expire.</span></span>|
|<span data-ttu-id="a9b1d-149">**X-Activity-Id**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-149">**X-Activity-Id**</span></span>|<span data-ttu-id="a9b1d-150">ID d’activité généré par le serveur.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-150">The server-generated activity Id.</span></span>|
|<span data-ttu-id="a9b1d-151">**OData-Version**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-151">**OData-Version**</span></span>|<span data-ttu-id="a9b1d-152">Version d’OData prise en charge (4.0).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-152">The supported OData Version (4.0).</span></span>|
|<span data-ttu-id="a9b1d-153">**Date**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-153">**Date**</span></span>|<span data-ttu-id="a9b1d-154">Date UTC d’envoi de la réponse à partir du serveur.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-154">The date in UTC when the response was sent from the server.</span></span>|
|<span data-ttu-id="a9b1d-155">**X-Time-Taken**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-155">**X-Time-Taken**</span></span>|<span data-ttu-id="a9b1d-156">Durée de génération de la réponse (ms).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-156">The time it took to generate the response (ms).</span></span>|
|<span data-ttu-id="a9b1d-157">**X-Instance-Name**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-157">**X-Instance-Name**</span></span>|<span data-ttu-id="a9b1d-158">Identificateur de l’instance Azure utilisé pour générer la réponse (à des fins de débogage).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-158">The identifier of the Azure instance used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="a9b1d-159">**Serveur**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-159">**Server**</span></span>|<span data-ttu-id="a9b1d-160">Serveur utilisé pour générer la réponse (à des fins de débogage).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-160">The server used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="a9b1d-161">**X-ASPNET-Version**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-161">**X-ASPNET-Version**</span></span>|<span data-ttu-id="a9b1d-162">Version d’ASP.Net utilisée par le serveur ayant généré la réponse (à des fins de débogage).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-162">The version of ASP.Net used by the server that generated the response (for debugging purposes).</span></span>|
|<span data-ttu-id="a9b1d-163">**X-Powered-By**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-163">**X-Powered-By**</span></span>|<span data-ttu-id="a9b1d-164">Technologies utilisées dans le serveur ayant généré la réponse (à des fins de débogage).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-164">The technologies used in the server that generated the response (for debugging purposes).</span></span>|

<br/>

<span data-ttu-id="a9b1d-165">Voici les opérations de l’API Office 365 Service Communications.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-165">Following are the Office 365 Service Communications API operations.</span></span>


## <a name="get-services"></a><span data-ttu-id="a9b1d-166">Obtenir les services</span><span class="sxs-lookup"><span data-stu-id="a9b1d-166">Get Services</span></span>

<span data-ttu-id="a9b1d-167">Renvoie la liste des services abonnés.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-167">Returns the list of subscribed services.</span></span>

||<span data-ttu-id="a9b1d-168">Service</span><span class="sxs-lookup"><span data-stu-id="a9b1d-168">Service</span></span>|<span data-ttu-id="a9b1d-169">Description</span><span class="sxs-lookup"><span data-stu-id="a9b1d-169">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a9b1d-170">**Path**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-170">**Path**</span></span>| `/Services`||
|<span data-ttu-id="a9b1d-171">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-171">**Query-option**</span></span>|<span data-ttu-id="a9b1d-172">$select</span><span class="sxs-lookup"><span data-stu-id="a9b1d-172">$select</span></span>|<span data-ttu-id="a9b1d-173">Sélectionnez un sous-ensemble de propriétés.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-173">Pick a subset of properties.</span></span>|
|<span data-ttu-id="a9b1d-174">**Response**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-174">**Response**</span></span>|<span data-ttu-id="a9b1d-175">Liste des entités « Service »</span><span class="sxs-lookup"><span data-stu-id="a9b1d-175">List of "Service" entities</span></span>|<span data-ttu-id="a9b1d-176">L’entité « Service » contient « Id » (chaîne), « DisplayName » (chaîne) et « FeatureNames » (liste de chaînes).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-176">"Service" entity contains "Id" (String), "DisplayName" (String), and "FeatureNames" (list of Strings).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="a9b1d-177">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a9b1d-177">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

#### <a name="sample-response"></a><span data-ttu-id="a9b1d-178">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a9b1d-178">Sample response</span></span>

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


## <a name="get-current-status"></a><span data-ttu-id="a9b1d-179">Obtenir l’état actuel</span><span class="sxs-lookup"><span data-stu-id="a9b1d-179">Get Current Status</span></span>

<span data-ttu-id="a9b1d-180">Renvoie l’état actuel du service.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-180">Returns the current status of the service.</span></span>

||<span data-ttu-id="a9b1d-181">Service</span><span class="sxs-lookup"><span data-stu-id="a9b1d-181">Service</span></span>|<span data-ttu-id="a9b1d-182">Description</span><span class="sxs-lookup"><span data-stu-id="a9b1d-182">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a9b1d-183">**Path**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-183">**Path**</span></span>| `/CurrentStatus`||
|<span data-ttu-id="a9b1d-184">**Filter**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-184">**Filter**</span></span>|<span data-ttu-id="a9b1d-185">Charge de travail</span><span class="sxs-lookup"><span data-stu-id="a9b1d-185">Workload</span></span>|<span data-ttu-id="a9b1d-186">Filtrez par charge de travail (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-186">Filter by workload (String, default: all).</span></span>|
|<span data-ttu-id="a9b1d-187">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-187">**Query-option**</span></span>|<span data-ttu-id="a9b1d-188">$select</span><span class="sxs-lookup"><span data-stu-id="a9b1d-188">$select</span></span>|<span data-ttu-id="a9b1d-189">Sélectionnez un sous-ensemble de propriétés.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-189">Pick a subset of properties.</span></span>|
|<span data-ttu-id="a9b1d-190">**Response**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-190">**Response**</span></span>|<span data-ttu-id="a9b1d-191">Liste des entités « WorkloadStatus ».</span><span class="sxs-lookup"><span data-stu-id="a9b1d-191">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="a9b1d-192">L’entité « WorkloadStatus » contient « Id » (chaîne), « Workload » (chaîne), « StatusTime »(DateTimeOffset), « WorkloadDisplayName » (chaîne), « Status » (chaîne), « IncidentIds » (liste de chaînes) et FeatureGroupStatusCollection (liste des « FeatureStatus »).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-192">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="a9b1d-193">L’entité « FeatureStatus » contient « Feature » (chaîne), « FeatureGroupDisplayName » (chaîne) et « FeatureStatus » (chaîne).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-193">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="a9b1d-194">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a9b1d-194">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="a9b1d-195">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a9b1d-195">Sample response</span></span>

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


## <a name="get-historical-status"></a><span data-ttu-id="a9b1d-196">Obtenir l’état de l’historique</span><span class="sxs-lookup"><span data-stu-id="a9b1d-196">Get Historical Status</span></span>

<span data-ttu-id="a9b1d-197">Renvoie l’état historique du service, par jour, sur un intervalle de temps donné.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-197">Returns the historical status of the service, by day, over a certain time range.</span></span>

||<span data-ttu-id="a9b1d-198">Service</span><span class="sxs-lookup"><span data-stu-id="a9b1d-198">Service</span></span>|<span data-ttu-id="a9b1d-199">Description</span><span class="sxs-lookup"><span data-stu-id="a9b1d-199">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a9b1d-200">**Path**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-200">**Path**</span></span>| `/HistoricalStatus`||
|<span data-ttu-id="a9b1d-201">**Filters**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-201">**Filters**</span></span>|<span data-ttu-id="a9b1d-202">Charge de travail</span><span class="sxs-lookup"><span data-stu-id="a9b1d-202">Workload</span></span>|<span data-ttu-id="a9b1d-203">Filtrez par charge de travail (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-203">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="a9b1d-204">StatusTime</span><span class="sxs-lookup"><span data-stu-id="a9b1d-204">StatusTime</span></span>|<span data-ttu-id="a9b1d-205">Filtrez par jour supérieur à StatusTime (DateTimeOffset, valeur par défaut : ge CurrentTime - 7 jours).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-205">Filter by days greater than StatusTime (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
|<span data-ttu-id="a9b1d-206">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-206">**Query-option**</span></span>|<span data-ttu-id="a9b1d-207">$select</span><span class="sxs-lookup"><span data-stu-id="a9b1d-207">$select</span></span>|<span data-ttu-id="a9b1d-208">Sélectionnez un sous-ensemble de propriétés.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-208">Pick a subset of properties.</span></span>|
|<span data-ttu-id="a9b1d-209">**Response**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-209">**Response**</span></span>|<span data-ttu-id="a9b1d-210">Liste des entités « WorkloadStatus ».</span><span class="sxs-lookup"><span data-stu-id="a9b1d-210">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="a9b1d-211">L’entité « WorkloadStatus » contient « Id » (chaîne), « Workload » (chaîne), « StatusTime »(DateTimeOffset), « WorkloadDisplayName » (chaîne), « Status » (chaîne), « IncidentIds » (liste de chaînes) et FeatureGroupStatusCollection (liste des « FeatureStatus »).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-211">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="a9b1d-212">L’entité « FeatureStatus » contient « Feature » (chaîne), « FeatureGroupDisplayName » (chaîne) et « FeatureStatus » (chaîne).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-212">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="a9b1d-213">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a9b1d-213">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="a9b1d-214">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a9b1d-214">Sample response</span></span>

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


## <a name="get-messages"></a><span data-ttu-id="a9b1d-215">Obtenir les messages</span><span class="sxs-lookup"><span data-stu-id="a9b1d-215">Get Messages</span></span>

<span data-ttu-id="a9b1d-216">Renvoie les messages sur le service sur un intervalle de temps donné.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-216">Returns the messages about the service over a certain time range.</span></span> <span data-ttu-id="a9b1d-217">Utilisez le filtre de type pour filtrer les messages « Incident de service », « Maintenance planifiée » ou « Centre de messages ».</span><span class="sxs-lookup"><span data-stu-id="a9b1d-217">Use the type filter to filter for "Service Incident", "Planned Maintenance", or "Message Center" messages.</span></span>

||<span data-ttu-id="a9b1d-218">Service</span><span class="sxs-lookup"><span data-stu-id="a9b1d-218">Service</span></span>|<span data-ttu-id="a9b1d-219">Description</span><span class="sxs-lookup"><span data-stu-id="a9b1d-219">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="a9b1d-220">**Path**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-220">**Path**</span></span>| `/Messages`||
|<span data-ttu-id="a9b1d-221">**Filters**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-221">**Filters**</span></span>|<span data-ttu-id="a9b1d-222">Charge de travail</span><span class="sxs-lookup"><span data-stu-id="a9b1d-222">Workload</span></span>|<span data-ttu-id="a9b1d-223">Filtrez par charge de travail (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-223">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="a9b1d-224">StartTime</span><span class="sxs-lookup"><span data-stu-id="a9b1d-224">StartTime</span></span>|<span data-ttu-id="a9b1d-225">Filtrez par Start Time (DateTimeOffset, valeur par défaut : ge CurrentTime - 7 jours).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-225">Filter by Start Time (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
||<span data-ttu-id="a9b1d-226">EndTime</span><span class="sxs-lookup"><span data-stu-id="a9b1d-226">EndTime</span></span>|<span data-ttu-id="a9b1d-227">Filtrez par End Time (DateTimeOffset, valeur par défaut : le CurrentTime).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-227">Filter by End Time (DateTimeOffset, default: le CurrentTime).</span></span>|
||<span data-ttu-id="a9b1d-228">MessageType</span><span class="sxs-lookup"><span data-stu-id="a9b1d-228">MessageType</span></span>|<span data-ttu-id="a9b1d-229">Filtrez par MessageType (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-229">Filter by MessageType (String, default: all).</span></span>|
||<span data-ttu-id="a9b1d-230">ID</span><span class="sxs-lookup"><span data-stu-id="a9b1d-230">ID</span></span>|<span data-ttu-id="a9b1d-231">Filtrez par ID (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-231">Filter by ID (String, default: all).</span></span>|
|<span data-ttu-id="a9b1d-232">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-232">**Query-option**</span></span>|<span data-ttu-id="a9b1d-233">$select</span><span class="sxs-lookup"><span data-stu-id="a9b1d-233">$select</span></span>|<span data-ttu-id="a9b1d-234">Sélectionnez un sous-ensemble de propriétés.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-234">Pick a subset of properties.</span></span>|
||<span data-ttu-id="a9b1d-235">$top</span><span class="sxs-lookup"><span data-stu-id="a9b1d-235">$top</span></span>|<span data-ttu-id="a9b1d-236">Sélectionnez le nombre de résultats le plus élevé (valeur par défaut et max $top=100).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-236">Pick the top number of results (default and max $top=100).</span></span>|
||<span data-ttu-id="a9b1d-237">$skip</span><span class="sxs-lookup"><span data-stu-id="a9b1d-237">$skip</span></span>|<span data-ttu-id="a9b1d-238">Ignorez le nombre de résultats (valeur par défaut : $skip = 0).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-238">Skip number of results (default: $skip=0).</span></span>|
|<span data-ttu-id="a9b1d-239">**Response**</span><span class="sxs-lookup"><span data-stu-id="a9b1d-239">**Response**</span></span>|<span data-ttu-id="a9b1d-240">Liste des entités « Message ».</span><span class="sxs-lookup"><span data-stu-id="a9b1d-240">List of "Message" entities.</span></span>|<span data-ttu-id="a9b1d-241">L’entité « Message » contient « Id » (chaîne), « StartTime » (DateTimeOffset), « EndTime » (DateTimeOffset), « Status » (chaîne), « Messages » (liste des entités « MessagHistory »), « LastUpdatedTime » (DateTimeOffset), « Workload » (chaîne), « WorkloadDisplayName » (chaîne), « Feature » (chaîne), « FeatureDisplayName » (chaîne), « MessageType » (Enum, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-241">"Message" entity contains "Id" (String), "StartTime" (DateTimeOffset), "EndTime" (DateTimeOffset), "Status" (String), "Messages" (list of "MessagHistory" entity), "LastUpdatedTime" (DateTimeOffset), "Workload" (String), "WorkloadDisplayName" (String), "Feature" (String), "FeatureDisplayName" (String), "MessageType" (Enum, default: all).</span></span><br/><br/><span data-ttu-id="a9b1d-242">L’entité « MessageHistory » contient « PublishedTime » (DateTimeOffset) et « MessageText » (chaîne).</span><span class="sxs-lookup"><span data-stu-id="a9b1d-242">"MessageHistory" entity contains "PublishedTime" (DateTimeOffset), "MessageText" (String).</span></span>|

#### <a name="sample-request"></a><span data-ttu-id="a9b1d-243">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="a9b1d-243">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

#### <a name="sample-response"></a><span data-ttu-id="a9b1d-244">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="a9b1d-244">Sample response</span></span>

```json
{
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


## <a name="errors"></a><span data-ttu-id="a9b1d-245">Errors</span><span class="sxs-lookup"><span data-stu-id="a9b1d-245">Errors</span></span>

<span data-ttu-id="a9b1d-246">Lorsque le service rencontre une erreur, il signale le code de la réponse d’erreur à l’appelant à l’aide de la syntaxe de code d’erreur HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-246">When the service encounters an error, it reports the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="a9b1d-247">Selon la [spécification OData V4](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), des informations supplémentaires sont incluses dans le corps de l’appel ayant échoué en tant qu’objet JSON unique.</span><span class="sxs-lookup"><span data-stu-id="a9b1d-247">As per [OData V4 specification](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="a9b1d-248">Voici un exemple de corps d’erreur JSON complet :</span><span class="sxs-lookup"><span data-stu-id="a9b1d-248">The following is an example of a full JSON error body.</span></span>


```json

{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}

```

