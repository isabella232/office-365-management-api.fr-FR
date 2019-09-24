---
ms.TocTitle: Office 365 Service Communications API reference
title: Référence de l’API Office 365 Service Communications
description: 'Utilisez cette API pour accéder aux données suivantes : Obtenir les services, Obtenir l’état actuel, Obtenir l’état de l’historique et Obtenir les messages.'
ms.ContentId: d0b9341a-b205-5442-1c20-8fb56407351d
ms.topic: reference (API)
ms.date: ''
localization_priority: Priority
ms.openlocfilehash: 427c741f623f46962c3cd6818adbb64bfc0f1e7a
ms.sourcegitcommit: 0e6d71ad2375e5d1fc72d6893724511c08840c27
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/24/2019
ms.locfileid: "37131423"
---
# <a name="office-365-service-communications-api-reference"></a><span data-ttu-id="d3c77-103">Référence de l’API Office 365 Service Communications</span><span class="sxs-lookup"><span data-stu-id="d3c77-103">Office 365 Service Communications API reference (preview)</span></span>

<span data-ttu-id="d3c77-104">Vous pouvez utiliser l’API V2 Office 365 Service Communications pour accéder aux données suivantes :</span><span class="sxs-lookup"><span data-stu-id="d3c77-104">You can use the Office 365 Service Communications API V2 to access the following data:</span></span>

- <span data-ttu-id="d3c77-105">**Obtenir les services** : obtenez la liste des services abonnés.</span><span class="sxs-lookup"><span data-stu-id="d3c77-105">**Get Services**: Get the list of subscribed services.</span></span>
    
- <span data-ttu-id="d3c77-106">**Obtenir l’état actuel** : obtenez une vue en temps réel des incidents de service des événements en cours.</span><span class="sxs-lookup"><span data-stu-id="d3c77-106">**Get Current Status**: Get a real-time view of current and ongoing service incidents and maintenance events</span></span>
    
- <span data-ttu-id="d3c77-107">**Obtenir l’état de l’historique** : obtenez une vue historique des incidents de service.</span><span class="sxs-lookup"><span data-stu-id="d3c77-107">**Get Historical Status**: Get a historical view of service health, including service incidents and maintenance events.</span></span>
    
- <span data-ttu-id="d3c77-108">**Obtenir les messages** : communications Rechercher un incident et Centre de messages.</span><span class="sxs-lookup"><span data-stu-id="d3c77-108">**Get Messages**: Find Incident, Planned Maintenance, and Message Center communications.</span></span>
    
<span data-ttu-id="d3c77-109">Actuellement, l’API Office 365 Service Communications contient des données pour Office 365, Yammer, Dynamics CRM et les services Cloud de Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="d3c77-109">Currently, the Office 365 Service Communications API contains data for Office 365, Yammer, Dynamics CRM and Microsoft Intune cloud services.</span></span>

## <a name="the-fundamentals"></a><span data-ttu-id="d3c77-110">Les principes de base</span><span class="sxs-lookup"><span data-stu-id="d3c77-110">The fundamentals</span></span>

<span data-ttu-id="d3c77-111">L’URL racine de l’API inclut un identificateur client qui étend les opérations sur un seul client :</span><span class="sxs-lookup"><span data-stu-id="d3c77-111">The root URL of the API includes a tenant identifier that scopes the operations to a single tenant:</span></span>

```http
https://manage.office.com/api/v1.0/{tenant_identifier}/ServiceComms/{operation}
```

<span data-ttu-id="d3c77-112">L’**API Office 365 Service Communications** est un service REST qui vous permet de développer des solutions à l’aide de n’importe quel langage web et environnement d’hébergement qui prend en charge les certificats X.509 et HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d3c77-112">The **Office 365 Service Communications API** is a REST service that allows you to develop solutions using any web language and hosting environment that supports HTTPS and X.509 certificates.</span></span> <span data-ttu-id="d3c77-113">L’API se base sur **Microsoft Azure Active Directory** et le protocole **OAuth2** pour l’authentification et l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="d3c77-113">The API relies on **Microsoft Azure Active Directory** and the **OAuth2** protocol for authentication and authorization.</span></span> <span data-ttu-id="d3c77-114">Pour accéder à l’API depuis votre application, vous devez d’abord l’enregistrer dans Azure AD et la configurer avec les autorisations appropriées.</span><span class="sxs-lookup"><span data-stu-id="d3c77-114">To access the API from your application, you'll need to first register it in Azure AD and configure it with permissions at the appropriate scope.</span></span> <span data-ttu-id="d3c77-115">Cela permettra à votre application de demander les jetons d’accès OAuth2 nécessaires pour appeler l’API.</span><span class="sxs-lookup"><span data-stu-id="d3c77-115">This will enable your application to request OAuth2 access tokens necessary for calling the API.</span></span> <span data-ttu-id="d3c77-116">Vous trouverez plus d’informations sur l’enregistrement et la configuration d’une application dans Azure AD dans la rubrique relative à la [prise en main des API de gestion Office 365](get-started-with-office-365-management-apis.md).</span><span class="sxs-lookup"><span data-stu-id="d3c77-116">You can find more information about registering and configuring an application in Azure AD at [Office 365 Management APIs getting started](get-started-with-office-365-management-apis.md).</span></span>

