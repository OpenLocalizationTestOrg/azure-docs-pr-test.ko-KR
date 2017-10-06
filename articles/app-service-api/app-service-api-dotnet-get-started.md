---
title: "API 앱 및 앱 서비스에서 ASP.NET을 시작 하는 aaaGet | Microsoft Docs"
description: "Toocreate, 배포 하 고 Visual Studio 2015를 사용 하 여 Azure 앱 서비스의 ASP.NET API 앱을 사용 하는 방법에 대해 알아봅니다."
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="6be7a-103">Azure 앱 서비스에서 API 앱, ASP.NET 및 Swagger 시작</span><span class="sxs-lookup"><span data-stu-id="6be7a-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="6be7a-104">이 hello 먼저 일련의 어떻게 toouse 기능 Azure 응용 프로그램의 서비스를 보여 주는 자습서는 개발 및 호스팅 Api는 RESTful 데 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-104">This is hello first in a series of tutorials that show how toouse features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="6be7a-105">이 자습서에는 Swagger 형식인 API 메타데이터에 대한 지원을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="6be7a-106">다음 내용을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-106">You'll learn:</span></span>

* <span data-ttu-id="6be7a-107">어떻게 toocreate 배포 [API 앱](app-service-api-apps-why-best-platform.md) Visual Studio 2015에 내장 된 도구를 사용 하 여 Azure 앱 서비스의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-107">How toocreate and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="6be7a-108">Hello를 사용 하 여 tooautomate API 검색 Swashbuckle NuGet 패키지로 방법 toodynamically API Swagger 메타 데이터를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-108">How tooautomate API discovery by using hello Swashbuckle NuGet package toodynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="6be7a-109">어떻게 toouse API Swagger 메타 데이터 tooautomatically API 앱에 대 한 클라이언트 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-109">How toouse Swagger API metadata tooautomatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="6be7a-110">샘플 응용 프로그램 개요</span><span class="sxs-lookup"><span data-stu-id="6be7a-110">Sample application overview</span></span>
<span data-ttu-id="6be7a-111">이 자습서에서는 간단한 할 일 모음 샘플 응용 프로그램으로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="6be7a-112">hello 응용 프로그램에 단일 페이지 응용 프로그램 (SPA) 프런트 엔드, ASP.NET Web API 중간 계층 및 ASP.NET Web API 데이터 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-112">hello application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![API 앱 샘플 응용 프로그램 다이어그램](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="6be7a-114">다음은 hello의 스크린 샷을 [AngularJS](https://angularjs.org/) 프런트 엔드 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-114">Here's a screen shot of hello [AngularJS](https://angularjs.org/) front end.</span></span>

