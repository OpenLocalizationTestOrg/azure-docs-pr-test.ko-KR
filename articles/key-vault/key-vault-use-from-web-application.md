---
title: "웹 응용 프로그램에서 Azure Key Vault 사용 | Microsoft Docs"
description: "이 자습서에서는 웹 응용 프로그램에서 Azure 주요 자격 증명 모음을 사용하는 방법을 알아볼 수 있습니다."
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
ms.openlocfilehash: d095bcfe37baefa90cf79bb48bff3f703ce1dad7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="f7b74-103">웹 응용 프로그램에서 Azure 주요 자격 증명 모음 사용</span><span class="sxs-lookup"><span data-stu-id="f7b74-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="f7b74-104">소개</span><span class="sxs-lookup"><span data-stu-id="f7b74-104">Introduction</span></span>
<span data-ttu-id="f7b74-105">이 자습서에서는 Azure의 웹 응용 프로그램에서 Azure 주요 자격 증명 모음을 사용하는 방법을 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-105">Use this tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="f7b74-106">웹 응용 프로그램에서 사용할 수 있도록 Azure 주요 자격 증명 모음의 암호에 액세스하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-106">It walks you through the process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="f7b74-107">**예상 완료 시간:** 15분</span><span class="sxs-lookup"><span data-stu-id="f7b74-107">**Estimated time to complete:** 15 minutes</span></span>

