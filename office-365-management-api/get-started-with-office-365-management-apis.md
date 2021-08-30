---
ms.technology: o365-service-communications
ms.TocTitle: Get started with Office 365 Management APIs
title: Prise en main des API de gestion d’Office 365
description: Les API utilisent Azure AD pour fournir des services d’authentification que vous pouvez utiliser pour octroyer des droits à votre application pour y accéder.
ms.ContentId: 74137c9a-29e0-b588-6122-26f4d2c5e3fc
ms.topic: reference (API)
ms.date: ''
ms.localizationpriority: high
ms.openlocfilehash: 96a0cd71c55251160117d1ae598c8935479b6780
ms.sourcegitcommit: 13b50617b1a73f5890414087d8eabe6b2240cfb4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2021
ms.locfileid: "58510145"
---
# <a name="get-started-with-office-365-management-apis"></a>Prise en main des API de gestion d’Office 365

Lorsque vous créez une application qui doit accéder à des services sécurisés tels qu’aux API de gestion d’Office 365, vous devez trouver un moyen d’indiquer au service si votre application dispose des droits appropriés pour y accéder. Les API de gestion d’Office 365 utilisent Azure AD pour fournir des services d’authentification que vous pouvez utiliser pour octroyer des droits à votre application pour y accéder. 

Vous devez suivre quatre étapes principales :

1. **Inscrire votre application dans Azure AD**. Pour autoriser votre application à accéder aux API de gestion d’Office 365, vous devez inscrire votre application dans Azure AD. Cela vous permet d’établir une identité pour votre application et de spécifier les niveaux d’autorisation dont elle a besoin pour accéder aux API.
    
2. **Obtenir le consentement de l’administrateur client d’Office 365**. Un administrateur client d’Office 365 doit donner explicitement son consentement pour autoriser votre application à accéder à ses données client au moyen des API de gestion d’Office 365. Le processus de consentement est une expérience basée sur le navigateur où l’administrateur client se connecte à l’**interface utilisateur de consentement d’Azure AD** et analyse les autorisations d’accès demandées par votre application, puis accorde ou refuse la demande. Une fois le consentement donné, l’interface utilisateur redirige l’utilisateur vers votre application avec un code d’autorisation dans l’URL. Votre application passe un appel de service à service à Azure AD pour échanger ce code d’autorisation contre un jeton d’accès, qui contient des informations sur l’administrateur client et votre application. L’ID client doit être extrait du jeton d’accès et stocké en vue d’une utilisation ultérieure.
    
3. **Demander des jetons d’accès à Azure AD**. Votre application utilise les informations d’identification la concernant comme configuré dans Azure AD pour demander régulièrement d’autres jetons d’accès pour un client ayant donné son consentement, sans aucune interaction de l’administrateur client supplémentaire. Ces jetons d’accès sont appelés jetons d’application uniquement car ils n’incluent pas d’informations sur l’administrateur client.
    
4. **Appeler les API de gestion d’Office 365**. Les jetons d’accès d’application uniquement sont transmis aux API de gestion d’Office 365 pour authentifier et autoriser votre application.
    
Le diagramme suivant illustre la séquence des demandes de consentement et de jetons d’accès.

![Flux d’autorisation de mise en route des API de gestion](images/authorization-flow.png)

> [!IMPORTANT]
> Avant de pouvoir accéder aux données via l’API Activité de gestion Office 365, vous devez activer la journalisation d’audit unifié pour votre organisation Office 365. Pour ce faire, vous devez activer le journal d’audit d’Office 365. Pour obtenir des instructions, consultez la rubrique [Activer ou désactiver la recherche dans un journal d’audit Office 365](/office365/securitycompliance/turn-audit-log-search-on-or-off). <br/><br/>L’activation de la journalisation d’audit unifié n’est pas requise si vous utilisez uniquement l’API de communications de service Office 365.

## <a name="register-your-application-in-azure-ad"></a>Inscrire votre application dans Azure AD