<span data-ttu-id="d3c77-117">Toutes les demandes API nécessitent un en-tête HTTP d’autorisation contenant un jeton d’accès JWT OAuth2 valide provenant d’Azure AD qui contient la revendication **ServiceHealth.Read** ; et l’identificateur client doit correspondre à l’identificateur client dans l’URL racine.</span><span class="sxs-lookup"><span data-stu-id="d3c77-117">All API requests require an Authorization HTTP header that has a valid OAuth2 JWT access token obtained from Azure AD that contains the **ServiceHealth.Read** claim; and the tenant identifier must match the tenant identifier in the root URL.</span></span>

```json
Authorization: Bearer {OAuth2 token}
```

### <a name="request-headers"></a><span data-ttu-id="d3c77-118">En-têtes de demande</span><span class="sxs-lookup"><span data-stu-id="d3c77-118">Request headers</span></span>

<span data-ttu-id="d3c77-119">Voici les en-têtes de demande pris en charge pour toutes les opérations de l’API Office 365 Service Communications.</span><span class="sxs-lookup"><span data-stu-id="d3c77-119">These are the supported request headers for all Office 365 Service Communications API operations.</span></span>

|<span data-ttu-id="d3c77-120">En-tête</span><span class="sxs-lookup"><span data-stu-id="d3c77-120">Header</span></span>|<span data-ttu-id="d3c77-121">Description</span><span class="sxs-lookup"><span data-stu-id="d3c77-121">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="d3c77-122">**Accept (facultatif)**</span><span class="sxs-lookup"><span data-stu-id="d3c77-122">**Accept (Optional)**</span></span>|<span data-ttu-id="d3c77-123">Voici les représentations acceptables pour la réponse :</span><span class="sxs-lookup"><span data-stu-id="d3c77-123">The following are acceptable representations for the response:</span></span><br/><span data-ttu-id="d3c77-124">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="d3c77-124">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="d3c77-125">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="d3c77-125">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="d3c77-126">[La valeur par défaut si l’en-tête n’est pas spécifié] **application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="d3c77-126">[The default if header not specified] **application/json;odata.metadata=none**</span></span>|
|<span data-ttu-id="d3c77-127">**Authorization (obligatoire)**</span><span class="sxs-lookup"><span data-stu-id="d3c77-127">**Authorization (Required)**</span></span>|<span data-ttu-id="d3c77-128">Jeton d’autorisation (jeton Azure AD JWT du porteur) de la demande.</span><span class="sxs-lookup"><span data-stu-id="d3c77-128">Authorization token (Bearer JWT Azure AD Token) for the request.</span></span>|


<br/>

### <a name="response-headers"></a><span data-ttu-id="d3c77-129">En-têtes de réponse</span><span class="sxs-lookup"><span data-stu-id="d3c77-129">Response headers</span></span>

<span data-ttu-id="d3c77-130">Voici les en-têtes de réponse renvoyés pour toutes les opérations de l’API Office 365 Service Communications :</span><span class="sxs-lookup"><span data-stu-id="d3c77-130">These are the response headers returned for all Office 365 Service Communications API operations:</span></span>

