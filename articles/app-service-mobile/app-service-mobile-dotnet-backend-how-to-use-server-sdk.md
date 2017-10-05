---
title: "모바일 앱용 .NET 백 엔드 서버 SDK를 사용하는 방법 | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱용 .NET 백 엔드 서버 SDK를 사용하는 방법에 대해 알아봅니다."
keywords: "앱 서비스, Azure 앱 서비스, 모바일 앱, 모바일 서비스, 규모, 확장성, 앱 배포, Azure 앱 배포"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 657fea16e47c15efd262c86d6a150a721476134a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="a5820-104">Azure 모바일 앱용 .NET 백 엔드 서버 SDK 사용</span><span class="sxs-lookup"><span data-stu-id="a5820-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="a5820-105">이 항목은 주요 Azure 앱 서비스 모바일 앱 시나리오에서 .NET 백 엔드 서버 SDK를 사용하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="a5820-106">Azure 모바일 앱 SDK를 사용하면 ASP.NET 응용 프로그램에서 모바일 클라이언트를 사용하여 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="a5820-107">[Azure Mobile Apps용 .NET 서버 SDK][2]는 GitHub에서 오픈 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="a5820-108">리포지토리는 전체 서버 SDK 단위 테스트 도구 모음 및 일부 샘플 프로젝트를 포함하는 모든 소스 코드를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="a5820-109">참조 설명서</span><span class="sxs-lookup"><span data-stu-id="a5820-109">Reference documentation</span></span>
<span data-ttu-id="a5820-110">서버 SDK에 대한 참조 설명서는 [Azure Mobile Apps .NET 참조][1]에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="a5820-111"><a name="create-app"></a>방법: .NET 모바일 앱 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="a5820-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="a5820-112">새 프로젝트를 시작하는 경우 [Azure 포털] 과 Visual Studio 중 하나를 사용하여 앱 서비스 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="a5820-113">App Service 응용 프로그램을 로컬로 실행하거나 클라우드 기반 앱 서비스 모바일 앱에 프로젝트를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>