Les API de gestion d’Office 365 utilisent Azure AD pour fournir une authentification sécurisée aux données client d’Office 365. Pour accéder aux API de gestion d’Office 365, vous devez inscrire votre application dans Azure AD, et dans le cadre de la configuration, vous devez spécifier les niveaux d’autorisation nécessaires à votre application pour accéder aux API.


### <a name="prerequisites"></a>Conditions préalables

Pour inscrire votre application dans Azure AD, vous devez avoir un abonnement à Office 365 et un abonnement à Azure qui a été associé à votre abonnement Office 365. Vous pouvez utiliser des abonnements à la version d’évaluation d’Office 365 et Azure pour commencer. Pour plus d’informations, consultez [Bienvenue dans le programme pour les développeurs Office 365](/office/developer-program/office-365-developer-program).


### <a name="use-the-azure-management-portal-to-register-your-application-in-azure-ad"></a>Inscrire votre application dans Azure AD à l’aide du portail de gestion Azure

Une fois que vous disposez d’un client Microsoft avec les abonnements appropriés, vous pouvez inscrire votre application dans Azure AD.

1. Connectez-vous au [portail de gestion Azure](https://manage.windowsazure.com/) à l’aide des informations d’identification de votre client Microsoft qui dispose de l’abonnement à Office 365 que vous souhaitez utiliser. Vous pouvez également accéder au portail de gestion Azure en utilisant le lien qui s’affiche dans le volet de navigation gauche du [portail d’administration Office](https://portal.office.com/).
    
2. Dans le volet de navigation gauche, sélectionnez Active Directory (1). Assurez-vous que l’onglet Directory (2) est bien sélectionné, puis cliquez sur le nom du répertoire (3).
    
   ![Page d’inscription à Office 365](images/o365-sign-up-page.png)
    
    
3. Sur la page du répertoire, sélectionnez **Applications**. Azure AD affiche la liste des applications actuellement installées dans votre client.
    
4. Sélectionnez **Ajouter**.
    
   ![Page d’administration d’Office 365](images/o365-admin-page.png)
    
    
5. Sélectionnez **Ajouter une application développée par mon organisation**.
    
6. Entrez le **NOM** de votre application et spécifiez le **Type** comme APPLICATION WEB ET/OU API WEB.
    
7. Entrez les propriétés appropriées de l’application :
    
   - **URL DE CONNEXION**. URL permettant aux utilisateurs de se connecter et d’utiliser votre application. Vous pouvez la modifier ultérieurement selon vos besoins.
    
   - **URI ID D’APPLICATION**. URI utilisé comme identificateur unique logique pour votre application. L’URI doit être dans un domaine personnalisé vérifié pour qu’un utilisateur externe puisse accorder à votre application l’accès à ses données dans Windows Azure AD. Par exemple, si votre client Microsoft est **contoso.onmicrosoft.com**, l’URI ID D’APPLICATION peut être **https://app.contoso.onmicrosoft.com**.
    
8. Votre application est désormais inscrite auprès d’Azure Active Directory et un ID client lui a été affecté. Toutefois, il reste plusieurs aspects importants de votre application à configurer.
    

### <a name="configure-your-application-properties-in-azure-ad"></a>Configurer les propriétés de votre application dans Azure AD

Maintenant que votre application est inscrite, vous devez spécifier plusieurs propriétés importantes qui déterminent comment fonctionne votre application dans Azure AD et comment les administrateurs clients donnent leur consentement pour permettre à votre application d’accéder à leurs données à l’aide des API de gestion d’Office 365.

Pour plus d’informations sur la configuration de l’application Azure AD en général, reportez-vous à [Objets application et principal du service dans Azure Active Directory](/azure/active-directory/develop/active-directory-application-objects).


1. **ID CLIENT**. Cette valeur est générée automatiquement par Azure AD. Votre application utilisera cette valeur lors de la demande de consentement aux administrateurs clients et de la demande de jetons d’application uniquement à Azure AD.
    
2. **L’APPLICATION EST MUTUALISÉE**. Cette propriété doit être définie sur **OUI** pour permettre aux administrateurs clients de donner leur consentement à votre application pour accéder à leurs données à l’aide des API de gestion d’Office 365. Si cette propriété est définie sur **NON**, votre application pourra accéder uniquement aux données de votre propre client.
    
3. **URL DE RÉPONSE**. Il s’agit de l’URL vers laquelle un administrateur client sera dirigé après avoir donné son consentement pour autoriser votre application à accéder à ses données à l’aide des API de gestion d’Office 365. Vous pouvez configurer plusieurs URL de réponse selon vos besoins. Azure définit automatiquement la première URL pour qu’elle corresponde à l’URL de connexion que vous avez spécifiée lorsque vous avez créé l’application, mais vous pouvez modifier cette valeur selon vos besoins.
    
Veillez à choisir **Enregistrer** après avoir modifié ces propriétés.


### <a name="generate-a-new-key-for-your-application"></a>Générer une nouvelle clé pour votre application

Les clés, également appelées clés secrètes client, sont utilisées lors de l’échange d’un code d’autorisation contre un jeton d’accès.


1. Dans le portail de gestion Azure, sélectionnez votre application et choisissez **Configurer** dans le menu supérieur. Faites défiler jusqu'à **clés**.
    
2. Sélectionnez la durée de votre clé, puis choisissez **Enregistrer**.
    
   ![Page d’abonnement Azure](images/azure-subscription-page.png)
    
    
3. Azure affiche la question secrète de l’application uniquement après l’avoir enregistrée. Sélectionnez l’icône Presse-papiers pour copier la clé secrète client dans le Presse-papiers.
    
   ![Page du portail Azure](images/azure-portal-page.png)

   > [!IMPORTANT] 
   > Azure affiche uniquement la clé secrète client au moment où vous l’avez initialement générée. Vous ne pouvez pas revenir à cette page et récupérer la clé secrète client ultérieurement.

### <a name="configure-an-x509-certificate-to-enable-service-to-service-calls"></a>Configurer un certificat X.509 pour activer les appels de service à service

Une application qui est en cours d’exécution en arrière-plan, comme un démon ou un service, peut utiliser les informations d’identification client pour demander des jetons d’accès d’application uniquement sans demander plusieurs fois le consentement à l’administrateur client une fois que le consentement initial a été donné. 

Pour plus d’informations, consultez la rubrique relative aux [appels de service à service à l’aide des informations d’identification client](https://msdn.microsoft.com/library/azure/dn645543.aspx).

Vous devez configurer un certificat X.509 avec votre application pour être utilisé comme informations d’identification client lorsque vous demandez des jetons d’accès d’application uniquement à Azure AD. Il y a deux étapes au processus:

- Obtenez un certificat X 509. Vous pouvez utiliser un certificat auto-signé ou un certificat émis par une autorité de certification approuvée publiquement.
    
- Modifier votre manifeste d’application pour inclure l’empreinte et la clé publique de votre certificat.
    
Les instructions suivantes montrent comment utiliser l’outil _makecert_ du Kit de développement logiciel (SDK) Windows ou Visual Studio pour générer un certificat auto-signé et exporter la clé publique dans un fichier codé en base 64.


1. Dans la ligne de commande, exécutez la commande suivante :
    
   ```
    makecert -r -pe -n "CN=MyCompanyName MyAppName Cert" -b 03/15/2015 -e 03/15/2017 -ss my -len 2048
   ```

   > [!NOTE] 
   > Lorsque vous générez le certificat X.509, vérifiez que la longueur minimale de la clé est 2048. Les raccourcis clavier ne sont pas acceptés en tant que clés valides.

2. Ouvrez le composant logiciel enfichable Certificats MMC et connectez-vous à votre compte d’utilisateur. 
    
3. Recherchez le nouveau certificat dans le dossier personnel et exportez la clé publique dans un fichier codé en base 64 (par exemple, mycompanyname.cer). Votre application utilisera ce certificat pour communiquer avec Azure AD. Par conséquent, assurez-vous de conserver l’accès à la clé privée également.
    
   > [!NOTE] 
   > Vous pouvez utiliser Windows PowerShell pour extraire l’empreinte et la clé publique codée en base 64. D’autres plateformes fournissent des outils similaires pour récupérer les propriétés des certificats.

4. Dans l’invite Windows PowerShell, tapez et exécutez la commande suivante :
    
   ```powershell
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $cer.Import("mycer.cer")
    $bin = $cer.GetRawCertData()
    $base64Value = [System.Convert]::ToBase64String($bin)
    $bin = $cer.GetCertHash()
    $base64Thumbprint = [System.Convert]::ToBase64String($bin)
    $keyid = [System.Guid]::NewGuid().ToString()
   ```

5. Stockez les valeurs pour `$base64Thumbprint`, `$base64Value` et `$keyid` à utiliser lorsque vous mettez à jour le manifeste de votre application dans les étapes suivantes.
    
   Utilisez à présent les valeurs extraites du certificat et l’ID de la clé générée pour mettre à jour le manifeste de votre application dans Azure AD.
    
6. Dans le portail de gestion Azure, sélectionnez votre application et choisissez **Configurer** dans le menu supérieur.
    
7. Dans la barre de commandes, sélectionnez **Gérer le manifeste**, puis **Télécharger le manifeste**.
    
   ![Affichage de certificats de ligne de commande](images/command-line-certificate-display.png)
    
    
8. Ouvrez le manifeste téléchargé pour le modifier et remplacez la propriété vide KeyCredentials par le fichier JSON suivant :
    
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
   > La propriété [KeyCredentials](https://msdn.microsoft.com/library/azure/ad/graph/api/entity-and-complex-type-reference#KeyCredentialType) est une collection qui permet de charger plusieurs certificats X.509 pour des scénarios de substitution ou de supprimer des certificats pour des scénarios de compromission.

9. Enregistrez vos modifications et chargez le manifeste mis à jour en cliquant sur **Gérer le manifeste** dans la barre de commandes, puis sélectionnez **Télécharger le manifeste**, naviguez jusqu’à votre fichier manifeste mis à jour et sélectionnez-le.
    

### <a name="specify-the-permissions-your-app-requires-to-access-the-office-365-management-apis"></a>Spécifier les autorisations requises par votre application pour accéder aux API de gestion d’Office 365

Enfin, vous devrez spécifier exactement les autorisations requises par votre application pour les API de gestion d’Office 365. Pour ce faire, vous ajoutez l’accès aux API de gestion d’Office 365 à votre application, puis vous spécifiez les autorisations dont vous avez besoin.


1. Dans le portail de gestion Azure, sélectionnez votre application et choisissez **Configurer** dans le menu supérieur. Faites défiler vers le bas jusqu’à **Autorisations accordées à d’autres applications**, et sélectionnez **Ajouter une application**.
    
   ![Page Azure AD](images/azure-ad-page.png)
    
    
2. Sélectionnez **API de gestion d’Office 365** (1) pour que l’élément apparaisse dans la colonne **Sélectionné** (2), puis cochez la case située en bas à droite (3) pour enregistrer votre sélection et revenir à la page de configuration principale pour votre application.
    
   ![Page Azure AD - Applications](images/azure-ad-apps-page.png)
    
    
3. Les API de gestion d’Office apparaissent maintenant dans la liste des applications pour lesquelles votre application requiert des autorisations. Sous **Autorisations d’application** et **Autorisations déléguées**, sélectionnez les autorisations requises par votre application. Reportez-vous à la référence de l’API spécifique pour plus d’informations sur chaque autorisation.  

   > [!NOTE] 
   > Il existe actuellement quatre autorisations inutilisées relatives aux rapports d’activité et à l’intelligence des menaces qui seront supprimées à l’avenir. Ne sélectionnez pas ces autorisations car elles sont inutiles.
    
   ![Boîte de dialogue Ajouter une application](images/add-an-application-dialog.png)
    
    
4. Cliquez sur **Enregistrer** pour enregistrer la configuration.
    

## <a name="get-office-365-tenant-admin-consent"></a>Obtenir le consentement de l’administrateur client d’Office 365

Maintenant que votre application est configurée avec les autorisations requises pour utiliser les API de gestion d’Office 365, un administrateur client doit octroyer ces autorisations explicitement à votre application pour accéder aux données de son client à l’aide des API. Pour donner son consentement, l’administrateur client doit se connecter à Azure AD à l’aide de l’URL suivante spécialement créée, où il peut revoir les autorisations demandées de votre application. Cette étape n’est pas obligatoire lorsque vous utilisez les API pour accéder aux données de votre propre client.


```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id={your_client_id}&redirect_uri={your_redirect_url }
```

L’URL de redirection doit correspondre à l’une des URL de réponse configurées pour votre application dans Azure AD ou être un chemin d’accès secondaire sous l’une d’elles.

Par exemple :

```http
https://login.windows.net/common/oauth2/authorize?response_type=code&resource=https%3A%2F%2Fmanage.office.com&client_id=2d4d11a2-f814-46a7-890a-274a72a7309e&redirect_uri=http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F
```

Vous pouvez tester l’URL de consentement en la collant dans un navigateur et en vous connectant à l’aide des informations d’identification d’un administrateur Office 365 pour un locataire autre que le locataire que vous avez utilisé pour inscrire l’application. Vous verrez la demande d’octroi de l’autorisation à votre application d’utiliser les APIs de gestion Office.


![Page Azure AD - Application ajoutée](images/azure-ad-app-added-page.png)

Après avoir sélectionné **Accepter**, vous êtes redirigé vers la page spécifiée où se trouve un code dans la chaîne de requête. 

Par exemple :

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

Votre application utilise ce code d’autorisation pour obtenir un jeton d’accès d’Azure AD à partir duquel l’ID client peut être extrait. Une fois que vous avez extrait et stocké l’ID client, vous pouvez obtenir d’autres jetons d’accès sans demander à l’administrateur client de se connecter.


## <a name="request-access-tokens-from-azure-ad"></a>Demander des jetons d’accès à Azure AD

Vous disposez de deux méthodes pour demander des jetons d’accès à Azure AD :

- Le [flux d’octroi de code d’autorisation](https://msdn.microsoft.com/library/azure/dn645542.aspx) implique qu’un administrateur client donne son consentement explicite, ce qui renvoie un code d’autorisation à votre application. Votre application échange ensuite le code d’autorisation contre un jeton d’accès. Cette méthode est nécessaire pour obtenir le consentement initial requis par votre application pour accéder aux données client à l’aide de l’API. Ce premier jeton d’accès est nécessaire pour obtenir et stocker l’ID client.
    
- Le [flux d’octroi d’informations d’identification du client](https://msdn.microsoft.com/library/azure/dn645543.aspx) permet à votre application de demander d’autres jetons d’accès lorsque les anciens expirent, sans que l’administrateur client doive se connecter et donner explicitement son consentement. Cette méthode doit être utilisée pour les applications qui s’exécutent en continu en arrière-plan appelant les API une fois que le consentement initial de l’administrateur client a été donné.
    

### <a name="request-an-access-token-using-the-authorization-code"></a>Demander un jeton d’accès à l’aide du code d’autorisation

Une fois qu’un client administrateur donne son consentement, votre application reçoit un code d’autorisation sous la forme d’un paramètre de chaîne de requête lorsqu’Azure AD redirige l’administrateur client vers votre URL désignée.

```http
http://www.mycompany.com/myapp/?code=AAABAAAAvPM1KaPlrEqdFSB...
```

Votre application effectue un POST REST HTTP sur Azure AD pour échanger le code d’autorisation contre un jeton d’accès. Étant donné que l’ID client n’est pas encore connu, le POST sera effectué sur le point de terminaison « courant », qui ne dispose pas de l’ID client incorporé dans l’URL :

```http
https://login.windows.net/common/oauth2/token
```

Le corps du POST contient les éléments suivants :

```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code= AAABAAAAvPM1KaPlrEqdFSB...
```

#### <a name="sample-request"></a>Exemple de demande

```json
POST https://login.windows.net/common/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 944

resource=https%3A%2F%2Fmanage.office.com&amp;client_id=a6099727-6b7b-482c-b509-1df309acc563 &amp;redirect_uri= http%3A%2F%2Fwww.mycompany.com%2Fmyapp%2F &amp;client_secret={your_client_key}&amp;grant_type=authorization_code&amp;code=AAABAAAAvPM1KaPlrEqdFSB...
```

<br/>

Le corps de la réponse inclura plusieurs propriétés, y compris le jeton d’accès. 

#### <a name="sample-response"></a>Exemple de réponse

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 3265

{"expires_in":"3599","token_type":"Bearer","scope":"ActivityFeed.Read ActivityReports.Read ServiceHealth.Read","expires_on":"1438290275","not_before":"1438286375","resource":"https://manage.office.com","access_token":"eyJ0eX...","refresh_token":"AAABAAA...","id_token":"eyJ0eXAi..."}
```

Le jeton d’accès renvoyé est un jeton JWT qui inclut des informations sur l’administrateur qui a donné son consentement et l’application qui demande l’accès. Voici ci-dessous un exemple de jeton non codé. Votre application doit extraire l’ID client « tid » de ce jeton et le stocker afin de pouvoir l’utiliser pour demander d’autres jetons d’accès à leur expiration, sans interaction supplémentaire de l’administrateur.

#### <a name="sample-token"></a>Exemple de jeton

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

### <a name="request-an-access-token-by-using-client-credentials"></a>Demander un jeton d’accès à l’aide des informations d’identification client

Une fois que l’ID client est connu, votre application peut effectuer des appels de service à service à Azure AD pour demander d’autres jetons d’accès lorsqu’ils expirent. Ces jetons incluent des informations sur l’application qui demande l’accès uniquement et non sur l’administrateur qui a donné son consentement à l’origine. Les appels de service à service exigent que votre application utilise un certificat X.509 pour créer une assertion client sous la forme d’un jeton de porteur JWT signé SHA256 et codé en base 64.

Lorsque vous développez votre application dans .NET, vous pouvez utiliser la [bibliothèque d’authentification Azure AD (ADAL)](/azure/active-directory/develop/active-directory-authentication-libraries) pour créer des assertions client. Les autres plateformes de développement doivent avoir des bibliothèques similaires.

Un jeton JWT non codé se compose d’un en-tête et d’une charge utile ayant les propriétés suivantes.

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

#### <a name="sample-jwt-token"></a>Exemple de jeton JWT


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

L’assertion client est ensuite transmise à Azure AD dans le cadre d’un appel de service à service pour demander un jeton d’accès. Lorsque vous utilisez les informations d’identification client pour demander un jeton d’accès, utilisez un POST HTTP sur un point de terminaison spécifique au client, où l’ID client extrait et stocké précédemment est incorporé dans l’URL.


```http
https://login.windows.net/{tenantid}/oauth2/token
```

Le corps du POST contient les éléments suivants :


```json
resource=https%3A%2F%2Fmanage.office.com&amp;client_id={your_app_client_id}&amp;grant_type=client_credentials&amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion={encoded_signed_JWT_token}
```

#### <a name="sample-request"></a>Exemple de demande

```json
POST https://login.windows.net/41463f53-8812-40f4-890f-865bf6e35190/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.windows.net
Content-Length: 994

resource=https%3A%2F%2Fmanage.office.com&amp;client_id= a6099727-6b7b-482c-b509-1df309acc563&amp;grant_type=client_credentials &amp;client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&amp;client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Ill5ZnNoSkMzclBRLWtwR281ZFVhaVk1dDNpVSJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ud2luZG93cy5uZXRcLzQxNDYzZjUzLTg4MTItNDBmNC04OTBmLTg2NWJmNmUzNTE5MFwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQyNzI0ODY0OCwiaXNzIjoiYTYwOTk3MjctNmI3Yi00ODJjLWI1MDktMWRmMzA5YWNjNTYzIiwianRpIjoiMGNlMjU0YzQtODFiMS00YTJlLTg0MzYtOWE4YzNiNDlkZmI5IiwibmJmIjoxNDI3MjQ4MDQ4LCJzdWIiOiJhNjA5OTcyNy02YjdiLTQ4MmMtYjUwOS0xZGYzMDlhY2M1NjMifQ.vfDrmCjiXgoj2JrTkwyOpr-NOeQTzlXQcGlKGNpLLe0oh4Zvjdcim5C7E0UbI3Z2yb9uKQdx9G7GeqS-gVc9kNV_XSSNP4wEQj3iYNKpf_JD2ikUVIWBkOg41BiTuknRJAYOMjiuBE2a6Wyk-vPCs_JMd7Sr-N3LiNZ-TjluuVzWHfok_HWz_wH8AzdoMF3S0HtrjNd9Ld5eI7MVMt4OTpRfh-Syofi7Ow0HN07nKT5FYeC_ThBpGiIoODnMQQtDA2tM7D3D6OlLQRgLfI8ir73PVXWL7V7Zj2RcOiooIeXx38dvuSwYreJYtdphmrDBZ2ehqtduzUZhaHL1iDvLlw
```

La réponse sera la même qu’avant, mais le jeton n’aura pas les mêmes propriétés, car il ne contient pas les propriétés de l’administrateur qui a donné son consentement. 

#### <a name="sample-response"></a>Exemple de réponse

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Content-Length: 1276

{"token_type":"Bearer","expires_in":"3599","expires_on":"1431659094","not_before":"1431655194","resource":"https://manage.office.com","access_token":"eyJ0eXAiOiJKV1QiL..."}
```

#### <a name="sample-access-token"></a>Exemple de jeton d’accès

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


## <a name="build-your-app"></a>Créer votre application

Maintenant que vous avez inscrit votre application dans Azure AD et l’avez configurée avec les autorisations nécessaires, vous êtes prêt à créer votre application. Voici quelque aspects clés à prendre en considération lors de la conception et de la création de votre application :

- **Expérience relative au consentement**. Pour obtenir le consentement de vos clients, vous devez les diriger dans un navigateur vers le site web Azure AD, à l’aide de l’URL spécialement construite décrite précédemment, et vous devez avoir un site web vers lequel Azure AD redirigera l’administrateur une fois qu’il a donné son consentement. Ce site web doit extraire le code d’autorisation de l’URL et l’utiliser pour demander un jeton d’accès à partir duquel il peut obtenir l’ID client.
    
- **Stocker l’ID client dans votre système**. Cela est nécessaire lors de la demande de jetons d’accès à Azure AD et lors de l’appel des API de gestion d’Office.
    
- **Gestion des jetons d’accès**. Vous devez avoir un composant qui demande et gère les jetons d’accès selon vos besoins. Si votre application appelle les API régulièrement, elle peut demander des jetons à la demande, ou si elle appelle les API en permanence pour récupérer des données, elle peut demander des jetons à des intervalles réguliers (par exemple, toutes les 45 minutes).
    
- **Implémenter un détecteur de webhook** selon les besoins de l’API spécifique que vous utilisez.
    
- **Extraction des données et stockage**. Vous devez avoir un composant qui récupère les données pour chaque client à l’aide de l’interrogation continue ou en réponse à des notifications de webhook, en fonction de l’API spécifique que vous utilisez.
    