![API 앱 샘플 응용 프로그램 toodo 목록](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="6be7a-116">Visual Studio 솔루션 hello 세 개의 프로젝트가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-116">hello Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="6be7a-117">**ToDoListAngular** -hello 프런트 엔드: hello 중간 계층을 호출 하는 AngularJS SPA 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-117">**ToDoListAngular** - hello front end: an AngularJS SPA that calls hello middle tier.</span></span>
* <span data-ttu-id="6be7a-118">**ToDoListAPI** -hello 중간 계층: hello 데이터 계층에 할 일 항목 tooperform CRUD 작업을 호출 하는 ASP.NET Web API 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-118">**ToDoListAPI** - hello middle tier: an ASP.NET Web API project that calls hello data tier tooperform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="6be7a-119">**ToDoListDataAPI** -hello 데이터 계층: 할 일 항목에 대 한 CRUD 작업을 수행 하는 ASP.NET Web API 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-119">**ToDoListDataAPI** - hello data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="6be7a-120">hello 3 계층 아키텍처 API 앱을 사용 하 여 구현할 수 있고은 여기서 데모 목적 으로만 사용 하는 많은 아키텍처 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-120">hello three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="6be7a-121">각 계층의 hello 코드는 하기만 하면 가능한 toodemonstrate API 앱 기능입니다. 예를 들어 hello 데이터 계층 지 속성 메커니즘으로 데이터베이스 대신 서버 메모리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-121">hello code in each tier is as simple as possible toodemonstrate API Apps features; for example, hello data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="6be7a-122">이 자습서를 완료를 두 개의 웹 API 프로젝트 hello 및 hello 클라우드에서 응용 프로그램 서비스 API 앱에서 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-122">On completing this tutorial, you'll have hello two Web API projects up and running in hello cloud in App Service API apps.</span></span>

<span data-ttu-id="6be7a-123">hello 시리즈의 다음 자습서 hello hello SPA 프런트 엔드 toohello 클라우드를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-123">hello next tutorial in hello series deploys hello SPA front end toohello cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6be7a-124">필수 조건</span><span class="sxs-lookup"><span data-stu-id="6be7a-124">Prerequisites</span></span>
* <span data-ttu-id="6be7a-125">ASP.NET Web API-hello 자습서 지침은 방법에 대 한 기본적인 지식이 있다고 가정 asp.net toowork [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) Visual Studio에서.</span><span class="sxs-lookup"><span data-stu-id="6be7a-125">ASP.NET Web API - hello tutorial instructions assume you have a basic knowledge of how toowork with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="6be7a-126">Azure 계정 - [무료로 Azure 계정을 열거나](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) [Visual Studio 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="6be7a-127">Tooget Azure 계정에 등록 하기 전에 Azure 앱 서비스를 시작 하려는 경우 너무 이동[앱 서비스 시도](https://azure.microsoft.com/try/app-service/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-127">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="6be7a-128">여기서 **신용 카드와 약정 없이**App Service에서 수명이 짧은 스타터 앱을 즉시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="6be7a-129">Visual Studio 2015 hello로 [Azure SDK for.NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -hello SDK에서 Visual Studio 2015 자동으로 설치 아직 없는 경우.</span><span class="sxs-lookup"><span data-stu-id="6be7a-129">Visual Studio 2015 with hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - hello SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="6be7a-130">Visual Studio에서 도움말 -> Microsoft Visual Studio를 클릭하고 "Azure App Service 도구 v2.9.1" 이상을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Azure 앱 도구 버전](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="6be7a-132">Hello SDK 종속성의 개수를 이미 있는 컴퓨터에 따라 설치 hello SDK에는 몇 분 tooa 30 분 이상에서 시간이 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-132">Depending on how many of hello SDK dependencies you already have on your machine, installing hello SDK could take a long time, from several minutes tooa half hour or more.</span></span>
    > 
    > 

## <a name="download-hello-sample-application"></a><span data-ttu-id="6be7a-133">Hello 샘플 응용 프로그램 다운로드</span><span class="sxs-lookup"><span data-stu-id="6be7a-133">Download hello sample application</span></span>
1. <span data-ttu-id="6be7a-134">Hello 다운로드 [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) 저장소입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-134">Download hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="6be7a-135">Hello를 클릭할 수 있는 **zip 파일 다운로드** 로컬 컴퓨터의 hello 리포지토리 단추 또는 복제 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-135">You can click hello **Download ZIP** button or clone hello repository on your local machine.</span></span>
2. <span data-ttu-id="6be7a-136">Visual Studio 2015 또는 2013에서 hello ToDoList 솔루션을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-136">Open hello ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="6be7a-137">각 솔루션 tootrust 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-137">You will need tootrust each solution.</span></span>
         <span data-ttu-id="6be7a-138">![보안 경고](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="6be7a-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="6be7a-139">Hello 솔루션 (CTRL + SHIFT + B) toorestore hello NuGet 패키지를 빌드하십시오.</span><span class="sxs-lookup"><span data-stu-id="6be7a-139">Build hello solution (CTRL + SHIFT + B)  toorestore hello NuGet packages.</span></span>
   
    <span data-ttu-id="6be7a-140">배포 하기 전에 작업에서 toosee hello 응용 프로그램을 하려는 경우 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-140">If you want toosee hello application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="6be7a-141">ToDoListDataAPI 시작 프로젝트 및 실행된 hello 솔루션 인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-141">Make sure that ToDoListDataAPI is your startup project and run hello solution.</span></span> <span data-ttu-id="6be7a-142">브라우저에서 toosee HTTP 403 오류를 하시면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-142">You should expect toosee a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="6be7a-143">Swagger API 메타데이터 및 UI 사용</span><span class="sxs-lookup"><span data-stu-id="6be7a-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="6be7a-144">Azure 앱 서비스에서는 기본적으로 [Swagger](http://swagger.io/) 2.0 API 메타데이터를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="6be7a-145">각 API 앱 Swagger JSON 형식의 hello API에 대 한 메타 데이터를 반환 하는 URL 끝점을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-145">Each API app can specify a URL endpoint that returns metadata for hello API in Swagger JSON format.</span></span> <span data-ttu-id="6be7a-146">hello 해당 끝점에서 반환 된 메타 데이터 수 toogenerate 클라이언트 코드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-146">hello metadata returned from that endpoint can be used toogenerate client code.</span></span>

<span data-ttu-id="6be7a-147">Hello를 사용 하 여 ASP.NET Web API 프로젝트 Swagger 메타 데이터를 동적으로 생성할 수 [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="6be7a-148">hello Swashbuckle NuGet 패키지는 다운로드 한 hello ToDoListDataAPI 및 ToDoListAPI 프로젝트에 이미 설치 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-148">hello Swashbuckle NuGet package is already installed in hello ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="6be7a-149">Hello 자습서의이 섹션에서는 생성 된 hello Swagger 2.0 메타 데이터를 보면을 hello Swagger 메타 데이터를 기반으로 하는 UI 테스트 하십시오.</span><span class="sxs-lookup"><span data-stu-id="6be7a-149">In this section of hello tutorial, you look at hello generated Swagger 2.0 metadata, and then you try out a test UI that is based on hello Swagger metadata.</span></span>

1. <span data-ttu-id="6be7a-150">Hello ToDoListDataAPI 프로젝트 설정 (**하지** hello ToDoListAPI 프로젝트) hello 시작 프로젝트로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-150">Set hello ToDoListDataAPI project (**not** hello ToDoListAPI project) as hello startup project.</span></span>
   
    ![ToDoDataAPI를 시작 프로젝트로 설정](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="6be7a-152">F5 키를 누르거나 클릭 **디버그 > 디버깅 시작** toorun hello 프로젝트를 디버그 모드에서.</span><span class="sxs-lookup"><span data-stu-id="6be7a-152">Press F5 or click **Debug > Start Debugging** toorun hello project in debug mode.</span></span>
   
    <span data-ttu-id="6be7a-153">hello 브라우저가 열리고 hello HTTP 403 오류 페이지를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-153">hello browser opens and shows hello HTTP 403 error page.</span></span>
3. <span data-ttu-id="6be7a-154">브라우저 주소 표시줄에서 추가 `swagger/docs/v1` toohello 끝날 hello 선과 다음 리턴 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-154">In your browser address bar, add `swagger/docs/v1` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="6be7a-155">(URL이 hello `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="6be7a-155">(hello URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="6be7a-156">Hello API에 대 한 Swashbuckle tooreturn Swagger 2.0 JSON 메타 데이터에서 사용 하는 hello 기본 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-156">This is hello default URL used by Swashbuckle tooreturn Swagger 2.0 JSON metadata for hello API.</span></span>
   
    <span data-ttu-id="6be7a-157">Internet Explorer를 사용 하 여 hello 묻는 toodownload는 *v1.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-157">If you're using Internet Explorer, hello browser prompts you toodownload a *v1.json* file.</span></span>
   
    ![IE에서 JSON 메타데이터 다운로드](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="6be7a-159">Chrome, Firefox 또는 가장자리를 사용 하는 hello 브라우저 hello 브라우저 창에서 JSON hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-159">If you're using Chrome, Firefox, or Edge, hello browser displays hello JSON in hello browser window.</span></span> <span data-ttu-id="6be7a-160">다른 브라우저 JSON를 다르게 처리 하 고 브라우저 창의 hello 예제 처럼 정확 하 게 나타나지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-160">Different browsers handle JSON differently, and your browser window may not look exactly like hello example.</span></span>
   
    ![Chrome에서 JSON 메타데이터](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="6be7a-162">hello에 대 한 hello 정의 된 hello 다음 샘플은 hello API에 대 한 hello Swagger 메타 데이터의 첫 번째 섹션 hello 메서드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-162">hello following sample shows hello first section of hello Swagger metadata for hello API, with hello definition for hello Get method.</span></span> <span data-ttu-id="6be7a-163">이 메타 데이터는 어떤 드라이브 hello Swagger UI 단계에 따라 hello에서 사용 하 고 hello 자습서 tooautomatically의 이후 섹션에서는 클라이언트 코드를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-163">This metadata is what drives hello Swagger UI that you use in hello following steps, and you use it in a later section of hello tutorial tooautomatically generate client code.</span></span>
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. <span data-ttu-id="6be7a-164">Hello 브라우저를 닫고 Visual Studio의 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-164">Close hello browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="6be7a-165">Hello ToDoListDataAPI에서에서 프로젝트를 **솔루션 탐색기**개방형 hello *App_Start\SwaggerConfig.cs* 파일을 다음 스크롤 tooline 174 한 hello 코드 다음 주석 처리를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-165">In hello ToDoListDataAPI project in **Solution Explorer**, open hello *App_Start\SwaggerConfig.cs* file, then scroll down tooline 174 and uncomment hello following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="6be7a-166">hello *SwaggerConfig.cs* 파일이 프로젝트에서 hello Swashbuckle 패키지를 설치할 때 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-166">hello *SwaggerConfig.cs* file is created when you install hello Swashbuckle package in a project.</span></span> <span data-ttu-id="6be7a-167">hello 파일에는 다양 한 방법으로 tooconfigure Swashbuckle 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-167">hello file provides a number of ways tooconfigure Swashbuckle.</span></span>
   
    <span data-ttu-id="6be7a-168">hello 코드 사용 hello hello 다음에서 사용 하는 Swagger UI 단계를 제거 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-168">hello code you've uncommented enables hello Swagger UI that you use in hello following steps.</span></span> <span data-ttu-id="6be7a-169">Hello API 응용 프로그램 프로젝트 템플릿을 사용 하 여 웹 API 프로젝트를 만들면이 코드 주석 처리 되어 기본적으로 보안 조치로 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-169">When you create a Web API project by using hello API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="6be7a-170">Hello 프로젝트를 다시 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-170">Run hello project again.</span></span>
7. <span data-ttu-id="6be7a-171">브라우저 주소 표시줄에서 추가 `swagger` toohello 끝날 hello 선과 다음 리턴 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-171">In your browser address bar, add `swagger` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="6be7a-172">(URL이 hello `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="6be7a-172">(hello URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="6be7a-173">Hello Swagger UI 페이지가 나타나면 클릭 **ToDoList** toosee hello 메서드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-173">When hello Swagger UI page appears, click **ToDoList** toosee hello methods available.</span></span>
   
    ![Swagger UI 사용 가능한 메서드](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="6be7a-175">Hello를 처음 클릭 **가져오기** hello 목록에서 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-175">Click hello first **Get** button in hello list.</span></span>
10. <span data-ttu-id="6be7a-176">Hello에 **매개 변수** 섹션에서 hello의 hello 값으로 별표를 입력 `owner` 매개 변수를 클릭 한 다음 **기능 직접 사용해**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-176">In hello **Parameters** section, enter an asterisk as hello value of hello `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="6be7a-177">이후의 자습서에서 인증을 추가 하면 hello 중간 계층 hello 실제 사용자 ID toohello 데이터 계층을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-177">When you add authentication in later tutorials, hello middle tier will provide hello actual user ID toohello data tier.</span></span> <span data-ttu-id="6be7a-178">지금은 모든 작업은 서로 별표 해당 소유자 ID로 인증을 사용 하지 않고 hello 응용 프로그램을 실행 하는 동안 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-178">For now, all tasks will have asterisk as their owner ID while hello application runs without authentication enabled.</span></span>
    
    ![Swagger UI 사용해 보기](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="6be7a-180">hello Swagger UI hello ToDoList Get 메서드를 호출 하 고 hello 응답 코드 및 JSON 결과 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-180">hello Swagger UI calls hello ToDoList Get method and displays hello response code and JSON results.</span></span>
    
    ![Swagger UI 사용해 보기 결과](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="6be7a-182">클릭 **Post**, 아래의 hello 상자를 클릭 하 고 **모델 스키마**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-182">Click **Post**, and then click hello box under **Model Schema**.</span></span>
    
    <span data-ttu-id="6be7a-183">상자를 클릭 하면 hello 모델 스키마 prefills hello 입력 Post 메서드 hello에 대 한 hello 매개 변수 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-183">Clicking hello model schema prefills hello input box where you can specify hello parameter value for hello Post method.</span></span> <span data-ttu-id="6be7a-184">(Internet Explorer에서 작동 하지 않는 경우 다른 브라우저를 사용 하거나 hello 다음 단계에서 수동으로 hello 매개 변수 값을 입력 합니다.)</span><span class="sxs-lookup"><span data-stu-id="6be7a-184">(If this doesn't work in Internet Explorer, use a different browser or enter hello parameter value manually in hello next step.)</span></span>  
    
    ![Swagger UI 사용해 보기 게시물](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="6be7a-186">Hello에 대 한 JSON 변경 hello `todo` 매개 변수 입력 상자를 다음과 같이 다음 예에서는, hello 또는 사용자 고유의 설명 텍스트를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-186">Change hello JSON in hello `todo` parameter input box so that it looks like hello following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="6be7a-187">**Try it out**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="6be7a-188">hello ToDoList API에서 HTTP 204 응답 코드가 성공을 나타내는 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-188">hello ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="6be7a-189">Hello를 처음 클릭 **가져오기** 단추를 클릭 한 다음 hello 페이지의 해당 섹션에 hello 클릭 **기능 직접 사용해** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-189">Click hello first **Get** button, and then in that section of hello page click hello **Try it out** button.</span></span>
    
    <span data-ttu-id="6be7a-190">이제 Get 메서드 응답 hello hello 새 toodo 항목을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-190">hello Get method response now includes hello new toodo item.</span></span>
15. <span data-ttu-id="6be7a-191">선택 사항: Put, Delete, hello를 시도 하십시오. 하 고 ID 메서드에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-191">Optional: Try also hello Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="6be7a-192">Hello 브라우저를 닫고 Visual Studio의 디버깅을 중지 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-192">Close hello browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="6be7a-193">Swashbuckle은 모든 ASP.NET Web API 프로젝트에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="6be7a-194">Tooadd Swagger 메타 데이터 생성 tooan 기존 프로젝트를 사용 하도록 하려는 경우 방금 hello Swashbuckle 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-194">If you want tooadd Swagger metadata generation tooan existing project, just install hello Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="6be7a-195">Swagger 메타데이터에는 각 API 작업에 대한 고유 ID가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="6be7a-196">기본적으로 Swashbuckle은 Web API 컨트롤러 메서드에 대한 중복 Swagger 작업 ID를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="6be7a-197">컨트롤러에 오버로드된 HTTP 메서드가 있는 경우 이러한 동작이 발생합니다(예: `Get()` 및 `Get(id)`).</span><span class="sxs-lookup"><span data-stu-id="6be7a-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="6be7a-198">Toohandle 오버 로드 하는 방법에 대 한 정보를 참조 하십시오. [Swashbuckle 사용자 지정에서 생성 된 API 정의](app-service-api-dotnet-swashbuckle-customize.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-198">For information about how toohandle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="6be7a-199">Visual Studio에서 Web API 프로젝트를 만들면 hello Azure API 앱 템플릿을 사용 하 여 고유한 작업 Id를 생성 하는 코드를 자동으로 추가 toohello *SwaggerConfig.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-199">If you create a Web API project in Visual Studio by using hello Azure API App template, code that generates unique operation IDs is automatically added toohello *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="6be7a-200"><a id="createapiapp"></a>Azure에서 API 앱 만들기 및 코드 tooit 배포</span><span class="sxs-lookup"><span data-stu-id="6be7a-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code tooit</span></span>
<span data-ttu-id="6be7a-201">Hello Visual Studio에 통합 된 Azure 도구를 사용 하면이 섹션에서는 **웹 게시** Azure에서 새로운 API toocreate 앱 마법사.</span><span class="sxs-lookup"><span data-stu-id="6be7a-201">In this section, you use Azure tools that are integrated into hello Visual Studio **Publish Web** wizard toocreate a new API app in Azure.</span></span> <span data-ttu-id="6be7a-202">그런 다음 hello ToDoListDataAPI 프로젝트 toohello 새 API 앱을 배포 하 고 hello Swagger UI를 실행 하 여 hello API를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-202">Then you deploy hello ToDoListDataAPI project toohello new API app and call hello API by running hello Swagger UI.</span></span>

1. <span data-ttu-id="6be7a-203">**솔루션 탐색기**hello ToDoListDataAPI 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-203">In **Solution Explorer**, right-click hello ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Visual Studio에서 게시 클릭](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="6be7a-205">Hello에 **프로필** hello 단계의 **웹 게시** 마법사를 클릭 하 여 **Microsoft Azure 앱 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-205">In hello **Profile** step of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![웹 게시에서 Azure 앱 서비스 클릭](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="6be7a-207">있습니다 아직 수행 하지 않은, 경우 tooyour Azure 계정에에서 서명 하거나 만료 된 하는 경우 자격 증명을 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-207">Sign in tooyour Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="6be7a-208">Hello 앱 서비스 대화 상자에서 Azure hello 선택 **구독** toouse을 차례로 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-208">In hello App Service dialog box, choose hello Azure **Subscription** you want toouse, and then click **New**.</span></span>
   
    ![앱 서비스 대화 상자에서 새로 만들기 클릭](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="6be7a-210">hello **호스팅** hello 탭 **응용 프로그램 서비스 만들기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-210">hello **Hosting** tab of hello **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="6be7a-211">설치 Swashbuckle 지정 된 웹 API 프로젝트를 배포 하기 때문에 Visual Studio API 앱 toocreate 한다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want toocreate an API App.</span></span> <span data-ttu-id="6be7a-212">이 hello로 표시 **API 앱 이름** 제목 및 여 hello 팩트는 hello **변경 유형을** 드롭다운 목록이 너무 설정 되어**API 앱**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-212">This is indicated by hello **API App Name** title and by hello fact that hello **Change Type** drop-down list is set too**API App**.</span></span>
   
    ![앱 서비스 대화 상자에서 앱 형식](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="6be7a-214">입력 한 **API 앱 이름** hello에 고유 *azurewebsites.net* 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-214">Enter an **API App Name** that is unique in hello *azurewebsites.net* domain.</span></span> <span data-ttu-id="6be7a-215">Visual Studio에서는 제안 된 hello 기본 이름을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-215">You can accept hello default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="6be7a-216">다른 사용자가 이미 사용 하는 이름을 입력 하는 경우 빨간색 느낌표가 toohello 바로 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-216">If you enter a name that someone else has already used, you see a red exclamation mark toohello right.</span></span>
   
    <span data-ttu-id="6be7a-217">hello hello API 앱의 URL을 됩니다 `{API app name}.azurewebsites.net`합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-217">hello URL of hello API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="6be7a-218">Hello에 **리소스 그룹** 드롭 다운 클릭 **새로**를 선택한 다음 원하는 경우 "ToDoListGroup" 또는 다른 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-218">In hello **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="6be7a-219">리소스 그룹은 API 앱, 데이터베이스, VM 등 Azure 리소스의 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="6be7a-220">이 자습서를 사용 하면 쉽게 toodelete hello 자습서에 대해 만드는 Azure 리소스를 hello 모두 한 번에 때문 최상의 toocreate 새 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-220">For this tutorial, it's best toocreate a new resource group because that makes it easy toodelete in one step all hello Azure resources that you create for hello tutorial.</span></span>
   
    <span data-ttu-id="6be7a-221">이 상자에서 기존 [리소스 그룹](../azure-resource-manager/resource-group-overview.md)을 선택하거나 구독의 기존 리소스 그룹과 다른 이름을 입력하여 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="6be7a-222">Hello 클릭 **새로** 단추 다음 toohello **앱 서비스 계획** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-222">Click hello **New** button next toohello **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="6be7a-223">hello 스크린 샷 샘플 값을 보여 줍니다 **API 앱 이름**, **구독**, 및 **리소스 그룹** -값이 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-223">hello screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![앱 서비스 만들기 대화 상자](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="6be7a-225">단계를 수행 하는 hello hello 새 리소스 그룹에 대 한 앱 서비스 계획을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-225">In hello following steps you create an App Service plan for hello new resource group.</span></span> <span data-ttu-id="6be7a-226">앱 서비스 계획에서 API 앱에서 실행 되는 hello 계산 리소스를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-226">An App Service plan specifies hello compute resources that your API app runs on.</span></span> <span data-ttu-id="6be7a-227">예를 들어 hello 무료 계층을 선택 하면 일부 유료 계층에 대 한 전용된 Vm에서 실행 하는 동안 공유 Vm에서 API 앱 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-227">For example, if you choose hello free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="6be7a-228">앱 서비스 계획에 대한 자세한 내용은 [앱 서비스 계획 개요](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be7a-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="6be7a-229">Hello에 **앱 서비스 계획 구성** 대화 상자에서 원하는 경우 "ToDoListPlan" 또는 다른 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-229">In hello **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="6be7a-230">Hello에 **위치** 드롭 다운 목록에서 가장 가까운 tooyou hello 위치 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-230">In hello **Location** drop-down list, choose hello location that is closest tooyou.</span></span>
   
    <span data-ttu-id="6be7a-231">이 설정은 앱이 실행되는 Azure 데이터 센터를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="6be7a-232">위치 닫기 tooyou toominimize 선택 [대기 시간](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-232">Choose a location close tooyou toominimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="6be7a-233">Hello에 **크기** 드롭 다운 클릭 **무료**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-233">In hello **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="6be7a-234">이 자습서에 대 한 hello 무료 가격 책정 계층에 충분 한 성능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-234">For this tutorial, hello free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="6be7a-235">Hello에 **앱 서비스 계획 구성** 대화 상자를 클릭 하 여 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-235">In hello **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![앱 서비스 계획 구성에서 확인 클릭](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="6be7a-237">Hello에 **응용 프로그램 서비스 만들기** 대화 상자를 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-237">In hello **Create App Service** dialog box, click **Create**.</span></span>
    
    ![앱 서비스 만들기 대화 상자에서 만들기 클릭](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="6be7a-239">Visual Studio hello API 앱 및 모든 hello API 앱에 대 한 hello 필요한 설정을 포함 하는 게시 프로필을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-239">Visual Studio creates hello API app and a publish profile that has all of hello required settings for hello API app.</span></span> <span data-ttu-id="6be7a-240">Hello를 엽니다 **웹 게시** 마법사를 사용 하 여 toodeploy hello 프로젝트.</span><span class="sxs-lookup"><span data-stu-id="6be7a-240">Then it opens hello **Publish Web** wizard, which you'll use toodeploy hello project.</span></span>
    
    <span data-ttu-id="6be7a-241">hello **웹 게시** hello에 마법사가 열립니다. **연결** 탭 (아래 그림 참조).</span><span class="sxs-lookup"><span data-stu-id="6be7a-241">hello **Publish Web** wizard opens on hello **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="6be7a-242">Hello에 **연결** 탭 hello **서버** 및 **사이트 이름** 지점 tooyour API 앱을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-242">On hello **Connection** tab, hello **Server** and **Site name** settings point tooyour API app.</span></span> <span data-ttu-id="6be7a-243">hello **사용자 이름** 및 **암호** 배포 하는 자격 증명이 Azure 만들어 드립니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-243">hello **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="6be7a-244">배포 후 Visual Studio는 브라우저 toohello 열립니다 **대상 URL** (즉 hello 유일한 목적은 **대상 URL**).</span><span class="sxs-lookup"><span data-stu-id="6be7a-244">After deployment, Visual Studio opens a browser toohello **Destination URL** (that's hello only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="6be7a-245">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-245">Click **Next**.</span></span>
    
    ![웹 게시의 연결 탭에서 다음 클릭](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="6be7a-247">다음 탭 hello는 hello **설정을** 탭 (아래 그림 참조).</span><span class="sxs-lookup"><span data-stu-id="6be7a-247">hello next tab is hello **Settings** tab (shown below).</span></span> <span data-ttu-id="6be7a-248">빌드 구성 탭 toodeploy hello에 대 한 디버그 빌드를 변경할 수 여기 [원격 디버깅](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-248">Here you can change hello build configuration tab toodeploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="6be7a-249">hello 탭에서는 여러 **파일 게시 옵션**:</span><span class="sxs-lookup"><span data-stu-id="6be7a-249">hello tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="6be7a-250">대상에 있는 추가적인 파일을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="6be7a-251">게시 중 미리 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-251">Precompile during publishing</span></span>
    * <span data-ttu-id="6be7a-252">Hello App_Data 폴더에서 파일 제외</span><span class="sxs-lookup"><span data-stu-id="6be7a-252">Exclude files from hello App_Data folder</span></span>
    
    <span data-ttu-id="6be7a-253">이 자습서의 경우 이런 것들이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="6be7a-254">옵션을 통해 수행하는 작업에 대한 자세한 설명은 [Visual Studio의 One-Click 게시를 사용하여 웹 프로젝트 배포 방법](https://msdn.microsoft.com/library/dd465337.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be7a-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="6be7a-255">**다음**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-255">Click **Next**.</span></span>
    
    ![웹 게시의 설정 탭에서 다음 클릭](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="6be7a-257">그런 다음는 hello **미리 보기** 수 파일 toobe 프로젝트 toohello API 앱에서 복사 하려는 영업 기회 toosee 제공 (아래 그림 참조)을 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-257">Next is hello **Preview** tab (shown below), which gives you an opportunity toosee what files are going toobe copied from your project toohello API app.</span></span> <span data-ttu-id="6be7a-258">Tooearlier에 배포한 프로젝트 tooan API 앱을 배포할 때 변경 된 파일만 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-258">When you're deploying a project tooan API app that you already deployed tooearlier, only changed files are copied.</span></span> <span data-ttu-id="6be7a-259">Toosee 복사 될 작업의 목록을 원하는 경우 클릭할 수 있는 hello **미리 보기 시작** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-259">If you want toosee a list of what will be copied, you can click hello **Start Preview** button.</span></span>
15. <span data-ttu-id="6be7a-260">**게시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-260">Click **Publish**.</span></span>
    
    ![웹 게시의 미리 보기 탭에서 게시 클릭](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="6be7a-262">Visual Studio hello ToDoListDataAPI 프로젝트 toohello 새 API 앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-262">Visual Studio deploys hello ToDoListDataAPI project toohello new API app.</span></span> <span data-ttu-id="6be7a-263">hello **출력** 창 로그 성공적으로 배포 하 고 hello API 앱의 브라우저 창 열고 toohello URL에 "성공적으로 만들어진된" 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-263">hello **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened toohello URL of hello API app.</span></span>
    
    ![출력 창 성공적인 배포](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![새 API 앱을 성공적으로 만들었습니다 페이지](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="6be7a-266">Hello 브라우저의 주소 표시줄에 "swagger" toohello URL을 추가 하 고 enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-266">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="6be7a-267">(URL이 hello `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="6be7a-267">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="6be7a-268">hello 브라우저 hello 클라우드에서 실행 되는 이전에 본 것과 동일한 Swagger UI 하지만 이제 hello를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-268">hello browser displays hello same Swagger UI that you saw earlier, but now it's running in hello cloud.</span></span> <span data-ttu-id="6be7a-269">Get 메서드 hello 및 뒤로 toohello 기본 2 할 일 항목 되 고 있는지 확인할 해보세요.</span><span class="sxs-lookup"><span data-stu-id="6be7a-269">Try out hello Get method, and you see that you're back toohello default 2 to-do items.</span></span> <span data-ttu-id="6be7a-270">hello 로컬 컴퓨터의 메모리에에서에 이전에 만든 hello 변경 내용이 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-270">hello changes you made earlier were saved in memory in hello local machine.</span></span>
17. <span data-ttu-id="6be7a-271">열기 hello [Azure 포털](https://portal.azure.com/)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-271">Open hello [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="6be7a-272">hello Azure 포털에는 API 앱 같은 Azure 리소스 관리에 대 한 웹 인터페이스입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-272">hello Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="6be7a-273">**더 많은 서비스 > App Services**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-273">Click **More Services > App Services**.</span></span>
    
    ![앱 서비스 찾아보기](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="6be7a-275">Hello에 **응용 프로그램 서비스** 블레이드를 찾아 새 API 앱을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-275">In hello **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="6be7a-276">(Azure 포털 hello toohello 오른쪽 열리는 창 라고 *블레이드*.)</span><span class="sxs-lookup"><span data-stu-id="6be7a-276">(In hello Azure portal, windows that open toohello right are called *blades*.)</span></span>
    
    ![앱 서비스 블레이드](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="6be7a-278">두 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-278">Two blades open.</span></span> <span data-ttu-id="6be7a-279">하나의 블레이드 hello API 앱에 대해 간략하게 않았으며 하나에 긴 보고 변경할 수 있는 설정 목록이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-279">One blade has an overview of hello API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="6be7a-280">Hello에 **설정** 블레이드, 찾기 hello **API** 섹션 및 클릭 **API 정의**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-280">In hello **Settings** blade, find hello **API** section and click **API Definition**.</span></span>
    
    ![설정 블레이드에서 API 정의](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="6be7a-282">hello **API 정의** 블레이드를 사용 하면 JSON 형식의 Swagger 2.0 메타 데이터를 반환 하는 hello URL을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-282">hello **API Definition** blade lets you specify hello URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="6be7a-283">기본 Swashbuckle 생성 된 메타 데이터가 이전에 본 hello API 앱에 대 한 hello API 정의 URL toohello 기본값 설정 Visual Studio hello API 앱을 만들 때 URL 더하기 `/swagger/docs/v1`합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-283">When Visual Studio creates hello API app, it sets hello API definition URL toohello default value for Swashbuckle-generated metadata that you saw earlier, which is hello API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![API 정의 URL](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="6be7a-285">에 API 앱 toogenerate 클라이언트 코드를 선택 하면 Visual Studio이이 URL에서 hello 메타 데이터를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-285">When you select an API app toogenerate client code for it, Visual Studio retrieves hello metadata from this URL.</span></span>

## <span data-ttu-id="6be7a-286"><a id="codegen"></a>Hello 데이터 계층에 대 한 클라이언트 코드 생성</span><span class="sxs-lookup"><span data-stu-id="6be7a-286"><a id="codegen"></a> Generate client code for hello data tier</span></span>
<span data-ttu-id="6be7a-287">Swagger Azure API 앱에 통합 hello 장점 중 하나에 자동 코드 생성입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-287">One of hello advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="6be7a-288">생성 된 클라이언트 클래스는 API 앱을 호출 하는 보다 쉽게 toowrite 코드를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-288">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="6be7a-289">hello ToDoListAPI 프로젝트에 이미 생성 된 hello 클라이언트 코드 있지만 hello 단계에서 삭제 및 toosee toodo hello 코드 생성 방법을 다시 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-289">hello ToDoListAPI project already has hello generated client code, but in hello following steps you'll delete it and regenerate it toosee how toodo hello code generation.</span></span>

1. <span data-ttu-id="6be7a-290">Visual Studio에서 **솔루션 탐색기**hello ToDoListAPI에서에서 프로젝트를 hello 삭제, *ToDoListDataAPI* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-290">In Visual Studio **Solution Explorer**, in hello ToDoListAPI project, delete hello *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="6be7a-291">**주의: hello ToDoListDataAPI 프로젝트가 아닌 hello 폴더만 삭제 합니다.**</span><span class="sxs-lookup"><span data-stu-id="6be7a-291">**Caution: Delete only hello folder, not hello ToDoListDataAPI project.**</span></span>
   
    ![생성된 클라이언트 코드 삭제](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="6be7a-293">이 폴더는 hello 코드 생성 프로세스를 통해 toogo에 대 한 참여를 사용 하 여 생성 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-293">This folder was created by using hello code generation process that you're about toogo through.</span></span>
2. <span data-ttu-id="6be7a-294">Hello ToDoListAPI 프로젝트를 마우스 오른쪽 단추로 누른 **추가 > REST API 클라이언트**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-294">Right-click hello ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![Visual Studio에서 REST API 클라이언트 추가](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="6be7a-296">Hello에 **REST API 클라이언트 추가** 대화 상자를 클릭 **Swagger URL**, 클릭 하 고 **Azure 자산 선택**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-296">In hello **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Azure 자산 선택](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="6be7a-298">Hello에 **앱 서비스** 대화 상자에서이 자습서에 사용할 hello 리소스 그룹을 확장 하 고 API 앱 선택한 다음 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-298">In hello **App Service** dialog box, expand hello resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![코드 생성을 위한 API 앱 선택](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="6be7a-300">Toohello이 반환 되 면 다음에 유의 **REST API 클라이언트 추가** 대화 상자에서 hello 텍스트 상자가 채워져 hello API 정의 사용 하 여 hello 포털의 앞부분에 표시 된 URL 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-300">Notice that when you return toohello **Add REST API Client** dialog, hello text box has been filled in with hello API definition URL value that you saw earlier in hello portal.</span></span>
   
    ![API 정의 URL](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="6be7a-302">코드 생성에는 다른 방법으로 tooget 메타 데이터에는 찾아보기 대화 상자로 hello 통하지 않고 직접 tooenter hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-302">An alternative way tooget metadata for code generation is tooenter hello URL directly instead of going through hello browse dialog.</span></span> <span data-ttu-id="6be7a-303">또는 tooAzure를 배포 하기 전에 toogenerate 클라이언트 코드를 원하는 경우을 수 있습니다 hello 웹 API 프로젝트를 로컬로 실행, hello 파일을 저장 hello Swagger JSON 파일을 제공 하는 toohello URL 이동 hello를 사용 하 여 **기존Swagger메타데이터파일선택**옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-303">Or if you want toogenerate client code before deploying tooAzure, you could run hello Web API project locally, go toohello URL that provides hello Swagger JSON file, save hello file, and use hello **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="6be7a-304">Hello에 **REST API 클라이언트 추가** 대화 상자를 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-304">In hello **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="6be7a-305">Visual Studio hello API 앱의 이름을 딴 폴더를 만들고 클라이언트 클래스를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-305">Visual Studio creates a folder named after hello API app and generates client classes.</span></span>
   
    ![생성된 클라이언트에 대한 코드 파일](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="6be7a-307">Hello ToDoListAPI 프로젝트를 열고 *Controllers\ToDoListController.cs* hello 생성 된 클라이언트를 사용 하 여 hello API를 호출 하는 40 줄 toosee hello 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-307">In hello ToDoListAPI project, open *Controllers\ToDoListController.cs* toosee hello code at line 40  that calls hello API by using hello generated client.</span></span>
   
    <span data-ttu-id="6be7a-308">호출에 Get 메서드가 hello 및 다음 코드 조각 hello hello 코드 hello 클라이언트 개체를 인스턴스화하고 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-308">hello following snippet shows how hello code instantiates hello client object and calls hello Get method.</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    <span data-ttu-id="6be7a-309">hello 생성자 매개 변수는 hello에서 hello 끝점 URL을 가져옵니다 `toDoListDataAPIURL` 앱 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-309">hello constructor parameter gets hello endpoint URL from  hello `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="6be7a-310">Hello Web.config 파일에서 해당 값은 집합 toohello hello 응용 프로그램을 로컬로 실행할 수 있도록 로컬 IIS Express URL의 hello API 프로젝트입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-310">In hello Web.config file, that value is set toohello local IIS Express URL of hello API project so that you can run hello application locally.</span></span> <span data-ttu-id="6be7a-311">Hello 생성자 매개 변수를 생략 하면 hello 기본 끝점은 hello 코드를 생성 하는 hello URL입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-311">If you omit hello constructor parameter, hello default endpoint is hello URL that you generated hello code from.</span></span>
7. <span data-ttu-id="6be7a-312">클라이언트 클래스를 기반으로 API 앱 이름입니다; 다른 이름으로 생성 됩니다. hello 코드 변경 *Controllers\ToDoListController.cs* hello 형식 이름이 일치 프로젝트에서 생성 된 어떤 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-312">Your client class will be generated with a different name based on your API app name; change hello code in *Controllers\ToDoListController.cs* so that hello type name matches what was generated in your project.</span></span> <span data-ttu-id="6be7a-313">예를 들어 API 앱을 ToDoListDataAPI071316이라고 명명한 경우 이 코드를</span><span class="sxs-lookup"><span data-stu-id="6be7a-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="6be7a-314">toothis:</span><span class="sxs-lookup"><span data-stu-id="6be7a-314">toothis:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a><span data-ttu-id="6be7a-315">API 앱 toohost hello 중간 계층 만들기</span><span class="sxs-lookup"><span data-stu-id="6be7a-315">Create an API app toohost hello middle tier</span></span>
<span data-ttu-id="6be7a-316">앞서 있습니다 [hello 데이터 계층 API 앱을 만들고 코드 tooit 배포한](#createapiapp)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-316">Earlier you [created hello data tier API app and deployed code tooit](#createapiapp).</span></span>  <span data-ttu-id="6be7a-317">Hello를 수행 하는 이제 hello 중간 계층 API 앱에 대해 동일한 절차입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-317">Now you follow hello same procedure for hello middle tier API app.</span></span>

1. <span data-ttu-id="6be7a-318">**솔루션 탐색기**를 마우스 오른쪽 단추로 클릭 hello 중간 계층 ToDoListAPI (하지 hello 데이터 계층 ToDoListDataAPI), 프로젝트 및 클릭 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-318">In **Solution Explorer**, right-click hello middle tier ToDoListAPI  project (not hello data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Visual Studio에서 게시 클릭](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="6be7a-320">Hello에 **프로필** hello 탭 **웹 게시** 마법사를 클릭 하 여 **Microsoft Azure 앱 서비스**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-320">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="6be7a-321">Hello에 **앱 서비스** 대화 상자를 클릭 **새로**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-321">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="6be7a-322">Hello에 **호스팅** hello 탭 **응용 프로그램 서비스 만들기** 대화 상자에서 기본값을 사용한 hello **API 앱 이름** hello에서 고유한 이름을 입력 하거나  *azurewebsites.net* 도메인입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-322">In hello **Hosting** tab of hello **Create App Service** dialog box, accept hello default **API App Name** or enter a name that is unique in hello *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="6be7a-323">Azure hello 선택 **구독** 사용 되 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-323">Choose hello Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="6be7a-324">Hello에 **리소스 그룹** 드롭다운 목록에서 선택 hello 앞에서 만든 동일한 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-324">In hello **Resource Group** drop-down, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="6be7a-325">Hello에 **앱 서비스 계획** 드롭다운 목록에서 선택 hello 앞에서 만든 동일한 계획 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-325">In hello **App Service Plan** drop-down, choose hello same plan you created earlier.</span></span> <span data-ttu-id="6be7a-326">Toothat 값을 기본값이 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-326">It will default toothat value.</span></span>
8. <span data-ttu-id="6be7a-327">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-327">Click **Create**.</span></span>
   
    <span data-ttu-id="6be7a-328">Visual Studio hello API 앱에 대 한 게시 프로필을 만듭니다 만들고를 hello 표시 **연결** hello 단계의 **웹 게시** 마법사.</span><span class="sxs-lookup"><span data-stu-id="6be7a-328">Visual Studio creates hello API app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
9. <span data-ttu-id="6be7a-329">Hello에 **연결** hello 단계의 **웹 게시** 마법사를 클릭 하 여 **게시**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-329">In hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="6be7a-330">Visual Studio는 hello ToDoListAPI 프로젝트 toohello 새 API 앱을 배포 하 고 브라우저 toohello hello API 앱의 URL을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-330">Visual Studio deploys hello ToDoListAPI project toohello new API app and opens a browser toohello URL of hello API app.</span></span> <span data-ttu-id="6be7a-331">"만들었습니다" hello 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-331">hello "successfully created" page appears.</span></span>

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a><span data-ttu-id="6be7a-332">Hello 중간 계층 toocall hello 데이터 계층 구성</span><span class="sxs-lookup"><span data-stu-id="6be7a-332">Configure hello middle tier toocall hello data tier</span></span>
<span data-ttu-id="6be7a-333">이제 hello 중간 계층 API 앱을 호출 하면 toocall hello 데이터 계층 hello Web.config 파일에 여전히 있는 hello localhost URL을 사용 하 여 시도 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-333">If you called hello middle tier API app now, it would try toocall hello data tier using hello localhost URL that is still in hello Web.config file.</span></span> <span data-ttu-id="6be7a-334">이 섹션의 hello 중간 계층 API 앱에는 환경 설정에 hello 데이터 계층 API 앱 URL을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-334">In this section you enter hello data tier API app URL into an environment setting in hello middle tier API app.</span></span> <span data-ttu-id="6be7a-335">Hello hello 중간 계층 API 앱의 코드를 검색 하는 hello 데이터 계층 URL 설정, hello Web.config 파일에 무엇이 hello 환경 설정을 재정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-335">When hello code in hello middle tier API app retrieves hello data tier URL setting, hello environment setting will override what's in hello Web.config file.</span></span>

1. <span data-ttu-id="6be7a-336">Toohello 이동 [Azure 포털](https://portal.azure.com/)를 이동한 후 toohello **API 앱** 블레이드 toohost hello TodoListAPI (중간 계층) 프로젝트를 만든 hello API 앱에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-336">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **API App** blade for hello API app that you created toohost hello TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="6be7a-337">API 앱 hello **설정** 블레이드에서 클릭 **응용 프로그램 설정**합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-337">In hello API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="6be7a-338">API 앱 hello **응용 프로그램 설정** 블레이드에서 toohello 아래로 스크롤하여 **앱 설정** 섹션 및 hello 다음 추가 키와 값입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-338">In hello API App's **Application Settings** blade, scroll down toohello **App settings** section and add hello following key and value.</span></span> <span data-ttu-id="6be7a-339">hello 값 hello 첫 번째 API이이 자습서에는 게시 된 앱의 URL을 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-339">hello value will be hello URL of hello first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="6be7a-340">**키**</span><span class="sxs-lookup"><span data-stu-id="6be7a-340">**Key**</span></span> | <span data-ttu-id="6be7a-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="6be7a-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="6be7a-342">**값**</span><span class="sxs-lookup"><span data-stu-id="6be7a-342">**Value**</span></span> |<span data-ttu-id="6be7a-343">https://{데이터 계층 API 앱 이름}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="6be7a-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="6be7a-344">**예제**</span><span class="sxs-lookup"><span data-stu-id="6be7a-344">**Example**</span></span> |<span data-ttu-id="6be7a-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="6be7a-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="6be7a-346">**Save**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-346">Click **Save**.</span></span>
   
    ![앱 설정에서 저장 클릭](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="6be7a-348">Azure의 hello 코드가 실행 되 면이 값은 이제 hello Web.config 파일에 있는 hello localhost URL을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-348">When hello code runs in Azure, this value will now override hello localhost URL that is in hello Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="6be7a-349">테스트</span><span class="sxs-lookup"><span data-stu-id="6be7a-349">Test</span></span>
1. <span data-ttu-id="6be7a-350">브라우저 창에서 hello 새 중간 계층 위에서 만든 ToDoListAPI에 대 한 API 앱의 toohello URL를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-350">In a browser window, browse toohello URL of hello new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="6be7a-351">Hello 포털에서 API hello 응용 프로그램의 주 블레이드에서 hello URL을 클릭 하 여 있습니다 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-351">You can get there by clicking hello URL in hello API app's main blade in hello portal.</span></span>
2. <span data-ttu-id="6be7a-352">Hello 브라우저의 주소 표시줄에 "swagger" toohello URL을 추가 하 고 enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-352">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="6be7a-353">(URL이 hello `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="6be7a-353">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="6be7a-354">hello 브라우저 표시 hello 했 듯이 ToDoListDataAPI에 대 한 하지만 이제는 동일한 Swagger UI `owner` hello 중간 계층 API 앱 사용자에 대 한 해당 값 toohello 데이터 계층 API 응용 프로그램에서 보내고 있으므로 hello 가져오기 작업에 대 한 필수 필드가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-354">hello browser displays hello same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for hello Get operation, because hello middle tier API app is sending that value toohello data tier API app for you.</span></span> <span data-ttu-id="6be7a-355">(Hello 중간 계층 hello에 대 한 실제 사용자 Id를 송신할 때 인증 자습서 hello 수행, `owner` 매개 변수; 이제 것은 하드 코딩 별표.)</span><span class="sxs-lookup"><span data-stu-id="6be7a-355">(When you do hello authentication tutorials, hello middle tier will send actual user IDs for hello `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="6be7a-356">Get 메서드 hello 및 hello 중간 계층 API 앱 hello 다른 메서드 toovalidate 성공적으로 호출 하는 hello 데이터 계층 응용 프로그램 API 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-356">Try out hello Get method and hello other methods toovalidate that hello middle tier API app is successfully calling hello data tier API app.</span></span>
   
    ![Swagger UI 가져오기 메서드](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="6be7a-358">문제 해결</span><span class="sxs-lookup"><span data-stu-id="6be7a-358">Troubleshooting</span></span>
<span data-ttu-id="6be7a-359">다음은 이 자습서를 수행하는 동안 문제가 발생하는 경우에 사용할 몇 가지 문제 해결 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="6be7a-360">최신 버전의 hello hello를 사용 하는 확인 [Azure SDK for.NET](http://go.microsoft.com/fwlink/?linkid=518003)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-360">Make sure that you're using hello latest version of hello [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="6be7a-361">Hello 프로젝트 이름은 두 가지 비슷한 (ToDoListAPI, ToDoListDataAPI)입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-361">Two of hello project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="6be7a-362">작업은 프로젝트와 작업 하는 hello 지침에 설명 된 대로 표시 되지 않는, hello 올바른 프로젝트를 열면 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-362">If things don't look as described in hello instructions when you are working with a project, make sure you have opened hello correct project.</span></span>
* <span data-ttu-id="6be7a-363">방화벽을 통해 toodeploy tooAzure 앱 서비스 시도 회사 네트워크에는 경우에 포트 443 및 8172 웹 배포에 대 한 열려 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-363">If you're on a corporate network and are trying toodeploy tooAzure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="6be7a-364">이러한 포트를 열 수 없으면 다른 배포 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="6be7a-365">참조 [프로그램 응용 프로그램 tooAzure 앱 서비스 배포](../app-service-web/web-sites-deploy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-365">See [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="6be7a-366">"경로 이름은 고유 해야" 오류 발생-얻을 수 있습니다 이러한 실수로 hello 잘못 된 프로젝트 tooan API 앱을 배포 하 고 올바른 하나의 tooit hello를 나중에 배포 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="6be7a-366">"Route names must be unique" errors -- you could get these if you accidentally deploy hello wrong project tooan API app and then later deploy hello correct one tooit.</span></span> <span data-ttu-id="6be7a-367">toocorrect이를 재배포 hello 올바른 프로젝트 toohello API 앱 및 hello **설정** hello 탭 **웹 게시** 마법사 선택 **대상에서추가파일제거**.</span><span class="sxs-lookup"><span data-stu-id="6be7a-367">toocorrect this, redeploy hello correct project toohello API app, and on hello **Settings** tab of hello **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="6be7a-368">Azure 앱 서비스에서 실행 되는 ASP.NET API 앱을 사용 하는 다음 문제 해결을 간소화 하는 Visual Studio 기능에 대 한 자세한 toolearn을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-368">After you have your ASP.NET API app running in Azure App Service, you may want toolearn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="6be7a-369">로깅, 원격 디버깅 등에 대한 정보는 [Visual Studio에서 Azure App Service 앱 문제 해결](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6be7a-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6be7a-370">다음 단계</span><span class="sxs-lookup"><span data-stu-id="6be7a-370">Next steps</span></span>
<span data-ttu-id="6be7a-371">Toodeploy 기존 웹 API 프로젝트 tooAPI 응용 프로그램, API 앱에 대 한 클라이언트 코드를 생성 하 고.NET 클라이언트에서 API 앱을 사용 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-371">You've seen how toodeploy existing Web API projects tooAPI apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="6be7a-372">이 시리즈의 다음 자습서 hello 너무 방법을 보여 줍니다[JavaScript 클라이언트에서 CORS tooconsume API 앱을 사용 하 여](app-service-api-cors-consume-javascript.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-372">hello next tutorial in this series shows how too[use CORS tooconsume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="6be7a-373">클라이언트 코드 생성에 대 한 자세한 내용은 참조 hello [Azure/AutoRest](https://github.com/azure/autorest) GitHub.com에 리포지토리 합니다. 에 대 한 도움말 hello 생성 된 클라이언트를 사용 하 여 문제를 열고는 [hello AutoRest 리포지토리에 문제](https://github.com/azure/autorest/issues)합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-373">For more information about client code generation, see hello [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com. For help with problems using hello generated client, open an [issue in hello AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="6be7a-374">Hello를 사용 하 여 처음부터 toocreate 새 API 앱 프로젝트를 원하는 경우 **Azure API 앱** 템플릿.</span><span class="sxs-lookup"><span data-stu-id="6be7a-374">If you want toocreate new API app projects from scratch, use hello **Azure API App** template.</span></span>

![Visual Studio에서 API 앱 템플릿](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="6be7a-376">hello **Azure API 앱** 프로젝트 템플릿에 해당 toochoosing hello **빈** ASP.NET 4.5.2 템플릿을 hello 확인란 tooadd 웹 API 지원를 클릭 하 고 hello Swashbuckle NuGet 패키지를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-376">hello **Azure API App** project template is equivalent toochoosing hello **Empty** ASP.NET 4.5.2 template, clicking hello check box tooadd Web API support, and installing hello Swashbuckle NuGet package.</span></span> <span data-ttu-id="6be7a-377">또한 hello 템플릿은 중복 Swagger 작업 Id의 몇 가지 Swashbuckle 구성 코드 설계 tooprevent hello 만들기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-377">In addition, hello template adds some Swashbuckle configuration code designed tooprevent hello creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="6be7a-378">API 앱 프로젝트를 만든 후 배포할 수 있습니다 tooan API 앱 hello 동일한 방식으로이 자습서에서 본 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6be7a-378">Once you've created an API App project, you can deploy it tooan API app hello same way you saw in this tutorial.</span></span>

