---
title: "hello.NET 백 엔드 서버 모바일 앱에 대 한 SDK와 aaaHow toowork | Microsoft Docs"
description: "Azure 앱 서비스 모바일 앱에 대 한와 toowork.NET 백 엔드 서버 SDK hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="82494-104">Azure 모바일 앱에 대 한 hello.NET 백 엔드 서버 SDK 사용</span><span class="sxs-lookup"><span data-stu-id="82494-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="82494-105">이 항목에서는 toouse 주요 Azure 앱 서비스 모바일 앱 시나리오에서.NET 백 엔드 서버 SDK hello 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82494-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="82494-106">hello Azure 모바일 앱 SDK를 사용 하면 모바일 클라이언트 및 ASP.NET 응용 프로그램에서 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="82494-107">hello [.NET 서버 Azure 모바일 앱에 대 한 SDK] [ 2] 은 GitHub의 오픈 소스입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="82494-108">hello 리포지토리 hello 전체 서버 SDK 단위 테스트 도구 모음 및 일부 샘플 프로젝트를 포함 하 여 모든 소스 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="82494-109">참조 설명서</span><span class="sxs-lookup"><span data-stu-id="82494-109">Reference documentation</span></span>
<span data-ttu-id="82494-110">hello 서버 SDK에 대 한 참조 설명서 hello은 여기에서 찾을: [Azure 모바일 앱.NET 참조][1]합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="82494-111"><a name="create-app"></a>방법: .NET 모바일 앱 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="82494-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="82494-112">새 프로젝트를 시작 하는 경우에 어느 hello를 사용 하 여 응용 프로그램 서비스 응용 프로그램을 만들 수 있습니다 [Azure 포털] 또는 Visual Studio입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="82494-113">Hello 응용 프로그램 서비스 응용 프로그램을 로컬로 실행 하거나 hello 프로젝트 tooyour 클라우드 기반 앱 서비스 모바일 앱을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="82494-114">모바일 기능 tooan 기존 프로젝트를 추가 하는 경우 참조 hello [다운로드 하 고 hello SDK 초기화](#install-sdk) 섹션.</span><span class="sxs-lookup"><span data-stu-id="82494-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="82494-115">Hello Azure 포털을 사용 하 여.NET 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="82494-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="82494-116">hello를 수행 하거나 앱 서비스 모바일 백 엔드 toocreate [빠른 시작 자습서] [ 3] 하거나이 단계를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="82494-117">Hello에 다시 *시작* 블레이드 아래 **API 테이블을 만들**, 선택 **C#** 으로 프로그램 **백 엔드 언어**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="82494-118">클릭 **다운로드**, 압축 된 프로젝트 파일 tooyour 로컬 컴퓨터에 압축을 풀고 Visual Studio에서 hello 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="82494-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="82494-119">Visual Studio 2013 및 Visual Studio 2015를 사용하여 .NET 백 엔드 만들기</span><span class="sxs-lookup"><span data-stu-id="82494-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="82494-120">Hello 설치 [Azure SDK for.NET] [ 4] (2.9.0 버전 이상) toocreate Visual Studio에서 Azure 모바일 앱 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="82494-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="82494-121">Hello SDK를 설치한 경우 단계를 수행 하는 hello를 사용 하 여 ASP.NET 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82494-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="82494-122">열기 hello **새 프로젝트** 대화 (에서 *파일* > **새로** > **프로젝트...** ).</span><span class="sxs-lookup"><span data-stu-id="82494-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="82494-123">**템플릿** > **Visual C#**를 확장하고 **웹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="82494-124">**ASP.NET 웹 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="82494-125">Hello 프로젝트 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-125">Fill in hello project name.</span></span> <span data-ttu-id="82494-126">그런 후 **OK**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-126">Then click **OK**.</span></span>
5. <span data-ttu-id="82494-127">*ASP.NET 4.5.2 템플릿*아래에서 **Azure Mobile App**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="82494-128">확인 **hello 클라우드의 호스트에에서** toocreate hello에 모바일 백 엔드 클라우드 toowhich이이 프로젝트를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="82494-129">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-129">Click **OK**.</span></span>

