---
ms.TocTitle: Office 365 Management APIs overview
title: Vue d’ensemble des API de gestion d’Office 365
description: Fournit une plateforme d’extensibilité unique pour toutes les tâches de gestion des clients et des partenaires d’Office 365, y compris les communications de service, la sécurité, la conformité, le compte-rendu et l’audit.
ms.ContentId: 4fca85f9-efa6-3b4b-b10d-a07cb31f803f
ms.topic: reference (API)
ms.date: 09/28/2016
localization_priority: Priority
ms.openlocfilehash: 88b7e590d769699ed186d7cecaf80e162d79a095
ms.sourcegitcommit: 36d0167805d24bbb3e2cf1a02d0f011270cc31cb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/22/2020
ms.locfileid: "41263281"
---
# <a name="office-365-management-apis-overview"></a><span data-ttu-id="37e7f-103">Vue d’ensemble des API de gestion d’Office 365</span><span class="sxs-lookup"><span data-stu-id="37e7f-103">Office 365 Management APIs overview</span></span>

<span data-ttu-id="37e7f-104">Les API de gestion d’Office 365 fournissent une plateforme d’extensibilité unique pour toutes les tâches de gestion des clients et des partenaires d’Office 365, y compris les communications de service, la sécurité, la conformité, le compte-rendu et l’audit.</span><span class="sxs-lookup"><span data-stu-id="37e7f-104">The Office 365 Management APIs provide a single extensibility platform for all Office 365 customers' and partners' management tasks, including service communications, security, compliance, reporting, and auditing.</span></span> <span data-ttu-id="37e7f-105">Tous les API de gestion d’Office 365 sont cohérentes au niveau de leur conception et de leur implémentation avec la suite actuelle des API REST Office 365, utilisant des approches standard courantes, notamment OAuth v2, OData v4 et JSON.</span><span class="sxs-lookup"><span data-stu-id="37e7f-105">All of the Office 365 Management APIs are consistent in design and implementation with the current suite of Office 365 REST APIs, using common industry-standard approaches, including OAuth v2, OData v4, and JSON.</span></span> <span data-ttu-id="37e7f-106">À l’instar des autres API Office 365, les applications sont enregistrées dans Azure Active Directory, permettant ainsi aux développeurs d’authentifier et d’autoriser leurs applications de façon cohérente.</span><span class="sxs-lookup"><span data-stu-id="37e7f-106">Like the other Office 365 APIs, applications are registered in Azure Active Directory, giving developers a consistent way to authenticate and authorize their apps.</span></span>