<span data-ttu-id="a5820-114">기존 프로젝트에 모바일 기능을 추가하는 경우 [SDK 다운로드 및 초기화](#install-sdk) 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5820-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="a5820-115">Azure 포털을 사용하여 .NET 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="a5820-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="a5820-116">App Service 모바일 백 엔드를 만들려면 [빠른 시작 자습서][3]를 따르거나 다음과 같은 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="a5820-117">*시작* 블레이드로 돌아가서 **테이블 API 만들기** 아래에서 **백 엔드 언어**로 **C#**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="a5820-118">**다운로드**를 클릭하고 로컬 컴퓨터에 압축된 프로젝트 파일을 풀고 Visual Studio에서 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="a5820-119">Visual Studio 2013 및 Visual Studio 2015를 사용하여 .NET 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="a5820-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="a5820-120">Visual Studio에서 Azure Mobile Apps 프로젝트를 만들려면 [.NET용 Azure SDK][4](버전 2.9.0 이상)을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="a5820-121">SDK를 설치한 후 다음 단계를 사용하여 ASP.NET 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="a5820-122">**새 프로젝트** 대화를 엽니다(*파일* > **새로 만들기** > **프로젝트...**에서).</span><span class="sxs-lookup"><span data-stu-id="a5820-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="a5820-123">**템플릿** > **Visual C#**를 확장하고 **웹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="a5820-124">**ASP.NET 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="a5820-125">프로젝트 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-125">Fill in the project name.</span></span> <span data-ttu-id="a5820-126">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-126">Then click **OK**.</span></span>
5. <span data-ttu-id="a5820-127">*ASP.NET 4.5.2 템플릿*아래에서 **Azure Mobile App**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="a5820-128">**클라우드에 호스트** 를 선택하여 클라우드에 이 프로젝트를 게시할 수 있는 모바일 백 엔드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="a5820-129">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-129">Click **OK**.</span></span>

## <span data-ttu-id="a5820-130"><a name="install-sdk"></a>방법: SDK 다운로드 및 설치</span><span class="sxs-lookup"><span data-stu-id="a5820-130"><a name="install-sdk"></a>How to: Download and initialize the SDK</span></span>
<span data-ttu-id="a5820-131">SDK는 [NuGet.org]에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-131">The SDK is available on [NuGet.org].</span></span> <span data-ttu-id="a5820-132">이 패키지는 SDK를 사용하여 시작하는 데 필요한 기본 기능을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-132">This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="a5820-133">SDK를 초기화하려면 **HttpConfiguration** 개체에서 작업을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-133">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="a5820-134">SDK 설치</span><span class="sxs-lookup"><span data-stu-id="a5820-134">Install the SDK</span></span>
<span data-ttu-id="a5820-135">SDK를 설치하려면 Visual Studio에서 서버 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 선택합니다. [Microsoft.Azure.Mobile.Server] 패키지를 검색한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-135">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="a5820-136"><a name="server-project-setup"></a> 서버 프로젝트 초기화</span><span class="sxs-lookup"><span data-stu-id="a5820-136"><a name="server-project-setup"></a> Initialize the server project</span></span>
<span data-ttu-id="a5820-137">A .NET 백 엔드 서버 프로젝트는 OWIN 시작 클래스를 포함하여 다른 ASP.NET 프로젝트와 유사하게 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-137">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="a5820-138">NuGet 패키지 `Microsoft.Owin.Host.SystemWeb`을 참조하도록 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-138">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="a5820-139">Visual Studio에서 이 클래스를 추가하려면 서버 프로젝트를 마우스 오른쪽 단추로 클릭하고 **추가** >
**새 항목**을 선택하고 **웹** > **일반** > **OWIN 시작 클래스**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-139">To add this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="a5820-140">다음과 같은 특성의 클래스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-140">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="a5820-141">OWIN 시작 클래스의 `Configuration()` 메서드에서 **HttpConfiguration** 개체를 사용하여 Azure Mobile Apps 환경을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-141">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="a5820-142">다음 예제는 추가된 기능이 없는 서버 프로젝트를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-142">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="a5820-143">개별 기능을 사용하려면 **ApplyTo**를 호출하기 전에 **MobileAppConfiguration** 개체에서 확장 메서드를 호출해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-143">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="a5820-144">예를 들어 다음 코드는 초기화하는 동안 `[MobileAppController]` 특성을 포함하는 모든 API 컨트롤러에 기본 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-144">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="a5820-145">Azure 포털의 빠른 시작 서버에서 **UseDefaultConfiguration()**을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-145">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="a5820-146">이것은 다음 설정과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-146">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="a5820-147">사용되는 확장 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-147">The extension methods used are:</span></span>

* <span data-ttu-id="a5820-148">`AddMobileAppHomeController()`은(는) 기본 Azure Mobile Apps 홈 페이지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-148">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="a5820-149">`MapApiControllers()`은(는) `[MobileAppController]` 특성으로 데코레이팅된 WebAPI 컨트롤러에 대한 사용자 지정 API 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-149">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="a5820-150">`AddTables()`은(는) 테이블 컨트롤러에 대한 `/tables` 끝점의 매핑을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-150">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="a5820-151">`AddTablesWithEntityFramework()`은(는) Entity Framework 기반 컨트롤러를 사용하는 `/tables` 끝점 매핑에 대한 약칭입니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-151">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="a5820-152">`AddPushNotifications()`은(는) Notification Hubs에 대한 장치를 등록하는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-152">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="a5820-153">`MapLegacyCrossDomainController()` 은(는) 로컬 개발을 위한 표준 CORS 헤더를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-153">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="a5820-154">SDK 확장</span><span class="sxs-lookup"><span data-stu-id="a5820-154">SDK extensions</span></span>
<span data-ttu-id="a5820-155">다음 NuGet 기반 확장 패키지는 응용 프로그램에서 사용할 수 있는 다양한 모바일 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-155">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="a5820-156">**MobileAppConfiguration** 개체를 사용하여 초기화하는 동안 확장을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-156">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="a5820-157">[Microsoft.Azure.Mobile.Server.Quickstart] 기본 모바일 앱 설정을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="a5820-158">초기화하는 동안 **UseDefaultConfiguration** 확장 메서드를 호출하여 구성에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-158">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="a5820-159">이 확장은 알림, 인증, 엔터티, 테이블, Crossdomain 및 홈 패키지와 같은 확장을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-159">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="a5820-160">이 패키지는 Azure 포털에서 사용할 수 있는 Mobile Apps 빠른 시작에서 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-160">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="a5820-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) 웹 사이트 루트에 대해 기본 *이 모바일 앱이 실행 중인 페이지* 를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="a5820-162">**AddMobileAppHomeController** 확장 메서드를 호출하여 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-162">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="a5820-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) 데이터로 작업하기 위한 클래스를 포함하고 데이터 파이프라인을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="a5820-164">**AddTables** 확장 메서드를 호출하여 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-164">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="a5820-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) SQL 데이터베이스에서 데이터를 액세스하는 Entity Framework를 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="a5820-166">**AddTablesWithEntityFramework** 확장 메서드를 호출하여 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-166">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="a5820-167">[Microsoft.Azure.Mobile.Server.Authentication] 인증을 사용할 수 있도록 하고 토큰의 유효성을 검사하는 데 사용되는 OWIN 미들웨어를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-167">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="a5820-168">**AddAppServiceAuthentication** 및 **IAppBuilder**.**UseAppServiceAuthentication** 확장 메서드를 호출하여 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-168">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="a5820-169">[Microsoft.Azure.Mobile.Server.Notifications] 푸시 알림을 사용할 수 있도록 하며 푸시 등록 끝점을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-169">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="a5820-170">**AddPushNotifications** 확장 메서드를 호출하여 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-170">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="a5820-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) 모바일 앱에서 레거시 웹 브라우저에 데이터를 제공하는 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="a5820-172">**MapLegacyCrossDomainController** 확장 메서드를 호출하여 구성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-172">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="a5820-173">[Microsoft.Azure.Mobile.Server.Login]은 사용자 지정 인증 시나리오 동안 사용되는 정적 메서드인 AppServiceLoginHandler.CreateToken() 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-173">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="a5820-174"><a name="publish-server-project"></a>방법: 서버 프로젝트 게시</span><span class="sxs-lookup"><span data-stu-id="a5820-174"><a name="publish-server-project"></a>How to: Publish the server project</span></span>
<span data-ttu-id="a5820-175">이 섹션에서는 Visual Studio에서 .NET 백 엔드 프로젝트를 게시하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-175">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="a5820-176">[Azure 앱 서비스 배포 설명서](../app-service-web/web-sites-deploy.md)에 나오는 Git 또는 다른 메서드를 사용하여 백 엔드 프로젝트를 배포할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-176">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="a5820-177">Visual Studio에서 NuGet 패키지를 복원하려면 프로젝트를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="a5820-177">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="a5820-178">솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-178">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="a5820-179">처음 게시할 때는 게시 프로필을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-179">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="a5820-180">이미 정의된 프로필이 있을 때 프로필을 선택하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-180">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="a5820-181">게시 대상을 선택하도록 요청 받으면 **Microsoft Azure App Service** > **다음**을 클릭한 다음 (필요한 경우) Azure 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-181">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="a5820-182">Visual Studio가 Azure에서 직접 게시 설정을 안전하게 다운로드하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-182">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="a5820-183">**구독**을 선택하고 **보기**에서 **리소스 형식**을 선택하며 **모바일 앱**을 확장하고 모바일 앱 백 엔드를 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-183">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="a5820-184">게시 프로필 정보를 확인하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-184">Verify the publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="a5820-185">모바일 앱 백 엔드가 성공적으로 게시되면 성공했다는 것을 나타내는 방문 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-185">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="a5820-186"><a name="define-table-controller"></a> 방법: 테이블 컨트롤러 정의</span><span class="sxs-lookup"><span data-stu-id="a5820-186"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="a5820-187">모바일 클라이언트에 SQL 테이블을 노출하는 테이블 컨트롤러를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-187">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="a5820-188">테이블 컨트롤러를 구성하려면 세 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-188">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="a5820-189">데이터 전송 개체(DTO) 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-189">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="a5820-190">Mobile DbContext 클래스에 테이블 참조를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-190">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="a5820-191">테이블 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-191">Create a table controller.</span></span>