## <span data-ttu-id="82494-130"><a name="install-sdk"></a>방법: 다운로드 및 hello SDK를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="82494-131">hello SDK는에서 사용할 수 있는 [NuGet.org]합니다. 이 패키지에 hello 필요한 기본 기능 tooget hello SDK를 사용 하 여 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="82494-132">tooinitialize SDK hello, tooperform 작업 hello에 필요한 **HttpConfiguration** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="82494-133">Hello SDK 설치</span><span class="sxs-lookup"><span data-stu-id="82494-133">Install hello SDK</span></span>
<span data-ttu-id="82494-134">tooinstall hello SDK, Visual Studio의 hello 서버 프로젝트를 마우스 오른쪽 단추로 선택 **NuGet 패키지 관리**, hello에 대 한 검색 [Microsoft.Azure.Mobile.Server] 패키지 하 고, 한 다음 클릭  **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="82494-135"><a name="server-project-setup"></a>Hello 서버 프로젝트를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="82494-136">.NET 백 엔드 서버 프로젝트에는 OWIN 시작 클래스를 포함 하 여 초기화 된 유사한 tooother ASP.NET 프로젝트는.</span><span class="sxs-lookup"><span data-stu-id="82494-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="82494-137">Hello NuGet 패키지를 참조 한 확인 `Microsoft.Owin.Host.SystemWeb`합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="82494-138">tooadd Visual Studio에서이 클래스 단추로 클릭 하 여 서버 프로젝트 고 **추가** >
**새 항목**, 다음 **웹**  >  ** 일반** > **OWIN 시작 클래스**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="82494-139">클래스는 hello 특성을 다음으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82494-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="82494-140">Hello에 `Configuration()` OWIN 시작 클래스를 사용 하 여의 메서드로 **HttpConfiguration** 개체 tooconfigure hello Azure 모바일 앱 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="82494-141">다음 예제는 hello 추가 된 기능이 없는 hello 서버 프로젝트를 초기화 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="82494-142">tooenable 개별 기능 hello에 확장 메서드를 호출 해야 **MobileAppConfiguration** 호출 하기 전에 개체 **ApplyTo**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="82494-143">예를 들어 hello 코드 다음 추가 hello 기본 라우팅합니다 hello 특성이 있는 tooall API 컨트롤러 `[MobileAppController]` 초기화 하는 동안:</span><span class="sxs-lookup"><span data-stu-id="82494-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="82494-144">hello 서버 빠른 시작에서 Azure 포털 호출 hello **UseDefaultConfiguration()**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="82494-145">다음 단계를이 해당 toohello:</span><span class="sxs-lookup"><span data-stu-id="82494-145">This equivalent toohello following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="82494-146">사용 되는 hello 확장 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-146">hello extension methods used are:</span></span>

