---
title: "AD FS 인증에 사용 되는 기간 업무 Azure 앱 aaaCreate | Microsoft Docs"
description: "어떻게 toocreate는 기간 업무 앱을 인증 하 고 있는 Azure 앱 서비스의 온-프레미스 STS에 알아봅니다. 이 자습서에는 AD FS 온-프레미스 STS hello으로 대상으로 합니다."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="7c308-104">AD FS 인증을 사용하여 LOB(기간 업무) Azure 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7c308-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="7c308-105">이 문서에서는 어떻게 toocreate는 ASP.NET MVC의 업무 응용 프로그램에서 [Azure 앱 서비스](../app-service/app-service-value-prop-what-is.md) 온-프레미스를 사용 하 여 [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) hello id 공급자로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="7c308-106">이 시나리오는 toocreate 기간 업무 응용 프로그램을 Azure 앱 서비스의 원하는 었 조직 디렉터리 데이터 toobe 온사이트에 저장에 필요한 경우 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="7c308-107">Azure 앱 서비스에 대 한 hello 다른 엔터프라이즈 인증 및 권한 부여 옵션의 개요를 참조 하십시오. [Azure 응용 프로그램에서 온-프레미스 Active Directory로 인증](web-sites-authentication-authorization.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="7c308-108">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="7c308-108">What you will build</span></span>
<span data-ttu-id="7c308-109">같은 기능 hello로 Azure 앱 서비스 웹 앱에서 기본 ASP.NET 응용 프로그램을 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="7c308-110">AD FS에 대해 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="7c308-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="7c308-111">사용 하 여 `[Authorize]` 다양 한 작업에 대 한 tooauthorize 사용자</span><span class="sxs-lookup"><span data-stu-id="7c308-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="7c308-112">Visual Studio에서 디버깅와 tooApp 서비스 웹 앱 게시에 대 한 고정 구성을 (한 번의 구성, 디버깅 및 게시를 언제 든 지)</span><span class="sxs-lookup"><span data-stu-id="7c308-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="7c308-113">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="7c308-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="7c308-114">이 자습서 toocomplete 다음 hello 필요:</span><span class="sxs-lookup"><span data-stu-id="7c308-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="7c308-115">온-프레미스 AD FS 배포 (이 자습서에 사용 된 hello 테스트 랩의 종단 간 연습을 참조 하십시오. [테스트 랩: (테스트에만 해당)에 대 한 Azure VM의 AD FS와 함께 독립 실행형 STS](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="7c308-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="7c308-116">사용 권한 toocreate 신뢰 당사자 트러스트가 AD FS 관리 있습니다</span><span class="sxs-lookup"><span data-stu-id="7c308-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="7c308-117">Visual Studio 2013 업데이트 4 이상</span><span class="sxs-lookup"><span data-stu-id="7c308-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="7c308-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) 이상</span><span class="sxs-lookup"><span data-stu-id="7c308-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="7c308-119">기간 업무 템플릿에 예제 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="7c308-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="7c308-120">이 자습서에서는 샘플 응용 프로그램 hello [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), hello Azure Active Directory 팀에서 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="7c308-121">AD FS Ws-federation을 지 원하는 하므로 손쉽게 템플릿 toocreate 기간 업무 응용 프로그램으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="7c308-122">같은 기능 hello 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-122">It has hello following features:</span></span>

* <span data-ttu-id="7c308-123">사용 하 여 [WS-페더레이션](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate 온-프레미스 AD FS 배포</span><span class="sxs-lookup"><span data-stu-id="7c308-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="7c308-124">로그인 및 로그아웃 기능</span><span class="sxs-lookup"><span data-stu-id="7c308-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="7c308-125">사용 하 여 [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (Windows Identity Foundation)를 대신 하는 hello ASP.NET 및 WIF 보다 인증 및 권한 부여에 대해 훨씬 더 간단 tooset의 이후</span><span class="sxs-lookup"><span data-stu-id="7c308-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="7c308-126">Hello 샘플 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="7c308-126">Set up hello sample application</span></span>
1. <span data-ttu-id="7c308-127">복제 또는에 hello 샘플 솔루션 다운로드 [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour 로컬 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7c308-128">지침에 hello [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) 방법을 보여 줍니다 tooset Azure Active Directory와 hello 응용 프로그램을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="7c308-129">하지만이 자습서에서는 AD FS를 사용 하 여 설정 하면,이 따라서 대신 hello 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="7c308-130">Hello 솔루션을 연 다음 Controllers\AccountController.cs hello에 **솔루션 탐색기**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="7c308-131">Hello 코드에 단순히 Ws-federation을 사용 하는 인증 챌린지 tooauthenticate hello 사용자 문제를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="7c308-132">모든 인증은 App_Start\Startup.Auth.cs에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="7c308-133">App_Start\Startup.Auth.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="7c308-134">Hello에 `ConfigureAuth` 메서드, 참고 hello 줄:</span><span class="sxs-lookup"><span data-stu-id="7c308-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="7c308-135">Hello OWIN 환경에서이 코드 조각은 실제로 hello tooconfigure WS-페더레이션 인증 필요한 최소 운영 체제 미 설치입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="7c308-136">것이 훨씬 쉽고 hello 장소 전 세계 Web.config XML로 주입 여기서 WIF 보다 더 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="7c308-137">필요한 정보 hello의 RP (신뢰 당사자) 파일인 hello AD FS 서비스의 메타 데이터 파일의 URL 식별자 및 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="7c308-138">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-138">Here's an example:</span></span>
   
   * <span data-ttu-id="7c308-139">RP 식별자: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="7c308-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="7c308-140">메타데이터 주소: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="7c308-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="7c308-141">App_Start\Startup.Auth.cs, hello 다음 정적 문자열 정의 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="7c308-142">Web.config의 hello 해당 변경 내용을 확인 합니다. Hello Web.config를 열고 hello 다음 응용 프로그램 설정을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="7c308-143">해당 환경에 따라 hello 키 값을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="7c308-144">오류가 없는 있는지 hello 응용 프로그램 toomake를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="7c308-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="7c308-145">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-145">That's it.</span></span> <span data-ttu-id="7c308-146">이제 hello 샘플 응용 프로그램은 AD FS와 함께 준비 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="7c308-147">이 응용 프로그램으로 AD FS에서 나중에 RP trust tooconfigure를 보내야합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="7c308-148">Hello 샘플 응용 프로그램 tooAzure 앱 서비스 웹 앱 배포</span><span class="sxs-lookup"><span data-stu-id="7c308-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="7c308-149">여기에서는 있습니다 hello 응용 프로그램 tooa web app을 게시 앱 서비스 웹 앱에서 hello 디버그 환경 유지 하면서 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="7c308-150">Note 하 겠 군요 toopublish hello 응용 프로그램 인증 여전히 작동 하지 않으면 아직 하므로 RP trust AD FS와 함께 갖기 전에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="7c308-151">그러나 이렇게 하면 이제 가질 수 있습니다 tooconfigure hello RP trust을 나중에 사용할 수 있는 hello 웹 앱 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="7c308-152">프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="7c308-153">**Microsoft Azure 앱 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="7c308-154">TooAzure에 서명 하지 않은 경우 클릭 **로그인** 에 Azure 구독 toosign 프로그램에 대 한 hello Microsoft 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="7c308-155">로그인 한 후 클릭 **새로** toocreate 웹 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="7c308-156">모든 필수 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-156">Fill in all required fields.</span></span> <span data-ttu-id="7c308-157">하려고 tooconnect tooon 온-프레미스 데이터 나중 하므로이 웹 앱에 대 한 데이터베이스를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="7c308-158">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-158">Click **Create**.</span></span> <span data-ttu-id="7c308-159">Hello 웹 응용 프로그램을 만든 후에 hello 웹 게시 대화 상자를 열면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="7c308-160">**대상 URL**, 변경 **http** 너무**https**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="7c308-161">복사 hello 전체 URL tooa 텍스트 편집기 나중에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="7c308-162">그런 다음 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="7c308-163">Visual Studio에서 프로젝트의 **Web.Release.config** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="7c308-164">Hello에 다음과 같은 XML hello 삽입 `<configuration>` 태그, 및 hello 키 값을 게시 웹 앱의 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="7c308-165">완료 되 면 Visual Studio에서 디버그 환경에 대 한 프로젝트에 구성 된 두 개의 RP 식별자가 있으며 Azure에서 웹 앱을 게시 한 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="7c308-166">각 AD FS에서 두 가지 환경 hello에 대 한 RP 트러스트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="7c308-167">디버깅 하는 동안 hello 응용 프로그램의 Web.config 설정이 사용 되는 toomake 프로그램 **디버그** AD FS와 함께 구성 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="7c308-168">게시 되는 경우 (기본적으로 hello **릴리스** 구성 게시), 통합 hello Web.Release.config에 응용 프로그램은 설정을 변경 하는 변환 된 Web.config 업로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="7c308-169">Hello의 복제본을 만들 수 있습니다, (예: hello 게시 된 웹 앱에서 코드의 디버그 기호를 업로드 해야 합니다) Azure toohello 디버거에서 디버그, 디버깅 하는 Azure에 대 한 구성 하지만 고유한 사용자 지정 Web.config 사용 (변환할 tooattach hello 게시 된 웹 앱에 포함 하려는 경우 예를 들어 Web.AzureDebug.config) Web.Release.config에서 응용 프로그램 설정을 hello를 사용 하 합니다. 이렇게 하면 있습니다 toomaintain 고정 구성을 hello 서로 다른 환경에서.</span><span class="sxs-lookup"><span data-stu-id="7c308-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="7c308-170">AD FS 관리에서 신뢰 당사자 트러스트 구성</span><span class="sxs-lookup"><span data-stu-id="7c308-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="7c308-171">이제 있어야만 tooconfigure는 RP trust AD FS 관리에서 샘플 응용 프로그램을 사용 하 고 AD FS와 함께 실제로 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="7c308-172">디버그 환경 및 게시 된 웹 앱에 대 한 두 개의 별도 RP 트러스트를 tooset 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="7c308-173">Hello 사용자 환경의 둘 다에 대해 다음 단계를 반복 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="7c308-174">AD FS 서버에서 관리 권한 tooAD FS 권한이 있는 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="7c308-175">AD FS 관리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-175">Open AD FS Management.</span></span> <span data-ttu-id="7c308-176">**AD FS\Trusted Relationships\Relying Party Trusts**를 마우스 오른쪽 단추로 클릭하고 **신뢰 당사자 트러스트 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="7c308-177">Hello에 **데이터 원본 선택** 페이지 **hello 신뢰 당사자에 대 한 데이터를 직접 입력**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="7c308-178">Hello에 **표시 이름 지정** 페이지 hello 응용 프로그램에 대 한 표시 이름을 입력 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="7c308-179">Hello에 **프로토콜 선택** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="7c308-180">Hello에 **인증서 구성** 페이지 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7c308-181">HTTPS를 이미 사용하고 있으므로 암호화된 토큰은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="7c308-182">이 페이지에서 AD FS에서 tooencrypt 토큰을 원하는 경우에 코드에도 토큰 암호 해독 논리를 추가할 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="7c308-183">자세한 내용은 [OWIN WS-Federation 미들웨어를 수동으로 구성하고 암호화된 토큰 적용](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c308-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="7c308-184">Hello 다음 단계로 이동 하기 전에 Visual Studio 프로젝트에서 하나의 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="7c308-185">Hello 프로젝트 속성에서 확인 hello **SSL URL** hello 응용 프로그램의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="7c308-186">Hello에 AD FS 관리에 다시 **URL 구성** hello 페이지 **신뢰 당사자 트러스트 추가 마법사**선택, **hello Ws-federation 수동 프로토콜 지원 사용** 및 hello 이전 단계에서 기록해둔 hello Visual Studio 프로젝트의 SSL URL에에서 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="7c308-187">그런 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="7c308-188">URL은 toosend hello 클라이언트 인증이 성공 하면를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="7c308-189">Hello 디버그 환경에 대 한 것 <code>https://localhost:&lt;port&gt;/</code>합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="7c308-190">Hello 게시 된 웹 앱에 대 한 hello 웹 앱 URL 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="7c308-191">Hello에 **식별자 구성** 페이지 SSL URL을 프로젝트에 이미 나열 되어 있는지 확인 하 고 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="7c308-192">클릭 **다음** 기본 선택 항목으로 hello 마법사의 방식으로 toohello 마지막 hello 모든 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7c308-193">Visual Studio 프로젝트의 App_Start\Startup.Auth.cs에서이 식별자는 일치의 hello 값 <code>WsFederationAuthenticationOptions.Wtrealm</code> 페더레이션된 인증 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="7c308-194">기본적으로 hello 이전 단계의 hello 응용 프로그램의 URL은 RP 식별자로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="7c308-195">이제 AD FS에서 hello RP 응용 프로그램 프로젝트에 대 한 구성 작업이 완료 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="7c308-196">이제이 응용 프로그램 toosend 구성 hello 클레임 응용 프로그램에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="7c308-197">hello **클레임 규칙 편집** 대화 상자가 열려 기본적으로 사용자에 대 한 hello 마법사 hello 끝나기 전에 즉시 시작할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="7c308-198">구성 (스키마와 함께 괄호 안에 있음) 클레임 다음 hello 이상:</span><span class="sxs-lookup"><span data-stu-id="7c308-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="7c308-199">ASP.NET toohydrate에서 사용 하는 이름 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name)- `User.Identity.Name`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="7c308-200">사용자 계정 이름 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn)-사용 되는 toouniquely hello 조직에서 사용자를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="7c308-201">와 함께 사용할 수 역할로 (http://schemas.microsoft.com/ws/2008/06/identity/claims/role)-그룹 구성원 자격 `[Authorize(Roles="role1, role2,...")]` 장식 tooauthorize 컨트롤러/작업 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="7c308-202">실제로이 방법을 사용 될 수 있습니다 되지 수 hello 역할 권한 부여에 대 한 대부분 고성능 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="7c308-203">AD 사용자가 속하는 보안 그룹의 toohundreds, 수백 hello SAML 토큰에서 역할 클레임의 되 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="7c308-204">또 다른 방법은 단일 역할 hello 사용자의 특정 그룹 구성원 자격에 따라 조건부로 클레임 toosend 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="7c308-205">하지만 이 자습서에서는 이 접근 방식을 단순한 형태로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="7c308-206">이름 ID(http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier)는 위조 방지 유효성 검사를 위해 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="7c308-207">어떻게 toomake 작동 위조 방지 유효성 검사에 대 한 자세한 내용은 참조 hello **기간 업무 기능을 추가할** 의 섹션 [Azure Active Directory 인증으로 업무의 Azure 응용 프로그램 만들기 ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="7c308-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="7c308-208">hello 클레임 형식에 응용 프로그램은 응용 프로그램의 요구 사항에 따라 결정 tooconfigure 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="7c308-209">Azure Active Directory 응용 프로그램 (즉, RP 트러스트)에서 지원 되는 클레임의 hello 목록에 대 한 예를 들어 참조 [지원 되는 토큰 및 클레임 유형](http://msdn.microsoft.com/library/azure/dn195587.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="7c308-210">Hello 클레임 규칙 편집 대화 상자에서 **규칙 추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="7c308-211">Hello 스크린샷에 표시 된 대로 hello 이름, UPN 및 역할 클레임을 구성 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="7c308-212">다음으로 일시적인 이름 ID 클레임에서 보여 준 hello 단계를 사용 하 여 만듭니다 [SAML 어설션 식별자 이름](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="7c308-213">**규칙 추가** 를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="7c308-214">**사용자 지정 규칙을 사용하여 클레임 보내기**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="7c308-215">붙여넣기 hello 다음 hello에 언어 규칙 **사용자 지정 규칙** 상자, 이름 hello 규칙 **세션 식별자 당** 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    <span data-ttu-id="7c308-216">사용자 지정 규칙은 이 스크린샷과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="7c308-217">**규칙 추가** 를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="7c308-218">**들어오는 클레임 변환**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="7c308-219">(Hello 사용자 지정 규칙에서 만든 hello 클레임 유형을 사용 하 여) hello 스크린샷에 표시 된 대로 hello 규칙을 구성 하 고 클릭 **마침**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="7c308-220">Hello 일시적인 이름 ID 클레임에 대 한 hello 단계에 대 한 자세한 내용은 참조 하십시오. [SAML 어설션 식별자 이름](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="7c308-221">클릭 **적용** hello에 **클레임 규칙 편집** 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="7c308-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="7c308-222">이 파일은 이제 같아야 스크린 샷 다음 hello:</span><span class="sxs-lookup"><span data-stu-id="7c308-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="7c308-223">즉, 디버그 환경과 게시된 웹 앱 둘 다에 대해 이러한 단계를 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="7c308-224">응용 프로그램에 대한 페더레이션 인증 테스트</span><span class="sxs-lookup"><span data-stu-id="7c308-224">Test federated authentication for your application</span></span>
<span data-ttu-id="7c308-225">사용자는 준비 tootest AD FS에 대 한 응용 프로그램의 인증 논리입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="7c308-226">내 AD FS 랩 환경에서 tooa 테스트 그룹에 AD (Active Directory)에 속하는 테스트 사용자를 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="7c308-227">하기만 하면 toodo 이제 hello 디버거에서 tootest 인증 형식이 `F5`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="7c308-228">Hello 게시 된 웹 응용 프로그램에서 tootest 인증 하려는 경우 toohello URL을 탐색 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="7c308-229">Hello 웹 응용 프로그램에 로드 된 후 클릭 **로그인**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="7c308-230">이제 중 하나는 로그인 대화 상자 또는 hello 로그인 페이지에 AD FS에서 선택한 hello 인증 방법에 따라 AD FS을 구해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="7c308-231">다음은 Internet Explorer 11의 화면 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="7c308-232">사용 하 여 다시 hello 홈 페이지 이제 표시 hello AD FS 배포의 hello AD 도메인에서 사용자를 사용 하 여 로그온 한 후 **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="7c308-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="7c308-233">hello 구석에 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-233">in hello corner.</span></span> <span data-ttu-id="7c308-234">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="7c308-235">지금까지 다음 방법으로 hello 성공:</span><span class="sxs-lookup"><span data-stu-id="7c308-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="7c308-236">응용 프로그램에 AD FS를 성공적으로 도달 하 고 hello AD FS 데이터베이스에서에서 일치 하는 RP 식별자를 찾을 수합니다</span><span class="sxs-lookup"><span data-stu-id="7c308-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="7c308-237">AD FS에는 AD 사용자 및 toohello 응용 프로그램의 홈 페이지를 다시 리디렉션 성공적으로 인증 된</span><span class="sxs-lookup"><span data-stu-id="7c308-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="7c308-238">해당 hello 사용자 hello 팩트에 표시 된 대로 성공적으로 보낸된 hello 이름으로 AD FS 클레임 (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour 응용 프로그램 이름이 hello 모서리에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="7c308-239">Hello 이름 클레임이 없는 경우 했겠지만 **Hello,!**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="7c308-240">Views\Shared 보면\_사용 하는 것을 찾을 LoginPartial.cshtml, `User.Identity.Name` toodisplay hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="7c308-241">Hello 이름 hello SAML 토큰에서 사용할 수 있는 사용자가 인증 된 hello의 청구 하는 경우 이전에 언급 했 듯이 ASP.NET hydrates 함께이 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="7c308-242">모든 hello toosee Index 작업 메서드의 hello에서 Controllers\HomeController.cs에 중단점을 배치 하는 AD FS에서 전송 된 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="7c308-243">Hello 사용자가 인증 되 면 hello 검사 `System.Security.Claims.Current.Claims` 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="7c308-244">사용자에게 특정 컨트롤러 또는 작업에 대한 권한 부여</span><span class="sxs-lookup"><span data-stu-id="7c308-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="7c308-245">RP 신뢰 구성에서 역할 클레임으로 그룹 멤버 자격을 포함 한, 있으므로 이제 사용할 수 있습니다 이러한 hello에 직접 `[Authorize(Roles="...")]` 컨트롤러 및 작업에 대 한 장식 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="7c308-246">Hello 만들기-읽기-업데이트-삭제 (CRUD) 패턴으로 기간 업무 응용 프로그램에서는 특정 역할 tooaccess 각 동작을 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="7c308-247">이제 방금 hello 기존 홈 컨트롤러에이 기능을 미리 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="7c308-248">Controllers\HomeController.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="7c308-249">Hello 데코레이팅 `About` 및 `Contact` 동작 메서드 비슷한 toohello 코드 다음, 인증 된 사용자가 보안 그룹 구성원 자격을 사용 하 여 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    <span data-ttu-id="7c308-250">추가한 이후 **테스트 사용자** 너무**테스트 그룹** 내 AD FS 랩 환경에서 테스트 그룹 tootest 권한 부여에 사용 합니다 I `About`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="7c308-251">에 대 한 `Contact`의 hello 음수일 경우 테스트할 **Domain Admins**, toowhich **테스트 사용자** 속해 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="7c308-252">입력 하 여 hello 디버거를 시작 `F5` 로그인 하 고 다음 클릭 **에 대 한**합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="7c308-253">지금 표시할 수 있습니다 hello `~/About/Index` 페이지 성공적으로 인증 된 사용자가 해당 작업에 대 한 권한을 부여 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="7c308-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="7c308-254">클릭 하 여 지금 **연락처**, 여기서에서는 승인 하지 해야 **테스트 사용자** hello 동작에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="7c308-255">그러나 hello 브라우저 리디렉션된 tooAD FS, 결국이 메시지를 표시 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="7c308-256">AD FS 서버 hello에 이벤트 뷰어에서이 오류를 조사 하는 경우이 예외 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="7c308-257">이 오류에 대 한 hello 이유는 기본적으로 MVC 반환 401 권한 없음 사용자 역할은 권한이 없는 경우는입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="7c308-258">재인증 요청 tooyour id 공급자를 (AD FS)를 트리거합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="7c308-259">Hello 사용자가 이미 인증 AD FS toohello 반환 같은 페이지에서 리디렉션 루프를 작성 하는 다른 401을 발급 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="7c308-260">AuthorizeAttribute의 대체 `HandleUnauthorizedRequest` 간단한 논리 tooshow 사용 메서드를 계속 hello 리디렉션 루프 대신 의미가 있는 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="7c308-261">AuthorizeAttribute.cs, 및 코드를 다음 붙여넣기 hello 라는 hello 프로젝트에서 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    <span data-ttu-id="7c308-262">hello 코드 보냅니다 HTTP 403 (금지 됨) HTTP 401 (권한 없음) 하는 대신 인증 된 하지만 권한이 없는 경우에서를 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="7c308-263">사용 하 여 다시 hello 디버거 실행 `F5`합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="7c308-264">이제 **Contact** 를 클릭하면 보다 자세한(중요하지는 않음) 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="7c308-265">Hello 응용 프로그램 tooAzure 앱 서비스 웹 앱을 다시 게시 하 고 hello 라이브 응용 프로그램의 hello 동작을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="7c308-266">Tooon 온-프레미스 데이터 연결</span><span class="sxs-lookup"><span data-stu-id="7c308-266">Connect tooon-premises data</span></span>
<span data-ttu-id="7c308-267">Tooimplement AD fs를 Azure Active Directory 대신 기간 업무 응용 프로그램을 사용할 수 있는지는 이유는 조직의 데이터 오프-프레미스를 유지 하는 규정 준수 문제입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="7c308-268">Toouse 수 있으므로 Azure에서 웹 앱이 온-프레미스 데이터베이스를 액세스 해야 또한 것일 [SQL 데이터베이스](/services/sql-database/) 웹 앱에 대 한 hello 데이터 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="7c308-269">Azure App Service Web Apps는 [하이브리드 연결](../biztalk-services/integration-hybrid-connection-overview.md) 및 [가상 네트워크](web-sites-integrate-with-vnet.md)의 두 가지 방법으로 온-프레미스 데이터베이스 액세스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7c308-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="7c308-270">자세한 내용은 [Azure App Service Web Apps에서 VNET 통합 및 하이브리드 연결 사용](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7c308-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="7c308-271">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="7c308-271">Further resources</span></span>
* [<span data-ttu-id="7c308-272">Azure 앱에서 온-프레미스 Active Directory를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="7c308-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="7c308-273">Azure Active Directory 인증을 사용하여 LOB(기간 업무) Azure 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7c308-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="7c308-274">Visual Studio 2013에서 온-프레미스 조직 인증 옵션 (ADFS)으로 ASP.NET hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7c308-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="7c308-275">VS2013 웹 프로젝트에서 WIF tooKatana 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="7c308-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="7c308-276">Active Directory Federation Services 개요</span><span class="sxs-lookup"><span data-stu-id="7c308-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="7c308-277">WS-Federation 1.1 사양</span><span class="sxs-lookup"><span data-stu-id="7c308-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

