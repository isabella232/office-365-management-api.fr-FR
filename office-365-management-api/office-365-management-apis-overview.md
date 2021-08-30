---
ms.technology: o365-service-communications
ms.TocTitle: Office 365 Management APIs overview
title: Vue d’ensemble des API de gestion d’Office 365
description: Fournit une plateforme d’extensibilité unique pour toutes les tâches de gestion des clients et des partenaires d’Office 365, y compris les communications de service, la sécurité, la conformité, le compte-rendu et l’audit.
ms.ContentId: 4fca85f9-efa6-3b4b-b10d-a07cb31f803f
ms.topic: reference (API)
ms.date: 09/28/2016
ms.localizationpriority: high
ms.openlocfilehash: 52924d518dd74f822a61977d96c5edbb7fc1e888
ms.sourcegitcommit: 13b50617b1a73f5890414087d8eabe6b2240cfb4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2021
ms.locfileid: "58510110"
---
# <a name="office-365-management-apis-overview"></a>Vue d’ensemble des API de gestion d’Office 365

Les API de gestion d’Office 365 fournissent une plateforme d’extensibilité unique pour toutes les tâches de gestion des clients et des partenaires d’Office 365, y compris les communications de service, la sécurité, la conformité, le compte-rendu et l’audit. Tous les API de gestion d’Office 365 sont cohérentes au niveau de leur conception et de leur implémentation avec la suite actuelle des API REST Office 365, utilisant des approches standard courantes, notamment OAuth v2, OData v4 et JSON. À l’instar des autres API Office 365, les applications sont enregistrées dans Azure Active Directory, permettant ainsi aux développeurs d’authentifier et d’autoriser leurs applications de façon cohérente.

Si vous avez des questions sur les API de gestion d’Office 365, posez votre question sur [Stack Overflow](http://stackoverflow.com/tags/office365), à l’aide de la balise [office365].

## <a name="office-365-service-communications-api-preview"></a>API de communications de service Office 365 (préversion)

L’API de communications de service Office 365 a été publiée en mode préversion. Elle remplace l’API de communications de service Office 365 pour fournir des informations d’état du service aux administrateurs clients et partenaires. Contrairement à la version précédente, la nouvelle API de communications de service offre une expérience de plateforme homogène, avec des API REST conçues de manière cohérente, y compris au niveau de la dénomination des URL, du format de données et de l’authentification.

De nouvelles fonctionnalités sont ajoutées à la nouvelle version de l’API uniquement, encourageant ainsi son adoption rapide par les anciens clients. Lorsque l’annonce générale de l’API de communications de service d’Office 365 a été effectuée, l’ancienne version de l’API de communications de service a commencé à être déconseillée. 

Pour la référence des opérations, consultez [Référence de l’API Office 365 Service Communications (préversion)](office-365-service-communications-api-reference.md).


## <a name="office-365-management-activity-api"></a>API Activité de gestion Office 365

L’API Activité de gestion Office 365 fournit des informations sur diverses actions et événements d’utilisateur, d’administrateur, de système et de stratégie à partir des journaux d’activité Office 365 et Azure Active Directory. Les clients et les partenaires peuvent utiliser ces informations pour créer des opérations ou améliorer les opérations existantes, la sécurité et les solutions de surveillance de la conformité pour l’entreprise. 

Pour la référence des opérations, consultez la rubrique [Référence de l’API Activité de gestion Office 365](office-365-management-activity-api-reference.md).

## <a name="see-also"></a>Voir aussi

- [Prise en main des API de gestion d’Office 365](get-started-with-office-365-management-apis.md)
- [Schéma de l’API Activité de gestion Office 365](office-365-management-activity-api-schema.md)
- [Résolution des problèmes d’API d’activités de gestion d’Office 365](troubleshooting-the-office-365-management-activity-api.md)
- [API REST Office 365](/previous-versions/office/office-365-api/how-to/platform-development-overview)