* <span data-ttu-id="82494-147">`AddMobileAppHomeController()`hello 기본 Azure 모바일 앱 홈 페이지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="82494-148">`MapApiControllers()`hello로 데코 레이트 된 WebAPI 컨트롤러에 대 한 사용자 지정 API 기능을 제공 `[MobileAppController]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="82494-149">`AddTables()`hello의 매핑을 제공 `/tables` 끝점 tootable 컨트롤러입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="82494-150">`AddTablesWithEntityFramework()`매핑 hello에 대 한 축약형 `/tables` Entity Framework를 사용 하 여 끝점 컨트롤러를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="82494-151">`AddPushNotifications()`은(는) Notification Hubs에 대한 장치를 등록하는 간단한 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="82494-152">`MapLegacyCrossDomainController()` 은(는) 로컬 개발을 위한 표준 CORS 헤더를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="82494-153">SDK 확장</span><span class="sxs-lookup"><span data-stu-id="82494-153">SDK extensions</span></span>
<span data-ttu-id="82494-154">hello NuGet 기반 확장 패키지를 다음 응용 프로그램에서 사용할 수 있는 다양 한 모바일 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="82494-155">Hello를 사용 하 여 초기화 하는 동안 확장을 사용 하면 **MobileAppConfiguration** 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="82494-156">[Microsoft.Azure.Mobile.Server.Quickstart] 지원 hello 기본 모바일 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="82494-157">Hello 호출 하 여 추가 된 toohello 구성을 **UseDefaultConfiguration** 초기화 하는 동안 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="82494-158">이 확장은 알림, 인증, 엔터티, 테이블, Crossdomain 및 홈 패키지와 같은 확장을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="82494-159">이 패키지는 hello hello Azure 포털에서 사용할 수 있는 모바일 앱 빠른 시작에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82494-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="82494-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) hello 기본 구현 *모바일 앱이 실행 되 고 페이지* hello 웹 사이트 루트에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="82494-161">Toohello 구성을 호출 하 여 추가 된 **AddMobileAppHomeController** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="82494-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) 데이터 및 설정 접속 hello 데이터 파이프라인을 사용 하기 위한 클래스가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82494-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="82494-163">Hello를 호출 하 여 toohello 구성을 추가 **AddTables** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="82494-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) hello Entity Framework hello SQL 데이터베이스에서에서 데이터를 tooaccess 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="82494-165">Hello를 호출 하 여 toohello 구성을 추가 **AddTablesWithEntityFramework** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="82494-166">[Microsoft.Azure.Mobile.Server.Authentication] toovalidate 토큰을 사용 하는 사용 하면 인증 및 집합 접속 hello OWIN 미들웨어입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="82494-167">Hello를 호출 하 여 toohello 구성을 추가 **AddAppServiceAuthentication** 및 **IAppBuilder**. **UseAppServiceAuthentication** 확장 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="82494-168">[Microsoft.Azure.Mobile.Server.Notifications] 푸시 알림을 사용할 수 있도록 하며 푸시 등록 끝점을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="82494-169">Hello를 호출 하 여 toohello 구성을 추가 **AddPushNotifications** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="82494-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) 데이터 toolegacy 모바일 앱에서 웹 브라우저를 사용 하는 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82494-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="82494-171">Toohello 구성을 호출 하 여 추가 된 **MapLegacyCrossDomainController** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="82494-172">[Microsoft.Azure.Mobile.Server.Login] hello AppServiceLoginHandler.CreateToken() 메서드를 사용자 지정 인증 시나리오를 사용 하는 정적 메서드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="82494-173"><a name="publish-server-project"></a>방법: hello 서버 프로젝트 게시</span><span class="sxs-lookup"><span data-stu-id="82494-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="82494-174">이 섹션에서는 어떻게 toopublish.NET 백 엔드에서에서 프로젝트를 Visual Studio를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82494-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="82494-175">Git를 사용 하 여 백 엔드 프로젝트를 배포할 수도 있습니다 또는 hello에서 설명 하는 다른 방법 중 하나 hello [Azure 앱 서비스 배포 설명서](../app-service-web/web-sites-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="82494-176">Visual Studio에서 hello 프로젝트 toorestore NuGet 패키지를 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="82494-177">솔루션 탐색기, 마우스 오른쪽 단추로 클릭 hello 프로젝트에서에서 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="82494-178">hello 처음 게시할 때는 해야 toodefine 게시 프로필.</span><span class="sxs-lookup"><span data-stu-id="82494-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="82494-179">이미 정의된 프로필이 있을 때 프로필을 선택하고 **게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="82494-180">게시 대상 tooselect 묻는 메시지가 나타나면 클릭 **Microsoft Azure 앱 서비스** > **다음**, (필요한 경우) 한 다음 Azure 자격 증명으로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="82494-181">Visual Studio가 Azure에서 직접 게시 설정을 안전하게 다운로드하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="82494-182">**구독**을 선택하고 **보기**에서 **리소스 형식**을 선택하며 **모바일 앱**을 확장하고 모바일 앱 백 엔드를 클릭한 다음 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="82494-183">Hello 확인을 클릭 하 고 게시 프로필 정보 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="82494-184">모바일 앱 백 엔드가 성공적으로 게시되면 성공했다는 것을 나타내는 방문 페이지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="82494-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="82494-185"><a name="define-table-controller"></a> 방법: 테이블 컨트롤러 정의</span><span class="sxs-lookup"><span data-stu-id="82494-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="82494-186">SQL 테이블 toomobile 클라이언트 테이블 컨트롤러 tooexpose를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="82494-187">테이블 컨트롤러를 구성하려면 세 단계가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="82494-188">데이터 전송 개체(DTO) 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82494-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="82494-189">Hello 모바일 DbContext 클래스에에서 대 한 테이블 참조를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="82494-190">테이블 컨트롤러를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82494-190">Create a table controller.</span></span>

<span data-ttu-id="82494-191">데이터 전송 개체(DTO)는 `EntityData`에서 상속하는 일반 C# 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="82494-192">예:</span><span class="sxs-lookup"><span data-stu-id="82494-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="82494-193">hello DTO는 hello SQL 데이터베이스 내에서 사용 되는 toodefine hello 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="82494-194">toocreate hello 추가, 항목 데이터베이스는 `DbSet<>` 속성을 사용 하는 DbContext hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="82494-195">Azure 모바일 앱에 대 한 기본 프로젝트 템플릿에서 hello hello DbContext 라고 `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="82494-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="82494-196">Azure SDK를 설치 하는 hello를 사용 하도록 설정한 경우 다음과 같은 템플릿 테이블 컨트롤러를 만들 이제 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="82494-197">안녕하세요 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 선택 **추가** > **컨트롤러 중...** .</span><span class="sxs-lookup"><span data-stu-id="82494-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="82494-198">선택 hello **Azure 모바일 앱 테이블 컨트롤러** 클릭 한 다음 옵션을 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="82494-199">Hello에 **컨트롤러 추가** 대화 상자:</span><span class="sxs-lookup"><span data-stu-id="82494-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="82494-200">Hello에 **모델 클래스** 드롭다운을 선택 하면 새 DTO 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="82494-201">Hello에 **DbContext** 드롭다운에서 선택 hello 모바일 서비스 DbContext 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="82494-202">hello 컨트롤러 이름이 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82494-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="82494-203">**추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-203">Click **Add**.</span></span>

