---
title: "웹 응용 프로그램에서 Azure 주요 자격 증명 모음 aaaUse | Microsoft Docs"
description: "이 자습서 toohelp 배웁니다, 어떻게 toouse Azure 키 자격 증명 모음에 있는 웹 응용 프로그램을 사용 합니다."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="23baf-103">웹 응용 프로그램에서 Azure 주요 자격 증명 모음 사용</span><span class="sxs-lookup"><span data-stu-id="23baf-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="23baf-104">소개</span><span class="sxs-lookup"><span data-stu-id="23baf-104">Introduction</span></span>
<span data-ttu-id="23baf-105">이 자습서에 어떻게 toouse Azure 키 자격 증명 모음에 있는 웹 응용 프로그램을 Azure에 알아봅니다 toohelp를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="23baf-106">웹 응용 프로그램에서 사용할 수 있도록 Azure 키 자격 증명 모음에서 암호에 액세스 하는 hello 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="23baf-107">**예상 시간 toocomplete:** 15 분</span><span class="sxs-lookup"><span data-stu-id="23baf-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="23baf-108">Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="23baf-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23baf-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="23baf-109">Prerequisites</span></span>
<span data-ttu-id="23baf-110">toocomplete이이 자습서에서는 다음 hello 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="23baf-111">Azure 키 자격 증명 모음에 사용 되는 URI tooa 암호</span><span class="sxs-lookup"><span data-stu-id="23baf-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="23baf-112">클라이언트 ID 및 클라이언트 암호는 웹 응용 프로그램에 대 한 액세스 tooyour 주요 자격 증명 모음에 있는 Azure Active Directory에 등록</span><span class="sxs-lookup"><span data-stu-id="23baf-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="23baf-113">웹 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="23baf-113">A web application.</span></span> <span data-ttu-id="23baf-114">웹 앱으로 Azure에 배포 된 ASP.NET MVC 응용 프로그램에 대 한 hello 단계를 보여 줄 것입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="23baf-115">에 나열 된 hello 단계를 완료 해야 [Azure 키 자격 증명 모음 시작](key-vault-get-started.md) 이 자습서를 마쳤으므로 hello URI tooa 암호 및 hello 클라이언트 ID와 클라이언트 암호는 웹 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="23baf-116">hello 키 자격 증명 모음에 액세스 하는 hello 웹 응용 프로그램에는 Azure Active Directory에 등록 되 고 액세스 tooyour 주요 자격 증명 모음 부여 되었는지 여부를 지정 하는 하나 hello입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="23baf-117">이 정보가 hello 대/소문자를 tooRegister hello 시작 자습서의 응용 프로그램을 다시 이동 하 고 나열 된 hello 단계를 반복 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="23baf-118">이 자습서는 Azure에서 웹 응용 프로그램을 만드는 hello 기본 사항을 이해 하는 웹 개발자를 위해 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="23baf-119">Azure 웹앱에 대한 자세한 내용은 [웹앱 개요](../app-service-web/app-service-web-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23baf-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="23baf-120"><a id="packages"></a>NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="23baf-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="23baf-121">웹 응용 프로그램 toohave 설치에 필요한 두 개의 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="23baf-122">Active Directory 인증 라이브러리 - Azure Active Directory를 조작하고 사용자 ID를 관리하기 위한 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="23baf-123">Azure 주요 자격 증명 모음 라이브러리 - Azure 주요 자격 증명 모음을 조작하기 위한 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="23baf-124">이러한 패키지 중 둘 다 사용 하 여 설치할 수 hello Install-package 명령을 사용 하 여 패키지 관리자 콘솔 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="23baf-125"><a id="webconfig"></a>Web.Config 수정</span><span class="sxs-lookup"><span data-stu-id="23baf-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="23baf-126">세 가지 응용 프로그램 설정을 toobe 추가 toohello web.config 파일을 다음과 같이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="23baf-127">않으려는 toohost Azure 웹 앱으로 응용 프로그램, hello 실제 ClientId, 클라이언트 암호 및 암호 URI 값 toohello web.config을 추가 해야 합니다. Azure 포털의 보안 수준 높이기 위해 hello에 hello 실제 값으로 추가 하기 때문에 이러한 dummy 값 둡니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="23baf-128"><a id="gettoken"></a>메서드 tooGet 액세스 토큰을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="23baf-129">순서 toouse hello 키 자격 증명 모음 API에에서 액세스 토큰이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="23baf-130">키 자격 증명 모음 API toohello 해야만 toosupply 호출을 처리 하는 키 자격 증명 모음 클라이언트 hello 사용 하 여 hello 액세스 토큰을 가져오는 함수는 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="23baf-131">다음은 hello 코드 tooget Azure Active Directory에서 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="23baf-132">이 코드는 응용 프로그램의 아무 곳에나 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="23baf-133">마음에 tooadd는 유틸리티 또는 EncryptionHelper 클래스.</span><span class="sxs-lookup"><span data-stu-id="23baf-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="23baf-134">클라이언트 ID와 클라이언트 암호를 사용 하 여 hello 가장 쉬운 방법은 tooauthenticate Azure AD 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="23baf-135">웹 응용 프로그램에서 클라이언트 ID 및 클라이언트 암호를 사용하여 의무를 분리하고 키 관리를 보다 세밀하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="23baf-136">하지만 일부에 대 한 구성 설정에서 tooprotect 되도록 hello 비밀 배치로으로 것은 위험할 수 있는 구성 설정에서 hello 클라이언트 암호를 배치에 의존지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="23baf-137">어떻게 toouse 클라이언트 ID 및 인증서 클라이언트 ID와 클라이언트 암호가 tooauthenticate 대신 hello Azure AD 응용 프로그램에 대 한 내용은 아래를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="23baf-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="23baf-138"><a id="appstart"></a>Hello 보안 응용 프로그램 시작을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="23baf-139">이제 toocall hello 키 자격 증명 모음 API를 코드 및 hello 암호를 검색할 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="23baf-140">hello 다음 코드 전환할 수 있습니다. 원격으로 toouse 필요 하기 전에 호출 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="23baf-141">시작 시에 한 번 실행 하 고는 hello 비밀 hello 응용 프로그램에 사용할 수 있도록 hello Global.asax에에서 hello 응용 프로그램 시작 이벤트에서이 코드를 배치 했습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="23baf-142"><a id="portalsettings"></a>Azure 포털 (선택 사항) hello에 응용 프로그램 설정을 추가합니다</span><span class="sxs-lookup"><span data-stu-id="23baf-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="23baf-143">Azure 웹 앱이 있는 경우 hello Azure 포털에서에서 이제 hello AppSettings hello에 대 한 실제 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="23baf-144">이 작업을 수행 하 여 hello 실제 값 hello web.config에 위치 하지 않습니다 있지만 hello 별도 액세스 제어 기능이 제공 되는 포털을 통해 보호 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="23baf-145">Web.config 파일에 입력 한 hello 값에 대 한 이러한 값이 대체 됩니다. Hello 이름은 동일 hello는 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Azure 포털에 표시되는 응용 프로그램 설정][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="23baf-147">클라이언트 암호 대신 인증서로 인증</span><span class="sxs-lookup"><span data-stu-id="23baf-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="23baf-148">또 다른 방법은 tooauthenticate Azure AD 응용 프로그램 클라이언트 ID와 클라이언트 암호 대신 클라이언트 ID 및 인증서를 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="23baf-149">다음 단계는 Azure 웹 앱에 인증서가 toouse를 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="23baf-150">인증서 얻기 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="23baf-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="23baf-151">Hello 인증서는 Azure AD 응용 프로그램에 연결</span><span class="sxs-lookup"><span data-stu-id="23baf-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="23baf-152">코드 tooyour 웹 앱 toouse hello 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="23baf-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="23baf-153">인증서 tooyour 웹 응용 프로그램 추가</span><span class="sxs-lookup"><span data-stu-id="23baf-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="23baf-154">**인증서 얻기 또는 만들기** 학습을 위한 목적으로 테스트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="23baf-155">다음은 몇 가지 명령 사용할 수 있는 개발자 명령 프롬프트 toocreate에 인증서입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="23baf-156">디렉터리 toowhere 만든 hello 인증서 파일을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="23baf-157">또한 시작 및 끝 날짜 hello 인증서의 hello에 대 한 사용 하 여 hello 현재 날짜와 1 년입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="23baf-158">Hello 종료 날짜 및 hello.pfx에 대 한 hello 암호를 기록 (이 예제의: 07/31/2016 및 test123).</span><span class="sxs-lookup"><span data-stu-id="23baf-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="23baf-159">아래에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-159">You will need them below.</span></span>

<span data-ttu-id="23baf-160">테스트 인증서 만들기에 대한 자세한 내용은 [방법: 사용자 고유의 테스트 인증서 만들기](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="23baf-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="23baf-161">**Azure AD 응용 프로그램으로 연결 hello 인증서** tooassociate 필요한 인증서를가지고 사용 하 여 Azure AD 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="23baf-162">현재는 Azure 포털 hello이이 워크플로; 지원 하지 않습니다. PowerShell을 통해이 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="23baf-163">Hello 명령을 tooassoicate hello 인증서 hello Azure AD 응용 프로그램으로 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="23baf-164">이러한 명령은 실행 한 후에 Azure AD에서 hello 응용 프로그램을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="23baf-165">를 검색할 때 "회사가 보유 한 응용 프로그램" 선택 "응용 프로그램 사용" 대신에 확인 hello 검색 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="23baf-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="23baf-166">Azure AD 응용 프로그램 개체 및 ServicePrincipal 개체에 대해 자세히 toolearn 참조 [응용 프로그램 개체 및 서비스 사용자 개체](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="23baf-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="23baf-167">**추가 코드 tooyour 웹 앱 toouse hello 인증서** 이제 코드 tooyour 웹 앱 tooaccess cert hello 및 인증을 위해 사용 하 여 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="23baf-168">먼저 코드 tooaccess hello 인증서가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="23baf-169">해당 hello StoreLocation은 LocalMachine 대신 CurrentUser note 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="23baf-170">테스트 인증서를 사용 중 이므로 'false' toohello 제공 하는 것을 Find 메서드.</span><span class="sxs-lookup"><span data-stu-id="23baf-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="23baf-171">다음은 코드를 CertificateHelper hello를 사용 하며 인증에 필요한 ClientAssertionCertificate를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="23baf-172">다음은 hello 새 코드 tooget hello 액세스 토큰입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="23baf-173">위의 hello GetToken 메서드를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="23baf-174">편의를 위해 다른 이름을 부여했습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="23baf-175">사용 편의를 위해 이 모든 코드를 웹앱 프로젝트의 Utils 클래스에 넣어 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="23baf-176">hello 마지막 코드 변경이 hello Application_Start 메서드가입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="23baf-177">먼저 toocall hello GetCert() 메서드 tooload hello ClientAssertionCertificate 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="23baf-178">한 다음 새 KeyVaultClient를 만들 때 제공 하는 hello 콜백 메서드를 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="23baf-179">위에서 몇 hello 코드를 대체이 note 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="23baf-180">**Hello Azure 포털을 통해 인증서 tooyour 웹 응용 프로그램 추가** 인증서 tooyour 웹 응용 프로그램을 추가 하는 것은 간단한 2 단계 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="23baf-181">먼저, Azure 포털 toohello 이동 하 고 tooyour 웹 응용 프로그램을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="23baf-182">웹 앱에 대 한 hello 설정 블레이드에서 "사용자 지정 도메인 및 SSL"에 대 한 hello 항목을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="23baf-183">Hello에 하면 블레이드 컴퓨터 이름은 수 tooupload hello KVWebApp.pfx 위에서 만든 인증서를 반드시 hello pfx에 대 한 hello 암호를 기억해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![Hello Azure 포털에서에서 인증서 tooa 웹 응용 프로그램 추가][2]

<span data-ttu-id="23baf-185">hello toodo를 필요한 것은 응용 프로그램 설정 tooyour hello 이름 웹 사이트에 웹 앱 tooadd\_부하\_인증서 및 값이 * 합니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="23baf-186">이렇게 하면 모든 인증서가 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="23baf-187">하려는 경우이 단계는 tooload만 hello 인증서를 업로드 한 경우 해당 지문 쉼표로 구분 된 목록에 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="23baf-188">추가 인증서 tooa 웹 앱에 대 한 더 toolearn 참조 [Azure 웹 사이트 응용 프로그램에 대 한 인증서를 사용 하 여](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="23baf-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="23baf-189">**암호로 인증서 tooKey 자격 증명 모음을 추가** 사용자 인증서 toohello 웹 응용 프로그램 서비스를 직접 업로드 하는 대신는 암호로 키 자격 증명 모음에 저장 한 위치에서 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23baf-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="23baf-190">이 hello 다음 블로그 게시물에에서 설명 된 2 단계 프로세스 [주요 자격 증명 모음을 통해 Azure 웹 앱 인증서 배포](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="23baf-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="23baf-191"><a id="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="23baf-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="23baf-192">프로그래밍 참조는 [Azure 주요 자격 증명 모음 C# 클라이언트 API 참조](https://msdn.microsoft.com/library/azure/dn903628.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23baf-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
