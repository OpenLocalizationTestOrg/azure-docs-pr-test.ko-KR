---
title: "Azure AD 앱 프록시 커넥터 자동 설치 | Microsoft Docs"
description: "Azure AD 응용 프로그램 프록시 커넥터를 무인으로 설치하여 온-프레미스 앱에 대한 보안된 원격 액세스를 제공하는 방법에 대해 설명합니다."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9e28c89d8f64f0ae3d4150017ca544e606075c45
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="bf576-103">Azure AD 응용 프로그램 프록시 커넥터를 자동으로 설치</span><span class="sxs-lookup"><span data-stu-id="bf576-103">Silently install the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="bf576-104">사용자 인터페이스를 사용하도록 설정되지 않은 Windows Server 또는 여러 Windows 서버에 설치 스크립트를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="bf576-105">이 문서는 Azure AD 응용 프로그램 프록시 커넥터에 대한 무인 설치 및 등록을 수행할 수 있게 하는 Windows PowerShell 스크립트를 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="bf576-106">이 기능은 다음을 수행하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="bf576-107">UI 계층이 없는 경우 또는 컴퓨터에 RDP를 수행할 수 없는 경우 컴퓨터에 커넥터를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span></span>
* <span data-ttu-id="bf576-108">한 번에 여러 커넥터를 설치하고 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="bf576-109">커넥터 설치 및 등록을 다른 절차의 일부분으로 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-109">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="bf576-110">커넥터 비트를 포함하지만 등록되지 않은 표준 서버 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-110">Create a standard server image that contains the connector bits but is not registered.</span></span>

<span data-ttu-id="bf576-111">응용 프로그램 프록시는 네트워크 내부에서 커넥터라고 불리는 간단한 Windows Server 서비스를 설치하여 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-111">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span></span> <span data-ttu-id="bf576-112">응용 프로그램 프록시 커넥터가 작동하려면 전역 관리자 및 암호를 사용하여 Azure AD 디렉터리에 등록되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-112">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="bf576-113">일반적으로 이러한 정보는 커넥터 설치 중에 팝업 대화 상자에서 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="bf576-114">그러나 등록 정보를 입력하기 위해 자격 증명 개체를 만드는 데 Windows PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-114">However, you can use Windows PowerShell to create a credential object to enter your registration information.</span></span> <span data-ttu-id="bf576-115">또는 고유한 토큰을 만들고 등록 정보를 입력하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-115">Or you can create your own token and use it to enter your registration information.</span></span>

## <a name="install-the-connector"></a><span data-ttu-id="bf576-116">커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="bf576-116">Install the connector</span></span>
<span data-ttu-id="bf576-117">다음과 같이 커넥터를 등록하지 않고 커넥터 MSI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-117">Install the Connector MSIs without registering the Connector as follows:</span></span>

1. <span data-ttu-id="bf576-118">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-118">Open a command prompt.</span></span>
2. <span data-ttu-id="bf576-119">다음 명령을 실행합니다. 여기서 /q는 무인 설치를 의미하며 설치 시 최종 사용자 사용권 계약에 동의할지 묻는 메시지가 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-119">Run the following command in which the /q means quiet installation - the installation doesn't prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a><span data-ttu-id="bf576-120">Azure AD에 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="bf576-120">Register the connector with Azure AD</span></span>
<span data-ttu-id="bf576-121">커넥터를 등록하는 데 사용할 수 있는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-121">There are two methods you can use to register the connector:</span></span>

* <span data-ttu-id="bf576-122">Windows PowerShell 자격 증명 개체를 사용하여 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="bf576-122">Register the connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="bf576-123">오프라인에서 만든 토큰을 사용하여 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="bf576-123">Register the connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="bf576-124">Windows PowerShell 자격 증명 개체를 사용하여 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="bf576-124">Register the connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="bf576-125">이 명령을 실행하여 Windows PowerShell 자격 증명 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-125">Create the Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="bf576-126">*\<사용자 이름\>* 및 *\<암호\>*를 디렉터리에 대한 사용자 이름과 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-126">Replace *\<username\>* and *\<password\>* with the username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="bf576-127">**C:\Program Files\Microsoft AAD App Proxy Connector**로 이동하여 만든 PowerShell 자격 증명 개체를 사용하여 해당 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created.</span></span> <span data-ttu-id="bf576-128">*$cred*를 만든 PowerShell 자격 증명 개체의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-128">Replace *$cred* with the name of the PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="bf576-129">오프라인에서 만든 토큰을 사용하여 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="bf576-129">Register the connector using a token created offline</span></span>
1. <span data-ttu-id="bf576-130">코드 조각의 값을 사용하여 AuthenticationContext 클래스를 사용하는 오프라인 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-130">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// The application ID of the connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// The reply address of the connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// The AppIdUri of the registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. <span data-ttu-id="bf576-131">토큰을 만들었으면 토큰을 사용하여 SecureString을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-131">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="bf576-132">다음 Windows PowerShell 명령을 실행하여 \<테넌트 GUID\>를 디렉터리 ID로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="bf576-132">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="bf576-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="bf576-133">Next steps</span></span> 
* [<span data-ttu-id="bf576-134">고유한 도메인 이름을 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="bf576-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="bf576-135">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="bf576-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="bf576-136">응용 프로그램 프록시에서 발생한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="bf576-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


