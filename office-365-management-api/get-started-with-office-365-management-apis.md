---
ms.TocTitle: Get started with Office 365 Management APIs
title: Prise en main des API de gestion d’Office 365
description: Les API utilisent Azure AD pour fournir des services d’authentification que vous pouvez utiliser pour octroyer des droits à votre application pour y accéder.
ms.ContentId: 74137c9a-29e0-b588-6122-26f4d2c5e3fc
ms.topic: reference (API)
ms.date: 09/05/2018
ms.openlocfilehash: 87abfbe89f60710dc6c9981fa57bde4238790b1f
ms.sourcegitcommit: 525c0d0e78cc44ea8cb6a4bdce1858cb4ef91d57
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2018
ms.locfileid: "25834826"
---
# <a name="get-started-with-office-365-management-apis"></a><span data-ttu-id="29322-103">Prise en main des API de gestion d’Office 365</span><span class="sxs-lookup"><span data-stu-id="29322-103">Get started with Office 365 APIs powered by Microsoft Graph</span></span>

<span data-ttu-id="29322-104">Lorsque vous créez une application qui doit accéder à des services sécurisés tels qu’aux API de gestion d’Office 365, vous devez trouver un moyen d’indiquer au service si votre application dispose des droits appropriés pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="29322-104">When you create an application that needs access to secured services like the Office 365 Management APIs, you need to provide a way to let the service know if your application has rights to access it.</span></span> <span data-ttu-id="29322-105">Les API de gestion d’Office 365 utilisent Azure AD pour fournir des services d’authentification que vous pouvez utiliser pour octroyer des droits à votre application pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="29322-105">The Office 365 Management APIs use Azure AD to provide authentication services that you can use to grant rights for your application to access them.</span></span> 

<span data-ttu-id="29322-106">Vous devez suivre quatre étapes principales :</span><span class="sxs-lookup"><span data-stu-id="29322-106">There are four key steps:</span></span>

1. <span data-ttu-id="29322-107">**Inscrire votre application dans Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="29322-107">\*\*\*\* Register your application in Azure Active Directory</span></span> <span data-ttu-id="29322-108">Pour autoriser votre application à accéder aux API de gestion d’Office 365, vous devez inscrire votre application dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29322-108">To allow your application access to the Office 365 Management APIs, you need to register your application in Azure AD.</span></span> <span data-ttu-id="29322-109">Cela vous permet d’établir une identité pour votre application et de spécifier les niveaux d’autorisation dont elle a besoin pour accéder aux API.</span><span class="sxs-lookup"><span data-stu-id="29322-109">This allows you to establish an identity for your application and specify the permission levels it needs to access the APIs.</span></span>
    
2. <span data-ttu-id="29322-110">**Obtenir le consentement de l’administrateur client d’Office 365**.</span><span class="sxs-lookup"><span data-stu-id="29322-110">**Get Office 365 tenant admin consent**.</span></span> <span data-ttu-id="29322-111">Un administrateur client d’Office 365 doit donner explicitement son consentement pour autoriser votre application à accéder à ses données client au moyen des API de gestion d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="29322-111">An Office 365 tenant admin must explicitly grant consent to allow your application to access their tenant data by means of the Office 365 Management APIs.</span></span> <span data-ttu-id="29322-112">Le processus de consentement est une expérience basée sur le navigateur où l’administrateur client se connecte à l’**interface utilisateur de consentement d’Azure AD** et analyse les autorisations d’accès demandées par votre application, puis accorde ou refuse la demande.</span><span class="sxs-lookup"><span data-stu-id="29322-112">The consent process is a browser-based experience that requires the tenant admin to sign in to the **Azure AD consent UI** and review the access permissions that your application is requesting, and then either grant or deny the request.</span></span> <span data-ttu-id="29322-113">Une fois le consentement donné, l’interface utilisateur redirige l’utilisateur vers votre application avec un code d’autorisation dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="29322-113">After consent is granted, the UI redirects the user back to your application with an authorization code in the URL.</span></span> <span data-ttu-id="29322-114">Votre application passe un appel de service à service à Azure AD pour échanger ce code d’autorisation contre un jeton d’accès, qui contient des informations sur l’administrateur client et votre application.</span><span class="sxs-lookup"><span data-stu-id="29322-114">Your application makes a service-to-service call to Azure AD to exchange this authorization code for an access token, which contains information about both the tenant admin and your application.</span></span> <span data-ttu-id="29322-115">L’ID client doit être extrait du jeton d’accès et stocké en vue d’une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="29322-115">The tenant ID must be extracted from the access token and stored for future use.</span></span>
    
3. <span data-ttu-id="29322-116">**Demander des jetons d’accès à Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="29322-116">\*\*\*\* Request and acquire an access token from Azure AD</span></span> <span data-ttu-id="29322-117">Votre application utilise les informations d’identification la concernant comme configuré dans Azure AD pour demander régulièrement d’autres jetons d’accès pour un client ayant donné son consentement, sans aucune interaction de l’administrateur client supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="29322-117">Using your application's credentials as configured in Azure AD, your application requests additional access tokens for a consented tenant on an ongoing basis, without the need for further tenant admin interaction.</span></span> <span data-ttu-id="29322-118">Ces jetons d’accès sont appelés jetons d’application uniquement car ils n’incluent pas d’informations sur l’administrateur client.</span><span class="sxs-lookup"><span data-stu-id="29322-118">These access tokens are called app-only tokens because they do not include information about the tenant admin.</span></span>
    
4. <span data-ttu-id="29322-119">**Appeler les API de gestion d’Office 365**.</span><span class="sxs-lookup"><span data-stu-id="29322-119">**Call the Office 365 Management APIs**.</span></span> <span data-ttu-id="29322-120">Les jetons d’accès d’application uniquement sont transmis aux API de gestion d’Office 365 pour authentifier et autoriser votre application.</span><span class="sxs-lookup"><span data-stu-id="29322-120">The app-only access tokens are passed to the Office 365 Management APIs to authenticate and authorize your application.</span></span>
    
<span data-ttu-id="29322-121">Le diagramme suivant illustre la séquence des demandes de consentement et de jetons d’accès.</span><span class="sxs-lookup"><span data-stu-id="29322-121">The following diagram shows the sequence of consent and access token requests.</span></span>


![Flux d’autorisation de mise en route des API de gestion](images/authorization-flow.png)


## <a name="register-your-application-in-azure-ad"></a><span data-ttu-id="29322-123">Inscrire votre application dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="29322-123">Register your application in Azure Active Directory</span></span>

<span data-ttu-id="29322-124">Les API de gestion d’Office 365 utilisent Azure AD pour fournir une authentification sécurisée aux données client d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="29322-124">The Office 365 API services use Azure AD to provide secure authentication to users' Office 365 data.</span></span> <span data-ttu-id="29322-125">Pour accéder aux API de gestion d’Office 365, vous devez inscrire votre application dans Azure AD, et dans le cadre de la configuration, vous devez spécifier les niveaux d’autorisation nécessaires à votre application pour accéder aux API.</span><span class="sxs-lookup"><span data-stu-id="29322-125">To access the Office 365 Management APIs, you need to register your app in Azure AD, and as part of the configuration, you will specify the permission levels your app needs to access the APIs.</span></span>