<span data-ttu-id="82494-204">hello 퀵 스타트 서버 프로젝트에 단순에 대 한 예가 포함 되어 **TodoItemController**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="82494-205"><a name="adjust-pagesize"></a>방법: hello 테이블 페이징 크기 조정</span><span class="sxs-lookup"><span data-stu-id="82494-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="82494-206">기본적으로 Azure 모바일 앱은 요청당 50개의 레코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="82494-207">페이징은 hello 클라이언트 사용 너무 오래 동안 UI 스레드와 hello 서버 효율적인 사용자 환경을 보장 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="82494-208">toochange hello 테이블 페이징 크기 증가 hello 서버 쪽 "허용 되는 쿼리 크기" 고 hello 클라이언트 쪽 페이지 크기 hello 서버 쪽 "허용 쿼리 크기"는 hello를 사용 하 여 `EnableQuery` 특성:</span><span class="sxs-lookup"><span data-stu-id="82494-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="82494-209">Hello PageSize는 hello 클라이언트에서 요청한 hello 크기 보다 크거나 같은 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="82494-210">Hello 클라이언트 페이지 크기 변경에 대 한 내용은 toohello 특정 클라이언트 방법 문서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="82494-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="82494-211">방법: 사용자 지정 API 컨트롤러 정의</span><span class="sxs-lookup"><span data-stu-id="82494-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="82494-212">사용자 지정 API 컨트롤러 hello 끝점을 노출 하 여 hello 가장 기본적인 기능 tooyour 모바일 앱 백 엔드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="82494-213">Hello [MobileAppController] 특성을 사용 하 여 모바일 전용 API 컨트롤러를 등록할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="82494-214">hello `MobileAppController` 특성 hello 경로 등록 hello 모바일 앱 JSON serializer를 설정 하 고 설정 [클라이언트 버전을 확인](app-service-mobile-client-and-server-versioning.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="82494-215">Visual Studio를 마우스 오른쪽 단추로 클릭 안녕하세요 Controllers 폴더를 클릭 한 다음 **추가** > **컨트롤러**선택, **Web API 2 컨트롤러&mdash;빈** 및 클릭 **추가**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="82494-216">`CustomController`와 같은 **컨트롤러 이름**을 제공하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="82494-217">Hello 새 컨트롤러 클래스 파일에서 추가 hello 다음 문을 사용 하 여:</span><span class="sxs-lookup"><span data-stu-id="82494-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="82494-218">Hello 적용 **[MobileAppController]** hello 다음 예제와 같이 toohello API 컨트롤러 클래스 정의 특성:</span><span class="sxs-lookup"><span data-stu-id="82494-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="82494-219">App_Start/Startup.MobileApp.cs 파일에서 추가 호출 toohello **MapApiControllers** hello 다음 예제와 같이 확장 메서드를:</span><span class="sxs-lookup"><span data-stu-id="82494-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="82494-220">Hello를 사용할 수도 있습니다 `UseDefaultConfiguration()` 확장 메서드 대신 `MapApiControllers()`합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="82494-221">**MobileAppControllerAttribute** 가 적용되지 않는 모든 컨트롤러는 클라이언트에서 여전히 액세스할 수 있지만 모든 모바일 앱 클라이언트 SDK로 올바르게 사용되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="82494-222">방법: 인증으로 작업</span><span class="sxs-lookup"><span data-stu-id="82494-222">How to: Work with authentication</span></span>
<span data-ttu-id="82494-223">앱 서비스 인증을 사용 하 여 azure 모바일 앱 / 권한 부여 toosecure 모바일 백 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="82494-224">이 섹션에서는 tooperform hello.NET 백 엔드 서버 프로젝트의 인증 관련 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="82494-225">방법: 인증 tooa 서버 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="82494-226">방법: 응용 프로그램에 사용자 지정 인증 사용</span><span class="sxs-lookup"><span data-stu-id="82494-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="82494-227">방법: 인증된 사용자 정보 검색</span><span class="sxs-lookup"><span data-stu-id="82494-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="82494-228">방법: 인증된 사용자에 대한 데이터 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="82494-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="82494-229"><a name="add-auth"></a>방법: 인증 tooa 서버 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="82494-230">Hello를 확장 하 여 인증 tooyour 서버 프로젝트를 추가할 수 있습니다 **MobileAppConfiguration** 개체 및 OWIN 미들웨어를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="82494-231">Hello를 설치 하는 경우 [Microsoft.Azure.Mobile.Server.Quickstart] 패키지 및 호출 hello **UseDefaultConfiguration** 확장 메서드를 toostep 3을 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="82494-232">Visual Studio에서 설치 hello [Microsoft.Azure.Mobile.Server.Authentication] 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="82494-233">Hello Startup.cs 프로젝트 파일에서 다음 hello hello 시작 시 코드 줄을 hello 추가 **구성** 메서드:</span><span class="sxs-lookup"><span data-stu-id="82494-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="82494-234">이 OWIN 미들웨어 구성 요소 관련 hello 앱 서비스 게이트웨이에서 발급 한 토큰의 유효성을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="82494-235">Hello 추가 `[Authorize]` 특성 tooany 컨트롤러 또는 인증을 요구 하는 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="82494-236">방법에 대 한 toolearn tooauthenticate 클라이언트 tooyour 모바일 앱 백 엔드 참조 [추가 인증 tooyour 앱](app-service-mobile-ios-get-started-users.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="82494-237"><a name="custom-auth"></a>방법: 응용 프로그램에 사용자 지정 인증 사용</span><span class="sxs-lookup"><span data-stu-id="82494-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="82494-238">Toouse hello 응용 프로그램 서비스 인증/권한 부여 공급자 중 하나를 싶지 않은 경우 로그인 하는 시스템을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="82494-239">Hello 설치 [Microsoft.Azure.Mobile.Server.Login] tooassist 인증 토큰 생성 된 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="82494-240">사용자 자격 증명의 유효성 검사를 위한 고유 코드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="82494-241">예를 들어 데이터베이스의 솔트되고 해시된 암호를 기준으로 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="82494-242">Hello 아래의 예제에서는 hello `isValidAssertion()` 메서드 (다른 곳에서 정의 됨)는 이러한 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="82494-243">사용자 지정 인증 hello는 ApiController 만들고 노출 하 여 노출 됩니다 `register` 및 `login` 동작 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="82494-244">hello 클라이언트 hello 사용자 로부터 사용자 지정 UI toocollect hello 정보를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="82494-245">hello 정보가 다음 표준 HTTP POST로 제출 된 toohello API 호출 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="82494-246">Hello를 사용 하 여 토큰이 발급 될 hello 서버 hello 어설션에 유효성 검사, 일단 `AppServiceLoginHandler.CreateToken()` 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="82494-247">hello ApiController **하지 않아야** hello를 사용 하 여 `[MobileAppController]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="82494-248">예제 `login` 작업:</span><span class="sxs-lookup"><span data-stu-id="82494-248">An example `login` action:</span></span>

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

<span data-ttu-id="82494-249">앞 예제는 hello, LoginResult 및 LoginResultUser은 필수 속성을 노출 하는 직렬화 가능 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="82494-250">hello 클라이언트에서 로그인 응답 toobe hello 폼의 JSON 개체로 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="82494-251">hello `AppServiceLoginHandler.CreateToken()` 메서드를 포함 한 *대상 그룹* 및 *발급자* 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="82494-252">이러한 매개 변수를 모두 hello HTTPS 체계를 사용 하 여 응용 프로그램 루트의 toohello URL 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82494-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="82494-253">마찬가지로 설정 해야 *secretKey* 응용 프로그램의 toobe hello 값의 키를 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="82494-254">Hello를 사용 하는 toomint 키 수 있으며 사용자를 가장할 때 서명 클라이언트에서 키를 배포 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="82494-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="82494-255">Hello 서명 hello를 참조 하 여 응용 프로그램 서비스에서 호스트 하는 동안 키를 가져올 수 있습니다 *웹 사이트\_AUTH\_서명\_키* 환경 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="82494-256">로컬 디버깅 컨텍스트에서 필요한 경우 hello 지침 hello에 따라 [인증을 사용 하 여 로컬 디버깅](#local-debug) tooretrieve hello 키 섹션 및 응용 프로그램 설정으로 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="82494-257">hello 발급 된 토큰 다른 클레임 및 만료 날짜를 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="82494-258">최소한, hello 발급 된 토큰 주제를 포함 해야 합니다 (**sub**) 클레임입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="82494-259">Hello 표준 클라이언트를 지원할 수 있습니다 `loginAsync()` hello 인증 경로 오버 로드 하 여 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="82494-260">클라이언트 hello 호출 하는 경우 `client.loginAsync('custom');` 에 toolog, 프로그램 경로가 있어야 `/.auth/login/custom`합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="82494-261">사용 하 여 hello 사용자 지정 인증 컨트롤러에 대 한 hello 경로 설정할 수 있습니다 `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="82494-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="82494-262">Hello를 사용 하 여 `loginAsync()` 방식이 사용 되므로 해당 hello 인증 토큰이 연결 된 tooevery 후속 호출 toohello 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="82494-263"><a name="user-info"></a>방법: 인증된 사용자 정보 검색</span><span class="sxs-lookup"><span data-stu-id="82494-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="82494-264">사용자가 앱 서비스에 의해 인증, 사용자 ID 및 기타 정보.NET 백 엔드 코드를 할당 하는 hello를 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="82494-265">hello 사용자 정보 hello 백 엔드에 대 한 권한 부여 결정에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="82494-266">hello 다음 코드 가져오는 hello 사용자 ID를 요청과 연결 된 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="82494-267">hello SID hello 공급자 특정 사용자 ID에서 파생 되 고 지정 된 사용자와 로그인 공급자에 대 한 정적이 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="82494-268">hello SID 잘못 된 인증 토큰에 대 한 null입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="82494-269">또한 앱 서비스는 로그인 공급자에서 특정 클레임을 요청할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="82494-270">각 ID 공급자는 ID 공급자 SDK를 사용하여 자세한 정보를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="82494-271">예를 들어 친구 정보에 대 한 hello Facebook Graph API를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="82494-272">Hello 공급자 블레이드에서 hello Azure 포털에서에서 요청 된 클레임을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="82494-273">일부 클레임 hello id 공급자와 추가 구성이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="82494-274">hello 다음 호출 hello 코드 **GetAppServiceIdentityAsync** 확장 메서드 tooget hello 로그인 자격 증명을 hello Facebook Graph API에 대 한 hello 액세스 토큰 필요한 toomake 요청 포함:</span><span class="sxs-lookup"><span data-stu-id="82494-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="82494-275">사용 하 여 추가 대해 문을 `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** 확장 메서드.</span><span class="sxs-lookup"><span data-stu-id="82494-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="82494-276"><a name="authorize"></a>방법: 인증된 사용자에 대한 데이터 액세스 제한</span><span class="sxs-lookup"><span data-stu-id="82494-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="82494-277">Hello 이전 단원의 tooretrieve 인증된 된 사용자의 사용자 ID를 hello 하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="82494-278">액세스 toodata 및이 값에 따라 기타 리소스를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="82494-279">예를 들어 사용자 Id 열 tootables를 추가 하 고 hello hello 사용자 ID 기준으로 쿼리 결과 필터링 tooauthorized 사용자만 데이터를 반환 하는 간단한 방법을 toolimit입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="82494-280">hello 다음 코드 행을 반환 데이터 hello SID hello UserId hello TodoItem 테이블의 열 값과 일치 하는 경우에:</span><span class="sxs-lookup"><span data-stu-id="82494-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="82494-281">hello `Query()` 메서드가 반환 되는 `IQueryable` LINQ toohandle 필터링 하 여 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="82494-282">방법: 푸시 알림을 tooa 서버 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="82494-283">Hello를 확장 하 여 푸시 알림 tooyour 서버 프로젝트를 추가 **MobileAppConfiguration** 개체와 알림 허브 클라이언트 만들기.</span><span class="sxs-lookup"><span data-stu-id="82494-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="82494-284">Visual Studio에서 hello 서버 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 클릭 **NuGet 패키지 관리**, 검색할 `Microsoft.Azure.Mobile.Server.Notifications`, 클릭 **설치**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="82494-285">이 단계 tooinstall hello 반복 `Microsoft.Azure.NotificationHubs` hello 알림 허브 클라이언트 라이브러리를 포함 하는 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="82494-286">App_Start/Startup.MobileApp.cs에 추가 호출 toohello **AddPushNotifications()** 초기화 하는 동안 확장 메서드:</span><span class="sxs-lookup"><span data-stu-id="82494-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="82494-287">알림 허브 클라이언트를 만드는 코드를 다음 hello를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-287">Add hello following code that creates a Notification Hubs client:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="82494-288">이제 hello 알림 허브 클라이언트 toosend 푸시 알림을 tooregistered 장치를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="82494-289">자세한 내용은 참조 [추가 푸시 알림 tooyour 앱](app-service-mobile-ios-get-started-push.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="82494-290">알림 허브에 대해 자세히 toolearn 참조 [알림 허브 개요](../notification-hubs/notification-hubs-push-notification-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="82494-291"><a name="tags"></a>방법: 태그를 사용하여 대상 지정 푸시 활성화</span><span class="sxs-lookup"><span data-stu-id="82494-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="82494-292">알림 허브를 사용 하면 대상으로 지정 된 알림을 toospecific 등록 태그를 사용 하 여 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="82494-293">여러 태그가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="82494-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="82494-294">hello 설치 ID는 특정 장치를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="82494-295">hello 사용자 Id에 따라 인증 hello SID 특정 사용자를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="82494-296">ID는 hello에서 액세스할 수 있습니다 설치 hello **installationId** hello 속성 **MobileServiceClient**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="82494-297">hello 다음 예제에서는 설치 ID tooadd를 사용 하는 방법을 태그 tooa 특정 설치를 알림 허브에서:</span><span class="sxs-lookup"><span data-stu-id="82494-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="82494-298">푸시 알림 등록 하는 동안 hello 클라이언트에서 제공 하는 태그는 hello 설치를 만들 때 hello 백 엔드에서 무시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82494-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="82494-299">클라이언트 tooadd tooenable 태그 toohello 설치, 패턴 앞 hello를 사용 하 여 태그를 추가 하는 사용자 지정 API를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="82494-300">참조 [클라이언트 추가 푸시 알림 태그] [ 5] 예제를 보려면 hello 앱 서비스 모바일 앱 완료 된 quickstart 샘플에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="82494-301"><a name="push-user"></a>방법: 사용자를 인증 하는 송신 푸시 알림을 tooan</span><span class="sxs-lookup"><span data-stu-id="82494-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="82494-302">인증된 된 사용자 푸시 알림에 등록, 사용자 ID 태그 toohello 등록 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="82494-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="82494-303">이 태그를 사용 하 여 푸시 알림 tooall 장치가 해당 사용자가 등록 되어 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="82494-304">hello 다음 코드 hello 요청을 만드는 사용자의 SID 가져오고 해당 사용자에 대 한 템플릿 푸시 알림 tooevery 장치 등록을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="82494-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="82494-305">인증된 클라이언트의 푸시 알림을 등록할 때 등록을 시도하기 전에 인증이 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="82494-306">자세한 내용은 참조 [toousers 푸시] [ 6] .NET 백 엔드에 대 한 hello 앱 서비스 모바일 앱 완료 된 quickstart 샘플에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="82494-307">방법: 디버그 및.NET 서버 SDK hello 문제 해결</span><span class="sxs-lookup"><span data-stu-id="82494-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="82494-308">Azure 앱 서비스는 ASP.NET 응용 프로그램에 대한 여러 디버깅 및 문제 해결 기술을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="82494-309">Azure 앱 서비스 모니터링</span><span class="sxs-lookup"><span data-stu-id="82494-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="82494-310">Azure 앱 서비스에 진단 로그 사용</span><span class="sxs-lookup"><span data-stu-id="82494-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="82494-311">Visual Studio에서 Azure 앱 서비스 문제 해결</span><span class="sxs-lookup"><span data-stu-id="82494-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="82494-312">로깅</span><span class="sxs-lookup"><span data-stu-id="82494-312">Logging</span></span>
<span data-ttu-id="82494-313">Hello 표준 ASP.NET 추적 쓰기를 사용 하 여 tooApp 서비스 진단 로그를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="82494-314">Toohello 로그를 작성 하려면 먼저 모바일 앱 백엔드에 진단을 활성화 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="82494-315">tooenable 진단 및 쓰기 toohello 로그:</span><span class="sxs-lookup"><span data-stu-id="82494-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="82494-316">Hello 단계에 따라 [어떻게 tooenable 진단](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag)합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="82494-317">Hello 다음 추가 문을 사용 하 여 코드 파일에:</span><span class="sxs-lookup"><span data-stu-id="82494-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="82494-318">추적 기록기 toowrite를 hello.NET 백 엔드 toohello 진단 로그에서 다음과 같이 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82494-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="82494-319">서버 프로젝트를 다시 게시 하 고 hello 모바일 앱 백 엔드 tooexecute hello 코드 경로 hello 로깅 사용 하 여 액세스 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="82494-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="82494-320">다운로드 하 고에 설명 된 대로 hello 로그 평가 [하는 방법: 로그를 다운로드](../app-service-web/web-sites-enable-diagnostic-log.md#download)합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="82494-321"><a name="local-debug"></a>인증을 사용하여 로컬 디버깅</span><span class="sxs-lookup"><span data-stu-id="82494-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="82494-322">응용 프로그램을 실행할 수 tootest toohello 클라우드 가격표를 게시 하기 전에 변경 되는 로컬입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="82494-323">대부분의 Azure Mobile Apps 백 엔드의 경우 Visual Studio에 있는 동안 *F5* 를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="82494-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="82494-324">그러나 인증을 사용할 때 몇 가지 추가 고려 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82494-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="82494-325">클라우드 기반 모바일 앱으로 응용 프로그램 서비스 인증/권한 부여 구성 되어 있어야 하 고 클라이언트 hello 대체 로그인 호스트로 지정 하는 hello 클라우드 끝점 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="82494-326">필요한 hello 특별 한 단계에 대 한 클라이언트 플랫폼에 대 한 hello 설명서를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="82494-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="82494-327">모바일 백 엔드에 [Microsoft.Azure.Mobile.Server.Authentication] 을 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="82494-328">그런 다음 응용 프로그램의 OWIN 시작 클래스에서 후 hello 다음 추가 `MobileAppConfiguration` 적용된 tooyour 되었습니다 `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="82494-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="82494-329">앞 예제는 hello, hello를 구성 해야 *authAudience* 및 *authIssuer* Web.config 내에서 응용 프로그램 설정 파일 tooeach hello HTTPS를 사용 하 여 응용 프로그램 루트의 url 체계입니다.</span><span class="sxs-lookup"><span data-stu-id="82494-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="82494-330">마찬가지로 설정 해야 *authSigningKey* 응용 프로그램의 toobe hello 값의 키를 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="82494-331">tooobtain hello 서명 키:</span><span class="sxs-lookup"><span data-stu-id="82494-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="82494-332">Hello 내에서 tooyour 앱 이동 [Azure 포털]</span><span class="sxs-lookup"><span data-stu-id="82494-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="82494-333">**도구**, **Kudu**, **이동**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="82494-334">Hello Kudu 관리 사이트에서 클릭 **환경**합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="82494-335">에 대 한 hello 식일 *웹 사이트\_AUTH\_서명\_키*합니다.</span><span class="sxs-lookup"><span data-stu-id="82494-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="82494-336">서명 키 hello 사용 하 여 hello *authSigningKey* 로컬 응용 프로그램 config에 매개 변수입니다.  모바일 백 엔드는 이제 장착된 toovalidate 토큰을 로컬로 실행 하는 경우 hello 클라이언트 hello 클라우드 기반 끝점에서 hello 토큰을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="82494-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[Azure 포털]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