|<span data-ttu-id="d3c77-131">En-tête</span><span class="sxs-lookup"><span data-stu-id="d3c77-131">Header</span></span>|<span data-ttu-id="d3c77-132">Description</span><span class="sxs-lookup"><span data-stu-id="d3c77-132">Description</span></span>|
|:-----|:-----|
|<span data-ttu-id="d3c77-133">**Content-Length**</span><span class="sxs-lookup"><span data-stu-id="d3c77-133">**Content-Length**</span></span>|<span data-ttu-id="d3c77-134">La longueur du corps de la réponse.</span><span class="sxs-lookup"><span data-stu-id="d3c77-134">The length of the response body.</span></span>|
|<span data-ttu-id="d3c77-135">**Content-Type**</span><span class="sxs-lookup"><span data-stu-id="d3c77-135">**Content-Type**</span></span>|<span data-ttu-id="d3c77-136">Représentation de la réponse :</span><span class="sxs-lookup"><span data-stu-id="d3c77-136">Representation of the response:</span></span><br/><span data-ttu-id="d3c77-137">**application/json**</span><span class="sxs-lookup"><span data-stu-id="d3c77-137">**application/json**</span></span><br/><span data-ttu-id="d3c77-138">**application/json;odata.metadata=full**</span><span class="sxs-lookup"><span data-stu-id="d3c77-138">**application/json;odata.metadata=full**</span></span><br/><span data-ttu-id="d3c77-139">**application/json;odata.metadata=minimal**</span><span class="sxs-lookup"><span data-stu-id="d3c77-139">**application/json;odata.metadata=minimal**</span></span><br/><span data-ttu-id="d3c77-140">**application/json;odata.metadata=none**</span><span class="sxs-lookup"><span data-stu-id="d3c77-140">**application/json;odata.metadata=none**</span></span><br/><span data-ttu-id="d3c77-141">**odata.streaming=true**</span><span class="sxs-lookup"><span data-stu-id="d3c77-141">**odata.streaming=true**</span></span>|
|<span data-ttu-id="d3c77-142">**Cache-Control**</span><span class="sxs-lookup"><span data-stu-id="d3c77-142">**Cache-Control**</span></span>|<span data-ttu-id="d3c77-143">Utilisé pour spécifier les directives que doivent respecter tous les mécanismes de mise en cache accompagnant la chaîne de demande/réponse.</span><span class="sxs-lookup"><span data-stu-id="d3c77-143">Used to specify directives that all caching mechanisms along the request/response chain must obey.</span></span>|
|<span data-ttu-id="d3c77-144">**Pragma**</span><span class="sxs-lookup"><span data-stu-id="d3c77-144">**Pragma**</span></span>|<span data-ttu-id="d3c77-145">Comportements propres à l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="d3c77-145">Implementation-specific behaviors.</span></span>|
|<span data-ttu-id="d3c77-146">**Date d’expiration**</span><span class="sxs-lookup"><span data-stu-id="d3c77-146">**Expires**</span></span>|<span data-ttu-id="d3c77-147">Date d’expiration de la ressource définie par le client.</span><span class="sxs-lookup"><span data-stu-id="d3c77-147">When the client should make the resource expire.</span></span>|
|<span data-ttu-id="d3c77-148">**X-Activity-Id**</span><span class="sxs-lookup"><span data-stu-id="d3c77-148">**X-Activity-Id**</span></span>|<span data-ttu-id="d3c77-149">ID d’activité généré par le serveur.</span><span class="sxs-lookup"><span data-stu-id="d3c77-149">The server-generated activity Id.</span></span>|
|<span data-ttu-id="d3c77-150">**OData-Version**</span><span class="sxs-lookup"><span data-stu-id="d3c77-150">**OData-Version**</span></span>|<span data-ttu-id="d3c77-151">Version d’OData prise en charge (4.0).</span><span class="sxs-lookup"><span data-stu-id="d3c77-151">The supported OData Version (4.0).</span></span>|
|<span data-ttu-id="d3c77-152">**Date**</span><span class="sxs-lookup"><span data-stu-id="d3c77-152">**Date**</span></span>|<span data-ttu-id="d3c77-153">Date UTC d’envoi de la réponse à partir du serveur.</span><span class="sxs-lookup"><span data-stu-id="d3c77-153">The date in UTC when the response was sent from the server.</span></span>|
|<span data-ttu-id="d3c77-154">**X-Time-Taken**</span><span class="sxs-lookup"><span data-stu-id="d3c77-154">**X-Time-Taken**</span></span>|<span data-ttu-id="d3c77-155">Durée de génération de la réponse (ms).</span><span class="sxs-lookup"><span data-stu-id="d3c77-155">The time it took to generate the response (ms).</span></span>|
|<span data-ttu-id="d3c77-156">**X-Instance-Name**</span><span class="sxs-lookup"><span data-stu-id="d3c77-156">**X-Instance-Name**</span></span>|<span data-ttu-id="d3c77-157">Identificateur de l’instance Azure utilisé pour générer la réponse (à des fins de débogage).</span><span class="sxs-lookup"><span data-stu-id="d3c77-157">The identifier of the Azure instance used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="d3c77-158">**Serveur**</span><span class="sxs-lookup"><span data-stu-id="d3c77-158">**Server**</span></span>|<span data-ttu-id="d3c77-159">Serveur utilisé pour générer la réponse (à des fins de débogage).</span><span class="sxs-lookup"><span data-stu-id="d3c77-159">The server used to generate the response (for debugging purposes).</span></span>|
|<span data-ttu-id="d3c77-160">**X-ASPNET-Version**</span><span class="sxs-lookup"><span data-stu-id="d3c77-160">**X-ASPNET-Version**</span></span>|<span data-ttu-id="d3c77-161">Version d’ASP.Net utilisée par le serveur ayant généré la réponse (à des fins de débogage).</span><span class="sxs-lookup"><span data-stu-id="d3c77-161">The version of ASP.Net used by the server that generated the response (for debugging purposes).</span></span>|
|<span data-ttu-id="d3c77-162">**X-Powered-By**</span><span class="sxs-lookup"><span data-stu-id="d3c77-162">**X-Powered-By**</span></span>|<span data-ttu-id="d3c77-163">Technologies utilisées dans le serveur ayant généré la réponse (à des fins de débogage).</span><span class="sxs-lookup"><span data-stu-id="d3c77-163">The technologies used in the server that generated the response (for debugging purposes).</span></span>|
|||