<span data-ttu-id="a5820-192">데이터 전송 개체(DTO)는 `EntityData`에서 상속하는 일반 C# 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-192">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="a5820-193">예:</span><span class="sxs-lookup"><span data-stu-id="a5820-193">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="a5820-194">DTO는 SQL 데이터베이스 내에서 테이블을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-194">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="a5820-195">데이터베이스 항목을 만들려면 사용하는 DbContext에 `DbSet<>` 속성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-195">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="a5820-196">Azure Mobile Apps에 대한 기본 프로젝트 템플릿에서 DbContext는 `Models\MobileServiceContext.cs`(이)라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-196">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="a5820-197">Azure SDK가 설치되어 있으면 이제 다음과 같이 템플릿 테이블 컨트롤러를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-197">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="a5820-198">컨트롤러 폴더를 마우스 오른쪽 단추로 클릭하고 **추가** > **컨트롤러를 참조하세요.를 참조하세요.를 참조하세요.**를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5820-198">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="a5820-199">**Azure Mobile Apps 테이블 컨트롤러** 옵션을 선택한 다음 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-199">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="a5820-200">**컨트롤러 추가** 대화 상자에서 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-200">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="a5820-201">**모델 클래스** 드롭다운에서 새 DTO를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-201">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="a5820-202">**DbContext** 드롭다운에서 모바일 서비스 DbContext 클래스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-202">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="a5820-203">컨트롤러 이름이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-203">The Controller name is created for you.</span></span>
4. <span data-ttu-id="a5820-204">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-204">Click **Add**.</span></span>