<span data-ttu-id="37e7f-107">Si vous avez des questions sur les API de gestion d’Office 365, posez votre question sur [Stack Overflow](http://stackoverflow.com/tags/office365), à l’aide de la balise [office365].</span><span class="sxs-lookup"><span data-stu-id="37e7f-107">If you have questions about the Office 365 Management APIs, post your question on [Stack Overflow](http://stackoverflow.com/tags/office365), using the [office365] tag.</span></span>

## <a name="office-365-service-communications-api-preview"></a><span data-ttu-id="37e7f-108">API de communications de service Office 365 (préversion)</span><span class="sxs-lookup"><span data-stu-id="37e7f-108">Office 365 Service Communications API (preview)</span></span>

<span data-ttu-id="37e7f-109">L’API de communications de service Office 365 a été publiée en mode préversion.</span><span class="sxs-lookup"><span data-stu-id="37e7f-109">The Office 365 Service Communications API has been released in preview mode.</span></span> <span data-ttu-id="37e7f-110">Elle remplace l’API de communications de service Office 365 pour fournir des informations d’état du service aux administrateurs clients et partenaires.</span><span class="sxs-lookup"><span data-stu-id="37e7f-110">It replaces the Office 365 Service Communications API to provide service health information to tenant administrators and partners.</span></span> <span data-ttu-id="37e7f-111">Contrairement à la version précédente, la nouvelle API de communications de service offre une expérience de plateforme homogène, avec des API REST conçues de manière cohérente, y compris au niveau de la dénomination des URL, du format de données et de l’authentification.</span><span class="sxs-lookup"><span data-stu-id="37e7f-111">Unlike the previous version, the new Service Communications API delivers a cohesive platform experience, with REST APIs built in a consistent fashion including URL naming, data format, and authentication.</span></span>

<span data-ttu-id="37e7f-112">De nouvelles fonctionnalités sont ajoutées à la nouvelle version de l’API uniquement, encourageant ainsi son adoption rapide par les anciens clients.</span><span class="sxs-lookup"><span data-stu-id="37e7f-112">New features are only added to the new version of the API, encouraging early adoption by legacy customers.</span></span> <span data-ttu-id="37e7f-113">Lorsque l’annonce générale de l’API de communications de service d’Office 365 a été effectuée, l’ancienne version de l’API de communications de service a commencé à être déconseillée.</span><span class="sxs-lookup"><span data-stu-id="37e7f-113">When the General Announcement of Office 365 Service Communications API was made, the older version of the Service Communications API began a period of deprecation.</span></span> 

<span data-ttu-id="37e7f-114">Pour la référence des opérations, consultez [Référence de l’API Office 365 Service Communications (préversion)](office-365-service-communications-api-reference.md).</span><span class="sxs-lookup"><span data-stu-id="37e7f-114">For the operations reference, see [Office 365 Service Communications API reference (preview)](office-365-service-communications-api-reference.md).</span></span>


## <a name="office-365-management-activity-api"></a><span data-ttu-id="37e7f-115">API Activité de gestion Office 365</span><span class="sxs-lookup"><span data-stu-id="37e7f-115">Office 365 Management Activity API</span></span>

<span data-ttu-id="37e7f-116">L’API Activité de gestion Office 365 fournit des informations sur diverses actions et événements d’utilisateur, d’administrateur, de système et de stratégie à partir des journaux d’activité Office 365 et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="37e7f-116">The Office 365 Management Activity API provides information about various user, admin, system, and policy actions and events from Office 365 and Azure Active Directory activity logs.</span></span> <span data-ttu-id="37e7f-117">Les clients et les partenaires peuvent utiliser ces informations pour créer des opérations ou améliorer les opérations existantes, la sécurité et les solutions de surveillance de la conformité pour l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="37e7f-117">Customers and partners can use this information to create new or enhance existing operations, security, and compliance-monitoring solutions for the enterprise.</span></span> 

<span data-ttu-id="37e7f-118">Pour la référence des opérations, consultez la rubrique [Référence de l’API Activité de gestion Office 365](office-365-management-activity-api-reference.md).</span><span class="sxs-lookup"><span data-stu-id="37e7f-118">For the operations reference, see [Office 365 Management Activity API reference](office-365-management-activity-api-reference.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="37e7f-119">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="37e7f-119">See also</span></span>

- [<span data-ttu-id="37e7f-120">Prise en main des API de gestion d’Office 365</span><span class="sxs-lookup"><span data-stu-id="37e7f-120">Get started with Office 365 Management APIs</span></span>](get-started-with-office-365-management-apis.md)
- [<span data-ttu-id="37e7f-121">Schéma de l’API Activité de gestion Office 365</span><span class="sxs-lookup"><span data-stu-id="37e7f-121">Office 365 Management Activity API schema</span></span>](office-365-management-activity-api-schema.md)
- [<span data-ttu-id="37e7f-122">Résolution des problèmes d’API d’activités de gestion d’Office 365</span><span class="sxs-lookup"><span data-stu-id="37e7f-122">Troubleshooting the Office 365 Management Activity API</span></span>](troubleshooting-the-office-365-management-activity-api.md)
- [<span data-ttu-id="37e7f-123">API REST Office 365</span><span class="sxs-lookup"><span data-stu-id="37e7f-123">Office 365 REST APIs</span></span>](https://docs.microsoft.com/previous-versions/office/office-365-api/how-to/platform-development-overview)