<br/>

<span data-ttu-id="d3c77-164">Voici les opérations de l’API Office 365 Service Communications.</span><span class="sxs-lookup"><span data-stu-id="d3c77-164">Following are the Office 365 Service Communications API operations.</span></span>


## <a name="get-services"></a><span data-ttu-id="d3c77-165">Obtenir les services</span><span class="sxs-lookup"><span data-stu-id="d3c77-165">Get Services</span></span>

<span data-ttu-id="d3c77-166">Renvoie la liste des services abonnés.</span><span class="sxs-lookup"><span data-stu-id="d3c77-166">Returns the list of subscribed services.</span></span>

||<span data-ttu-id="d3c77-167">Service</span><span class="sxs-lookup"><span data-stu-id="d3c77-167">Service</span></span>|<span data-ttu-id="d3c77-168">Description</span><span class="sxs-lookup"><span data-stu-id="d3c77-168">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="d3c77-169">**Path**</span><span class="sxs-lookup"><span data-stu-id="d3c77-169">**Path**</span></span>| `/Services`||
|<span data-ttu-id="d3c77-170">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="d3c77-170">**Query-option**</span></span>|<span data-ttu-id="d3c77-171">$select</span><span class="sxs-lookup"><span data-stu-id="d3c77-171">$select</span></span>|<span data-ttu-id="d3c77-172">Sélectionnez un sous-ensemble de propriétés.</span><span class="sxs-lookup"><span data-stu-id="d3c77-172">Pick a subset of properties.</span></span>|
|<span data-ttu-id="d3c77-173">**Response**</span><span class="sxs-lookup"><span data-stu-id="d3c77-173">**Response**</span></span>|<span data-ttu-id="d3c77-174">Liste des entités « Service »</span><span class="sxs-lookup"><span data-stu-id="d3c77-174">List of "Service" entities</span></span>|<span data-ttu-id="d3c77-175">L’entité « Service » contient « Id » (chaîne), « DisplayName » (chaîne) et « FeatureNames » (liste de chaînes).</span><span class="sxs-lookup"><span data-stu-id="d3c77-175">"Service" entity contains "Id" (String), "DisplayName" (String), and "FeatureNames" (list of Strings).</span></span>|
||||

### <a name="sample-request"></a><span data-ttu-id="d3c77-176">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="d3c77-176">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Services 
Authorization: Bearer {AAD_Bearer_JWT_Token}