<span data-ttu-id="f7b74-108">Azure 키 자격 증명 모음에 대한 개요는 [Azure 키 자격 증명 모음이란?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="f7b74-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7b74-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="f7b74-109">Prerequisites</span></span>
<span data-ttu-id="f7b74-110">이 자습서를 완료하려면 다음이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-110">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="f7b74-111">Azure 주요 자격 증명 모음의 암호에 대한 URI</span><span class="sxs-lookup"><span data-stu-id="f7b74-111">A URI to a secret in an Azure Key Vault</span></span>
* <span data-ttu-id="f7b74-112">주요 자격 증명 모음에 액세스할 수 있는, Azure Active Directory에 등록된 웹 응용 프로그램의 클라이언트 ID 및 클라이언트 암호</span><span class="sxs-lookup"><span data-stu-id="f7b74-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access to your Key Vault</span></span>
* <span data-ttu-id="f7b74-113">웹 응용 프로그램.</span><span class="sxs-lookup"><span data-stu-id="f7b74-113">A web application.</span></span> <span data-ttu-id="f7b74-114">Azure에 웹앱으로 배포된 ASP.NET MVC 응용 프로그램에 대한 단계를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-114">We will be showing the steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="f7b74-115">이 자습서에 대해 [Azure 주요 자격 증명 모음 시작](key-vault-get-started.md) 에 나열된 단계를 완료하여 웹 응용 프로그램의 클라이언트 ID 및 클라이언트 암호에 대한 URI가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-115">It is essential that you have completed the steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have the URI to a secret and the Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="f7b74-116">Azure Active Directory에 등록되고 주요 자격 증명 모음에 대한 액세스 권한이 부여된 웹 응용 프로그램에서 주요 자격 증명 모음에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-116">The web application that will be accessing the Key Vault is the one that is registered in Azure Active Directory and has been given access to your Key Vault.</span></span> <span data-ttu-id="f7b74-117">그렇지 않은 경우 시작 자습서의 응용 프로그램 등록으로 돌아가서 나열된 단계를 반복합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-117">If this is not the case, go back to Register an Application in the Get Started tutorial and repeat the steps listed.</span></span>

<span data-ttu-id="f7b74-118">이 자습서는 Azure에서 웹 응용 프로그램을 만들기 위한 기본 사항을 잘 알고 있는 웹 개발자를 대상으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-118">This tutorial is designed for web developers that understand the basics of creating web applications on Azure.</span></span> <span data-ttu-id="f7b74-119">Azure 웹앱에 대한 자세한 내용은 [웹앱 개요](../app-service-web/app-service-web-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7b74-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="f7b74-120"><a id="packages"></a>NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="f7b74-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="f7b74-121">웹 응용 프로그램을 위해 설치해야 하는 2개의 패키지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-121">There are two packages that your web application needs to have installed.</span></span>

* <span data-ttu-id="f7b74-122">Active Directory 인증 라이브러리 - Azure Active Directory를 조작하고 사용자 ID를 관리하기 위한 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="f7b74-123">Azure 주요 자격 증명 모음 라이브러리 - Azure 주요 자격 증명 모음을 조작하기 위한 메서드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="f7b74-124">패키지 관리자 콘솔에서 Install-Package 명령을 사용하여 이러한 패키지를 모두 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-124">Both of these packages can be installed using the Package Manager Console using the Install-Package command.</span></span>

    // this is currently the latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="f7b74-125"><a id="webconfig"></a>Web.Config 수정</span><span class="sxs-lookup"><span data-stu-id="f7b74-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="f7b74-126">다음과 같이 web.config 파일에 추가해야 하는 3개의 응용 프로그램 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-126">There are three application settings that need to be added to the web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer to the web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is the URI for the secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="f7b74-127">응용 프로그램을 Azure 웹앱으로 호스트하지 않으려는 경우 web.config에 실제 ClientId, 클라이언트 암호 및 암호 URI 값을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-127">If you are not going to host your application as an Azure Web App, then you should add the actual ClientId, Client Secret, and Secret URI values to the web.config.</span></span> <span data-ttu-id="f7b74-128">그렇지 않으면 보안 강화를 위해 Azure 포털에서 실제 값을 추가할 것이므로 이러한 더미 값을 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-128">Otherwise leave these dummy values because we will be adding the actual values in the Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="f7b74-129"><a id="gettoken"></a>액세스 토큰을 가져오는 메서드 추가</span><span class="sxs-lookup"><span data-stu-id="f7b74-129"><a id="gettoken"></a>Add Method to Get an Access Token</span></span>
<span data-ttu-id="f7b74-130">주요 자격 증명 모음 API를 사용하려면 액세스 토큰이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-130">In order to use the Key Vault API you need an access token.</span></span> <span data-ttu-id="f7b74-131">주요 자격 증명 모음 클라이언트가 주요 자격 증명 모음 API 호출을 처리하지만 액세스 토큰을 가져오는 함수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-131">The Key Vault Client handles calls to the Key Vault API but you need to supply it with a function that gets the access token.</span></span>  

<span data-ttu-id="f7b74-132">다음은 Azure Active Directory에서 액세스 토큰을 가져오는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-132">Following is the code to get an access token from Azure Active Directory.</span></span> <span data-ttu-id="f7b74-133">이 코드는 응용 프로그램의 아무 곳에나 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-133">This code can go anywhere in your application.</span></span> <span data-ttu-id="f7b74-134">이 경우 Utils 또는 EncryptionHelper 클래스를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-134">I like to add a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property to hold the secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //the method that will be provided to the KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed to obtain the JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="f7b74-135">클라이언트 ID 및 클라이언트 암호를 사용하는 것은 Azure AD 응용 프로그램을 인증하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-135">Using a Client ID and Client Secret is the easiest way to authenticate an Azure AD application.</span></span> <span data-ttu-id="f7b74-136">웹 응용 프로그램에서 클라이언트 ID 및 클라이언트 암호를 사용하여 의무를 분리하고 키 관리를 보다 세밀하게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-136">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="f7b74-137">하지만 이 방법은 클라이언트 암호를 구성 설정에 배치하는 것을 기반으로 하며 이것은 보호할 암호를 구성 설정에 배치하는 것 만큼이나 위험할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-137">But it does rely on putting the Client Secret in your configuration settings which for some can be as risky as putting the secret that you want to protect in your configuration settings.</span></span> <span data-ttu-id="f7b74-138">클라이언트 ID 및 클라이언트 암호 대신 클라이언트 ID 및 인증서를 사용하여 Azure AD 응용 프로그램을 인증하는 방법에 대한 설명은 다음을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7b74-138">See below for a discussion on how to use a Client ID and Certificate instead of Client ID and Client Secret to authenticate the Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="f7b74-139"><a id="appstart"></a>응용 프로그램 시작 시 암호 검색</span><span class="sxs-lookup"><span data-stu-id="f7b74-139"><a id="appstart"></a>Retrieve the secret on Application Start</span></span>
<span data-ttu-id="f7b74-140">이제 주요 자격 증명 모음 API를 호출하고 암호를 검색하는 코드가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-140">Now we need code to call the Key Vault API and retrieve the secret.</span></span> <span data-ttu-id="f7b74-141">다음 코드는 사용하기 전에 호출되기만 하면 아무 곳에나 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-141">The following code can be put anywhere as long as it is called before you need to use it.</span></span> <span data-ttu-id="f7b74-142">이 경우 시작 시 한 번 실행되어 응용 프로그램에서 암호를 사용할 수 있도록 Global.asax의 Application Start 이벤트에 이 코드를 배치했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-142">I have put this code in the Application Start event in the Global.asax so that it runs once on start and makes the secret available for the application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class to hold the secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="f7b74-143"><a id="portalsettings"></a>Azure 포털에서 앱 설정 추가(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="f7b74-143"><a id="portalsettings"></a>Add App Settings in the Azure Portal (optional)</span></span>
<span data-ttu-id="f7b74-144">Azure 웹앱이 있는 경우 이제 Azure 포털에서 AppSettings의 실제 값을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-144">If you have an Azure Web App you can now add the actual values for the AppSettings in the Azure Portal.</span></span> <span data-ttu-id="f7b74-145">이 작업을 수행하면 실제 값이 web.config에 포함되지 않고 별도 액세스 제어 기능이 있는 포털을 통해 보호됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-145">By doing this, the actual values will not be in the web.config but protected via the Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="f7b74-146">이러한 값은 web.config에 입력된 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-146">These values will be substituted for the values that you entered in your web.config.</span></span> <span data-ttu-id="f7b74-147">이름이 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-147">Make sure that the names are the same.</span></span>

![Azure 포털에 표시되는 응용 프로그램 설정][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="f7b74-149">클라이언트 암호 대신 인증서로 인증</span><span class="sxs-lookup"><span data-stu-id="f7b74-149">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="f7b74-150">클라이언트 ID 및 클라이언트 암호 대신 클라이언트 ID 및 인증서를 사용하여 Azure AD 응용 프로그램을 인증하는 다른 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-150">Another way to authenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="f7b74-151">Azure 웹앱에서 인증서를 사용하는 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-151">Following are the steps to use a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="f7b74-152">인증서 얻기 또는 만들기</span><span class="sxs-lookup"><span data-stu-id="f7b74-152">Get or Create a Certificate</span></span>
2. <span data-ttu-id="f7b74-153">인증서를 Azure AD 응용 프로그램에 연결</span><span class="sxs-lookup"><span data-stu-id="f7b74-153">Associate the Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="f7b74-154">인증서를 사용하도록 웹앱에 코드 추가</span><span class="sxs-lookup"><span data-stu-id="f7b74-154">Add code to your Web App to use the Certificate</span></span>
4. <span data-ttu-id="f7b74-155">웹앱에 인증서 추가</span><span class="sxs-lookup"><span data-stu-id="f7b74-155">Add a Certificate to your Web App</span></span>

<span data-ttu-id="f7b74-156">**인증서 얻기 또는 만들기** 학습을 위한 목적으로 테스트 인증서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-156">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="f7b74-157">다음은 개발자 명령 프롬프트에서 인증서를 만들기 위해 사용할 수 있는 몇 가지 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-157">Here are a couple of commands that you can use in a Developer Command Prompt to create a certificate.</span></span> <span data-ttu-id="f7b74-158">인증서 파일을 만들 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-158">Change directory to where you want the cert files created.</span></span>  <span data-ttu-id="f7b74-159">또한 인증서의 시작 및 종료 날짜는 현재 날짜 더하기 1년을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-159">Also, for the beginning and ending date of the certificate, use the current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="f7b74-160">.pfx에 대한 종료 날짜와 암호를 메모해 둡니다(이 예에서는 07/31/2016 및 test123).</span><span class="sxs-lookup"><span data-stu-id="f7b74-160">Make note of the end date and the password for the .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="f7b74-161">아래에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-161">You will need them below.</span></span>

<span data-ttu-id="f7b74-162">테스트 인증서 만들기에 대한 자세한 내용은 [방법: 사용자 고유의 테스트 인증서 만들기](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="f7b74-162">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="f7b74-163">**인증서를 Azure AD 응용 프로그램에 연결** 이제 인증서를 만들었고 Azure AD 응용 프로그램에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-163">**Associate the Certificate with an Azure AD application** Now that you have a certificate, you need to associate it with an Azure AD application.</span></span> <span data-ttu-id="f7b74-164">현재 Azure Portal에서는 이 워크플로를 지원하지 않으며, PowerShell을 통해 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-164">Presently, the Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="f7b74-165">다음 명령을 실행하여 인증서를 Azure AD 응용 프로그램과 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-165">Run the following commands to assoicate the certificate with the Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get the thumbprint to use in your app settings
    $x509.Thumbprint

<span data-ttu-id="f7b74-166">이러한 명령을 실행하면 Azure AD에서 응용 프로그램을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-166">After you have run these commands, you can see the application in Azure AD.</span></span> <span data-ttu-id="f7b74-167">검색 시 검색 대화 상자에서 “회사에서 사용하는 응용 프로그램” 대신 “회사가 보유한 응용 프로그램”을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="f7b74-167">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in the search dialog.</span></span>

<span data-ttu-id="f7b74-168">Azure AD 응용 프로그램 개체 및 ServicePrincipal 개체에 대해 자세히 알아보려면 [응용 프로그램 개체 및 서비스 주체 개체](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="f7b74-168">To learn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="f7b74-169">**인증서를 사용하도록 웹앱에 코드 추가** 이제 웹앱에 코드를 추가하여 인증서에 액세스하고 인증에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-169">**Add code to your Web App to use the Certificate** Now we will add code to your Web App to access the cert and use it for authentication.</span></span>

<span data-ttu-id="f7b74-170">먼저 인증서에 액세스하기 위한 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-170">First there is code to access the cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since the test root isn't installed.
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


<span data-ttu-id="f7b74-171">StoreLocation은 LocalMachine이 아닌, CurrentUser입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-171">Note that the StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="f7b74-172">테스트 인증서를 사용 중이므로 Find 메서드에 'false'를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-172">And that we are supplying 'false' to the Find method because we are using a test cert.</span></span>

<span data-ttu-id="f7b74-173">다음은 CertificateHelper를 사용하고 인증에 필요한 ClientAssertionCertificate를 만드는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-173">Next is code that uses the CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="f7b74-174">다음은 액세스 토큰을 가져오는 새로운 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-174">Here is the new code to get the access token.</span></span> <span data-ttu-id="f7b74-175">이 코드는 위의 GetToken 메서드를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-175">This replaces the GetToken method above.</span></span> <span data-ttu-id="f7b74-176">편의를 위해 다른 이름을 부여했습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-176">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="f7b74-177">사용 편의를 위해 이 모든 코드를 웹앱 프로젝트의 Utils 클래스에 넣어 두었습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-177">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="f7b74-178">마지막 코드 변경은 Application_Start 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-178">The last code change is in the Application_Start method.</span></span> <span data-ttu-id="f7b74-179">먼저 GetCert() 메서드를 호출하여 ClientAssertionCertificate를 로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-179">First we need to call the GetCert() method to load the ClientAssertionCertificate.</span></span> <span data-ttu-id="f7b74-180">그런 다음 새 KeyVaultClient를 만들 때 제공한 콜백 메서드를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-180">And then we change the callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="f7b74-181">이 코드는 위의 코드를 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-181">Note that this replaces the code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="f7b74-182">**Azure Portal을 통해 Web App에 인증서 추가** Web App에 인증서를 추가하는 과정은 간단한 두 단계로 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-182">**Add a Certificate to your Web App through the Azure Portal** Adding a Certificate to your Web App is a simple two-step process.</span></span> <span data-ttu-id="f7b74-183">먼저 Azure 포털로 이동하여 웹앱을 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-183">First, go to the Azure Portal and navigate to your Web App.</span></span> <span data-ttu-id="f7b74-184">웹앱에 대한 설정 블레이드에서 "사용자 지정 도메인 및 SSL" 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-184">On the Settings blade for your Web App, click on the entry for "Custom domains and SSL".</span></span> <span data-ttu-id="f7b74-185">열리는 블레이드에서 위에서 만든 인증서인 KVWebApp.pfx를 업로드할 수 있습니다. pfx에 대한 암호는 기억하고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-185">On the blade that opens you will be able to upload the Certificate that you created above, KVWebApp.pfx, make sure that you remember the password for the pfx.</span></span>

![Azure 포털에서 웹앱에 인증서 추가][2]

<span data-ttu-id="f7b74-187">마지막으로 수행해야 하는 일은 응용 프로그램 설정을 이름이 WEBSITE\_LOAD\_CERTIFICATES이고 값이 *인 웹앱에 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-187">The last thing that you need to do is to add an Application Setting to your Web App that has the name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="f7b74-188">이렇게 하면 모든 인증서가 로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-188">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="f7b74-189">업로드한 인증서만 로드하려면 지문 복사의  쉼표로 구분된 목록을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-189">If you wanted to load only the Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="f7b74-190">웹앱에 인증서 추가에 대해 자세히 알아보려면 [Azure 웹 사이트 응용 프로그램에서 인증서 사용](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="f7b74-190">To learn more about adding a Certificate to a Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="f7b74-191">**주요 자격 증명 모음에 암호로 인증서 추가** 웹앱 서비스에 인증서를 직접 업로드하는 대신, 암호로 주요 자격 증명 모음에 저장하고 해당 위치에서 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7b74-191">**Add a Certificate to Key Vault as a secret** Instead of uploading your certificate to the Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="f7b74-192">다음은 다음 블로그 게시물 [주요 자격 증명 모음을 통해 Azure 웹앱 인증서 배포](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="f7b74-192">This is a two-step process that is outlined in the following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="f7b74-193"><a id="next"></a>다음 단계</span><span class="sxs-lookup"><span data-stu-id="f7b74-193"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="f7b74-194">프로그래밍 참조는 [Azure 주요 자격 증명 모음 C# 클라이언트 API 참조](https://msdn.microsoft.com/library/azure/dn903628.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7b74-194">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