<span data-ttu-id="a5820-205">빠른 시작 서버 프로젝트는 간단한 **TodoItemController**에 대한 예제를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-205">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="a5820-206"><a name="adjust-pagesize"></a>방법: 테이블 페이징 크기 조정</span><span class="sxs-lookup"><span data-stu-id="a5820-206"><a name="adjust-pagesize"></a>How to: Adjust the table paging size</span></span>
<span data-ttu-id="a5820-207">기본적으로 Azure 모바일 앱은 요청당 50개의 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-207">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="a5820-208">페이징은 클라이언트가 해당 UI 스레드와도, 서버와도 너무 오랫동안 연결되지 않으므로 최적의 사용자 환경을 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-208">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="a5820-209">테이블 페이징 크기를 변경하려면 서버 쪽의 "허용되는 쿼리 크기"와 클라이언트 쪽 페이지 크기를 늘립니다. 서버 쪽의 "허용되는 쿼리 크기"는 `EnableQuery` 특성을 사용하여 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-209">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="a5820-210">PageSize은 클라이언트에서 요청하는 크기보다 크거나 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-210">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="a5820-211">클라이언트 페이지 크기 변경에 대한 내용은 특정 클라이언트 방법 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5820-211">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="a5820-212">방법: 사용자 지정 API 컨트롤러 정의</span><span class="sxs-lookup"><span data-stu-id="a5820-212">How to: Define a custom API controller</span></span>
<span data-ttu-id="a5820-213">사용자 지정 API 컨트롤러는 끝점을 노출하여 모바일 앱 백 엔드에서 가장 기본적인 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-213">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="a5820-214">[MobileAppController] 특성을 사용하여 모바일 전용 API 컨트롤러를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-214">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="a5820-215">`MobileAppController` 특성은 경로를 등록하고 모바일 앱 JSON 직렬 변환기를 설정한 후 [클라이언트 버전 검사](app-service-mobile-client-and-server-versioning.md)를 켭니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-215">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="a5820-216">Visual Studio에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭한 다음 **추가** > **컨트롤러**를 클릭하고 **웹 API 2 컨트롤러&mdash;비어 있음**을 선택한 후 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-216">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="a5820-217">`CustomController`와 같은 **컨트롤러 이름**을 제공하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-217">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="a5820-218">새로운 컨트롤러 클래스 파일에서 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-218">In the new controller class file, add the following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="a5820-219">다음 예제와 같이 **[MobileAppController]** 특성을 API 컨트롤러 클래스 정의에 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-219">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="a5820-220">App_Start/Startup.MobileApp.cs 파일에서 다음 예제와 같이 **MapApiControllers** 확장 메서드에 대한 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-220">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="a5820-221">`MapApiControllers()` 대신 `UseDefaultConfiguration()` 확장 메서드를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-221">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="a5820-222">**MobileAppControllerAttribute** 가 적용되지 않는 모든 컨트롤러는 클라이언트에서 여전히 액세스할 수 있지만 모든 모바일 앱 클라이언트 SDK로 올바르게 사용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-222">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="a5820-223">방법: 인증으로 작업</span><span class="sxs-lookup"><span data-stu-id="a5820-223">How to: Work with authentication</span></span>
<span data-ttu-id="a5820-224">Azure Mobile Apps는 App Service 인증/권한 부여를 사용하여 모바일 백 엔드를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-224">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="a5820-225">이 섹션에서는 .NET 백 엔드 서버 프로젝트에서 다음과 같은 인증 관련 작업을 수행하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-225">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="a5820-226">방법: 서버 프로젝트에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="a5820-226">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="a5820-227">방법: 응용 프로그램에 사용자 지정 인증 사용</span><span class="sxs-lookup"><span data-stu-id="a5820-227">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="a5820-228">방법: 인증된 사용자 정보 검색</span><span class="sxs-lookup"><span data-stu-id="a5820-228">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="a5820-229">방법: 인증된 사용자에 대한 데이터 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="a5820-229">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="a5820-230"><a name="add-auth"></a>방법: 서버 프로젝트에 인증 추가</span><span class="sxs-lookup"><span data-stu-id="a5820-230"><a name="add-auth"></a>How to: Add authentication to a server project</span></span>
<span data-ttu-id="a5820-231">**MobileAppConfiguration** 개체를 확장하고 OWIN 미들웨어를 구성하여 서버 프로젝트에 인증을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-231">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="a5820-232">[Microsoft.Azure.Mobile.Server.Quickstart] 패키지를 설치하고 **UseDefaultConfiguration** 확장 메서드를 호출하는 경우 3단계로 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-232">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="a5820-233">Visual Studio에서 [Microsoft.Azure.Mobile.Server.Authentication] 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-233">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="a5820-234">Startup.cs 프로젝트 파일에서 **Configuration** 메서드의 시작 부분에 다음 코드 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-234">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="a5820-235">이 OWIN 미들웨어 구성 요소는 관련 App Service 게이트웨이에서 발급된 토큰의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-235">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="a5820-236">인증을 요구하는 모든 컨트롤러 또는 메서드에 `[Authorize]` 특성을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-236">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span>

