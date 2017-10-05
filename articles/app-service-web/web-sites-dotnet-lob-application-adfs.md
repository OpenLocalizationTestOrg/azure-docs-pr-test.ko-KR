---
title: "AD FS 인증을 사용하여 LOB(기간 업무) Azure 앱 만들기 | Microsoft Docs"
description: "Azure App Service에서 온-프레미스 STS로 인증하는 LOB(기간 업무) 앱을 만드는 방법에 대해 알아봅니다. 이 자습서에서는 AD FS를 온-프레미스 STS로 사용합니다."
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
ms.openlocfilehash: f9a8984400378d154a504af8a41609900128d052
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="0b4a7-104">AD FS 인증을 사용하여 LOB(기간 업무) Azure 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0b4a7-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="0b4a7-105">이 문서에서는 온-프레미스 [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx)를 ID 공급자로 사용하여 [Azure App Service](../app-service/app-service-value-prop-what-is.md)에서 ASP.NET MVC LOB(기간 업무) 응용 프로그램을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-105">This article shows you how to create an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as the identity provider.</span></span> <span data-ttu-id="0b4a7-106">이 시나리오는 Azure App Service에서 기간 업무 응용 프로그램을 만들 때 조직의 규정에 따라 디렉터리 데이터를 온사이트에 저장해야 하는 경우에 적용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-106">This scenario can work when you want to create line-of-business applications in Azure App Service but your organization requires directory data to be stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="0b4a7-107">Azure App Service에 대한 다른 엔터프라이즈 인증 및 권한 부여 옵션의 개요는 [Azure 앱에서 온-프레미스 Active Directory를 사용하여 인증](web-sites-authentication-authorization.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-107">For an overview of the different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="0b4a7-108">빌드할 내용</span><span class="sxs-lookup"><span data-stu-id="0b4a7-108">What you will build</span></span>
<span data-ttu-id="0b4a7-109">Azure 앱 서비스 웹 앱에서 다음 기능이 있는 기본 ASP.NET 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-109">You will build a basic ASP.NET application in Azure App Service Web Apps with the following features:</span></span>

* <span data-ttu-id="0b4a7-110">AD FS에 대해 사용자 인증</span><span class="sxs-lookup"><span data-stu-id="0b4a7-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="0b4a7-111">`[Authorize]` 를 사용하여 다른 동작에 대해 사용자에게 권한 부여</span><span class="sxs-lookup"><span data-stu-id="0b4a7-111">Uses `[Authorize]` to authorize users for different actions</span></span>
* <span data-ttu-id="0b4a7-112">Visual Studio에서의 디버깅 및 앱 서비스 웹 앱에 게시 둘 다에 대한 정적 구성(한 번 구성하여 언제든 디버그 및 게시)</span><span class="sxs-lookup"><span data-stu-id="0b4a7-112">Static configuration for both debugging in Visual Studio and publishing to App Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="0b4a7-113">필요한 항목</span><span class="sxs-lookup"><span data-stu-id="0b4a7-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="0b4a7-114">이 자습서를 완료하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-114">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="0b4a7-115">온-프레미스 AD FS 배포(이 자습서에서 사용된 테스트 랩의 종단 간 연습은 [테스트 랩: Azure VM에서 AD FS를 사용한 독립 실행형 STS(테스트 전용)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/)참조)</span><span class="sxs-lookup"><span data-stu-id="0b4a7-115">An on-premises AD FS deployment (for an end-to-end walkthrough of the test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="0b4a7-116">AD FS 관리에서 신뢰 당사자 트러스트를 만들 수 있는 권한</span><span class="sxs-lookup"><span data-stu-id="0b4a7-116">Permissions to create relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="0b4a7-117">Visual Studio 2013 업데이트 4 이상</span><span class="sxs-lookup"><span data-stu-id="0b4a7-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="0b4a7-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) 이상</span><span class="sxs-lookup"><span data-stu-id="0b4a7-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="0b4a7-119">기간 업무 템플릿에 예제 응용 프로그램 사용</span><span class="sxs-lookup"><span data-stu-id="0b4a7-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="0b4a7-120">이 자습서의 예제 응용 프로그램( [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet)은 Azure Active Directory 팀이 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-120">The sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by the Azure Active Directory team.</span></span> <span data-ttu-id="0b4a7-121">AD FS는 WS-Federation을 지원하므로 이를 템플릿으로 사용하여 LOB(기간 업무) 응용 프로그램을 손쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-121">Since AD FS supports WS-Federation, you can use it as a template to create line-of-business applications with ease.</span></span> <span data-ttu-id="0b4a7-122">제공되는 기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-122">It has the following features:</span></span>

* <span data-ttu-id="0b4a7-123">[WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) 을 사용하여 온-프레미스 AD FS 배포로 인증</span><span class="sxs-lookup"><span data-stu-id="0b4a7-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) to authenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="0b4a7-124">로그인 및 로그아웃 기능</span><span class="sxs-lookup"><span data-stu-id="0b4a7-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="0b4a7-125">[Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana)(Windows Identity Foundation 대신)을 사용합니다. 이는 ASP.NET의 미래이며 WIF보다 인증 및 권한 부여 설정이 훨씬 간편합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is the future of ASP.NET and much simpler to set up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-the-sample-application"></a><span data-ttu-id="0b4a7-126">예제 응용 프로그램 설정</span><span class="sxs-lookup"><span data-stu-id="0b4a7-126">Set up the sample application</span></span>
1. <span data-ttu-id="0b4a7-127">[WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) 에서 로컬 디렉터리에 예제 솔루션을 복제하거나 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-127">Clone or download the sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) to your local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0b4a7-128">[README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) 의 지침은 Azure Active Directory를 사용하여 응용 프로그램을 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-128">The instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how to set up the application with Azure Active Directory.</span></span> <span data-ttu-id="0b4a7-129">그러나 이 자습서에서는 AD FS를 사용하여 설정하므로 대신 여기의 단계를 따르세요.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-129">But in this tutorial, you set it up with AD FS, so follow the steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="0b4a7-130">솔루션을 열고 **솔루션 탐색기**에서 Controllers\AccountController.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-130">Open the solution, and then open Controllers\AccountController.cs in the **Solution Explorer**.</span></span>
   
   <span data-ttu-id="0b4a7-131">코드가 단순히 인증 챌린지를 실행하여 WS-Federation을 통해 사용자를 인증하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-131">You will see that the code simply issues an authentication challenge to authenticate the user using WS-Federation.</span></span> <span data-ttu-id="0b4a7-132">모든 인증은 App_Start\Startup.Auth.cs에서 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="0b4a7-133">App_Start\Startup.Auth.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="0b4a7-134">`ConfigureAuth` 메서드에서 다음 줄을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-134">In the `ConfigureAuth` method, note the line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="0b4a7-135">OWIN 환경에서 이 코드 조각은 실제로 WS-Federation 인증을 구성하는 데 필요한 최소 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-135">In the OWIN world, this snippet is really the bare minimum you need to configure WS-Federation authentication.</span></span> <span data-ttu-id="0b4a7-136">이는 Web.config의 여러 곳에 XML이 주입되는 WIF보다 훨씬 단순하고 세련된 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over the place.</span></span> <span data-ttu-id="0b4a7-137">필요한 정보는 RP(신뢰 당사자)의 식별자와 AD FS 서비스의 메타데이터 파일 URL뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-137">The only information you need is the relying party's (RP) identifier and the URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="0b4a7-138">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-138">Here's an example:</span></span>
   
   * <span data-ttu-id="0b4a7-139">RP 식별자: `https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="0b4a7-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="0b4a7-140">메타데이터 주소: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="0b4a7-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="0b4a7-141">App_Start\Startup.Auth.cs에서 다음 정적 문자열 정의를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-141">In App_Start\Startup.Auth.cs, change the following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="0b4a7-142">이제 해당 Web.config를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-142">Now, make the corresponding changes in Web.config.</span></span> <span data-ttu-id="0b4a7-143">Web.config를 열고 다음 앱 설정을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-143">Open the Web.config and modify the following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter the App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter the relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter the FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="0b4a7-144">각 환경을 기반으로 키 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-144">Fill in the key values based on your respective environment.</span></span>
6. <span data-ttu-id="0b4a7-145">응용 프로그램을 빌드하여 오류가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-145">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="0b4a7-146">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-146">That's it.</span></span> <span data-ttu-id="0b4a7-147">이제 예제 응용 프로그램이 AD FS에서 작동할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-147">Now the sample application is ready to work with AD FS.</span></span> <span data-ttu-id="0b4a7-148">나중에 AD FS에서 이 응용 프로그램과 RP 트러스트를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-148">You still need to configure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-the-sample-application-to-azure-app-service-web-apps"></a><span data-ttu-id="0b4a7-149">Azure 앱 서비스 웹 앱에 샘플 응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="0b4a7-149">Deploy the sample application to Azure App Service Web Apps</span></span>
<span data-ttu-id="0b4a7-150">여기에서는 디버그 환경을 유지하는 동안 App Service Web Apps에서 웹앱에 응용 프로그램을 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-150">Here, you publish the application to a web app in App Service Web Apps while preserving the debug environment.</span></span> <span data-ttu-id="0b4a7-151">AD FS와의 RP 트러스트가 설정되기 전에 응용 프로그램을 게시할 것이므로 인증은 아직 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-151">Note that you're going to publish the application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="0b4a7-152">하지만 이렇게 한 경우 나중에 RP 트러스트를 구성하는 데 사용할 수 있는 웹앱 URL이 생성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-152">However, if you do it now you can have the web app URL that you can use to configure the RP trust later.</span></span>

1. <span data-ttu-id="0b4a7-153">프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-153">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="0b4a7-154">**Microsoft Azure 앱 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-154">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="0b4a7-155">Azure에 로그인하지 않은 경우 **로그인** 을 클릭하고 Azure 구독에 대한 Microsoft 계정을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-155">If you haven't signed in to Azure, click **Sign In** and use the Microsoft account for your Azure subscription to sign in.</span></span>
4. <span data-ttu-id="0b4a7-156">로그인되면 **새로 만들기** 를 클릭하여 웹앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-156">Once signed in, click **New** to create a web app.</span></span>
5. <span data-ttu-id="0b4a7-157">모든 필수 필드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-157">Fill in all required fields.</span></span> <span data-ttu-id="0b4a7-158">온-프레미스 데이터에는 나중에 연결할 것이므로 이 웹앱에 대한 데이터베이스를 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-158">You are going to connect to on-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="0b4a7-159">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-159">Click **Create**.</span></span> <span data-ttu-id="0b4a7-160">웹 앱이 만들어지면 웹 게시 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-160">Once the web app is created, the Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="0b4a7-161">**대상 URL**에서 **http**를 **https**로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-161">In **Destination URL**, change **http** to **https**.</span></span> <span data-ttu-id="0b4a7-162">나중에 사용하기 위해 전체 URL을 텍스트 편집기에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-162">Copy the entire URL to a text editor for later use.</span></span> <span data-ttu-id="0b4a7-163">그런 다음 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-163">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="0b4a7-164">Visual Studio에서 프로젝트의 **Web.Release.config** 를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-164">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="0b4a7-165">다음 XML을 `<configuration>` 태그에 삽입하고 키 값을 게시 웹앱의 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-165">Insert the following XML into the `<configuration>` tag, and replace the key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="0b4a7-166">작업을 마치면 RP 식별자 두 개가 프로젝트에 구성됩니다. 하나는 Visual Studio의 디버그 환경에 대한 RP 식별자이고, 나머지 하나는 Azure에 게시된 웹 앱에 대한 RP 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-166">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for the published web app in Azure.</span></span> <span data-ttu-id="0b4a7-167">AD FS에서 두 환경 각각에 대한 RP 트러스트를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-167">You will set up an RP trust for each of the two environments in AD FS.</span></span> <span data-ttu-id="0b4a7-168">디버그하는 동안 **디버그** 구성이 AD FS와 작동하도록 Web.config의 앱 설정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-168">During debugging, the app settings in Web.config are used to make your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="0b4a7-169">게시된 경우(기본적으로 **릴리스** 구성이 게시됨) 변환된 Web.config가 업로드되어 응용 프로그램 설정 변경 사항이 Web.Release.config에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-169">When it's published (by default, the **Release** configuration is published), a transformed Web.config is uploaded that incorporates the app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="0b4a7-170">Azure에서 게시된 웹 앱을 디버거에 연결하려는 경우(즉, 게시된 웹 앱에서 코드의 디버그 기호를 업로드해야 함) Web.Release.config의 앱 설정을 사용하는 고유한 사용자 지정 Web.config 변환(예: Web.AzureDebug.config)을 통해 Azure 디버깅을 위한 디버그 구성의 복제본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-170">If you want to attach the published web app in Azure to the debugger (i.e. you must upload debug symbols of your code in the published web app), you can create a clone of the Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses the app settings from Web.Release.config.</span></span> <span data-ttu-id="0b4a7-171">이렇게 하면 여러 환경에서 정적 구성을 유지 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-171">This allows you to maintain a static configuration across the different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="0b4a7-172">AD FS 관리에서 신뢰 당사자 트러스트 구성</span><span class="sxs-lookup"><span data-stu-id="0b4a7-172">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="0b4a7-173">이제 응용 프로그램 예제를 사용하고 실제로 AD FS를 인증하기 전에 AD FS 관리에서 RP 트러스트를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-173">Now you need to configure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="0b4a7-174">각각 디버그 환경과 게시된 웹 앱에 대한 별도의 RP 트러스트 두 개를 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-174">You will need to set up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="0b4a7-175">두 환경 모두에 대해 다음 단계를 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-175">Make sure that you repeat the following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="0b4a7-176">AD FS 서버에서 AD FS 관리 권한이 있는 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-176">On your AD FS server, log in with credentials that have management rights to AD FS.</span></span>
2. <span data-ttu-id="0b4a7-177">AD FS 관리를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-177">Open AD FS Management.</span></span> <span data-ttu-id="0b4a7-178">**AD FS\Trusted Relationships\Relying Party Trusts**를 마우스 오른쪽 단추로 클릭하고 **신뢰 당사자 트러스트 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-178">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="0b4a7-179">**데이터 원본 선택** 페이지에서 **신뢰 당사자에 대한 데이터를 수동으로 입력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-179">In the **Select Data Source** page, select **Enter data about the relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="0b4a7-180">**표시 이름 지정** 페이지에서 응용 프로그램의 표시 이름을 입력하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-180">In the **Specify Display Name** page, type a display name for the application and click **Next**.</span></span>
5. <span data-ttu-id="0b4a7-181">**프로토콜 선택** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-181">In the **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="0b4a7-182">**인증서 구성** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-182">In the **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0b4a7-183">HTTPS를 이미 사용하고 있으므로 암호화된 토큰은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-183">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="0b4a7-184">이 페이지에서 AD FS의 토큰을 암호화하려면 토큰 암호 해독 논리도 코드에 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-184">If you really want to encrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="0b4a7-185">자세한 내용은 [OWIN WS-Federation 미들웨어를 수동으로 구성하고 암호화된 토큰 적용](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-185">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="0b4a7-186">다음 단계를 진행하기 전에 Visual Studio 프로젝트에서 한 가지 정보를 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-186">Before you move onto the next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="0b4a7-187">프로젝트 속성에서 응용 프로그램의 **SSL URL** 을 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-187">In the project properties, note the **SSL URL** of the application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="0b4a7-188">AD FS 관리로 돌아와 **신뢰 당사자 트러스트 추가 마법사**의 **URL 구성** 페이지에서 **WS-Federation Passive 프로토콜 지원**을 선택하고 이전 단계에서 기록해 둔 Visual Studio 프로젝트의 SSL URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-188">Back in AD FS Management, in the **Configure URL** page of the **Add Relying Party Trust Wizard**, select **Enable support for the WS-Federation Passive protocol** and type in the SSL URL of your Visual Studio project that you noted in the previous step.</span></span> <span data-ttu-id="0b4a7-189">그런 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-189">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="0b4a7-190">URL은 인증에 성공한 후 클라이언트를 전송할 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-190">URL specifies where to send the client after authentication succeeds.</span></span> <span data-ttu-id="0b4a7-191">디버그 환경의 경우 <code>https://localhost:&lt;port&gt;/</code>여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-191">For the debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="0b4a7-192">게시된 웹 앱의 경우 웹 앱 URL이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-192">For the published web app, it should be the web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="0b4a7-193">**식별자 구성** 페이지에서 프로젝트 SSL URL이 이미 나열되어 있는지 확인하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-193">In the **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="0b4a7-194">기본값을 선택하여 마법사의 끝까지 **다음** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-194">Click **Next** all the way to the end of the wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="0b4a7-195">Visual Studio 프로젝트의 App_Start\Startup.Auth.cs에서 이 식별자는 페더레이션 인증 중에 <code>WsFederationAuthenticationOptions.Wtrealm</code> 값에 일치됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-195">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against the value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="0b4a7-196">기본적으로 이전 단계의 응용 프로그램 URL이 RP 식별자로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-196">By default, the application's URL from the previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="0b4a7-197">이제 AD FS에서 프로젝트에 대한 RP 응용 프로그램 구성을 마쳤습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-197">You have now finished configuring the RP application for your project in AD FS.</span></span> <span data-ttu-id="0b4a7-198">다음으로, 응용 프로그램에 필요한 클레임을 보내도록 이 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-198">Next, you configure this application to send the claims needed by your application.</span></span> <span data-ttu-id="0b4a7-199">마법사가 종료되면 즉시 시작할 수 있도록 **클레임 규칙 편집** 대화 상자가 기본적으로 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-199">The **Edit Claim Rules** dialog is opened by default for you at the end of the wizard so you can start immediately.</span></span> <span data-ttu-id="0b4a7-200">최소한 다음 클레임을 구성해 보겠습니다(스키마는 괄호 안에 포함).</span><span class="sxs-lookup"><span data-stu-id="0b4a7-200">Let's configure at least the following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="0b4a7-201">이름(http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name)은 `User.Identity.Name`을 하이드레이션하는 ASP.NET에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-201">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET to hydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="0b4a7-202">사용자 계정 이름(http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn)은 직에서 사용자를 고유하게 식별하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-202">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used to uniquely identify users in the organization.</span></span>
    * <span data-ttu-id="0b4a7-203">역할로서의 그룹 멤버 자격(http://schemas.microsoft.com/ws/2008/06/identity/claims/role)은 `[Authorize(Roles="role1, role2,...")]` 장식과 함께 컨트롤러/작업에 대한 권한을 부여하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-203">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration to authorize controllers/actions.</span></span> <span data-ttu-id="0b4a7-204">실제로 이 방법은 역할 권한 부여에 대해 효율적이지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-204">In reality, this approach may not be the most performant for role authorization.</span></span> <span data-ttu-id="0b4a7-205">AD 사용자가 수백 개의 보안 그룹에 속해 있는 경우 SAML 토큰에서 수백 개의 역할 클레임이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-205">If your AD users belong to hundreds of security groups, they become hundreds of role claims in the SAML token.</span></span> <span data-ttu-id="0b4a7-206">이 접근 방식의 대안은 특정 그룹에 속한 사용자의 멤버 자격에 따라 단일 역할 클레임을 조건부로 보내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-206">An alternative approach is to send a single role claim conditionally depending on the user's membership in a particular group.</span></span> <span data-ttu-id="0b4a7-207">하지만 이 자습서에서는 이 접근 방식을 단순한 형태로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-207">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="0b4a7-208">이름 ID(http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier)는 위조 방지 유효성 검사를 위해 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-208">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="0b4a7-209">위조 방지 유효성 검사와 함께 사용하는 방법에 대한 정보는 **Azure Active Directory 인증으로 LOB(기간 업무) Azure 앱 만들기** 의 [LOB(기간 업무) 기능 추가](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud)섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-209">For more information on how to make it work with anti-forgery validation, see the **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="0b4a7-210">응용 프로그램에 대해 구성해야 하는 클레임 유형은 응용 프로그램의 요구 사항에 따라 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-210">The claim types you need to configure for your application is determined by your application's needs.</span></span> <span data-ttu-id="0b4a7-211">예를 들어, Azure Active Directory 응용 프로그램(즉, RP 트러스트)에서 [지원되는 클레임 목록은 지원되는 토큰 및 클레임 유형](http://msdn.microsoft.com/library/azure/dn195587.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-211">For the list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="0b4a7-212">클레임 규칙 편집 대화 상자에서 **규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-212">In the Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="0b4a7-213">스크린샷에 표시된 대로 이름, UPN 및 역할 클레임을 구성하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-213">Configure the name, UPN, and role claims as shown in the screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="0b4a7-214">그런 다음 [SAML 어설션의 이름 식별자](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)에 설명된 단계를 사용하여 임시 이름 ID 클레임을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-214">Next, you create a transient name ID claim using the steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="0b4a7-215">**규칙 추가** 를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-215">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="0b4a7-216">**사용자 지정 규칙을 사용하여 클레임 보내기**를 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-216">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="0b4a7-217">다음 규칙 언어를 **사용자 지정 규칙** 상자에 붙여 넣고 규칙 이름을 **세션별 식별자**로 지정한 후 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-217">Paste the following rule language into the **Custom rule** box, name the rule **Per Session Identifier** and click **Finish**.</span></span>  
    
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
    
    <span data-ttu-id="0b4a7-218">사용자 지정 규칙은 이 스크린샷과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-218">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="0b4a7-219">**규칙 추가** 를 다시 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-219">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="0b4a7-220">**들어오는 클레임 변환**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-220">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="0b4a7-221">스크린샷에 표시된 대로 규칙을 구성(사용자 지정 규칙에서 만든 클레임 유형 사용)하고 **마침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-221">Configure the rule as shown in the screenshot (using the claim type you created in the custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="0b4a7-222">임시 이름 ID 클레임 단계에 자세한 내용은 [SAML 어설션의 이름 식별자](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-222">For detailed information on the steps for the transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="0b4a7-223">**클레임 규칙 편집** 대화 상자에서 **적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-223">Click **Apply** in the **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="0b4a7-224">이제 다음 스크린샷처럼 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-224">It should now look like the following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="0b4a7-225">즉, 디버그 환경과 게시된 웹 앱 둘 다에 대해 이러한 단계를 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-225">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="0b4a7-226">응용 프로그램에 대한 페더레이션 인증 테스트</span><span class="sxs-lookup"><span data-stu-id="0b4a7-226">Test federated authentication for your application</span></span>
<span data-ttu-id="0b4a7-227">AD FS에 대해 응용 프로그램의 인증 논리를 테스트할 준비가 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-227">You are ready to test your application's authentication logic against AD FS.</span></span> <span data-ttu-id="0b4a7-228">이 AD FS 실습 환경에는 AD(Active Directory)의 테스트 그룹에 속한 테스트 사용자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-228">In my AD FS lab environment, I have a test user that belongs to a test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="0b4a7-229">디버거에서 인증을 테스트하려면 `F5`키를 누르기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-229">To test authentication in the debugger, all you need to do now is type `F5`.</span></span> <span data-ttu-id="0b4a7-230">게시된 웹 앱에서 인증을 테스트하려면 해당 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-230">If you want to test authentication in the published web app, navigate to the URL.</span></span>

<span data-ttu-id="0b4a7-231">웹 응용 프로그램이 로드되면 **로그인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-231">After the web application loads, click **Sign In**.</span></span> <span data-ttu-id="0b4a7-232">AD FS에서 선택한 인증 방법에 따라 로그인 대화 상자 또는 AD FS에서 제공하는 로그인 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-232">You should now get either a login dialog or the login page served by AD FS, depending on the authentication method chosen by AD FS.</span></span> <span data-ttu-id="0b4a7-233">다음은 Internet Explorer 11의 화면 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-233">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="0b4a7-234">AD FS 배포의 AD 도메인에 속한 사용자로 로그인하면 가장자리에 **안녕하세요, <User Name>님!**이 표시된 홈 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-234">Once you log in with a user in the AD domain of the AD FS deployment, you should now see the homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="0b4a7-235">이 표시된 홈 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-235">in the corner.</span></span> <span data-ttu-id="0b4a7-236">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-236">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="0b4a7-237">지금까지 다음 방법에 성공했습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-237">So far, you've succeeded in the following ways:</span></span>

* <span data-ttu-id="0b4a7-238">응용 프로그램에서 성공적으로 AD FS에 연결하고 AD FS 데이터베이스에서 일치하는 RP 식별자를 찾았습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-238">Your application has successfully reached AD FS and a matching RP identifier is found in the AD FS database</span></span>
* <span data-ttu-id="0b4a7-239">AD FS가 AD 사용자를 성공적으로 인증하고 응용 프로그램의 홈 페이지로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-239">AD FS has successfully authenticated an AD user and redirect you back to the application's homepage</span></span>
* <span data-ttu-id="0b4a7-240">가장자리에 사용자 이름이 표시되어 있다는 사실로 알 수 있듯이, AD FS에서 이름 클레임(http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name)을 응용 프로그램으로 성공적으로 전송했습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-240">AD FS as successfully sent the name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) to your application, as indicated by the fact that the user name is displayed in the corner.</span></span> 

<span data-ttu-id="0b4a7-241">이름 클레임이 누락된 경우 **안녕하세요, 님!**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-241">If the name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="0b4a7-242">Views\Shared\_LoginPartial.cshtml을 보면 `User.Identity.Name`을 사용하여 사용자 이름을 표시한다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-242">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` to display the user name.</span></span> <span data-ttu-id="0b4a7-243">앞서 설명한 바와 같이, 인증된 사용자의 이름 클레임을 SAML 토큰에서 사용할 수 있는 경우 ASP.NET은 해당 클레임으로 이 속성을 하이드레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-243">As mentioned previously, if the name claim of the authenticated user is available in the SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="0b4a7-244">AD FS에서 전송된 모든 클레임을 보려면 Controllers\HomeController.cs의 Index 작업 메서드에 중단점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-244">To see all the claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in the Index action method.</span></span> <span data-ttu-id="0b4a7-245">사용자가 인증되고 나면 `System.Security.Claims.Current.Claims` 컬렉션을 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-245">After the user is authenticated, inspect the `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="0b4a7-246">사용자에게 특정 컨트롤러 또는 작업에 대한 권한 부여</span><span class="sxs-lookup"><span data-stu-id="0b4a7-246">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="0b4a7-247">RP 트러스트 구성에서 그룹 멤버 자격을 역할 클레임으로 포함했기 때문에 이제 컨트롤러 및 작업에 대한 `[Authorize(Roles="...")]` 장식에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-247">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in the `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="0b4a7-248">CRUD(만들기-읽기-업데이트-삭제) 패턴이 있는 LOB(기간 업무) 응용 프로그램에서는 특정 역할에 각 작업에 대한 액세스 권한을 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-248">In a line-of-business application with the Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles to access each action.</span></span> <span data-ttu-id="0b4a7-249">지금은 기존 Home 컨트롤러에서 이 기능을 사용해 보기만 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-249">For now, you will just try out this feature on the existing Home controller.</span></span>

1. <span data-ttu-id="0b4a7-250">Controllers\HomeController.cs를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-250">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="0b4a7-251">인증된 사용자의 보안 그룹 멤버 자격을 사용하여 다음 코드와 유사하게 `About` 및 `Contact` 작업 메서드를 장식합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-251">Decorate the `About` and `Contact` action methods similar to the following code, using security group memberships that your authenticated user has.</span></span>  
   
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
   
    <span data-ttu-id="0b4a7-252">이 자습서의 AD FS 실습 환경에서는 **테스트 사용자**를 **테스트 그룹**에 추가했기 때문에 테스트 그룹을 사용하여 `About`에 대한 권한 부여를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-252">Since I added **Test User** to **Test Group** in my AD FS lab environment, I'll use Test Group to test authorization on `About`.</span></span> <span data-ttu-id="0b4a7-253">`Contact`의 경우 **테스트 사용자**가 속해 있지 않은 **도메인 관리**의 부정적인 사례를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-253">For `Contact`, I'll test the negative case of **Domain Admins**, to which **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="0b4a7-254">`F5` 키를 눌러 디버거를 시작하고 로그인한 후 **About**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-254">Start the debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="0b4a7-255">이제 인증된 사용자에게 해당 작업에 대한 권한이 부여된 경우 `~/About/Index` 페이지가 성공적으로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-255">You should now be viewing the `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="0b4a7-256">**연결**을 클릭합니다(이 자습서에서는 **테스트 사용자**에게 작업에 대한 권한이 부여되지 않음).</span><span class="sxs-lookup"><span data-stu-id="0b4a7-256">Now click **Contact**, which in my case should not authorize **Test User** for the action.</span></span> <span data-ttu-id="0b4a7-257">그러나 브라우저가 AD FS로 리디렉션되므로 다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-257">However, the browser is redirected to AD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="0b4a7-258">AD FS 서버의 이벤트 뷰어에서 이 오류를 조사하면 다음 예외 메시지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-258">If you investigate this error in Event Viewer on the AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>The same client browser session has made '6' requests in the last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="0b4a7-259">이 오류의 원인은 사용자의 역할에 권한이 부여되지 않은 경우 기본적으로 MVC에서 401 권한 없음을 반환하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-259">The reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="0b4a7-260">이 경우 ID 공급자(AD FS)에 대한 재인증 요청이 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-260">This triggers a reauthentication request to your identity provider (AD FS).</span></span> <span data-ttu-id="0b4a7-261">사용자가 이미 인증되었으므로 AD FS가 동일한 페이지로 돌아가고 또 다른 401이 발생하여 리디렉션 루프가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-261">Since the user is already authenticated, AD FS returns to the same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="0b4a7-262">단순한 논리로 AuthorizeAttribute의 `HandleUnauthorizedRequest` 메서드를 재정의하여 리디렉션 루프를 계속하는 대신 의미 있는 내용을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-262">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic to show something that makes sense instead of continuing the redirect loop.</span></span>
5. <span data-ttu-id="0b4a7-263">프로젝트에서 AuthorizeAttribute.cs라는 파일을 만들어 다음 코드를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-263">Create a file in the project called AuthorizeAttribute.cs, and paste the following code into it.</span></span>
   
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
   
    <span data-ttu-id="0b4a7-264">인증되었지만 권한의 없는 경우 재정의 코드는 HTTP 401(권한 없음) 대신 HTTP 403(사용 권한 없음)을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-264">The override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="0b4a7-265">`F5`키를 눌러 디버거를 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-265">Run the debugger again with `F5`.</span></span> <span data-ttu-id="0b4a7-266">이제 **Contact** 를 클릭하면 보다 자세한(중요하지는 않음) 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-266">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="0b4a7-267">응용 프로그램을 Azure 앱 서비스 웹 앱에 다시 게시하고 라이브 응용 프로그램의 동작을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-267">Publish the application to Azure App Service Web Apps again, and test the behavior of the live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-to-on-premises-data"></a><span data-ttu-id="0b4a7-268">온-프레미스 데이터 연결</span><span class="sxs-lookup"><span data-stu-id="0b4a7-268">Connect to on-premises data</span></span>
<span data-ttu-id="0b4a7-269">Azure Active Directory 대신 AD FS를 사용하여 LOB(기간 업무) 응용 프로그램을 구현하는 이유는 조직의 데이터를 오프-프레미스로 유지하는 경우의 규정 준수 문제 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-269">A reason that you would want to implement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="0b4a7-270">이는 [SQL 데이터베이스](/services/sql-database/) 를 웹앱의 데이터 계층으로 사용할 수 없어 Azure의 웹앱에서 온-프레미스 데이터베이스에 액세스해야 함을 의미할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-270">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed to use [SQL Database](/services/sql-database/) as the data tier for your web apps.</span></span>

<span data-ttu-id="0b4a7-271">Azure App Service Web Apps는 [하이브리드 연결](../biztalk-services/integration-hybrid-connection-overview.md) 및 [가상 네트워크](web-sites-integrate-with-vnet.md)의 두 가지 방법으로 온-프레미스 데이터베이스 액세스를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-271">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="0b4a7-272">자세한 내용은 [Azure App Service Web Apps에서 VNET 통합 및 하이브리드 연결 사용](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b4a7-272">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="0b4a7-273">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="0b4a7-273">Further resources</span></span>
* [<span data-ttu-id="0b4a7-274">Azure 앱에서 온-프레미스 Active Directory를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="0b4a7-274">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="0b4a7-275">Azure Active Directory 인증을 사용하여 LOB(기간 업무) Azure 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="0b4a7-275">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="0b4a7-276">Visual Studio 2013의 ASP.NET에서 온-프레미스 조직 인증 옵션(ADFS) 사용</span><span class="sxs-lookup"><span data-stu-id="0b4a7-276">Use the On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="0b4a7-277">WIF에서 Katana로 VS2013 웹 프로젝트 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="0b4a7-277">Migrate a VS2013 Web Project From WIF to Katana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="0b4a7-278">Active Directory Federation Services 개요</span><span class="sxs-lookup"><span data-stu-id="0b4a7-278">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="0b4a7-279">WS-Federation 1.1 사양</span><span class="sxs-lookup"><span data-stu-id="0b4a7-279">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

