---
title: "Azure AD 응용 프로그램 프록시 커넥터를 설치 하는 aaaSilent | Microsoft Docs"
description: "어떻게 tooperform 무인된 설치 된 Azure AD 응용 프로그램 프록시 커넥터 tooprovide 보안 된 원격 액세스 tooyour 온-프레미스 응용 프로그램에 설명 합니다."
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
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="9e1ef-103">Azure AD 응용 프로그램 프록시 커넥터 hello를 자동으로 설치</span><span class="sxs-lookup"><span data-stu-id="9e1ef-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="9e1ef-104">원하는 toobe 수 toosend toomultiple Windows 서버 또는 사용자 인터페이스를 사용 하도록 설정 하지 않은 tooWindows 서버 설치를 스크립팅 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="9e1ef-105">이 문서는 Azure AD 응용 프로그램 프록시 커넥터에 대한 무인 설치 및 등록을 수행할 수 있게 하는 Windows PowerShell 스크립트를 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="9e1ef-106">이 기능은 다음을 수행하는 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="9e1ef-107">없는 UI 레이어 또는 RDP toohello 컴퓨터 수 없는 컴퓨터에 hello 커넥터를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="9e1ef-108">한 번에 여러 커넥터를 설치하고 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="9e1ef-109">Hello 커넥터 설치 및 등록 다른 절차의 일부로 통합 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="9e1ef-110">Hello 커넥터 비트를 포함 하지만 등록 되지 않은 표준 서버 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="9e1ef-111">응용 프로그램 프록시 커넥터 네트워크 내부 hello 라는 slim Windows Server 서비스를 설치 하 여 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="9e1ef-112">Hello 응용 프로그램 프록시 커넥터 toowork가 toobe 전역 관리자 및 암호를 사용 하 여 Azure AD 디렉터리에 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="9e1ef-113">일반적으로 이러한 정보는 커넥터 설치 중에 팝업 대화 상자에서 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="9e1ef-114">그러나 Windows PowerShell 자격 증명 개체 tooenter toocreate 등록 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="9e1ef-115">또는 고유한 토큰을 만들고 tooenter 사용 수 등록 정보입니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="9e1ef-116">Hello 커넥터 설치</span><span class="sxs-lookup"><span data-stu-id="9e1ef-116">Install hello connector</span></span>
<span data-ttu-id="9e1ef-117">다음과 같이 hello 커넥터를 등록 하지 않고 hello 커넥터 Msi를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="9e1ef-118">명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-118">Open a command prompt.</span></span>
2. <span data-ttu-id="9e1ef-119">다음 명령을 /q는 hello에서 자동 설치를 의미 하는 hello 실행-hello 설치 하지 않는 묻는 tooaccept hello 최종 사용자 사용권 계약.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="9e1ef-120">Azure AD에 hello 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="9e1ef-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="9e1ef-121">Tooregister hello 커넥터를 사용할 수는 두 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="9e1ef-122">Windows PowerShell 자격 증명 개체를 사용 하 여 hello 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="9e1ef-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="9e1ef-123">오프 라인에서 만든 토큰을 사용 하 여 hello 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="9e1ef-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="9e1ef-124">Windows PowerShell 자격 증명 개체를 사용 하 여 hello 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="9e1ef-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="9e1ef-125">이 명령을 실행 하 여 hello Windows PowerShell 자격 증명 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="9e1ef-126">대체  *\<username\>*  및  *\<암호\>*  hello 사용자 이름 및 디렉터리에 대 한 암호:</span><span class="sxs-lookup"><span data-stu-id="9e1ef-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="9e1ef-127">너무 이동**C:\Program Files\Microsoft AAD 응용 프로그램 프록시 커넥터** PowerShell hello를 사용 하 여 hello 스크립트 실행 자격 증명 개체 및 만든 합니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="9e1ef-128">대체 *$cred* hello PowerShell의 hello 이름으로 자격 증명을 만들었으므로 개체:</span><span class="sxs-lookup"><span data-stu-id="9e1ef-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="9e1ef-129">오프 라인에서 만든 토큰을 사용 하 여 hello 커넥터 등록</span><span class="sxs-lookup"><span data-stu-id="9e1ef-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="9e1ef-130">Hello 코드 조각 hello 값을 사용 하 여 hello AuthenticationContext 클래스를 사용 하는 오프 라인 토큰을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
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


2. <span data-ttu-id="9e1ef-131">Hello 토큰을 사용 하는 후에 SecureString hello 토큰을 사용 하 여 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9e1ef-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="9e1ef-132">다음 Windows PowerShell 명령을, 대체 실행된 hello \<GUID를 테 넌 트\> 디렉터리 ID로:</span><span class="sxs-lookup"><span data-stu-id="9e1ef-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="9e1ef-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9e1ef-133">Next steps</span></span> 
* [<span data-ttu-id="9e1ef-134">고유한 도메인 이름을 사용하여 응용 프로그램 게시</span><span class="sxs-lookup"><span data-stu-id="9e1ef-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="9e1ef-135">Single Sign-On 사용</span><span class="sxs-lookup"><span data-stu-id="9e1ef-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="9e1ef-136">응용 프로그램 프록시에서 발생한 문제 해결</span><span class="sxs-lookup"><span data-stu-id="9e1ef-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