<span data-ttu-id="a5820-237">모바일 앱 백 엔드에 클라이언트를 인증하는 방법에 대해 알아보려면 [앱에 인증 추가](app-service-mobile-ios-get-started-users.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5820-237">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="a5820-238"><a name="custom-auth"></a>방법: 응용 프로그램에 사용자 지정 인증 사용</span><span class="sxs-lookup"><span data-stu-id="a5820-238"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="a5820-239">App Service 인증/권한 부여 공급자 중 하나를 사용하지 않으려면 본인의 고유한 로그인 시스템을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-239">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="a5820-240">인증 토큰 생성을 위한 [Microsoft.Azure.Mobile.Server.Login] 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-240">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="a5820-241">사용자 자격 증명의 유효성 검사를 위한 고유 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-241">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="a5820-242">예를 들어 데이터베이스의 솔트되고 해시된 암호를 기준으로 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-242">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="a5820-243">다음 예제에서 `isValidAssertion()` 메서드(다른 곳에 정의됨)는 이러한 검사를 담당합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-243">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="a5820-244">사용자 지정 인증은 ApiController 만들기 및 `register` 및 `login` 작업 노출로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-244">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="a5820-245">클라이언트는 사용자로부터 정보를 수집하는 데 사용자 지정 UI를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-245">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="a5820-246">그러면 정보는 표준 HTTP POST 호출을 사용하여 API에 제출됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-246">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="a5820-247">서버가 어설션의 유효성을 검사하면 `AppServiceLoginHandler.CreateToken()` 메서드를 사용하여 토큰이 발급됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-247">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="a5820-248">ApiController는 `[MobileAppController]` 특성을 사용하면 **안 됩니다**.</span><span class="sxs-lookup"><span data-stu-id="a5820-248">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="a5820-249">예제 `login` 작업:</span><span class="sxs-lookup"><span data-stu-id="a5820-249">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="a5820-250">앞의 예에서 LoginResult 및 LoginResultUser는 필요한 속성을 노출하는 직렬화 가능 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-250">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="a5820-251">클라이언트는 로그인 응답을 통해 다음과 같은 형식의 JSON 개체로 반환되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-251">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="a5820-252">`AppServiceLoginHandler.CreateToken()` 메서드는 *audience* 및 *issuer* 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-252">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="a5820-253">이러한 매개 변수 모두 HTTPS 체계를 사용하여 응용 프로그램 루트의 URL로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-253">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="a5820-254">마찬가지로 *secretKey* 를 응용 프로그램의 서명 키의 값으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-254">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="a5820-255">키를 만들고 사용자를 가장하는 데 사용될 수 있으므로 클라이언트의 서명 키를 배포하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a5820-255">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="a5820-256">App Service에서 호스트하는 동안 *WEBSITE\_AUTH\_SIGNING\_KEY* 환경 변수를 참조하여 서명 키를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-256">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="a5820-257">로컬 디버깅 컨텍스트에서 필요한 경우 [인증을 사용하여 로컬 디버깅](#local-debug) 섹션의 지침에 따라 키를 검색하고 이 키를 응용 프로그램 설정으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-257">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="a5820-258">발급된 토큰은 다른 클레임 및 만료 날짜를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-258">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="a5820-259">최소한 발급된 토큰은 제목(**sub**) 클레임을 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-259">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="a5820-260">인증 경로를 오버로드하여 표준 클라이언트 `loginAsync()` 메서드를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-260">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="a5820-261">클라이언트가 `client.loginAsync('custom');`을(를) 호출하여 로그인하는 경우 경로는 `/.auth/login/custom`이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-261">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="a5820-262">`MapHttpRoute()`을(를) 사용하여 사용자 지정 인증 컨트롤러에 대한 경로를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-262">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="a5820-263">`loginAsync()` 방식을 사용하여 인증 토큰이 서비스에 대한 모든 후속 호출에 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-263">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
>
>

### <span data-ttu-id="a5820-264"><a name="user-info"></a>방법: 인증된 사용자 정보 검색</span><span class="sxs-lookup"><span data-stu-id="a5820-264"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="a5820-265">사용자가 앱 서비스에서 인증을 하는 경우 .NET 백 엔드 코드에서 할당된 사용자 ID와 기타 정보에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-265">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="a5820-266">백 엔드에서 권한 부여를 결정하는 데 사용자 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-266">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="a5820-267">다음 코드는 요청과 연결된 사용자 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-267">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="a5820-268">SID는 공급자 특정 사용자 ID에서 파생되고 지정된 사용자 및 로그인 공급자에 대해 정적입니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-268">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="a5820-269">SID는 잘못된 인증 토큰에 대한 null입니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-269">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="a5820-270">또한 앱 서비스는 로그인 공급자에서 특정 클레임을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-270">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="a5820-271">각 ID 공급자는 ID 공급자 SDK를 사용하여 자세한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-271">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="a5820-272">예를 들어 친구 정보에 대한 Facebook Graph API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-272">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="a5820-273">Azure 포털의 공급자 블레이드에서 요청된 클레임을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-273">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="a5820-274">일부 클레임은 ID 공급자를 사용하여 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-274">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="a5820-275">다음 코드는 **GetAppServiceIdentityAsync** 확장 메서드를 호출하여 로그인 자격 증명을 가져오며 이는 Facebook Graph API에 대한 요청에 필요한 액세스 토큰을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-275">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="a5820-276">**GetAppServiceIdentityAsync** 확장 메서드를 제공하는 `System.Security.Principal`에 문을 사용하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-276">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="a5820-277"><a name="authorize"></a>방법: 인증된 사용자에 대한 데이터 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="a5820-277"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="a5820-278">이전 섹션에서는 인증된 사용자의 사용자 ID를 검색하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-278">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="a5820-279">이 값에 따라 데이터 및 다른 리소스에 대한 액세스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-279">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="a5820-280">예를 들어 테이블에 userId 열을 추가하고 사용자 ID를 기준으로 쿼리 결과를 필터링하면 반환된 데이터를 허가된 사용자만 액세스하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-280">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="a5820-281">다음 코드는 SID가 TodoItem 테이블의 UserId 열 값과 일치할 때만 데이터 행을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-281">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="a5820-282">`Query()` 메서드는 필터링을 처리하는 LINQ에 의해 조작될 수 있는 `IQueryable`을(를) 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-282">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="a5820-283">방법: 서버 프로젝트에 푸시 알림 추가</span><span class="sxs-lookup"><span data-stu-id="a5820-283">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="a5820-284">**MobileAppConfiguration** 개체를 확장하고 알림 허브 클라이언트를 만들어 서버 프로젝트에 푸시 알림을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-284">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="a5820-285">Visual Studio에서 서버 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리**를 클릭한 후 `Microsoft.Azure.Mobile.Server.Notifications`를 검색한 다음 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-285">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="a5820-286">이 단계를 반복하여 알림 허브 클라이언트 라이브러리를 포함하는 `Microsoft.Azure.NotificationHubs` 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-286">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="a5820-287">App_Start/Startup.MobileApp.cs에서 초기화하는 동안 **AddPushNotifications()** 확장 메서드에 대한 호출을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-287">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="a5820-288">알림 허브 클라이언트를 만드는 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-288">Add the following code that creates a Notification Hubs client:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="a5820-289">이제 등록된 장치에 푸시 알림을 보내는 데 알림 허브 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-289">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="a5820-290">자세한 내용은 [앱에 푸시 알림 추가](app-service-mobile-ios-get-started-push.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5820-290">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="a5820-291">알림 허브에 대한 자세한 내용은 [알림 허브 개요](../notification-hubs/notification-hubs-push-notification-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5820-291">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="a5820-292"><a name="tags"></a>방법: 태그를 사용하여 대상 지정 푸시 활성화</span><span class="sxs-lookup"><span data-stu-id="a5820-292"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="a5820-293">알림 허브를 사용하면 태그를 사용하여 특정 등록에 대상이 지정된 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-293">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="a5820-294">여러 태그가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-294">Several tags are created automatically:</span></span>

* <span data-ttu-id="a5820-295">설치 ID는 특정 장치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-295">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="a5820-296">인증된 SID에 따라 사용자 ID는 특정 사용자를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-296">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="a5820-297">**MobileServiceClient**의 **installationId** 속성에서 설치 ID에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-297">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="a5820-298">다음 예제에서는 설치 ID를 사용하여 알림 허브에서 특정 설치에 태그를 추가하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-298">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="a5820-299">설치를 만들 때 푸시 알림 등록을 수행하는 동안 클라이언트가 제공한 태그는 백 엔드에서 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-299">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="a5820-300">클라이언트를 사용하여 설치에 태그를 추가하려면 이전 패턴을 사용하여 태그를 추가하는 사용자 지정 API를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-300">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span>

<span data-ttu-id="a5820-301">예제는 App Service Mobile Apps 완료된 빠른 시작 샘플에서 [클라이언트 추가 푸시 알림 태그][5]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5820-301">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="a5820-302"><a name="push-user"></a>방법: 인증된 사용자에게 푸시 알림 보내기</span><span class="sxs-lookup"><span data-stu-id="a5820-302"><a name="push-user"></a>How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="a5820-303">인증된 사용자가 푸시 알림에 등록하면 사용자 ID 태그가 등록에 자동으로 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-303">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="a5820-304">이 태그를 사용하여 해당 사용자로 등록된 모든 장치에 푸시 알림을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-304">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="a5820-305">다음 코드는 요청을 만드는 사용자의 SID를 가져오고 해당 사용자에 대한 모든 장치 등록에 템플릿 푸시 알림을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-305">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="a5820-306">인증된 클라이언트의 푸시 알림을 등록할 때 등록을 시도하기 전에 인증이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-306">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="a5820-307">자세한 내용은 .NET 백 엔드에 대한 App Service Mobile Apps 완료된 빠른 시작 샘플에서 [사용자에게 푸시 알림 보내기][6]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5820-307">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="a5820-308">방법: .NET 서버 SDK 디버그 및 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a5820-308">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="a5820-309">Azure 앱 서비스는 ASP.NET 응용 프로그램에 대한 여러 디버깅 및 문제 해결 기술을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-309">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="a5820-310">Azure 앱 서비스 모니터링</span><span class="sxs-lookup"><span data-stu-id="a5820-310">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="a5820-311">Azure 앱 서비스에 진단 로그 사용</span><span class="sxs-lookup"><span data-stu-id="a5820-311">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="a5820-312">Visual Studio에서 Azure 앱 서비스 문제 해결</span><span class="sxs-lookup"><span data-stu-id="a5820-312">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="a5820-313">로깅</span><span class="sxs-lookup"><span data-stu-id="a5820-313">Logging</span></span>
<span data-ttu-id="a5820-314">표준 ASP.NET 추적 작성을 사용하여 앱 서비스 진단 로그에 쓸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-314">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="a5820-315">로그를 작성하려면 먼저 모바일 앱 백 엔드에서 진단을 활성화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-315">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="a5820-316">진단을 사용하도록 설정하고 로그에 쓰려면:</span><span class="sxs-lookup"><span data-stu-id="a5820-316">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="a5820-317">[진단을 사용하는 방법](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag)에서 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-317">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="a5820-318">코드 파일에 다음 using 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-318">Add the following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="a5820-319">.NET 백 엔드에서 진단 로그에 작성하려면 다음과 같이 추적 작성기를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-319">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="a5820-320">서버 프로젝트를 다시 게시하고 모바일 앱 백 엔드에 액세스하여 로깅을 통해 코드 경로를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-320">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="a5820-321">[방법: 로그 다운로드](../app-service-web/web-sites-enable-diagnostic-log.md#download)에 설명된 대로 로그를 다운로드하고 평가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-321">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="a5820-322"><a name="local-debug"></a>인증을 사용하여 로컬 디버깅</span><span class="sxs-lookup"><span data-stu-id="a5820-322"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="a5820-323">응용 프로그램을 로컬로 실행하여 변경 내용을 클라우드에 게시하기 전에 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-323">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="a5820-324">대부분의 Azure Mobile Apps 백 엔드의 경우 Visual Studio에 있는 동안 *F5* 를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-324">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="a5820-325">그러나 인증을 사용할 때 몇 가지 추가 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-325">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="a5820-326">클라우드 기반 모바일 앱에서 앱 서비스 인증/권한 부여를 구성해야 하며 클라이언트가 클라우드 끝점을 대체 로그인 호스트로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-326">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="a5820-327">필요한 구체적인 단계는 클라이언트 플랫폼에 대한 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a5820-327">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="a5820-328">모바일 백 엔드에 [Microsoft.Azure.Mobile.Server.Authentication] 을 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-328">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="a5820-329">그런 다음 `MobileAppConfiguration`를 `HttpConfiguration`에 적용한 후 응용 프로그램의 OWIN 시작 클래스에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-329">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="a5820-330">앞의 예제에서는 HTTPS 체계를 사용하여 Web.config 파일 내에서 *authAudience* 및 *authIssuer* 응용 프로그램 설정을 응용 프로그램 루트의 URL로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-330">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="a5820-331">마찬가지로 *authSigningKey* 를 응용 프로그램의 서명 키의 값으로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-331">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span>
<span data-ttu-id="a5820-332">서명 키를 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="a5820-332">To obtain the signing key:</span></span>

1. <span data-ttu-id="a5820-333">[Azure 포털]</span><span class="sxs-lookup"><span data-stu-id="a5820-333">Navigate to your app within the [Azure portal]</span></span>
2. <span data-ttu-id="a5820-334">**도구**, **Kudu**, **이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-334">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="a5820-335">Kudu 관리 사이트에서 **환경**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-335">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="a5820-336">*WEBSITE\_AUTH\_SIGNING\_KEY*에 대한 값을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-336">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="a5820-337">로컬 응용 프로그램 구성에서 *authSigningKey* 매개 변수에 대한 서명 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-337">Use the signing key for the *authSigningKey* parameter in your local application config.</span></span>  <span data-ttu-id="a5820-338">로컬로 실행 중일 때 모바일 백 엔드가 이제 클라이언트가 클라우드 기반 끝점에서 가져오는 토큰을 확인하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a5820-338">Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
<span data-ttu-id="a5820-339">[Azure 포털]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="a5820-339">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="a5820-340">[NuGet.org]: http://www.nuget.org/</span><span class="sxs-lookup"><span data-stu-id="a5820-340">[NuGet.org]: http://www.nuget.org/</span></span>
<span data-ttu-id="a5820-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span><span class="sxs-lookup"><span data-stu-id="a5820-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span></span>
<span data-ttu-id="a5820-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span><span class="sxs-lookup"><span data-stu-id="a5820-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span></span>
<span data-ttu-id="a5820-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span><span class="sxs-lookup"><span data-stu-id="a5820-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span></span>
<span data-ttu-id="a5820-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span><span class="sxs-lookup"><span data-stu-id="a5820-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span></span>
<span data-ttu-id="a5820-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span><span class="sxs-lookup"><span data-stu-id="a5820-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span></span>
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