```

### <a name="sample-response"></a><span data-ttu-id="d3c77-177">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="d3c77-177">Sample response</span></span>

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


## <a name="get-current-status"></a><span data-ttu-id="d3c77-178">Obtenir l’état actuel</span><span class="sxs-lookup"><span data-stu-id="d3c77-178">Get Current Status</span></span>

<span data-ttu-id="d3c77-179">Renvoie l’état du service au cours des 24 heures précédentes.</span><span class="sxs-lookup"><span data-stu-id="d3c77-179">Returns the status of the service over the previous 24 hours.</span></span>

> [!NOTE] 
> <span data-ttu-id="d3c77-180">La réponse du service contient l’état et les éventuels incidents au cours des 24 heures précédentes.</span><span class="sxs-lookup"><span data-stu-id="d3c77-180">The service response will contain the status and any incidents within the previous 24 hours.</span></span> <span data-ttu-id="d3c77-181">La valeur StatusDate ou StatusTime renvoyée sera exactement 24 heures dans le passé.</span><span class="sxs-lookup"><span data-stu-id="d3c77-181">The StatusDate or StatusTime value returned will be exactly 24 hours in the past.</span></span> <span data-ttu-id="d3c77-182">Pour obtenir la dernière mise à jour d’un incident particulier, utilisez la fonctionnalité Obtenir les messages et lisez la valeur LastUpdatedTime de l’enregistrement de la réponse qui correspond à votre ID d’incident.</span><span class="sxs-lookup"><span data-stu-id="d3c77-182">To get the last update for a particular incident, use the Get Messages functionality and read the LastUpdatedTime value from the response record that matches your incident ID.</span></span> <br/>

<br/>

||<span data-ttu-id="d3c77-183">Service</span><span class="sxs-lookup"><span data-stu-id="d3c77-183">Service</span></span>|<span data-ttu-id="d3c77-184">Description</span><span class="sxs-lookup"><span data-stu-id="d3c77-184">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="d3c77-185">**Path**</span><span class="sxs-lookup"><span data-stu-id="d3c77-185">**Path**</span></span>| `/CurrentStatus`||
|<span data-ttu-id="d3c77-186">**Filter**</span><span class="sxs-lookup"><span data-stu-id="d3c77-186">**Filter**</span></span>|<span data-ttu-id="d3c77-187">Charge de travail</span><span class="sxs-lookup"><span data-stu-id="d3c77-187">Workload</span></span>|<span data-ttu-id="d3c77-188">Filtrez par charge de travail (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="d3c77-188">Filter by workload (String, default: all).</span></span>|
|<span data-ttu-id="d3c77-189">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="d3c77-189">**Query-option**</span></span>|<span data-ttu-id="d3c77-190">$select</span><span class="sxs-lookup"><span data-stu-id="d3c77-190">$select</span></span>|<span data-ttu-id="d3c77-191">Sélectionnez un sous-ensemble de propriétés.</span><span class="sxs-lookup"><span data-stu-id="d3c77-191">Pick a subset of properties.</span></span>|
|<span data-ttu-id="d3c77-192">**Response**</span><span class="sxs-lookup"><span data-stu-id="d3c77-192">**Response**</span></span>|<span data-ttu-id="d3c77-193">Liste des entités « WorkloadStatus ».</span><span class="sxs-lookup"><span data-stu-id="d3c77-193">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="d3c77-194">L’entité « WorkloadStatus » contient « Id » (chaîne), « Workload » (chaîne), « StatusTime »(DateTimeOffset), « WorkloadDisplayName » (chaîne), « Status » (chaîne), « IncidentIds » (liste de chaînes) et FeatureGroupStatusCollection (liste des « FeatureStatus »).</span><span class="sxs-lookup"><span data-stu-id="d3c77-194">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="d3c77-195">L’entité « FeatureStatus » contient « Feature » (chaîne), « FeatureGroupDisplayName » (chaîne) et « FeatureStatus » (chaîne).</span><span class="sxs-lookup"><span data-stu-id="d3c77-195">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|
||||

### <a name="sample-request"></a><span data-ttu-id="d3c77-196">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="d3c77-196">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/CurrentStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a><span data-ttu-id="d3c77-197">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="d3c77-197">Sample response</span></span>

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

### <a name="status-definitions"></a><span data-ttu-id="d3c77-198">Définitions des états</span><span class="sxs-lookup"><span data-stu-id="d3c77-198">Status definitions</span></span>

<span data-ttu-id="d3c77-199">Les définitions d’état englobent les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d3c77-199">The status definitions include the following values:</span></span> 

- <span data-ttu-id="d3c77-200">Investigating</span><span class="sxs-lookup"><span data-stu-id="d3c77-200">Investigating</span></span>
- <span data-ttu-id="d3c77-201">ServiceDegradation</span><span class="sxs-lookup"><span data-stu-id="d3c77-201">ServiceDegradation</span></span>
- <span data-ttu-id="d3c77-202">ServiceInterruption</span><span class="sxs-lookup"><span data-stu-id="d3c77-202">ServiceInterruption</span></span> 
- <span data-ttu-id="d3c77-203">RestoringService</span><span class="sxs-lookup"><span data-stu-id="d3c77-203">RestoringService</span></span>
- <span data-ttu-id="d3c77-204">ExtendedRecovery</span><span class="sxs-lookup"><span data-stu-id="d3c77-204">ExtendedRecovery</span></span>
- <span data-ttu-id="d3c77-205">ServiceRestored</span><span class="sxs-lookup"><span data-stu-id="d3c77-205">ServiceRestored</span></span>
- <span data-ttu-id="d3c77-206">PostIncidentReportPublished</span><span class="sxs-lookup"><span data-stu-id="d3c77-206">PostIncidentReportPublished</span></span> 
- <span data-ttu-id="d3c77-207">VerifyingService</span><span class="sxs-lookup"><span data-stu-id="d3c77-207">VerifyingService</span></span>
- <span data-ttu-id="d3c77-208">ServiceOperational</span><span class="sxs-lookup"><span data-stu-id="d3c77-208">ServiceOperational</span></span>

<span data-ttu-id="d3c77-209">Pour obtenir une liste et une description à jour de ces définitions d’état, voir [Vérifier l’état du service Office 365](https://docs.microsoft.com/office365/enterprise/view-service-health#status-definitions).</span><span class="sxs-lookup"><span data-stu-id="d3c77-209">For an up-to-date list and description of these status definitions, see [How to check Office 365 service health](https://docs.microsoft.com/office365/enterprise/view-service-health#status-definitions).</span></span>


## <a name="get-historical-status"></a><span data-ttu-id="d3c77-210">Obtenir l’état de l’historique</span><span class="sxs-lookup"><span data-stu-id="d3c77-210">Get Historical Status</span></span>

<span data-ttu-id="d3c77-211">Renvoie l’état historique du service, par jour, sur un intervalle de temps donné.</span><span class="sxs-lookup"><span data-stu-id="d3c77-211">Returns the historical status of the service, by day, over a certain time range.</span></span>

||<span data-ttu-id="d3c77-212">Service</span><span class="sxs-lookup"><span data-stu-id="d3c77-212">Service</span></span>|<span data-ttu-id="d3c77-213">Description</span><span class="sxs-lookup"><span data-stu-id="d3c77-213">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="d3c77-214">**Path**</span><span class="sxs-lookup"><span data-stu-id="d3c77-214">**Path**</span></span>| `/HistoricalStatus`||
|<span data-ttu-id="d3c77-215">**Filters**</span><span class="sxs-lookup"><span data-stu-id="d3c77-215">**Filters**</span></span>|<span data-ttu-id="d3c77-216">Charge de travail</span><span class="sxs-lookup"><span data-stu-id="d3c77-216">Workload</span></span>|<span data-ttu-id="d3c77-217">Filtrez par charge de travail (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="d3c77-217">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="d3c77-218">StatusTime</span><span class="sxs-lookup"><span data-stu-id="d3c77-218">StatusTime</span></span>|<span data-ttu-id="d3c77-219">Filtrez par jour supérieur à StatusTime (DateTimeOffset, valeur par défaut : ge CurrentTime - 7 jours).</span><span class="sxs-lookup"><span data-stu-id="d3c77-219">Filter by days greater than StatusTime (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
|<span data-ttu-id="d3c77-220">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="d3c77-220">**Query-option**</span></span>|<span data-ttu-id="d3c77-221">$select</span><span class="sxs-lookup"><span data-stu-id="d3c77-221">$select</span></span>|<span data-ttu-id="d3c77-222">Sélectionnez un sous-ensemble de propriétés.</span><span class="sxs-lookup"><span data-stu-id="d3c77-222">Pick a subset of properties.</span></span>|
|<span data-ttu-id="d3c77-223">**Response**</span><span class="sxs-lookup"><span data-stu-id="d3c77-223">**Response**</span></span>|<span data-ttu-id="d3c77-224">Liste des entités « WorkloadStatus ».</span><span class="sxs-lookup"><span data-stu-id="d3c77-224">List of "WorkloadStatus" entities.</span></span>|<span data-ttu-id="d3c77-225">L’entité « WorkloadStatus » contient « Id » (chaîne), « Workload » (chaîne), « StatusTime »(DateTimeOffset), « WorkloadDisplayName » (chaîne), « Status » (chaîne), « IncidentIds » (liste de chaînes) et FeatureGroupStatusCollection (liste des « FeatureStatus »).</span><span class="sxs-lookup"><span data-stu-id="d3c77-225">"WorkloadStatus" entity contains "Id" (String), "Workload" (String), "StatusTime"(DateTimeOffset), "WorkloadDisplayName" (String), "Status" (String), "IncidentIds" (list of Strings), and FeatureGroupStatusCollection (list of "FeatureStatus").</span></span><br/><br/><span data-ttu-id="d3c77-226">L’entité « FeatureStatus » contient « Feature » (chaîne), « FeatureGroupDisplayName » (chaîne) et « FeatureStatus » (chaîne).</span><span class="sxs-lookup"><span data-stu-id="d3c77-226">"FeatureStatus" entity contains "Feature" (String), "FeatureGroupDisplayName" (String), and "FeatureStatus" (String).</span></span>|
||||

### <a name="sample-request"></a><span data-ttu-id="d3c77-227">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="d3c77-227">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/HistoricalStatus
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a><span data-ttu-id="d3c77-228">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="d3c77-228">Sample response</span></span>

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

## <a name="get-messages"></a><span data-ttu-id="d3c77-229">Obtenir les messages</span><span class="sxs-lookup"><span data-stu-id="d3c77-229">Get Messages</span></span>

<span data-ttu-id="d3c77-230">Renvoie les messages sur le service sur un intervalle de temps donné.</span><span class="sxs-lookup"><span data-stu-id="d3c77-230">Returns the messages about the service over a certain time range.</span></span> <span data-ttu-id="d3c77-231">Utilisez le filtre de type pour filtrer les messages « Incident de service », « Maintenance planifiée » ou « Centre de messages ».</span><span class="sxs-lookup"><span data-stu-id="d3c77-231">Use the type filter to filter for "Service Incident", "Planned Maintenance", or "Message Center" messages.</span></span>

||<span data-ttu-id="d3c77-232">Service</span><span class="sxs-lookup"><span data-stu-id="d3c77-232">Service</span></span>|<span data-ttu-id="d3c77-233">Description</span><span class="sxs-lookup"><span data-stu-id="d3c77-233">Description</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="d3c77-234">**Path**</span><span class="sxs-lookup"><span data-stu-id="d3c77-234">**Path**</span></span>| `/Messages`||
|<span data-ttu-id="d3c77-235">**Filters**</span><span class="sxs-lookup"><span data-stu-id="d3c77-235">**Filters**</span></span>|<span data-ttu-id="d3c77-236">Charge de travail</span><span class="sxs-lookup"><span data-stu-id="d3c77-236">Workload</span></span>|<span data-ttu-id="d3c77-237">Filtrez par charge de travail (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="d3c77-237">Filter by workload (String, default: all).</span></span>|
||<span data-ttu-id="d3c77-238">StartTime</span><span class="sxs-lookup"><span data-stu-id="d3c77-238">StartTime</span></span>|<span data-ttu-id="d3c77-239">Filtrez par Start Time (DateTimeOffset, valeur par défaut : ge CurrentTime - 7 jours).</span><span class="sxs-lookup"><span data-stu-id="d3c77-239">Filter by Start Time (DateTimeOffset, default: ge CurrentTime - 7 days).</span></span>|
||<span data-ttu-id="d3c77-240">EndTime</span><span class="sxs-lookup"><span data-stu-id="d3c77-240">EndTime</span></span>|<span data-ttu-id="d3c77-241">Filtrez par End Time (DateTimeOffset, valeur par défaut : le CurrentTime).</span><span class="sxs-lookup"><span data-stu-id="d3c77-241">Filter by End Time (DateTimeOffset, default: le CurrentTime).</span></span>|
||<span data-ttu-id="d3c77-242">MessageType</span><span class="sxs-lookup"><span data-stu-id="d3c77-242">MessageType</span></span>|<span data-ttu-id="d3c77-243">Filtrez par MessageType (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="d3c77-243">Filter by MessageType (String, default: all).</span></span>|
||<span data-ttu-id="d3c77-244">ID</span><span class="sxs-lookup"><span data-stu-id="d3c77-244">ID</span></span>|<span data-ttu-id="d3c77-245">Filtrez par ID (chaîne, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="d3c77-245">Filter by ID (String, default: all).</span></span>|
|<span data-ttu-id="d3c77-246">**Query-option**</span><span class="sxs-lookup"><span data-stu-id="d3c77-246">**Query-option**</span></span>|<span data-ttu-id="d3c77-247">$select</span><span class="sxs-lookup"><span data-stu-id="d3c77-247">$select</span></span>|<span data-ttu-id="d3c77-248">Sélectionnez un sous-ensemble de propriétés.</span><span class="sxs-lookup"><span data-stu-id="d3c77-248">Pick a subset of properties.</span></span>|
||<span data-ttu-id="d3c77-249">$top</span><span class="sxs-lookup"><span data-stu-id="d3c77-249">$top</span></span>|<span data-ttu-id="d3c77-250">Sélectionnez le nombre de résultats le plus élevé (valeur par défaut et max $top=100).</span><span class="sxs-lookup"><span data-stu-id="d3c77-250">Pick the top number of results (default and max $top=100).</span></span>|
||<span data-ttu-id="d3c77-251">$skip</span><span class="sxs-lookup"><span data-stu-id="d3c77-251">$skip</span></span>|<span data-ttu-id="d3c77-252">Ignorez le nombre de résultats (valeur par défaut : $skip = 0).</span><span class="sxs-lookup"><span data-stu-id="d3c77-252">Skip number of results (default: $skip=0).</span></span>|
|<span data-ttu-id="d3c77-253">**Response**</span><span class="sxs-lookup"><span data-stu-id="d3c77-253">**Response**</span></span>|<span data-ttu-id="d3c77-254">Liste des entités « Message ».</span><span class="sxs-lookup"><span data-stu-id="d3c77-254">List of "Message" entities.</span></span>|<span data-ttu-id="d3c77-255">L’entité « Message » contient « Id » (chaîne), « StartTime » (DateTimeOffset), « EndTime » (DateTimeOffset), « Status » (chaîne), « Messages » (liste des entités « MessageHistory »), « LastUpdatedTime » (DateTimeOffset), « Workload » (chaîne), « WorkloadDisplayName » (chaîne), « Feature » (chaîne), « FeatureDisplayName » (chaîne), « MessageType » (Enum, valeur par défaut : all).</span><span class="sxs-lookup"><span data-stu-id="d3c77-255">"Message" entity contains "Id" (String), "StartTime" (DateTimeOffset), "EndTime" (DateTimeOffset), "Status" (String), "Messages" (list of "MessageHistory" entity), "LastUpdatedTime" (DateTimeOffset), "Workload" (String), "WorkloadDisplayName" (String), "Feature" (String), "FeatureDisplayName" (String), "MessageType" (Enum, default: all).</span></span><br/><br/><span data-ttu-id="d3c77-256">L’entité « MessageHistory » contient « PublishedTime » (DateTimeOffset) et « MessageText » (chaîne).</span><span class="sxs-lookup"><span data-stu-id="d3c77-256">"MessageHistory" entity contains "PublishedTime" (DateTimeOffset), "MessageText" (String).</span></span>|
||||

### <a name="sample-request"></a><span data-ttu-id="d3c77-257">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="d3c77-257">Sample request</span></span>

```json
GET https://manage.office.com/api/v1.0/contoso.com/ServiceComms/Messages
Authorization: Bearer {AAD_Bearer_JWT_Token}
```

### <a name="sample-response"></a><span data-ttu-id="d3c77-258">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="d3c77-258">Sample response</span></span>

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


## <a name="errors"></a><span data-ttu-id="d3c77-259">Errors</span><span class="sxs-lookup"><span data-stu-id="d3c77-259">Errors</span></span>

<span data-ttu-id="d3c77-260">Lorsque le service rencontre une erreur, il signale le code de la réponse d’erreur à l’appelant à l’aide de la syntaxe de code d’erreur HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="d3c77-260">When the service encounters an error, it reports the error response code to the caller, using standard HTTP error-code syntax.</span></span> <span data-ttu-id="d3c77-261">Selon la [spécification OData V4](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), des informations supplémentaires sont incluses dans le corps de l’appel ayant échoué en tant qu’objet JSON unique.</span><span class="sxs-lookup"><span data-stu-id="d3c77-261">As per [OData V4 specification](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part1-protocol.html), additional information is included in the body of the failed call as a single JSON object.</span></span> <span data-ttu-id="d3c77-262">Voici un exemple de corps d’erreur JSON complet :</span><span class="sxs-lookup"><span data-stu-id="d3c77-262">The following is an example of a full JSON error body:</span></span>


```json
{ 
    "error":{ 
        "code":"AF5000.  An internal server error occurred.",
        "message": "Retry the request." 
    } 
}
```