### <a name="prerequisites"></a><span data-ttu-id="29322-126">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="29322-126">Prerequisites</span></span>

<span data-ttu-id="29322-127">Pour inscrire votre application dans Azure AD, vous devez avoir un abonnement à Office 365 et un abonnement à Azure qui a été associé à votre abonnement Office 365.</span><span class="sxs-lookup"><span data-stu-id="29322-127">To register your app in Azure AD, you need a subscription to Office 365 and a subscription to Azure that has been associated with your Office 365 subscription.</span></span> <span data-ttu-id="29322-128">Vous pouvez utiliser des abonnements à la version d’évaluation d’Office 365 et Azure pour commencer.</span><span class="sxs-lookup"><span data-stu-id="29322-128">You can use trial subscriptions to both Office 365 and Azure to get started.</span></span> <span data-ttu-id="29322-129">Pour plus d’informations, consultez [Bienvenue dans le programme pour les développeurs Office 365](https://docs.microsoft.com/fr-FR/office/developer-program/office-365-developer-program).</span><span class="sxs-lookup"><span data-stu-id="29322-129">For more information, see [Join the Office 365 Developer Program](https://docs.microsoft.com/fr-FR/office/developer-program/office-365-developer-program).</span></span>


### <a name="use-the-azure-management-portal-to-register-your-application-in-azure-ad"></a><span data-ttu-id="29322-130">Inscrire votre application dans Azure AD à l’aide du portail de gestion Azure</span><span class="sxs-lookup"><span data-stu-id="29322-130">Use the Azure Management Portal to register your application in Azure AD</span></span>

<span data-ttu-id="29322-131">Une fois que vous disposez d’un client Microsoft avec les abonnements appropriés, vous pouvez inscrire votre application dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29322-131">After you have a Microsoft tenant with the proper subscriptions, you can register your application in Azure AD.</span></span>

1. <span data-ttu-id="29322-132">Connectez-vous au [portail de gestion Azure](https://manage.windowsazure.com/) à l’aide des informations d’identification de votre client Microsoft qui dispose de l’abonnement à Office 365 que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="29322-132">Sign into the [Azure management portal](https://manage.windowsazure.com/), using the credential of your Microsoft tenant that has the subscription to Office 365 you wish to use.</span></span> <span data-ttu-id="29322-133">Vous pouvez également accéder au portail de gestion Azure en utilisant le lien qui s’affiche dans le volet de navigation gauche du [portail d’administration Office](https://portal.office.com/).</span><span class="sxs-lookup"><span data-stu-id="29322-133">You can also access the Azure Management Portal via a link that appears in the left navigation pane in the [Office admin portal](https://portal.office.com/).</span></span>
    
2. <span data-ttu-id="29322-134">Dans le volet de navigation gauche, sélectionnez Active Directory (1).</span><span class="sxs-lookup"><span data-stu-id="29322-134">In the left navigation panel, choose Active Directory (1).</span></span> <span data-ttu-id="29322-135">Assurez-vous que l’onglet Directory (2) est bien sélectionné, puis cliquez sur le nom du répertoire (3).</span><span class="sxs-lookup"><span data-stu-id="29322-135">Make sure the Directory tab is selected, and then click on the directory name.</span></span>
    
   ![Page d’inscription à Office 365](images/o365-sign-up-page.png)
    
    
3. <span data-ttu-id="29322-137">Sur la page du répertoire, sélectionnez **Applications**.</span><span class="sxs-lookup"><span data-stu-id="29322-137">On the directory page, select Applications.</span></span> <span data-ttu-id="29322-138">Azure AD affiche la liste des applications actuellement installées dans votre client.</span><span class="sxs-lookup"><span data-stu-id="29322-138">Azure AD displays a list of the applications currently installed in your tenancy.</span></span>
    
4. <span data-ttu-id="29322-139">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="29322-139">Choose **Add**.</span></span>
    
   ![Page d’administration d’Office 365](images/o365-admin-page.png)
    
    
5. <span data-ttu-id="29322-141">Sélectionnez **Ajouter une application développée par mon organisation**.</span><span class="sxs-lookup"><span data-stu-id="29322-141">Select **Add an application my organization is developing**.</span></span>
    
6. <span data-ttu-id="29322-142">Entrez le **NOM** de votre application et spécifiez le **Type** comme APPLICATION WEB ET/OU API WEB.</span><span class="sxs-lookup"><span data-stu-id="29322-142">Enter the **NAME** of your application and specify the **Type** as WEB APPLICATION AND/OR WEB API.</span></span>
    
7. <span data-ttu-id="29322-143">Entrez les propriétés appropriées de l’application :</span><span class="sxs-lookup"><span data-stu-id="29322-143">Enter the appropriate App properties:</span></span>
    
   - <span data-ttu-id="29322-144">**URL DE CONNEXION**.</span><span class="sxs-lookup"><span data-stu-id="29322-144">Sign-on URL</span></span> <span data-ttu-id="29322-145">URL permettant aux utilisateurs de se connecter et d’utiliser votre application.</span><span class="sxs-lookup"><span data-stu-id="29322-145">The Sign-on URL is the address of a web page where users can sign in and use your app.</span></span> <span data-ttu-id="29322-146">Vous pouvez la modifier ultérieurement selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="29322-146">You can change this later as needed.</span></span>
    
   - <span data-ttu-id="29322-147">**URI ID D’APPLICATION**.</span><span class="sxs-lookup"><span data-stu-id="29322-147">App ID URI</span></span> <span data-ttu-id="29322-148">URI utilisé comme identificateur unique logique pour votre application.</span><span class="sxs-lookup"><span data-stu-id="29322-148">The URI used as a unique logical identifier for your app.</span></span> <span data-ttu-id="29322-149">L’URI doit être dans un domaine personnalisé vérifié pour qu’un utilisateur externe puisse accorder à votre application l’accès à ses données dans Windows Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29322-149">The URI must be in a verified custom domain for an external user to grant your app access to their data in Windows Azure AD.</span></span> <span data-ttu-id="29322-150">Par exemple, si votre client Microsoft est **contoso.onmicrosoft.com**, l’URI ID D’APPLICATION peut être **https://app.contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="29322-150">For example, if your Microsoft tenant is **contoso.onmicrosoft.com**, the APP ID URI could be **https://app.contoso.onmicrosoft.com**.</span></span>
    
8. <span data-ttu-id="29322-151">Votre application est désormais inscrite auprès d’Azure Active Directory et un ID client lui a été affecté.</span><span class="sxs-lookup"><span data-stu-id="29322-151">Your app is now registered with Azure AD, and has been assigned a client ID.</span></span> <span data-ttu-id="29322-152">Toutefois, il reste plusieurs aspects importants de votre application à configurer.</span><span class="sxs-lookup"><span data-stu-id="29322-152">However, there are several important aspects of your app left to configure.</span></span>
    

### <a name="configure-your-application-properties-in-azure-ad"></a><span data-ttu-id="29322-153">Configurer les propriétés de votre application dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="29322-153">Configure your application properties in Azure AD</span></span>

<span data-ttu-id="29322-154">Maintenant que votre application est inscrite, vous devez spécifier plusieurs propriétés importantes qui déterminent comment fonctionne votre application dans Azure AD et comment les administrateurs clients donnent leur consentement pour permettre à votre application d’accéder à leurs données à l’aide des API de gestion d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="29322-154">Now that your application is registered, there are several important properties you must specify that determine how your application functions within Azure AD and how tenant admins will grant consent to allow your application to access their data by using the Office 365 Management APIs.</span></span>

<span data-ttu-id="29322-155">Pour plus d’informations sur la configuration de l’application Azure AD en général, reportez-vous à [Objets application et principal du service dans Azure Active Directory](https://docs.microsoft.com/fr-FR/azure/active-directory/develop/active-directory-application-objects).</span><span class="sxs-lookup"><span data-stu-id="29322-155">For more information about Azure AD application configuration in general, see [Application Object Properties](https://docs.microsoft.com/fr-FR/azure/active-directory/develop/active-directory-application-objects).</span></span>


1. <span data-ttu-id="29322-156">**ID CLIENT**.</span><span class="sxs-lookup"><span data-stu-id="29322-156">Client Id:</span></span> <span data-ttu-id="29322-157">Cette valeur est générée automatiquement par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29322-157">This value is automatically generated by Azure AD.</span></span> <span data-ttu-id="29322-158">Votre application utilisera cette valeur lors de la demande de consentement aux administrateurs clients et de la demande de jetons d’application uniquement à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29322-158">Your application will use this value when requesting consent from tenant admins and when requesting app-only tokens from Azure AD.</span></span>
    
2. <span data-ttu-id="29322-159">**L’APPLICATION EST MUTUALISÉE**.</span><span class="sxs-lookup"><span data-stu-id="29322-159">**APPLICATION IS MULTI-TENANT**.</span></span> <span data-ttu-id="29322-160">Cette propriété doit être définie sur **OUI** pour permettre aux administrateurs clients de donner leur consentement à votre application pour accéder à leurs données à l’aide des API de gestion d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="29322-160">This property must be set to **YES** to allow tenant admins to grant consent to your app to access their data by using the Office 365 Management APIs.</span></span> <span data-ttu-id="29322-161">Si cette propriété est définie sur **NON**, votre application pourra accéder uniquement aux données de votre propre client.</span><span class="sxs-lookup"><span data-stu-id="29322-161">If this property is set to **NO**, your application will only be able to access your own tenant's data.</span></span>
    
3. <span data-ttu-id="29322-162">**URL DE RÉPONSE**.</span><span class="sxs-lookup"><span data-stu-id="29322-162">Reply URL</span></span> <span data-ttu-id="29322-163">Il s’agit de l’URL vers laquelle un administrateur client sera dirigé après avoir donné son consentement pour autoriser votre application à accéder à ses données à l’aide des API de gestion d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="29322-163">This is the URL that a tenant admin will be redirected to after granting consent to allow your application to access their data by using the Office 365 Management APIs.</span></span> <span data-ttu-id="29322-164">Vous pouvez configurer plusieurs URL de réponse selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="29322-164">You can configure multiple reply URLs as needed.</span></span> <span data-ttu-id="29322-165">Azure définit automatiquement la première URL pour qu’elle corresponde à l’URL de connexion que vous avez spécifiée lorsque vous avez créé l’application, mais vous pouvez modifier cette valeur selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="29322-165">Azure automatically sets the first one to match the sign-on URL you specified when you created the application, but you can change this value as needed.</span></span>
    
<span data-ttu-id="29322-166">Veillez à choisir **Enregistrer** après avoir modifié ces propriétés.</span><span class="sxs-lookup"><span data-stu-id="29322-166">Be sure to choose **Save** after making any changes to these properties.</span></span>


### <a name="generate-a-new-key-for-your-application"></a><span data-ttu-id="29322-167">Générer une nouvelle clé pour votre application</span><span class="sxs-lookup"><span data-stu-id="29322-167">Generate a new app secret for your web application</span></span>

<span data-ttu-id="29322-168">Les clés, également appelées clés secrètes client, sont utilisées lors de l’échange d’un code d’autorisation contre un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="29322-168">Keys, also known as client secrets, are used when exchanging an authorization code for an access token.</span></span>


1. <span data-ttu-id="29322-169">Dans le portail de gestion Azure, sélectionnez votre application et choisissez **Configurer** dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="29322-169">In the Azure Management Portal, select your application and choose **Configure** in the top menu.</span></span> <span data-ttu-id="29322-170">Faites défiler jusqu'à **clés**.</span><span class="sxs-lookup"><span data-stu-id="29322-170">Scroll down to **keys**.</span></span>
    
2. <span data-ttu-id="29322-171">Sélectionnez la durée de votre clé, puis choisissez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="29322-171">Select the duration for your key, and choose **Save**.</span></span>
    
   ![Page d’abonnement Azure](images/azure-subscription-page.png)
    
    
3. <span data-ttu-id="29322-173">Azure affiche la question secrète de l’application uniquement après l’avoir enregistrée.</span><span class="sxs-lookup"><span data-stu-id="29322-173">Azure displays the app secret only after saving it.</span></span> <span data-ttu-id="29322-174">Sélectionnez l’icône Presse-papiers pour copier la clé secrète client dans le Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="29322-174">Click the Clipboard icon to copy the client secret to the Clipboard.</span></span>
    
   ![Page du portail Azure](images/azure-portal-page.png)

   > [!IMPORTANT] 
   > <span data-ttu-id="29322-176">Azure affiche uniquement la clé secrète client au moment où vous l’avez initialement générée.</span><span class="sxs-lookup"><span data-stu-id="29322-176">Important Azure only displays the client secret at the time you initially generate it.</span></span> <span data-ttu-id="29322-177">Vous ne pouvez pas revenir à cette page et récupérer la clé secrète client ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="29322-177">You cannot navigate back to this page and retrieve the client secret later.</span></span>

### <a name="configure-an-x509-certificate-to-enable-service-to-service-calls"></a><span data-ttu-id="29322-178">Configurer un certificat X.509 pour activer les appels de service à service</span><span class="sxs-lookup"><span data-stu-id="29322-178">Configure an X.509 certificate to enable service-to-service calls</span></span>

<span data-ttu-id="29322-179">Une application qui est en cours d’exécution en arrière-plan, comme un démon ou un service, peut utiliser les informations d’identification client pour demander des jetons d’accès d’application uniquement sans demander plusieurs fois le consentement à l’administrateur client une fois que le consentement initial a été donné.</span><span class="sxs-lookup"><span data-stu-id="29322-179">An application that is running in the background, such as a daemon or service, can use client credentials to request app-only access tokens without repeatedly requesting consent from the tenant admin after initial consent is granted.</span></span> 

<span data-ttu-id="29322-180">Pour plus d’informations, consultez la rubrique relative aux [appels de service à service à l’aide des informations d’identification client](https://msdn.microsoft.com/fr-FR/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="29322-180">For details about the authentication flow, see [Service to Service Calls Using Client Credentials](https://msdn.microsoft.com/fr-FR/library/azure/dn645543.aspx).</span></span>

<span data-ttu-id="29322-181">Vous devez configurer un certificat X.509 avec votre application à utiliser comme informations d’identification client lorsque vous demandez des jetons d’accès d’application uniquement à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29322-181">You must configure an X.509 certificate with your application to be used as client credentials when requesting app-only access tokens from Azure AD.</span></span> <span data-ttu-id="29322-182">Le processus se déroule en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="29322-182">There are two main components to the IRM migration process:</span></span>

- <span data-ttu-id="29322-183">Obtenir un certificat X.509.</span><span class="sxs-lookup"><span data-stu-id="29322-183">Obtain an X.509 certificate.</span></span> <span data-ttu-id="29322-184">Vous pouvez utiliser un certificat auto-signé ou un certificat émis par une autorité de certification approuvée publiquement.</span><span class="sxs-lookup"><span data-stu-id="29322-184">You can use a self-signed certificate or a certificate issued by publicly trusted certificate authority.</span></span>
    
- <span data-ttu-id="29322-185">Modifier votre manifeste d’application pour inclure l’empreinte et la clé publique de votre certificat.</span><span class="sxs-lookup"><span data-stu-id="29322-185">Modify your application manifest to include the thumbprint and public key of your certificate.</span></span>
    
<span data-ttu-id="29322-186">Les instructions suivantes montrent comment utiliser l’outil _makecert_ du Kit de développement logiciel (SDK) Windows ou Visual Studio pour générer un certificat auto-signé et exporter la clé publique dans un fichier codé en base 64.</span><span class="sxs-lookup"><span data-stu-id="29322-186">The following instructions show you how to use the Visual Studio or Windows SDK _makecert_ tool to generate a self-signed certificate and export the public key to a base64-encoded file.</span></span>


1. <span data-ttu-id="29322-187">Dans la ligne de commande, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="29322-187">On the command line, run the following command:</span></span>
    
   ```
    makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 03/15/2015 -e 03/15/2017 -ss my -len 2048
   ```

   > [!NOTE] 
   > <span data-ttu-id="29322-188">Lorsque vous générez le certificat X.509, vérifiez que la longueur minimale de la clé est 2048.</span><span class="sxs-lookup"><span data-stu-id="29322-188">When you are generating the X.509 certificate, make sure the key length is at least 2048.</span></span> <span data-ttu-id="29322-189">Les raccourcis clavier ne sont pas acceptés en tant que clés valides.</span><span class="sxs-lookup"><span data-stu-id="29322-189">Shorter key length are not accepted as valid keys.</span></span>

2. <span data-ttu-id="29322-190">Ouvrez le composant logiciel enfichable Certificats MMC et connectez-vous à votre compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29322-190">Open the Certificates management console snap-in and connect to your user account.</span></span> 
    
3. <span data-ttu-id="29322-191">Recherchez le nouveau certificat dans le dossier personnel et exportez la clé publique dans un fichier codé en base 64 (par exemple, mycompanyname.cer).</span><span class="sxs-lookup"><span data-stu-id="29322-191">Find the new certificate in the Personal folder and export the public key to a base64-encoded file (for example, mycompanyname.cer).</span></span> <span data-ttu-id="29322-192">Votre application utilisera ce certificat pour communiquer avec Azure AD. Par conséquent, assurez-vous de conserver l’accès à la clé privée également.</span><span class="sxs-lookup"><span data-stu-id="29322-192">Your application will use this certificate to communicate with Azure AD, so make sure you retain access to the private key as well.</span></span>
    
   > [!NOTE] 
   > <span data-ttu-id="29322-193">Vous pouvez utiliser Windows PowerShell pour extraire l’empreinte et la clé publique codée en base 64.</span><span class="sxs-lookup"><span data-stu-id="29322-193">You can use Windows PowerShell to extract the thumbprint and base64-encoded public key.</span></span> <span data-ttu-id="29322-194">D’autres plateformes fournissent des outils similaires pour récupérer les propriétés des certificats.</span><span class="sxs-lookup"><span data-stu-id="29322-194">Other platforms provide similar tools to retrieve properties of certificates.</span></span>

4. <span data-ttu-id="29322-195">Dans l’invite Windows PowerShell, tapez et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="29322-195">From the Windows PowerShell prompt, type and run the following cmdlets:</span></span>
    
   ```powershell
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $cer.Import("mycer.cer")
    $bin = $cer.GetRawCertData()
    $base64Value = [System.Convert]::ToBase64String($bin)
    $bin = $cer.GetCertHash()
    $base64Thumbprint = [System.Convert]::ToBase64String($bin)
    $keyid = [System.Guid]::NewGuid().ToString()
   ```

5. <span data-ttu-id="29322-196">Stockez les valeurs pour `$base64Thumbprint`, `$base64Value` et `$keyid` à utiliser lorsque vous mettez à jour le manifeste de votre application dans les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="29322-196">Store the values for `$base64Thumbprint`, `$base64Value`, and `$keyid` to be used when you update your application manifest in the next set of steps.</span></span>
    
   <span data-ttu-id="29322-197">Utilisez à présent les valeurs extraites du certificat et l’ID de la clé générée pour mettre à jour le manifeste de votre application dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29322-197">Using the values extracted from the certificate and the generated key ID, you must now update your application manifest in Azure AD.</span></span>
    
6. <span data-ttu-id="29322-198">Dans le portail de gestion Azure, sélectionnez votre application et choisissez **Configurer** dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="29322-198">In the Azure Management Portal, select your application and choose **Configure** in the top menu.</span></span>
    
7. <span data-ttu-id="29322-199">Dans la barre de commandes, sélectionnez **Gérer le manifeste**, puis **Télécharger le manifeste**.</span><span class="sxs-lookup"><span data-stu-id="29322-199">In the command bar, choose **Manage manifest**, and then choose **Download Manifest**.</span></span>
    
   ![Affichage de certificats de ligne de commande](images/command-line-certificate-display.png)
    
    
8. <span data-ttu-id="29322-201">Ouvrez le manifeste téléchargé pour le modifier et remplacez la propriété vide KeyCredentials par le fichier JSON suivant :</span><span class="sxs-lookup"><span data-stu-id="29322-201">Open the downloaded file for editing and replace the empty KeyCredentials property with the following JSON:</span></span>
    
   ```json
      "keyCredentials": [
        {
            "customKeyIdentifier" : "$base64Thumbprint_from_above",
            "keyId": "$keyid_from_above",
            "type": "AsymmetricX509Cert",
            "usage": "Verify",
            "value": "$base64Value_from_above"
        }
    ],
   ```


   > [!NOTE] 
   > <span data-ttu-id="29322-202">La propriété [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) est une collection qui permet de charger plusieurs certificats X.509 pour des scénarios de substitution ou de supprimer des certificats pour des scénarios de compromission.</span><span class="sxs-lookup"><span data-stu-id="29322-202">The [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) property is a collection, making it possible to upload multiple X.509 certificates for rollover scenarios or delete certificates for compromise scenarios.</span></span>

9. <span data-ttu-id="29322-203">Enregistrez vos modifications et chargez le manifeste mis à jour en cliquant sur **Gérer le manifeste** dans la barre de commandes, puis sélectionnez **Télécharger le manifeste**, naviguez jusqu’à votre fichier manifeste mis à jour et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="29322-203">Save your changes, and upload the updated app manifest file by clicking **Manage manifest** in the command bar, selecting **Upload manifest**, browsing to your updated manifest file and then selecting it.</span></span>
    

### <a name="specify-the-permissions-your-app-requires-to-access-the-office-365-management-apis"></a><span data-ttu-id="29322-204">Spécifier les autorisations requises par votre application pour accéder aux API de gestion d’Office 365</span><span class="sxs-lookup"><span data-stu-id="29322-204">Specify the permissions your app requires to access the Office 365 Management APIs</span></span>

<span data-ttu-id="29322-205">Enfin, vous devrez spécifier exactement les autorisations requises par votre application pour les API de gestion d’Office 365.</span><span class="sxs-lookup"><span data-stu-id="29322-205">Finally, you'll need to specify exactly what permissions your app requires of the Office 365 APIs.</span></span> <span data-ttu-id="29322-206">Pour ce faire, vous ajoutez l’accès aux API de gestion d’Office 365 à votre application, puis vous spécifiez les autorisations dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="29322-206">To do so, you add access to the Office 365 service containing the API you require to your app, and then specify the permission(s) you need from the APIs in that service.</span></span>


1. <span data-ttu-id="29322-207">Dans le portail de gestion Azure, sélectionnez votre application et choisissez **Configurer** dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="29322-207">In the Azure Management Portal, select your application and choose **Configure** in the top menu.</span></span> <span data-ttu-id="29322-208">Faites défiler vers le bas jusqu’à **Autorisations accordées à d’autres applications**, et sélectionnez **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="29322-208">Scroll down to the **permissions to other applications** section and click the **Add application** button.</span></span>
    
   ![Page Azure AD](images/azure-ad-page.png)
    
    
2. <span data-ttu-id="29322-210">Sélectionnez **API de gestion d’Office 365** (1) pour que l’élément apparaisse dans la colonne **Sélectionné** (2), puis cochez la case située en bas à droite (3) pour enregistrer votre sélection et revenir à la page de configuration principale pour votre application.</span><span class="sxs-lookup"><span data-stu-id="29322-210">Select the **Office 365 Management APIs** (1) so that it appears in the **Selected** column (2), and then select the check mark in the lower right (3) to save your selection and return to the main configuration page for your application.</span></span>
    
   ![Page Azure AD - Applications](images/azure-ad-apps-page.png)
    
    
3. <span data-ttu-id="29322-212">Les API de gestion d’Office apparaissent maintenant dans la liste des applications pour lesquelles votre application requiert des autorisations.</span><span class="sxs-lookup"><span data-stu-id="29322-212">The Office Management APIs now appear in the list of applications to which your application requires permissions.</span></span> <span data-ttu-id="29322-213">Sous **Autorisations d’application** et **Autorisations déléguées**, sélectionnez les autorisations requises par votre application.</span><span class="sxs-lookup"><span data-stu-id="29322-213">Under both **Application Permissions** and **Delegated Permissions**, select the permissions your application requires.</span></span> <span data-ttu-id="29322-214">Reportez-vous à la référence de l’API spécifique pour plus d’informations sur chaque autorisation.</span><span class="sxs-lookup"><span data-stu-id="29322-214">Refer to the specific API reference for more details about each permission.</span></span>  

   > [!NOTE] 
   > <span data-ttu-id="29322-215">Il existe actuellement quatre autorisations inutilisées relatives aux rapports d’activité et à l’intelligence des menaces qui seront supprimées à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="29322-215">There are currently four unused permissions related to activity reports and threat intelligence that will be removed in the future.</span></span> <span data-ttu-id="29322-216">Ne sélectionnez pas ces autorisations car elles sont inutiles.</span><span class="sxs-lookup"><span data-stu-id="29322-216">Do not select any of these permissions because they are unnecessary.</span></span>
    
   ![Boîte de dialogue Ajouter une application](images/add-an-application-dialog.png)
    
    
4. <span data-ttu-id="29322-218">Cliquez sur **Enregistrer** pour enregistrer la configuration.</span><span class="sxs-lookup"><span data-stu-id="29322-218">Choose **Save** to save the rule.</span></span>
    

## <a name="get-office-365-tenant-admin-consent"></a><span data-ttu-id="29322-219">Obtenir le consentement de l’administrateur client d’Office 365</span><span class="sxs-lookup"><span data-stu-id="29322-219">Get Office 365 tenant admin consent</span></span>

<span data-ttu-id="29322-220">Maintenant que votre application est configurée avec les autorisations requises pour utiliser les API de gestion d’Office 365, un administrateur client doit octroyer ces autorisations explicitement à votre application pour accéder aux données de son client à l’aide des API.</span><span class="sxs-lookup"><span data-stu-id="29322-220">Now that your application is configured with the permissions it needs to use the Office 365 Management APIs, a tenant admin must explicitly grant your application these permissions in order to access their tenant's data by using the APIs.</span></span> <span data-ttu-id="29322-221">Pour donner son consentement, l’administrateur client doit se connecter à Azure AD à l’aide de l’URL suivante spécialement créée, où il peut revoir les autorisations demandées de votre application.</span><span class="sxs-lookup"><span data-stu-id="29322-221">To grant consent, the tenant admin must sign in to Azure AD by using the following specially constructed URL, where they can review your application's requested permissions.</span></span> <span data-ttu-id="29322-222">Cette étape n’est pas obligatoire lorsque vous utilisez les API pour accéder aux données de votre propre client.</span><span class="sxs-lookup"><span data-stu-id="29322-222">This step is not required when using the APIs to access data from your own tenant.</span></span>


```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id={your_client_id}&redirect_uri={your_redirect_url }
```

<span data-ttu-id="29322-223">L’URL de redirection doit correspondre à l’une des URL de réponse configurées pour votre application dans Azure AD ou être un chemin d’accès secondaire sous l’une d’elles.</span><span class="sxs-lookup"><span data-stu-id="29322-223">The redirect URL must match or be a sub-path under one of the Reply URLs configured for your application in Azure AD.</span></span>

<span data-ttu-id="29322-224">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="29322-224">For example:</span></span>

```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e&redirect_uri=http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F
```

<span data-ttu-id="29322-225">Vous pouvez tester l’URL de consentement en la collant dans un navigateur et en vous connectant à l’aide des informations d’identification d’un administrateur Office 365 pour un client autre que celui que vous avez utilisé pour inscrire l’application.</span><span class="sxs-lookup"><span data-stu-id="29322-225">You can test the consent URL by pasting it into a browser and signing in using the credentials of an Office 365 admin for a tenant other than the tenant that you used to register the application.</span></span> <span data-ttu-id="29322-226">Vous verrez la demande d’octroi d’autorisation à votre application pour utiliser les API de gestion d’Office.</span><span class="sxs-lookup"><span data-stu-id="29322-226">You will see the request to grant your application permission to use the Office Management APIs.</span></span>


![Page Azure AD - Application ajoutée](images/azure-ad-app-added-page.png)

<span data-ttu-id="29322-228">Après avoir sélectionné **Accepter**, vous êtes redirigé vers la page spécifiée où se trouve un code dans la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="29322-228">After choosing **Accept**, you are redirected to the specified page, and there will be a code in the query string.</span></span> 

<span data-ttu-id="29322-229">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="29322-229">For example:</span></span>

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

<span data-ttu-id="29322-230">Votre application utilise ce code d’autorisation pour obtenir un jeton d’accès d’Azure AD à partir duquel l’ID client peut être extrait.</span><span class="sxs-lookup"><span data-stu-id="29322-230">Your application uses this authorization code to obtain an access token from Azure AD, from which the tenant ID can be extracted.</span></span> <span data-ttu-id="29322-231">Une fois que vous avez extrait et stocké l’ID client, vous pouvez obtenir d’autres jetons d’accès sans demander à l’administrateur client de se connecter.</span><span class="sxs-lookup"><span data-stu-id="29322-231">After you have extracted and stored the tenant ID, you can obtain subsequent access tokens without requiring the tenant admin to sign in.</span></span>


## <a name="request-access-tokens-from-azure-ad"></a><span data-ttu-id="29322-232">Demander des jetons d’accès à Azure AD</span><span class="sxs-lookup"><span data-stu-id="29322-232">Request and acquire an access token from Azure AD</span></span>

<span data-ttu-id="29322-233">Vous disposez de deux méthodes pour demander des jetons d’accès à Azure AD :</span><span class="sxs-lookup"><span data-stu-id="29322-233">There are two methods for requesting access tokens from Azure AD:</span></span>

- <span data-ttu-id="29322-234">Le [flux d’octroi de code d’autorisation](https://msdn.microsoft.com/en-us/library/azure/dn645542.aspx) implique qu’un administrateur client donne son consentement explicite, ce qui renvoie un code d’autorisation à votre application.</span><span class="sxs-lookup"><span data-stu-id="29322-234">The [Authorization Code Grant Flow](https://msdn.microsoft.com/en-us/library/azure/dn645542.aspx) involves a tenant admin granting explicit consent, which returns an authorization code to your application.</span></span> <span data-ttu-id="29322-235">Votre application échange ensuite le code d’autorisation contre un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="29322-235">Your application then exchanges the authorization code for an access token.</span></span> <span data-ttu-id="29322-236">Cette méthode est nécessaire pour obtenir le consentement initial requis par votre application pour accéder aux données client à l’aide de l’API. Ce premier jeton d’accès est nécessaire pour obtenir et stocker l’ID client.</span><span class="sxs-lookup"><span data-stu-id="29322-236">This method is required to obtain the initial consent that your application needs to access the tenant data by using the API, and this first access token is needed in order to obtain and store the tenant ID.</span></span>
    
- <span data-ttu-id="29322-237">Le [flux d’octroi d’informations d’identification du client](https://msdn.microsoft.com/fr-FR/library/azure/dn645543.aspx) permet à votre application de demander d’autres jetons d’accès lorsque les anciens expirent, sans que l’administrateur client doive se connecter et donner explicitement son consentement.</span><span class="sxs-lookup"><span data-stu-id="29322-237">The [Client Credentials Grant Flow](https://msdn.microsoft.com/fr-FR/library/azure/dn645543.aspx) allows your application to request subsequent access tokens as old ones expire, without requiring the tenant admin to sign in and explicitly grant consent.</span></span> <span data-ttu-id="29322-238">Cette méthode doit être utilisée pour les applications qui s’exécutent en continu en arrière-plan appelant les API une fois que le consentement initial de l’administrateur client a été donné.</span><span class="sxs-lookup"><span data-stu-id="29322-238">This method must be used for applications that run continuously in the background calling the APIs once the initial tenant admin consent has been granted.</span></span>
    

### <a name="request-an-access-token-using-the-authorization-code"></a><span data-ttu-id="29322-239">Demander un jeton d’accès à l’aide du code d’autorisation</span><span class="sxs-lookup"><span data-stu-id="29322-239">Request an access token using the authorization code</span></span>

<span data-ttu-id="29322-240">Une fois qu’un client administrateur donne son consentement, votre application reçoit un code d’autorisation sous la forme d’un paramètre de chaîne de requête lorsqu’Azure AD redirige l’administrateur client vers votre URL désignée.</span><span class="sxs-lookup"><span data-stu-id="29322-240">After a tenant admin grants consent, your application receives an authorization code as a query string parameter when Azure AD redirects the tenant admin to your designated URL.</span></span>

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

<span data-ttu-id="29322-241">Votre application effectue un POST REST HTTP sur Azure AD pour échanger le code d’autorisation contre un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="29322-241">Your application makes an HTTP REST POST to Azure AD to exchange the authorization code for an access token.</span></span> <span data-ttu-id="29322-242">Étant donné que l’ID client n’est pas encore connu, le POST sera effectué sur le point de terminaison « courant », qui ne dispose pas de l’ID client incorporé dans l’URL :</span><span class="sxs-lookup"><span data-stu-id="29322-242">Because the tenant ID is not yet known, the POST will be to the "common" endpoint, which does not have the tenant ID embedded in the URL:</span></span>

```http
https://login.windows.net/common/oauth2/token
```

<span data-ttu-id="29322-243">Le corps du POST contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="29322-243">The body of the POST contains the following:</span></span>

```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code= AAABAAAAvPM1KaPlrEqdFSB...
```

#### <a name="sample-request"></a><span data-ttu-id="29322-244">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="29322-244">Sample request</span></span>

```json
POST https://login.windows.net/common/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 944

resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code=AAABAAAAvPM1KaPlrEqdFSB...
```

<br/>

<span data-ttu-id="29322-245">Le corps de la réponse inclura plusieurs propriétés, y compris le jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="29322-245">The body of the response will include several properties, including the access token.</span></span> 

#### <a name="sample-response"></a><span data-ttu-id="29322-246">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="29322-246">Sample response</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 3265

{"expires_in":"3599","token_type":"Bearer","scope":"ActivityFeed.Read ActivityReports.Read ServiceHealth.Read","expires_on":"1438290275","not_before":"1438286375","resource":"https://manage.office.com","access_token":"eyJ0eX...","refresh_token":"AAABAAA...","id_token":"eyJ0eXAi..."}
```

<span data-ttu-id="29322-247">Le jeton d’accès renvoyé est un jeton JWT qui inclut des informations sur l’administrateur qui a donné son consentement et l’application qui demande l’accès.</span><span class="sxs-lookup"><span data-stu-id="29322-247">The access token that is returned is a JWT token that includes information about both the admin that granted consent and the application requesting access.</span></span> <span data-ttu-id="29322-248">Voici ci-dessous un exemple de jeton non codé.</span><span class="sxs-lookup"><span data-stu-id="29322-248">The following code shows an example of a token file.</span></span> <span data-ttu-id="29322-249">Votre application doit extraire l’ID client « tid » de ce jeton et le stocker afin de pouvoir l’utiliser pour demander d’autres jetons d’accès à leur expiration, sans interaction supplémentaire de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="29322-249">Your application must extract the tenant ID "tid" from this token and store it so that it can be used to request additional access tokens as they expire, without further admin interaction.</span></span>

#### <a name="sample-token"></a><span data-ttu-id="29322-250">Exemple de jeton</span><span class="sxs-lookup"><span data-stu-id="29322-250">Sample token</span></span>

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1427246416,
  "nbf": 1427246416,
  "exp": 1427250316,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "amr": [
    "pwd"
  ],
  "oid": "1cef1fdb-ff52-48c4-8e4e-dfb5ea83d357",
  "upn": "admin@contoso.onmicrosoft.com",
  "puid": "1003BFFD8EC47CA6",
  "sub": "7XpD5OWAXM1OWmKiVKh1FOkKXV4N3OSRol6mz1pxxhU",
  "given_name": "John",
  "family_name": "Doe",
  "name": "Contoso, Inc.",
  "unique_name": "admin@contoso.onmicrosoft.com",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1",
  "scp": "ActivityFeed.Read ServiceHealth.Read",
  "acr": "1"
}
```


### <a name="request-an-access-token-by-using-client-credentials"></a><span data-ttu-id="29322-251">Demander un jeton d’accès à l’aide des informations d’identification client</span><span class="sxs-lookup"><span data-stu-id="29322-251">Request an access token by using client credentials</span></span>

<span data-ttu-id="29322-252">Une fois que l’ID client est connu, votre application peut effectuer des appels de service à service à Azure AD pour demander d’autres jetons d’accès lorsqu’ils expirent.</span><span class="sxs-lookup"><span data-stu-id="29322-252">After the tenant ID is known, your application can make service-to-service calls to Azure AD to request additional access tokens as they expire.</span></span> <span data-ttu-id="29322-253">Ces jetons incluent des informations sur l’application qui demande l’accès uniquement et non sur l’administrateur qui a donné son consentement à l’origine.</span><span class="sxs-lookup"><span data-stu-id="29322-253">These tokens include information only about the requesting application and not about the admin that originally granted consent.</span></span> <span data-ttu-id="29322-254">Les appels de service à service exigent que votre application utilise un certificat X.509 pour créer une assertion client sous la forme d’un jeton de porteur JWT signé SHA256 et codé en base 64.</span><span class="sxs-lookup"><span data-stu-id="29322-254">Service-to-service calls require that your application use an X.509 certificate to create client assertion in the form of a base64-encoded, SHA256 signed JWT bearer token.</span></span>

<span data-ttu-id="29322-255">Lorsque vous développez votre application dans .NET, vous pouvez utiliser la [bibliothèque d’authentification Azure AD (ADAL)](https://docs.microsoft.com/fr-FR/azure/active-directory/develop/active-directory-authentication-libraries) pour créer des assertions client.</span><span class="sxs-lookup"><span data-stu-id="29322-255">When you are developing your application in .NET, you can use the [Azure AD Authentication Library (ADAL)](https://docs.microsoft.com/fr-FR/azure/active-directory/develop/active-directory-authentication-libraries) to create client assertions.</span></span> <span data-ttu-id="29322-256">Les autres plateformes de développement doivent avoir des bibliothèques similaires.</span><span class="sxs-lookup"><span data-stu-id="29322-256">Other development platforms should have similar libraries.</span></span>

<span data-ttu-id="29322-257">Un jeton JWT non codé se compose d’un en-tête et d’une charge utile ayant les propriétés suivantes.</span><span class="sxs-lookup"><span data-stu-id="29322-257">An un-encoded JWT token consists of a header and payload that have the following properties.</span></span>

```json
HEADER:

{
  "alg": "RS256",
  "x5t": "{thumbprint of your X.509 certificate used to sign the token",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/{tenantid}/oauth2/token",
  "iss": "{your app client ID}",
  "sub": "{your app client ID}"
  "jti": "{random GUID}",
  "nbf": {epoch time, before which the token is not valid},
  "exp": {epoch time, after which the token is not valid},
}

```

#### <a name="sample-jwt-token"></a><span data-ttu-id="29322-258">Exemple de jeton JWT</span><span class="sxs-lookup"><span data-stu-id="29322-258">Sample JWT token</span></span>


```json
HEADER:

{
  "alg": "RS256",
  "x5t": "YyfshJC3rPQ-kpGo5dUaiY5t3iU",
}

PAYLOAD:

{
  "aud": "https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token",
  "iss": "a6099727-6b7b-482c-b509-1df309acc563",
  "sub": "a6099727-6b7b-482c-b509-1df309acc563"
  "jti": "0ce254c4-81b1-4a2e-8436-9a8c3b49dfb9",
  "nbf": 1427248048,
  "exp": 1427248648,
}
```

<span data-ttu-id="29322-259">L’assertion client est ensuite transmise à Azure AD dans le cadre d’un appel de service à service pour demander un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="29322-259">The client assertion is then passed to Azure AD as part of a service-to-service call to request an access token.</span></span> <span data-ttu-id="29322-260">Lorsque vous utilisez les informations d’identification client pour demander un jeton d’accès, utilisez un POST HTTP sur un point de terminaison spécifique au client, où l’ID client extrait et stocké précédemment est incorporé dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="29322-260">When using client credentials to request an access token, use an HTTP POST to a tenant-specific endpoint, where the previously extracted and stored tenant ID is embedded in the URL.</span></span>


```http
https://login.windows.net/{tenantid}/oauth2/token
```

<span data-ttu-id="29322-261">Le corps du POST contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="29322-261">The body of the POST contains the following:</span></span>


```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id={your_app_client_id}&amp;grant_type=client_credentials&amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion={encoded_signed_JWT_token}
```

#### <a name="sample-request"></a><span data-ttu-id="29322-262">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="29322-262">Sample request</span></span>

```json
POST https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 994

resource=https%3A%2F%2Fmanage.office.com&amp;client_id= a6099727-6b7b-482c-b509-1df309acc563&amp;grant_type=client_credentials &amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Ill5ZnNoSkMzclBRLWtwR281ZFVhaVk1dDNpVSJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ud2luZG93cy5uZXRcLzQxNDYzZjUzLTg4MTItNDBmNC04OTBmLTg2NWJmNmUzNTE5MFwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQyNzI0ODY0OCwiaXNzIjoiYTYwOTk3MjctNmI3Yi00ODJjLWI1MDktMWRmMzA5YWNjNTYzIiwianRpIjoiMGNlMjU0YzQtODFiMS00YTJlLTg0MzYtOWE4YzNiNDlkZmI5IiwibmJmIjoxNDI3MjQ4MDQ4LCJzdWIiOiJhNjA5OTcyNy02YjdiLTQ4MmMtYjUwOS0xZGYzMDlhY2M1NjMifQ.vfDrmCjiXgoj2JrTkwyOpr-NOeQTzlXQcGlKGNpLLe0oh4Zvjdcim5C7E0UbI3Z2yb9uKQdx9G7GeqS-gVc9kNV_XSSNP4wEQj3iYNKpf_JD2ikUVIWBkOg41BiTuknRJAYOMjiuBE2a6Wyk-vPCs_JMd7Sr-N3LiNZ-TjluuVzWHfok_HWz_wH8AzdoMF3S0HtrjNd9Ld5eI7MVMt4OTpRfh-Syofi7Ow0HN07nKT5FYeC_ThBpGiIoODnMQQtDA2tM7D3D6OlLQRgLfI8ir73PVXWL7V7Zj2RcOiooIeXx38dvuSwYreJYtdphmrDBZ2ehqtduzUZhaHL1iDvLlw
```

<span data-ttu-id="29322-263">La réponse sera la même qu’avant, mais le jeton n’aura pas les mêmes propriétés, car il ne contient pas les propriétés de l’administrateur qui a donné son consentement.</span><span class="sxs-lookup"><span data-stu-id="29322-263">The response will be the same as before, but the token will not have the same properties, because it does not contain properties of the admin that granted consent.</span></span> 

#### <a name="sample-response"></a><span data-ttu-id="29322-264">Exemple de réponse</span><span class="sxs-lookup"><span data-stu-id="29322-264">Sample response</span></span>

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 1276

{"token_type":"Bearer","expires_in":"3599","expires_on":"1431659094","not_before":"1431655194","resource":"https://manage.office.com","access_token":"eyJ0eXAiOiJKV1QiL..."}
```

#### <a name="sample-access-token"></a><span data-ttu-id="29322-265">Exemple de jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="29322-265">Sample access token</span></span>

```json
{
  "aud": "https://manage.office.com",
  "iss": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "iat": 1431655194,
  "nbf": 1431655194,
  "exp": 1431659094,
  "ver": "1.0",
  "tid": "41463f53-8812-40f4-890f-865bf6e35190",
  "roles": [
    "ServiceHealth.Read",
    "ActivityFeed.Read"
  ],
  "oid": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "sub": "67cb0334-e242-4783-8028-0f39132fb5ad",
  "idp": "https://sts.windows.net/41463f53-8812-40f4-890f-865bf6e35190/",
  "appid": "a6099727-6b7b-482c-b509-1df309acc563",
  "appidacr": "1"
}
```


## <a name="build-your-app"></a><span data-ttu-id="29322-266">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="29322-266">Build your app</span></span>

<span data-ttu-id="29322-267">Maintenant que vous avez inscrit votre application dans Azure AD et l’avez configurée avec les autorisations nécessaires, vous êtes prêt à créer votre application.</span><span class="sxs-lookup"><span data-stu-id="29322-267">Now that you have registered your app in Azure AD and configured it with the necessary permissions, you're ready to build your app.</span></span> <span data-ttu-id="29322-268">Voici quelque aspects clés à prendre en considération lors de la conception et de la création de votre application :</span><span class="sxs-lookup"><span data-stu-id="29322-268">The following are some of the key aspects to consider when designing and building your app:</span></span>

- <span data-ttu-id="29322-269">**Expérience relative au consentement**.</span><span class="sxs-lookup"><span data-stu-id="29322-269">**The consent experience**.</span></span> <span data-ttu-id="29322-270">Pour obtenir le consentement de vos clients, vous devez les diriger dans un navigateur vers le site web Azure AD, à l’aide de l’URL spécialement construite décrite précédemment, et vous devez avoir un site web vers lequel Azure AD redirigera l’administrateur une fois qu’il a donné son consentement.</span><span class="sxs-lookup"><span data-stu-id="29322-270">To obtain consent from your customers, you must direct them in a browser to the Azure AD website, using the specially constructed URL described previously, and you must have a website to which Azure AD will redirect the admin once they grant consent.</span></span> <span data-ttu-id="29322-271">Ce site web doit extraire le code d’autorisation de l’URL et l’utiliser pour demander un jeton d’accès à partir duquel il peut obtenir l’ID client.</span><span class="sxs-lookup"><span data-stu-id="29322-271">This website must extract the authorization code from the URL and use it to request an access token from which it can obtain the tenant ID.</span></span>
    
- <span data-ttu-id="29322-272">**Stocker l’ID client dans votre système**.</span><span class="sxs-lookup"><span data-stu-id="29322-272">**Store the tenant ID in your system**.</span></span> <span data-ttu-id="29322-273">Cela est nécessaire lors de la demande de jetons d’accès à Azure AD et lors de l’appel des API de gestion d’Office.</span><span class="sxs-lookup"><span data-stu-id="29322-273">This will be needed when requesting access tokens from Azure AD and when calling the Office Management APIs.</span></span>
    
- <span data-ttu-id="29322-274">**Gestion des jetons d’accès**.</span><span class="sxs-lookup"><span data-stu-id="29322-274">**Managing access tokens**.</span></span> <span data-ttu-id="29322-275">Vous devez avoir un composant qui demande et gère les jetons d’accès selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="29322-275">You will need a component that requests and manages access tokens as needed.</span></span> <span data-ttu-id="29322-276">Si votre application appelle les API régulièrement, elle peut demander des jetons à la demande, ou si elle appelle les API en permanence pour récupérer des données, elle peut demander des jetons à des intervalles réguliers (par exemple, toutes les 45 minutes).</span><span class="sxs-lookup"><span data-stu-id="29322-276">If your app calls the APIs periodically, it can request tokens on demand, or if it calls the APIs continuously to retrieve data, it can request tokens at regular intervals (for example, every 45 minutes).</span></span>
    
- <span data-ttu-id="29322-277">**Implémenter un détecteur de webhook** selon les besoins de l’API spécifique que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="29322-277">**Implement a webhook listener** as needed by the particular API you are using.</span></span>
    
- <span data-ttu-id="29322-278">**Extraction des données et stockage**.</span><span class="sxs-lookup"><span data-stu-id="29322-278">**Data retrieval and storage**.</span></span> <span data-ttu-id="29322-279">Vous devez avoir un composant qui récupère les données pour chaque client à l’aide de l’interrogation continue ou en réponse à des notifications de webhook, en fonction de l’API spécifique que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="29322-279">You'll need a component that retrieves data for each tenant, either by using continuous polling or in response to webhook notifications, depending on the particular API you are using.</span></span>
    
